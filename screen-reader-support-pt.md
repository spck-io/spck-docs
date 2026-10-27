# <a name="screen-reader-support"></a>Suporte a leitores de tela (experimental)

O suporte a leitores de tela é **experimental** e abrange os fluxos principais do editor. A compatibilidade pode variar conforme o dispositivo, o sistema operacional e o leitor; alguns controles e recursos avançados ainda podem precisar de melhorias.

## <a name="screen-reader-activation"></a>Ativar a edição com leitor de tela

Ative o leitor de tela nas configurações de acessibilidade do dispositivo. Nas versões móveis que informam seu estado, o Spck apresenta automaticamente o documento ativo em um campo de texto acessível. Não há uma configuração separada no editor para ativar esse modo.

O campo disponibiliza o conteúdo e o nome do arquivo para leitura, seleção e edição. As alterações usam o salvamento automático normal; a seleção permanece sincronizada e desfazer e refazer continuam disponíveis. Ao trocar de arquivo, o conteúdo e o nome são atualizados; documentos somente leitura permanecem assim. Desativar o leitor restaura o editor habitual nas versões compatíveis.

## <a name="screen-reader-navigation"></a>Navegação e controles

Os fluxos compatíveis incluem:

- Rótulos no idioma da interface para botões com ícones, abas de navegação e arquivos, controles de pesquisa e ações de controle de versão.
- Linhas de arquivos e projetos que podem ser ativadas pelo leitor ou teclado. As pastas informam seu estado expandido; no teclado físico, use as setas direita e esquerda para expandir e recolher.
- Abas que indicam o arquivo ativo e letras de status Git que complementam as cores dos nomes de arquivos.
- Configurações associadas a seus rótulos e estados e campos de formulário que disponibilizam erros de validação.
- Diálogos nomeados que mantêm o foco do teclado dentro enquanto estão abertos e o devolvem ao controle de origem ao fechar. Os menus de ações recebem o foco ao abrir e o devolvem ao fechar com Escape.

No teclado físico, use **Tab** para percorrer os controles, **Enter** ou **Espaço** para ativar botões e **Escape** para fechar menus de ações. Você também pode usar os gestos habituais de navegação e ativação do leitor de tela.

## <a name="screen-reader-limitations"></a>Limitações atuais

- A edição acessível depende de o aplicativo móvel informar que o leitor está ativado. O navegador e o editor incorporado não ativam esse modo automaticamente.
- O suporte cobre atualmente os fluxos principais acima. Interações avançadas e outros recursos podem funcionar de maneira diferente conforme o leitor.
- O comportamento pode variar entre versões do aplicativo, sistemas e dispositivos. Relate controles inacessíveis ou impossíveis de ativar, mudanças inesperadas de foco e problemas de leitura ou edição.

Consulte [Atalhos de teclado](./editor#keyboard-shortcuts) para comandos de edição e [Suporte e limitações do Git](./git-support#git-limitations) para as diferenças entre Git móvel, no navegador e remoto.

## <a name="screen-reader-feedback"></a>Feedback

[Envie feedback para support@spck.io](mailto:support@spck.io) se um controle estiver sem nome, o foco for perdido ou a leitura ou edição não funcionar como esperado. Inclua a versão do Spck, o dispositivo e sistema operacional, o leitor de tela e os passos para reproduzir o problema.
