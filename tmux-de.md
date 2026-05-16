# <a name="tmux"></a>Tmux mit Spck CLI verwenden

Tmux (Terminal-Multiplexer) ermöglicht es, Terminal-Sitzungen unabhängig von dem Fenster oder der SSH-Verbindung weiterlaufen zu lassen, die sie gestartet hat. Für Spck-CLI-Nutzer bedeutet das: Sitzungen bleiben nach einer Verbindungsunterbrechung erhalten, eine laufende Agent-Sitzung lässt sich zwischen Desktop und Mobilgerät teilen, und die CLI läuft dauerhaft auf einem Remote-Server weiter — auch wenn die SSH-Verbindung getrennt wird.

## <a name="installation"></a>Installation

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux läuft nativ unter Linux. Unter Windows verwende das [Windows-Subsystem für Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install) und installiere tmux dann innerhalb von WSL.

**Schritt 1 — WSL installieren (PowerShell als Administrator):**

```powershell
wsl --install
```

**Schritt 2 — Ein WSL-Terminal öffnen und tmux installieren:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Anwendungsfall 1: Agent-Sitzungen zwischen Desktop und Mobilgerät teilen

Der wirkungsvollste tmux-Workflow mit Spck CLI besteht darin, einen KI-Coding-Agenten auf dem Desktop zu starten und ihn nahtlos vom Mobilgerät aus weiterzuführen — oder umgekehrt. Beide Clients sehen exakt den gleichen Terminal-Zustand einschließlich des vollständigen Scrollback-Verlaufs.

### Sitzung auf dem Desktop starten

Eine benannte tmux-Sitzung erstellen:

```bash
tmux new -s code
```

Den KI-Agenten innerhalb der Sitzung starten:

```bash
claude
```

Der Agent läuft innerhalb von tmux. Mit **Strg+B** und anschließend **D** kann die Sitzung jederzeit getrennt werden — die Sitzung und alles, was darin läuft, läuft im Hintergrund weiter.

### Vom Mobilgerät verbinden

1. Spck Editor öffnen und mit dem CLI-Server verbinden
2. Ein Terminal aus dem Spck Editor-Terminal-Panel öffnen
3. Die laufende tmux-Sitzung verbinden:

```bash
tmux attach -t code
```

Das Terminal sieht genauso aus wie auf dem Desktop — einschließlich des laufenden Agenten, seiner Ausgabe und des vollständigen Scrollback-Verlaufs. Mehrere Clients können gleichzeitig verbunden sein und die Live-Ausgabe sehen.

### Zurück zum Desktop wechseln

Jederzeit von einem beliebigen Terminal aus neu verbinden:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Anwendungsfall 2: Dauerhaft laufende CLI auf einem Remote-Server

Wenn Spck CLI auf einem Remote-Server über SSH betrieben wird, stoppt die CLI sobald die SSH-Sitzung endet — egal ob der Laptop zugeklappt wird, die WLAN-Verbindung abbricht oder die Verbindung durch einen Timeout unterbrochen wird. Tmux hält den Prozess auf dem Server am Laufen, unabhängig vom Verbindungsstatus.

### Einrichtung auf dem Remote-Server

Per SSH auf den Server verbinden und eine benannte tmux-Sitzung starten, bevor die CLI gestartet wird:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

Die CLI läuft jetzt innerhalb von tmux auf dem Server. Die SSH-Verbindung kann geschlossen werden — oder vollständig unterbrochen sein — und die CLI läuft weiter.

### Nach einer Verbindungsunterbrechung neu verbinden

```bash
ssh user@your-server.com
tmux attach -t spck
```

Die CLI macht genau da weiter, wo sie aufgehört hat. Mobilclients können sich über den Relay-Server normal neu verbinden.

### Laufende Sitzungen auflisten

```bash
tmux ls
```

## <a name="linux-service"></a>Alternative: Linux-Dienst

Für ein vollständig automatisiertes Setup, das die CLI beim Systemstart ohne manuelle tmux-Verwaltung startet, kann Spck CLI als systemd-Dienst betrieben werden.

### Dienstdatei erstellen

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

`your-username` und `/path/to/your/project` durch die tatsächlichen Werte ersetzen. Falls `spck` global installiert wurde (`npm install -g spck`), `ExecStart` durch die Ausgabe von `which spck` ersetzen.

### Aktivieren und starten

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Status und Protokolle prüfen

```bash
# Status anzeigen
sudo systemctl status spck-cli

# Live-Protokoll verfolgen
journalctl -u spck-cli -f
```

Der Dienst startet automatisch bei jedem Neustart und startet sich selbst neu, wenn der Prozess abstürzt.

## <a name="essential-tmux-commands"></a>Wichtige Tmux-Befehle

| Befehl | Aktion |
| --- | --- |
| `tmux new -s name` | Neue benannte Sitzung erstellen |
| `tmux attach -t name` | An eine bestehende Sitzung anhängen |
| `tmux ls` | Alle Sitzungen auflisten |
| `tmux kill-session -t name` | Eine Sitzung beenden |
| Ctrl+B, D | Von Sitzung trennen (läuft weiter) |
| Ctrl+B, C | Neues Fenster erstellen |
| Ctrl+B, N | Zum nächsten Fenster wechseln |
| Ctrl+B, P | Zum vorherigen Fenster wechseln |
| Ctrl+B, [ | Scrollmodus aktivieren (Pfeiltasten / BildAuf / BildAb) |
| Q | Scrollmodus beenden |
