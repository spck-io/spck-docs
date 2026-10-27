# Intégrer l’éditeur

Intégrez Spck Editor dans un iframe pour créer des exemples modifiables, des tutoriels ou des outils de code. Le wrapper `SpckEditor` communique avec l’iframe par `postMessage` et `MessageChannel`.

## <a name="screen-reader-support"></a>Prise en charge des lecteurs d’écran (expérimental)

Consultez [Prise en charge des lecteurs d’écran (expérimental)](./screen-reader-support#screen-reader-limitations) pour les fonctions d’accessibilité et les limites actuelles. L’éditeur intégré n’active pas automatiquement le mode mobile d’édition avec un lecteur d’écran.

La [référence complète de l’API en anglais](/en/editor-embed) décrit la configuration, les projets et fichiers, les réglages, les événements et le dépannage. Le code et les déclarations TypeScript sont disponibles dans [spckio/spck-embed](https://github.com/spckio/spck-embed).
