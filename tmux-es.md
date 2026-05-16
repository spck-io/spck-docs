# <a name="tmux"></a>Usar Tmux con Spck CLI

Tmux (Terminal Multiplexer) permite que las sesiones de terminal se ejecuten de forma independiente a la ventana o conexión SSH que las inició. Para los usuarios de Spck CLI esto significa que puedes mantener las sesiones activas durante las reconexiones, compartir una sesión de agente en ejecución entre el escritorio y el móvil, y ejecutar la CLI de forma persistente en un servidor remoto incluso después de que tu conexión SSH se interrumpa.

## <a name="installation"></a>Instalación

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux se ejecuta de forma nativa en Linux. En Windows, usa el [Subsistema de Windows para Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install) y luego instala tmux dentro de WSL.

**Paso 1 — Instalar WSL (PowerShell como Administrador):**

```powershell
wsl --install
```

**Paso 2 — Abrir un terminal WSL e instalar tmux:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Caso de uso 1: Compartir sesiones de agente entre escritorio y móvil

El flujo de trabajo más potente de tmux con Spck CLI es iniciar un agente de codificación IA en tu escritorio y retomarlo sin problemas desde tu móvil — o al revés. Ambos ven exactamente el mismo estado del terminal, incluyendo el historial de desplazamiento completo.

### Iniciar una sesión en el escritorio

Crea una sesión tmux con nombre:

```bash
tmux new -s code
```

Inicia tu agente IA dentro de la sesión:

```bash
claude
```

El agente se ejecuta dentro de tmux. Desconéctate en cualquier momento presionando **Ctrl+B** y luego **D** — la sesión y todo lo que se ejecuta dentro de ella continúa en segundo plano.

### Conectarse desde el móvil

1. Abre Spck Editor y conéctate a tu servidor CLI
2. Abre un terminal desde el panel de terminal de Spck Editor
3. Conéctate a la sesión tmux en ejecución:

```bash
tmux attach -t code
```

Verás exactamente el mismo terminal que en tu escritorio — incluyendo el agente en ejecución, su salida y el historial de desplazamiento completo. Varios clientes pueden conectarse simultáneamente y ver la salida en tiempo real.

### Volver al escritorio

Reconéctate desde cualquier terminal en cualquier momento:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Caso de uso 2: CLI persistente en un servidor remoto

Si ejecutas Spck CLI en un servidor remoto a través de SSH, la CLI se detiene en el momento en que la sesión SSH termina — ya sea porque cierras el portátil, pierdes la conexión Wi-Fi o la conexión se agota. Tmux mantiene el proceso activo en el servidor independientemente del estado de tu conexión.

### Configuración en el servidor remoto

Conéctate por SSH a tu servidor e inicia una sesión tmux con nombre antes de lanzar la CLI:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

La CLI ahora se ejecuta dentro de tmux en el servidor. Cierra la conexión SSH — o piérdela por completo — y la CLI sigue ejecutándose.

### Reconectarse después de desconectarse

```bash
ssh user@your-server.com
tmux attach -t spck
```

La CLI reanuda exactamente donde lo dejó. Los clientes móviles pueden reconectarse normalmente a través del servidor relay.

### Listar sesiones en ejecución

```bash
tmux ls
```

## <a name="linux-service"></a>Alternativa: Servicio de Linux

Para una configuración totalmente automatizada que inicie la CLI al arrancar sin ninguna gestión manual de tmux, ejecuta Spck CLI como un servicio systemd.

### Crear el archivo de servicio

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Reemplaza `your-username` y `/path/to/your/project` con tus valores reales. Si instalaste `spck` globalmente (`npm install -g spck`), reemplaza `ExecStart` con la salida de `which spck`.

### Habilitar e iniciar

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Comprobar estado y registros

```bash
# Ver estado
sudo systemctl status spck-cli

# Seguir registros en tiempo real
journalctl -u spck-cli -f
```

El servicio se inicia automáticamente en cada reinicio y se reinicia solo si el proceso falla.

## <a name="essential-tmux-commands"></a>Comandos esenciales de Tmux

| Comando | Acción |
| --- | --- |
| `tmux new -s name` | Crear una nueva sesión con nombre |
| `tmux attach -t name` | Conectarse a una sesión existente |
| `tmux ls` | Listar todas las sesiones |
| `tmux kill-session -t name` | Terminar una sesión |
| Ctrl+B, D | Desconectarse de la sesión (sigue ejecutándose) |
| Ctrl+B, C | Crear una nueva ventana |
| Ctrl+B, N | Cambiar a la ventana siguiente |
| Ctrl+B, P | Cambiar a la ventana anterior |
| Ctrl+B, [ | Entrar en modo desplazamiento (teclas de flecha / AvPág / RePág) |
| Q | Salir del modo desplazamiento |
