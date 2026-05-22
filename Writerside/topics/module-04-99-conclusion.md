# Conclusion du module 4

Vous voici au terme de ce quatrième module, le plus dense de la
formation, consacré à la Privacy by Design et à la Privacy by
Default. Vous venez de franchir une étape décisive dans votre
parcours : vous êtes passé du statut de développeur conscient des
règles à celui d'**architecte capable d'intégrer la protection des
données dans la structure même de ses applications**. C'est une
compétence rare, recherchée, et qui fait la différence entre un
projet qui passera l'épreuve d'un contrôle CNIL et un projet qui
s'effondrera au premier audit.

Vous avez d'abord exploré les **fondements** : les sept principes
de Ann Cavoukian et l'article 25 du RGPD. Vous savez désormais que
la Privacy by Design est avant tout une **discipline de
conception** qui anticipe plutôt que de corriger, et que la
Privacy by Default est une obligation juridique sur les paramètres
initiaux. Vous avez compris que ces principes, vieux de plus de
trente ans, sont devenus pour partie des obligations contraignantes
par leur incorporation au RGPD.

Vous avez ensuite acquis une véritable **boîte à outils technique** :
pseudonymisation pour réduire l'identifiabilité, anonymisation
pour sortir du champ du RGPD, chiffrement à plusieurs niveaux,
séparation des données et data vault pour les zones les plus
sensibles. Pour chaque pattern, vous savez quand l'utiliser,
comment l'implémenter, et quelles sont ses limites. Vous avez
compris que la sécurité d'une application ne tient pas à un seul
mécanisme, mais à leur **combinaison intelligente** adaptée au
risque.

Vous avez ensuite plongé dans les enjeux d'**infrastructure** :
arbitrage self-hosting versus SaaS, localisation des serveurs, et
ce dossier crucial mais souvent négligé des **transferts
internationaux** dans le contexte post-Schrems II. Vous savez
maintenant que choisir un sous-traitant américain n'est jamais
neutre, que le Data Privacy Framework reste fragile, et qu'il faut
préparer des plans B pour les services critiques. Vous comprenez
l'écosystème des cadres juridiques (décisions d'adéquation, CCT,
BCR) et savez conduire un Transfer Impact Assessment.

Vous avez enfin maîtrisé le **cycle de vie des données**, de la
collecte initiale à la suppression définitive. Vous savez
distinguer soft-delete, anonymisation et hard-delete, vous savez
gérer le délicat sujet des sauvegardes, et surtout vous avez
intégré le réflexe de l'**automatisation** via les jobs cron.
Conserver une donnée trop longtemps, c'est une violation. Conserver
une donnée trop peu, c'est rater une obligation légale ou perdre
une information précieuse. L'art consiste à trouver la juste
durée et à l'appliquer fidèlement à grande échelle, ce qui n'est
possible que par l'automatisation.

À l'issue de ce module, vous repartez avec une vraie **identité
professionnelle d'architecte Privacy by Design**. Vous ne verrez
plus jamais une nouvelle fonctionnalité comme un simple objet
technique : vous y verrez automatiquement un cycle de vie, des
choix de stockage, des questions de sous-traitance, des défauts à
configurer. Cette posture, cette vigilance permanente, c'est la
marque des bons architectes de la vie privée.

## Auto-évaluation

### Questions à choix multiples

**Question 1** : Lequel des sept principes de Cavoukian impose que
les paramètres initiaux d'une application soient les plus
protecteurs ?

- A. Proactif, pas réactif
- B. Protection de la vie privée par défaut
- C. Sécurité de bout en bout
- D. Visibilité et transparence

---

**Question 2** : Une donnée pseudonymisée :

- A. Sort du champ d'application du RGPD
- B. Reste une donnée personnelle au sens du RGPD
- C. Devient une donnée anonyme
- D. Peut être publiée librement

---

**Question 3** : Selon l'arrêt Schrems II, le transfert de données
personnelles vers les États-Unis :

- A. Est totalement interdit
- B. Est libre sans conditions
- C. Nécessite des garanties supplémentaires (CCT, DPF, mesures
   complémentaires)
- D. Relève automatiquement d'une décision d'adéquation

---

**Question 4** : Le soft-delete simple (champ deleted_at) est-il
suffisant pour respecter le droit à l'effacement de l'article 17 ?

- A. Oui, dans tous les cas
- B. Oui, à condition d'être chiffré
- C. Non, il faut une suppression effective ou une anonymisation
- D. Non, le hard-delete est toujours obligatoire

---

**Question 5** : Pour des données de santé en France,
l'hébergement doit obligatoirement être :

A. Localisé en France
B. Certifié HDS (Hébergeur de Données de Santé)
C. Auto-hébergé par le responsable de traitement
D. Réalisé chez un hyperscaler américain

### Questions ouvertes

**Question 1** : Expliquez en quoi la Privacy by Design diffère
d'une approche « sécurité ajoutée en fin de projet ». Donnez un
exemple concret de coût évité grâce à la PbD.

---

**Question 2** : Vous concevez une nouvelle application qui
utilisera un service d'IA américain pour analyser les
contributions des utilisateurs. Quelles mesures de Privacy by
Design intégrez-vous pour limiter les risques liés à ce transfert
hors UE ?

---

**Question 3** : Décrivez en plusieurs étapes la politique
technique que vous mettriez en place pour automatiser la durée de
conservation d'un compte utilisateur sur trois ans à compter de
sa dernière connexion. Soyez précis sur les phases, les
notifications, et le code applicatif.

## Corrections des auto-évaluations {collapsible="true"}

### Réponses aux QCM

#### Réponse 1 : **B**

Le principe 2 (« Protection de la vie privée comme paramètre par
défaut ») impose précisément que les paramètres initiaux soient
les plus protecteurs, sans nécessiter d'action de l'utilisateur.
C'est ce principe qui justifie les cases décochées par défaut
pour le marketing, les profils privés par défaut sur les réseaux
sociaux destinés aux jeunes, et plus généralement l'opt-in plutôt
que l'opt-out. Ce principe est ensuite inscrit à l'article 25.2
du RGPD.

#### Réponse 2 : **B**

Une donnée pseudonymisée **reste une donnée personnelle** au sens
du RGPD (considérant 26). C'est l'une des plus grandes
incompréhensions sur le sujet. La pseudonymisation est une mesure
de **réduction du risque**, encouragée par l'article 25, mais elle
ne fait pas sortir les données du champ d'application du
règlement. Seule l'anonymisation effective (irréversible) permet
cette sortie.

#### Réponse 3 : **C**

L'arrêt Schrems II (juillet 2020) n'a pas interdit les transferts
UE-USA, mais il a exigé des garanties supplémentaires : clauses
contractuelles types (CCT) à jour, certification au Data Privacy
Framework (DPF, depuis juillet 2023), et le cas échéant des
mesures complémentaires (chiffrement, pseudonymisation) pour
neutraliser le risque d'accès par les autorités américaines. Une
Transfer Impact Assessment doit être conduite et documentée.

#### Réponse 4 : **C**

Le soft-delete simple **n'est pas une suppression** au sens de
l'article 17. La donnée est toujours présente en base, toujours
lisible par les administrateurs, toujours dans le champ du RGPD.
Le soft-delete peut être utilisé comme étape **intermédiaire**
(période de grâce, par exemple) mais doit être suivi soit d'une
anonymisation effective, soit d'une suppression physique. Il faut
aussi penser aux sauvegardes, qui doivent être purgées selon une
politique de rotation.

#### Réponse 5 : **B**

L'article L1111-8 du Code de la santé publique impose que les
données de santé soient hébergées par un Hébergeur de Données de
Santé (HDS) certifié. La localisation en France n'est pas
obligatoire en elle-même (l'hébergement HDS peut techniquement
être en UE), mais en pratique la plupart des prestataires HDS
hébergent en France. L'auto-hébergement par le responsable est
théoriquement possible mais soumis à des exigences techniques
strictes équivalentes au référentiel HDS.

### Réponses aux questions ouvertes

#### Réponse 1

La Privacy by Design diffère d'une « sécurité ajoutée en fin de
projet » par sa **logique d'anticipation**. Dans une approche
classique, on développe d'abord la fonctionnalité, puis on ajoute
des couches de sécurité et de conformité à la fin, sous pression
d'un audit ou d'un lancement imminent. La Privacy by Design
intègre la protection comme **composante structurelle** de
l'architecture, dès la conception.

**Exemple de coût évité** : un projet d'application e-commerce
développé sans PbD s'aperçoit deux mois avant le lancement que
les mots de passe sont stockés en SHA-1, que les données
utilisateurs sont mélangées dans une seule table sans
pseudonymisation, et que les sauvegardes sont envoyées non
chiffrées chez un prestataire américain. La refonte nécessaire
représente :

- réécriture du module d'authentification (2 semaines de
  développement) ;
- migration de la base avec création d'un schéma vault
  (3 semaines) ;
- renégociation des contrats sous-traitants et migration des
  sauvegardes vers un prestataire européen (1 mois) ;
- décalage du lancement de 2 mois et perte d'opportunités
  commerciales.

À comparer avec un projet PbD initial : les bonnes architectures
auraient été choisies en sprint zéro, sans coût supplémentaire,
juste par bons choix initiaux. Le total évité se compte
typiquement en dizaines voire centaines de milliers d'euros
selon la taille du projet.

#### Réponse 2

Mesures de Privacy by Design face à un service d'IA américain :

**1. Évaluer d'abord les alternatives européennes** : Mistral AI
(français), Azure OpenAI en région UE, modèles open source
auto-hébergés (Llama, Mixtral). Si une alternative européenne est
mature, la préférer systématiquement.

**2. Si le service américain est conservé** :

- pseudonymisation systématique avant envoi : aucune donnée
  identifiante ne sort en clair (remplacement des noms, emails,
  identifiants par des tokens) ;
- minimisation : envoyer le strict minimum nécessaire au
  traitement IA, pas l'historique complet ;
- chiffrement applicatif des données sensibles, déchiffrement
  uniquement chez le sous-traitant si nécessaire ;
- vérification de la certification DPF du sous-traitant ;
- signature des CCT à jour ;
- conduite d'un Transfer Impact Assessment formel ;
- documentation dans l'AIPD du projet.

**3. Information renforcée** : la politique de confidentialité
doit mentionner explicitement le transfert et permettre à
l'utilisateur de comprendre l'enjeu. Pour les traitements relevant
de l'article 22 (décisions automatisées), information complète
sur la logique sous-jacente.

**4. Plan de migration** : prévoir un scénario de bascule rapide
vers une alternative européenne si le cadre juridique devient
instable (« Schrems III » potentielle).

**5. Suivi régulier** : audit annuel de la chaîne de sous-traitance,
veille juridique sur les évolutions du DPF.

#### Réponse 3

Politique technique d'automatisation de la conservation à 3 ans :

**Phase 1 - Détection et prévenance (J-30 avant échéance)**

Cron quotidien qui détecte les comptes dont la dernière connexion
remonte à 3 ans moins 30 jours :

```sql
SELECT id, email FROM users
WHERE deletion_status = 'active'
    AND last_login_at = CURRENT_DATE
        - INTERVAL '3 years'
        + INTERVAL '30 days';
```

Action : envoi d'un email de prévenance avec :

- rappel du contenu présent dans le compte ;
- lien de connexion pour réactiver le compte ;
- lien de téléchargement complet des données (export RGPD) ;
- lien pour confirmer la suppression immédiate ;
- échéance précise mentionnée.

**Phase 2 - Soft-delete (J0 à 3 ans d'inactivité)**

Cron quotidien qui passe en `pending_deletion` les comptes ayant
atteint 3 ans d'inactivité :

```sql
UPDATE users SET
    deletion_status = 'pending_deletion',
    deletion_requested_at = CURRENT_TIMESTAMP
WHERE deletion_status = 'active'
    AND last_login_at < CURRENT_DATE - INTERVAL '3 years';
```

Action complémentaire : le compte devient inutilisable (refus de
connexion), mais peut être restauré pendant 30 jours sur demande
de l'utilisateur. Email de confirmation envoyé.

**Phase 3 - Anonymisation (J+30 après soft-delete)**

Cron quotidien qui anonymise les comptes en attente depuis plus
de 30 jours :

```javascript
async function anonymizeExpiredAccounts() {
    const accounts = await db.users.find({
        deletion_status: 'pending_deletion',
        deletion_requested_at: {
            '<': subDays(new Date(), 30)
        }
    });

    for (const account of accounts) {
        await db.transaction(async (tx) => {
            const userIdHash = await hashUserId(account.id);

            await tx.users.update(account.id, {
                email: `anon-${userIdHash}@local`,
                first_name: 'ANONYMIZED',
                last_name: 'USER',
                deletion_status: 'anonymized',
                anonymized_at: new Date()
            });

            await tx.userPreferences
                .deleteByUserId(account.id);

            await tx.erasureLog.insert({
                user_id_hash: userIdHash,
                erased_at: new Date(),
                reason: '3y_inactivity_after_grace'
            });
        });
    }
}
```

Les données comptables (factures notamment) sont conservées
selon leur propre cycle (10 ans pour la comptabilité), avec
anonymisation des champs nominatifs.

**Phase 4 - Hard-delete (J+10 ans après anonymisation)**

Cron mensuel qui supprime physiquement les comptes anonymisés
depuis plus de 10 ans :

```sql
DELETE FROM users
WHERE deletion_status = 'anonymized'
    AND anonymized_at < CURRENT_DATE - INTERVAL '10 years';
```

**Phase 5 - Sauvegardes**

Rotation automatique des sauvegardes à 30 jours. En cas de
restauration nécessaire, rejeu obligatoire des effacements
mémorisés dans le registre `erasure_log`.

**Phase 6 - Documentation et audit**

Toutes les actions sont journalisées et accessibles à l'audit :

- date de l'exécution du job ;
- nombre de comptes traités ;
- éventuelles erreurs ;
- temps d'exécution.

Cette politique est documentée dans le registre des activités de
traitement, mentionnée dans la politique de confidentialité,
auditée trimestriellement par le DPO.

## Conclusion du module

### Ce que vous avez appris

Vous repartez de ce module avec une vision globale et opérationnelle
de la Privacy by Design. Concrètement, vous savez désormais :
appliquer les sept principes de Cavoukian et l'article 25 du RGPD,
mobiliser les patterns techniques appropriés (pseudonymisation,
anonymisation, chiffrement, séparation, data vault), arbitrer les
choix d'infrastructure et de sous-traitance dans le contexte
post-Schrems II, et automatiser le cycle de vie des données via
des jobs cron et une politique de conservation rigoureuse.

Vous avez surtout acquis une **posture d'architecte** : celle qui
intègre la protection des données dans la **structure même** d'une
application, plutôt que de la rattraper en fin de projet. Cette
posture, c'est ce qui transforme un développeur compétent en un
véritable artisan de la conformité, capable de défendre ses choix
face à un DPO, à un client, à un auditeur ou à la CNIL.

### Aller plus loin

Pour approfondir et consolider, plusieurs ressources sont
recommandées :

- **Les lignes directrices 4/2019** du CEPD sur la protection des
  données dès la conception et par défaut, qui détaillent
  l'interprétation officielle de l'article 25 ;
- **Le guide de la CNIL sur la sécurité des données personnelles**,
  régulièrement mis à jour, qui constitue un référentiel pratique
  reconnu ;
- **Les recommandations du CEPD 01/2020** sur les mesures qui
  complètent les outils de transfert, élaborées suite à Schrems II ;
- **Les référentiels de l'ANSSI** sur les hébergeurs cloud
  (SecNumCloud), qui montent en exigence et deviennent une
  référence pour la souveraineté numérique ;
- **Le référentiel HDS** de l'ANS pour l'hébergement de données
  de santé, indispensable si vous travaillez dans ce secteur ;
- **L'AI Act européen** et ses lignes directrices, qui interagissent
  étroitement avec le RGPD sur les sujets de profilage et de
  décisions automatisées ;
- **Le PIA Tool de la CNIL** pour conduire vos analyses d'impact,
  outil gratuit et reconnu.

### Conseils pour la pratique professionnelle

Quelques conseils concrets pour intégrer la Privacy by Design
dans votre quotidien :

- **Imposez l'AIPD au sprint zéro** : tout projet manipulant des
  données personnelles mérite au moins une analyse préliminaire,
  même informelle. Elle évitera des refontes coûteuses.
- **Rédigez une Definition of Done RGPD** : chaque user story
  intégrant des données personnelles doit cocher des cases
  (consentement, journalisation, chiffrement, durée de
  conservation).
- **Préférez l'Union européenne** : pour les nouveaux projets,
  privilégier les sous-traitants européens chaque fois qu'une
  alternative mature existe. Cela simplifie la conformité et
  contribue à la souveraineté.
- **Automatisez la conservation** : les politiques manuelles
  échouent toujours à l'échelle. Investissez dans les cron jobs
  dès la conception, c'est un effort modeste pour un bénéfice
  permanent.
- **Documentez vos choix d'architecture** : pas seulement le quoi,
  mais le pourquoi. Un audit demande toujours « pourquoi avez-vous
  choisi cette technologie plutôt qu'une autre ? ». La réponse
  doit être prête.
- **Veillez sur l'écosystème juridique** : Schrems II, DPF, AI
  Act, NIS2, Data Act... le paysage évolue rapidement. Une heure
  de veille mensuelle vaut mieux qu'une refonte en urgence.

### Ressources complémentaires

- **Articles 25, 32, 35, et 44 à 50 du RGPD** : eur-lex.europa.eu.
- **Lignes directrices CEPD** sur la PbD, le transfert, la
  notification de violations : edpb.europa.eu.
- **Guide CNIL sur la sécurité** des données personnelles :
  cnil.fr.
- **Site de l'ANSSI** sur SecNumCloud et la cybersécurité :
  ssi.gouv.fr.
- **Liste DPF** des entreprises certifiées :
  dataprivacyframework.gov.
- **Privacy by Design Foundation** de Ann Cavoukian (anglais) :
  privacybydesign.foundation.

### Mot de fin

La Privacy by Design n'est pas un sujet à part. Ce n'est pas un
chapitre du RGPD, ce n'est pas un module à cocher dans une
checklist. C'est une **philosophie de conception** qui doit
imprégner toute votre démarche technique. Vous concevez une
application ? Demandez-vous comment elle protège ses
utilisateurs. Vous choisissez un sous-traitant ? Demandez-vous
qui pourra accéder à ses données. Vous archivez de l'information ?
Demandez-vous quand elle devra disparaître. Ce questionnement
permanent, naturel chez les architectes expérimentés, est la
vraie marque du métier.

Vous venez de franchir une étape importante de votre montée en
compétences. Le prochain module abordera la sécurité technique
sous l'angle RGPD : confidentialité, intégrité, disponibilité,
journalisation, gestion des violations.
