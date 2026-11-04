# <a name="git-support"></a>Prise en charge de Git

Spck prend en charge Git pour les projets locaux sur Android et iOS, dans le navigateur et pour les projets distants via Spck CLI. Ce guide couvre les identifiants des fournisseurs, les pull requests, l’inspection des commits, la résolution des conflits et les limites des plateformes.

L’intégration Git de base, l’historique des commits et la résolution des conflits sont disponibles dans la version gratuite. L’[intégration Git avancée](#enhanced-git-integration) ajoute la gestion des pull requests et les diffs de fichiers des commits.

## <a name="git-credentials"></a>Identifiants Git et pull requests

Ouvrez **Git menu → Git Credentials**, choisissez votre fournisseur et enregistrez son jeton d’accès. Les liens de création et d’aide ci-dessous s’ouvrent dans un nouvel onglet pour vous permettre de revenir dans Spck et de coller le jeton.

| Fournisseur | Création du jeton | Autorisations pour Git et les pull requests |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">Créer un jeton GitHub</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Guide de configuration</a> | Sélectionnez le dépôt. Le lien présélectionne **Contents: Read and write**, **Pull requests: Read and write** et **Metadata: Read**. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">Créer un jeton GitLab</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Guide de configuration</a> | Le lien présélectionne la portée `api` pour les merge requests. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">Créer un jeton API</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Guide de configuration</a> | Choisissez **Create API token with scopes**, sélectionnez **Bitbucket**, puis cochez manuellement `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket` et `write:pullrequest:bitbucket`. L’API utilise l’adresse e-mail du compte Atlassian. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">Guide de création d’un PAT</a> | Ouvrez **User settings → Personal access tokens → New Token** dans votre organisation, sélectionnez celle-ci et cochez manuellement **Code (Read & write)**. |

Pour créer une pull request, commitez et poussez la branche source, puis ouvrez **Git menu → Create PR**. Sélectionnez le remote et les identifiants, choisissez une branche cible différente et saisissez un titre et une description. **Generate with AI** peut préparer le message à partir des modifications commitées depuis l’ancêtre commun des branches ; récupérez d’abord la branche cible. Relisez le brouillon avant de choisir **Create PR**. GitLab crée une merge request.

La création et la gestion des pull requests sont une **fonction Premium**, incluse dans l’[intégration Git avancée](#enhanced-git-integration). Lite les inclut avec l’achat unique de l’application. Dans l’application complète, connectez-vous avec un abonnement Supporter, Gold ou Node actif, ou avec le compte possédant le déverrouillage à vie du terminal Spck for NodeJS.

## <a name="pull-request-management"></a>Gestion des pull requests (Premium)

Gérez les pull requests sans quitter l’éditeur. Les remotes pris en charge sont **GitHub.com, GitLab.com, Bitbucket Cloud et Azure DevOps** ; GitLab les appelle merge requests.

1. Ouvrez un projet Git et ajoutez le jeton du fournisseur dans **Git menu → Git Credentials**, avec les autorisations ci-dessus.
2. Ouvrez **Branches menu → Pull Requests**, puis choisissez le remote et les identifiants pour afficher les demandes ouvertes.
3. Sélectionnez une demande pour voir son titre, sa description, son auteur, les branches source et cible et son état.
4. Sélectionnez un fichier modifié pour examiner son diff en lecture seule avant la fusion.
5. Utilisez **Merge** pour fusionner une demande admissible ou **Close** pour la fermer sans fusion. Les revues, vérifications, autorisations du jeton et règles de branche restent applicables ; les brouillons et les demandes avec conflits ne peuvent pas être fusionnés depuis cette boîte de dialogue.

Utilisez **Refresh** pour actualiser la liste après des changements chez le fournisseur. Les détails de la demande proposent aussi un lien vers le fournisseur pour les revues, vérifications et autres actions.

Pour créer une demande, utilisez **Git menu → Create PR** comme indiqué ci-dessus. Si la branche source doit être poussée, la boîte de dialogue propose **Push** avant la création. La rédaction facultative par IA utilise le service d’IA configuré et ses limites d’utilisation ; elle est distincte de l’accès aux pull requests inclus avec Lite.

Si la création échoue à cause des autorisations du jeton, utilisez le lien du fournisseur pour créer ou actualiser le jeton, enregistrez-le dans **Git Credentials** et réessayez. Le brouillon de la pull request est conservé.

## <a name="enhanced-git-integration"></a>Intégration Git avancée

L’intégration Git avancée ajoute deux outils pour examiner et partager les modifications :

- **Gestion des pull requests :** créer des demandes, parcourir les demandes ouvertes, examiner les fichiers et les diffs, puis fusionner ou fermer les demandes. Consultez la [gestion des pull requests](#pull-request-management) pour la configuration et les étapes.
- **Inspection des commits :** parcourir les fichiers modifiés d’un commit et leurs diffs sans modifier les fichiers de travail.

Ouvrez l’onglet **History** du panneau Git et sélectionnez un commit pour voir les fichiers ajoutés, modifiés et supprimés. Sélectionnez un fichier pour ouvrir un diff en lecture seule par rapport au premier parent du commit. Pour le premier commit, les fichiers sont comparés à un arbre vide. Le visualiseur utilise les versions commitées ; les modifications non commitées n’affectent pas le diff. Les fichiers binaires ne peuvent pas être affichés comme diffs textuels.

Vous pouvez aussi appuyer longuement sur une entrée de l’historique, ou faire un clic droit, puis choisir **View Commit**.

L’intégration Git avancée est incluse avec :

- **Spck Editor Lite :** déverrouillée définitivement par l’achat unique de l’application, sans connexion requise.
- **Achat à vie du terminal Spck for NodeJS :** déverrouillée définitivement pour le compte propriétaire de l’achat ; connexion requise.
- **Abonnements Supporter, Gold ou Node :** déverrouillée tant que l’abonnement est actif ; connexion requise.

L’intégration Git de base et la consultation de l’historique restent disponibles dans la version gratuite. Consultez les [tarifs](https://spck.io/pricing) pour les détails des offres.

## <a name="merge-conflict-resolution"></a>Résoudre les conflits de fusion

Le visualiseur de diffs aide aussi à résoudre les conflits dans les fichiers de travail. Cette fonction fait partie de l’intégration Git de base et ne nécessite pas Premium.

1. Ouvrez un fichier en conflit depuis la liste des modifications Git.
2. Pour chaque conflit, choisissez **Accept Current**, **Accept Incoming** ou **Accept Both**. Vous pouvez aussi modifier le fichier pour combiner les changements manuellement.
3. Vérifiez le résultat. Une fois tous les marqueurs de conflit supprimés, choisissez **Resolve** dans le visualiseur pour indexer le fichier résolu.
4. Résolvez les autres fichiers, puis commitez la fusion.

Sur les appareils tactiles, appuyez longuement sur les fichiers ou les entrées Git pour ouvrir leur menu contextuel. Les lettres d’état Git complètent les couleurs des noms de fichiers pour mieux distinguer les modifications.

## <a name="git-limitations"></a>Limites de Git

### <a name="git-limitations-overview"></a>Vue d’ensemble

L’implémentation de Git dépend de l’emplacement du projet et de la version de Spck utilisée :

| Environnement | Implémentation de Git | Principales contraintes |
| --- | --- | --- |
| Applications Android et iOS, y compris Lite et Spck for NodeJS | **libgit2** compilée nativement pour les projets locaux | Projet stocké sur l’appareil requis ; ressources et restrictions du système de fichiers de l’appareil toujours applicables. |
| Navigateur et éditeur intégré | [isomorphic-git](https://isomorphic-git.org/), exécuté en JavaScript | Limites de mémoire, de stockage et de réseau du navigateur. |
| Projets distants via Spck CLI | **Binaire Git** de l’ordinateur hôte | Utilise les ressources, le système de fichiers, les identifiants et l’installation Git de l’hôte. |

Les versions mobiles actuelles utilisent Git natif au lieu du moteur Git du navigateur. Si une opération locale affiche **Native Git requires a device folder**, déplacez le projet vers le stockage de l’appareil. Les projets conservés uniquement dans la base de données du navigateur de l’éditeur ne peuvent pas utiliser le client Git natif mobile.

La gestion des pull requests appelle directement l’API du fournisseur avec le jeton enregistré dans **Git Credentials**. Les cookies de connexion du navigateur ne sont pas utilisés et les réponses de l’API ne sont pas mises en cache, pour qu’une actualisation récupère l’état et les branches les plus récents. Consultez les [identifiants Git et pull requests](#git-credentials) pour les autorisations et la [gestion des pull requests](#pull-request-management) pour les fournisseurs et actions pris en charge.

### <a name="git-limitations-memory"></a>Contraintes mémoire

- Git natif sur Android et iOS effectue les opérations en dehors du moteur Git JavaScript. Les contraintes de ce moteur ne constituent pas une limite fixe de Git mobile.
- Git natif nécessite toujours de la mémoire et de l’espace disque disponibles. Les gros dépôts ou fichiers pack peuvent dépasser les ressources de l’appareil et provoquer un échec ou l’arrêt de l’application par le système.
- Git dans le navigateur reste soumis aux limites de mémoire JavaScript et de stockage du navigateur. Les gros fichiers pack peuvent demander beaucoup de mémoire et faire échouer un clonage ou une récupération.

> 💡 **Astuce :** Pour les gros dépôts, utilisez si possible des clones superficiels ou travaillez avec une plus petite partie du dépôt.

### <a name="git-limitations-symlinks"></a>Compatibilité des liens symboliques

- Le stockage du navigateur et la couche de système de fichiers de l’appareil utilisent des **liens symboliques émulés** pour les dépôts contenant des liens symboliques.
- Le passage à libgit2 sur mobile ne supprime pas les restrictions du système de fichiers et ne garantit pas de vrais liens symboliques du système.
- Les liens émulés peuvent se comporter différemment avec les outils de compilation, gestionnaires de paquets ou scripts qui attendent de vrais liens et résolvent leurs cibles à l’exécution.
- Pour les projets nécessitant de vrais liens symboliques, utilisez un projet distant sur un hôte dont le système de fichiers et les autorisations les prennent en charge.

### <a name="git-limitations-cli"></a>Utiliser la CLI comme alternative

Pour les gros dépôts ou les tâches nécessitant les outils Git et le système de fichiers de l’hôte, utilisez un **projet distant via Spck CLI**. Les opérations Git s’exécutent alors avec le **binaire Git de l’hôte**, pendant que vous modifiez les fichiers depuis Spck :

- Les opérations utilisent la mémoire et le disque de l’hôte plutôt que les ressources du mobile ou du navigateur.
- Les liens symboliques suivent les capacités et les autorisations du système de fichiers de l’hôte.
- Utilisez les outils Git de l’hôte pour les commandes absentes des contrôles Git de l’éditeur.

Consultez [Premiers pas avec Spck CLI](./cli-start) pour connecter un hôte. Les projets distants nécessitent un compte Spck et restent soumis aux limites de votre offre ; consultez [Projets distants](./editor-lite#remote-projects) pour l’abonnement requis par Lite. Cloner un dépôt sur l’appareil utilise toujours le client Git natif de l’application mobile.

## <a name="git-related-guides"></a>Guides associés

- [Prise en charge des lecteurs d’écran (expérimental)](./screen-reader-support) : navigation accessible, contrôles de gestion de versions et commentaires.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration) : outils Git inclus dans l’achat unique de l’application.
- [Premiers pas avec Spck CLI](./cli-start) : connecter un projet distant pour utiliser les outils Git de l’hôte.
