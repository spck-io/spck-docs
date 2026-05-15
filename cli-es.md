# <a name="cli-reference"></a>Referencia CLI

## <a name="key-features"></a>Características Principales

- **Sistema de archivos remoto**: Accede y edita archivos locales desde la aplicación móvil Spck Editor
- **Integración con Git**: Operaciones git completas (commit, push, pull, gestión de ramas) — requiere Git 2.20.0+
- **Acceso al terminal**: Sesiones de terminal interactivas con xterm.js
- **Proxy de navegador**: Previsualiza tu servidor local en una vista de navegador a pantalla completa dentro de Spck Editor
- **Búsqueda rápida**: Búsqueda de archivos optimizada con detección automática de ripgrep (100x más rápido cuando está instalado)
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

### El Código QR No Se Escanea

- Verificar que la aplicación Spck Editor esté instalada antes de escanear
- Usar entrada manual: Projects → New Project → Link Remote Server
- Usar la aplicación de Cámara nativa, no escáneres de terceros

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

El número máximo de conexiones CLI simultáneas y los límites de uso diario dependen de tu tipo de cuenta:

| Plan      | Conexiones CLI | Límite Diario |
| --------- | -------------- | ------------- |
| Free      | 1              | 30 minutos    |
| Supporter | 2              | Ilimitado     |
| Gold      | 5              | Ilimitado     |

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
