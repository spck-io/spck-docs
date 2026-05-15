# <a name="cli-configuration"></a>CLI-Konfiguration

## <a name="configuration"></a>Konfiguration

### Speicherort der Konfigurationsdatei

Die Konfiguration wird in `.spck-editor/config/spck-cli.config.json` in Ihrem Projektverzeichnis gespeichert.

**Wichtig**: `.spck-editor/config` ist ein **Symlink** zu `~/.spck-editor/projects/{project_id}/`, wodurch Geheimnisse außerhalb Ihres Projektverzeichnisses bleiben.

### Standardkonfiguration

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### Browser-Proxy-Einstellungen

- **`browserProxy.enabled`** (boolean): Browser-Proxy-Funktion aktivieren/deaktivieren
  - Standard: `true`
  - Auf `false` setzen, um zu verhindern, dass die Mobile-App eine Browser-Proxy-Sitzung über die CLI öffnet

### Terminal-Einstellungen

- **`terminal.enabled`** (boolean): Terminal-Zugang aktivieren/deaktivieren
  - Standard: `true`
  - Auf `false` setzen, um das Risiko unbefugten Zugriffs auf Ihr Terminal zu reduzieren

- **`terminal.maxBufferedLines`** (number): Maximaler Scrollback-Puffer
  - Standard: `10000`
  - Beeinflusst den Speicherverbrauch (~1MB pro 10.000 Zeilen)

- **`terminal.maxTerminals`** (number): Maximale gleichzeitige Terminal-Sitzungen
  - Standard: `10`
  - Jedes Terminal verwendet ~5-10MB Speicher

### Dateisystem-Einstellungen

- **`filesystem.maxFileSize`** (string): Maximale Dateigröße für Lese-/Schreibvorgänge
  - Standard: `"10MB"`
  - Akzeptiert: `"5MB"`, `"50MB"`, etc.

- **`filesystem.watchIgnorePatterns`** (string[]): Muster zum Ausschließen von der Dateiüberwachung
  - Standard: Ignoriert Build-Ausgaben und Abhängigkeiten
  - Verbessert die Leistung durch Vermeidung von Tausenden generierter Dateien

### Sicherheitseinstellungen

- **`security.userAuthenticationEnabled`** (boolean): Firebase-Benutzerauthentifizierung aktivieren
  - Standard: `false`
  - Bei `false`: Geringere Latenz, kompatibel mit Lite, immer noch durch Secret-Signierung geschützt
  - Bei `true`: Zusätzliche Sicherheitsebene, Benutzeridentitätsverifizierung, fügt 2-20s anfängliche Latenz hinzu
  - **Alle Anfragen werden unabhängig von dieser Einstellung immer kryptographisch signiert**

## <a name="security"></a>Sicherheit

### Verschlüsselte Verbindungen

Alle Kommunikation verwendet:

- **WSS (WebSocket Secure)**: TLS/SSL-Verschlüsselung
- **HTTPS**: Verschlüsselter initialer Handshake

### Anfragensignierung

Jede Anfrage wird kryptographisch signiert:

- Secret Key wird lokal generiert, niemals über das Internet übertragen
- Es wird empfohlen, keine Drittanbieter-QR-Scanner zu verwenden, die Ihren Secret Key offenlegen könnten

### Best Practices

1. **Anmeldedaten schützen**:

   ```bash
   # Zur .gitignore hinzufügen (automatisch während der Einrichtung)
   echo ".spck-editor/" >> .gitignore
   ```

2. **Auf geteilten Rechnern abmelden**:

   ```bash
   spck --logout
   ```

3. **Exponierte Verzeichnisse begrenzen**:

   ```bash
   # Statt des gesamten Home-Verzeichnisses
   spck --root /path/to/specific/project
   ```

4. **Terminal deaktivieren, wenn nicht benötigt**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **Browser-Proxy deaktivieren, wenn nicht benötigt**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>Benutzerauthentifizierung

Spck CLI unterstützt optionale Firebase-Benutzerauthentifizierung als zweite Sicherheitsebene zusätzlich zur immer aktiven Anfragensignierung.

### Funktionsweise

Wenn aktiviert, erfordert die CLI die Anmeldung mit Ihrem Spck Editor-Konto. Verbindungen werden mit Firebase-ID-Tokens authentifiziert, die stündlich ablaufen und automatisch mit sicheren Refresh-Tokens erneuert werden, die in `~/.spck-editor/.credentials.json` gespeichert sind.

### Benutzerauthentifizierung aktivieren

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### Kompromisse

|                        | Deaktiviert (Standard)     | Aktiviert                               |
| ---------------------- | -------------------------- | --------------------------------------- |
| **Schutz**             | Secret-Signierungsschlüssel | + Firebase-Identitätsverifizierung     |
| **Anfangslatenz**      | Kein Auth-Overhead          | Fügt 2–20s beim ersten Verbinden hinzu |
| **Spck Editor Lite**   | ✅ Unterstützt              | ❌ Nicht unterstützt                   |
| **Offline-Nutzung**    | Funktioniert ohne Internet  | Erfordert Internet für Token-Erneuerung |

### Wann aktivieren

**Deaktiviert lassen (Standard) wenn:**

- **Spck Editor Lite** verwendet wird — Firebase-Login wird in Lite nicht unterstützt; Setzen auf `true` verhindert, dass Lite-Benutzer sich verbinden können
- In einem lokalen Netzwerk oder einer vertrauenswürdigen Umgebung arbeiten, in der der Secret-Signierungsschlüssel ausreicht
- Minimierung der Verbindungslatenz Priorität hat

**Aktivieren wenn:**

- Die CLI auf einem Server exponiert ist, der über das Internet erreichbar ist
- Sie Benutzeridentitätsverifizierung als zusätzliche Zugangskontrollebene über den Signierungsschlüssel hinaus wünschen

> ⚠️ **Spck Editor Lite unterstützt keine Firebase-Authentifizierung.** Wenn `userAuthenticationEnabled` auf `true` gesetzt ist, kann sich Spck Editor Lite nicht verbinden. Belassen Sie diese Einstellung bei `false`, wenn Sie Lite verwenden.
