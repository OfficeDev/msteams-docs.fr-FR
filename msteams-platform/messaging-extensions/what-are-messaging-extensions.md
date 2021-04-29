---
title: Extensions de messagerie
author: clearab
description: Vue d'ensemble des extensions de messagerie sur la plateforme Microsoft Teams
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ee59a7ad96572f5a8ebc6afedd2e0e8485169e5a
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075667"
---
# <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie permettent aux utilisateurs d'interagir avec votre service web via des boutons et des formulaires dans le client Microsoft Teams. Ils peuvent rechercher ou initier des actions dans un système externe à partir de la zone de composition du message, de la zone de commande ou directement à partir d'un message. Vous pouvez renvoyer les résultats de cette interaction au client Microsoft Teams sous la forme d'une carte richement mise en forme. Ce document donne une vue d'ensemble de l'extension de messagerie, des tâches effectuées dans différents scénarios, de l'utilisation de l'extension de messagerie, des commandes d'action et de recherche, et du déploiement de liens.

L'image suivante affiche les emplacements d'où les extensions de messagerie sont invoquées :

![emplacements d'appel d'extension de messagerie](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="scenarios-where-messaging-extensions-are-used"></a>Scénarios dans lequel les extensions de messagerie sont utilisées

| Scénario | Exemple |
|:-----------------|:-----------------|
|Vous souhaitez qu'un système externe soit en mesure d'action et que le résultat de l'action soit renvoyé à votre conversation.|Réservez une ressource et autorisez le canal à connaître l'créneau horaire réservé.|
|Vous souhaitez trouver quelque chose dans un système externe et partager les résultats avec la conversation.|Recherchez un élément de travail dans Azure DevOps et partagez-le avec le groupe en tant que carte adaptative.|
|Vous souhaitez effectuer une tâche complexe impliquant plusieurs étapes ou une grande quantité d'informations dans un système externe et partager les résultats avec une conversation.|Créez un bogue dans votre système de suivi en fonction d'un message Teams, affectez ce bogue à Bob et envoyez une carte au thread de conversation avec les détails du bogue.|

## <a name="understand-how-messaging-extensions-work"></a>Comprendre le fonctionnement des extensions de messagerie

Une extension de messagerie se compose d'un service web que vous hébergez et d'un manifeste d'application, qui définit l'endroit à partir duquel votre service web est appelé dans le client Microsoft Teams. Le service web tire parti du schéma de messagerie et du protocole de communication sécurisée de Bot Framework. Vous devez donc inscrire votre service web en tant que bot dans Bot Framework. 

> [!NOTE]
> Bien que vous pouvez créer le service web manuellement, utilisez le [SDK Bot Framework](https://github.com/microsoft/botframework) pour utiliser le protocole.

Dans le manifeste de l'application Microsoft Teams, une seule extension de messagerie est définie avec jusqu'à dix commandes différentes. Chaque commande définit un type, tel qu'une action ou une recherche, ainsi que les emplacements dans le client à partir de l'endroit où elle est invoquée. Les emplacements d'appel sont la zone de message de composition, la barre de commandes et le message. Lors de l'appel, le service web reçoit un message HTTPS avec une charge utile JSON incluant toutes les informations pertinentes. Répondez avec une charge utile JSON, ce qui permet au client Teams de connaître l'interaction suivante à activer. 

## <a name="types-of-messaging-extension-commands"></a>Types de commandes d'extension de messagerie

Il existe deux types de commandes d'extension de messagerie : commande d'action et commande de recherche. Le type de commande d'extension de messagerie définit les éléments d'interface utilisateur et les flux d'interaction disponibles pour votre service web. Certaines interactions, telles que l'authentification et la configuration, sont disponibles pour les deux types de commandes.

### <a name="action-commands"></a>Commandes d'action

Les commandes d'action sont utilisées pour présenter aux utilisateurs une fenêtre popup modale pour collecter ou afficher des informations. Lorsque l'utilisateur soumet le formulaire, votre service web répond en insérant un message directement dans la conversation ou en insérant un message dans la zone de composition du message. Après cela, l'utilisateur peut envoyer le message. Vous pouvez chaîner plusieurs formulaires pour des flux de travail plus complexes.

Les commandes d'action sont déclenchées à partir de la zone de composition du message, de la zone de commande ou d'un message. Lorsque la commande est invoquée à partir d'un message, la charge utile JSON initiale envoyée à votre bot inclut l'intégralité du message à partir de qui elle a été invoquée. L'image suivante affiche le module de tâche de commande d'action d'extension de messagerie : module de tâche de commande ![ d'action d'extension de messagerie](~/assets/images/task-module.png)

### <a name="search-commands"></a>Commandes de recherche

Les commandes de recherche permettent aux utilisateurs de rechercher des informations manuellement dans un système externe par le biais d'une zone de recherche ou en csérant un lien vers un domaine surveillé dans la zone de composition du message et en insérant les résultats de la recherche dans un message. Dans le flux de commande de recherche le plus élémentaire, le message d'appel initial inclut la chaîne de recherche envoyée par l'utilisateur. Vous répondez avec une liste de cartes et d'aperçus de carte. Le client Teams affiche une liste d'aperçus de carte pour l'utilisateur. Lorsque l'utilisateur sélectionne une carte dans la liste, la carte pleine taille est insérée dans la zone de composition du message.

Les cartes sont déclenchées à partir de la zone de composition du message ou de la zone de commande et ne sont pas déclenchées à partir d'un message. Ils ne peuvent pas être déclenchés à partir d'un message.
L'image suivante affiche le module de tâche de recherche d'extension de messagerie :

![Commande de recherche d'extension de messagerie](~/assets/images/search-extension.png)

> [!NOTE]
> Pour plus d'informations sur les cartes, voir [les cartes.](../task-modules-and-cards/what-are-cards.md)

## <a name="link-unfurling"></a>Déploiement de lien

Un service web est appelé lorsqu'une URL est passée dans la zone de composition du message. Cette fonctionnalité est connue sous le nom de déploiement de lien. Vous pouvez vous abonner pour recevoir un appel lorsque les URL contenant un domaine particulier sont passées dans la zone de rédaction du message. Votre service web peut « déployer » l'URL dans une carte détaillée, fournissant plus d'informations que la carte d'aperçu du site web standard. Vous pouvez ajouter des boutons pour permettre aux utilisateurs d'agir immédiatement sans quitter le client Microsoft Teams.
Les images suivantes affichent la fonctionnalité de déploiement de lien lorsqu'un lien est passé dans l'extension de messagerie :
 
![lien de déploiement](../assets/images/messaging-extension/unfurl-link.png)

![déploiement de lien](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|
| Extension de messagerie avec commandes basées sur l'action | Cet exemple montre comment créer une extension de messagerie basée sur une action. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extension de messagerie avec commandes basées sur la recherche | Cet exemple montre comment créer une extension de messagerie basée sur la recherche. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="see-also"></a>Voir aussi

[Créer une extension de messagerie](../build-your-first-app/build-messaging-extension.md)


## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Définir la commande d'extension de messagerie d'action](~/messaging-extensions/how-to/action-commands/define-action-command.md)

> [!div class="nextstepaction"]
> [Définir la commande d'extension de messagerie de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md)
