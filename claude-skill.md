# <a name="claude-skill"></a>Claude Skill: Run Spck CLI as a Linux Service

This page provides a downloadable [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) that automates installing the Spck CLI (`spck`) as a `systemd` service on Linux. With the skill installed, you can ask Claude Code to "run spck as a service" and it will check your environment, generate a correct unit file with your absolute paths, install it, and verify it is running — without you copy-pasting commands from a checklist.

The skill encodes the same systemd setup described in [Using Tmux → Alternative: Linux Service](./tmux#linux-service), plus the pre-flight checks and failure-mode diagnostics that are easy to miss when writing the unit file by hand.

## <a name="download"></a>Download

Download the skill file and save it to your local Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

Or download manually: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — place it at `~/.claude/skills/spck-cli-service/SKILL.md`.

## <a name="what-the-skill-does"></a>What the Skill Does

When invoked, the skill walks Claude Code through the full install:

1. Verifies the host is Linux running `systemd`.
2. Resolves the absolute path to `spck` (avoids the `PATH` mismatch that breaks `ExecStart`).
3. Warns if `node` is installed via `nvm` — those paths change on every Node upgrade and silently break the unit.
4. Confirms `~/.spck-editor/.credentials.json` exists (the CLI must be configured interactively at least once before running as a service).
5. Picks between a **user service** (`systemctl --user`, no `sudo`) and a **system service** based on your needs.
6. Writes the unit file with your real paths filled in — no placeholders.
7. Runs `daemon-reload`, `enable --now`, then tails the journal to confirm the CLI connected to the relay server.

The skill also documents the seven most common failure modes (wrong `ExecStart` path, missing credentials, permission errors on the project directory, restart loops hitting `start-limit-hit`, stale nvm paths after npm upgrade, etc.) so Claude Code can diagnose a broken service instead of just regenerating the unit file.

## <a name="installation"></a>Installation

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Step 1 — Download the skill file:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Step 2 — Verify Claude Code picked it up:**

```bash
claude /skills
```

You should see `spck-cli-service` in the list. If not, restart Claude Code so it rescans the skills directory.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop loads skills from the same `~/.claude/skills/` directory on macOS and Linux. On Windows, the path is `%USERPROFILE%\.claude\skills\` — but the skill itself only works on Linux hosts, so install it on the machine you want to run `spck` on, not on the machine running Claude Desktop.

If you are managing a remote Linux server, run Claude Code over SSH on that server (or via the Spck CLI terminal, which exposes a full shell to the server). Installing the skill on a local Mac will not help configure a remote Linux service.

</div>
  </div>
</div>

## <a name="usage"></a>Usage

Once installed, invoke the skill by asking Claude Code in plain language. Examples that will trigger it:

- "Install spck as a systemd service"
- "Make the Spck CLI start on boot"
- "My spck-cli.service keeps restarting, can you debug it?"
- "Run spck as a daemon so it survives my SSH disconnect"

Claude Code will read the skill, run the pre-flight checks (which will prompt you to approve each command), and then generate and install the unit file. Review each command before approving — particularly the ones that write to `/etc/systemd/system/` under `sudo`.

## <a name="what-gets-installed"></a>What Gets Installed

The skill installs a single unit file. For a user service, that is:

```bash
~/.config/systemd/user/spck-cli.service
```

With contents like:

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

For a system service, the file lives at `/etc/systemd/system/spck-cli.service` and adds `User=` and `Group=` directives. The skill picks the right variant based on your environment and writes the actual absolute paths into the file.

## <a name="why-a-skill-instead-of-copy-paste"></a>Why a Skill Instead of Copy-Paste?

The unit file in the [tmux docs](./tmux#linux-service) is a starting point, but several things have to be right for the service to actually work:

- `ExecStart` must be the **absolute path** to `spck`. `which spck` inside a login shell will resolve PATH manipulations from `.bashrc` that systemd does not see.
- If `spck` was installed under `nvm`, the path embeds the Node version — upgrading Node breaks the service silently until next reboot.
- The CLI must have been run interactively at least once to create `~/.spck-editor/.credentials.json`. A fresh service start with no credentials exits cleanly with no obvious error.
- `User=` must own the `WorkingDirectory`, otherwise file-watch hits `EACCES` and the CLI restart-loops.
- User services need `loginctl enable-linger` on headless servers, otherwise they only run while a login session is active.

The skill encodes all of this so you do not have to remember it.

## <a name="uninstall"></a>Uninstall

Disable and remove the service:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

For a system service:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

To remove the skill itself from Claude Code:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>See Also

- [Using Tmux](./tmux) — alternative approach using `tmux` for keeping the CLI alive across SSH disconnects.
- [Advanced Usage](./cli-advanced) — full CLI command reference, configuration overrides, and multi-project setups.
- [Configuration](./cli-config) — terminal, filesystem, security, and authentication settings the unit file does not cover.
