---
title: Comprendre les fonctionnalités de l’application Teams
author: heath-hamilton
description: Fonctionnalités de l’application Teams expliquées
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034704"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="be740-103">Comprendre les fonctionnalités de l’application Teams</span><span class="sxs-lookup"><span data-stu-id="be740-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="be740-104">*Les fonctionnalités sont* les points d’extension pour la création d’applications sur la plateforme Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="be740-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="be740-105">Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique : certaines n’ont qu’une seule fonctionnalité (par exemple, un webhook), tandis que d’autres ont quelques-unes pour donner des options aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="be740-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="be740-106">Par exemple, votre application peut afficher des données dans un emplacement central (onglet) et présenter ces mêmes informations via une interface de conversation (bot).</span><span class="sxs-lookup"><span data-stu-id="be740-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="be740-107">Votre application Teams a une ou toutes les fonctionnalités principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="be740-107">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="be740-108">Onglets</span><span class="sxs-lookup"><span data-stu-id="be740-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="be740-109">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="be740-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="be740-110">Bots</span><span class="sxs-lookup"><span data-stu-id="be740-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="be740-111">Webhooks et connecteurs</span><span class="sxs-lookup"><span data-stu-id="be740-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="be740-112">Votre application peut également tirer parti des fonctionnalités avancées, telles que [l’API Microsoft Graph pour Teams.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="be740-112">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="be740-113">Consultez l’illustration suivante pour vous faire une idée des fonctionnalités qui offriraient les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="be740-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Carte d’esprit illustrant les fonctionnalités de l’application Teams.":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="be740-115">Faire ce qui est le mieux pour vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="be740-115">Doing what's best for your users</span></span>

<span data-ttu-id="be740-116">À mesure que vous vous familiariserez avec le développement d’applications Teams, vous commencerez à comprendre ses subtiles.</span><span class="sxs-lookup"><span data-stu-id="be740-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="be740-117">Il existe plusieurs façons de créer certaines fonctionnalités (telles que la collecte d’entrées utilisateur).</span><span class="sxs-lookup"><span data-stu-id="be740-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="be740-118">Par exemple, vous pouvez incorporer un formulaire web dans un onglet à l’aide d’un `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="be740-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="be740-119">Vous pouvez également le faire dans un onglet à l’aide d’un module de tâche, une convention d’interface utilisateur Teams, pour une expérience plus native que vos utilisateurs préfèrent.</span><span class="sxs-lookup"><span data-stu-id="be740-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="be740-120">Le choix des fonctionnalités et de la conception qui vous sont nécessaires revient à comprendre d’abord les cas [d’utilisation de votre public.](../concepts/design/understand-use-cases.md)</span><span class="sxs-lookup"><span data-stu-id="be740-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
