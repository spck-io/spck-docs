# <a name="cli-configuration"></a>Configuração do CLI

## <a name="configuration"></a>Configuração

### Localização do Arquivo de Configuração

A configuração é armazenada em `.spck-editor/config/spck-cli.config.json` no diretório do seu projeto.

**Importante**: `.spck-editor/config` é um **link simbólico** para `~/.spck-editor/projects/{project_id}/`, mantendo as informações sigilosas fora do diretório do projeto.

### Configuração Padrão

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### Configurações do Proxy de Navegador

- **`browserProxy.enabled`** (boolean): Ativa/desativa o recurso de proxy de navegador
  - Padrão: `true`
  - Defina como `false` para impedir que o aplicativo móvel abra uma sessão de proxy de navegador pelo CLI

### Configurações do Terminal

- **`terminal.enabled`** (boolean): Ativa/desativa o acesso ao terminal
  - Padrão: `true`
  - Defina como `false` para reduzir o risco de acesso não autorizado ao terminal

- **`terminal.maxBufferedLines`** (number): Buffer máximo de rolagem
  - Padrão: `10000`
  - Afeta o uso de memória (~1MB por 10 mil linhas)

- **`terminal.maxTerminals`** (number): Número máximo de sessões de terminal simultâneas
  - Padrão: `10`
  - Cada terminal usa aproximadamente 5–10MB de memória

### Configurações do Sistema de Arquivos

- **`filesystem.maxFileSize`** (string): Tamanho máximo de arquivo para leitura/escrita
  - Padrão: `"10MB"`
  - Aceita: `"5MB"`, `"50MB"`, etc.

- **`filesystem.watchIgnorePatterns`** (string[]): Padrões a excluir do monitoramento de arquivos
  - Padrão: Ignora saídas de build e dependências
  - Melhora o desempenho ao evitar milhares de arquivos gerados

### Configurações de Segurança

- **`security.userAuthenticationEnabled`** (boolean): Ativa a autenticação de usuário via Firebase
  - Padrão: `false`
  - Quando `false`: Menor latência, compatível com o Lite, ainda protegido por assinatura de requisições
  - Quando `true`: Camada extra de segurança, verificação de identidade do usuário, adiciona 2–20s de latência inicial
  - **Todas as requisições são sempre assinadas criptograficamente, independentemente desta configuração**

## <a name="security"></a>Segurança

### Conexões Criptografadas

Toda a comunicação utiliza:

- **WSS (WebSocket Secure)**: Criptografia TLS/SSL
- **HTTPS**: Handshake inicial criptografado

### Assinatura de Requisições

Cada requisição é assinada criptograficamente:

- A chave secreta é gerada localmente e nunca transmitida pela internet
- Recomenda-se não usar leitores de QR code de terceiros, pois podem expor sua chave secreta

### Boas Práticas

1. **Proteja as credenciais**:

   ```bash
   # Adicionar ao .gitignore (automático durante a configuração)
   echo ".spck-editor/" >> .gitignore
   ```

2. **Saia em máquinas compartilhadas**:

   ```bash
   spck --logout
   ```

3. **Limite os diretórios expostos**:

   ```bash
   # Em vez de expor o diretório home inteiro
   spck --root /path/to/specific/project
   ```

4. **Desative o terminal se não for necessário**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **Desative o proxy de navegador se não for necessário**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>Autenticação de Usuário

O Spck CLI suporta autenticação de usuário via Firebase opcional como uma segunda camada de segurança, adicional à assinatura de requisições sempre ativa.

### Como Funciona

Quando ativada, o CLI exige que você entre com sua conta Spck Editor. As conexões são autenticadas usando tokens de ID do Firebase que expiram a cada hora e são renovados automaticamente usando tokens de atualização seguros armazenados em `~/.spck-editor/.credentials.json`.

### Ativando a Autenticação de Usuário

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### Compensações

|                         | Desativado (padrão)         | Ativado                                      |
| ----------------------- | --------------------------- | -------------------------------------------- |
| **Proteção**            | Chave de assinatura secreta | + Verificação de identidade via Firebase     |
| **Latência inicial**    | Sem sobrecarga de auth      | Adiciona 2–20s na primeira conexão           |
| **Spck Editor Lite**    | ✅ Compatível               | ❌ Não compatível                            |
| **Uso offline**         | Funciona sem internet       | Requer internet para renovação do token      |

### Quando Ativar

**Mantenha desativado (padrão) quando:**

- Usar o **Spck Editor Lite** — o login via Firebase não é suportado no Lite; definir como `true` impedirá que usuários do Lite se conectem
- Trabalhar em uma rede local ou ambiente confiável onde a chave de assinatura secreta é suficiente
- Minimizar a latência de conexão for uma prioridade

**Ative quando:**

- O CLI estiver exposto em um servidor acessível pela internet
- Você quiser a verificação de identidade do usuário como uma camada adicional de controle de acesso além da chave de assinatura

> ⚠️ **O Spck Editor Lite não suporta autenticação via Firebase.** Se `userAuthenticationEnabled` for definido como `true`, o Spck Editor Lite não poderá se conectar. Mantenha esta configuração em `false` ao usar o Lite.
