# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Ubersicht

Spck Editor Lite ist eine Einmalkauf-Version von Spck Editor, die Premium-Bearbeitungsfunktionen ohne Abonnement freischaltet. Die App ist sowohl fur Android als auch fur iOS als separate App verfugbar.

Lite enthalt alles aus der kostenlosen Version, plus:

- **Predictive Keyboard** -- kontextbezogene Symbolvorschlage auf der Zusatztastatur
- **Benutzerdefinierte Snippets** -- eigene Code-Vorlagen mit Tab-Stop-Platzhaltern
- **Neon-Theme** -- ein exklusives Editor-Theme

Diese Funktionen sind auch in der Vollversion von Spck Editor mit einem aktiven Gold- oder Supporter-Abonnement verfugbar. Die Lite-App bietet die gleiche Funktionalitat als Einzelkauf.

## <a name="predictive-keyboard"></a>Predictive Keyboard

Das Predictive Keyboard ersetzt die Standard-Zusatztastatur durch eine Reihe kontextbezogener Symboltasten. Anstatt eine Taste lange zu drucken, um aus einem Menu auszuwahlen, werden die wahrscheinlichsten Symbole direkt angezeigt -- basierend auf der aktuellen Cursorposition in der Datei.

### Funktionsweise

Die Vorhersagen werden aus statistischen Haufigkeitstabellen generiert, die pro Sprache erstellt werden. Wenn sich der Cursor bewegt, ordnet die Tastatur die Symbole danach neu, wie haufig jedes Symbol an dieser Art von Position in echtem Code vorkommt. Unterstutzte Sprachen sind JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown und Klartext.

### Aktivieren oder Deaktivieren

Gehe zu `Settings > Touch > Predictive Keyboard`, um die Funktion umzuschalten. In Lite ist das Predictive Keyboard standardmassig aktiviert. Durch Deaktivieren wird die Standard-Zusatztastatur wiederhergestellt.

> Das Predictive Keyboard ist nur auf Touchscreen-Geraten verfugbar. Es erscheint nicht bei Verwendung einer physischen Tastatur oder im Tablet-Modus mit angeschlossener externer Tastatur.

## <a name="custom-snippets"></a>Benutzerdefinierte Snippets

Mit benutzerdefinierten Snippets konnen Sie wiederverwendbare Code-Vorlagen erstellen, die beim Tippen in der Autovervollstandigungsliste erscheinen. Jedes Snippet ist auf eine bestimmte Sprache beschrankt, sodass Ihre JavaScript-Snippets nicht in Python-Dateien erscheinen.

### Ein Snippet erstellen

1. Offne `Settings > Editor > Custom Snippets`
2. Wahle die Sprache aus (z.B. JavaScript, Python, HTML)
3. Tippe auf **Snippet hinzufugen**
4. Gib einen **Ausloser** ein -- die Abkurzung, die du tippst, um das Snippet aufzurufen
5. Gib den **Inhalt** ein -- den Code, der eingefugt wird

### Tab-Stops und Platzhalter

Snippets unterstutzen Tab-Stops, sodass der Cursor nach dem Einfugen zwischen bearbeitbaren Positionen springt:

- `$1`, `$2`, `$3` -- nummerierte Tab-Stops in Durchlaufreihenfolge
- `$0` -- endgultige Cursorposition nach allen Tab-Stops
- `${1:defaultText}` -- ein Tab-Stop mit Platzhaltertext, der zur einfachen Ersetzung vorausgewahlt ist

Beispiel -- ein JavaScript-`for`-Schleifen-Snippet:

**Ausloser:** `forloop`

**Inhalt:**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

Wenn du `forloop` tippst und es aus der Autovervollstandigung auswahlst, wird die vollstandige Schleife eingefugt. Drucke Tab, um zwischen `i`, `array` und dem Schleifenkorper zu wechseln.

### Importieren und Exportieren

Du kannst alle Snippets in eine Datei exportieren und auf einem anderen Gerat importieren. Das ist praktisch, um Snippet-Sammlungen zwischen Geraten zu teilen oder deine Konfiguration zu sichern.

## <a name="neon-theme"></a>Neon-Theme

Lite enthalt das **Neon**-Editor-Theme, ein dunkles Theme mit leuchtenden Akzentfarben. Es ist in Lite als Standard-Theme eingestellt und kann jederzeit unter `Settings > Appearance > Theme` geandert werden.

## <a name="comparison"></a>Funktionsvergleich

| Funktion | Kostenlos | Lite (Einmalkauf) | Voll (Abonnement) |
| --- | :---: | :---: | :---: |
| Code-Bearbeitung und Syntaxhervorhebung | Ja | Ja | Ja |
| Git-Integration | Ja | Ja | Ja |
| Zusatztastatur | Ja | Ja | Ja |
| Touch-Tastatur und Cursor | Ja | Ja | Ja |
| Projektvorschau | Ja | Ja | Ja |
| Predictive Keyboard | -- | Ja | Gold / Supporter |
| Benutzerdefinierte Snippets | -- | Ja | Gold / Supporter |
| Neon-Theme | -- | Ja | -- |
| KI-Assistent | -- | -- | Ja |
| Benutzerkonten und Cloud-Synchronisierung | -- | -- | Ja |
| Labs / Community-Projekte | -- | -- | Ja |
