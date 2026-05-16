# <a name="claude-skill"></a>Claude Skill: Spck CLI als Linux-Dienst ausführen

Diese Seite stellt eine herunterladbare [Claude Code-Skill](https://docs.claude.com/en/docs/claude-code/skills) bereit, die die Installation von Spck CLI (`spck`) als `systemd`-Dienst unter Linux automatisiert. Mit installierter Skill kannst du Claude Code bitten, „spck als Dienst auszuführen", und Claude Code prüft dann deine Umgebung, generiert eine korrekte Unit-Datei mit deinen absoluten Pfaden, installiert sie und verifiziert, dass sie läuft — ohne manuelles Kopieren von Befehlen aus einer Checkliste.

Die Skill kodiert dasselbe systemd-Setup wie unter [Tmux verwenden → Alternative: Linux-Dienst](./tmux#linux-service) beschrieben, plus die Vorab-Prüfungen und Fehlerdiagnosen, die beim manuellen Schreiben der Unit-Datei leicht übersehen werden.

## <a name="download"></a>Herunterladen

Lade die Skill-Datei herunter und speichere sie im lokalen Claude Code-Skills-Verzeichnis:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

Oder manuell herunterladen: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — unter `~/.claude/skills/spck-cli-service/SKILL.md` ablegen.

## <a name="what-the-skill-does"></a>Was die Skill tut

Bei Aufruf führt die Skill Claude Code durch die vollständige Installation:

1. Prüft, ob der Host Linux mit `systemd` ist.
2. Ermittelt den absoluten Pfad zu `spck` (vermeidet den `PATH`-Konflikt, der `ExecStart` zum Scheitern bringt).
3. Warnt, wenn `node` via `nvm` installiert ist — diese Pfade ändern sich bei jedem Node-Upgrade und machen den Dienst lautlos kaputt.
4. Bestätigt, dass `~/.spck-editor/.credentials.json` vorhanden ist (die CLI muss mindestens einmal interaktiv ausgeführt worden sein, bevor sie als Dienst läuft).
5. Wählt zwischen einem **Benutzerdienst** (`systemctl --user`, kein `sudo`) und einem **Systemdienst** je nach Bedarf.
6. Schreibt die Unit-Datei mit deinen echten Pfaden ausgefüllt — keine Platzhalter.
7. Führt `daemon-reload`, `enable --now` aus und verfolgt anschließend das Journal, um zu bestätigen, dass die CLI mit dem Relay-Server verbunden ist.

Die Skill dokumentiert außerdem die sieben häufigsten Fehlermodi (falscher `ExecStart`-Pfad, fehlende Credentials, Berechtigungsfehler im Projektverzeichnis, Restart-Loops mit `start-limit-hit`, veraltete nvm-Pfade nach npm-Upgrade usw.), sodass Claude Code einen defekten Dienst diagnostizieren kann, anstatt die Unit-Datei einfach neu zu generieren.

## <a name="installation"></a>Installation

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Schritt 1 — Skill-Datei herunterladen:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Schritt 2 — Prüfen, ob Claude Code die Skill erkannt hat:**

```bash
claude /skills
```

`spck-cli-service` sollte in der Liste erscheinen. Falls nicht, Claude Code neu starten, damit das Skills-Verzeichnis erneut gescannt wird.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop lädt Skills aus demselben Verzeichnis `~/.claude/skills/` unter macOS und Linux. Unter Windows lautet der Pfad `%USERPROFILE%\.claude\skills\` — aber die Skill selbst funktioniert nur auf Linux-Hosts. Installiere sie also auf dem Rechner, auf dem `spck` laufen soll, nicht auf dem Rechner mit Claude Desktop.

Wenn du einen Remote-Linux-Server verwaltest, führe Claude Code per SSH auf diesem Server aus (oder über das Spck CLI-Terminal, das der Shell des Servers vollständigen Zugriff gewährt). Die Installation der Skill auf einem lokalen Mac hilft nicht dabei, einen Remote-Linux-Dienst zu konfigurieren.

</div>
  </div>
</div>

## <a name="usage"></a>Verwendung

Nach der Installation kannst du die Skill aufrufen, indem du Claude Code in normaler Sprache bittest. Beispiele, die sie auslösen:

- „Installiere spck als systemd-Dienst"
- „Lass Spck CLI beim Systemstart starten"
- „Mein spck-cli.service startet ständig neu, kannst du das debuggen?"
- „Führe spck als Daemon aus, damit es meine SSH-Trennung überlebt"

Claude Code liest die Skill, führt die Vorab-Prüfungen durch (du wirst gebeten, jeden Befehl zu genehmigen) und generiert und installiert dann die Unit-Datei. Überprüfe jeden Befehl vor der Genehmigung — insbesondere jene, die unter `sudo` in `/etc/systemd/system/` schreiben.

## <a name="what-gets-installed"></a>Was installiert wird

Die Skill installiert eine einzelne Unit-Datei. Bei einem Benutzerdienst lautet der Pfad:

```bash
~/.config/systemd/user/spck-cli.service
```

Mit folgendem Inhalt:

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

Bei einem Systemdienst liegt die Datei unter `/etc/systemd/system/spck-cli.service` und enthält zusätzliche `User=`- und `Group=`-Direktiven. Die Skill wählt die richtige Variante basierend auf deiner Umgebung und trägt die tatsächlichen absoluten Pfade in die Datei ein.

## <a name="why-a-skill-instead-of-copy-paste"></a>Warum eine Skill statt Copy-Paste?

Die Unit-Datei in der [tmux-Dokumentation](./tmux#linux-service) ist ein Ausgangspunkt, aber mehrere Dinge müssen korrekt sein, damit der Dienst tatsächlich funktioniert:

- `ExecStart` muss der **absolute Pfad** zu `spck` sein. `which spck` innerhalb einer Login-Shell löst PATH-Manipulationen aus `.bashrc` auf, die systemd nicht sieht.
- Wenn `spck` unter `nvm` installiert wurde, enthält der Pfad die Node-Version — ein Node-Upgrade macht den Dienst lautlos kaputt bis zum nächsten Neustart.
- Die CLI muss mindestens einmal interaktiv ausgeführt worden sein, um `~/.spck-editor/.credentials.json` zu erstellen. Ein frischer Dienststart ohne Credentials endet sauber ohne offensichtliche Fehlermeldung.
- `User=` muss das `WorkingDirectory` besitzen, sonst trifft die Dateiüberwachung auf `EACCES` und die CLI startet in einer Schleife neu.
- Benutzerdienste benötigen `loginctl enable-linger` auf kopflosen Servern, sonst laufen sie nur während einer aktiven Login-Sitzung.

Die Skill kodiert all das, damit du es dir nicht merken musst.

## <a name="uninstall"></a>Deinstallation

Dienst deaktivieren und entfernen:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

Für einen Systemdienst:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Um die Skill selbst aus Claude Code zu entfernen:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>Siehe auch

- [Tmux verwenden](./tmux) — alternativer Ansatz mit `tmux`, um die CLI bei SSH-Trennungen am Laufen zu halten.
- [Erweiterte Nutzung](./cli-advanced) — vollständige CLI-Befehlsreferenz, Konfigurationsüberschreibungen und Multi-Projekt-Setups.
- [Konfiguration](./cli-config) — Terminal-, Dateisystem-, Sicherheits- und Authentifizierungseinstellungen, die die Unit-Datei nicht abdeckt.
