# <a name="getting-started"></a>Primeros Pasos

## <a name="getting-started-overview"></a>Visión General

Spck Editor es una solución de edición de código móvil con múltiples variantes diseñadas para desarrolladores.

### Versiones

#### Spck Editor (Gratis)

- Funcionalidad básica de edición de código móvil
- Integración Git nativa en Android e iOS; Git del navegador mediante isomorphic-git

#### Spck Editor Lite

**Precio**: Pago único
**Funciones**:

- Snippets Personalizados
- Teclado Predictivo
- Tema Neon Exclusivo
- Integración Git mejorada

#### Spck para NodeJS

**Plataforma**: Exclusivo de Android
**Función Principal**: Terminal integrada con soporte para NodeJS

La integración Git mejorada se incluye con una suscripción Node activa o se desbloquea permanentemente con la compra de acceso de por vida al terminal. Ambas opciones requieren iniciar sesión.

#### Versión para Navegador

- Incrustable en cualquier sitio web
- Interfaz ligera de edición de código

[Integrar el editor](./editor-embed)

### Características Principales

- Diseño mobile-first
- [Compatibilidad y limitaciones de Git](./git-support)
- Compatibilidad multiplataforma
- [Compatibilidad con lectores de pantalla (experimental)](./screen-reader-support)

### <a name="git-credentials"></a>Credenciales Git y pull requests

<a name="pull-request-management"></a>

Consulta [Compatibilidad con Git](./git-support) para la [configuración de tokens](./git-support#git-credentials), la [gestión de pull requests](./git-support#pull-request-management) y la [integración Git mejorada](./git-support#enhanced-git-integration).

### Uso Recomendado

- Edición de código sobre la marcha
- Modificaciones rápidas de proyectos
- Aprendizaje y prototipado

## <a name="getting-started-terminology"></a>Terminología

| Término             | Descripción                                                                                                                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Menú de Navegación  | Se refiere a la primera pestaña del menú lateral en dispositivos móviles, este menú no está disponible en la versión Navegador ni en modo Tablet |
| Menú de Archivos    | Se refiere a la pestaña _Archivo_ en el menú lateral o barra lateral                                                                 |
| Teclado Extra       | En dispositivos móviles existe un teclado adicional con símbolos de codificación de uso común para una inserción rápida              |
| Teclado Táctil      | Generalmente se refiere a la fila de teclas que contiene las teclas de flecha, la tecla tab y más                                    |
| Barra de Acción Táctil | Es el menú flotante que aparece sobre el cursor cuando se selecciona texto en un dispositivo móvil/táctil                          |
| Cursores Táctiles   | Los cursores en pantalla que aparecen en dispositivos móviles/táctiles cuando se selecciona texto o el cursor está activo            |
| Modo Tablet         | Se refiere a una configuración que se puede activar en dispositivos táctiles más grandes como tabletas                               |
| Tecla ⌘             | Este símbolo en el Teclado Táctil equivale a la tecla Ctrl en Windows o la tecla Command en Mac                                      |
| Tecla ⌥             | Este símbolo en el Teclado Táctil equivale a la tecla Alt en Windows o la tecla Option en Mac                                        |

&nbsp;

&nbsp;

# <a name="screen-reader-support"></a>Compatibilidad con lectores de pantalla (experimental)

La compatibilidad con lectores de pantalla es **experimental**. La [guía de lectores de pantalla](./screen-reader-support) explica la activación, edición, navegación con teclado, limitaciones y [comentarios](./screen-reader-support#screen-reader-feedback).

&nbsp;

&nbsp;

# <a name="keyboard-shortcuts"></a>Atajos de Teclado

## <a name="keyboard-shortcuts-overview"></a>Visión General

¡Desbloquea una eficiencia ultrarrápida con estos prácticos atajos de teclado! Aunque no es un catálogo completo, estas joyas potenciarán tu productividad y harán que la navegación sea pan comido.

### Aspectos Clave

- **No exhaustivo**: Una selección curada de los atajos más prácticos
- **Propósito**: Impulsar tu flujo de trabajo con comandos rápidos e intuitivos
- **Beneficio**: Ahorra tiempo y reduce la dependencia del ratón

> 💡 **Consejo Pro**: ¡Memoriza estos atajos y mira cómo se dispara tu productividad! 🌟

Puedes ver la lista completa de atajos en `Settings > Editor > Keyboard Shortcuts`

> Los usuarios premium también pueden acceder a los atajos de teclado directamente desde el Teclado Extra o usando el atajo `⌘ K`

> Habilita la tecla Ctrl/Command (⌘) y la tecla Alt/Option activando `Settings > Touch > Show ⌘ Key` y `Settings > Touch > Show ⌥ Key`

Para el foco del teclado, la activación de menús y la edición accesible, consulta [Compatibilidad con lectores de pantalla (experimental)](./screen-reader-support).

## <a name="keyboard-shortcuts-editor"></a>Editor

| Atajo  | Acción                                            |
| ------ | ------------------------------------------------- |
| ⌘ A    | Seleccionar todo                                  |
| ⌘ C    | Copiar                                            |
| ⌘ V    | Pegar                                             |
| ⌘ X    | Cortar                                            |
| ⌘ Z    | Deshacer                                          |
| ⌘ ⇧ Z  | Rehacer                                           |
| ⌘ D    | Duplicar línea                                    |
| ⌘ /    | Comentar/Descomentar línea                        |
| ⌥ F    | Formatear código                                  |
| ⌘ F    | Buscar                                            |
| ⌘ G    | Buscar siguiente (Funciona con texto seleccionado)|
| ⌘ ⇧ G  | Buscar anterior                                   |
| ⌘ L    | Saltar a línea                                    |

## <a name="keyboard-shortcuts-quick-actions"></a>Acciones Rápidas

| Atajo  | Acción                                              |
| ------ | --------------------------------------------------- |
| ⌘ ⇧ C  | Git Commit                                          |
| ⌘ O    | Abrir Archivos Recientes                            |
| ⌘ ⇧ P  | Iniciar Vista Previa del Proyecto                   |
| ⌘ P    | Alternar Vista Previa de Archivo (SVG, Markdown)    |
| ⌘ K    | **Supporter+**: Abrir Atajos                        |

&nbsp;

&nbsp;

# <a name="touch-settings"></a>Configuración Táctil

## <a name="touch-settings-extra"></a>Teclado Extra

- El Teclado Extra es un teclado de símbolos diseñado para dispositivos táctiles.
- Se puede acceder a teclas/símbolos adicionales manteniendo presionadas las teclas, lo que abre un menú de opciones.
- Puedes activarlo o desactivarlo en el menú `Settings > Touch > Extra Keyboard`.

> 💡 **Consejo Pro**: Consulta _**Edición Avanzada**_ para obtener consejos sobre cómo rodear texto, lo cual es compatible con el Teclado Extra.

## <a name="touch-settings-touch"></a>Teclado Táctil

- Las teclas táctiles consisten en una fila de teclas que incluye teclas de flecha, tecla Command y otras teclas de uso frecuente.
- Esta función está disponible en dispositivos táctiles.
- Puedes activarlo o desactivarlo en la sección `Settings > Touch > Touch Keyboard`.

> 💡 **Consejo Pro**: Puedes personalizar teclas individuales de este teclado ajustando la configuración.

## <a name="touch-settings-action-bar"></a>Barra de Acción Táctil

- Aparecerá una barra de acción con las opciones Copiar, Cortar y Pegar cuando se seleccione texto.
- Esta función se puede activar o desactivar en `Settings > Touch > Touch Action Bar`.

## <a name="touch-settings-cursors"></a>Cursores Táctiles

- Cursores en pantalla que aparecen cuando se selecciona texto o el cursor está activo.
- Esta función se puede activar o desactivar en `Settings > Touch > Touch Cursors`.

> 💡 **Consejo Pro**: No se recomienda desactivar esta función a menos que tengas un ratón/dispositivo señalador emparejado con el dispositivo móvil. Desactivar los cursores táctiles puede mejorar la visibilidad de la pantalla durante la edición y mejorar la experiencia de edición al usar dispositivos señaladores externos.

## <a name="touch-settings-predictive"></a>Teclas Predictivas

- Las Teclas Predictivas son una función premium que reemplaza al Teclado Extra estándar.
- Ofrece entrada de símbolos con un solo toque en lugar de tener que mantener presionado y seleccionar en el Teclado Extra regular.
- Las teclas se ordenan por la frecuencia estadística de los símbolos que aparecen en una posición específica del archivo.
- Se puede activar o desactivar en `Settings > Touch > Predictive Keyboard`.

> 💡 **Consejo Pro**: Las Teclas Predictivas reemplazan al Teclado Extra regular, que algunos usuarios pueden preferir. Las Teclas Predictivas son una opción predeterminada en la versión **Lite** del editor, y se pueden desactivar para recuperar el Teclado Extra regular.

&nbsp;

&nbsp;

# <a name="file-navigation"></a>Navegación de Archivos

## <a name="file-navigation-overview"></a>Visión General

- Hay múltiples métodos para navegar entre archivos
- Puedes navegar por los archivos usando Archivos en el menú lateral
- Puedes usar la ruta de navegación (breadcrumb) para navegar por los archivos comenzando desde el directorio del archivo actual
- Puedes abrir Archivos Recientes con `Ctrl-O` para buscar archivos rápidamente
- Puedes usar el ícono "Localizar" en el menú lateral de Archivos para identificar rápidamente los archivos actuales
- Los menús laterales de Control de Código Fuente y Búsqueda también ofrecen formas únicas de navegar entre archivos

## <a name="file-navigation-tabs"></a>Gestión de Pestañas de Archivos

### Comportamiento de las Pestañas

- Los archivos se desanclan automáticamente al abrirse inicialmente
- Las pestañas se anclan cuando se realizan ediciones

### Opciones de Ordenación de Pestañas

Los archivos se pueden ordenar por:

- Orden alfabético
- Extensión del archivo
- Ruta del archivo

### Canales de Navegación Alternativos

- **Menú de Control de Código Fuente**: Navega por los archivos a través del contexto de control de versiones
- **Menú de Búsqueda**: Encuentra y accede a archivos basándose en criterios de búsqueda

> 💡 **Consejo Pro**: Las Pestañas de Archivos se pueden ocultar de la vista en `Settings > Appearance > Show File Tabs`. Consulta _Modo Zen_ para maximizar el espacio de pantalla en dispositivos más pequeños.

&nbsp;

&nbsp;

# <a name="advanced-editing"></a>Edición Avanzada

## Usar el Teclado Predictivo de manera eficiente

### Selección Básica

- Doble toque para seleccionar una palabra o bloque de texto

### Rodear Texto

Rodea rápidamente el texto seleccionado utilizando pares de paréntesis o comillas:

- Paréntesis: `( )`
- Corchetes: `[ ]`
- Llaves: `{ }`
- Comillas simples: `' '`
- Comillas dobles: `" "`

### Navegación y Edición

#### Búsqueda de Texto

- `⌘ G`: Buscar siguiente instancia
- `⌘ ⇧ G`: Buscar instancia anterior

#### Sangría

- Selecciona un bloque de texto
- Presiona Tab para sangrar

&nbsp;

## <a name="multiple-cursors"></a>Múltiples Cursores

### Configuración Rápida

- ¡Activa múltiples cursores con la tecla Alt/Option! ✨
- Navega a `Settings > Touch > Show ⌥ Key` para activarlo

### Cómo Usar

1. Selecciona las teclas ⌥ y ⌘
2. Haz clic para colocar los cursores exactamente donde los quieras
3. ¡Edita múltiples líneas simultáneamente con facilidad! 💻

> 💡 **Consejo Pro**: ¡Edición con múltiples cursores = transformación de código ultrarrápida! ⚡️
> También es posible agregar múltiples cursores usando los comandos `Add Cursor Above` y `Add Cursor Below` de la paleta de comandos, que agregarían un cursor directamente encima o debajo de la posición actual del cursor.

&nbsp;

&nbsp;

# <a name="enhanced-git-integration"></a>Compatibilidad con Git

Consulta la [guía Git](./git-support) para credenciales, gestión de pull requests, inspección de commits y acceso a la integración Git mejorada.

<a name="merge-conflict-resolution"></a>

Git básico incluye la [resolución de conflictos](./git-support#merge-conflict-resolution) en el visor con **Accept Current**, **Accept Incoming**, **Accept Both** y **Resolve**.

## <a name="git-limitations"></a>Limitaciones de Git

<a name="git-limitations-overview"></a>
<a name="git-limitations-memory"></a>
<a name="git-limitations-symlinks"></a>
<a name="git-limitations-cli"></a>

Android e iOS usan libgit2 nativo para proyectos locales; el navegador usa isomorphic-git y los proyectos remotos, el binario Git del anfitrión. Consulta las [limitaciones de Git](./git-support#git-limitations) para almacenamiento, memoria, enlaces simbólicos y alternativas remotas.

&nbsp;

&nbsp;

# <a name="zen-mode"></a>🌟 Modo Zen

## Visión General

El Modo Zen es una configuración del editor encantadora y maximizadora del espacio diseñada para transformar tu experiencia de codificación en pantallas compactas.

El modo Zen consiste en:

- Desactivar `Show Line Numbers` en la configuración
- Desactivar `Show File Tab`
- Desactivar `Touch Action Bar`

### Características Principales

#### 🧘‍♀️ Espacio de Pantalla Maximizado

- **¡Adiós a los Números de Línea!**
  - Libera un valioso espacio horizontal
  - Evita que el texto se sienta apretado
  - Adopta el aspecto limpio y minimalista

#### 🎨 Interfaz Optimizada

- **Minimización de la Barra de Acción**
  - Despídete de las barras de herramientas saturadas
  - Utiliza métodos de entrada alternativos:
    - Botones de pegar/cortar del teclado extra
    - Atajos de teclado (`Ctrl-C/Ctrl-V`)

#### 📂 Navegación Simplificada

- **Eliminación de Pestañas de Archivos**
  - `Ctrl-O` se convierte en tu nuevo mejor amigo de navegación
  - Espacio de trabajo más limpio
  - Cambio de contexto más rápido

> 💡 **Consejo Pro**: ¡No todos los estilos de codificación son iguales! Recomendamos experimentar con el Modo Zen para ver si resuena con tu flujo de trabajo. ¡Tu entorno de codificación perfecto está a solo unos clics de distancia! 🌈✨
