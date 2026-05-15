# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>Visão geral

A Spck CLI inclui uma ponte Language Server Protocol (LSP) completa que executa servidores de linguagem para TypeScript, JavaScript, Python, HTML, CSS e SCSS diretamente no seu host remoto. Quando conectado a uma sessão CLI, o Spck Editor usa automaticamente o servidor de linguagem remoto em vez do integrado ao dispositivo móvel.

> 💡 **Dica**: Para uma descrição do servidor de linguagem integrado disponível sem a CLI, consulte [Editor Language Server](./editor-language-server).

## <a name="cli-ls-architecture"></a>Arquitetura

O servidor de linguagem da CLI é executado na mesma máquina que os arquivos do seu projeto. Isso oferece várias vantagens significativas em relação à abordagem baseada em navegador usada em dispositivos móveis:

### Sem transmissão de arquivos

Com o servidor de linguagem móvel integrado, os arquivos precisam ser transmitidos para o dispositivo e carregados em um worker do navegador antes que o servidor possa analisá-los. Com a CLI, o servidor de linguagem lê os arquivos diretamente do disco — sem transmissão. Isso elimina o consumo de largura de banda e mantém a análise rápida mesmo em projetos grandes.

### Conhecimento completo do projeto

O servidor de linguagem da CLI tem acesso a todo o diretório do seu projeto, incluindo:

- Todos os arquivos-fonte em cada subdiretório
- `node_modules/` para resolução de tipos de terceiros
- Arquivos `tsconfig.json` descobertos automaticamente em qualquer nível
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` e arquivos de declaração associados

Isso significa que ir para definição, localizar referências e renomear símbolo funcionam corretamente entre arquivos — mesmo quando você não os abriu no editor.

### Tratamento correto do `tsconfig.json`

O servidor de linguagem TypeScript descobre e respeita automaticamente o `tsconfig.json` (ou `jsconfig.json`) do seu projeto. Aliases de caminho (`paths`), opções do compilador (`strict`, `target`, `lib`), referências de projeto e layouts de workspace em monorepos são todos tratados corretamente. O servidor de linguagem móvel integrado não consegue ler `tsconfig.json` porque não tem acesso ao sistema de arquivos na inicialização.

### Processo persistente

O processo do servidor de linguagem permanece ativo durante toda a sessão CLI. Ele constrói um índice em memória do seu projeto e o mantém atualizado entre as edições, de modo que as respostas continuam rápidas mesmo após a inicialização inicial.

## <a name="cli-ls-features"></a>Recursos suportados

| Recurso | Descrição |
| --- | --- |
| **Conclusão de código** | Sugestões com reconhecimento de contexto e assinaturas de tipo, ordenadas por relevância |
| **Informação ao passar o cursor** | Informações de tipo e documentação JSDoc para o símbolo sob o cursor |
| **Ajuda de assinatura** | Dicas de parâmetros e documentação ao digitar uma chamada de função |
| **Ir para definição** | Saltar para a declaração de qualquer símbolo, incluindo os de `node_modules` |
| **Localizar referências** | Listar cada uso de um símbolo em todo o projeto |
| **Renomear símbolo** | Renomear um símbolo e atualizar todas as referências de forma atômica |
| **Diagnósticos** | Destaques de erros e avisos em tempo real enquanto você digita |
| **Renderização Markdown** | Documentação de hover e assinatura renderizada como Markdown com blocos de código com realce de sintaxe |

## <a name="cli-ls-languages"></a>Linguagens suportadas

| Linguagem | Conclusão | Hover | Assinaturas | Diagnósticos |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>Configuração

O suporte ao servidor de linguagem está habilitado por padrão. Você pode controlá-lo no seu arquivo de configuração:

```json
{
  "languageServer": {
    "enabled": true,
    "typescript": {
      "enabled": true
    },
    "python": {
      "enabled": true
    }
  }
}
```

- **`languageServer.enabled`** (boolean): Interruptor principal para todos os servidores de linguagem remotos. Padrão: `true`.
- **`languageServer.typescript.enabled`** (boolean): Habilitar o servidor de linguagem TypeScript/JavaScript. Padrão: `true`.
- **`languageServer.python.enabled`** (boolean): Habilitar o servidor de linguagem Python (requer `pylsp` no `PATH`). Padrão: `true`.

## <a name="cli-ls-requirements"></a>Requisitos

- **TypeScript / JavaScript**: Incluído com a CLI. Nenhuma instalação adicional necessária.
- **Python**: Requer [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) (`pip install python-lsp-server`).
- **HTML / CSS / SCSS**: Incluído com a CLI. Nenhuma instalação adicional necessária.

## <a name="cli-ls-vs-mobile"></a>CLI vs. servidor de linguagem móvel

| Capacidade | CLI Language Server | Integrado no móvel |
| --- | --- | --- |
| Acesso completo aos arquivos do projeto | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| Resolução de tipos `node_modules` | ✓ | — |
| Ir para definição entre arquivos | ✓ | Limitado |
| Localizar referências entre arquivos | ✓ | — |
| Renomear símbolo | ✓ | — |
| Suporte a Python | ✓ | — |
| Funciona offline (sem CLI) | — | ✓ |

&nbsp;

&nbsp;
