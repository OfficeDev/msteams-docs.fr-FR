---
title: Webhooks et connecteurs
author: clearab
description: Dans ce module, découvrez comment les webhooks et les connecteurs peuvent connecter vos services web à un client Teams.
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: fc65046c0bcbecb6ed4c0f15ea81beac77195256
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190034"
---
# <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les webhooks et les connecteurs permettent de connecter les services web aux canaux et aux équipes Microsoft Teams. Les webhooks sont des rappels HTTP définis par l’utilisateur qui informent les utilisateurs de toute action qui a eu lieu dans un canal Teams. C’est un moyen pour une application d’obtenir des données en temps réel. Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir les notifications et les messages de vos services web. Ils exposent un point de terminaison HTTPS pour que votre service publie des messages sous forme de cartes.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks permettent à Teams de s’intégrer à des applications externes. Avec les webhooks sortants, vous pouvez envoyer un SMS aux services web à partir d’un canal. Après avoir configuré les webhooks sortants, les utilisateurs peuvent @mentionner le webhook sortant et envoyer un message aux services web. Le service répond dans les dix secondes au message avec un SMS ou une carte.

> [!NOTE]
> Les webhooks sortants sont configurés par équipe et ne peuvent pas être inclus dans le cadre d’une application Teams normale.

## <a name="connectors"></a>Connecteurs

Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir des notifications et des messages de la part des services web. Ils exposent le point de terminaison HTTPS pour que le service publie des messages sur les canaux Teams, généralement sous forme de cartes.

### <a name="incoming-webhooks"></a>Webhooks entrants

Les webhooks entrants vous permettent de publier des messages à partir d’applications Teams. Si les webhooks entrants sont activés pour une équipe dans un canal, ils exposent le point de terminaison HTTPS, qui accepte le format JSON correct et insère les messages dans ce canal. Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps, configurer votre build et déployer et surveiller simultanément les services pour envoyer des alertes.

### <a name="office-365-connectors"></a>Connecteurs Office 365

Les connecteurs Office 365 vous permettent de créer une page de configuration personnalisée pour votre webhook entrant et de les regrouper dans une application Teams. Vous envoyez des messages principalement à l’aide de cartes de connecteur Office 365 et vous avez la possibilité de leur ajouter un ensemble limité d’actions de carte. Par exemple, un connecteur météo qui permet aux utilisateurs de sélectionner un emplacement et une heure de la journée, pour recevoir des mises à jour sur la météo de demain. Ils sont configurés au niveau du canal, mais sont installés au niveau de l’équipe.

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
