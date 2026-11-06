# <a name="cli-reference"></a>Referencia CLI

## <a name="key-features"></a>Características Principales

- **Sistema de archivos remoto**: Accede y edita archivos locales desde la aplicación móvil Spck Editor
- **Integración con Git**: Operaciones git completas (commit, push, pull, gestión de ramas) — requiere Git 2.20.0+
- **Acceso al terminal**: Sesiones de terminal interactivas con xterm.js
- **Proxy de navegador**: Previsualiza tu servidor local en una vista de navegador a pantalla completa dentro de Spck Editor
- **Búsqueda rápida**: Búsqueda de archivos optimizada con detección automática de ripgrep (100x más rápido cuando está instalado)
- **Agentes de IA locales (ACP)**: Controla Claude Code, Codex o Gemini CLI desde el Chat de IA de Spck Editor a través del [Agent Client Protocol](https://agentclientprotocol.com/). El agente se ejecuta en tu máquina con tu propia suscripción. Consulta [Agentes de IA en el móvil (ACP)](./cli-acp).
- **Fast Lane** (Supporter y Gold): Conexión directa peer-to-peer por WebRTC entre Spck Editor y la CLI, el doble de rápida que el relay en promedio. Consulta [Fast Lane](#fast-lane).
- **Seguro**: Solicitudes firmadas criptográficamente con autenticación Firebase opcional

## <a name="relay-server"></a>Servidor Relay

La CLI se conecta a Spck Editor a través de un servidor relay que reenvía mensajes entre ambos. En la primera ejecución, la CLI selecciona automáticamente el servidor relay con la menor latencia y guarda la preferencia en `~/.spck-editor/.credentials.json`.

**IMPORTANTE**: Tanto la CLI como el cliente Spck Editor deben usar el mismo servidor relay para conectarse. Si el cliente no puede encontrar la CLI, verifica que ambos lados hayan seleccionado el mismo servidor relay.

### Servidores Relay Disponibles

| Región        | URL                 |
| ------------- | ------------------- |
| Europa        | `cli-eu-1.spck.io`  |
| Norteamérica  | `cli-na-1.spck.io`  |
| Asia del Sur  | `cli-sas-1.spck.io` |
| Asia del Este | `cli-ea-1.spck.io`  |

### Sobrescribir el Servidor Relay

```bash
# Usar un servidor relay específico
spck --server cli-eu-1.spck.io

# Forma corta
spck -s cli-na-1.spck.io
```

La sobrescritura se guarda y reutiliza en ejecuciones posteriores. Para volver a ejecutar la selección automática, borra tus credenciales y reinicia:

```bash
spck --logout
spck
```

### Elegir un Servidor Relay en Spck Editor

Cuando te conectes desde la aplicación móvil vía **Link Remote Server**, selecciona el mismo servidor relay del menú desplegable **Relay Server** que la CLI está usando. El nombre del servidor relay se muestra en la salida de la CLI después de conectarse.

## <a name="fast-lane"></a>Fast Lane

Fast Lane es una función premium para suscriptores **Supporter** y **Gold**. En lugar de enviar cada mensaje a través del servidor relay, Spck Editor se conecta **directamente a tu CLI** mediante WebRTC (peer-to-peer). Al eliminar el salto por el relay y reducir los viajes de ida y vuelta, Fast Lane es **el doble de rápido que el relay en promedio**, por lo que las operaciones con archivos, la búsqueda, Git y la entrada del terminal responden de forma notablemente más ágil.

El servidor relay sigue siendo necesario: es donde se registra tu CLI y media en el handshake inicial entre el editor y la CLI. Una vez establecida la ruta directa, los datos de tu proyecto circulan por ella en lugar de pasar por el relay.

### Requisitos

- Una suscripción activa **Supporter** o **Gold** en la cuenta con la que ha iniciado sesión la CLI
- Spck CLI **0.7.0 o posterior** (`npm i -g spck`)
- Compatibilidad con WebRTC tanto en el dispositivo que ejecuta Spck Editor como en la máquina que ejecuta la CLI

### Activar o desactivar Fast Lane

**En Spck Editor:** Abre **Link Remote Server** (o edita una conexión existente desde el menú) y usa el interruptor **⚡ Fast Lane**. Está activado de forma predeterminada para las conexiones nuevas en cuentas Supporter y Gold.

**En la CLI:** Fast Lane está habilitado de forma predeterminada. Pulsa **`f`** en el panel de la CLI para activarlo o desactivarlo en el proyecto actual, o establece `fastLane.enabled` en la [configuración del proyecto](./cli-config#fast-lane-settings). Los cambios se aplican tras reiniciar la CLI. Desactívalo en redes que bloqueen el tráfico peer-to-peer.

El panel de la CLI muestra el estado actual de Fast Lane (activo, disponible, desactivado o no disponible en esta plataforma), y el panel de archivos de Spck Editor indica qué transporte se está usando junto con el ping actual, por ejemplo `Fast Lane · 24 ms` o `Relay · 80 ms`.

### Respaldo automático

Si no se puede establecer una conexión directa, Spck Editor recurre automáticamente al relay para que puedas seguir trabajando, y muestra un aviso con el motivo. Motivos habituales:

- La CLI está desactualizada — actualízala con `npm i -g spck`
- Fast Lane está desactivado en la configuración del proyecto de la CLI
- WebRTC no está disponible en la máquina que ejecuta la CLI ni en tu dispositivo
- El servidor relay aún no es compatible con Fast Lane
- La red bloquea la ruta peer-to-peer directa (por ejemplo, un firewall corporativo estricto o un NAT)

### Seguridad

El tráfico de Fast Lane se cifra de extremo a extremo con WebRTC (DTLS). Además, el handshake de autenticación de la CLI está vinculado a la sesión DTLS concreta, de modo que la CLI debe demostrar que posee el secreto de tu conexión en ese mismo canal antes de intercambiar cualquier dato del proyecto. Todas las solicitudes siguen firmándose criptográficamente, igual que en el relay. Consulta [Seguridad de la CLI](./cli-config#security).

## <a name="daily-workflow"></a>Flujo de Trabajo Diario

### Iniciar tu Sesión

```bash
cd /path/to/project
spck
# Conectar desde la aplicación móvil (se conecta automáticamente al servidor guardado)
# Comenzar a programar
```

### Editar Archivos

1. Explorar archivos en la aplicación móvil
2. Tocar para abrir y editar
3. Los archivos se guardan automáticamente en tu computadora

### Ejecutar Comandos Git

**Opción 1 - GUI de la aplicación móvil:**

- Abrir el panel Git
- Ver cambios, preparar archivos
- Hacer commit y push

**Opción 2 - Terminal:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### Sesiones de Terminal

Toca el icono de terminal en la aplicación móvil para acceso completo al shell con tus permisos de usuario.

### Finalizar tu Sesión

```bash
# Mantener la CLI ejecutándose para reconexiones rápidas (recomendado)
# O detener con Ctrl+C
```

## <a name="troubleshooting"></a>Solución de Problemas

### Directorio Raíz No Encontrado

```bash
# Reconfigurar con la ruta correcta
spck --setup

# O especificar directamente
spck --root /correct/path/to/project
```

### Configuración Corrupta

```bash
# Borrar configuración y empezar de nuevo
spck --logout
spck --setup
```

### Problemas de Conexión

1. Verificar la conexión a internet
2. Verificar que tanto la CLI como Spck Editor estén usando el **mismo servidor relay** (se muestra en la salida de la CLI después de conectarse)
3. Intentar cerrar sesión y reconectar:
   ```bash
   spck --logout
   spck
   ```
4. Verificar la configuración del firewall — asegurarse de que las conexiones WebSocket (puerto 443) estén permitidas
5. Si ves un aviso de que Fast Lane no está disponible y se usa el relay, la conexión sigue funcionando a través del relay. Consulta [Fast Lane](#fast-lane), sección «Respaldo automático», para ver los motivos y las soluciones

### El Código QR No Se Escanea

- Escanea desde Spck Editor: Proyectos → Nuevo proyecto → Vincular servidor remoto y toca el icono de código QR
- Si el terminal es demasiado pequeño para mostrar el código, la CLI indica el tamaño que necesita. Amplía la ventana o introduce los datos a mano en el mismo cuadro de diálogo
- Evita los escáneres de terceros, que podrían exponer tu clave secreta

### Las Operaciones Git No Funcionan

1. Verificar que Git esté instalado:

   ```bash
   git --version  # Requiere 2.20.0+
   ```

2. Instalar si es necesario:

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Descargar de git-scm.com
   ```

### Rendimiento de Búsqueda Lento

Instala ripgrep para búsqueda 100x más rápida:

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# La CLI detecta y usa ripgrep automáticamente
```

### Permiso Denegado

```bash
# Ver permisos
ls -la /path/to/file

# Corregir si es necesario
chmod 644 /path/to/file

# No usar sudo - la CLI debe ejecutarse como el usuario propietario de los archivos
```

## <a name="connection-limits"></a>Límites de Conexión

Lite permite editar proyectos ubicados en tu computadora o en una VM pública mediante Spck CLI. Los proyectos remotos requieren una **cuenta de Spck y una suscripción activa de Spck**, aparte de la compra única de Lite. La suscripción ayuda a cubrir los costos continuos de alojamiento, operación y mantenimiento de los servidores de Spck. Las herramientas locales de edición y Git incluidas siguen disponibles sin suscripción.

El número máximo de conexiones CLI simultáneas y los límites de uso diario dependen de tu tipo de cuenta:

| Plan      | Conexiones CLI | Límite Diario | Fast Lane |
| --------- | -------------- | ------------- | --------- |
| Free      | 1              | 30 minutos    | —         |
| Supporter | 2              | Ilimitado     | ✓         |
| Gold      | 5              | Ilimitado     | ✓         |

El uso del nivel gratuito se reinicia diariamente a las 12:00 AM UTC.

Cuando se alcanza el límite de conexiones:

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

Cuando se alcanza el límite diario gratuito:

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

Verificar conexiones activas:

```bash
spck --account
```

> 💡 **Nota**: Solo un dispositivo móvil puede conectarse a una instancia CLI a la vez. Cada instancia CLI usa un slot de conexión.

## <a name="support"></a>Soporte

- **Sitio web**: [https://spck.io](https://spck.io)
- **Soporte**: Contactar a través de la aplicación móvil Spck Editor
