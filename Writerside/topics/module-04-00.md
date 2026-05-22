# Privacy by Design et Privacy by Default

## Introduction

Vous arrivez sur un nouveau projet : une jeune équipe de cinq
développeurs travaille depuis huit mois sur une application mobile
prometteuse. Le code est élégant, les tests passent, le design est
soigné. À deux semaines du lancement public, votre client demande un
audit RGPD. Vous découvrez alors que la base de données contient des
mots de passe en clair, que les données de tous les utilisateurs
sont mélangées dans une seule table sans séparation, que les
sauvegardes nocturnes envoyées chez un prestataire américain ne sont
pas chiffrées, et qu'aucune politique de conservation n'a été
définie. Le DPO refuse la mise en production. L'équipe est dépitée :
« Pourquoi on n'a pas pensé à ça depuis le début ? ». La réponse est
simple : parce que personne ne leur a parlé de Privacy by Design.

Cette anecdote, malheureusement très fréquente, illustre la
différence fondamentale entre un projet où la conformité est
**rattrapée en fin de course**, et un projet où elle est **intégrée
dès la conception**. Dans le premier cas, on subit des refontes
coûteuses, des compromis techniques, des retards de mise en
production. Dans le second cas, on livre dans les temps une
application conforme, performante et défendable juridiquement.
C'est tout l'enjeu de ce module : vous donner les outils pour
intégrer la protection des données dans votre ADN de développeur.

Le concept de **Privacy by Design** (PbD) a été formalisé dans les
années 1990 par Ann Cavoukian, alors commissaire à l'information et
à la protection de la vie privée de l'Ontario, au Canada. Sa
proposition tient en une phrase : la protection de la vie privée
doit être pensée dès la conception des systèmes, pas ajoutée à la
fin. Cette idée, qui peut paraître évidente aujourd'hui, a mis vingt
ans à s'imposer. Elle est désormais inscrite à l'article 25 du
RGPD, qui en fait une obligation juridique sous le nom de
« protection des données dès la conception et par défaut ».

Imaginez la différence entre construire une maison écologique dès
les plans (isolation intégrée, orientation optimale, matériaux
durables) et essayer de la rendre écologique après coup (ajouter
des panneaux solaires, refaire l'isolation, changer les fenêtres).
Dans le premier cas, le surcoût est minime et l'efficacité maximale.
Dans le second, le coût explose pour un résultat dégradé. La
Privacy by Design, c'est la même logique appliquée à la protection
des données. Plus on intègre tôt, moins ça coûte cher et mieux ça
fonctionne.

Ce module est probablement le plus technique de toute la formation.
Vous allez y découvrir non seulement la doctrine officielle, mais
aussi les **patterns d'architecture** concrets que les développeurs
expérimentés mobilisent au quotidien : pseudonymisation,
anonymisation, chiffrement applicatif, séparation des données, data
vault, gestion fine des durées de conservation. Vous apprendrez
également à arbitrer les choix d'infrastructure qui ont des
conséquences juridiques majeures : héberger en France ou ailleurs,
utiliser un SaaS américain ou européen, gérer un transfert
international.

À l'issue de ce module, vous ne verrez plus jamais une nouvelle
fonctionnalité comme un simple objet technique. Vous y verrez
automatiquement un cycle de vie de la donnée, des choix
d'architecture, des risques à mitiger, des défaults à configurer.
Vous serez devenu un architecte de la vie privée.

## Objectifs du module

Au terme de ce module, vous serez capable de :

1. Énoncer les sept principes fondateurs de la Privacy by Design
   formulés par Ann Cavoukian, et expliquer comment ils sont
   incorporés à l'article 25 du RGPD.
2. Maîtriser les patterns d'architecture techniques qui protègent
   la vie privée : pseudonymisation, anonymisation, chiffrement,
   séparation des données, data vault, et comprendre quand
   mobiliser chacun.
3. Arbitrer en connaissance de cause les choix d'infrastructure
   ayant un impact RGPD : self-hosting versus SaaS, localisation
   des serveurs, sous-traitance, transferts internationaux après
   Schrems II et le Data Privacy Framework.
4. Modéliser le cycle de vie complet d'une donnée personnelle, de
   sa collecte jusqu'à son effacement ou son anonymisation, en
   intégrant les durées de conservation et les obligations légales.
5. Implémenter techniquement la suppression et l'archivage
   automatisés (cron jobs, soft-delete, anonymisation différée)
   pour garantir le respect du principe de limitation de la
   conservation.
