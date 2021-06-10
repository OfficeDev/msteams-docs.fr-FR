---
title: Messages proactifs
description: Décrit les bots qui peuvent démarrer une conversation dans Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: scénarios teams de bot de conversation de messagerie proactive
ms.openlocfilehash: 82282c4e2a2d48acad8f4bb384976906296be8f9
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630466"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="132bb-104">Messagerie proactive pour les bots</span><span class="sxs-lookup"><span data-stu-id="132bb-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="132bb-105">Un message proactif est un message envoyé par un bot pour démarrer une conversation.</span><span class="sxs-lookup"><span data-stu-id="132bb-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="132bb-106">Vous voudrez peut-être que votre bot démarre une conversation pour diverses raisons, notamment :</span><span class="sxs-lookup"><span data-stu-id="132bb-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="132bb-107">Messages de bienvenue pour les conversations de bot personnels.</span><span class="sxs-lookup"><span data-stu-id="132bb-107">Welcome messages for personal bot conversations.</span></span>
* <span data-ttu-id="132bb-108">Réponses aux sondages.</span><span class="sxs-lookup"><span data-stu-id="132bb-108">Poll responses.</span></span>
* <span data-ttu-id="132bb-109">Notifications d’événements externes.</span><span class="sxs-lookup"><span data-stu-id="132bb-109">External event notifications.</span></span>

<span data-ttu-id="132bb-110">L’envoi d’un message pour démarrer un nouveau thread de conversation est différent de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot démarre une nouvelle conversation, il n’y a aucune conversation pré-existante vers qui publier le message.</span><span class="sxs-lookup"><span data-stu-id="132bb-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="132bb-111">Pour envoyer un message proactif, vous devez :</span><span class="sxs-lookup"><span data-stu-id="132bb-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="132bb-112">Décider de ce que vous allez dire</span><span class="sxs-lookup"><span data-stu-id="132bb-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="132bb-113">Obtenir l’ID unique et l’ID client de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="132bb-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="132bb-114">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="132bb-114">Send the message</span></span>](#examples)

<span data-ttu-id="132bb-115">Lorsque vous créez des messages proactifs, vous devez appeler et transmettre l’URL du service avant de créer le message que vous utiliserez pour envoyer le  `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` message.</span><span class="sxs-lookup"><span data-stu-id="132bb-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="132bb-116">Si ce n’est pas le cas, votre application reçoit une `401: Unauthorized` réponse.</span><span class="sxs-lookup"><span data-stu-id="132bb-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="132bb-117">Pour plus d’informations, [voir les exemples ci-dessous.](#net-example-from-this-sample)</span><span class="sxs-lookup"><span data-stu-id="132bb-117">For more information, see [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="132bb-118">Meilleures pratiques en matière de messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="132bb-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="132bb-119">L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="132bb-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="132bb-120">Toutefois, de leur point de vue, ce message peut leur sembler totalement non improvisé et, dans le cas des messages de bienvenue, il s’agit de la première fois qu’ils interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="132bb-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="132bb-121">En tant que tel, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas envoyer de courrier indésirable à vos utilisateurs) et de leur fournir suffisamment d’informations pour leur faire comprendre pourquoi ils sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="132bb-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="132bb-122">Les messages proactifs sont généralement classés en deux catégories : les messages de bienvenue ou les messages de notification.</span><span class="sxs-lookup"><span data-stu-id="132bb-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="132bb-123">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="132bb-123">Welcome messages</span></span>

<span data-ttu-id="132bb-124">Lorsque vous utilisez une messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que pour la plupart des personnes qui reçoivent le message, elles n’ont aucun contexte pour la raison pour laquelle elles le reçoivent.</span><span class="sxs-lookup"><span data-stu-id="132bb-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="132bb-125">C’est également la première fois qu’ils interagissent avec votre application . c’est l’occasion de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="132bb-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="132bb-126">Les meilleurs messages de bienvenue sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="132bb-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="132bb-127">**Pourquoi reçoivent-ils ce message ?**</span><span class="sxs-lookup"><span data-stu-id="132bb-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="132bb-128">Il doit être très clair pour l’utilisateur pourquoi il reçoit le message.</span><span class="sxs-lookup"><span data-stu-id="132bb-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="132bb-129">Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et éventuellement qui l’a installé.</span><span class="sxs-lookup"><span data-stu-id="132bb-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="132bb-130">**Que proposez-vous ?**</span><span class="sxs-lookup"><span data-stu-id="132bb-130">**What do you offer.**</span></span> <span data-ttu-id="132bb-131">Que peuvent-ils faire avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="132bb-131">What can they do with your app?</span></span> <span data-ttu-id="132bb-132">Quelle valeur pouvez-vous leur apporter ?</span><span class="sxs-lookup"><span data-stu-id="132bb-132">What value can you bring to them?</span></span>
* <span data-ttu-id="132bb-133">**Que doivent-ils faire ensuite ?**</span><span class="sxs-lookup"><span data-stu-id="132bb-133">**What should they do next.**</span></span> <span data-ttu-id="132bb-134">Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="132bb-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="132bb-135">Les messages de notification</span><span class="sxs-lookup"><span data-stu-id="132bb-135">Notification messages</span></span>

<span data-ttu-id="132bb-136">Lorsque vous utilisez une messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin d’accès clair pour effectuer des actions courantes en fonction de votre notification et comprendre clairement pourquoi la notification s’est produite.</span><span class="sxs-lookup"><span data-stu-id="132bb-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="132bb-137">Les messages de notification de bonne qualité incluent généralement :</span><span class="sxs-lookup"><span data-stu-id="132bb-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="132bb-138">**Que s'est-il passé.**</span><span class="sxs-lookup"><span data-stu-id="132bb-138">**What happened.**</span></span> <span data-ttu-id="132bb-139">Indication claire de la cause de la notification.</span><span class="sxs-lookup"><span data-stu-id="132bb-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="132bb-140">**Qu’est-ce qu’il s’est passé ?**</span><span class="sxs-lookup"><span data-stu-id="132bb-140">**What it happened to.**</span></span> <span data-ttu-id="132bb-141">Il doit être clair quel élément/élément a été mis à jour pour provoquer la notification.</span><span class="sxs-lookup"><span data-stu-id="132bb-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="132bb-142">**Qui l’a fait.**</span><span class="sxs-lookup"><span data-stu-id="132bb-142">**Who did it.**</span></span> <span data-ttu-id="132bb-143">Qui l’action à l’origine de l’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="132bb-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="132bb-144">**Ce qu’ils peuvent faire à ce sujet.**</span><span class="sxs-lookup"><span data-stu-id="132bb-144">**What they can do about it.**</span></span> <span data-ttu-id="132bb-145">Faites en sorte que vos utilisateurs prennent facilement des mesures en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="132bb-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="132bb-146">**Comment ils peuvent refuser.** Vous devez fournir un chemin d’accès aux utilisateurs pour qu’ils ne choisissent pas d’autres notifications.</span><span class="sxs-lookup"><span data-stu-id="132bb-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="132bb-147">Obtenir les informations utilisateur nécessaires</span><span class="sxs-lookup"><span data-stu-id="132bb-147">Obtain necessary user information</span></span>

<span data-ttu-id="132bb-148">Les bots peuvent créer des conversations avec un utilisateur Microsoft Teams en obtenant *l’ID unique* et l’ID *client de l’utilisateur.*</span><span class="sxs-lookup"><span data-stu-id="132bb-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="132bb-149">Vous pouvez obtenir ces valeurs à l’aide de l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="132bb-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="132bb-150">En [extraire la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) à partir d’un canal où votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="132bb-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="132bb-151">En les mettre en cache lorsqu’un utilisateur [interagit avec votre bot dans un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)</span><span class="sxs-lookup"><span data-stu-id="132bb-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="132bb-152">Lorsqu’un utilisateur est @mentioned dans une conversation de [canal,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) le bot fait partie de.</span><span class="sxs-lookup"><span data-stu-id="132bb-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="132bb-153">En les mettre [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) en cache lorsque vous recevez l’événement lorsque votre application est installée dans une étendue personnelle, ou que de nouveaux membres sont ajoutés à une conversation de canal ou de groupe qui.</span><span class="sxs-lookup"><span data-stu-id="132bb-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that.</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="132bb-154">Installer votre application de manière proactive à l’aide Graph</span><span class="sxs-lookup"><span data-stu-id="132bb-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="132bb-155">L’installation proactive d’applications à l’aide d’un graphique est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="132bb-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="132bb-156">Parfois, il peut être nécessaire de transmettre un message de manière proactive aux utilisateurs qui n’ont pas installé votre application ou n’ont pas interagi avec celle-ci précédemment.</span><span class="sxs-lookup"><span data-stu-id="132bb-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="132bb-157">Par exemple, vous souhaitez utiliser le communicateur [d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="132bb-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="132bb-158">Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de l’événement que votre application recevra lors de `conversationUpdate` l’installation.</span><span class="sxs-lookup"><span data-stu-id="132bb-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="132bb-159">Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d’applications d’organisation ou dans Teams’application store.</span><span class="sxs-lookup"><span data-stu-id="132bb-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="132bb-160">Pour plus [d’informations,](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) voir Installer des applications pour les utilisateurs Graph documentation.</span><span class="sxs-lookup"><span data-stu-id="132bb-160">See [Install apps for users](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) in the Graph documentation for complete details.</span></span> <span data-ttu-id="132bb-161">Il existe également un [exemple dans .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="132bb-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="132bb-162">Exemples</span><span class="sxs-lookup"><span data-stu-id="132bb-162">Examples</span></span>

<span data-ttu-id="132bb-163">Veillez à vous authentifier et à avoir un jeton de support avant de créer une conversation à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="132bb-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="132bb-164">Vous devez fournir l’ID d’utilisateur et l’ID de client.</span><span class="sxs-lookup"><span data-stu-id="132bb-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="132bb-165">Si l’appel réussit, l’API renvoie avec l’objet de réponse suivant.</span><span class="sxs-lookup"><span data-stu-id="132bb-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="132bb-166">Cet ID est l’ID de conversation unique de la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="132bb-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="132bb-167">Stockez cette valeur et réutilisez-la pour les interactions futures avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="132bb-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="132bb-168">Utilisation de .NET</span><span class="sxs-lookup"><span data-stu-id="132bb-168">Using .NET</span></span>

<span data-ttu-id="132bb-169">Cet exemple utilise le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="132bb-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="132bb-170">Utilisation de Node.js</span><span class="sxs-lookup"><span data-stu-id="132bb-170">Using Node.js</span></span>

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

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="132bb-171">Créer une conversation de canal</span><span class="sxs-lookup"><span data-stu-id="132bb-171">Creating a channel conversation</span></span>

<span data-ttu-id="132bb-172">Le bot de votre équipe peut créer une chaîne de réponse dans un canal.</span><span class="sxs-lookup"><span data-stu-id="132bb-172">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="132bb-173">Si vous utilisez le SDK Node.js Teams, utilisez une adresse complète avec l’ID d’activité et `startReplyChain()` l’ID de conversation corrects. Si vous utilisez C#, consultez l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="132bb-173">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="132bb-174">Vous pouvez également utiliser l’API REST et émettre une demande POST à la [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ressource.</span><span class="sxs-lookup"><span data-stu-id="132bb-174">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="132bb-175">Exemple .NET (à partir [de cet exemple)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="132bb-175">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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

## <a name="see-also"></a><span data-ttu-id="132bb-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="132bb-176">See also</span></span>

[<span data-ttu-id="132bb-177">Exemples Bot Framework</span><span class="sxs-lookup"><span data-stu-id="132bb-177">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
