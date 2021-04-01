---
title: Créer des applications pour la plateforme Microsoft Teams
author: heath-hamilton
description: Obtenez une vue d’ensemble de la façon dont les développeurs peuvent étendre les fonctionnalités de Microsoft Teams avec des applications personnalisées.
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475927"
---
# <a name="build-apps-for-microsoft-teams"></a>Créer des applications pour Microsoft Teams

Les applications Microsoft Teams apportent des informations clés, des outils courants et des processus de confiance où les personnes se rassemblent, apprennent et travaillent de plus en plus.

Les applications sont la façon dont vous étendez Teams pour répondre à vos besoins. Créez quelque chose de nouveau pour Teams ou intégrez une application existante.

> [!div class="nextstepaction"]
> [Démarrer](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Qu’est-ce que les applications Teams ?

Les applications Teams sont une combinaison de [fonctionnalités et](concepts/capabilities-overview.md) de [points d’entrée.](concepts/extensibility-points.md) Par exemple, les personnes peuvent discuter avec le *bot* de votre application (fonctionnalité) dans un *canal* (point d’entrée).

Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (gérer les enregistrements des patients). Lors de la planification de votre application, n’oubliez pas que Teams est un hub de collaboration. Les meilleures applications Teams aident les personnes à s’exprimer et à travailler mieux ensemble.

:::row:::
   :::column span="":::

### <a name="tabs"></a>Onglets

**Obtenir des informations plus facilement**: parfois, il vous suffit de faciliter la recherche. Affichez une page web importante dans un [onglet,](tabs/what-are-tabs.md)ce qui fournit une expérience web en plein écran pour le contenu statique et dynamique dans Teams.

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle de l’apparence des onglets dans le client Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>Bots

**Transformer des mots en actions**: les conversations entraînent souvent la nécessité d’une action (générer une commande, passer en revue mon code, vérifier l’état du ticket, etc.). Un [bot](bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle de l’apparence des bots dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>Extensions de messagerie

**Faciliter la tâche multitâche**: avec les [extensions](messaging-extensions/what-are-messaging-extensions.md)de messagerie, vous pouvez rapidement partager des informations externes dans une conversation. Vous pouvez également agir sur un message, par exemple créer un ticket d’aide basé sur le contenu d’un billet de canal.

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de l’apparence des extensions de messagerie dans le client Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhooks

**Communiquer avec des applications externes**: [les webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications à partir d’une autre application vers un canal Teams. Les [webhooks sortants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envoient un message à votre service web avec une @mention.

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de l’apparence des connecteurs dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph pour Teams

**Utiliser les données Teams**: l’API [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) pour Teams permet d’accéder à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer des fonctionnalités pour votre application.

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Microsoft Graph pour Teams." border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a>Créer des solutions pour les applications Microsoft Teams
 
Microsoft propose un look book d’extensibilité, une bibliothèque de scénarios pour les applications Teams organisées par secteur d’activité. Ce livre vous aide à créer des applications sur la plateforme Teams et à comprendre différents scénarios possibles à l’aide de différentes fonctionnalités de la plateforme Teams. Les scénarios de look book commencent par un problème d’entreprise, les personnes impliquées avec leurs défis et se terminent par une solution d’application Teams qui permet de répondre aux besoins de l’entreprise.

Chaque scénario de cette bibliothèque est accompagné d’un ensemble de maquettes de concept de conception haute fidélité, qui peuvent servir d’inspiration pour concevoir vos applications et améliorer l’expérience utilisateur. En outre, le look book met en évidence les meilleures pratiques en matière de conception et d’architecture suivies lors de la création de chaque application. Pour plus d’informations, voir le manuel d’extensibilité. Pour plus d’informations, voir [le manuel d’extensibilité.](https://adoption.microsoft.com/extensibility-look-book/scenarios/) 

## <a name="start-building"></a>Démarrer la création

Familiarisez-vous rapidement avec la création de Teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.

> [!div class="nextstepaction"]
> [Créer votre première application maintenant](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>S'intégrer aux équipes

Associez les fonctionnalités que les utilisateurs aiment d’une application web, d’un service ou d’un système existant aux fonctionnalités collaboratives de Teams.

> [!div class="nextstepaction"]
> [Intégrer une application existante](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>Un peu de code est très long

Vous n’avez pas besoin d’être un programmeur expert pour créer une application Teams de qualité. Essayez l’une des solutions à code faible.

> [!div class="nextstepaction"]
> [Créer une application à code faible](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>Ressources

* [Ajouter un bouton Partager avec Teams à votre site web](concepts/build-and-test/share-to-teams.md)
* [Concevoir votre application Teams](concepts/design/design-teams-app-overview.md)
* [Microsoft Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* SDK Bot Framework pour [JavaScript et](https://github.com/Microsoft/botbuilder-js) [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Publier votre application Teams](concepts/deploy-and-publish/overview.md)
