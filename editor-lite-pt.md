# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Visao geral

Spck Editor Lite e uma versao de compra unica do Spck Editor que desbloqueia recursos de edicao premium sem assinatura. Esta disponivel como um aplicativo separado tanto para Android quanto para iOS.

O Lite inclui tudo da versao gratuita, alem de:

- **Predictive Keyboard** -- sugestoes de simbolos contextuais no teclado adicional
- **Snippets personalizados** -- modelos de codigo definidos pelo usuario com marcadores de tabulacao
- **Tema Neon** -- um tema de editor exclusivo

Esses recursos tambem estao disponiveis na versao completa do Spck Editor com uma assinatura Gold ou Supporter ativa. O aplicativo Lite oferece a mesma funcionalidade como compra unica.

## <a name="predictive-keyboard"></a>Predictive Keyboard

O Predictive Keyboard substitui o teclado adicional padrao por uma linha de teclas de simbolos contextuais. Em vez de pressionar e segurar uma tecla para escolher em um menu, os simbolos mais provaveis sao exibidos diretamente com base na posicao do cursor no arquivo.

### Como funciona

As previsoes sao geradas a partir de tabelas de frequencia estatistica construidas por linguagem. Quando o cursor se move, o teclado reordena os simbolos com base na frequencia com que cada um aparece nesse tipo de posicao em codigo real. As linguagens suportadas incluem JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown e texto simples.

### Ativar ou desativar

Va para `Settings > Touch > Predictive Keyboard` para alternar o recurso. No Lite, o Predictive Keyboard esta ativado por padrao. Desativa-lo restaura o teclado adicional padrao.

> O Predictive Keyboard esta disponivel apenas em dispositivos com tela sensivel ao toque. Ele nao aparece ao usar um teclado fisico ou no modo tablet com um teclado externo conectado.

## <a name="custom-snippets"></a>Snippets personalizados

Os snippets personalizados permitem criar modelos de codigo reutilizaveis que aparecem na lista de autocompletar enquanto voce digita. Cada snippet e associado a uma linguagem especifica para que seus snippets JavaScript nao aparecam em arquivos Python.

### Criar um snippet

1. Abra `Settings > Editor > Custom Snippets`
2. Selecione a linguagem (ex.: JavaScript, Python, HTML)
3. Toque em **Adicionar snippet**
4. Insira um **gatilho** -- a abreviacao que voce digita para invocar o snippet
5. Insira o **corpo** -- o codigo que sera inserido

### Tabulacoes e marcadores

Os snippets suportam tabulacoes para que o cursor salte entre posicoes editaveis apos a insercao:

- `$1`, `$2`, `$3` -- tabulacoes numeradas na ordem de percurso
- `$0` -- posicao final do cursor apos todas as tabulacoes
- `${1:defaultText}` -- uma tabulacao com texto de marcador pre-selecionado para facilitar a substituicao

Exemplo -- um snippet de loop `for` em JavaScript:

**Gatilho:** `forloop`

**Corpo:**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

Ao digitar `forloop` e seleciona-lo no autocompletar, o loop completo e inserido. Pressione Tab para alternar entre `i`, `array` e o corpo do loop.

### Importar e exportar

Voce pode exportar todos os snippets para um arquivo e importa-los em outro dispositivo. Isso e util para compartilhar colecoes de snippets entre celulares ou fazer backup da sua configuracao.

## <a name="neon-theme"></a>Tema Neon

O Lite inclui o tema de editor **Neon**, um tema escuro com cores de destaque vibrantes. Ele e definido como tema padrao no Lite e pode ser alterado a qualquer momento em `Settings > Appearance > Theme`.

## <a name="comparison"></a>Comparacao de recursos

| Recurso | Gratuito | Lite (Compra unica) | Completo (Assinatura) |
| --- | :---: | :---: | :---: |
| Edicao de codigo e destaque de sintaxe | Sim | Sim | Sim |
| Integracao com Git | Sim | Sim | Sim |
| Teclado adicional | Sim | Sim | Sim |
| Teclado sensivel ao toque e cursores | Sim | Sim | Sim |
| Pre-visualizacao do projeto | Sim | Sim | Sim |
| Predictive Keyboard | -- | Sim | Gold / Supporter |
| Snippets personalizados | -- | Sim | Gold / Supporter |
| Tema Neon | -- | Sim | -- |
| Assistente de IA | -- | -- | Sim |
| Contas de usuario e sincronizacao na nuvem | -- | -- | Sim |
| Labs / Projetos da comunidade | -- | -- | Sim |
