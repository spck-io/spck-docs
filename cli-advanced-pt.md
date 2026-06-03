# <a name="cli-advanced-usage"></a>Uso avançado do CLI

## <a name="cli-commands"></a>Comandos do CLI

### Comandos básicos

```bash
# Iniciar o CLI
spck

# Executar o assistente de configuração
spck --setup

# Exibir informações da conta
spck --account

# Fazer logout e limpar credenciais
spck --logout

# Exibir ajuda
spck --help

# Exibir versão
spck --version
```

### Opções avançadas

```bash
# Usar arquivo de configuração personalizado
spck --config /path/to/config.json
spck -c /path/to/config.json

# Substituir diretório raiz
spck --root /path/to/project
spck -r /path/to/project

# Substituir servidor de relay (ex.: usar uma região específica)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>Agentes de codificação com IA (ACP)

A Spck CLI conecta o Chat de IA do Spck Editor a um agente de codificação com IA instalado localmente — **Claude Code**, **Codex** ou **Gemini CLI** — através do [Agent Client Protocol (ACP)](https://agentclientprotocol.com/). O modelo é executado na sua máquina com sua própria assinatura, edita arquivos reais no disco e encaminha as solicitações de permissão para o seu celular.

![Modo IA local no Chat de IA do Spck Editor controlando o Claude Code a partir de um celular](https://docs.spck.io/assets/gifs/acp-ai.gif)

→ **[Agentes de IA no Mobile (ACP)](./cli-acp)** — o guia completo: agentes suportados, instalação, cobrança e limites de taxa (incluindo a cota separada da Anthropic para Claude Code de terceiros), configuração, FAQ e solução de problemas.

> 💡 **Dica**: Use o **tmux** para manter as sessões de agentes de IA em execução mesmo após desconectar. Inicie uma sessão tmux no seu desktop (`tmux new -s code`), inicie o agente e reconecte-se pelo terminal Spck CLI no seu celular (`tmux attach -t code`). Funciona tanto para agentes de shell quanto para agentes em modo ACP. Veja [Usando Tmux](./tmux) para um guia completo, incluindo configuração de servidor remoto persistente.

## <a name="advanced-usage"></a>Uso avançado

### Múltiplos projetos

Execute instâncias separadas do CLI para diferentes projetos simultaneamente:

```bash
# Terminal 1: Projeto A
cd /path/to/projectA
spck

# Terminal 2: Projeto B
cd /path/to/projectB
spck
```

Cada projeto mantém sua própria configuração e conexão.

> 💡 **Dica**: Você também pode usar múltiplas instâncias do CLI para transferir arquivos entre seu desktop e celular. Consulte [Transferência de Arquivos entre Mobile e Desktop](./cli-file-transfer) para um guia passo a passo.

### Arquivos de configuração personalizados

Crie configurações especializadas para diferentes cenários:

```bash
# Configuração de desenvolvimento
spck --config ~/configs/dev-config.json

# Configuração de produção (somente leitura, sem terminal)
spck --config ~/configs/prod-config.json
```

### Configuração específica por ambiente

**Desenvolvimento local:**

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

**Servidor de produção:**

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

Reduza o monitoramento de arquivos adicionando mais padrões de exclusão:

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

Limite terminais simultâneos:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>Reduzindo o prompt do shell para mobile

Em dispositivos móveis, o espaço horizontal na tela é limitado. O prompt padrão do shell — que normalmente inclui o caminho do diretório atual, nome de usuário e nome do host — pode sobrecarregar o terminal e dificultar a leitura da saída dos comandos.

Mudar seu prompt para apenas `$ ` proporciona uma experiência de terminal muito mais limpa em telas pequenas.

### Bash

Adicione o seguinte ao `~/.bashrc`:

```bash
export PS1='\$ '
```

Aplique sem reiniciar o shell:

```bash
source ~/.bashrc
```

### Zsh

Adicione o seguinte ao `~/.zshrc`:

```zsh
PROMPT='$ '
```

Aplique sem reiniciar o shell:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

Crie seu arquivo de perfil se ele ainda não existir e, em seguida, abra-o:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Adicione o seguinte ao perfil:

```powershell
function prompt { "$ " }
```

Aplique sem reiniciar o shell:

```powershell
. $PROFILE
```

### Prompt de Comando (Windows)

Defina um prompt mínimo para a sessão atual:

```cmd
PROMPT $$
```

Para tornar isso permanente, adicione `PROMPT` como uma variável de ambiente de **Usuário** ou **Sistema** com o valor `$$` via **Painel de Controle → Sistema → Configurações Avançadas do Sistema → Variáveis de Ambiente**.
