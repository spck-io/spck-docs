# <a name="git-support"></a>Suporte ao Git

O Spck oferece Git para projetos locais no Android e iOS, no navegador e em projetos remotos pelo Spck CLI. Este guia aborda credenciais, pull requests, inspeção de commits, resolução de conflitos e limitações das plataformas.

A integração Git básica, o histórico de commits e a resolução de conflitos estão disponíveis na versão gratuita. A [Integração Git aprimorada](#enhanced-git-integration) adiciona gerenciamento de pull requests e diffs de arquivos de commits.

## <a name="git-credentials"></a>Credenciais Git e pull requests

Abra **Git menu → Git Credentials**, selecione o provedor e salve seu token de acesso. Os links de configuração e ajuda abaixo abrem em outra aba para que você possa voltar ao Spck e colar o token.

| Provedor | Configuração do token | Permissões para Git e pull requests |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">Criar token do GitHub</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Guia de configuração</a> | Selecione o repositório. O link pré-seleciona **Contents: Read and write**, **Pull requests: Read and write** e **Metadata: Read**. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">Criar token do GitLab</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Guia de configuração</a> | O link pré-seleciona o escopo `api` para merge requests. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">Criar token API</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Guia de configuração</a> | Escolha **Create API token with scopes**, selecione **Bitbucket** e marque manualmente `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket` e `write:pullrequest:bitbucket`. A API usa o e-mail da conta Atlassian. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">Guia para criar um PAT</a> | Abra **User settings → Personal access tokens → New Token** na organização, selecione-a e marque manualmente **Code (Read & write)**. |

Para criar uma pull request, faça commit e push da branch de origem e abra **Git menu → Create PR**. Selecione o remoto, as credenciais e uma branch de destino diferente, e informe título e descrição. **Generate with AI** pode redigir a mensagem com base nas alterações commitadas desde o ancestral comum das branches; primeiro faça fetch da branch de destino. Revise o rascunho antes de selecionar **Create PR**. O GitLab cria uma merge request.

Criar e gerenciar pull requests é um **recurso Premium**, incluído na [Integração Git aprimorada](#enhanced-git-integration). O Lite inclui esse acesso na compra única. No aplicativo completo, entre com uma assinatura Supporter, Gold ou Node ativa, ou com a conta proprietária do desbloqueio vitalício do terminal Spck for NodeJS.

## <a name="pull-request-management"></a>Gerenciamento de pull requests (Premium)

Gerencie pull requests sem sair do editor. Os remotos compatíveis são **GitHub.com, GitLab.com, Bitbucket Cloud e Azure DevOps**; o GitLab usa o nome merge requests.

1. Abra um projeto Git e adicione o token em **Git menu → Git Credentials**, com as permissões acima.
2. Abra **Git menu → Pull Requests** e escolha remoto e credenciais para listar solicitações abertas.
3. Selecione uma solicitação para ver título, descrição, autor, branches de origem e destino e status.
4. Selecione um arquivo alterado para examinar seu diff somente leitura antes de fazer merge.
5. Use **Merge** para mesclar uma solicitação apta ou **Close** para fechá-la sem merge. Revisões, verificações, permissões do token e regras das branches continuam valendo; rascunhos e solicitações com conflitos não podem ser mesclados por esse diálogo.

Use **Refresh** para atualizar a lista após alterações no provedor. Os detalhes também incluem um link para revisões, verificações e outras ações no provedor.

Para iniciar uma solicitação, use **Git menu → Create PR** como descrito acima. Se a branch de origem precisar de push, o diálogo oferece **Push** antes da criação. A redação opcional com IA usa seu serviço configurado e seus limites; ela é separada do acesso a pull requests incluído no Lite.

Se a criação falhar por permissões, use o link do provedor para criar ou atualizar o token, salve-o em **Git Credentials** e tente novamente. O rascunho da PR é preservado.

## <a name="enhanced-git-integration"></a>Integração Git aprimorada

A Integração Git aprimorada adiciona duas ferramentas para revisar e compartilhar alterações:

- **Gerenciamento de pull requests:** criar solicitações, consultar as abertas, examinar arquivos e diffs e mesclar ou fechar solicitações. Veja [Gerenciamento de pull requests](#pull-request-management) para configuração e etapas.
- **Inspeção de commits:** examinar arquivos alterados e seus diffs sem modificar os arquivos de trabalho.

Abra **History** no painel Git e selecione um commit para ver arquivos adicionados, modificados e removidos. Selecione um arquivo para abrir um diff somente leitura em relação ao primeiro pai do commit. No primeiro commit, a comparação é com uma árvore vazia. O visualizador usa versões commitadas; alterações não commitadas não afetam o diff. Arquivos binários não são exibidos como diffs de texto.

Você também pode manter uma entrada do histórico pressionada, ou clicar com o botão direito, e escolher **View Commit**.

A Integração Git aprimorada está incluída em:

- **Spck Editor Lite:** desbloqueio permanente pela compra única, sem necessidade de login.
- **Compra vitalícia do terminal Spck for NodeJS:** desbloqueio permanente para a conta proprietária; requer login.
- **Assinaturas Supporter, Gold ou Node:** desbloqueio enquanto a assinatura estiver ativa; requer login.

A integração Git básica e a consulta ao histórico continuam na versão gratuita. Veja os [preços](https://spck.io/pricing) para detalhes dos planos.

## <a name="merge-conflict-resolution"></a>Resolver conflitos de merge

O visualizador de diffs também ajuda a resolver conflitos nos arquivos de trabalho. Isso faz parte da integração Git básica e não requer Premium.

1. Abra um arquivo em conflito na lista de alterações Git.
2. Para cada conflito, escolha **Accept Current**, **Accept Incoming** ou **Accept Both**. Você também pode editar o arquivo para combinar as alterações manualmente.
3. Revise o resultado. Quando todos os marcadores de conflito forem removidos, selecione **Resolve** no visualizador para colocar o arquivo resolvido na área de preparação.
4. Resolva os demais arquivos e faça commit do merge.

Em dispositivos de toque, mantenha arquivos ou entradas Git pressionados para abrir menus de contexto. As letras de status Git complementam as cores dos nomes de arquivos para identificar alterações.

## <a name="git-limitations"></a>Limitações do Git

### <a name="git-limitations-overview"></a>Visão geral

A implementação do Git depende de onde o projeto é armazenado e da versão do Spck:

| Ambiente | Implementação do Git | Principais restrições |
| --- | --- | --- |
| Aplicativos Android e iOS, incluindo Lite e Spck for NodeJS | **libgit2** compilada nativamente para projetos locais | Requer projeto no armazenamento do dispositivo; recursos e restrições do sistema de arquivos continuam valendo. |
| Navegador e editor incorporado | [isomorphic-git](https://isomorphic-git.org/) em JavaScript | Limites de memória, armazenamento e rede do navegador. |
| Projetos remotos pelo Spck CLI | **Binário Git** do computador anfitrião | Usa recursos, sistema de arquivos, credenciais e Git instalado no anfitrião. |

As versões móveis atuais usam Git nativo em vez do motor do navegador. Se aparecer **Native Git requires a device folder**, mova o projeto para o armazenamento do dispositivo. Projetos mantidos apenas no banco de dados do navegador do editor não podem usar o cliente Git nativo móvel.

O gerenciamento de pull requests chama a API do provedor diretamente com o token salvo em **Git Credentials**. Cookies de login do navegador não são usados e as respostas não são armazenadas em cache, permitindo recuperar status e branches atuais ao atualizar. Veja [Credenciais Git e pull requests](#git-credentials) para permissões e [Gerenciamento de pull requests](#pull-request-management) para provedores e ações compatíveis.

### <a name="git-limitations-memory"></a>Restrições de memória

- O Git nativo no Android e iOS opera fora do motor Git em JavaScript. As restrições desse motor não são um limite fixo para o Git móvel.
- O Git nativo ainda precisa de memória e espaço em disco disponíveis. Repositórios ou arquivos pack grandes podem exceder os recursos do dispositivo e causar falhas ou o encerramento do aplicativo pelo sistema.
- O Git do navegador continua sujeito aos limites de memória JavaScript e armazenamento do navegador. Arquivos pack grandes podem exigir muita memória e causar falhas ao clonar ou buscar alterações.

> 💡 **Dica:** Para repositórios grandes, use clones rasos quando possível ou trabalhe com uma parte menor do repositório.

### <a name="git-limitations-symlinks"></a>Compatibilidade com links simbólicos

- O armazenamento do navegador e a camada do sistema de arquivos do dispositivo usam **links simbólicos emulados** para repositórios que contêm links.
- A troca para libgit2 no aplicativo móvel não remove restrições do sistema de arquivos nem garante links simbólicos reais do sistema operacional.
- Links emulados podem se comportar de outra forma com ferramentas de compilação, gerenciadores de pacotes ou scripts que esperam links reais e resolvem destinos durante a execução.
- Para projetos que precisam de links reais, use um projeto remoto em um anfitrião cujo sistema de arquivos e permissões os suportem.

### <a name="git-limitations-cli"></a>Usar a CLI como alternativa

Para repositórios grandes ou fluxos que precisam do sistema de arquivos e ferramentas Git do anfitrião, use um **projeto remoto pelo Spck CLI**. As operações usam o **binário Git do anfitrião** enquanto você edita no Spck:

- As operações usam memória e disco do anfitrião em vez dos recursos do dispositivo móvel ou navegador.
- Links simbólicos seguem o suporte e as permissões do sistema de arquivos do anfitrião.
- Use as ferramentas Git do anfitrião para comandos não disponíveis nos controles do editor.

Veja [Primeiros passos com Spck CLI](./cli-start) para conectar um anfitrião. Projetos remotos requerem uma conta Spck e seguem os limites do plano; veja [Projetos remotos](./editor-lite#remote-projects) para os requisitos de assinatura do Lite. Clonar no armazenamento do dispositivo continua usando o cliente Git nativo móvel.

## <a name="git-related-guides"></a>Guias relacionados

- [Suporte a leitores de tela (experimental)](./screen-reader-support): navegação acessível, controles de versão e feedback.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration): ferramentas Git incluídas na compra única.
- [Primeiros passos com Spck CLI](./cli-start): conectar um projeto remoto para usar as ferramentas Git do anfitrião.
