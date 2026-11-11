# <a name="getting-started"></a>Spck CLI 入门

## <a name="overview"></a>概述

Spck CLI 已正式发布。将电脑连接到手机或平板上的 Spck Editor，即可编辑文件、使用 Git 和终端，以及预览本地服务器。连接使用加密中继，或 [Fast Lane](./cli#fast-lane) 点对点直连（Supporter 和 Gold）。

## <a name="requirements"></a>要求

Lite 支持通过 Spck CLI 编辑桌面电脑或公共虚拟机上的项目。远程项目需要 **Spck 账户和有效的 Spck 订阅**，不包含在 Lite 的一次性购买中。订阅有助于承担 Spck 服务器持续产生的托管、运行和维护费用。随 Lite 提供的本地编辑和 Git 工具仍可无需订阅使用。

### 必需

- **Node.js**：**22.22.2+ (22.x), 24.15.0+ (24.x), 或 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Spck Editor 账户**：免费账户（30 分钟/天）或 Premium 订阅（无限制）
- **Spck Editor 移动应用**：[Android](https://play.google.com/store/apps/details?id=io.spck) 或 [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### 可选（推荐）

- **Git**：远程项目的 [Git 集成](./git-support#git-limitations-cli)需要 2.20.0 或更高版本
- **ripgrep**：15.0.0 以上（文件搜索速度显著提升，提高 100 倍）

## <a name="installation"></a>安装

### 选项 1：使用 npx 运行（无需安装）

```bash
npx spck@latest
```

请求最新的 CLI 版本，适合首次设置或偶尔使用。`npx spck` 可能复用已安装的版本。

### 选项 2：全局安装

```bash
npm install -g spck
spck
```

安装一次后，日常直接运行 `spck`。使用 `npm install -g spck@latest` 更新。远程连接仍需要互联网。

## <a name="demo"></a>演示

[观看 Spck CLI 宣传视频](https://youtu.be/EtfEhd5EmKM)，了解新的 Fast Lane 功能。

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

如果浏览器无法访问 localhost，将通过中继完成登录。可使用 CLI 显示的登录二维码或链接在其他设备上登录。登录二维码与项目连接二维码不同。

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

新项目会显示连接二维码，直到编辑器首次成功连接。之后启动时直接打开仪表盘；按 **`c`** 再次显示二维码和连接信息，按 **`l`** 查看日志。如果二维码放不下，请扩大终端窗口。

### 方法 1：二维码（推荐）

1. 打开 Spck Editor → **项目** → **新建项目** → **链接远程服务器**
2. 点击二维码图标
3. 扫描终端中显示的二维码。应用会自动连接。

> 💡 **注意**：您也可以用设备的相机应用扫描二维码；如果已安装应用，链接会在 Spck Editor 中打开。

### 方法 2：手动输入

如果无法扫描二维码：

1. 打开 Spck Editor → **项目** → **新建项目** → **链接远程服务器**
2. 输入终端中显示的**客户端 ID** 和**密钥**
3. 选择终端中显示的中继服务器
4. 点击**连接**

如果启用了 **Require PIN to connect**，请输入在 CLI 仪表盘设置的 PIN。应用不会保存 PIN。参见[连接 PIN](./cli-config#connection-pin)。

## <a name="next-steps"></a>后续步骤

1. **了解中继系统**：了解 CLI 如何路由流量以及如何选择服务器——参见 [CLI 参考](./cli)
2. **配置设置**：调整终端、安全和文件系统设置——参见[配置](./cli-config)
3. **探索高级功能**：CLI 命令、AI 编码代理、多项目管理——参见[高级用法](./cli-advanced)
4. **在设备间传输文件**：无线复制手机和桌面之间的项目——参见[文件传输](./cli-file-transfer)
5. **保持会话活跃**：使用 tmux 在设备间共享会话——参见[使用 Tmux](./tmux)
