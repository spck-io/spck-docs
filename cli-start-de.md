# <a name="getting-started"></a>Erste Schritte mit Spck CLI

## <a name="overview"></a>Überblick

Spck CLI ist nicht mehr in der Beta. Verbinden Sie Ihren Computer mit Spck Editor auf dem Smartphone oder Tablet, um Dateien zu bearbeiten, Git und Terminals zu nutzen und lokale Server anzuzeigen. Die Verbindung erfolgt über einen verschlüsselten Relay-Server oder direkt mit [Fast Lane](./cli#fast-lane) (Supporter und Gold).

## <a name="requirements"></a>Voraussetzungen

Lite unterstützt Remote-Projekte auf Ihrem Desktop oder einer öffentlichen VM über Spck CLI. Dafür sind ein **Spck-Konto und ein aktives Spck-Abonnement** erforderlich, zusätzlich zum einmaligen Lite-Kauf. Das Abonnement hilft, die laufenden Kosten für Hosting, Betrieb und Wartung der Spck-Server zu decken. Die enthaltenen lokalen Editor- und Git-Werkzeuge bleiben ohne Abonnement nutzbar.

### Erforderlich

- **Node.js**: **22.22.2+ (22.x), 24.15.0+ (24.x), oder 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Spck Editor-Konto**: Kostenloses Konto (30 Min./Tag) oder Premium-Abonnement (unbegrenzt)
- **Spck Editor Mobile App**: [Android](https://play.google.com/store/apps/details?id=io.spck) oder [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Optional (Empfohlen)

- **Git**: 2.20.0+ für [Git-Integration](./git-support#git-limitations-cli) in entfernten Projekten
- **ripgrep**: 15.0.0+ für deutlich schnellere Dateisuche (100-fache Verbesserung)

## <a name="installation"></a>Installation

### Option 1: Mit npx ausführen (Keine Installation)

```bash
npx spck@latest
```

Fordert die neueste CLI-Version an – ideal für die Ersteinrichtung oder gelegentliche Nutzung. `npx spck` kann eine bereits installierte Version wiederverwenden.

### Option 2: Globale Installation

```bash
npm install -g spck
spck
```

Einmal installieren und im Alltag `spck` ausführen. Mit `npm install -g spck@latest` aktualisieren. Remote-Verbindungen benötigen weiterhin Internetzugang.

## <a name="demo"></a>Demo

[Spck CLI im Video ansehen](https://youtu.be/EtfEhd5EmKM), einschließlich der neuen Fast-Lane-Funktion.

Eine kurze Vorführung: Spck CLI mit der mobilen App verbinden und lokale Dateien remote bearbeiten:

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>Ersteinrichtung

Beim ersten Start des CLI führt dich ein interaktiver Einrichtungsassistent durch die Konfiguration:

### 1. Authentifizierung

```bash
spck
# ENTER drücken, um den Browser zu öffnen
# Mit deinem Spck Editor-Konto anmelden
# CLI autorisieren
# Zum Terminal zurückkehren
```

Zugangsdaten werden in `~/.spck-editor/.credentials.json` gespeichert und bleiben über Sitzungen hinweg erhalten.

Wenn der Browser localhost nicht erreicht, erfolgt die Anmeldung über den Relay-Server. Mit dem Anmelde-QR-Code oder dem angezeigten Link können Sie sich auch von einem anderen Gerät anmelden. Dieser Code ist vom QR-Code zur Projektverbindung getrennt.

### 2. Projektkonfiguration

Der Assistent konfiguriert Folgendes:

- **Stammverzeichnis**: Basisverzeichnis für den Dateizugriff (Standard: aktuelles Verzeichnis)
- **Projektname**: Anzeigename in der mobilen App (Standard: Verzeichnisname)

### 3. Git-Integration (Optional)

Wenn eine `.gitignore`-Datei erkannt wird, bietet das CLI an, `.spck-editor/` hinzuzufügen, um das versehentliche Einschecken von Geheimnissen zu verhindern:

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**Empfehlung**: Wähle `Y`, um Verbindungszugangsdaten zu schützen.

### Einrichtung erneut ausführen

Zur Neukonfiguration zu einem beliebigen Zeitpunkt:

```bash
spck --setup
```

## <a name="connecting"></a>Verbindung mit Spck Editor herstellen

Bei einem neuen Projekt zeigt die CLI den Verbindungs-QR-Code bis zur ersten erfolgreichen Editor-Verbindung. Spätere Starts öffnen direkt das Dashboard. Mit **`c`** zeigen Sie QR-Code und Verbindungsdaten erneut an, mit **`l`** die Logs. Vergrößern Sie das Terminal, falls der QR-Code nicht hineinpasst.

### Methode 1: QR-Code (Empfohlen)

1. Spck Editor öffnen → **Projekte** → **Neues Projekt** → **Remote-Server verknüpfen**
2. Tippen Sie auf das QR-Code-Symbol
3. Scannen Sie den im Terminal angezeigten QR-Code. Die App verbindet sich automatisch.

> 💡 **Hinweis**: Sie können den Code auch mit der Kamera-App Ihres Geräts scannen. Dadurch wird der Link in Spck Editor geöffnet, sofern die App installiert ist.

### Methode 2: Manuelle Eingabe

Falls Sie den QR-Code nicht scannen können:

1. Spck Editor öffnen → **Projekte** → **Neues Projekt** → **Remote-Server verknüpfen**
2. Die im Terminal angezeigte **Client-ID** und das **Secret** eingeben
3. Wählen Sie den im Terminal angezeigten Relay-Server aus
4. **Verbinden** antippen

Wenn **Require PIN to connect** aktiviert ist, geben Sie die im CLI-Dashboard gewählte PIN ein. Die App speichert sie nicht. Siehe [Verbindungs-PIN](./cli-config#connection-pin).

## <a name="next-steps"></a>Nächste Schritte

1. **Das Relay-System verstehen**: Erfahre, wie das CLI Datenverkehr weiterleitet und wie du einen Server auswählst – siehe [CLI-Referenz](./cli)
2. **Dein Setup konfigurieren**: Terminal-, Sicherheits- und Dateisystemeinstellungen anpassen – siehe [Konfiguration](./cli-config)
3. **Erweiterte Funktionen erkunden**: CLI-Befehle, KI-Coding-Agenten, mehrere Projekte – siehe [Erweiterte Nutzung](./cli-advanced)
4. **Dateien zwischen Geräten übertragen**: Projekte kabellos zwischen Telefon und Desktop kopieren – siehe [Dateiübertragung](./cli-file-transfer)
5. **Sitzungen am Leben erhalten**: Sitzungen mit tmux geräteübergreifend teilen – siehe [tmux verwenden](./tmux)
