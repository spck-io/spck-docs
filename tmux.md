# <a name="tmux"></a>Using Tmux with Spck CLI

Tmux (Terminal Multiplexer) lets terminal sessions run independently from the window or SSH connection that started them. For Spck CLI users this means you can keep sessions alive across reconnects, share a running agent session between desktop and mobile, and run the CLI persistently on a remote server even after your SSH connection drops.

## <a name="installation"></a>Installation

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

Tmux runs natively on Linux. On Windows, use [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install), then install tmux inside WSL.

**Step 1 — Install WSL (PowerShell as Administrator):**

```powershell
wsl --install
```

**Step 2 — Open a WSL terminal and install tmux:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Use Case 1: Sharing Agent Sessions Across Desktop and Mobile

The most powerful tmux workflow with Spck CLI is starting an AI coding agent on your desktop and seamlessly picking it up from your mobile — or the reverse. Both see the exact same terminal state including the full scrollback history.

### Start a Session on Desktop

Create a named tmux session:

```bash
tmux new -s code
```

Launch your AI agent inside the session:

```bash
claude
```

The agent runs inside tmux. Detach at any time by pressing **Ctrl+B** then **D** — the session and everything running inside it continues in the background.

### Attach from Mobile

1. Open Spck Editor and connect to your CLI server
2. Open a terminal from the Spck Editor terminal panel
3. Attach to the running tmux session:

```bash
tmux attach -t code
```

You see exactly the same terminal as on your desktop — including the running agent, its output, and full scrollback history. Multiple clients can attach simultaneously and see live output.

### Switch Back to Desktop

Reattach from any terminal at any time:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Use Case 2: Persistent CLI on a Remote Server

If you run Spck CLI on a remote server over SSH, the CLI stops the moment the SSH session ends — whether you close your laptop, lose Wi-Fi, or the connection times out. Tmux keeps the process alive on the server regardless of your connection state.

### Setup on the Remote Server

SSH into your server and start a named tmux session before launching the CLI:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

The CLI is now running inside tmux on the server. Close the SSH connection — or lose it entirely — and the CLI keeps running.

### Reconnect After Disconnecting

```bash
ssh user@your-server.com
tmux attach -t spck
```

The CLI resumes exactly where it left off. Mobile clients can reconnect through the relay server normally.

### List Running Sessions

```bash
tmux ls
```

## <a name="linux-service"></a>Alternative: Linux Service

For a fully automated setup that starts the CLI on boot without any manual tmux management, run Spck CLI as a systemd service.

### Create the Service File

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

Replace `your-username` and `/path/to/your/project` with your actual values. If you installed `spck` globally (`npm install -g spck`), replace `ExecStart` with the output of `which spck`.

### Enable and Start

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Check Status and Logs

```bash
# View status
sudo systemctl status spck-cli

# Follow live logs
journalctl -u spck-cli -f
```

The service starts automatically on every reboot and restarts itself if the process crashes.

## <a name="essential-tmux-commands"></a>Essential Tmux Commands

| Command | Action |
| --- | --- |
| `tmux new -s name` | Create a new named session |
| `tmux attach -t name` | Attach to an existing session |
| `tmux ls` | List all sessions |
| `tmux kill-session -t name` | Kill a session |
| Ctrl+B, D | Detach from session (keeps it running) |
| Ctrl+B, C | Create a new window |
| Ctrl+B, N | Switch to next window |
| Ctrl+B, P | Switch to previous window |
| Ctrl+B, [ | Enter scroll mode (arrow keys / PgUp / PgDn) |
| Q | Exit scroll mode |
