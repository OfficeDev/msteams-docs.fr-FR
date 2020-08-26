---
title: Plateforme de développement teams
author: clearab
description: Vue d’ensemble de la façon dont les développeurs peuvent étendre et personnaliser les fonctionnalités de Microsoft teams à l’aide de la plateforme Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 4af4d34ffa4581be6e69f6233d3eb356aa6a2a08
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874883"
---
# <a name="building-for-microsoft-teams"></a>Création pour Microsoft teams

Les applications Microsoft teams apportent des informations clés, des outils courants et des processus approuvés à des endroits où les utilisateurs recueillent, apprennent et travaillent de plus en plus.

Les applications vous permettent d’étendre les équipes pour répondre à vos besoins. Vous pouvez créer une personnalisation pour teams ou simplement intégrer des fonctionnalités dans vos applications et services préférés.

## <a name="what-can-teams-apps-do"></a>Que peuvent faire les applications teams ?

Les personnes découvrent et utilisent les applications teams via un ensemble de [fonctionnalités](capabilities-overview.md)de plateforme.

Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (afficher les enregistrements patients). Lors de la planification de votre application, rappelez-vous que teams est un hub de collaboration. Les meilleures applications teams aident les utilisateurs à s’exprimer et à collaborer efficacement.

### <a name="get-information-more-conveniently"></a>Obtenir des informations plus facilement

Parfois, vous avez simplement besoin de faciliter la recherche. Afficher une page Web importante dans un [onglet](doc-links/what-are-tabs.md), qui fournit une expérience Web en plein écran pour le contenu statique et dynamique dans Teams.

![Représentation conceptuelle des onglets qui ressemblent dans le client Teams.](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a>Partager des liens sans basculement de contexte

Extrayez les informations dans une conversation et ne laissez pas Teams. Par exemple, avec les [extensions de messagerie](doc-links/what-are-messaging-extensions.md) , vous pouvez partager du contenu riche et facilement digestible à partir d’un système externe à l’aide de la zone de composition du message.

![Représentation conceptuelle des extensions de messagerie qui ressemblent dans le client teams](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a>Transformer les mots en actions

Les conversations entraînent souvent un besoin (créer une commande, vérifier mon code, etc.). Un [bot](doc-links/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.

![Représentation conceptuelle des robots qui se ressemblent dans le client teams](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a>Communiquer avec des services et des applications externes

Les [webhooks entrants](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des alertes à partir d’une autre application à un canal ou une conversation Teams. Avec les [webhooks sortants](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), vous pouvez envoyer un message à votre service Web à l’aide d’une @mention.

![Représentation conceptuelle des connecteurs qui ressemblent au client Teams.](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a>Utiliser les données de teams

L' [API REST Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview) donne accès à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités de votre application.

![«Représentation conceptuelle de l’API REST Microsoft Graph pour teams](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a>Commencer à créer

   Familiarisez-vous rapidement avec la création de teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.

   > [!div class="nextstepaction"]
   > [Créer votre première application maintenant](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a>Ensemble

   Simplifiez les processus et les flux de travail pour les utilisateurs en combinant les applications Web, les services et les systèmes Web préférés de votre organisation avec des fonctionnalités collaboratives Teams.

   > [!div class="nextstepaction"]
   > [Intégration d’une application existante](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a>Approuver le processus

   Comprendre l’ensemble du processus de développement de la plateforme teams pour planifier, concevoir, créer et publier une application pour votre organisation ou tout le monde.

   > [!div class="nextstepaction"]
   > [Démarrer la planification de votre application](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a>Pas de code, pas de souci

   Vous n’avez pas besoin d’être programmeur pour créer une application intéressante. Créez une application teams avec peu ou pas de code à l’aide de Microsoft Power Platform.

   > [!div class="nextstepaction"]
   > [Importer une application Power Platform](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a>Ressources

* [Ajouter un bouton partager à teams à votre site Web](doc-links/share-to-teams.md)
* [Système de conception de l’interface utilisateur Fluent](https://fluentsite.z22.web.core.windows.net/)
* [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* [Kit de développement logiciel (SDK) robot for JavaScript](https://github.com/Microsoft/botbuilder-js) and [bot Framework SDK pour .net](https://github.com/Microsoft/botbuilder-dotnet/)
