# <a name="cli-reference"></a>CLI-Referenz

## <a name="key-features"></a>Hauptfunktionen

- **Remote-Dateisystem**: Zugriff auf und Bearbeitung lokaler Dateien über die Spck Editor Mobile-App
- **Git-Integration**: Vollständige Git-Operationen (Commit, Push, Pull, Branch-Verwaltung) — erfordert Git 2.20.0+
- **Terminal-Zugang**: Interaktive Terminal-Sitzungen mit xterm.js
- **Browser-Proxy**: Vorschau Ihres lokalen Servers in einer Vollbild-Browseransicht innerhalb von Spck Editor
- **Schnelle Suche**: Optimierte Dateisuche mit automatischer ripgrep-Erkennung (100x schneller wenn installiert)
- **Lokale KI-Coding-Agenten (ACP)**: Steuern Sie Claude Code, Codex oder Gemini CLI aus dem KI-Chat von Spck Editor über das [Agent Client Protocol](https://agentclientprotocol.com/). Der Agent läuft auf Ihrem Rechner mit Ihrem eigenen Abonnement. Siehe [KI-Coding-Agenten auf dem Handy (ACP)](./cli-acp).
- **Fast Lane** (Supporter & Gold): Direkte Peer-to-Peer-WebRTC-Verbindung zwischen Spck Editor und der CLI, im Durchschnitt doppelt so schnell wie der Relay-Server. Siehe [Fast Lane](#fast-lane).
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

## <a name="fast-lane"></a>Fast Lane

Fast Lane ist eine Premium-Funktion für **Supporter**- und **Gold**-Abonnenten. Statt jede Nachricht über den Relay-Server zu leiten, verbindet sich Spck Editor per WebRTC (Peer-to-Peer) **direkt mit Ihrer CLI**. Da der Umweg über den Relay-Server entfällt und weniger Round-Trips nötig sind, ist Fast Lane **im Durchschnitt doppelt so schnell wie der Relay-Server**, sodass sich Dateivorgänge, Suche, Git und Terminal-Eingaben spürbar flüssiger anfühlen.

Der Relay-Server wird weiterhin benötigt: Dort ist Ihre CLI registriert, und er vermittelt den anfänglichen Handshake zwischen dem Editor und der CLI. Sobald der direkte Pfad steht, fließen Ihre Projektdaten über ihn statt über den Relay-Server.

### Voraussetzungen

- Ein aktives **Supporter**- oder **Gold**-Abonnement für das Konto, mit dem die CLI angemeldet ist
- Spck CLI **0.7.0 oder neuer** (`npm i -g spck`)
- WebRTC-Unterstützung sowohl auf dem Gerät mit Spck Editor als auch auf dem Rechner, auf dem die CLI läuft

### Fast Lane ein- oder ausschalten

**In Spck Editor:** Öffnen Sie **Link Remote Server** (oder bearbeiten Sie eine bestehende Verbindung über das Menü) und verwenden Sie den Schalter **⚡ Fast Lane**. Für neue Verbindungen mit Supporter- und Gold-Konten ist er standardmäßig aktiviert.

**In der CLI:** Fast Lane ist standardmäßig aktiviert. Drücken Sie im CLI-Dashboard **`f`**, um es für das aktuelle Projekt umzuschalten, oder setzen Sie `fastLane.enabled` in der [Projektkonfiguration](./cli-config#fast-lane-settings). Änderungen werden nach einem Neustart der CLI wirksam. Schalten Sie es in Netzwerken aus, die Peer-to-Peer-Verkehr blockieren.

Das CLI-Dashboard zeigt den aktuellen Fast-Lane-Status an (aktiv, verfügbar, ausgeschaltet oder auf dieser Plattform nicht verfügbar). Das Dateien-Panel in Spck Editor zeigt, welcher Transportweg verwendet wird, zusammen mit dem aktuellen Ping, z. B. `Fast Lane · 24 ms` oder `Relay · 80 ms`.

### Automatischer Fallback

Wenn keine direkte Verbindung hergestellt werden kann, wechselt Spck Editor automatisch zum Relay-Server, damit Sie weiterarbeiten können, und zeigt einen Hinweis mit der Ursache an. Häufige Gründe:

- Die CLI ist veraltet — aktualisieren Sie sie mit `npm i -g spck`
- Fast Lane ist in der Projektkonfiguration der CLI ausgeschaltet
- WebRTC ist auf dem Rechner mit der CLI oder auf Ihrem Gerät nicht verfügbar
- Der Relay-Server unterstützt Fast Lane noch nicht
- Das Netzwerk blockiert einen direkten Peer-to-Peer-Pfad (z. B. durch eine strenge Firmen-Firewall oder NAT)

### Sicherheit

Der Fast-Lane-Verkehr wird von WebRTC (DTLS) Ende-zu-Ende verschlüsselt. Zusätzlich ist der Authentifizierungs-Handshake der CLI an die jeweilige DTLS-Sitzung gebunden: Die CLI muss auf genau diesem Kanal nachweisen, dass sie Ihr Verbindungsgeheimnis kennt, bevor Projektdaten ausgetauscht werden. Alle Anfragen werden weiterhin kryptografisch signiert, genau wie über den Relay-Server. Siehe [CLI-Sicherheit](./cli-config#security).

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
5. Wenn ein Hinweis erscheint, dass Fast Lane nicht verfügbar ist und stattdessen der Relay-Server verwendet wird, funktioniert die Verbindung weiterhin über den Relay-Server. Ursachen und Lösungen finden Sie unter [Fast Lane](#fast-lane) im Abschnitt „Automatischer Fallback“

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

Lite unterstützt Remote-Projekte auf Ihrem Desktop oder einer öffentlichen VM über Spck CLI. Dafür sind ein **Spck-Konto und ein aktives Spck-Abonnement** erforderlich, zusätzlich zum einmaligen Lite-Kauf. Das Abonnement hilft, die laufenden Kosten für Hosting, Betrieb und Wartung der Spck-Server zu decken. Die enthaltenen lokalen Editor- und Git-Werkzeuge bleiben ohne Abonnement nutzbar.

Die maximale Anzahl gleichzeitiger CLI-Verbindungen und tägliche Nutzungslimits hängen von Ihrem Kontotyp ab:

| Plan      | CLI-Verbindungen | Tageslimit  | Fast Lane |
| --------- | ---------------- | ----------- | --------- |
| Free      | 1                | 30 Minuten  | —         |
| Supporter | 2                | Unbegrenzt  | ✓         |
| Gold      | 5                | Unbegrenzt  | ✓         |

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
