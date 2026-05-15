# <a name="cli-file-transfer"></a>File Transfer Between Mobile and Desktop

## <a name="overview"></a>Overview

When you run the Spck CLI on your desktop, it acts as a sync hub between your desktop file system and the local projects stored on your phone. Both sides appear side-by-side in the Spck Editor file manager — your phone's local projects on the left and your desktop's files as a connected remote server — and you can copy files or entire folders between them in either direction using the standard copy and paste commands.

No Airdrop, Bluetooth, USB cable, or third-party cloud storage is required. Transfers are encrypted end-to-end over a WebSocket connection and stay on your local Wi-Fi when both devices are on the same network.

## <a name="how-it-works"></a>How It Works

The CLI exposes your desktop directory as a remote server project in the Spck Editor file manager. Local projects saved on your phone are stored in the app's local storage. Spck Editor treats both as first-class project locations, so any file operation that works within a single project — including copy and paste — also works across them.

```
Phone (local storage)          Desktop (via CLI)
─────────────────────          ─────────────────────
my-project/               ↔   ~/projects/my-project/
  ├── index.html                 ├── index.html
  ├── style.css                  ├── style.css
  └── assets/                    └── assets/
      └── logo.png                   └── logo.png
```

Directories are transferred recursively — all files inside are copied, with subdirectories created automatically on the destination.

## <a name="desktop-to-mobile"></a>Desktop to Mobile

Use this when you want to bring files from your computer onto your phone — for example, to work offline, share a project with a colleague who only has the mobile app, or take a snapshot of your work onto the device.

1. **Start the CLI** on your desktop, pointing at the folder you want to transfer from:

   ```bash
   spck --root ~/projects
   ```

2. **Connect your phone** by scanning the QR code with your camera app and opening the link in Spck Editor.

3. In Spck Editor, your desktop folder appears as a remote server project in the **Projects** panel.

4. **Long-press the file or folder** you want in the remote project, then tap **Copy**.

5. **Navigate to a local project** on your phone (or create a new one via **New Project**).

6. **Long-press the destination folder**, then tap **Paste**.

The files are downloaded from your desktop and saved to your phone's local storage.

## <a name="mobile-to-desktop"></a>Mobile to Desktop

Use this when you want to push work from your phone back to your desktop — for example, after editing on the go, or to consolidate projects created on the device.

1. **Start the CLI** on your desktop, pointing at the folder where you want the files to land:

   ```bash
   spck --root ~/Desktop/from-phone
   ```

2. **Connect your phone** by scanning the QR code.

3. In Spck Editor, open the **local project** on your phone that contains the files you want to send.

4. **Long-press the file or folder** you want, then tap **Copy**.

5. **Navigate to the remote desktop project** in the **Projects** panel.

6. **Long-press the destination folder**, then tap **Paste**.

The files are read from your phone's local storage and written to your desktop via the CLI.

## <a name="transferring-projects"></a>Transferring Entire Projects

You can copy a whole project folder in one paste operation. Long-press the project root in the file tree and select **Copy**, then navigate to the destination and **Paste**. The entire directory tree — including all files in all subdirectories — is transferred.

This is useful for:

- **Backing up a mobile project to your desktop** before making large changes
- **Seeding a new phone project** from an existing desktop codebase
- **Merging work** from multiple devices into one location

## <a name="tips"></a>Tips

### File Size Limit

The default maximum file size is **10 MB** per file. To transfer larger files such as images, archives, or compiled binaries, increase the limit in your CLI config:

```json
{
  "filesystem": {
    "maxFileSize": "200MB"
  }
}
```

See [CLI Configuration](./cli-config) for full details.

### Transfer Speed

Speed depends entirely on your local Wi-Fi or internet connection. For large directories, transfers run file by file, so overall throughput scales with the number of files. On a typical home Wi-Fi network, small text-heavy projects (hundreds of files) complete in a few seconds.

### Security

All transfers are encrypted over WSS (WebSocket Secure) and every request is signed with a per-session secret key. The relay server forwards messages between devices but never receives unencrypted content. See [CLI Security](./cli-config#security) for full details.

### Running Multiple Transfers

The CLI exposes a single root directory. To transfer from multiple locations simultaneously, run separate CLI instances in different terminals:

```bash
# Terminal 1: expose ~/projects
spck --root ~/projects

# Terminal 2: expose ~/Documents
spck --root ~/Documents
```

Each instance generates its own QR code and connection, and both remote servers appear in the Spck Editor **Projects** panel at the same time.
