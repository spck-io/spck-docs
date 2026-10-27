# <a name="getting-started"></a>Premiers pas

## <a name="getting-started-overview"></a>Vue d'ensemble

Spck Editor est une solution d'édition de code mobile avec plusieurs variantes conçues pour les développeurs.

### Versions

#### Spck Editor (Gratuit)

- Fonctionnalité de base d'édition de code mobile
- Intégration Git native sur Android et iOS ; Git dans le navigateur via isomorphic-git

#### Spck Editor Lite

**Prix** : Paiement unique
**Fonctionnalités** :

- Snippets personnalisés
- Clavier prédictif
- Thème Neon exclusif
- Intégration Git avancée

#### Spck pour NodeJS

**Plateforme** : Exclusivité Android
**Fonctionnalité clé** : Terminal intégré avec prise en charge NodeJS

L’intégration Git avancée est incluse avec un abonnement Node actif ou débloquée définitivement avec l’achat à vie du terminal. Les deux options nécessitent une connexion.

#### Version navigateur

- Intégrable sur n'importe quel site web
- Interface d'édition de code légère

[Intégrer l’éditeur](./editor-embed)

### Caractéristiques clés

- Conception mobile-first
- [Prise en charge et limites de Git](./git-support)
- Compatibilité multiplateforme
- [Prise en charge des lecteurs d’écran (expérimental)](./screen-reader-support)

### <a name="git-credentials"></a>Identifiants Git et pull requests

<a name="pull-request-management"></a>

Consultez [Prise en charge de Git](./git-support) pour la [configuration des jetons](./git-support#git-credentials), la [gestion des pull requests](./git-support#pull-request-management) et l’[intégration Git avancée](./git-support#enhanced-git-integration).

### Utilisation recommandée

- Édition de code en déplacement
- Modifications rapides de projet
- Apprentissage et prototypage

## <a name="getting-started-terminology"></a>Terminologie

| Terme              | Description                                                                                                                              |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Menu de navigation | Désigne le premier onglet du menu latéral sur les appareils mobiles ; ce menu n'est pas disponible dans la version navigateur ou en mode Tablette |
| Menu Fichiers      | Désigne l'onglet _Fichier_ dans le menu latéral ou la barre latérale                                                                     |
| Clavier additionnel | Sur les appareils mobiles, il existe un clavier supplémentaire avec des symboles de codage couramment utilisés pour une insertion rapide |
| Clavier tactile    | Désigne généralement la rangée de touches contenant les flèches directionnelles, la touche tab et d'autres                                |
| Barre d'action tactile | Il s'agit du menu flottant qui apparaît au-dessus du curseur lorsqu'un texte est sélectionné sur un appareil mobile/tactile          |
| Curseurs tactiles  | Les curseurs à l'écran qui apparaissent sur un appareil mobile/tactile lorsqu'un texte est sélectionné ou que le curseur est actif       |
| Mode Tablette      | Désigne un paramètre qui peut être activé sur les appareils tactiles plus grands comme une tablette                                       |
| Touche ⌘           | Ce symbole sur le clavier tactile équivaut à la touche Ctrl sous Windows ou à la touche Command sur Mac                                  |
| Touche ⌥           | Ce symbole sur le clavier tactile équivaut à la touche Alt sous Windows ou à la touche Option sur Mac                                    |

&nbsp;

&nbsp;

# <a name="screen-reader-support"></a>Prise en charge des lecteurs d’écran (expérimental)

La prise en charge des lecteurs d’écran est **expérimentale**. Consultez le [guide des lecteurs d’écran](./screen-reader-support) pour l’activation, l’édition, la navigation au clavier, les limites et les [commentaires](./screen-reader-support#screen-reader-feedback).

&nbsp;

&nbsp;

# <a name="keyboard-shortcuts"></a>Raccourcis clavier

## <a name="keyboard-shortcuts-overview"></a>Vue d'ensemble

Débloquez une efficacité ultra-rapide avec ces raccourcis clavier pratiques ! Bien qu'il ne s'agisse pas d'un catalogue complet, ces petites perles boosteront votre productivité et faciliteront votre navigation.

### Points clés

- **Non exhaustif** : Une sélection soignée des raccourcis les plus pratiques
- **Objectif** : Stimuler votre flux de travail avec des commandes rapides et intuitives
- **Avantage** : Gagner du temps et réduire la dépendance à la souris

> 💡 **Astuce de pro** : Mémorisez ces raccourcis et regardez votre productivité s'envoler ! 🌟

Vous pouvez consulter la liste complète des raccourcis en allant dans `Settings > Editor > Keyboard Shortcuts`

> Les utilisateurs premium peuvent également accéder aux raccourcis clavier directement depuis le clavier additionnel ou en utilisant le raccourci `⌘ K`

> Activez la touche Ctrl/Command (⌘) et la touche Alt/Option en activant `Settings > Touch > Show ⌘ Key` et `Settings > Touch > Show ⌥ Key`

Pour le focus clavier, l’activation des menus et l’édition accessible, consultez [Prise en charge des lecteurs d’écran (expérimental)](./screen-reader-support).

## <a name="keyboard-shortcuts-editor"></a>Éditeur

| Raccourci | Action                                                  |
| --------- | ------------------------------------------------------- |
| ⌘ A       | Tout sélectionner                                       |
| ⌘ C       | Copier                                                  |
| ⌘ V       | Coller                                                  |
| ⌘ X       | Couper                                                  |
| ⌘ Z       | Annuler                                                 |
| ⌘ ⇧ Z     | Rétablir                                                |
| ⌘ D       | Dupliquer la ligne                                      |
| ⌘ /       | Commenter/Décommenter la ligne                          |
| ⌥ F       | Formater le code                                        |
| ⌘ F       | Rechercher                                              |
| ⌘ G       | Rechercher suivant (fonctionne avec le texte sélectionné) |
| ⌘ ⇧ G     | Rechercher précédent                                    |
| ⌘ L       | Aller à la ligne                                        |

## <a name="keyboard-shortcuts-quick-actions"></a>Actions rapides

| Raccourci | Action                                              |
| --------- | --------------------------------------------------- |
| ⌘ ⇧ C     | Git Commit                                          |
| ⌘ O       | Ouvrir les fichiers récents                         |
| ⌘ ⇧ P     | Lancer l'aperçu du projet                           |
| ⌘ P       | Basculer l'aperçu de fichier (SVG, Markdown)        |
| ⌘ K       | **Supporter+** : Ouvrir les raccourcis              |

&nbsp;

&nbsp;

# <a name="touch-settings"></a>Paramètres tactiles

## <a name="touch-settings-extra"></a>Clavier additionnel

- Le clavier additionnel est un clavier de symboles conçu pour les appareils tactiles.
- Des touches/symboles supplémentaires sont accessibles en maintenant les touches appuyées, ce qui ouvre un menu d'options.
- Vous pouvez l'activer ou le désactiver dans le menu `Settings > Touch > Extra Keyboard`.

> 💡 **Astuce de pro** : Consultez _**Édition avancée**_ pour des conseils sur l'entourage de texte, compatible avec le clavier additionnel.

## <a name="touch-settings-touch"></a>Clavier tactile

- Les touches tactiles consistent en une rangée de touches comprenant les flèches directionnelles, la touche Command et d'autres touches fréquemment utilisées.
- Cette fonctionnalité est disponible sur les appareils tactiles.
- Vous pouvez l'activer ou la désactiver dans la section `Settings > Touch > Touch Keyboard`.

> 💡 **Astuce de pro** : Vous pouvez personnaliser les touches individuelles de ce clavier en ajustant les paramètres.

## <a name="touch-settings-action-bar"></a>Barre d'action tactile

- Une barre d'action apparaîtra avec les options Copier, Couper et Coller lorsqu'un texte est sélectionné.
- Cette fonctionnalité peut être activée ou désactivée dans `Settings > Touch > Touch Action Bar`.

## <a name="touch-settings-cursors"></a>Curseurs tactiles

- Curseurs à l'écran qui apparaissent lorsqu'un texte est sélectionné ou que le curseur est actif.
- Cette fonctionnalité peut être activée ou désactivée dans `Settings > Touch > Touch Cursors`.

> 💡 **Astuce de pro** : Il n'est pas recommandé de désactiver cette fonctionnalité à moins que vous n'ayez une souris/un dispositif de pointage couplé à l'appareil mobile. Désactiver les curseurs tactiles peut améliorer la visibilité de l'écran lors de l'édition et améliorer l'expérience d'édition lors de l'utilisation de dispositifs de pointage externes.

## <a name="touch-settings-predictive"></a>Touches prédictives

- Les touches prédictives sont une fonctionnalité premium qui remplace le clavier additionnel standard.
- Offre une saisie de symboles en un seul toucher plutôt que de devoir maintenir appuyé et sélectionner dans le clavier additionnel classique.
- Les touches sont classées selon la fréquence statistique des symboles apparaissant à une position spécifique dans le fichier.
- Elle peut être activée ou désactivée dans `Settings > Touch > Predictive Keyboard`.

> 💡 **Astuce de pro** : Les touches prédictives remplacent le clavier additionnel classique que certains utilisateurs peuvent préférer. Les touches prédictives sont une option par défaut dans la version **Lite** de l'éditeur, et peuvent être désactivées pour récupérer le clavier additionnel classique.

&nbsp;

&nbsp;

# <a name="file-navigation"></a>Navigation dans les fichiers

## <a name="file-navigation-overview"></a>Vue d'ensemble

- Il existe plusieurs méthodes pour naviguer entre les fichiers
- Vous pouvez naviguer dans les fichiers en utilisant les Fichiers dans le menu latéral
- Vous pouvez utiliser le fil d'Ariane pour naviguer dans les fichiers à partir du répertoire du fichier actuel
- Vous pouvez ouvrir les fichiers récents avec `Ctrl-O` pour rechercher rapidement des fichiers
- Vous pouvez utiliser l'icône « Localiser » dans le menu latéral Fichiers pour repérer rapidement les fichiers actuels
- Les menus latéraux Contrôle de source et Recherche offrent également des moyens uniques de naviguer entre les fichiers

## <a name="file-navigation-tabs"></a>Gestion des onglets de fichiers

### Comportement des onglets

- Les fichiers sont automatiquement détachés (non épinglés) lors de leur première ouverture
- Les onglets sont épinglés lorsque des modifications sont apportées

### Options de tri des onglets

Les fichiers peuvent être triés par :

- Ordre alphabétique
- Extension de fichier
- Chemin du fichier

### Canaux de navigation alternatifs

- **Menu Contrôle de source** : Naviguer dans les fichiers via le contexte du contrôle de version
- **Menu Recherche** : Trouver et accéder aux fichiers selon les critères de recherche

> 💡 **Astuce de pro** : Les onglets de fichiers peuvent être masqués dans `Settings > Appearance > Show File Tabs`. Consultez le _Mode Zen_ pour maximiser l'espace d'écran sur les petits appareils.

&nbsp;

&nbsp;

# <a name="advanced-editing"></a>Édition avancée

## Utiliser efficacement le clavier prédictif

### Sélection de base

- Double-tapez pour sélectionner un mot ou un bloc de texte

### Entourer du texte

Entourez rapidement le texte sélectionné en utilisant des paires de parenthèses ou de guillemets :

- Parenthèses : `( )`
- Crochets : `[ ]`
- Accolades : `{ }`
- Guillemets simples : `' '`
- Guillemets doubles : `" "`

### Navigation et édition

#### Recherche de texte

- `⌘ G` : Trouver l'occurrence suivante
- `⌘ ⇧ G` : Trouver l'occurrence précédente

#### Indentation

- Sélectionnez un bloc de texte
- Appuyez sur Tab pour indenter

&nbsp;

## <a name="multiple-cursors"></a>Curseurs multiples

### Configuration rapide

- Activez les curseurs multiples avec la touche Alt/Option ! ✨
- Allez dans `Settings > Touch > Show ⌥ Key` pour l'activer

### Comment utiliser

1. Sélectionnez les touches ⌥ et ⌘
2. Cliquez pour placer les curseurs exactement où vous le souhaitez
3. Modifiez plusieurs lignes simultanément avec facilité ! 💻

> 💡 **Astuce de pro** : Édition multi-curseurs = transformation de code ultra-rapide ! ⚡️
> Il est également possible d'ajouter des curseurs multiples à l'aide des commandes de la palette de commandes `Add Cursor Above` et `Add Cursor Below` qui ajouteraient un curseur directement au-dessus ou en dessous de la position actuelle du curseur.

&nbsp;

&nbsp;

# <a name="enhanced-git-integration"></a>Prise en charge de Git

Consultez le [guide Git](./git-support) pour les identifiants des fournisseurs, les pull requests, l’inspection des commits et l’accès à l’intégration Git avancée.

<a name="merge-conflict-resolution"></a>

Git de base comprend la [résolution des conflits](./git-support#merge-conflict-resolution) dans le visualiseur de diffs avec **Accept Current**, **Accept Incoming**, **Accept Both** et **Resolve**.

## <a name="git-limitations"></a>Limites de Git

<a name="git-limitations-overview"></a>
<a name="git-limitations-memory"></a>
<a name="git-limitations-symlinks"></a>
<a name="git-limitations-cli"></a>

Android et iOS utilisent libgit2 natif pour les projets locaux ; le navigateur utilise isomorphic-git et les projets distants le binaire Git de l’hôte. Consultez les [limites de Git](./git-support#git-limitations) pour le stockage, la mémoire, les liens symboliques et les alternatives à distance.

&nbsp;

&nbsp;

# <a name="zen-mode"></a>🌟 Mode Zen

## Vue d'ensemble

Le mode Zen est une configuration d'éditeur agréable et optimisant l'espace, conçue pour transformer votre expérience de codage sur les écrans compacts.

Le mode Zen consiste à :

- Désactiver `Show Line Numbers` dans les paramètres
- Désactiver `Show File Tab`
- Désactiver `Touch Action Bar`

### Caractéristiques clés

#### 🧘‍♀️ Espace écran maximisé

- **Adieu les numéros de ligne !**
  - Libérez un précieux espace horizontal
  - Évitez que le texte ne soit à l'étroit
  - Adoptez l'aspect épuré et minimaliste

#### 🎨 Interface rationalisée

- **Minimisation de la barre d'action**
  - Dites adieu aux barres d'outils encombrées
  - Utilisez des méthodes d'entrée alternatives :
    - Boutons coller/couper du clavier additionnel
    - Raccourcis clavier (`Ctrl-C/Ctrl-V`)

#### 📂 Navigation simplifiée

- **Élimination des onglets de fichiers**
  - `Ctrl-O` devient votre nouveau meilleur allié de navigation
  - Espace de travail plus épuré
  - Changement de contexte plus rapide

> 💡 **Astuce de pro** : Le style de codage de chacun n'est pas le même ! Nous vous recommandons d'expérimenter avec le mode Zen pour voir s'il résonne avec votre flux de travail. Votre environnement de codage parfait n'est qu'à quelques basculements ! 🌈✨
