# <a name="tmux"></a>在 Spck CLI 中使用 Tmux

Tmux（終端機多工器）讓終端機工作階段能夠獨立於啟動它的視窗或 SSH 連線執行。對 Spck CLI 使用者來說，這意味著你可以在斷線重連時保持工作階段，在桌面和行動裝置之間共用正在執行的 Agent 工作階段，並在 SSH 連線中斷後仍讓 CLI 在遠端伺服器上持續執行。

## <a name="installation"></a>安裝

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux 在 Linux 上原生執行。在 Windows 上，請使用[適用於 Linux 的 Windows 子系統 (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)，然後在 WSL 內安裝 tmux。

**第 1 步 — 安裝 WSL（以系統管理員身分執行 PowerShell）：**

```powershell
wsl --install
```

**第 2 步 — 開啟 WSL 終端機並安裝 tmux：**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>使用情境 1：在桌面和行動裝置間共用 Agent 工作階段

Spck CLI 與 tmux 最強大的工作流程是在桌面啟動 AI 程式碼撰寫 Agent，然後從手機無縫接管——或反向操作。兩端看到的終端機狀態完全一致，包含完整的捲動歷程。

### 在桌面啟動工作階段

建立一個具名的 tmux 工作階段：

```bash
tmux new -s code
```

在工作階段內啟動 AI Agent：

```bash
claude
```

Agent 在 tmux 內執行。按 **Ctrl+B** 再按 **D** 即可隨時分離——工作階段及其中執行的一切會繼續在背景運行。

### 從手機連線

1. 開啟 Spck Editor 並連線到你的 CLI 伺服器
2. 從 Spck Editor 終端機面板開啟終端機
3. 接入正在執行的 tmux 工作階段：

```bash
tmux attach -t code
```

你看到的終端機與桌面上完全相同——包含正在執行的 Agent、其輸出和完整的捲動歷程。多個用戶端可以同時接入並查看即時輸出。

### 切換回桌面

隨時從任意終端機重新連線：

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>使用情境 2：在遠端伺服器上持續執行 CLI

如果你透過 SSH 在遠端伺服器上執行 Spck CLI，SSH 工作階段一旦結束，CLI 就會停止——無論是合上筆電、失去 Wi-Fi，還是連線逾時。Tmux 讓程序在伺服器上持續執行，不受連線狀態影響。

### 在遠端伺服器上設定

SSH 登入伺服器，在啟動 CLI 之前先建立一個具名的 tmux 工作階段：

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

CLI 現在在伺服器的 tmux 內執行。關閉 SSH 連線——甚至完全斷線——CLI 仍然持續執行。

### 斷線後重新連線

```bash
ssh user@your-server.com
tmux attach -t spck
```

CLI 從中斷的地方精確恢復。行動用戶端可以透過中繼伺服器正常重新連線。

### 查看正在執行的工作階段

```bash
tmux ls
```

## <a name="linux-service"></a>替代方案：Linux 服務

如需完全自動化的設定，讓 CLI 在開機時無需手動管理 tmux 即可啟動，可以將 Spck CLI 作為 systemd 服務執行。

### 建立服務檔案

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

將 `your-username` 和 `/path/to/your/project` 替換為實際值。如果你是全域安裝的 `spck`（`npm install -g spck`），請將 `ExecStart` 替換為 `which spck` 的輸出。

### 啟用並啟動

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### 查看狀態和日誌

```bash
# 查看狀態
sudo systemctl status spck-cli

# 即時追蹤日誌
journalctl -u spck-cli -f
```

該服務在每次重新啟動時自動啟動，程序崩潰後也會自動重新啟動。

## <a name="essential-tmux-commands"></a>常用 Tmux 指令

| 指令 | 操作 |
| --- | --- |
| `tmux new -s name` | 建立新的具名工作階段 |
| `tmux attach -t name` | 接入已有工作階段 |
| `tmux ls` | 列出所有工作階段 |
| `tmux kill-session -t name` | 終止工作階段 |
| Ctrl+B, D | 從工作階段分離（保持執行） |
| Ctrl+B, C | 建立新視窗 |
| Ctrl+B, N | 切換到下一個視窗 |
| Ctrl+B, P | 切換到上一個視窗 |
| Ctrl+B, [ | 進入捲動模式（方向鍵 / PgUp / PgDn） |
| Q | 退出捲動模式 |
