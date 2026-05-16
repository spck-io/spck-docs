# <a name="getting-started"></a>Primeros pasos con Spck CLI

## <a name="overview"></a>Descripción general

Spck CLI es una herramienta de línea de comandos que conecta tu entorno de desarrollo local con la aplicación móvil Spck Editor a través de una conexión WebSocket segura. Una vez en ejecución, puedes explorar y editar archivos locales, ejecutar comandos de terminal y previsualizar servidores locales, todo desde tu teléfono o tablet.

## <a name="requirements"></a>Requisitos

### Obligatorios

- **Node.js**: 18.0.0 o superior
- **Cuenta de Spck Editor**: Cuenta gratuita (30 min/día) o suscripción Premium (ilimitada)
- **Aplicación móvil Spck Editor**: [Android](https://play.google.com/store/apps/details?id=io.spck) o [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Opcionales (Recomendados)

- **Git**: 2.20.0+ para funciones de integración con Git
- **ripgrep**: 15.0.0+ para búsqueda de archivos significativamente más rápida (mejora de 100x)

## <a name="installation"></a>Instalación

### Opción 1: Ejecutar con npx (Sin instalación)

```bash
npx spck
```

Siempre usa la versión más reciente; perfecto para la configuración inicial o el uso ocasional.

### Opción 2: Instalación global

```bash
npm install -g spck
spck
```

Inicio más rápido, funciona sin conexión y resulta conveniente para el uso diario.

## <a name="demo"></a>Demo

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

Una vez que el CLI está en ejecución, muestra un código QR y los detalles de conexión.

### Método 1: Código QR (Recomendado)

**IMPORTANTE**: Instala la aplicación Spck Editor ANTES de escanear el código QR.

**En Android:**

1. Usa la aplicación de cámara o el escáner QR de los ajustes rápidos
2. Al detectarlo, toca la notificación para abrir Spck Editor
3. La aplicación se conecta automáticamente

> 💡 **Nota**: Algunos lectores de códigos QR no pueden gestionar el esquema personalizado para abrir Spck Editor directamente. Copia la URL y pégala en Chrome, que lanzará Spck Editor desde la URL.

**En iOS:**

1. Usa la aplicación de cámara o el escáner QR del Centro de control
2. Al detectarlo, toca la notificación para abrir Spck Editor
3. La aplicación se conecta automáticamente

> 💡 **Nota**: Spck Editor NO tiene un escáner QR integrado. Usa la función QR nativa de tu dispositivo.

### Método 2: Entrada manual

Si el código QR no funciona:

1. Abre Spck Editor → **Proyectos** → **Nuevo proyecto** → **Vincular servidor remoto**
2. Ingresa el **ID de cliente** y el **secreto** que se muestran en el terminal
3. Toca **Conectar**

## <a name="next-steps"></a>Próximos pasos

1. **Entender el sistema de retransmisión**: Aprende cómo el CLI enruta el tráfico y cómo elegir un servidor; consulta la [Referencia CLI](./cli)
2. **Configurar tu entorno**: Ajusta la configuración del terminal, seguridad y sistema de archivos; consulta [Configuración](./cli-config)
3. **Explorar funciones avanzadas**: Comandos CLI, agentes de codificación con IA, múltiples proyectos; consulta [Uso avanzado](./cli-advanced)
4. **Transferir archivos entre dispositivos**: Copia proyectos entre tu teléfono y escritorio de forma inalámbrica; consulta [Transferencia de archivos](./cli-file-transfer)
5. **Mantener sesiones activas**: Comparte sesiones entre dispositivos con tmux; consulta [Uso de Tmux](./tmux)
