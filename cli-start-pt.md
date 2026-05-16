# <a name="getting-started"></a>Primeiros passos com o Spck CLI

## <a name="overview"></a>Visão geral

O Spck CLI é uma ferramenta de linha de comando que conecta seu ambiente de desenvolvimento local ao aplicativo móvel Spck Editor por meio de uma conexão WebSocket segura. Uma vez em execução, você pode navegar e editar arquivos locais, executar comandos no terminal e visualizar servidores locais — tudo a partir do seu celular ou tablet.

## <a name="requirements"></a>Requisitos

### Obrigatórios

- **Node.js**: 18.0.0 ou superior
- **Conta do Spck Editor**: Conta gratuita (30 min/dia) ou assinatura Premium (ilimitada)
- **Aplicativo móvel Spck Editor**: [Android](https://play.google.com/store/apps/details?id=io.spck) ou [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Opcionais (Recomendados)

- **Git**: 2.20.0+ para recursos de integração com Git
- **ripgrep**: 15.0.0+ para busca de arquivos significativamente mais rápida (melhoria de 100x)

## <a name="installation"></a>Instalação

### Opção 1: Executar com npx (Sem instalação)

```bash
npx spck
```

Sempre usa a versão mais recente — perfeito para configuração inicial ou uso ocasional.

### Opção 2: Instalação global

```bash
npm install -g spck
spck
```

Inicialização mais rápida, funciona offline e conveniente para uso diário.

## <a name="demo"></a>Demonstração

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

Assim que o CLI estiver em execução, ele exibirá um código QR e os detalhes de conexão.

### Método 1: Código QR (Recomendado)

**IMPORTANTE**: Instale o aplicativo Spck Editor ANTES de escanear o código QR.

**No Android:**

1. Use o aplicativo de câmera ou o scanner QR nas configurações rápidas
2. Quando detectado, toque na notificação para abrir o Spck Editor
3. O aplicativo se conecta automaticamente

> 💡 **Nota**: Alguns leitores de código QR não conseguem lidar com o esquema personalizado para abrir o Spck Editor diretamente. Copie a URL e cole-a no Chrome, que iniciará o Spck Editor pela URL.

**No iOS:**

1. Use o aplicativo de câmera ou o scanner QR na Central de Controle
2. Quando detectado, toque na notificação para abrir o Spck Editor
3. O aplicativo se conecta automaticamente

> 💡 **Nota**: O Spck Editor NÃO possui um scanner QR integrado. Use a função QR nativa do seu dispositivo.

### Método 2: Entrada manual

Se o código QR não funcionar:

1. Abra o Spck Editor → **Projetos** → **Novo Projeto** → **Vincular Servidor Remoto**
2. Insira o **ID do Cliente** e o **Segredo** exibidos no terminal
3. Toque em **Conectar**

## <a name="next-steps"></a>Próximos passos

1. **Entender o sistema de relay**: Saiba como o CLI roteia o tráfego e como escolher um servidor — consulte a [Referência CLI](./cli)
2. **Configurar seu ambiente**: Ajuste as configurações de terminal, segurança e sistema de arquivos — consulte [Configuração](./cli-config)
3. **Explorar recursos avançados**: Comandos CLI, agentes de codificação com IA, múltiplos projetos — consulte [Uso Avançado](./cli-advanced)
4. **Transferir arquivos entre dispositivos**: Copie projetos entre seu celular e desktop sem fio — consulte [Transferência de Arquivos](./cli-file-transfer)
5. **Manter sessões ativas**: Compartilhe sessões entre dispositivos com tmux — consulte [Usando o Tmux](./tmux)
