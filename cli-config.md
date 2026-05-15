# <a name="cli-configuration"></a>CLI Configuration

## <a name="configuration"></a>Configuration

### Configuration File Location

Configuration is stored in `.spck-editor/config/spck-cli.config.json` in your project directory.

**Important**: `.spck-editor/config` is a **symlink** to `~/.spck-editor/projects/{project_id}/`, keeping secrets outside your project directory.

### Default Configuration

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### Browser Proxy Settings

- **`browserProxy.enabled`** (boolean): Enable/disable the browser proxy feature
  - Default: `true`
  - Set to `false` to prevent the mobile app from opening a browser proxy session through the CLI

### Terminal Settings

- **`terminal.enabled`** (boolean): Enable/disable terminal access
  - Default: `true`
  - Set to `false` to reduce risk of unauthorized access to your terminal

- **`terminal.maxBufferedLines`** (number): Maximum scrollback buffer
  - Default: `10000`
  - Affects memory usage (~1MB per 10k lines)

- **`terminal.maxTerminals`** (number): Maximum concurrent terminal sessions
  - Default: `10`
  - Each terminal uses ~5-10MB memory

### Filesystem Settings

- **`filesystem.maxFileSize`** (string): Maximum file size for read/write
  - Default: `"10MB"`
  - Accepts: `"5MB"`, `"50MB"`, etc.

- **`filesystem.watchIgnorePatterns`** (string[]): Patterns to exclude from file watching
  - Default: Ignores build outputs and dependencies
  - Improves performance by avoiding thousands of generated files

### Security Settings

- **`security.userAuthenticationEnabled`** (boolean): Enable Firebase user authentication
  - Default: `false`
  - When `false`: Lower latency, compatible with Lite, still protected by secret signing
  - When `true`: Extra security layer, user identity verification, adds 2-20s initial latency
  - **All requests are always cryptographically signed regardless of this setting**

## <a name="security"></a>Security

### Encrypted Connections

All communication uses:

- **WSS (WebSocket Secure)**: TLS/SSL encryption
- **HTTPS**: Encrypted initial handshake

### Request Signing

Every request is cryptographically signed:

- Secret key generated locally, never transmitted over the internet
- Recommend against using 3rd party QR scanners which may expose your secret key

### Best Practices

1. **Protect credentials**:

   ```bash
   # Add to .gitignore (automatic during setup)
   echo ".spck-editor/" >> .gitignore
   ```

2. **Logout on shared machines**:

   ```bash
   spck --logout
   ```

3. **Limit exposed directories**:

   ```bash
   # Instead of entire home directory
   spck --root /path/to/specific/project
   ```

4. **Disable terminal if not needed**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **Disable browser proxy if not needed**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>User Authentication

Spck CLI supports optional Firebase user authentication as a second security layer on top of the always-active request signing.

### How It Works

When enabled, the CLI requires you to sign in with your Spck Editor account. Connections are authenticated using Firebase ID tokens that expire every hour and are automatically refreshed using secure refresh tokens stored in `~/.spck-editor/.credentials.json`.

### Enabling User Authentication

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### Trade-offs

|                      | Disabled (default)     | Enabled                             |
| -------------------- | ---------------------- | ----------------------------------- |
| **Protection**       | Secret signing key     | + Firebase identity verification    |
| **Initial latency**  | No auth overhead       | Adds 2–20s on first connect         |
| **Spck Editor Lite** | ✅ Supported           | ❌ Not supported                    |
| **Offline use**      | Works without internet | Requires internet for token refresh |

### When to Enable

**Keep disabled (default) when:**

- Using **Spck Editor Lite** — Firebase login is not supported in Lite; setting this to `true` will prevent Lite users from connecting
- Working on a local network or trusted environment where the secret signing key is sufficient
- Minimizing connection latency is a priority

**Enable when:**

- The CLI is exposed on a server accessible over the internet
- You want user identity verification as an additional access control layer beyond the signing key

> ⚠️ **Spck Editor Lite does not support Firebase authentication.** If `userAuthenticationEnabled` is set to `true`, Spck Editor Lite cannot connect. Keep this setting at `false` when using Lite.
