# <a name="cli-configuration"></a>CLI 配置

## <a name="configuration"></a>配置

### 配置文件位置

配置存储在项目目录下的 `.spck-editor/config/spck-cli.config.json` 中。

**重要提示**：`.spck-editor/config` 是一个指向 `~/.spck-editor/projects/{project_id}/` 的**符号链接**，可将敏感信息保存在项目目录之外。

### 默认配置

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

### 浏览器代理设置

- **`browserProxy.enabled`**（布尔值）：启用/禁用浏览器代理功能
  - 默认值：`true`
  - 设为 `false` 可阻止移动应用通过 CLI 打开浏览器代理会话

### 终端设置

- **`terminal.enabled`**（布尔值）：启用/禁用终端访问
  - 默认值：`true`
  - 设为 `false` 可降低终端被未授权访问的风险

- **`terminal.maxBufferedLines`**（数字）：最大滚动缓冲行数
  - 默认值：`10000`
  - 影响内存使用（约每 1 万行占用 1MB）

- **`terminal.maxTerminals`**（数字）：最大并发终端会话数
  - 默认值：`10`
  - 每个终端约占用 5-10MB 内存

### 文件系统设置

- **`filesystem.maxFileSize`**（字符串）：读写操作的最大文件大小
  - 默认值：`"10MB"`
  - 可接受值：`"5MB"`、`"50MB"` 等

- **`filesystem.watchIgnorePatterns`**（字符串数组）：文件监视中排除的匹配模式
  - 默认值：忽略构建输出和依赖项
  - 通过避免监视大量生成文件来提升性能

### 安全设置

- **`security.userAuthenticationEnabled`**（布尔值）：启用 Firebase 用户身份验证
  - 默认值：`false`
  - 设为 `false`：延迟较低，兼容 Lite 版本，仍通过签名密钥保护
  - 设为 `true`：额外安全层，用户身份验证，首次连接增加 2-20 秒延迟
  - **无论此设置如何，所有请求始终经过加密签名**

## <a name="security"></a>安全性

### 加密连接

所有通信使用：

- **WSS（WebSocket Secure）**：TLS/SSL 加密
- **HTTPS**：加密初始握手

### 请求签名

每个请求均经过加密签名：

- 密钥在本地生成，从不通过互联网传输
- 建议不要使用第三方二维码扫描器，以免暴露您的密钥

### 最佳实践

1. **保护凭证**：

   ```bash
   # 添加到 .gitignore（设置过程中自动完成）
   echo ".spck-editor/" >> .gitignore
   ```

2. **在共享机器上退出登录**：

   ```bash
   spck --logout
   ```

3. **限制暴露的目录范围**：

   ```bash
   # 避免暴露整个主目录
   spck --root /path/to/specific/project
   ```

4. **不需要时禁用终端**：

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **不需要时禁用浏览器代理**：
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>用户身份验证

Spck CLI 支持可选的 Firebase 用户身份验证，作为始终启用的请求签名之上的第二安全层。

### 工作原理

启用后，CLI 要求您使用 Spck Editor 账号登录。连接通过 Firebase ID 令牌进行身份验证，令牌每小时到期，并使用存储在 `~/.spck-editor/.credentials.json` 中的安全刷新令牌自动续期。

### 启用用户身份验证

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### 权衡对比

|                      | 禁用（默认）     | 启用                             |
| -------------------- | ---------------------- | ----------------------------------- |
| **安全防护**       | 密钥签名     | + Firebase 身份验证    |
| **初始延迟**  | 无身份验证开销       | 首次连接增加 2–20 秒         |
| **Spck Editor Lite** | ✅ 支持           | ❌ 不支持                    |
| **离线使用**      | 无需网络即可工作 | 需要网络进行令牌刷新 |

### 何时启用

**保持禁用（默认）的情况：**

- 使用 **Spck Editor Lite** 时 — Lite 版本不支持 Firebase 登录；将此项设为 `true` 将导致 Lite 用户无法连接
- 在本地网络或可信环境中工作，密钥签名已足够
- 最小化连接延迟是优先考量

**启用的情况：**

- CLI 部署在可通过互联网访问的服务器上
- 需要用户身份验证作为密钥之外的额外访问控制层

> ⚠️ **Spck Editor Lite 不支持 Firebase 身份验证。** 若将 `userAuthenticationEnabled` 设为 `true`，Spck Editor Lite 将无法连接。使用 Lite 版本时请将此设置保持为 `false`。
