# <a name="ai-coding-agents-acp"></a>Agentes de IA para codificar en el móvil (ACP)

Ejecuta **Claude Code**, **OpenAI Codex** o **Gemini CLI** directamente desde tu teléfono a través del **AI Chat** de Spck Editor. La Spck CLI conecta tu editor con los CLIs de agentes instalados localmente mediante el [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) abierto, de modo que el modelo se ejecuta en tu máquina, con tu suscripción, contra tus archivos reales — mientras lo supervisas desde un dispositivo móvil.

![Modo ACP de IA local en el AI Chat de Spck Editor, controlando Claude Code en un escritorio desde un teléfono](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>¿Qué es ACP y por qué usarlo?

El Agent Client Protocol (ACP) es un estándar abierto de Zed Industries para la comunicación entre editor y agente de IA, con el mismo espíritu que el Language Server Protocol (LSP). Spck CLI 0.6.0+ implementa ACP y actúa como **transporte** entre el AI Chat de Spck Editor (el cliente) y cualquier binario de agente compatible con ACP que tengas instalado (el agente).

Comparado con el AI Chat enrutado a través del servidor dentro de la app, la ruta ACP local te ofrece:

- **Tu propia suscripción** — las llamadas del agente se facturan a tu cuenta de Claude Code / ChatGPT / Gemini, no a tu cuota de IA de Spck Editor.
- **Acceso real al sistema de archivos** — los agentes leen y escriben archivos reales en disco a través de la CLI, no las copias en memoria del editor.
- **Herramientas nativas** — los observadores de archivos, los servidores de lenguaje y los comandos de shell se ejecutan en tu máquina real.
- **Continuidad con el escritorio** — el mismo login `claude` / `gemini` / `codex` que usas en tu escritorio impulsa el chat móvil.

## <a name="acp-supported-agents"></a>Agentes de IA compatibles

Instala los agentes que quieras tener disponibles. Spck CLI los detecta automáticamente al iniciar.

| Agente            | Instalación                                                                          |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>Instalación y configuración

### 1. Instala Spck CLI

Si aún no la tienes:

```bash
npm install -g spck
# o ejecútala sin instalar
npx spck
```

Consulta [Primeros pasos con Spck CLI](./cli-start) para el asistente completo del primer uso.

### 2. Instala uno o más CLIs de agente

Elige los agentes que quieras tener disponibles. Puedes instalar varios — el AI Chat te permitirá elegir entre ellos por sesión. Consulta la tabla [Agentes de IA compatibles](#acp-supported-agents) más arriba para ver los comandos de instalación.

### 3. Autentica cada agente una vez

Los CLIs de agente gestionan su propio login fuera de Spck Editor:

```bash
claude            # Flujo de login de Anthropic Claude Code
codex login       # Flujo de login de OpenAI Codex (usado por codex-acp)
gemini            # Flujo de login de Google Gemini
```

Si te saltas este paso, Spck Editor mostrará un error como `ACP agent requires authentication; run <binary> login and retry` la primera vez que inicies un chat.

### 4. Inicia Spck CLI

```bash
cd /path/to/your/project
spck
```

Al iniciar, la CLI imprime un informe de detección por agente listando qué agentes están disponibles, seguido de un resumen de una sola línea como `✅ ACP agents: Claude Code, Gemini CLI` en el bloque principal de funciones. Si no hay nada disponible, recae en el AI Chat enrutado al servidor.

### 5. Conecta Spck Editor

Escanea el código QR o usa [Entrada manual](./cli-start#connecting). Una vez conectado, abre el **AI Chat** en Spck Editor — el conmutador de transporte mostrará los agentes locales junto con la opción en la nube.

## <a name="acp-authentication"></a>Autenticación

Cada agente gestiona sus propias credenciales en la máquina donde se ejecuta Spck CLI. Ejecuta el flujo de login una vez por agente:

```bash
# Claude Code
claude

# Codex (codex-acp envuelve el propio login de la CLI de Codex)
codex login

# Gemini CLI
gemini
```

Si reinstalas o cambias de máquina, repite el login en el nuevo host. La autenticación es **por host, por agente** — Spck Editor mismo nunca guarda estas credenciales.

## <a name="acp-billing"></a>Facturación y límites de uso

Como ACP ejecuta el agente en tu máquina con tus propias credenciales, **todo el uso se factura a tu cuenta con ese proveedor** — no a tu suscripción de Spck Editor. Spck Editor y los servidores de relevo de Spck actúan como puro transporte en este modo y no consumen nada de tu cuota de IA en la app para el tráfico ACP.

### Facturación de Claude Code

> ⚠️ **Importante — Claude Code aplica un bucket de límite de uso separado cuando lo impulsan herramientas de terceros.**
>
> Cuando se invoca Claude Code desde un cliente de terceros a través de ACP, Anthropic contabiliza ese tráfico contra un **bucket de límite de uso diferente** al de tus sesiones interactivas de la CLI `claude` en una suscripción Pro / Max. La consecuencia práctica: puedes agotar el bucket de terceros mientras aún tienes margen interactivo de Claude Code (o al revés), y no puedes consolidarlos.
>
> Comprueba `/usage` dentro de `claude` y la [Anthropic Console](https://platform.claude.com/usage) para ver tu consumo actual, y consulta la [documentación de coste y límites de Claude Code](https://code.claude.com/docs/en/costs) para las cifras que aplican a tu plan.

### Facturación de Codex (codex-acp)

Facturado mediante la propia auth de OpenAI Codex CLI — tu clave API de OpenAI o login de ChatGPT. El uso cuenta contra cualquier plan que tenga esa cuenta. Los precios y cupos son los mismos que para el uso interactivo de `codex`; consulta [openai.com/codex](https://github.com/openai/codex) y tu panel de OpenAI para las cifras actuales.

### Facturación de Gemini CLI

Facturado mediante tu cuenta de Google o clave API de Gemini. El uso cuenta contra el plan de Gemini o cupo de API vinculado a ese login. Consulta [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits) para los detalles del límite de uso.

## <a name="acp-configuration"></a>Configuración

ACP está habilitado por defecto y se configura mediante el `spck-cli.config.json` del proyecto:

```json
{
  "acp": {
    "enabled": true
  }
}
```

Consulta [Configuración → Ajustes de ACP](./cli-config#acp-settings) para el esquema completo.

### Deshabilitar ACP por proyecto

Si no quieres que Spck Editor pueda controlar un agente local en este host:

```json
{
  "acp": {
    "enabled": false
  }
}
```

Cuando está deshabilitado, el conmutador de transporte del editor oculta la opción de agente local y cualquier RPC `acp.*` se rechaza con `FEATURE_DISABLED`. El asistente de configuración hace esta pregunta en el primer uso (por defecto `Y`); las configuraciones que preceden a esta opción se cargan con `acp.enabled: true` añadido automáticamente y se vuelven a guardar.

### Deshabilitar un único agente

Para evitar que se ofrezca un agente _en particular_ manteniendo ACP habilitado para los demás, desinstala el binario de ese agente. La detección se ejecuta en cada inicio de la CLI, así que el conmutador de transporte del editor lo eliminará de la lista.

## <a name="acp-vs-server-routed"></a>ACP local vs. AI Chat enrutado al servidor

| Capacidad                                  | Enrutado al servidor (por defecto, sin CLI) | Local (ACP, CLI conectada)                |
| ------------------------------------------ | ------------------------------------------- | ----------------------------------------- |
| Dónde se ejecuta el modelo                 | Nube de Spck                                | Tu máquina                                |
| Credenciales                               | Tu cuenta de Spck Editor                    | El propio login / clave API del agente    |
| Acceso a archivos                          | Sistema de archivos en memoria del editor   | Archivos reales en disco vía la raíz de la CLI |
| Cuenta contra la cuota de IA de Spck Editor| Sí                                          | **No** — facturado al proveedor del agente |
| Funciona sin la CLI ejecutándose           | Sí                                          | No (requiere CLI + WebSocket)             |
| Agentes disponibles                        | Modelos alojados en Spck                    | Claude Code, Codex, Gemini CLI            |
| Avisos de permiso de uso de herramientas en el móvil | Cuando aplique                    | Sí, reenviados por ACP                    |
| Streaming de tokens                        | Sí                                          | Sí                                        |
| Chat multi-turno                           | Sí                                          | Sí                                        |

Puedes cambiar de transporte a mitad de proyecto — el AI Chat muestra las rutas actualmente disponibles según el estado de conexión de la CLI y los agentes detectados.

## <a name="acp-tmux"></a>Combinar con Tmux para sesiones de larga duración

Las sesiones ACP siguen vivas a través de reconexiones del editor, pero el propio proceso de Spck CLI termina cuando se cierra su terminal. Para trabajo de agente de larga duración — grandes refactorizaciones, sesiones de planificación de varias horas — inicia la CLI dentro de una sesión de [tmux](./tmux) para que sobreviva a caídas de SSH, cierres de terminal y suspensiones del portátil:

```bash
tmux new -s spck
spck
# Ctrl+B luego D para desconectar
```

También puedes reconectarte desde tu teléfono a través del terminal de Spck CLI y `tmux attach -t spck` para monitorizar el agente en vivo. Consulta [Usar Tmux](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile) para el patrón completo, incluyendo la ejecución de la CLI como servicio en segundo plano persistente.

Para hosts Linux, la página [Claude Skill: Linux Service](./claude-skill) ofrece una configuración de un solo comando para ejecutar Spck CLI como un servicio `systemd`, de modo que la WebSocket — y cualquier sesión ACP encima de ella — se inicia automáticamente al arrancar.

## <a name="acp-faq"></a>Preguntas frecuentes

### ¿Puedo usar Claude Code en mi teléfono?

Sí. Instala Claude Code en tu escritorio, autentícate con `claude`, y luego ejecuta `spck` en tu proyecto. Conecta Spck Editor desde tu teléfono y elige Claude Code en el conmutador de transporte del AI Chat. El modelo se ejecuta en tu escritorio con tu suscripción; tú lo controlas desde tu teléfono.

### ¿Spck Editor ve mi clave API de Claude / OpenAI / Gemini?

No. Cada CLI de agente gestiona sus propias credenciales en la máquina donde se ejecuta Spck CLI. Los mensajes ACP se tunelizan por la WebSocket cifrada entre el teléfono y la CLI, pero los tokens de auth del propio agente nunca salen de tu host.

### ¿Hay coste adicional por usar Claude Code a través de Spck Editor?

Ningún cargo adicional de Spck Editor. El uso del agente cuenta contra tu plan de Anthropic / OpenAI / Google exactamente como si estuvieras ejecutando el agente de forma interactiva en tu escritorio — excepto que Anthropic aplica un bucket de límite de uso separado para clientes de terceros; consulta [Facturación y límites de uso](#acp-billing) arriba.

### ¿Necesito una suscripción de pago de Spck Editor para usar ACP?

No. El nivel gratuito (30 min/día de conexión de CLI) es suficiente para controlar cualquier agente ACP. Solo el AI Chat enrutado al servidor dentro de la app consume cuota de IA de Spck Editor.

### ¿Qué pasa si pierdo la conexión Wi-Fi a mitad del chat?

El proceso del agente sigue vivo en el host de la CLI. Cuando el editor se reconecta, la sesión se reanuda con el historial de chat completo. La salida de streaming que llegó mientras estabas desconectado se reproduce al reconectar.

### ¿Puedo ejecutar agentes en un servidor remoto en lugar de en mi portátil?

Sí. Ejecuta Spck CLI en cualquier host Linux/macOS accesible — una VM de desarrollo, un servidor doméstico, una estación de trabajo — y conéctate a él mediante el servidor de relevo. Combínalo con [tmux](./tmux) o el [skill de systemd](./claude-skill) para mantener la CLI viva entre conexiones.

### ¿ACP funciona con Spck Editor Lite?

Sí. El tráfico ACP usa el mismo transporte WebSocket que el sistema de archivos y git, que Spck Editor Lite soporta. Asegúrate de que `security.userAuthenticationEnabled` está puesto a `false` en tu configuración de CLI — la auth de Firebase no está soportada en Lite. Consulta [Configuración → Autenticación de usuario](./cli-config#user-authentication).

### ¿Por qué no aparece mi agente en el AI Chat?

Comprueba el log de arranque de la CLI para la línea por agente:

- Agente no detectado — instálalo (consulta [Agentes de IA compatibles](#acp-supported-agents)).
- Detectado pero ausente del editor — asegúrate de haber completado el flujo de login propio del agente (`claude`, `codex login`, `gemini`).
- ACP deshabilitado — comprueba `acp.enabled` en `.spck-editor/config/spck-cli.config.json`. Consulta [Configuración](./cli-config#acp-settings).

## <a name="acp-troubleshooting"></a>Solución de problemas

### Agente detectado pero la sesión no arranca

Esto suele significar que el agente no está autenticado. Ejecuta el flujo de login del agente en el host de la CLI:

```bash
claude              # luego completa la auth en el navegador
codex login
gemini
```

Si el problema persiste, revisa los logs de la CLI en `.spck-editor/logs/` buscando la salida stderr del agente, que normalmente apunta al fallo de auth o de binario.

### Errores de límite de uso durante un chat

Para Claude Code, el editor reenvía el 429 de Anthropic tal cual. Comprueba la [página de uso de Anthropic Console](https://platform.claude.com/usage) y los [docs de coste de Claude Code](https://code.claude.com/docs/en/costs) — recuerda que el bucket de límite de uso de terceros es separado de tu cupo interactivo de `claude`.

Para Codex y Gemini, el editor reenvía el propio error de cupo del proveedor. Resuélvelo desde la consola del proveedor.

### La CLI se cuelga al iniciar una sesión ACP

Spck CLI guarda el tráfico ACP en `.spck-editor/logs/`. Sigue el archivo de log más reciente mientras reproduces el problema:

```bash
tail -f .spck-editor/logs/spck-*.log
```

Reporta un bug en [github.com/spck-editor](https://github.com/spck-editor) con el fragmento relevante.

### El agente hace cambios fuera de la raíz del proyecto

Los agentes ACP están limitados al directorio `root` configurado de la CLI. Si ves escrituras fuera de él, reporta un issue — eso no debería ocurrir. Como solución temporal, ejecuta `spck --root /path/to/specific/project` para limitar aún más el alcance.

## <a name="acp-see-also"></a>Véase también

- [Primeros pasos con Spck CLI](./cli-start) — instalar, autenticar y conectar por primera vez
- [Referencia de CLI](./cli) — servidores de relevo, flujo de trabajo diario, límites de conexión
- [Configuración → Ajustes de ACP](./cli-config#acp-settings) — la opción de configuración `acp.enabled`
- [Uso avanzado](./cli-advanced) — flags de CLI, múltiples proyectos, consejos para prompts móviles
- [Usar Tmux](./tmux) — mantener vivas las sesiones ACP a través de reconexiones
- [Claude Skill: Linux Service](./claude-skill) — ejecutar Spck CLI como servicio `systemd` para que ACP esté siempre disponible
- [Especificación del Agent Client Protocol](https://agentclientprotocol.com/) — el estándar abierto que implementa ACP
- [Documentación de Claude Code](https://docs.claude.com/en/docs/claude-code/overview)
- [Repositorio de Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
