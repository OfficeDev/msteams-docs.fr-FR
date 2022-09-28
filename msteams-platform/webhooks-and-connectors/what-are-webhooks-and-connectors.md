---
title: Webhooks et connecteurs
author: clearab
description: Découvrez comment les webhooks et les connecteurs permettent de connecter les services web aux canaux et aux équipes dans Microsoft Teams. Découvrez les webhooks entrants, sortants et les connecteurs Office 365.
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 94c84b577dfb20cb823167d3af84f5460bb87554
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100447"
---
# <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les webhooks et les connecteurs permettent de connecter les services web aux canaux et aux équipes Microsoft Teams. Les webhooks sont des rappels HTTP définis par l’utilisateur qui informent les utilisateurs de toute action qui a eu lieu dans un canal Teams. Il s’agit d’un moyen pour une application d’obtenir des données en temps réel. Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir les notifications et les messages de vos services web. Ils exposent un point de terminaison HTTPS pour que votre service publie des messages sous forme de cartes.

> [!IMPORTANT]
> Vous pouvez choisir de créer une application Teams de bot de notification autre que les webhooks entrants. Ils fonctionnent de la même façon, mais le bot de notification a plus de fonctionnalités. Pour plus d’informations, consultez [le bot de notification Build avec JavaScript](../sbs-gs-notificationbot.yml) ou l’exemple de [notification de webhook entrant](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification). Pour commencer, téléchargez [le](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) Kit de ressources Teams maintenant et explorez. Pour plus d’informations, consultez les [documents du Kit de ressources Teams](../toolkit/teams-toolkit-fundamentals.md).

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks permettent à Teams de s’intégrer à des applications externes. Avec les webhooks sortants, vous pouvez envoyer un SMS aux services web à partir d’un canal. Après avoir configuré les webhooks sortants, les utilisateurs peuvent @mentionner le webhook sortant et envoyer un message aux services web. Le service répond dans les 10 secondes au message avec un texte ou une carte.

> [!NOTE]
> Les webhooks sortants sont configurés par équipe et ne peuvent pas être inclus dans le cadre d’une application Teams normale.

## <a name="connectors"></a>Connecteurs

Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir des notifications et des messages de la part des services web. Ils exposent le point de terminaison HTTPS pour que le service publie des messages sur les canaux Teams, généralement sous forme de cartes.

### <a name="incoming-webhooks"></a>Webhooks entrants

Les webhooks entrants vous permettent de publier des messages à partir d’applications Teams. Si les webhooks entrants sont activés pour une équipe dans un canal, ils exposent le point de terminaison HTTPS, qui accepte le format JSON correct et insère les messages dans ce canal. Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps, configurer votre build et déployer et surveiller simultanément les services pour envoyer des alertes.

#### <a name="notification-bot-or-incoming-webhook---choose-the-right-one"></a>Bot de notification ou webhook entrant : choisissez le bon bot

Avant de commencer à apprendre à générer des webhooks entrants, vous souhaiterez peut-être également savoir que vous pouvez générer un bot de notification à l’aide du Kit de ressources Teams. Les bots de notification peuvent permettre une expérience plus personnalisable pour répondre à différents scénarios métier.

En savoir plus sur les différences entre le bot de notification et le webhook entrant afin de pouvoir choisir les solutions appropriées pour vos scénarios :

| &nbsp; | Bot de notification |  Webhook entrant |
| --- | --- | --- |
| De quoi s’agit-il ? | Une application Teams | Fonctionnalité Teams |
| Installation requise | Oui | Non |
| Scénarios appropriés | • Recevoir régulièrement des notifications et des messages, par exemple, recevoir une notification quotidienne des tâches de l’équipe. <br>  • Recevoir des notifications et des messages basés sur des événements réels. Par exemple, une fois que vos collègues chargent des fichiers, vous recevez des notifications. | Communiquez avec des applications externes et recevez des notifications et des messages d’autres applications. |
| Configuration de l’étendue | • Canal Teams <br> • Conversation de groupe <br> • Conversation personnelle | Canal Teams |
| Processus de message | Un bot de notification fonctionne comme une application Teams. Vous pouvez définir votre logique métier pour traiter les données et afficher les données dans un format personnalisé. | Le webhook étant une fonctionnalité Teams plutôt qu’une application Teams, il reçoit et affiche uniquement les données sans traitement. |
| Récupérer le contexte Teams | Notification Bot peut récupérer le contexte Teams, tel que le canal ou les informations utilisateur, les messages, etc. | Non |
| Envoyer une carte adaptative | Oui | Oui |
| Envoyer un message de bienvenue | Peut envoyer un message de bienvenue | Aucun message de bienvenue |
| Déclencheur pris en charge | Tous les déclencheurs pris en charge. Si vous utilisez Teams Toolkit, vous pouvez rapidement obtenir des projets de modèle avec les déclencheurs suivants : <br> • Déclencheur de temps hébergé sur des fonctions Azure. <br> • Restify HTTP trigger hosted on Azure app service <br> • Déclencheur HTTP hébergé sur Azure Functions | Tous les déclencheurs pris en charge |
| Outils de génération | • [Vue d’ensemble du Kit de ressources Teams pour Visual Studio Code](../toolkit/teams-toolkit-fundamentals.md) <br> • [Vue d’ensemble du Kit de ressources Teams pour Visual Studio](../toolkit/teams-toolkit-fundamentals.md) <br> • [Bibliothèque TeamsFx](../toolkit/TeamsFx-CLI.md) <br> • [Kit de développement logiciel (SDK) TeamsFx](../toolkit/TeamsFx-SDK.md) | Aucun outil requis |
| Ressource cloud requise | Azure Bot Framework | Aucune ressource requise |
| Didacticiel | [Générer un bot de notification avec JavaScript](../sbs-gs-notificationbot.yml) | [Exemple de notification de webhook entrant](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification) |

### <a name="office-365-connectors"></a>Connecteurs Office 365

Les connecteurs Office 365 vous permettent de créer une page de configuration personnalisée pour votre webhook entrant et de les regrouper dans une application Teams. Vous envoyez des messages principalement à l’aide de cartes de connecteur Office 365 et vous avez la possibilité de leur ajouter un ensemble limité d’actions de carte. Par exemple, un connecteur météo qui permet aux utilisateurs de sélectionner un emplacement et à tout moment de la journée pour recevoir des mises à jour sur la météo de demain. Ils sont configurés au niveau du canal, mais ils sont installés au niveau de l’équipe.

> [!NOTE]
> Vous pouvez distribuer le connecteur Office 365 de l’application Teams à notre AppStore.

## <a name="create-and-send-messages"></a>Créer et envoyer des messages

Les messages actionnables permettent aux utilisateurs d’agir sans quitter leur client de messagerie, ce qui augmente leur engagement. Avec les webhook entrants Office 365, vous pouvez envoyer des messages en publiant une charge utile JSON sur l’URL du webhook.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="see-also"></a>Voir aussi

* [Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Générer un bot de notification avec JavaScript](../sbs-gs-notificationbot.yml)
* [Créer votre première application de bot à l’aide de JavaScript](../sbs-gs-bot.yml)
