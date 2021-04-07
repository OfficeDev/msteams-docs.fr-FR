---
title: Concepts de base d’une conversation
description: décrit les manières d’avoir une conversation avec un bot Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 193a93dbf775389383e0385207fa4112440bffe5
ms.sourcegitcommit: 82bda0599ba2676ab9348c2f4284f73c7dad0838
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596673"
---
# <a name="conversation-basics"></a><span data-ttu-id="b4651-103">Concepts de base d’une conversation</span><span class="sxs-lookup"><span data-stu-id="b4651-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="b4651-104">Une conversation est une série de messages envoyés entre votre bot Microsoft Teams et un ou plusieurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b4651-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="b4651-105">Il existe trois types de conversations, également appelées étendues dans Teams :</span><span class="sxs-lookup"><span data-stu-id="b4651-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="b4651-106">Type de conversation</span><span class="sxs-lookup"><span data-stu-id="b4651-106">Conversation type</span></span> | <span data-ttu-id="b4651-107">Description</span><span class="sxs-lookup"><span data-stu-id="b4651-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="b4651-108">Ce type de conversation est visible par tous les membres du canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="b4651-109">Ce type de conversation inclut les conversations entre les bots et un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b4651-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="b4651-110">Ce type de conversation inclut la conversation entre un bot et au moins deux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b4651-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="b4651-111">Il active également votre bot dans les conversations de réunion.</span><span class="sxs-lookup"><span data-stu-id="b4651-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="b4651-112">Un bot se comporte différemment en fonction de la conversation dans qui il est impliqué :</span><span class="sxs-lookup"><span data-stu-id="b4651-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="b4651-113">Les bots dans les conversations de canal et de groupe nécessitent que l’utilisateur mentionne @ le bot pour l’appeler dans un canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="b4651-114">Les bots d’une conversation un-à-un n’ont pas besoin d’une mention @ .</span><span class="sxs-lookup"><span data-stu-id="b4651-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="b4651-115">Tous les messages envoyés par l’utilisateur sont acheminés vers votre bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="b4651-116">Pour que le bot fonctionne dans une conversation ou une étendue particulière, ajoutez la prise en charge à cette étendue dans le manifeste [de l’application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="b4651-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="messages-in-bot-conversations"></a><span data-ttu-id="b4651-117">Messages dans les conversations de bot</span><span class="sxs-lookup"><span data-stu-id="b4651-117">Messages in bot conversations</span></span>

<span data-ttu-id="b4651-118">Chaque message d’une conversation est `Activity` un objet de type `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="b4651-118">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="b4651-119">Lorsqu’un utilisateur envoie un message, Teams publie le message à votre bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-119">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="b4651-120">Teams envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-120">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="b4651-121">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="b4651-121">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="b4651-122">Les conversations de base sont gérées via le connecteur Bot Framework, une API REST unique.</span><span class="sxs-lookup"><span data-stu-id="b4651-122">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="b4651-123">Cette API permet à votre bot de communiquer avec Teams et d’autres canaux.</span><span class="sxs-lookup"><span data-stu-id="b4651-123">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="b4651-124">Le SDK Bot Builder fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b4651-124">The Bot Builder SDK provides the following:</span></span>

* <span data-ttu-id="b4651-125">Accès facile au connecteur Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b4651-125">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="b4651-126">Fonctionnalités supplémentaires pour gérer le flux et l’état des conversations.</span><span class="sxs-lookup"><span data-stu-id="b4651-126">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="b4651-127">Méthodes simples pour incorporer des services cognitives tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="b4651-127">Simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

<span data-ttu-id="b4651-128">Votre bot reçoit des messages de Teams à l’aide de la propriété et envoie une ou plusieurs réponses aux `Text` messages aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b4651-128">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="b4651-129">Recevoir un message</span><span class="sxs-lookup"><span data-stu-id="b4651-129">Receive a message</span></span>

<span data-ttu-id="b4651-130">Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`.</span><span class="sxs-lookup"><span data-stu-id="b4651-130">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="b4651-131">Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.</span><span class="sxs-lookup"><span data-stu-id="b4651-131">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="b4651-132">Le code suivant montre un exemple de réception d’un message :</span><span class="sxs-lookup"><span data-stu-id="b4651-132">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="b4651-133">C#</span><span class="sxs-lookup"><span data-stu-id="b4651-133">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="b4651-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b4651-134">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="b4651-135">Python</span><span class="sxs-lookup"><span data-stu-id="b4651-135">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="b4651-136">JSON</span><span class="sxs-lookup"><span data-stu-id="b4651-136">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="b4651-137">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="b4651-137">Send a message</span></span>

<span data-ttu-id="b4651-138">Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité.</span><span class="sxs-lookup"><span data-stu-id="b4651-138">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="b4651-139">Dans le handler d’activité du bot, utilisez la méthode de l’objet de contexte turn pour `SendActivityAsync` envoyer une seule réponse de message.</span><span class="sxs-lookup"><span data-stu-id="b4651-139">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="b4651-140">Utilisez la méthode de l’objet `SendActivitiesAsync` pour envoyer plusieurs réponses à la fois.</span><span class="sxs-lookup"><span data-stu-id="b4651-140">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="b4651-141">Le code suivant montre un exemple d’envoi d’un message lorsqu’un utilisateur est ajouté à une conversation :</span><span class="sxs-lookup"><span data-stu-id="b4651-141">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

<span data-ttu-id="b4651-142">Le code suivant montre un exemple d’envoi d’un message :</span><span class="sxs-lookup"><span data-stu-id="b4651-142">The following code shows an example of sending a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="b4651-143">C#</span><span class="sxs-lookup"><span data-stu-id="b4651-143">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="b4651-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b4651-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="b4651-145">Python</span><span class="sxs-lookup"><span data-stu-id="b4651-145">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="b4651-146">JSON</span><span class="sxs-lookup"><span data-stu-id="b4651-146">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="b4651-147">Le fractionnement de message se produit lorsqu’un message texte et une pièce jointe sont envoyés dans la même charge utile d’activité.</span><span class="sxs-lookup"><span data-stu-id="b4651-147">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="b4651-148">Cette activité est divisée en activités distinctes par Microsoft Teams, l’une avec un message texte et l’autre avec une pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="b4651-148">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="b4651-149">Lorsque l’activité est fractionée, vous ne recevez pas [](~/bots/how-to/update-and-delete-bot-messages.md) l’ID du message en réponse, qui est utilisé pour mettre à jour ou supprimer le message de manière proactive.</span><span class="sxs-lookup"><span data-stu-id="b4651-149">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="b4651-150">Il est recommandé d’envoyer des activités distinctes au lieu de dépendre du fractionnement des messages.</span><span class="sxs-lookup"><span data-stu-id="b4651-150">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="b4651-151">Les messages envoyés entre les utilisateurs et les bots incluent des données de canal interne dans le message.</span><span class="sxs-lookup"><span data-stu-id="b4651-151">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="b4651-152">Ces données permettent au bot de communiquer correctement sur ce canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-152">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="b4651-153">Le SDK Bot Builder vous permet de modifier la structure des messages.</span><span class="sxs-lookup"><span data-stu-id="b4651-153">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="b4651-154">Données de canal Teams</span><span class="sxs-lookup"><span data-stu-id="b4651-154">Teams channel data</span></span>

<span data-ttu-id="b4651-155">L’objet contient des informations spécifiques à Teams et constitue une source définitive pour les ID d’équipe `channelData` et de canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-155">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="b4651-156">Si vous le souhaitez, vous pouvez mettre en cache et utiliser ces ID comme clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="b4651-156">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="b4651-157">Le SDK retire généralement des informations importantes de l’objet pour `TeamsActivityHandler` `channelData` les rendre facilement accessibles.</span><span class="sxs-lookup"><span data-stu-id="b4651-157">The `TeamsActivityHandler` in the SDK typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="b4651-158">Toutefois, vous pouvez toujours accéder aux données d’origine à partir de `turnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="b4651-158">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="b4651-159">L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en `channelData` dehors d’un canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-159">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="b4651-160">Un objet `channelData` type dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b4651-160">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="b4651-161">`eventType`: Type d’événement Teams transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="b4651-161">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="b4651-162">`tenant.id`: ID de client Azure Active Directory transmis dans tous les contextes.</span><span class="sxs-lookup"><span data-stu-id="b4651-162">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="b4651-163">`team`: Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="b4651-163">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="b4651-164">`id`: GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-164">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="b4651-165">`name`: Nom de l’équipe transmis uniquement en cas d’événements [de changement de nom d’équipe.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="b4651-165">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="b4651-166">`channel`: Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="b4651-166">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="b4651-167">`id`: GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="b4651-167">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="b4651-168">`name`: Nom du canal transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="b4651-168">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="b4651-169">`channelData.teamsTeamId`: Deprecated.</span><span class="sxs-lookup"><span data-stu-id="b4651-169">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="b4651-170">Cette propriété est incluse uniquement pour la compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="b4651-170">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="b4651-171">`channelData.teamsChannelId`: Deprecated.</span><span class="sxs-lookup"><span data-stu-id="b4651-171">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="b4651-172">Cette propriété est incluse uniquement pour la compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="b4651-172">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="b4651-173">Exemple d’objet channelData (événement channelCreated)</span><span class="sxs-lookup"><span data-stu-id="b4651-173">Example channelData object (channelCreated event)</span></span>

<span data-ttu-id="b4651-174">Le code suivant montre un exemple d’objet channelData :</span><span class="sxs-lookup"><span data-stu-id="b4651-174">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="b4651-175">Les messages reçus ou envoyés à votre bot peuvent inclure différents types de contenu de message.</span><span class="sxs-lookup"><span data-stu-id="b4651-175">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="b4651-176">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="b4651-176">Message content</span></span>

<span data-ttu-id="b4651-177">Votre bot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="b4651-177">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="b4651-178">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-178">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="b4651-179">Format</span><span class="sxs-lookup"><span data-stu-id="b4651-179">Format</span></span>    | <span data-ttu-id="b4651-180">De l’utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="b4651-180">From user to bot</span></span> | <span data-ttu-id="b4651-181">Du bot à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b4651-181">From bot to user</span></span> | <span data-ttu-id="b4651-182">Notes</span><span class="sxs-lookup"><span data-stu-id="b4651-182">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="b4651-183">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b4651-183">Rich text</span></span> | <span data-ttu-id="b4651-184">✔</span><span class="sxs-lookup"><span data-stu-id="b4651-184">✔</span></span>                | <span data-ttu-id="b4651-185">✔</span><span class="sxs-lookup"><span data-stu-id="b4651-185">✔</span></span>                |                                                                                         |
| <span data-ttu-id="b4651-186">Images</span><span class="sxs-lookup"><span data-stu-id="b4651-186">Pictures</span></span>  | <span data-ttu-id="b4651-187">✔</span><span class="sxs-lookup"><span data-stu-id="b4651-187">✔</span></span>                | <span data-ttu-id="b4651-188">✔</span><span class="sxs-lookup"><span data-stu-id="b4651-188">✔</span></span>                | <span data-ttu-id="b4651-189">Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="b4651-189">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="b4651-190">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b4651-190">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="b4651-191">Cartes</span><span class="sxs-lookup"><span data-stu-id="b4651-191">Cards</span></span>     | <span data-ttu-id="b4651-192">✖</span><span class="sxs-lookup"><span data-stu-id="b4651-192">✖</span></span>                | <span data-ttu-id="b4651-193">✔</span><span class="sxs-lookup"><span data-stu-id="b4651-193">✔</span></span>                | <span data-ttu-id="b4651-194">Consultez la référence [de carte Teams pour](~/task-modules-and-cards/cards/cards-reference.md) les cartes pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b4651-194">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="b4651-195">Emojis</span><span class="sxs-lookup"><span data-stu-id="b4651-195">Emojis</span></span>    | <span data-ttu-id="b4651-196">✖</span><span class="sxs-lookup"><span data-stu-id="b4651-196">✖</span></span>                | <span data-ttu-id="b4651-197">✔</span><span class="sxs-lookup"><span data-stu-id="b4651-197">✔</span></span>                | <span data-ttu-id="b4651-198">Teams prend actuellement en charge les emojis via UTF-16, par exemple U+1F600 pour le visage à l’aide du panoramique.</span><span class="sxs-lookup"><span data-stu-id="b4651-198">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="b4651-199">Vous pouvez également ajouter des notifications à votre message à l’aide de la `Notification.Alert` propriété.</span><span class="sxs-lookup"><span data-stu-id="b4651-199">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="b4651-200">Notifications à votre message</span><span class="sxs-lookup"><span data-stu-id="b4651-200">Notifications to your message</span></span>

<span data-ttu-id="b4651-201">Les notifications avertissent les utilisateurs des nouvelles tâches, mentions et commentaires.</span><span class="sxs-lookup"><span data-stu-id="b4651-201">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="b4651-202">Ces alertes sont liées à ce sur quoi les utilisateurs travaillent ou ce qu’ils doivent examiner en insérant une notification dans leur flux d’activités.</span><span class="sxs-lookup"><span data-stu-id="b4651-202">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="b4651-203">Pour que les notifications se déclenchent à partir de votre message bot, définissez la propriété des objets `TeamsChannelData` `Notification.Alert` sur true.</span><span class="sxs-lookup"><span data-stu-id="b4651-203">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="b4651-204">Le fait qu’une notification soit ou non élevée dépend des paramètres Teams de l’utilisateur individuel et vous ne pouvez pas remplacer ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="b4651-204">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="b4651-205">Le type de notification est soit une bannière, soit une bannière et un e-mail.</span><span class="sxs-lookup"><span data-stu-id="b4651-205">The notification type is either a banner or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="b4651-206">Le **champ Résumé** affiche tout texte de l’utilisateur en tant que message de notification dans le flux.</span><span class="sxs-lookup"><span data-stu-id="b4651-206">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="b4651-207">Le code suivant montre un exemple d’ajout de notifications à votre message :</span><span class="sxs-lookup"><span data-stu-id="b4651-207">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="b4651-208">C#</span><span class="sxs-lookup"><span data-stu-id="b4651-208">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="b4651-209">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b4651-209">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="b4651-210">Python</span><span class="sxs-lookup"><span data-stu-id="b4651-210">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="b4651-211">JSON</span><span class="sxs-lookup"><span data-stu-id="b4651-211">JSON</span></span>](#tab/json)

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

<span data-ttu-id="b4651-212">Pour améliorer votre message, vous pouvez inclure des images en tant que pièces jointes à ce message.</span><span class="sxs-lookup"><span data-stu-id="b4651-212">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="b4651-213">Messages image</span><span class="sxs-lookup"><span data-stu-id="b4651-213">Picture messages</span></span>

<span data-ttu-id="b4651-214">Les images sont envoyées en ajoutant des pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="b4651-214">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="b4651-215">Pour plus d’informations sur les pièces jointes, voir [la documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="b4651-215">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="b4651-216">Les images peuvent être au maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="b4651-216">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="b4651-217">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b4651-217">Animated GIF is not supported.</span></span>

<span data-ttu-id="b4651-218">Spécifiez la hauteur et la largeur de chaque image à l’aide de XML.</span><span class="sxs-lookup"><span data-stu-id="b4651-218">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="b4651-219">Dans markdown, la taille par défaut de l’image est 256×256.</span><span class="sxs-lookup"><span data-stu-id="b4651-219">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="b4651-220">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b4651-220">For example:</span></span>

* <span data-ttu-id="b4651-221">Utilisez : `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="b4651-221">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="b4651-222">N’utilisez pas : `![Duck on a rock](http://aka.ms/Fo983c)` .</span><span class="sxs-lookup"><span data-stu-id="b4651-222">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="b4651-223">Un bot de conversation peut inclure des cartes adaptatives qui simplifient les flux de travail d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="b4651-223">A conversational bot can include adaptive cards that simplify business workflows.</span></span> <span data-ttu-id="b4651-224">Les cartes adaptatives offrent des champs de texte, de reconnaissance vocale, d’images, de boutons et d’entrée personnalisables enrichis.</span><span class="sxs-lookup"><span data-stu-id="b4651-224">Adaptive cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="b4651-225">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="b4651-225">Adaptive cards</span></span>

<span data-ttu-id="b4651-226">Les cartes adaptatives peuvent être authored dans un bot et affichées dans plusieurs applications telles que Teams, votre site web, etc.</span><span class="sxs-lookup"><span data-stu-id="b4651-226">Adaptive cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="b4651-227">Pour plus d’informations, voir [cartes adaptatives.](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="b4651-227">For more information, see [adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="b4651-228">Le code suivant illustre un exemple d’envoi d’une carte adaptative simple :</span><span class="sxs-lookup"><span data-stu-id="b4651-228">The following code shows an example of sending a simple adaptive card:</span></span>

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

<span data-ttu-id="b4651-229">Pour en savoir plus sur les cartes et les cartes dans les bots, consultez [la documentation des cartes.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="b4651-229">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="b4651-230">La section suivante fournit des réponses de code d’état pour les erreurs générées à partir des API bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-230">The next section provides status code responses for errors generated from Bot APIs.</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="b4651-231">Réponses de code d’état</span><span class="sxs-lookup"><span data-stu-id="b4651-231">Status code responses</span></span>

<span data-ttu-id="b4651-232">Voici les codes d’état, leur code d’erreur et leurs valeurs de message :</span><span class="sxs-lookup"><span data-stu-id="b4651-232">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="b4651-233">Code d'état</span><span class="sxs-lookup"><span data-stu-id="b4651-233">Status code</span></span> | <span data-ttu-id="b4651-234">Code d’erreur et valeurs de message</span><span class="sxs-lookup"><span data-stu-id="b4651-234">Error code and message values</span></span> | <span data-ttu-id="b4651-235">Description</span><span class="sxs-lookup"><span data-stu-id="b4651-235">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="b4651-236">403</span><span class="sxs-lookup"><span data-stu-id="b4651-236">403</span></span> | <span data-ttu-id="b4651-237">**Code**: `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="b4651-237">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="b4651-238">**Message**: « L’utilisateur a bloqué la conversation avec le bot. »</span><span class="sxs-lookup"><span data-stu-id="b4651-238">**Message**: "User blocked the conversation with the bot."</span></span> | <span data-ttu-id="b4651-239">L’utilisateur a bloqué le bot dans une conversation en une:1 ou dans un canal via les paramètres de modération.</span><span class="sxs-lookup"><span data-stu-id="b4651-239">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="b4651-240">403</span><span class="sxs-lookup"><span data-stu-id="b4651-240">403</span></span> | <span data-ttu-id="b4651-241">**Code**: `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="b4651-241">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="b4651-242">**Message**: « Le bot ne fait pas partie de la liste de conversation. »</span><span class="sxs-lookup"><span data-stu-id="b4651-242">**Message**: "The bot is not part of the conversation roster."</span></span> | <span data-ttu-id="b4651-243">Le bot ne fait pas partie de la conversation.</span><span class="sxs-lookup"><span data-stu-id="b4651-243">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="b4651-244">403</span><span class="sxs-lookup"><span data-stu-id="b4651-244">403</span></span> | <span data-ttu-id="b4651-245">**Code**: `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="b4651-245">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="b4651-246">**Message**: « L’administrateur client a désactivé ce bot. »</span><span class="sxs-lookup"><span data-stu-id="b4651-246">**Message**: "The tenant admin disabled this bot."</span></span> | <span data-ttu-id="b4651-247">Le client a bloqué le bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-247">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="b4651-248">401</span><span class="sxs-lookup"><span data-stu-id="b4651-248">401</span></span> | <span data-ttu-id="b4651-249">**Code**: `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="b4651-249">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="b4651-250">**Message**: « Aucune inscription trouvée pour ce bot. »</span><span class="sxs-lookup"><span data-stu-id="b4651-250">**Message**: “No registration found for this bot.”</span></span> | <span data-ttu-id="b4651-251">L’inscription de ce bot est in trouvée.</span><span class="sxs-lookup"><span data-stu-id="b4651-251">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="b4651-252">412</span><span class="sxs-lookup"><span data-stu-id="b4651-252">412</span></span> | <span data-ttu-id="b4651-253">**Code**: `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="b4651-253">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="b4651-254">**Message :**« Échec de la condition préalable, veuillez essayer à nouveau. »</span><span class="sxs-lookup"><span data-stu-id="b4651-254">**Message**: “Precondition failed, please try again.”</span></span> | <span data-ttu-id="b4651-255">Une condition préalable a échoué sur l’une de nos dépendances en raison de plusieurs opérations simultanées sur la même conversation.</span><span class="sxs-lookup"><span data-stu-id="b4651-255">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="b4651-256">404</span><span class="sxs-lookup"><span data-stu-id="b4651-256">404</span></span> | <span data-ttu-id="b4651-257">**Code**: `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="b4651-257">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="b4651-258">**Message**: « Conversation in trouvée ».</span><span class="sxs-lookup"><span data-stu-id="b4651-258">**Message**: “Conversation not found.”</span></span> | <span data-ttu-id="b4651-259">La conversation est in trouvée.</span><span class="sxs-lookup"><span data-stu-id="b4651-259">The conversation was not found.</span></span> |
| <span data-ttu-id="b4651-260">413</span><span class="sxs-lookup"><span data-stu-id="b4651-260">413</span></span> | <span data-ttu-id="b4651-261">**Code**: `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="b4651-261">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="b4651-262">**Message**: « Taille du message trop grande. »</span><span class="sxs-lookup"><span data-stu-id="b4651-262">**Message**: “Message size too large.”</span></span> | <span data-ttu-id="b4651-263">La taille de la demande entrante était trop importante.</span><span class="sxs-lookup"><span data-stu-id="b4651-263">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="b4651-264">429</span><span class="sxs-lookup"><span data-stu-id="b4651-264">429</span></span> | <span data-ttu-id="b4651-265">**Code**: `Throttled`</span><span class="sxs-lookup"><span data-stu-id="b4651-265">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="b4651-266">**Message**: « Trop de demandes . »</span><span class="sxs-lookup"><span data-stu-id="b4651-266">**Message**: “Too many requests.”</span></span> <span data-ttu-id="b4651-267">Renvoie également quand réessayer après.</span><span class="sxs-lookup"><span data-stu-id="b4651-267">Also returns when to retry after.</span></span> | <span data-ttu-id="b4651-268">Trop de demandes ont été envoyées par le bot.</span><span class="sxs-lookup"><span data-stu-id="b4651-268">Too many requests were sent by the bot.</span></span> <span data-ttu-id="b4651-269">Pour plus d’informations, voir [limite de taux.](~/bots/how-to/rate-limit.md)</span><span class="sxs-lookup"><span data-stu-id="b4651-269">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

<span data-ttu-id="b4651-270">La section suivante illustre un exemple de code simple qui incorpore le flux de conversation de base dans une application Teams.</span><span class="sxs-lookup"><span data-stu-id="b4651-270">The next section illustrates a simple code sample that incorporates basic conversational flow into a Teams application.</span></span>

## <a name="code-sample"></a><span data-ttu-id="b4651-271">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="b4651-271">Code sample</span></span>

<span data-ttu-id="b4651-272">Voici les exemples de code pour le bot de conversation Teams :</span><span class="sxs-lookup"><span data-stu-id="b4651-272">Following are the code samples for Teams conversation bot:</span></span>

|<span data-ttu-id="b4651-273">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="b4651-273">Sample name</span></span> | <span data-ttu-id="b4651-274">Description</span><span class="sxs-lookup"><span data-stu-id="b4651-274">Description</span></span> | <span data-ttu-id="b4651-275">. NETCore</span><span class="sxs-lookup"><span data-stu-id="b4651-275">.NETCore</span></span> | <span data-ttu-id="b4651-276">Node.js</span><span class="sxs-lookup"><span data-stu-id="b4651-276">Node.js</span></span> | <span data-ttu-id="b4651-277">Python</span><span class="sxs-lookup"><span data-stu-id="b4651-277">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="b4651-278">Bot de conversation Teams</span><span class="sxs-lookup"><span data-stu-id="b4651-278">Teams conversation bot</span></span> | <span data-ttu-id="b4651-279">Gestion des événements de messagerie et de conversation.</span><span class="sxs-lookup"><span data-stu-id="b4651-279">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="b4651-280">View</span><span class="sxs-lookup"><span data-stu-id="b4651-280">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="b4651-281">View</span><span class="sxs-lookup"><span data-stu-id="b4651-281">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="b4651-282">View</span><span class="sxs-lookup"><span data-stu-id="b4651-282">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="b4651-283">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b4651-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4651-284">Envoi de messages proactifs</span><span class="sxs-lookup"><span data-stu-id="b4651-284">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="b4651-285">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="b4651-285">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="b4651-286">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b4651-286">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4651-287">Menus de commande du bot</span><span class="sxs-lookup"><span data-stu-id="b4651-287">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
