# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>概述

Spck CLI 包含一个完整的 Language Server Protocol (LSP) 桥接器，可直接在您的远程主机上运行 TypeScript、JavaScript、Python、HTML、CSS 和 SCSS 语言服务器。连接到 CLI 会话后，Spck Editor 会自动使用远程语言服务器，而不是内置的移动端语言服务器。

> 💡 **提示**：有关无需 CLI 即可使用的内置语言服务器的说明，请参阅[编辑器 Language Server](./editor-language-server)。

## <a name="cli-ls-architecture"></a>架构

CLI 语言服务器与您的项目文件运行在同一台机器上。与移动端采用的浏览器内方案相比，这具有几项显著优势：

### 无需文件传输

使用内置移动端语言服务器时，文件必须先传输到设备并加载到浏览器 Worker 中，语言服务器才能对其进行分析。使用 CLI 时，语言服务器直接从磁盘读取文件，无需传输。这消除了带宽开销，即使在大型项目中也能保持快速分析。

### 完整的项目感知

CLI 语言服务器可访问您整个项目目录，包括：

- 每个子目录中的所有源文件
- 用于第三方类型解析的 `node_modules/`
- 在任意深度自动发现的 `tsconfig.json` 文件
- `.js`、`.ts`、`.d.ts`、`.jsx`、`.tsx`、`.vue` 及相关声明文件

这意味着跳转到定义、查找引用和重命名符号可以正确地跨文件边界工作——即使您尚未在编辑器中打开这些文件。

### 正确处理 `tsconfig.json`

TypeScript 语言服务器会自动发现并遵守您项目的 `tsconfig.json`（或 `jsconfig.json`）。路径别名（`paths`）、编译器选项（`strict`、`target`、`lib`）、项目引用和 monorepo 工作区布局均能正确处理。内置移动端语言服务器无法读取 `tsconfig.json`，因为它在启动时没有文件系统访问权限。

### 持久化进程

语言服务器进程在整个 CLI 会话期间保持运行。它会构建项目的内存索引，并在编辑之间保持其活跃，因此即使初始启动之后，响应速度仍然很快。

## <a name="cli-ls-features"></a>支持的功能

| 功能 | 说明 |
| --- | --- |
| **代码补全** | 按相关性排序的上下文感知建议，包含类型签名 |
| **悬停信息** | 光标下符号的类型信息和 JSDoc 文档 |
| **签名帮助** | 输入函数调用时的参数提示和文档 |
| **跳转到定义** | 跳转到任意符号的声明，包括 `node_modules` 中的符号 |
| **查找引用** | 列出项目中符号的每一处用法 |
| **重命名符号** | 重命名符号并原子性地更新所有引用 |
| **诊断** | 键入时实时显示错误和警告高亮 |
| **Markdown 渲染** | 悬停和签名文档以 Markdown 格式渲染，代码块带语法高亮 |

## <a name="cli-ls-languages"></a>支持的语言

| 语言 | 补全 | 悬停 | 签名 | 诊断 |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>配置

语言服务器支持默认启用。您可以在配置文件中进行控制：

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

- **`languageServer.enabled`** (boolean)：所有远程语言服务器的主开关。默认值：`true`。
- **`languageServer.typescript.enabled`** (boolean)：启用 TypeScript/JavaScript 语言服务器。默认值：`true`。
- **`languageServer.python.enabled`** (boolean)：启用 Python 语言服务器（需要 `PATH` 中存在 `pylsp`）。默认值：`true`。

## <a name="cli-ls-requirements"></a>系统要求

- **TypeScript / JavaScript**：随 CLI 一起提供，无需额外安装。
- **Python**：需要 [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server)（`pip install python-lsp-server`）。
- **HTML / CSS / SCSS**：随 CLI 一起提供，无需额外安装。

## <a name="cli-ls-vs-mobile"></a>CLI 与移动端语言服务器对比

| 功能 | CLI Language Server | 移动端内置 |
| --- | --- | --- |
| 完整项目文件访问 | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| `node_modules` 类型解析 | ✓ | — |
| 跨文件跳转到定义 | ✓ | 受限 |
| 跨文件查找引用 | ✓ | — |
| 重命名符号 | ✓ | — |
| Python 支持 | ✓ | — |
| 离线工作（无 CLI） | — | ✓ |

&nbsp;

&nbsp;
