# <a name="claude-skill"></a>Claude Skill: Ejecutar Spck CLI como servicio Linux

Esta página proporciona una [skill de Claude Code](https://docs.claude.com/en/docs/claude-code/skills) descargable que automatiza la instalación de Spck CLI (`spck`) como servicio `systemd` en Linux. Con la skill instalada, puedes pedirle a Claude Code que "ejecute spck como un servicio" y verificará tu entorno, generará un archivo de unidad correcto con tus rutas absolutas, lo instalará y comprobará que está en ejecución — sin que tengas que copiar y pegar comandos de una lista.

La skill codifica la misma configuración de systemd descrita en [Usar Tmux → Alternativa: Servicio Linux](./tmux#linux-service), además de las verificaciones previas y los diagnósticos de fallos que son fáciles de pasar por alto al escribir el archivo de unidad manualmente.

## <a name="download"></a>Descargar

Descarga el archivo de skill y guárdalo en el directorio de skills de Claude Code:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

O descarga manualmente: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — colócalo en `~/.claude/skills/spck-cli-service/SKILL.md`.

## <a name="what-the-skill-does"></a>Qué hace la skill

Al invocarse, la skill guía a Claude Code a través de la instalación completa:

1. Verifica que el host sea Linux con `systemd` en ejecución.
2. Resuelve la ruta absoluta a `spck` (evita la discrepancia de `PATH` que rompe `ExecStart`).
3. Advierte si `node` está instalado a través de `nvm` — esas rutas cambian con cada actualización de Node y rompen el servicio silenciosamente.
4. Confirma que `~/.spck-editor/.credentials.json` existe (la CLI debe haberse ejecutado de forma interactiva al menos una vez antes de funcionar como servicio).
5. Elige entre un **servicio de usuario** (`systemctl --user`, sin `sudo`) y un **servicio de sistema** según tus necesidades.
6. Escribe el archivo de unidad con tus rutas reales completadas — sin marcadores de posición.
7. Ejecuta `daemon-reload`, `enable --now`, y luego sigue el journal para confirmar que la CLI se conectó al servidor relay.

La skill también documenta los siete modos de fallo más comunes (ruta `ExecStart` incorrecta, credenciales faltantes, errores de permisos en el directorio del proyecto, bucles de reinicio con `start-limit-hit`, rutas nvm obsoletas tras actualización de npm, etc.) para que Claude Code pueda diagnosticar un servicio roto en lugar de simplemente regenerar el archivo de unidad.

## <a name="installation"></a>Instalación

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Paso 1 — Descargar el archivo de skill:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Paso 2 — Verificar que Claude Code lo detectó:**

```bash
claude /skills
```

Deberías ver `spck-cli-service` en la lista. Si no, reinicia Claude Code para que vuelva a escanear el directorio de skills.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop carga las skills desde el mismo directorio `~/.claude/skills/` en macOS y Linux. En Windows, la ruta es `%USERPROFILE%\.claude\skills\` — pero la skill en sí solo funciona en hosts Linux, así que instálala en la máquina donde quieres ejecutar `spck`, no en la máquina que ejecuta Claude Desktop.

Si estás gestionando un servidor Linux remoto, ejecuta Claude Code por SSH en ese servidor (o a través del terminal de Spck CLI, que expone una shell completa al servidor). Instalar la skill en un Mac local no ayudará a configurar un servicio Linux remoto.

</div>
  </div>
</div>

## <a name="usage"></a>Uso

Una vez instalada, invoca la skill pidiéndoselo a Claude Code en lenguaje natural. Ejemplos que la activarán:

- "Instala spck como un servicio systemd"
- "Haz que Spck CLI arranque al inicio"
- "Mi spck-cli.service sigue reiniciándose, ¿puedes depurarlo?"
- "Ejecuta spck como un daemon para que sobreviva a la desconexión SSH"

Claude Code leerá la skill, ejecutará las verificaciones previas (que te pedirán aprobar cada comando) y luego generará e instalará el archivo de unidad. Revisa cada comando antes de aprobarlo — especialmente los que escriben en `/etc/systemd/system/` con `sudo`.

## <a name="what-gets-installed"></a>Qué se instala

La skill instala un único archivo de unidad. Para un servicio de usuario, es:

```bash
~/.config/systemd/user/spck-cli.service
```

Con contenido similar a:

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

Para un servicio de sistema, el archivo reside en `/etc/systemd/system/spck-cli.service` y agrega las directivas `User=` y `Group=`. La skill elige la variante correcta según tu entorno y escribe las rutas absolutas reales en el archivo.

## <a name="why-a-skill-instead-of-copy-paste"></a>¿Por qué una skill en lugar de copiar y pegar?

El archivo de unidad en la [documentación de tmux](./tmux#linux-service) es un punto de partida, pero varias cosas deben estar correctas para que el servicio funcione realmente:

- `ExecStart` debe ser la **ruta absoluta** a `spck`. `which spck` dentro de una shell de inicio resolverá las manipulaciones de PATH de `.bashrc` que systemd no ve.
- Si `spck` fue instalado bajo `nvm`, la ruta incorpora la versión de Node — actualizar Node rompe el servicio silenciosamente hasta el próximo reinicio.
- La CLI debe haberse ejecutado de forma interactiva al menos una vez para crear `~/.spck-editor/.credentials.json`. Un inicio de servicio nuevo sin credenciales termina limpiamente sin ningún error obvio.
- `User=` debe ser propietario del `WorkingDirectory`, de lo contrario la vigilancia de archivos falla con `EACCES` y la CLI entra en un bucle de reinicio.
- Los servicios de usuario necesitan `loginctl enable-linger` en servidores sin cabeza, de lo contrario solo se ejecutan mientras hay una sesión de inicio activa.

La skill codifica todo esto para que no tengas que recordarlo.

## <a name="uninstall"></a>Desinstalar

Deshabilitar y eliminar el servicio:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

Para un servicio de sistema:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Para eliminar la skill de Claude Code:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>Véase también

- [Usar Tmux](./tmux) — enfoque alternativo usando `tmux` para mantener la CLI activa tras las desconexiones SSH.
- [Uso avanzado](./cli-advanced) — referencia completa de comandos CLI, anulaciones de configuración y configuraciones multi-proyecto.
- [Configuración](./cli-config) — configuraciones de terminal, sistema de archivos, seguridad y autenticación que el archivo de unidad no cubre.
