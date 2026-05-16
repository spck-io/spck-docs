---
name: spck-cli-service
description: Install, manage, and troubleshoot the Spck CLI (`spck`) as a systemd user or system service on Linux so it auto-starts on boot and restarts on failure. Use this skill when the user asks to run `spck` as a service/daemon, keep the Spck CLI alive across reboots, set up a persistent remote development server, or diagnose a failing `spck-cli.service` unit.
---

# Spck CLI Linux Service

This skill helps the user install the Spck CLI (`spck`) as a `systemd` service so it starts on boot and restarts automatically on failure. Prefer a **user service** (`systemctl --user`) when possible — it does not require `sudo`, runs as the actual user that owns the project files, and keeps credentials in the user's `$HOME`. Fall back to a **system service** only when the user explicitly needs the CLI to start before login (e.g. on a headless server with `loginctl enable-linger` not viable).

## When to use this skill

Trigger this skill when the user asks to:

- Run `spck` as a service, daemon, or background process on Linux.
- Make the Spck CLI start automatically on boot.
- Keep the Spck CLI running after the SSH session ends (and `tmux`/`screen` is not preferred).
- Restart the Spck CLI automatically if it crashes.
- Debug a `spck-cli.service` that fails to start or keeps restarting.

Do **not** use this skill for macOS (use `launchd`) or Windows (use Task Scheduler / NSSM) — say so and stop.

## Prerequisites — verify before writing any unit file

Run these checks first and report what you find. Do not invent values.

1. **OS is Linux with systemd**:
   ```bash
   uname -s && ps -p 1 -o comm=
   ```
   Expect `Linux` and `systemd`. If not systemd, stop and tell the user.

2. **`spck` is installed and resolvable**:
   ```bash
   command -v spck || npm ls -g --depth=0 | grep spck
   ```
   Capture the **absolute path** to the `spck` binary — never use bare `spck` in `ExecStart`, systemd does not inherit the user's `$PATH`.

3. **Node.js is on a stable path** (only relevant if `spck` was installed via `nvm`):
   ```bash
   which node
   readlink -f "$(which node)"
   ```
   If the path contains `/.nvm/versions/node/`, warn the user: nvm-installed binaries live under a version-specific path that changes on every Node upgrade. Recommend either (a) installing Node from the distro package manager or NodeSource, or (b) symlinking `node` and `spck` into `/usr/local/bin`.

4. **Project root exists and is owned by the target user**:
   ```bash
   ls -ld "<project-path>"
   ```
   The `User=` in the unit must match the file owner, otherwise `spck` will hit permission errors when watching files.

5. **`spck` has been configured at least once interactively** (`spck --setup` or first run). The service unit runs non-interactively — if `~/.spck-editor/.credentials.json` does not exist, the service will fail. Confirm:
   ```bash
   test -f ~/.spck-editor/.credentials.json && echo "configured" || echo "run 'spck' once first"
   ```

## Decide: user service vs system service

Ask the user (or infer from context) which one to install:

| | User service | System service |
|---|---|---|
| Runs as | The logged-in user | A user you specify via `User=` |
| Starts on boot without login? | Only with `loginctl enable-linger <user>` | Yes, always |
| Needs `sudo`? | No | Yes |
| Unit file location | `~/.config/systemd/user/spck-cli.service` | `/etc/systemd/system/spck-cli.service` |
| Manage with | `systemctl --user ...` | `sudo systemctl ...` |
| Logs | `journalctl --user -u spck-cli` | `sudo journalctl -u spck-cli` |

**Default to user service** unless the user has a clear reason for system-wide. If you pick user service on a headless server, also run `sudo loginctl enable-linger <username>` so it starts at boot without an active login session.

## Generate the unit file

Fill in `SPCK_BIN`, `PROJECT_DIR`, and (system service only) `USERNAME` from the prerequisite checks. Do not leave placeholders.

### User service — `~/.config/systemd/user/spck-cli.service`

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/PROJECT_DIR
ExecStart=SPCK_BIN
Restart=on-failure
RestartSec=5
# Environment is minimal under systemd — pass anything spck or node need:
Environment=NODE_ENV=production
# Optional: cap restart storms (5 restarts in 60s, then stop trying)
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

Install and start:

```bash
mkdir -p ~/.config/systemd/user
# (write the file above to ~/.config/systemd/user/spck-cli.service)
systemctl --user daemon-reload
systemctl --user enable --now spck-cli
# On a headless server, also run (one-time, requires sudo):
sudo loginctl enable-linger "$USER"
```

### System service — `/etc/systemd/system/spck-cli.service`

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=USERNAME
Group=USERNAME
WorkingDirectory=/home/USERNAME/PROJECT_DIR
ExecStart=SPCK_BIN
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=multi-user.target
```

Install and start:

```bash
sudo tee /etc/systemd/system/spck-cli.service > /dev/null <<'EOF'
# (paste the unit file here)
EOF
sudo systemctl daemon-reload
sudo systemctl enable --now spck-cli
```

## Verify it is running

```bash
# User service
systemctl --user status spck-cli
journalctl --user -u spck-cli -n 50 --no-pager

# System service
sudo systemctl status spck-cli
sudo journalctl -u spck-cli -n 50 --no-pager
```

Confirm in the logs that the CLI printed its connection banner and the relay server name. If you see the banner, the service is healthy — tell the user to connect from the Spck Editor mobile app using the same relay server shown in the logs.

## Common failure modes — check these before changing the unit

1. **`status=203/EXEC` or `No such file or directory`** — `ExecStart` points at a path that does not exist. Re-run `command -v spck` as the target `User=`; the path may differ from the user who ran `sudo systemctl`.
2. **Service starts, then immediately exits clean (`status=0`)** — `spck` has not been configured. Run `spck --setup` interactively as the target user, then `systemctl restart`.
3. **`Permission denied` reading project files** — `User=` does not own `WorkingDirectory`. Either change `User=`, `chown` the project, or switch to a user service.
4. **Restart loop hitting `start-limit-hit`** — the underlying error is in the prior log entries before the limit kicked in. Read `journalctl -u spck-cli` without `-f`.
5. **User service does not start on boot** — `loginctl enable-linger <user>` was not set. Without it, user services only run while the user has an active login session.
6. **`spck` upgraded via npm and service broke** — if `which spck` resolves to a versioned nvm path, the symlink may have moved. Re-resolve the binary path and update `ExecStart`.
7. **Multiple CLI connection slot warnings** — the user is on the Free tier (1 connection) and another `spck` is already running. `systemctl stop` the duplicate or upgrade.

## Updating the unit file later

After editing the unit file:

```bash
# User service
systemctl --user daemon-reload && systemctl --user restart spck-cli

# System service
sudo systemctl daemon-reload && sudo systemctl restart spck-cli
```

`daemon-reload` is required after **every** edit to the unit file. `restart` alone re-runs the old definition.

## Uninstall

```bash
# User service
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload

# System service
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```
