---
title: Présentation des fonctionnalités des applications teams
author: heath-hamilton
description: vue d’ensemble des fonctionnalités de teams et des points d’extension
ms.topic: overview
ms.author: v-heha
ms.openlocfilehash: f83cf0240b32d35028135b48e7d4c56b939777a9
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819080"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="9af39-103">Présentation des fonctionnalités des applications teams</span><span class="sxs-lookup"><span data-stu-id="9af39-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="9af39-104">Les *fonctionnalités* sont les points d’extension pour la création d’applications sur la plateforme Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9af39-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="9af39-105">Il existe plusieurs façons d’étendre le client teams : toutes les applications sont uniques : une seule capacité (par exemple, un webhook), tandis que d’autres ont quelques possibilités pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9af39-105">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="9af39-106">Par exemple, votre application peut afficher les données dans un emplacement central (onglet) et présenter ces mêmes informations par le biais d’une interface de conversation (bot).</span><span class="sxs-lookup"><span data-stu-id="9af39-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="9af39-107">Votre application teams peut avoir une ou toutes les fonctionnalités de base suivantes :</span><span class="sxs-lookup"><span data-stu-id="9af39-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="9af39-108">Onglets</span><span class="sxs-lookup"><span data-stu-id="9af39-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="9af39-109">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="9af39-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="9af39-110">Webhooks et connecteurs</span><span class="sxs-lookup"><span data-stu-id="9af39-110">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="9af39-111">Bots</span><span class="sxs-lookup"><span data-stu-id="9af39-111">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="9af39-112">Votre application peut également tirer parti de fonctionnalités avancées, telles que l' [API REST Microsoft Graph](../graph-api/rsc/resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="9af39-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="9af39-113">Reportez-vous à l’illustration suivante pour obtenir une idée des fonctionnalités qui fourniraient les fonctionnalités souhaitées dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9af39-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Diagramme d’idées illustrant les fonctionnalités des applications teams](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="9af39-115">Faire ce qui convient le mieux pour vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9af39-115">Doing what's best for your users</span></span>

<span data-ttu-id="9af39-116">Lorsque vous vous familiarisez avec le développement d’applications Teams, vous commencerez à comprendre ses subtilités.</span><span class="sxs-lookup"><span data-stu-id="9af39-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="9af39-117">Il existe plusieurs façons de créer certaines fonctionnalités (par exemple, la collecte des données entrées par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="9af39-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="9af39-118">Par exemple, vous pouvez incorporer un formulaire Web dans un onglet à l’aide d’un `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="9af39-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="9af39-119">Vous pouvez également effectuer cette opération dans un onglet à l’aide d’un module de tâches, une convention de l’interface utilisateur Teams, pour une expérience plus Native que vos utilisateurs préféreront.</span><span class="sxs-lookup"><span data-stu-id="9af39-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="9af39-120">Le choix de la combinaison appropriée de fonctionnalités et de conventions de l’interface utilisateur, des contrôles et des éléments ne revient pas à [comprendre les cas d’utilisation de votre audience](../concepts/design/understand-use-cases.md).</span><span class="sxs-lookup"><span data-stu-id="9af39-120">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="9af39-121">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="9af39-121">Learn more</span></span>

* [<span data-ttu-id="9af39-122">Démarrer la planification de votre application</span><span class="sxs-lookup"><span data-stu-id="9af39-122">Start planning your app</span></span>](../concepts/extensibility-points.md)
