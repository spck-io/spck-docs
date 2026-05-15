# <a name="cli-reference"></a>Référence CLI

## <a name="key-features"></a>Fonctionnalités Principales

- **Système de fichiers distant** : Accédez et éditez des fichiers locaux depuis l’application mobile Spck Editor
- **Intégration Git** : Opérations git complètes (commit, push, pull, gestion des branches) — nécessite Git 2.20.0+
- **Accès terminal** : Sessions de terminal interactives avec xterm.js
- **Proxy navigateur** : Prévisualisez votre serveur local dans une vue navigateur plein écran dans Spck Editor
- **Recherche rapide** : Recherche de fichiers optimisée avec détection automatique de ripgrep (100x plus rapide quand installé)
- **Sécurisé** : Requêtes signées cryptographiquement avec authentification Firebase optionnelle

## <a name="relay-server"></a>Serveur Relay

La CLI se connecte à Spck Editor via un serveur relay qui transmet les messages entre les deux. Au premier lancement, la CLI sélectionne automatiquement le serveur relay avec la latence la plus faible et enregistre la préférence dans `~/.spck-editor/.credentials.json`.

**IMPORTANT** : La CLI et le client Spck Editor doivent utiliser le même serveur relay pour se connecter. Si le client ne trouve pas la CLI, vérifiez que les deux côtés ont sélectionné le même serveur relay.

### Serveurs Relay Disponibles

| Région         | URL                 |
| -------------- | ------------------- |
| Europe         | `cli-eu-1.spck.io`  |
| Amérique du Nord | `cli-na-1.spck.io`  |
| Asie du Sud    | `cli-sas-1.spck.io` |
| Asie de l’Est | `cli-ea-1.spck.io`  |

### Remplacer le Serveur Relay

```bash
# Utiliser un serveur relay spécifique
spck --server cli-eu-1.spck.io

# Forme courte
spck -s cli-na-1.spck.io
```

Le remplacement est sauvegardé et réutilisé lors des exécutions suivantes. Pour relancer la sélection automatique, effacez vos identifiants et redémarrez :

```bash
spck --logout
spck
```

### Choisir un Serveur Relay dans Spck Editor

Lors de la connexion depuis l’application mobile via **Link Remote Server**, sélectionnez le même serveur relay dans le menu déroulant **Relay Server** que celui utilisé par la CLI. Le nom du serveur relay est affiché dans la sortie de la CLI après la connexion.

## <a name="daily-workflow"></a>Flux de Travail Quotidien

### Démarrer Votre Session

```bash
cd /path/to/project
spck
# Se connecter depuis l'application mobile (connexion automatique au serveur enregistré)
# Commencer à coder
```

### Éditer des Fichiers

1. Parcourir les fichiers dans l’application mobile
2. Appuyer pour ouvrir et éditer
3. Les fichiers se sauvegardent automatiquement sur votre ordinateur

### Exécuter des Commandes Git

**Option 1 - GUI de l’application mobile :**

- Ouvrir le panneau Git
- Voir les changements, préparer les fichiers
- Commiter et pousser

**Option 2 - Terminal :**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### Sessions Terminal

Appuyez sur l’icône terminal dans l’application mobile pour un accès shell complet avec vos permissions utilisateur.

### Terminer Votre Session

```bash
# Garder la CLI active pour des reconnexions rapides (recommandé)
# Ou arrêter avec Ctrl+C
```

## <a name="troubleshooting"></a>Dépannage

### Répertoire Racine Non Trouvé

```bash
# Reconfigurer avec le bon chemin
spck --setup

# Ou spécifier directement
spck --root /correct/path/to/project
```

### Configuration Corrompue

```bash
# Effacer les paramètres et recommencer
spck --logout
spck --setup
```

### Problèmes de Connexion

1. Vérifier la connexion internet
2. Vérifier que la CLI et Spck Editor utilisent le **même serveur relay** (affiché dans la sortie de la CLI après la connexion)
3. Essayer de se déconnecter et se reconnecter :
   ```bash
   spck --logout
   spck
   ```
4. Vérifier les paramètres du pare-feu — s’assurer que les connexions WebSocket (port 443) sont autorisées

### Le Code QR Ne Se Scanne Pas

- Vérifier que l’application Spck Editor est installée avant de scanner
- Utiliser la saisie manuelle : Projects → New Project → Link Remote Server
- Utiliser l’application Appareil photo native, pas des scanners tiers

### Les Opérations Git Ne Fonctionnent Pas

1. Vérifier que Git est installé :

   ```bash
   git --version  # Nécessite 2.20.0+
   ```

2. Installer si nécessaire :

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows : Télécharger depuis git-scm.com
   ```

### Performance de Recherche Lente

Installez ripgrep pour une recherche 100x plus rapide :

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# La CLI détecte et utilise automatiquement ripgrep
```

### Permission Refusée

```bash
# Voir les permissions
ls -la /path/to/file

# Corriger si nécessaire
chmod 644 /path/to/file

# Ne pas utiliser sudo - la CLI doit s'exécuter en tant qu'utilisateur propriétaire des fichiers
```

## <a name="connection-limits"></a>Limites de Connexion

Le nombre maximum de connexions CLI simultanées et les limites d’utilisation quotidienne dépendent de votre type de compte :

| Plan      | Connexions CLI | Limite Quotidienne |
| --------- | -------------- | ------------------ |
| Free      | 1              | 30 minutes         |
| Supporter | 2              | Illimité           |
| Gold      | 5              | Illimité           |

L’utilisation du niveau gratuit se réinitialise quotidiennement à 00h00 UTC.

Quand la limite de connexions est atteinte :

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

Quand la limite quotidienne gratuite est atteinte :

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

Vérifier les connexions actives :

```bash
spck --account
```

> 💡 **Note** : Un seul appareil mobile peut se connecter à une instance CLI à la fois. Chaque instance CLI utilise un slot de connexion.

## <a name="support"></a>Support

- **Site web** : [https://spck.io](https://spck.io)
- **Support** : Contact via l’application mobile Spck Editor
