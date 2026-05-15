# <a name="cli-reference"></a>CLI Reference

## <a name="key-features"></a>Key Features

- **Remote Filesystem**: Access and edit local files from Spck Editor mobile app
- **Git Integration**: Full git operations (commit, push, pull, branch management) — requires Git 2.20.0+
- **Terminal Access**: Interactive terminal sessions with xterm.js
- **Browser Proxy**: Preview your local server in a full-screen browser view inside Spck Editor
- **Fast Search**: Optimized file search with automatic ripgrep detection (100x faster when installed)
- **Secure**: Cryptographically signed requests with optional Firebase authentication

## <a name="relay-server"></a>Relay Server

The CLI connects to Spck Editor through a relay server that forwards messages between the two. On first run, the CLI automatically selects the relay server with the lowest latency and saves the preference to `~/.spck-editor/.credentials.json`.

**IMPORTANT**: Both the CLI and the Spck Editor client must use the same relay server to connect. If the client cannot find the CLI, verify that both sides have selected the same relay server.

### Available Relay Servers

| Region        | URL                 |
| ------------- | ------------------- |
| Europe        | `cli-eu-1.spck.io`  |
| North America | `cli-na-1.spck.io`  |
| South Asia    | `cli-sas-1.spck.io` |
| East Asia     | `cli-ea-1.spck.io`  |

### Overriding the Relay Server

```bash
# Use a specific relay server
spck --server cli-eu-1.spck.io

# Short form
spck -s cli-na-1.spck.io
```

The override is saved and reused on subsequent runs. To re-run auto-selection, clear your credentials and restart:

```bash
spck --logout
spck
```

### Choosing a Relay Server in Spck Editor

When connecting from the mobile app via **Link Remote Server**, select the same relay server from the **Relay Server** dropdown that the CLI is using. The relay server name is displayed in the CLI output after connecting.

## <a name="daily-workflow"></a>Daily Workflow

### Starting Your Session

```bash
cd /path/to/project
spck
# Connect from mobile app (auto-connects to saved server)
# Start coding
```

### Editing Files

1. Browse files in mobile app
2. Tap to open and edit
3. Files save automatically to your computer

### Running Git Commands

**Option 1 - Mobile App GUI:**

- Open Git panel
- View changes, stage files
- Commit and push

**Option 2 - Terminal:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### Terminal Sessions

Tap the terminal icon in the mobile app for full shell access with your user permissions.

### Ending Your Session

```bash
# Keep CLI running for quick reconnects (recommended)
# Or stop with Ctrl+C
```

## <a name="troubleshooting"></a>Troubleshooting

### Root Directory Not Found

```bash
# Reconfigure with correct path
spck --setup

# Or specify directly
spck --root /correct/path/to/project
```

### Corrupted Configuration

```bash
# Clear settings and start fresh
spck --logout
spck --setup
```

### Connection Issues

1. Check internet connection
2. Verify both the CLI and Spck Editor are using the **same relay server** (shown in CLI output after connecting)
3. Try logging out and reconnecting:
   ```bash
   spck --logout
   spck
   ```
4. Check firewall settings — ensure WebSocket connections (port 443) are allowed

### QR Code Not Scanning

- Verify Spck Editor app is installed before scanning
- Use manual entry: Projects → New Project → Link Remote Server
- Use native Camera app, not third-party scanners

### Git Operations Not Working

1. Verify Git is installed:

   ```bash
   git --version  # Requires 2.20.0+
   ```

2. Install if needed:

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Download from git-scm.com
   ```

### Slow Search Performance

Install ripgrep for 100x faster search:

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI automatically detects and uses ripgrep
```

### Permission Denied

```bash
# View permissions
ls -la /path/to/file

# Fix if needed
chmod 644 /path/to/file

# Don't use sudo - CLI should run as the user who owns the files
```

## <a name="connection-limits"></a>Connection Limits

The maximum number of simultaneous CLI connections and daily usage limits depend on your account type:

| Plan      | CLI Connections | Daily Limit |
| --------- | --------------- | ----------- |
| Free      | 1               | 30 minutes  |
| Supporter | 2               | Unlimited   |
| Gold      | 5               | Unlimited   |

Free tier usage resets daily at 12:00 AM UTC.

When the connection limit is reached:

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

When the daily free tier limit is reached:

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

Check active connections:

```bash
spck --account
```

> 💡 **Note**: Only one mobile device can connect to a CLI instance at a time. Each CLI instance uses one connection slot.

## <a name="support"></a>Support

- **Website**: [https://spck.io](https://spck.io)
- **Support**: Contact through Spck Editor mobile app
