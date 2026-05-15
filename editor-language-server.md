# <a name="editor-language-server"></a>Editor Language Server

## <a name="editor-ls-overview"></a>Overview

Spck Editor includes a built-in language server that runs entirely in the browser without any server connection. It provides code completions, hover information, and real-time diagnostics for the files you are currently editing.

> 💡 **Tip**: When connected to a Spck CLI session, the editor automatically switches to the remote language server, which has full project awareness and supports more languages. See [CLI Language Server](./cli-language-server) for details.

## <a name="editor-ls-how-it-works"></a>How It Works

The built-in language server runs as a Web Worker inside the browser. When you open a file, its content is transferred to the worker where the language service analyzes it and returns completions, types, and errors. Because the worker runs in the browser, it only has access to files that have been opened in the current session.

## <a name="editor-ls-features"></a>Features

| Feature             | Description                                                        |
| ------------------- | ------------------------------------------------------------------ |
| **Code Completion** | Suggestions based on the current file's content                    |
| **Hover Info**      | Type information and documentation for the symbol under the cursor |
| **Signature Help**  | Parameter hints while typing a function call                       |
| **Diagnostics**     | Syntax and type errors highlighted in real time                    |

## <a name="editor-ls-languages"></a>Supported Languages

| Language         | Completions | Hover | Signatures | Diagnostics |
| ---------------- | ----------- | ----- | ---------- | ----------- |
| TypeScript / TSX | ✓           | ✓     | ✓          | ✓           |
| JavaScript / JSX | ✓           | ✓     | ✓          | ✓           |
| HTML             | ✓           | —     | —          | ✓           |
| CSS / SCSS       | ✓           | ✓     | —          | ✓           |

## <a name="editor-ls-limitations"></a>Limitations

The built-in language server has several limitations compared to the [CLI Language Server](./cli-language-server):

- **Single-file analysis only**: The worker can only analyze files that have been opened in the editor. Symbols defined in other files in your project are not resolved unless those files are also open.
- **No `tsconfig.json`**: Compiler options and path aliases defined in `tsconfig.json` or `jsconfig.json` are not applied because the language server does not have file system access at startup.
- **No `node_modules` resolution**: Third-party library types are not available unless you manually include the declaration files in your project.
- **No cross-file navigation**: Go to definition and find references only work within the currently open file.
- **No rename symbol**: Renaming across multiple files requires full project access.

## <a name="editor-ls-cli-upgrade"></a>Upgrading to the CLI Language Server

Connect to a [Spck CLI](./cli-language-server) session to unlock full project-wide language intelligence:

- Complete cross-file type resolution including `node_modules`
- Automatic `tsconfig.json` discovery and path alias support
- Go to definition and find references across the entire project
- Rename symbol with atomic multi-file updates
- Python language support

&nbsp;

&nbsp;
