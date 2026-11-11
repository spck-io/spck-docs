# <a name="getting-started"></a>Primeiros passos com o Spck CLI

## <a name="overview"></a>Visão geral

Spck CLI saiu da versão beta. Conecte seu computador ao Spck Editor no celular ou tablet para editar arquivos, usar Git e terminais e visualizar servidores locais. As conexões usam um relay criptografado ou uma conexão direta [Fast Lane](./cli#fast-lane) (Supporter e Gold).

## <a name="requirements"></a>Requisitos

O Lite permite editar projetos no seu computador ou em uma VM pública pelo Spck CLI. Projetos remotos exigem uma **conta Spck e uma assinatura Spck ativa**, separadas da compra única do Lite. A assinatura ajuda a cobrir os custos contínuos de hospedagem, operação e manutenção dos servidores Spck. As ferramentas locais de edição e Git incluídas continuam disponíveis sem assinatura.

### Obrigatórios

- **Node.js**: **22.22.2+ (22.x), 24.15.0+ (24.x), ou 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Conta do Spck Editor**: Conta gratuita (30 min/dia) ou assinatura Premium (ilimitada)
- **Aplicativo móvel Spck Editor**: [Android](https://play.google.com/store/apps/details?id=io.spck) ou [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Opcionais (Recomendados)

- **Git**: 2.20.0+ para [integração Git](./git-support#git-limitations-cli) em projetos remotos
- **ripgrep**: 15.0.0+ para busca de arquivos significativamente mais rápida (melhoria de 100x)

## <a name="installation"></a>Instalação

### Opção 1: Executar com npx (Sem instalação)

```bash
npx spck@latest
```

Solicita a versão mais recente da CLI, ideal para a configuração inicial ou uso ocasional. `npx spck` pode reutilizar uma versão instalada.

### Opção 2: Instalação global

```bash
npm install -g spck
spck
```

Instale uma vez e execute `spck` no dia a dia. Atualize com `npm install -g spck@latest`. Conexões remotas continuam exigindo internet.

## <a name="demo"></a>Demonstração

[Assista ao vídeo do Spck CLI](https://youtu.be/EtfEhd5EmKM), incluindo o novo recurso Fast Lane.

Uma breve demonstração conectando o Spck CLI ao app móvel e editando arquivos locais remotamente:

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>Configuração inicial

Ao executar o CLI pela primeira vez, um assistente de configuração interativo orienta você através de:

### 1. Autenticação

```bash
spck
# Pressione ENTER para abrir o navegador
# Faça login com sua conta do Spck Editor
# Autorize o CLI
# Retorne ao terminal
```

As credenciais são armazenadas em `~/.spck-editor/.credentials.json` e persistem entre sessões.

Se o navegador não alcançar localhost, o login usa o relay. Use o QR de login ou o link exibido pela CLI para entrar por outro dispositivo. Esse código é diferente do QR de conexão ao projeto.

### 2. Configuração do projeto

O assistente configurará:

- **Diretório raiz**: Diretório base para acesso a arquivos (padrão: diretório atual)
- **Nome do projeto**: Nome de exibição no aplicativo móvel (padrão: nome do diretório)

### 3. Integração com Git (Opcional)

Se um arquivo `.gitignore` for detectado, o CLI oferece adicionar `.spck-editor/` para evitar o commit acidental de segredos:

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**Recomendação**: Escolha `Y` para proteger as credenciais de conexão.

### Executar a configuração novamente

Para reconfigurar a qualquer momento:

```bash
spck --setup
```

## <a name="connecting"></a>Conectando ao Spck Editor

Em projetos novos, a CLI exibe o QR de conexão até o primeiro editor se conectar com sucesso. As próximas execuções abrem o painel diretamente; pressione **`c`** para mostrar o QR e os dados novamente, ou **`l`** para os logs. Aumente o terminal se o QR não couber.

### Método 1: Código QR (Recomendado)

1. Abra o Spck Editor → **Projetos** → **Novo Projeto** → **Vincular Servidor Remoto**
2. Toque no ícone de código QR
3. Escaneie o código QR exibido no terminal. O aplicativo se conecta automaticamente.

> 💡 **Nota**: Você também pode escanear o código com o app Câmera do dispositivo, que abre o link no Spck Editor se o aplicativo estiver instalado.

### Método 2: Entrada manual

Se você não conseguir escanear o código QR:

1. Abra o Spck Editor → **Projetos** → **Novo Projeto** → **Vincular Servidor Remoto**
2. Insira o **ID do Cliente** e o **Segredo** exibidos no terminal
3. Selecione o servidor de retransmissão exibido no terminal
4. Toque em **Conectar**

Se **Require PIN to connect** estiver ativo, digite o PIN escolhido no painel da CLI. O app não salva esse PIN. Veja [PIN de conexão](./cli-config#connection-pin).

## <a name="next-steps"></a>Próximos passos

1. **Entender o sistema de relay**: Saiba como o CLI roteia o tráfego e como escolher um servidor — consulte a [Referência CLI](./cli)
2. **Configurar seu ambiente**: Ajuste as configurações de terminal, segurança e sistema de arquivos — consulte [Configuração](./cli-config)
3. **Explorar recursos avançados**: Comandos CLI, agentes de codificação com IA, múltiplos projetos — consulte [Uso Avançado](./cli-advanced)
4. **Transferir arquivos entre dispositivos**: Copie projetos entre seu celular e desktop sem fio — consulte [Transferência de Arquivos](./cli-file-transfer)
5. **Manter sessões ativas**: Compartilhe sessões entre dispositivos com tmux — consulte [Usando o Tmux](./tmux)
