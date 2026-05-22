# Chiffrement, hachage et gestion des secrets

## Introduction

Avez-vous déjà écrit une lettre à un ami et hésité à la confier au
facteur, en imaginant qu'elle puisse être lue en chemin ? Pendant
des millénaires, les humains ont inventé des techniques pour
écrire des messages que seul le destinataire pouvait comprendre :
codes secrets des Égyptiens, machine Enigma des Allemands,
algorithmes modernes RSA et AES. Toute cette histoire repose sur
une idée simple : transformer un message clair en un message
incompréhensible pour quiconque ne possède pas la clé. C'est la
cryptographie, qui n'a jamais été aussi essentielle qu'à l'ère
numérique.

Cette partie aborde concrètement les techniques cryptographiques
que vous mobiliserez au quotidien. D'abord le chiffrement, sous
ses différentes formes (transit, repos, applicatif). Ensuite le
hachage, qui n'est pas un chiffrement mais une famille d'algorithmes
spécifiques pour les mots de passe et les empreintes. Enfin la
gestion des secrets en production, ce sujet trop souvent négligé
qui cause pourtant la majorité des fuites massives. Vous allez en
ressortir avec des choix techniques précis, à appliquer dès demain.

### Le chiffrement en transit avec TLS

Avez-vous déjà entendu le bruit caractéristique du modem 56k qui
établit une connexion ? À cette époque, on n'imaginait même pas
que la communication réseau puisse être chiffrée par défaut.
Aujourd'hui, transmettre des données personnelles sans chiffrement
serait inconcevable et juridiquement fautif. Le chiffrement en
transit est devenu une obligation de base, et TLS est devenu son
incarnation universelle.

TLS (Transport Layer Security) est le successeur de SSL. Il
fournit trois garanties cryptographiques fondamentales :

- **confidentialité** : personne ne peut lire les données
  échangées entre client et serveur ;
- **intégrité** : personne ne peut modifier les données en
  transit sans détection ;
- **authentification** : le client peut vérifier qu'il parle bien
  au bon serveur.

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Serveur
    Note over C,S: Handshake TLS 1.3

    C->>S: ClientHello + cles publiques
    S->>C: ServerHello + certificat
    Note over C: Validation du certificat<br/>via autorite de certification
    C->>S: Cles de session chiffrees
    Note over C,S: Communication chiffree avec<br/>AES-GCM ou ChaCha20-Poly1305

    C->>S: Donnees personnelles chiffrees
    S-->>C: Reponse chiffree
```

Quelques règles essentielles pour configurer TLS correctement :

- **Versions minimales** : TLS 1.2 acceptable, TLS 1.3 recommandé.
  TLS 1.0 et 1.1 sont obsolètes, à désactiver.
- **Suites cryptographiques** : préférer les suites AEAD
  (Authenticated Encryption with Associated Data) comme AES-GCM ou
  ChaCha20-Poly1305. Désactiver les algorithmes obsolètes (RC4,
  3DES).
- **Certificats** : utiliser des certificats Let's Encrypt
  (gratuits, renouvelés automatiquement) ou des certificats payants
  pour les cas plus exigeants. Surveiller leur expiration via du
  monitoring.
- **HSTS** : envoyer l'en-tête `Strict-Transport-Security` pour
  forcer le navigateur à toujours utiliser HTTPS.
- **HTTP/2 ou HTTP/3** : profiter de la migration TLS pour passer
  aux protocoles modernes, plus rapides et plus sûrs.

#### Exemple pratique {id="exemple-pratique-tls-1"}

Voici une configuration nginx moderne pour un site avec TLS 1.3
prioritaire et bonnes pratiques :

```nginx
server {
    listen 443 ssl http2;
    server_name app.example.com;

    # Certificats
    ssl_certificate /etc/letsencrypt/live/.../fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/.../privkey.pem;

    # Versions TLS : 1.2 et 1.3 uniquement
    ssl_protocols TLSv1.2 TLSv1.3;

    # Suites cryptographiques modernes (Mozilla intermediate)
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256;
    ssl_prefer_server_ciphers off;

    # Session tickets
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSLCache:10m;
    ssl_session_tickets off;

    # OCSP stapling pour la performance
    ssl_stapling on;
    ssl_stapling_verify on;

    # HSTS : forcer HTTPS pour 1 an
    add_header Strict-Transport-Security
        "max-age=31536000; includeSubDomains; preload"
        always;

    # Securite generale
    add_header X-Content-Type-Options nosniff always;
    add_header X-Frame-Options DENY always;
    add_header Referrer-Policy strict-origin-when-cross-origin
        always;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header X-Forwarded-Proto https;
    }
}

# Redirection HTTP vers HTTPS
server {
    listen 80;
    server_name app.example.com;
    return 301 https://$server_name$request_uri;
}
```

> **Note** : pour tester la qualité de votre configuration TLS,
> utilisez l'outil gratuit SSL Labs (ssllabs.com/ssltest). Vous
> devez viser une note A ou A+. Toute note inférieure révèle des
> faiblesses à corriger.

### Le chiffrement au repos

Vous avez sécurisé les communications avec TLS. Mais que se
passe-t-il quand quelqu'un vole physiquement le disque dur de votre
serveur, ou accède directement aux fichiers de la base de données ?
Le chiffrement au repos est la deuxième couche de protection : il
sécurise les données là où elles dorment, pas seulement là où
elles voyagent.

On distingue plusieurs niveaux de chiffrement au repos :

**Chiffrement de disque entier** (FDE - Full Disk Encryption) :
LUKS sur Linux, BitLocker sur Windows, FileVault sur macOS. Protège
en cas de vol physique du matériel. Transparent pour
l'application. Recommandation : systématique sur tous les serveurs
de production.

**Chiffrement de base de données** (TDE - Transparent Data
Encryption) : la base chiffre ses fichiers, ses logs de
transactions, ses sauvegardes. Disponible sur PostgreSQL (via
extensions), SQL Server (natif), Oracle (natif). Avantage :
transparent. Limite : un administrateur de base peut toujours lire
les données en clair.

**Chiffrement applicatif** : l'application chiffre les données
avant de les envoyer en base, déchiffre après lecture. Maximum de
sécurité (même un admin de base ne peut rien lire), mais complexité
accrue (recherche, indexation, performance).

```mermaid
flowchart TB
    App[Application]
    DB[Base de donnees]
    Disk[Stockage physique]

    App -->|Donnees claires| DB
    DB -->|Donnees chiffrees TDE| Disk
    Disk -->|Chiffrement FDE| HW[Hardware]

    App -.->|Option : chiffrement applicatif| DB

    Note1[Defense en profondeur :<br/>plusieurs couches]
```

Pour les **données les plus sensibles** (santé, finance,
authentification), le chiffrement applicatif est fortement
recommandé. Il complète, sans remplacer, les autres couches.

#### Exemple pratique {id="exemple-pratique-chiff-2"}

Voici un exemple de chiffrement applicatif avec rotation des clés,
appliqué à une colonne `medical_notes` sensible :

```javascript
// Module de chiffrement applicatif
// Utilise AES-256-GCM avec enveloppement de cles
const crypto = require('crypto');

class FieldCipher {
    constructor(kmsClient, currentKeyId) {
        this.kms = kmsClient;
        this.currentKeyId = currentKeyId;
    }

    // Chiffre un texte clair
    async encrypt(plaintext) {
        // Generation d une cle de donnees aleatoire
        const dataKey = crypto.randomBytes(32);
        const iv = crypto.randomBytes(12);

        // Chiffrement des donnees avec AES-256-GCM
        const cipher = crypto.createCipheriv(
            'aes-256-gcm', dataKey, iv
        );
        const ciphertext = Buffer.concat([
            cipher.update(plaintext, 'utf8'),
            cipher.final()
        ]);
        const authTag = cipher.getAuthTag();

        // Enveloppement : chiffrement de la cle par le KMS
        const wrappedKey = await this.kms.encrypt(
            this.currentKeyId, dataKey
        );

        // Stockage : enveloppement + IV + cipher + tag
        return {
            key_id: this.currentKeyId,
            wrapped_key: wrappedKey.toString('base64'),
            iv: iv.toString('base64'),
            ciphertext: ciphertext.toString('base64'),
            auth_tag: authTag.toString('base64')
        };
    }

    // Dechiffre un texte chiffre
    async decrypt(encryptedData) {
        // Dechiffrement de la cle via le KMS
        const dataKey = await this.kms.decrypt(
            encryptedData.key_id,
            Buffer.from(encryptedData.wrapped_key, 'base64')
        );

        // Dechiffrement des donnees
        const decipher = crypto.createDecipheriv(
            'aes-256-gcm',
            dataKey,
            Buffer.from(encryptedData.iv, 'base64')
        );
        decipher.setAuthTag(
            Buffer.from(encryptedData.auth_tag, 'base64')
        );

        return Buffer.concat([
            decipher.update(
                Buffer.from(encryptedData.ciphertext, 'base64')
            ),
            decipher.final()
        ]).toString('utf8');
    }
}
```

```sql
-- Schema accompagnant le chiffrement applicatif
CREATE TABLE patient_notes (
    id BIGINT PRIMARY KEY,
    patient_id BIGINT NOT NULL REFERENCES patients(id),

    -- Champ chiffre : JSON contenant tous les elements
    -- necessaires au dechiffrement
    encrypted_note JSON NOT NULL,

    -- Metadonnees lisibles (non sensibles)
    note_date DATE NOT NULL,
    author_id BIGINT NOT NULL REFERENCES users(id),
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

Avantages de ce modèle :

- une **clé différente** par enregistrement (impossible de tout
  déchiffrer avec une seule clé compromise) ;
- **rotation possible** des clés du KMS sans réchiffrer toutes les
  données ;
- **audit centralisé** des opérations de chiffrement/déchiffrement
  via le KMS ;
- **séparation** entre les clés (KMS) et les données (base) :
  compromettre l'un ne donne pas accès à l'autre.

### Le hachage des mots de passe

Quelle est la différence entre chiffrer et hacher ? Le chiffrement
est **réversible** (avec la clé) ; le hachage est **irréversible**
par conception. Pour stocker un mot de passe, on n'a pas besoin de
le retrouver, juste de vérifier qu'il correspond à celui qu'a saisi
l'utilisateur. Le hachage est parfait pour cela. Mais attention :
tous les algorithmes de hachage ne se valent pas, et certains
choix d'autrefois sont aujourd'hui catastrophiques.

**Algorithmes obsolètes (à NE PAS utiliser)** :

- MD5 : cassé depuis 1996, à proscrire absolument ;
- SHA-1 : cassé, à proscrire ;
- SHA-256 (sans dérivation lente) : trop rapide, vulnérable à
  l'attaque par force brute.

**Algorithmes acceptables (avec dérivation lente)** :

- bcrypt : éprouvé, bon compromis, paramètre de coût ajustable ;
- PBKDF2 : standard NIST, encore acceptable ;
- scrypt : conçu pour résister aux ASIC, bon choix.

**Algorithme recommandé en 2026** :

- **Argon2id** : vainqueur du Password Hashing Competition, conçu
  spécifiquement pour les mots de passe modernes, résistant aux
  GPU et ASIC. Recommandé par l'OWASP, le NIST, et la CNIL.

```mermaid
flowchart TB
    MP[Mot de passe<br/>en clair]
    Salt[Sel aleatoire<br/>16 octets unique]

    MP --> Comb[Concatenation]
    Salt --> Comb
    Comb --> Argon[Argon2id<br/>64 MiB, 3 iter,<br/>parallelisme 4]
    Argon --> Hash[Hash a stocker<br/>format PHC]

    Note1[PHC string :<br/>algo + params + sel<br/>+ hash combines]
```

Le format **PHC** (Password Hashing Competition string) est la
manière moderne de stocker un hash. Il contient dans une seule
chaîne : l'algorithme, ses paramètres, le sel, et le hash. Cela
permet de faire évoluer les paramètres dans le temps sans casser
la rétrocompatibilité.

Exemple de chaîne PHC Argon2id :

```
$argon2id$v=19$m=65536,t=3,p=4$c2FsdHNhbHRz...$hashedvaluehere...
```

Décomposition :

- `$argon2id$` : algorithme
- `v=19$` : version
- `m=65536` : 64 MiB de mémoire
- `t=3` : 3 itérations
- `p=4` : parallélisme 4
- `$c2FsdHNhbHRz...$` : sel en base64
- `$hashedvaluehere...` : hash final

#### Exemple pratique {id="exemple-pratique-hash-1"}

Voici une implémentation complète du hachage et de la vérification
de mot de passe avec Argon2id :

```javascript
const argon2 = require('argon2');

// Hachage a l inscription ou au changement de mot de passe
async function hashPassword(plainPassword) {
    // Verification que le mot de passe respecte les exigences
    if (plainPassword.length < 12) {
        throw new Error('Mot de passe trop court');
    }

    // Verification contre la liste des mots de passe compromis
    const isCompromised = await checkPasswordPwned(plainPassword);
    if (isCompromised) {
        throw new Error('Mot de passe trop frequent ou compromis');
    }

    // Hachage avec Argon2id et parametres recommandes
    const hash = await argon2.hash(plainPassword, {
        type: argon2.argon2id,
        memoryCost: 65536,
        timeCost: 3,
        parallelism: 4
    });

    return hash;
}

// Verification a la connexion
async function verifyPassword(storedHash, plainPassword) {
    try {
        const valid = await argon2.verify(storedHash, plainPassword);

        // Si l algorithme est obsolete, on rehache au passage
        if (valid && argon2.needsRehash(storedHash, {
            type: argon2.argon2id,
            memoryCost: 65536,
            timeCost: 3
        })) {
            const newHash = await hashPassword(plainPassword);
            return { valid: true, rehashed: newHash };
        }

        return { valid, rehashed: null };
    } catch (e) {
        return { valid: false, rehashed: null };
    }
}

// Verification contre HaveIBeenPwned
// (k-anonymat : on ne transmet que les 5 premiers caracteres du hash)
async function checkPasswordPwned(password) {
    const sha1Hash = crypto
        .createHash('sha1')
        .update(password)
        .digest('hex')
        .toUpperCase();

    const prefix = sha1Hash.substring(0, 5);
    const suffix = sha1Hash.substring(5);

    const response = await fetch(
        `https://api.pwnedpasswords.com/range/${prefix}`
    );
    const text = await response.text();

    return text.split('\n').some(line => {
        return line.startsWith(suffix);
    });
}
```

#### Exercice 1

Une application existante utilise SHA-256 (sans sel, sans
itérations) pour stocker les mots de passe utilisateurs. Vous êtes
chargé de la moderniser vers Argon2id. Décrivez votre stratégie de
migration sans interruption de service et sans demander à tous les
utilisateurs de changer leur mot de passe.

##### Correction exercice 1 {collapsible="true"}

**Stratégie de migration transparente**

L'approche recommandée est une **migration différée** lors des
connexions successives, sans rupture pour les utilisateurs :

**Phase 1 - Préparation** :

- Ajouter une colonne `password_hash_version` dans la table users,
  valant `legacy` par défaut.
- Ajouter Argon2id comme dépendance applicative, configurer le
  KMS si nécessaire.
- Tester en environnement de staging.

**Phase 2 - Migration au login** :

- À chaque connexion réussie, vérifier la version du hash stocké :
  - Si `legacy` (SHA-256) : vérifier le mot de passe avec
    SHA-256, puis re-hacher avec Argon2id et mettre à jour le
    champ + passer la version à `argon2id_v1`.
  - Si `argon2id_v1` : vérification standard avec Argon2id.

```javascript
async function loginWithMigration(email, plainPassword) {
    const user = await db.users.findByEmail(email);

    if (user.password_hash_version === 'legacy') {
        // Verification SHA-256 legacy
        const sha256 = computeLegacyHash(plainPassword);
        if (sha256 !== user.password_hash) {
            return { success: false };
        }

        // Migration immediate vers Argon2id
        const newHash = await hashPassword(plainPassword);
        await db.users.update(user.id, {
            password_hash: newHash,
            password_hash_version: 'argon2id_v1'
        });

        return { success: true, migrated: true };
    }

    // Verification Argon2id standard
    const { valid } = await verifyPassword(
        user.password_hash, plainPassword
    );
    return { success: valid };
}
```

**Phase 3 - Échéance pour les comptes inactifs** :

Au bout de 6 à 12 mois, les utilisateurs qui ne se sont jamais
reconnectés restent en `legacy`. Plusieurs options :

- envoyer un email de prévenance avec un lien pour se reconnecter
  (incitation douce) ;
- forcer une réinitialisation pour les comptes restant en
  `legacy` au-delà d'un certain délai (sécurité prime).

**Phase 4 - Suppression du code legacy** :

Une fois la quasi-totalité des comptes migrés, supprimer le code
de vérification SHA-256. Documenter l'opération.

**Bénéfices** :

- aucune perturbation pour les utilisateurs actifs ;
- migration progressive et transparente ;
- traçabilité (qui est migré, qui ne l'est pas) ;
- montée en sécurité naturelle.

### La gestion des secrets

Connaissez-vous l'histoire de ce développeur qui a publié sur GitHub
un fichier de configuration contenant ses clés AWS, et qui a vu son
compte cloud facturé de 50 000 dollars en quelques heures par des
mineurs de cryptomonnaie ? Cette histoire, racontée par dizaines,
illustre un problème majeur : la **gestion des secrets** en
production est souvent le maillon faible de la sécurité, et les
conséquences sont brutales.

Un **secret** est une donnée sensible nécessaire à
l'authentification ou au chiffrement : clé d'API, mot de passe de
base de données, certificat privé, clé de chiffrement. Ces données
ne doivent **jamais** apparaître :

- dans le **code source** committé dans Git ;
- dans les **logs** d'application ;
- dans les **messages d'erreur** envoyés au client ;
- dans les **URL** ou les **headers HTTP** accessibles.

Quelques bonnes pratiques pour gérer les secrets :

**Variables d'environnement** : le minimum vital pour séparer code
et secrets. Les secrets sont injectés au démarrage du processus.
Configuration distincte par environnement (dev, staging, prod).

**Fichiers `.env` (en développement)** : ajoutés à `.gitignore`,
jamais committés. Un fichier `.env.example` documente les variables
attendues sans contenir les valeurs réelles.

**Gestionnaires de secrets centralisés (en production)** :
HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, Google
Secret Manager, Bitwarden Secrets Manager. Avantages : rotation
automatique, journalisation des accès, contrôle d'accès fin.

**Sécurité au runtime** : les secrets ne sont chargés en mémoire
que lorsqu'ils sont nécessaires, jamais exposés aux processus
voisins, et purgés rapidement.

```mermaid
flowchart TB
    Dev[Developpement local]
    Prod[Production]

    Dev --> EnvFile[Fichier .env<br/>dans gitignore]
    Dev --> Sample[.env.example<br/>committe en exemple]

    Prod --> Vault[Vault centralise<br/>HashiCorp / AWS / Azure]
    Prod --> Inject[Injection au demarrage]

    Vault --> Rot[Rotation periodique]
    Vault --> Audit[Audit des acces]
    Vault --> ACL[Controle fin par service]
```

#### Exemple pratique {id="exemple-pratique-secrets-1"}

Voici un exemple de structure de configuration avec variables
d'environnement et validation :

```javascript
// config/env.js : chargement et validation des secrets
const z = require('zod');
require('dotenv').config();

// Schema de validation : toutes les variables sont obligatoires
const envSchema = z.object({
    NODE_ENV: z.enum(['development', 'staging', 'production']),
    DATABASE_URL: z.string().url(),
    JWT_SIGNING_KEY: z.string().min(32),
    ENCRYPTION_KEY_ID: z.string(),
    SMTP_PASSWORD: z.string().min(8),
    SENTRY_DSN: z.string().url().optional()
});

// Validation au demarrage
let env;
try {
    env = envSchema.parse(process.env);
} catch (e) {
    console.error('Configuration invalide :', e.errors);
    process.exit(1);
}

// Export ne contient JAMAIS le contenu en clair
// (uniquement le statut presence/absence)
module.exports = {
    env,
    isProduction: env.NODE_ENV === 'production'
};
```

```
# .env.example : a committer (sans les vraies valeurs)
NODE_ENV=development
DATABASE_URL=postgres://user:password@localhost:5432/mydb
JWT_SIGNING_KEY=changeme_minimum_32_characters_secret
ENCRYPTION_KEY_ID=local-dev-key
SMTP_PASSWORD=changeme
SENTRY_DSN=
```

```
# .gitignore : a verifier rigoureusement
.env
.env.local
.env.production
*.pem
*.key
secrets/
```

#### Exercice 2

Vous découvrez en faisant un audit qu'un développeur a poussé sur
GitHub, il y a deux mois, un fichier de configuration contenant
les credentials de votre base de données de production. Décrivez
le plan d'action en urgence et les mesures préventives à mettre en
place pour éviter que cela se reproduise.

##### Correction exercice 2 {collapsible="true"}

**Plan d'action en urgence**

1. **Considérer les secrets comme compromis** (même si le commit
   a depuis été supprimé). Une donnée publiée sur GitHub peut être
   indexée, copiée, archivée. La suppression du commit ne suffit
   pas.

2. **Faire tourner immédiatement tous les secrets exposés** :
   - changer les mots de passe de la base de données ;
   - révoquer et régénérer les clés d'API ;
   - changer les clés de chiffrement (si exposées, anticiper le
     déchiffrement et re-chiffrement des données concernées) ;
   - faire tourner les certificats si exposés.

3. **Vérifier les logs d'accès** : la base de données a-t-elle eu
   des connexions inhabituelles depuis l'exposition ? Quelles IP ?
   Quelles requêtes ? Recherche d'indices de compromission
   effective.

4. **Évaluer la nature et l'ampleur d'une violation potentielle** :
   - si les credentials ont permis un accès non autorisé à des
     données personnelles, c'est une **violation au sens de
     l'article 33**, à notifier à la CNIL sous 72 heures.
   - documenter rigoureusement la chronologie pour la procédure.

5. **Nettoyer le dépôt Git** : utiliser `git filter-repo` ou BFG
   Repo-Cleaner pour réécrire l'historique. Mais sachant que le
   secret est probablement déjà copié ailleurs, cela ne dispense
   pas de la rotation.

**Mesures préventives**

1. **Pre-commit hooks** : installer un outil comme `gitleaks` ou
   `git-secrets` qui scanne les commits avant push pour détecter
   des patterns de secrets (clés API, mots de passe, certificats).

2. **CI/CD avec scan de secrets** : configurer le pipeline pour
   échouer le build si des secrets sont détectés.

3. **Vault centralisé** : migrer toute la gestion des secrets vers
   un gestionnaire dédié (HashiCorp Vault, AWS Secrets Manager).
   Les développeurs ne manipulent plus les secrets directement.

4. **Politique de revue de code** : aucun commit n'arrive en main
   sans revue par un pair. La revue inclut une vérification
   explicite de l'absence de secrets.

5. **Formation de l'équipe** : sensibilisation régulière au sujet
   des secrets, partage des incidents (en interne), mise à jour
   des bonnes pratiques.

6. **Audit régulier** : balayage automatique du dépôt à intervalles
   réguliers pour détecter les secrets qui auraient échappé aux
   filtres.

7. **Documentation des incidents** : tenir un registre des incidents
   de sécurité internes, même mineurs, pour apprendre
   collectivement.

## Exercice final

Vous êtes développeur senior dans une fintech française, *PayLink*,
qui propose une solution de paiement par lien envoyé par SMS. Le
système gère : authentification des marchands, données de cartes
bancaires (en réalité tokenisées via un PSP), historiques de
transactions, conversations entre marchands et clients en cas de
litige. La direction vous demande de produire la **politique
cryptographique** complète de l'application.

Rédigez un document structuré couvrant :

1. **Chiffrement en transit** : protocoles, suites, configuration
   serveur.
2. **Chiffrement au repos** : niveaux mobilisés, données concernées,
   gestion des clés.
3. **Hachage des mots de passe** : algorithme, paramètres, politique
   de migration future.
4. **Gestion des secrets** : architecture, vault choisi, rotation,
   contrôle d'accès.
5. **Audit cryptographique** : tests réguliers, indicateurs de
   conformité, plan de rotation.

### Correction exercice final {collapsible="true"}

**Politique cryptographique — PayLink**

**1. Chiffrement en transit**

- **Protocoles** : TLS 1.2 minimum, TLS 1.3 par défaut. Les
  versions antérieures sont désactivées sur tous les serveurs et
  équilibreurs de charge.
- **Suites cryptographiques** : suites AEAD uniquement (AES-GCM,
  ChaCha20-Poly1305). Configuration Mozilla « intermediate »
  pour la compatibilité avec les anciens navigateurs ; configuration
  « modern » sur les API internes.
- **Certificats** : Let's Encrypt avec renouvellement automatique
  (certbot) pour les services web standard. Certificats payants
  (DigiCert, Sectigo) pour les services critiques avec besoin
  d'EV.
- **HSTS** : max-age 1 an, includeSubDomains, preload.
- **Tests** : tests SSL Labs mensuels, objectif note A+ minimum.

**2. Chiffrement au repos**

| Données | Niveau | Technique |
|---------|--------|-----------|
| Tous serveurs | FDE | LUKS / dm-crypt |
| Bases de données | TDE | PostgreSQL TDE |
| Cartes bancaires | Tokenisé via PSP | Pas de stockage chez nous |
| Identités marchands | Applicatif | AES-256-GCM via KMS |
| Conversations | Applicatif | AES-256-GCM via KMS |
| Logs | TDE seul | Pseudonymisation au préalable |
| Sauvegardes | AES-256 + clés séparées | Rotation 90 jours |

**Gestion des clés** :

- HSM cloud (AWS CloudHSM ou équivalent) pour les clés racines.
- KMS managé (AWS KMS) pour les clés dérivées.
- Enveloppement de clés : chaque enregistrement chiffré avec sa
  propre clé, elle-même chiffrée par le KMS.
- Rotation annuelle des clés racines, rotation trimestrielle des
  clés dérivées (sans réchiffrement des données existantes grâce
  à l'enveloppement).
- Procédure documentée de récupération en cas de perte de clé
  (escrow chez deux dirigeants).

**3. Hachage des mots de passe**

- **Algorithme** : Argon2id (recommandation NIST/OWASP/CNIL).
- **Paramètres initiaux** :
  - mémoire : 65 536 KiB (64 MiB) ;
  - itérations : 3 ;
  - parallélisme : 4 ;
  - longueur du sel : 16 octets aléatoires ;
  - longueur du hash : 32 octets.
- **Format de stockage** : chaîne PHC complète dans la base.
- **Vérification de la qualité** : intégration de la base
  HaveIBeenPwned (k-anonymat) au moment du choix du mot de passe.
- **Politique** :
  - longueur minimale 12 caractères ;
  - pas d'exigence de complexité forcée ;
  - pas d'expiration sauf compromission ;
  - blocage des mots de passe compromis.
- **Migration future** : si Argon2id devient obsolète, migration
  transparente au login via `needsRehash`.

**4. Gestion des secrets**

- **Vault central** : HashiCorp Vault Enterprise auto-hébergé dans
  l'UE.
- **Architecture** :
  - chaque service applicatif possède un compte Vault dédié ;
  - authentification via méthode AppRole (RoleID + SecretID) ;
  - chargement des secrets au démarrage du service ;
  - renouvellement automatique des leases.
- **Contrôle d'accès** : politiques Vault fines par service. Un
  service n'a accès qu'aux secrets dont il a besoin.
- **Rotation** :
  - mots de passe BDD : rotation tous les 90 jours, automatique
    via Vault Database Secrets Engine ;
  - clés API : rotation tous les 6 mois ;
  - certificats : renouvellement automatique avant 30 jours
    d'expiration.
- **Audit** : tous les accès Vault sont journalisés et envoyés au
  SIEM. Anomalies détectées par alertes automatiques.
- **Développement local** : fichiers `.env` jamais committés,
  `.env.example` documenté. Pre-commit hook `gitleaks` obligatoire.

**5. Audit cryptographique**

| Test | Fréquence | Responsable |
|------|-----------|-------------|
| SSL Labs (TLS) | Mensuel automatique | DevOps |
| Scan de secrets dans Git | Hebdomadaire | CI/CD |
| Pen-test externe | Annuel | Auditeur tiers |
| Audit du KMS | Trimestriel | RSSI |
| Revue des rôles Vault | Trimestrielle | RSSI |
| Vérification expiration certificats | Continue | Monitoring |
| Test de restauration sauvegardes | Mensuel | DevOps |

**Indicateurs de conformité (KPI)** :

- taux d'erreurs de chiffrement < 0,01 % ;
- 100 % des connexions externes en TLS 1.3 ou 1.2 ;
- 0 secret détecté dans le dépôt Git lors des scans ;
- 100 % des clés dans leur fenêtre de validité ;
- temps de rotation moyen des secrets < 90 jours.

**Plan de rotation prévisionnel** :

```mermaid
gantt
    title Plan de rotation cryptographique annuel
    dateFormat YYYY-MM-DD
    section Cles
    Cles racines HSM       :2026-01-01, 365d
    Cles derivees KMS      :2026-01-01, 90d
    Cles applicatives      :2026-01-01, 90d
    section Secrets
    Mots de passe BDD      :2026-01-01, 90d
    Cles API internes      :2026-01-01, 180d
    Cles API externes      :2026-01-01, 365d
    section Certificats
    TLS Let s Encrypt      :2026-01-01, 60d
```

Ce document constitue la référence cryptographique de *PayLink*. Il
est revu annuellement par le RSSI et le CTO, et plus fréquemment
si de nouvelles vulnérabilités cryptographiques apparaissent dans
le paysage.

## Conclusion de la partie

Vous disposez désormais d'une vraie maîtrise des techniques
cryptographiques applicatives. Vous savez configurer TLS
correctement, déployer le chiffrement au repos à plusieurs niveaux,
hacher les mots de passe avec un algorithme moderne (Argon2id), et
gérer les secrets en production via un vault centralisé.

Retenez ces principes incontournables :

- TLS 1.2 ou 1.3 partout, sans exception ;
- chiffrement applicatif pour les données les plus sensibles, en
  complément du TDE et du FDE (défense en profondeur) ;
- Argon2id pour les mots de passe, avec migration transparente
  depuis tout algorithme legacy ;
- aucun secret dans le code source, jamais ;
- rotation périodique de tous les secrets, avec automatisation
  autant que possible.

La cryptographie est un domaine en évolution permanente. Les
algorithmes recommandés aujourd'hui pourraient être affaiblis
demain. La règle d'or : rester informé, prévoir des mécanismes de
migration, et auditer régulièrement. La partie suivante explorera
la sécurité du code lui-même, à travers une lecture critique de
l'OWASP Top 10 et la gestion des dépendances.
