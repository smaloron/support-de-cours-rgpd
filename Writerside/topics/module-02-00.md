# Les 7 principes fondamentaux et les bases légales

## Introduction

Vous lancez votre IDE, vous créez une nouvelle table dans votre base de
données, vous ajoutez une colonne `marketing_consent` parce que votre
product owner vous l'a demandé, et vous passez à la fonctionnalité
suivante. Cinq mois plus tard, lors d'un audit de conformité, un
juriste vous demande : « Quelle est la finalité de cette donnée ? Sur
quelle base légale repose son traitement ? Avez-vous documenté votre
choix ? Pouvez-vous prouver le consentement de chaque utilisateur ? ».
Silence gêné dans la salle. Personne ne sait répondre, et le projet
de mise en production de la fonctionnalité est suspendu.

Cette scène, malheureusement très fréquente dans les entreprises
françaises, illustre une vérité fondamentale : connaître le RGPD ne
suffit pas, il faut savoir l'appliquer concrètement à chaque
traitement. Or, à la base de cette application opérationnelle, deux
piliers se dressent : les **7 principes fondamentaux** de l'article 5,
et les **6 bases légales** de l'article 6. Sans la maîtrise de ces
deux piliers, impossible de raisonner correctement sur un traitement
de données, impossible de défendre une architecture devant un DPO,
impossible de remplir un registre, impossible de répondre à un
contrôle. Ces deux piliers, c'est la grammaire fondamentale du RGPD.

Imaginez que vous appreniez à conduire sans connaître le code de la
route. Vous savez démarrer la voiture, passer les vitesses, freiner,
mais vous n'avez jamais lu un panneau de signalisation. Vous roulez
à 130 km/h dans une zone 30, vous brûlez les stops, vous prenez les
sens interdits. Pendant un moment, ça passe. Puis viennent
l'accident, la sanction, le retrait de permis. Les principes
fondamentaux et les bases légales du RGPD, c'est exactement le code
de la route du développeur d'applications. Sans eux, vous codez à
l'aveugle ; avec eux, chaque décision technique trouve sa
justification.

La bonne nouvelle, c'est que ces principes ne sont pas si nombreux et
qu'une fois compris, ils deviennent des réflexes naturels. Le RGPD a
été pensé pour être lisible : 99 articles, dont l'article 5 (les 7
principes), l'article 6 (les 6 bases légales), et l'article 9 (les
données sensibles) constituent à eux trois le cœur opérationnel.
Maîtriser ces trois articles, c'est posséder l'essentiel pour
travailler avec rigueur. Ce module va vous y conduire.

Dans la pratique professionnelle, ces notions reviennent à chaque
sprint : lorsqu'on conçoit un formulaire d'inscription (quelles
informations demander, sur quelle base légale ?), lorsqu'on définit
une politique de conservation (combien de temps garder les données,
pourquoi ?), lorsqu'on met en place une bannière cookies (consentement
ou intérêt légitime ?), lorsqu'on rédige une politique de
confidentialité (quelles finalités, quels destinataires ?). Chaque
fois, ce sont les 7 principes et les 6 bases légales qui sont
mobilisés. Vous allez les manipuler tellement souvent dans votre
carrière qu'ils deviendront aussi familiers que les patterns de
conception logicielle.

## Objectifs du module

Au terme de ce module, vous serez capable de :

1. Énoncer et expliquer les sept principes fondamentaux du RGPD posés
   à l'article 5, en illustrant chacun d'eux par un exemple concret
   issu du développement d'applications.
2. Identifier la base légale appropriée parmi les six prévues à
   l'article 6 du RGPD pour un traitement de données donné, et
   justifier ce choix.
3. Reconnaître une donnée sensible au sens de l'article 9 et
   appliquer le régime juridique renforcé qui lui correspond.
4. Vérifier la validité d'un consentement (libre, spécifique, éclairé,
   univoque) et concevoir une interface de recueil de consentement
   conforme aux exigences européennes.
5. Articuler les principes et les bases légales pour analyser un
   traitement complexe et produire une justification professionnelle
   défendable devant un DPO ou une autorité de contrôle.
