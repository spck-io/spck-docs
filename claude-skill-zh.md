# <a name="claude-skill"></a>Claude 技能：将 Spck CLI 作为 Linux 服务运行

本页提供一个可下载的 [Claude Code 技能](https://docs.claude.com/en/docs/claude-code/skills)，用于自动化在 Linux 上将 Spck CLI（`spck`）安装为 `systemd` 服务的过程。安装技能后，你可以让 Claude Code "将 spck 作为服务运行"，它会检查你的环境、生成填入实际绝对路径的正确 unit 文件、安装并验证其是否正常运行——无需从清单中复制粘贴命令。

该技能自动化了与 [使用 Tmux → 替代方案：Linux 服务](./tmux#linux-service) 中描述的相同 systemd 配置，并加入了手动编写 unit 文件时容易遗漏的预检检查和失败诊断。

## <a name="download"></a>下载

下载技能文件并保存到本地 Claude Code 技能目录：

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

或手动下载：<a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a>——放置到 `~/.claude/skills/spck-cli-service/SKILL.md`。

## <a name="what-the-skill-does"></a>技能的作用

被调用时，技能引导 Claude Code 完成完整安装：

1. 验证主机是运行 `systemd` 的 Linux。
2. 解析 `spck` 的绝对路径（避免导致 `ExecStart` 失效的 `PATH` 不匹配）。
3. 如果 `node` 通过 `nvm` 安装则发出警告——这些路径在每次 Node 升级时都会变化，并静默地破坏 unit。
4. 确认 `~/.spck-editor/.credentials.json` 存在（CLI 必须在作为服务运行之前至少以交互方式运行一次）。
5. 根据需求在**用户服务**（`systemctl --user`，无需 `sudo`）和**系统服务**之间选择。
6. 写入填入实际路径的 unit 文件——无占位符。
7. 执行 `daemon-reload`、`enable --now`，然后追踪 journal 以确认 CLI 已连接到中继服务器。

技能还记录了七种最常见的故障模式（错误的 `ExecStart` 路径、缺少凭证、项目目录权限错误、触发 `start-limit-hit` 的重启循环、npm 升级后的过期 nvm 路径等），以便 Claude Code 能够诊断损坏的服务而不是简单地重新生成 unit 文件。

## <a name="installation"></a>安装

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**第 1 步 — 下载技能文件：**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**第 2 步 — 验证 Claude Code 已识别它：**

```bash
claude /skills
```

你应该在列表中看到 `spck-cli-service`。如果没有，重启 Claude Code 让它重新扫描技能目录。

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop 在 macOS 和 Linux 上从同一个 `~/.claude/skills/` 目录加载技能。在 Windows 上，路径是 `%USERPROFILE%\.claude\skills\`——但技能本身只在 Linux 主机上工作，因此请将其安装在你想运行 `spck` 的机器上，而不是运行 Claude Desktop 的机器上。

如果你管理的是远程 Linux 服务器，请在该服务器上通过 SSH 运行 Claude Code（或通过 Spck CLI 终端，它为服务器提供完整的 shell 访问）。在本地 Mac 上安装技能无法帮助配置远程 Linux 服务。

</div>
  </div>
</div>

## <a name="usage"></a>使用方法

安装后，用自然语言向 Claude Code 发出请求来调用技能。可以触发技能的示例：

- "将 spck 安装为 systemd 服务"
- "让 Spck CLI 开机自启"
- "我的 spck-cli.service 一直在重启，你能调试一下吗？"
- "将 spck 作为守护进程运行，这样 SSH 断开后也能继续工作"

Claude Code 会读取技能，执行预检（会提示你批准每个命令），然后生成并安装 unit 文件。在批准前审查每个命令——特别是在 `sudo` 下写入 `/etc/systemd/system/` 的命令。

## <a name="what-gets-installed"></a>安装内容

技能安装一个单独的 unit 文件。用户服务的文件路径为：

```bash
~/.config/systemd/user/spck-cli.service
```

内容类似：

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

对于系统服务，文件位于 `/etc/systemd/system/spck-cli.service`，并添加 `User=` 和 `Group=` 指令。技能根据你的环境选择正确的变体，并将实际绝对路径写入文件。

## <a name="why-a-skill-instead-of-copy-paste"></a>为什么用技能而不是复制粘贴？

[tmux 文档](./tmux#linux-service)中的 unit 文件只是起点，但服务要真正正常工作需要几件事都正确：

- `ExecStart` 必须是 `spck` 的**绝对路径**。在登录 shell 中执行 `which spck` 会解析 `.bashrc` 中的 PATH 操作，但 systemd 看不到这些。
- 如果 `spck` 通过 `nvm` 安装，路径中嵌入了 Node 版本——升级 Node 会静默地破坏服务，直到下次重启。
- CLI 必须至少以交互方式运行一次才能创建 `~/.spck-editor/.credentials.json`。没有凭证的全新服务启动会干净地退出，没有明显错误。
- `User=` 必须拥有 `WorkingDirectory`，否则文件监视会遇到 `EACCES` 并导致 CLI 进入重启循环。
- 用户服务在无头服务器上需要 `loginctl enable-linger`，否则只有在登录会话活跃时才会运行。

技能将这些全部自动化，这样你就不必记住这些细节。

## <a name="uninstall"></a>卸载

禁用并删除服务：

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

对于系统服务：

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

从 Claude Code 中删除技能本身：

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>另请参阅

- [使用 Tmux](./tmux) — 使用 `tmux` 在 SSH 断开时保持 CLI 运行的替代方法。
- [高级用法](./cli-advanced) — 完整的 CLI 命令参考、配置覆盖和多项目设置。
- [配置](./cli-config) — unit 文件未涵盖的终端、文件系统、安全和认证设置。
