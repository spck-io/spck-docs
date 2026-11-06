# <a name="cli-reference"></a>Referência do CLI

## <a name="key-features"></a>Recursos Principais

- **Sistema de Arquivos Remoto**: Acesse e edite arquivos locais pelo aplicativo móvel Spck Editor
- **Integração com Git**: Operações git completas (commit, push, pull, gerenciamento de branches) — requer Git 2.20.0+
- **Acesso ao Terminal**: Sessões de terminal interativas com xterm.js
- **Proxy de Navegador**: Visualize seu servidor local em uma janela de navegador em tela cheia dentro do Spck Editor
- **Busca Rápida**: Busca de arquivos otimizada com detecção automática do ripgrep (100x mais rápido quando instalado)
- **Agentes de IA Locais (ACP)**: Controle Claude Code, Codex ou Gemini CLI a partir do Chat de IA do Spck Editor via [Agent Client Protocol](https://agentclientprotocol.com/). O agente é executado em sua máquina com sua própria assinatura. Veja [Agentes de IA no Mobile (ACP)](./cli-acp).
- **Fast Lane** (Supporter e Gold): Conexão WebRTC direta (peer-to-peer) entre o Spck Editor e o CLI, em média 2x mais rápida que o relay. Veja [Fast Lane](#fast-lane).
- **Seguro**: Requisições assinadas criptograficamente com autenticação Firebase opcional

## <a name="relay-server"></a>Servidor Relay

O CLI se conecta ao Spck Editor por meio de um servidor relay que encaminha mensagens entre os dois. Na primeira execução, o CLI seleciona automaticamente o servidor relay com menor latência e salva a preferência em `~/.spck-editor/.credentials.json`.

**IMPORTANTE**: Tanto o CLI quanto o cliente Spck Editor precisam usar o mesmo servidor relay para se conectar. Se o cliente não encontrar o CLI, verifique se ambos selecionaram o mesmo servidor relay.

### Servidores Relay Disponíveis

| Região          | URL                 |
| --------------- | ------------------- |
| Europa          | `cli-eu-1.spck.io`  |
| América do Norte | `cli-na-1.spck.io`  |
| Sul da Ásia     | `cli-sas-1.spck.io` |
| Leste da Ásia   | `cli-ea-1.spck.io`  |

### Substituindo o Servidor Relay

```bash
# Usar um servidor relay específico
spck --server cli-eu-1.spck.io

# Forma abreviada
spck -s cli-na-1.spck.io
```

A substituição é salva e reutilizada nas execuções seguintes. Para executar a seleção automática novamente, limpe suas credenciais e reinicie:

```bash
spck --logout
spck
```

### Escolhendo um Servidor Relay no Spck Editor

Ao conectar pelo aplicativo móvel via **Link Remote Server**, selecione o mesmo servidor relay no menu suspenso **Relay Server** que o CLI está usando. O nome do servidor relay é exibido na saída do CLI após a conexão.

## <a name="fast-lane"></a>Fast Lane

O Fast Lane é um recurso premium para assinantes **Supporter** e **Gold**. Em vez de encaminhar cada mensagem pelo servidor relay, o Spck Editor se conecta **diretamente ao seu CLI** usando WebRTC (peer-to-peer). Ao eliminar a passagem pelo relay e reduzir as idas e vindas, o Fast Lane é **em média 2x mais rápido que o relay**, e as operações com arquivos, a busca, o Git e a digitação no terminal ficam visivelmente mais responsivos.

O servidor relay continua sendo necessário: é nele que seu CLI é registrado, e ele intermedeia o handshake inicial entre o editor e o CLI. Depois que o caminho direto é estabelecido, os dados do seu projeto passam por ele em vez de passar pelo relay.

### Requisitos

- Uma assinatura **Supporter** ou **Gold** ativa na conta com a qual o CLI está conectado
- Spck CLI **0.7.0 ou posterior** (`npm i -g spck`)
- Suporte a WebRTC tanto no dispositivo que executa o Spck Editor quanto na máquina que executa o CLI

### Ativando ou Desativando o Fast Lane

**No Spck Editor:** Abra **Link Remote Server** (ou edite uma conexão existente pelo menu) e use a chave **⚡ Fast Lane**. Ela vem ativada por padrão para novas conexões em contas Supporter e Gold.

**No CLI:** O Fast Lane vem ativado por padrão. Pressione **`f`** no painel do CLI para ativá-lo ou desativá-lo no projeto atual, ou defina `fastLane.enabled` na [configuração do projeto](./cli-config#fast-lane-settings). As alterações entram em vigor após reiniciar o CLI. Desative-o em redes que bloqueiam tráfego peer-to-peer.

O painel do CLI mostra o status atual do Fast Lane (ativo, disponível, desativado ou indisponível nesta plataforma), e o painel de Arquivos do Spck Editor mostra qual transporte está em uso, junto com o ping atual, por exemplo `Fast Lane · 24 ms` ou `Relay · 80 ms`.

### Fallback Automático

Se não for possível estabelecer uma conexão direta, o Spck Editor recorre automaticamente ao relay para que você possa continuar trabalhando, e exibe um aviso explicando o motivo. Motivos comuns:

- O CLI está desatualizado — atualize com `npm i -g spck`
- O Fast Lane está desativado na configuração do projeto do CLI
- O WebRTC não está disponível na máquina que executa o CLI ou no seu dispositivo
- O servidor relay ainda não oferece suporte ao Fast Lane
- A rede bloqueia o caminho peer-to-peer direto (por exemplo, um firewall corporativo rígido ou NAT)

### Segurança

O tráfego do Fast Lane é criptografado de ponta a ponta pelo WebRTC (DTLS). Além disso, o handshake de autenticação do CLI é vinculado à sessão DTLS específica: o CLI precisa provar que possui o segredo da sua conexão naquele canal exato antes que qualquer dado do projeto seja trocado. Todas as requisições continuam sendo assinadas criptograficamente, como no relay. Veja [Segurança do CLI](./cli-config#security).

## <a name="daily-workflow"></a>Fluxo de Trabalho Diário

### Iniciando sua Sessão

```bash
cd /path/to/project
spck
# Conecte pelo aplicativo móvel (conecta automaticamente ao servidor salvo)
# Comece a codificar
```

### Editando Arquivos

1. Navegue pelos arquivos no aplicativo móvel
2. Toque para abrir e editar
3. Os arquivos são salvos automaticamente no seu computador

### Executando Comandos Git

**Opção 1 - Interface gráfica do aplicativo móvel:**

- Abra o painel Git
- Visualize alterações, adicione arquivos ao stage
- Faça commit e push

**Opção 2 - Terminal:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### Sessões de Terminal

Toque no ícone de terminal no aplicativo móvel para acesso completo ao shell com as permissões do seu usuário.

### Encerrando sua Sessão

```bash
# Mantenha o CLI em execução para reconexões rápidas (recomendado)
# Ou pare com Ctrl+C
```

## <a name="troubleshooting"></a>Resolução de Problemas

### Diretório Raiz Não Encontrado

```bash
# Reconfigurar com o caminho correto
spck --setup

# Ou especificar diretamente
spck --root /correct/path/to/project
```

### Configuração Corrompida

```bash
# Limpar configurações e começar do zero
spck --logout
spck --setup
```

### Problemas de Conexão

1. Verifique a conexão com a internet
2. Confirme que tanto o CLI quanto o Spck Editor estão usando o **mesmo servidor relay** (exibido na saída do CLI após a conexão)
3. Tente sair e reconectar:
   ```bash
   spck --logout
   spck
   ```
4. Verifique as configurações de firewall — certifique-se de que conexões WebSocket (porta 443) são permitidas
5. Se aparecer um aviso de que o Fast Lane está indisponível e o relay está sendo usado, a conexão continua funcionando pelo relay. Veja "Fallback Automático" em [Fast Lane](#fast-lane) para os motivos e as soluções

### QR Code Não Está Sendo Lido

- Escaneie pelo Spck Editor: Projetos → Novo Projeto → Vincular Servidor Remoto e toque no ícone de código QR
- Se o terminal for pequeno demais para mostrar o código, a CLI informa o tamanho necessário. Aumente a janela ou insira os dados manualmente na mesma caixa de diálogo
- Evite leitores de terceiros, que podem expor sua chave secreta

### Operações Git Não Estão Funcionando

1. Verifique se o Git está instalado:

   ```bash
   git --version  # Requer 2.20.0+
   ```

2. Instale se necessário:

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Baixe em git-scm.com
   ```

### Desempenho Lento na Busca

Instale o ripgrep para busca 100x mais rápida:

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# O CLI detecta e usa o ripgrep automaticamente
```

### Permissão Negada

```bash
# Ver permissões
ls -la /path/to/file

# Corrigir se necessário
chmod 644 /path/to/file

# Não use sudo - o CLI deve ser executado como o usuário que possui os arquivos
```

## <a name="connection-limits"></a>Limites de Conexão

O Lite permite editar projetos no seu computador ou em uma VM pública pelo Spck CLI. Projetos remotos exigem uma **conta Spck e uma assinatura Spck ativa**, separadas da compra única do Lite. A assinatura ajuda a cobrir os custos contínuos de hospedagem, operação e manutenção dos servidores Spck. As ferramentas locais de edição e Git incluídas continuam disponíveis sem assinatura.

O número máximo de conexões simultâneas do CLI e os limites de uso diário dependem do tipo de conta:

| Plano     | Conexões CLI | Limite Diário | Fast Lane |
| --------- | ------------ | ------------- | --------- |
| Gratuito  | 1            | 30 minutos    | —         |
| Apoiador  | 2            | Ilimitado     | ✓         |
| Gold      | 5            | Ilimitado     | ✓         |

O uso do plano gratuito é redefinido diariamente à meia-noite UTC.

Quando o limite de conexões é atingido:

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

Quando o limite diário do plano gratuito é atingido:

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

Verifique as conexões ativas:

```bash
spck --account
```

> 💡 **Nota**: Apenas um dispositivo móvel pode se conectar a uma instância do CLI por vez. Cada instância do CLI utiliza um slot de conexão.

## <a name="support"></a>Suporte

- **Site**: [https://spck.io](https://spck.io)
- **Suporte**: Entre em contato pelo aplicativo móvel Spck Editor
