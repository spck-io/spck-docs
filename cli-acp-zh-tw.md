# <a name="ai-coding-agents-acp"></a>行動裝置上的 AI 編碼代理（ACP）

透過 Spck Editor 的 **AI Chat** 直接從手機執行 **Claude Code**、**OpenAI Codex** 或 **Gemini CLI**。Spck CLI 透過開放的 [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) 將您的編輯器與本機安裝的代理 CLI 橋接,使模型在您的機器上、使用您的訂閱、針對您真實的檔案執行——而您從行動裝置進行監督。

![Spck Editor 的 AI Chat 中的 ACP 本機 AI 模式,從手機驅動桌面上的 Claude Code](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>什麼是 ACP 以及為什麼使用它?

Agent Client Protocol (ACP) 是 Zed Industries 推出的、用於編輯器 ↔ AI 代理通訊的開放標準,精神上與 Language Server Protocol (LSP) 一致。Spck CLI 0.6.0+ 實作了 ACP,作為 Spck Editor 的 AI Chat(用戶端)與您所安裝的任何相容 ACP 的代理執行檔(代理)之間的**傳輸層**。

與應用程式內透過伺服器路由的 AI Chat 相比,本機 ACP 路徑提供:

- **您自己的訂閱** —— 代理呼叫計入您的 Claude Code / ChatGPT / Gemini 帳戶,而不是您的 Spck Editor AI 配額。
- **真實的檔案系統存取** —— 代理透過 CLI 讀寫磁碟上的真實檔案,而不是編輯器的記憶體副本。
- **原生工具** —— 檔案監看器、語言伺服器和 shell 命令在您真實的機器上執行。
- **與桌面的連續性** —— 您在辦公桌上使用的同一個 `claude` / `gemini` / `codex` 登入,驅動著行動端聊天。

## <a name="acp-supported-agents"></a>支援的 AI 代理

安裝您希望可用的任何代理。Spck CLI 在啟動時自動偵測它們。

| 代理              | 安裝                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>安裝與設定

### 1. 安裝 Spck CLI

如果您還沒有:

```bash
npm install -g spck
# 或不安裝而直接執行
npx spck
```

完整的首次執行精靈見[開始使用 Spck CLI](./cli-start)。

### 2. 安裝一個或多個代理 CLI

選擇您希望可用的任何代理。可以安裝多個 —— AI Chat 會讓您按工作階段在它們之間選擇。安裝命令參見上面的[支援的 AI 代理](#acp-supported-agents)表。

### 3. 對每個代理進行一次身分驗證

各代理 CLI 在 Spck Editor 之外管理自己的登入:

```bash
claude            # Anthropic Claude Code 登入流程
codex login       # OpenAI Codex 登入流程(由 codex-acp 使用)
gemini            # Google Gemini 登入流程
```

如果跳過此步驟,Spck Editor 在您第一次開始聊天時會顯示類似 `ACP agent requires authentication; run <binary> login and retry` 的錯誤。

### 4. 啟動 Spck CLI

```bash
cd /path/to/your/project
spck
```

啟動時,CLI 會按代理列印一份偵測報告,列出哪些代理可用,接著在主要功能區塊中顯示一行摘要,例如 `✅ ACP agents: Claude Code, Gemini CLI`。如果沒有任何可用的,它將退回到經伺服器路由的 AI Chat。

### 5. 連線 Spck Editor

掃描 QR code 或使用[手動輸入](./cli-start#connecting)。連線後,在 Spck Editor 中開啟 **AI Chat** —— 傳輸切換器會將本機代理與雲端選項並列顯示。

## <a name="acp-authentication"></a>身分驗證

每個代理在 Spck CLI 執行的機器上管理自己的憑證。為每個代理執行一次登入流程:

```bash
# Claude Code
claude

# Codex(codex-acp 包裝了 Codex CLI 自身的登入)
codex login

# Gemini CLI
gemini
```

如果重新安裝或更換機器,請在新主機上重新登入。身分驗證是**按主機、按代理**的 —— Spck Editor 本身從不持有這些憑證。

## <a name="acp-billing"></a>計費與速率限制

由於 ACP 在您的機器上以您自己的憑證執行代理,**所有使用都計入您在該供應商處的帳戶** —— 而不是您的 Spck Editor 訂閱。在此模式下,Spck Editor 和 Spck 中繼伺服器只擔任純傳輸,不會為 ACP 流量消耗您應用程式內的任何 AI 配額。

### Claude Code 計費

> ⚠️ **重要 —— 當 Claude Code 被第三方工具驅動時,會套用獨立的速率限制桶。**
>
> 當 Claude Code 透過 ACP 從第三方用戶端被呼叫時,Anthropic 將該流量計入與 Pro / Max 訂閱下您的互動式 `claude` CLI 工作階段**不同的速率限制桶**。實際影響是:您可能在仍有互動式 Claude Code 餘量(或反之)時就耗盡了第三方桶,而且兩者無法合併。
>
> 在 `claude` 內執行 `/usage`,並在 [Anthropic Console](https://platform.claude.com/usage) 查看目前消耗;適用於您方案的具體數字,請參閱 [Claude Code 成本與限制文件](https://code.claude.com/docs/en/costs)。

### Codex(codex-acp)計費

透過 OpenAI Codex CLI 自身的身分驗證計費 —— 即您的 OpenAI API 金鑰或 ChatGPT 登入。使用量計入該帳戶擁有的任何方案。價格和配額與互動式 `codex` 使用相同;目前數字參見 [openai.com/codex](https://github.com/openai/codex) 與您的 OpenAI 控制台。

### Gemini CLI 計費

透過您的 Google 帳戶或 Gemini API 金鑰計費。使用量計入該登入綁定的 Gemini 方案或 API 配額。速率限制詳情請見 [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits)。

## <a name="acp-configuration"></a>設定

ACP 預設啟用,透過專案的 `spck-cli.config.json` 進行設定:

```json
{
  "acp": {
    "enabled": true
  }
}
```

完整的 schema 見[設定 → ACP 設定](./cli-config#acp-settings)。

### 按專案停用 ACP

如果您不希望 Spck Editor 能在該主機上驅動本機代理:

```json
{
  "acp": {
    "enabled": false
  }
}
```

停用時,編輯器的傳輸切換器會隱藏本機代理選項,任何 `acp.*` RPC 會以 `FEATURE_DISABLED` 拒絕。設定精靈在首次執行時會詢問此問題(預設 `Y`);早於該選項的設定會自動載入 `acp.enabled: true` 並重新儲存。

### 停用單一代理

要在保持其他代理 ACP 可用的同時阻止 _特定_ 代理被提供,解除安裝該代理的執行檔即可。偵測在每次 CLI 啟動時執行,因此編輯器的傳輸切換器會把它從清單中移除。

## <a name="acp-vs-server-routed"></a>本機 ACP vs. 經伺服器路由的 AI Chat

| 能力                                       | 經伺服器路由(預設,無 CLI)          | 本機(ACP,CLI 已連線)                |
| ------------------------------------------ | ----------------------------------- | --------------------------------------- |
| 模型執行位置                                | Spck 雲                             | 您的機器                                |
| 憑證                                        | 您的 Spck Editor 帳戶               | 代理自己的登入 / API 金鑰               |
| 檔案存取                                    | 編輯器的記憶體檔案系統              | 透過 CLI 根目錄的磁碟真實檔案           |
| 計入 Spck Editor AI 配額                    | 是                                  | **否** —— 由代理供應商計費              |
| 無需 CLI 執行即可運作                       | 是                                  | 否(需要 CLI + WebSocket)               |
| 可用代理                                    | Spck 託管的模型                     | Claude Code、Codex、Gemini CLI          |
| 手機上的工具使用權限提示                    | 適用時                              | 是,透過 ACP 轉發                       |
| 權杖串流                                    | 是                                  | 是                                      |
| 多輪聊天                                    | 是                                  | 是                                      |

您可以在專案中途切換傳輸 —— AI Chat 會根據 CLI 連線狀態與偵測到的代理,顯示目前可用的路徑。

## <a name="acp-tmux"></a>與 Tmux 搭配用於長時間工作階段

ACP 工作階段能夠跨編輯器重連保持存活,但 Spck CLI 行程本身在其終端機關閉時就會結束。對於長時間執行的代理工作 —— 大型重構、數小時的規劃工作階段 —— 請在 [tmux](./tmux) 工作階段中啟動 CLI,以便在 SSH 斷線、終端機關閉與筆電休眠後仍能存活:

```bash
tmux new -s spck
spck
# Ctrl+B 然後 D 即可分離
```

您也可以從手機透過 Spck CLI 終端機重新連線,並使用 `tmux attach -t spck` 即時監控代理。完整的模式(包括將 CLI 作為持久背景服務執行)見[使用 Tmux](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile)。

對於 Linux 主機,[Claude Skill: Linux Service](./claude-skill) 頁面提供了將 Spck CLI 作為 `systemd` 服務執行的一鍵設定,這樣 WebSocket —— 以及其上的任何 ACP 工作階段 —— 在開機時自動啟動。

## <a name="acp-faq"></a>常見問題

### 我可以在手機上使用 Claude Code 嗎?

可以。在桌面上安裝 Claude Code,使用 `claude` 進行身分驗證,然後在您的專案中執行 `spck`。從手機連線 Spck Editor,並在 AI Chat 的傳輸切換器中選擇 Claude Code。模型在桌面上以您的訂閱執行;您從手機來驅動它。

### Spck Editor 能看到我的 Claude / OpenAI / Gemini API 金鑰嗎?

不會。每個代理 CLI 在執行 Spck CLI 的機器上管理自己的憑證。ACP 訊息透過手機與 CLI 之間加密的 WebSocket 通道傳遞,但代理自身的身分驗證權杖不會離開您的主機。

### 透過 Spck Editor 使用 Claude Code 會產生額外費用嗎?

不會有 Spck Editor 的額外費用。代理的使用計入您的 Anthropic / OpenAI / Google 方案,與您在辦公桌前互動式執行代理完全一致 —— 唯一不同的是,Anthropic 對第三方用戶端套用獨立的速率限制桶;參見上文[計費與速率限制](#acp-billing)。

### 使用 ACP 需要付費的 Spck Editor 訂閱嗎?

不需要。免費方案(每天 30 分鐘 CLI 連線)足以驅動任何 ACP 代理。只有應用程式內經伺服器路由的 AI Chat 才會消耗 Spck Editor AI 配額。

### 如果我在聊天中途斷開 Wi-Fi 會怎樣?

代理行程在 CLI 主機上繼續存活。當編輯器重新連線時,工作階段以完整的聊天歷史恢復。您離線期間到達的串流輸出會在重連時重播。

### 我可以在遠端伺服器而不是筆電上執行代理嗎?

可以。在任何可達的 Linux/macOS 主機上執行 Spck CLI —— 開發 VM、家用伺服器、工作站 —— 並透過中繼伺服器連線到它。搭配 [tmux](./tmux) 或 [systemd skill](./claude-skill),以在連線之間保持 CLI 存活。

### ACP 在 Spck Editor Lite 中可用嗎?

可以。ACP 流量使用與檔案系統和 git 相同的 WebSocket 傳輸,Spck Editor Lite 支援該傳輸。請確保在 CLI 設定中將 `security.userAuthenticationEnabled` 設為 `false` —— Lite 不支援 Firebase 身分驗證。參見[設定 → 使用者驗證](./cli-config#user-authentication)。

### 為什麼我的代理沒出現在 AI Chat 中?

檢查 CLI 啟動日誌中按代理的行:

- 代理未被偵測到 —— 安裝它(參見[支援的 AI 代理](#acp-supported-agents))。
- 已偵測到但在編輯器中缺失 —— 確認您已完成代理自己的登入流程(`claude`、`codex login`、`gemini`)。
- ACP 已停用 —— 檢查 `.spck-editor/config/spck-cli.config.json` 中的 `acp.enabled`。參見[設定](./cli-config#acp-settings)。

## <a name="acp-troubleshooting"></a>疑難排解

### 代理已偵測但工作階段無法啟動

通常意味著代理未通過身分驗證。在 CLI 主機上執行代理的登入流程:

```bash
claude              # 然後完成瀏覽器驗證
codex login
gemini
```

如果問題仍存在,查看 CLI 在 `.spck-editor/logs/` 下的日誌中代理的 stderr 輸出,通常會指向失敗的驗證或執行檔。

### 聊天過程中出現速率限制錯誤

對於 Claude Code,編輯器會逐字呈現 Anthropic 的 429。請查看 [Anthropic Console 用量頁](https://platform.claude.com/usage)與 [Claude Code 成本文件](https://code.claude.com/docs/en/costs) —— 記得第三方速率限制桶與您的互動式 `claude` 配額是分開的。

對於 Codex 與 Gemini,編輯器會呈現各自供應商的配額錯誤。請透過供應商控制台解決。

### 啟動 ACP 工作階段時 CLI 崩潰

Spck CLI 將 ACP 流量記錄在 `.spck-editor/logs/`。在重現問題時追蹤最新的日誌檔案:

```bash
tail -f .spck-editor/logs/spck-*.log
```

請在 [github.com/spck-editor](https://github.com/spck-editor) 提交 bug,並附上相關片段。

### 代理在專案根目錄之外進行了變更

ACP 代理被限定在 CLI 設定的 `root` 目錄內。如果您看到寫入出現在它之外,請提交 issue —— 這不應發生。作為臨時解決方法,執行 `spck --root /path/to/specific/project` 進一步縮小範圍。

## <a name="acp-see-also"></a>另見

- [開始使用 Spck CLI](./cli-start) —— 首次安裝、身分驗證與連線
- [CLI 參考](./cli) —— 中繼伺服器、日常工作流、連線限制
- [設定 → ACP 設定](./cli-config#acp-settings) —— `acp.enabled` 設定選項
- [進階用法](./cli-advanced) —— CLI 旗標、多專案、行動端提示詞技巧
- [使用 Tmux](./tmux) —— 跨重連保持 ACP 工作階段存活
- [Claude Skill: Linux Service](./claude-skill) —— 將 Spck CLI 作為 `systemd` 服務執行,使 ACP 始終可用
- [Agent Client Protocol 規範](https://agentclientprotocol.com/) —— ACP 實作的開放標準
- [Claude Code 文件](https://docs.claude.com/en/docs/claude-code/overview)
- [Gemini CLI 儲存庫](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
