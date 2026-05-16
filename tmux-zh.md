# <a name="tmux"></a>在 Spck CLI 中使用 Tmux

Tmux（终端复用器）让终端会话能够独立于启动它的窗口或 SSH 连接运行。对于 Spck CLI 用户来说，这意味着你可以在断线重连时保持会话，在桌面和移动设备之间共享正在运行的 Agent 会话，并在 SSH 连接断开后仍让 CLI 在远程服务器上持续运行。

## <a name="installation"></a>安装

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

Tmux 在 Linux 上原生运行。在 Windows 上，请使用[适用于 Linux 的 Windows 子系统 (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)，然后在 WSL 内安装 tmux。

**第 1 步 — 安装 WSL（以管理员身份运行 PowerShell）：**

```powershell
wsl --install
```

**第 2 步 — 打开 WSL 终端并安装 tmux：**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>使用场景 1：在桌面和移动设备间共享 Agent 会话

Spck CLI 与 tmux 最强大的工作流是在桌面启动 AI 编码 Agent，然后从手机无缝接管——或反向操作。两端看到的终端状态完全一致，包括完整的滚动历史。

### 在桌面启动会话

创建一个命名的 tmux 会话：

```bash
tmux new -s code
```

在会话内启动 AI Agent：

```bash
claude
```

Agent 在 tmux 内运行。按 **Ctrl+B** 再按 **D** 即可随时分离——会话及其中运行的一切会继续在后台运行。

### 从手机连接

1. 打开 Spck Editor 并连接到你的 CLI 服务器
2. 从 Spck Editor 终端面板打开一个终端
3. 接入正在运行的 tmux 会话：

```bash
tmux attach -t code
```

你看到的终端与桌面上完全一样——包括正在运行的 Agent、其输出和完整的滚动历史。多个客户端可以同时接入并查看实时输出。

### 切换回桌面

随时从任意终端重新连接：

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>使用场景 2：在远程服务器上持续运行 CLI

如果你通过 SSH 在远程服务器上运行 Spck CLI，SSH 会话一旦结束，CLI 就会停止——无论是合上笔记本、失去 Wi-Fi，还是连接超时。Tmux 让进程在服务器上持续运行，不受连接状态影响。

### 在远程服务器上配置

SSH 登录服务器，在启动 CLI 之前先创建一个命名的 tmux 会话：

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

CLI 现在在服务器的 tmux 内运行。关闭 SSH 连接——甚至完全断线——CLI 仍然持续运行。

### 断线后重新连接

```bash
ssh user@your-server.com
tmux attach -t spck
```

CLI 从中断的地方精确恢复。移动客户端可以通过中继服务器正常重新连接。

### 查看正在运行的会话

```bash
tmux ls
```

## <a name="linux-service"></a>替代方案：Linux 服务

如需完全自动化的配置，让 CLI 在开机时无需手动管理 tmux 即可启动，可以将 Spck CLI 作为 systemd 服务运行。

### 创建服务文件

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

将 `your-username` 和 `/path/to/your/project` 替换为实际值。如果你是全局安装的 `spck`（`npm install -g spck`），请将 `ExecStart` 替换为 `which spck` 的输出。

### 启用并启动

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### 查看状态和日志

```bash
# 查看状态
sudo systemctl status spck-cli

# 实时跟踪日志
journalctl -u spck-cli -f
```

该服务在每次重启时自动启动，进程崩溃后也会自动重启。

## <a name="essential-tmux-commands"></a>常用 Tmux 命令

| 命令 | 操作 |
| --- | --- |
| `tmux new -s name` | 创建新的命名会话 |
| `tmux attach -t name` | 接入已有会话 |
| `tmux ls` | 列出所有会话 |
| `tmux kill-session -t name` | 终止会话 |
| Ctrl+B, D | 从会话分离（保持运行） |
| Ctrl+B, C | 创建新窗口 |
| Ctrl+B, N | 切换到下一个窗口 |
| Ctrl+B, P | 切换到上一个窗口 |
| Ctrl+B, [ | 进入滚动模式（方向键 / PgUp / PgDn） |
| Q | 退出滚动模式 |
