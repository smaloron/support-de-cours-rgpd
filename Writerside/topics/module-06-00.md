# Documentation et conformité opérationnelle

## Introduction

Imaginez la scène. Vous êtes développeur dans une PME française.
Un beau matin, une lettre recommandée arrive au siège : la CNIL
annonce un contrôle dans deux semaines. Panique générale. Le DPO
cherche le registre des traitements, qui n'a jamais vraiment été
tenu à jour. Le marketing essaie de retrouver les bases légales
des dernières campagnes. Personne ne sait précisément où sont
documentés les transferts de données vers le prestataire d'emailing
américain. La politique de confidentialité, rédigée il y a trois
ans par un stagiaire, ne reflète plus du tout les pratiques
actuelles. Le jour du contrôle, l'inspectrice de la CNIL pose des
questions précises ; les réponses tâtonnent ; les preuves
manquent. Six mois plus tard, l'amende tombe : non pour des
manquements opérationnels graves, mais pour **incapacité à
démontrer la conformité**. C'est l'histoire la plus banale du
contentieux RGPD français.

Cette histoire illustre une vérité essentielle : la conformité RGPD
n'est pas seulement une question de pratiques, c'est aussi une
question de **documentation**. Vous pouvez avoir les meilleures
pratiques du monde, si vous ne pouvez pas le prouver, vous serez
sanctionné. À l'inverse, vous pouvez avoir des pratiques
perfectibles, si elles sont rigoureusement documentées et que vous
démontrez une démarche d'amélioration, vous serez traité avec
clémence. Le RGPD a institué cette philosophie sous le nom de
**responsabilité** (*accountability*), inscrite à l'article 5.2.

Pensez à la documentation comme à un journal de bord en mer. Un
bon capitaine consigne tout : route, vents, manœuvres, incidents.
Si tout va bien, ce journal ne sert à rien. Si quelque chose
arrive, ce journal devient l'outil principal de défense, de
compréhension, et d'amélioration. La documentation RGPD, c'est
exactement la même chose : invisible quand tout va bien,
indispensable dès qu'un contrôle ou un incident survient.

Ce module aborde les **livrables obligatoires ou attendus** du
RGPD : le registre des activités de traitement (article 30),
l'analyse d'impact relative à la protection des données (article
35), la politique de confidentialité et les mentions d'information
(articles 13 et 14), les contrats de sous-traitance (article 28),
et l'épineux sujet des cookies (encadré par la directive ePrivacy
et la loi française). Chacun de ces documents fait l'objet d'une
norme précise. Chacun est attendu par les autorités de contrôle.
Chacun est aussi un **outil de pilotage interne** : le DPO et la
direction y trouvent une vision claire des traitements, des
risques, et des chantiers en cours.

Pour le développeur, ce module a une triple importance.
Premièrement, vous serez souvent sollicité pour **alimenter** ces
documents : décrire les traitements, identifier les sous-traitants,
documenter les choix techniques. Deuxièmement, vous devez
**comprendre** ces documents pour vérifier qu'ils correspondent à
la réalité technique. Troisièmement, vous serez parfois en
**première ligne** pour les rédiger, notamment dans les petites
structures où le rôle de DPO n'est pas pourvu en interne.

Ce module est plus juridique que les précédents, mais il reste
profondément opérationnel. Vous y trouverez des modèles, des
checklists, des exemples concrets. Vous repartirez avec la
capacité de produire chacun de ces livrables à la demande, et
surtout de les maintenir dans le temps. Cette compétence est
particulièrement recherchée sur le marché : peu de développeurs
maîtrisent ces aspects, et ceux qui les maîtrisent prennent
naturellement des responsabilités plus larges (lead, architecte,
consultant).

## Objectifs du module

Au terme de ce module, vous serez capable de :

1. Rédiger un registre des activités de traitement complet et
   conforme à l'article 30, en distinguant le rôle de responsable
   de traitement et de sous-traitant.
2. Conduire une analyse d'impact relative à la protection des
   données (AIPD) selon la méthodologie de la CNIL en quatre
   étapes, et savoir quand elle est obligatoire.
3. Rédiger une politique de confidentialité et des mentions
   d'information conformes aux articles 13 et 14, en privilégiant
   la clarté et la lisibilité.
4. Négocier et conclure un accord de sous-traitance (DPA) conforme
   à l'article 28, avec les clauses obligatoires.
5. Mettre en place une gestion des cookies et traceurs conforme
   aux recommandations CNIL : bandeau, CMP, choix granulaire,
   refus aussi facile que l'acceptation.
6. Organiser dans le temps la production, la mise à jour, et
   l'audit de la documentation de conformité.
