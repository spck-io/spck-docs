# Embedding the Editor

Embed Spck Editor in an iframe to create editable examples, tutorials, or tools that work with code. The `SpckEditor` wrapper communicates with the iframe through `postMessage` and `MessageChannel`; your page does not need access to the iframe's DOM.

The wrapper source, generated scripts, and TypeScript declarations are in [spckio/spck-embed](https://github.com/spckio/spck-embed). This guide describes the updated editor and wrapper APIs. Use matching builds: older releases such as `spck-embed@0.2.0` contain event, promise, and declaration bugs addressed in the current source.

## Quick Start

This complete page creates an editor, sets its text, and displays subsequent edits. Serve it from a web origin, then open it in a browser.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Spck Editor example</title>
</head>
<body>
  <iframe
    id="editor"
    title="JavaScript editor"
    src="https://embed.spck.io/?theme=dracula"
    style="width:100%;height:420px;border:0"
  ></iframe>
  <p id="status">Connecting…</p>
  <pre id="output"></pre>

  <script src="https://embed.spck.io/embed/spck-embed.min.js"></script>
  <script>
    const editor = new SpckEditor('#editor');
    const output = document.getElementById('output');
    const status = document.getElementById('status');

    editor.on({
      textChange: (text) => { output.textContent = text; }
    });

    async function initialize() {
      await editor.connect();
      await editor.send({
        editor: {
          mode: 'javascript',
          text: 'console.log("Hello from Spck!");',
          fontSize: '14px',
          tabSize: 2,
          gutter: true
        }
      });
      output.textContent = await editor.getText();
      status.textContent = 'Ready';
    }

    initialize().catch((error) => {
      status.textContent = error.message || String(error);
    });
  </script>
</body>
</html>
```

Register handlers before connecting if you need events from the initial configuration. Await `connect()` before issuing requests, and await `send()` when another operation depends on its results. Both methods use promises; callback-style overloads are not supported.

## Loading the Wrapper

For a plain HTML page, load the hosted script as shown above. It defines the global `SpckEditor` constructor.

For a bundled application, install a checkout of the wrapper repository:

```sh
git clone https://github.com/spckio/spck-embed.git
npm install ./spck-embed
```

Then use its named export in code that runs in the browser:

```javascript
import { SpckEditor } from 'spck-embed';

const editor = new SpckEditor('#editor');
await editor.connect();
```

CommonJS bundlers can use `const { SpckEditor } = require('spck-embed')`. The package also includes TypeScript declarations. A selector must resolve to an existing iframe element; an iframe element can be passed directly instead.

## Iframe URL Options

| Parameter | Behavior |
| --- | --- |
| `files` | Shows the file menu when present, unless its value is `0`. Hidden when omitted. |
| `preview` | Enables the Run/preview controls when present, unless its value is `0`. Hidden when omitted. |
| `touch` | Enables touch mode only when its value is `1`. |
| `theme` | Selects the initial theme. |
| `project` | Sets the initial project name; defaults to `main`. |
| `config_url` | Loads an initial configuration from a JSON URL. See [Initial Configuration](#initial-configuration). |

Supported URL themes are `chrome`, `xcode`, `ayu-light`, `dracula`, `monokai`, `ayu-mirage`, `one-light`, `one-dark`, and `github-dark`.

```html
<iframe
  id="editor"
  title="Web project editor"
  src="https://embed.spck.io/?files=1&amp;preview=1&amp;touch=1&amp;theme=one-dark"
  style="width:100%;height:600px;border:0"
></iframe>
```

Use `files=0&preview=0` to explicitly hide both features. URL options are read when the iframe loads; configure editor text and appearance with `send()` after connecting.

## Connection and Custom Origins

`new SpckEditor(iframeOrSelector, origin?)` defaults to the editor origin `https://embed.spck.io`. When hosting the editor yourself, pass the iframe's origin, including its scheme and port, without a URL path:

```javascript
const iframe = document.getElementById('editor');
iframe.src = 'http://localhost:8123/?files=1';
const editor = new SpckEditor(iframe, 'http://localhost:8123');

const { tries } = await editor.connect({ maxTries: 40, interval: 250 });
console.log(`Connected after ${tries} attempt(s)`);
```

The iframe must serve an embedded editor build. The second constructor argument identifies the **editor's** origin; project storage is scoped separately by the **parent page's** origin.

`connect()` defaults to 20 attempts, 500 milliseconds apart. It resolves with `{ tries }` after the editor is initialized and the initial configuration is applied. It rejects if connection attempts fail or initialization fails. If you navigate or replace the iframe, create a wrapper for the new iframe and connect again.

## Projects and Files

All properties in `send()` are optional. Its promise resolves with `{ success: true }` after the requested operations complete, or rejects with an `Error` when processing fails. A message can create a project, write files, open tabs, and configure the editor together.

| Property | Type | Meaning |
| --- | --- | --- |
| `project` | `string` | Creates or opens this project. With `appendFiles` omitted or `false`, replaces its existing files. |
| `appendFiles` | `boolean` | With a named project, `true` preserves existing files and writes or overwrites only the supplied paths. |
| `files` | `{ path, text?, url? }[]` | Writes files in the current or named project, creating parent folders as needed. |
| `open` | `string` or `string[]` | Opens a project-relative file, or sets the tab list and activates the first file in the array. An empty array leaves tabs unchanged. |
| `clearProjects` | `boolean` or `string[]` | `true` clears this parent origin's projects; an array deletes only the named projects. |
| `editor` | `object` | Updates the active editor buffer and settings. See [Editor Settings](#editor-settings). |

### Create a Web Project

With `files=1&preview=1` in the iframe URL, this example supplies an HTML entry page, CSS, and JavaScript. Use the editor's Run control to preview the project.

```javascript
await editor.send({
  project: 'web-demo',
  files: [
    {
      path: 'index.html',
      text: '<!doctype html><html><head><link rel="stylesheet" href="style.css"></head><body><h1 id="greeting"></h1><script src="index.js"></script></body></html>'
    },
    { path: 'style.css', text: 'body { font-family: sans-serif; padding: 2rem; }' },
    { path: 'index.js', text: 'document.getElementById("greeting").textContent = "Hello!";' }
  ],
  open: ['index.html', 'index.js', 'style.css']
});
```

The HTML string above belongs in a JavaScript module or external script file. If placing it inside an HTML `<script>` element, escape the embedded closing tag as `<\/script>` so the browser does not end the outer script early.

### Update Files Without Replacing the Project

```javascript
await editor.send({
  project: 'web-demo',
  appendFiles: true,
  files: [{ path: 'src/helpers.js', text: 'export const double = n => n * 2;' }],
  open: 'src/helpers.js'
});

// Open another existing file without writing files or replacing the project.
await editor.send({ open: 'index.js' });
```

When `project` is omitted, file writes use the active project and do not replace it. If there is no active project for this parent origin, the editor creates `main` for file/open requests. Supplying a project name with no files and without `appendFiles: true` still replaces that project, so use `appendFiles: true` to reopen a project you want to retain.

### Load a File from a URL

```javascript
await editor.send({
  project: 'remote-example',
  files: [{ path: 'example.js', url: 'https://example.com/examples/example.js' }],
  open: 'example.js'
});
```

The editor iframe fetches the URL. The response must permit access from the editor's origin through CORS when it is cross-origin. If both `url` and `text` are provided, the fetched contents take precedence.

### Storage and Paths

Projects are stored in the editor's browser filesystem under a root for each parent origin, including its scheme and port. Different origins do not overwrite each other's same-named projects. Embeds on the same parent origin share this storage, so use distinct project names for independent examples. Browser storage settings determine whether data persists across visits.

`files[].path` and `open` are project-relative inputs, such as `src/index.js`. Absolute paths, URL schemes, backslashes, and `..` path segments are rejected. Events and `get('currentFile')` return full internal paths instead. Treat those paths as identifiers; convert them to project-relative paths before sending them back as inputs.

The updated implementation uses new per-origin roots. Projects created by older builds in the shared root are not automatically migrated.

### Clear Projects

```javascript
// Delete only these projects for the current parent origin.
await editor.send({ clearProjects: ['web-demo', 'remote-example'] });

// Clear every project for this parent origin.
await editor.send({ clearProjects: true });
```

These operations delete stored project files. Neither form deletes another parent origin's projects.

## Editor Settings

```javascript
await editor.send({
  editor: {
    mode: 'javascript',
    text: 'const answer = 42;\nconsole.log(answer);',
    fontSize: '16px',
    tabSize: 2,
    gutter: false,
    theme: 'dracula',
    position: { row: 1, column: 0 }
  }
});
```

| Setting | Type | Meaning |
| --- | --- | --- |
| `mode` | `string` | Ace language mode, such as `javascript`, `typescript`, `html`, `css`, `json`, or `markdown`. |
| `text` | `string` | Replaces the active buffer; `''` clears it. This does not write a project file or emit `textChange`. Use `files` to write stored file contents. |
| `fontSize` | `string` | Font size, such as `14px`. |
| `tabSize` | `number` | Positive indentation size, such as `2` or `4`. |
| `gutter` | `boolean` | Shows or hides line numbers; `false` is supported. |
| `theme` | `string` | Changes the editor theme. |
| `position` | `{ row, column }` | Moves the cursor and scrolls to that row. Both coordinates are zero-based. |

Settings apply after file creation and opening. If a message includes both `open` and `editor.text`, the text replacement affects the newly opened buffer. Read it explicitly with `getText()` if your host UI needs the result of a programmatic text update.

## Read Editor State

| Method | Resolved value |
| --- | --- |
| `getText()` | Active buffer text. |
| `getMode()` | Language mode name. |
| `getTheme()` | Theme name. |
| `getTabSize()` | Tab size number. |
| `getPosition()` | `{ row, column }`, using zero-based coordinates. |
| `get('currentFile')` | Full internal path of the active file, or no path for a blank session. |

```javascript
const [text, position, path] = await Promise.all([
  editor.getText(),
  editor.getPosition(),
  editor.get('currentFile')
]);
console.log({ text, position, path });
```

The generic `get()` also accepts `text`, `mode`, `theme`, `tabSize`, and `position`. Unsupported property names reject with an error.

## Subscribe to Events

Pass only the handlers you need to `on()`. Each new handler replaces the previous handler for the same event; handlers for other events stay registered.

| Event | Callback arguments |
| --- | --- |
| `textChange` | `(text, path)`; the full active buffer and its full internal path, or `null` for a blank session. |
| `positionChange` | `({ row, column })`. |
| `selectionChange` | `({ selectedText, selectionRanges })`; each range has `start` and `end` positions. |
| `fileOpen` | `(path)`; a full internal path string, rather than a file object. |
| `projectOpen` | `(project)`; a project object with a `dir` property, rather than a project-name string. |
| `projectClose` | No arguments. |
| `focus` | No arguments. |
| `blur` | No arguments. |

This example converts a file event into a relative path and displays selected text. Register it before `connect()` to capture startup events too.

```javascript
let projectDir = '';

editor.on({
  projectOpen: (project) => { projectDir = project.dir; },
  projectClose: () => { projectDir = ''; },
  fileOpen: (path) => {
    const prefix = projectDir + '/';
    const relativePath = projectDir && path.startsWith(prefix)
      ? path.slice(prefix.length)
      : path;
    console.log('Opened:', relativePath);
  },
  positionChange: ({ row, column }) => {
    console.log(`Line ${row + 1}, column ${column + 1}`);
  },
  selectionChange: ({ selectedText, selectionRanges }) => {
    console.log('Selection:', selectedText, selectionRanges);
  }
});
```

`textChange` reports interactive edits, not a file-save acknowledgement. A handler runs synchronously on the host when its message arrives; debounce expensive host-side work such as sending edits to your server.

## Initial Configuration

Use `config_url` to load a JSON message during connection, instead of sending the initial project from your host JavaScript. The JSON accepts the same properties as `send()`:

```json
{
  "project": "configured-demo",
  "appendFiles": true,
  "files": [
    { "path": "index.js", "text": "console.log('Configured demo');" }
  ],
  "open": "index.js",
  "editor": { "fontSize": "14px", "tabSize": 2 }
}
```

Construct the iframe URL with `URLSearchParams` so the configuration URL is encoded correctly:

```javascript
const url = new URL('https://embed.spck.io/');
url.searchParams.set('files', '1');
url.searchParams.set('config_url', 'https://example.com/embed-config.json');

const iframe = document.getElementById('editor');
iframe.src = url.href;
const editor = new SpckEditor(iframe);
await editor.connect();
```

The JSON URL must be readable by the editor iframe, including any required CORS permission. Its `project` takes precedence over the iframe's `project` query parameter. If neither supplies a name, the initial project is `main`. Initial configuration defaults to preserving existing files (`appendFiles: true`); set `appendFiles: false` explicitly for a fresh project on load. By contrast, a later `send({ project: ... })` defaults to replacement.

## Troubleshooting

- **Connection fails:** check that the iframe loaded an embed build, that the constructor origin exactly matches its origin, and that the browser supports `MessageChannel`. Allow more attempts if loading takes longer than the default retry window.
- **Awaiting `send()` hangs or event arguments are missing:** use the updated iframe and wrapper together. Older builds do not acknowledge configuration requests and send incompatible event payloads.
- **Files disappear after opening a project:** include `appendFiles: true` when sending an existing project name.
- **Opening a file fails:** use its project-relative path, including folders, and await the request that creates it first.
- **Remote files or configuration fail to load:** verify the URL and CORS permissions from the iframe's origin, rather than only from your host page.
- **Setting text does not update the host preview:** `editor.text` is silent; update your host UI from `await editor.getText()` after `send()` resolves.
