# <a name="tmux"></a>Utiliser Tmux avec Spck CLI

Tmux (Terminal Multiplexer) permet aux sessions de terminal de s'exécuter indépendamment de la fenêtre ou de la connexion SSH qui les a démarrées. Pour les utilisateurs de Spck CLI, cela signifie que vous pouvez maintenir des sessions actives lors des reconnexions, partager une session d'agent en cours entre le bureau et le mobile, et exécuter la CLI de manière persistante sur un serveur distant même après la chute de votre connexion SSH.

## <a name="installation"></a>Installation

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux fonctionne nativement sous Linux. Sous Windows, utilisez le [Sous-système Windows pour Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install), puis installez tmux dans WSL.

**Étape 1 — Installer WSL (PowerShell en tant qu'Administrateur) :**

```powershell
wsl --install
```

**Étape 2 — Ouvrir un terminal WSL et installer tmux :**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Cas d'usage 1 : Partager des sessions d'agent entre bureau et mobile

Le workflow tmux le plus puissant avec Spck CLI consiste à démarrer un agent de codage IA sur votre bureau et à le reprendre facilement depuis votre mobile — ou l'inverse. Les deux voient exactement le même état du terminal, y compris l'historique de défilement complet.

### Démarrer une session sur le bureau

Créez une session tmux nommée :

```bash
tmux new -s code
```

Lancez votre agent IA dans la session :

```bash
claude
```

L'agent s'exécute dans tmux. Détachez-vous à tout moment en appuyant sur **Ctrl+B** puis **D** — la session et tout ce qui s'y exécute continue en arrière-plan.

### Se connecter depuis le mobile

1. Ouvrez Spck Editor et connectez-vous à votre serveur CLI
2. Ouvrez un terminal depuis le panneau terminal de Spck Editor
3. Rattachez-vous à la session tmux en cours :

```bash
tmux attach -t code
```

Vous voyez exactement le même terminal que sur votre bureau — y compris l'agent en cours d'exécution, sa sortie et l'historique de défilement complet. Plusieurs clients peuvent se connecter simultanément et voir la sortie en direct.

### Revenir au bureau

Reconnectez-vous depuis n'importe quel terminal à tout moment :

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Cas d'usage 2 : CLI persistante sur un serveur distant

Si vous exécutez Spck CLI sur un serveur distant via SSH, la CLI s'arrête dès que la session SSH se termine — que vous fermiez votre ordinateur portable, perdiez le Wi-Fi ou que la connexion expire. Tmux maintient le processus actif sur le serveur quel que soit l'état de votre connexion.

### Configuration sur le serveur distant

Connectez-vous en SSH à votre serveur et démarrez une session tmux nommée avant de lancer la CLI :

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

La CLI s'exécute maintenant dans tmux sur le serveur. Fermez la connexion SSH — ou perdez-la complètement — et la CLI continue de fonctionner.

### Se reconnecter après une déconnexion

```bash
ssh user@your-server.com
tmux attach -t spck
```

La CLI reprend exactement là où elle s'était arrêtée. Les clients mobiles peuvent se reconnecter normalement via le serveur relais.

### Lister les sessions en cours

```bash
tmux ls
```

## <a name="linux-service"></a>Alternative : Service Linux

Pour une configuration entièrement automatisée qui démarre la CLI au démarrage sans gestion manuelle de tmux, exécutez Spck CLI en tant que service systemd.

### Créer le fichier de service

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Remplacez `your-username` et `/path/to/your/project` par vos valeurs réelles. Si vous avez installé `spck` globalement (`npm install -g spck`), remplacez `ExecStart` par la sortie de `which spck`.

### Activer et démarrer

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Vérifier le statut et les journaux

```bash
# Voir le statut
sudo systemctl status spck-cli

# Suivre les journaux en direct
journalctl -u spck-cli -f
```

Le service démarre automatiquement à chaque redémarrage et redémarre lui-même si le processus plante.

## <a name="essential-tmux-commands"></a>Commandes essentielles de Tmux

| Commande | Action |
| --- | --- |
| `tmux new -s name` | Créer une nouvelle session nommée |
| `tmux attach -t name` | Se rattacher à une session existante |
| `tmux ls` | Lister toutes les sessions |
| `tmux kill-session -t name` | Fermer une session |
| Ctrl+B, D | Se détacher de la session (continue en arrière-plan) |
| Ctrl+B, C | Créer une nouvelle fenêtre |
| Ctrl+B, N | Passer à la fenêtre suivante |
| Ctrl+B, P | Passer à la fenêtre précédente |
| Ctrl+B, [ | Entrer en mode défilement (touches fléchées / Page préc. / Page suiv.) |
| Q | Quitter le mode défilement |
