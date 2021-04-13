---
title: Points d’entrée pour les applications Teams
author: heath-hamilton
description: Décrit l’endroit où les personnes peuvent découvrir et utiliser votre application dans Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f61e5b5c05855c0a3a766920095cf46f699f08a6
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654355"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="844bc-103">Points d’entrée pour les applications Teams</span><span class="sxs-lookup"><span data-stu-id="844bc-103">Entry points for Teams apps</span></span>

<span data-ttu-id="844bc-104">La plateforme Teams fournit un ensemble flexible de points d’entrée, tels que l’équipe, le canal et la conversation, où les personnes peuvent découvrir et utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="844bc-104">The Teams platform provides a flexible set of entry points, such as team, channel, and chat where people can discover and use your app.</span></span> <span data-ttu-id="844bc-105">Votre application peut être aussi simple que l'intégration d'un contenu web existant dans un onglet ou une application à plusieurs facettes avec laquelle les utilisateurs interagissent dans plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="844bc-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>
<span data-ttu-id="844bc-106">Les applications les plus réussies sont natives de Teams. Choisissez donc soigneusement les points d’entrée de votre application.</span><span class="sxs-lookup"><span data-stu-id="844bc-106">The most successful apps are native to Teams, so choose your app's entry points carefully.</span></span>

## <a name="shared-app-experiences"></a><span data-ttu-id="844bc-107">Expériences d’application partagées</span><span class="sxs-lookup"><span data-stu-id="844bc-107">Shared app experiences</span></span>

<span data-ttu-id="844bc-108">Les équipes, les canaux et les discussions sont des espaces de collaboration.</span><span class="sxs-lookup"><span data-stu-id="844bc-108">Team, channel, and chat are collaboration spaces.</span></span> <span data-ttu-id="844bc-109">Les applications dans ces contextes sont disponibles pour tout le monde dans cet espace.</span><span class="sxs-lookup"><span data-stu-id="844bc-109">Apps in these contexts are available to everyone in that space.</span></span> <span data-ttu-id="844bc-110">Les espaces de collaboration se concentrent généralement sur des flux de travail supplémentaires ou sur le déverrouillage de nouvelles interactions sociales.</span><span class="sxs-lookup"><span data-stu-id="844bc-110">Collaboration spaces typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="844bc-111">La liste suivante montre comment les fonctionnalités d’application Teams sont couramment utilisées dans des contextes de collaboration :</span><span class="sxs-lookup"><span data-stu-id="844bc-111">The following list shows how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="844bc-112">[**Les onglets**](~/tabs/what-are-tabs.md) offrent une expérience web intégrée en plein écran configurée pour l’équipe, le canal ou la conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="844bc-112">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="844bc-113">Tous les membres interagissent avec le même contenu web, de sorte qu’une expérience d’application mono-page sans état est typique.</span><span class="sxs-lookup"><span data-stu-id="844bc-113">All members interact with the same web-based content, so a stateless single-page app experience is typical.</span></span>

* <span data-ttu-id="844bc-114">[**Les extensions de messagerie**](~/messaging-extensions/what-are-messaging-extensions.md) sont des raccourcis permettant d'insérer du contenu externe dans une conversation ou de prendre des mesures concernant les messages sans quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="844bc-114">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="844bc-115">[Le déploiement de liens](~/messaging-extensions/how-to/link-unfurling.md) fournit un contenu enrichi lors du partage de contenu à partir d’une URL commune.</span><span class="sxs-lookup"><span data-stu-id="844bc-115">[Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="844bc-116">Les bots interagissent avec les membres de la conversation par le biais d’une conversation et de la réponse à des [**événements,**](~/bots/what-are-bots.md) tels que l’ajout d’un nouveau membre ou le changement de nom d’un canal.</span><span class="sxs-lookup"><span data-stu-id="844bc-116">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events, such as adding a new member or renaming a channel.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="844bc-117">Les conversations avec un bot dans ces contextes sont visibles par tous les membres de l’équipe, du canal ou du groupe, de sorte que les conversations de bot doivent être pertinentes pour tout le monde.</span><span class="sxs-lookup"><span data-stu-id="844bc-117">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations must be relevant to everyone.</span></span>

* <span data-ttu-id="844bc-118">[**Les webhooks et connecteurs**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permettent à un service externe de publier des messages dans une conversation et aux utilisateurs d’envoyer des messages à un service.</span><span class="sxs-lookup"><span data-stu-id="844bc-118">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="844bc-119">[**L’API REST Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) pour obtenir des données sur les équipes, les canaux et les conversations de groupe pour automatiser et gérer les processus Teams.</span><span class="sxs-lookup"><span data-stu-id="844bc-119">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-app-experiences"></a><span data-ttu-id="844bc-120">Expériences d’application personnelles</span><span class="sxs-lookup"><span data-stu-id="844bc-120">Personal app experiences</span></span>

<span data-ttu-id="844bc-121">[Les applications personnelles](../concepts/design/personal-apps.md) sont la partie de votre application Teams qui se concentre sur les communications avec un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="844bc-121">[Personal apps](../concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="844bc-122">L’expérience dans ce contexte est propre à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="844bc-122">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="844bc-123">La liste suivante montre comment les fonctionnalités teams sont couramment utilisées dans les contextes personnels :</span><span class="sxs-lookup"><span data-stu-id="844bc-123">The following list shows how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="844bc-124">[**Les bots**](~/bots/what-are-bots.md) ont des conversations à deux avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="844bc-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="844bc-125">Les bots qui nécessitent des conversations à plusieurs tours ou qui fournissent des notifications pertinentes uniquement pour un utilisateur spécifique sont mieux adaptés aux applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="844bc-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="844bc-126">[**Les onglets**](~/tabs/what-are-tabs.md) offrent une expérience web incorporée plein écran qui est significative pour l’utilisateur qui la regarde.</span><span class="sxs-lookup"><span data-stu-id="844bc-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that is meaningful to the user looking at it.</span></span>

## <a name="see-also"></a><span data-ttu-id="844bc-127">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="844bc-127">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="844bc-128">Recommandations en matière de conception d’applications Teams</span><span class="sxs-lookup"><span data-stu-id="844bc-128">Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="844bc-129">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="844bc-129">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="844bc-130">Comprendre les cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="844bc-130">Understand use cases</span></span>](../concepts/design/understand-use-cases.md)
