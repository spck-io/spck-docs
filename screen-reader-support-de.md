# <a name="screen-reader-support"></a>Screenreader-Unterstützung (experimentell)

Die Screenreader-Unterstützung ist **experimentell** und umfasst grundlegende Arbeitsabläufe im Editor. Die Kompatibilität kann je nach Gerät, Betriebssystem und Screenreader variieren; einige Bedienelemente und erweiterte Funktionen müssen möglicherweise noch verbessert werden.

## <a name="screen-reader-activation"></a>Bearbeitung mit Screenreader aktivieren

Aktivieren Sie Ihren Screenreader in den Bedienungshilfen des Geräts. In mobilen Versionen, die den Screenreader-Status melden, stellt Spck das aktive Dokument automatisch als barrierefreies Textfeld bereit. Eine separate Einstellung im Editor ist nicht erforderlich.

Das Textfeld stellt Dokumentinhalt und Dateinamen zum Lesen, Auswählen und Bearbeiten bereit. Änderungen werden wie gewohnt automatisch gespeichert; die Auswahl bleibt synchronisiert und Rückgängig sowie Wiederholen stehen weiter zur Verfügung. Beim Dateiwechsel werden Inhalt und Dateiname aktualisiert; schreibgeschützte Dokumente bleiben schreibgeschützt. Auf unterstützten Versionen stellt das Ausschalten des Screenreaders den üblichen Editor wieder her.

## <a name="screen-reader-navigation"></a>Navigation und Bedienelemente

Unterstützt werden unter anderem:

- Beschriftungen für Symbolschaltflächen, Navigations- und Dateireiter, Suchfelder und Versionskontrollaktionen in der gewählten Oberflächensprache.
- Datei- und Projektzeilen, die per Screenreader oder Tastatur aktiviert werden können. Ordner melden ihren aufgeklappten Zustand; mit einer physischen Tastatur klappen Sie sie mit Pfeil rechts und links auf und zu.
- Dateireiter, die die aktive Datei kennzeichnen, sowie Git-Statusbuchstaben als Ergänzung zu den Dateinamenfarben.
- Einstellungen mit zugeordneten Beschriftungen und Zuständen sowie Formularfelder, die Validierungsfehler zugänglich machen.
- Benannte Dialoge, die den Tastaturfokus beim Öffnen im Dialog halten und beim Schließen zum auslösenden Element zurückgeben. Aktionsmenüs erhalten beim Öffnen den Fokus und geben ihn beim Schließen mit Escape zurück.

Mit einer physischen Tastatur wechseln Sie mit **Tab** zwischen fokussierbaren Elementen, aktivieren Schaltflächen mit **Enter** oder **Leertaste** und schließen Aktionsmenüs mit **Escape**. Die üblichen Navigations- und Aktivierungsgesten Ihres Screenreaders stehen ebenfalls zur Verfügung.

## <a name="screen-reader-limitations"></a>Aktuelle Einschränkungen

- Die barrierefreie Dokumentbearbeitung setzt voraus, dass die mobile App einen aktivierten Screenreader meldet. Browser und eingebetteter Editor aktivieren diesen Modus nicht automatisch.
- Die Unterstützung umfasst derzeit die oben genannten grundlegenden Abläufe. Erweiterte Editorinteraktionen und andere App-Funktionen funktionieren möglicherweise nicht mit jedem Screenreader gleich gut.
- Das Verhalten kann sich je nach App-Version, Betriebssystem und Gerät unterscheiden. Melden Sie nicht erreichbare oder nicht aktivierbare Elemente, unerwartete Fokuswechsel und Probleme beim Lesen oder Bearbeiten.

Siehe [Tastenkombinationen](./editor#keyboard-shortcuts) für Bearbeitungsbefehle und [Git-Unterstützung und Einschränkungen](./git-support#git-limitations) für Unterschiede zwischen mobilem, browserbasiertem und entferntem Git.

## <a name="screen-reader-feedback"></a>Feedback

Bitte [senden Sie Feedback an support@spck.io](mailto:support@spck.io), wenn ein Element unbeschriftet ist, der Fokus verloren geht oder Lesen und Bearbeiten nicht wie erwartet funktionieren. Nennen Sie Ihre Spck-Version, Gerät und Betriebssystem, den Screenreader und die Schritte zum Reproduzieren des Problems.
