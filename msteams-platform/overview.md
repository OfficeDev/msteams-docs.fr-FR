---
title: Créer des applications pour la plate Microsoft Teams plateforme
author: heath-hamilton
description: Obtenez un aperçu de la façon dont les développeurs peuvent étendre Microsoft Teams fonctionnalités avec des applications personnalisées.
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 8724b669476b11aa8cb1aca6d9586fc7ea42587d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566508"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="2e1e1-103">Créer des applications pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2e1e1-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="2e1e1-104">Microsoft Teams applications apportent des informations clés, des outils communs et des processus fiables là où les gens se rassemblent, apprennent et travaillent de plus en plus.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="2e1e1-105">Les applications sont la façon dont vous Teams pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="2e1e1-106">Créez quelque chose de nouveau pour Teams ou intégrez une application existante.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e1e1-107">Démarrer</span><span class="sxs-lookup"><span data-stu-id="2e1e1-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="2e1e1-108">Quelles sont Teams applications ?</span><span class="sxs-lookup"><span data-stu-id="2e1e1-108">What are Teams apps?</span></span>

<span data-ttu-id="2e1e1-109">Teams applications sont une combinaison de [fonctionnalités et de](concepts/capabilities-overview.md) [points d’entrée.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="2e1e1-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="2e1e1-110">Par exemple, les gens peuvent discuter avec le *bot* (capacité) de votre application dans un *canal* (point d’entrée).</span><span class="sxs-lookup"><span data-stu-id="2e1e1-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="2e1e1-111">Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (gérer les dossiers des patients).</span><span class="sxs-lookup"><span data-stu-id="2e1e1-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="2e1e1-112">Lors de la planification de votre application, n’oubliez Teams est un hub de collaboration.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="2e1e1-113">Les meilleures applications Teams aident les gens à s’exprimer et à mieux travailler ensemble.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="2e1e1-114">Onglets</span><span class="sxs-lookup"><span data-stu-id="2e1e1-114">Tabs</span></span>

<span data-ttu-id="2e1e1-115">**Obtenez des informations plus commodément**: Parfois, vous avez juste besoin de rendre les choses plus faciles à trouver.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="2e1e1-116">Affichez une page Web importante dans un [onglet,](tabs/what-are-tabs.md)qui fournit une expérience Web plein écran pour le contenu statique et dynamique dans Teams.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle de ce à quoi ressemblent les onglets dans Teams client." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="2e1e1-118">Bots</span><span class="sxs-lookup"><span data-stu-id="2e1e1-118">Bots</span></span>

<span data-ttu-id="2e1e1-119">**Transformez les mots en actions**: Les conversations entraînent souvent la nécessité de faire quelque chose (générer une commande, revoir mon code, vérifier l’état du billet, et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="2e1e1-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="2e1e1-120">Un [bot peut](bots/what-are-bots.md) lancer ce genre de flux de travail juste à l’intérieur Teams.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle de ce que les bots ressemblent dans Teams client." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="2e1e1-122">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2e1e1-122">Messaging extensions</span></span>

<span data-ttu-id="2e1e1-123">**Facilitez le multitâche :** Avec les [extensions de messagerie,](messaging-extensions/what-are-messaging-extensions.md)vous pouvez rapidement partager des informations externes dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="2e1e1-124">Vous pouvez également agir sur un message, comme la création d’un billet d’aide basé sur le contenu d’un message de chaîne.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de ce à quoi ressemblent les extensions de messagerie dans Teams client." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="2e1e1-126">Webhooks</span><span class="sxs-lookup"><span data-stu-id="2e1e1-126">Webhooks</span></span>

<span data-ttu-id="2e1e1-127">**Communiquez avec des applications externes**: Les [webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications d’une autre application à Teams canal.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="2e1e1-128">Avec [les webhooks sortants,](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envoie un message à votre service Web avec @mention.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de ce à quoi ressemblent les connecteurs dans Teams client." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="2e1e1-130">Microsoft Graph pour Teams</span><span class="sxs-lookup"><span data-stu-id="2e1e1-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="2e1e1-131">**Utilisez Teams données :** [L’API Microsoft Graph pour Teams donne](/graph/teams-concept-overview) accès à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou à améliorer des fonctionnalités pour votre application.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Graph Microsoft pour Teams." border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="2e1e1-133">Commencer à construire</span><span class="sxs-lookup"><span data-stu-id="2e1e1-133">Start building</span></span>

<span data-ttu-id="2e1e1-134">Familiarisez-vous rapidement avec la création Teams en installant votre environnement et en créant une application simple.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e1e1-135">Créer votre première application</span><span class="sxs-lookup"><span data-stu-id="2e1e1-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="2e1e1-136">S'intégrer aux équipes</span><span class="sxs-lookup"><span data-stu-id="2e1e1-136">Integrate with Teams</span></span>

<span data-ttu-id="2e1e1-137">Mélangez les fonctionnalités que les utilisateurs aiment dans une application web, un service ou un système existant avec les fonctionnalités collaboratives de Teams.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e1e1-138">Intégrer une application existante</span><span class="sxs-lookup"><span data-stu-id="2e1e1-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="2e1e1-139">Un peu de code va un long chemin</span><span class="sxs-lookup"><span data-stu-id="2e1e1-139">A little code goes a long way</span></span>

<span data-ttu-id="2e1e1-140">Vous n’avez pas besoin d’être un programmeur expert pour construire une grande Teams application.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="2e1e1-141">Essayez l’une des nombreuses solutions à code bas.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-141">Try one of the several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e1e1-142">Créer une application à code bas</span><span class="sxs-lookup"><span data-stu-id="2e1e1-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="2e1e1-143">Obtenez des idées pour votre application</span><span class="sxs-lookup"><span data-stu-id="2e1e1-143">Get ideas for your app</span></span>

<span data-ttu-id="2e1e1-144">Vous cherchez l’inspiration pour le développement d’applications ?</span><span class="sxs-lookup"><span data-stu-id="2e1e1-144">Looking for app development inspiration?</span></span> <span data-ttu-id="2e1e1-145">Parcourez notre liste de scénarios réels et de solutions de l’industrie avec des maquettes concept haute fidélité pour comprendre les différentes façons dont Teams applications peuvent aider vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2e1e1-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e1e1-146">Voir les scénarios d’applications</span><span class="sxs-lookup"><span data-stu-id="2e1e1-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="2e1e1-147">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2e1e1-147">See also</span></span>

* [<span data-ttu-id="2e1e1-148">Ajoutez un bouton Share-to-Teams à votre site Web</span><span class="sxs-lookup"><span data-stu-id="2e1e1-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="2e1e1-149">Concevez votre application Teams’argent</span><span class="sxs-lookup"><span data-stu-id="2e1e1-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="2e1e1-150">Microsoft Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="2e1e1-150">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="2e1e1-151">Bot Framework SDK pour [JavaScript](https://github.com/Microsoft/botbuilder-js) et [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="2e1e1-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="2e1e1-152">Distribuez votre Teams appe</span><span class="sxs-lookup"><span data-stu-id="2e1e1-152">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
