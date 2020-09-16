---
title: Concepts de base d’une conversation
author: clearab
description: Comment effectuer une conversation avec un robot Microsoft teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc016a8f0dcce474f80898dc93e309692ba20471
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819052"
---
# <a name="conversation-basics"></a><span data-ttu-id="592a1-103">Concepts de base d’une conversation</span><span class="sxs-lookup"><span data-stu-id="592a1-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="592a1-104">Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="592a1-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="592a1-105">Il existe trois types de conversations (ou portées) dans Teams :</span><span class="sxs-lookup"><span data-stu-id="592a1-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="592a1-106">`teams` Également appelés conversations de canal, visibles par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="592a1-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="592a1-107">`personal` Les conversations entre les robots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="592a1-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="592a1-108">`groupChat` Conversation entre un bot et deux utilisateurs ou plus.</span><span class="sxs-lookup"><span data-stu-id="592a1-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="592a1-109">Active également votre robot dans les conversations de réunion.</span><span class="sxs-lookup"><span data-stu-id="592a1-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="592a1-110">Un bot se comporte de manière légèrement différente en fonction du type de conversation impliquée :</span><span class="sxs-lookup"><span data-stu-id="592a1-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="592a1-111">Les robots dans les conversations de conversation de groupe et de canal exigent que l’utilisateur appelle le robot pour l’appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="592a1-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="592a1-112">Dans une conversation un-à-un, les robots ne nécessitent pas de mention @.</span><span class="sxs-lookup"><span data-stu-id="592a1-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="592a1-113">Tous les messages envoyés par l’utilisateur sont acheminés à votre bot.</span><span class="sxs-lookup"><span data-stu-id="592a1-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="592a1-114">Pour activer votre robot dans une étendue particulière, ajoutez cette étendue à votre [manifeste d’application](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="592a1-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="592a1-115">Activités</span><span class="sxs-lookup"><span data-stu-id="592a1-115">Activities</span></span>

<span data-ttu-id="592a1-116">Chaque message est un objet `Activity` de type `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="592a1-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="592a1-117">Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="592a1-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="592a1-118">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="592a1-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="592a1-119">La conversation de base est gérée via le connecteur de l’infrastructure bot, une seule API REST pour permettre à votre bot de communiquer avec teams et d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="592a1-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="592a1-120">Le kit de développement logiciel (SDK) du générateur de robots offre un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux de conversation et l’État, et des méthodes simples pour incorporer des services cognitifs tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="592a1-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="592a1-121">Recevoir un message</span><span class="sxs-lookup"><span data-stu-id="592a1-121">Receive a message</span></span>

<span data-ttu-id="592a1-122">Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`.</span><span class="sxs-lookup"><span data-stu-id="592a1-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="592a1-123">Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.</span><span class="sxs-lookup"><span data-stu-id="592a1-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="592a1-124">Le code ci-dessous illustre un exemple.</span><span class="sxs-lookup"><span data-stu-id="592a1-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="592a1-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="592a1-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="592a1-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="592a1-126">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[<span data-ttu-id="592a1-127">Python</span><span class="sxs-lookup"><span data-stu-id="592a1-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="592a1-128">JSON</span><span class="sxs-lookup"><span data-stu-id="592a1-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a><span data-ttu-id="592a1-129">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="592a1-129">Send a message</span></span>

<span data-ttu-id="592a1-130">Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité.</span><span class="sxs-lookup"><span data-stu-id="592a1-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="592a1-131">Dans le gestionnaire d’activités du bot, utilisez la méthode `SendActivityAsync` de l’objet de contexte de tour pour envoyer un seul message de réponse.</span><span class="sxs-lookup"><span data-stu-id="592a1-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="592a1-132">Vous pouvez également utiliser la méthode de l’objet `SendActivitiesAsync` pour envoyer plusieurs réponses à la fois.</span><span class="sxs-lookup"><span data-stu-id="592a1-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="592a1-133">Le code ci-dessous montre un exemple d’envoi d’un message lorsqu’une personne est ajoutée à une conversation.</span><span class="sxs-lookup"><span data-stu-id="592a1-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="592a1-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="592a1-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="592a1-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="592a1-135">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="592a1-136">Python</span><span class="sxs-lookup"><span data-stu-id="592a1-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="592a1-137">JSON</span><span class="sxs-lookup"><span data-stu-id="592a1-137">JSON</span></span>](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="teams-channel-data"></a><span data-ttu-id="592a1-138">Données de canal teams</span><span class="sxs-lookup"><span data-stu-id="592a1-138">Teams channel data</span></span>

<span data-ttu-id="592a1-139">L' `channelData` objet contient des informations spécifiques aux équipes et constitue la source définitive des ID d’équipe et de canal.</span><span class="sxs-lookup"><span data-stu-id="592a1-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="592a1-140">Vous devrez peut-être mettre en cache et utiliser ces ID en tant que clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="592a1-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="592a1-141">Le `TeamsActivityHandler` dans le kit de développement logiciel (SDK) extraira généralement les informations importantes de l' `channelData` objet pour le rend plus facilement accessible, mais vous pouvez toujours accéder aux informations d’origine à partir de l' `turnContext` objet.</span><span class="sxs-lookup"><span data-stu-id="592a1-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="592a1-142">L' `channelData` objet n’est pas inclus dans les messages dans les conversations personnelles, étant donné qu’ils ont lieu en dehors de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="592a1-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="592a1-143">Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="592a1-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="592a1-144">`eventType` Type d’événement teams ; transmis uniquement en cas d' [événements de modification de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="592a1-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="592a1-145">`tenant.id` ID de locataire Azure Active Directory ; transmis dans tous les contextes</span><span class="sxs-lookup"><span data-stu-id="592a1-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="592a1-146">`team` Transmis uniquement dans les contextes de canal, pas dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="592a1-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="592a1-147">`id` GUID du canal</span><span class="sxs-lookup"><span data-stu-id="592a1-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="592a1-148">`name` Nom de l’équipe ; transmis uniquement en cas d' [événement de changement de nom d’équipe](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="592a1-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="592a1-149">`channel` Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour des événements dans des canaux dans teams où le bot a été ajouté</span><span class="sxs-lookup"><span data-stu-id="592a1-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="592a1-150">`id` GUID du canal</span><span class="sxs-lookup"><span data-stu-id="592a1-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="592a1-151">`name` Nom du canal ; transmis uniquement en cas d' [événements de modification de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="592a1-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="592a1-152">`channelData.teamsTeamId` Déconseillées.</span><span class="sxs-lookup"><span data-stu-id="592a1-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="592a1-153">Cette propriété est incluse uniquement à des fins de compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="592a1-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="592a1-154">`channelData.teamsChannelId` Déconseillées.</span><span class="sxs-lookup"><span data-stu-id="592a1-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="592a1-155">Cette propriété est incluse uniquement à des fins de compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="592a1-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="592a1-156">Exemple d’objet channelData (événement channelCreated)</span><span class="sxs-lookup"><span data-stu-id="592a1-156">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a><span data-ttu-id="592a1-157">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="592a1-157">Message content</span></span>

<span data-ttu-id="592a1-158">Votre robot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="592a1-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="592a1-159">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="592a1-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="592a1-160">Format</span><span class="sxs-lookup"><span data-stu-id="592a1-160">Format</span></span>    | <span data-ttu-id="592a1-161">De l’utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="592a1-161">From user to bot</span></span> | <span data-ttu-id="592a1-162">Du bot à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="592a1-162">From bot to user</span></span> | <span data-ttu-id="592a1-163">Notes</span><span class="sxs-lookup"><span data-stu-id="592a1-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="592a1-164">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="592a1-164">Rich text</span></span> | <span data-ttu-id="592a1-165">✔</span><span class="sxs-lookup"><span data-stu-id="592a1-165">✔</span></span>                | <span data-ttu-id="592a1-166">✔</span><span class="sxs-lookup"><span data-stu-id="592a1-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="592a1-167">Images</span><span class="sxs-lookup"><span data-stu-id="592a1-167">Pictures</span></span>  | <span data-ttu-id="592a1-168">✔</span><span class="sxs-lookup"><span data-stu-id="592a1-168">✔</span></span>                | <span data-ttu-id="592a1-169">✔</span><span class="sxs-lookup"><span data-stu-id="592a1-169">✔</span></span>                | <span data-ttu-id="592a1-170">Taille maximale 1024 x 1024 et 1 Mo au format PNG, JPEG ou GIF ; les images GIF animées ne sont pas prises en charge</span><span class="sxs-lookup"><span data-stu-id="592a1-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="592a1-171">Cartes</span><span class="sxs-lookup"><span data-stu-id="592a1-171">Cards</span></span>     | <span data-ttu-id="592a1-172">✖</span><span class="sxs-lookup"><span data-stu-id="592a1-172">✖</span></span>                | <span data-ttu-id="592a1-173">✔</span><span class="sxs-lookup"><span data-stu-id="592a1-173">✔</span></span>                | <span data-ttu-id="592a1-174">Voir la [référence de la carte teams](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes prises en charge</span><span class="sxs-lookup"><span data-stu-id="592a1-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="592a1-175">Emojis</span><span class="sxs-lookup"><span data-stu-id="592a1-175">Emojis</span></span>    | <span data-ttu-id="592a1-176">✖</span><span class="sxs-lookup"><span data-stu-id="592a1-176">✖</span></span>                | <span data-ttu-id="592a1-177">✔</span><span class="sxs-lookup"><span data-stu-id="592a1-177">✔</span></span>                | <span data-ttu-id="592a1-178">Teams prend actuellement en charge les Emoji via UTF-16 (par exemple, U + 1F600 pour Grinning face)</span><span class="sxs-lookup"><span data-stu-id="592a1-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="592a1-179">Ajout de notifications à votre message</span><span class="sxs-lookup"><span data-stu-id="592a1-179">Adding notifications to your message</span></span>

<span data-ttu-id="592a1-180">Les notifications signalent aux utilisateurs les nouvelles tâches, les mentions et les commentaires relatifs à ce qu’ils travaillent ou doivent examiner en insérant un avertissement dans leur flux d’activité.</span><span class="sxs-lookup"><span data-stu-id="592a1-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="592a1-181">Vous pouvez définir des notifications à déclencher à partir de votre message bot en affectant la `TeamsChannelData` valeur true à la propriété Objects `Notification.Alert` .</span><span class="sxs-lookup"><span data-stu-id="592a1-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="592a1-182">Le déclenchement ou non d’une notification dépend finalement des paramètres de teams de l’utilisateur individuel et vous ne pouvez pas substituer ces paramètres par programmation.</span><span class="sxs-lookup"><span data-stu-id="592a1-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="592a1-183">Le type de notification sera une bannière ou une bannière et un message électronique.</span><span class="sxs-lookup"><span data-stu-id="592a1-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="592a1-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="592a1-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="592a1-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="592a1-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="592a1-186">Python</span><span class="sxs-lookup"><span data-stu-id="592a1-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="592a1-187">JSON</span><span class="sxs-lookup"><span data-stu-id="592a1-187">JSON</span></span>](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a><span data-ttu-id="592a1-188">Messages d’image</span><span class="sxs-lookup"><span data-stu-id="592a1-188">Picture messages</span></span>

<span data-ttu-id="592a1-189">Les images sont envoyées par l’ajout de pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="592a1-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="592a1-190">Vous trouverez plus d’informations sur les pièces jointes dans la documentation de l' [infrastructure bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="592a1-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="592a1-191">Les images peuvent être d’au moins 1024 × 1024 et 1 Mo au format PNG, JPEG ou GIF ; l’image GIF animée n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="592a1-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="592a1-192">Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML.</span><span class="sxs-lookup"><span data-stu-id="592a1-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="592a1-193">Si vous utilisez la démarque, la taille de l’image est par défaut de 256 × 256.</span><span class="sxs-lookup"><span data-stu-id="592a1-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="592a1-194">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="592a1-194">For example:</span></span>

* <span data-ttu-id="592a1-195">Utilisant `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="592a1-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="592a1-196">Ne pas utiliser- `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="592a1-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="next-steps"></a><span data-ttu-id="592a1-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="592a1-197">Next steps</span></span>

* [<span data-ttu-id="592a1-198">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="592a1-198">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="592a1-199">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="592a1-199">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
