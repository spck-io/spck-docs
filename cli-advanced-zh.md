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

### 仪表板

在交互式终端中，CLI 会打开全屏仪表盘。新项目在首次成功连接前显示二维码，之后启动时进入主视图。仪表盘显示已连接的编辑器、延迟、Relay/Fast Lane 状态和可用工具。输出重定向或作为服务运行时，使用普通文本日志。

| 视图 | 按键 |
|------|------|
| 主视图 | `l` 日志，`c` 连接二维码，`m` 管理终端，`q` `q` 退出 |
| 设置（主视图） | `t` 终端，`b` 浏览器代理，`a` AI 代理，`s` 语言服务器，`u` 用户验证，`f` Fast Lane，`w` 保持计算机唤醒, `p` 精简 Shell 提示符，`i` 连接时要求 PIN |
| 日志 | `↑` `↓` / `j` `k` 滚动，`PgUp` `PgDn` 翻页，`←` `→` 左右移动长行，`g` `G` 第一行 / 最后一行，`Esc` 返回 |
| 终端 | `↑` `↓` / `j` `k` 选择，`x` `x` 终止（或移除已退出的终端），`Esc` 返回 |
| 二维码 | `c` / `Esc` 返回 |

`Ctrl+L` 重绘屏幕，`Ctrl+C` 可从任意视图退出。CLI 断开连接期间再次按 `Ctrl+C` 会立即退出。

## <a name="ai-coding-agents"></a>AI 编程助手 (ACP)

Spck CLI 通过 [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) 将 Spck Editor 的 AI 聊天与本地安装的 AI 编程助手（**Claude Code**、**Codex** 或 **Gemini CLI**）连接起来。模型在您的本地机器上以您自己的订阅运行，编辑磁盘上的真实文件，并将权限请求转发到您的手机。

![Spck Editor 的 AI 聊天本地 AI 模式从手机驱动 Claude Code](https://docs.spck.io/assets/gifs/acp-ai.gif)

→ **[移动端 AI 编程助手 (ACP)](./cli-acp)** — 完整指南：支持的智能体、安装、计费与速率限制（包括 Anthropic 对第三方 Claude Code 单独的配额）、配置、常见问题和故障排查。

> 💡 **提示**：使用 **tmux** 可以让 AI 智能体会话在断开连接后继续运行。在桌面启动 tmux 会话（`tmux new -s code`），启动智能体，然后从手机上的 Spck CLI 终端重新连接（`tmux attach -t code`）。同时适用于普通 shell 智能体和 ACP 模式智能体。包含持久远程服务器设置的完整指南，请参见[使用 Tmux](./tmux)。

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

Spck CLI 默认在 Bash、Zsh 和 Fish 中使用精简提示符：`folder $`，root 用户显示 `folder #`，主目录显示 `~`。在仪表盘按 **`p`** 或设置 **`terminal.compactPrompt`** 即可切换，对新终端生效。不会修改 Shell 配置文件。参见[精简提示符](./cli-config#compact-prompt)。

对于其他 Shell，或关闭内置精简提示符后需要自定义格式时，可使用下面的手动设置示例。

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
