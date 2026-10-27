# <a name="screen-reader-support"></a>Prise en charge des lecteurs d’écran (expérimental)

La prise en charge des lecteurs d’écran est **expérimentale** et couvre les principales tâches de l’éditeur. La compatibilité varie selon l’appareil, le système d’exploitation et le lecteur d’écran ; certains contrôles et fonctions avancées peuvent encore nécessiter des améliorations.

## <a name="screen-reader-activation"></a>Activer l’édition avec un lecteur d’écran

Activez votre lecteur d’écran dans les réglages d’accessibilité de l’appareil. Sur les versions mobiles qui signalent son état, Spck présente automatiquement le document actif dans un champ de texte accessible. Aucun réglage distinct de l’éditeur n’est nécessaire.

Ce champ expose le contenu du document et son nom pour lire, sélectionner et modifier le texte. Les modifications utilisent l’enregistrement automatique habituel ; la sélection reste synchronisée et les fonctions annuler et rétablir restent disponibles. Changer de fichier actualise le contenu et le nom ; les documents en lecture seule le restent. Désactiver le lecteur d’écran rétablit l’éditeur habituel sur les versions compatibles.

## <a name="screen-reader-navigation"></a>Navigation et contrôles

Les fonctions prises en charge comprennent :

- Des libellés pour les boutons à icône, les onglets de navigation et de fichiers, les contrôles de recherche et les actions de gestion de versions, dans la langue de l’interface.
- Des lignes de fichiers et de projets activables au clavier ou avec un lecteur d’écran. Les dossiers exposent leur état ouvert ou fermé ; au clavier physique, les flèches droite et gauche permettent de les ouvrir et de les fermer.
- Des onglets qui indiquent le fichier actif et des lettres d’état Git qui complètent les couleurs des noms de fichiers.
- Des réglages associés à leurs libellés et états, et des champs de formulaire qui exposent les erreurs de validation.
- Des boîtes de dialogue nommées qui gardent le focus clavier à l’intérieur lorsqu’elles sont ouvertes et le rendent au contrôle déclencheur à la fermeture. Les menus d’actions reçoivent le focus à l’ouverture et le rendent lorsqu’on les ferme avec Échap.

Avec un clavier physique, utilisez **Tab** pour parcourir les contrôles, **Entrée** ou **Espace** pour activer les boutons et **Échap** pour fermer les menus d’actions. Vous pouvez aussi utiliser les gestes habituels de navigation et d’activation de votre lecteur d’écran.

## <a name="screen-reader-limitations"></a>Limites actuelles

- L’édition accessible dépend du signalement de l’activation du lecteur d’écran par l’application mobile. Le navigateur et l’éditeur intégré n’activent pas automatiquement ce mode.
- La prise en charge couvre actuellement les tâches principales ci-dessus. Les interactions avancées et les autres fonctions de l’application peuvent se comporter différemment selon le lecteur d’écran.
- Le comportement peut varier selon la version de l’application, le système et l’appareil. Signalez les contrôles inaccessibles ou impossibles à activer, les changements de focus inattendus et les difficultés de lecture ou d’édition.

Consultez les [raccourcis clavier](./editor#keyboard-shortcuts) pour les commandes d’édition et la [prise en charge et les limites de Git](./git-support#git-limitations) pour les différences entre Git sur mobile, dans le navigateur et à distance.

## <a name="screen-reader-feedback"></a>Commentaires

Veuillez [envoyer vos commentaires à support@spck.io](mailto:support@spck.io) si un contrôle n’a pas de nom, si le focus est perdu ou si la lecture ou l’édition ne fonctionne pas comme prévu. Indiquez la version de Spck, l’appareil et le système d’exploitation, le nom du lecteur d’écran et les étapes permettant de reproduire le problème.
