# <a name="cli-file-transfer"></a>Transferencia de archivos entre móvil y escritorio

## <a name="overview"></a>Descripción general

Cuando ejecutas Spck CLI en tu escritorio, actúa como un hub de sincronización entre el sistema de archivos de tu escritorio y los proyectos locales almacenados en tu teléfono. Ambos lados aparecen uno al lado del otro en el gestor de archivos de Spck Editor —los proyectos locales de tu teléfono a la izquierda y los archivos de tu escritorio como un servidor remoto conectado— y puedes copiar archivos o carpetas enteras en cualquier dirección usando los comandos estándar de copiar y pegar.

No se necesita AirDrop, Bluetooth, cable USB ni almacenamiento en la nube de terceros. Las transferencias están cifradas de extremo a extremo a través de una conexión WebSocket y permanecen en tu Wi-Fi local cuando ambos dispositivos están en la misma red.

## <a name="how-it-works"></a>Cómo funciona

El CLI expone tu directorio de escritorio como un proyecto de servidor remoto en el gestor de archivos de Spck Editor. Los proyectos locales guardados en tu teléfono se almacenan en el almacenamiento local de la aplicación. Spck Editor trata ambos como ubicaciones de proyecto de primera clase, por lo que cualquier operación de archivo que funcione dentro de un único proyecto —incluido copiar y pegar— también funciona entre ellos.

```
Teléfono (almacenamiento local)   Escritorio (via CLI)
───────────────────────────────   ─────────────────────
my-project/               ↔      ~/projects/my-project/
  ├── index.html                    ├── index.html
  ├── style.css                     ├── style.css
  └── assets/                       └── assets/
      └── logo.png                      └── logo.png
```

Los directorios se transfieren de forma recursiva: todos los archivos dentro se copian y los subdirectorios se crean automáticamente en el destino.

## <a name="desktop-to-mobile"></a>De escritorio a móvil

Usa esto cuando quieras llevar archivos de tu computadora a tu teléfono; por ejemplo, para trabajar sin conexión, compartir un proyecto con un colega que solo tiene la aplicación móvil, o guardar una instantánea de tu trabajo en el dispositivo.

1. **Inicia el CLI** en tu escritorio, apuntando a la carpeta desde la que quieres transferir:

   ```bash
   spck --root ~/projects
   ```

2. **Conecta tu teléfono** escaneando el código QR con la aplicación de cámara y abriendo el enlace en Spck Editor.

3. En Spck Editor, tu carpeta de escritorio aparece como un proyecto de servidor remoto en el panel **Proyectos**.

4. **Mantén pulsado el archivo o carpeta** que quieras en el proyecto remoto y toca **Copiar**.

5. **Navega a un proyecto local** en tu teléfono (o crea uno nuevo con **Nuevo proyecto**).

6. **Mantén pulsada la carpeta de destino** y toca **Pegar**.

Los archivos se descargan de tu escritorio y se guardan en el almacenamiento local de tu teléfono.

## <a name="mobile-to-desktop"></a>De móvil a escritorio

Usa esto cuando quieras enviar trabajo de tu teléfono de vuelta al escritorio; por ejemplo, después de editar en movimiento, o para consolidar proyectos creados en el dispositivo.

1. **Inicia el CLI** en tu escritorio, apuntando a la carpeta donde quieres que lleguen los archivos:

   ```bash
   spck --root ~/Desktop/from-phone
   ```

2. **Conecta tu teléfono** escaneando el código QR.

3. En Spck Editor, abre el **proyecto local** en tu teléfono que contiene los archivos que quieres enviar.

4. **Mantén pulsado el archivo o carpeta** que quieras y toca **Copiar**.

5. **Navega al proyecto remoto del escritorio** en el panel **Proyectos**.

6. **Mantén pulsada la carpeta de destino** y toca **Pegar**.

Los archivos se leen del almacenamiento local de tu teléfono y se escriben en tu escritorio a través del CLI.

## <a name="transferring-projects"></a>Transferir proyectos completos

Puedes copiar una carpeta de proyecto entera en una sola operación de pegado. Mantén pulsada la raíz del proyecto en el árbol de archivos, selecciona **Copiar**, navega al destino y **Pegar**. Se transfiere el árbol de directorios completo, incluyendo todos los archivos en todos los subdirectorios.

Esto es útil para:

- **Hacer una copia de seguridad de un proyecto móvil en tu escritorio** antes de realizar cambios importantes
- **Inicializar un nuevo proyecto en el teléfono** desde una base de código existente en el escritorio
- **Consolidar trabajo** de múltiples dispositivos en un solo lugar

## <a name="tips"></a>Consejos

### Límite de tamaño de archivo

El tamaño máximo de archivo predeterminado es de **10 MB** por archivo. Para transferir archivos más grandes como imágenes, archivos comprimidos o binarios compilados, aumenta el límite en la configuración de tu CLI:

```json
{
  "filesystem": {
    "maxFileSize": "200MB"
  }
}
```

Consulta [Configuración CLI](./cli-config) para más detalles.

### Velocidad de transferencia

La velocidad depende completamente de tu conexión Wi-Fi local o de Internet. Para directorios grandes, las transferencias se realizan archivo por archivo, por lo que el rendimiento total escala con el número de archivos. En una red Wi-Fi doméstica típica, los proyectos pequeños con muchos archivos de texto (cientos de archivos) se completan en unos pocos segundos.

### Seguridad

Todas las transferencias están cifradas mediante WSS (WebSocket Secure) y cada solicitud está firmada con una clave secreta por sesión. El servidor de retransmisión reenvía mensajes entre dispositivos pero nunca recibe contenido sin cifrar. Consulta [Seguridad CLI](./cli-config#security) para más detalles.

### Ejecutar múltiples transferencias

El CLI expone un único directorio raíz. Para transferir desde múltiples ubicaciones simultáneamente, ejecuta instancias separadas del CLI en distintos terminales:

```bash
# Terminal 1: exponer ~/projects
spck --root ~/projects

# Terminal 2: exponer ~/Documents
spck --root ~/Documents
```

Cada instancia genera su propio código QR y conexión, y ambos servidores remotos aparecen en el panel **Proyectos** de Spck Editor al mismo tiempo.
