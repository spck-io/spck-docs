# <a name="cli-reference"></a>Référence CLI

## <a name="key-features"></a>Fonctionnalités Principales

- **Système de fichiers distant** : Accédez et éditez des fichiers locaux depuis l’application mobile Spck Editor
- **Intégration Git** : Opérations git complètes (commit, push, pull, gestion des branches) — nécessite Git 2.20.0+
- **Accès terminal** : Sessions de terminal interactives avec xterm.js
- **Proxy navigateur** : Prévisualisez votre serveur local dans une vue navigateur plein écran dans Spck Editor
- **Recherche rapide** : Recherche de fichiers optimisée avec détection automatique de ripgrep (100x plus rapide quand installé)
- **Agents IA de code locaux (ACP)** : Pilotez Claude Code, Codex ou Gemini CLI depuis le Chat IA de Spck Editor via l’[Agent Client Protocol](https://agentclientprotocol.com/). L’agent s’exécute sur votre machine avec votre propre abonnement. Voir [Agents IA de code sur mobile (ACP)](./cli-acp).
- **Fast Lane** (Supporter & Gold) : Connexion WebRTC directe en pair-à-pair entre Spck Editor et la CLI, 2 fois plus rapide que le relay en moyenne. Voir [Fast Lane](#fast-lane).
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

## <a name="fast-lane"></a>Fast Lane

Fast Lane est une fonctionnalité premium réservée aux abonnés **Supporter** et **Gold**. Au lieu de faire transiter chaque message par le serveur relay, Spck Editor se connecte **directement à votre CLI** via WebRTC (pair-à-pair). En supprimant l’étape du relay et en réduisant les allers-retours, Fast Lane est **en moyenne 2 fois plus rapide que le relay** : les opérations sur les fichiers, la recherche, Git et la saisie dans le terminal paraissent nettement plus réactives.

Le serveur relay reste nécessaire : c’est là que votre CLI est enregistrée, et il orchestre la négociation initiale entre l’éditeur et la CLI. Une fois le chemin direct établi, les données de votre projet y transitent au lieu de passer par le relay.

### Prérequis

- Un abonnement **Supporter** ou **Gold** actif sur le compte avec lequel la CLI est connectée
- Spck CLI **0.7.0 ou ultérieur** (`npm i -g spck`)
- La prise en charge de WebRTC, à la fois sur l’appareil exécutant Spck Editor et sur la machine exécutant la CLI

### Activer ou désactiver Fast Lane

**Dans Spck Editor :** Ouvrez **Link Remote Server** (ou modifiez une connexion existante depuis le menu) et utilisez l’interrupteur **⚡ Fast Lane**. Il est activé par défaut pour les nouvelles connexions sur les comptes Supporter et Gold.

**Dans la CLI :** Fast Lane est activé par défaut. Appuyez sur **`f`** dans le tableau de bord de la CLI pour l’activer ou le désactiver pour le projet en cours, ou définissez `fastLane.enabled` dans la [configuration du projet](./cli-config#fast-lane-settings). Les changements prennent effet après le redémarrage de la CLI. Désactivez-le sur les réseaux qui bloquent le trafic pair-à-pair.

Le tableau de bord de la CLI affiche l’état actuel de Fast Lane (actif, disponible, désactivé ou indisponible sur cette plateforme), et le panneau Fichiers de Spck Editor indique le transport utilisé ainsi que le ping actuel, par exemple `Fast Lane · 24 ms` ou `Relay · 80 ms`.

### Repli automatique

Si une connexion directe ne peut pas être établie, Spck Editor bascule automatiquement sur le relay pour que vous puissiez continuer à travailler, et affiche un message en expliquant la raison. Causes fréquentes :

- La CLI n’est pas à jour — mettez-la à jour avec `npm i -g spck`
- Fast Lane est désactivé dans la configuration du projet de la CLI
- WebRTC n’est pas disponible sur la machine exécutant la CLI, ni sur votre appareil
- Le serveur relay ne prend pas encore en charge Fast Lane
- Le réseau bloque le chemin pair-à-pair direct (par exemple, un pare-feu d’entreprise strict ou un NAT)

### Sécurité

Le trafic Fast Lane est chiffré de bout en bout par WebRTC (DTLS). De plus, la négociation d’authentification de la CLI est liée à la session DTLS précise : la CLI doit prouver qu’elle détient le secret de votre connexion sur ce canal exact avant tout échange de données du projet. Toutes les requêtes restent signées cryptographiquement, comme sur le relay. Voir [Sécurité de la CLI](./cli-config#security).

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
5. Si un message indique que Fast Lane est indisponible et que le relay est utilisé, la connexion fonctionne toujours via le relay. Consultez [Fast Lane](#fast-lane), section « Repli automatique », pour les causes et les solutions

### Le Code QR Ne Se Scanne Pas

- Scannez depuis Spck Editor : Projets → Nouveau projet → Lier un serveur distant, puis appuyez sur l’icône de QR code
- Si le terminal est trop petit pour afficher le code, la CLI indique la taille nécessaire. Agrandissez la fenêtre ou saisissez les informations à la main dans la même boîte de dialogue
- Évitez les scanners tiers, qui pourraient exposer votre clé secrète

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

Lite permet de modifier des projets sur votre ordinateur ou une VM publique via Spck CLI. Les projets distants nécessitent un **compte Spck et un abonnement Spck actif**, en plus de l’achat unique de Lite. L’abonnement contribue aux frais récurrents d’hébergement, d’exploitation et de maintenance des serveurs Spck. Les outils locaux d’édition et Git inclus restent accessibles sans abonnement.

Le nombre maximum de connexions CLI simultanées et les limites d’utilisation quotidienne dépendent de votre type de compte :

| Plan      | Connexions CLI | Limite Quotidienne | Fast Lane |
| --------- | -------------- | ------------------ | --------- |
| Free      | 1              | 30 minutes         | —         |
| Supporter | 2              | Illimité           | ✓         |
| Gold      | 5              | Illimité           | ✓         |

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
