# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Presentation

Spck Editor Lite est une version a achat unique de Spck Editor qui deverrouille les fonctionnalites d\u2019edition premium sans abonnement. L\u2019application est disponible separement sur Android et iOS.

Lite inclut tout ce que contient la version gratuite, plus :

- **Predictive Keyboard** -- suggestions de symboles contextuelles sur le clavier supplementaire
- **Snippets personnalises** -- modeles de code definis par l\u2019utilisateur avec des marqueurs de tabulation
- **Theme Neon** -- un theme d\u2019editeur exclusif
- **Intégration Git avancée** — Gestion des pull requests ; Modifications et diffs des commits

Ces fonctionnalites sont egalement disponibles dans la version complete de Spck Editor avec un abonnement Gold ou Supporter actif. L\u2019application Lite offre les memes fonctionnalites en un seul achat.

Pour le focus clavier, l’activation des menus et l’édition accessible, consultez [Prise en charge des lecteurs d’écran (expérimental)](./screen-reader-support).

## <a name="remote-projects"></a>Projets distants

Lite permet de modifier des projets sur votre ordinateur ou une VM publique via Spck CLI. Les projets distants nécessitent un **compte Spck et un abonnement Spck actif**, en plus de l’achat unique de Lite. L’abonnement contribue aux frais récurrents d’hébergement, d’exploitation et de maintenance des serveurs Spck. Les outils locaux d’édition et Git inclus restent accessibles sans abonnement.

[Spck CLI](./cli-start) · [Spck](https://spck.io/pricing)

## <a name="predictive-keyboard"></a>Predictive Keyboard

Le Predictive Keyboard remplace le clavier supplementaire standard par une rangee de touches de symboles contextuelles. Au lieu d\u2019appuyer longuement sur une touche pour choisir dans un menu, les symboles les plus probables s\u2019affichent directement en fonction de la position du curseur dans le fichier.

### Fonctionnement

Les predictions sont generees a partir de tables de frequences statistiques construites par langage. Lorsque le curseur se deplace, le clavier reordonne les symboles en fonction de la frequence d\u2019apparition de chacun a ce type de position dans du code reel. Les langages pris en charge incluent JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown et le texte brut.

### Activer ou desactiver

Allez dans `Settings > Touch > Predictive Keyboard` pour activer ou desactiver la fonctionnalite. Dans Lite, le Predictive Keyboard est active par defaut. Le desactiver restaure le clavier supplementaire standard.

> Le Predictive Keyboard n\u2019est disponible que sur les appareils tactiles. Il n\u2019apparait pas lors de l\u2019utilisation d\u2019un clavier physique ou en mode tablette avec un clavier externe connecte.

## <a name="custom-snippets"></a>Snippets personnalises

Les snippets personnalises vous permettent de creer des modeles de code reutilisables qui apparaissent dans la liste d\u2019auto-completion lors de la saisie. Chaque snippet est associe a un langage specifique afin que vos snippets JavaScript n\u2019encombrent pas les fichiers Python.

### Creer un snippet

1. Ouvrez `Settings > Editor > Custom Snippets`
2. Selectionnez le langage (par ex. JavaScript, Python, HTML)
3. Appuyez sur **Ajouter un snippet**
4. Saisissez un **declencheur** -- l\u2019abreviation que vous tapez pour invoquer le snippet
5. Saisissez le **corps** -- le code qui sera insere

### Tabulations et marqueurs

Les snippets prennent en charge les tabulations pour que le curseur saute entre les positions editables apres l\u2019insertion :

- `$1`, `$2`, `$3` -- tabulations numerotees dans l\u2019ordre de parcours
- `$0` -- position finale du curseur apres toutes les tabulations
- `${1:defaultText}` -- une tabulation avec un texte de marqueur preselectionne pour un remplacement facile

Exemple -- un snippet de boucle `for` en JavaScript :

**Declencheur :** `forloop`

**Corps :**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

En tapant `forloop` et en le selectionnant dans l\u2019auto-completion, la boucle complete est inseree. Appuyez sur Tab pour naviguer entre `i`, `array` et le corps de la boucle.

### Importer et exporter

Vous pouvez exporter tous les snippets dans un fichier et les importer sur un autre appareil. C\u2019est pratique pour partager des collections de snippets entre telephones ou sauvegarder votre configuration.

## <a name="neon-theme"></a>Theme Neon

Lite inclut le theme d\u2019editeur **Neon**, un theme sombre avec des couleurs d\u2019accentuation vives. Il est defini comme theme par defaut dans Lite et peut etre modifie a tout moment dans `Settings > Appearance > Theme`.

## <a name="enhanced-git-integration"></a>Intégration Git avancée

### Gestion des pull requests (Premium)

Lite inclut les mêmes outils Premium de pull requests que l’application complète, sans abonnement. Consultez la [gestion des pull requests](./git-support#pull-request-management) pour créer des demandes, parcourir les demandes ouvertes, examiner les diffs et fusionner ou fermer les demandes selon les règles du fournisseur.

Enregistrez le jeton dans **Git menu → Git Credentials**. Utilisez **Git menu → Create PR** pour créer une demande et **Git menu → Pull Requests** pour gérer les demandes. La rédaction facultative par IA nécessite un service d’IA configuré et ne constitue pas une allocation de crédits IA incluse avec Lite.

### Modifications et diffs des commits

Ouvrez l’onglet **History** du panneau Git et sélectionnez un commit pour voir les fichiers ajoutés, modifiés et supprimés. Sélectionnez un fichier pour ouvrir un diff en lecture seule par rapport au premier parent du commit. Pour le premier commit, les fichiers sont comparés à un arbre vide. Le visualiseur utilise les versions commitées ; les modifications non commitées n’affectent pas le diff. Les fichiers binaires ne peuvent pas être affichés comme diffs textuels.

Vous pouvez aussi appuyer longuement sur une entrée de l’historique, ou faire un clic droit, puis choisir **View Commit**.

L’intégration Git avancée est incluse avec :

- **Spck Editor Lite :** déverrouillée définitivement par l’achat unique de l’application, sans connexion requise.
- **Achat à vie du terminal Spck for NodeJS :** déverrouillée définitivement pour le compte propriétaire de l’achat ; connexion requise.
- **Abonnements Supporter, Gold ou Node :** déverrouillée tant que l’abonnement est actif ; connexion requise.

Consultez [Prise en charge de Git](./git-support) pour la [configuration des jetons](./git-support#git-credentials), la [gestion des pull requests](./git-support#pull-request-management) et l’[intégration Git avancée](./git-support#enhanced-git-integration).

## <a name="comparison"></a>Comparaison des fonctionnalites

| Fonctionnalite | Gratuit | Lite (Achat unique) | Complet (Abonnement) |
| --- | :---: | :---: | :---: |
| Edition de code et coloration syntaxique | Oui | Oui | Oui |
| Integration Git | Oui | Oui | Oui |
| Intégration Git avancée | -- | Oui | Supporter / Gold / Node |
| Clavier supplementaire | Oui | Oui | Oui |
| Clavier tactile et curseurs | Oui | Oui | Oui |
| Apercu du projet | Oui | Oui | Oui |
| Predictive Keyboard | -- | Oui | Gold / Supporter |
| Snippets personnalises | -- | Oui | Gold |
| Theme Neon | -- | Oui | -- |
| Assistant IA | -- | -- | Oui |
| Synchronisation cloud | -- | -- | Oui |
| Labs / Projets communautaires | -- | -- | Oui |
