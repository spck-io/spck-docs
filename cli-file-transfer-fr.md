# <a name="cli-file-transfer"></a>Transfert de fichiers entre mobile et ordinateur

## <a name="overview"></a>Présentation

Lorsque vous exécutez Spck CLI sur votre ordinateur, il agit comme un hub de synchronisation entre le système de fichiers de votre ordinateur et les projets locaux stockés sur votre téléphone. Les deux côtés apparaissent côte à côte dans le gestionnaire de fichiers de Spck Editor — les projets locaux de votre téléphone à gauche et les fichiers de votre ordinateur en tant que serveur distant connecté — et vous pouvez copier des fichiers ou des dossiers entiers dans n'importe quelle direction en utilisant les commandes standard copier-coller.

Pas besoin d'AirDrop, de Bluetooth, de câble USB ni de stockage cloud tiers. Les transferts sont chiffrés de bout en bout via une connexion WebSocket et restent sur votre Wi-Fi local lorsque les deux appareils sont sur le même réseau.

## <a name="how-it-works"></a>Fonctionnement

Le CLI expose votre répertoire d'ordinateur en tant que projet de serveur distant dans le gestionnaire de fichiers de Spck Editor. Les projets locaux enregistrés sur votre téléphone sont stockés dans le stockage local de l'application. Spck Editor traite les deux comme des emplacements de projet de première classe, de sorte que toute opération de fichier qui fonctionne au sein d'un seul projet — y compris copier et coller — fonctionne également entre eux.

```
Téléphone (stockage local)     Ordinateur (via CLI)
──────────────────────────     ─────────────────────
my-project/               ↔   ~/projects/my-project/
  ├── index.html                 ├── index.html
  ├── style.css                  ├── style.css
  └── assets/                    └── assets/
      └── logo.png                   └── logo.png
```

Les répertoires sont transférés de manière récursive — tous les fichiers à l'intérieur sont copiés, avec les sous-répertoires créés automatiquement à la destination.

## <a name="desktop-to-mobile"></a>De l'ordinateur vers le mobile

Utilisez ceci lorsque vous souhaitez apporter des fichiers de votre ordinateur sur votre téléphone — par exemple, pour travailler hors connexion, partager un projet avec un collègue qui n'a que l'application mobile, ou prendre un instantané de votre travail sur l'appareil.

1. **Démarrez le CLI** sur votre ordinateur, en pointant vers le dossier depuis lequel vous souhaitez transférer :

   ```bash
   spck --root ~/projects
   ```

2. **Connectez votre téléphone** en scannant le QR code avec votre application appareil photo et en ouvrant le lien dans Spck Editor.

3. Dans Spck Editor, votre dossier d'ordinateur apparaît comme un projet de serveur distant dans le panneau **Projets**.

4. **Appuyez longuement sur le fichier ou dossier** souhaité dans le projet distant, puis appuyez sur **Copier**.

5. **Naviguez vers un projet local** sur votre téléphone (ou créez-en un nouveau via **Nouveau projet**).

6. **Appuyez longuement sur le dossier de destination**, puis appuyez sur **Coller**.

Les fichiers sont téléchargés depuis votre ordinateur et enregistrés dans le stockage local de votre téléphone.

## <a name="mobile-to-desktop"></a>Du mobile vers l'ordinateur

Utilisez ceci lorsque vous souhaitez renvoyer du travail de votre téléphone vers votre ordinateur — par exemple, après avoir édité en déplacement, ou pour consolider des projets créés sur l'appareil.

1. **Démarrez le CLI** sur votre ordinateur, en pointant vers le dossier où vous souhaitez que les fichiers arrivent :

   ```bash
   spck --root ~/Desktop/from-phone
   ```

2. **Connectez votre téléphone** en scannant le QR code.

3. Dans Spck Editor, ouvrez le **projet local** sur votre téléphone qui contient les fichiers que vous souhaitez envoyer.

4. **Appuyez longuement sur le fichier ou dossier** souhaité, puis appuyez sur **Copier**.

5. **Naviguez vers le projet distant de l'ordinateur** dans le panneau **Projets**.

6. **Appuyez longuement sur le dossier de destination**, puis appuyez sur **Coller**.

Les fichiers sont lus depuis le stockage local de votre téléphone et écrits sur votre ordinateur via le CLI.

## <a name="transferring-projects"></a>Transférer des projets entiers

Vous pouvez copier un dossier de projet entier en une seule opération de collage. Appuyez longuement sur la racine du projet dans l'arborescence des fichiers et sélectionnez **Copier**, puis naviguez vers la destination et **Coller**. L'arborescence complète des répertoires — incluant tous les fichiers dans tous les sous-répertoires — est transférée.

C'est utile pour :

- **Sauvegarder un projet mobile sur votre ordinateur** avant d'apporter des modifications importantes
- **Initialiser un nouveau projet sur le téléphone** à partir d'une base de code existante sur l'ordinateur
- **Fusionner du travail** de plusieurs appareils en un seul endroit

## <a name="tips"></a>Conseils

### Limite de taille de fichier

La taille maximale de fichier par défaut est de **10 Mo** par fichier. Pour transférer des fichiers plus volumineux comme des images, des archives ou des binaires compilés, augmentez la limite dans votre configuration CLI :

```json
{
  "filesystem": {
    "maxFileSize": "200MB"
  }
}
```

Voir [Configuration CLI](./cli-config) pour tous les détails.

### Vitesse de transfert

La vitesse dépend entièrement de votre connexion Wi-Fi locale ou Internet. Pour les grands répertoires, les transferts s'effectuent fichier par fichier, donc le débit global évolue en fonction du nombre de fichiers. Sur un réseau Wi-Fi domestique typique, les petits projets à prédominance textuelle (des centaines de fichiers) se terminent en quelques secondes.

### Sécurité

Tous les transferts sont chiffrés via WSS (WebSocket Secure) et chaque requête est signée avec une clé secrète par session. Le serveur de relais transmet les messages entre les appareils mais ne reçoit jamais de contenu non chiffré. Voir [Sécurité CLI](./cli-config#security) pour tous les détails.

### Exécuter plusieurs transferts

Le CLI expose un seul répertoire racine. Pour transférer depuis plusieurs emplacements simultanément, exécutez des instances CLI séparées dans différents terminaux :

```bash
# Terminal 1 : exposer ~/projects
spck --root ~/projects

# Terminal 2 : exposer ~/Documents
spck --root ~/Documents
```

Chaque instance génère son propre QR code et sa propre connexion, et les deux serveurs distants apparaissent simultanément dans le panneau **Projets** de Spck Editor.
