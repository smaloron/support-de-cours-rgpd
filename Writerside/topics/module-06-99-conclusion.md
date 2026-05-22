# Conclusion du module 6

Vous voici au terme du sixième et dernier module de la formation,
consacré à la documentation et à la conformité opérationnelle.
Ce module a peut-être semblé plus juridique et organisationnel
que les précédents, mais ne vous y trompez pas : c'est un module
absolument central. La meilleure architecture technique du monde,
le code le plus rigoureux, les mesures de sécurité les plus
sophistiquées ne valent **rien** si vous ne pouvez pas le
documenter et le démontrer. Le RGPD est ainsi fait : la
responsabilité (article 5.2) impose de prouver, pas seulement de
faire.

Vous avez d'abord maîtrisé le **registre des activités de
traitement** (article 30), pierre angulaire de la conformité
opérationnelle. Vous savez constituer un registre complet,
distinguer responsable de traitement et sous-traitant, et le
maintenir dans le temps. Vous comprenez que ce document n'est
pas une corvée administrative mais un véritable **outil de
pilotage** qui donne à votre organisation une vision panoramique
de ses traitements.

Vous avez ensuite plongé dans l'**analyse d'impact relative à la
protection des données** (AIPD, article 35), document à la fois
craint et incompris. Vous savez identifier les traitements qui
en requièrent une, conduire la démarche en quatre étapes selon
la méthodologie CNIL, et utiliser l'outil PIA. Surtout, vous
comprenez que l'AIPD est un **outil de décision** qui peut amener
à modifier, reporter, ou renoncer à un projet. C'est sa vraie
puissance.

Vous avez exploré les **documents externes** : politique de
confidentialité, mentions d'information contextuelles, accords
de sous-traitance, et dispositif cookies. Vous savez maintenant
rédiger une politique claire et lisible, négocier un DPA conforme
à l'article 28, et déployer une CMP respectant les recommandations
CNIL. Vous avez intégré le réflexe de privilégier des **solutions
européennes** et de documenter rigoureusement les transferts
internationaux.

À l'issue de ce module, vous repartez avec une **vision complète
du cycle de la conformité** : de la conception (modules 4 et 5)
à la production (ce module). Vous savez non seulement faire les
choses correctement, mais aussi les **prouver**, ce qui est
fondamentalement différent. Cette compétence rare est
particulièrement recherchée : peu de développeurs maîtrisent
l'aspect documentaire, et ceux qui le font prennent naturellement
des responsabilités élargies.

Plus largement, vous avez acquis une **maturité professionnelle**.
La conformité RGPD n'est plus pour vous une contrainte extérieure
à laquelle on cède à contrecœur, mais une **discipline
constructive** qui structure les projets, sécurise les
utilisateurs, et protège l'organisation. C'est cette posture qui
fera de vous, dans la suite de votre carrière, un acteur fiable
et apprécié de vos équipes.

## Auto-évaluation

### Questions à choix multiples

**Question 1** : Selon l'article 30 du RGPD, qui doit tenir un
registre des activités de traitement ?

- A. Uniquement les grandes entreprises de plus de 250 salariés
- B. Uniquement le sous-traitant
- C. Le responsable de traitement et le sous-traitant, avec une exemption très limitée pour les petites structures
- D. Uniquement le responsable de traitement

---

**Question 2** : Quand une AIPD est-elle obligatoire selon
l'article 35 du RGPD ?

- A. Pour tous les traitements de données personnelles
- B. Uniquement si le traitement concerne plus de 10 000 personnes
- C. Lorsque le traitement est susceptible d'engendrer un risque élevé pour les droits et libertés des personnes
- D. Uniquement à la demande de la CNIL

---

**Question 3** : Concernant le bandeau cookies, quelle
affirmation est conforme aux recommandations CNIL ?

- A. Le bouton « Accepter tout » peut être plus visible que les autres options
- B. Les boutons « Accepter », « Refuser » et « Personnaliser » doivent être équivalents visuellement
- C. Le refus n'a pas besoin d'être proposé
- D. Le consentement peut être implicite après quelques secondes
   de navigation

---

**Question 4** : Que doit contenir obligatoirement un accord de
sous-traitance (DPA) selon l'article 28 du RGPD ?

- A. Uniquement le tarif des prestations
- B. Uniquement les coordonnées des parties
- C. Les clauses sur la sécurité, la confidentialité, la sous-sous-traitance, l'aide aux droits des personnes, la 
notification de violation, et la restitution des données
- D. Uniquement les transferts internationaux

---

**Question 5** : Qu'est-ce que la « consultation préalable » de
l'article 36 du RGPD ?

- A. Une consultation obligatoire de la CNIL avant chaque traitement
- B. Une consultation de la CNIL en cas de violation
- C. Une consultation de la CNIL lorsque l'AIPD identifie des risques résiduels élevés malgré les mesures envisagées
- D. Une consultation du DPO en cas de doute

### Questions ouvertes

**Question 1** : Expliquez la différence entre la politique de
confidentialité et les mentions d'information contextuelles.
Pour quels usages chacune est-elle utilisée, et pourquoi sont-elles
complémentaires ?

---

**Question 2** : Vous découvrez qu'un sous-traitant SaaS que
votre entreprise utilise depuis deux ans pour son outil de
recrutement est basé aux États-Unis et n'a jamais signé de DPA.
Quelle est votre démarche ? Précisez les étapes, les risques
encourus, et les solutions possibles.

---

**Question 3** : Décrivez la méthodologie CNIL en quatre étapes
pour conduire une AIPD. Pour chaque étape, indiquez les acteurs
impliqués, les livrables produits, et les questions clés à se
poser.

## Corrections des auto-évaluations {collapsible="true"}

### Réponses aux QCM

#### Réponse 1 : **C**

L'article 30 impose un registre **au responsable de traitement et
au sous-traitant**. Une exemption existe pour les organisations
de moins de 250 salariés, mais elle est très limitée : elle ne
s'applique pas si le traitement est susceptible d'engendrer un
risque, s'il est non occasionnel, ou s'il porte sur des données
sensibles ou pénales. En pratique, la quasi-totalité des
organisations doivent tenir un registre. Un même éditeur peut
même devoir tenir deux registres : l'un pour ses traitements
internes (responsable), l'autre pour les traitements effectués
pour ses clients (sous-traitant).

#### Réponse 2 : **C**

L'AIPD est obligatoire **lorsque le traitement est susceptible
d'engendrer un risque élevé** pour les droits et libertés des
personnes (article 35.1). L'article 35.3 cite trois cas explicites
(profilage à effets significatifs, traitement à grande échelle de
données sensibles, surveillance systématique d'une zone publique),
et la CNIL publie en France une liste complémentaire. Plusieurs
critères combinés (au moins deux) suggèrent généralement la
nécessité d'une AIPD. La CNIL publie aussi une liste de
traitements exemptés.

#### Réponse 3 : **B**

Selon les lignes directrices CNIL de 2020 et 2021, les boutons
« Accepter », « Refuser » et « Personnaliser » doivent être
équivalents visuellement (même taille, même couleur, même mise
en forme). Donner plus de visibilité au bouton d'acceptation
constitue un *dark pattern* susceptible d'invalider le
consentement. Le refus doit être aussi simple à exprimer que
l'acceptation. Le consentement implicite (par défilement,
inactivité) n'est pas valable. Plusieurs sanctions CNIL ont
visé des sites contrevenant à ces principes (Google, Amazon,
TikTok, etc.).

#### Réponse 4 : **C**

L'article 28.3 du RGPD énumère précisément les clauses
obligatoires d'un DPA, qui doivent prévoir notamment : que le
sous-traitant traite les données sur instruction documentée, que
les personnes autorisées s'engagent à la confidentialité, que
les mesures de sécurité de l'article 32 sont prises, que la
sous-sous-traitance est encadrée, que le sous-traitant aide le
responsable à respecter les droits des personnes et ses propres
obligations, qu'il notifie les violations, qu'il restitue ou
supprime les données à la fin, et qu'il se soumet à des audits.
Un DPA dépourvu d'une de ces clauses est non conforme.

#### Réponse 5 : **C**

La consultation préalable de l'article 36 intervient **lorsque
l'AIPD identifie des risques résiduels élevés** malgré les
mesures envisagées. C'est un cas relativement rare : on ne
consulte la CNIL préalablement que lorsque l'analyse de risque
révèle que les mesures classiques sont insuffisantes. La CNIL
dispose alors de 8 semaines (prolongeables) pour donner son avis,
ses recommandations, voire interdire le traitement. Le
responsable peut prudemment consulter la CNIL même hors cas
strict, par mesure de précaution sur des projets très sensibles
(ex : profilage politique vu en partie 2).

### Réponses aux questions ouvertes

#### Réponse 1

**Politique de confidentialité vs mentions d'information
contextuelles**

La **politique de confidentialité** est un document complet et
général, accessible en permanence depuis le site (typiquement
via un lien en pied de page). Elle couvre l'ensemble des
traitements de l'organisation, présente une vue d'ensemble, et
sert de référence. Elle est consultée par les utilisateurs qui
souhaitent approfondir, par les partenaires qui évaluent
l'organisation, et par les autorités en cas de contrôle.
Caractéristiques : exhaustive, détaillée, structurée, versionnée.

Les **mentions d'information contextuelles** (parfois appelées
« notices courtes » ou « notices in-form ») sont des informations
**ciblées au moment de la collecte**. Elles accompagnent un
formulaire d'inscription, une demande de consentement, une
collecte de données. Elles sont courtes (3 à 5 lignes), centrées
sur la finalité spécifique de cette collecte, et renvoient à la
politique complète pour les détails. Caractéristiques : brèves,
ciblées, immédiates.

**Pourquoi elles sont complémentaires** :

- La politique complète **ne dispense pas** des mentions
  contextuelles. L'article 13 exige une information **préalable**
  à la collecte, donc visible au moment où l'utilisateur saisit
  ses données. Renvoyer simplement à la politique générale est
  insuffisant.
- Les mentions contextuelles **ne dispensent pas** de la
  politique complète. L'utilisateur doit pouvoir, à tout moment,
  consulter une vision globale et détaillée des traitements.
- Ensemble, elles couvrent les besoins : information ciblée au
  bon moment (mentions) + référence approfondie disponible en
  permanence (politique).

**Exemple concret** : sur un site e-commerce, le formulaire
d'inscription affiche une mention courte expliquant que les
données collectées servent à créer le compte, avec un lien
« en savoir plus » qui pointe vers la politique de
confidentialité complète. C'est cette articulation qui satisfait
l'obligation d'information de manière conforme et ergonomique.

#### Réponse 2

**Démarche en cas de sous-traitant SaaS américain sans DPA**

**Étape 1 - Évaluation immédiate**

- *Identifier le sous-traitant* : nom exact, entité contractante,
  localisation des serveurs, types de données traitées.
- *Cartographier les données* : quelles catégories de données
  passent par ce sous-traitant ? Données identifiantes ? Données
  sensibles ? Volume ?
- *Inventaire des risques* : transferts vers les USA sans
  encadrement (article 44), absence de DPA (article 28),
  potentielle violation continue.

**Étape 2 - Risques encourus**

- *Sanction CNIL* : amende possible jusqu'à 20 M€ ou 4 % du CA
  mondial pour manquements aux articles 28 et 44.
- *Préjudice réputationnel* : en cas de plainte ou de contrôle,
  publication possible de la décision.
- *Exposition contractuelle* : si une violation survient et que
  le DPA n'existe pas, la responsabilité est intégralement
  portée par l'organisation, sans recours contre le
  sous-traitant.

**Étape 3 - Actions immédiates**

- *Évaluer la criticité du service* : peut-on suspendre son
  usage le temps de régulariser ?
- *Bloquer toute extension* : pas de nouveau projet engageant
  ce sous-traitant tant que la situation n'est pas régularisée.

**Étape 4 - Régularisation**

Deux options :

*Option A - Négocier un DPA avec ce sous-traitant* :

- contact officiel par le DPO ;
- demande de DPA standard du sous-traitant + CCT à jour
  (juin 2021) + certification DPF ;
- analyse critique du DPA reçu (notification, audit, restitution,
  sous-sous-traitance) ;
- négociation des points problématiques ;
- conduite d'un TIA (Transfer Impact Assessment) documenté ;
- signature et archivage.

*Option B - Migrer vers une alternative européenne* :

- recherche d'un équivalent UE (Welcome to the Jungle, JobAffinity,
  Beetween en recrutement) ;
- évaluation comparative (fonctionnalités, prix, intégration) ;
- négociation du DPA dès la phase de proposition ;
- planification d'une migration progressive.

**Étape 5 - Évaluation a posteriori**

- vérifier si des violations ont déjà eu lieu (logs d'accès,
  exfiltration possible) ;
- si une violation est probable : qualification au sens de
  l'article 33, notification CNIL en 72 heures si applicable.

**Étape 6 - Documentation**

- inscription au registre des traitements ;
- inscription au registre des violations si pertinent ;
- conservation de la chronologie pour démontrer la diligence ;
- mise à jour de la politique de confidentialité avec mention
  du transfert (si maintenu).

**Étape 7 - Prévention**

- mise en place d'un processus interne empêchant l'engagement
  d'un nouveau sous-traitant sans DPA signé ;
- formation des équipes (notamment achats, RH, marketing) ;
- revue annuelle de tous les sous-traitants.

**Recommandation pratique** : sauf nécessité opérationnelle
contraignante, l'option B (migration vers une alternative
européenne) est préférable. Elle élimine les risques juridiques
liés à Schrems II et à l'instabilité du DPF, et simplifie
durablement la conformité.

#### Réponse 3

**Méthodologie CNIL en 4 étapes pour conduire une AIPD**

**Étape 1 - Description du traitement**

- *Acteurs* : équipe métier (finalités, usages), équipe technique
  (architecture, flux de données, sécurité), DPO (cadrage).
- *Livrables* : description structurée du traitement (8 à 15
  pages), schémas de flux, liste exhaustive des données et des
  acteurs.
- *Questions clés* : Quelles sont les finalités exactes ?
  Quelles données sont collectées ? Auprès de qui ? Stockées
  où ? Qui y accède ? Combien de temps ? Quelle base légale ?
  Quelles mesures déjà prévues ?

**Étape 2 - Nécessité et proportionnalité**

- *Acteurs* : DPO (pilote), juridique (validation), métier
  (justification des choix).
- *Livrables* : analyse argumentée principe par principe du
  RGPD, identification des points à améliorer.
- *Questions clés* : La finalité est-elle légitime et explicite ?
  La base légale est-elle appropriée ? Les données sont-elles
  strictement nécessaires (minimisation) ? Les durées sont-elles
  proportionnées ? L'information est-elle complète ? Les droits
  sont-ils exerçables ? Les sous-traitants sont-ils encadrés ?

**Étape 3 - Étude des risques pour les personnes**

- *Acteurs* : équipe technique (analyse des vulnérabilités),
  RSSI (mesures de sécurité), DPO (analyse globale).
- *Livrables* : matrice des risques avec vraisemblance et
  gravité, identification des risques résiduels.
- *Questions clés* : Quels sont les scénarios d'accès illégitime
  envisageables ? De modification non autorisée ? De perte ou
  destruction ? Quelle est la vraisemblance de chaque scénario ?
  Quelle gravité pour les personnes ? Quelles mesures
  pourraient-elles réduire ces risques ?

**Étape 4 - Mesures retenues et validation**

- *Acteurs* : DPO (synthèse), direction (validation),
  responsable de traitement (décision finale).
- *Livrables* : plan d'action des mesures complémentaires,
  décision motivée, AIPD validée signée, éventuelle
  consultation préalable CNIL.
- *Questions clés* : Quelles mesures supplémentaires
  permettent de ramener les risques résiduels à un niveau
  acceptable ? Le bilan global est-il satisfaisant ? Faut-il
  consulter la CNIL préalablement (article 36) ? Quel calendrier
  pour la mise en œuvre des mesures ? Quand prévoir la
  réévaluation ?

**Outil mobilisé** : le **logiciel PIA** gratuit et open source
de la CNIL guide pas à pas chacune de ces étapes. Il génère un
rapport complet exportable en PDF, qui peut servir de référence
durable.

**Acteurs transversaux à toutes les étapes** :

- *Le DPO* est l'orchestrateur central. Il conseille
  obligatoirement (article 35.2), supervise la méthodologie,
  valide la qualité.
- *Le responsable de traitement* porte la décision finale et la
  responsabilité juridique.
- *Les personnes concernées* peuvent être consultées (panel,
  enquête), bonne pratique sur les sujets sensibles.

**Durée typique** : 1 à 3 mois pour une AIPD complète sur un
traitement important. Cette durée permet la consultation des
différents acteurs et la réflexion approfondie. Une AIPD bâclée
en une semaine ne vaut généralement rien.

## Conclusion du module

### Ce que vous avez appris

Vous repartez de ce module avec une **vraie maîtrise documentaire
de la conformité RGPD**. Concrètement, vous savez : constituer
et maintenir un registre des activités de traitement complet,
conduire une AIPD selon la méthodologie CNIL en quatre étapes,
rédiger une politique de confidentialité claire et conforme,
négocier et formaliser des accords de sous-traitance, et déployer
un dispositif cookies respectant les recommandations CNIL.

Vous avez aussi acquis une **vision systémique** de la conformité
RGPD. Vous comprenez désormais que les six modules forment un
tout cohérent : connaissance des fondamentaux (modules 1 et 2),
respect des droits des personnes (module 3), Privacy by Design
(module 4), sécurité technique (module 5), et documentation
opérationnelle (module 6). Aucun de ces aspects ne suffit
isolément ; c'est leur combinaison qui crée une conformité réelle
et défendable.

### Aller plus loin

Pour approfondir et rester à jour, plusieurs ressources sont
incontournables :

- **Le site CNIL** (cnil.fr) : modèles, guides, outil PIA,
  recommandations, mises à jour régulières. C'est la référence
  pratique numéro un en France.
- **Le site du CEPD** (edpb.europa.eu) : lignes directrices
  européennes harmonisées, qui font autorité dans l'interprétation
  du RGPD.
- **Eur-Lex** : texte officiel du RGPD et de ses amendements
  éventuels.
- **Les blogs juridiques spécialisés** : Mathias Avocats,
  Cabinet Bensoussan, Cabinet Caprioli, qui décryptent l'actualité
  juridique et la jurisprudence.
- **Les conférences et formations** : Privacy Summit (CNIL),
  conférences de l'AFCDP (Association française des
  correspondants à la protection des données).
- **Les certifications** : CIPP/E (IAPP), DPO certifié AFNOR,
  qui structurent les compétences pour ceux qui souhaitent en
  faire un métier.

### Conseils pour la pratique professionnelle

Quelques conseils concrets pour faire de la conformité un
allié quotidien :

- **Documentez au fur et à mesure** : créer le registre, l'AIPD,
  la politique au lancement d'un nouveau projet coûte peu ; les
  rattraper après six mois coûte cher.
- **Impliquez le DPO en amont** : ne pas attendre la phase
  juridique pour solliciter le DPO. Son expertise est précieuse
  dès la conception, pour éviter de mauvais choix structurants.
- **Préférez les outils dédiés** : un tableur peut suffire au
  début, mais un outil spécialisé (Dastra, Witik) devient vite
  rentable dès qu'on dépasse une vingtaine de traitements.
- **Privilégiez les sous-traitants européens** : moins de
  complexité juridique, plus de stabilité, et un soutien à
  l'écosystème numérique européen.
- **Préparez-vous à un contrôle** : faire une simulation interne
  de contrôle CNIL une fois par an permet d'identifier les
  faiblesses et de progresser sereinement.
- **Communiquez en interne** : la conformité n'est pas l'affaire
  du seul DPO. Tous les métiers doivent comprendre les
  obligations, les bons réflexes, les écueils. Un programme de
  sensibilisation régulier est crucial.

### Ressources complémentaires

- **Articles 5, 13, 14, 28, 30, 32, 35 et 36 du RGPD** :
  eur-lex.europa.eu.
- **Modèles de registres et d'AIPD** : cnil.fr.
- **Outil PIA** : cnil.fr/fr/outil-pia.
- **Modèles de DPA (CNIL et Commission UE)** :
  ec.europa.eu/info/law/law-topic/data-protection.
- **Lignes directrices CEPD** sur les transferts, les cookies,
  les AIPD : edpb.europa.eu.
- **CNIL fiches secteur** : santé, RH, marketing, etc.
- **Outils CMP recommandés** : axeptio.eu, didomi.io,
  tarteaucitron.io.

### Mot de fin de formation

Vous voici au terme de la formation complète sur l'intégration des
obligations RGPD dans un projet d'application. Vous avez parcouru
six modules denses, totalisant plus de cent heures de contenu
pédagogique. Vous avez acquis des connaissances juridiques
(fondamentaux, droits des personnes, obligations contractuelles),
des compétences techniques (Privacy by Design, sécurité,
cryptographie), et des savoir-faire opérationnels (documentation,
gestion d'incidents, audit).

Mais surtout, vous avez acquis quelque chose de plus profond : une
**posture professionnelle** qui placera désormais la protection des
données au cœur de votre métier. Vous ne verrez plus une donnée
personnelle comme une simple chaîne de caractères dans une base.
Vous y verrez une personne réelle qui vous a confié quelque chose
d'elle, et qui mérite votre rigueur et votre respect.

Cette posture, vous allez la mettre en pratique dans vos prochains
projets. Vous serez parfois seul à la défendre face à des
pressions de délai, de budget, ou de fonctionnalité. Vous serez
parfois critiqué pour votre vigilance. Tenez bon. Ce sont les
développeurs comme vous qui rendent le numérique digne de
confiance, qui protègent les utilisateurs contre l'arbitraire et
les fuites, qui font progresser la profession.

Le RGPD évoluera, les techniques évolueront, les outils évolueront.
Mais les principes que vous avez intégrés resteront : licéité,
finalité, minimisation, sécurité, responsabilité, respect des
droits. Ces principes sont des **repères durables**, qui
traverseront les modes et les générations technologiques. Vous
êtes désormais armé pour les porter avec compétence.

Bravo pour le travail accompli. Bonne chance dans la suite de
votre parcours. Et surtout, continuez à apprendre, à douter, à
progresser. C'est la marque des bons professionnels.
