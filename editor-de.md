# <a name="getting-started"></a>Erste Schritte

## <a name="getting-started-overview"></a>Überblick

Spck Editor ist eine mobile Code-Editing-Lösung mit mehreren Varianten, die für Entwickler konzipiert wurde.

### Versionen

#### Spck Editor (Kostenlos)

- Grundlegende mobile Code-Editing-Funktionalität
- Native Git-Integration auf Android und iOS; Browser-Git über isomorphic-git

#### Spck Editor Lite

**Preis**: Einmalige Zahlung
**Funktionen**:

- Benutzerdefinierte Snippets
- Vorausschauende Tastatur
- Exklusives Neon-Theme
- Erweiterte Git-Integration

#### Spck für NodeJS

**Plattform**: Exklusiv für Android
**Hauptfunktion**: Integriertes Terminal mit NodeJS-Unterstützung

Die erweiterte Git-Integration ist mit einem aktiven Node-Abonnement enthalten oder durch den Terminal-Einmalkauf dauerhaft freigeschaltet. Für beide Optionen ist eine Anmeldung erforderlich.

#### Browser-Version

- Auf jeder Website einbettbar
- Leichtgewichtige Code-Editing-Oberfläche

[Editor einbetten](./editor-embed)

### Hauptmerkmale

- Mobile-First-Design
- [Git-Unterstützung und Einschränkungen](./git-support)
- Plattformübergreifende Kompatibilität
- [Screenreader-Unterstützung (experimentell)](./screen-reader-support)

### <a name="git-credentials"></a>Git-Zugangsdaten und Pull Requests

<a name="pull-request-management"></a>

Siehe [Git-Unterstützung](./git-support) für [Anbieter-Token](./git-support#git-credentials), [Pull-Request-Verwaltung](./git-support#pull-request-management) und [erweiterte Git-Integration](./git-support#enhanced-git-integration).

### Empfohlene Verwendung

- Code-Bearbeitung unterwegs
- Schnelle Projektänderungen
- Lernen und Prototyping

## <a name="getting-started-terminology"></a>Terminologie

| Begriff           | Beschreibung                                                                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Navigationsmenü   | Bezieht sich auf den ersten Tab im Seitenmenü auf Mobilgeräten; dieses Menü ist in der Browser-Version oder im Tablet-Modus nicht verfügbar |
| Dateimenü         | Bezieht sich auf den _Datei_-Tab im Seitenmenü oder in der Seitenleiste                                                                     |
| Zusatztastatur    | Auf Mobilgeräten gibt es eine zusätzliche Tastatur mit häufig verwendeten Code-Symbolen zum schnellen Einfügen                              |
| Touch-Tastatur    | Bezieht sich im Allgemeinen auf die Tastenreihe mit den Pfeiltasten, der Tab-Taste und weiteren Tasten                                      |
| Touch-Aktionsbar  | Dies ist das schwebende Menü, das oberhalb des Cursors erscheint, wenn Text auf einem Mobil-/Touchgerät ausgewählt wird                     |
| Touch-Cursor      | Die auf dem Bildschirm angezeigten Cursor, die auf Mobil-/Touchgeräten erscheinen, wenn Text ausgewählt oder der Cursor aktiv ist           |
| Tablet-Modus      | Bezieht sich auf eine Einstellung, die auf größeren Touchgeräten wie Tablets aktiviert werden kann                                          |
| ⌘-Taste           | Dieses Symbol auf der Touch-Tastatur entspricht der Strg-Taste unter Windows oder der Command-Taste auf dem Mac                             |
| ⌥-Taste           | Dieses Symbol auf der Touch-Tastatur entspricht der Alt-Taste unter Windows oder der Option-Taste auf dem Mac                               |

&nbsp;

&nbsp;

# <a name="screen-reader-support"></a>Screenreader-Unterstützung (experimentell)

Die Screenreader-Unterstützung ist **experimentell**. Die [Screenreader-Anleitung](./screen-reader-support) beschreibt Aktivierung, Bearbeitung, Tastaturnavigation, Einschränkungen und [Feedback](./screen-reader-support#screen-reader-feedback).

&nbsp;

&nbsp;

# <a name="keyboard-shortcuts"></a>Tastenkombinationen

## <a name="keyboard-shortcuts-overview"></a>Überblick

Erreichen Sie blitzschnelle Effizienz mit diesen praktischen Tastenkombinationen! Auch wenn sie keinen vollständigen Katalog darstellen, werden diese Perlen Ihre Produktivität ankurbeln und die Navigation zum Kinderspiel machen.

### Wichtige Highlights

- **Nicht vollständig**: Eine kuratierte Auswahl der praktischsten Tastenkürzel
- **Zweck**: Verbessern Sie Ihren Workflow mit schnellen, intuitiven Befehlen
- **Vorteil**: Sparen Sie Zeit und reduzieren Sie die Abhängigkeit von der Maus

> 💡 **Profi-Tipp**: Prägen Sie sich diese Tastenkürzel ein und sehen Sie zu, wie Ihre Produktivität steigt! 🌟

Sie können die vollständige Liste der Tastenkürzel unter `Settings > Editor > Keyboard Shortcuts` einsehen.

> Premium-Benutzer können auch direkt über die Zusatztastatur oder mit dem Tastenkürzel `⌘ K` auf die Tastenkombinationen zugreifen.

> Aktivieren Sie die Strg/Command-Taste (⌘) und Alt/Option-Taste unter `Settings > Touch > Show ⌘ Key` und `Settings > Touch > Show ⌥ Key`.

Hinweise zu Tastaturfokus, Menüaktivierung und barrierefreier Bearbeitung finden Sie unter [Screenreader-Unterstützung (experimentell)](./screen-reader-support).

## <a name="keyboard-shortcuts-editor"></a>Editor

| Kürzel  | Aktion                                                  |
| ------- | ------------------------------------------------------- |
| ⌘ A     | Alles auswählen                                         |
| ⌘ C     | Kopieren                                                |
| ⌘ V     | Einfügen                                                |
| ⌘ X     | Ausschneiden                                            |
| ⌘ Z     | Rückgängig                                              |
| ⌘ ⇧ Z   | Wiederherstellen                                        |
| ⌘ D     | Zeile duplizieren                                       |
| ⌘ /     | Zeile kommentieren/auskommentieren                      |
| ⌥ F     | Code formatieren                                        |
| ⌘ F     | Suchen                                                  |
| ⌘ G     | Nächsten finden (funktioniert mit ausgewähltem Text)    |
| ⌘ ⇧ G   | Vorherigen finden                                       |
| ⌘ L     | Zu Zeile springen                                       |

## <a name="keyboard-shortcuts-quick-actions"></a>Schnellaktionen

| Kürzel  | Aktion                                       |
| ------- | -------------------------------------------- |
| ⌘ ⇧ C   | Git Commit                                   |
| ⌘ O     | Zuletzt verwendete Dateien öffnen            |
| ⌘ ⇧ P   | Projektvorschau starten                      |
| ⌘ P     | Dateivorschau umschalten (SVG, Markdown)     |
| ⌘ K     | **Supporter+**: Tastenkürzel öffnen          |

&nbsp;

&nbsp;

# <a name="touch-settings"></a>Touch-Einstellungen

## <a name="touch-settings-extra"></a>Zusatztastatur

- Die Zusatztastatur ist eine Symboltastatur, die speziell für Touchgeräte entwickelt wurde.
- Auf zusätzliche Tasten/Symbole kann durch Drücken und Halten der Tasten zugegriffen werden, was ein Menü mit Optionen öffnet.
- Sie können sie im Menü `Settings > Touch > Extra Keyboard` aktivieren oder deaktivieren.

> 💡 **Profi-Tipp**: Siehe _**Erweiterte Bearbeitung**_ für Tipps zum Umschließen von Text, die mit der Zusatztastatur kompatibel sind.

## <a name="touch-settings-touch"></a>Touch-Tastatur

- Touch-Tasten bestehen aus einer Tastenreihe mit Pfeiltasten, Command-Taste und anderen häufig verwendeten Tasten.
- Diese Funktion ist auf Touchgeräten verfügbar.
- Sie können sie unter `Settings > Touch > Touch Keyboard` ein- oder ausschalten.

> 💡 **Profi-Tipp**: Sie können einzelne Tasten dieser Tastatur durch Anpassen der Einstellungen individualisieren.

## <a name="touch-settings-action-bar"></a>Touch-Aktionsbar

- Eine Aktionsleiste mit den Optionen Kopieren, Ausschneiden und Einfügen wird angezeigt, wenn Text ausgewählt ist.
- Diese Funktion kann unter `Settings > Touch > Touch Action Bar` aktiviert oder deaktiviert werden.

## <a name="touch-settings-cursors"></a>Touch-Cursor

- Bildschirm-Cursor, die erscheinen, wenn Text ausgewählt oder der Cursor aktiv ist.
- Diese Funktion kann unter `Settings > Touch > Touch Cursors` aktiviert oder deaktiviert werden.

> 💡 **Profi-Tipp**: Es wird nicht empfohlen, diese Funktion zu deaktivieren, es sei denn, Sie haben eine Maus/ein Zeigegerät mit dem Mobilgerät gekoppelt. Das Deaktivieren der Touch-Cursor kann die Sichtbarkeit beim Bearbeiten verbessern und das Bearbeitungserlebnis bei Verwendung externer Zeigegeräte optimieren.

## <a name="touch-settings-predictive"></a>Vorausschauende Tasten

- Vorausschauende Tasten sind eine Premium-Funktion, die die Standard-Zusatztastatur ersetzt.
- Bietet die Eingabe von Symbolen per Einzelberührung, statt halten und auswählen wie bei der regulären Zusatztastatur.
- Tasten werden nach der statistischen Häufigkeit von Symbolen an einer bestimmten Position in der Datei sortiert.
- Sie kann unter `Settings > Touch > Predictive Keyboard` ein- oder ausgeschaltet werden.

> 💡 **Profi-Tipp**: Vorausschauende Tasten ersetzen die reguläre Zusatztastatur, die einige Benutzer möglicherweise bevorzugen. Vorausschauende Tasten sind in der **Lite**-Version des Editors standardmäßig aktiviert und können deaktiviert werden, um die reguläre Zusatztastatur zurückzubekommen.

&nbsp;

&nbsp;

# <a name="file-navigation"></a>Dateinavigation

## <a name="file-navigation-overview"></a>Überblick

- Es gibt mehrere Methoden, um zwischen Dateien zu navigieren.
- Sie können über die Dateien im Seitenmenü durch die Dateien navigieren.
- Sie können das Breadcrumb verwenden, um vom aktuellen Dateiverzeichnis aus durch die Dateien zu navigieren.
- Sie können die Zuletzt verwendeten Dateien mit `Ctrl-O` öffnen, um schnell nach Dateien zu suchen.
- Sie können das Symbol „Lokalisieren" im Seitenmenü „Dateien" verwenden, um die aktuellen Dateien schnell zu lokalisieren.
- Auch die Seitenmenüs Versionskontrolle und Suche bieten einzigartige Möglichkeiten zur Navigation zwischen Dateien.

## <a name="file-navigation-tabs"></a>Verwaltung von Dateitabs

### Tab-Verhalten

- Dateien werden beim ersten Öffnen automatisch gelöst (nicht angeheftet)
- Tabs werden angeheftet, sobald Bearbeitungen vorgenommen werden

### Optionen zur Tab-Sortierung

Dateien können sortiert werden nach:

- Alphabetischer Reihenfolge
- Dateiendung
- Dateipfad

### Alternative Navigationswege

- **Versionskontrollmenü**: Navigieren Sie durch Dateien im Kontext der Versionskontrolle
- **Suchmenü**: Finden und greifen Sie basierend auf Suchkriterien auf Dateien zu

> 💡 **Profi-Tipp**: Dateitabs können unter `Settings > Appearance > Show File Tabs` ausgeblendet werden. Siehe _Zen-Modus_, um den Bildschirmplatz auf kleineren Geräten zu maximieren.

&nbsp;

&nbsp;

# <a name="advanced-editing"></a>Erweiterte Bearbeitung

## Effiziente Nutzung der vorausschauenden Tastatur

### Grundlegende Auswahl

- Doppeltippen, um ein Wort oder einen Textblock auszuwählen

### Text umschließen

Umschließen Sie ausgewählten Text schnell mit Klammer- oder Anführungspaaren:

- Runde Klammern: `( )`
- Eckige Klammern: `[ ]`
- Geschweifte Klammern: `{ }`
- Einfache Anführungszeichen: `' '`
- Doppelte Anführungszeichen: `" "`

### Navigation und Bearbeitung

#### Textsuche

- `⌘ G`: Nächste Instanz finden
- `⌘ ⇧ G`: Vorherige Instanz finden

#### Einrückung

- Wählen Sie einen Textblock aus
- Drücken Sie Tab zum Einrücken

&nbsp;

## <a name="multiple-cursors"></a>Mehrere Cursor

### Schnelle Einrichtung

- Aktivieren Sie mehrere Cursor mit der Alt/Option-Taste! ✨
- Navigieren Sie zu `Settings > Touch > Show ⌥ Key` zur Aktivierung

### Verwendung

1. Wählen Sie sowohl die ⌥- als auch die ⌘-Taste aus
2. Klicken Sie, um Cursor genau dort zu platzieren, wo Sie sie haben möchten
3. Bearbeiten Sie mehrere Zeilen gleichzeitig mit Leichtigkeit! 💻

> 💡 **Profi-Tipp**: Multi-Cursor-Bearbeitung = blitzschnelle Code-Transformation! ⚡️
> Es ist auch möglich, Multi-Cursor über die Befehle `Add Cursor Above` und `Add Cursor Below` der Befehlspalette hinzuzufügen, die einen Cursor direkt über oder unter der aktuellen Cursorposition hinzufügen würden.

&nbsp;

&nbsp;

# <a name="enhanced-git-integration"></a>Git-Unterstützung

Die [Git-Anleitung](./git-support) beschreibt Anbieter-Zugangsdaten, Pull-Request-Verwaltung, Commit-Ansichten und den Zugriff auf die erweiterte Git-Integration.

<a name="merge-conflict-resolution"></a>

Grundlegendes Git umfasst die [Konfliktauflösung](./git-support#merge-conflict-resolution) im Diff-Viewer mit **Accept Current**, **Accept Incoming**, **Accept Both** und **Resolve**.

## <a name="git-limitations"></a>Git-Einschränkungen

<a name="git-limitations-overview"></a>
<a name="git-limitations-memory"></a>
<a name="git-limitations-symlinks"></a>
<a name="git-limitations-cli"></a>

Android und iOS nutzen natives libgit2 für lokale Projekte, der Browser isomorphic-git und entfernte Projekte die Git-Binary des Hosts. Siehe [Git-Einschränkungen](./git-support#git-limitations) für Speicherort, Speichergrenzen, Symlinks und entfernte Alternativen.

&nbsp;

&nbsp;

# <a name="zen-mode"></a>🌟 Zen-Modus

## Überblick

Der Zen-Modus ist eine angenehme, platzmaximierende Editor-Konfiguration, die Ihr Codierungserlebnis auf kompakten Displays transformiert.

Der Zen-Modus besteht aus:

- Deaktivieren von `Show Line Numbers` in den Einstellungen
- Deaktivieren von `Show File Tab`
- Deaktivieren von `Touch Action Bar`

### Hauptmerkmale

#### 🧘‍♀️ Maximierter Bildschirmplatz

- **Weg mit den Zeilennummern!**
  - Geben Sie wertvollen horizontalen Platz frei
  - Verhindern Sie, dass sich Text beengt anfühlt
  - Genießen Sie den klaren, minimalistischen Look

#### 🎨 Optimierte Benutzeroberfläche

- **Minimierung der Aktionsleiste**
  - Verabschieden Sie sich von überfüllten Symbolleisten
  - Nutzen Sie alternative Eingabemethoden:
    - Einfüge-/Ausschneide-Tasten der Zusatztastatur
    - Tastenkombinationen (`Ctrl-C/Ctrl-V`)

#### 📂 Vereinfachte Navigation

- **Eliminierung der Dateitabs**
  - `Ctrl-O` wird zu Ihrem neuen Navigations-Best-Buddy
  - Aufgeräumterer Arbeitsbereich
  - Schnelleres Kontextwechseln

> 💡 **Profi-Tipp**: Nicht jeder Programmierstil ist gleich! Wir empfehlen, mit dem Zen-Modus zu experimentieren, um zu sehen, ob er zu Ihrem Workflow passt. Ihre perfekte Codierungsumgebung ist nur ein paar Schalter entfernt! 🌈✨
