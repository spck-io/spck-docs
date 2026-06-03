# <a name="ai-coding-agents-acp"></a>移动端 AI 编程代理（ACP）

通过 Spck Editor 的 **AI Chat** 直接从手机运行 **Claude Code**、**OpenAI Codex** 或 **Gemini CLI**。Spck CLI 通过开放的 [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) 将您的编辑器与本地安装的代理 CLI 桥接,使模型在您的机器上、使用您的订阅、针对您真实的文件运行——而您从移动设备进行监督。

![Spck Editor 的 AI Chat 中的 ACP 本地 AI 模式,从手机驱动桌面上的 Claude Code](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>什么是 ACP 以及为什么使用它?

Agent Client Protocol (ACP) 是 Zed Industries 推出的、用于编辑器 ↔ AI 代理通信的开放标准,精神上与 Language Server Protocol (LSP) 一致。Spck CLI 0.6.0+ 实现了 ACP,作为 Spck Editor 的 AI Chat(客户端)与您所安装的任何兼容 ACP 的代理二进制(代理)之间的**传输层**。

与应用内通过服务器路由的 AI Chat 相比,本地 ACP 路径给您带来:

- **您自己的订阅** —— 代理调用计入您的 Claude Code / ChatGPT / Gemini 账户,而不是您的 Spck Editor AI 配额。
- **真实的文件系统访问** —— 代理通过 CLI 读写磁盘上的真实文件,而不是编辑器的内存副本。
- **原生工具** —— 文件监视器、语言服务器和 shell 命令在您真实的机器上运行。
- **与桌面的连续性** —— 您在办公桌上使用的同一个 `claude` / `gemini` / `codex` 登录,驱动着移动端聊天。

## <a name="acp-supported-agents"></a>支持的 AI 代理

安装您希望可用的任何代理。Spck CLI 在启动时自动检测它们。

| 代理              | 安装                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>安装与设置

### 1. 安装 Spck CLI

如果您还没有:

```bash
npm install -g spck
# 或不安装而直接运行
npx spck
```

完整的首次运行向导见[开始使用 Spck CLI](./cli-start)。

### 2. 安装一个或多个代理 CLI

选择您希望可用的任何代理。可以安装多个 —— AI Chat 会让您按会话在它们之间选择。安装命令参见上面的[支持的 AI 代理](#acp-supported-agents)表。

### 3. 对每个代理进行一次身份验证

各代理 CLI 在 Spck Editor 之外管理自己的登录:

```bash
claude            # Anthropic Claude Code 登录流程
codex login       # OpenAI Codex 登录流程(由 codex-acp 使用)
gemini            # Google Gemini 登录流程
```

如果跳过此步骤,Spck Editor 在您第一次开始聊天时会弹出类似 `ACP agent requires authentication; run <binary> login and retry` 的错误。

### 4. 启动 Spck CLI

```bash
cd /path/to/your/project
spck
```

启动时,CLI 会按代理打印一份检测报告,列出哪些代理可用,随后在主要功能块中显示一行摘要,例如 `✅ ACP agents: Claude Code, Gemini CLI`。如果没有任何可用的,它将回退到经服务器路由的 AI Chat。

### 5. 连接 Spck Editor

扫描二维码或使用[手动输入](./cli-start#connecting)。连接后,在 Spck Editor 中打开 **AI Chat** —— 传输切换器会将本地代理与云端选项并列显示。

## <a name="acp-authentication"></a>身份验证

每个代理在 Spck CLI 运行的机器上管理自己的凭证。为每个代理运行一次登录流程:

```bash
# Claude Code
claude

# Codex(codex-acp 包装了 Codex CLI 自身的登录)
codex login

# Gemini CLI
gemini
```

如果重装或更换机器,请在新主机上重新登录。身份验证是**按主机、按代理**的 —— Spck Editor 本身从不持有这些凭证。

## <a name="acp-billing"></a>计费与速率限制

由于 ACP 在您的机器上以您自己的凭证运行代理,**所有使用都计入您在该供应商处的账户** —— 而不是您的 Spck Editor 订阅。在此模式下,Spck Editor 和 Spck 中继服务器只充当纯传输,不会为 ACP 流量消耗您应用内的任何 AI 配额。

### Claude Code 计费

> ⚠️ **重要 —— 当 Claude Code 被第三方工具驱动时,会应用单独的速率限制桶。**
>
> 当 Claude Code 通过 ACP 从第三方客户端被调用时,Anthropic 将该流量计入与 Pro / Max 订阅下您的交互式 `claude` CLI 会话**不同的速率限制桶**。实际影响是:您可能在仍有交互式 Claude Code 余量(或反之)时就耗尽了第三方桶,并且无法合并两者。
>
> 在 `claude` 内执行 `/usage`,并在 [Anthropic Console](https://platform.claude.com/usage) 查看当前消耗,适用于您所在套餐的具体数字请参阅 [Claude Code 成本与限制文档](https://code.claude.com/docs/en/costs)。

### Codex(codex-acp)计费

通过 OpenAI Codex CLI 自身的身份验证计费 —— 即您的 OpenAI API 密钥或 ChatGPT 登录。使用量计入该账户所拥有的任何套餐。价格和配额与交互式 `codex` 使用相同;当前数字参见 [openai.com/codex](https://github.com/openai/codex) 与您的 OpenAI 控制台。

### Gemini CLI 计费

通过您的 Google 账户或 Gemini API 密钥计费。使用量计入该登录绑定的 Gemini 套餐或 API 配额。速率限制详情请见 [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits)。

## <a name="acp-configuration"></a>配置

ACP 默认启用,通过项目的 `spck-cli.config.json` 进行配置:

```json
{
  "acp": {
    "enabled": true
  }
}
```

完整的 schema 见[配置 → ACP 设置](./cli-config#acp-settings)。

### 按项目禁用 ACP

如果您不希望 Spck Editor 能在该主机上驱动本地代理:

```json
{
  "acp": {
    "enabled": false
  }
}
```

禁用时,编辑器的传输切换器会隐藏本地代理选项,任何 `acp.*` RPC 会以 `FEATURE_DISABLED` 拒绝。设置向导在首次运行时会询问这个问题(默认 `Y`);早于该选项的配置会自动加载 `acp.enabled: true` 并重新保存。

### 禁用单个代理

要在保持其他代理 ACP 可用的同时阻止 _特定_ 代理被提供,卸载该代理的二进制即可。检测在每次 CLI 启动时运行,因此编辑器的传输切换器会把它从列表中移除。

## <a name="acp-vs-server-routed"></a>本地 ACP vs. 经服务器路由的 AI Chat

| 能力                                       | 经服务器路由(默认,无 CLI)          | 本地(ACP,CLI 已连接)                |
| ------------------------------------------ | ----------------------------------- | --------------------------------------- |
| 模型运行位置                                | Spck 云                             | 您的机器                                |
| 凭证                                        | 您的 Spck Editor 账户               | 代理自己的登录 / API 密钥               |
| 文件访问                                    | 编辑器的内存文件系统                | 通过 CLI 根目录的磁盘真实文件           |
| 计入 Spck Editor AI 配额                    | 是                                  | **否** —— 由代理供应商计费              |
| 无需 CLI 运行即可工作                       | 是                                  | 否(需要 CLI + WebSocket)               |
| 可用代理                                    | Spck 托管的模型                     | Claude Code、Codex、Gemini CLI          |
| 手机上的工具使用权限提示                    | 适用时                              | 是,通过 ACP 转发                       |
| 令牌流                                      | 是                                  | 是                                      |
| 多轮聊天                                    | 是                                  | 是                                      |

您可以在项目中途切换传输 —— AI Chat 会根据 CLI 连接状态与检测到的代理,显示当前可用的路径。

## <a name="acp-tmux"></a>与 Tmux 搭配用于长时间会话

ACP 会话能够跨编辑器重连保持存活,但 Spck CLI 进程本身在其终端关闭时就会结束。对于长时间运行的代理工作 —— 大型重构、数小时的规划会话 —— 请在 [tmux](./tmux) 会话中启动 CLI,以便在 SSH 断开、终端关闭和笔记本休眠后依然存活:

```bash
tmux new -s spck
spck
# Ctrl+B 然后 D 即可分离
```

您还可以从手机通过 Spck CLI 终端重新连接,并使用 `tmux attach -t spck` 实时监控代理。完整的模式(包括将 CLI 作为持久后台服务运行)见[使用 Tmux](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile)。

对于 Linux 主机,[Claude Skill: Linux Service](./claude-skill) 页面提供了将 Spck CLI 作为 `systemd` 服务运行的一键设置,这样 WebSocket —— 以及其上的任何 ACP 会话 —— 在开机时自动启动。

## <a name="acp-faq"></a>常见问题

### 我可以在手机上使用 Claude Code 吗?

可以。在桌面上安装 Claude Code,使用 `claude` 进行身份验证,然后在您的项目中运行 `spck`。从手机连接 Spck Editor,并在 AI Chat 的传输切换器中选择 Claude Code。模型在桌面上以您的订阅运行;您从手机来驱动它。

### Spck Editor 能看到我的 Claude / OpenAI / Gemini API 密钥吗?

不会。每个代理 CLI 在运行 Spck CLI 的机器上管理自己的凭证。ACP 消息通过手机与 CLI 之间加密的 WebSocket 隧道传递,但代理自身的身份验证令牌不会离开您的主机。

### 通过 Spck Editor 使用 Claude Code 会产生额外费用吗?

不会有 Spck Editor 的额外费用。代理的使用计入您的 Anthropic / OpenAI / Google 套餐,与您在办公桌前交互式运行代理完全一致 —— 唯一不同的是,Anthropic 对第三方客户端应用单独的速率限制桶;参见上文[计费与速率限制](#acp-billing)。

### 使用 ACP 需要付费的 Spck Editor 订阅吗?

不需要。免费层(每天 30 分钟 CLI 连接)足以驱动任何 ACP 代理。只有应用内经服务器路由的 AI Chat 才会消耗 Spck Editor AI 配额。

### 如果我在聊天中途断开 Wi-Fi 会怎样?

代理进程在 CLI 主机上继续存活。当编辑器重新连接时,会话以完整的聊天历史恢复。您离线期间到达的流式输出会在重连时回放。

### 我可以在远程服务器而不是笔记本上运行代理吗?

可以。在任何可达的 Linux/macOS 主机上运行 Spck CLI —— 开发 VM、家庭服务器、工作站 —— 并通过中继服务器连接到它。搭配 [tmux](./tmux) 或 [systemd skill](./claude-skill),以在连接之间保持 CLI 存活。

### ACP 在 Spck Editor Lite 中可用吗?

可以。ACP 流量使用与文件系统和 git 相同的 WebSocket 传输,Spck Editor Lite 支持该传输。请确保在 CLI 配置中将 `security.userAuthenticationEnabled` 设为 `false` —— Lite 不支持 Firebase 身份验证。参见[配置 → 用户身份验证](./cli-config#user-authentication)。

### 为什么我的代理没出现在 AI Chat 中?

检查 CLI 启动日志中按代理的行:

- 代理未被检测到 —— 安装它(参见[支持的 AI 代理](#acp-supported-agents))。
- 已检测到但在编辑器中缺失 —— 确认您已完成代理自己的登录流程(`claude`、`codex login`、`gemini`)。
- ACP 已禁用 —— 检查 `.spck-editor/config/spck-cli.config.json` 中的 `acp.enabled`。参见[配置](./cli-config#acp-settings)。

## <a name="acp-troubleshooting"></a>故障排查

### 代理已检测但会话无法启动

通常意味着代理未通过身份验证。在 CLI 主机上运行代理的登录流程:

```bash
claude              # 然后完成浏览器认证
codex login
gemini
```

如果问题仍存在,查看 CLI 在 `.spck-editor/logs/` 下的日志中代理的 stderr 输出,通常会指向失败的认证或二进制。

### 聊天过程中出现速率限制错误

对于 Claude Code,编辑器会逐字呈现 Anthropic 的 429。请查看 [Anthropic Console 用量页](https://platform.claude.com/usage)与 [Claude Code 成本文档](https://code.claude.com/docs/en/costs) —— 记住第三方速率限制桶与您的交互式 `claude` 配额是分开的。

对于 Codex 与 Gemini,编辑器会呈现各自供应商的配额错误。请通过供应商控制台解决。

### 启动 ACP 会话时 CLI 崩溃

Spck CLI 将 ACP 流量记录在 `.spck-editor/logs/`。在重现问题时跟踪最新的日志文件:

```bash
tail -f .spck-editor/logs/spck-*.log
```

请在 [github.com/spck-editor](https://github.com/spck-editor) 提交 bug,并附上相关片段。

### 代理在项目根目录之外做了更改

ACP 代理被限定在 CLI 配置的 `root` 目录内。如果您看到写入出现在它之外,请提交 issue —— 这不应发生。作为临时解决方法,运行 `spck --root /path/to/specific/project` 进一步缩小范围。

## <a name="acp-see-also"></a>另见

- [开始使用 Spck CLI](./cli-start) —— 首次安装、身份验证与连接
- [CLI 参考](./cli) —— 中继服务器、日常工作流、连接限制
- [配置 → ACP 设置](./cli-config#acp-settings) —— `acp.enabled` 配置选项
- [高级用法](./cli-advanced) —— CLI 标志、多项目、移动端提示词技巧
- [使用 Tmux](./tmux) —— 跨重连保持 ACP 会话存活
- [Claude Skill: Linux Service](./claude-skill) —— 将 Spck CLI 作为 `systemd` 服务运行,使 ACP 始终可用
- [Agent Client Protocol 规范](https://agentclientprotocol.com/) —— ACP 实现的开放标准
- [Claude Code 文档](https://docs.claude.com/en/docs/claude-code/overview)
- [Gemini CLI 仓库](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
