# <a name="cli-configuration"></a>Configuración CLI

## <a name="configuration"></a>Configuración

### Ubicación del Archivo de Configuración

La configuración se almacena en `.spck-editor/config/spck-cli.config.json` en el directorio de tu proyecto.

**Importante**: `.spck-editor/config` es un **enlace simbólico** a `~/.spck-editor/projects/{project_id}/`, manteniendo los secretos fuera del directorio de tu proyecto.

### Configuración Predeterminada

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### Configuración del Proxy de Navegador

- **`browserProxy.enabled`** (boolean): Habilitar/deshabilitar la función de proxy de navegador
  - Predeterminado: `true`
  - Establecer en `false` para evitar que la aplicación móvil abra una sesión de proxy de navegador a través de la CLI

### Configuración del Terminal

- **`terminal.enabled`** (boolean): Habilitar/deshabilitar el acceso al terminal
  - Predeterminado: `true`
  - Establecer en `false` para reducir el riesgo de acceso no autorizado a tu terminal

- **`terminal.maxBufferedLines`** (number): Búfer de desplazamiento máximo
  - Predeterminado: `10000`
  - Afecta el uso de memoria (~1MB por cada 10.000 líneas)

- **`terminal.maxTerminals`** (number): Sesiones de terminal simultáneas máximas
  - Predeterminado: `10`
  - Cada terminal usa ~5-10MB de memoria

### Configuración del Sistema de Archivos

- **`filesystem.maxFileSize`** (string): Tamaño máximo de archivo para lectura/escritura
  - Predeterminado: `"10MB"`
  - Acepta: `"5MB"`, `"50MB"`, etc.

- **`filesystem.watchIgnorePatterns`** (string[]): Patrones a excluir de la vigilancia de archivos
  - Predeterminado: Ignora salidas de compilación y dependencias
  - Mejora el rendimiento al evitar miles de archivos generados

### Configuración de Seguridad

- **`security.userAuthenticationEnabled`** (boolean): Habilitar autenticación de usuario Firebase
  - Predeterminado: `false`
  - Cuando es `false`: Menor latencia, compatible con Lite, aún protegido por firma de secreto
  - Cuando es `true`: Capa de seguridad adicional, verificación de identidad de usuario, añade 2-20s de latencia inicial
  - **Todas las solicitudes siempre están firmadas criptográficamente independientemente de esta configuración**

## <a name="security"></a>Seguridad

### Conexiones Encriptadas

Toda la comunicación utiliza:

- **WSS (WebSocket Secure)**: Encriptación TLS/SSL
- **HTTPS**: Handshake inicial encriptado

### Firma de Solicitudes

Cada solicitud está firmada criptográficamente:

- La clave secreta se genera localmente, nunca se transmite por internet
- Se recomienda no usar escáneres QR de terceros que puedan exponer tu clave secreta

### Mejores Prácticas

1. **Proteger credenciales**:

   ```bash
   # Añadir a .gitignore (automático durante la configuración)
   echo ".spck-editor/" >> .gitignore
   ```

2. **Cerrar sesión en máquinas compartidas**:

   ```bash
   spck --logout
   ```

3. **Limitar directorios expuestos**:

   ```bash
   # En lugar del directorio home completo
   spck --root /path/to/specific/project
   ```

4. **Deshabilitar el terminal si no es necesario**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **Deshabilitar el proxy de navegador si no es necesario**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>Autenticación de Usuario

Spck CLI soporta autenticación de usuario Firebase opcional como segunda capa de seguridad sobre la firma de solicitudes siempre activa.

### Cómo Funciona

Cuando está habilitada, la CLI requiere que inicies sesión con tu cuenta de Spck Editor. Las conexiones se autentican usando tokens de ID de Firebase que expiran cada hora y se renuevan automáticamente usando tokens de actualización seguros almacenados en `~/.spck-editor/.credentials.json`.

### Habilitar Autenticación de Usuario

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### Compromisos

|                        | Deshabilitado (predeterminado) | Habilitado                               |
| ---------------------- | ------------------------------ | ---------------------------------------- |
| **Protección**         | Clave de firma secreta         | + Verificación de identidad Firebase     |
| **Latencia inicial**   | Sin sobrecarga de auth         | Añade 2–20s en la primera conexión       |
| **Spck Editor Lite**   | ✅ Soportado                   | ❌ No soportado                          |
| **Uso sin conexión**   | Funciona sin internet          | Requiere internet para renovar tokens    |

### Cuándo Habilitar

**Mantener deshabilitado (predeterminado) cuando:**

- Se usa **Spck Editor Lite** — el inicio de sesión Firebase no está soportado en Lite; establecer esto en `true` impedirá que los usuarios de Lite se conecten
- Se trabaja en una red local o entorno de confianza donde la clave de firma secreta es suficiente
- Minimizar la latencia de conexión es una prioridad

**Habilitar cuando:**

- La CLI está expuesta en un servidor accesible por internet
- Se desea verificación de identidad de usuario como capa adicional de control de acceso más allá de la clave de firma

> ⚠️ **Spck Editor Lite no soporta autenticación Firebase.** Si `userAuthenticationEnabled` se establece en `true`, Spck Editor Lite no puede conectarse. Mantén esta configuración en `false` cuando uses Lite.
