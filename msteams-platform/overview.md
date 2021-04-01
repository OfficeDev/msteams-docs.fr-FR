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
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="99bbf-103">Créer des applications pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="99bbf-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="99bbf-104">Les applications Microsoft Teams apportent des informations clés, des outils courants et des processus de confiance où les personnes se rassemblent, apprennent et travaillent de plus en plus.</span><span class="sxs-lookup"><span data-stu-id="99bbf-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="99bbf-105">Les applications sont la façon dont vous étendez Teams pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="99bbf-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="99bbf-106">Créez quelque chose de nouveau pour Teams ou intégrez une application existante.</span><span class="sxs-lookup"><span data-stu-id="99bbf-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99bbf-107">Démarrer</span><span class="sxs-lookup"><span data-stu-id="99bbf-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="99bbf-108">Qu’est-ce que les applications Teams ?</span><span class="sxs-lookup"><span data-stu-id="99bbf-108">What are Teams apps?</span></span>

<span data-ttu-id="99bbf-109">Les applications Teams sont une combinaison de [fonctionnalités et](concepts/capabilities-overview.md) de [points d’entrée.](concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="99bbf-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="99bbf-110">Par exemple, les personnes peuvent discuter avec le *bot* de votre application (fonctionnalité) dans un *canal* (point d’entrée).</span><span class="sxs-lookup"><span data-stu-id="99bbf-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="99bbf-111">Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (gérer les enregistrements des patients).</span><span class="sxs-lookup"><span data-stu-id="99bbf-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="99bbf-112">Lors de la planification de votre application, n’oubliez pas que Teams est un hub de collaboration.</span><span class="sxs-lookup"><span data-stu-id="99bbf-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="99bbf-113">Les meilleures applications Teams aident les personnes à s’exprimer et à travailler mieux ensemble.</span><span class="sxs-lookup"><span data-stu-id="99bbf-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="99bbf-114">Onglets</span><span class="sxs-lookup"><span data-stu-id="99bbf-114">Tabs</span></span>

<span data-ttu-id="99bbf-115">**Obtenir des informations plus facilement**: parfois, il vous suffit de faciliter la recherche.</span><span class="sxs-lookup"><span data-stu-id="99bbf-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="99bbf-116">Affichez une page web importante dans un [onglet,](tabs/what-are-tabs.md)ce qui fournit une expérience web en plein écran pour le contenu statique et dynamique dans Teams.</span><span class="sxs-lookup"><span data-stu-id="99bbf-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle de l’apparence des onglets dans le client Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="99bbf-118">Bots</span><span class="sxs-lookup"><span data-stu-id="99bbf-118">Bots</span></span>

<span data-ttu-id="99bbf-119">**Transformer des mots en actions**: les conversations entraînent souvent la nécessité d’une action (générer une commande, passer en revue mon code, vérifier l’état du ticket, etc.).</span><span class="sxs-lookup"><span data-stu-id="99bbf-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="99bbf-120">Un [bot](bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="99bbf-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle de l’apparence des bots dans le client Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="99bbf-122">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="99bbf-122">Messaging extensions</span></span>

<span data-ttu-id="99bbf-123">**Faciliter la tâche multitâche**: avec les [extensions](messaging-extensions/what-are-messaging-extensions.md)de messagerie, vous pouvez rapidement partager des informations externes dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="99bbf-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="99bbf-124">Vous pouvez également agir sur un message, par exemple créer un ticket d’aide basé sur le contenu d’un billet de canal.</span><span class="sxs-lookup"><span data-stu-id="99bbf-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de l’apparence des extensions de messagerie dans le client Teams." border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="99bbf-126">Webhooks</span><span class="sxs-lookup"><span data-stu-id="99bbf-126">Webhooks</span></span>

<span data-ttu-id="99bbf-127">**Communiquer avec des applications externes**: [les webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications à partir d’une autre application vers un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="99bbf-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="99bbf-128">Les [webhooks sortants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)envoient un message à votre service web avec une @mention.</span><span class="sxs-lookup"><span data-stu-id="99bbf-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle de l’apparence des connecteurs dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="99bbf-130">Microsoft Graph pour Teams</span><span class="sxs-lookup"><span data-stu-id="99bbf-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="99bbf-131">**Utiliser les données Teams**: l’API [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview) pour Teams permet d’accéder à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer des fonctionnalités pour votre application.</span><span class="sxs-lookup"><span data-stu-id="99bbf-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Microsoft Graph pour Teams." border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a><span data-ttu-id="99bbf-133">Créer des solutions pour les applications Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="99bbf-133">Build solutions for Microsoft Teams apps</span></span>
 
<span data-ttu-id="99bbf-134">Microsoft propose un look book d’extensibilité, une bibliothèque de scénarios pour les applications Teams organisées par secteur d’activité.</span><span class="sxs-lookup"><span data-stu-id="99bbf-134">Microsoft offers an extensibility look book, a scenario library for Teams apps organized by industry.</span></span> <span data-ttu-id="99bbf-135">Ce livre vous aide à créer des applications sur la plateforme Teams et à comprendre différents scénarios possibles à l’aide de différentes fonctionnalités de la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="99bbf-135">This book helps you build apps on the Teams platform and understand different possible scenarios using various Teams platform capabilities.</span></span> <span data-ttu-id="99bbf-136">Les scénarios de look book commencent par un problème d’entreprise, les personnes impliquées avec leurs défis et se terminent par une solution d’application Teams qui permet de répondre aux besoins de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="99bbf-136">The look book scenarios start with a business problem, the personas involved along with their challenges, and end with a Teams app solution addressing the business needs.</span></span>

<span data-ttu-id="99bbf-137">Chaque scénario de cette bibliothèque est accompagné d’un ensemble de maquettes de concept de conception haute fidélité, qui peuvent servir d’inspiration pour concevoir vos applications et améliorer l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="99bbf-137">Each scenario in this library is accompanied by a set of high-fidelity design concept mocks, which can serve as an inspiration for designing your apps and enhancing user experience.</span></span> <span data-ttu-id="99bbf-138">En outre, le look book met en évidence les meilleures pratiques en matière de conception et d’architecture suivies lors de la création de chaque application.</span><span class="sxs-lookup"><span data-stu-id="99bbf-138">In addition, the look book highlights the design and architecture best practices followed in building each app.</span></span> <span data-ttu-id="99bbf-139">Pour plus d’informations, voir le manuel d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="99bbf-139">For more information, see the extensibility look book.</span></span> <span data-ttu-id="99bbf-140">Pour plus d’informations, voir [le manuel d’extensibilité.](https://adoption.microsoft.com/extensibility-look-book/scenarios/)</span><span class="sxs-lookup"><span data-stu-id="99bbf-140">For more information, see [extensibility look book](https://adoption.microsoft.com/extensibility-look-book/scenarios/).</span></span> 

## <a name="start-building"></a><span data-ttu-id="99bbf-141">Démarrer la création</span><span class="sxs-lookup"><span data-stu-id="99bbf-141">Start building</span></span>

<span data-ttu-id="99bbf-142">Familiarisez-vous rapidement avec la création de Teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="99bbf-142">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99bbf-143">Créer votre première application maintenant</span><span class="sxs-lookup"><span data-stu-id="99bbf-143">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="99bbf-144">S'intégrer aux équipes</span><span class="sxs-lookup"><span data-stu-id="99bbf-144">Integrate with Teams</span></span>

<span data-ttu-id="99bbf-145">Associez les fonctionnalités que les utilisateurs aiment d’une application web, d’un service ou d’un système existant aux fonctionnalités collaboratives de Teams.</span><span class="sxs-lookup"><span data-stu-id="99bbf-145">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99bbf-146">Intégrer une application existante</span><span class="sxs-lookup"><span data-stu-id="99bbf-146">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="99bbf-147">Un peu de code est très long</span><span class="sxs-lookup"><span data-stu-id="99bbf-147">A little code goes a long way</span></span>

<span data-ttu-id="99bbf-148">Vous n’avez pas besoin d’être un programmeur expert pour créer une application Teams de qualité.</span><span class="sxs-lookup"><span data-stu-id="99bbf-148">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="99bbf-149">Essayez l’une des solutions à code faible.</span><span class="sxs-lookup"><span data-stu-id="99bbf-149">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99bbf-150">Créer une application à code faible</span><span class="sxs-lookup"><span data-stu-id="99bbf-150">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="99bbf-151">Ressources</span><span class="sxs-lookup"><span data-stu-id="99bbf-151">Resources</span></span>

* [<span data-ttu-id="99bbf-152">Ajouter un bouton Partager avec Teams à votre site web</span><span class="sxs-lookup"><span data-stu-id="99bbf-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="99bbf-153">Concevoir votre application Teams</span><span class="sxs-lookup"><span data-stu-id="99bbf-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="99bbf-154">Microsoft Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="99bbf-154">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="99bbf-155">SDK Bot Framework pour [JavaScript et](https://github.com/Microsoft/botbuilder-js) [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="99bbf-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="99bbf-156">Publier votre application Teams</span><span class="sxs-lookup"><span data-stu-id="99bbf-156">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
