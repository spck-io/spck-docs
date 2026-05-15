# <a name="cli-file-transfer"></a>Dateiübertragung zwischen Mobilgerät und Desktop

## <a name="overview"></a>Überblick

Wenn du Spck CLI auf deinem Desktop ausführst, fungiert es als Synchronisierungshub zwischen deinem Desktop-Dateisystem und den lokalen Projekten auf deinem Telefon. Beide Seiten erscheinen nebeneinander im Spck Editor-Dateimanager – die lokalen Projekte deines Telefons auf der linken Seite und die Dateien deines Desktops als verbundener Remote-Server – und du kannst Dateien oder ganze Ordner in beide Richtungen mit den normalen Kopieren-und-Einfügen-Befehlen übertragen.

Kein AirDrop, kein Bluetooth, kein USB-Kabel und kein Cloud-Speicher eines Drittanbieters erforderlich. Übertragungen sind Ende-zu-Ende-verschlüsselt über eine WebSocket-Verbindung und bleiben in deinem lokalen WLAN, wenn beide Geräte im selben Netzwerk sind.

## <a name="how-it-works"></a>Funktionsweise

Das CLI stellt dein Desktop-Verzeichnis als Remote-Server-Projekt im Spck Editor-Dateimanager zur Verfügung. Lokale Projekte auf deinem Telefon werden im lokalen Speicher der App gespeichert. Spck Editor behandelt beide als gleichwertige Projektspeicherorte, sodass alle Dateioperationen, die innerhalb eines einzelnen Projekts funktionieren – einschließlich Kopieren und Einfügen – auch projektübergreifend funktionieren.

```
Telefon (lokaler Speicher)     Desktop (via CLI)
──────────────────────────     ─────────────────────
my-project/               ↔   ~/projects/my-project/
  ├── index.html                 ├── index.html
  ├── style.css                  ├── style.css
  └── assets/                    └── assets/
      └── logo.png                   └── logo.png
```

Verzeichnisse werden rekursiv übertragen – alle enthaltenen Dateien werden kopiert und Unterverzeichnisse am Ziel automatisch erstellt.

## <a name="desktop-to-mobile"></a>Desktop zu Mobilgerät

Verwende dies, wenn du Dateien von deinem Computer auf dein Telefon übertragen möchtest – beispielsweise um offline zu arbeiten, ein Projekt mit einem Kollegen zu teilen, der nur die mobile App hat, oder um eine Momentaufnahme deiner Arbeit auf dem Gerät zu speichern.

1. **CLI starten** auf deinem Desktop, das auf den Ordner zeigt, aus dem du übertragen möchtest:

   ```bash
   spck --root ~/projects
   ```

2. **Telefon verbinden**, indem du den QR-Code mit der Kamera-App scannst und den Link in Spck Editor öffnest.

3. In Spck Editor erscheint dein Desktop-Ordner als Remote-Server-Projekt im **Projekte**-Panel.

4. **Datei oder Ordner gedrückt halten**, den du im Remote-Projekt möchtest, dann **Kopieren** antippen.

5. **Zu einem lokalen Projekt** auf deinem Telefon navigieren (oder ein neues über **Neues Projekt** erstellen).

6. **Zielordner gedrückt halten**, dann **Einfügen** antippen.

Die Dateien werden von deinem Desktop heruntergeladen und im lokalen Speicher deines Telefons gespeichert.

## <a name="mobile-to-desktop"></a>Mobilgerät zu Desktop

Verwende dies, wenn du Arbeit vom Telefon zurück auf den Desktop übertragen möchtest – beispielsweise nach dem Bearbeiten unterwegs oder um auf dem Gerät erstellte Projekte zusammenzuführen.

1. **CLI starten** auf deinem Desktop, das auf den Ordner zeigt, in dem die Dateien landen sollen:

   ```bash
   spck --root ~/Desktop/from-phone
   ```

2. **Telefon verbinden**, indem du den QR-Code scannst.

3. In Spck Editor das **lokale Projekt** auf deinem Telefon öffnen, das die zu sendenden Dateien enthält.

4. **Datei oder Ordner gedrückt halten**, dann **Kopieren** antippen.

5. **Zum Remote-Desktop-Projekt** im **Projekte**-Panel navigieren.

6. **Zielordner gedrückt halten**, dann **Einfügen** antippen.

Die Dateien werden aus dem lokalen Speicher deines Telefons gelesen und über das CLI auf deinen Desktop geschrieben.

## <a name="transferring-projects"></a>Ganze Projekte übertragen

Du kannst einen kompletten Projektordner in einem einzigen Einfügevorgang kopieren. Den Projektstamm im Dateibaum gedrückt halten, **Kopieren** auswählen, dann zum Ziel navigieren und **Einfügen** antippen. Die gesamte Verzeichnisstruktur – einschließlich aller Dateien in allen Unterverzeichnissen – wird übertragen.

Dies ist nützlich für:

- **Sicherung eines mobilen Projekts auf deinem Desktop** vor größeren Änderungen
- **Einrichten eines neuen Telefon-Projekts** aus einer bestehenden Desktop-Codebasis
- **Zusammenführen von Arbeit** von mehreren Geräten an einem Ort

## <a name="tips"></a>Tipps

### Dateigrößenlimit

Die standardmäßige maximale Dateigröße beträgt **10 MB** pro Datei. Um größere Dateien wie Bilder, Archive oder kompilierte Binärdateien zu übertragen, erhöhe das Limit in deiner CLI-Konfiguration:

```json
{
  "filesystem": {
    "maxFileSize": "200MB"
  }
}
```

Vollständige Details unter [CLI-Konfiguration](./cli-config).

### Übertragungsgeschwindigkeit

Die Geschwindigkeit hängt vollständig von deiner lokalen WLAN- oder Internetverbindung ab. Bei großen Verzeichnissen werden Übertragungen Datei für Datei durchgeführt, sodass der Gesamtdurchsatz mit der Anzahl der Dateien skaliert. In einem typischen Heimnetzwerk werden kleine, textlastige Projekte (Hunderte von Dateien) in wenigen Sekunden abgeschlossen.

### Sicherheit

Alle Übertragungen sind über WSS (WebSocket Secure) verschlüsselt, und jede Anfrage wird mit einem sitzungsspezifischen Geheimschlüssel signiert. Der Relay-Server leitet Nachrichten zwischen Geräten weiter, empfängt aber niemals unverschlüsselte Inhalte. Vollständige Details unter [CLI-Sicherheit](./cli-config#security).

### Mehrere Übertragungen gleichzeitig

Das CLI stellt ein einzelnes Stammverzeichnis zur Verfügung. Um gleichzeitig von mehreren Speicherorten zu übertragen, starte separate CLI-Instanzen in verschiedenen Terminals:

```bash
# Terminal 1: ~/projects freigeben
spck --root ~/projects

# Terminal 2: ~/Documents freigeben
spck --root ~/Documents
```

Jede Instanz generiert ihren eigenen QR-Code und ihre eigene Verbindung, und beide Remote-Server erscheinen gleichzeitig im Spck Editor **Projekte**-Panel.
