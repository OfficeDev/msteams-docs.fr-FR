---
title: Créer des applications pour la plateforme Microsoft Teams web
author: heath-hamilton
description: Obtenez une vue d'ensemble de la façon dont les développeurs peuvent étendre Microsoft Teams fonctionnalités avec des applications personnalisées.
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 69c36cf5f925bdb9802e7ec081a7765187a06128
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101841"
---
# <a name="build-apps-for-microsoft-teams"></a>Créer des applications pour Microsoft Teams

Microsoft Teams applications apportent des informations clés, des outils courants et des processus fiables là où les personnes se rassemblent, apprennent et travaillent de plus en plus.

Les applications vous permettent d'étendre Teams pour répondre à vos besoins. Créez un tout nouveau Teams ou intégrez une application existante.

> [!div class="nextstepaction"]
> [Démarrer](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Qu'est-ce Teams applications ?

Teams applications sont une combinaison de [fonctionnalités et](concepts/capabilities-overview.md) de [points d'entrée.](concepts/extensibility-points.md) Par exemple, les personnes peuvent discuter avec le *bot* de votre application (fonctionnalité) dans un *canal* (point d'entrée).

Certaines applications sont simples (envoyer des notifications), tandis que d'autres sont complexes (gérer les enregistrements des patients). Lors de la planification de votre application, n'oubliez Teams est un hub de collaboration. Les meilleures Teams permettent aux personnes de s'exprimer et de travailler mieux ensemble.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Onglets

**Obtenir des informations plus facilement**: parfois, il vous suffit de faciliter la recherche. Affichez une page web importante dans un [onglet,](tabs/what-are-tabs.md)ce qui fournit une expérience web en plein écran pour le contenu statique et dynamique dans Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle de l'apparence des onglets dans le client Teams client." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>Bots

**Transformer des mots en actions**: les conversations entraînent souvent la nécessité d'une action (générer une commande, passer en revue mon code, vérifier l'état du ticket, et ainsi de suite). Un [bot](bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle de l'apparence des bots dans le client Teams client." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Extensions de messagerie

**Faciliter la tâche multitâche**: avec les [extensions](messaging-extensions/what-are-messaging-extensions.md)de messagerie, vous pouvez rapidement partager des informations externes dans une conversation. Vous pouvez également agir sur un message, par exemple créer un ticket d'aide basé sur le contenu d'un billet de canal.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de l'apparence des extensions de messagerie dans Teams client." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhooks

**Communiquer avec des applications externes**: les [webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d'envoyer automatiquement des notifications à partir d'une autre application vers Teams canal. Les [webhooks sortants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envoient un message à votre service web avec une @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de l'apparence des connecteurs dans le client Teams client." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

Utiliser **Teams** données : [l'API Microsoft Graph pour Teams](https://docs.microsoft.com/graph/teams-concept-overview) fournit l'accès à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités de votre application.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l'API microsoft Graph pour Teams." border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>Démarrer la création

Familiarisez-vous rapidement avec la création de Teams en mettant en place votre environnement et en créant une application simple.

> [!div class="nextstepaction"]
> [Créer votre première application](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>S'intégrer aux équipes

Associez les fonctionnalités que les utilisateurs aiment d'une application web, d'un service ou d'un système existant aux fonctionnalités collaboratives de Teams.

> [!div class="nextstepaction"]
> [Intégrer une application existante](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Un peu de code est très long

Vous n'avez pas besoin d'être un programmeur expert pour créer une application Teams excellente. Essayez l'une des solutions à code faible.

> [!div class="nextstepaction"]
> [Créer une application à code faible](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>Obtenir des idées pour votre application

Vous recherchez une source d'inspiration pour le développement d'applications ? Parcourez notre liste de scénarios réels et de solutions industrielles avec des maquettes de concept haute fidélité pour comprendre les différentes façons Teams applications peuvent aider vos utilisateurs.

> [!div class="nextstepaction"]
> [Voir les scénarios d'application](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Voir aussi

* [Ajouter un bouton Partager à Teams votre site web](concepts/build-and-test/share-to-teams.md)
* [Concevoir votre application Teams web](concepts/design/design-teams-app-overview.md)
* [Microsoft Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* SDK Bot Framework pour [JavaScript et](https://github.com/Microsoft/botbuilder-js) [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Distribuer votre application Teams de messagerie](concepts/deploy-and-publish/apps-publish-overview.md)
