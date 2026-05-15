# <a name="getting-started"></a>Getting Started with Spck CLI

## <a name="overview"></a>Overview

Spck CLI is a command-line tool that connects your local development environment to the Spck Editor mobile app over a secure WebSocket connection. Once running, you can browse and edit local files, run terminal commands, and preview local servers — all from your phone or tablet.

## <a name="requirements"></a>Requirements

### Required

- **Node.js**: 18.0.0 or higher
- **Spck Editor Account**: Free account (30 min/day) or Premium subscription (unlimited)
- **Spck Editor Mobile App**: [Android](https://play.google.com/store/apps/details?id=io.spck) or [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Optional (Recommended)

- **Git**: 2.20.0+ for git integration features
- **ripgrep**: 15.0.0+ for dramatically faster file search (100x improvement)

## <a name="installation"></a>Installation

### Option 1: Run with npx (No Installation)

```bash
npx spck
```

Always uses the latest version — perfect for first-time setup or occasional use.

### Option 2: Global Installation

```bash
npm install -g spck
spck
```

Faster startup, works offline, and convenient for daily use.

## <a name="demo"></a>Demo

A short walkthrough of connecting Spck CLI to the mobile app and editing local files remotely:

<img src="https://docs.spck.io/assets/gifs/remote-cli-preview.gif" alt="Spck CLI demo" width="100%" />

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

Once the CLI is running, it displays a QR code and connection details.

### Method 1: QR Code (Recommended)

**IMPORTANT**: Install Spck Editor app BEFORE scanning the QR code.

**On Android:**

1. Use Camera app or Quick Settings QR scanner
2. When detected, tap the notification to open Spck Editor
3. App automatically connects

> 💡 **Note**: Some QR code scanners cannot handle the custom scheme to open Spck Editor directly. Copy the URL and paste it in Chrome, which will launch Spck Editor from the URL.

**On iOS:**

1. Use Camera app or Control Center QR scanner
2. When detected, tap the notification to open Spck Editor
3. App automatically connects

> 💡 **Note**: Spck Editor does NOT have a built-in QR scanner. Use your device's native QR capability.

### Method 2: Manual Entry

If the QR code doesn't work:

1. Open Spck Editor → **Projects** → **New Project** → **Link Remote Server**
2. Enter the **Client ID** and **Secret** shown in the terminal
3. Tap **Connect**

## <a name="next-steps"></a>Next Steps

1. **Understand the relay system**: Learn how the CLI routes traffic and how to choose a server — see [CLI Reference](./cli)
2. **Configure your setup**: Adjust terminal, security, and filesystem settings — see [Configuration](./cli-config)
3. **Explore power features**: CLI commands, AI coding agents, multiple projects — see [Advanced Usage](./cli-advanced)
4. **Transfer files between devices**: Copy projects between your phone and desktop wirelessly — see [File Transfer](./cli-file-transfer)
5. **Keep sessions alive**: Share sessions across devices with tmux — see [Using Tmux](./tmux)
