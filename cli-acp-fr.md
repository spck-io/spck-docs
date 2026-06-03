# <a name="ai-coding-agents-acp"></a>Agents de codage IA sur mobile (ACP)

Exécutez **Claude Code**, **OpenAI Codex** ou **Gemini CLI** directement depuis votre téléphone via l'**AI Chat** de Spck Editor. La Spck CLI relie votre éditeur aux CLI d'agents installés localement via l'[Agent Client Protocol (ACP)](https://agentclientprotocol.com/) ouvert, afin que le modèle s'exécute sur votre machine, avec votre abonnement, sur vos vrais fichiers — pendant que vous le supervisez depuis un appareil mobile.

![Mode IA locale ACP dans l'AI Chat de Spck Editor, pilotant Claude Code sur un bureau depuis un téléphone](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>Qu'est-ce qu'ACP et pourquoi l'utiliser ?

L'Agent Client Protocol (ACP) est une norme ouverte de Zed Industries pour la communication éditeur ↔ agent IA, dans le même esprit que le Language Server Protocol (LSP). Spck CLI 0.6.0+ implémente ACP et joue le rôle de **transport** entre l'AI Chat de Spck Editor (le client) et tout binaire d'agent compatible ACP que vous avez installé (l'agent).

Comparée à l'AI Chat routé via le serveur dans l'application, la voie ACP locale vous offre :

- **Votre propre abonnement** — les appels d'agent sont facturés à votre compte Claude Code / ChatGPT / Gemini, pas à votre quota IA Spck Editor.
- **Accès réel au système de fichiers** — les agents lisent et écrivent de vrais fichiers sur le disque via la CLI, et non les copies en mémoire de l'éditeur.
- **Outils natifs** — les observateurs de fichiers, les serveurs de langage et les commandes shell s'exécutent sur votre vraie machine.
- **Continuité avec le bureau** — le même login `claude` / `gemini` / `codex` que vous utilisez à votre bureau pilote le chat mobile.

## <a name="acp-supported-agents"></a>Agents IA pris en charge

Installez les agents que vous voulez avoir disponibles. Spck CLI les détecte automatiquement au démarrage.

| Agent             | Installation                                                                         |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>Installation et configuration

### 1. Installez Spck CLI

Si vous ne l'avez pas encore :

```bash
npm install -g spck
# ou exécutez-la sans installation
npx spck
```

Consultez [Démarrer avec Spck CLI](./cli-start) pour l'assistant complet de premier démarrage.

### 2. Installez un ou plusieurs CLI d'agent

Choisissez les agents que vous voulez avoir disponibles. Vous pouvez en installer plusieurs — l'AI Chat vous laissera choisir entre eux par session. Voir le tableau [Agents IA pris en charge](#acp-supported-agents) ci-dessus pour les commandes d'installation.

### 3. Authentifiez chaque agent une fois

Les CLI d'agent gèrent leur propre login en dehors de Spck Editor :

```bash
claude            # Flux de connexion Anthropic Claude Code
codex login       # Flux de connexion OpenAI Codex (utilisé par codex-acp)
gemini            # Flux de connexion Google Gemini
```

Si vous sautez cette étape, Spck Editor affichera une erreur du type `ACP agent requires authentication; run <binary> login and retry` au premier lancement d'un chat.

### 4. Démarrez Spck CLI

```bash
cd /path/to/your/project
spck
```

Au démarrage, la CLI affiche un rapport de détection par agent listant quels agents sont disponibles, suivi d'un résumé sur une ligne comme `✅ ACP agents: Claude Code, Gemini CLI` dans le bloc principal des fonctionnalités. Si rien n'est disponible, elle se replie sur l'AI Chat routé via le serveur.

### 5. Connectez Spck Editor

Scannez le QR code ou utilisez la [saisie manuelle](./cli-start#connecting). Une fois connecté, ouvrez l'**AI Chat** dans Spck Editor — le commutateur de transport affichera les agents locaux à côté de l'option cloud.

## <a name="acp-authentication"></a>Authentification

Chaque agent gère ses propres identifiants sur la machine où s'exécute Spck CLI. Exécutez le flux de connexion une fois par agent :

```bash
# Claude Code
claude

# Codex (codex-acp s'appuie sur le login propre de la CLI Codex)
codex login

# Gemini CLI
gemini
```

Si vous réinstallez ou changez de machine, répétez la connexion sur le nouvel hôte. L'authentification se fait **par hôte, par agent** — Spck Editor lui-même ne conserve jamais ces identifiants.

## <a name="acp-billing"></a>Facturation et limites d'utilisation

Étant donné qu'ACP exécute l'agent sur votre machine avec vos propres identifiants, **toute l'utilisation est facturée à votre compte auprès de ce fournisseur** — et non à votre abonnement Spck Editor. Spck Editor et les serveurs de relais Spck agissent comme un pur transport dans ce mode et ne consomment pas votre quota IA in-app pour le trafic ACP.

### Facturation Claude Code

> ⚠️ **Important — Claude Code applique un seau de limite d'utilisation distinct lorsqu'il est piloté par des outils tiers.**
>
> Lorsque Claude Code est invoqué depuis un client tiers via ACP, Anthropic compte ce trafic contre un **seau de limite d'utilisation différent** de vos sessions interactives de la CLI `claude` sur un abonnement Pro / Max. Conséquence pratique : vous pouvez épuiser le seau tiers tout en ayant encore de la marge interactive Claude Code (ou inversement), et vous ne pouvez pas les fusionner.
>
> Vérifiez `/usage` à l'intérieur de `claude` et la [Anthropic Console](https://platform.claude.com/usage) pour voir votre consommation actuelle, et consultez la [documentation des coûts et limites Claude Code](https://code.claude.com/docs/en/costs) pour les chiffres qui s'appliquent à votre forfait.

### Facturation Codex (codex-acp)

Facturé via l'auth propre de la CLI OpenAI Codex — votre clé API OpenAI ou login ChatGPT. L'utilisation compte contre le forfait de ce compte. Les tarifs et quotas sont les mêmes que pour l'usage interactif de `codex` ; voir [openai.com/codex](https://github.com/openai/codex) et votre tableau de bord OpenAI pour les chiffres actuels.

### Facturation Gemini CLI

Facturé via votre compte Google ou clé API Gemini. L'utilisation compte contre le forfait Gemini ou le quota API lié à ce login. Voir [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits) pour les détails des limites d'utilisation.

## <a name="acp-configuration"></a>Configuration

ACP est activé par défaut et configuré via le `spck-cli.config.json` du projet :

```json
{
  "acp": {
    "enabled": true
  }
}
```

Voir [Configuration → Paramètres ACP](./cli-config#acp-settings) pour le schéma complet.

### Désactiver ACP par projet

Si vous ne voulez pas que Spck Editor puisse piloter un agent local sur cet hôte :

```json
{
  "acp": {
    "enabled": false
  }
}
```

Lorsqu'il est désactivé, le commutateur de transport de l'éditeur masque l'option d'agent local et tout RPC `acp.*` est rejeté avec `FEATURE_DISABLED`. L'assistant de configuration pose cette question au premier lancement (défaut `Y`) ; les configurations antérieures à cette option sont chargées avec `acp.enabled: true` ajouté automatiquement et ré-enregistrées.

### Désactiver un seul agent

Pour empêcher qu'un agent _particulier_ soit proposé tout en gardant ACP activé pour les autres, désinstallez le binaire de cet agent. La détection s'exécute à chaque démarrage de la CLI, donc le commutateur de transport de l'éditeur le retirera de la liste.

## <a name="acp-vs-server-routed"></a>ACP local vs. AI Chat routé via le serveur

| Capacité                                | Routé via le serveur (par défaut, sans CLI) | Local (ACP, CLI connectée)                |
| --------------------------------------- | ------------------------------------------- | ----------------------------------------- |
| Où s'exécute le modèle                  | Cloud Spck                                  | Votre machine                             |
| Identifiants                            | Votre compte Spck Editor                    | Le login / la clé API propre de l'agent   |
| Accès aux fichiers                      | Système de fichiers en mémoire de l'éditeur | Vrais fichiers sur le disque via la racine de la CLI |
| Compte contre le quota IA Spck Editor   | Oui                                         | **Non** — facturé au fournisseur de l'agent |
| Fonctionne sans CLI en marche           | Oui                                         | Non (nécessite CLI + WebSocket)           |
| Agents disponibles                      | Modèles hébergés par Spck                   | Claude Code, Codex, Gemini CLI            |
| Invites de permission d'outil sur le téléphone | Le cas échéant                       | Oui, transmises via ACP                   |
| Streaming des tokens                    | Oui                                         | Oui                                       |
| Chat multi-tour                         | Oui                                         | Oui                                       |

Vous pouvez changer de transport en plein projet — l'AI Chat affiche les voies actuellement disponibles selon l'état de connexion de la CLI et les agents détectés.

## <a name="acp-tmux"></a>Associer à Tmux pour des sessions de longue durée

Les sessions ACP restent en vie à travers les reconnexions de l'éditeur, mais le processus Spck CLI lui-même se termine lorsque son terminal se ferme. Pour le travail d'agent de longue durée — gros refactorings, sessions de planification de plusieurs heures — démarrez la CLI dans une session [tmux](./tmux) afin qu'elle survive aux coupures SSH, fermetures de terminal et mises en veille de l'ordinateur portable :

```bash
tmux new -s spck
spck
# Ctrl+B puis D pour détacher
```

Vous pouvez également vous reconnecter depuis votre téléphone via le terminal Spck CLI et `tmux attach -t spck` pour suivre l'agent en direct. Voir [Utiliser Tmux](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile) pour le motif complet, y compris l'exécution de la CLI en tant que service d'arrière-plan persistant.

Pour les hôtes Linux, la page [Claude Skill : Linux Service](./claude-skill) propose une configuration en une seule commande pour exécuter Spck CLI comme service `systemd`, de sorte que la WebSocket — et toute session ACP au-dessus — démarre automatiquement au boot.

## <a name="acp-faq"></a>Foire aux questions

### Puis-je utiliser Claude Code sur mon téléphone ?

Oui. Installez Claude Code sur votre bureau, authentifiez-vous avec `claude`, puis exécutez `spck` dans votre projet. Connectez Spck Editor depuis votre téléphone et choisissez Claude Code dans le commutateur de transport de l'AI Chat. Le modèle s'exécute sur votre bureau avec votre abonnement ; vous le pilotez depuis votre téléphone.

### Spck Editor voit-il ma clé API Claude / OpenAI / Gemini ?

Non. Chaque CLI d'agent gère ses propres identifiants sur la machine où Spck CLI s'exécute. Les messages ACP sont tunnelisés via la WebSocket chiffrée entre le téléphone et la CLI, mais les jetons d'auth propres à l'agent ne quittent jamais votre hôte.

### Y a-t-il un coût supplémentaire pour utiliser Claude Code via Spck Editor ?

Pas de frais Spck Editor supplémentaires. L'utilisation de l'agent compte contre votre forfait Anthropic / OpenAI / Google exactement comme si vous exécutiez l'agent de façon interactive à votre bureau — sauf qu'Anthropic applique un seau de limite d'utilisation distinct pour les clients tiers ; voir [Facturation et limites d'utilisation](#acp-billing) ci-dessus.

### Ai-je besoin d'un abonnement Spck Editor payant pour utiliser ACP ?

Non. Le palier gratuit (30 min/jour de connexion CLI) suffit pour piloter n'importe quel agent ACP. Seul l'AI Chat routé via le serveur in-app consomme du quota IA Spck Editor.

### Que se passe-t-il si je perds ma connexion Wi-Fi en plein chat ?

Le processus de l'agent reste en vie sur l'hôte CLI. Lorsque l'éditeur se reconnecte, la session reprend avec l'historique complet du chat. La sortie en streaming arrivée pendant que vous étiez hors ligne est rejouée à la reconnexion.

### Puis-je exécuter les agents sur un serveur distant plutôt que sur mon portable ?

Oui. Exécutez Spck CLI sur n'importe quel hôte Linux/macOS accessible — une VM de développement, un serveur domestique, une station de travail — et connectez-vous via le serveur de relais. Associez-le à [tmux](./tmux) ou au [skill systemd](./claude-skill) pour maintenir la CLI en vie entre les connexions.

### ACP fonctionne-t-il avec Spck Editor Lite ?

Oui. Le trafic ACP utilise le même transport WebSocket que le système de fichiers et git, que Spck Editor Lite prend en charge. Assurez-vous que `security.userAuthenticationEnabled` est à `false` dans votre config CLI — l'auth Firebase n'est pas prise en charge dans Lite. Voir [Configuration → Authentification utilisateur](./cli-config#user-authentication).

### Pourquoi mon agent n'apparaît-il pas dans l'AI Chat ?

Vérifiez le log de démarrage de la CLI pour la ligne par agent :

- Agent non détecté — installez-le (voir [Agents IA pris en charge](#acp-supported-agents)).
- Détecté mais absent de l'éditeur — assurez-vous d'avoir complété le flux de connexion propre à l'agent (`claude`, `codex login`, `gemini`).
- ACP désactivé — vérifiez `acp.enabled` dans `.spck-editor/config/spck-cli.config.json`. Voir [Configuration](./cli-config#acp-settings).

## <a name="acp-troubleshooting"></a>Dépannage

### Agent détecté mais la session ne démarre pas

Cela signifie le plus souvent que l'agent n'est pas authentifié. Exécutez le flux de connexion de l'agent sur l'hôte CLI :

```bash
claude              # puis complétez l'auth dans le navigateur
codex login
gemini
```

Si le problème persiste, consultez les logs de la CLI dans `.spck-editor/logs/` pour la sortie stderr de l'agent, qui pointe généralement vers l'auth ou le binaire défaillant.

### Erreurs de limite d'utilisation pendant un chat

Pour Claude Code, l'éditeur transmet le 429 d'Anthropic mot pour mot. Vérifiez la [page d'usage Anthropic Console](https://platform.claude.com/usage) et les [docs de coût Claude Code](https://code.claude.com/docs/en/costs) — rappelez-vous que le seau de limite d'utilisation tiers est distinct de votre allocation `claude` interactive.

Pour Codex et Gemini, l'éditeur transmet l'erreur de quota propre du fournisseur. Résolvez-la via la console du fournisseur.

### La CLI plante au démarrage d'une session ACP

Spck CLI enregistre le trafic ACP dans `.spck-editor/logs/`. Suivez le fichier de log le plus récent en reproduisant le problème :

```bash
tail -f .spck-editor/logs/spck-*.log
```

Signalez un bug sur [github.com/spck-editor](https://github.com/spck-editor) avec l'extrait pertinent.

### L'agent modifie des fichiers hors de la racine du projet

Les agents ACP sont confinés au répertoire `root` configuré de la CLI. Si vous voyez des écritures en dehors, signalez un issue — cela ne devrait pas arriver. Comme contournement, exécutez `spck --root /path/to/specific/project` pour restreindre davantage le périmètre.

## <a name="acp-see-also"></a>Voir aussi

- [Démarrer avec Spck CLI](./cli-start) — installer, authentifier et se connecter pour la première fois
- [Référence de la CLI](./cli) — serveurs de relais, flux de travail quotidien, limites de connexion
- [Configuration → Paramètres ACP](./cli-config#acp-settings) — l'option de configuration `acp.enabled`
- [Utilisation avancée](./cli-advanced) — flags CLI, projets multiples, astuces pour les prompts mobiles
- [Utiliser Tmux](./tmux) — maintenir les sessions ACP vivantes à travers les reconnexions
- [Claude Skill : Linux Service](./claude-skill) — exécuter Spck CLI comme service `systemd` pour qu'ACP soit toujours disponible
- [Spécification de l'Agent Client Protocol](https://agentclientprotocol.com/) — la norme ouverte qu'ACP implémente
- [Documentation Claude Code](https://docs.claude.com/en/docs/claude-code/overview)
- [Dépôt Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
