# <a name="cli-advanced-usage"></a>CLI 進階用法

## <a name="cli-commands"></a>CLI 命令

### 基本命令

```bash
# 啟動 CLI
spck

# 執行設定精靈
spck --setup

# 顯示帳號資訊
spck --account

# 登出並清除憑證
spck --logout

# 顯示說明
spck --help

# 顯示版本
spck --version
```

### 進階選項

```bash
# 使用自訂設定檔
spck --config /path/to/config.json
spck -c /path/to/config.json

# 覆蓋根目錄
spck --root /path/to/project
spck -r /path/to/project

# 覆蓋中繼伺服器（例如使用特定區域）
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>AI 程式設計代理

Spck CLI 終端機提供完整的 shell 存取權限，這意味著您可以直接從行動裝置執行 AI 程式設計代理。這些代理可以在您透過 Spck Editor 監督的同時讀取、寫入和重構專案程式碼。

> 💡 **提示**：使用 **tmux** 可以讓 AI 代理工作階段在斷線後繼續執行。在桌面啟動 tmux 工作階段（`tmux new -s code`），啟動 AI 代理，然後從手機上的 Spck CLI 終端機重新連線（`tmux attach -t code`）。這樣您就可以在桌面和行動裝置之間無縫切換而不遺失上下文。包含持久遠端伺服器設定的完整指南，請參見[使用 Tmux](./tmux)。

## <a name="advanced-usage"></a>進階用法

### 多個專案

同時為不同專案執行獨立的 CLI 執行個體：

```bash
# 終端機 1：專案 A
cd /path/to/projectA
spck

# 終端機 2：專案 B
cd /path/to/projectB
spck
```

每個專案維護各自的設定和連線。

> 💡 **提示**：您還可以使用多個 CLI 執行個體在桌面和手機之間傳輸檔案。請參見[行動裝置與桌面之間的檔案傳輸](./cli-file-transfer)獲取逐步指南。

### 自訂設定檔

為不同情境建立專用設定：

```bash
# 開發設定
spck --config ~/configs/dev-config.json

# 生產設定（唯讀，無終端機）
spck --config ~/configs/prod-config.json
```

### 特定環境設定

**本地開發：**

```json
{
  "security": {
    "userAuthenticationEnabled": false
  },
  "terminal": {
    "enabled": true
  }
}
```

**生產伺服器：**

```json
{
  "security": {
    "userAuthenticationEnabled": true
  },
  "terminal": {
    "enabled": false
  }
}
```

### CPU 使用率偏高

透過新增更多忽略模式來減少檔案監控：

```json
{
  "filesystem": {
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/dist/**",
      "**/build/**",
      "**/.next/**",
      "**/coverage/**",
      "**/.cache/**"
    ]
  }
}
```

限制並行終端機數量：

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>為行動裝置縮短 Shell 提示符號

在行動裝置上，水平螢幕空間有限。預設的 shell 提示符號（通常包含目前目錄路徑、使用者名稱和主機名稱）會占用終端機空間，使命令輸出更難閱讀。

將提示符號改為簡單的 `$ ` 可以在小螢幕上獲得更清爽的終端機體驗。

### Bash

在 `~/.bashrc` 中新增以下內容：

```bash
export PS1='\$ '
```

無需重新啟動 shell 即可套用：

```bash
source ~/.bashrc
```

### Zsh

在 `~/.zshrc` 中新增以下內容：

```zsh
PROMPT='$ '
```

無需重新啟動 shell 即可套用：

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

如果設定檔不存在，請先建立，然後開啟：

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

在設定檔中新增以下內容：

```powershell
function prompt { "$ " }
```

無需重新啟動 shell 即可套用：

```powershell
. $PROFILE
```

### 命令提示字元 (Windows)

為目前工作階段設定最簡提示符號：

```cmd
PROMPT $$
```

若要使其永久生效，請透過**控制台 → 系統 → 進階系統設定 → 環境變數**，將 `PROMPT` 新增為值為 `$$` 的**使用者**或**系統**環境變數。
