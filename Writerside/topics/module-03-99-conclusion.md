# Conclusion du module 3

Vous voici au terme de ce troisième module, consacré aux droits des
personnes concernées. Ce module marque un tournant dans votre
formation : nous quittons le terrain purement juridique pour entrer
sur celui de l'implémentation technique concrète. Chaque droit que
nous avons étudié se traduit, dans votre quotidien de développeur,
par un endpoint, une interface, une procédure, un modèle de données.

Nous avons d'abord exploré l'**obligation d'information préalable**
des articles 13 et 14. Vous savez désormais distinguer la collecte
directe (sous votre formulaire) de la collecte indirecte (auprès
d'un tiers), et fournir l'information requise au bon moment, dans
un langage clair, avec une approche en plusieurs niveaux pour
concilier exhaustivité et lisibilité.

Vous avez ensuite découvert les **quatre droits actifs** : accès,
rectification, effacement, portabilité. Pour chacun, vous savez
quoi fournir, dans quel format, et comment l'implémenter dans une
architecture moderne. Vous avez vu que l'accès ne se limite pas à
un `SELECT * FROM users` : il englobe toutes les sources de
données, internes et externes, et impose un travail de
cartographie préalable. Vous avez compris que l'effacement est
souvent partiel, avec une conservation imposée par d'autres lois,
et qu'il doit être tracé. Vous avez maîtrisé le format de l'export
de portabilité (JSON structuré, schéma documenté).

Vous avez enfin parcouru les **trois droits défensifs** : limitation
du traitement, opposition, et le régime particulier des décisions
automatisées de l'article 22. Vous savez désormais qu'une opposition
à la prospection est absolue et immédiate, qu'une opposition pour
motifs particuliers s'examine au cas par cas, et qu'une décision
purement algorithmique avec effet significatif appelle des garanties
spécifiques (intervention humaine, droit à l'explication,
contestation).

Sur le plan opérationnel, vous savez gérer les **délais et
modalités** : un mois pour répondre, prorogeable de deux mois si
nécessaire, gratuité de principe, vérification d'identité préalable,
réponse motivée même en cas de refus.

Vous repartez de ce module avec une **boîte à outils complète** pour
implémenter les droits dans n'importe quel projet : modèles de
tables techniques, spécifications d'endpoints, patterns
d'architecture, parcours utilisateur, textes d'information. Cette
boîte à outils, c'est ce qui transforme un développeur sensibilisé
au RGPD en un véritable artisan de la conformité.

## Auto-évaluation

### Questions à choix multiples

**Question 1** : Quel est le délai de réponse standard à une demande
d'exercice des droits, prévu par le RGPD ?

- A. 72 heures
- B. 1 semaine
- C. 1 mois prorogeable de 2 mois
- D. 6 mois

---

**Question 2** : Lequel des droits suivants ne s'applique PAS lorsque
le traitement repose sur la base de l'obligation légale ?

- A. Le droit d'accès
- B. Le droit de rectification
- C. Le droit à l'effacement
- D. Le droit à la portabilité

---

**Question 3** : Une utilisatrice s'oppose à recevoir vos
newsletters marketing. Quelle est votre obligation ?

- A. Examiner si ses motifs sont légitimes avant de cesser l'envoi
- B. Cesser l'envoi immédiatement, sans examen possible
- C. Demander une justification écrite avant toute action
- D. Maintenir l'envoi tant que le contrat est en cours

---

**Question 4** : Selon l'article 22 du RGPD, lequel de ces droits
n'est PAS systématiquement reconnu à la personne dans le cadre
d'une décision automatisée ?

- A. L'intervention humaine
- B. L'expression d'un point de vue
- C. La contestation de la décision
- D. L'annulation automatique de la décision

---

**Question 5** : Lors d'un export au titre du droit à la portabilité,
lequel des éléments suivants n'est PAS obligatoire ?

- A. Un format structuré
- B. Un format couramment utilisé
- C. Un format lisible par machine
- D. Un format compatible avec tous les SGBD existants

### Questions ouvertes

**Question 1** : Expliquez en quelques phrases la différence entre
le droit à l'effacement et le droit à la limitation du traitement.
Donnez un exemple où la limitation serait plus appropriée que
l'effacement.

---

**Question 2** : Un utilisateur vous demande l'export de ses données.
Vous lui fournissez un PDF de 35 pages contenant toutes ses
informations sous forme de paragraphes en français. Est-ce
conforme au droit à la portabilité ? Justifiez.

---

**Question 3** : Vous concevez un endpoint d'effacement de compte
pour une application e-commerce. Quels traitements faut-il prévoir
en cascade lorsqu'un utilisateur déclenche son droit à
l'effacement ? Indiquez ce que vous supprimez, ce que vous
conservez, et pourquoi.

## Corrections des auto-évaluations {collapsible="true"}

### Réponses aux QCM

#### Réponse 1 : **C**

L'article 12.3 prévoit un délai d'un mois, prorogeable de deux mois
supplémentaires en cas de complexité, à condition d'informer la
personne dans le délai initial avec les motifs de la prorogation.

#### Réponse 2 : **D**

Le droit à la portabilité (article 20) ne s'applique que lorsque le
traitement repose sur le consentement ou sur l'exécution d'un
contrat. Les traitements fondés sur une obligation légale en sont
exclus. Les autres droits (accès, rectification, et selon les cas
l'effacement) restent applicables même sur une base d'obligation
légale.

#### Réponse 3 : **B**

L'article 21.2 prévoit que la personne peut s'opposer à la
prospection commerciale à tout moment, sans avoir à se justifier.
La cessation doit être immédiate. Aucun examen de motifs n'est
possible : c'est un droit absolu.

#### Réponse 4 : **D**

L'article 22.3 garantit trois droits dans le cadre des décisions
automatisées admises par exception : l'intervention humaine,
l'expression du point de vue, et la contestation. L'annulation
automatique n'est pas un droit prévu par le texte : la décision
peut être maintenue après examen humain.

#### Réponse 5 : **D**

L'article 20 exige un format structuré, couramment utilisé et
lisible par machine (par exemple JSON, XML, CSV). Il n'est pas
exigé de compatibilité avec tous les SGBD existants ; cela serait
techniquement infaisable et n'apparaît dans aucun texte.

### Réponses aux questions ouvertes

#### Réponse 1

Le **droit à l'effacement** (article 17) entraîne la suppression
définitive des données. Le **droit à la limitation** (article 18)
ne supprime rien : il fige les données dans leur état actuel et
interdit toute opération de traitement actif, à l'exception de la
conservation pure.

La limitation est plus appropriée lorsque la personne souhaite
conserver ses données mais en suspendre l'usage. Exemple typique :
un utilisateur conteste l'exactitude de certaines informations le
concernant. En attendant la vérification, il peut demander la
limitation du traitement, ce qui empêche la diffusion ou
l'utilisation des données contestées sans pour autant les
supprimer. Une fois la vérification effectuée, le traitement
reprend (ou non) son cours normal.

#### Réponse 2

Cela **n'est pas conforme** au droit à la portabilité tel que
défini à l'article 20. Le RGPD exige un format **structuré,
couramment utilisé, et lisible par machine**. Un PDF rédactionnel
de 35 pages, lisible par un humain mais difficile à parser
automatiquement, ne satisfait pas à cette exigence.

Le format approprié serait JSON, XML ou CSV, éventuellement
accompagné d'une documentation de schéma pour faciliter la
réutilisation par une autre application. Un PDF reste pertinent
pour le droit d'accès (article 15), où la lisibilité humaine prime,
mais pas pour la portabilité. En pratique, il est de bon ton de
proposer les deux : un JSON pour la portabilité technique et un PDF
résumé pour la lecture humaine.

#### Réponse 3

Pour une application e-commerce, l'effacement en cascade implique :

À **supprimer immédiatement** :

- les données de profil (nom, prénom, email, téléphone, adresse,
  préférences) ;
- les listes de souhaits et paniers en cours ;
- les avis publiés (ou anonymisation s'ils restent visibles
  publiquement) ;
- les consentements et préférences ;
- les notifications de marketing chez l'ESP.

À **conserver pour obligation légale** :

- les factures et les commandes : 10 ans (Code de commerce). Les
  données nominatives associées peuvent être anonymisées (remplacer
  nom/email par des valeurs factices) tout en conservant les
  montants et les références.
- les preuves de paiement si exigées par la lutte anti-blanchiment.

À **anonymiser** :

- les logs récents (selon politique de conservation), généralement
  6 mois à 1 an.

À **notifier** :

- les sous-traitants (CRM, ESP, agrégateurs) pour qu'ils effacent
  ou anonymisent à leur tour.

À **tracer** :

- enregistrement dans un journal d'effacement avec hash anonymisé
  de l'identifiant utilisateur, date, motif, et liste des données
  conservées avec leur justification légale.

L'ensemble doit être atomique (transaction SQL) et confirmé à
l'utilisateur par un email récapitulatif.

## Conclusion du module

### Ce que vous avez appris

Vous repartez de ce module avec une compréhension opérationnelle
complète des droits des personnes concernées. Concrètement, vous
savez : rédiger des mentions d'information conformes aux articles 13
et 14, implémenter les quatre droits actifs (accès, rectification,
effacement, portabilité), gérer les droits défensifs (limitation,
opposition, décisions automatisées), respecter les délais et les
modalités de réponse, et concevoir un module utilisateur intégré
qui industrialise tout cela.

Vous avez surtout acquis une **vision technique** : chaque droit
correspond à un endpoint, à un parcours, à un modèle de données.
Cette vision vous permet d'intégrer le RGPD dès la phase de
conception, plutôt que de le rattraper en fin de projet.

Vous êtes maintenant prêt à aborder les modules suivants, qui
exploreront le Privacy by Design (comment penser la conformité dès
l'architecture), la sécurité (comment protéger les données
techniquement), la documentation (comment formaliser tout cela), et
le travail d'équipe (comment dialoguer avec DPO, client, et
collègues).

### Aller plus loin

Pour consolider et approfondir vos acquis, vous pouvez :

- consulter les **fiches pratiques de la CNIL** sur les droits des
  personnes (accès, effacement, portabilité), qui détaillent
  l'interprétation officielle des textes ;
- lire les **lignes directrices du CEPD n°1/2022** sur le droit
  d'accès, qui clarifient le périmètre exact ;
- étudier les **lignes directrices du CEPD n°5/2020** sur le
  consentement, en lien avec le droit de retrait ;
- explorer les **lignes directrices du G29 sur la portabilité** et
  sur les décisions automatisées, qui restent des références ;
- analyser les **décisions CNIL** récentes sur les manquements aux
  droits (notamment difficultés d'effacement et opposition au
  marketing) ;
- s'inscrire au **MOOC de la CNIL** « L'atelier RGPD », qui couvre
  ces sujets avec des cas pratiques.

### Conseils pour la pratique professionnelle

Quelques conseils concrets pour intégrer ces acquis dans votre
quotidien :

- **Concevez l'espace utilisateur RGPD dès le sprint zéro** : la
  page « Mes données personnelles » doit faire partie du backlog
  initial, pas être ajoutée en fin de projet.
- **Cartographiez les sources de données** avant tout : c'est ce qui
  permet de répondre complètement à une demande d'accès. Mettez à
  jour cette cartographie à chaque évolution de l'architecture.
- **Industrialisez le suivi des demandes** : une table dédiée, un
  tableau de bord, des alertes sur les délais. Cela évite les
  oublis et fournit un KPI de conformité utile en audit.
- **Testez le parcours d'effacement** régulièrement : c'est le plus
  complexe et celui qui révèle les oublis. Un *bug* sur l'effacement
  est rapidement repéré par les utilisateurs et rapporté à la CNIL.
- **Privilégiez le JSON pour la portabilité** : c'est le format le
  plus universel, supporté par tous les langages et les
  utilisateurs avancés.
- **Évitez les dark patterns** dans le parcours d'effacement : pas
  de bouton « Supprimer » caché ou désactivé, pas de procédure à
  rallonge. La CNIL sanctionne désormais les obstacles déloyaux.

### Ressources complémentaires

- **Articles 12 à 22 du RGPD** : eur-lex.europa.eu (textes
  officiels).
- **Lignes directrices CEPD n°1/2022** sur le droit d'accès :
  edpb.europa.eu.
- **Lignes directrices G29** sur la portabilité et sur les
  décisions automatisées.
- **Guide CNIL** sur les droits des personnes : cnil.fr.
- **Outil PIA** de la CNIL pour les AIPD : cnil.fr.
- **Fiches techniques** de la CNIL sur l'effacement,
  l'anonymisation, et la pseudonymisation.

### Mot de fin

Bien implémenter les droits des personnes, c'est plus qu'une
obligation légale : c'est un acte de respect envers vos utilisateurs.
Les applications qui rendent visible et facile l'exercice de ces
droits gagnent en confiance, en réputation et finalement en
performance commerciale. Vous venez de construire un savoir-faire
technique très demandé : celui d'un développeur capable de
transformer un texte juridique en lignes de code. Vous franchissez
une étape importante de votre montée en compétences.
