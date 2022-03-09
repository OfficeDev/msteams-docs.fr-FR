---
title: Comprendre les fonctionnalités de l’application
author: heath-hamilton
description: Description des fonctionnalités de l’application Teams, telles que les onglets, les bots, les extensions de messagerie et les webhooks et connecteurs ; étendue de l’application, telle que les applications personnelles et partagées
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 09/22/2020
keywords: connecteurs webhooks des extensions de messagerie des bots tabulations
ms.openlocfilehash: 7200e785bc7c857aa65cf8b228720fe8e1d40a66
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398952"
---
# <a name="understand-microsoft-teams-app-features"></a>Comprendre les fonctionnalités de l’application Microsoft Teams

Il existe plusieurs façons d’étendre Teams afin que chaque application soit unique. Une application Teams peut se manifester à un utilisateur de différentes manières. Les fonctionnalités d’une application Teams sont les suivantes :

* Fonctionnalités de l’application
* Étendue de l’application

Par exemple, un utilisateur peut interagir avec une application dans un onglet de canevas pour effectuer une activité ou peut choisir de faire de même à l’aide d’un bot conversationnel. Vous ne pouvez utiliser qu’une seule fonctionnalité, telle qu’un webhook, tandis que d’autres disposent de plusieurs fonctionnalités pour offrir aux utilisateurs différentes options.

Ces capacités peuvent exister dans différents domaines. Par exemple, votre application peut afficher des données dans un emplacement central partagé, c'est-à-dire l'onglet, et présenter ces mêmes informations dans une interface conversationnelle personnelle, c'est-à-dire le robot.

## <a name="app-capabilities"></a>Fonctionnalités de l’application

Pour pouvoir étendre votre application, vous devez comprendre toutes les fonctionnalités de base, et les points d’entrée qui fonctionnent dans un espace de collaboration. Vous pouvez expérimenter les points d’extension pour créer vos applications. Les composants importants du projet d’application vous aident à configurer correctement votre page d’application.

Vos applications Teams disposent d’une ou de toutes les fonctionnalités principales suivantes :

:::row:::
   :::column span="":::

### <a name="personal-apps"></a>Applications personnelles

Une [application personnelle](../concepts/design/personal-apps.md) est un espace dédié ou un bot pour aider les utilisateurs à se concentrer sur leurs propres tâches ou à afficher les activités importantes pour eux.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-personal-apps-2021.png" alt-text="Représentation conceptuelle de l’apparence des applications personnelles dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="tabs"></a>Onglets

Affichez votre contenu web basé dans un [onglet](../tabs/what-are-tabs.md) où les utilisateurs peuvent discuter et travailler dessus ensemble.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-channel-chat-apps-2021.png" alt-text="Représentation conceptuelle de l’apparence des onglets dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>Bots

Les conversations entraînent souvent la nécessité d’effectuer quelque chose (générer une commande, évaluer mon code, vérifier l’état du ticket, etc.). Un [bot](../bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-bots-2021.png" alt-text="Représentation conceptuelle de l’apparence des bots dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Extensions de messagerie

Avec les [extension de messagerie](../messaging-extensions/what-are-messaging-extensions.md), vous pouvez rapidement partager des informations externes dans une conversation. Vous pouvez également agir sur un message, par exemple créer un ticket d’aide basé sur le contenu d’une publication de canal.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-messaging-extensions-2021.png" alt-text="Représentation conceptuelle de l’apparence des extensions de messagerie dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="meeting-extensions"></a>Extensions de réunion

Il existe quelques options pour [l’incorporation de votre application dans l’expérience d’appel Teams](../apps-in-teams-meetings/design/designing-apps-in-meetings.md).

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-meeting-extensions-2021.png" alt-text="Représentation conceptuelle de l’apparence des extensions de réunion dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les[webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications d’une autre application vers un canal Teams. Avec les [webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), envoyez des messages à votre service web avec une @mention.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de l’apparence des connecteurs dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph pour Teams

L’[API Microsoft Graph pour Teams](/graph/teams-concept-overview) API permet d’accéder à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités pour votre application (telles que des notifications enrichies).

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Microsoft Graph pour Teams." border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> Le magasin Teams a évolué : Auparavant, les applications de la LPP étaient mises à jour en sélectionnant les ellipses sur la tuile. Avec l’expérience mise à jour du Magasin Teams, vous pouvez maintenant mettre à jour les applications métier en vous connectant au [Centre d’administration Teams](https://admin.teams.microsoft.com).

## <a name="choose-the-correct-scope-for-your-app"></a>Choisir l’étendue appropriée pour votre application

Vous pouvez choisir l’étendue de l’application parmi les éléments suivants :

* Expérience d’application personnelle : une application personnelle est un espace dédié ou un bot pour aider les utilisateurs à se concentrer sur leurs propres tâches ou à afficher les activités importantes pour eux.
* Expérience d’application partagée : l’équipe, le canal et la conversation sont des espaces de collaboration. Les applications de ces contextes sont accessibles à tous les utilisateurs de cet espace. Les espaces de collaboration se concentrent généralement sur les flux de travail pour les interactions de votre application ou sur le déverrouillage de nouvelles interactions sociales.

## <a name="see-also"></a>Voir aussi

* [Créer des applications pour Teams](../overview.md)
* [Créer votre première application Microsoft Teams](../build-your-first-app/build-first-app-overview.md)
