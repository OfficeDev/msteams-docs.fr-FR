---
title: Messages proactifs
description: Décrit les robots pouvant démarrer une conversation dans Microsoft teams
keywords: scénarios de teams robot de conversation de messagerie proactive
ms.openlocfilehash: 2f644820da33acc885a7972b13a1f61c167d6d8f
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228065"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="70561-104">Messagerie proactive pour les robots</span><span class="sxs-lookup"><span data-stu-id="70561-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="70561-105">Un message proactif est un message qui est envoyé par un bot pour démarrer une conversation.</span><span class="sxs-lookup"><span data-stu-id="70561-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="70561-106">Vous souhaiterez peut-être que votre bot entame une conversation pour plusieurs raisons, notamment :</span><span class="sxs-lookup"><span data-stu-id="70561-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="70561-107">Messages de bienvenue pour les conversations personnelles de robots</span><span class="sxs-lookup"><span data-stu-id="70561-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="70561-108">Interrogation des réponses</span><span class="sxs-lookup"><span data-stu-id="70561-108">Poll responses</span></span>
* <span data-ttu-id="70561-109">Notifications d’événements externes</span><span class="sxs-lookup"><span data-stu-id="70561-109">External event notifications</span></span>

<span data-ttu-id="70561-110">L’envoi d’un message pour démarrer un nouveau thème de conversation est différent de celui de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot démarre une nouvelle conversation, il n’existe pas de conversation préexistante vers laquelle publier le message.</span><span class="sxs-lookup"><span data-stu-id="70561-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="70561-111">Pour envoyer un message proactif, vous devez :</span><span class="sxs-lookup"><span data-stu-id="70561-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="70561-112">Décider de ce que vous allez dire</span><span class="sxs-lookup"><span data-stu-id="70561-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="70561-113">Obtenir l’ID unique et l’ID de client uniques de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="70561-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="70561-114">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="70561-114">Send the message</span></span>](#examples)

<span data-ttu-id="70561-115">Lors de la création de messages proactifs que vous **devez** appeler `MicrosoftAppCredentials.TrustServiceUrl`, et transmettre l' `ConnectorClient` URL du service avant de créer le message que vous allez utiliser pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="70561-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="70561-116">Si vous ne le faites pas, votre application recevra une `401: Unauthorized` réponse.</span><span class="sxs-lookup"><span data-stu-id="70561-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="70561-117">Consultez [les exemples ci-dessous](#net-example-from-this-sample).</span><span class="sxs-lookup"><span data-stu-id="70561-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="70561-118">Meilleures pratiques pour la messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="70561-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="70561-119">L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="70561-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="70561-120">Toutefois, à partir de leur perspective, ce message peut sembler indésirable et, dans le cas de messages de bienvenue, il s’agit de la première fois qu’ils interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="70561-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="70561-121">Par conséquent, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas envoyer de courrier indésirable) et de leur fournir suffisamment d’informations pour les informer de la raison pour laquelle ils reçoivent des messages.</span><span class="sxs-lookup"><span data-stu-id="70561-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="70561-122">Les messages proactifs font généralement partie de l’une des deux catégories suivantes : messages d’accueil ou notifications.</span><span class="sxs-lookup"><span data-stu-id="70561-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="70561-123">Messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="70561-123">Welcome messages</span></span>

<span data-ttu-id="70561-124">Lors de l’utilisation de la messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que pour la plupart des personnes qui reçoivent le message, il n’y aura pas de contexte pour la raison pour laquelle ils le reçoivent.</span><span class="sxs-lookup"><span data-stu-id="70561-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="70561-125">Il s’agit également de la première fois qu’ils interagissent avec votre application ; Il s’agit de votre opportunité de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="70561-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="70561-126">Les meilleurs messages d’accueil sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="70561-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="70561-127">**Pourquoi reçoit-il ce message ?**</span><span class="sxs-lookup"><span data-stu-id="70561-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="70561-128">Il doit être très clair que les utilisateurs reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="70561-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="70561-129">Si votre robot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, indiquez-lui quel canal il a été installé et éventuellement qui l’a installé.</span><span class="sxs-lookup"><span data-stu-id="70561-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="70561-130">**Ce que vous proposez.**</span><span class="sxs-lookup"><span data-stu-id="70561-130">**What do you offer.**</span></span> <span data-ttu-id="70561-131">Qu’est-il possible de faire avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="70561-131">What can they do with your app?</span></span> <span data-ttu-id="70561-132">Quelle valeur pouvez-vous leur apporter ?</span><span class="sxs-lookup"><span data-stu-id="70561-132">What value can you bring to them?</span></span>
* <span data-ttu-id="70561-133">**Que dois-je faire ensuite ?**</span><span class="sxs-lookup"><span data-stu-id="70561-133">**What should they do next.**</span></span> <span data-ttu-id="70561-134">Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="70561-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="70561-135">Messages de notification</span><span class="sxs-lookup"><span data-stu-id="70561-135">Notification messages</span></span>

<span data-ttu-id="70561-136">Lors de l’utilisation de la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs disposent d’un chemin d’accès clair afin de prendre des mesures courantes en fonction de votre notification et de bien comprendre la raison pour laquelle la notification s’est produite.</span><span class="sxs-lookup"><span data-stu-id="70561-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="70561-137">Les messages de notification valides sont généralement les suivants :</span><span class="sxs-lookup"><span data-stu-id="70561-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="70561-138">**Que s'est-il passé.**</span><span class="sxs-lookup"><span data-stu-id="70561-138">**What happened.**</span></span> <span data-ttu-id="70561-139">Indication claire de l’origine de la notification.</span><span class="sxs-lookup"><span data-stu-id="70561-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="70561-140">**Ce qu’il y a eu.**</span><span class="sxs-lookup"><span data-stu-id="70561-140">**What it happened to.**</span></span> <span data-ttu-id="70561-141">Il doit être clair quel élément/élément a été mis à jour pour déclencher la notification.</span><span class="sxs-lookup"><span data-stu-id="70561-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="70561-142">**Qui a fait ça.**</span><span class="sxs-lookup"><span data-stu-id="70561-142">**Who did it.**</span></span> <span data-ttu-id="70561-143">Qui a effectué l’action qui a provoqué l’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="70561-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="70561-144">**Ce qu’ils peuvent faire.**</span><span class="sxs-lookup"><span data-stu-id="70561-144">**What they can do about it.**</span></span> <span data-ttu-id="70561-145">Permettre aux utilisateurs de prendre facilement des mesures en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="70561-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="70561-146">**Comment les désactiver.** Vous devez fournir un chemin d’accès permettant aux utilisateurs de désactiver les notifications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="70561-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="70561-147">Obtenir les informations utilisateur nécessaires</span><span class="sxs-lookup"><span data-stu-id="70561-147">Obtain necessary user information</span></span>

<span data-ttu-id="70561-148">Les robots peuvent créer de nouvelles conversations avec un utilisateur individuel de Microsoft teams en obtenant l’ID *unique* et l' *ID de client* de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="70561-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user’s *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="70561-149">Vous pouvez obtenir ces valeurs à l’aide de l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="70561-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="70561-150">En [extrayant la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) à partir d’un canal dans lequel votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="70561-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="70561-151">En les mettant en cache lorsqu’un utilisateur [interagit avec votre robot dans un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span><span class="sxs-lookup"><span data-stu-id="70561-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="70561-152">Lorsqu’un utilisateur est [@mentioned dans une conversation de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) dont le robot fait partie.</span><span class="sxs-lookup"><span data-stu-id="70561-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="70561-153">En les mettant en cache lorsque vous [recevez l' `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) événement lorsque votre application est installée dans une étendue personnelle, ou que de nouveaux membres sont ajoutés à un canal ou à une conversation de groupe qui</span><span class="sxs-lookup"><span data-stu-id="70561-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="70561-154">Installer de manière proactive votre application à l’aide de Graph</span><span class="sxs-lookup"><span data-stu-id="70561-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="70561-155">L’installation proactive d’applications à l’aide de Graph est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="70561-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="70561-156">Parfois, il peut s’avérer nécessaire de messageer de manière proactive les utilisateurs qui n’ont pas installé ou interagi avec votre application précédemment.</span><span class="sxs-lookup"><span data-stu-id="70561-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="70561-157">Par exemple, vous souhaitez utiliser l' [entreprise Communicator](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="70561-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="70561-158">Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs `conversationUpdate` nécessaires à partir de l’événement que votre application recevra lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="70561-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="70561-159">Vous ne pouvez installer que les applications figurant dans le catalogue d’applications de votre organisation ou dans le magasin d’applications Teams.</span><span class="sxs-lookup"><span data-stu-id="70561-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="70561-160">Pour plus d’informations, consultez la rubrique [installer des applications pour les utilisateurs](/graph/teams-proactive-messaging) dans la documentation Graph.</span><span class="sxs-lookup"><span data-stu-id="70561-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="70561-161">Il existe également un [exemple dans .net](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="70561-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="70561-162">Exemples</span><span class="sxs-lookup"><span data-stu-id="70561-162">Examples</span></span>

<span data-ttu-id="70561-163">Assurez-vous d’authentifier et de posséder un jeton de support avant de créer une conversation à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="70561-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="70561-164">Vous devez fournir l’ID d’utilisateur et l’ID de client.</span><span class="sxs-lookup"><span data-stu-id="70561-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="70561-165">Si l’appel réussit, l’API renvoie avec l’objet de réponse suivant.</span><span class="sxs-lookup"><span data-stu-id="70561-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="70561-166">Cet ID est l’ID de conversation unique de la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="70561-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="70561-167">Veuillez stocker cette valeur et la réutiliser pour les futures interactions avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="70561-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="70561-168">Utilisation de .NET</span><span class="sxs-lookup"><span data-stu-id="70561-168">Using .NET</span></span>

<span data-ttu-id="70561-169">Cet exemple utilise le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="70561-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a><span data-ttu-id="70561-170">Utilisation de node. js</span><span class="sxs-lookup"><span data-stu-id="70561-170">Using Node.js</span></span>

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

<span data-ttu-id="70561-171">*Voir aussi* [exemples de robots d’infrastructure](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="70561-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="70561-172">Création d’une conversation de canal</span><span class="sxs-lookup"><span data-stu-id="70561-172">Creating a channel conversation</span></span>

<span data-ttu-id="70561-173">Votre robot ajouté en équipe peut effectuer des publications dans un canal pour créer une chaîne de réponse.</span><span class="sxs-lookup"><span data-stu-id="70561-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="70561-174">Si vous utilisez le kit de développement logiciel (SDK) node `startReplyChain()` . js Teams, utilisez qui vous fournit une adresse complète avec l’ID d’activité et l’ID de conversation corrects. Si vous utilisez C#, consultez l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="70561-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="70561-175">Vous pouvez également utiliser l’API REST et émettre une requête POST à [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) la ressource.</span><span class="sxs-lookup"><span data-stu-id="70561-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="70561-176">Exemple .NET (de [cet exemple](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span><span class="sxs-lookup"><span data-stu-id="70561-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```
