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
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="ceda3-103">Créer des applications pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="ceda3-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="ceda3-104">Les applications Microsoft teams apportent des informations clés, des outils courants et des processus approuvés à des endroits où les utilisateurs recueillent, apprennent et travaillent de plus en plus.</span><span class="sxs-lookup"><span data-stu-id="ceda3-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="ceda3-105">Les applications vous permettent d’étendre les équipes pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ceda3-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="ceda3-106">Créez un article nouveau pour teams ou intégrez une application existante.</span><span class="sxs-lookup"><span data-stu-id="ceda3-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="ceda3-107">Qu’est-ce que les applications teams ?</span><span class="sxs-lookup"><span data-stu-id="ceda3-107">What are Teams apps?</span></span>

<span data-ttu-id="ceda3-108">Les applications teams sont une combinaison de [fonctionnalités](concepts/capabilities-overview.md) et de [points d’entrée](concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="ceda3-108">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="ceda3-109">Par exemple, les utilisateurs peuvent discuter avec le *robot* de votre application (fonctionnalité) dans un *canal* (point d’entrée).</span><span class="sxs-lookup"><span data-stu-id="ceda3-109">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="ceda3-110">Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (gérer les enregistrements des patients).</span><span class="sxs-lookup"><span data-stu-id="ceda3-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="ceda3-111">Lors de la planification de votre application, rappelez-vous que teams est un hub de collaboration.</span><span class="sxs-lookup"><span data-stu-id="ceda3-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="ceda3-112">Les meilleures applications teams aident les utilisateurs à s’exprimer et à collaborer efficacement.</span><span class="sxs-lookup"><span data-stu-id="ceda3-112">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="ceda3-113">Onglets</span><span class="sxs-lookup"><span data-stu-id="ceda3-113">Tabs</span></span>

<span data-ttu-id="ceda3-114">**Obtenir des informations plus facilement**: parfois, vous avez simplement besoin de faciliter la recherche.</span><span class="sxs-lookup"><span data-stu-id="ceda3-114">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="ceda3-115">Afficher une page Web importante dans un [onglet](tabs/what-are-tabs.md), qui fournit une expérience Web en plein écran pour le contenu statique et dynamique dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ceda3-115">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Représentation conceptuelle des onglets qui ressemblent dans le client Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="ceda3-117">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="ceda3-117">Messaging extensions</span></span>

<span data-ttu-id="ceda3-118">Facilitez **le multitâche**: avec les [extensions de messagerie](messaging-extensions/what-are-messaging-extensions.md), vous pouvez partager rapidement des informations externes dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="ceda3-118">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="ceda3-119">Vous pouvez également agir sur un message, tel que la création d’un ticket d’aide basé sur le contenu d’un billet de canal.</span><span class="sxs-lookup"><span data-stu-id="ceda3-119">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Représentation conceptuelle de l’apparence des extensions de messagerie dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="ceda3-121">Bots</span><span class="sxs-lookup"><span data-stu-id="ceda3-121">Bots</span></span>

<span data-ttu-id="ceda3-122">**Transformer les mots en actions**: les conversations entraînent souvent une action (générer une commande, vérifier mon code, vérifier l’état du ticket, etc.).</span><span class="sxs-lookup"><span data-stu-id="ceda3-122">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="ceda3-123">Un [bot](bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ceda3-123">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Représentation conceptuelle des robots qui se ressemblent dans le client Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="ceda3-125">Webhooks</span><span class="sxs-lookup"><span data-stu-id="ceda3-125">Webhooks</span></span>

<span data-ttu-id="ceda3-126">**Communiquer avec des applications externes**: les [webhooks entrants](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications à partir d’une autre application vers un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="ceda3-126">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="ceda3-127">Avec les [webhooks sortants, envoyez](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)un message à votre service Web à l’aide d’une @mention.</span><span class="sxs-lookup"><span data-stu-id="ceda3-127">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Représentation conceptuelle des connecteurs qui ressemblent au client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="ceda3-129">Microsoft Graph pour teams</span><span class="sxs-lookup"><span data-stu-id="ceda3-129">Microsoft Graph for Teams</span></span>

<span data-ttu-id="ceda3-130">**Utiliser les données teams**: l' [API Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview) fournit un accès aux informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="ceda3-130">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API Microsoft Graph pour Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="ceda3-132">Prise en main</span><span class="sxs-lookup"><span data-stu-id="ceda3-132">Get started</span></span>

<span data-ttu-id="ceda3-133">Accédez directement à l’aide de nos didacticiels d’application ou Découvrez comment intégrer et importer des applications existantes.</span><span class="sxs-lookup"><span data-stu-id="ceda3-133">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="ceda3-134">Commencer à créer</span><span class="sxs-lookup"><span data-stu-id="ceda3-134">Start building</span></span>

   <span data-ttu-id="ceda3-135">Familiarisez-vous rapidement avec la création de teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="ceda3-135">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="ceda3-136">Créer votre première application maintenant</span><span class="sxs-lookup"><span data-stu-id="ceda3-136">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="ceda3-137">Intégration à teams</span><span class="sxs-lookup"><span data-stu-id="ceda3-137">Integrate with Teams</span></span>

   <span data-ttu-id="ceda3-138">Combinez les fonctionnalités que les utilisateurs aiment à une application Web existante, un service ou un système avec les fonctionnalités collaboratives de teams.</span><span class="sxs-lookup"><span data-stu-id="ceda3-138">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="ceda3-139">Intégration d’une application existante</span><span class="sxs-lookup"><span data-stu-id="ceda3-139">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="ceda3-140">Un petit code est long</span><span class="sxs-lookup"><span data-stu-id="ceda3-140">A little code goes a long way</span></span>

   <span data-ttu-id="ceda3-141">Vous n’avez pas besoin d’être un programmeur expert pour créer une application de qualité de teams.</span><span class="sxs-lookup"><span data-stu-id="ceda3-141">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="ceda3-142">Essayez l’une des solutions à faible code.</span><span class="sxs-lookup"><span data-stu-id="ceda3-142">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="ceda3-143">Créer une application à code bas</span><span class="sxs-lookup"><span data-stu-id="ceda3-143">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="ceda3-144">Ressources</span><span class="sxs-lookup"><span data-stu-id="ceda3-144">Resources</span></span>

* [<span data-ttu-id="ceda3-145">Ajouter un bouton partager à teams à votre site Web</span><span class="sxs-lookup"><span data-stu-id="ceda3-145">Add a Share to Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="ceda3-146">Système de conception Fluent</span><span class="sxs-lookup"><span data-stu-id="ceda3-146">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="ceda3-147">Kit de développement logiciel (SDK) JavaScript client Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="ceda3-147">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="ceda3-148">[Kit de développement logiciel (SDK) robot for JavaScript](https://github.com/Microsoft/botbuilder-js) and [bot Framework SDK pour .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="ceda3-148">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="ceda3-149">Publier votre application dans une organisation ou AppSource</span><span class="sxs-lookup"><span data-stu-id="ceda3-149">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
