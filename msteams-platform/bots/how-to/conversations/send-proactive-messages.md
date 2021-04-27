---
title: Envoyer des messages proactifs
description: Décrit comment envoyer des messages proactifs avec votre bot Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: envoyer un message pour obtenir l'ID de conversation de l'ID de canal de l'ID de l'utilisateur
ms.openlocfilehash: ae651ac94b1b092374f6fae284b67070036b561f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020918"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="e69df-104">Envoyer des messages proactifs</span><span class="sxs-lookup"><span data-stu-id="e69df-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e69df-105">Un message proactif est un message envoyé par un bot qui ne répond pas à une demande d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e69df-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="e69df-106">Cela peut inclure des messages, tels que :</span><span class="sxs-lookup"><span data-stu-id="e69df-106">This can include messages, such as:</span></span>

* <span data-ttu-id="e69df-107">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="e69df-107">Welcome messages</span></span>
* <span data-ttu-id="e69df-108">Notifications</span><span class="sxs-lookup"><span data-stu-id="e69df-108">Notifications</span></span>
* <span data-ttu-id="e69df-109">Messages programmés</span><span class="sxs-lookup"><span data-stu-id="e69df-109">Scheduled messages</span></span>

<span data-ttu-id="e69df-110">Pour que votre bot envoie un message proactif à un utilisateur, une conversation de groupe ou une équipe, il doit avoir accès pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="e69df-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="e69df-111">Pour une conversation de groupe ou une équipe, l'application qui contient votre bot doit d'abord être installée à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="e69df-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="e69df-112">Vous pouvez installer votre application de manière proactive à l'aide de [Microsoft Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une stratégie d'application pour faire sortir les applications vers les équipes et les utilisateurs de votre client. [](/microsoftteams/teams-custom-app-policies-and-settings)</span><span class="sxs-lookup"><span data-stu-id="e69df-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="e69df-113">Pour les utilisateurs, votre application doit être installée pour l'utilisateur ou votre utilisateur doit faire partie d'une équipe sur laquelle votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="e69df-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="e69df-114">L'envoi d'un message proactif est différent de l'envoi d'un message normal.</span><span class="sxs-lookup"><span data-stu-id="e69df-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="e69df-115">Il n'est pas actif `turnContext` à utiliser pour une réponse.</span><span class="sxs-lookup"><span data-stu-id="e69df-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="e69df-116">Vous devez créer la conversation avant d'envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="e69df-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="e69df-117">Par exemple, une nouvelle conversation un-à-un ou un nouveau thread de conversation dans un canal.</span><span class="sxs-lookup"><span data-stu-id="e69df-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="e69df-118">Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe avec une messagerie proactive.</span><span class="sxs-lookup"><span data-stu-id="e69df-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="e69df-119">**Pour envoyer un message proactif**</span><span class="sxs-lookup"><span data-stu-id="e69df-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="e69df-120">[Obtenez l'ID d'utilisateur, l'ID d'équipe ou l'ID](#get-the-user-id-team-id-or-channel-id)de canal, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e69df-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="e69df-121">[Créez la conversation,](#create-the-conversation)si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e69df-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="e69df-122">[Obtenir l'ID de conversation](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="e69df-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="e69df-123">[Envoyer le message](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="e69df-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="e69df-124">Les extraits de code de la section [exemples](#samples) sont pour la création d'une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="e69df-124">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="e69df-125">Pour obtenir des liens vers des exemples de travail complets pour les conversations un-à-un et les groupes ou canaux, voir [l'exemple de code.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="e69df-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code sample](#code-sample).</span></span>

<span data-ttu-id="e69df-126">Pour utiliser efficacement les messages proactifs, consultez les meilleures pratiques en matière [de messagerie proactive.](#best-practices-for-proactive-messaging)</span><span class="sxs-lookup"><span data-stu-id="e69df-126">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="e69df-127">Dans certains scénarios, vous devez installer votre application de manière [proactive à l'aide de Graph.](#proactively-install-your-app-using-graph)</span><span class="sxs-lookup"><span data-stu-id="e69df-127">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="e69df-128">Les extraits de code de la section [exemples](#samples) sont pour la création d'une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="e69df-128">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="e69df-129">Pour obtenir des exemples de travail complets pour les conversations et les groupes ou canaux un-à-un, voir [l'exemple de code.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="e69df-129">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="e69df-130">Obtenir l'ID d'utilisateur, l'ID d'équipe ou l'ID de canal</span><span class="sxs-lookup"><span data-stu-id="e69df-130">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="e69df-131">Pour créer une conversation ou un thread de conversation dans un canal, vous devez avoir l'ID correct.</span><span class="sxs-lookup"><span data-stu-id="e69df-131">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="e69df-132">Vous pouvez recevoir ou récupérer cet ID à l'aide des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e69df-132">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="e69df-133">Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="e69df-133">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="e69df-134">Lorsqu'un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="e69df-134">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="e69df-135">Vous pouvez récupérer la [liste des canaux dans](~/bots/how-to/get-teams-context.md) une équipe où votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="e69df-135">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="e69df-136">Vous pouvez récupérer la [liste des membres d'une](~/bots/how-to/get-teams-context.md) équipe sur laquelle votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="e69df-136">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="e69df-137">Chaque activité que reçoit votre bot doit contenir les informations requises.</span><span class="sxs-lookup"><span data-stu-id="e69df-137">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="e69df-138">Quelle que soit la façon dont vous obtenez les informations, vous devez stocker ou créer `tenantId` `userId` une `channelId` conversation.</span><span class="sxs-lookup"><span data-stu-id="e69df-138">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="e69df-139">Vous pouvez également l'utiliser pour créer un thread de conversation dans le canal général ou `teamId` par défaut d'une équipe.</span><span class="sxs-lookup"><span data-stu-id="e69df-139">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="e69df-140">Il `userId` est propre à votre ID de bot et à un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="e69df-140">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="e69df-141">Vous ne pouvez pas réutiliser les `userId` bots.</span><span class="sxs-lookup"><span data-stu-id="e69df-141">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="e69df-142">`channelId`L'objectif est global.</span><span class="sxs-lookup"><span data-stu-id="e69df-142">The `channelId` is global.</span></span> <span data-ttu-id="e69df-143">Toutefois, votre bot doit être installé dans l'équipe avant de pouvoir envoyer un message proactif à un canal.</span><span class="sxs-lookup"><span data-stu-id="e69df-143">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="e69df-144">Une fois que vous avez les informations de l'utilisateur ou du canal, vous devez créer la conversation.</span><span class="sxs-lookup"><span data-stu-id="e69df-144">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="e69df-145">Créer la conversation</span><span class="sxs-lookup"><span data-stu-id="e69df-145">Create the conversation</span></span>

<span data-ttu-id="e69df-146">Vous devez créer la conversation si elle n'existe pas ou si vous ne connaissez pas le `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="e69df-146">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="e69df-147">Vous ne devez créer la conversation qu'une seule fois et stocker la `conversationId` valeur ou `conversationReference` l'objet.</span><span class="sxs-lookup"><span data-stu-id="e69df-147">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="e69df-148">Une fois la conversation créée, vous devez obtenir l'ID de conversation.</span><span class="sxs-lookup"><span data-stu-id="e69df-148">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="e69df-149">Obtenir l'ID de conversation</span><span class="sxs-lookup"><span data-stu-id="e69df-149">Get the conversation ID</span></span>

<span data-ttu-id="e69df-150">Utilisez `conversationReference` l'objet ou et pour envoyer le `conversationId` `tenantId` message.</span><span class="sxs-lookup"><span data-stu-id="e69df-150">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="e69df-151">Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n'importe quelle activité qui vous est envoyée à partir de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="e69df-151">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="e69df-152">Stockez cet ID pour référence.</span><span class="sxs-lookup"><span data-stu-id="e69df-152">Store this ID for reference.</span></span>

<span data-ttu-id="e69df-153">Une fois que vous avez reçu les informations d'adresse appropriées, vous pouvez envoyer votre message.</span><span class="sxs-lookup"><span data-stu-id="e69df-153">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="e69df-154">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="e69df-154">Send the message</span></span>

<span data-ttu-id="e69df-155">Maintenant que vous avez les bonnes informations d'adresse, vous pouvez envoyer votre message.</span><span class="sxs-lookup"><span data-stu-id="e69df-155">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="e69df-156">Si vous utilisez le SDK, vous le faites à l'aide de la méthode et pour effectuer un appel `continueConversation` `conversationId` `tenantId` d'API direct.</span><span class="sxs-lookup"><span data-stu-id="e69df-156">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="e69df-157">Vous devez définir correctement `conversationParameters` l'envoi de votre message.</span><span class="sxs-lookup"><span data-stu-id="e69df-157">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="e69df-158">Consultez la section [exemples](#samples) ou utilisez l'un des exemples répertoriés dans la section [exemple de code.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="e69df-158">See the [samples](#samples) section or use one of the samples listed in the [code sample](#code-sample) section.</span></span>

<span data-ttu-id="e69df-159">Si vous utilisez le SDK, vous devez utiliser la méthode et effectuer un appel `continueConversation` `conversationId` `tenantId` d'API direct pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="e69df-159">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="e69df-160">Vous devez définir correctement `conversationParameters` l'envoi de votre message.</span><span class="sxs-lookup"><span data-stu-id="e69df-160">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="e69df-161">Maintenant que vous avez envoyé le message proactif, vous devez suivre ces meilleures pratiques tout en envoyant des messages proactifs pour un meilleur échange d'informations entre les utilisateurs et le bot.</span><span class="sxs-lookup"><span data-stu-id="e69df-161">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="e69df-162">Meilleures pratiques en matière de messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="e69df-162">Best practices for proactive messaging</span></span>

<span data-ttu-id="e69df-163">L'envoi de messages proactifs aux utilisateurs est un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e69df-163">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="e69df-164">Toutefois, de leur point de vue, ce message peut apparaître complètement non improvisé et, dans le cas des messages de bienvenue, c'est la première fois qu'ils interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="e69df-164">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="e69df-165">Par conséquent, il est très important d'utiliser avec parcimonie la messagerie proactive, et non de mettre vos utilisateurs en courrier indésirable, et de fournir suffisamment d'informations pour que les utilisateurs comprennent pourquoi ils reçoivent les messages.</span><span class="sxs-lookup"><span data-stu-id="e69df-165">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="e69df-166">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="e69df-166">Welcome messages</span></span>

<span data-ttu-id="e69df-167">Lorsque la messagerie proactive est utilisée pour envoyer un message de bienvenue à un utilisateur, il n’existe aucun contexte pour expliquer pourquoi les utilisateurs reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="e69df-167">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="e69df-168">C’est également la première fois que les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="e69df-168">This is also the first time users interact with your app.</span></span> <span data-ttu-id="e69df-169">Il s’agit d’une opportunité de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="e69df-169">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="e69df-170">Les meilleurs messages de bienvenue doivent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="e69df-170">The best welcome messages must include:</span></span>

* <span data-ttu-id="e69df-171">Pourquoi un utilisateur reçoit le message : il doit être très clair pour l’utilisateur pourquoi il reçoit le message.</span><span class="sxs-lookup"><span data-stu-id="e69df-171">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="e69df-172">Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et qui l’a installé.</span><span class="sxs-lookup"><span data-stu-id="e69df-172">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="e69df-173">Que proposez-vous : les utilisateurs doivent être en mesure d’identifier ce qu’ils peuvent faire avec votre application et la valeur que vous pouvez leur apporter.</span><span class="sxs-lookup"><span data-stu-id="e69df-173">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="e69df-174">Que doivent-ils faire ensuite : inviter les utilisateurs à essayer une commande ou à interagir avec votre application.</span><span class="sxs-lookup"><span data-stu-id="e69df-174">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="e69df-175">Les messages d’accueil médiocres peuvent entraîner le blocage de votre bot par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e69df-175">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="e69df-176">Écrivez au point et effacer les messages de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="e69df-176">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="e69df-177">Itérer sur les messages de bienvenue s’ils n’ont pas l’effet souhaité.</span><span class="sxs-lookup"><span data-stu-id="e69df-177">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="e69df-178">Les messages de notification</span><span class="sxs-lookup"><span data-stu-id="e69df-178">Notification messages</span></span>

<span data-ttu-id="e69df-179">Pour envoyer des notifications à l’aide d’une messagerie proactive, assurez-vous que vos utilisateurs ont un chemin d’accès clair pour prendre des mesures communes en fonction de votre notification.</span><span class="sxs-lookup"><span data-stu-id="e69df-179">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="e69df-180">Assurez-vous que les utilisateurs comprennent clairement pourquoi ils ont reçu une notification.</span><span class="sxs-lookup"><span data-stu-id="e69df-180">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="e69df-181">Les messages de notification de bonne qualité sont généralement les suivants :</span><span class="sxs-lookup"><span data-stu-id="e69df-181">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="e69df-182">Ce qui s’est passé : une indication claire de ce qui est arrivé à l’origine de la notification.</span><span class="sxs-lookup"><span data-stu-id="e69df-182">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="e69df-183">Résultat : il doit être clair sur quel élément a été mis à jour pour provoquer la notification.</span><span class="sxs-lookup"><span data-stu-id="e69df-183">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="e69df-184">Qui ou qu’est-ce qui l’a déclenché : qui ou qui a pris l’action qui a provoqué l’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="e69df-184">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="e69df-185">Que peuvent faire les utilisateurs en réponse : faciliter l’action de vos utilisateurs en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="e69df-185">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="e69df-186">Comment les utilisateurs peuvent-ils refuser : vous devez fournir un chemin d’accès aux utilisateurs pour qu’ils ne choisissent pas d’autres notifications.</span><span class="sxs-lookup"><span data-stu-id="e69df-186">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="e69df-187">Pour envoyer des messages à un grand groupe d’utilisateurs, par exemple à votre organisation, installez votre application de manière proactive à l’aide de Graph.</span><span class="sxs-lookup"><span data-stu-id="e69df-187">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="e69df-188">Messages programmés</span><span class="sxs-lookup"><span data-stu-id="e69df-188">Scheduled messages</span></span>

<span data-ttu-id="e69df-189">Lorsque vous utilisez une messagerie proactive pour envoyer des messages programmés aux utilisateurs, vérifiez que votre fuseau horaire est mis à jour vers leur fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="e69df-189">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="e69df-190">Cela garantit que les messages sont remis aux utilisateurs au moment approprié.</span><span class="sxs-lookup"><span data-stu-id="e69df-190">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="e69df-191">Les messages de planification incluent généralement :</span><span class="sxs-lookup"><span data-stu-id="e69df-191">Schedule messages generally include:</span></span>

* <span data-ttu-id="e69df-192">Pourquoi l'utilisateur reçoit-il le message : faciliter la compréhension de la raison pour laquelle il reçoit le message ?</span><span class="sxs-lookup"><span data-stu-id="e69df-192">Why is the user receiving the message: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="e69df-193">Que peut faire l'utilisateur ensuite : les utilisateurs peuvent prendre l'action requise en fonction du contenu du message.</span><span class="sxs-lookup"><span data-stu-id="e69df-193">What can user do next: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="e69df-194">Installer votre application de manière proactive à l'aide de Graph</span><span class="sxs-lookup"><span data-stu-id="e69df-194">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="e69df-195">L'installation proactive d'applications à l'aide de Graph est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="e69df-195">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="e69df-196">Envoyer un message de manière proactive aux utilisateurs qui n'ont pas précédemment installé ou interagi avec votre application.</span><span class="sxs-lookup"><span data-stu-id="e69df-196">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="e69df-197">Par exemple, vous souhaitez utiliser le communicateur [d'entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l'ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="e69df-197">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="e69df-198">Dans ce cas, vous pouvez utiliser l'API Graph pour installer de manière proactive votre application pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e69df-198">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="e69df-199">Mettre en cache les valeurs nécessaires à partir `conversationUpdate` de l'événement que votre application reçoit lors de l'installation.</span><span class="sxs-lookup"><span data-stu-id="e69df-199">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="e69df-200">Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d'applications d'organisation ou dans l'App Store Teams.</span><span class="sxs-lookup"><span data-stu-id="e69df-200">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="e69df-201">Voir [installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps) dans la documentation Graph, ainsi que l'installation proactive d'un bot et la messagerie dans Teams avec [Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e69df-201">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="e69df-202">Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) sur la plateforme GitHub.</span><span class="sxs-lookup"><span data-stu-id="e69df-202">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="e69df-203">Exemples</span><span class="sxs-lookup"><span data-stu-id="e69df-203">Samples</span></span>

<span data-ttu-id="e69df-204">Le code suivant présente un exemple de code simple qui installe de manière proactive votre application à l'aide de Graph :</span><span class="sxs-lookup"><span data-stu-id="e69df-204">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="e69df-205">C#</span><span class="sxs-lookup"><span data-stu-id="e69df-205">C#</span></span>](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="e69df-206">TypeScript</span><span class="sxs-lookup"><span data-stu-id="e69df-206">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="e69df-207">Python</span><span class="sxs-lookup"><span data-stu-id="e69df-207">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="e69df-208">JSON</span><span class="sxs-lookup"><span data-stu-id="e69df-208">JSON</span></span>](#tab/json)

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

<span data-ttu-id="e69df-209">Vous devez fournir l'ID d'utilisateur et l'ID de client.</span><span class="sxs-lookup"><span data-stu-id="e69df-209">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="e69df-210">Si l'appel réussit, l'API renvoie l'objet de réponse suivant :</span><span class="sxs-lookup"><span data-stu-id="e69df-210">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="e69df-211">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="e69df-211">Code sample</span></span>

<span data-ttu-id="e69df-212">Le tableau suivant fournit un exemple de code simple qui incorpore le flux de conversation de base dans une application Teams et comment créer un thread de conversation dans un canal dans Teams :</span><span class="sxs-lookup"><span data-stu-id="e69df-212">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="e69df-213">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="e69df-213">**Sample Name**</span></span> | <span data-ttu-id="e69df-214">**Description**</span><span class="sxs-lookup"><span data-stu-id="e69df-214">**Description**</span></span> | <span data-ttu-id="e69df-215">**.NET**</span><span class="sxs-lookup"><span data-stu-id="e69df-215">**.NET**</span></span> | <span data-ttu-id="e69df-216">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="e69df-216">**Node.js**</span></span> | <span data-ttu-id="e69df-217">**Python**</span><span class="sxs-lookup"><span data-stu-id="e69df-217">**Python**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="e69df-218">Informations de base sur les conversations Teams</span><span class="sxs-lookup"><span data-stu-id="e69df-218">Teams Conversation Basics</span></span>  | <span data-ttu-id="e69df-219">Présente les principes de base des conversations dans Teams, notamment l'envoi de messages proactifs un-à-un.</span><span class="sxs-lookup"><span data-stu-id="e69df-219">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>| [<span data-ttu-id="e69df-220">View</span><span class="sxs-lookup"><span data-stu-id="e69df-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="e69df-221">View</span><span class="sxs-lookup"><span data-stu-id="e69df-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="e69df-222">View</span><span class="sxs-lookup"><span data-stu-id="e69df-222">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| <span data-ttu-id="e69df-223">Démarrer un nouveau thread dans un canal</span><span class="sxs-lookup"><span data-stu-id="e69df-223">Start new thread in a channel</span></span> | <span data-ttu-id="e69df-224">Illustre la création d'un thread dans un canal.</span><span class="sxs-lookup"><span data-stu-id="e69df-224">Demonstrates creating a new thread in a channel.</span></span> | [<span data-ttu-id="e69df-225">View</span><span class="sxs-lookup"><span data-stu-id="e69df-225">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="e69df-226">View</span><span class="sxs-lookup"><span data-stu-id="e69df-226">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="e69df-227">View</span><span class="sxs-lookup"><span data-stu-id="e69df-227">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="e69df-228">Exemple de code supplémentaire</span><span class="sxs-lookup"><span data-stu-id="e69df-228">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e69df-229">Exemples de code de messagerie proactive Teams</span><span class="sxs-lookup"><span data-stu-id="e69df-229">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="e69df-230">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e69df-230">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="e69df-231">Exemples de [**code de messagerie proactive Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
>  [Mettre en forme vos messages de bot](~/bots/how-to/format-your-bot-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e69df-231">[**Teams proactive messaging code samples**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
[Format your bot messages](~/bots/how-to/format-your-bot-messages.md)</span></span>
