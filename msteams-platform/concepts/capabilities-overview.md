---
title: Présentation des fonctionnalités des applications teams
author: heath-hamilton
description: Explications sur les fonctionnalités des applications teams
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210277"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="12a9a-103">Présentation des fonctionnalités des applications teams</span><span class="sxs-lookup"><span data-stu-id="12a9a-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="12a9a-104">Les *fonctionnalités* sont les points d’extension pour la création d’applications sur la plateforme Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="12a9a-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="12a9a-105">Il existe plusieurs façons d’étendre Teams, de sorte que chaque application est unique : une seule capacité (par exemple, un webhook), tandis que d’autres ont quelques possibilités pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="12a9a-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="12a9a-106">Par exemple, votre application peut afficher les données dans un emplacement central (onglet) et présenter ces mêmes informations par le biais d’une interface de conversation (bot).</span><span class="sxs-lookup"><span data-stu-id="12a9a-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="12a9a-107">Votre application teams peut avoir une ou toutes les fonctionnalités de base suivantes :</span><span class="sxs-lookup"><span data-stu-id="12a9a-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="12a9a-108">Onglets</span><span class="sxs-lookup"><span data-stu-id="12a9a-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="12a9a-109">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="12a9a-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="12a9a-110">Bots</span><span class="sxs-lookup"><span data-stu-id="12a9a-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="12a9a-111">Webhooks et connecteurs</span><span class="sxs-lookup"><span data-stu-id="12a9a-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="12a9a-112">Votre application peut également tirer parti de fonctionnalités avancées, telles que l' [API Microsoft Graph pour teams](https://docs.microsoft.com/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="12a9a-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="12a9a-113">Reportez-vous à l’illustration suivante pour obtenir une idée des fonctionnalités qui fourniraient les fonctionnalités souhaitées dans votre application.</span><span class="sxs-lookup"><span data-stu-id="12a9a-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Diagramme d’idées illustrant les fonctionnalités des applications Teams.":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="12a9a-115">Faire ce qui convient le mieux pour vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="12a9a-115">Doing what's best for your users</span></span>

<span data-ttu-id="12a9a-116">Lorsque vous vous familiarisez avec le développement d’applications Teams, vous commencerez à comprendre ses subtilités.</span><span class="sxs-lookup"><span data-stu-id="12a9a-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="12a9a-117">Il existe plusieurs façons de créer certaines fonctionnalités (par exemple, la collecte des données entrées par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="12a9a-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="12a9a-118">Par exemple, vous pouvez incorporer un formulaire Web dans un onglet à l’aide d’un `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="12a9a-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="12a9a-119">Vous pouvez également effectuer cette opération dans un onglet à l’aide d’un module de tâches, une convention de l’interface utilisateur Teams, pour une expérience plus Native que vos utilisateurs préféreront.</span><span class="sxs-lookup"><span data-stu-id="12a9a-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="12a9a-120">Le choix des fonctionnalités et de la conception appropriées ne revient pas à [comprendre les cas d’utilisation de votre public](../concepts/design/understand-use-cases.md).</span><span class="sxs-lookup"><span data-stu-id="12a9a-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
