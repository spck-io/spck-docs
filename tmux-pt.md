# <a name="tmux"></a>Usando Tmux com Spck CLI

Tmux (Terminal Multiplexer) permite que sessões de terminal sejam executadas independentemente da janela ou conexão SSH que as iniciou. Para usuários do Spck CLI isso significa que você pode manter sessões ativas entre reconexões, compartilhar uma sessão de agente em execução entre o desktop e o mobile, e executar a CLI persistentemente em um servidor remoto mesmo após a conexão SSH cair.

## <a name="installation"></a>Instalação

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

O Tmux é executado nativamente no Linux. No Windows, use o [Subsistema Windows para Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install) e depois instale o tmux dentro do WSL.

**Passo 1 — Instalar o WSL (PowerShell como Administrador):**

```powershell
wsl --install
```

**Passo 2 — Abrir um terminal WSL e instalar o tmux:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Caso de uso 1: Compartilhando sessões de agente entre desktop e mobile

O fluxo de trabalho mais poderoso do tmux com Spck CLI é iniciar um agente de codificação IA no seu desktop e retomá-lo perfeitamente pelo mobile — ou o contrário. Ambos veem exatamente o mesmo estado do terminal, incluindo o histórico de rolagem completo.

### Iniciar uma sessão no desktop

Crie uma sessão tmux com nome:

```bash
tmux new -s code
```

Inicie seu agente IA dentro da sessão:

```bash
claude
```

O agente é executado dentro do tmux. Desanexe a qualquer momento pressionando **Ctrl+B** e depois **D** — a sessão e tudo o que está sendo executado nela continua em segundo plano.

### Conectar pelo mobile

1. Abra o Spck Editor e conecte-se ao seu servidor CLI
2. Abra um terminal no painel de terminal do Spck Editor
3. Anexe-se à sessão tmux em execução:

```bash
tmux attach -t code
```

Você vê exatamente o mesmo terminal que no desktop — incluindo o agente em execução, sua saída e o histórico de rolagem completo. Vários clientes podem se conectar simultaneamente e ver a saída ao vivo.

### Voltar para o desktop

Reconecte-se de qualquer terminal a qualquer momento:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Caso de uso 2: CLI persistente em um servidor remoto

Se você executa o Spck CLI em um servidor remoto via SSH, a CLI para assim que a sessão SSH termina — seja porque você fecha o notebook, perde o Wi-Fi ou a conexão expira. O Tmux mantém o processo ativo no servidor independentemente do estado da sua conexão.

### Configuração no servidor remoto

Conecte-se ao servidor via SSH e inicie uma sessão tmux com nome antes de iniciar a CLI:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

A CLI agora está sendo executada dentro do tmux no servidor. Feche a conexão SSH — ou perca-a completamente — e a CLI continua rodando.

### Reconectar após desconexão

```bash
ssh user@your-server.com
tmux attach -t spck
```

A CLI retoma exatamente de onde parou. Os clientes mobile podem se reconectar normalmente pelo servidor relay.

### Listar sessões em execução

```bash
tmux ls
```

## <a name="linux-service"></a>Alternativa: Serviço Linux

Para uma configuração totalmente automatizada que inicia a CLI no boot sem nenhum gerenciamento manual do tmux, execute o Spck CLI como um serviço systemd.

### Criar o arquivo de serviço

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

Substitua `your-username` e `/path/to/your/project` pelos seus valores reais. Se você instalou o `spck` globalmente (`npm install -g spck`), substitua `ExecStart` pela saída de `which spck`.

### Habilitar e iniciar

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Verificar status e logs

```bash
# Ver status
sudo systemctl status spck-cli

# Acompanhar logs ao vivo
journalctl -u spck-cli -f
```

O serviço inicia automaticamente em cada reinicialização e reinicia sozinho se o processo travar.

## <a name="essential-tmux-commands"></a>Comandos essenciais do Tmux

| Comando | Ação |
| --- | --- |
| `tmux new -s name` | Criar uma nova sessão com nome |
| `tmux attach -t name` | Anexar a uma sessão existente |
| `tmux ls` | Listar todas as sessões |
| `tmux kill-session -t name` | Encerrar uma sessão |
| Ctrl+B, D | Desanexar da sessão (continua em execução) |
| Ctrl+B, C | Criar uma nova janela |
| Ctrl+B, N | Mudar para a próxima janela |
| Ctrl+B, P | Mudar para a janela anterior |
| Ctrl+B, [ | Entrar no modo de rolagem (teclas de seta / PgUp / PgDn) |
| Q | Sair do modo de rolagem |
