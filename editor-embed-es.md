# Integrar el editor

Integra Spck Editor en un iframe para crear ejemplos editables, tutoriales o herramientas de código. El wrapper `SpckEditor` se comunica con el iframe mediante `postMessage` y `MessageChannel`.

## <a name="screen-reader-support"></a>Compatibilidad con lectores de pantalla (experimental)

Consulta [Compatibilidad con lectores de pantalla (experimental)](./screen-reader-support#screen-reader-limitations) para las funciones de accesibilidad y las limitaciones actuales. El editor integrado no activa automáticamente el modo móvil de edición con lector de pantalla.

La [referencia completa de la API en inglés](/en/editor-embed) explica configuración, proyectos y archivos, ajustes del editor, eventos y solución de problemas. El código y las declaraciones TypeScript están en [spckio/spck-embed](https://github.com/spckio/spck-embed).
