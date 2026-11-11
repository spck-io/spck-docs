# <a name="getting-started"></a>Getting Started with Spck CLI

## <a name="overview"></a>Overview

Spck CLI is out of beta. Connect your computer to Spck Editor on your phone or tablet to edit files, use Git and terminals, and preview local servers. Connections use an encrypted relay or a direct [Fast Lane](./cli#fast-lane) connection (Supporter and Gold).

## <a name="requirements"></a>Requirements

### Required

- **Node.js**: **22.22.2+ (22.x), 24.15.0+ (24.x), or 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Spck Editor Account**: In the full app, a free account (30 min/day) or Premium subscription (unlimited). **Spck Editor Lite requires a Spck account and an active Spck subscription for Remote Projects.**
- **Spck Editor Mobile App**: [Android](https://play.google.com/store/apps/details?id=io.spck) or [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

Lite supports editing projects on your desktop or a public VM through Spck CLI. This remote service is separate from the one-time Lite app purchase. The subscription helps cover the ongoing hosting, operation, and maintenance costs of Spck's servers. See [Lite Remote Projects](./editor-lite#remote-projects).

### Optional (Recommended)

- **Git**: 2.20.0+ for [Git integration](./git-support#git-limitations-cli) in remote projects
- **ripgrep**: 15.0.0+ for dramatically faster file search (100x improvement)

## <a name="installation"></a>Installation

### Option 1: Run with npx (No Installation)

```bash
npx spck@latest
```

Requests the latest CLI version — ideal for first-time setup or occasional use. Plain `npx spck` can reuse an installed version.

### Option 2: Global Installation

```bash
npm install -g spck
spck
```

Install once, then run `spck` for daily use. Update with `npm install -g spck@latest`. Remote connections still require internet access.

## <a name="demo"></a>Demo

[Watch the Spck CLI promo video](https://youtu.be/EtfEhd5EmKM), including the new Fast Lane feature.

A short walkthrough of connecting Spck CLI to the mobile app and editing local files remotely:

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>First-Time Setup

When you first run the CLI, an interactive setup wizard guides you through:

### 1. Authentication

```bash
spck
# Press ENTER to open browser
# Sign in with your Spck Editor account
# Authorize the CLI
# Return to terminal
```

Credentials are stored in `~/.spck-editor/.credentials.json` and persist across sessions.

If the browser cannot reach localhost, sign-in falls back to the relay. Use the sign-in QR code or manual link printed by the CLI to finish signing in from another device. This sign-in code is separate from the project connection QR code.

### 2. Project Configuration

The wizard will configure:

- **Root directory**: Base directory for file access (default: current directory)
- **Project name**: Display name in the mobile app (default: directory name)

### 3. Git Integration (Optional)

If a `.gitignore` file is detected, the CLI offers to add `.spck-editor/` to prevent committing secrets:

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**Recommendation**: Choose `Y` to protect connection credentials.

### Re-run Setup

To reconfigure at any time:

```bash
spck --setup
```

## <a name="connecting"></a>Connecting to Spck Editor

For a new project, the CLI shows a connection QR code until the first editor connects successfully. Later launches open the dashboard directly; press **`c`** to show the QR code and connection details again. Press **`l`** for logs. Enlarge the terminal if the QR code does not fit.

### Method 1: QR Code (Recommended)

1. Open Spck Editor → **Projects** → **New Project** → **Link Remote Server**
2. Tap the QR code icon
3. Scan the QR code shown in the terminal. The app connects automatically.

> 💡 **Note**: You can also scan the code with your device's Camera app, which opens the link in Spck Editor if the app is installed.

### Method 2: Manual Entry

If you can't scan the QR code:

1. Open Spck Editor → **Projects** → **New Project** → **Link Remote Server**
2. Enter the **Client ID** and **Secret** shown in the terminal
3. Select the relay server shown in the terminal
4. Tap **Connect**

If **Require PIN to connect** is enabled, enter the PIN chosen in the CLI dashboard to finish connecting. The app does not save it. See [Connection PIN](./cli-config#connection-pin).

## <a name="next-steps"></a>Next Steps

1. **Understand the relay system**: Learn how the CLI routes traffic and how to choose a server — see [CLI Reference](./cli)
2. **Configure your setup**: Adjust terminal, security, and filesystem settings — see [Configuration](./cli-config)
3. **Drive a local AI agent from your phone**: Run Claude Code, Codex, or Gemini CLI through Spck Editor's AI Chat using your own subscription — see [AI Coding Agents on Mobile (ACP)](./cli-acp)
4. **Explore power features**: CLI commands, multiple projects, and mobile prompt tips — see [Advanced Usage](./cli-advanced)
5. **Transfer files between devices**: Copy projects between your phone and desktop wirelessly — see [File Transfer](./cli-file-transfer)
6. **Keep sessions alive**: Share sessions across devices with tmux — see [Using Tmux](./tmux)
