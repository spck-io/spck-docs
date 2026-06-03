# <a name="cli-advanced-usage"></a>Utilisation avancée du CLI

## <a name="cli-commands"></a>Commandes du CLI

### Commandes de base

```bash
# Démarrer le CLI
spck

# Lancer l'assistant de configuration
spck --setup

# Afficher les informations du compte
spck --account

# Se déconnecter et effacer les identifiants
spck --logout

# Afficher l'aide
spck --help

# Afficher la version
spck --version
```

### Options avancées

```bash
# Utiliser un fichier de configuration personnalisé
spck --config /path/to/config.json
spck -c /path/to/config.json

# Remplacer le répertoire racine
spck --root /path/to/project
spck -r /path/to/project

# Remplacer le serveur de relais (par ex., utiliser une région spécifique)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>Agents de codage IA (ACP)

La Spck CLI relie le Chat IA de Spck Editor à un agent de codage IA installé localement — **Claude Code**, **Codex** ou **Gemini CLI** — via l'[Agent Client Protocol (ACP)](https://agentclientprotocol.com/). Le modèle s'exécute sur votre machine avec votre propre abonnement, modifie de vrais fichiers sur le disque et transmet les demandes de permission à votre téléphone.

![Mode IA local dans le Chat IA de Spck Editor pilotant Claude Code depuis un téléphone](https://docs.spck.io/assets/gifs/acp-ai.gif)

→ **[Agents IA de code sur mobile (ACP)](./cli-acp)** — le guide complet : agents pris en charge, installation, facturation & limites de débit (y compris le quota Claude Code tiers distinct d'Anthropic), configuration, FAQ et dépannage.

> 💡 **Conseil** : Utilisez **tmux** pour maintenir les sessions d'agents IA en cours d'exécution même après vous être déconnecté. Démarrez une session tmux sur votre ordinateur (`tmux new -s code`), lancez l'agent, puis reconnectez-vous depuis le terminal Spck CLI sur votre téléphone (`tmux attach -t code`). Fonctionne aussi bien avec les agents shell qu'avec les agents en mode ACP. Voir [Utiliser Tmux](./tmux) pour un guide complet incluant la configuration d'un serveur distant persistant.

## <a name="advanced-usage"></a>Utilisation avancée

### Projets multiples

Exécutez des instances CLI séparées pour différents projets simultanément :

```bash
# Terminal 1 : Projet A
cd /path/to/projectA
spck

# Terminal 2 : Projet B
cd /path/to/projectB
spck
```

Chaque projet conserve sa propre configuration et connexion.

> 💡 **Conseil** : Vous pouvez également utiliser plusieurs instances CLI pour transférer des fichiers entre votre ordinateur et votre téléphone. Voir [Transfert de fichiers entre mobile et ordinateur](./cli-file-transfer) pour un guide étape par étape.

### Fichiers de configuration personnalisés

Créez des configurations spécialisées pour différents scénarios :

```bash
# Configuration de développement
spck --config ~/configs/dev-config.json

# Configuration de production (lecture seule, sans terminal)
spck --config ~/configs/prod-config.json
```

### Configuration par environnement

**Développement local :**

```json
{
  "security": {
    "userAuthenticationEnabled": false
  },
  "terminal": {
    "enabled": true
  }
}
```

**Serveur de production :**

```json
{
  "security": {
    "userAuthenticationEnabled": true
  },
  "terminal": {
    "enabled": false
  }
}
```

### Utilisation CPU élevée

Réduisez la surveillance des fichiers en ajoutant des patterns d'exclusion supplémentaires :

```json
{
  "filesystem": {
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/dist/**",
      "**/build/**",
      "**/.next/**",
      "**/coverage/**",
      "**/.cache/**"
    ]
  }
}
```

Limitez le nombre de terminaux simultanés :

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>Réduire le prompt du shell pour mobile

Sur les appareils mobiles, l'espace horizontal à l'écran est limité. Le prompt par défaut du shell — qui inclut généralement le chemin du répertoire courant, le nom d'utilisateur et le nom d'hôte — peut encombrer le terminal et rendre la lecture de la sortie des commandes plus difficile.

Remplacer votre prompt par simplement `$ ` offre une expérience de terminal bien plus épurée sur les petits écrans.

### Bash

Ajoutez ce qui suit dans `~/.bashrc` :

```bash
export PS1='\$ '
```

Appliquez sans redémarrer le shell :

```bash
source ~/.bashrc
```

### Zsh

Ajoutez ce qui suit dans `~/.zshrc` :

```zsh
PROMPT='$ '
```

Appliquez sans redémarrer le shell :

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

Créez votre fichier de profil s'il n'existe pas encore, puis ouvrez-le :

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Ajoutez ce qui suit au profil :

```powershell
function prompt { "$ " }
```

Appliquez sans redémarrer le shell :

```powershell
. $PROFILE
```

### Invite de commandes (Windows)

Définissez un prompt minimal pour la session en cours :

```cmd
PROMPT $$
```

Pour rendre cela permanent, ajoutez `PROMPT` en tant que variable d'environnement **Utilisateur** ou **Système** avec la valeur `$$` via **Panneau de configuration → Système → Paramètres système avancés → Variables d'environnement**.
