# <a name="getting-started"></a>Premiers pas avec Spck CLI

## <a name="overview"></a>Présentation

Spck CLI sort de bêta. Connectez votre ordinateur à Spck Editor sur téléphone ou tablette pour modifier des fichiers, utiliser Git et les terminaux et prévisualiser des serveurs locaux. Les connexions utilisent un relais chiffré ou une connexion directe [Fast Lane](./cli#fast-lane) (Supporter et Gold).

## <a name="requirements"></a>Prérequis

Lite permet de modifier des projets sur votre ordinateur ou une VM publique via Spck CLI. Les projets distants nécessitent un **compte Spck et un abonnement Spck actif**, en plus de l’achat unique de Lite. L’abonnement contribue aux frais récurrents d’hébergement, d’exploitation et de maintenance des serveurs Spck. Les outils locaux d’édition et Git inclus restent accessibles sans abonnement.

### Obligatoires

- **Node.js** : **22.22.2+ (22.x), 24.15.0+ (24.x), ou 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Compte Spck Editor** : Compte gratuit (30 min/jour) ou abonnement Premium (illimité)
- **Application mobile Spck Editor** : [Android](https://play.google.com/store/apps/details?id=io.spck) ou [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Optionnels (Recommandés)

- **Git** : 2.20.0+ pour l’[intégration Git](./git-support#git-limitations-cli) dans les projets distants
- **ripgrep** : 15.0.0+ pour une recherche de fichiers nettement plus rapide (amélioration 100x)

## <a name="installation"></a>Installation

### Option 1 : Exécuter avec npx (Sans installation)

```bash
npx spck@latest
```

Demande la dernière version de la CLI, idéale pour la première configuration ou un usage occasionnel. `npx spck` peut réutiliser une version installée.

### Option 2 : Installation globale

```bash
npm install -g spck
spck
```

Installez une fois, puis lancez `spck` au quotidien. Mettez à jour avec `npm install -g spck@latest`. Les connexions distantes nécessitent toujours Internet.

## <a name="demo"></a>Démo

[Voir la vidéo de Spck CLI](https://youtu.be/EtfEhd5EmKM), avec la nouvelle fonction Fast Lane.

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

Si le navigateur ne peut pas joindre localhost, la connexion passe par le relais. Utilisez le QR code de connexion au compte ou le lien affiché pour vous authentifier depuis un autre appareil. Ce code est distinct du QR code de connexion au projet.

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

Pour un nouveau projet, la CLI affiche le QR code jusqu’à la première connexion réussie d’un éditeur. Les lancements suivants ouvrent directement le tableau de bord ; appuyez sur **`c`** pour revoir le QR code et les détails de connexion, ou **`l`** pour les journaux. Agrandissez le terminal si le QR code ne tient pas.

### Méthode 1 : QR code (Recommandé)

1. Ouvrez Spck Editor → **Projets** → **Nouveau projet** → **Lier un serveur distant**
2. Appuyez sur l’icône de QR code
3. Scannez le QR code affiché dans le terminal. L’application se connecte automatiquement.

> 💡 **Remarque** : vous pouvez aussi scanner le code avec l’application Appareil photo de votre appareil, qui ouvre le lien dans Spck Editor si l’application est installée.

### Méthode 2 : Saisie manuelle

Si vous ne pouvez pas scanner le QR code :

1. Ouvrez Spck Editor → **Projets** → **Nouveau projet** → **Lier un serveur distant**
2. Saisissez l'**ID client** et le **Secret** affichés dans le terminal
3. Sélectionnez le serveur relais affiché dans le terminal
4. Appuyez sur **Connecter**

Si **Require PIN to connect** est activé, saisissez le PIN choisi dans le tableau de bord CLI. L’app ne le conserve pas. Voir [PIN de connexion](./cli-config#connection-pin).

## <a name="next-steps"></a>Prochaines étapes

1. **Comprendre le système de relais** : Apprenez comment le CLI achemine le trafic et comment choisir un serveur — voir [Référence CLI](./cli)
2. **Configurer votre environnement** : Ajustez les paramètres du terminal, de la sécurité et du système de fichiers — voir [Configuration](./cli-config)
3. **Explorer les fonctionnalités avancées** : Commandes CLI, agents de codage IA, projets multiples — voir [Utilisation avancée](./cli-advanced)
4. **Transférer des fichiers entre appareils** : Copiez des projets entre votre téléphone et votre ordinateur de bureau sans fil — voir [Transfert de fichiers](./cli-file-transfer)
5. **Maintenir les sessions actives** : Partagez des sessions entre appareils avec tmux — voir [Utilisation de Tmux](./tmux)
