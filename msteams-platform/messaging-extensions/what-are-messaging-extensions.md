---
title: Qu’est-ce que les extensions de messagerie ?
author: clearab
description: Vue d’ensemble des extensions de messagerie sur la plateforme Microsoft teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 01a038d57368826345a55358b1d628447b21f772
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673847"
---
# <a name="what-are-messaging-extensions"></a>Qu’est-ce que les extensions de messagerie ?

Les extensions de messagerie permettent aux utilisateurs d’interagir avec votre service Web par le biais de boutons et de formulaires dans le client Microsoft Teams. Ils peuvent effectuer des recherches ou initier des actions dans un système externe à partir de la zone de message de composition, de la zone de commande ou directement à partir d’un message. Vous pouvez ensuite renvoyer les résultats de cette interaction au client Microsoft Teams, généralement sous la forme d’une carte formatée de manière enrichie.

La capture d’écran ci-dessous montre les emplacements à partir desquels les extensions de messagerie peuvent être appelées.

![emplacements d’appel d’extension de messagerie](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a>Quels types de tâches sont-elles utiles ?

**Scénario :** J’ai besoin d’un système externe pour effectuer une opération et je souhaite que le résultat de l’action soit renvoyé à ma conversation. \
**Exemple :** Réservez une ressource et indiquez au canal la date/l’heure à laquelle vous l’avez réservée.

**Scénario :** J’ai besoin de trouver des éléments dans un système externe et je souhaite partager les résultats avec ma conversation. \
**Exemple :**  Recherchez un élément de travail dans Azure DevOps et partagez-le avec le groupe sous forme de carte adaptative.

**Scénario :** J’ai besoin d’effectuer une tâche complexe impliquant plusieurs étapes (ou un grand nombre d’informations) dans un système externe, et les résultats doivent être partagés avec une conversation. \
**Exemple :** Créez un bogue dans votre système de suivi en fonction d’un message Teams, affectez ce bogue à Bob, puis envoyez une carte au thread de conversation avec les détails du bogue.

## <a name="how-do-messaging-extensions-work"></a>Comment fonctionnent les extensions de messagerie ?

Une extension de messagerie se compose d’un service Web que vous hébergez et de votre manifeste d’application qui définit l’emplacement à partir duquel votre service Web peut être appelé dans le client Microsoft Teams. Elles tirent parti du schéma de messagerie de l’infrastructure de moteur et du protocole de communication sécurisé, vous devez donc également enregistrer votre service Web en tant que bot dans l’infrastructure de robot. Bien que vous puissiez créer entièrement votre service Web manuellement, nous vous recommandons de tirer parti du [Kit de développement logiciel (SDK)](https://github.com/microsoft/botframework) de l’infrastructure de robots pour utiliser plus facilement le protocole.

Dans le manifeste de l’application pour votre application Microsoft Teams, vous allez définir une extension de messagerie unique avec jusqu’à dix commandes différentes. Chaque commande définit un type (action ou recherche), ainsi que les emplacements dans le client à partir duquel elle peut être appelée (zone de message, barre de commandes et/ou message de composition). Une fois l’appel effectué, votre service Web reçoit un message HTTPs avec une charge utile JSON, y compris toutes les informations pertinentes. Vous allez répondre avec une charge utile JSON, ce qui permet au client teams de savoir quelle interaction activer ensuite.

## <a name="types-of-messaging-extension-commands"></a>Types de commandes d’extension de messagerie

Le type de commande d’extension de messagerie définit les éléments d’interface utilisateur et les flux d’interaction disponibles pour votre service Web. Certaines interactions, telles que l’authentification et la configuration, sont disponibles pour les deux types de commandes.

### <a name="action-commands"></a>Commandes d’action

Les commandes d’action vous permettent de présenter à vos utilisateurs une fenêtre contextuelle modale pour collecter ou afficher des informations. Lors de l’envoi du formulaire, votre service Web peut répondre en insérant un message directement dans la conversation ou en insérant un message dans la zone de message de composition et en permettant à l’utilisateur d’envoyer le message. Vous pouvez même regrouper plusieurs formulaires pour des flux de travail plus complexes.

Elles peuvent être déclenchées à partir de la zone de message de composition, de la zone de commande ou d’un message. Lorsqu’elle est appelée à partir d’un message, la charge utile JSON initiale envoyée à votre bot inclut l’intégralité du message à partir duquel elle a été appelée.

![module de tâche de commande d’action d’extension de messagerie](~/assets/images/task-module.png)

### <a name="search-commands"></a>Commandes de recherche

Les commandes de recherche permettent aux utilisateurs de rechercher des informations sur un système externe (soit manuellement par le biais d’une zone de recherche, soit en collant un lien vers un domaine surveillé dans la zone de message composer), puis en insérant les résultats de la recherche dans un message. Dans le flux de commandes de recherche le plus simple, le message d’appel initial inclut la chaîne de recherche que l’utilisateur a envoyé. Vous allez répondre avec une liste de cartes et d’aperçus de carte. Le client teams affiche les aperçus de carte dans une liste à partir de laquelle l’utilisateur final peut effectuer une sélection. Lorsque l’utilisateur sélectionne une carte, la carte pleine taille est insérée dans la zone de message de composition.

Ils peuvent être déclenchés à partir de la zone de message composer ou de la zone de commande. Contrairement aux commandes d’action, elles ne peuvent pas être déclenchées à partir d’un message.

![commande de recherche de l’extension de messagerie](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a>Lien unfurling

Vous avez également la possibilité d’appeler votre service lorsqu’une URL est collée dans la zone de message de composition. Cette fonctionnalité, appelée **liaison unfurling**, vous permet de vous abonner pour recevoir un appel lorsque des URL contenant un domaine particulier sont collées dans la zone de message de composition. Votre service Web peut « Unfurl » l’URL en une carte détaillée, ce qui fournit davantage d’informations que la carte d’aperçu de site Web standard. Vous pouvez même ajouter des boutons pour permettre à vos utilisateurs de prendre immédiatement des mesures sans quitter le client Microsoft Teams.

## <a name="get-started"></a>Prise en main

Vous êtes prêt à commencer à créer ? Essayez l’un de nos Démarrages rapides :

* Démarrages rapides pour C #
  * [Extension de messagerie avec des commandes basées sur l’action](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extension de messagerie avec des commandes basées sur la recherche](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Démarrages rapides pour JavaScript
  * [Extension de messagerie avec des commandes basées sur l’action](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extension de messagerie avec des commandes basées sur la recherche](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a>En savoir plus

Créer une extension de messagerie :

* [Créer une extension de messagerie](~/messaging-extensions/how-to/create-messaging-extension.md)
* [Commande définir une extension de messagerie d’action](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Commande define Search Messaging extension](~/messaging-extensions/how-to/search-commands/define-search-command.md)
