# Les droits des personnes concernées

## Introduction

Imaginez un instant la situation suivante. Vous recevez un email
inattendu, signé par un utilisateur de votre application : « Bonjour,
en application de l'article 15 du RGPD, je vous demande de me
fournir l'intégralité des données me concernant que vous détenez,
ainsi que les destinataires de ces données, dans un délai d'un mois.
À défaut, je saisirai la CNIL. ». Votre chef vous transmet le message
en vous demandant simplement : « Tu peux gérer ? ». Vous ouvrez la
base de données et là, panique : les données de l'utilisateur sont
dispersées dans douze tables, plusieurs services externes, des
sauvegardes, des logs, des fichiers de marketing automatisé. Par où
commencer ? Que devez-vous fournir ? Sous quel format ? Que se
passe-t-il si vous oubliez quelque chose ?

Cette situation, beaucoup plus fréquente qu'on ne le pense, illustre
le cœur de ce module : les **droits des personnes concernées**. Ces
droits sont l'aspect le plus tangible du RGPD pour les utilisateurs.
Tandis que les principes et bases légales restent invisibles, les
droits, eux, se manifestent par des emails reçus, des tickets dans le
support, des demandes formelles parfois véhémentes. Si vous ne savez
pas y répondre techniquement, c'est tout l'édifice de votre conformité
qui s'effondre face à un seul utilisateur déterminé.

L'analogie avec un compte bancaire est éclairante. Quand vous ouvrez
un compte, vous avez le droit de consulter votre solde, vos
opérations, votre historique. Vous pouvez demander une rectification
en cas d'erreur, transférer votre argent vers une autre banque,
fermer votre compte. Personne ne vous oblige à justifier ces
demandes. Le RGPD applique la même philosophie aux données
personnelles : la personne concernée est, dans une large mesure,
maîtresse de ses données. Et le responsable de traitement a
l'obligation, dans des délais courts et selon des modalités précises,
de répondre à ses demandes.

Pour un développeur d'applications, ce module est probablement le
plus pratique de toute la formation. Pourquoi ? Parce qu'à la
différence des modules juridiques, celui-ci se traduit directement en
code. Quand on parle du droit d'accès, on parle d'un endpoint
`GET /me/data` ou d'un export JSON. Quand on parle du droit à
l'effacement, on parle d'une procédure de suppression en cascade
dans toutes les tables. Quand on parle du droit à la portabilité, on
parle d'un format d'export standardisé. Tout cela se conçoit, se
développe, se teste comme n'importe quelle autre fonctionnalité, à
condition de bien comprendre les exigences sous-jacentes.

Plus largement, bien implémenter ces droits, c'est aussi un acte de
respect envers l'utilisateur et un avantage concurrentiel. Les études
le montrent : les utilisateurs sont plus enclins à faire confiance
aux applications qui rendent visible et facile l'exercice de leurs
droits. Inversement, ceux qui se sentent piégés (compte impossible à
supprimer, données impossible à récupérer) deviennent rapidement des
détracteurs publics. Concevoir des parcours « Mes données » fluides
et complets, c'est à la fois une obligation légale et une bonne
pratique produit.

## Objectifs du module

Au terme de ce module, vous serez capable de :

1. Énumérer et expliquer les huit principaux droits des personnes
   concernées prévus aux articles 12 à 22 du RGPD.
2. Rédiger des mentions d'information préalable conformes aux
   articles 13 et 14, adaptées au contexte de la collecte.
3. Concevoir et implémenter techniquement les parcours utilisateur
   correspondants : consultation des données, rectification,
   effacement, portabilité, limitation, opposition.
4. Développer des endpoints REST conformes au droit à la portabilité,
   produisant des exports structurés et lisibles par machine.
5. Articuler ces droits avec les obligations connexes : délais de
   réponse (un mois, prorogeable), vérification d'identité, gestion
   des refus motivés, encadrement des décisions automatisées.
