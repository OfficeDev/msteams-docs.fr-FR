---
title: Comprendre les capacités de l’application
author: heath-hamilton
description: Teams d’applications expliquées
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565150"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="7a98f-103">Comprendre les Microsoft Teams’applications</span><span class="sxs-lookup"><span data-stu-id="7a98f-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="7a98f-104">L’extensibilité ou les points d’entrée sont différentes façons dont une application peut se manifester à un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7a98f-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="7a98f-105">Par exemple, un utilisateur peut interagir avec une application sur un onglet de toile pour faire une activité ou peut choisir de faire de même à l’aide d’un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="7a98f-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="7a98f-106">Les différentes fonctionnalités utilisées pour créer votre application Teams vous permettent d’augmenter sa portée d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="7a98f-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="7a98f-107">Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique.</span><span class="sxs-lookup"><span data-stu-id="7a98f-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="7a98f-108">Certains n’ont qu’une seule capacité, comme un webhook, tandis que d’autres ont plus d’une fonctionnalité pour donner aux utilisateurs diverses options.</span><span class="sxs-lookup"><span data-stu-id="7a98f-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="7a98f-109">Par exemple, votre application peut afficher des données dans un emplacement central, c’est-à-dire **l’onglet** et présenter ces mêmes informations via une interface conversationnelle, c’est-à-dire **le bot**.</span><span class="sxs-lookup"><span data-stu-id="7a98f-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="7a98f-110">Fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="7a98f-110">App capabilities</span></span>

<span data-ttu-id="7a98f-111">Votre Teams’application a une ou toutes les fonctionnalités de base suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a98f-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="7a98f-112">Onglets</span><span class="sxs-lookup"><span data-stu-id="7a98f-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="7a98f-113">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7a98f-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="7a98f-114">Bots</span><span class="sxs-lookup"><span data-stu-id="7a98f-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="7a98f-115">Webhooks et connecteurs</span><span class="sxs-lookup"><span data-stu-id="7a98f-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="7a98f-116">Votre application peut également tirer parti des fonctionnalités avancées, telles que [l’API microsoft Graph pour Teams](/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="7a98f-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="7a98f-117">L’illustration suivante vous donne une idée des fonctionnalités qui fourniront les fonctionnalités que vous souhaitez dans votre application :</span><span class="sxs-lookup"><span data-stu-id="7a98f-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app:</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Carte mentale illustrant ce que Teams d’application sont.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="7a98f-119">Considérez toujours votre utilisateur</span><span class="sxs-lookup"><span data-stu-id="7a98f-119">Always consider your user</span></span>

<span data-ttu-id="7a98f-120">En vous familiarisez avec le développement Teams’applications, vous comprenez ses fondamentaux fondamentaux.</span><span class="sxs-lookup"><span data-stu-id="7a98f-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="7a98f-121">Vous comprenez qu’il existe plus d’une façon de construire certaines fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="7a98f-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="7a98f-122">Dans de tels scénarios, réfléchissez à la façon dont vous pouvez fournir une expérience plus native à votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7a98f-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="7a98f-123">Par exemple, vous pouvez collecter l’entrée de l’utilisateur sous un formulaire construit comme onglet dans l’application.</span><span class="sxs-lookup"><span data-stu-id="7a98f-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="7a98f-124">Vous pouvez également le faire à l’aide d’un module de tâches sans changer de vue et perturber le flux de travail de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7a98f-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="7a98f-125">Il est important de choisir des points d’extension qui offrent le moins d’écart par rapport au flux de travail régulier d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7a98f-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="7a98f-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7a98f-126">See also</span></span>

[<span data-ttu-id="7a98f-127">Créez des applications pour Teams</span><span class="sxs-lookup"><span data-stu-id="7a98f-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="7a98f-128">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="7a98f-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a98f-129">Points d'entrée de l'application Teams</span><span class="sxs-lookup"><span data-stu-id="7a98f-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
