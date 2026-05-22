# La sécurité des données et les mesures techniques

## Introduction

Imaginez le scénario suivant. Un lundi matin, en arrivant au bureau,
vous découvrez votre boîte de réception inondée d'alertes : des
milliers de comptes utilisateurs de votre application ont été
publiés sur un forum spécialisé. Emails, mots de passe hachés
faiblement, adresses postales, historiques d'achat. Le téléphone
sonne : c'est la direction. Le DPO arrive en urgence. Les
journalistes commencent à appeler. Vous avez 72 heures pour notifier
la CNIL, sous peine de sanction supplémentaire. Et vous découvrez
que personne, dans l'entreprise, ne sait exactement comment
procéder. Ce moment, qui semble cauchemardesque, est devenu réalité
pour des centaines d'entreprises ces dernières années. Ce module
vous prépare à ne **jamais** vous y retrouver, et si malgré tout
cela arrivait, à savoir exactement quoi faire.

La sécurité des données n'est pas un sujet annexe du RGPD : c'est
l'une de ses **obligations fondamentales**, posée par l'article 32.
Au-delà du règlement européen, c'est aussi un sujet de
responsabilité professionnelle, de réputation, et de survie
économique. Une violation de données mal gérée peut détruire une
entreprise en quelques semaines. Une violation bien gérée peut être
absorbée sans dégâts irréparables. La différence ? La préparation,
la rigueur technique, et la maîtrise des procédures.

Pensez à la sécurité comme à la santé d'une personne. On ne devient
pas en bonne santé en faisant un check-up médical de temps en
temps : on entretient sa santé tous les jours par des habitudes
saines. Pareil pour la sécurité d'une application : ce ne sont pas
les audits ponctuels qui protègent, c'est la rigueur quotidienne
des pratiques. Chaque ligne de code, chaque configuration de
serveur, chaque accès accordé est une occasion de renforcer ou
d'affaiblir la sécurité globale.

Ce module est l'un des plus opérationnels de la formation. Vous y
trouverez du code, des exemples de configuration, des commandes
techniques, des procédures détaillées. Vous allez apprendre à
implémenter concrètement les mesures de sécurité exigées par
l'article 32 : chiffrement au repos et en transit, hachage robuste
des mots de passe, authentification forte, gestion fine des accès,
journalisation, sauvegardes. Vous allez aussi maîtriser une
compétence rare et précieuse : savoir gérer techniquement et
opérationnellement une violation de données, depuis la détection
jusqu'à la notification CNIL.

Surtout, ce module va vous donner une **posture professionnelle**.
Un développeur conscient de la sécurité ne stocke jamais un mot de
passe en clair. Ne commit jamais un secret dans Git. Ne désactive
jamais TLS « pour debugger plus vite ». Ne donne jamais les droits
administrateur à un service applicatif. Ces réflexes, anodins
individuellement, font la différence entre une application
défendable et une bombe à retardement juridique.

Plus largement, la sécurité est aussi un enjeu **éthique**. Les
utilisateurs vous confient leurs données par défaut, sans vérifier
ce que vous en faites. C'est un acte de confiance considérable que
vous ne devez pas trahir. Bien protéger les données, c'est respecter
l'engagement implicite que vous prenez à chaque inscription.

## Objectifs du module

Au terme de ce module, vous serez capable de :

1. Énoncer et appliquer les mesures techniques et organisationnelles
   exigées par l'article 32 du RGPD, en fonction des risques propres
   à chaque traitement.
2. Implémenter les fondamentaux de la sécurité applicative :
   authentification forte, contrôle d'accès basé sur les rôles
   (RBAC), gestion sécurisée des sessions et des secrets.
3. Maîtriser les techniques de protection des données : hachage
   robuste des mots de passe (Argon2, bcrypt), chiffrement en
   transit (TLS) et au repos, gestion des clés.
4. Identifier et corriger les vulnérabilités du code sous l'angle
   RGPD, à travers une lecture critique de l'OWASP Top 10 et une
   politique de gestion des dépendances et des secrets.
5. Mettre en œuvre une journalisation efficace (audit trail) et une
   stratégie de sauvegardes conforme au principe de disponibilité.
6. Gérer une violation de données conformément aux articles 33 et
   34 du RGPD : détection, qualification, notification CNIL sous
   72 heures, information des personnes concernées.
