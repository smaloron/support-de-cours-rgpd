# TP : Audit de sécurité et simulation de violation

## Introduction

### Contexte du TP

Vous venez d'être recruté comme **développeur sécurité** chez
*MediCare+*, jeune startup française qui édite une application web
de téléconsultation médicale et de suivi patient. La société
compte 12 personnes et environ 25 000 utilisateurs actifs
(patients et professionnels de santé). L'application est en
production depuis 18 mois ; elle a été développée rapidement par
deux développeurs externes et reprise en interne il y a 6 mois.

Votre première mission consiste à conduire un **audit complet de
sécurité** sur l'application, à identifier les faiblesses, à
proposer un plan de remédiation, et à mettre à l'épreuve la
capacité de l'équipe à gérer un incident en simulant une violation
de données.

L'application traite des **données de santé** (article 9 du
RGPD), ce qui implique des exigences renforcées. Toute faille peut
avoir des conséquences réputationnelles, juridiques et humaines
considérables. Votre intervention est attendue avec impatience
par la direction, qui a déjà subi un quasi-incident il y a deux
mois (alerte de sécurité d'un client) et veut éviter qu'il s'en
produise un réel.

### Objectifs du TP

À l'issue de ce TP, vous serez capable de :

1. Conduire un audit de sécurité systématique d'une application
   web en mobilisant l'OWASP Top 10 sous l'angle RGPD.
2. Identifier les vulnérabilités d'authentification, de
   cryptographie, de contrôle d'accès, et de gestion des secrets.
3. Hiérarchiser et planifier un plan de remédiation réaliste sur
   plusieurs sprints.
4. Simuler la gestion d'un incident de violation de données en
   appliquant les procédures des articles 33 et 34.
5. Produire une notification CNIL conforme et un email
   d'information aux personnes concernées.

### Durée estimée

Environ **6 heures** (peut être étendu à 8 heures avec
restitution orale ou exercice complet de cellule de crise).

### Prérequis techniques

- Avoir lu intégralement les parties 1 à 4 du module.
- Connaître l'OWASP Top 10 et ses principales catégories.
- Maîtriser SQL (compatible MySQL et PostgreSQL) et JavaScript
  (Node.js).
- Notion d'architecture web (frontend / backend / base de données).
- Idéalement, avoir manipulé un outil d'audit comme Snyk, npm
  audit, ou OWASP ZAP.

## Étape 1 : Audit du code et des configurations

### 1.1 Lecture critique de l'application

Vous découvrez un code source qui présente plusieurs problèmes
inquiétants. Pour chaque extrait de code ci-dessous, identifiez la
vulnérabilité, indiquez le risque RGPD correspondant, et proposez
la correction.

**Extrait 1 - Authentification**

```javascript
async function login(req, res) {
    const { email, password } = req.body;
    const user = await db.users.findOne({ email });

    // Comparaison directe : faille critique
    if (user && user.password === md5(password)) {
        const token = jwt.sign(
            { id: user.id, email: user.email, role: user.role },
            'SECRET123',
            { expiresIn: '30d' }
        );
        res.json({ token });
    } else {
        res.json({ error: 'Identifiants invalides' });
    }
}
```

**Extrait 2 - Endpoint d'export**

```javascript
app.get('/api/patients/:id/export', async (req, res) => {
    const patientId = req.params.id;
    const patient = await db.query(
        `SELECT * FROM patients WHERE id = ${patientId}`
    );
    res.json(patient);
});
```

**Extrait 3 - Configuration**

```javascript
// config.js
module.exports = {
    db_host: 'prod-db.medicare.fr',
    db_user: 'medicare_admin',
    db_password: 'M3d1Care2024!',
    jwt_secret: 'SECRET123',
    smtp_password: 'sendgrid_api_key_xxxxx'
};
```

**Extrait 4 - Route de recherche**

```javascript
app.get('/api/search/patients', async (req, res) => {
    const term = req.query.q;
    const sql = `
        SELECT id, name, dob, phone
        FROM patients
        WHERE name LIKE '%${term}%' OR phone LIKE '%${term}%'
    `;
    const results = await db.query(sql);
    res.json(results);
});
```

**Extrait 5 - Reset password**

```javascript
app.post('/api/reset-password', async (req, res) => {
    const { email } = req.body;
    const user = await db.users.findOne({ email });

    if (user) {
        const newPassword = generateRandomString(8);
        await db.users.update(user.id, {
            password: md5(newPassword)
        });
        await sendEmail(email,
            `Votre nouveau mot de passe : ${newPassword}`);
        res.json({ success: true });
    } else {
        res.json({ error: 'Email inconnu' });
    }
});
```

Pour chaque extrait, produisez une analyse structurée :

- **Vulnérabilité identifiée** : catégorie OWASP.
- **Risque RGPD** : conséquence si exploitée.
- **Gravité** : faible / moyenne / élevée / critique.
- **Correction proposée** : code corrigé avec explications.

### 1.2 Audit des dépendances

L'application est en Node.js. Le `package.json` contient :

```json
{
  "dependencies": {
    "express": "4.16.0",
    "mongoose": "5.0.0",
    "jsonwebtoken": "8.5.0",
    "lodash": "4.17.10",
    "bcryptjs": "2.4.3",
    "moment": "2.24.0",
    "request": "2.88.0",
    "node-fetch": "2.6.0"
  }
}
```

Analysez ces dépendances :

- Quelles bibliothèques sont obsolètes ou abandonnées ?
- Quelles ont des CVE connus à corriger ?
- Quelles alternatives modernes recommandez-vous ?
- Quelle politique mettre en place pour éviter ce retard à l'avenir ?

### 1.3 Audit du dépôt Git

Vous découvrez en examinant le dépôt Git :

- un fichier `.env.production` versionné depuis 6 mois ;
- un commit ancien qui contenait un dump de base de données pour
  tester en local (10 000 patients fictifs mais structure réelle) ;
- des credentials AWS dans un commentaire de code (`// pour
  debug en local`).

Décrivez votre plan d'action complet :

- mesures immédiates ;
- nettoyage du dépôt ;
- prévention de la récidive ;
- évaluation de l'éventuelle violation RGPD.

## Étape 2 : Plan de remédiation

### 2.1 Hiérarchisation des actions

Sur la base de votre audit (étape 1) et des éléments
complémentaires suivants :

- pas de MFA en place, même pour les médecins ;
- aucun audit trail des accès aux dossiers patients ;
- sauvegardes manuelles, jamais testées en restauration ;
- pas de TLS sur l'API interne (HTTPS uniquement sur le frontend) ;
- pas de WAF ni de protection DDoS ;
- pas de monitoring de sécurité (pas de SIEM, pas d'alertes).

Établissez le plan de remédiation complet, organisé par priorité
(P0 / P1 / P2 / P3) et avec un calendrier sur 6 mois.

Présentez sous forme de tableau :

| Mesure | Priorité | Sprint | Complexité | Risque RGPD |
|--------|----------|--------|------------|-------------|

### 2.2 Politique de sécurité

Rédigez une **politique de sécurité** pour MediCare+, qui
couvrira :

1. Authentification (mots de passe, MFA, sessions).
2. Cryptographie (TLS, chiffrement au repos, secrets).
3. Contrôle d'accès (RBAC, principe du moindre privilège).
4. Journalisation et audit trail.
5. Sauvegardes et continuité d'activité.
6. Gestion des incidents.
7. Formation et sensibilisation des équipes.

Ce document constituera le cadre opérationnel de la sécurité de
l'entreprise.

### 2.3 Schéma SQL d'audit trail

Concevez le schéma SQL complet (compatible MySQL et PostgreSQL)
pour l'audit trail de l'application MediCare+. Il devra notamment
permettre de répondre aux questions :

- qui a consulté quel dossier patient, et quand ?
- qui a effectué une exportation de données, et de quel volume ?
- qui a modifié les permissions d'un autre utilisateur, et quand ?
- y a-t-il eu des tentatives d'accès à des dossiers en dehors de
  la patientèle déclarée ?

## Étape 3 : Simulation de violation

### 3.1 Le scénario

Trois mois après votre prise de poste, vos améliorations sont en
cours mais pas toutes appliquées. Un jeudi à 16h, vous recevez une
alerte de votre nouveau système de monitoring : un compte
administrateur, normalement utilisé uniquement par le DPO en
journée, vient de réaliser à 16h05 un **export massif de la base
patients**. Le DPO est en réunion externe et n'a pas pu être
contacté immédiatement. L'export concerne 8 500 dossiers patients
(nom, prénom, date de naissance, numéro de sécurité sociale,
antécédents médicaux).

L'analyse des logs révèle :

- la connexion provient d'une IP localisée à l'étranger ;
- l'authentification a réussi du premier coup (pas de force
  brute) ;
- l'export a duré 12 minutes ;
- le DPO n'a pas effectué cette action.

À 16h30, le DPO confirme par téléphone qu'il n'est pas à l'origine
de l'export et que ses identifiants ont peut-être été compromis.

### 3.2 Action 1 : Réponse en temps réel

Décrivez votre plan d'action heure par heure pour les 24 premières
heures, en précisant :

- les actions techniques immédiates (containment) ;
- l'investigation (forensics) ;
- la communication interne ;
- les décisions de qualification de la violation ;
- la préparation des notifications.

### 3.3 Action 2 : Notification CNIL

Rédigez la **notification CNIL** complète à envoyer dans le délai
légal. Reprenez tous les éléments de l'article 33.3.

### 3.4 Action 3 : Information des personnes concernées

Rédigez l'**email d'information** à envoyer aux 8 500 patients
concernés, en mobilisant les bonnes pratiques de la partie 4 :
clair, factuel, actionnable, transparent.

### 3.5 Action 4 : Post-mortem

Une fois la crise gérée, conduisez le post-mortem. Identifiez :

- les causes racines (pourquoi la violation est-elle survenue ?) ;
- les facteurs aggravants (pourquoi a-t-elle pu durer 12 minutes ?) ;
- les leçons à tirer ;
- les améliorations à apporter au plan de réponse aux incidents.

### 3.6 Action 5 : Documentation pour le registre

Rédigez la **fiche d'inscription au registre des violations** pour
cet incident.

## Étape 4 : Document de synthèse

Compilez l'ensemble de votre travail en un **rapport d'audit et de
réponse à incident** qui pourra être présenté au COMEX. Le rapport
doit comporter :

1. Synthèse exécutive (1 page).
2. Constat de l'audit initial : forces et faiblesses.
3. Plan de remédiation détaillé et calendrier.
4. Politique de sécurité applicable.
5. Récit de la simulation d'incident et démonstration de la
   capacité à gérer une vraie violation.
6. Recommandations à moyen terme : audit externe, formation,
   investissements.
7. Indicateurs de suivi proposés (KPI).

## Correction du TP {collapsible="true"}

Cette correction présente une réponse type. Le TP est très étendu :
il est attendu que l'apprenant ne fournisse pas tout en détail,
mais qu'il démontre une maîtrise structurée sur l'ensemble des
sujets.

### Étape 1.1 : Analyse des extraits

**Extrait 1 - Authentification**

- *Vulnérabilité* : Cryptographic Failures (A02) + Authentication
  Failures (A07).
- *Risques* : MD5 cassé depuis longtemps + comparaison directe
  vulnérable au timing + JWT signé avec un secret faible et
  expiration trop longue + email/role dans le JWT (élargit
  l'attaque si compromission) + pas de protection contre la force
  brute.
- *Gravité* : critique.
- *Correction* : Argon2id pour le hash, secret JWT robuste (32+
  caractères, hors code), expiration courte (15 min) + refresh
  token, rate limiting, MFA pour les rôles sensibles.

**Extrait 2 - Endpoint d'export**

- *Vulnérabilité* : Injection (A03) + Broken Access Control (A01).
- *Risques* : injection SQL trivialement exploitable +
  aucun contrôle que l'utilisateur a le droit de voir ce patient.
- *Gravité* : critique.
- *Correction* : requête paramétrée + middleware d'autorisation
  qui vérifie le lien médecin-patient + journalisation de chaque
  export.

**Extrait 3 - Configuration**

- *Vulnérabilité* : Cryptographic Failures (A02) + Security
  Misconfiguration (A05).
- *Risques* : secrets en clair dans le code, susceptibles d'être
  committés et de fuiter. Pour une application de santé, c'est
  une faute caractérisée.
- *Gravité* : critique.
- *Correction* : variables d'environnement, idéalement vault
  centralisé. `.env` ajouté à `.gitignore`. Rotation immédiate
  des secrets exposés.

**Extrait 4 - Recherche**

- *Vulnérabilité* : Injection (A03) + exposition excessive
  (potentielle).
- *Risques* : injection SQL, énumération possible des patients,
  pas de pagination, pas de limite.
- *Gravité* : élevée.
- *Correction* : ORM ou requête paramétrée + ACL (qui peut
  rechercher ?) + pagination + rate limiting + logs d'audit pour
  toute recherche.

**Extrait 5 - Reset password**

- *Vulnérabilité* : Authentication Failures (A07).
- *Risques* : envoi du mot de passe en clair par email
  (interception, fuite), reset effectif même sans confirmation
  (DoS du compte), longueur insuffisante.
- *Gravité* : élevée.
- *Correction* : envoi d'un **lien de reset** à usage unique
  expirant en 30 minutes. L'utilisateur choisit lui-même son
  nouveau mot de passe via le lien. Pas de stockage en clair.
  Réponse identique que l'email existe ou non (anti-énumération).

### Étape 1.2 : Dépendances

- *express 4.16.0* : ancien (version actuelle 4.19+), CVE
  connues. À mettre à jour.
- *mongoose 5.0.0* : très ancien (6.x est la version stable).
  Risques cumulés.
- *jsonwebtoken 8.5.0* : CVE majeur (CVE-2022-23529 sur la
  vérification). Mise à jour critique vers 9.0+.
- *lodash 4.17.10* : CVE de prototype pollution. Mise à jour
  immédiate vers 4.17.21+.
- *bcryptjs 2.4.3* : encore acceptable, mais migration vers
  argon2 recommandée pour la santé.
- *moment 2.24.0* : bibliothèque en maintenance uniquement. À
  remplacer par date-fns ou day.js.
- *request 2.88.0* : **abandonnée** depuis 2020. À remplacer par
  fetch natif Node 18+ ou axios/got.
- *node-fetch 2.6.0* : ancien, version 3+ disponible.

**Politique recommandée** :

- Dependabot ou Renovate activé ;
- `npm audit` dans le CI/CD avec échec si niveau élevé ;
- mises à jour mensuelles regroupées ;
- revue trimestrielle des dépendances avec décision sur les
  abandons.

### Étape 1.3 : Dépôt Git

**Mesures immédiates** :

- considérer tous les secrets exposés comme compromis ;
- rotation immédiate de tous les credentials (BDD, AWS, etc.) ;
- audit des logs d'accès AWS pour détecter d'éventuels usages
  malveillants ;
- vérifier si le dump de base contenait des données réelles ou
  fictives (information cruciale pour la qualification d'une
  violation).

**Nettoyage du dépôt** :

- réécrire l'historique Git (`git filter-repo` ou BFG) pour
  supprimer les fichiers sensibles ;
- mais ne pas se fier à cela : Git distribué = secrets déjà
  potentiellement copiés.

**Prévention** :

- pre-commit hook `gitleaks` ;
- scan CI/CD ;
- formation équipe ;
- audit régulier du dépôt.

**Évaluation RGPD** :

- si le dump contient des données réelles : c'est une fuite
  potentielle dès la publication du dépôt. Évaluer accessibilité
  du dépôt (privé ? clonage par tiers ?). Si potentiellement
  exposé : violation à notifier.

### Étape 2 : Plan de remédiation {id="tape-2-plan-de-rem-diation_1"}

**Plan priorisé** :

| Mesure | Priorité | Sprint | Complexité | Risque |
|--------|----------|--------|------------|--------|
| Rotation secrets exposés | P0 | 1 | Faible | Critique |
| Migration MD5 → Argon2id | P0 | 1-2 | Moyenne | Critique |
| Correction injections SQL | P0 | 1 | Moyenne | Critique |
| Mise à jour dépendances critiques | P0 | 1 | Faible | Critique |
| TLS sur API interne | P0 | 1 | Faible | Élevé |
| MFA obligatoire médecins | P1 | 2 | Moyenne | Élevé |
| RBAC complet | P1 | 2-3 | Élevée | Élevé |
| Audit trail | P1 | 2-3 | Moyenne | Élevé |
| Vault centralisé | P1 | 3 | Élevée | Élevé |
| Sauvegardes automatisées | P1 | 3 | Moyenne | Élevé |
| Tests restauration | P2 | 4 | Moyenne | Moyen |
| WAF + protection DDoS | P2 | 4-5 | Moyenne | Moyen |
| SIEM et monitoring | P2 | 5 | Élevée | Moyen |
| AIPD complète | P2 | 4-5 | Élevée | Conformité |
| Audit externe annuel | P3 | 6 | Faible | Conformité |
| Formation équipe | P3 | Continu | Faible | Conformité |

### Étape 3 : Simulation d'incident

**Réponse heure par heure (extrait)** :

*16h00 - 16h30 - Détection* : alerte du SIEM, vérification par
le développeur d'astreinte, confirmation de l'anomalie, contact
DPO et CTO.

*16h30 - 17h30 - Containment* : désactivation immédiate du
compte DPO, révocation de toutes ses sessions, blocage de l'IP
source, snapshot des bases pour forensics, vérification d'absence
d'autres comptes compromis.

*17h30 - 19h00 - Investigation* : analyse des logs sur les
30 derniers jours du compte DPO (chercher les indices de
compromission), vérification des données exportées (nature,
volume confirmé), identification des vecteurs possibles
(phishing récent ? credentials sur HaveIBeenPwned ?).

*19h00 - 22h00 - Qualification et préparation* : confirmation
que c'est une violation au sens de l'article 33. Risque élevé
en raison de la nature (données de santé, NIR) et du volume.
Décision : notification CNIL en cours + information des
personnes concernées sous 24 à 48h.

*Vendredi 09h00 - 12h00 - Notifications* : envoi de la
notification CNIL (largement dans les 72h, dès le lendemain de
la prise de connaissance). Préparation de l'envoi aux patients
concernés.

*Vendredi 14h00 - 18h00 - Information* : envoi des emails aux
8 500 patients. Communication interne et préparation d'un
communiqué de presse en cas de relais médiatique.

**Notification CNIL** : structurée selon l'article 33.3 (cf.
modèle de la partie 4). Insister sur la nature santé (article 9),
le volume, et les mesures immédiates prises.

**Email patients** : explication claire, recommandations
actionnables (vigilance phishing, surveillance sécurité sociale,
contact CPAM si suspicion), excuses, contacts.

**Post-mortem - Causes racines probables** :

- mot de passe DPO compromis (réutilisé d'un autre service
  fuité ? Phishing ?) ;
- absence de MFA sur le compte DPO (le plan était en cours mais
  pas terminé) ;
- pas d'alerte sur les connexions depuis l'étranger ;
- pas de limite sur le volume d'export possible par un seul
  compte.

**Améliorations à apporter** :

- MFA obligatoire **immédiatement** pour tous les comptes admin ;
- alertes automatiques sur les connexions depuis géographies
  inhabituelles ;
- limites de quota sur les exports massifs (workflow d'approbation
  au-delà de N enregistrements) ;
- accélération du calendrier d'implémentation des autres mesures
  P1.

**Fiche au registre des violations** : utilisant le schéma de la
partie 4, documentation complète de l'incident avec chronologie,
nature, mesures, et leçons apprises.

### Étape 4 : Document de synthèse {id="tape-4-document-de-synth-se_1"}

Le rapport final doit synthétiser :

- l'état initial de l'application (au moment de l'audit) ;
- les progrès accomplis (qu'est-ce qui a été corrigé) ;
- l'incident survenu et sa gestion (démonstration de capacité) ;
- les recommandations pour la suite (consolidation, montée en
  maturité).

Ce document, présenté au COMEX, doit obtenir :

- la **reconnaissance** du travail accompli ;
- la **validation** du plan de poursuite ;
- les **moyens** nécessaires (budget, recrutements, formation) ;
- l'**engagement** de la direction sur la sécurité comme priorité
  stratégique.

Le TP est considéré comme réussi si l'apprenant démontre une
**maîtrise opérationnelle complète** : capacité à auditer du
code, à planifier des actions, à gérer un incident en temps réel,
à communiquer avec rigueur, et à mobiliser les bons outils
réglementaires. C'est cette maîtrise qui distinguera, dans la
suite de sa carrière, un développeur compétent en sécurité d'un
simple exécutant.
