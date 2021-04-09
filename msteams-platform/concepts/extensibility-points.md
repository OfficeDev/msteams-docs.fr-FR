---
title: Points d’entrée pour les applications Teams
author: heath-hamilton
description: Décrit l’endroit où les personnes peuvent découvrir et utiliser votre application dans Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713626"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="787fa-103">Points d’entrée pour les applications Teams</span><span class="sxs-lookup"><span data-stu-id="787fa-103">Entry points for Teams apps</span></span>

<span data-ttu-id="787fa-104">La plateforme Teams offre un ensemble flexible de points d’entrée où les personnes peuvent découvrir et utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="787fa-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="787fa-105">Votre application peut être aussi simple que l'intégration d'un contenu web existant dans un onglet ou une application à plusieurs facettes avec laquelle les utilisateurs interagissent dans plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="787fa-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>

<span data-ttu-id="787fa-106">Les applications les plus efficaces semblent natives pour Teams. Il est donc important de planifier avec soin les points d’entrée de votre application.</span><span class="sxs-lookup"><span data-stu-id="787fa-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-chats"></a><span data-ttu-id="787fa-107">Équipes, canaux et conversations</span><span class="sxs-lookup"><span data-stu-id="787fa-107">Teams, channels, and chats</span></span>

<span data-ttu-id="787fa-108">Les équipes, canaux et conversations sont des espaces de collaboration.</span><span class="sxs-lookup"><span data-stu-id="787fa-108">Teams, channels, and chats are collaboration spaces.</span></span> <span data-ttu-id="787fa-109">Dans ces contextes, les applications sont disponibles pour tous les utilisateurs de cet espace. Elles se concentrent généralement sur des flux de travail supplémentaires ou déverrouillent de nouvelles interactions sociales.</span><span class="sxs-lookup"><span data-stu-id="787fa-109">Apps in these contexts are available to everyone in that space and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="787fa-110">Voici comment les fonctionnalités d’application Teams sont couramment utilisées dans des contextes de collaboration :</span><span class="sxs-lookup"><span data-stu-id="787fa-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="787fa-111">[**Les onglets**](~/tabs/what-are-tabs.md) offrent une expérience web intégrée en plein écran configurée pour l’équipe, le canal ou la conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="787fa-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="787fa-112">Tous les membres interagissent avec le même contenu web, de sorte qu’une expérience d’application de page unique sans état est classique.</span><span class="sxs-lookup"><span data-stu-id="787fa-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="787fa-113">[**Les extensions de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md) sont des raccourcis permettant d'insérer du contenu externe dans une conversation ou de prendre des mesures concernant les messages sans quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="787fa-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="787fa-114">Le déploiement de liens fournit un contenu riche lors du partage de contenu à partir d'une URL commune.</span><span class="sxs-lookup"><span data-stu-id="787fa-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="787fa-115">[**Les bots**](~/bots/what-are-bots.md) interagissent avec les membres de la conversation via une conversation instantanée et répondent à des événements (comme l’ajout d’un nouveau membre ou la modification de nom d’un canal).</span><span class="sxs-lookup"><span data-stu-id="787fa-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="787fa-116">Les conversations avec un bot dans ces contextes sont visibles par tous les membres de l’équipe, du canal ou du groupe. Les conversations bot doivent donc être pertinentes pour tout le monde.</span><span class="sxs-lookup"><span data-stu-id="787fa-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="787fa-117">[**Les webhooks et connecteurs**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettent à un service externe de publier des messages dans une conversation et aux utilisateurs d’envoyer des messages à un service.</span><span class="sxs-lookup"><span data-stu-id="787fa-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="787fa-118">[**L’API REST Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) pour obtenir des données sur les équipes, les canaux et les conversations de groupe pour automatiser et gérer les processus Teams.</span><span class="sxs-lookup"><span data-stu-id="787fa-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="787fa-119">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="787fa-119">Personal apps</span></span>

<span data-ttu-id="787fa-120">[Les applications personnelles](~/concepts/design/personal-apps.md) sont la partie de votre application Teams qui se concentre sur les communications avec un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="787fa-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="787fa-121">L’expérience dans ce contexte est propre à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="787fa-121">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="787fa-122">Voici comment les fonctionnalités Teams sont couramment utilisées dans des contextes personnels :</span><span class="sxs-lookup"><span data-stu-id="787fa-122">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="787fa-123">[**Les bots**](~/bots/what-are-bots.md) ont des conversations à deux avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="787fa-123">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="787fa-124">Les bots qui nécessitent des conversations à plusieurs tours ou qui fournissent des notifications pertinentes uniquement pour un utilisateur spécifique sont mieux adaptés aux applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="787fa-124">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="787fa-125">[**Les onglets**](~/tabs/what-are-tabs.md) fournissent une expérience web incorporée en plein écran qui a du sens pour l’utilisateur qui la regarde.</span><span class="sxs-lookup"><span data-stu-id="787fa-125">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to the user looking at it.</span></span>

## <a name="examples"></a><span data-ttu-id="787fa-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="787fa-126">Examples</span></span>

<span data-ttu-id="787fa-127">Les instructions de conception de l’application Teams fournissent des visuels détaillés qui vous montrent où les personnes peuvent trouver et utiliser les applications Teams.</span><span class="sxs-lookup"><span data-stu-id="787fa-127">The Teams app design guidelines provide detailed visuals showing you where people can find and use Teams apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="787fa-128">Consultez les instructions de conception de l’application Teams</span><span class="sxs-lookup"><span data-stu-id="787fa-128">See the Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)
