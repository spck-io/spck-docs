# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>Übersicht

Die Spck CLI enthält eine vollständige Language Server Protocol (LSP)-Brücke, die TypeScript-, JavaScript-, Python-, HTML-, CSS- und SCSS-Sprachserver direkt auf Ihrem Remote-Host ausführt. Sobald eine CLI-Sitzung verbunden ist, verwendet Spck Editor automatisch den Remote-Sprachserver anstelle des integrierten mobilen Servers.

> 💡 **Tipp**: Eine Beschreibung des integrierten Sprachservers, der ohne CLI verfügbar ist, finden Sie unter [Editor Language Server](./editor-language-server).

## <a name="cli-ls-architecture"></a>Architektur

Der CLI-Sprachserver läuft auf demselben Rechner wie Ihre Projektdateien. Dies bietet gegenüber dem im Browser ausgeführten Ansatz auf Mobilgeräten mehrere wesentliche Vorteile:

### Keine Dateiübertragung

Beim integrierten mobilen Sprachserver müssen Dateien zunächst auf das Gerät übertragen und in einen Browser-Worker geladen werden, bevor der Sprachserver sie analysieren kann. Mit der CLI liest der Sprachserver Dateien direkt von der Festplatte – ohne Übertragung. Das eliminiert den Bandbreitenaufwand und hält die Analyse auch bei großen Projekten schnell.

### Vollständige Projektkenntnis

Der CLI-Sprachserver hat Zugriff auf Ihr gesamtes Projektverzeichnis, einschließlich:

- Alle Quelldateien in jedem Unterverzeichnis
- `node_modules/` für die Auflösung von Drittanbieter-Typen
- Automatisch erkannte `tsconfig.json`-Dateien auf jeder Ebene
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` und zugehörige Deklarationsdateien

Das bedeutet, dass „Gehe zu Definition", „Referenzen suchen" und „Symbol umbenennen" korrekt über Dateigrenzen hinweg funktionieren – auch wenn Sie diese Dateien im Editor nicht geöffnet haben.

### Korrekte `tsconfig.json`-Verarbeitung

Der TypeScript-Sprachserver erkennt die `tsconfig.json` (oder `jsconfig.json`) Ihres Projekts automatisch und respektiert sie. Pfad-Aliasse (`paths`), Compiler-Optionen (`strict`, `target`, `lib`), Projektreferenzen und Monorepo-Workspace-Layouts werden alle korrekt verarbeitet. Der integrierte mobile Sprachserver kann `tsconfig.json` nicht lesen, da er beim Start keinen Zugriff auf das Dateisystem hat.

### Persistenter Prozess

Der Sprachserver-Prozess bleibt für die Dauer Ihrer CLI-Sitzung aktiv. Er erstellt einen In-Memory-Index Ihres Projekts und hält ihn zwischen Bearbeitungen warm, sodass die Antworten auch nach dem ersten Start schnell bleiben.

## <a name="cli-ls-features"></a>Unterstützte Funktionen

| Funktion | Beschreibung |
| --- | --- |
| **Codevervollständigung** | Kontextbewusste Vorschläge mit Typsignaturen, sortiert nach Relevanz |
| **Hover-Info** | Typinformationen und JSDoc-Dokumentation für das Symbol unter dem Cursor |
| **Signaturhilfe** | Parameterhinweise und Dokumentation beim Eingeben eines Funktionsaufrufs |
| **Gehe zu Definition** | Springe zur Deklaration eines Symbols, auch in `node_modules` |
| **Referenzen suchen** | Listet jede Verwendung eines Symbols im gesamten Projekt auf |
| **Symbol umbenennen** | Benennt ein Symbol um und aktualisiert alle Referenzen atomar |
| **Diagnose** | Echtzeit-Fehler- und Warnungshervorhebungen beim Tippen |
| **Markdown-Darstellung** | Hover- und Signaturdokumentation als Markdown mit syntaxhervorgehobenen Codeblöcken gerendert |

## <a name="cli-ls-languages"></a>Unterstützte Sprachen

| Sprache | Vervollständigung | Hover | Signaturen | Diagnose |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>Konfiguration

Die Sprachserver-Unterstützung ist standardmäßig aktiviert. Sie können sie in Ihrer Konfigurationsdatei steuern:

```json
{
  "languageServer": {
    "enabled": true,
    "typescript": {
      "enabled": true
    },
    "python": {
      "enabled": true
    }
  }
}
```

- **`languageServer.enabled`** (boolean): Hauptschalter für alle Remote-Sprachserver. Standard: `true`.
- **`languageServer.typescript.enabled`** (boolean): TypeScript/JavaScript-Sprachserver aktivieren. Standard: `true`.
- **`languageServer.python.enabled`** (boolean): Python-Sprachserver aktivieren (erfordert `pylsp` im `PATH`). Standard: `true`.

## <a name="cli-ls-requirements"></a>Voraussetzungen

- **TypeScript / JavaScript**: Im CLI enthalten. Keine zusätzliche Installation erforderlich.
- **Python**: Erfordert [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) (`pip install python-lsp-server`).
- **HTML / CSS / SCSS**: Im CLI enthalten. Keine zusätzliche Installation erforderlich.

## <a name="cli-ls-vs-mobile"></a>CLI vs. mobiler Sprachserver

| Funktion | CLI-Sprachserver | Mobiler integrierter Server |
| --- | --- | --- |
| Vollständiger Projektdateizugriff | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| `node_modules`-Typauflösung | ✓ | — |
| Dateiübergreifend: Gehe zu Definition | ✓ | Eingeschränkt |
| Dateiübergreifend: Referenzen suchen | ✓ | — |
| Symbol umbenennen | ✓ | — |
| Python-Unterstützung | ✓ | — |
| Funktioniert offline (ohne CLI) | — | ✓ |

&nbsp;

&nbsp;
