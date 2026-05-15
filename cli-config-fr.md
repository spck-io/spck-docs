# <a name="cli-configuration"></a>Configuration CLI

## <a name="configuration"></a>Configuration

### Emplacement du Fichier de Configuration

La configuration est stockée dans `.spck-editor/config/spck-cli.config.json` dans le répertoire de votre projet.

**Important** : `.spck-editor/config` est un **lien symbolique** vers `~/.spck-editor/projects/{project_id}/`, gardant les secrets en dehors du répertoire de votre projet.

### Configuration Par Défaut

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### Paramètres du Proxy Navigateur

- **`browserProxy.enabled`** (boolean) : Activer/désactiver la fonctionnalité de proxy navigateur
  - Par défaut : `true`
  - Mettre à `false` pour empêcher l’application mobile d’ouvrir une session de proxy navigateur via la CLI

### Paramètres du Terminal

- **`terminal.enabled`** (boolean) : Activer/désactiver l’accès au terminal
  - Par défaut : `true`
  - Mettre à `false` pour réduire le risque d’accès non autorisé à votre terminal

- **`terminal.maxBufferedLines`** (number) : Tampon de défilement maximum
  - Par défaut : `10000`
  - Affecte l’utilisation mémoire (~1 Mo pour 10 000 lignes)

- **`terminal.maxTerminals`** (number) : Sessions de terminal simultanées maximum
  - Par défaut : `10`
  - Chaque terminal utilise ~5-10 Mo de mémoire

### Paramètres du Système de Fichiers

- **`filesystem.maxFileSize`** (string) : Taille maximale de fichier pour lecture/écriture
  - Par défaut : `"10MB"`
  - Accepte : `"5MB"`, `"50MB"`, etc.

- **`filesystem.watchIgnorePatterns`** (string[]) : Modèles à exclure de la surveillance des fichiers
  - Par défaut : Ignore les sorties de build et les dépendances
  - Améliore les performances en évitant des milliers de fichiers générés

### Paramètres de Sécurité

- **`security.userAuthenticationEnabled`** (boolean) : Activer l’authentification utilisateur Firebase
  - Par défaut : `false`
  - Quand `false` : Latence réduite, compatible avec Lite, toujours protégé par la signature secrète
  - Quand `true` : Couche de sécurité supplémentaire, vérification d’identité utilisateur, ajoute 2-20s de latence initiale
  - **Toutes les requêtes sont toujours signées cryptographiquement indépendamment de ce paramètre**

## <a name="security"></a>Sécurité

### Connexions Chiffrées

Toute communication utilise :

- **WSS (WebSocket Secure)** : Chiffrement TLS/SSL
- **HTTPS** : Handshake initial chiffré

### Signature des Requêtes

Chaque requête est signée cryptographiquement :

- La clé secrète est générée localement, jamais transmise sur internet
- Il est recommandé de ne pas utiliser de scanners QR tiers qui pourraient exposer votre clé secrète

### Bonnes Pratiques

1. **Protéger les identifiants** :

   ```bash
   # Ajouter au .gitignore (automatique pendant la configuration)
   echo ".spck-editor/" >> .gitignore
   ```

2. **Se déconnecter sur les machines partagées** :

   ```bash
   spck --logout
   ```

3. **Limiter les répertoires exposés** :

   ```bash
   # Au lieu du répertoire home entier
   spck --root /path/to/specific/project
   ```

4. **Désactiver le terminal si non nécessaire** :

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **Désactiver le proxy navigateur si non nécessaire** :
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>Authentification Utilisateur

Spck CLI prend en charge l’authentification utilisateur Firebase optionnelle comme deuxième couche de sécurité en plus de la signature de requêtes toujours active.

### Fonctionnement

Lorsqu’elle est activée, la CLI nécessite de se connecter avec votre compte Spck Editor. Les connexions sont authentifiées à l’aide de tokens ID Firebase qui expirent toutes les heures et sont automatiquement renouvelés à l’aide de tokens de rafraîchissement sécurisés stockés dans `~/.spck-editor/.credentials.json`.

### Activer l’Authentification Utilisateur

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### Compromis

|                        | Désactivé (par défaut)        | Activé                                    |
| ---------------------- | ----------------------------- | ----------------------------------------- |
| **Protection**         | Clé de signature secrète      | + Vérification d’identité Firebase   |
| **Latence initiale**   | Pas de surcharge d’auth  | Ajoute 2–20s à la première connexion      |
| **Spck Editor Lite**   | ✅ Supporté                   | ❌ Non supporté                           |
| **Utilisation hors ligne** | Fonctionne sans internet  | Nécessite internet pour le renouvellement des tokens |

### Quand Activer

**Garder désactivé (par défaut) quand :**

- Utilisation de **Spck Editor Lite** — la connexion Firebase n’est pas supportée dans Lite ; mettre à `true` empêchera les utilisateurs Lite de se connecter
- Travail sur un réseau local ou un environnement de confiance où la clé de signature secrète est suffisante
- La minimisation de la latence de connexion est une priorité

**Activer quand :**

- La CLI est exposée sur un serveur accessible via internet
- Vous souhaitez la vérification d’identité utilisateur comme couche supplémentaire de contrôle d’accès au-delà de la clé de signature

> ⚠️ **Spck Editor Lite ne supporte pas l’authentification Firebase.** Si `userAuthenticationEnabled` est défini sur `true`, Spck Editor Lite ne peut pas se connecter. Gardez ce paramètre à `false` lors de l’utilisation de Lite.
