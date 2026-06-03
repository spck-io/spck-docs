# <a name="ai-coding-agents-acp"></a>Agentes de Codificação com IA no Celular (ACP)

Execute **Claude Code**, **OpenAI Codex** ou **Gemini CLI** diretamente do seu celular através do **AI Chat** do Spck Editor. O Spck CLI conecta seu editor às CLIs de agente instaladas localmente sobre o [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) aberto, de modo que o modelo roda na sua máquina, com sua assinatura, contra seus arquivos reais — enquanto você supervisiona a partir de um dispositivo móvel.

![Modo IA local ACP no AI Chat do Spck Editor, controlando o Claude Code em um desktop a partir de um celular](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>O que é ACP e por que usá-lo?

O Agent Client Protocol (ACP) é um padrão aberto da Zed Industries para comunicação editor ↔ agente de IA, no mesmo espírito do Language Server Protocol (LSP). O Spck CLI 0.6.0+ implementa ACP e atua como **transporte** entre o AI Chat do Spck Editor (o cliente) e qualquer binário de agente compatível com ACP que você tenha instalado (o agente).

Comparado ao AI Chat roteado pelo servidor dentro do app, o caminho ACP local lhe dá:

- **Sua própria assinatura** — chamadas do agente são cobradas na sua conta Claude Code / ChatGPT / Gemini, não na sua cota de IA do Spck Editor.
- **Acesso real ao sistema de arquivos** — agentes leem e escrevem arquivos reais em disco via o CLI, não as cópias em memória do editor.
- **Ferramentas nativas** — observadores de arquivo, servidores de linguagem e comandos shell rodam na sua máquina real.
- **Continuidade com o desktop** — o mesmo login `claude` / `gemini` / `codex` que você usa na sua mesa impulsiona o chat móvel.

## <a name="acp-supported-agents"></a>Agentes de IA Suportados

Instale os agentes que você quiser ter disponíveis. O Spck CLI os detecta automaticamente na inicialização.

| Agente            | Instalação                                                                           |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>Instalação e Configuração

### 1. Instale o Spck CLI

Se você ainda não o tem:

```bash
npm install -g spck
# ou execute sem instalar
npx spck
```

Veja [Primeiros passos com Spck CLI](./cli-start) para o assistente completo de primeira execução.

### 2. Instale uma ou mais CLIs de agente

Escolha quais agentes quer ter disponíveis. Você pode instalar vários — o AI Chat permitirá escolher entre eles a cada sessão. Veja a tabela [Agentes de IA Suportados](#acp-supported-agents) acima para os comandos de instalação.

### 3. Autentique cada agente uma vez

As CLIs de agente gerenciam o próprio login fora do Spck Editor:

```bash
claude            # Fluxo de login do Anthropic Claude Code
codex login       # Fluxo de login do OpenAI Codex (usado pelo codex-acp)
gemini            # Fluxo de login do Google Gemini
```

Se você pular esta etapa, o Spck Editor mostrará um erro como `ACP agent requires authentication; run <binary> login and retry` na primeira vez que você iniciar um chat.

### 4. Inicie o Spck CLI

```bash
cd /path/to/your/project
spck
```

Na inicialização, o CLI imprime um relatório de detecção por agente listando quais agentes estão disponíveis, seguido por um resumo de uma linha como `✅ ACP agents: Claude Code, Gemini CLI` no bloco principal de funcionalidades. Se nada estiver disponível, recai para o AI Chat roteado pelo servidor.

### 5. Conecte o Spck Editor

Escaneie o QR code ou use [Entrada Manual](./cli-start#connecting). Uma vez conectado, abra o **AI Chat** no Spck Editor — o seletor de transporte mostrará os agentes locais ao lado da opção em nuvem.

## <a name="acp-authentication"></a>Autenticação

Cada agente gerencia suas próprias credenciais na máquina onde o Spck CLI roda. Execute o fluxo de login uma vez por agente:

```bash
# Claude Code
claude

# Codex (codex-acp envolve o próprio login do Codex CLI)
codex login

# Gemini CLI
gemini
```

Se você reinstalar ou trocar de máquina, repita o login no novo host. A autenticação é **por host, por agente** — o Spck Editor em si nunca retém essas credenciais.

## <a name="acp-billing"></a>Cobrança e Limites de Uso

Como o ACP roda o agente na sua máquina com suas próprias credenciais, **todo o uso é cobrado na sua conta junto àquele provedor** — não na sua assinatura do Spck Editor. O Spck Editor e os servidores de relay do Spck atuam como puro transporte neste modo e não consomem nada da sua cota de IA in-app para o tráfego ACP.

### Cobrança do Claude Code

> ⚠️ **Importante — Claude Code aplica um bucket de limite de uso separado quando é controlado por ferramentas de terceiros.**
>
> Quando o Claude Code é invocado a partir de um cliente de terceiros via ACP, a Anthropic contabiliza esse tráfego em um **bucket de limite de uso diferente** das suas sessões interativas do CLI `claude` em uma assinatura Pro / Max. Consequência prática: você pode esgotar o bucket de terceiros enquanto ainda tem espaço no Claude Code interativo (ou vice-versa), e você não pode consolidá-los.
>
> Verifique `/usage` dentro do `claude` e o [Anthropic Console](https://platform.claude.com/usage) para ver seu consumo atual, e revise a [documentação de custo e limites do Claude Code](https://code.claude.com/docs/en/costs) para os números aplicáveis ao seu plano.

### Cobrança do Codex (codex-acp)

Cobrado pela auth própria do OpenAI Codex CLI — sua chave de API OpenAI ou login do ChatGPT. O uso conta contra qualquer plano daquela conta. Os preços e cotas são os mesmos do uso interativo do `codex`; veja [openai.com/codex](https://github.com/openai/codex) e o painel da OpenAI para os números atuais.

### Cobrança do Gemini CLI

Cobrado pela sua conta Google ou chave de API Gemini. O uso conta contra o plano Gemini ou cota de API vinculada àquele login. Veja [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits) para detalhes de limite de uso.

## <a name="acp-configuration"></a>Configuração

ACP está habilitado por padrão e configurado via o `spck-cli.config.json` do projeto:

```json
{
  "acp": {
    "enabled": true
  }
}
```

Veja [Configuração → Configurações do ACP](./cli-config#acp-settings) para o esquema completo.

### Desabilitar ACP por projeto

Se você não quiser que o Spck Editor possa controlar um agente local neste host:

```json
{
  "acp": {
    "enabled": false
  }
}
```

Quando desabilitado, o seletor de transporte do editor esconde a opção de agente local e qualquer RPC `acp.*` é rejeitado com `FEATURE_DISABLED`. O assistente de configuração faz esta pergunta na primeira execução (padrão `Y`); configurações que antecedem esta opção são carregadas com `acp.enabled: true` adicionado automaticamente e salvas de novo.

### Desabilitar um único agente

Para evitar que um agente _específico_ seja oferecido enquanto mantém o ACP habilitado para os outros, desinstale o binário desse agente. A detecção roda a cada inicialização do CLI, então o seletor de transporte do editor o removerá da lista.

## <a name="acp-vs-server-routed"></a>ACP Local vs. AI Chat Roteado pelo Servidor

| Capacidade                                  | Roteado pelo servidor (padrão, sem CLI) | Local (ACP, CLI conectado)              |
| ------------------------------------------- | --------------------------------------- | --------------------------------------- |
| Onde o modelo roda                          | Nuvem Spck                              | Sua máquina                             |
| Credenciais                                 | Sua conta Spck Editor                   | Login / chave de API do próprio agente  |
| Acesso a arquivos                           | Sistema de arquivos em memória do editor | Arquivos reais em disco via raiz do CLI |
| Conta contra a cota de IA do Spck Editor    | Sim                                     | **Não** — cobrado do provedor do agente |
| Funciona sem o CLI rodando                  | Sim                                     | Não (requer CLI + WebSocket)            |
| Agentes disponíveis                         | Modelos hospedados pelo Spck            | Claude Code, Codex, Gemini CLI          |
| Prompts de permissão de ferramenta no celular | Quando aplicável                      | Sim, encaminhados via ACP               |
| Streaming de tokens                         | Sim                                     | Sim                                     |
| Chat multi-turno                            | Sim                                     | Sim                                     |

Você pode trocar de transporte no meio do projeto — o AI Chat mostra os caminhos atualmente disponíveis com base no estado de conexão do CLI e nos agentes detectados.

## <a name="acp-tmux"></a>Combinando com Tmux para Sessões Duradouras

Sessões ACP permanecem vivas através de reconexões do editor, mas o processo do Spck CLI em si termina quando seu terminal fecha. Para trabalho de agente de longa duração — grandes refatorações, sessões de planejamento de várias horas — inicie o CLI dentro de uma sessão [tmux](./tmux) para que sobreviva a quedas de SSH, fechamentos de terminal e suspensões do notebook:

```bash
tmux new -s spck
spck
# Ctrl+B depois D para desanexar
```

Você também pode reconectar do seu celular via o terminal do Spck CLI e `tmux attach -t spck` para monitorar o agente ao vivo. Veja [Usando Tmux](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile) para o padrão completo, incluindo rodar o CLI como serviço de fundo persistente.

Para hosts Linux, a página [Claude Skill: Linux Service](./claude-skill) oferece uma configuração de um único comando para rodar o Spck CLI como um serviço `systemd`, de modo que o WebSocket — e qualquer sessão ACP sobre ele — auto-inicia no boot.

## <a name="acp-faq"></a>Perguntas Frequentes

### Posso usar Claude Code no meu celular?

Sim. Instale o Claude Code no seu desktop, autentique com `claude`, e então execute `spck` no seu projeto. Conecte o Spck Editor do seu celular e escolha Claude Code no seletor de transporte do AI Chat. O modelo roda no seu desktop com sua assinatura; você o controla do seu celular.

### O Spck Editor vê minha chave de API Claude / OpenAI / Gemini?

Não. Cada CLI de agente gerencia suas próprias credenciais na máquina onde o Spck CLI roda. Mensagens ACP são tuneladas pelo WebSocket criptografado entre o celular e o CLI, mas os tokens de auth do próprio agente nunca saem do seu host.

### Há custo extra por usar Claude Code através do Spck Editor?

Sem cobrança extra do Spck Editor. O uso do agente conta contra seu plano Anthropic / OpenAI / Google exatamente como se você estivesse rodando o agente interativamente na sua mesa — exceto que a Anthropic aplica um bucket de limite de uso separado para clientes de terceiros; veja [Cobrança e Limites de Uso](#acp-billing) acima.

### Preciso de uma assinatura paga do Spck Editor para usar ACP?

Não. O nível gratuito (30 min/dia de conexão CLI) é suficiente para controlar qualquer agente ACP. Apenas o AI Chat roteado pelo servidor in-app consome cota de IA do Spck Editor.

### O que acontece se eu perder minha conexão Wi-Fi no meio do chat?

O processo do agente continua vivo no host do CLI. Quando o editor se reconecta, a sessão é retomada com o histórico de chat completo. A saída de streaming que chegou enquanto você estava offline é reproduzida na reconexão.

### Posso rodar agentes em um servidor remoto em vez do meu notebook?

Sim. Execute o Spck CLI em qualquer host Linux/macOS alcançável — uma VM de dev, um servidor doméstico, uma estação de trabalho — e conecte-se via o servidor de relay. Combine com [tmux](./tmux) ou o [skill systemd](./claude-skill) para manter o CLI vivo entre conexões.

### O ACP funciona com Spck Editor Lite?

Sim. O tráfego ACP usa o mesmo transporte WebSocket que sistema de arquivos e git, que o Spck Editor Lite suporta. Certifique-se de que `security.userAuthenticationEnabled` está definido como `false` na sua configuração do CLI — a auth Firebase não é suportada no Lite. Veja [Configuração → Autenticação de Usuário](./cli-config#user-authentication).

### Por que meu agente não aparece no AI Chat?

Verifique o log de inicialização do CLI na linha por agente:

- Agente não detectado — instale-o (veja [Agentes de IA Suportados](#acp-supported-agents)).
- Detectado mas ausente do editor — certifique-se de ter completado o fluxo de login do próprio agente (`claude`, `codex login`, `gemini`).
- ACP desabilitado — verifique `acp.enabled` em `.spck-editor/config/spck-cli.config.json`. Veja [Configuração](./cli-config#acp-settings).

## <a name="acp-troubleshooting"></a>Solução de Problemas

### Agente detectado mas a sessão não inicia

Na maioria das vezes isso significa que o agente não está autenticado. Execute o fluxo de login do agente no host do CLI:

```bash
claude              # então complete a auth do navegador
codex login
gemini
```

Se o problema persistir, verifique os logs do CLI em `.spck-editor/logs/` pela saída stderr do agente, que geralmente aponta para a auth ou binário com falha.

### Erros de limite de uso durante um chat

Para o Claude Code, o editor mostra o 429 da Anthropic textualmente. Verifique a [página de uso do Anthropic Console](https://platform.claude.com/usage) e os [docs de custo do Claude Code](https://code.claude.com/docs/en/costs) — lembre-se de que o bucket de limite de uso de terceiros é separado da sua cota interativa do `claude`.

Para Codex e Gemini, o editor mostra o erro de cota do próprio provedor. Resolva pelo console do provedor.

### CLI trava ao iniciar uma sessão ACP

O Spck CLI registra o tráfego ACP em `.spck-editor/logs/`. Acompanhe o arquivo de log mais recente enquanto reproduz o problema:

```bash
tail -f .spck-editor/logs/spck-*.log
```

Abra um bug em [github.com/spck-editor](https://github.com/spck-editor) com o trecho relevante.

### O agente faz alterações fora da raiz do projeto

Agentes ACP têm escopo restrito ao diretório `root` configurado do CLI. Se você vir escritas aparecendo fora dele, abra uma issue — isso não deveria acontecer. Como workaround, execute `spck --root /path/to/specific/project` para estreitar ainda mais o escopo.

## <a name="acp-see-also"></a>Veja Também

- [Primeiros passos com Spck CLI](./cli-start) — instalar, autenticar e conectar pela primeira vez
- [Referência do CLI](./cli) — servidores de relay, fluxo de trabalho diário, limites de conexão
- [Configuração → Configurações do ACP](./cli-config#acp-settings) — a opção de configuração `acp.enabled`
- [Uso Avançado](./cli-advanced) — flags do CLI, múltiplos projetos, dicas de prompt mobile
- [Usando Tmux](./tmux) — manter sessões ACP vivas através de reconexões
- [Claude Skill: Linux Service](./claude-skill) — rodar Spck CLI como serviço `systemd` para que o ACP esteja sempre disponível
- [Especificação do Agent Client Protocol](https://agentclientprotocol.com/) — o padrão aberto que o ACP implementa
- [Documentação do Claude Code](https://docs.claude.com/en/docs/claude-code/overview)
- [Repositório do Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
