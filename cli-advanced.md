# <a name="cli-advanced-usage"></a>CLI Advanced Usage

## <a name="cli-commands"></a>CLI Commands

### Basic Commands

```bash
# Start the CLI
spck

# Run setup wizard
spck --setup

# Show account information
spck --account

# Logout and clear credentials
spck --logout

# Show help
spck --help

# Show version
spck --version
```

### Advanced Options

```bash
# Use custom configuration file
spck --config /path/to/config.json
spck -c /path/to/config.json

# Override root directory
spck --root /path/to/project
spck -r /path/to/project

# Override relay server (e.g., use a specific region)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

### Dashboard

In an interactive terminal, the CLI opens a full-screen dashboard. New projects show the QR code until the first successful editor connection; later launches open the main view. It shows connected editors, ping, Relay/Fast Lane status, and available tools. Piped and service runs print plain logs instead.

| View | Keys |
|------|------|
| Main | `l` logs, `c` connection QR code, `m` manage terminals, `q` `q` quit |
| Settings (main view) | `t` terminal, `b` browser proxy, `a` AI agents, `s` language server, `u` user verification, `f` Fast Lane, `w` keep computer awake, `p` compact shell prompt, `i` require PIN to connect |
| Logs | `↑` `↓` / `j` `k` scroll, `PgUp` `PgDn` page, `←` `→` pan long lines, `g` `G` first / last line, `Esc` back |
| Terminals | `↑` `↓` / `j` `k` select, `x` `x` kill (or remove an exited terminal), `Esc` back |
| QR code | `c` / `Esc` back |

`Ctrl+L` redraws the screen and `Ctrl+C` quits from any view. Pressing `Ctrl+C` again while the CLI is disconnecting exits immediately.

## <a name="ai-coding-agents"></a>AI Coding Agents (ACP)

The Spck CLI bridges Spck Editor's AI Chat to a locally installed AI coding agent — **Claude Code**, **Codex**, or **Gemini CLI** — over the [Agent Client Protocol (ACP)](https://agentclientprotocol.com/). The model runs on your machine with your own subscription, edits real files on disk, and forwards permission prompts to your phone.

![Local AI mode in Spck Editor's AI Chat driving Claude Code from a phone](https://docs.spck.io/assets/gifs/acp-ai.gif)

→ **[AI Coding Agents on Mobile (ACP)](./cli-acp)** — the full guide: supported agents, installation, billing & rate limits (including Anthropic's separate third-party Claude Code quota), configuration, FAQ, and troubleshooting.

> 💡 **Tip**: Use **tmux** to keep AI agent sessions running even after you disconnect. Start a tmux session on your desktop (`tmux new -s code`), launch the agent, then reattach from the Spck CLI terminal on your phone (`tmux attach -t code`). Works for both raw shell agents and ACP-mode agents. See [Using Tmux](./tmux) for a full guide including persistent remote server setup.

## <a name="advanced-usage"></a>Advanced Usage

### Multiple Projects

Run separate CLI instances for different projects simultaneously:

```bash
# Terminal 1: Project A
cd /path/to/projectA
spck

# Terminal 2: Project B
cd /path/to/projectB
spck
```

Each project maintains its own configuration and connection.

> 💡 **Tip**: You can also use multiple CLI instances to transfer files between your desktop and phone. See [File Transfer Between Mobile and Desktop](./cli-file-transfer) for a step-by-step guide.

### Custom Configuration Files

Create specialized configs for different scenarios:

```bash
# Development config
spck --config ~/configs/dev-config.json

# Production config (read-only, no terminal)
spck --config ~/configs/prod-config.json
```

### Environment-Specific Setup

**Local Development:**

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

**Production Server:**

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

### High CPU Usage

Reduce file watching by adding more ignore patterns:

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

Limit concurrent terminals:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>Reducing the Shell Prompt for Mobile

Spck CLI now enables a compact prompt by default for Bash, Zsh and Fish: `folder $`, or `folder #` for root, with `~` for home. Press **`p`** in the dashboard or set **`terminal.compactPrompt`** to toggle it for new terminals. Your shell configuration files are not changed. See [Compact prompt](./cli-config#compact-prompt).

For other shells, or if you disable the built-in compact prompt and want your own format, use the manual examples below.

### Bash

Add the following to `~/.bashrc`:

```bash
export PS1='\$ '
```

Apply without restarting the shell:

```bash
source ~/.bashrc
```

### Zsh

Add the following to `~/.zshrc`:

```zsh
PROMPT='$ '
```

Apply without restarting the shell:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

Create your profile file if it doesn't exist yet, then open it:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Add the following to the profile:

```powershell
function prompt { "$ " }
```

Apply without restarting the shell:

```powershell
. $PROFILE
```

### Command Prompt (Windows)

Set a minimal prompt for the current session:

```cmd
PROMPT $$
```

To make this permanent, add `PROMPT` as a **User** or **System** environment variable with the value `$$` via **Control Panel → System → Advanced System Settings → Environment Variables**.
