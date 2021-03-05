---
title: Concepts de base d’une conversation
description: décrit les manières d’avoir une conversation avec un bot Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 4eba22e9b29f5378dc03480ba5f6ba421f816eb3
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449506"
---
# <a name="conversation-basics"></a><span data-ttu-id="42d1d-103">Concepts de base d’une conversation</span><span class="sxs-lookup"><span data-stu-id="42d1d-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="42d1d-104">Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="42d1d-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="42d1d-105">Il existe trois types de conversations, également appelées étendues dans Teams :</span><span class="sxs-lookup"><span data-stu-id="42d1d-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="42d1d-106">Type de conversation</span><span class="sxs-lookup"><span data-stu-id="42d1d-106">Conversation type</span></span> | <span data-ttu-id="42d1d-107">Description</span><span class="sxs-lookup"><span data-stu-id="42d1d-107">Description</span></span> |
| ------- | ----------- |
|  `teams` | <span data-ttu-id="42d1d-108">Également appelées conversations de canal, visibles par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-108">Also called channel conversations, visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="42d1d-109">Conversations entre les bots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="42d1d-109">Conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="42d1d-110">Discutez entre un bot et au moins deux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="42d1d-110">Chat between a bot and two or more users.</span></span> <span data-ttu-id="42d1d-111">Active également votre bot dans les conversations de réunion.</span><span class="sxs-lookup"><span data-stu-id="42d1d-111">Also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="42d1d-112">Un bot se comporte légèrement différemment selon le type de conversation dans qui il est impliqué :</span><span class="sxs-lookup"><span data-stu-id="42d1d-112">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="42d1d-113">Les bots dans les conversations de canal et de groupe nécessitent que l’utilisateur mentionne @ le bot pour l’appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="42d1d-114">Les bots d’une conversation un-à-un ne nécessitent pas de mention @ .</span><span class="sxs-lookup"><span data-stu-id="42d1d-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="42d1d-115">Tous les messages envoyés par l’utilisateur sont acheminés vers votre bot.</span><span class="sxs-lookup"><span data-stu-id="42d1d-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="42d1d-116">Pour activer votre bot dans une étendue particulière, ajoutez cette étendue au manifeste [de votre application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="42d1d-116">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="42d1d-117">Activités</span><span class="sxs-lookup"><span data-stu-id="42d1d-117">Activities</span></span>

<span data-ttu-id="42d1d-118">Chaque message est un objet `Activity` de type `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="42d1d-118">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="42d1d-119">Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="42d1d-119">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="42d1d-120">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="42d1d-120">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="42d1d-121">Les conversations de base sont gérées par le biais du connecteur Bot Framework, une API REST unique.</span><span class="sxs-lookup"><span data-stu-id="42d1d-121">Basic conversations are handled through the Bot Framework Connector, a single REST API.</span></span> <span data-ttu-id="42d1d-122">Cette API permet à votre bot de communiquer avec Teams et d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="42d1d-122">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="42d1d-123">Le SDK Bot Builder fournit un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux et l’état des conversations, ainsi que des moyens simples d’incorporer des services cognitives tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="42d1d-123">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="42d1d-124">Recevoir un message</span><span class="sxs-lookup"><span data-stu-id="42d1d-124">Receive a message</span></span>

<span data-ttu-id="42d1d-125">Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`.</span><span class="sxs-lookup"><span data-stu-id="42d1d-125">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="42d1d-126">Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.</span><span class="sxs-lookup"><span data-stu-id="42d1d-126">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="42d1d-127">Le code ci-dessous vous montre un exemple.</span><span class="sxs-lookup"><span data-stu-id="42d1d-127">The following code shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="42d1d-128">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="42d1d-128">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="42d1d-129">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="42d1d-129">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="42d1d-130">Python</span><span class="sxs-lookup"><span data-stu-id="42d1d-130">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="42d1d-131">JSON</span><span class="sxs-lookup"><span data-stu-id="42d1d-131">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="42d1d-132">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="42d1d-132">Send a message</span></span>

<span data-ttu-id="42d1d-133">Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité.</span><span class="sxs-lookup"><span data-stu-id="42d1d-133">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="42d1d-134">Dans le handler d’activité du bot, utilisez la méthode de l’objet de contexte turn pour `SendActivityAsync` envoyer une seule réponse de message.</span><span class="sxs-lookup"><span data-stu-id="42d1d-134">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="42d1d-135">Utilisez la méthode de `SendActivitiesAsync` l’objet pour envoyer plusieurs réponses à la fois.</span><span class="sxs-lookup"><span data-stu-id="42d1d-135">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="42d1d-136">Le code suivant montre un exemple d’envoi d’un message lorsqu’une personne est ajoutée à une conversation.</span><span class="sxs-lookup"><span data-stu-id="42d1d-136">The following code shows an example of sending a message when someone is added to a conversation.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="42d1d-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="42d1d-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="42d1d-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="42d1d-138">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="42d1d-139">Python</span><span class="sxs-lookup"><span data-stu-id="42d1d-139">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="42d1d-140">JSON</span><span class="sxs-lookup"><span data-stu-id="42d1d-140">JSON</span></span>](#tab/json)

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

> [!NOTE]
> <span data-ttu-id="42d1d-141">Le fractionnement de message se produit lorsqu’un message texte et une pièce jointe sont envoyés dans la même charge utile d’activité.</span><span class="sxs-lookup"><span data-stu-id="42d1d-141">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="42d1d-142">Cette activité est divisée en activités distinctes par Microsoft Teams, une activité avec un message texte et l’autre avec une pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="42d1d-142">This activity is split into separate activities by Microsoft Teams, one activity with just a text message and the other with an attachment.</span></span> <span data-ttu-id="42d1d-143">Lorsque l’activité est fractionée, vous ne recevez pas l’ID de message en réponse, qui est utilisé pour mettre à jour ou supprimer [le](~/bots/how-to/update-and-delete-bot-messages.md) message de manière proactive.</span><span class="sxs-lookup"><span data-stu-id="42d1d-143">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="42d1d-144">Il est recommandé d’envoyer des activités distinctes au lieu de dépendre du fractionnement des messages.</span><span class="sxs-lookup"><span data-stu-id="42d1d-144">It is recommended to send separate activities instead of depending on message splitting.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="42d1d-145">Données de canal Teams</span><span class="sxs-lookup"><span data-stu-id="42d1d-145">Teams channel data</span></span>

<span data-ttu-id="42d1d-146">L’objet contient des informations spécifiques à Teams et constitue une source définitive pour les ID d’équipe `channelData` et de canal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-146">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="42d1d-147">Vous devrez peut-être mettre en cache et utiliser ces ID comme clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="42d1d-147">You may need to cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="42d1d-148">Le SDK, en général, retire des informations importantes de `TeamsActivityHandler` l’objet pour les rendre facilement `channelData` accessibles.</span><span class="sxs-lookup"><span data-stu-id="42d1d-148">The `TeamsActivityHandler` in the SDK, typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="42d1d-149">Toutefois, vous pouvez toujours accéder aux données d’origine à partir de `turnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="42d1d-149">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="42d1d-150">L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en `channelData` dehors de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-150">The `channelData` object is not included in messages in personal conversations, as these take place outside of any channel.</span></span>

<span data-ttu-id="42d1d-151">Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="42d1d-151">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="42d1d-152">`eventType`Type d’événement Teams ; transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="42d1d-152">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="42d1d-153">`tenant.id` ID de client Azure Active Directory, transmis dans tous les contextes.</span><span class="sxs-lookup"><span data-stu-id="42d1d-153">`tenant.id` Azure Active Directory tenant ID, passed in all contexts.</span></span>
* <span data-ttu-id="42d1d-154">`team` Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="42d1d-154">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="42d1d-155">`id` GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-155">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="42d1d-156">`name`Nom de l’équipe ; transmis uniquement dans les cas d’événements [de changement de nom d’équipe.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="42d1d-156">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="42d1d-157">`channel` Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="42d1d-157">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="42d1d-158">`id` GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-158">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="42d1d-159">`name`Nom du canal ; transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="42d1d-159">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="42d1d-160">`channelData.teamsTeamId` Deprecated.</span><span class="sxs-lookup"><span data-stu-id="42d1d-160">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="42d1d-161">Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="42d1d-161">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="42d1d-162">`channelData.teamsChannelId` Deprecated.</span><span class="sxs-lookup"><span data-stu-id="42d1d-162">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="42d1d-163">Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="42d1d-163">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="42d1d-164">Exemple d’objet channelData (événement channelCreated)</span><span class="sxs-lookup"><span data-stu-id="42d1d-164">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="42d1d-165">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="42d1d-165">Message content</span></span>

<span data-ttu-id="42d1d-166">Votre bot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="42d1d-166">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="42d1d-167">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="42d1d-167">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="42d1d-168">Format</span><span class="sxs-lookup"><span data-stu-id="42d1d-168">Format</span></span>    | <span data-ttu-id="42d1d-169">De l’utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="42d1d-169">From user to bot</span></span> | <span data-ttu-id="42d1d-170">Du bot à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="42d1d-170">From bot to user</span></span> | <span data-ttu-id="42d1d-171">Notes</span><span class="sxs-lookup"><span data-stu-id="42d1d-171">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="42d1d-172">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="42d1d-172">Rich text</span></span> | <span data-ttu-id="42d1d-173">✔</span><span class="sxs-lookup"><span data-stu-id="42d1d-173">✔</span></span>                | <span data-ttu-id="42d1d-174">✔</span><span class="sxs-lookup"><span data-stu-id="42d1d-174">✔</span></span>                |                                                                                         |
| <span data-ttu-id="42d1d-175">Images</span><span class="sxs-lookup"><span data-stu-id="42d1d-175">Pictures</span></span>  | <span data-ttu-id="42d1d-176">✔</span><span class="sxs-lookup"><span data-stu-id="42d1d-176">✔</span></span>                | <span data-ttu-id="42d1d-177">✔</span><span class="sxs-lookup"><span data-stu-id="42d1d-177">✔</span></span>                | <span data-ttu-id="42d1d-178">Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge</span><span class="sxs-lookup"><span data-stu-id="42d1d-178">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="42d1d-179">Cartes</span><span class="sxs-lookup"><span data-stu-id="42d1d-179">Cards</span></span>     | <span data-ttu-id="42d1d-180">✖</span><span class="sxs-lookup"><span data-stu-id="42d1d-180">✖</span></span>                | <span data-ttu-id="42d1d-181">✔</span><span class="sxs-lookup"><span data-stu-id="42d1d-181">✔</span></span>                | <span data-ttu-id="42d1d-182">Voir la référence [de carte Teams pour](~/task-modules-and-cards/cards/cards-reference.md) les cartes pris en charge</span><span class="sxs-lookup"><span data-stu-id="42d1d-182">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="42d1d-183">Emojis</span><span class="sxs-lookup"><span data-stu-id="42d1d-183">Emojis</span></span>    | <span data-ttu-id="42d1d-184">✖</span><span class="sxs-lookup"><span data-stu-id="42d1d-184">✖</span></span>                | <span data-ttu-id="42d1d-185">✔</span><span class="sxs-lookup"><span data-stu-id="42d1d-185">✔</span></span>                | <span data-ttu-id="42d1d-186">Teams prend actuellement en charge les emojis via UTF-16 (par exemple, U+1F600 pour le visage de l’en-tête)</span><span class="sxs-lookup"><span data-stu-id="42d1d-186">Teams currently supports emojis through UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="42d1d-187">Ajout de notifications à votre message</span><span class="sxs-lookup"><span data-stu-id="42d1d-187">Adding notifications to your message</span></span>

<span data-ttu-id="42d1d-188">Notifications alert users about new tasks, mentions, and comments related to what they are working on or need to look at by inserting a notice into their activity feed.</span><span class="sxs-lookup"><span data-stu-id="42d1d-188">Notifications alert users about new tasks, mentions, and comments related to what they are working on or need to look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="42d1d-189">Vous pouvez définir des notifications pour qu’ils se déclenchent à partir de votre bot-message en réglant la propriété des objets `TeamsChannelData` `Notification.Alert` sur true.</span><span class="sxs-lookup"><span data-stu-id="42d1d-189">You can set notifications to trigger from your bot-message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="42d1d-190">Le fait qu’une notification soit ou non élevée dépend en fin de compte des paramètres Teams de l’utilisateur individuel et vous ne pouvez pas remplacer ces paramètres par programme.</span><span class="sxs-lookup"><span data-stu-id="42d1d-190">Whether or not a notification is raised ultimately depends on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="42d1d-191">Le type de notification est soit une bannière, soit une bannière et un e-mail.</span><span class="sxs-lookup"><span data-stu-id="42d1d-191">The type of notification is either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="42d1d-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="42d1d-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="42d1d-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="42d1d-193">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="42d1d-194">Python</span><span class="sxs-lookup"><span data-stu-id="42d1d-194">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="42d1d-195">JSON</span><span class="sxs-lookup"><span data-stu-id="42d1d-195">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="42d1d-196">Messages image</span><span class="sxs-lookup"><span data-stu-id="42d1d-196">Picture messages</span></span>

<span data-ttu-id="42d1d-197">Les images sont envoyées en ajoutant des pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="42d1d-197">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="42d1d-198">Vous trouverez plus d’informations sur les pièces jointes dans la [documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="42d1d-198">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="42d1d-199">Les images peuvent être au maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="42d1d-199">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="42d1d-200">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="42d1d-200">Animated GIF is not supported.</span></span>

<span data-ttu-id="42d1d-201">Spécifiez toujours la hauteur et la largeur de chaque image à l’aide de XML.</span><span class="sxs-lookup"><span data-stu-id="42d1d-201">Always specify the height and width of each image by using XML.</span></span> <span data-ttu-id="42d1d-202">Dans Markdown, la taille par défaut de l’image est 256×256.</span><span class="sxs-lookup"><span data-stu-id="42d1d-202">In Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="42d1d-203">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="42d1d-203">For example:</span></span>

* <span data-ttu-id="42d1d-204">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="42d1d-204">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="42d1d-205">Ne pas utiliser - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="42d1d-205">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="42d1d-206">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="42d1d-206">Adaptive cards</span></span>

<span data-ttu-id="42d1d-207">Utilisez le code suivant pour envoyer une carte adaptative simple :</span><span class="sxs-lookup"><span data-stu-id="42d1d-207">Use the following code to send a simple adaptive card:</span></span>

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

<span data-ttu-id="42d1d-208">Pour en savoir plus sur les cartes et les cartes dans les bots, consultez [la documentation des cartes.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="42d1d-208">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="42d1d-209">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="42d1d-209">Code sample</span></span>

|<span data-ttu-id="42d1d-210">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="42d1d-210">**Sample name**</span></span> | <span data-ttu-id="42d1d-211">**Description**</span><span class="sxs-lookup"><span data-stu-id="42d1d-211">**Description**</span></span> | <span data-ttu-id="42d1d-212">**. NETCore**</span><span class="sxs-lookup"><span data-stu-id="42d1d-212">**.NETCore**</span></span> | <span data-ttu-id="42d1d-213">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="42d1d-213">**JavaScript**</span></span> | <span data-ttu-id="42d1d-214">**Python**</span><span class="sxs-lookup"><span data-stu-id="42d1d-214">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="42d1d-215">Teams Conversation Bot</span><span class="sxs-lookup"><span data-stu-id="42d1d-215">Teams Conversation Bot</span></span> | <span data-ttu-id="42d1d-216">Gestion des événements de messagerie et de conversation.</span><span class="sxs-lookup"><span data-stu-id="42d1d-216">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="42d1d-217">View</span><span class="sxs-lookup"><span data-stu-id="42d1d-217">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="42d1d-218">View</span><span class="sxs-lookup"><span data-stu-id="42d1d-218">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="42d1d-219">View</span><span class="sxs-lookup"><span data-stu-id="42d1d-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="42d1d-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42d1d-220">Next steps</span></span>

* [<span data-ttu-id="42d1d-221">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="42d1d-221">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="42d1d-222">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="42d1d-222">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
