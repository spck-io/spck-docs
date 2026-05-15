# <a name="cli-advanced-usage"></a>Uso avanzado del CLI

## <a name="cli-commands"></a>Comandos del CLI

### Comandos básicos

```bash
# Iniciar el CLI
spck

# Ejecutar el asistente de configuración
spck --setup

# Mostrar información de la cuenta
spck --account

# Cerrar sesión y borrar credenciales
spck --logout

# Mostrar ayuda
spck --help

# Mostrar versión
spck --version
```

### Opciones avanzadas

```bash
# Usar un archivo de configuración personalizado
spck --config /path/to/config.json
spck -c /path/to/config.json

# Sobreescribir el directorio raíz
spck --root /path/to/project
spck -r /path/to/project

# Sobreescribir el servidor de retransmisión (p. ej., usar una región específica)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>Agentes de codificación con IA

El terminal Spck CLI te da acceso completo al shell, lo que significa que puedes ejecutar agentes de codificación con IA directamente desde tu dispositivo móvil. Estos agentes pueden leer, escribir y refactorizar código en tu proyecto mientras supervisas desde Spck Editor.

> 💡 **Consejo**: Usa **tmux** para mantener las sesiones de agentes de IA en ejecución incluso después de desconectarte. Inicia una sesión tmux en tu escritorio (`tmux new -s code`), lanza el agente de IA y luego reconéctate desde el terminal Spck CLI en tu teléfono (`tmux attach -t code`). Esto te permite cambiar sin problemas entre escritorio y móvil sin perder el contexto. Consulta [Uso de Tmux](./tmux) para obtener una guía completa, incluida la configuración de un servidor remoto persistente.

## <a name="advanced-usage"></a>Uso avanzado

### Múltiples proyectos

Ejecuta instancias separadas del CLI para distintos proyectos de forma simultánea:

```bash
# Terminal 1: Proyecto A
cd /path/to/projectA
spck

# Terminal 2: Proyecto B
cd /path/to/projectB
spck
```

Cada proyecto mantiene su propia configuración y conexión.

> 💡 **Consejo**: También puedes usar varias instancias del CLI para transferir archivos entre tu escritorio y tu teléfono. Consulta [Transferencia de archivos entre móvil y escritorio](./cli-file-transfer) para obtener una guía paso a paso.

### Archivos de configuración personalizados

Crea configuraciones especializadas para distintos escenarios:

```bash
# Configuración de desarrollo
spck --config ~/configs/dev-config.json

# Configuración de producción (solo lectura, sin terminal)
spck --config ~/configs/prod-config.json
```

### Configuración específica por entorno

**Desarrollo local:**

```json
{
  "security": {
    "userAuthenticationEnabled": false
  },
  "terminal": {
    "enabled": true
  }
}
```

**Servidor de producción:**

```json
{
  "security": {
    "userAuthenticationEnabled": true
  },
  "terminal": {
    "enabled": false
  }
}
```

### Alto uso de CPU

Reduce la supervisión de archivos añadiendo más patrones de exclusión:

```json
{
  "filesystem": {
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/dist/**",
      "**/build/**",
      "**/.next/**",
      "**/coverage/**",
      "**/.cache/**"
    ]
  }
}
```

Limita los terminales simultáneos:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>Reducir el prompt del shell para móvil

En dispositivos móviles, el espacio horizontal en pantalla es limitado. El prompt predeterminado del shell —que normalmente incluye la ruta del directorio actual, el nombre de usuario y el nombre del host— puede saturar el terminal y dificultar la lectura de la salida de los comandos.

Cambiar el prompt a simplemente `$ ` ofrece una experiencia de terminal mucho más limpia en pantallas pequeñas.

### Bash

Añade lo siguiente a `~/.bashrc`:

```bash
export PS1='\$ '
```

Aplícalo sin reiniciar el shell:

```bash
source ~/.bashrc
```

### Zsh

Añade lo siguiente a `~/.zshrc`:

```zsh
PROMPT='$ '
```

Aplícalo sin reiniciar el shell:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

Crea el archivo de perfil si aún no existe y luego ábrelo:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Añade lo siguiente al perfil:

```powershell
function prompt { "$ " }
```

Aplícalo sin reiniciar el shell:

```powershell
. $PROFILE
```

### Símbolo del sistema (Windows)

Establece un prompt mínimo para la sesión actual:

```cmd
PROMPT $$
```

Para que sea permanente, añade `PROMPT` como variable de entorno de **usuario** o **sistema** con el valor `$$` a través de **Panel de control → Sistema → Configuración avanzada del sistema → Variables de entorno**.
