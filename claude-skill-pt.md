# <a name="claude-skill"></a>Claude Skill: Executar Spck CLI como Serviço Linux

Esta página fornece uma [skill do Claude Code](https://docs.claude.com/en/docs/claude-code/skills) para download que automatiza a instalação do Spck CLI (`spck`) como um serviço `systemd` no Linux. Com a skill instalada, você pode pedir ao Claude Code para "executar o spck como um serviço" e ele verificará seu ambiente, gerará um arquivo de unidade correto com seus caminhos absolutos, instalará e verificará se está em execução — sem precisar copiar e colar comandos de uma lista.

A skill codifica a mesma configuração do systemd descrita em [Usando Tmux → Alternativa: Serviço Linux](./tmux#linux-service), mais as verificações prévias e os diagnósticos de falha que são fáceis de perder ao escrever o arquivo de unidade manualmente.

## <a name="download"></a>Download

Baixe o arquivo de skill e salve no diretório de skills local do Claude Code:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

Ou baixe manualmente: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — coloque em `~/.claude/skills/spck-cli-service/SKILL.md`.

## <a name="what-the-skill-does"></a>O que a Skill Faz

Quando invocada, a skill guia o Claude Code por toda a instalação:

1. Verifica se o host é Linux com `systemd` em execução.
2. Resolve o caminho absoluto para `spck` (evita a incompatibilidade de `PATH` que quebra o `ExecStart`).
3. Avisa se `node` foi instalado via `nvm` — esses caminhos mudam a cada atualização do Node e quebram a unidade silenciosamente.
4. Confirma que `~/.spck-editor/.credentials.json` existe (a CLI deve ter sido executada de forma interativa pelo menos uma vez antes de funcionar como serviço).
5. Escolhe entre um **serviço de usuário** (`systemctl --user`, sem `sudo`) e um **serviço de sistema** com base nas suas necessidades.
6. Escreve o arquivo de unidade com seus caminhos reais preenchidos — sem marcadores de posição.
7. Executa `daemon-reload`, `enable --now`, e então acompanha o journal para confirmar que a CLI se conectou ao servidor relay.

A skill também documenta os sete modos de falha mais comuns (caminho `ExecStart` errado, credenciais ausentes, erros de permissão no diretório do projeto, loops de reinicialização atingindo `start-limit-hit`, caminhos nvm obsoletos após atualização do npm, etc.) para que o Claude Code possa diagnosticar um serviço quebrado em vez de simplesmente regenerar o arquivo de unidade.

## <a name="installation"></a>Instalação

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Passo 1 — Baixar o arquivo de skill:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Passo 2 — Verificar se o Claude Code detectou:**

```bash
claude /skills
```

Você deve ver `spck-cli-service` na lista. Caso contrário, reinicie o Claude Code para que ele reescaneie o diretório de skills.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

O Claude Desktop carrega skills do mesmo diretório `~/.claude/skills/` no macOS e Linux. No Windows, o caminho é `%USERPROFILE%\.claude\skills\` — mas a skill em si só funciona em hosts Linux, então instale-a na máquina onde você quer executar o `spck`, não na máquina que executa o Claude Desktop.

Se você está gerenciando um servidor Linux remoto, execute o Claude Code via SSH nesse servidor (ou através do terminal do Spck CLI, que expõe um shell completo ao servidor). Instalar a skill em um Mac local não ajudará a configurar um serviço Linux remoto.

</div>
  </div>
</div>

## <a name="usage"></a>Uso

Uma vez instalada, invoque a skill pedindo ao Claude Code em linguagem natural. Exemplos que a ativarão:

- "Instale o spck como um serviço systemd"
- "Faça o Spck CLI iniciar no boot"
- "Meu spck-cli.service fica reiniciando, você consegue depurar?"
- "Execute o spck como um daemon para que sobreviva à minha desconexão SSH"

O Claude Code lerá a skill, executará as verificações prévias (que solicitarão aprovação de cada comando) e então gerará e instalará o arquivo de unidade. Revise cada comando antes de aprovar — especialmente os que escrevem em `/etc/systemd/system/` com `sudo`.

## <a name="what-gets-installed"></a>O que é Instalado

A skill instala um único arquivo de unidade. Para um serviço de usuário:

```bash
~/.config/systemd/user/spck-cli.service
```

Com conteúdo como:

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

Para um serviço de sistema, o arquivo fica em `/etc/systemd/system/spck-cli.service` e adiciona as diretivas `User=` e `Group=`. A skill escolhe a variante correta com base no seu ambiente e escreve os caminhos absolutos reais no arquivo.

## <a name="why-a-skill-instead-of-copy-paste"></a>Por que uma Skill em vez de Copiar e Colar?

O arquivo de unidade na [documentação do tmux](./tmux#linux-service) é um ponto de partida, mas várias coisas precisam estar corretas para o serviço realmente funcionar:

- `ExecStart` deve ser o **caminho absoluto** para `spck`. `which spck` dentro de um shell de login resolverá manipulações de PATH do `.bashrc` que o systemd não vê.
- Se `spck` foi instalado sob `nvm`, o caminho incorpora a versão do Node — atualizar o Node quebra o serviço silenciosamente até o próximo reboot.
- A CLI deve ter sido executada de forma interativa pelo menos uma vez para criar `~/.spck-editor/.credentials.json`. Uma nova inicialização do serviço sem credenciais termina de forma limpa sem nenhum erro óbvio.
- `User=` deve ser o proprietário do `WorkingDirectory`, caso contrário o monitoramento de arquivos encontra `EACCES` e a CLI entra em loop de reinicialização.
- Serviços de usuário precisam de `loginctl enable-linger` em servidores sem monitor, caso contrário só executam enquanto uma sessão de login está ativa.

A skill codifica tudo isso para que você não precise lembrar.

## <a name="uninstall"></a>Desinstalar

Desativar e remover o serviço:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

Para um serviço de sistema:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Para remover a skill do Claude Code:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>Veja Também

- [Usando Tmux](./tmux) — abordagem alternativa usando `tmux` para manter a CLI ativa durante desconexões SSH.
- [Uso Avançado](./cli-advanced) — referência completa de comandos CLI, substituições de configuração e configurações multi-projeto.
- [Configuração](./cli-config) — configurações de terminal, sistema de arquivos, segurança e autenticação que o arquivo de unidade não cobre.
