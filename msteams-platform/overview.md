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
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="37394-103">Créer des applications pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="37394-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="37394-104">Microsoft Teams applications apportent des informations clés, des outils courants et des processus fiables là où les personnes se rassemblent, apprennent et travaillent de plus en plus.</span><span class="sxs-lookup"><span data-stu-id="37394-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="37394-105">Les applications vous permettent d'étendre Teams pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="37394-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="37394-106">Créez un tout nouveau Teams ou intégrez une application existante.</span><span class="sxs-lookup"><span data-stu-id="37394-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37394-107">Démarrer</span><span class="sxs-lookup"><span data-stu-id="37394-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="37394-108">Qu'est-ce Teams applications ?</span><span class="sxs-lookup"><span data-stu-id="37394-108">What are Teams apps?</span></span>

<span data-ttu-id="37394-109">Teams applications sont une combinaison de [fonctionnalités et](concepts/capabilities-overview.md) de [points d'entrée.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="37394-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="37394-110">Par exemple, les personnes peuvent discuter avec le *bot* de votre application (fonctionnalité) dans un *canal* (point d'entrée).</span><span class="sxs-lookup"><span data-stu-id="37394-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="37394-111">Certaines applications sont simples (envoyer des notifications), tandis que d'autres sont complexes (gérer les enregistrements des patients).</span><span class="sxs-lookup"><span data-stu-id="37394-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="37394-112">Lors de la planification de votre application, n'oubliez Teams est un hub de collaboration.</span><span class="sxs-lookup"><span data-stu-id="37394-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="37394-113">Les meilleures Teams permettent aux personnes de s'exprimer et de travailler mieux ensemble.</span><span class="sxs-lookup"><span data-stu-id="37394-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="37394-114">Onglets</span><span class="sxs-lookup"><span data-stu-id="37394-114">Tabs</span></span>

<span data-ttu-id="37394-115">**Obtenir des informations plus facilement**: parfois, il vous suffit de faciliter la recherche.</span><span class="sxs-lookup"><span data-stu-id="37394-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="37394-116">Affichez une page web importante dans un [onglet,](tabs/what-are-tabs.md)ce qui fournit une expérience web en plein écran pour le contenu statique et dynamique dans Teams.</span><span class="sxs-lookup"><span data-stu-id="37394-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle de l'apparence des onglets dans le client Teams client." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="37394-118">Bots</span><span class="sxs-lookup"><span data-stu-id="37394-118">Bots</span></span>

<span data-ttu-id="37394-119">**Transformer des mots en actions**: les conversations entraînent souvent la nécessité d'une action (générer une commande, passer en revue mon code, vérifier l'état du ticket, et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="37394-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="37394-120">Un [bot](bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="37394-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle de l'apparence des bots dans le client Teams client." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="37394-122">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="37394-122">Messaging extensions</span></span>

<span data-ttu-id="37394-123">**Faciliter la tâche multitâche**: avec les [extensions](messaging-extensions/what-are-messaging-extensions.md)de messagerie, vous pouvez rapidement partager des informations externes dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="37394-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="37394-124">Vous pouvez également agir sur un message, par exemple créer un ticket d'aide basé sur le contenu d'un billet de canal.</span><span class="sxs-lookup"><span data-stu-id="37394-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de l'apparence des extensions de messagerie dans Teams client." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="37394-126">Webhooks</span><span class="sxs-lookup"><span data-stu-id="37394-126">Webhooks</span></span>

<span data-ttu-id="37394-127">**Communiquer avec des applications externes**: les [webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d'envoyer automatiquement des notifications à partir d'une autre application vers Teams canal.</span><span class="sxs-lookup"><span data-stu-id="37394-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="37394-128">Les [webhooks sortants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envoient un message à votre service web avec une @mention.</span><span class="sxs-lookup"><span data-stu-id="37394-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de l'apparence des connecteurs dans le client Teams client." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="37394-130">Microsoft Graph for Teams</span><span class="sxs-lookup"><span data-stu-id="37394-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="37394-131">Utiliser **Teams** données : [l'API Microsoft Graph pour Teams](https://docs.microsoft.com/graph/teams-concept-overview) fournit l'accès à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="37394-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l'API microsoft Graph pour Teams." border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="37394-133">Démarrer la création</span><span class="sxs-lookup"><span data-stu-id="37394-133">Start building</span></span>

<span data-ttu-id="37394-134">Familiarisez-vous rapidement avec la création de Teams en mettant en place votre environnement et en créant une application simple.</span><span class="sxs-lookup"><span data-stu-id="37394-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37394-135">Créer votre première application</span><span class="sxs-lookup"><span data-stu-id="37394-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="37394-136">S'intégrer aux équipes</span><span class="sxs-lookup"><span data-stu-id="37394-136">Integrate with Teams</span></span>

<span data-ttu-id="37394-137">Associez les fonctionnalités que les utilisateurs aiment d'une application web, d'un service ou d'un système existant aux fonctionnalités collaboratives de Teams.</span><span class="sxs-lookup"><span data-stu-id="37394-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37394-138">Intégrer une application existante</span><span class="sxs-lookup"><span data-stu-id="37394-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="37394-139">Un peu de code est très long</span><span class="sxs-lookup"><span data-stu-id="37394-139">A little code goes a long way</span></span>

<span data-ttu-id="37394-140">Vous n'avez pas besoin d'être un programmeur expert pour créer une application Teams excellente.</span><span class="sxs-lookup"><span data-stu-id="37394-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="37394-141">Essayez l'une des solutions à code faible.</span><span class="sxs-lookup"><span data-stu-id="37394-141">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37394-142">Créer une application à code faible</span><span class="sxs-lookup"><span data-stu-id="37394-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="37394-143">Obtenir des idées pour votre application</span><span class="sxs-lookup"><span data-stu-id="37394-143">Get ideas for your app</span></span>

<span data-ttu-id="37394-144">Vous recherchez une source d'inspiration pour le développement d'applications ?</span><span class="sxs-lookup"><span data-stu-id="37394-144">Looking for app development inspiration?</span></span> <span data-ttu-id="37394-145">Parcourez notre liste de scénarios réels et de solutions industrielles avec des maquettes de concept haute fidélité pour comprendre les différentes façons Teams applications peuvent aider vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="37394-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37394-146">Voir les scénarios d'application</span><span class="sxs-lookup"><span data-stu-id="37394-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="37394-147">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="37394-147">See also</span></span>

* [<span data-ttu-id="37394-148">Ajouter un bouton Partager à Teams votre site web</span><span class="sxs-lookup"><span data-stu-id="37394-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="37394-149">Concevoir votre application Teams web</span><span class="sxs-lookup"><span data-stu-id="37394-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="37394-150">Microsoft Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="37394-150">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="37394-151">SDK Bot Framework pour [JavaScript et](https://github.com/Microsoft/botbuilder-js) [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="37394-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="37394-152">Distribuer votre application Teams de messagerie</span><span class="sxs-lookup"><span data-stu-id="37394-152">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
