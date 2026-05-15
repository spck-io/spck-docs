# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>Descripción general

La Spck CLI incluye un puente completo de Language Server Protocol (LSP) que ejecuta servidores de lenguaje para TypeScript, JavaScript, Python, HTML, CSS y SCSS directamente en tu host remoto. Cuando se conecta a una sesión de CLI, Spck Editor utiliza automáticamente el servidor de lenguaje remoto en lugar del integrado en el dispositivo móvil.

> 💡 **Consejo**: Para obtener una descripción del servidor de lenguaje integrado disponible sin la CLI, consulta [Editor Language Server](./editor-language-server).

## <a name="cli-ls-architecture"></a>Arquitectura

El servidor de lenguaje de la CLI se ejecuta en la misma máquina que los archivos de tu proyecto. Esto ofrece varias ventajas significativas sobre el enfoque basado en navegador utilizado en dispositivos móviles:

### Sin transmisión de archivos

Con el servidor de lenguaje móvil integrado, los archivos deben transmitirse al dispositivo y cargarse en un worker del navegador antes de que el servidor pueda analizarlos. Con la CLI, el servidor de lenguaje lee los archivos directamente desde el disco, sin necesidad de transmisión. Esto elimina el consumo de ancho de banda y mantiene el análisis rápido incluso en proyectos grandes.

### Conocimiento completo del proyecto

El servidor de lenguaje de la CLI tiene acceso a todo el directorio de tu proyecto, incluyendo:

- Todos los archivos fuente en cada subdirectorio
- `node_modules/` para la resolución de tipos de terceros
- Archivos `tsconfig.json` descubiertos automáticamente en cualquier nivel
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` y archivos de declaración asociados

Esto significa que ir a definición, buscar referencias y renombrar símbolo funcionan correctamente entre archivos, incluso cuando no los has abierto en el editor.

### Manejo correcto de `tsconfig.json`

El servidor de lenguaje de TypeScript descubre y respeta automáticamente el `tsconfig.json` (o `jsconfig.json`) de tu proyecto. Los alias de rutas (`paths`), las opciones del compilador (`strict`, `target`, `lib`), las referencias de proyecto y los diseños de workspace en monorepos se gestionan correctamente. El servidor de lenguaje móvil integrado no puede leer `tsconfig.json` porque no tiene acceso al sistema de archivos al iniciarse.

### Proceso persistente

El proceso del servidor de lenguaje permanece activo durante toda la sesión de CLI. Construye un índice en memoria de tu proyecto y lo mantiene activo entre ediciones, por lo que las respuestas siguen siendo rápidas incluso después del inicio inicial.

## <a name="cli-ls-features"></a>Funciones admitidas

| Función | Descripción |
| --- | --- |
| **Autocompletado** | Sugerencias con reconocimiento de contexto con firmas de tipos, ordenadas por relevancia |
| **Información al pasar el cursor** | Información de tipos y documentación JSDoc para el símbolo bajo el cursor |
| **Ayuda de firma** | Sugerencias de parámetros y documentación al escribir una llamada a función |
| **Ir a definición** | Salta a la declaración de cualquier símbolo, incluidos los de `node_modules` |
| **Buscar referencias** | Lista cada uso de un símbolo en todo el proyecto |
| **Renombrar símbolo** | Renombra un símbolo y actualiza todas las referencias de forma atómica |
| **Diagnósticos** | Resaltado de errores y advertencias en tiempo real mientras escribes |
| **Renderizado Markdown** | Documentación de hover y firma renderizada como Markdown con bloques de código con resaltado de sintaxis |

## <a name="cli-ls-languages"></a>Lenguajes admitidos

| Lenguaje | Autocompletado | Hover | Firmas | Diagnósticos |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>Configuración

La compatibilidad con el servidor de lenguaje está habilitada de forma predeterminada. Puedes controlarla en tu archivo de configuración:

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

- **`languageServer.enabled`** (boolean): Interruptor principal para todos los servidores de lenguaje remotos. Predeterminado: `true`.
- **`languageServer.typescript.enabled`** (boolean): Habilitar el servidor de lenguaje TypeScript/JavaScript. Predeterminado: `true`.
- **`languageServer.python.enabled`** (boolean): Habilitar el servidor de lenguaje Python (requiere `pylsp` en el `PATH`). Predeterminado: `true`.

## <a name="cli-ls-requirements"></a>Requisitos

- **TypeScript / JavaScript**: Incluido con la CLI. No se requiere instalación adicional.
- **Python**: Requiere [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) (`pip install python-lsp-server`).
- **HTML / CSS / SCSS**: Incluido con la CLI. No se requiere instalación adicional.

## <a name="cli-ls-vs-mobile"></a>CLI vs. servidor de lenguaje móvil

| Capacidad | CLI Language Server | Integrado en móvil |
| --- | --- | --- |
| Acceso completo a archivos del proyecto | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| Resolución de tipos en `node_modules` | ✓ | — |
| Ir a definición entre archivos | ✓ | Limitado |
| Buscar referencias entre archivos | ✓ | — |
| Renombrar símbolo | ✓ | — |
| Compatibilidad con Python | ✓ | — |
| Funciona sin conexión (sin CLI) | — | ✓ |

&nbsp;

&nbsp;
