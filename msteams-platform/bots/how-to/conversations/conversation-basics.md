---
title: Concepts de base d’une conversation
author: clearab
description: Comment avoir une conversation avec un bot Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075692"
---
# <a name="conversation-basics"></a><span data-ttu-id="ba2f7-103">Concepts de base d’une conversation</span><span class="sxs-lookup"><span data-stu-id="ba2f7-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="ba2f7-104">Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="ba2f7-105">Il existe trois types de conversations (ou portées) dans Teams :</span><span class="sxs-lookup"><span data-stu-id="ba2f7-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="ba2f7-106">`teams` Également appelées conversations de canal, visibles par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="ba2f7-107">`personal` Conversations entre les bots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="ba2f7-108">`groupChat` Discutez entre un bot et au moins deux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="ba2f7-109">Active également votre bot dans les conversations de réunion.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="ba2f7-110">Un bot se comporte légèrement différemment selon le type de conversation dans qui il est impliqué :</span><span class="sxs-lookup"><span data-stu-id="ba2f7-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="ba2f7-111">Les bots dans les conversations de canal et de groupe nécessitent que l’utilisateur mentionne @ le bot pour l’appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="ba2f7-112">Les bots d’une conversation un-à-un ne nécessitent pas de mention @ .</span><span class="sxs-lookup"><span data-stu-id="ba2f7-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="ba2f7-113">Tous les messages envoyés par l’utilisateur sont acheminés à votre bot.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="ba2f7-114">Pour activer votre bot dans une étendue particulière, ajoutez cette étendue au manifeste [de votre application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="ba2f7-115">Activités</span><span class="sxs-lookup"><span data-stu-id="ba2f7-115">Activities</span></span>

<span data-ttu-id="ba2f7-116">Chaque message est un objet `Activity` de type `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="ba2f7-117">Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="ba2f7-118">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="ba2f7-119">La conversation de base est gérée par le biais du connecteur Bot Framework, une API REST unique permettant à votre bot de communiquer avec Teams et d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="ba2f7-120">Le SDK Bot Builder fournit un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux et l’état des conversations, ainsi que des moyens simples d’incorporer des services cognitives tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="ba2f7-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="ba2f7-121">Recevoir un message</span><span class="sxs-lookup"><span data-stu-id="ba2f7-121">Receive a message</span></span>

<span data-ttu-id="ba2f7-122">Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="ba2f7-123">Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="ba2f7-124">Le code ci-dessous présente un exemple.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ba2f7-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ba2f7-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="ba2f7-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ba2f7-126">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="ba2f7-127">Python</span><span class="sxs-lookup"><span data-stu-id="ba2f7-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="ba2f7-128">JSON</span><span class="sxs-lookup"><span data-stu-id="ba2f7-128">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="ba2f7-129">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="ba2f7-129">Send a message</span></span>

<span data-ttu-id="ba2f7-130">Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="ba2f7-131">Dans le gestionnaire d’activités du bot, utilisez la méthode `SendActivityAsync` de l’objet de contexte de tour pour envoyer un seul message de réponse.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="ba2f7-132">Vous pouvez également utiliser la méthode de l’objet `SendActivitiesAsync` pour envoyer plusieurs réponses à la fois.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="ba2f7-133">Le code ci-dessous montre un exemple d’envoi d’un message lorsqu’une personne est ajoutée à une conversation.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="ba2f7-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ba2f7-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="ba2f7-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ba2f7-135">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="ba2f7-136">Python</span><span class="sxs-lookup"><span data-stu-id="ba2f7-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="ba2f7-137">JSON</span><span class="sxs-lookup"><span data-stu-id="ba2f7-137">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="ba2f7-138">Données de canal Teams</span><span class="sxs-lookup"><span data-stu-id="ba2f7-138">Teams channel data</span></span>

<span data-ttu-id="ba2f7-139">L’objet contient des informations spécifiques à Teams et constitue la source définitive des ID d’équipe et `channelData` de canal.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="ba2f7-140">Vous devrez peut-être mettre en cache et utiliser ces ID comme clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="ba2f7-141">Le SDK retire généralement des informations importantes de l’objet pour les rendre plus facilement accessibles, mais vous pouvez toujours accéder aux informations d’origine à partir de `TeamsActivityHandler` `channelData` `turnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="ba2f7-142">`channelData`L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en dehors d’un canal.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="ba2f7-143">Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba2f7-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="ba2f7-144">`eventType` Type d’événement Teams ; transmis uniquement en cas d’événements [de modification de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="ba2f7-145">`tenant.id` ID de client Azure Active Directory ; transmis dans tous les contextes</span><span class="sxs-lookup"><span data-stu-id="ba2f7-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="ba2f7-146">`team` Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="ba2f7-147">`id` GUID du canal</span><span class="sxs-lookup"><span data-stu-id="ba2f7-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="ba2f7-148">`name` Nom de l’équipe ; transmis uniquement en cas d’événements [de changement de nom d’équipe](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="ba2f7-149">`channel` Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté</span><span class="sxs-lookup"><span data-stu-id="ba2f7-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="ba2f7-150">`id` GUID du canal</span><span class="sxs-lookup"><span data-stu-id="ba2f7-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="ba2f7-151">`name`Nom du canal ; transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="ba2f7-152">`channelData.teamsTeamId` Deprecated.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="ba2f7-153">Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="ba2f7-154">`channelData.teamsChannelId` Deprecated.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="ba2f7-155">Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="ba2f7-156">Exemple d’objet channelData (événement channelCreated)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-156">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="ba2f7-157">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="ba2f7-157">Message content</span></span>

<span data-ttu-id="ba2f7-158">Votre bot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="ba2f7-159">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="ba2f7-160">Format</span><span class="sxs-lookup"><span data-stu-id="ba2f7-160">Format</span></span>    | <span data-ttu-id="ba2f7-161">De l’utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="ba2f7-161">From user to bot</span></span> | <span data-ttu-id="ba2f7-162">Du bot à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ba2f7-162">From bot to user</span></span> | <span data-ttu-id="ba2f7-163">Notes</span><span class="sxs-lookup"><span data-stu-id="ba2f7-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="ba2f7-164">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="ba2f7-164">Rich text</span></span> | <span data-ttu-id="ba2f7-165">✔</span><span class="sxs-lookup"><span data-stu-id="ba2f7-165">✔</span></span>                | <span data-ttu-id="ba2f7-166">✔</span><span class="sxs-lookup"><span data-stu-id="ba2f7-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="ba2f7-167">Images</span><span class="sxs-lookup"><span data-stu-id="ba2f7-167">Pictures</span></span>  | <span data-ttu-id="ba2f7-168">✔</span><span class="sxs-lookup"><span data-stu-id="ba2f7-168">✔</span></span>                | <span data-ttu-id="ba2f7-169">✔</span><span class="sxs-lookup"><span data-stu-id="ba2f7-169">✔</span></span>                | <span data-ttu-id="ba2f7-170">Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge</span><span class="sxs-lookup"><span data-stu-id="ba2f7-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="ba2f7-171">Cartes</span><span class="sxs-lookup"><span data-stu-id="ba2f7-171">Cards</span></span>     | <span data-ttu-id="ba2f7-172">✖</span><span class="sxs-lookup"><span data-stu-id="ba2f7-172">✖</span></span>                | <span data-ttu-id="ba2f7-173">✔</span><span class="sxs-lookup"><span data-stu-id="ba2f7-173">✔</span></span>                | <span data-ttu-id="ba2f7-174">Voir la référence [de carte Teams pour](~/task-modules-and-cards/cards/cards-reference.md) les cartes pris en charge</span><span class="sxs-lookup"><span data-stu-id="ba2f7-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="ba2f7-175">Emojis</span><span class="sxs-lookup"><span data-stu-id="ba2f7-175">Emojis</span></span>    | <span data-ttu-id="ba2f7-176">✖</span><span class="sxs-lookup"><span data-stu-id="ba2f7-176">✖</span></span>                | <span data-ttu-id="ba2f7-177">✔</span><span class="sxs-lookup"><span data-stu-id="ba2f7-177">✔</span></span>                | <span data-ttu-id="ba2f7-178">Teams prend actuellement en charge les emojis via UTF-16 (par exemple, U+1F600 pour le visage de panoramique)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="ba2f7-179">Ajout de notifications à votre message</span><span class="sxs-lookup"><span data-stu-id="ba2f7-179">Adding notifications to your message</span></span>

<span data-ttu-id="ba2f7-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="ba2f7-181">Vous pouvez définir des notifications pour qu’ils se déclenchent à partir de votre message bot en réglant la propriété des objets `TeamsChannelData` `Notification.Alert` sur true.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="ba2f7-182">Le fait qu’une notification soit ou non élevée dépend en fin de compte des paramètres Teams de l’utilisateur individuel et vous ne pouvez pas remplacer ces paramètres par programme.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="ba2f7-183">Le type de notification sera soit une bannière, soit une bannière et un e-mail.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ba2f7-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ba2f7-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="ba2f7-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ba2f7-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="ba2f7-186">Python</span><span class="sxs-lookup"><span data-stu-id="ba2f7-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="ba2f7-187">JSON</span><span class="sxs-lookup"><span data-stu-id="ba2f7-187">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="ba2f7-188">Messages image</span><span class="sxs-lookup"><span data-stu-id="ba2f7-188">Picture messages</span></span>

<span data-ttu-id="ba2f7-189">Les images sont envoyées en ajoutant des pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="ba2f7-190">Vous trouverez plus d’informations sur les pièces jointes dans la [documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ba2f7-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="ba2f7-191">Les images peuvent être au maximum 1 024 × 1 024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="ba2f7-192">Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="ba2f7-193">Si vous utilisez Markdown, la taille par défaut de l’image est 256×256.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="ba2f7-194">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba2f7-194">For example:</span></span>

* <span data-ttu-id="ba2f7-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="ba2f7-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="ba2f7-196">Ne pas utiliser - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="ba2f7-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="code-sample"></a><span data-ttu-id="ba2f7-197">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ba2f7-197">Code sample</span></span>
|<span data-ttu-id="ba2f7-198">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="ba2f7-198">**Sample name**</span></span> | <span data-ttu-id="ba2f7-199">**Description**</span><span class="sxs-lookup"><span data-stu-id="ba2f7-199">**Description**</span></span> | <span data-ttu-id="ba2f7-200">**. NETCore**</span><span class="sxs-lookup"><span data-stu-id="ba2f7-200">**.NETCore**</span></span> | <span data-ttu-id="ba2f7-201">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="ba2f7-201">**Javascript**</span></span> | <span data-ttu-id="ba2f7-202">**Python**</span><span class="sxs-lookup"><span data-stu-id="ba2f7-202">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="ba2f7-203">Teams Conversation Bot</span><span class="sxs-lookup"><span data-stu-id="ba2f7-203">Teams Conversation Bot</span></span> | <span data-ttu-id="ba2f7-204">Gestion des événements de messagerie et de conversation.</span><span class="sxs-lookup"><span data-stu-id="ba2f7-204">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="ba2f7-205">View</span><span class="sxs-lookup"><span data-stu-id="ba2f7-205">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="ba2f7-206">View</span><span class="sxs-lookup"><span data-stu-id="ba2f7-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="ba2f7-207">View</span><span class="sxs-lookup"><span data-stu-id="ba2f7-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="ba2f7-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba2f7-208">Next steps</span></span>

* [<span data-ttu-id="ba2f7-209">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="ba2f7-209">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="ba2f7-210">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="ba2f7-210">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
