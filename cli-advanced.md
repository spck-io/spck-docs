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

## <a name="ai-coding-agents"></a>AI Coding Agents

The Spck CLI terminal gives you full shell access, which means you can run AI coding agents directly from your mobile device. These agents can read, write, and refactor code in your project while you supervise from Spck Editor.

> 💡 **Tip**: Use **tmux** to keep AI agent sessions running even after you disconnect. Start a tmux session on your desktop (`tmux new -s code`), launch the AI agent, then reattach from the Spck CLI terminal on your phone (`tmux attach -t code`). This lets you seamlessly switch between desktop and mobile without losing context. See [Using Tmux](./tmux) for a full guide including persistent remote server setup.

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

On mobile devices, horizontal screen space is limited. The default shell prompt — which typically includes the current directory path, username, and hostname — can crowd the terminal and make it harder to read command output.

Changing your prompt to just `$ ` gives a much cleaner terminal experience on small screens.

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
