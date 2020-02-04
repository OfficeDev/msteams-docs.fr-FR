---
title: Mapper vos cas d’utilisation aux fonctionnalités de l’application
author: clearab
description: Décider de la façon de distribuer votre application
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5ebfa73df9b4f2c83533a33fbc6366c2c0ccffb4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673865"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Mapper vos cas d’utilisation sur les fonctionnalités des applications teams

Si vous ne l’avez pas encore fait, vérifiez que vous avez [pris en compte vos cas d’utilisation](~/concepts/design/map-use-cases.md) avec soin. Vous avez également besoin d’une bonne compréhension des [points d’extensibilité et des éléments d’interface utilisateur](~/concepts/extensibility-points.md) disponibles pour votre application. Une fois que vous avez décidé *de votre tentative* de *résolution et de votre responsable,* il est temps de commencer à réfléchir sur *la façon dont*.

Vous trouverez ci-dessous des scénarios courants, ainsi qu’une sélection de points d’extensibilité et d’éléments d’interface utilisateur qui fonctionnent bien avec eux. Il n’est pas destiné à être une liste exhaustive, simplement pour vous aider à réfléchir sur certaines des possibilités dont vous disposez et sur la plateforme Teams.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Créer, partager et collaborer sur des éléments dans un système externe

L’application pour Microsoft teams est un excellent moyen d’interagir avec vos données, et il existe plusieurs points d’intégration parmi lesquels choisir.

* Extensions de messagerie avec commandes de recherche : recherchez les systèmes externes et partagez les résultats en tant que carte interactive.

* Extensions de messagerie avec commandes d’action : collecter des informations à insérer dans un magasin de données ou effectuer des recherches avancées.

* Onglets : créer des expériences Web intégrées pour afficher, utiliser et partager des données.

* Connecteurs et webhooks : moyen simple de transmettre des données dans le client teams et d’envoyer des données.

* Modules de tâches : formulaires modaux interactifs à partir de l’endroit où vous en avez besoin pour recueillir ou afficher des informations.

## <a name="initiate-workflows-and-processes"></a>Initier des flux de travail et des processus

Parfois, vous avez simplement besoin d’un moyen rapide pour démarrer un processus ou un flux de travail dans un système externe.

* Commandes d’action d’extensions de messagerie : déclenchent des messages, ce qui permet à vos utilisateurs d’envoyer rapidement le contenu d’un message à vos services Web.

* Modules de tâches : Ouvrez-les à partir d’un onglet, d’un bot ou d’une extension de messagerie pour collecter des informations avant de lancer un flux de travail.

* Robots de conversation : interagissez avec vos utilisateurs par le biais de cartes de texte et enrichies.

* Webhooks sortants : un bon choix pour une interaction simple et arrière lorsque vous n’avez pas besoin de créer un robot de conversation entier.

## <a name="send-notifications-and-alerts"></a>Envoyer des notifications et des alertes

Envoyez des notifications et des alertes asynchrones à vos utilisateurs dans Teams. Utilisez des cartes interactives pour fournir un accès rapide aux actions fréquemment utilisées et des liens vers des informations supplémentaires.

* Robots de conversation : envoyez des messages proactifs à des groupes, des canaux ou des utilisateurs individuels.

* Connecteurs & webhooks entrants : permet à un canal de s’abonner pour recevoir des messages. Avec un connecteur, les utilisateurs peuvent personnaliser l’abonnement à l’aide d’une page de configuration.

## <a name="ask-questions-and-get-answers"></a>Poser des questions et obtenir des réponses

Les personnes ont des questions. Vous avez probablement beaucoup de réponses stockées quelque part. Malheureusement, il est souvent difficile de connecter les deux ensemble.

* Robots de conversation-traitement de langage naturel, AI, apprentissage d’ordinateur, tous les Buzzwords. Utilisez un bot alimenté par le Cloud intelligent pour connecter vos utilisateurs aux réponses dont ils ont besoin.

* Onglets : incorporez votre portail Web existant dans teams ou créez une version spécifique à teams pour une fonctionnalité ajoutée.

## <a name="get-social"></a>Obtenir des amis

Une plateforme de collaboration est fondamentalement une plateforme sociale. Faites en sorte que votre partie créative soit gratuite et ajoutez un peu de plaisir à votre espace de travail.

* Toutes les blagues-envoyer des blagues, donner des félicitations, obtenir quelques mèmes pour, jeter certains Emoji ou tout autre remède.

## <a name="anything-you-can-do-in-a-single-page-app-spa"></a>Tout ce que vous pouvez faire dans une application de page unique (SPA)

Les onglets sont des pages Web incorporées. À peu près tout ce que vous pouvez faire dans un SPA, vous pouvez le faire dans un onglet de teams. N’oubliez pas de prêter attention aux onglets de groupe d’étendue et de canal pour les expériences partagées, les onglets personnels sont pour... expériences personnelles. La liste des éléments de l’équipe s’affiche sous l’onglet canal, la liste de vos sélections apparaît dans l’onglet personnel.

## <a name="start-small"></a>Démarrer petit

Vous ne savez pas où commencer ? Vous sentez un peu submergé de la diversité des options disponibles ? Ne vous inquiétez pas, choisissez une fonctionnalité principale de votre application et démarrez-la. Une fois que vous avez une bonne idée du flux d’informations par le biais des différents contextes de teams, il sera beaucoup plus facile d’afficher une interaction plus complexe.

## <a name="putting-it-all-together"></a>Exemple complet

Cela étant dit, les meilleures applications combinent généralement plusieurs fonctionnalités, créant une application qui engage les utilisateurs dans le contexte approprié avec les bonnes fonctionnalités au bon moment. N’essayez pas d’imposer une fonctionnalité à un endroit où elle n’appartient pas, car vous disposez d’un robot de conversation un-à-un approprié, mais vous devez simplement l’ajouter à une équipe. Différents points d’extensibilité sont adaptés à différentes opérations ; Jouez à leurs points forts et votre application se tiendra.
