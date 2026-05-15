# <a name="cli-reference"></a>CLI-Referenz

## <a name="key-features"></a>Hauptfunktionen

- **Remote-Dateisystem**: Zugriff auf und Bearbeitung lokaler Dateien über die Spck Editor Mobile-App
- **Git-Integration**: Vollständige Git-Operationen (Commit, Push, Pull, Branch-Verwaltung) — erfordert Git 2.20.0+
- **Terminal-Zugang**: Interaktive Terminal-Sitzungen mit xterm.js
- **Browser-Proxy**: Vorschau Ihres lokalen Servers in einer Vollbild-Browseransicht innerhalb von Spck Editor
- **Schnelle Suche**: Optimierte Dateisuche mit automatischer ripgrep-Erkennung (100x schneller wenn installiert)
- **Sicher**: Kryptographisch signierte Anfragen mit optionaler Firebase-Authentifizierung

## <a name="relay-server"></a>Relay-Server

Die CLI verbindet sich über einen Relay-Server mit Spck Editor, der Nachrichten zwischen beiden weiterleitet. Beim ersten Start wählt die CLI automatisch den Relay-Server mit der niedrigsten Latenz und speichert die Einstellung in `~/.spck-editor/.credentials.json`.

**WICHTIG**: Sowohl die CLI als auch der Spck Editor-Client müssen denselben Relay-Server verwenden, um sich zu verbinden. Wenn der Client die CLI nicht finden kann, überprüfen Sie, ob beide Seiten denselben Relay-Server ausgewählt haben.

### Verfügbare Relay-Server

| Region        | URL                 |
| ------------- | ------------------- |
| Europa        | `cli-eu-1.spck.io`  |
| Nordamerika   | `cli-na-1.spck.io`  |
| Südasien      | `cli-sas-1.spck.io` |
| Ostasien      | `cli-ea-1.spck.io`  |

### Relay-Server überschreiben

```bash
# Einen bestimmten Relay-Server verwenden
spck --server cli-eu-1.spck.io

# Kurzform
spck -s cli-na-1.spck.io
```

Die Überschreibung wird gespeichert und bei nachfolgenden Starts wiederverwendet. Um die automatische Auswahl erneut durchzuführen, löschen Sie Ihre Anmeldedaten und starten Sie neu:

```bash
spck --logout
spck
```

### Relay-Server in Spck Editor auswählen

Wenn Sie sich über die Mobile-App via **Link Remote Server** verbinden, wählen Sie denselben Relay-Server aus der **Relay Server**-Dropdown-Liste, den die CLI verwendet. Der Name des Relay-Servers wird in der CLI-Ausgabe nach dem Verbinden angezeigt.

## <a name="daily-workflow"></a>Täglicher Workflow

### Sitzung starten

```bash
cd /path/to/project
spck
# Über Mobile-App verbinden (verbindet sich automatisch mit gespeichertem Server)
# Mit dem Programmieren beginnen
```

### Dateien bearbeiten

1. Dateien in der Mobile-App durchsuchen
2. Tippen zum Öffnen und Bearbeiten
3. Dateien werden automatisch auf Ihrem Computer gespeichert

### Git-Befehle ausführen

**Option 1 - Mobile-App-GUI:**

- Git-Panel öffnen
- Änderungen anzeigen, Dateien stagen
- Committen und pushen

**Option 2 - Terminal:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### Terminal-Sitzungen

Tippen Sie auf das Terminal-Symbol in der Mobile-App für vollen Shell-Zugriff mit Ihren Benutzerberechtigungen.

### Sitzung beenden

```bash
# CLI laufen lassen für schnelle Wiederverbindungen (empfohlen)
# Oder mit Ctrl+C stoppen
```

## <a name="troubleshooting"></a>Fehlerbehebung

### Stammverzeichnis nicht gefunden

```bash
# Mit korrektem Pfad neu konfigurieren
spck --setup

# Oder direkt angeben
spck --root /correct/path/to/project
```

### Beschädigte Konfiguration

```bash
# Einstellungen löschen und neu beginnen
spck --logout
spck --setup
```

### Verbindungsprobleme

1. Internetverbindung prüfen
2. Überprüfen, ob sowohl die CLI als auch Spck Editor denselben **Relay-Server** verwenden (wird in der CLI-Ausgabe nach dem Verbinden angezeigt)
3. Versuchen Sie, sich abzumelden und neu zu verbinden:
   ```bash
   spck --logout
   spck
   ```
4. Firewall-Einstellungen prüfen — stellen Sie sicher, dass WebSocket-Verbindungen (Port 443) erlaubt sind

### QR-Code lässt sich nicht scannen

- Überprüfen Sie, ob die Spck Editor-App vor dem Scannen installiert ist
- Manuelle Eingabe verwenden: Projects → New Project → Link Remote Server
- Native Kamera-App verwenden, keine Drittanbieter-Scanner

### Git-Operationen funktionieren nicht

1. Überprüfen Sie, ob Git installiert ist:

   ```bash
   git --version  # Erfordert 2.20.0+
   ```

2. Bei Bedarf installieren:

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Download von git-scm.com
   ```

### Langsame Suchleistung

Installieren Sie ripgrep für 100x schnellere Suche:

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI erkennt und verwendet ripgrep automatisch
```

### Zugriff verweigert

```bash
# Berechtigungen anzeigen
ls -la /path/to/file

# Bei Bedarf korrigieren
chmod 644 /path/to/file

# Verwenden Sie nicht sudo - CLI sollte als der Benutzer laufen, dem die Dateien gehören
```

## <a name="connection-limits"></a>Verbindungslimits

Die maximale Anzahl gleichzeitiger CLI-Verbindungen und tägliche Nutzungslimits hängen von Ihrem Kontotyp ab:

| Plan      | CLI-Verbindungen | Tageslimit  |
| --------- | ---------------- | ----------- |
| Free      | 1                | 30 Minuten  |
| Supporter | 2                | Unbegrenzt  |
| Gold      | 5                | Unbegrenzt  |

Das kostenlose Kontingent wird täglich um 12:00 Uhr UTC zurückgesetzt.

Wenn das Verbindungslimit erreicht ist:

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

Wenn das tägliche kostenlose Limit erreicht ist:

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

Aktive Verbindungen prüfen:

```bash
spck --account
```

> 💡 **Hinweis**: Nur ein Mobilgerät kann sich gleichzeitig mit einer CLI-Instanz verbinden. Jede CLI-Instanz belegt einen Verbindungsslot.

## <a name="support"></a>Support

- **Website**: [https://spck.io](https://spck.io)
- **Support**: Kontakt über die Spck Editor Mobile-App
