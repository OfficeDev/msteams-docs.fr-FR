---
title: Créer des applications pour la plateforme Microsoft teams
author: heath-hamilton
description: Vue d’ensemble de la façon dont les développeurs peuvent étendre et personnaliser les fonctionnalités de Microsoft teams avec des applications personnalisées.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: c430add71e7c23a44a552270c5e3c1bacbe650e4
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209792"
---
# <a name="build-apps-for-microsoft-teams"></a>Créer des applications pour Microsoft teams

Les applications Microsoft teams apportent des informations clés, des outils courants et des processus approuvés à des endroits où les utilisateurs recueillent, apprennent et travaillent de plus en plus.

Les applications vous permettent d’étendre les équipes pour répondre à vos besoins. Créez un article nouveau pour teams ou intégrez une application existante.

## <a name="what-are-teams-apps"></a>Qu’est-ce que les applications teams ?

Les applications teams sont une combinaison de [fonctionnalités](concepts/capabilities-overview.md) et de [points d’entrée](concepts/extensibility-points.md). Par exemple, les utilisateurs peuvent discuter avec le *robot* de votre application (fonctionnalité) dans un *canal* (point d’entrée).

Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (gérer les enregistrements des patients). Lors de la planification de votre application, rappelez-vous que teams est un hub de collaboration. Les meilleures applications teams aident les utilisateurs à s’exprimer et à collaborer efficacement.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Onglets

**Obtenir des informations plus facilement**: parfois, vous avez simplement besoin de faciliter la recherche. Afficher une page Web importante dans un [onglet](tabs/what-are-tabs.md), qui fournit une expérience Web en plein écran pour le contenu statique et dynamique dans Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle des onglets qui ressemblent dans le client Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a>Extensions de messagerie

Facilitez **le multitâche**: avec les [extensions de messagerie](messaging-extensions/what-are-messaging-extensions.md), vous pouvez partager rapidement des informations externes dans une conversation. Vous pouvez également agir sur un message, tel que la création d’un ticket d’aide basé sur le contenu d’un billet de canal.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de l’apparence des extensions de messagerie dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>Bots

**Transformer les mots en actions**: les conversations entraînent souvent une action (générer une commande, vérifier mon code, vérifier l’état du ticket, etc.). Un [bot](bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle des robots qui se ressemblent dans le client Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a>Webhooks

**Communiquer avec des applications externes**: les [webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications à partir d’une autre application vers un canal Teams. Avec les [webhooks sortants, envoyez](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)un message à votre service Web à l’aide d’une @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle des connecteurs qui ressemblent au client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph pour teams

**Utiliser les données teams**: l' [API Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview) fournit un accès aux informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités de votre application.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Microsoft Graph pour Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a>Prise en main

Accédez directement à l’aide de nos didacticiels d’application ou Découvrez comment intégrer et importer des applications existantes.

:::row:::
   :::column span="2":::

### <a name="start-building"></a>Commencer à créer

   Familiarisez-vous rapidement avec la création de teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.

   > [!div class="nextstepaction"]
   > [Créer votre première application maintenant](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a>Intégration à teams

   Combinez les fonctionnalités que les utilisateurs aiment à une application Web existante, un service ou un système avec les fonctionnalités collaboratives de teams.

   > [!div class="nextstepaction"]
   > [Intégration d’une application existante](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a>Un petit code est long

   Vous n’avez pas besoin d’être un programmeur expert pour créer une application de qualité de teams. Essayez l’une des solutions à faible code.

   > [!div class="nextstepaction"]
   > [Créer une application à code bas](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a>Ressources

* [Ajouter un bouton partager à teams à votre site Web](concepts/build-and-test/share-to-teams.md)
* [Système de conception Fluent](https://fluentsite.z22.web.core.windows.net/)
* [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Kit de développement logiciel (SDK) robot for JavaScript](https://github.com/Microsoft/botbuilder-js) and [bot Framework SDK pour .net](https://github.com/Microsoft/botbuilder-dotnet/)
* [Publier votre application dans une organisation ou AppSource](concepts/deploy-and-publish/overview.md)
