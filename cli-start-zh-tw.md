# <a name="getting-started"></a>Spck CLI 入門

## <a name="overview"></a>概述

Spck CLI 是一個命令列工具，透過安全的 WebSocket 連線將本地開發環境連接到 Spck Editor 行動應用程式。啟動後，您可以在手機或平板電腦上瀏覽和編輯本地檔案、執行終端機命令以及預覽本地伺服器。

## <a name="requirements"></a>需求

### 必要

- **Node.js**：18.0.0 或更高版本
- **Spck Editor 帳號**：免費帳號（30 分鐘/天）或 Premium 訂閱（無限制）
- **Spck Editor 行動應用程式**：[Android](https://play.google.com/store/apps/details?id=io.spck) 或 [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### 選用（建議）

- **Git**：2.20.0 以上（用於 Git 整合功能）
- **ripgrep**：15.0.0 以上（檔案搜尋速度顯著提升，提高 100 倍）

## <a name="installation"></a>安裝

### 選項 1：使用 npx 執行（無需安裝）

```bash
npx spck
```

一律使用最新版本，非常適合首次設定或偶爾使用。

### 選項 2：全域安裝

```bash
npm install -g spck
spck
```

啟動更快，支援離線使用，便於日常使用。

## <a name="demo"></a>示範

下方是一段簡短示範，展示如何將 Spck CLI 連接到行動應用程式並遠端編輯本機檔案：

<img src="https://docs.spck.io/assets/gifs/remote-cli-preview.gif" alt="Spck CLI 示範" width="100%" />

## <a name="first-time-setup"></a>首次設定

首次執行 CLI 時，互動式設定精靈將引導您完成以下步驟：

### 1. 身份驗證

```bash
spck
# 按 ENTER 開啟瀏覽器
# 使用 Spck Editor 帳號登入
# 授權 CLI
# 返回終端機
```

憑證儲存在 `~/.spck-editor/.credentials.json` 中，會在工作階段間持久保存。

### 2. 專案設定

精靈將設定：

- **根目錄**：檔案存取的基礎目錄（預設：目前目錄）
- **專案名稱**：在行動應用程式中顯示的名稱（預設：目錄名稱）

### 3. Git 整合（選用）

如果偵測到 `.gitignore` 檔案，CLI 將提示是否新增 `.spck-editor/` 以防止意外提交敏感資訊：

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**建議**：選擇 `Y` 以保護連線憑證。

### 重新執行設定

隨時重新設定：

```bash
spck --setup
```

## <a name="connecting"></a>連線到 Spck Editor

CLI 執行後會顯示 QR 碼和連線詳情。

### 方法 1：QR 碼（建議）

**重要**：掃描 QR 碼**之前**請先安裝 Spck Editor 應用程式。

**在 Android 上：**

1. 使用相機應用程式或快速設定中的 QR 掃描器
2. 偵測到後，點選通知開啟 Spck Editor
3. 應用程式自動連線

> 💡 **注意**：部分 QR 碼掃描器無法處理直接開啟 Spck Editor 的自訂通訊協定。請複製 URL 並貼到 Chrome 中，Chrome 會透過該 URL 啟動 Spck Editor。

**在 iOS 上：**

1. 使用相機應用程式或控制中心中的 QR 掃描器
2. 偵測到後，點選通知開啟 Spck Editor
3. 應用程式自動連線

> 💡 **注意**：Spck Editor **沒有**內建 QR 掃描器。請使用裝置的原生 QR 功能。

### 方法 2：手動輸入

如果 QR 碼無法使用：

1. 開啟 Spck Editor → **專案** → **新增專案** → **連結遠端伺服器**
2. 輸入終端機中顯示的**用戶端 ID** 和**密鑰**
3. 點選**連線**

## <a name="next-steps"></a>後續步驟

1. **了解中繼系統**：了解 CLI 如何路由流量以及如何選擇伺服器——參見 [CLI 參考](./cli)
2. **設定配置**：調整終端機、安全性和檔案系統設定——參見[設定](./cli-config)
3. **探索進階功能**：CLI 命令、AI 程式設計代理、多專案管理——參見[進階用法](./cli-advanced)
4. **在裝置間傳輸檔案**：無線複製手機和桌面之間的專案——參見[檔案傳輸](./cli-file-transfer)
5. **保持工作階段活躍**：使用 tmux 在裝置間共享工作階段——參見[使用 Tmux](./tmux)
