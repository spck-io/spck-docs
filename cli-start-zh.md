# <a name="getting-started"></a>Spck CLI 入门

## <a name="overview"></a>概述

Spck CLI 是一个命令行工具，通过安全的 WebSocket 连接将本地开发环境连接到 Spck Editor 移动应用。启动后，您可以在手机或平板电脑上浏览和编辑本地文件、运行终端命令以及预览本地服务器。

## <a name="requirements"></a>要求

### 必需

- **Node.js**：18.0.0 或更高版本
- **Spck Editor 账户**：免费账户（30 分钟/天）或 Premium 订阅（无限制）
- **Spck Editor 移动应用**：[Android](https://play.google.com/store/apps/details?id=io.spck) 或 [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### 可选（推荐）

- **Git**：2.20.0 以上（用于 Git 集成功能）
- **ripgrep**：15.0.0 以上（文件搜索速度显著提升，提高 100 倍）

## <a name="installation"></a>安装

### 选项 1：使用 npx 运行（无需安装）

```bash
npx spck
```

始终使用最新版本，非常适合首次设置或偶尔使用。

### 选项 2：全局安装

```bash
npm install -g spck
spck
```

启动更快，支持离线使用，便于日常使用。

## <a name="demo"></a>演示

以下是一段简短的演示，展示如何将 Spck CLI 连接到移动应用并远程编辑本地文件：

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>首次设置

首次运行 CLI 时，交互式设置向导将引导您完成以下步骤：

### 1. 身份验证

```bash
spck
# 按 ENTER 打开浏览器
# 使用 Spck Editor 账户登录
# 授权 CLI
# 返回终端
```

凭据存储在 `~/.spck-editor/.credentials.json` 中，会在会话间持久保存。

### 2. 项目配置

向导将配置：

- **根目录**：文件访问的基础目录（默认：当前目录）
- **项目名称**：在移动应用中显示的名称（默认：目录名称）

### 3. Git 集成（可选）

如果检测到 `.gitignore` 文件，CLI 将提示是否添加 `.spck-editor/` 以防止意外提交敏感信息：

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**建议**：选择 `Y` 以保护连接凭据。

### 重新运行设置

随时重新配置：

```bash
spck --setup
```

## <a name="connecting"></a>连接到 Spck Editor

CLI 运行后会显示二维码和连接详情。

### 方法 1：二维码（推荐）

**重要**：扫描二维码**之前**请先安装 Spck Editor 应用。

**在 Android 上：**

1. 使用相机应用或快捷设置中的二维码扫描仪
2. 检测到后，点击通知打开 Spck Editor
3. 应用自动连接

> 💡 **注意**：部分二维码扫描仪无法处理直接打开 Spck Editor 的自定义协议。请复制 URL 并粘贴到 Chrome 中，Chrome 会通过该 URL 启动 Spck Editor。

**在 iOS 上：**

1. 使用相机应用或控制中心中的二维码扫描仪
2. 检测到后，点击通知打开 Spck Editor
3. 应用自动连接

> 💡 **注意**：Spck Editor **没有**内置二维码扫描仪。请使用设备的原生二维码功能。

### 方法 2：手动输入

如果二维码无法使用：

1. 打开 Spck Editor → **项目** → **新建项目** → **链接远程服务器**
2. 输入终端中显示的**客户端 ID** 和**密钥**
3. 点击**连接**

## <a name="next-steps"></a>后续步骤

1. **了解中继系统**：了解 CLI 如何路由流量以及如何选择服务器——参见 [CLI 参考](./cli)
2. **配置设置**：调整终端、安全和文件系统设置——参见[配置](./cli-config)
3. **探索高级功能**：CLI 命令、AI 编码代理、多项目管理——参见[高级用法](./cli-advanced)
4. **在设备间传输文件**：无线复制手机和桌面之间的项目——参见[文件传输](./cli-file-transfer)
5. **保持会话活跃**：使用 tmux 在设备间共享会话——参见[使用 Tmux](./tmux)
