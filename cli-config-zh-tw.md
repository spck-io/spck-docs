# <a name="cli-configuration"></a>CLI 設定

## <a name="configuration"></a>設定說明

### 設定檔位置

設定檔儲存於專案目錄中的 `.spck-editor/config/spck-cli.config.json`。

**重要**：`.spck-editor/config` 是指向 `~/.spck-editor/projects/{project_id}/` 的**符號連結**，可將敏感資訊保存在專案目錄之外。

### 預設設定

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "compactPrompt": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false,
    "requirePin": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  },
  "acp": {
    "enabled": true
  },
  "fastLane": {
    "enabled": true
  }
}
```

### 瀏覽器代理設定

- **`browserProxy.enabled`**（布林值）：啟用或停用瀏覽器代理功能
  - 預設值：`true`
  - 設為 `false` 可防止行動應用程式透過 CLI 開啟瀏覽器代理工作階段

### ACP（本機 AI 代理）設定

- **`acp.enabled`**（布林值）：啟用或停用 ACP（本機 AI 編碼代理）整合
  - 預設值：`true`
  - 控制 Spck Editor 是否可以透過 [Agent Client Protocol](https://agentclientprotocol.com/) 在此主機上驅動本機安裝的 AI 編碼代理（Claude Code、Codex、Gemini CLI）
  - 為 `false` 時，`acp.capabilities` 會回應 `{ available: false, agents: [] }`，編輯器的本機代理傳輸切換器會被隱藏，並改用雲端（SSE）路徑
  - 代理具有間接的 shell 與檔案系統存取權，因此若不想暴露此攻擊面，請逐專案停用此選項
  - **向下相容**：在此選項出現之前建立的設定會自動填入 `acp: { enabled: true }` 並重新儲存

> 💡 **另請參閱**：[行動裝置上的 AI 程式設計助手 (ACP)](./cli-acp) — 支援的代理（Claude Code、Codex、Gemini CLI）、身分驗證與**計費**的完整指南，包括 Anthropic 對從 Spck Editor 等第三方工具驅動的 Claude Code 所套用的獨立速率限制配額。

### <a name="fast-lane-settings"></a>Fast Lane 設定

- **`fastLane.enabled`**（布林值）：允許編輯器透過 WebRTC 直接連線到此 CLI（[Fast Lane](./cli#fast-lane)，適用於 Supporter 與 Gold 帳號）
  - 預設值：`true`（沒有 `fastLane` 項目的設定視為已啟用）
  - 在不允許點對點流量的網路中設為 `false`，編輯器將改為透過中繼連線
  - 也可以在 CLI 儀表板中按 **`f`** 鍵切換
  - 需要重新啟動 CLI 才會生效

### 終端機設定

- **`terminal.enabled`**（布林值）：啟用或停用終端機存取
  - 預設值：`true`
  - 設為 `false` 可降低終端機遭未授權存取的風險

<a name="compact-prompt"></a>

- **`terminal.compactPrompt`**（boolean）：Bash、Zsh 和 Fish 的精簡提示字元（`folder $`，root 為 `folder #`，家目錄為 `~`）。預設值為 `true`，舊設定缺少此項時也預設啟用。在儀表板按 **`p`** 切換，對新終端機生效。設為 `false` 可使用原來的提示字元。不會修改 Shell 設定檔。

- **`terminal.maxBufferedLines`**（數字）：最大捲動回溯緩衝區
  - 預設值：`10000`
  - 影響記憶體使用量（每 10,000 行約 1MB）

- **`terminal.maxTerminals`**（數字）：最大同時終端機工作階段數
  - 預設值：`10`
  - 每個終端機約使用 5–10MB 記憶體

### 檔案系統設定

- **`filesystem.maxFileSize`**（字串）：讀寫的最大檔案大小
  - 預設值：`"10MB"`
  - 可接受：`"5MB"`、`"50MB"` 等

- **`filesystem.watchIgnorePatterns`**（字串陣列）：從檔案監看中排除的模式
  - 預設值：忽略建置輸出和相依套件
  - 透過避免監看大量自動產生的檔案來提升效能

### 安全性設定

<a name="connection-pin"></a>

- **`security.requirePin`**（boolean）：連線時要求 4–6 位數 PIN，預設為 `false`。在儀表板按 **`i`**，選擇並確認 PIN。應用程式在授權存取前要求輸入，且不會儲存。QR 碼不包含 PIN；`security.pin` 儲存加鹽驗證值。五次錯誤會觸發跨裝置和重新連線共用的 60 秒冷卻期。對新連線和重新連線生效，現有連線保持開啟。關閉即可停用；重新啟用時可選擇新 PIN。

- **`security.userAuthenticationEnabled`**（布林值）：啟用 Firebase 使用者身分驗證
  - 預設值：`false`
  - `false` 時：延遲較低、與 Lite 版相容，仍受密鑰簽章保護
  - `true` 時：額外的安全層、使用者身分驗證，首次連線增加 2–20 秒延遲
  - **無論此設定為何，所有請求均始終進行密碼學簽章**

## <a name="security"></a>安全性

### 加密連線

所有通訊均使用：

- **WSS（WebSocket Secure）**：TLS/SSL 加密
- **HTTPS**：加密初始交握

### Fast Lane 加密

啟用 [Fast Lane](./cli#fast-lane) 時，資料會透過以 DTLS 加密的 WebRTC 直連傳輸。CLI 的身分驗證證明與該 DTLS 工作階段綁定，因此連線無法被劫持，也無法在其他通道上重放。

### 請求簽章

每個請求均進行密碼學簽章：

- 密鑰在本機產生，從不透過網際網路傳輸
- 建議避免使用可能暴露您密鑰的第三方 QR 掃描器

### 最佳實踐

1. **保護憑證**：

   ```bash
   # 加入 .gitignore（設定過程中自動執行）
   echo ".spck-editor/" >> .gitignore
   ```

2. **在共用電腦上登出**：

   ```bash
   spck --logout
   ```

3. **限制開放的目錄**：

   ```bash
   # 不要開放整個家目錄
   spck --root /path/to/specific/project
   ```

4. **若不需要可停用終端機**：

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **若不需要可停用瀏覽器代理**：
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

6. **若不需要可停用 ACP（本機 AI 代理）**：
   ```json
   {
     "acp": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>使用者身分驗證

Lite 支援透過 Spck CLI 編輯桌上型電腦或公用虛擬機上的專案。遠端專案需要 **Spck 帳戶和有效的 Spck 訂閱**，不包含在 Lite 的一次性購買中。訂閱有助於負擔 Spck 伺服器持續產生的託管、運作和維護費用。隨 Lite 提供的本機編輯和 Git 工具仍可無需訂閱使用。 CLI 的選用設定 `userAuthenticationEnabled` 不會免除帳戶和訂閱要求。

Spck CLI 支援可選的 Firebase 使用者身分驗證，作為在始終啟用的請求簽章之上的第二道安全防線。

### 運作原理

啟用後，CLI 要求您使用 Spck Editor 帳號登入。連線透過每小時過期的 Firebase ID 令牌進行驗證，並使用儲存於 `~/.spck-editor/.credentials.json` 的安全重新整理令牌自動更新。

### 啟用使用者身分驗證

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### 取捨比較

|                      | 停用（預設）               | 啟用                              |
| -------------------- | -------------------------- | --------------------------------- |
| **保護機制**         | 密鑰簽章                   | + Firebase 身分驗證               |
| **初始延遲**         | 無驗證額外負擔             | 首次連線增加 2–20 秒              |
| **Spck Editor Lite** | ✅ 支援                    | ❌ 不支援                         |
| **離線使用**         | 無需網路連線               | 需要網路連線以更新令牌            |

### 何時啟用

**保持停用（預設）的情況：**

- 使用 **Spck Editor Lite**——Lite 版不支援 Firebase 登入；將此設定為 `true` 將導致 Lite 使用者無法連線
- 在本機網路或受信任環境中工作，且密鑰簽章已足夠安全
- 優先考量最小化連線延遲

**啟用的情況：**

- CLI 部署於可透過網際網路存取的伺服器上
- 除簽章金鑰外，您還需要使用者身分驗證作為額外的存取控制層

> ⚠️ **Spck Editor Lite 不支援 Firebase 身分驗證。** 若 `userAuthenticationEnabled` 設為 `true`，Spck Editor Lite 將無法連線。使用 Lite 版時請將此設定保持為 `false`。
