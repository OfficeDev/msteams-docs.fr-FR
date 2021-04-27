---
title: Vue d'ensemble des principes de base du développement d'applications
author: heath-hamilton
description: Décrire les concepts fondamentaux du développement de plateforme Teams.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b52eebf2b8e0884cd225298ae557bb7ac65d4a68
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020862"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="3aa94-103">Principes de base du développement d'applications Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3aa94-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="3aa94-104">Les principes de base de l'application Microsoft Teams donnent la direction dont vous avez besoin pour créer votre application Teams personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3aa94-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="3aa94-105">Vous pouvez reconnaître l'infrastructure requise pour planifier votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="3aa94-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="3aa94-106">Le document vous aide à comprendre la communication utilisateur-application et à déterminer le type de surfaces d'application que vous devez utiliser ou les API dont votre application peut avoir besoin dans le processus.</span><span class="sxs-lookup"><span data-stu-id="3aa94-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="3aa94-107">Inspirez-vous pour adopter l'interactivité qui peut renforcer l'expérience d'application lorsque vous intégrez Teams.</span><span class="sxs-lookup"><span data-stu-id="3aa94-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="3aa94-108">Fonctionnalités et points d'entrée</span><span class="sxs-lookup"><span data-stu-id="3aa94-108">Capabilities and entry points</span></span>

<span data-ttu-id="3aa94-109">Vous pouvez étendre votre application Teams de plusieurs manières.</span><span class="sxs-lookup"><span data-stu-id="3aa94-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="3aa94-110">Pour pouvoir étendre votre application, vous devez comprendre toutes les fonctionnalités principales et les points d'entrée qui fonctionnent dans un espace de collaboration.</span><span class="sxs-lookup"><span data-stu-id="3aa94-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="3aa94-111">Vous pouvez tester les points d'extension pour créer vos applications.</span><span class="sxs-lookup"><span data-stu-id="3aa94-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="3aa94-112">Les composants importants d'un projet d'application vous aident à configurer correctement votre page d'application.</span><span class="sxs-lookup"><span data-stu-id="3aa94-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="3aa94-113">L'application Teams peut avoir [plusieurs fonctionnalités et](../concepts/capabilities-overview.md) [points d'entrée.](../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="3aa94-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="3aa94-114">Comprendre vos cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="3aa94-114">Understand your use cases</span></span>

<span data-ttu-id="3aa94-115">Vous pouvez reconnaître les problèmes des utilisateurs et identifier les réponses à certains problèmes courants auxquels ils sont confrontés.</span><span class="sxs-lookup"><span data-stu-id="3aa94-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="3aa94-116">Vous pouvez créer votre application Teams en trouvant la combinaison qui répond aux besoins de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3aa94-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="3aa94-117">[Comprendre les cas d'utilisation](../concepts/design/understand-use-cases.md) pour savoir comment un utilisateur final interagit avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3aa94-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="3aa94-118">Vous apprenez à comprendre l'utilisateur et son problème.</span><span class="sxs-lookup"><span data-stu-id="3aa94-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="3aa94-119">Voici quelques questions fréquemment posées :</span><span class="sxs-lookup"><span data-stu-id="3aa94-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="3aa94-120">Avez-vous besoin d'une authentification ?</span><span class="sxs-lookup"><span data-stu-id="3aa94-120">Do you need authentication?</span></span>
* <span data-ttu-id="3aa94-121">Quel problème votre application va-t-elle résoudre ?</span><span class="sxs-lookup"><span data-stu-id="3aa94-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="3aa94-122">Qui sont les utilisateurs finaux de l'application ?</span><span class="sxs-lookup"><span data-stu-id="3aa94-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="3aa94-123">Comment l'expérience d'intégration doit-elle être et quelles autres sont les autres activités de l'application ?</span><span class="sxs-lookup"><span data-stu-id="3aa94-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="3aa94-124">Map vos cas d'utilisation aux fonctionnalités de l'application Teams</span><span class="sxs-lookup"><span data-stu-id="3aa94-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="3aa94-125">[Maposez vos cas d'utilisation](../concepts/design/map-use-cases.md) sur certains scénarios courants et sur la façon de choisir les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="3aa94-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="3aa94-126">Des informations pour partager votre application et collaborer sur des éléments dans un système externe sont fournies.</span><span class="sxs-lookup"><span data-stu-id="3aa94-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="3aa94-127">Vous pouvez également apprendre à initier des flux de travail et à envoyer des notifications aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3aa94-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="3aa94-128">Obtenez des conseils supplémentaires sur l'endroit où commencer, la mise en réseau avec les utilisateurs, les bots de conversation et la combinaison de plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3aa94-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="3aa94-129">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3aa94-129">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3aa94-130">Intégrer des applications web à Teams</span><span class="sxs-lookup"><span data-stu-id="3aa94-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3aa94-131">Créer votre première application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3aa94-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="3aa94-132">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="3aa94-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3aa94-133">Comprendre les fonctionnalités de l'application Teams</span><span class="sxs-lookup"><span data-stu-id="3aa94-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

