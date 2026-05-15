# <a name="cli-reference"></a>CLI 參考文件

## <a name="key-features"></a>主要功能

- **遠端檔案系統**：從 Spck Editor 行動應用程式存取並編輯本機檔案
- **Git 整合**：完整的 Git 操作（提交、推送、拉取、分支管理）——需要 Git 2.20.0 以上版本
- **終端機存取**：透過 xterm.js 提供互動式終端機工作階段
- **瀏覽器代理**：在 Spck Editor 內以全螢幕瀏覽器視圖預覽本機伺服器
- **快速搜尋**：具自動偵測 ripgrep 功能的最佳化檔案搜尋（安裝後速度快 100 倍）
- **安全性**：採用密碼學簽章請求，並支援可選的 Firebase 身分驗證

## <a name="relay-server"></a>中繼伺服器

CLI 透過中繼伺服器連接至 Spck Editor，該伺服器負責在兩者之間轉發訊息。首次執行時，CLI 會自動選擇延遲最低的中繼伺服器，並將偏好設定儲存至 `~/.spck-editor/.credentials.json`。

**重要**：CLI 和 Spck Editor 用戶端必須使用同一個中繼伺服器才能建立連線。若用戶端找不到 CLI，請確認雙方已選擇相同的中繼伺服器。

### 可用中繼伺服器

| 地區     | 網址                |
| -------- | ------------------- |
| 歐洲     | `cli-eu-1.spck.io`  |
| 北美     | `cli-na-1.spck.io`  |
| 南亞     | `cli-sas-1.spck.io` |
| 東亞     | `cli-ea-1.spck.io`  |

### 覆寫中繼伺服器

```bash
# 使用指定的中繼伺服器
spck --server cli-eu-1.spck.io

# 縮寫形式
spck -s cli-na-1.spck.io
```

覆寫設定會被儲存並在後續執行時沿用。若要重新執行自動選擇，請清除憑證後重新啟動：

```bash
spck --logout
spck
```

### 在 Spck Editor 中選擇中繼伺服器

透過行動應用程式的 **Link Remote Server** 連線時，請從 **Relay Server** 下拉選單中選擇與 CLI 相同的中繼伺服器。中繼伺服器名稱會在連線後顯示於 CLI 輸出中。

## <a name="daily-workflow"></a>日常工作流程

### 開始工作階段

```bash
cd /path/to/project
spck
# 從行動應用程式連線（自動連接至已儲存的伺服器）
# 開始編寫程式碼
```

### 編輯檔案

1. 在行動應用程式中瀏覽檔案
2. 點選以開啟並編輯
3. 檔案自動儲存至您的電腦

### 執行 Git 指令

**方式一 - 行動應用程式圖形介面：**

- 開啟 Git 面板
- 查看變更、暫存檔案
- 提交並推送

**方式二 - 終端機：**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### 終端機工作階段

點選行動應用程式中的終端機圖示，以您的使用者權限取得完整的 Shell 存取權。

### 結束工作階段

```bash
# 保持 CLI 執行以便快速重新連線（建議）
# 或使用 Ctrl+C 停止
```

## <a name="troubleshooting"></a>疑難排解

### 找不到根目錄

```bash
# 以正確路徑重新設定
spck --setup

# 或直接指定
spck --root /correct/path/to/project
```

### 設定檔損毀

```bash
# 清除設定並重新開始
spck --logout
spck --setup
```

### 連線問題

1. 確認網路連線正常
2. 確認 CLI 和 Spck Editor 均使用**相同的中繼伺服器**（連線後顯示於 CLI 輸出中）
3. 嘗試登出後重新連線：
   ```bash
   spck --logout
   spck
   ```
4. 檢查防火牆設定——確保允許 WebSocket 連線（連接埠 443）

### QR 碼無法掃描

- 掃描前確認已安裝 Spck Editor 應用程式
- 改用手動輸入：Projects → New Project → Link Remote Server
- 使用裝置原生相機應用程式，而非第三方掃描器

### Git 操作無法使用

1. 確認已安裝 Git：

   ```bash
   git --version  # 需要 2.20.0 以上版本
   ```

2. 若未安裝，請依以下方式安裝：

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows：從 git-scm.com 下載
   ```

### 搜尋速度緩慢

安裝 ripgrep 可讓搜尋速度快 100 倍：

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI 會自動偵測並使用 ripgrep
```

### 權限被拒

```bash
# 查看權限
ls -la /path/to/file

# 若需要可修正
chmod 644 /path/to/file

# 不要使用 sudo——CLI 應以擁有檔案的使用者身分執行
```

## <a name="connection-limits"></a>連線限制

最大同時 CLI 連線數和每日使用量限制取決於您的帳號類型：

| 方案      | CLI 連線數 | 每日限制   |
| --------- | ---------- | ---------- |
| 免費版    | 1          | 30 分鐘    |
| 支持者    | 2          | 無限制     |
| 黃金方案  | 5          | 無限制     |

免費版每日使用量於 UTC 時間凌晨 12:00 重置。

達到連線限制時：

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

達到每日免費版限制時：

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

查看目前的連線狀態：

```bash
spck --account
```

> 💡 **注意**：每次只有一台行動裝置可以連接到一個 CLI 實例。每個 CLI 實例佔用一個連線配額。

## <a name="support"></a>支援

- **官方網站**：[https://spck.io](https://spck.io)
- **客服支援**：透過 Spck Editor 行動應用程式聯絡
