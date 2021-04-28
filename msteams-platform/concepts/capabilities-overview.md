---
title: Comprendre les fonctionnalités de l'application
author: heath-hamilton
description: Fonctionnalités de l'application Teams expliquées
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: f670f1f7b3db01f89fab4335c33f92e02cad1d9a
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058487"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="190a1-103">Comprendre les fonctionnalités de l'application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="190a1-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="190a1-104">L'extensibilité ou les points d'entrée sont différentes façons dont une application peut se manifester pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="190a1-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="190a1-105">Par exemple, un utilisateur peut interagir avec une application sur un onglet de zone de dessin pour faire une activité ou peut choisir d'en faire de même à l'aide d'un bot de conversation.</span><span class="sxs-lookup"><span data-stu-id="190a1-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="190a1-106">Les différentes fonctionnalités utilisées pour créer votre application Teams vous permettent d'augmenter son étendue d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="190a1-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="190a1-107">Il existe plusieurs façons d'étendre Teams, de sorte que chaque application est unique.</span><span class="sxs-lookup"><span data-stu-id="190a1-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="190a1-108">Certaines n'ont qu'une seule fonctionnalité, telle qu'un webhook, tandis que d'autres disposent de plusieurs fonctionnalités pour offrir aux utilisateurs différentes options.</span><span class="sxs-lookup"><span data-stu-id="190a1-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="190a1-109">Par exemple, votre application peut afficher des données  dans un emplacement central, autrement dit, l'onglet et présenter ces mêmes informations via une interface de conversation, autrement dit, le **bot**.</span><span class="sxs-lookup"><span data-stu-id="190a1-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="190a1-110">Fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="190a1-110">App capabilities</span></span>

<span data-ttu-id="190a1-111">Votre application Teams a une ou toutes les fonctionnalités principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="190a1-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="190a1-112">Onglets</span><span class="sxs-lookup"><span data-stu-id="190a1-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="190a1-113">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="190a1-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="190a1-114">Bots</span><span class="sxs-lookup"><span data-stu-id="190a1-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="190a1-115">Webhooks et connecteurs</span><span class="sxs-lookup"><span data-stu-id="190a1-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="190a1-116">Votre application peut également tirer parti des fonctionnalités avancées, telles que [l'API Microsoft Graph pour Teams.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="190a1-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="190a1-117">L'illustration suivante vous donne une idée des fonctionnalités qui fourniront les fonctionnalités que vous souhaitez dans votre application.</span><span class="sxs-lookup"><span data-stu-id="190a1-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Carte d'esprit illustrant les fonctionnalités de l'application Teams.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="190a1-119">Toujours prendre en compte votre utilisateur</span><span class="sxs-lookup"><span data-stu-id="190a1-119">Always consider your user</span></span>

<span data-ttu-id="190a1-120">Lorsque vous vous familiarisez avec le développement d'applications Teams, vous comprenez ses principes de base.</span><span class="sxs-lookup"><span data-stu-id="190a1-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="190a1-121">Vous comprenez qu'il existe plusieurs façons de créer certaines fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="190a1-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="190a1-122">Dans de tels scénarios, réfléchissez à la façon dont vous pouvez offrir une expérience plus native à votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="190a1-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="190a1-123">Par exemple, vous pouvez collecter les entrées utilisateur dans un formulaire créé sous la forme d'un onglet dans l'application.</span><span class="sxs-lookup"><span data-stu-id="190a1-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="190a1-124">Vous pouvez également le faire à l'aide d'un module de tâche sans changer d'affichage et perturber le flux de travail de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="190a1-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="190a1-125">Il est important de choisir des points d'extension qui fournissent le moins d'écart par rapport au flux de travail normal d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="190a1-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="190a1-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="190a1-126">See also</span></span>

- [<span data-ttu-id="190a1-127">Créer des applications pour Teams</span><span class="sxs-lookup"><span data-stu-id="190a1-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="190a1-128">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="190a1-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="190a1-129">Points d'entrée de l'application Teams</span><span class="sxs-lookup"><span data-stu-id="190a1-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
