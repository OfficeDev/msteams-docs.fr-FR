---
title: Plateforme de développement teams
author: clearab
description: Vue d’ensemble de la façon dont les développeurs peuvent étendre et personnaliser les fonctionnalités de Microsoft teams à l’aide de la plateforme Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651936"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="a7c56-103">Création pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="a7c56-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="a7c56-104">Les applications Microsoft teams apportent des informations clés, des outils courants et des processus approuvés à des endroits où les utilisateurs recueillent, apprennent et travaillent de plus en plus.</span><span class="sxs-lookup"><span data-stu-id="a7c56-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="a7c56-105">Les applications vous permettent d’étendre les équipes pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="a7c56-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="a7c56-106">Vous pouvez créer une personnalisation pour teams ou simplement intégrer des fonctionnalités dans vos applications et services préférés.</span><span class="sxs-lookup"><span data-stu-id="a7c56-106">You can create something brand new for Teams or simply integrate features in your favorite apps and services.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="a7c56-107">Que peuvent faire les applications teams ?</span><span class="sxs-lookup"><span data-stu-id="a7c56-107">What can Teams apps do?</span></span>

<span data-ttu-id="a7c56-108">Les personnes découvrent et utilisent les applications teams via un ensemble de [fonctionnalités](capabilities-overview.md)de plateforme.</span><span class="sxs-lookup"><span data-stu-id="a7c56-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="a7c56-109">Certaines applications sont simples (envoyer des notifications), tandis que d’autres sont complexes (afficher les enregistrements patients).</span><span class="sxs-lookup"><span data-stu-id="a7c56-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="a7c56-110">Lors de la planification de votre application, rappelez-vous que teams est un hub de collaboration.</span><span class="sxs-lookup"><span data-stu-id="a7c56-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="a7c56-111">Les meilleures applications teams aident les utilisateurs à s’exprimer et à collaborer efficacement.</span><span class="sxs-lookup"><span data-stu-id="a7c56-111">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="get-information-more-conveniently"></a><span data-ttu-id="a7c56-112">Obtenir des informations plus facilement</span><span class="sxs-lookup"><span data-stu-id="a7c56-112">Get information more conveniently</span></span>

<span data-ttu-id="a7c56-113">Parfois, vous avez simplement besoin de faciliter la recherche.</span><span class="sxs-lookup"><span data-stu-id="a7c56-113">Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="a7c56-114">Afficher une page Web importante dans un [onglet](doc-links/what-are-tabs.md), qui fournit une expérience Web en plein écran pour le contenu statique et dynamique dans Teams.</span><span class="sxs-lookup"><span data-stu-id="a7c56-114">Display an important webpage in a [tab](doc-links/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

![Représentation conceptuelle des onglets qui ressemblent dans le client Teams.](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a><span data-ttu-id="a7c56-116">Partager des liens sans basculement de contexte</span><span class="sxs-lookup"><span data-stu-id="a7c56-116">Share links without switching context</span></span>

<span data-ttu-id="a7c56-117">Extrayez les informations dans une conversation et ne laissez pas Teams.</span><span class="sxs-lookup"><span data-stu-id="a7c56-117">Pull information into a conversation and never leave Teams.</span></span> <span data-ttu-id="a7c56-118">Par exemple, avec les [extensions de messagerie](doc-links/what-are-messaging-extensions.md) , vous pouvez partager du contenu riche et facilement digestible à partir d’un système externe à l’aide de la zone de composition du message.</span><span class="sxs-lookup"><span data-stu-id="a7c56-118">For example, with [messaging extensions](doc-links/what-are-messaging-extensions.md) you can share rich, easily digestible content from an external system using the message compose box.</span></span>

![Représentation conceptuelle des extensions de messagerie qui ressemblent dans le client teams](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a><span data-ttu-id="a7c56-120">Transformer les mots en actions</span><span class="sxs-lookup"><span data-stu-id="a7c56-120">Turn words into actions</span></span>

<span data-ttu-id="a7c56-121">Les conversations entraînent souvent un besoin (créer une commande, vérifier mon code, etc.).</span><span class="sxs-lookup"><span data-stu-id="a7c56-121">Conversations often result in the need to do something (create an order, review my code, etc.).</span></span> <span data-ttu-id="a7c56-122">Un [bot](doc-links/what-are-bots.md) peut lancer ces types de flux de travail directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="a7c56-122">A [bot](doc-links/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

![Représentation conceptuelle des robots qui se ressemblent dans le client teams](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a><span data-ttu-id="a7c56-124">Communiquer avec des services et des applications externes</span><span class="sxs-lookup"><span data-stu-id="a7c56-124">Communicate with external apps and services</span></span>

<span data-ttu-id="a7c56-125">Les [webhooks entrants](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) sont un moyen simple d’envoyer automatiquement des alertes à partir d’une autre application à un canal ou une conversation Teams.</span><span class="sxs-lookup"><span data-stu-id="a7c56-125">[Incoming webhooks](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send alerts from another app to a Teams channel or chat.</span></span> <span data-ttu-id="a7c56-126">Avec les [webhooks sortants](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), vous pouvez envoyer un message à votre service Web à l’aide d’une @mention.</span><span class="sxs-lookup"><span data-stu-id="a7c56-126">With [outgoing webhooks](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), you can send a message to your web service with an @mention.</span></span>

![Représentation conceptuelle des connecteurs qui ressemblent au client Teams.](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a><span data-ttu-id="a7c56-128">Utiliser les données de teams</span><span class="sxs-lookup"><span data-stu-id="a7c56-128">Utilize Teams data</span></span>

<span data-ttu-id="a7c56-129">L' [API REST Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview) donne accès à des informations sur les équipes, les canaux, les utilisateurs et les messages qui peuvent vous aider à créer ou améliorer les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="a7c56-129">The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

![«Représentation conceptuelle de l’API REST Microsoft Graph pour teams](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a><span data-ttu-id="a7c56-131">Commencer à créer</span><span class="sxs-lookup"><span data-stu-id="a7c56-131">Start building</span></span>

   <span data-ttu-id="a7c56-132">Familiarisez-vous rapidement avec la création de teams en créant une application simple et en ajoutant des fonctionnalités couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="a7c56-132">Quickly familiarize yourself with building for Teams by creating a simple app and adding a couple commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="a7c56-133">Créer votre première application maintenant</span><span class="sxs-lookup"><span data-stu-id="a7c56-133">Build your first app now</span></span>](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a><span data-ttu-id="a7c56-134">Ensemble</span><span class="sxs-lookup"><span data-stu-id="a7c56-134">Bring it all together</span></span>

   <span data-ttu-id="a7c56-135">Simplifiez les processus et les flux de travail pour les utilisateurs en combinant les applications Web, les services et les systèmes Web préférés de votre organisation avec des fonctionnalités collaboratives Teams.</span><span class="sxs-lookup"><span data-stu-id="a7c56-135">Simplify processes and workflows for users by blending your organization's favorite web apps, services, and systems with Teams collaborative features.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="a7c56-136">Intégration d’une application existante</span><span class="sxs-lookup"><span data-stu-id="a7c56-136">Integrate an existing app</span></span>](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a><span data-ttu-id="a7c56-137">Approuver le processus</span><span class="sxs-lookup"><span data-stu-id="a7c56-137">Trust the process</span></span>

   <span data-ttu-id="a7c56-138">Comprendre l’ensemble du processus de développement de la plateforme teams pour planifier, concevoir, créer et publier une application pour votre organisation ou tout le monde.</span><span class="sxs-lookup"><span data-stu-id="a7c56-138">Understand the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="a7c56-139">Démarrer la planification de votre application</span><span class="sxs-lookup"><span data-stu-id="a7c56-139">Start planning your app</span></span>](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a><span data-ttu-id="a7c56-140">Pas de code, pas de souci</span><span class="sxs-lookup"><span data-stu-id="a7c56-140">No code, no worries</span></span>

   <span data-ttu-id="a7c56-141">Vous n’avez pas besoin d’être programmeur pour créer une application intéressante.</span><span class="sxs-lookup"><span data-stu-id="a7c56-141">You don't need to be a programmer to build a great app.</span></span> <span data-ttu-id="a7c56-142">Créez une application teams avec peu ou pas de code à l’aide de Microsoft Power Platform.</span><span class="sxs-lookup"><span data-stu-id="a7c56-142">Create a Teams app with little to no code using the Microsoft Power Platform.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="a7c56-143">Importer une application Power Platform</span><span class="sxs-lookup"><span data-stu-id="a7c56-143">Import a Power Platform app</span></span>](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a><span data-ttu-id="a7c56-144">Ressources</span><span class="sxs-lookup"><span data-stu-id="a7c56-144">Resources</span></span>

* [<span data-ttu-id="a7c56-145">Ajouter un bouton partager à teams à votre site Web</span><span class="sxs-lookup"><span data-stu-id="a7c56-145">Add a Share to Teams button to your website</span></span>](doc-links/share-to-teams.md)
* [<span data-ttu-id="a7c56-146">Concevoir votre application à l’aide des recommandations recommandées</span><span class="sxs-lookup"><span data-stu-id="a7c56-146">Design your app using recommended guidelines</span></span>](doc-links/designing-overview.md)
* [<span data-ttu-id="a7c56-147">Système de conception de l’interface utilisateur Fluent</span><span class="sxs-lookup"><span data-stu-id="a7c56-147">Fluent UI Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="a7c56-148">Kit de développement logiciel (SDK) JavaScript client Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="a7c56-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* <span data-ttu-id="a7c56-149">[Kit de développement logiciel (SDK) robot for JavaScript](https://github.com/Microsoft/botbuilder-js) and [bot Framework SDK pour .net](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="a7c56-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
