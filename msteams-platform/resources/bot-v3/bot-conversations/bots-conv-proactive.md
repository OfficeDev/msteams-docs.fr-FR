---
title: Messages proactifs
description: Décrit bots peuvent commencer une conversation dans Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: équipes scénarios proactives messagerie conversation bot
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566788"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="01a9c-104">Messagerie proactive pour les bots</span><span class="sxs-lookup"><span data-stu-id="01a9c-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="01a9c-105">Un message proactif est un message qui est envoyé par un bot pour démarrer une conversation.</span><span class="sxs-lookup"><span data-stu-id="01a9c-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="01a9c-106">Vous voudrez peut-être que votre bot démarre une conversation pour diverses raisons, notamment :</span><span class="sxs-lookup"><span data-stu-id="01a9c-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="01a9c-107">Messages de bienvenue pour les conversations personnelles bot.</span><span class="sxs-lookup"><span data-stu-id="01a9c-107">Welcome messages for personal bot conversations.</span></span>
* <span data-ttu-id="01a9c-108">Réponses au sondage.</span><span class="sxs-lookup"><span data-stu-id="01a9c-108">Poll responses.</span></span>
* <span data-ttu-id="01a9c-109">Notifications d’événements externes.</span><span class="sxs-lookup"><span data-stu-id="01a9c-109">External event notifications.</span></span>

<span data-ttu-id="01a9c-110">Envoyer un message pour démarrer un nouveau thread de conversation est différent de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot commence une nouvelle conversation, il n’y a pas de conversation préexistant pour poster le message.</span><span class="sxs-lookup"><span data-stu-id="01a9c-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="01a9c-111">Afin d’envoyer un message proactif, vous devez :</span><span class="sxs-lookup"><span data-stu-id="01a9c-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="01a9c-112">Décidez ce que vous allez dire</span><span class="sxs-lookup"><span data-stu-id="01a9c-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="01a9c-113">Obtenez l’id unique de l’utilisateur et l’id du locataire</span><span class="sxs-lookup"><span data-stu-id="01a9c-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="01a9c-114">Envoyer le message</span><span class="sxs-lookup"><span data-stu-id="01a9c-114">Send the message</span></span>](#examples)

<span data-ttu-id="01a9c-115">Lors de la  création de messages `MicrosoftAppCredentials.TrustServiceUrl` proactifs, vous devez appeler et passer dans l’URL du service avant de `ConnectorClient` créer le que vous utiliserez pour envoyer le message.</span><span class="sxs-lookup"><span data-stu-id="01a9c-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="01a9c-116">Si vous ne le faites pas, votre application recevra une `401: Unauthorized` réponse.</span><span class="sxs-lookup"><span data-stu-id="01a9c-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="01a9c-117">Pour plus d’informations, voir [les échantillons ci-dessous](#net-example-from-this-sample).</span><span class="sxs-lookup"><span data-stu-id="01a9c-117">For more information, see [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="01a9c-118">Meilleures pratiques pour la messagerie proactive</span><span class="sxs-lookup"><span data-stu-id="01a9c-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="01a9c-119">L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="01a9c-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="01a9c-120">Toutefois, de leur point de vue, ce message peut sembler leur venir complètement sans lempt, et dans le cas des messages de bienvenue sera la première fois qu’ils ont interagi avec votre application.</span><span class="sxs-lookup"><span data-stu-id="01a9c-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="01a9c-121">En tant que tel, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas spam vos utilisateurs), et de leur fournir suffisamment d’informations pour leur faire comprendre pourquoi ils sont messages.</span><span class="sxs-lookup"><span data-stu-id="01a9c-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="01a9c-122">Les messages proactifs sont généralement classés en deux catégories : les messages de bienvenue ou les messages de notification.</span><span class="sxs-lookup"><span data-stu-id="01a9c-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="01a9c-123">Les messages de bienvenue</span><span class="sxs-lookup"><span data-stu-id="01a9c-123">Welcome messages</span></span>

<span data-ttu-id="01a9c-124">Lorsque vous utilisez la messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que pour la plupart des personnes recevant le message, ils n’auront aucun contexte pour expliquer pourquoi ils le reçoivent.</span><span class="sxs-lookup"><span data-stu-id="01a9c-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="01a9c-125">C’est aussi la première fois qu’ils interagissent avec votre application; c’est l’occasion de créer une bonne première impression.</span><span class="sxs-lookup"><span data-stu-id="01a9c-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="01a9c-126">Les meilleurs messages de bienvenue seront les suivants :</span><span class="sxs-lookup"><span data-stu-id="01a9c-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="01a9c-127">**Pourquoi reçoivent-ils ce message?**</span><span class="sxs-lookup"><span data-stu-id="01a9c-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="01a9c-128">Il devrait être très clair pour l’utilisateur pourquoi ils reçoivent le message.</span><span class="sxs-lookup"><span data-stu-id="01a9c-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="01a9c-129">Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et potentiellement qui l’a installé.</span><span class="sxs-lookup"><span data-stu-id="01a9c-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="01a9c-130">**Qu’est-ce que tu offres?**</span><span class="sxs-lookup"><span data-stu-id="01a9c-130">**What do you offer.**</span></span> <span data-ttu-id="01a9c-131">Que peuvent-ils faire avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="01a9c-131">What can they do with your app?</span></span> <span data-ttu-id="01a9c-132">Quelle valeur pouvez-vous leur apporter?</span><span class="sxs-lookup"><span data-stu-id="01a9c-132">What value can you bring to them?</span></span>
* <span data-ttu-id="01a9c-133">**Que devraient-ils faire ensuite?**</span><span class="sxs-lookup"><span data-stu-id="01a9c-133">**What should they do next.**</span></span> <span data-ttu-id="01a9c-134">Invitez-les à essayer une commande ou à interagir d’une manière ou d’une autre avec votre application.</span><span class="sxs-lookup"><span data-stu-id="01a9c-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="01a9c-135">Les messages de notification</span><span class="sxs-lookup"><span data-stu-id="01a9c-135">Notification messages</span></span>

<span data-ttu-id="01a9c-136">Lorsque vous utilisez la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin clair pour prendre des mesures communes basées sur votre notification, et une compréhension claire des raisons pour lesquelles la notification s’est produite.</span><span class="sxs-lookup"><span data-stu-id="01a9c-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="01a9c-137">Les bons messages de notification incluent généralement :</span><span class="sxs-lookup"><span data-stu-id="01a9c-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="01a9c-138">**Que s'est-il passé?.**</span><span class="sxs-lookup"><span data-stu-id="01a9c-138">**What happened.**</span></span> <span data-ttu-id="01a9c-139">Une indication claire de ce qui s’est passé pour causer la notification.</span><span class="sxs-lookup"><span data-stu-id="01a9c-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="01a9c-140">**Ce qu’il est arrivé à.**</span><span class="sxs-lookup"><span data-stu-id="01a9c-140">**What it happened to.**</span></span> <span data-ttu-id="01a9c-141">Il devrait être clair quel élément / chose a été mis à jour pour causer la notification.</span><span class="sxs-lookup"><span data-stu-id="01a9c-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="01a9c-142">**Qui l’ai fait.**</span><span class="sxs-lookup"><span data-stu-id="01a9c-142">**Who did it.**</span></span> <span data-ttu-id="01a9c-143">Qui pris les mesures qui ont causé l’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="01a9c-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="01a9c-144">**Ce qu’ils peuvent faire.**</span><span class="sxs-lookup"><span data-stu-id="01a9c-144">**What they can do about it.**</span></span> <span data-ttu-id="01a9c-145">Facilitez la prise de mesures par vos utilisateurs en fonction de vos notifications.</span><span class="sxs-lookup"><span data-stu-id="01a9c-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="01a9c-146">**Comment ils peuvent se retirer.** Vous devez fournir un chemin pour que les utilisateurs se retirent des notifications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="01a9c-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="01a9c-147">Obtenir les informations nécessaires sur les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="01a9c-147">Obtain necessary user information</span></span>

<span data-ttu-id="01a9c-148">Bots peut créer de nouvelles conversations avec un utilisateur Microsoft Teams en obtenant l’identifiant unique de *l’utilisateur et l’iD* du *locataire.*</span><span class="sxs-lookup"><span data-stu-id="01a9c-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="01a9c-149">Vous pouvez obtenir ces valeurs en utilisant l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="01a9c-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="01a9c-150">En [récupérant la liste d’équipe à](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) partir d’un canal dans qui votre application est installée.</span><span class="sxs-lookup"><span data-stu-id="01a9c-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="01a9c-151">En les tafonant lorsqu’un [utilisateur interagit avec votre bot dans un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)</span><span class="sxs-lookup"><span data-stu-id="01a9c-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="01a9c-152">Lorsqu’un @mentioned [dans une conversation de](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) canal, le bot fait partie de.</span><span class="sxs-lookup"><span data-stu-id="01a9c-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="01a9c-153">En les caching lorsque vous [recevez l’événement `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) lorsque votre application est installée dans une portée personnelle, ou de nouveaux membres sont ajoutés à un canal ou un chat de groupe qui.</span><span class="sxs-lookup"><span data-stu-id="01a9c-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that.</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="01a9c-154">Installez proactivement votre application à l’aide Graph</span><span class="sxs-lookup"><span data-stu-id="01a9c-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="01a9c-155">L’installation proactive d’applications à l’aide d’un graphique est actuellement en version bêta.</span><span class="sxs-lookup"><span data-stu-id="01a9c-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="01a9c-156">Parfois, il peut être nécessaire de transmettre des messages proactifs aux utilisateurs qui n’ont pas installé ou interagi avec votre application auparavant.</span><span class="sxs-lookup"><span data-stu-id="01a9c-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="01a9c-157">Par exemple, vous souhaitez utiliser le communicateur de [l’entreprise pour envoyer](~/samples/app-templates.md#company-communicator) des messages à l’ensemble de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="01a9c-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="01a9c-158">Pour ce scénario, vous pouvez utiliser l’API Graph pour installer proactivement votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de `conversationUpdate` l’événement que votre application recevra lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="01a9c-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="01a9c-159">Vous ne pouvez installer que des applications qui se trouvent dans votre catalogue d’applications organisationnelles ou dans Teams’App Store.</span><span class="sxs-lookup"><span data-stu-id="01a9c-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="01a9c-160">Voir [Installer des applications pour les utilisateurs](/graph/teams-proactive-messaging) dans la documentation Graph pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="01a9c-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="01a9c-161">Il ya aussi un [échantillon dans .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span><span class="sxs-lookup"><span data-stu-id="01a9c-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="01a9c-162">Exemples</span><span class="sxs-lookup"><span data-stu-id="01a9c-162">Examples</span></span>

<span data-ttu-id="01a9c-163">Assurez-vous que vous authentifiez et avez un jeton porteur avant de créer une nouvelle conversation à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="01a9c-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="01a9c-164">Vous devez fournir l’identifiant de l’utilisateur et l’identifiant du locataire.</span><span class="sxs-lookup"><span data-stu-id="01a9c-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="01a9c-165">Si l’appel réussit, l’API revient avec l’objet de réponse suivant.</span><span class="sxs-lookup"><span data-stu-id="01a9c-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="01a9c-166">Cet ID est l’iD de conversation unique du chat personnel.</span><span class="sxs-lookup"><span data-stu-id="01a9c-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="01a9c-167">Veuillez stocker cette valeur et la réutiliser pour les interactions futures avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01a9c-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="01a9c-168">Utilisation de .NET</span><span class="sxs-lookup"><span data-stu-id="01a9c-168">Using .NET</span></span>

<span data-ttu-id="01a9c-169">Cet exemple utilise le [paquet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="01a9c-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="01a9c-170">Utilisation de Node.js</span><span class="sxs-lookup"><span data-stu-id="01a9c-170">Using Node.js</span></span>

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

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="01a9c-171">Créer une conversation de canal</span><span class="sxs-lookup"><span data-stu-id="01a9c-171">Creating a channel conversation</span></span>

<span data-ttu-id="01a9c-172">Le bot de votre équipe peut créer une chaîne de réponse dans un canal.</span><span class="sxs-lookup"><span data-stu-id="01a9c-172">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="01a9c-173">Si vous utilisez le SDK Node.js Teams, utilisez-le qui `startReplyChain()` vous donne une adresse entièrement remplie avec l’id d’activité correct et l’id de conversation. Si vous utilisez C#, voir l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="01a9c-173">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="01a9c-174">Vous pouvez également utiliser l’API REST et émettre une demande POST de [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ressources.</span><span class="sxs-lookup"><span data-stu-id="01a9c-174">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="01a9c-175">Exemple .NET (à partir [de cet échantillon)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="01a9c-175">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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

## <a name="see-also"></a><span data-ttu-id="01a9c-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="01a9c-176">See also</span></span>

[<span data-ttu-id="01a9c-177">Échantillons de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="01a9c-177">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)