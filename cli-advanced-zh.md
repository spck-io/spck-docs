# <a name="cli-advanced-usage"></a>CLI 高级用法

## <a name="cli-commands"></a>CLI 命令

### 基本命令

```bash
# 启动 CLI
spck

# 运行设置向导
spck --setup

# 显示账户信息
spck --account

# 注销并清除凭据
spck --logout

# 显示帮助
spck --help

# 显示版本
spck --version
```

### 高级选项

```bash
# 使用自定义配置文件
spck --config /path/to/config.json
spck -c /path/to/config.json

# 覆盖根目录
spck --root /path/to/project
spck -r /path/to/project

# 覆盖中继服务器（例如使用特定区域）
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>AI 编码代理

Spck CLI 终端提供完整的 shell 访问权限，这意味着您可以直接从移动设备运行 AI 编码代理。这些代理可以在您通过 Spck Editor 监督的同时读取、写入和重构项目代码。

> 💡 **提示**：使用 **tmux** 可以让 AI 代理会话在断开连接后继续运行。在桌面启动 tmux 会话（`tmux new -s code`），启动 AI 代理，然后从手机上的 Spck CLI 终端重新连接（`tmux attach -t code`）。这样您就可以在桌面和移动设备之间无缝切换而不丢失上下文。包含持久远程服务器设置的完整指南，请参见[使用 Tmux](./tmux)。

## <a name="advanced-usage"></a>高级用法

### 多项目

同时为不同项目运行独立的 CLI 实例：

```bash
# 终端 1：项目 A
cd /path/to/projectA
spck

# 终端 2：项目 B
cd /path/to/projectB
spck
```

每个项目维护各自的配置和连接。

> 💡 **提示**：您还可以使用多个 CLI 实例在桌面和手机之间传输文件。请参见[移动设备与桌面之间的文件传输](./cli-file-transfer)获取分步指南。

### 自定义配置文件

为不同场景创建专用配置：

```bash
# 开发配置
spck --config ~/configs/dev-config.json

# 生产配置（只读，无终端）
spck --config ~/configs/prod-config.json
```

### 特定环境设置

**本地开发：**

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

**生产服务器：**

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

### CPU 占用率高

通过添加更多忽略模式来减少文件监视：

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

限制并发终端数量：

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>为移动设备缩短 Shell 提示符

在移动设备上，水平屏幕空间有限。默认的 shell 提示符（通常包含当前目录路径、用户名和主机名）会占用终端空间，使命令输出更难阅读。

将提示符改为简单的 `$ ` 可以在小屏幕上获得更清爽的终端体验。

### Bash

在 `~/.bashrc` 中添加以下内容：

```bash
export PS1='\$ '
```

无需重启 shell 即可应用：

```bash
source ~/.bashrc
```

### Zsh

在 `~/.zshrc` 中添加以下内容：

```zsh
PROMPT='$ '
```

无需重启 shell 即可应用：

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

如果配置文件不存在，请先创建，然后打开：

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

在配置文件中添加以下内容：

```powershell
function prompt { "$ " }
```

无需重启 shell 即可应用：

```powershell
. $PROFILE
```

### 命令提示符 (Windows)

为当前会话设置最简提示符：

```cmd
PROMPT $$
```

要使其永久生效，请通过**控制面板 → 系统 → 高级系统设置 → 环境变量**，将 `PROMPT` 添加为值为 `$$` 的**用户**或**系统**环境变量。
