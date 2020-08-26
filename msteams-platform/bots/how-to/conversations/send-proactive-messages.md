---
title: Envoi de messages proactifs
author: clearab
description: Comment envoyer des messages proactifs avec votre robot Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874848"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="3afe2-103">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="3afe2-103">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="3afe2-104">Un message proactif est un message envoyé par un bot qui n’est pas en réponse directe à une demande d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3afe2-104">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="3afe2-105">Cela peut inclure des messages comme :</span><span class="sxs-lookup"><span data-stu-id="3afe2-105">This can include messages like:</span></span>

* <span data-ttu-id="3afe2-106">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="3afe2-106">Welcome messages</span></span>
* <span data-ttu-id="3afe2-107">Notifications</span><span class="sxs-lookup"><span data-stu-id="3afe2-107">Notifications</span></span>
* <span data-ttu-id="3afe2-108">Messages planifiés</span><span class="sxs-lookup"><span data-stu-id="3afe2-108">Scheduled messages</span></span>

<span data-ttu-id="3afe2-109">Pour que votre bot puisse envoyer un message proactif, il doit avoir accès à l’utilisateur, à la conversation de groupe ou à l’équipe à laquelle vous souhaitez envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="3afe2-109">In order for your bot to send a proactive message, it must have access to the user, group chat, or team that you wish to send the message to.</span></span> <span data-ttu-id="3afe2-110">Pour une conversation de groupe ou une équipe, cela signifie que l’application qui contient votre robot doit d’abord être installée à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="3afe2-110">For a group chat or team, this means the app that contains your bot must first be installed to that location.</span></span> <span data-ttu-id="3afe2-111">Vous pouvez [installer votre application de façon proactive en utilisant Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une [stratégie d’application](/microsoftteams/teams-custom-app-policies-and-settings) pour envoyer des applications à des équipes et des utilisateurs de votre client.</span><span class="sxs-lookup"><span data-stu-id="3afe2-111">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team if necessary, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="3afe2-112">Pour les utilisateurs, votre application doit être installée pour cet utilisateur ou votre utilisateur doit faire partie d’une équipe où votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="3afe2-112">For users, your app either needs to be installed for that user, or your user needs to be part of a team where your app is installed.</span></span>

<span data-ttu-id="3afe2-113">L’envoi d’un message proactif est différent de l’envoi d’un message standard dans lequel vous n’aurez pas `turnContext` à utiliser une réponse pour répondre.</span><span class="sxs-lookup"><span data-stu-id="3afe2-113">Sending a proactive message is different than sending a regular message in that you won't have an active `turnContext` to use for a reply.</span></span> <span data-ttu-id="3afe2-114">Vous devrez peut-être également créer la conversation (par exemple, une nouvelle conversation un-à-un ou un nouveau fil de conversation dans un canal) avant d’envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="3afe2-114">You may also need to create the conversation (for example a new one-to-one chat, or a new conversation thread in a channel) before sending the message.</span></span> <span data-ttu-id="3afe2-115">Vous ne pouvez pas créer une nouvelle conversation de groupe ou une nouvelle chaîne dans une équipe avec la messagerie proactive.</span><span class="sxs-lookup"><span data-stu-id="3afe2-115">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="3afe2-116">À un niveau élevé, les étapes que vous devez effectuer pour envoyer un message proactif sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3afe2-116">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="3afe2-117">[Obtenir l’ID d’utilisateur ou l’ID d’équipe/de canal](#get-the-user-id-or-teamchannel-id) (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="3afe2-117">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="3afe2-118">[Créez le thème conversation ou conversation](#create-the-conversation) (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="3afe2-118">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="3afe2-119">[Obtenir l’ID de conversation](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="3afe2-119">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="3afe2-120">[Envoyer le message](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="3afe2-120">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="3afe2-121">Les extraits de code dans la section [exemples](#examples) ci-dessous permettent de créer une conversation un-à-un, consultez la section [références](#references) pour obtenir des liens vers des exemples de travail complets pour les conversations et les groupes/canaux un-à-un.</span><span class="sxs-lookup"><span data-stu-id="3afe2-121">The code snippets in the [examples](#examples) section below are for creating a one-to-one conversation, see the [references](#references) section for links to complete working samples for both one-to-once conversations and group/channels.</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="3afe2-122">Obtenir l’ID d’utilisateur ou l’ID d’équipe/de canal</span><span class="sxs-lookup"><span data-stu-id="3afe2-122">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="3afe2-123">Si vous devez créer un nouveau thème de conversation ou de conversation dans un canal, vous aurez d’abord besoin de l’ID approprié pour créer la conversation.</span><span class="sxs-lookup"><span data-stu-id="3afe2-123">If you need to create a new conversation or conversation thread in a channel you'll first need the right ID to create the conversation.</span></span> <span data-ttu-id="3afe2-124">Vous pouvez recevoir/récupérer cet ID de plusieurs façons :</span><span class="sxs-lookup"><span data-stu-id="3afe2-124">You can receive/retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="3afe2-125">Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="3afe2-125">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="3afe2-126">Lorsqu’un nouvel utilisateur est ajouté à un contexte dans lequel votre application est installée, vous recevez une [ `onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="3afe2-126">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="3afe2-127">Vous pouvez récupérer la [liste des canaux](~/bots/how-to/get-teams-context.md) d’une équipe installée sur votre application.</span><span class="sxs-lookup"><span data-stu-id="3afe2-127">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="3afe2-128">Vous pouvez récupérer la [liste des membres](~/bots/how-to/get-teams-context.md) d’une équipe installée sur votre application.</span><span class="sxs-lookup"><span data-stu-id="3afe2-128">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="3afe2-129">Chaque activité reçue par votre robot contient les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="3afe2-129">Every Activity your bot receives will contain the necessary information.</span></span>

<span data-ttu-id="3afe2-130">Quelle que soit la façon dont vous obtenez les informations, vous devez stocker le `tenantId` et le `userId` ou `channelId` pour créer une conversation.</span><span class="sxs-lookup"><span data-stu-id="3afe2-130">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` in order to create a new conversation.</span></span> <span data-ttu-id="3afe2-131">Vous pouvez également utiliser le `teamId` pour créer un fil de conversation dans le canal général/par défaut d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="3afe2-131">You can also use the `teamId` to create a new conversation thread in the general/default channel of a team.</span></span>

<span data-ttu-id="3afe2-132">Le `userId` est unique pour votre ID de robot et un utilisateur particulier, vous ne pouvez pas les réutiliser entre les robots.</span><span class="sxs-lookup"><span data-stu-id="3afe2-132">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="3afe2-133">Le `channelId` est global, toutefois, votre robot _doit_ être installé dans l’équipe avant de pouvoir envoyer un message proactif à un canal.</span><span class="sxs-lookup"><span data-stu-id="3afe2-133">The `channelId` is global, however your bot _must_ be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="3afe2-134">Créer la conversation</span><span class="sxs-lookup"><span data-stu-id="3afe2-134">Create the conversation</span></span>

<span data-ttu-id="3afe2-135">Une fois que vous avez les informations de l’utilisateur/du canal, vous devez créer la conversation si elle n’existe pas déjà (ou si vous ne connaissez pas le `conversationId` ).</span><span class="sxs-lookup"><span data-stu-id="3afe2-135">Once you have the user/channel information, you'll need to create the conversation if it doesn't already exist (or you don't know the `conversationId`).</span></span> <span data-ttu-id="3afe2-136">Vous devez uniquement créer la conversation une seule fois ; Veillez à stocker la `conversationId` valeur ou l' `conversationReference` objet à utiliser à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="3afe2-136">You should only create the conversation once; make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="3afe2-137">Obtenir l’ID de conversation</span><span class="sxs-lookup"><span data-stu-id="3afe2-137">Get the conversation ID</span></span>

<span data-ttu-id="3afe2-138">Une fois la conversation créée, vous devez utiliser l' `conversationReference` objet ou le `conversationId` et le `tenantId` pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="3afe2-138">Once the conversation has been created, you will use either the `conversationReference` object or the `conversationId` and the `tenantId` to send the message.</span></span> <span data-ttu-id="3afe2-139">Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n’importe quelle activité qui vous a été envoyée à partir de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="3afe2-139">You can get this Id by either creating the conversation, or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="3afe2-140">Assurez-vous que vous stockez cet ID.</span><span class="sxs-lookup"><span data-stu-id="3afe2-140">Make certain that you store this Id.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="3afe2-141">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="3afe2-141">Send the message</span></span>

<span data-ttu-id="3afe2-142">Maintenant que vous disposez des informations d’adresse appropriées, vous pouvez envoyer votre message.</span><span class="sxs-lookup"><span data-stu-id="3afe2-142">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="3afe2-143">Si vous utilisez le kit de développement logiciel (SDK), vous pouvez le faire à l’aide de la `continueConversation` méthode et du `conversationId` et `tenantId` pour effectuer un appel d’API direct.</span><span class="sxs-lookup"><span data-stu-id="3afe2-143">If you're using the SDK, you'll do so using the `continueConversation` method,and the `conversationId` and `tenantId` to make a direct API call.</span></span>  <span data-ttu-id="3afe2-144">Vous devrez définir `conversationParameters` correctement l’envoi de votre message : consultez les [exemples](#examples) ci-dessous ou utilisez l’un des exemples figurant dans la section [références](#references) .</span><span class="sxs-lookup"><span data-stu-id="3afe2-144">You'll need to set the `conversationParameters` correctly to successfully send your message - see the [examples](#examples) below or use one of the samples listed in the [references](#references) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="3afe2-145">Meilleures pratiques pour la messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="3afe2-145">Best practices for proactive messaging</span></span>

<span data-ttu-id="3afe2-146">L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3afe2-146">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="3afe2-147">Toutefois, à partir de leur perspective, ce message peut sembler totalement indésirable et, dans le cas de messages de bienvenue, il sera la première fois qu’il interagit avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3afe2-147">However, from their perspective this message can appear completely unprompted and, in the case of welcome messages, it will be the first time they've interacted with your app.</span></span> <span data-ttu-id="3afe2-148">Par conséquent, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas envoyer de courrier indésirable) et de fournir suffisamment d’informations pour permettre aux utilisateurs de comprendre la raison pour laquelle ils reçoivent des messages.</span><span class="sxs-lookup"><span data-stu-id="3afe2-148">As such, it is very important to use this functionality sparingly (don't spam your users) and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="3afe2-149">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="3afe2-149">Welcome messages</span></span>

<span data-ttu-id="3afe2-150">Lors de l’utilisation de la messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que, pour la plupart des personnes qui reçoivent le message, il n’y aura pas de contexte pour les raisons pour lesquelles ils le reçoivent.</span><span class="sxs-lookup"><span data-stu-id="3afe2-150">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there will be no context for why they are receiving it.</span></span> <span data-ttu-id="3afe2-151">Il s’agit également de la première fois qu’ils interagissent avec votre application ; Il s’agit de votre opportunité de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="3afe2-151">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="3afe2-152">Les meilleurs messages d’accueil sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3afe2-152">The best welcome messages will include:</span></span>

* <span data-ttu-id="3afe2-153">**Raisons pour lesquelles un utilisateur reçoit le message.**</span><span class="sxs-lookup"><span data-stu-id="3afe2-153">**Why a user is receiving the message.**</span></span> <span data-ttu-id="3afe2-154">Il doit être très clair que les utilisateurs reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="3afe2-154">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="3afe2-155">Si votre robot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, indiquez-lui quel canal il a été installé et éventuellement qui l’a installé.</span><span class="sxs-lookup"><span data-stu-id="3afe2-155">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="3afe2-156">**Ce que vous proposez.**</span><span class="sxs-lookup"><span data-stu-id="3afe2-156">**What do you offer.**</span></span> <span data-ttu-id="3afe2-157">Qu’est-il possible de faire avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="3afe2-157">What can they do with your app?</span></span> <span data-ttu-id="3afe2-158">Quelle valeur pouvez-vous leur apporter ?</span><span class="sxs-lookup"><span data-stu-id="3afe2-158">What value can you bring to them?</span></span>
* <span data-ttu-id="3afe2-159">**Que dois-je faire ensuite ?**</span><span class="sxs-lookup"><span data-stu-id="3afe2-159">**What should they do next.**</span></span> <span data-ttu-id="3afe2-160">Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="3afe2-160">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="3afe2-161">N’oubliez pas que les messages de bienvenue médiocres peuvent amener les utilisateurs à bloquer votre robot.</span><span class="sxs-lookup"><span data-stu-id="3afe2-161">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="3afe2-162">Vous devez consacrer suffisamment de temps à la conception de vos messages de bienvenue et les parcourir s’ils n’ont pas l’effet escompté.</span><span class="sxs-lookup"><span data-stu-id="3afe2-162">You should spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="3afe2-163">Les messages de notification</span><span class="sxs-lookup"><span data-stu-id="3afe2-163">Notification messages</span></span>

<span data-ttu-id="3afe2-164">Lors de l’utilisation de la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs disposent d’un chemin d’accès clair afin de prendre des mesures courantes en fonction de votre notification et de bien comprendre la raison pour laquelle la notification s’est produite.</span><span class="sxs-lookup"><span data-stu-id="3afe2-164">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="3afe2-165">Les messages de notification valides sont généralement les suivants :</span><span class="sxs-lookup"><span data-stu-id="3afe2-165">Good notification messages will generally include:</span></span>

* <span data-ttu-id="3afe2-166">**Que s'est-il passé.**</span><span class="sxs-lookup"><span data-stu-id="3afe2-166">**What happened.**</span></span> <span data-ttu-id="3afe2-167">Indication claire de l’origine de la notification.</span><span class="sxs-lookup"><span data-stu-id="3afe2-167">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="3afe2-168">**Quel a été le résultat.**</span><span class="sxs-lookup"><span data-stu-id="3afe2-168">**What was the result.**</span></span> <span data-ttu-id="3afe2-169">Il doit être clair quel élément/élément a été mis à jour pour déclencher la notification.</span><span class="sxs-lookup"><span data-stu-id="3afe2-169">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="3afe2-170">**OMS/ce qui a été déclenché.**</span><span class="sxs-lookup"><span data-stu-id="3afe2-170">**Who/what triggered it.**</span></span> <span data-ttu-id="3afe2-171">Les personnes ou les actions qui ont entraîné l’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="3afe2-171">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="3afe2-172">**Ce que les utilisateurs peuvent faire en réponse.**</span><span class="sxs-lookup"><span data-stu-id="3afe2-172">**What can users do in response.**</span></span> <span data-ttu-id="3afe2-173">Permettre aux utilisateurs de prendre facilement des mesures en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="3afe2-173">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="3afe2-174">**Comment les utilisateurs peuvent-ils les désactiver** ? Vous devez fournir un chemin d’accès permettant aux utilisateurs de désactiver les notifications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3afe2-174">**How can users opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="3afe2-175">Installer de manière proactive votre application à l’aide de Graph</span><span class="sxs-lookup"><span data-stu-id="3afe2-175">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="3afe2-176">L’installation proactive d’applications à l’aide de Microsoft Graph est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="3afe2-176">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="3afe2-177">Parfois, il peut s’avérer nécessaire de messageer de manière proactive les utilisateurs qui n’ont pas installé ou interagi avec votre application précédemment.</span><span class="sxs-lookup"><span data-stu-id="3afe2-177">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="3afe2-178">Par exemple, vous souhaitez utiliser l' [entreprise Communicator](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="3afe2-178">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="3afe2-179">Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de l’événement que votre application recevra lors de l' `conversationUpdate` installation.</span><span class="sxs-lookup"><span data-stu-id="3afe2-179">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="3afe2-180">Vous ne pouvez installer que les applications figurant dans le catalogue d’applications de votre organisation ou dans le magasin d’applications Teams.</span><span class="sxs-lookup"><span data-stu-id="3afe2-180">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="3afe2-181">Voir [installer des applications pour les utilisateurs](/graph/teams-proactive-messaging) dans la documentation Graph et l' [installation et la messagerie de robots proactifs dans teams avec Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="3afe2-181">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="3afe2-182">Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  sur la plateforme github.</span><span class="sxs-lookup"><span data-stu-id="3afe2-182">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="3afe2-183">Exemples</span><span class="sxs-lookup"><span data-stu-id="3afe2-183">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3afe2-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3afe2-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="3afe2-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3afe2-185">TypeScript/Node.js</span></span>](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[<span data-ttu-id="3afe2-186">Python</span><span class="sxs-lookup"><span data-stu-id="3afe2-186">Python</span></span>](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[<span data-ttu-id="3afe2-187">JSON</span><span class="sxs-lookup"><span data-stu-id="3afe2-187">JSON</span></span>](#tab/json)

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="3afe2-188">Vous devez fournir l’ID d’utilisateur et l’ID de client.</span><span class="sxs-lookup"><span data-stu-id="3afe2-188">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="3afe2-189">Si l’appel réussit, l’API renvoie avec l’objet de réponse suivant.</span><span class="sxs-lookup"><span data-stu-id="3afe2-189">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a><span data-ttu-id="3afe2-190">Références</span><span class="sxs-lookup"><span data-stu-id="3afe2-190">References</span></span>

<span data-ttu-id="3afe2-191">Les exemples officiels de messagerie proactive sont répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3afe2-191">The official proactive messaging samples are listed below.</span></span>

|  <span data-ttu-id="3afe2-192">Non.</span><span class="sxs-lookup"><span data-stu-id="3afe2-192">No.</span></span>  | <span data-ttu-id="3afe2-193">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="3afe2-193">Sample Name</span></span>           | <span data-ttu-id="3afe2-194">Description</span><span class="sxs-lookup"><span data-stu-id="3afe2-194">Description</span></span>                                                                      | <span data-ttu-id="3afe2-195">.NET</span><span class="sxs-lookup"><span data-stu-id="3afe2-195">.NET</span></span>    | <span data-ttu-id="3afe2-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3afe2-196">JavaScript</span></span>   | <span data-ttu-id="3afe2-197">Python</span><span class="sxs-lookup"><span data-stu-id="3afe2-197">Python</span></span>  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="3afe2-198">57</span><span class="sxs-lookup"><span data-stu-id="3afe2-198">57</span></span>|<span data-ttu-id="3afe2-199">Concepts de base des conversations de teams</span><span class="sxs-lookup"><span data-stu-id="3afe2-199">Teams Conversation Basics</span></span>  | <span data-ttu-id="3afe2-200">Présente des notions de base des conversations dans Teams, y compris l’envoi de messages proactifs un-à-un.</span><span class="sxs-lookup"><span data-stu-id="3afe2-200">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="3afe2-201">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="3afe2-201">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="3afe2-202">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3afe2-202">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="3afe2-203">Python</span><span class="sxs-lookup"><span data-stu-id="3afe2-203">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="3afe2-204">58</span><span class="sxs-lookup"><span data-stu-id="3afe2-204">58</span></span>|<span data-ttu-id="3afe2-205">Démarrer un nouveau thread dans un canal</span><span class="sxs-lookup"><span data-stu-id="3afe2-205">Start new thread in a channel</span></span>     | <span data-ttu-id="3afe2-206">Illustre la création d’un nouveau thread dans un canal.</span><span class="sxs-lookup"><span data-stu-id="3afe2-206">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="3afe2-207">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="3afe2-207">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="3afe2-208">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3afe2-208">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="3afe2-209">Python</span><span class="sxs-lookup"><span data-stu-id="3afe2-209">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

<span data-ttu-id="3afe2-210">L’exemple ci-dessous illustre la quantité minimale d’informations nécessaires à l’envoi d’un message proactif (sans utiliser d' `conversationReference` objet).</span><span class="sxs-lookup"><span data-stu-id="3afe2-210">The sample below demonstrates the minimal amount of information needed to send a proactive message (without using a `conversationReference` object).</span></span> <span data-ttu-id="3afe2-211">Cet exemple peut être utile si vous utilisez des appels d’API REST directement ou si vous n’avez pas stocké d' `conversationReference` objets complets.</span><span class="sxs-lookup"><span data-stu-id="3afe2-211">This sample can be useful if you're using REST API calls directly, or haven't been storing full `conversationReference` objects.</span></span>

* [<span data-ttu-id="3afe2-212">Messagerie proactive teams</span><span class="sxs-lookup"><span data-stu-id="3afe2-212">Teams Proactive Messaging</span></span>](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a><span data-ttu-id="3afe2-213">Afficher du code supplémentaire</span><span class="sxs-lookup"><span data-stu-id="3afe2-213">View additional code</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3afe2-214">**Exemples de code de messagerie proactive teams**</span><span class="sxs-lookup"><span data-stu-id="3afe2-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>