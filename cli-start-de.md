# <a name="getting-started"></a>Erste Schritte mit Spck CLI

## <a name="overview"></a>Überblick

Spck CLI ist ein Befehlszeilenwerkzeug, das deine lokale Entwicklungsumgebung über eine sichere WebSocket-Verbindung mit der mobilen Spck Editor-App verbindet. Sobald es läuft, kannst du lokale Dateien durchsuchen und bearbeiten, Terminalbefehle ausführen und lokale Server in der Vorschau anzeigen – alles direkt vom Telefon oder Tablet aus.

## <a name="requirements"></a>Voraussetzungen

### Erforderlich

- **Node.js**: 18.0.0 oder höher
- **Spck Editor-Konto**: Kostenloses Konto (30 Min./Tag) oder Premium-Abonnement (unbegrenzt)
- **Spck Editor Mobile App**: [Android](https://play.google.com/store/apps/details?id=io.spck) oder [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Optional (Empfohlen)

- **Git**: 2.20.0+ für Git-Integrationsfunktionen
- **ripgrep**: 15.0.0+ für deutlich schnellere Dateisuche (100-fache Verbesserung)

## <a name="installation"></a>Installation

### Option 1: Mit npx ausführen (Keine Installation)

```bash
npx spck
```

Verwendet immer die neueste Version – ideal für die Ersteinrichtung oder gelegentliche Nutzung.

### Option 2: Globale Installation

```bash
npm install -g spck
spck
```

Schnellerer Start, funktioniert offline und ist praktisch für den täglichen Einsatz.

## <a name="demo"></a>Demo

Eine kurze Vorführung: Spck CLI mit der mobilen App verbinden und lokale Dateien remote bearbeiten:

<img src="https://docs.spck.io/assets/gifs/remote-cli-preview.gif" alt="Spck CLI Demo" width="100%" />

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

Sobald das CLI läuft, zeigt es einen QR-Code und Verbindungsdetails an.

### Methode 1: QR-Code (Empfohlen)

**WICHTIG**: Installiere die Spck Editor-App, BEVOR du den QR-Code scannst.

**Auf Android:**

1. Kamera-App oder QR-Scanner in den Schnelleinstellungen verwenden
2. Nach Erkennung die Benachrichtigung antippen, um Spck Editor zu öffnen
3. App verbindet sich automatisch

> 💡 **Hinweis**: Einige QR-Code-Scanner können das benutzerdefinierte Schema zum direkten Öffnen von Spck Editor nicht verarbeiten. URL kopieren und in Chrome einfügen, das Spck Editor über die URL startet.

**Auf iOS:**

1. Kamera-App oder QR-Scanner im Kontrollzentrum verwenden
2. Nach Erkennung die Benachrichtigung antippen, um Spck Editor zu öffnen
3. App verbindet sich automatisch

> 💡 **Hinweis**: Spck Editor verfügt über KEINEN integrierten QR-Scanner. Verwende die native QR-Funktion deines Geräts.

### Methode 2: Manuelle Eingabe

Falls der QR-Code nicht funktioniert:

1. Spck Editor öffnen → **Projekte** → **Neues Projekt** → **Remote-Server verknüpfen**
2. Die im Terminal angezeigte **Client-ID** und das **Secret** eingeben
3. **Verbinden** antippen

## <a name="next-steps"></a>Nächste Schritte

1. **Das Relay-System verstehen**: Erfahre, wie das CLI Datenverkehr weiterleitet und wie du einen Server auswählst – siehe [CLI-Referenz](./cli)
2. **Dein Setup konfigurieren**: Terminal-, Sicherheits- und Dateisystemeinstellungen anpassen – siehe [Konfiguration](./cli-config)
3. **Erweiterte Funktionen erkunden**: CLI-Befehle, KI-Coding-Agenten, mehrere Projekte – siehe [Erweiterte Nutzung](./cli-advanced)
4. **Dateien zwischen Geräten übertragen**: Projekte kabellos zwischen Telefon und Desktop kopieren – siehe [Dateiübertragung](./cli-file-transfer)
5. **Sitzungen am Leben erhalten**: Sitzungen mit tmux geräteübergreifend teilen – siehe [tmux verwenden](./tmux)
