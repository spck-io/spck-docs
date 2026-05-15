# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>Overview

The Spck CLI includes a full Language Server Protocol (LSP) bridge that runs TypeScript, JavaScript, Python, HTML, CSS, and SCSS language servers directly on your remote host. When connected to a CLI session, Spck Editor automatically uses the remote language server instead of the built-in mobile one.

> 💡 **Tip**: For a description of the built-in language server available without the CLI, see [Editor Language Server](./editor-language-server).

## <a name="cli-ls-architecture"></a>Architecture

The CLI language server runs on the same machine as your project files. This has several significant advantages over the in-browser approach used on mobile:

### No File Transmission

With the built-in mobile language server, files must be transmitted to the device and loaded into a browser worker before the language server can analyze them. With the CLI, the language server reads files directly from disk — no transmission required. This eliminates bandwidth overhead and keeps analysis fast even in large projects.

### Full Project Awareness

The CLI language server has access to your entire project directory, including:

- All source files across every subdirectory
- `node_modules/` for third-party type resolution
- Automatically discovered `tsconfig.json` files at any depth
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` and associated declaration files

This means go-to-definition, find references, and rename symbol work correctly across file boundaries — even when you have not opened those files in the editor.

### Proper `tsconfig.json` Handling

The TypeScript language server discovers and respects your project's `tsconfig.json` (or `jsconfig.json`) automatically. Path aliases (`paths`), compiler options (`strict`, `target`, `lib`), project references, and monorepo workspace layouts are all handled correctly. The mobile built-in language server cannot read `tsconfig.json` because it does not have access to the file system at startup.

### Persistent Process

The language server process stays alive for the duration of your CLI session. It builds an in-memory index of your project and keeps it warm between edits, so responses remain fast even after the initial startup.

## <a name="cli-ls-features"></a>Supported Features

| Feature                | Description                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------ |
| **Code Completion**    | Context-aware suggestions with type signatures, sorted by relevance                        |
| **Hover Info**         | Type information and JSDoc documentation for the symbol under the cursor                   |
| **Signature Help**     | Parameter hints and documentation while typing a function call                             |
| **Go to Definition**   | Jump to the declaration of any symbol, including those in `node_modules`                   |
| **Find References**    | List every usage of a symbol across the whole project                                      |
| **Rename Symbol**      | Rename a symbol and update all references atomically                                       |
| **Diagnostics**        | Real-time error and warning highlights as you type                                         |
| **Markdown Rendering** | Hover and signature documentation rendered as Markdown with syntax-highlighted code blocks |

## <a name="cli-ls-languages"></a>Supported Languages

| Language          | Completions | Hover | Signatures | Diagnostics |
| ----------------- | ----------- | ----- | ---------- | ----------- |
| TypeScript / TSX  | ✓           | ✓     | ✓          | ✓           |
| JavaScript / JSX  | ✓           | ✓     | ✓          | ✓           |
| Python            | ✓           | ✓     | ✓          | ✓           |
| HTML              | ✓           | ✓     | —          | ✓           |
| CSS / SCSS / Less | ✓           | ✓     | —          | ✓           |

## <a name="cli-ls-config"></a>Configuration

Language server support is enabled by default. You can control it in your configuration file:

```json
{
  "languageServer": {
    "enabled": true,
    "typescript": {
      "enabled": true
    },
    "python": {
      "enabled": true
    }
  }
}
```

- **`languageServer.enabled`** (boolean): Master switch for all remote language servers. Default: `true`.
- **`languageServer.typescript.enabled`** (boolean): Enable TypeScript/JavaScript language server. Default: `true`.
- **`languageServer.python.enabled`** (boolean): Enable Python language server (powered by bundled Pyright). Default: `true`.

## <a name="cli-ls-requirements"></a>Requirements

- **TypeScript / JavaScript**: Bundled with the CLI. No additional installation required.
- **Python**: Bundled with the CLI via Pyright — no additional installation required.
- **HTML / CSS / SCSS**: Bundled with the CLI. No additional installation required.

## <a name="cli-ls-vs-mobile"></a>CLI vs Mobile Language Server

| Capability                        | CLI Language Server | Mobile Built-in |
| --------------------------------- | ------------------- | --------------- |
| Full project file access          | ✓                   | —               |
| `tsconfig.json` / `jsconfig.json` | ✓                   | —               |
| `node_modules` type resolution    | ✓                   | —               |
| Cross-file go to definition       | ✓                   | Limited         |
| Cross-file find references        | ✓                   | —               |
| Rename symbol                     | ✓                   | —               |
| Works offline (no CLI)            | —                   | ✓               |

&nbsp;

&nbsp;
