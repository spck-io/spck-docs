# Editor einbetten

Betten Sie Spck Editor in einen iframe ein, um bearbeitbare Beispiele, Anleitungen oder Werkzeuge für Code anzubieten. Der Wrapper `SpckEditor` kommuniziert über `postMessage` und `MessageChannel` mit dem iframe.

## <a name="screen-reader-support"></a>Screenreader-Unterstützung (experimentell)

Siehe [Screenreader-Unterstützung (experimentell)](./screen-reader-support#screen-reader-limitations) für Barrierefreiheit und aktuelle Einschränkungen. Der eingebettete Editor aktiviert den mobilen Screenreader-Bearbeitungsmodus nicht automatisch.

Die vollständige [API-Referenz auf Englisch](/en/editor-embed) beschreibt Einrichtung, Projekte und Dateien, Editor-Einstellungen, Ereignisse und Fehlerbehebung. Quellcode und TypeScript-Deklarationen finden Sie unter [spckio/spck-embed](https://github.com/spckio/spck-embed).
