---
title: Plateforme de développeurs Microsoft teams
author: clearab
description: Vue d’ensemble de la façon dont les développeurs peuvent étendre et personnaliser les fonctionnalités de Microsoft teams à l’aide de la plateforme Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 73cbd4f68d8878872147bd412972495de1b5de6e
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964570"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="4535f-103">Création pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="4535f-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="4535f-104">Les applications Microsoft teams apportent des informations clés, des outils courants et des processus approuvés à des endroits où les utilisateurs recueillent, apprennent et travaillent de plus en plus.</span><span class="sxs-lookup"><span data-stu-id="4535f-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="4535f-105">Les applications vous permettent d’étendre les équipes pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4535f-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="4535f-106">Créez un article nouveau pour teams ou intégrez une application existante.</span><span class="sxs-lookup"><span data-stu-id="4535f-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="4535f-107">Qu’est-ce que les applications teams ?</span><span class="sxs-lookup"><span data-stu-id="4535f-107">What are Teams apps?</span></span>

<span data-ttu-id="4535f-108">Les personnes découvrent et utilisent les applications teams via un ensemble de [fonctionnalités](capabilities-overview.md)de plateforme.</span><span class="sxs-lookup"><span data-stu-id="4535f-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="4535f-109">Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (afficher les enregistrements patients).</span><span class="sxs-lookup"><span data-stu-id="4535f-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="4535f-110">Lors de la planification de votre application, rappelez-vous que teams est un hub de collaboration.</span><span class="sxs-lookup"><span data-stu-id="4535f-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="4535f-111">Les meilleures applications teams aident les utilisateurs à s’exprimer et à collaborer efficacement.</span><span class="sxs-lookup"><span data-stu-id="4535f-111">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="4535f-112">Onglets</span><span class="sxs-lookup"><span data-stu-id="4535f-112">Tabs</span></span>

<span data-ttu-id="4535f-113">**Obtenir des informations plus facilement**: parfois, vous avez simplement besoin de faciliter la recherche.</span><span class="sxs-lookup"><span data-stu-id="4535f-113">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="4535f-114">Afficher une page Web importante dans un [onglet](../tabs/what-are-tabs.md), qui fournit une expérience Web en plein écran pour le contenu statique et dynamique dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4535f-114">Display an important webpage in a [tab](../tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="doc-links/images/overview-tabs.png" alt-text="Représentation conceptuelle des onglets qui ressemblent dans le client Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="4535f-116">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4535f-116">Messaging extensions</span></span>

<span data-ttu-id="4535f-117">Facilitez **le multitâche**: avec les [extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md), vous pouvez partager rapidement des informations externes dans une conversation.</span><span class="sxs-lookup"><span data-stu-id="4535f-117">**Make it easier to multitask**: With [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="4535f-118">Vous pouvez également agir sur un message, tel que la création d’un ticket d’aide basé sur le contenu d’un billet de canal.</span><span class="sxs-lookup"><span data-stu-id="4535f-118">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="doc-links/images/overview-messaging.png" alt-text="Représentation conceptuelle de l’apparence des extensions de messagerie dans le client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="4535f-120">Bots</span><span class="sxs-lookup"><span data-stu-id="4535f-120">Bots</span></span>

<span data-ttu-id="4535f-121">**Transformer les mots en actions**: les conversations entraînent souvent une action (générer une commande, vérifier mon code, vérifier l’état du ticket, etc.).</span><span class="sxs-lookup"><span data-stu-id="4535f-121">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="4535f-122">Un [bot](../bots/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4535f-122">A [bot](../bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="doc-links/images/overview-bots.png" alt-text="Représentation conceptuelle des robots qui se ressemblent dans le client Teams." border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="4535f-124">Webhooks</span><span class="sxs-lookup"><span data-stu-id="4535f-124">Webhooks</span></span>

<span data-ttu-id="4535f-125">**Communiquer avec des applications externes**: les [webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des notifications à partir d’une autre application vers un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="4535f-125">**Communicate with external apps**: [Incoming webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="4535f-126">Avec les [webhooks sortants, envoyez](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)un message à votre service Web à l’aide d’une @mention.</span><span class="sxs-lookup"><span data-stu-id="4535f-126">With [outgoing webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="doc-links/images/overview-connectors.png" alt-text="Représentation conceptuelle des connecteurs qui ressemblent au client Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="4535f-128">Microsoft Graph pour teams</span><span class="sxs-lookup"><span data-stu-id="4535f-128">Microsoft Graph for Teams</span></span>

<span data-ttu-id="4535f-129">**Utiliser les données teams**: l' [API REST Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview) permet d’accéder à des informations sur des équipes, des canaux, des utilisateurs et des messages qui peuvent vous aider à créer ou améliorer des fonctionnalités pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4535f-129">**Utilize Teams data**: The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="doc-links/images/overview-graph.png" alt-text="Représentation conceptuelle de l’API REST Microsoft Graph pour Teams." border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="4535f-131">Prise en main</span><span class="sxs-lookup"><span data-stu-id="4535f-131">Get started</span></span>

<span data-ttu-id="4535f-132">Accédez directement à l’aide de nos didacticiels d’application, Découvrez comment intégrer et importer des applications existantes ou prendre le temps de découvrir le cycle de vie de développement des applications Teams.</span><span class="sxs-lookup"><span data-stu-id="4535f-132">Jump right in with our first app tutorials, find out how to integrate and import existing apps, or take your time to learn about the Teams app development lifecycle.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="4535f-133">Commencer à créer</span><span class="sxs-lookup"><span data-stu-id="4535f-133">Start building</span></span>

   <span data-ttu-id="4535f-134">Familiarisez-vous rapidement avec la création de teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="4535f-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="4535f-135">Créer votre première application maintenant</span><span class="sxs-lookup"><span data-stu-id="4535f-135">Build your first app now</span></span>](build-your-first-app/building-real-world-app.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="4535f-136">Intégration à teams</span><span class="sxs-lookup"><span data-stu-id="4535f-136">Integrate with Teams</span></span>

   <span data-ttu-id="4535f-137">Combinez les fonctionnalités que les utilisateurs aiment à une application Web existante, un service ou un système avec les fonctionnalités collaboratives de teams.</span><span class="sxs-lookup"><span data-stu-id="4535f-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="4535f-138">Intégration d’une application existante</span><span class="sxs-lookup"><span data-stu-id="4535f-138">Integrate an existing app</span></span>](migrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="4535f-139">Un petit code est long</span><span class="sxs-lookup"><span data-stu-id="4535f-139">A little code goes a long way</span></span>

   <span data-ttu-id="4535f-140">Vous n’avez pas besoin d’être un programmeur expert pour créer une application de qualité de teams.</span><span class="sxs-lookup"><span data-stu-id="4535f-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="4535f-141">Essayez l’une des solutions à faible code.</span><span class="sxs-lookup"><span data-stu-id="4535f-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="4535f-142">Créer une application à code bas</span><span class="sxs-lookup"><span data-stu-id="4535f-142">Create a low-code app</span></span>](low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="trust-the-process"></a><span data-ttu-id="4535f-143">Approuver le processus</span><span class="sxs-lookup"><span data-stu-id="4535f-143">Trust the process</span></span>

   <span data-ttu-id="4535f-144">Découvrez l’ensemble du processus de développement de la plateforme teams pour planifier, concevoir, créer et publier une application pour votre organisation ou tout le monde.</span><span class="sxs-lookup"><span data-stu-id="4535f-144">Learn the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="4535f-145">Démarrer la planification de votre application</span><span class="sxs-lookup"><span data-stu-id="4535f-145">Start planning your app</span></span>](../concepts/extensibility-points.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="4535f-146">Ressources</span><span class="sxs-lookup"><span data-stu-id="4535f-146">Resources</span></span>

* [<span data-ttu-id="4535f-147">Ajouter un bouton partager à teams à votre site Web</span><span class="sxs-lookup"><span data-stu-id="4535f-147">Add a Share to Teams button to your website</span></span>](../concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="4535f-148">Système de conception Fluent</span><span class="sxs-lookup"><span data-stu-id="4535f-148">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="4535f-149">Microsoft teams JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="4535f-149">Microsoft Teams JavaScript SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="4535f-150">[Kit de développement logiciel (SDK) robot for JavaScript](https://github.com/Microsoft/botbuilder-js) and [bot Framework SDK pour .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="4535f-150">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="4535f-151">Publier votre application dans une organisation ou AppSource</span><span class="sxs-lookup"><span data-stu-id="4535f-151">Publish your app to an organization or AppSource</span></span>](../concepts/deploy-and-publish/overview.md)
