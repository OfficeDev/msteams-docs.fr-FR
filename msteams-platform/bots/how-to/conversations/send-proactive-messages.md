---
title: envoyer des messages proactifs
description: explique comment envoyer des messages proactifs avec votre bot Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: envoyer un message pour obtenir l’ID de conversation de l’ID de canal de l’ID utilisateur
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654292"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="d9366-104">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="d9366-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="d9366-105">Un message proactif est tout message envoyé par un bot qui n’est pas en réponse directe à une demande d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9366-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="d9366-106">Cela peut inclure des messages tels que :</span><span class="sxs-lookup"><span data-stu-id="d9366-106">This can include messages like:</span></span>

* <span data-ttu-id="d9366-107">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="d9366-107">Welcome messages</span></span>
* <span data-ttu-id="d9366-108">Notifications</span><span class="sxs-lookup"><span data-stu-id="d9366-108">Notifications</span></span>
* <span data-ttu-id="d9366-109">Messages programmés</span><span class="sxs-lookup"><span data-stu-id="d9366-109">Scheduled messages</span></span>

<span data-ttu-id="d9366-110">Pour que votre bot envoie un message proactif, il doit avoir accès à l’utilisateur, à la conversation de groupe ou à l’équipe à qui vous souhaitez envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="d9366-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="d9366-111">Pour une conversation de groupe ou une équipe, cela signifie que l’application qui contient votre bot doit d’abord être installée à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="d9366-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="d9366-112">Vous pouvez [installer votre](#proactively-install-your-app-using-graph) application de manière proactive à [](/microsoftteams/teams-custom-app-policies-and-settings) l’aide de Graph dans une équipe, si nécessaire, ou utiliser une stratégie d’application pour faire sortir les applications vers les équipes et les utilisateurs de votre client.</span><span class="sxs-lookup"><span data-stu-id="d9366-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="d9366-113">Pour les utilisateurs, votre application doit être installée pour l’utilisateur ou votre utilisateur doit faire partie d’une équipe sur laquelle votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="d9366-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="d9366-114">L’envoi d’un message proactif est différent de l’envoi d’un message normal.</span><span class="sxs-lookup"><span data-stu-id="d9366-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="d9366-115">Dans ce cas, il n’est pas actif `turnContext` à utiliser pour une réponse.</span><span class="sxs-lookup"><span data-stu-id="d9366-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="d9366-116">Vous devrez peut-être également créer la conversation avant d’envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="d9366-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="d9366-117">Par exemple, une nouvelle conversation un-à-un ou un nouveau thread de conversation dans un canal.</span><span class="sxs-lookup"><span data-stu-id="d9366-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="d9366-118">Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe avec une messagerie proactive.</span><span class="sxs-lookup"><span data-stu-id="d9366-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="d9366-119">À un niveau élevé, les étapes à suivre pour envoyer un message proactif sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9366-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="d9366-120">[Obtenez l’ID utilisateur ou l’ID d’équipe/canal](#get-the-user-id-or-teamchannel-id) (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="d9366-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="d9366-121">[Créez la conversation ou le thread de conversation](#create-the-conversation) (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="d9366-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="d9366-122">[Obtenir l’ID de conversation](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="d9366-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="d9366-123">[Envoyez le message](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="d9366-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="d9366-124">Les extraits de code de la section [Exemples](#examples) sont pour la création d’une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="d9366-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="d9366-125">Pour obtenir des liens vers des exemples de travail complets pour les conversations un-à-un et les groupes ou canaux, voir [les exemples de code.](#code-samples)</span><span class="sxs-lookup"><span data-stu-id="d9366-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="d9366-126">Obtenir l’ID utilisateur ou l’ID d’équipe/canal</span><span class="sxs-lookup"><span data-stu-id="d9366-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="d9366-127">Pour créer une conversation ou un thread de conversation dans un canal, vous avez besoin de l’ID correct.</span><span class="sxs-lookup"><span data-stu-id="d9366-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="d9366-128">Vous pouvez recevoir ou récupérer cet ID de plusieurs manières :</span><span class="sxs-lookup"><span data-stu-id="d9366-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="d9366-129">Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="d9366-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="d9366-130">Lorsqu’un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [ `onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="d9366-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="d9366-131">Vous pouvez récupérer la [liste des canaux](~/bots/how-to/get-teams-context.md) d’une équipe où votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="d9366-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="d9366-132">Vous pouvez récupérer la [liste des membres d’une](~/bots/how-to/get-teams-context.md) équipe sur l’installation de votre application.</span><span class="sxs-lookup"><span data-stu-id="d9366-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="d9366-133">Chaque activité que reçoit votre bot doit contenir les informations requises.</span><span class="sxs-lookup"><span data-stu-id="d9366-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="d9366-134">Quelle que soit la façon dont vous gagnez les informations, vous devez stocker les informations et créer `tenantId` `userId` une nouvelle `channelId` conversation.</span><span class="sxs-lookup"><span data-stu-id="d9366-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="d9366-135">Vous pouvez également l’utiliser pour créer un thread de conversation dans le canal général ou `teamId` par défaut d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="d9366-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="d9366-136">Il est propre à votre ID de bot et à un utilisateur particulier, vous ne pouvez pas `userId` les ré-utiliser entre les bots.</span><span class="sxs-lookup"><span data-stu-id="d9366-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="d9366-137">La stratégie globale, toutefois, votre bot doit être installé dans l’équipe avant de pouvoir envoyer un `channelId` message proactif à un canal.</span><span class="sxs-lookup"><span data-stu-id="d9366-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="d9366-138">Créer la conversation</span><span class="sxs-lookup"><span data-stu-id="d9366-138">Create the conversation</span></span>

<span data-ttu-id="d9366-139">Une fois que vous avez les informations de l’utilisateur ou du canal, vous devez créer la conversation si elle n’existe pas déjà ou si vous ne connaissez pas le `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="d9366-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="d9366-140">Vous ne devez créer la conversation qu’une seule fois et vous assurer de stocker la valeur ou `conversationId` l’objet à utiliser à `conversationReference` l’avenir.</span><span class="sxs-lookup"><span data-stu-id="d9366-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="d9366-141">Obtenir l’ID de conversation</span><span class="sxs-lookup"><span data-stu-id="d9366-141">Get the conversation ID</span></span>

<span data-ttu-id="d9366-142">Une fois la conversation créée, utilisez l’objet ou `conversationReference` pour `conversationId` envoyer le `tenantId` message.</span><span class="sxs-lookup"><span data-stu-id="d9366-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="d9366-143">Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n’importe quelle activité qui vous est envoyée à partir de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="d9366-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="d9366-144">Assurez-vous de stocker cet ID.</span><span class="sxs-lookup"><span data-stu-id="d9366-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="d9366-145">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="d9366-145">Send the message</span></span>

<span data-ttu-id="d9366-146">Maintenant que vous avez les bonnes informations d’adresse, vous pouvez envoyer votre message.</span><span class="sxs-lookup"><span data-stu-id="d9366-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="d9366-147">Si vous utilisez le SDK, vous le faites à l’aide de la méthode et pour effectuer un appel `continueConversation` `conversationId` `tenantId` d’API direct.</span><span class="sxs-lookup"><span data-stu-id="d9366-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="d9366-148">Vous devez définir correctement `conversationParameters` l’envoi de votre message.</span><span class="sxs-lookup"><span data-stu-id="d9366-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="d9366-149">Consultez la section [exemples](#examples) ou utilisez l’un des exemples répertoriés dans la section [exemples de](#code-samples) code.</span><span class="sxs-lookup"><span data-stu-id="d9366-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="d9366-150">Meilleures pratiques en matière de messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="d9366-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="d9366-151">L’envoi de messages proactifs aux utilisateurs est un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d9366-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="d9366-152">Toutefois, de leur point de vue, ce message peut apparaître complètement non improvisé et, dans le cas des messages de bienvenue, c’est la première fois qu’ils interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="d9366-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="d9366-153">Par conséquent, il est très important d’utiliser cette fonctionnalité avec parcimonie, de ne pas envoyer de courrier indésirable à vos utilisateurs et de fournir suffisamment d’informations pour que les utilisateurs comprennent pourquoi ils sont envoyés par message.</span><span class="sxs-lookup"><span data-stu-id="d9366-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="d9366-154">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="d9366-154">Welcome messages</span></span>

<span data-ttu-id="d9366-155">Lorsque vous utilisez une messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que, pour la plupart des personnes qui reçoivent le message, il n’existe aucun contexte pour la raison pour laquelle elles le reçoivent.</span><span class="sxs-lookup"><span data-stu-id="d9366-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="d9366-156">C’est également la première fois qu’ils interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="d9366-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="d9366-157">C’est l’occasion de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="d9366-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="d9366-158">Les meilleurs messages de bienvenue doivent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="d9366-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="d9366-159">**Pourquoi un utilisateur reçoit le message .**</span><span class="sxs-lookup"><span data-stu-id="d9366-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="d9366-160">Il doit être très clair pour l’utilisateur pourquoi il reçoit le message.</span><span class="sxs-lookup"><span data-stu-id="d9366-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="d9366-161">Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et éventuellement qui l’a installé.</span><span class="sxs-lookup"><span data-stu-id="d9366-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="d9366-162">**Que proposez-vous ?**</span><span class="sxs-lookup"><span data-stu-id="d9366-162">**What do you offer.**</span></span> <span data-ttu-id="d9366-163">Que peuvent-ils faire avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="d9366-163">What can they do with your app?</span></span> <span data-ttu-id="d9366-164">Quelle valeur pouvez-vous leur apporter ?</span><span class="sxs-lookup"><span data-stu-id="d9366-164">What value can you bring to them?</span></span>
* <span data-ttu-id="d9366-165">**Que doivent-ils faire ensuite ?**</span><span class="sxs-lookup"><span data-stu-id="d9366-165">**What should they do next.**</span></span> <span data-ttu-id="d9366-166">Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="d9366-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="d9366-167">N’oubliez pas que des messages d’accueil médiocres peuvent entraîner le blocage de votre bot par des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d9366-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="d9366-168">Passez beaucoup de temps à créer vos messages de bienvenue et à les itérer s’ils n’ont pas l’effet souhaité.</span><span class="sxs-lookup"><span data-stu-id="d9366-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="d9366-169">Les messages de notification</span><span class="sxs-lookup"><span data-stu-id="d9366-169">Notification messages</span></span>

<span data-ttu-id="d9366-170">Lorsque vous utilisez une messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin d’accès clair pour prendre des mesures communes en fonction de votre notification et comprendre clairement pourquoi la notification s’est produite.</span><span class="sxs-lookup"><span data-stu-id="d9366-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="d9366-171">Les messages de notification de bonne qualité sont généralement les suivants :</span><span class="sxs-lookup"><span data-stu-id="d9366-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="d9366-172">**Que s'est-il passé.**</span><span class="sxs-lookup"><span data-stu-id="d9366-172">**What happened.**</span></span> <span data-ttu-id="d9366-173">Indication claire de ce qui est arrivé à l’origine de la notification.</span><span class="sxs-lookup"><span data-stu-id="d9366-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="d9366-174">**Quel a été le résultat.**</span><span class="sxs-lookup"><span data-stu-id="d9366-174">**What was the result.**</span></span> <span data-ttu-id="d9366-175">Il doit être clair quel élément ou élément a été mis à jour pour provoquer la notification.</span><span class="sxs-lookup"><span data-stu-id="d9366-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="d9366-176">**Qui/ce qui l’a déclenché.**</span><span class="sxs-lookup"><span data-stu-id="d9366-176">**Who/what triggered it.**</span></span> <span data-ttu-id="d9366-177">Qui ou quelle action a été à l’origine de l’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="d9366-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="d9366-178">**Que peuvent faire les utilisateurs en réponse ?**</span><span class="sxs-lookup"><span data-stu-id="d9366-178">**What can users do in response.**</span></span> <span data-ttu-id="d9366-179">Faites en sorte que vos utilisateurs prennent facilement des mesures en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="d9366-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="d9366-180">**Comment les utilisateurs peuvent-ils refuser ?** Vous devez fournir un chemin d’accès pour que les utilisateurs ne choisissent pas d’autres notifications.</span><span class="sxs-lookup"><span data-stu-id="d9366-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="d9366-181">Messages programmés</span><span class="sxs-lookup"><span data-stu-id="d9366-181">Scheduled messages</span></span>

<span data-ttu-id="d9366-182">Lorsque vous utilisez une messagerie proactive pour envoyer des messages programmés aux utilisateurs, vérifiez que votre fuseau horaire est mis à jour vers leur fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="d9366-182">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="d9366-183">Cela garantit que les messages sont remis aux utilisateurs au moment approprié.</span><span class="sxs-lookup"><span data-stu-id="d9366-183">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="d9366-184">Les messages de planification incluent généralement :</span><span class="sxs-lookup"><span data-stu-id="d9366-184">Schedule messages generally include:</span></span>

* <span data-ttu-id="d9366-185">**Pourquoi l’utilisateur reçoit-il le message**: faites en sorte que vos utilisateurs comprennent facilement la raison pour laquelle ils reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="d9366-185">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="d9366-186">**Que peut faire l’utilisateur ensuite**: les utilisateurs peuvent prendre l’action requise en fonction du contenu du message.</span><span class="sxs-lookup"><span data-stu-id="d9366-186">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="d9366-187">Installer votre application de manière proactive à l’aide de Graph</span><span class="sxs-lookup"><span data-stu-id="d9366-187">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="d9366-188">L’installation proactive d’applications à l’aide de Microsoft Graph est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="d9366-188">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="d9366-189">Parfois, il peut être nécessaire de transmettre un message de manière proactive aux utilisateurs qui n’ont pas installé votre application ou n’ont pas interagi avec celle-ci précédemment.</span><span class="sxs-lookup"><span data-stu-id="d9366-189">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="d9366-190">Par exemple, vous souhaitez utiliser le communicateur [d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d9366-190">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="d9366-191">Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de l’événement que votre application reçoit lors de `conversationUpdate` l’installation.</span><span class="sxs-lookup"><span data-stu-id="d9366-191">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="d9366-192">Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d’applications d’organisation ou dans le magasin d’applications Teams.</span><span class="sxs-lookup"><span data-stu-id="d9366-192">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="d9366-193">Voir [Installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps) dans la documentation Graph, ainsi que l’installation et la messagerie proactives du bot dans Teams avec Microsoft [Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="d9366-193">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="d9366-194">Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) sur la plateforme GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9366-194">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="d9366-195">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9366-195">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d9366-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d9366-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="d9366-197">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="d9366-197">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="d9366-198">Python</span><span class="sxs-lookup"><span data-stu-id="d9366-198">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="d9366-199">JSON</span><span class="sxs-lookup"><span data-stu-id="d9366-199">JSON</span></span>](#tab/json)

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

<span data-ttu-id="d9366-200">Vous devez fournir l’ID d’utilisateur et l’ID de client.</span><span class="sxs-lookup"><span data-stu-id="d9366-200">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="d9366-201">Si l’appel réussit, l’API renvoie avec l’objet de réponse suivant.</span><span class="sxs-lookup"><span data-stu-id="d9366-201">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="d9366-202">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="d9366-202">Code samples</span></span>

<span data-ttu-id="d9366-203">Les exemples de messagerie proactive officiels sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d9366-203">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="d9366-204">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="d9366-204">Sample Name</span></span>           | <span data-ttu-id="d9366-205">Description</span><span class="sxs-lookup"><span data-stu-id="d9366-205">Description</span></span>                                                                      | <span data-ttu-id="d9366-206">.NET</span><span class="sxs-lookup"><span data-stu-id="d9366-206">.NET</span></span>    | <span data-ttu-id="d9366-207">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d9366-207">JavaScript</span></span>   | <span data-ttu-id="d9366-208">Python</span><span class="sxs-lookup"><span data-stu-id="d9366-208">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="d9366-209">Informations de base sur les conversations Teams</span><span class="sxs-lookup"><span data-stu-id="d9366-209">Teams Conversation Basics</span></span>  | <span data-ttu-id="d9366-210">Présente les principes de base des conversations dans Teams, notamment l’envoi de messages proactifs un-à-un.</span><span class="sxs-lookup"><span data-stu-id="d9366-210">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="d9366-211">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="d9366-211">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="d9366-212">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d9366-212">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="d9366-213">Python</span><span class="sxs-lookup"><span data-stu-id="d9366-213">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="d9366-214">Démarrer un nouveau thread dans un canal</span><span class="sxs-lookup"><span data-stu-id="d9366-214">Start new thread in a channel</span></span>     | <span data-ttu-id="d9366-215">Illustre la création d’un thread dans un canal.</span><span class="sxs-lookup"><span data-stu-id="d9366-215">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="d9366-216">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="d9366-216">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="d9366-217">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d9366-217">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="d9366-218">Python</span><span class="sxs-lookup"><span data-stu-id="d9366-218">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="d9366-219">Afficher des exemples de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d9366-219">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d9366-220">**Exemples de code de messagerie proactive Teams**</span><span class="sxs-lookup"><span data-stu-id="d9366-220">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
