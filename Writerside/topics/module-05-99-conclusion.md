# Conclusion du module 5

Vous voici au terme du module le plus opérationnel de la formation,
consacré à la sécurité des données. Ce module a sans doute été le
plus dense techniquement, et c'est normal : la sécurité ne tolère
ni l'approximation, ni l'à-peu-près. Une faille, même minime, peut
exposer des milliers d'utilisateurs et faire basculer la conformité
de toute une organisation. À l'inverse, une rigueur quotidienne
construit progressivement un niveau de protection considérable.
Vous repartez aujourd'hui avec les compétences nécessaires pour
faire cette différence.

Vous avez d'abord abordé les **fondamentaux conceptuels et
juridiques** : l'article 32 du RGPD, le triptyque CIA
(confidentialité, intégrité, disponibilité, complété par la
résilience), et l'approche par les risques. Vous savez désormais
que la sécurité n'est pas une checklist universelle mais une
démarche proportionnée : on adapte les mesures au contexte, au
volume, à la sensibilité. Vous avez aussi maîtrisé le premier
domaine opérationnel : le **contrôle d'accès**, avec
l'authentification forte (MFA), le RBAC, et la sécurisation des
sessions. C'est sur ce socle que repose la plupart des défenses
applicatives.

Vous avez ensuite plongé dans la **cryptographie appliquée** :
configuration moderne de TLS (1.2 minimum, 1.3 idéalement),
chiffrement au repos à plusieurs niveaux (FDE, TDE, applicatif),
hachage robuste des mots de passe avec Argon2id, et gestion des
secrets via un vault centralisé. Vous savez que la cryptographie
n'est pas un domaine où on improvise : les algorithmes obsolètes
(MD5, SHA-1) sont à proscrire, les bibliothèques éprouvées sont à
privilégier, et la rotation périodique des clés est non
négociable.

Vous avez exploré la **sécurité du code** sous l'angle RGPD :
lecture critique de l'OWASP Top 10, gestion proactive des
dépendances (Dependabot, audit automatique, pre-commit hooks),
discipline anti-fuites des secrets dans Git. Vous comprenez que
la sécurité est une discipline **quotidienne**, pas une couche
ajoutée en fin de projet. Vous savez aussi mettre en place une
**journalisation efficace** (audit trail) et concevoir une
**politique de sauvegardes** conforme au principe de disponibilité.

Vous avez enfin maîtrisé le sujet le plus stressant du métier : la
**gestion d'une violation de données**. Vous connaissez les
obligations strictes des articles 33 et 34 (notification CNIL en
72 heures, information des personnes en cas de risque élevé), vous
savez analyser un incident pour le qualifier juridiquement, et
vous savez rédiger les documents officiels (notification CNIL,
email aux personnes). Vous avez compris l'importance critique de
préparer un **plan de réponse aux incidents** en amont, plutôt
que d'improviser sous le stress.

À l'issue de ce module, vous repartez avec une **posture
professionnelle de développeur sécurité**. Vous ne stockerez jamais
un mot de passe en clair, vous ne commit jamais un secret dans
Git, vous ne désactiverez jamais TLS « pour debugger plus vite »,
vous ne donnerez jamais les droits administrateur à un service
applicatif. Ces réflexes, anodins pris individuellement, font la
différence entre une application défendable et une bombe
juridique à retardement. Vous savez aussi que la sécurité absolue
n'existe pas : ce qui existe, c'est la rigueur, la défense en
profondeur, et la capacité à réagir vite et bien quand l'incident
survient.

## Auto-évaluation

### Questions à choix multiples

**Question 1** : Selon l'article 32 du RGPD, quels sont les
critères à prendre en compte pour évaluer le niveau de sécurité
approprié ?

- A. Uniquement la nature des données  
- B. La taille de l'entreprise et son chiffre d'affaires  
- C. L'état de l'art, les coûts, la nature et les risques du
traitement  
- D. La seule volonté du responsable de traitement  

---

**Question 2** : Quel algorithme de hachage est aujourd'hui
recommandé pour les mots de passe ?

- A. MD5
- B. SHA-256 sans sel
- C. Argon2id
- D. ROT13

---

**Question 3** : Une violation de données doit être notifiée à
la CNIL :

- A. Toujours et systématiquement
- B. Uniquement si plus de 1000 personnes sont concernées
- C. Dans les 72 heures après la prise de connaissance, si elle
   présente un risque pour les personnes
- D. Au plus tard une semaine après l'incident

---

**Question 4** : Qu'est-ce que le principe du moindre privilège
en contrôle d'accès ?

- A. Donner tous les droits aux administrateurs par défaut
- B. Attribuer à chaque utilisateur le minimum de droits nécessaires
   à sa fonction
- C. Ne donner aucun droit, par sécurité maximale
- D. Donner les mêmes droits à tous les utilisateurs

---

**Question 5** : Concernant les sauvegardes, quelle affirmation
est correcte au regard du RGPD ?

- A. Les sauvegardes sont exclues du périmètre du RGPD
- B. Une sauvegarde non testée en restauration ne garantit pas la
   disponibilité
- C. Il suffit d'une sauvegarde, pas besoin de rotation
- D. Les sauvegardes peuvent rester en clair si elles sont sur disque

### Questions ouvertes

**Question 1** : Expliquez la différence entre chiffrement et
hachage. Pour quel usage privilégie-t-on l'un ou l'autre, et
pourquoi ?

---

**Question 2** : Vous découvrez qu'un développeur a poussé sur
GitHub, il y a deux semaines, un fichier contenant les clés API
de votre service de paiement. Décrivez votre plan d'action
détaillé.

---

**Question 3** : Décrivez les étapes principales de la gestion
d'une violation de données, de la détection jusqu'au post-mortem.
Pour chaque étape, indiquez les délais légaux applicables et les
acteurs impliqués.

## Corrections des auto-évaluations {collapsible="true"}

### Réponses aux QCM

#### Réponse 1 : **C**

L'article 32 du RGPD exige une approche par les risques qui prend
en compte cinq critères : l'**état de l'art** (ce que la profession
sait faire à un moment donné), les **coûts de mise en œuvre**
(proportionnalité acceptée), la **nature, la portée, le contexte
et les finalités** du traitement, les **risques** pour les droits
et libertés des personnes, et les **conséquences** d'une violation
éventuelle. Cette approche est volontairement souple pour s'adapter
à toutes les tailles d'organisation et à tous les contextes.

#### Réponse 2 : **C**

**Argon2id** est l'algorithme recommandé en 2026 pour le hachage
des mots de passe. Il a remporté le Password Hashing Competition
et est aujourd'hui recommandé par l'OWASP, le NIST et la CNIL. Ses
paramètres typiques (mémoire 64 MiB, 3 itérations, parallélisme
4) le rendent résistant aux attaques par GPU et ASIC. MD5 et
SHA-256 sans sel sont à proscrire absolument : le premier est
cassé depuis 1996, le second est trop rapide pour résister à la
force brute. ROT13 est un simple décalage de lettres, sans aucune
valeur cryptographique.

#### Réponse 3 : **C**

L'article 33 du RGPD impose la notification à la CNIL **dans les
72 heures** suivant la prise de connaissance d'une violation, **à
moins que celle-ci ne soit pas susceptible d'engendrer un risque**
pour les droits et libertés des personnes. La notification est
donc conditionnelle au risque, pas systématique. Le décompte des
72 heures démarre à la prise de connaissance effective, pas à la
survenance de l'incident. Si le délai n'est pas respecté, la
notification doit être accompagnée des motifs du retard.

#### Réponse 4 : **B**

Le **principe du moindre privilège** consiste à attribuer à chaque
utilisateur (humain ou service) le **minimum de droits
nécessaires** à l'accomplissement de sa fonction. C'est un
principe fondamental de la sécurité, qui limite mécaniquement les
dégâts en cas de compromission d'un compte. Il s'oppose à la
tentation de donner « tout par sécurité » ou « les mêmes droits
par simplicité ». Combiné au RBAC, il permet une gestion fine et
maintenable des autorisations.

#### Réponse 5 : **B**

Une **sauvegarde non testée en restauration n'apporte aucune
garantie réelle**. C'est une erreur fréquente : on met en place
des sauvegardes, on les vérifie en théorie, mais on ne teste
jamais leur restauration effective. Le jour de l'incident, on
découvre que la sauvegarde est corrompue, incomplète, ou
inutilisable. La CNIL et l'ANSSI recommandent des tests de
restauration **mensuels** en environnement isolé. Par ailleurs, les
sauvegardes contiennent des données personnelles donc relèvent
pleinement du RGPD (chiffrement obligatoire, durée de conservation
maîtrisée, accès journalisé).

### Réponses aux questions ouvertes

#### Réponse 1

**Différence entre chiffrement et hachage**

Le **chiffrement** est une transformation **réversible** : avec
la clé de chiffrement, on peut retrouver le contenu original.
C'est utilisé pour protéger des données qu'on doit pouvoir
récupérer en clair : communications (TLS), stockage de données
sensibles (notes médicales chiffrées en base), sauvegardes. Les
algorithmes modernes (AES-256, ChaCha20) sont symétriques (même
clé pour chiffrer et déchiffrer) ou asymétriques (paire de clés
publique/privée comme RSA, ECC).

Le **hachage** est une transformation **irréversible** : à partir
du hash, on ne peut pas retrouver le contenu original (pas
mathématiquement, juste informatiquement avec les algorithmes
modernes). On l'utilise quand on n'a pas besoin de récupérer la
donnée en clair, juste de **vérifier une correspondance**. Cas
typique : les mots de passe. Lorsqu'un utilisateur s'authentifie,
on hache son mot de passe saisi et on compare au hash stocké,
sans jamais avoir besoin de connaître le mot de passe en clair.

**Quand utiliser quoi** :

- **Chiffrement** : pour toutes les données qui doivent être
  lisibles ultérieurement (TLS, BDD, sauvegardes, chiffrement de
  champs sensibles).
- **Hachage** : pour les vérifications d'égalité sans besoin de
  récupération (mots de passe, empreintes de fichiers, signatures
  d'intégrité).

Une erreur courante : utiliser un hash rapide (SHA-256) pour des
mots de passe. Pour les mots de passe, on a besoin d'un hash
**lent par conception** (Argon2id, bcrypt) qui résiste à la force
brute. Pour les empreintes de fichiers en revanche, on veut un
hash **rapide** : SHA-256 ou SHA-3 sont parfaits.

#### Réponse 2

**Plan d'action - Clés API de paiement exposées sur GitHub**

**Étape 1 - Considérer les clés comme compromises**

Même si le commit a été récent ou peu visible, GitHub est
constamment scrappé par des bots qui détectent automatiquement
les clés API. Considérer les clés comme **publiques** dès leur
push.

**Étape 2 - Rotation immédiate**

- Contacter le prestataire de paiement (Stripe, Adyen, etc.) ;
- Révoquer toutes les clés exposées via leur dashboard ;
- Générer de nouvelles clés ;
- Mettre à jour la configuration de production (de préférence
  via le vault) ;
- Redéployer les services concernés.

**Étape 3 - Audit des accès depuis l'exposition**

- Vérifier dans le tableau de bord du prestataire de paiement
  les opérations effectuées avec les clés exposées sur les
  deux semaines passées ;
- Rechercher des transactions inhabituelles : remboursements
  suspects, créations de comptes anormales, opérations en
  dehors des horaires habituels ;
- Si activité malveillante détectée : c'est une violation au
  sens de l'article 33 (les clés permettent d'accéder à des
  données de transactions, donc à des données personnelles
  financières).

**Étape 4 - Qualification d'une éventuelle violation**

- Si **aucun accès malveillant détecté** : pas de violation au
  sens strict (pas d'accès non autorisé effectif), mais
  documenter rigoureusement l'incident dans le registre interne
  des violations potentielles ;
- Si **accès malveillants confirmés** : notification CNIL sous
  72 heures, et information des personnes affectées si risque
  élevé.

**Étape 5 - Nettoyage du dépôt**

- Réécrire l'historique Git avec `git filter-repo` ou BFG ;
- Force-push après communication à l'équipe ;
- Avertir que les clones existants sont à supprimer/rafraîchir.

**Étape 6 - Mesures préventives**

- Installer `gitleaks` ou `git-secrets` en pre-commit hook ;
- Activer le scan de secrets dans le CI/CD ;
- Activer la **Secret Scanning** native de GitHub (gratuite sur
  les dépôts publics, payante sur les privés mais
  recommandée) ;
- Migrer la gestion des secrets vers un vault centralisé
  (HashiCorp Vault, AWS Secrets Manager) ;
- Former l'équipe sur les bonnes pratiques de gestion des
  secrets ;
- Réviser le processus de revue de code pour inclure
  explicitement la vérification anti-secrets.

**Étape 7 - Documentation**

- Inscription au registre des incidents ;
- Post-mortem en équipe (sans blâme individuel) ;
- Partage des leçons apprises.

#### Réponse 3

**Étapes principales de la gestion d'une violation**

**Étape 1 - Détection** (T0)

- *Acteurs* : équipe technique, monitoring automatique, équipe
  sécurité, utilisateurs signalant ;
- *Délai* : aussi rapide que possible. Le RGPD ne fixe pas de
  délai de détection, mais l'absence de monitoring peut être
  reprochée comme manquement à l'article 32 ;
- *Actions* : confirmer le caractère réel de l'incident, ne pas
  donner l'alerte sur de simples suspicions techniques.

**Étape 2 - Activation de la cellule de crise** (T0 + minutes)

- *Acteurs* : incident commander, lead technique, DPO, direction,
  juriste, communication ;
- *Délai* : moins d'une heure après la détection confirmée ;
- *Actions* : réunion d'urgence (visio ou présentiel),
  qualification initiale, attribution des rôles.

**Étape 3 - Containment** (T0 + 1 à 4 heures)

- *Acteurs* : lead technique et équipe sécurité ;
- *Délai* : aussi vite que possible pour limiter l'ampleur ;
- *Actions* : stopper la fuite (révocation, isolation,
  désactivation des comptes compromis), préserver les preuves
  pour l'investigation.

**Étape 4 - Investigation** (T0 + 4 à 24 heures)

- *Acteurs* : équipe technique, idéalement avec des spécialistes
  forensics ;
- *Délai* : suffisant pour qualifier précisément l'incident, mais
  sans retarder la notification ;
- *Actions* : déterminer le périmètre exact (qui ? quoi ? combien
  de personnes ?), identifier la cause racine, évaluer le risque
  résiduel.

**Étape 5 - Qualification et décision** (T0 + 24 à 48 heures
maximum)

- *Acteurs* : DPO, direction, juriste ;
- *Délai* : avant l'échéance des 72 heures ;
- *Actions* : décider si notification CNIL nécessaire (article
  33), si information des personnes nécessaire (article 34),
  préparer la documentation.

**Étape 6 - Notification CNIL** (T0 + 72 heures maximum)

- *Acteurs* : DPO ;
- *Délai* : **72 heures à compter de la prise de connaissance**
  (article 33) ;
- *Actions* : remplir le téléservice CNIL, fournir toutes les
  informations exigées (article 33.3), conserver une preuve de
  l'envoi.

**Étape 7 - Information des personnes** (T0 + 24 à 72 heures
généralement)

- *Acteurs* : DPO, communication ;
- *Délai* : « dans les meilleurs délais » (article 34), pas de
  durée chiffrée mais doit être rapide ;
- *Actions* : envoi d'emails clairs et actionnables (sauf cas de
  dispense de l'article 34.3), accompagnement par un support
  client renforcé.

**Étape 8 - Communications complémentaires** (T0 + variable)

- *Acteurs* : communication, direction ;
- *Délai* : selon le contexte (avant que les médias ne s'en
  emparent) ;
- *Actions* : communiqué de presse si nécessaire, communication
  interne à l'organisation, réponse aux questions des partenaires.

**Étape 9 - Restauration et retour à la normale** (T0 + jours à
semaines)

- *Acteurs* : équipe technique ;
- *Délai* : selon la complexité technique ;
- *Actions* : remise en service complète, correctifs déployés,
  monitoring renforcé.

**Étape 10 - Post-mortem** (T0 + 1 à 2 semaines)

- *Acteurs* : toute la cellule de crise ;
- *Délai* : suffisamment tôt pour que les souvenirs soient
  précis ;
- *Actions* : analyse sans blâme individuel, identification des
  causes racines, plan d'amélioration, mise à jour du plan de
  réponse aux incidents.

**Étape 11 - Documentation au registre** (en continu)

- *Acteurs* : DPO ;
- *Délai* : tout au long de la gestion, finalisation après le
  post-mortem ;
- *Actions* : alimentation du registre des violations (article
  33.5), conservation pour les contrôles éventuels.

**Étape 12 - Suivi avec la CNIL** (variable)

- *Acteurs* : DPO ;
- *Délai* : selon les demandes de la CNIL ;
- *Actions* : répondre aux éventuelles questions complémentaires,
  produire les justifications demandées, démontrer l'effectivité
  des mesures correctives.

La maîtrise de ces étapes, dans cet ordre, fait la différence
entre une organisation qui gère sereinement une crise et une
organisation qui s'effondre sous la pression. La préparation en
amont (plan de réponse aux incidents documenté, exercices de
simulation, équipes formées) est ce qui rend l'exécution réelle
fluide.

## Conclusion du module

### Ce que vous avez appris

Vous repartez de ce module avec une **maîtrise opérationnelle de
la sécurité applicative RGPD**. Concrètement, vous savez :
appliquer l'article 32 du RGPD selon une approche par les risques,
implémenter une authentification forte et un contrôle d'accès
RBAC, mobiliser correctement la cryptographie (TLS, chiffrement
applicatif, Argon2id), sécuriser le code (OWASP Top 10, gestion
des dépendances, anti-fuites de secrets), mettre en place une
journalisation et des sauvegardes conformes, et gérer une
violation de données de bout en bout selon les articles 33 et 34.

Surtout, vous avez acquis une **posture de développeur sécurité**
qui rendra naturelle la rigueur quotidienne attendue dans le
métier. Cette posture, vous allez l'enrichir avec l'expérience,
mais elle est désormais ancrée. C'est elle qui transformera, au
fil des projets, un développeur de plus en un véritable artisan
de la confiance numérique.

### Aller plus loin

Pour approfondir et rester à jour, plusieurs ressources sont
incontournables :

- **Le guide de la CNIL sur la sécurité des données personnelles** :
  référentiel pratique régulièrement mis à jour, qui décrit le
  niveau minimal attendu pour différentes catégories de
  traitements ;
- **Les guides de l'ANSSI** : authentification, hygiène
  informatique, sécurisation des sites web, sauvegardes,
  cryptographie. L'agence française est une référence
  internationale ;
- **L'OWASP Top 10** et ses ressources associées (Cheat Sheets,
  Application Security Verification Standard) : la base mondiale
  pour la sécurité applicative ;
- **Les recommandations du NIST** (notamment SP 800-63B sur les
  mots de passe et l'authentification) : référence en matière de
  bonnes pratiques de sécurité ;
- **Les publications de l'ENISA** (Agence européenne de
  cybersécurité) : guides pratiques sur les violations de
  données, la pseudonymisation, la cryptographie ;
- **Le téléservice de notification CNIL** : se familiariser avec
  l'interface, savoir ce qui est attendu, anticiper les
  réponses ;
- **Les communautés et conférences** : OWASP Chapter local, FIC
  (Forum International de la Cybersécurité), conférences
  techniques régulières.

### Conseils pour la pratique professionnelle

Quelques conseils concrets pour faire de la sécurité un réflexe
permanent :

- **Faites des revues de code orientées sécurité** : en plus de
  la revue fonctionnelle, prendre 10 minutes pour chasser les
  anti-patterns (concaténation SQL, comparaisons de mots de
  passe en clair, secrets dans le code).
- **Automatisez tout ce qui peut l'être** : audits de
  dépendances, scans de secrets, tests de restauration des
  sauvegardes. L'humain oublie ; l'automatisation tient.
- **Préparez le plan de réponse aux incidents avant d'en avoir
  besoin** : un plan rédigé en urgence ne sert à rien. Un plan
  préparé en amont, partagé, testé en exercice, vous sauve la
  vie le jour J.
- **Conservez une posture humble** : la sécurité parfaite
  n'existe pas, les vulnérabilités sont permanentes. L'attitude
  saine est la vigilance continue, pas l'arrogance.
- **Suivez l'actualité sécurité** : abonnez-vous à des
  newsletters (ZATAZ, Risky Business, Cybersecurity News), suivez
  des chercheurs sérieux, lisez les rapports d'incident
  publiés (Mandiant, CrowdStrike).
- **Partagez les leçons apprises** : en interne (post-mortems
  sans blâme), avec la communauté quand c'est possible. La
  sécurité est un effort collectif.

### Ressources complémentaires

- **Articles 32, 33 et 34 du RGPD** : eur-lex.europa.eu.
- **Guides CNIL sécurité** : cnil.fr/fr/securite.
- **Téléservice notification violations** :
  cnil.fr/fr/notifier-une-violation-de-donnees-personnelles.
- **Lignes directrices CEPD sur les violations** :
  edpb.europa.eu.
- **Site de l'ANSSI** : ssi.gouv.fr.
- **OWASP** : owasp.org, notamment owasp.org/Top10.
- **NIST Cybersecurity Framework** : nist.gov/cyberframework.
- **ENISA** : enisa.europa.eu.

### Mot de fin

La sécurité n'est pas une discipline parmi d'autres dans le métier
de développeur : c'est une **dimension transversale** qui colore
tous les choix techniques. Vous concevez une nouvelle
fonctionnalité ? Pensez aux risques. Vous installez une nouvelle
dépendance ? Vérifiez ses CVE. Vous écrivez une requête SQL ?
Utilisez des paramètres. Vous loguez une opération ? Vérifiez que
vous ne loguez pas de secret. Cette vigilance permanente, qui
peut paraître pénible au début, devient progressivement un
**réflexe naturel**, intégré au geste de coder. Elle est la marque
des bons professionnels.

Surtout, n'oubliez jamais que derrière chaque donnée que vous
manipulez, il y a une personne réelle. Un patient qui a confié son
dossier médical. Un client qui a confié son IBAN. Un mineur qui a
confié ses échanges. Chaque mesure de sécurité que vous mettez en
place les protège concrètement. C'est cette dimension humaine qui
rend la sécurité non pas une corvée technique, mais une vraie
**responsabilité morale**.

Vous arrivez au terme du cinquième module. Il vous reste un
sixième et dernier module à découvrir, qui abordera la dimension
documentaire et stratégique du métier : registre des activités de
traitement, AIPD, et accompagnement organisationnel de la
conformité.
