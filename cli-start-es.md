# <a name="getting-started"></a>Primeros pasos con Spck CLI

## <a name="overview"></a>Descripción general

Spck CLI sale de beta. Conecta tu ordenador a Spck Editor en tu teléfono o tableta para editar archivos, usar Git y terminales y previsualizar servidores locales. Las conexiones usan un relay cifrado o una conexión directa [Fast Lane](./cli#fast-lane) (Supporter y Gold).

## <a name="requirements"></a>Requisitos

Lite permite editar proyectos ubicados en tu computadora o en una VM pública mediante Spck CLI. Los proyectos remotos requieren una **cuenta de Spck y una suscripción activa de Spck**, aparte de la compra única de Lite. La suscripción ayuda a cubrir los costos continuos de alojamiento, operación y mantenimiento de los servidores de Spck. Las herramientas locales de edición y Git incluidas siguen disponibles sin suscripción.

### Obligatorios

- **Node.js**: **22.22.2+ (22.x), 24.15.0+ (24.x), o 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Cuenta de Spck Editor**: Cuenta gratuita (30 min/día) o suscripción Premium (ilimitada)
- **Aplicación móvil Spck Editor**: [Android](https://play.google.com/store/apps/details?id=io.spck) o [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Opcionales (Recomendados)

- **Git**: 2.20.0+ para la [integración Git](./git-support#git-limitations-cli) en proyectos remotos
- **ripgrep**: 15.0.0+ para búsqueda de archivos significativamente más rápida (mejora de 100x)

## <a name="installation"></a>Instalación

### Opción 1: Ejecutar con npx (Sin instalación)

```bash
npx spck@latest
```

Solicita la última versión de la CLI; ideal para la primera configuración o el uso ocasional. `npx spck` puede reutilizar una versión instalada.

### Opción 2: Instalación global

```bash
npm install -g spck
spck
```

Instala una vez y ejecuta `spck` a diario. Actualiza con `npm install -g spck@latest`. Las conexiones remotas siguen necesitando Internet.

## <a name="demo"></a>Demo

[Mira el vídeo de Spck CLI](https://youtu.be/EtfEhd5EmKM), incluida la nueva función Fast Lane.

Un breve recorrido conectando Spck CLI a la app móvil y editando archivos locales de forma remota:

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>Configuración inicial

Al ejecutar el CLI por primera vez, un asistente de configuración interactivo te guía a través del proceso:

### 1. Autenticación

```bash
spck
# Pulsa ENTER para abrir el navegador
# Inicia sesión con tu cuenta de Spck Editor
# Autoriza el CLI
# Regresa al terminal
```

Las credenciales se almacenan en `~/.spck-editor/.credentials.json` y persisten entre sesiones.

Si el navegador no puede acceder a localhost, el inicio de sesión usa el relay. Usa el QR de inicio de sesión o el enlace que muestra la CLI para autenticarte desde otro dispositivo. Este código es distinto del QR de conexión al proyecto.

### 2. Configuración del proyecto

El asistente configurará:

- **Directorio raíz**: Directorio base para el acceso a archivos (por defecto: directorio actual)
- **Nombre del proyecto**: Nombre visible en la aplicación móvil (por defecto: nombre del directorio)

### 3. Integración con Git (Opcional)

Si se detecta un archivo `.gitignore`, el CLI ofrece añadir `.spck-editor/` para evitar confirmar secretos accidentalmente:

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**Recomendación**: Elige `Y` para proteger las credenciales de conexión.

### Volver a ejecutar la configuración

Para reconfigurar en cualquier momento:

```bash
spck --setup
```

## <a name="connecting"></a>Conectarse a Spck Editor

En un proyecto nuevo, la CLI muestra el QR de conexión hasta que un editor se conecta correctamente. Los siguientes inicios abren el panel directamente; pulsa **`c`** para volver a mostrar el QR y los datos de conexión, o **`l`** para ver los registros. Amplía el terminal si el QR no cabe.

### Método 1: Código QR (Recomendado)

1. Abre Spck Editor → **Proyectos** → **Nuevo proyecto** → **Vincular servidor remoto**
2. Toca el icono de código QR
3. Escanea el código QR que aparece en el terminal. La aplicación se conecta automáticamente.

> 💡 **Nota**: También puedes escanear el código con la app Cámara de tu dispositivo, que abre el enlace en Spck Editor si la aplicación está instalada.

### Método 2: Entrada manual

Si no puedes escanear el código QR:

1. Abre Spck Editor → **Proyectos** → **Nuevo proyecto** → **Vincular servidor remoto**
2. Ingresa el **ID de cliente** y el **secreto** que se muestran en el terminal
3. Selecciona el servidor de retransmisión que aparece en el terminal
4. Toca **Conectar**

Si está activado **Require PIN to connect**, introduce el PIN elegido en el panel de la CLI. La app no lo guarda. Consulta [PIN de conexión](./cli-config#connection-pin).

## <a name="next-steps"></a>Próximos pasos

1. **Entender el sistema de retransmisión**: Aprende cómo el CLI enruta el tráfico y cómo elegir un servidor; consulta la [Referencia CLI](./cli)
2. **Configurar tu entorno**: Ajusta la configuración del terminal, seguridad y sistema de archivos; consulta [Configuración](./cli-config)
3. **Explorar funciones avanzadas**: Comandos CLI, agentes de codificación con IA, múltiples proyectos; consulta [Uso avanzado](./cli-advanced)
4. **Transferir archivos entre dispositivos**: Copia proyectos entre tu teléfono y escritorio de forma inalámbrica; consulta [Transferencia de archivos](./cli-file-transfer)
5. **Mantener sesiones activas**: Comparte sesiones entre dispositivos con tmux; consulta [Uso de Tmux](./tmux)
