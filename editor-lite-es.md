# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Descripcion general

Spck Editor Lite es una version de compra unica de Spck Editor que desbloquea funciones de edicion premium sin necesidad de suscripcion. Esta disponible como una aplicacion independiente tanto en Android como en iOS.

Lite incluye todo lo de la version gratuita, ademas de:

- **Predictive Keyboard** -- sugerencias de simbolos contextuales en el teclado adicional
- **Snippets personalizados** -- plantillas de codigo definidas por el usuario con marcadores de tabulacion
- **Tema Neon** -- un tema de editor exclusivo

Estas funciones tambien estan disponibles en la version completa de Spck Editor con una suscripcion Gold o Supporter activa. La aplicacion Lite ofrece la misma funcionalidad como compra unica.

## <a name="predictive-keyboard"></a>Predictive Keyboard

El Predictive Keyboard reemplaza el teclado adicional estandar con una fila de teclas de simbolos contextuales. En lugar de mantener presionada una tecla para elegir de un menu, los simbolos mas probables se muestran directamente segun la posicion del cursor en el archivo.

### Como funciona

Las predicciones se generan a partir de tablas de frecuencia estadistica construidas por lenguaje. Cuando el cursor se mueve, el teclado reordena los simbolos segun la frecuencia con la que cada uno aparece en ese tipo de posicion en codigo real. Los lenguajes compatibles incluyen JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown y texto plano.

### Activar o desactivar

Ve a `Settings > Touch > Predictive Keyboard` para activar o desactivar la funcion. En Lite, el Predictive Keyboard esta activado por defecto. Desactivarlo restaura el teclado adicional estandar.

> El Predictive Keyboard solo esta disponible en dispositivos tactiles. No aparece cuando se usa un teclado fisico o en modo tableta con un teclado externo conectado.

## <a name="custom-snippets"></a>Snippets personalizados

Los snippets personalizados te permiten crear plantillas de codigo reutilizables que aparecen en la lista de autocompletado mientras escribes. Cada snippet esta asociado a un lenguaje especifico, por lo que tus snippets de JavaScript no aparecen en archivos Python.

### Crear un snippet

1. Abre `Settings > Editor > Custom Snippets`
2. Selecciona el lenguaje (por ejemplo, JavaScript, Python, HTML)
3. Toca **Agregar snippet**
4. Ingresa un **disparador** -- la abreviatura que escribes para invocar el snippet
5. Ingresa el **cuerpo** -- el codigo que se inserta

### Tabulaciones y marcadores

Los snippets admiten tabulaciones para que el cursor salte entre posiciones editables despues de la insercion:

- `$1`, `$2`, `$3` -- tabulaciones numeradas en orden de recorrido
- `$0` -- posicion final del cursor despues de todas las tabulaciones
- `${1:defaultText}` -- una tabulacion con texto de marcador preseleccionado para facilitar el reemplazo

Ejemplo -- un snippet de bucle `for` en JavaScript:

**Disparador:** `forloop`

**Cuerpo:**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

Al escribir `forloop` y seleccionarlo del autocompletado, se inserta el bucle completo. Presiona Tab para saltar entre `i`, `array` y el cuerpo del bucle.

### Importar y exportar

Puedes exportar todos los snippets a un archivo e importarlos en otro dispositivo. Esto es util para compartir colecciones de snippets entre telefonos o hacer una copia de seguridad de tu configuracion.

## <a name="neon-theme"></a>Tema Neon

Lite incluye el tema de editor **Neon**, un tema oscuro con colores de acento vibrantes. Esta establecido como tema predeterminado en Lite y se puede cambiar en cualquier momento en `Settings > Appearance > Theme`.

## <a name="comparison"></a>Comparacion de funciones

| Funcion | Gratuito | Lite (Compra unica) | Completo (Suscripcion) |
| --- | :---: | :---: | :---: |
| Edicion de codigo y resaltado de sintaxis | Si | Si | Si |
| Integracion con Git | Si | Si | Si |
| Teclado adicional | Si | Si | Si |
| Teclado tactil y cursores | Si | Si | Si |
| Vista previa del proyecto | Si | Si | Si |
| Predictive Keyboard | -- | Si | Gold / Supporter |
| Snippets personalizados | -- | Si | Gold / Supporter |
| Tema Neon | -- | Si | -- |
| Asistente de IA | -- | -- | Si |
| Cuentas de usuario y sincronizacion en la nube | -- | -- | Si |
| Labs / Proyectos de la comunidad | -- | -- | Si |
