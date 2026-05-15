# <a name="cli-advanced-usage"></a>Erweiterte CLI-Nutzung

## <a name="cli-commands"></a>CLI-Befehle

### Grundlegende Befehle

```bash
# CLI starten
spck

# Einrichtungsassistenten ausführen
spck --setup

# Kontoinformationen anzeigen
spck --account

# Abmelden und Zugangsdaten löschen
spck --logout

# Hilfe anzeigen
spck --help

# Version anzeigen
spck --version
```

### Erweiterte Optionen

```bash
# Benutzerdefinierte Konfigurationsdatei verwenden
spck --config /path/to/config.json
spck -c /path/to/config.json

# Stammverzeichnis überschreiben
spck --root /path/to/project
spck -r /path/to/project

# Relay-Server überschreiben (z. B. eine bestimmte Region verwenden)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>KI-Coding-Agenten

Das Spck CLI-Terminal bietet vollständigen Shell-Zugriff, sodass du KI-Coding-Agenten direkt von deinem Mobilgerät aus ausführen kannst. Diese Agenten können Code in deinem Projekt lesen, schreiben und umstrukturieren, während du vom Spck Editor aus überwachst.

> 💡 **Tipp**: Verwende **tmux**, damit KI-Agenten-Sitzungen auch nach dem Trennen der Verbindung weiterlaufen. Starte eine tmux-Sitzung auf deinem Desktop (`tmux new -s code`), starte den KI-Agenten, und verbinde dich vom Spck CLI-Terminal auf deinem Telefon wieder damit (`tmux attach -t code`). So wechselst du nahtlos zwischen Desktop und Mobilgerät, ohne den Kontext zu verlieren. Siehe [tmux verwenden](./tmux) für eine vollständige Anleitung einschließlich persistenter Remote-Server-Einrichtung.

## <a name="advanced-usage"></a>Erweiterte Nutzung

### Mehrere Projekte

Separate CLI-Instanzen für verschiedene Projekte gleichzeitig ausführen:

```bash
# Terminal 1: Projekt A
cd /path/to/projectA
spck

# Terminal 2: Projekt B
cd /path/to/projectB
spck
```

Jedes Projekt behält seine eigene Konfiguration und Verbindung.

> 💡 **Tipp**: Du kannst auch mehrere CLI-Instanzen verwenden, um Dateien zwischen Desktop und Telefon zu übertragen. Siehe [Dateiübertragung zwischen Mobilgerät und Desktop](./cli-file-transfer) für eine Schritt-für-Schritt-Anleitung.

### Benutzerdefinierte Konfigurationsdateien

Erstelle spezialisierte Konfigurationen für verschiedene Szenarien:

```bash
# Entwicklungskonfiguration
spck --config ~/configs/dev-config.json

# Produktionskonfiguration (schreibgeschützt, kein Terminal)
spck --config ~/configs/prod-config.json
```

### Umgebungsspezifische Einrichtung

**Lokale Entwicklung:**

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

**Produktionsserver:**

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

### Hohe CPU-Auslastung

Dateiüberwachung durch zusätzliche Ignore-Muster reduzieren:

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

Anzahl gleichzeitiger Terminals begrenzen:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>Shell-Prompt für Mobilgeräte verkleinern

Auf Mobilgeräten ist der horizontale Bildschirmplatz begrenzt. Der Standard-Shell-Prompt – der in der Regel den aktuellen Verzeichnispfad, Benutzernamen und Hostnamen enthält – kann das Terminal überfüllen und die Ausgabe schwerer lesbar machen.

Den Prompt auf `$ ` zu reduzieren sorgt für ein deutlich übersichtlicheres Terminal-Erlebnis auf kleinen Bildschirmen.

### Bash

Folgendes in `~/.bashrc` einfügen:

```bash
export PS1='\$ '
```

Ohne Neustart der Shell anwenden:

```bash
source ~/.bashrc
```

### Zsh

Folgendes in `~/.zshrc` einfügen:

```zsh
PROMPT='$ '
```

Ohne Neustart der Shell anwenden:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

Profildatei erstellen, falls sie noch nicht existiert, und dann öffnen:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Folgendes zum Profil hinzufügen:

```powershell
function prompt { "$ " }
```

Ohne Neustart der Shell anwenden:

```powershell
. $PROFILE
```

### Eingabeaufforderung (Windows)

Minimalen Prompt für die aktuelle Sitzung setzen:

```cmd
PROMPT $$
```

Um dies dauerhaft zu machen, füge `PROMPT` als **Benutzer-** oder **Systemumgebungsvariable** mit dem Wert `$$` über **Systemsteuerung → System → Erweiterte Systemeinstellungen → Umgebungsvariablen** hinzu.
