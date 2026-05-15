# <a name="cli-file-transfer"></a>Transferência de Arquivos entre Mobile e Desktop

## <a name="overview"></a>Visão geral

Quando você executa o Spck CLI no seu desktop, ele age como um hub de sincronização entre o sistema de arquivos do seu desktop e os projetos locais armazenados no seu celular. Ambos os lados aparecem lado a lado no gerenciador de arquivos do Spck Editor — os projetos locais do seu celular à esquerda e os arquivos do seu desktop como um servidor remoto conectado — e você pode copiar arquivos ou pastas inteiras em qualquer direção usando os comandos padrão de copiar e colar.

Não é necessário AirDrop, Bluetooth, cabo USB ou armazenamento em nuvem de terceiros. As transferências são criptografadas de ponta a ponta por uma conexão WebSocket e permanecem na sua Wi-Fi local quando ambos os dispositivos estão na mesma rede.

## <a name="how-it-works"></a>Como funciona

O CLI expõe seu diretório do desktop como um projeto de servidor remoto no gerenciador de arquivos do Spck Editor. Os projetos locais salvos no seu celular são armazenados no armazenamento local do aplicativo. O Spck Editor trata ambos como locais de projeto de primeira classe, portanto qualquer operação de arquivo que funcione dentro de um único projeto — incluindo copiar e colar — também funciona entre eles.

```
Celular (armazenamento local)  Desktop (via CLI)
─────────────────────────────  ─────────────────────
my-project/               ↔   ~/projects/my-project/
  ├── index.html                 ├── index.html
  ├── style.css                  ├── style.css
  └── assets/                    └── assets/
      └── logo.png                   └── logo.png
```

Os diretórios são transferidos recursivamente — todos os arquivos internos são copiados, com subdiretórios criados automaticamente no destino.

## <a name="desktop-to-mobile"></a>Do desktop para o mobile

Use isso quando quiser trazer arquivos do seu computador para o celular — por exemplo, para trabalhar offline, compartilhar um projeto com um colega que só tem o aplicativo móvel, ou tirar um instantâneo do seu trabalho para o dispositivo.

1. **Inicie o CLI** no seu desktop, apontando para a pasta da qual deseja transferir:

   ```bash
   spck --root ~/projects
   ```

2. **Conecte seu celular** escaneando o código QR com o aplicativo de câmera e abrindo o link no Spck Editor.

3. No Spck Editor, sua pasta do desktop aparece como um projeto de servidor remoto no painel **Projetos**.

4. **Mantenha pressionado o arquivo ou pasta** que deseja no projeto remoto e toque em **Copiar**.

5. **Navegue até um projeto local** no seu celular (ou crie um novo via **Novo Projeto**).

6. **Mantenha pressionada a pasta de destino** e toque em **Colar**.

Os arquivos são baixados do seu desktop e salvos no armazenamento local do seu celular.

## <a name="mobile-to-desktop"></a>Do mobile para o desktop

Use isso quando quiser enviar trabalho do seu celular de volta para o desktop — por exemplo, após editar em trânsito, ou para consolidar projetos criados no dispositivo.

1. **Inicie o CLI** no seu desktop, apontando para a pasta onde deseja que os arquivos sejam salvos:

   ```bash
   spck --root ~/Desktop/from-phone
   ```

2. **Conecte seu celular** escaneando o código QR.

3. No Spck Editor, abra o **projeto local** no seu celular que contém os arquivos que deseja enviar.

4. **Mantenha pressionado o arquivo ou pasta** que deseja e toque em **Copiar**.

5. **Navegue até o projeto remoto do desktop** no painel **Projetos**.

6. **Mantenha pressionada a pasta de destino** e toque em **Colar**.

Os arquivos são lidos do armazenamento local do seu celular e gravados no seu desktop via CLI.

## <a name="transferring-projects"></a>Transferindo projetos inteiros

Você pode copiar uma pasta de projeto inteira em uma única operação de colagem. Mantenha pressionada a raiz do projeto na árvore de arquivos e selecione **Copiar**, depois navegue até o destino e **Cole**. Toda a árvore de diretórios — incluindo todos os arquivos em todos os subdiretórios — é transferida.

Isso é útil para:

- **Fazer backup de um projeto mobile no seu desktop** antes de fazer grandes alterações
- **Inicializar um novo projeto no celular** a partir de uma base de código existente no desktop
- **Consolidar trabalho** de múltiplos dispositivos em um só lugar

## <a name="tips"></a>Dicas

### Limite de tamanho de arquivo

O tamanho máximo padrão de arquivo é de **10 MB** por arquivo. Para transferir arquivos maiores como imagens, arquivos comprimidos ou binários compilados, aumente o limite na configuração do seu CLI:

```json
{
  "filesystem": {
    "maxFileSize": "200MB"
  }
}
```

Consulte [Configuração CLI](./cli-config) para detalhes completos.

### Velocidade de transferência

A velocidade depende inteiramente da sua conexão Wi-Fi local ou de internet. Para diretórios grandes, as transferências são feitas arquivo por arquivo, então o rendimento geral escala com o número de arquivos. Em uma rede Wi-Fi doméstica típica, projetos pequenos com muitos arquivos de texto (centenas de arquivos) são concluídos em alguns segundos.

### Segurança

Todas as transferências são criptografadas via WSS (WebSocket Secure) e cada requisição é assinada com uma chave secreta por sessão. O servidor de relay encaminha mensagens entre dispositivos, mas nunca recebe conteúdo não criptografado. Consulte [Segurança CLI](./cli-config#security) para detalhes completos.

### Executando múltiplas transferências

O CLI expõe um único diretório raiz. Para transferir de múltiplos locais simultaneamente, execute instâncias separadas do CLI em terminais diferentes:

```bash
# Terminal 1: expor ~/projects
spck --root ~/projects

# Terminal 2: expor ~/Documents
spck --root ~/Documents
```

Cada instância gera seu próprio código QR e conexão, e ambos os servidores remotos aparecem no painel **Projetos** do Spck Editor ao mesmo tempo.
