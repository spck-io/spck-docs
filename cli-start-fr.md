# <a name="getting-started"></a>Premiers pas avec Spck CLI

## <a name="overview"></a>Présentation

Spck CLI est un outil en ligne de commande qui connecte votre environnement de développement local à l'application mobile Spck Editor via une connexion WebSocket sécurisée. Une fois lancé, vous pouvez parcourir et modifier des fichiers locaux, exécuter des commandes dans le terminal et prévisualiser des serveurs locaux, le tout depuis votre téléphone ou tablette.

## <a name="requirements"></a>Prérequis

### Obligatoires

- **Node.js** : 18.0.0 ou supérieur
- **Compte Spck Editor** : Compte gratuit (30 min/jour) ou abonnement Premium (illimité)
- **Application mobile Spck Editor** : [Android](https://play.google.com/store/apps/details?id=io.spck) ou [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Optionnels (Recommandés)

- **Git** : 2.20.0+ pour les fonctionnalités d'intégration Git
- **ripgrep** : 15.0.0+ pour une recherche de fichiers nettement plus rapide (amélioration 100x)

## <a name="installation"></a>Installation

### Option 1 : Exécuter avec npx (Sans installation)

```bash
npx spck
```

Utilise toujours la dernière version — idéal pour la première configuration ou une utilisation occasionnelle.

### Option 2 : Installation globale

```bash
npm install -g spck
spck
```

Démarrage plus rapide, fonctionne hors connexion et pratique pour une utilisation quotidienne.

## <a name="demo"></a>Démo

Une courte démonstration de la connexion de Spck CLI à l’application mobile et de l’édition de fichiers locaux à distance :

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>Configuration initiale

Au premier lancement du CLI, un assistant de configuration interactif vous guide à travers les étapes :

### 1. Authentification

```bash
spck
# Appuyez sur ENTRÉE pour ouvrir le navigateur
# Connectez-vous avec votre compte Spck Editor
# Autorisez le CLI
# Revenez au terminal
```

Les identifiants sont stockés dans `~/.spck-editor/.credentials.json` et persistent d'une session à l'autre.

### 2. Configuration du projet

L'assistant configure :

- **Répertoire racine** : Répertoire de base pour l'accès aux fichiers (par défaut : répertoire courant)
- **Nom du projet** : Nom affiché dans l'application mobile (par défaut : nom du répertoire)

### 3. Intégration Git (Optionnel)

Si un fichier `.gitignore` est détecté, le CLI propose d'y ajouter `.spck-editor/` pour éviter de valider accidentellement des secrets :

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**Recommandation** : Choisissez `Y` pour protéger les identifiants de connexion.

### Relancer la configuration

Pour reconfigurer à tout moment :

```bash
spck --setup
```

## <a name="connecting"></a>Se connecter à Spck Editor

Une fois le CLI lancé, il affiche un QR code et les détails de connexion.

### Méthode 1 : QR code (Recommandé)

**IMPORTANT** : Installez l'application Spck Editor AVANT de scanner le QR code.

**Sur Android :**

1. Utilisez l'application Appareil photo ou le scanner QR des réglages rapides
2. Une fois détecté, appuyez sur la notification pour ouvrir Spck Editor
3. L'application se connecte automatiquement

> 💡 **Remarque** : Certains lecteurs de QR code ne peuvent pas gérer le schéma personnalisé pour ouvrir Spck Editor directement. Copiez l'URL et collez-la dans Chrome, qui lancera Spck Editor depuis l'URL.

**Sur iOS :**

1. Utilisez l'application Appareil photo ou le scanner QR du Centre de contrôle
2. Une fois détecté, appuyez sur la notification pour ouvrir Spck Editor
3. L'application se connecte automatiquement

> 💡 **Remarque** : Spck Editor ne dispose PAS d'un scanner QR intégré. Utilisez la fonction QR native de votre appareil.

### Méthode 2 : Saisie manuelle

Si le QR code ne fonctionne pas :

1. Ouvrez Spck Editor → **Projets** → **Nouveau projet** → **Lier un serveur distant**
2. Saisissez l'**ID client** et le **Secret** affichés dans le terminal
3. Appuyez sur **Connecter**

## <a name="next-steps"></a>Prochaines étapes

1. **Comprendre le système de relais** : Apprenez comment le CLI achemine le trafic et comment choisir un serveur — voir [Référence CLI](./cli)
2. **Configurer votre environnement** : Ajustez les paramètres du terminal, de la sécurité et du système de fichiers — voir [Configuration](./cli-config)
3. **Explorer les fonctionnalités avancées** : Commandes CLI, agents de codage IA, projets multiples — voir [Utilisation avancée](./cli-advanced)
4. **Transférer des fichiers entre appareils** : Copiez des projets entre votre téléphone et votre ordinateur de bureau sans fil — voir [Transfert de fichiers](./cli-file-transfer)
5. **Maintenir les sessions actives** : Partagez des sessions entre appareils avec tmux — voir [Utilisation de Tmux](./tmux)
