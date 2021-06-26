---
title: Concevoir votre application - Comprendre la structure de l’application
description: Comprenez ce que vous pouvez et ne pouvez pas personnaliser Microsoft Teams lors de la conception de votre application.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a574ebeb5416e614152bb24d52cc798f0032943c
ms.sourcegitcommit: 0fe60b3fd406a5768b18977df53d1f4c665e5300
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53133392"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="08de9-103">Comprendre la structure Microsoft Teams’application</span><span class="sxs-lookup"><span data-stu-id="08de9-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="08de9-104">Lors de la création de votre application, il est important de savoir ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="08de9-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="08de9-105">Ces informations peuvent vous aider à mieux comprendre les parties de l’expérience d’application que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="08de9-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="08de9-106">Les images filaire suivantes vous montrent :</span><span class="sxs-lookup"><span data-stu-id="08de9-106">The following wireframes show you:</span></span>

* <span data-ttu-id="08de9-107">Surfaces que vous pouvez personnaliser dans chaque Teams d’application (en rose).</span><span class="sxs-lookup"><span data-stu-id="08de9-107">The surfaces you can customize in each Teams app capability (outlined in pink).</span></span>
* <span data-ttu-id="08de9-108">Étendues que chaque fonctionnalité prend en charge.</span><span class="sxs-lookup"><span data-stu-id="08de9-108">The scopes each capability supports.</span></span>

> [!TIP]
> <span data-ttu-id="08de9-109">**Que signifie l’étendue ?**</span><span class="sxs-lookup"><span data-stu-id="08de9-109">**What does scope mean?**</span></span> <span data-ttu-id="08de9-110">Une étendue est un domaine dans Teams où les personnes peuvent utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="08de9-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="08de9-111">Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, des canaux, des conversations et des réunions.</span><span class="sxs-lookup"><span data-stu-id="08de9-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="08de9-112">Applications personnelles</span><span class="sxs-lookup"><span data-stu-id="08de9-112">Personal apps</span></span>

<span data-ttu-id="08de9-113">Les applications personnelles fournissent une grande zone de dessin pour héberger le contenu de votre application pour des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="08de9-113">Personal apps provide a large canvas to host your app content for individual users.</span></span>

<span data-ttu-id="08de9-114">\***Étendues pris en charge**: Personnel\*</span><span class="sxs-lookup"><span data-stu-id="08de9-114">\***Supported scopes**: Personal\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="08de9-115">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="08de9-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="08de9-116">La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.</span><span class="sxs-lookup"><span data-stu-id="08de9-116">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="08de9-118">Mobile</span><span class="sxs-lookup"><span data-stu-id="08de9-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="08de9-119">La zone de dessin est une vue web pour vous aider à personnaliser entièrement l’expérience.</span><span class="sxs-lookup"><span data-stu-id="08de9-119">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur mobile." border="false":::

---

## <a name="tabs"></a><span data-ttu-id="08de9-121">Onglets</span><span class="sxs-lookup"><span data-stu-id="08de9-121">Tabs</span></span>

<span data-ttu-id="08de9-122">Les onglets fournissent une grande zone de dessin pour héberger le contenu de votre application pour un groupe d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="08de9-122">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="08de9-123">Vous pouvez inclure des onglets dans des espaces partagés tels que des canaux, des conversations et des invitations à des réunions.</span><span class="sxs-lookup"><span data-stu-id="08de9-123">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span>

<span data-ttu-id="08de9-124">\***Étendues pris en charge**: Canaux, Conversations, Réunions\*</span><span class="sxs-lookup"><span data-stu-id="08de9-124">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="08de9-125">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="08de9-125">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="08de9-126">La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.</span><span class="sxs-lookup"><span data-stu-id="08de9-126">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="08de9-128">Mobile</span><span class="sxs-lookup"><span data-stu-id="08de9-128">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="08de9-129">La zone de dessin est une vue web pour vous aider à personnaliser entièrement l’expérience.</span><span class="sxs-lookup"><span data-stu-id="08de9-129">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets sur appareils mobiles." border="false":::

---

## <a name="bots"></a><span data-ttu-id="08de9-131">Bots</span><span class="sxs-lookup"><span data-stu-id="08de9-131">Bots</span></span>

<span data-ttu-id="08de9-132">Les bots sont des applications conversationnelles qui s’intègrent Teams fonctionnalités de messagerie native, de sorte que le travail de l’interface utilisateur est géré pour vous.</span><span class="sxs-lookup"><span data-stu-id="08de9-132">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="08de9-133">Du point de vue de la conception, il est toujours possible d’ajouter de la personnalité, des fonctionnalités personnalisées et des informations riches et actionnables avec notre prise en charge du traitement du langage naturel (NLP) et la plateforme de cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="08de9-133">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="08de9-134">\***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions\*</span><span class="sxs-lookup"><span data-stu-id="08de9-134">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="08de9-135">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="08de9-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="08de9-137">Mobile</span><span class="sxs-lookup"><span data-stu-id="08de9-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur mobile." border="false":::

---

## <a name="messaging-extensions"></a><span data-ttu-id="08de9-139">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="08de9-139">Messaging extensions</span></span>

<span data-ttu-id="08de9-140">Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou agir sur un message sans quitter la conversation.</span><span class="sxs-lookup"><span data-stu-id="08de9-140">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="08de9-141">Les extensions de messagerie basées sur l’action vous donnent davantage de contrôle sur l’expérience, tandis que Teams gère la plupart des rendus des extensions de messagerie basées sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="08de9-141">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="08de9-142">\***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions\*</span><span class="sxs-lookup"><span data-stu-id="08de9-142">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="08de9-143">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="08de9-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de messagerie sur ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="08de9-145">Mobile</span><span class="sxs-lookup"><span data-stu-id="08de9-145">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de messagerie sur mobile." border="false":::

---

## <a name="meeting-extensions"></a><span data-ttu-id="08de9-147">Extensions de réunion</span><span class="sxs-lookup"><span data-stu-id="08de9-147">Meeting extensions</span></span>

<span data-ttu-id="08de9-148">Les extensions de réunion sont des applications pour améliorer les réunions en direct.</span><span class="sxs-lookup"><span data-stu-id="08de9-148">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="08de9-149">Vous pouvez héberger le contenu de votre application dans plusieurs scénarios, notamment avant, pendant et après les réunions.</span><span class="sxs-lookup"><span data-stu-id="08de9-149">You can host your app content in several scenarios, including before, during, and after meetings.</span></span>

<span data-ttu-id="08de9-150">\***Étendues prise en charge**: réunions, conversations\*</span><span class="sxs-lookup"><span data-stu-id="08de9-150">\***Supported scopes**: Meetings, Chats\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="08de9-151">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="08de9-151">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="08de9-152">La surface est un iframe qui vous permet de personnaliser l’expérience, mais n’oubliez pas que pendant les réunions, ces applications utilisent un thème foncé et sont étroites.</span><span class="sxs-lookup"><span data-stu-id="08de9-152">The surface is an iframe, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme and are narrow.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur ordinateur de bureau." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="08de9-154">Mobile</span><span class="sxs-lookup"><span data-stu-id="08de9-154">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="08de9-155">La surface est une vue web, qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que pendant les réunions, ces applications utilisent un thème foncé.</span><span class="sxs-lookup"><span data-stu-id="08de9-155">The surface is a webview, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur mobile." border="false":::

---
