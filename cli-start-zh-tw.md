# <a name="getting-started"></a>Spck CLI 入門

## <a name="overview"></a>概述

Spck CLI 已正式發布。將電腦連接到手機或平板上的 Spck Editor，即可編輯檔案、使用 Git 和終端機，以及預覽本機伺服器。連線使用加密中繼，或 [Fast Lane](./cli#fast-lane) 點對點直連（Supporter 與 Gold）。

## <a name="requirements"></a>需求

Lite 支援透過 Spck CLI 編輯桌上型電腦或公用虛擬機上的專案。遠端專案需要 **Spck 帳戶和有效的 Spck 訂閱**，不包含在 Lite 的一次性購買中。訂閱有助於負擔 Spck 伺服器持續產生的託管、運作和維護費用。隨 Lite 提供的本機編輯和 Git 工具仍可無需訂閱使用。

### 必要

- **Node.js**：**22.22.2+ (22.x), 24.15.0+ (24.x), 或 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Spck Editor 帳號**：免費帳號（30 分鐘/天）或 Premium 訂閱（無限制）
- **Spck Editor 行動應用程式**：[Android](https://play.google.com/store/apps/details?id=io.spck) 或 [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### 選用（建議）

- **Git**：遠端專案的 [Git 整合](./git-support#git-limitations-cli)需要 2.20.0 或更新版本
- **ripgrep**：15.0.0 以上（檔案搜尋速度顯著提升，提高 100 倍）

## <a name="installation"></a>安裝

### 選項 1：使用 npx 執行（無需安裝）

```bash
npx spck@latest
```

要求最新的 CLI 版本，適合首次設定或偶爾使用。`npx spck` 可能重複使用已安裝的版本。

### 選項 2：全域安裝

```bash
npm install -g spck
spck
```

安裝一次後，日常直接執行 `spck`。使用 `npm install -g spck@latest` 更新。遠端連線仍需要網際網路。

## <a name="demo"></a>示範

[觀看 Spck CLI 宣傳影片](https://youtu.be/EtfEhd5EmKM)，瞭解新的 Fast Lane 功能。

下方是一段簡短示範，展示如何將 Spck CLI 連接到行動應用程式並遠端編輯本機檔案：

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

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

如果瀏覽器無法存取 localhost，將透過中繼完成登入。可使用 CLI 顯示的登入 QR 碼或連結，在其他裝置上登入。登入 QR 碼與專案連線 QR 碼不同。

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

新專案會顯示連線 QR 碼，直到編輯器首次成功連線。之後啟動時直接開啟儀表板；按 **`c`** 再次顯示 QR 碼和連線資訊，按 **`l`** 查看日誌。如果 QR 碼放不下，請放大終端機視窗。

### 方法 1：QR 碼（建議）

1. 開啟 Spck Editor → **專案** → **新增專案** → **連結遠端伺服器**
2. 點選 QR 碼圖示
3. 掃描終端機中顯示的 QR 碼。應用程式會自動連線。

> 💡 **注意**：您也可以用裝置的相機應用程式掃描 QR 碼；如果已安裝應用程式，連結會在 Spck Editor 中開啟。

### 方法 2：手動輸入

如果無法掃描 QR 碼：

1. 開啟 Spck Editor → **專案** → **新增專案** → **連結遠端伺服器**
2. 輸入終端機中顯示的**用戶端 ID** 和**密鑰**
3. 選擇終端機中顯示的中繼伺服器
4. 點選**連線**

如果啟用了 **Require PIN to connect**，請輸入在 CLI 儀表板設定的 PIN。應用程式不會儲存 PIN。參閱[連線 PIN](./cli-config#connection-pin)。

## <a name="next-steps"></a>後續步驟

1. **了解中繼系統**：了解 CLI 如何路由流量以及如何選擇伺服器——參見 [CLI 參考](./cli)
2. **設定配置**：調整終端機、安全性和檔案系統設定——參見[設定](./cli-config)
3. **探索進階功能**：CLI 命令、AI 程式設計代理、多專案管理——參見[進階用法](./cli-advanced)
4. **在裝置間傳輸檔案**：無線複製手機和桌面之間的專案——參見[檔案傳輸](./cli-file-transfer)
5. **保持工作階段活躍**：使用 tmux 在裝置間共享工作階段——參見[使用 Tmux](./tmux)
