# <a name="claude-skill"></a>Claude 技能：將 Spck CLI 作為 Linux 服務執行

本頁提供一個可下載的 [Claude Code 技能](https://docs.claude.com/en/docs/claude-code/skills)，用於自動化在 Linux 上將 Spck CLI（`spck`）安裝為 `systemd` 服務的過程。安裝技能後，你可以讓 Claude Code「將 spck 作為服務執行」，它會檢查你的環境、產生填入實際絕對路徑的正確 unit 檔案、安裝並驗證其是否正常執行——無需從清單中複製貼上命令。

該技能自動化了與[使用 Tmux → 替代方案：Linux 服務](./tmux#linux-service)中描述的相同 systemd 設定，並加入了手動編寫 unit 檔案時容易遺漏的預先檢查和失敗診斷。

## <a name="download"></a>下載

下載技能檔案並儲存到本地 Claude Code 技能目錄：

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

或手動下載：<a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a>——放置到 `~/.claude/skills/spck-cli-service/SKILL.md`。

## <a name="what-the-skill-does"></a>技能的作用

被呼叫時，技能引導 Claude Code 完成完整安裝：

1. 驗證主機是執行 `systemd` 的 Linux。
2. 解析 `spck` 的絕對路徑（避免導致 `ExecStart` 失效的 `PATH` 不匹配）。
3. 如果 `node` 透過 `nvm` 安裝則發出警告——這些路徑在每次 Node 升級時都會變更，並靜默地破壞 unit。
4. 確認 `~/.spck-editor/.credentials.json` 存在（CLI 必須在作為服務執行之前至少以互動方式執行一次）。
5. 根據需求在**使用者服務**（`systemctl --user`，無需 `sudo`）和**系統服務**之間選擇。
6. 寫入填入實際路徑的 unit 檔案——無佔位符。
7. 執行 `daemon-reload`、`enable --now`，然後追蹤 journal 以確認 CLI 已連線到中繼伺服器。

技能還記錄了七種最常見的故障模式（錯誤的 `ExecStart` 路徑、缺少憑證、專案目錄權限錯誤、觸發 `start-limit-hit` 的重新啟動迴圈、npm 升級後的過時 nvm 路徑等），以便 Claude Code 能夠診斷損壞的服務而不是簡單地重新產生 unit 檔案。

## <a name="installation"></a>安裝

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**第 1 步 — 下載技能檔案：**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**第 2 步 — 驗證 Claude Code 已識別它：**

```bash
claude /skills
```

你應該在清單中看到 `spck-cli-service`。如果沒有，重新啟動 Claude Code 讓它重新掃描技能目錄。

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop 在 macOS 和 Linux 上從同一個 `~/.claude/skills/` 目錄載入技能。在 Windows 上，路徑是 `%USERPROFILE%\.claude\skills\`——但技能本身只在 Linux 主機上運作，因此請將其安裝在你想執行 `spck` 的電腦上，而不是執行 Claude Desktop 的電腦上。

如果你管理的是遠端 Linux 伺服器，請在該伺服器上透過 SSH 執行 Claude Code（或透過 Spck CLI 終端機，它為伺服器提供完整的 shell 存取）。在本地 Mac 上安裝技能無法幫助設定遠端 Linux 服務。

</div>
  </div>
</div>

## <a name="usage"></a>使用方式

安裝後，用自然語言向 Claude Code 發出請求來呼叫技能。可以觸發技能的範例：

- 「將 spck 安裝為 systemd 服務」
- 「讓 Spck CLI 開機自動啟動」
- 「我的 spck-cli.service 一直在重新啟動，你能除錯嗎？」
- 「將 spck 作為守護程序執行，這樣 SSH 斷線後也能繼續工作」

Claude Code 會讀取技能，執行預先檢查（會提示你核准每個命令），然後產生並安裝 unit 檔案。在核准前審查每個命令——特別是在 `sudo` 下寫入 `/etc/systemd/system/` 的命令。

## <a name="what-gets-installed"></a>安裝內容

技能安裝一個單獨的 unit 檔案。使用者服務的檔案路徑為：

```bash
~/.config/systemd/user/spck-cli.service
```

內容類似：

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

對於系統服務，檔案位於 `/etc/systemd/system/spck-cli.service`，並新增 `User=` 和 `Group=` 指令。技能根據你的環境選擇正確的變體，並將實際絕對路徑寫入檔案。

## <a name="why-a-skill-instead-of-copy-paste"></a>為什麼用技能而不是複製貼上？

[tmux 文件](./tmux#linux-service)中的 unit 檔案只是起點，但服務要真正正常運作需要幾件事都正確：

- `ExecStart` 必須是 `spck` 的**絕對路徑**。在登入 shell 中執行 `which spck` 會解析 `.bashrc` 中的 PATH 操作，但 systemd 看不到這些。
- 如果 `spck` 透過 `nvm` 安裝，路徑中嵌入了 Node 版本——升級 Node 會靜默地破壞服務，直到下次重新啟動。
- CLI 必須至少以互動方式執行一次才能建立 `~/.spck-editor/.credentials.json`。沒有憑證的全新服務啟動會乾淨地退出，沒有明顯錯誤。
- `User=` 必須擁有 `WorkingDirectory`，否則檔案監視會遇到 `EACCES` 並導致 CLI 進入重新啟動迴圈。
- 使用者服務在無頭伺服器上需要 `loginctl enable-linger`，否則只有在登入工作階段活躍時才會執行。

技能將這些全部自動化，這樣你就不必記住這些細節。

## <a name="uninstall"></a>解除安裝

停用並移除服務：

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

對於系統服務：

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

從 Claude Code 中移除技能本身：

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>另請參閱

- [使用 Tmux](./tmux) — 使用 `tmux` 在 SSH 斷線時保持 CLI 執行的替代方法。
- [進階用法](./cli-advanced) — 完整的 CLI 命令參考、設定覆寫和多專案設定。
- [設定](./cli-config) — unit 檔案未涵蓋的終端機、檔案系統、安全性和認證設定。
