---
title: Envoi de messages proactifs
description: Décrit comment envoyer des messages proactifs avec votre bot Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
Keywords: envoyer un message pour obtenir l'ID de conversation de l'ID de canal de l'ID de l'utilisateur
ms.openlocfilehash: 25d5c6a1b51240c87ff0d8610a965d30f6b01095
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697052"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="40ae1-104">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="40ae1-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="40ae1-105">Un message proactif est un message envoyé par un bot qui ne répond pas à une demande d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40ae1-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="40ae1-106">Cela peut inclure des messages, tels que :</span><span class="sxs-lookup"><span data-stu-id="40ae1-106">This can include messages, such as:</span></span>

* <span data-ttu-id="40ae1-107">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="40ae1-107">Welcome messages</span></span>
* <span data-ttu-id="40ae1-108">Notifications</span><span class="sxs-lookup"><span data-stu-id="40ae1-108">Notifications</span></span>
* <span data-ttu-id="40ae1-109">Messages programmés</span><span class="sxs-lookup"><span data-stu-id="40ae1-109">Scheduled messages</span></span>

<span data-ttu-id="40ae1-110">Pour que votre bot envoie un message proactif à un utilisateur, une conversation de groupe ou une équipe, il doit avoir accès pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="40ae1-111">Pour une conversation de groupe ou une équipe, l'application qui contient votre bot doit d'abord être installée à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="40ae1-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="40ae1-112">Vous pouvez installer votre application de manière proactive à l'aide de [Microsoft Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une stratégie d'application pour faire sortir les applications vers les équipes et les utilisateurs de votre client. [](/microsoftteams/teams-custom-app-policies-and-settings)</span><span class="sxs-lookup"><span data-stu-id="40ae1-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="40ae1-113">Pour les utilisateurs, votre application doit être installée pour l'utilisateur ou votre utilisateur doit faire partie d'une équipe sur laquelle votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="40ae1-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="40ae1-114">L'envoi d'un message proactif est différent de l'envoi d'un message normal.</span><span class="sxs-lookup"><span data-stu-id="40ae1-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="40ae1-115">Il n'est pas actif `turnContext` à utiliser pour une réponse.</span><span class="sxs-lookup"><span data-stu-id="40ae1-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="40ae1-116">Vous devez créer la conversation avant d'envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="40ae1-117">Par exemple, une nouvelle conversation un-à-un ou un nouveau thread de conversation dans un canal.</span><span class="sxs-lookup"><span data-stu-id="40ae1-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="40ae1-118">Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe avec une messagerie proactive.</span><span class="sxs-lookup"><span data-stu-id="40ae1-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="40ae1-119">**Pour envoyer un message proactif**</span><span class="sxs-lookup"><span data-stu-id="40ae1-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="40ae1-120">[Obtenez l'ID d'utilisateur, l'ID d'équipe ou l'ID de](#get-the-user-id-team-id-or-channel-id)canal, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40ae1-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="40ae1-121">[Créez la conversation,](#create-the-conversation)si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40ae1-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="40ae1-122">[Obtenir l'ID de conversation](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="40ae1-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="40ae1-123">[Envoyer le message](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="40ae1-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="40ae1-124">Pour utiliser efficacement les messages proactifs, consultez les meilleures pratiques en matière [de messagerie proactive.](#best-practices-for-proactive-messaging)</span><span class="sxs-lookup"><span data-stu-id="40ae1-124">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="40ae1-125">Dans certains scénarios, vous devez installer votre application de manière [proactive à l'aide de Graph.](#proactively-install-your-app-using-graph)</span><span class="sxs-lookup"><span data-stu-id="40ae1-125">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="40ae1-126">Les extraits de code de la section [exemples](#samples) sont pour la création d'une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="40ae1-126">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="40ae1-127">Pour obtenir des exemples de travail complets pour les conversations et les groupes ou canaux un-à-un, voir [l'exemple de code.](#code-sample)</span><span class="sxs-lookup"><span data-stu-id="40ae1-127">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="40ae1-128">Obtenir l'ID d'utilisateur, l'ID d'équipe ou l'ID de canal</span><span class="sxs-lookup"><span data-stu-id="40ae1-128">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="40ae1-129">Pour créer une conversation ou un thread de conversation dans un canal, vous devez avoir l'ID correct.</span><span class="sxs-lookup"><span data-stu-id="40ae1-129">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="40ae1-130">Vous pouvez recevoir ou récupérer cet ID à l'aide des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ae1-130">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="40ae1-131">Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="40ae1-131">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="40ae1-132">Lorsqu'un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="40ae1-132">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="40ae1-133">Vous pouvez récupérer la [liste des canaux dans](~/bots/how-to/get-teams-context.md) une équipe où votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="40ae1-133">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="40ae1-134">Vous pouvez récupérer la [liste des membres d'une](~/bots/how-to/get-teams-context.md) équipe sur laquelle votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="40ae1-134">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="40ae1-135">Chaque activité que reçoit votre bot doit contenir les informations requises.</span><span class="sxs-lookup"><span data-stu-id="40ae1-135">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="40ae1-136">Quelle que soit la façon dont vous obtenez les informations, vous devez stocker ou créer `tenantId` `userId` une `channelId` conversation.</span><span class="sxs-lookup"><span data-stu-id="40ae1-136">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="40ae1-137">Vous pouvez également l'utiliser pour créer un thread de conversation dans le canal général ou `teamId` par défaut d'une équipe.</span><span class="sxs-lookup"><span data-stu-id="40ae1-137">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="40ae1-138">Il `userId` est propre à votre ID de bot et à un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="40ae1-138">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="40ae1-139">Vous ne pouvez pas réutiliser les `userId` bots.</span><span class="sxs-lookup"><span data-stu-id="40ae1-139">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="40ae1-140">Il `channelId` s'agit d'une stratégie globale.</span><span class="sxs-lookup"><span data-stu-id="40ae1-140">The `channelId` is global.</span></span> <span data-ttu-id="40ae1-141">Toutefois, votre bot doit être installé dans l'équipe avant de pouvoir envoyer un message proactif à un canal.</span><span class="sxs-lookup"><span data-stu-id="40ae1-141">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="40ae1-142">Une fois que vous avez les informations de l'utilisateur ou du canal, vous devez créer la conversation.</span><span class="sxs-lookup"><span data-stu-id="40ae1-142">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="40ae1-143">Créer la conversation</span><span class="sxs-lookup"><span data-stu-id="40ae1-143">Create the conversation</span></span>

<span data-ttu-id="40ae1-144">Vous devez créer la conversation si elle n'existe pas ou si vous ne connaissez pas le `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="40ae1-144">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="40ae1-145">Vous ne devez créer la conversation qu'une seule fois et stocker la `conversationId` valeur ou `conversationReference` l'objet.</span><span class="sxs-lookup"><span data-stu-id="40ae1-145">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="40ae1-146">Une fois la conversation créée, vous devez obtenir l'ID de conversation.</span><span class="sxs-lookup"><span data-stu-id="40ae1-146">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="40ae1-147">Obtenir l'ID de conversation</span><span class="sxs-lookup"><span data-stu-id="40ae1-147">Get the conversation ID</span></span>

<span data-ttu-id="40ae1-148">Utilisez `conversationReference` l'objet ou et pour envoyer le `conversationId` `tenantId` message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-148">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="40ae1-149">Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n'importe quelle activité qui vous est envoyée à partir de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="40ae1-149">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="40ae1-150">Stockez cet ID pour référence.</span><span class="sxs-lookup"><span data-stu-id="40ae1-150">Store this ID for reference.</span></span>

<span data-ttu-id="40ae1-151">Une fois que vous avez reçu les informations d'adresse appropriées, vous pouvez envoyer votre message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-151">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="40ae1-152">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="40ae1-152">Send the message</span></span>

<span data-ttu-id="40ae1-153">Si vous utilisez le SDK, vous devez utiliser la méthode et effectuer un appel `continueConversation` `conversationId` `tenantId` d'API direct pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-153">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="40ae1-154">Vous devez définir correctement `conversationParameters` l'envoi de votre message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-154">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="40ae1-155">Maintenant que vous avez envoyé le message proactif, vous devez suivre ces meilleures pratiques tout en envoyant des messages proactifs pour un meilleur échange d'informations entre les utilisateurs et le bot.</span><span class="sxs-lookup"><span data-stu-id="40ae1-155">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="40ae1-156">Meilleures pratiques en matière de messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="40ae1-156">Best practices for proactive messaging</span></span>

<span data-ttu-id="40ae1-157">L'envoi de messages proactifs aux utilisateurs est un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="40ae1-157">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="40ae1-158">Toutefois, de leur point de vue, ce message peut apparaître complètement non improvisé et, dans le cas des messages de bienvenue, c'est la première fois qu'ils interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="40ae1-158">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="40ae1-159">Par conséquent, il est très important d'utiliser avec parcimonie la messagerie proactive, et non de mettre vos utilisateurs en courrier indésirable, et de fournir suffisamment d'informations pour que les utilisateurs comprennent pourquoi ils reçoivent les messages.</span><span class="sxs-lookup"><span data-stu-id="40ae1-159">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="40ae1-160">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="40ae1-160">Welcome messages</span></span>

<span data-ttu-id="40ae1-161">Lorsque la messagerie proactive est utilisée pour envoyer un message de bienvenue à un utilisateur, il n'existe aucun contexte pour expliquer pourquoi les utilisateurs reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-161">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="40ae1-162">C'est également la première fois que les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="40ae1-162">This is also the first time users interact with your app.</span></span> <span data-ttu-id="40ae1-163">Il s'agit d'une opportunité de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="40ae1-163">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="40ae1-164">Les meilleurs messages de bienvenue doivent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="40ae1-164">The best welcome messages must include:</span></span>

* <span data-ttu-id="40ae1-165">Pourquoi un utilisateur reçoit le message : il doit être très clair pour l'utilisateur pourquoi il reçoit le message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-165">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="40ae1-166">Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et qui l'a installé.</span><span class="sxs-lookup"><span data-stu-id="40ae1-166">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="40ae1-167">Que proposez-vous : les utilisateurs doivent être en mesure d'identifier ce qu'ils peuvent faire avec votre application et la valeur que vous pouvez leur apporter.</span><span class="sxs-lookup"><span data-stu-id="40ae1-167">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="40ae1-168">Que doivent-ils faire ensuite : inviter les utilisateurs à essayer une commande ou à interagir avec votre application.</span><span class="sxs-lookup"><span data-stu-id="40ae1-168">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="40ae1-169">Les messages d'accueil médiocres peuvent entraîner le blocage de votre bot par des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="40ae1-169">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="40ae1-170">Écrivez au point et effacer les messages de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="40ae1-170">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="40ae1-171">Itérer sur les messages de bienvenue s'ils n'ont pas l'effet souhaité.</span><span class="sxs-lookup"><span data-stu-id="40ae1-171">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="40ae1-172">Les messages de notification</span><span class="sxs-lookup"><span data-stu-id="40ae1-172">Notification messages</span></span>

<span data-ttu-id="40ae1-173">Pour envoyer des notifications à l'aide d'une messagerie proactive, assurez-vous que vos utilisateurs ont un chemin d'accès clair pour prendre des mesures communes en fonction de votre notification.</span><span class="sxs-lookup"><span data-stu-id="40ae1-173">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="40ae1-174">Assurez-vous que les utilisateurs comprennent clairement pourquoi ils ont reçu une notification.</span><span class="sxs-lookup"><span data-stu-id="40ae1-174">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="40ae1-175">Les messages de notification de bonne qualité incluent généralement les suivants :</span><span class="sxs-lookup"><span data-stu-id="40ae1-175">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="40ae1-176">Ce qui s'est passé : une indication claire de ce qui est arrivé à l'origine de la notification.</span><span class="sxs-lookup"><span data-stu-id="40ae1-176">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="40ae1-177">Résultat : il doit être clair sur quel élément a été mis à jour pour provoquer la notification.</span><span class="sxs-lookup"><span data-stu-id="40ae1-177">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="40ae1-178">Qui ou qu'est-ce qui l'a déclenché : qui ou qui a pris l'action qui a provoqué l'envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="40ae1-178">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="40ae1-179">Que peuvent faire les utilisateurs en réponse : faciliter l'action de vos utilisateurs en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="40ae1-179">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="40ae1-180">Comment les utilisateurs peuvent-ils refuser : vous devez fournir un chemin d'accès aux utilisateurs pour qu'ils ne choisissent pas d'autres notifications.</span><span class="sxs-lookup"><span data-stu-id="40ae1-180">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="40ae1-181">Pour envoyer des messages à un grand groupe d'utilisateurs, par exemple à votre organisation, installez votre application de manière proactive à l'aide de Graph.</span><span class="sxs-lookup"><span data-stu-id="40ae1-181">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="40ae1-182">Messages programmés</span><span class="sxs-lookup"><span data-stu-id="40ae1-182">Scheduled messages</span></span>

<span data-ttu-id="40ae1-183">Lorsque vous utilisez une messagerie proactive pour envoyer des messages programmés aux utilisateurs, vérifiez que votre fuseau horaire est mis à jour vers leur fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="40ae1-183">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="40ae1-184">Cela garantit que les messages sont remis aux utilisateurs au moment approprié.</span><span class="sxs-lookup"><span data-stu-id="40ae1-184">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="40ae1-185">Les messages de planification incluent généralement :</span><span class="sxs-lookup"><span data-stu-id="40ae1-185">Schedule messages generally include:</span></span>

* <span data-ttu-id="40ae1-186">**Pourquoi l'utilisateur reçoit-il le message**: faites en sorte que vos utilisateurs comprennent facilement la raison pour laquelle ils reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-186">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="40ae1-187">**Que peut faire l'utilisateur ensuite**: les utilisateurs peuvent prendre l'action requise en fonction du contenu du message.</span><span class="sxs-lookup"><span data-stu-id="40ae1-187">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="40ae1-188">Installer votre application de manière proactive à l'aide de Graph</span><span class="sxs-lookup"><span data-stu-id="40ae1-188">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="40ae1-189">L'installation proactive d'applications à l'aide de Graph est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="40ae1-189">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="40ae1-190">Envoyer un message de manière proactive aux utilisateurs qui n'ont pas précédemment installé ou interagi avec votre application.</span><span class="sxs-lookup"><span data-stu-id="40ae1-190">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="40ae1-191">Par exemple, vous souhaitez utiliser le communicateur [d'entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l'ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="40ae1-191">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="40ae1-192">Dans ce cas, vous pouvez utiliser l'API Graph pour installer de manière proactive votre application pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="40ae1-192">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="40ae1-193">Mettre en cache les valeurs nécessaires à partir `conversationUpdate` de l'événement que votre application reçoit lors de l'installation.</span><span class="sxs-lookup"><span data-stu-id="40ae1-193">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="40ae1-194">Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d'applications d'organisation ou dans l'App Store Teams.</span><span class="sxs-lookup"><span data-stu-id="40ae1-194">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="40ae1-195">Voir [installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps) dans la documentation Graph, ainsi que l'installation proactive du bot et la messagerie dans Teams avec [Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="40ae1-195">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="40ae1-196">Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) sur la plateforme GitHub.</span><span class="sxs-lookup"><span data-stu-id="40ae1-196">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="40ae1-197">Exemples</span><span class="sxs-lookup"><span data-stu-id="40ae1-197">Samples</span></span>

<span data-ttu-id="40ae1-198">Le code suivant présente un exemple de code simple qui installe de manière proactive votre application à l'aide de Graph :</span><span class="sxs-lookup"><span data-stu-id="40ae1-198">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="40ae1-199">C#</span><span class="sxs-lookup"><span data-stu-id="40ae1-199">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="40ae1-200">TypeScript</span><span class="sxs-lookup"><span data-stu-id="40ae1-200">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="40ae1-201">Python</span><span class="sxs-lookup"><span data-stu-id="40ae1-201">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="40ae1-202">JSON</span><span class="sxs-lookup"><span data-stu-id="40ae1-202">JSON</span></span>](#tab/json)

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

<span data-ttu-id="40ae1-203">Vous devez fournir l'ID d'utilisateur et l'ID de client.</span><span class="sxs-lookup"><span data-stu-id="40ae1-203">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="40ae1-204">Si l'appel réussit, l'API renvoie l'objet de réponse suivant :</span><span class="sxs-lookup"><span data-stu-id="40ae1-204">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="40ae1-205">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="40ae1-205">Code sample</span></span>

<span data-ttu-id="40ae1-206">Le tableau suivant fournit un exemple de code simple qui incorpore le flux de conversation de base dans une application Teams et comment créer un thread de conversation dans un canal dans Teams :</span><span class="sxs-lookup"><span data-stu-id="40ae1-206">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="40ae1-207">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="40ae1-207">Sample name</span></span>           | <span data-ttu-id="40ae1-208">Description</span><span class="sxs-lookup"><span data-stu-id="40ae1-208">Description</span></span>                                                                      | <span data-ttu-id="40ae1-209">.NET</span><span class="sxs-lookup"><span data-stu-id="40ae1-209">.NET</span></span>    | <span data-ttu-id="40ae1-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="40ae1-210">Node.js</span></span>   | <span data-ttu-id="40ae1-211">Python</span><span class="sxs-lookup"><span data-stu-id="40ae1-211">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="40ae1-212">Informations de base sur les conversations Teams</span><span class="sxs-lookup"><span data-stu-id="40ae1-212">Teams conversation basics</span></span>  | <span data-ttu-id="40ae1-213">Présente les principes de base des conversations dans Teams, notamment l'envoi de messages proactifs un-à-un.</span><span class="sxs-lookup"><span data-stu-id="40ae1-213">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="40ae1-214">View</span><span class="sxs-lookup"><span data-stu-id="40ae1-214">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="40ae1-215">View</span><span class="sxs-lookup"><span data-stu-id="40ae1-215">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="40ae1-216">View</span><span class="sxs-lookup"><span data-stu-id="40ae1-216">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="40ae1-217">Démarrer un nouveau thread dans un canal</span><span class="sxs-lookup"><span data-stu-id="40ae1-217">Start new thread in a channel</span></span>     | <span data-ttu-id="40ae1-218">Illustre la création d'un thread dans un canal.</span><span class="sxs-lookup"><span data-stu-id="40ae1-218">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="40ae1-219">View</span><span class="sxs-lookup"><span data-stu-id="40ae1-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="40ae1-220">View</span><span class="sxs-lookup"><span data-stu-id="40ae1-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="40ae1-221">View</span><span class="sxs-lookup"><span data-stu-id="40ae1-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="40ae1-222">Exemple de code supplémentaire</span><span class="sxs-lookup"><span data-stu-id="40ae1-222">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="40ae1-223">Exemples de code de messagerie proactive Teams</span><span class="sxs-lookup"><span data-stu-id="40ae1-223">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="40ae1-224">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="40ae1-224">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="40ae1-225">Mettre en forme vos messages de bot</span><span class="sxs-lookup"><span data-stu-id="40ae1-225">Format your bot messages</span></span>](~/bots/how-to/format-your-bot-messages.md)
