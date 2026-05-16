# <a name="claude-skill"></a>Skill Claude : Exécuter Spck CLI en tant que service Linux

Cette page fournit une [skill Claude Code](https://docs.claude.com/en/docs/claude-code/skills) téléchargeable qui automatise l'installation de Spck CLI (`spck`) en tant que service `systemd` sur Linux. Une fois la skill installée, vous pouvez demander à Claude Code d'« exécuter spck en tant que service » et il vérifiera votre environnement, générera un fichier d'unité correct avec vos chemins absolus, l'installera et vérifiera qu'il fonctionne — sans avoir à copier-coller des commandes depuis une liste.

La skill encode la même configuration systemd décrite dans [Utiliser Tmux → Alternative : Service Linux](./tmux#linux-service), ainsi que les vérifications préalables et les diagnostics d'échec qu'il est facile de manquer lors de l'écriture manuelle du fichier d'unité.

## <a name="download"></a>Télécharger

Téléchargez le fichier de skill et enregistrez-le dans votre répertoire de skills Claude Code local :

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

Ou téléchargez manuellement : <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — placez-le à `~/.claude/skills/spck-cli-service/SKILL.md`.

## <a name="what-the-skill-does"></a>Ce que fait la skill

Lorsqu'elle est invoquée, la skill guide Claude Code tout au long de l'installation complète :

1. Vérifie que l'hôte est Linux avec `systemd` en cours d'exécution.
2. Résout le chemin absolu vers `spck` (évite la divergence de `PATH` qui casse `ExecStart`).
3. Avertit si `node` est installé via `nvm` — ces chemins changent à chaque mise à jour de Node et cassent l'unité silencieusement.
4. Confirme que `~/.spck-editor/.credentials.json` existe (la CLI doit avoir été exécutée de manière interactive au moins une fois avant de fonctionner en tant que service).
5. Choisit entre un **service utilisateur** (`systemctl --user`, sans `sudo`) et un **service système** selon vos besoins.
6. Écrit le fichier d'unité avec vos chemins réels renseignés — sans espaces réservés.
7. Exécute `daemon-reload`, `enable --now`, puis suit le journal pour confirmer que la CLI s'est connectée au serveur relais.

La skill documente également les sept modes d'échec les plus courants (mauvais chemin `ExecStart`, identifiants manquants, erreurs de permissions sur le répertoire de projet, boucles de redémarrage atteignant `start-limit-hit`, chemins nvm périmés après mise à jour de npm, etc.) pour que Claude Code puisse diagnostiquer un service défaillant plutôt que de simplement régénérer le fichier d'unité.

## <a name="installation"></a>Installation

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Étape 1 — Télécharger le fichier de skill :**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Étape 2 — Vérifier que Claude Code l'a détecté :**

```bash
claude /skills
```

Vous devriez voir `spck-cli-service` dans la liste. Sinon, redémarrez Claude Code pour qu'il réanalyse le répertoire des skills.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop charge les skills depuis le même répertoire `~/.claude/skills/` sur macOS et Linux. Sur Windows, le chemin est `%USERPROFILE%\.claude\skills\` — mais la skill elle-même ne fonctionne que sur des hôtes Linux, donc installez-la sur la machine où vous souhaitez exécuter `spck`, pas sur la machine exécutant Claude Desktop.

Si vous gérez un serveur Linux distant, exécutez Claude Code via SSH sur ce serveur (ou via le terminal Spck CLI, qui expose un shell complet au serveur). Installer la skill sur un Mac local n'aidera pas à configurer un service Linux distant.

</div>
  </div>
</div>

## <a name="usage"></a>Utilisation

Une fois installée, invoquez la skill en demandant à Claude Code en langage naturel. Exemples qui la déclencheront :

- « Installe spck en tant que service systemd »
- « Fais démarrer Spck CLI au boot »
- « Mon spck-cli.service ne cesse de redémarrer, peux-tu le déboguer ? »
- « Exécute spck en tant que daemon pour qu'il survive à ma déconnexion SSH »

Claude Code lira la skill, exécutera les vérifications préalables (qui vous demanderont d'approuver chaque commande), puis générera et installera le fichier d'unité. Examinez chaque commande avant de l'approuver — en particulier celles qui écrivent dans `/etc/systemd/system/` sous `sudo`.

## <a name="what-gets-installed"></a>Ce qui est installé

La skill installe un seul fichier d'unité. Pour un service utilisateur, il s'agit de :

```bash
~/.config/systemd/user/spck-cli.service
```

Avec un contenu similaire à :

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

Pour un service système, le fichier réside dans `/etc/systemd/system/spck-cli.service` et ajoute les directives `User=` et `Group=`. La skill choisit la bonne variante en fonction de votre environnement et renseigne les chemins absolus réels dans le fichier.

## <a name="why-a-skill-instead-of-copy-paste"></a>Pourquoi une skill plutôt que du copier-coller ?

Le fichier d'unité dans la [documentation tmux](./tmux#linux-service) est un point de départ, mais plusieurs choses doivent être correctes pour que le service fonctionne vraiment :

- `ExecStart` doit être le **chemin absolu** vers `spck`. `which spck` dans un shell de connexion résoudra les manipulations de PATH depuis `.bashrc` que systemd ne voit pas.
- Si `spck` a été installé sous `nvm`, le chemin intègre la version de Node — mettre à jour Node casse le service silencieusement jusqu'au prochain redémarrage.
- La CLI doit avoir été exécutée de manière interactive au moins une fois pour créer `~/.spck-editor/.credentials.json`. Un démarrage de service sans identifiants se termine proprement sans erreur évidente.
- `User=` doit posséder le `WorkingDirectory`, sinon la surveillance des fichiers renvoie `EACCES` et la CLI entre dans une boucle de redémarrage.
- Les services utilisateur ont besoin de `loginctl enable-linger` sur les serveurs headless, sinon ils ne fonctionnent que pendant une session de connexion active.

La skill encode tout cela pour que vous n'ayez pas à vous en souvenir.

## <a name="uninstall"></a>Désinstaller

Désactiver et supprimer le service :

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

Pour un service système :

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Pour supprimer la skill elle-même de Claude Code :

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>Voir aussi

- [Utiliser Tmux](./tmux) — approche alternative utilisant `tmux` pour maintenir la CLI active lors des déconnexions SSH.
- [Utilisation avancée](./cli-advanced) — référence complète des commandes CLI, substitutions de configuration et configurations multi-projets.
- [Configuration](./cli-config) — paramètres de terminal, de système de fichiers, de sécurité et d'authentification que le fichier d'unité ne couvre pas.
