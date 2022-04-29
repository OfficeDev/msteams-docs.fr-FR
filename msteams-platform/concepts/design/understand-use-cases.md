---
title: Présentation des cas d’utilisation et des fonctionnalités Teams de votre application
author: heath-hamilton
description: Dans cet article, découvrez les fonctionnalités de l’application Microsoft Teams, planifiez votre application Teams, comprenez l’utilisateur de votre application et ses besoins, comprenez les problèmes utilisateur que votre application Teams résoudrait, planifiez l’authentification des utilisateurs et leur expérience d’intégration.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: dbed78461fd39f4442c67ac7ec7523ca5cc09ba5
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104377"
---
# <a name="understand-your-use-cases"></a>Comprendre vos cas d’utilisation

Dans l’infrastructure sociale collaborative de Teams, il existe un large éventail de besoins utilisateur que vous pouvez résoudre avec une application Teams. Par exemple, une application qui comblera les lacunes dans l’obtention d’une collaboration efficace est parfaitement adaptée.

L’utilisateur de l’application et les exigences de son application sont les instructions de base qui déterminent tous les choix d’application que vous allez faire. La création de la conception d’applications, la sélection des fonctionnalités, la détermination de l’environnement de génération et de test et la distribution d’applications suivent les exigences de l’utilisateur à partir de l’application.

Si vous souhaitez répondre aux exigences des utilisateurs avec votre application, vous devez d’abord les comprendre.

- **Comprenez votre utilisateur** :
  - Reconnaissez les problèmes des utilisateurs et identifiez les solutions à certains problèmes courants auxquels les utilisateurs sont confrontés.
  - Créez votre application Teams en recherchant la combinaison appropriée de fonctionnalités Teams pour répondre aux besoins de votre utilisateur.
  - Comprendre les cas d’usage pour savoir comment un utilisateur final interagit avec votre application.

- **Comprendre le problème**: déterminez le problème principal que votre application doit résoudre.

- **Envisagez l’intégration** : identifiez les applications et services requis par votre application, tels que l’authentification, les Microsoft Graph ou les applications web.

## <a name="microsoft-teams-app-features"></a>Fonctionnalités de l’application Microsoft Teams

Il existe plusieurs façons d’étendre Teams afin que chaque application soit unique. Offre de fonctionnalités d’application Teams :

- [Fonctionnalités de l’application](#app-capabilities)
- [Étendue de l’application](#app-scope)

### <a name="app-capabilities"></a>Fonctionnalités de l’application

Les fonctionnalités sont les principales fonctionnalités que vous pouvez créer dans votre application. Ils sont également appelés points d’entrée ou d’extension, car ils permettent l’intégration et l’interaction.

Vos applications Teams disposent d’une ou de toutes les fonctionnalités principales suivantes :

:::row:::
   :::column span="":::

#### <a name="personal-apps"></a>Applications personnelles

Une [application personnelle](../../concepts/design/personal-apps.md)est un espace ou un bot dédié pour aider les utilisateurs à se concentrer sur leurs propres tâches ou à afficher les activités pertinentes.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-personal-apps-2021.png" alt-text="Représentation conceptuelle de l’apparence des applications personnelles dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="tabs"></a>Onglets

Affichez votre contenu web basé dans un [onglet](../../tabs/what-are-tabs.md) où les utilisateurs peuvent discuter et travailler dessus ensemble.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-channel-chat-apps-2021.png" alt-text="Représentation conceptuelle de l’apparence des onglets dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="bots"></a>Bots

Les conversations entraînent souvent la nécessité d’effectuer quelque chose (générer une commande, passer en revue le code, vérifier l’état du ticket, etc.). Un [bot](../../bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-bots-2021.png" alt-text="Représentation conceptuelle de l’apparence des bots dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

#### <a name="message-extensions"></a>Extensions de messages

Avec les [extensions de message](../../messaging-extensions/what-are-messaging-extensions.md), vous pouvez rechercher et partager des informations externes. Vous pouvez également agir sur un message, par exemple créer un ticket d’aide basé sur le contenu d’une publication de canal.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-messaging-extensions-2021.png" alt-text="Représentation conceptuelle des extensions de message dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="meeting-extensions"></a>Extensions de réunion

Il existe quelques options pour [l’incorporation de votre application dans l’expérience d’appel Teams](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md).

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-meeting-extensions-2021.png" alt-text="Représentation conceptuelle de l’apparence des extensions de réunion dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les[webhooks entrants](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications d’une autre application à un canal Teams. Avec les[webhooks sortants](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), vous pouvez envoyer un message à votre service web avec une @mention.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de l’apparence des connecteurs dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="microsoft-graph-for-teams"></a>Microsoft Graph pour Teams

L’API [Microsoft Graph pour Teams](/graph/teams-concept-overview) donne accès à des informations sur les équipes, les canaux, les utilisateurs et les messages qui vous aident à créer ou à améliorer les fonctionnalités de votre application.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Microsoft Graph pour Teams." border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> Le magasin Teams a évolué :
>
> Auparavant, les applications métier étaient mises à jour en sélectionnant les points de suspension sur la vignette. Avec l’expérience mise à jour du Magasin Teams, vous pouvez maintenant mettre à jour les applications métier en vous connectant au [centre d’administration Teams](https://admin.teams.microsoft.com).

### <a name="app-scope"></a>Étendue de l’application

Votre application peut avoir l’une des étendues suivantes :

- **Expérience d’application personnelle**: une application personnelle est un espace dédié ou un bot pour aider les utilisateurs à se concentrer sur leurs propres tâches ou à afficher les activités importantes pour eux.
- **Expérience d’application partagée**: l’équipe, le canal et la conversation sont des espaces de collaboration. Les applications de ces contextes sont accessibles à tous les utilisateurs de cet espace. Les espaces de collaboration se concentrent généralement sur les flux de travail pour les interactions de votre application ou sur le déverrouillage de nouvelles interactions sociales.

Une application peut exister dans différentes étendues. Par exemple :

- Votre application peut afficher des données dans un emplacement partagé central, c’est-à-dit un onglet.
- Il peut également présenter ces mêmes informations par le biais d’une interface conversationnelle personnelle, c’est-à-d., un bot.

Un utilisateur peut interagir avec une application dans un onglet de canevas pour effectuer une activité ou peut choisir de faire de même à l’aide d’un bot conversationnel.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Mapper vos cas d’usage](../../concepts/design/map-use-cases.md)

## <a name="see-also"></a>Voir aussi

[Intégrer les fonctionnalités de l’appareil](~/concepts/device-capabilities/device-capabilities-overview.md)
