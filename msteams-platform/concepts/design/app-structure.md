---
title: Concevoir votre application - Comprendre la structure de l’application
description: Comprenez ce que vous pouvez et ne pouvez pas personnaliser Microsoft Teams lors de la conception de votre application.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631309"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="bb8b4-103">Comprendre la structure Microsoft Teams’application</span><span class="sxs-lookup"><span data-stu-id="bb8b4-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="bb8b4-104">Lors de la création de votre application, il est important de savoir ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="bb8b4-105">Ces informations peuvent vous aider à mieux comprendre les parties de l’expérience d’application que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="bb8b4-106">Les images filaire suivantes vous montrent :</span><span class="sxs-lookup"><span data-stu-id="bb8b4-106">The following wireframes show you:</span></span>

* <span data-ttu-id="bb8b4-107">Surfaces que vous pouvez personnaliser dans chaque Teams d’application (en bleu).</span><span class="sxs-lookup"><span data-stu-id="bb8b4-107">The surfaces you can customize in each Teams app capability (outlined in blue).</span></span>
* <span data-ttu-id="bb8b4-108">Étendues que chaque fonctionnalité prend en charge.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-108">The scopes each capability supports.</span></span>

> [!NOTE]
> <span data-ttu-id="bb8b4-109">**Que signifie l’étendue ?**</span><span class="sxs-lookup"><span data-stu-id="bb8b4-109">**What does scope mean?**</span></span> <span data-ttu-id="bb8b4-110">Une étendue est une zone de Teams où les personnes peuvent utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="bb8b4-111">Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, des canaux, des conversations et des réunions.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="bb8b4-112">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="bb8b4-112">Personal apps</span></span>

<span data-ttu-id="bb8b4-113">Les applications personnelles fournissent une grande zone de dessin pour héberger le contenu de votre application pour des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-113">Personal apps provide a large canvas to host your app content for individual users.</span></span> <span data-ttu-id="bb8b4-114">La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-114">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="bb8b4-115">\***Étendues pris en charge**: Personnel\*</span><span class="sxs-lookup"><span data-stu-id="bb8b4-115">\***Supported scopes**: Personal\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles." border="false":::

## <a name="tabs"></a><span data-ttu-id="bb8b4-117">Onglets</span><span class="sxs-lookup"><span data-stu-id="bb8b4-117">Tabs</span></span>

<span data-ttu-id="bb8b4-118">Les onglets fournissent une grande zone de dessin pour héberger le contenu de votre application pour un groupe d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-118">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="bb8b4-119">Vous pouvez inclure des onglets dans des espaces partagés tels que des canaux, des conversations et des invitations à des réunions.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-119">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span> <span data-ttu-id="bb8b4-120">La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-120">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="bb8b4-121">\***Étendues pris en charge**: Canaux, Conversations, Réunions\*</span><span class="sxs-lookup"><span data-stu-id="bb8b4-121">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets." border="false":::

## <a name="bots"></a><span data-ttu-id="bb8b4-123">Bots</span><span class="sxs-lookup"><span data-stu-id="bb8b4-123">Bots</span></span>

<span data-ttu-id="bb8b4-124">Les bots sont des applications conversationnelles qui s’intègrent Teams fonctionnalités de messagerie native, de sorte que le travail de l’interface utilisateur est géré pour vous.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-124">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="bb8b4-125">Du point de vue de la conception, il est toujours possible d’ajouter de la personnalité, des fonctionnalités personnalisées et des informations riches et actionnables avec notre prise en charge du traitement du langage naturel (NLP) et la plateforme de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-125">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="bb8b4-126">\***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions\*</span><span class="sxs-lookup"><span data-stu-id="bb8b4-126">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots." border="false":::

## <a name="messaging-extensions"></a><span data-ttu-id="bb8b4-128">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="bb8b4-128">Messaging extensions</span></span>

<span data-ttu-id="bb8b4-129">Les extensions de messagerie sont des raccourcis pour insérer du contenu d’application ou agir sur un message sans sortir de la conversation.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-129">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="bb8b4-130">Les extensions de messagerie basées sur l’action vous donnent davantage de contrôle sur l’expérience, tandis que Teams gère la plupart des rendus des extensions de messagerie basées sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-130">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="bb8b4-131">\***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions\*</span><span class="sxs-lookup"><span data-stu-id="bb8b4-131">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de messagerie." border="false":::

## <a name="meeting-extensions"></a><span data-ttu-id="bb8b4-133">Extensions de réunion</span><span class="sxs-lookup"><span data-stu-id="bb8b4-133">Meeting extensions</span></span>

<span data-ttu-id="bb8b4-134">Les extensions de réunion sont des applications pour améliorer les réunions en direct.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-134">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="bb8b4-135">Vous pouvez héberger le contenu de votre application dans plusieurs scénarios, notamment avant, pendant et après les réunions.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-135">You can host your app content in several scenarios, including before, during, and after meetings.</span></span> <span data-ttu-id="bb8b4-136">La surface est un iframe qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que ces applications sont sombres et étroites pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="bb8b4-136">The surface is an iframe, allowing you to customize the experience, but keep in mind that these apps are dark themed and narrow during meetings.</span></span>

<span data-ttu-id="bb8b4-137">\***Étendues pris en charge**: réunions, conversations\*</span><span class="sxs-lookup"><span data-stu-id="bb8b4-137">\***Supported scopes**: Meetings, Chats\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion." border="false":::
