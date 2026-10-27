# <a name="screen-reader-support"></a>Compatibilidad con lectores de pantalla (experimental)

La compatibilidad con lectores de pantalla es **experimental** y abarca las tareas principales del editor. Puede variar según el dispositivo, el sistema operativo y el lector; algunos controles y funciones avanzadas todavía pueden necesitar mejoras.

## <a name="screen-reader-activation"></a>Activar la edición con lector de pantalla

Activa el lector de pantalla en los ajustes de accesibilidad del dispositivo. En las versiones móviles que comunican su estado, Spck muestra automáticamente el documento activo en un campo de texto accesible. No hay que activar otro ajuste en el editor.

El campo expone el contenido y el nombre del archivo para leer, seleccionar y editar texto. Los cambios usan el guardado automático habitual; la selección permanece sincronizada y se mantienen las funciones de deshacer y rehacer. Cambiar de archivo actualiza el contenido y el nombre; los documentos de solo lectura siguen siendo de solo lectura. Desactivar el lector restaura el editor habitual en las versiones compatibles.

## <a name="screen-reader-navigation"></a>Navegación y controles

Las funciones compatibles incluyen:

- Etiquetas en el idioma de la interfaz para botones con iconos, pestañas de navegación y archivos, controles de búsqueda y acciones de control de versiones.
- Filas de archivos y proyectos activables con el lector o el teclado. Las carpetas indican si están expandidas; con un teclado físico, las flechas derecha e izquierda permiten expandirlas y contraerlas.
- Pestañas que indican el archivo activo y letras de estado Git que complementan los colores de los nombres de archivo.
- Ajustes asociados a sus etiquetas y estados, y campos de formulario que exponen los errores de validación.
- Diálogos con nombre que mantienen el foco del teclado dentro mientras están abiertos y lo devuelven al control de origen al cerrarse. Los menús de acciones reciben el foco al abrirse y lo devuelven al cerrarse con Escape.

Con un teclado físico, usa **Tab** para recorrer los controles, **Intro** o **Espacio** para activar botones y **Escape** para cerrar menús de acciones. También puedes usar los gestos habituales de navegación y activación del lector de pantalla.

## <a name="screen-reader-limitations"></a>Limitaciones actuales

- La edición accesible depende de que la aplicación móvil indique que el lector está activado. El navegador y el editor integrado no activan automáticamente este modo.
- La compatibilidad abarca actualmente las tareas principales anteriores. Las interacciones avanzadas y otras funciones de la aplicación pueden funcionar de forma diferente con cada lector.
- El comportamiento puede variar según la versión de la aplicación, el sistema y el dispositivo. Informa de controles inaccesibles o imposibles de activar, cambios inesperados de foco y problemas al leer o editar.

Consulta los [atajos de teclado](./editor#keyboard-shortcuts) para editar y la [compatibilidad y limitaciones de Git](./git-support#git-limitations) para conocer las diferencias entre Git móvil, del navegador y remoto.

## <a name="screen-reader-feedback"></a>Comentarios

[Envía tus comentarios a support@spck.io](mailto:support@spck.io) si un control no tiene nombre, se pierde el foco o la lectura o edición no funciona como esperabas. Incluye la versión de Spck, el dispositivo y sistema operativo, el lector de pantalla y los pasos para reproducir el problema.
