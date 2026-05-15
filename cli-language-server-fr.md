# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>Vue d'ensemble

La Spck CLI inclut un pont Language Server Protocol (LSP) complet qui exécute des serveurs de langage pour TypeScript, JavaScript, Python, HTML, CSS et SCSS directement sur votre hôte distant. Lorsqu'il est connecté à une session CLI, Spck Editor utilise automatiquement le serveur de langage distant plutôt que celui intégré à l'application mobile.

> 💡 **Conseil** : Pour une description du serveur de langage intégré disponible sans la CLI, consultez [Editor Language Server](./editor-language-server).

## <a name="cli-ls-architecture"></a>Architecture

Le serveur de langage de la CLI s'exécute sur la même machine que les fichiers de votre projet. Cela présente plusieurs avantages significatifs par rapport à l'approche dans le navigateur utilisée sur mobile :

### Aucune transmission de fichiers

Avec le serveur de langage mobile intégré, les fichiers doivent être transmis à l'appareil et chargés dans un worker du navigateur avant que le serveur puisse les analyser. Avec la CLI, le serveur de langage lit les fichiers directement depuis le disque — aucune transmission n'est nécessaire. Cela élimine la consommation de bande passante et maintient l'analyse rapide, même dans les grands projets.

### Connaissance complète du projet

Le serveur de langage de la CLI a accès à l'intégralité du répertoire de votre projet, notamment :

- Tous les fichiers sources dans chaque sous-répertoire
- `node_modules/` pour la résolution des types tiers
- Les fichiers `tsconfig.json` découverts automatiquement à n'importe quel niveau
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` et les fichiers de déclaration associés

Cela signifie que « Aller à la définition », « Rechercher les références » et « Renommer le symbole » fonctionnent correctement entre les fichiers — même si vous ne les avez pas ouverts dans l'éditeur.

### Gestion correcte de `tsconfig.json`

Le serveur de langage TypeScript découvre et respecte automatiquement le `tsconfig.json` (ou `jsconfig.json`) de votre projet. Les alias de chemins (`paths`), les options du compilateur (`strict`, `target`, `lib`), les références de projet et les dispositions de workspace en monorepo sont tous gérés correctement. Le serveur de langage mobile intégré ne peut pas lire `tsconfig.json` car il n'a pas accès au système de fichiers au démarrage.

### Processus persistant

Le processus du serveur de langage reste actif pendant toute la durée de votre session CLI. Il construit un index en mémoire de votre projet et le maintient à jour entre les modifications, de sorte que les réponses restent rapides même après le démarrage initial.

## <a name="cli-ls-features"></a>Fonctionnalités prises en charge

| Fonctionnalité | Description |
| --- | --- |
| **Complétion de code** | Suggestions contextuelles avec signatures de types, triées par pertinence |
| **Info au survol** | Informations de type et documentation JSDoc pour le symbole sous le curseur |
| **Aide à la signature** | Indications de paramètres et documentation lors de la saisie d'un appel de fonction |
| **Aller à la définition** | Accéder à la déclaration de n'importe quel symbole, y compris ceux dans `node_modules` |
| **Rechercher les références** | Lister chaque utilisation d'un symbole dans l'ensemble du projet |
| **Renommer le symbole** | Renommer un symbole et mettre à jour toutes les références de manière atomique |
| **Diagnostics** | Mise en évidence des erreurs et avertissements en temps réel lors de la saisie |
| **Rendu Markdown** | Documentation de survol et de signature rendue en Markdown avec blocs de code colorisés |

## <a name="cli-ls-languages"></a>Langages pris en charge

| Langage | Complétion | Survol | Signatures | Diagnostics |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>Configuration

La prise en charge du serveur de langage est activée par défaut. Vous pouvez la contrôler dans votre fichier de configuration :

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

- **`languageServer.enabled`** (boolean) : Interrupteur principal pour tous les serveurs de langage distants. Par défaut : `true`.
- **`languageServer.typescript.enabled`** (boolean) : Activer le serveur de langage TypeScript/JavaScript. Par défaut : `true`.
- **`languageServer.python.enabled`** (boolean) : Activer le serveur de langage Python (nécessite `pylsp` dans le `PATH`). Par défaut : `true`.

## <a name="cli-ls-requirements"></a>Prérequis

- **TypeScript / JavaScript** : Inclus avec la CLI. Aucune installation supplémentaire requise.
- **Python** : Nécessite [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) (`pip install python-lsp-server`).
- **HTML / CSS / SCSS** : Inclus avec la CLI. Aucune installation supplémentaire requise.

## <a name="cli-ls-vs-mobile"></a>CLI vs. serveur de langage mobile

| Capacité | CLI Language Server | Intégré mobile |
| --- | --- | --- |
| Accès complet aux fichiers du projet | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| Résolution des types `node_modules` | ✓ | — |
| Aller à la définition inter-fichiers | ✓ | Limité |
| Rechercher les références inter-fichiers | ✓ | — |
| Renommer le symbole | ✓ | — |
| Prise en charge de Python | ✓ | — |
| Fonctionne hors ligne (sans CLI) | — | ✓ |

&nbsp;

&nbsp;
