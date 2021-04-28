---
title: Bots dans Microsoft Teams
author: clearab
description: Vue d'ensemble des bots dans Microsoft Teams.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 9ba7b6b96a8cbd55fac968975794d7c41d57f514
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058494"
---
# <a name="bots-in-microsoft-teams"></a><span data-ttu-id="62ec1-103">Bots dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="62ec1-103">Bots in Microsoft Teams</span></span>

<span data-ttu-id="62ec1-104">Un bot également appelé bot de conversation est une application qui exécute des tâches automatisées simples et répétitives effectuées par les utilisateurs, telles que le service clientèle ou le personnel de support technique.</span><span class="sxs-lookup"><span data-stu-id="62ec1-104">A bot also referred to as a chatbot or conversational bot is an app that runs simple and repetitive automated tasks performed by the users, such as customer service or support staff.</span></span> <span data-ttu-id="62ec1-105">Parmi les exemples de bots utilisés quotidiennement, citons les bots qui fournissent des informations sur la météo, qui réservent des réservations de réservations ou qui fournissent des informations de voyage.</span><span class="sxs-lookup"><span data-stu-id="62ec1-105">Examples of bots in everyday use include, bots that provide information about the weather, make dinner reservations, or provide travel information.</span></span> <span data-ttu-id="62ec1-106">Une interaction de bot peut être une question et une réponse rapides, ou il peut s'agit d'une conversation complexe qui permet d'accéder aux services.</span><span class="sxs-lookup"><span data-stu-id="62ec1-106">A bot interaction can be a quick question and answer, or it can be a complex conversation that provides access to services.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

<span data-ttu-id="62ec1-107">Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâches.</span><span class="sxs-lookup"><span data-stu-id="62ec1-107">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span>

![Appeler un bot à l'aide de texte](~/assets/images/invokebotwithtext.png)

![Appeler un bot à l'aide d'une carte](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

<span data-ttu-id="62ec1-110">Les bots de conversation sont extrêmement flexibles et peuvent être étendues pour gérer quelques commandes simples ou des tâches complexes, optimisées pour l'intelligence artificielle et de traitement du langage naturel.</span><span class="sxs-lookup"><span data-stu-id="62ec1-110">Conversational bots are incredibly flexible and can be scoped to handle a few simple commands, or complex, artificial-intelligence-powered, and natural-language-processing tasks.</span></span> <span data-ttu-id="62ec1-111">Ils peuvent être un aspect d'une application plus grande ou être entièrement autonomes.</span><span class="sxs-lookup"><span data-stu-id="62ec1-111">They can be one aspect of a larger application, or be completely stand-alone.</span></span>

<span data-ttu-id="62ec1-112">La recherche de la combinaison de cartes, de texte et de modules de tâche est essentielle pour créer un bot utile.</span><span class="sxs-lookup"><span data-stu-id="62ec1-112">Finding the right mix of cards, text, and task modules are key to create a useful bot.</span></span> <span data-ttu-id="62ec1-113">L'image suivante montre un utilisateur qui discute avec un bot dans une conversation un-à-un à l'aide de cartes texte et interactives :</span><span class="sxs-lookup"><span data-stu-id="62ec1-113">The following image shows a user conversing with a bot in a one-to-one chat using both, text and interactive cards:</span></span>

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Exemple de bot FAQ" border="true":::

<span data-ttu-id="62ec1-115">Chaque interaction entre l'utilisateur et le bot est représentée comme une activité.</span><span class="sxs-lookup"><span data-stu-id="62ec1-115">Every interaction between the user and the bot is represented as an activity.</span></span> <span data-ttu-id="62ec1-116">Lorsqu'un bot reçoit une activité, il la transmet à ses handlers d'activité.</span><span class="sxs-lookup"><span data-stu-id="62ec1-116">When a bot receives an activity, it passes it on to its activity handlers.</span></span> <span data-ttu-id="62ec1-117">Pour plus d'informations, voir [les handlers d'activité des bots.](~/bots/bot-basics.md)</span><span class="sxs-lookup"><span data-stu-id="62ec1-117">For more information, see [bot activity handlers](~/bots/bot-basics.md).</span></span> 

<span data-ttu-id="62ec1-118">En outre, les bots sont des applications qui ont une interface de conversation.</span><span class="sxs-lookup"><span data-stu-id="62ec1-118">In addition, bots are apps that have a conversational interface.</span></span> <span data-ttu-id="62ec1-119">Vous pouvez interagir avec un bot à l'aide de texte, de cartes interactives et de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="62ec1-119">You can interact with a bot using text, interactive cards, and speech.</span></span> <span data-ttu-id="62ec1-120">Un bot se comporte différemment selon qu'il s'agit d'une conversation de canal ou de groupe, ou d'une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="62ec1-120">A bot behaves differently depending on whether the conversation is a channel or group chat conversation, or it is a one-to-one conversation.</span></span> <span data-ttu-id="62ec1-121">Les conversations sont gérées via le connecteur Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="62ec1-121">Conversations are handled through the Bot Framework connector.</span></span> <span data-ttu-id="62ec1-122">Pour plus d'informations, voir [les informations de base de la conversation.](~/bots/how-to/conversations/conversation-basics.md)</span><span class="sxs-lookup"><span data-stu-id="62ec1-122">For more information, see [conversation basics](~/bots/how-to/conversations/conversation-basics.md).</span></span>

<span data-ttu-id="62ec1-123">Votre bot nécessite des informations contextuelles, telles que des détails de profil utilisateur pour accéder au contenu pertinent et améliorer l'expérience du bot.</span><span class="sxs-lookup"><span data-stu-id="62ec1-123">Your bot requires contextual information, such as user profile details to access relevant content and enhance the bot experience.</span></span> <span data-ttu-id="62ec1-124">Pour plus d'informations, voir [obtenir le contexte Teams.](~/bots/how-to/get-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="62ec1-124">For more information, see [get Teams context](~/bots/how-to/get-teams-context.md).</span></span> 

<span data-ttu-id="62ec1-125">Vous pouvez également envoyer et recevoir des fichiers via le bot à l'aide des API Graph ou des API de bot Teams.</span><span class="sxs-lookup"><span data-stu-id="62ec1-125">You can also send and receive files through the bot using Graph APIs or Teams bot APIs.</span></span> <span data-ttu-id="62ec1-126">Pour plus d'informations, voir [envoyer et recevoir des fichiers via le bot.](~/bots/how-to/bots-filesv4.md)</span><span class="sxs-lookup"><span data-stu-id="62ec1-126">For more information, see [send and receive files through the bot](~/bots/how-to/bots-filesv4.md).</span></span>

<span data-ttu-id="62ec1-127">En outre, la limitation des taux est utilisée pour optimiser les bots utilisés pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="62ec1-127">In addition, rate limiting is used to optimize bots used for your Teams application.</span></span> <span data-ttu-id="62ec1-128">Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="62ec1-128">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="62ec1-129">Pour plus d'informations, voir [optimiser votre bot avec une limite de taux dans Teams.](~/bots/how-to/rate-limit.md)</span><span class="sxs-lookup"><span data-stu-id="62ec1-129">For more information, see [optimize your bot with rate limiting in Teams](~/bots/how-to/rate-limit.md).</span></span>

<span data-ttu-id="62ec1-130">Avec les API Microsoft Graph pour les appels et les réunions en ligne, les applications Microsoft Teams peuvent désormais interagir avec les utilisateurs à l'aide de la voix et de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="62ec1-130">With Microsoft Graph APIs for calls and online meetings, Microsoft Teams apps can now interact with users using voice and video.</span></span> <span data-ttu-id="62ec1-131">Pour plus d'informations, voir [les bots d'appels et de réunions.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="62ec1-131">For more information, see [calls and meetings bots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span> 

<span data-ttu-id="62ec1-132">Vous pouvez utiliser les API de bot Teams pour obtenir des informations pour un ou plusieurs membres d'une conversation ou d'une équipe.</span><span class="sxs-lookup"><span data-stu-id="62ec1-132">You can use the Teams bot APIs to get information for one or more members of a chat or team.</span></span> <span data-ttu-id="62ec1-133">Pour plus d'informations, voir [les modifications apportées aux API de bot Teams](~/resources/team-chat-member-api-changes.md)pour récupérer des membres d'équipe ou de conversation.</span><span class="sxs-lookup"><span data-stu-id="62ec1-133">For more information, see [changes to Teams bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="62ec1-134">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="62ec1-134">See also</span></span>

- [<span data-ttu-id="62ec1-135">Créer un robot pour Teams</span><span class="sxs-lookup"><span data-stu-id="62ec1-135">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a><span data-ttu-id="62ec1-136">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="62ec1-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62ec1-137">Bots et kits de développement</span><span class="sxs-lookup"><span data-stu-id="62ec1-137">Bots and SDKs</span></span>](~/bots/bot-features.md)
