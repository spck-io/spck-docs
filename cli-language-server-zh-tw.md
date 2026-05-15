# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>概述

Spck CLI 包含一個完整的 Language Server Protocol (LSP) 橋接器，可直接在您的遠端主機上執行 TypeScript、JavaScript、Python、HTML、CSS 和 SCSS 語言伺服器。連線到 CLI 工作階段後，Spck Editor 會自動使用遠端語言伺服器，而不是內建的行動端語言伺服器。

> 💡 **提示**：有關無需 CLI 即可使用的內建語言伺服器的說明，請參閱[編輯器 Language Server](./editor-language-server)。

## <a name="cli-ls-architecture"></a>架構

CLI 語言伺服器與您的專案檔案執行在同一台機器上。與行動端採用的瀏覽器內方案相比，這具有幾項顯著優勢：

### 無需檔案傳輸

使用內建行動端語言伺服器時，檔案必須先傳輸到裝置並載入瀏覽器 Worker 中，語言伺服器才能對其進行分析。使用 CLI 時，語言伺服器直接從磁碟讀取檔案，無需傳輸。這消除了頻寬開銷，即使在大型專案中也能保持快速分析。

### 完整的專案感知

CLI 語言伺服器可存取您整個專案目錄，包括：

- 每個子目錄中的所有原始檔
- 用於第三方型別解析的 `node_modules/`
- 在任意深度自動探索的 `tsconfig.json` 檔案
- `.js`、`.ts`、`.d.ts`、`.jsx`、`.tsx`、`.vue` 及相關宣告檔案

這表示跳轉到定義、尋找參考和重新命名符號可以正確地跨檔案邊界運作——即使您尚未在編輯器中開啟這些檔案。

### 正確處理 `tsconfig.json`

TypeScript 語言伺服器會自動探索並遵守您專案的 `tsconfig.json`（或 `jsconfig.json`）。路徑別名（`paths`）、編譯器選項（`strict`、`target`、`lib`）、專案參考和 monorepo 工作區佈局均能正確處理。內建行動端語言伺服器無法讀取 `tsconfig.json`，因為它在啟動時沒有檔案系統存取權限。

### 持久化程序

語言伺服器程序在整個 CLI 工作階段期間保持執行。它會建立專案的記憶體索引，並在編輯之間保持其活躍，因此即使初始啟動之後，回應速度仍然很快。

## <a name="cli-ls-features"></a>支援的功能

| 功能 | 說明 |
| --- | --- |
| **程式碼補全** | 按相關性排序的上下文感知建議，包含型別簽章 |
| **懸停資訊** | 游標下符號的型別資訊和 JSDoc 文件 |
| **簽章說明** | 輸入函式呼叫時的參數提示和文件 |
| **跳轉到定義** | 跳轉到任意符號的宣告，包括 `node_modules` 中的符號 |
| **尋找參考** | 列出整個專案中符號的每一處用法 |
| **重新命名符號** | 重新命名符號並以原子方式更新所有參考 |
| **診斷** | 輸入時即時顯示錯誤和警告醒目提示 |
| **Markdown 渲染** | 懸停和簽章文件以 Markdown 格式渲染，程式碼區塊帶語法醒目提示 |

## <a name="cli-ls-languages"></a>支援的語言

| 語言 | 補全 | 懸停 | 簽章 | 診斷 |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>設定

語言伺服器支援預設為啟用。您可以在設定檔中進行控制：

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

- **`languageServer.enabled`** (boolean)：所有遠端語言伺服器的主開關。預設值：`true`。
- **`languageServer.typescript.enabled`** (boolean)：啟用 TypeScript/JavaScript 語言伺服器。預設值：`true`。
- **`languageServer.python.enabled`** (boolean)：啟用 Python 語言伺服器（需要 `PATH` 中存在 `pylsp`）。預設值：`true`。

## <a name="cli-ls-requirements"></a>系統需求

- **TypeScript / JavaScript**：隨 CLI 一起提供，無需額外安裝。
- **Python**：需要 [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server)（`pip install python-lsp-server`）。
- **HTML / CSS / SCSS**：隨 CLI 一起提供，無需額外安裝。

## <a name="cli-ls-vs-mobile"></a>CLI 與行動端語言伺服器比較

| 功能 | CLI Language Server | 行動端內建 |
| --- | --- | --- |
| 完整專案檔案存取 | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| `node_modules` 型別解析 | ✓ | — |
| 跨檔案跳轉到定義 | ✓ | 受限 |
| 跨檔案尋找參考 | ✓ | — |
| 重新命名符號 | ✓ | — |
| Python 支援 | ✓ | — |
| 離線工作（無 CLI） | — | ✓ |

&nbsp;

&nbsp;
