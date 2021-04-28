---
title: Messages dans les conversations des robots
description: Décrit les méthodes de conversation avec un bot Microsoft Teams
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 5b23e3b2548e3d0eab98fae73d37316063fe60c1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058599"
---
# <a name="messages-in-bot-conversations"></a><span data-ttu-id="cb2dc-103">Messages dans les conversations des robots</span><span class="sxs-lookup"><span data-stu-id="cb2dc-103">Messages in bot conversations</span></span>

<span data-ttu-id="cb2dc-104">Chaque message d'une conversation est `Activity` un objet de type `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="cb2dc-104">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="cb2dc-105">Lorsqu'un utilisateur envoie un message, Teams publie le message à votre bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-105">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="cb2dc-106">Teams envoie un objet JSON au point de terminaison de messagerie de votre bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-106">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="cb2dc-107">Votre bot examine le message pour déterminer son type et répond en conséquence.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-107">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="cb2dc-108">Les conversations de base sont gérées via le connecteur Bot Framework, une API REST unique.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-108">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="cb2dc-109">Cette API permet à votre bot de communiquer avec Teams et d'autres canaux.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-109">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="cb2dc-110">Le SDK Bot Builder fournit les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-110">The Bot Builder SDK provides the following features:</span></span>

* <span data-ttu-id="cb2dc-111">Accès facile au connecteur Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-111">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="cb2dc-112">Fonctionnalités supplémentaires pour gérer le flux et l'état des conversations.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-112">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="cb2dc-113">Méthodes simples pour incorporer des services cognitives, tels que le traitement du langage naturel (NLP).</span><span class="sxs-lookup"><span data-stu-id="cb2dc-113">Simple ways to incorporate cognitive services, such as natural language processing (NLP).</span></span>

<span data-ttu-id="cb2dc-114">Votre bot reçoit des messages de Teams à l'aide de la propriété et envoie une ou plusieurs réponses aux `Text` messages aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-114">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="cb2dc-115">Recevoir un message</span><span class="sxs-lookup"><span data-stu-id="cb2dc-115">Receive a message</span></span>

<span data-ttu-id="cb2dc-116">Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-116">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="cb2dc-117">Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-117">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="cb2dc-118">Le code suivant montre un exemple de réception d'un message :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-118">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="cb2dc-119">C#</span><span class="sxs-lookup"><span data-stu-id="cb2dc-119">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="cb2dc-120">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cb2dc-120">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="cb2dc-121">Python</span><span class="sxs-lookup"><span data-stu-id="cb2dc-121">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="cb2dc-122">JSON</span><span class="sxs-lookup"><span data-stu-id="cb2dc-122">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="cb2dc-123">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="cb2dc-123">Send a message</span></span>

<span data-ttu-id="cb2dc-124">Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-124">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="cb2dc-125">Dans le handler d'activité du bot, utilisez la méthode de l'objet de contexte turn pour `SendActivityAsync` envoyer une seule réponse de message.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-125">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="cb2dc-126">Utilisez la méthode de l'objet `SendActivitiesAsync` pour envoyer plusieurs réponses à la fois.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-126">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span>

<span data-ttu-id="cb2dc-127">Le code suivant montre un exemple d'envoi d'un message lorsqu'un utilisateur est ajouté à une conversation :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-127">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

# <a name="c"></a>[<span data-ttu-id="cb2dc-128">C#</span><span class="sxs-lookup"><span data-stu-id="cb2dc-128">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="cb2dc-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cb2dc-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="cb2dc-130">Python</span><span class="sxs-lookup"><span data-stu-id="cb2dc-130">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="cb2dc-131">JSON</span><span class="sxs-lookup"><span data-stu-id="cb2dc-131">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="cb2dc-132">Le fractionnement de message se produit lorsqu'un message texte et une pièce jointe sont envoyés dans la même charge utile d'activité.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-132">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="cb2dc-133">Cette activité est divisée en activités distinctes par Microsoft Teams, l'une avec un message texte et l'autre avec une pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-133">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="cb2dc-134">Lorsque l'activité est fractionée, vous ne recevez pas [](~/bots/how-to/update-and-delete-bot-messages.md) l'ID du message en réponse, qui est utilisé pour mettre à jour ou supprimer le message de manière proactive.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-134">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="cb2dc-135">Il est recommandé d'envoyer des activités distinctes au lieu de dépendre du fractionnement des messages.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-135">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="cb2dc-136">Les messages envoyés entre les utilisateurs et les bots incluent des données de canal interne dans le message.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-136">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="cb2dc-137">Ces données permettent au bot de communiquer correctement sur ce canal.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-137">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="cb2dc-138">Le SDK Bot Builder vous permet de modifier la structure des messages.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-138">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="cb2dc-139">Données de canal Teams</span><span class="sxs-lookup"><span data-stu-id="cb2dc-139">Teams channel data</span></span>

<span data-ttu-id="cb2dc-140">L'objet contient des informations spécifiques à Teams et est une source définitive pour les ID d'équipe et `channelData` de canal.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-140">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="cb2dc-141">Si vous le souhaitez, vous pouvez mettre en cache et utiliser ces ID comme clés pour le stockage local.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-141">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="cb2dc-142">Le `TeamsActivityHandler` SDK dans le SDK retire des informations importantes de `channelData` l'objet pour les rendre facilement accessibles.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-142">The `TeamsActivityHandler` in the SDK pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="cb2dc-143">Toutefois, vous pouvez toujours accéder aux données d'origine à partir de `turnContext` l'objet.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-143">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="cb2dc-144">L'objet n'est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en `channelData` dehors d'un canal.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-144">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="cb2dc-145">Un objet `channelData` type dans une activité envoyée à votre bot contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-145">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="cb2dc-146">`eventType`: Type d'événement Teams transmis uniquement en cas d'événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-146">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="cb2dc-147">`tenant.id`: ID de client Azure Active Directory transmis dans tous les contextes.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-147">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="cb2dc-148">`team`: Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-148">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="cb2dc-149">`id`: GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-149">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="cb2dc-150">`name`: Nom de l'équipe transmis uniquement en cas d'événements [de changement de nom d'équipe.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-150">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="cb2dc-151">`channel`: Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-151">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="cb2dc-152">`id`: GUID du canal.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-152">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="cb2dc-153">`name`: Nom du canal transmis uniquement en cas d'événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-153">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="cb2dc-154">`channelData.teamsTeamId`: Deprecated.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-154">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="cb2dc-155">Cette propriété est incluse uniquement pour la compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-155">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="cb2dc-156">`channelData.teamsChannelId`: Deprecated.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-156">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="cb2dc-157">Cette propriété est incluse uniquement pour la compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-157">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-or-channelcreated-event"></a><span data-ttu-id="cb2dc-158">Exemple d'objet channelData ou d'événement channelCreated</span><span class="sxs-lookup"><span data-stu-id="cb2dc-158">Example channelData object or channelCreated event</span></span>

<span data-ttu-id="cb2dc-159">Le code suivant montre un exemple d'objet channelData :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-159">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="cb2dc-160">Les messages reçus ou envoyés à votre bot peuvent inclure différents types de contenu de message.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-160">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="cb2dc-161">Contenu du message</span><span class="sxs-lookup"><span data-stu-id="cb2dc-161">Message content</span></span>

| <span data-ttu-id="cb2dc-162">Format</span><span class="sxs-lookup"><span data-stu-id="cb2dc-162">Format</span></span>    | <span data-ttu-id="cb2dc-163">De l'utilisateur au bot</span><span class="sxs-lookup"><span data-stu-id="cb2dc-163">From user to bot</span></span> | <span data-ttu-id="cb2dc-164">Du bot à l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="cb2dc-164">From bot to user</span></span> | <span data-ttu-id="cb2dc-165">Notes</span><span class="sxs-lookup"><span data-stu-id="cb2dc-165">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="cb2dc-166">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="cb2dc-166">Rich text</span></span> | <span data-ttu-id="cb2dc-167">✔</span><span class="sxs-lookup"><span data-stu-id="cb2dc-167">✔</span></span>                | <span data-ttu-id="cb2dc-168">✔</span><span class="sxs-lookup"><span data-stu-id="cb2dc-168">✔</span></span>                | <span data-ttu-id="cb2dc-169">Votre bot peut envoyer du texte enrichi, des images et des cartes.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-169">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="cb2dc-170">Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-170">Users can send rich text and pictures to your bot.</span></span>                                                                                        |
| <span data-ttu-id="cb2dc-171">Images</span><span class="sxs-lookup"><span data-stu-id="cb2dc-171">Pictures</span></span>  | <span data-ttu-id="cb2dc-172">✔</span><span class="sxs-lookup"><span data-stu-id="cb2dc-172">✔</span></span>                | <span data-ttu-id="cb2dc-173">✔</span><span class="sxs-lookup"><span data-stu-id="cb2dc-173">✔</span></span>                | <span data-ttu-id="cb2dc-174">Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-174">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="cb2dc-175">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-175">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="cb2dc-176">Cartes</span><span class="sxs-lookup"><span data-stu-id="cb2dc-176">Cards</span></span>     | <span data-ttu-id="cb2dc-177">✖</span><span class="sxs-lookup"><span data-stu-id="cb2dc-177">✖</span></span>                | <span data-ttu-id="cb2dc-178">✔</span><span class="sxs-lookup"><span data-stu-id="cb2dc-178">✔</span></span>                | <span data-ttu-id="cb2dc-179">Consultez la référence [de carte Teams pour](~/task-modules-and-cards/cards/cards-reference.md) les cartes pris en charge.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-179">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="cb2dc-180">Emojis</span><span class="sxs-lookup"><span data-stu-id="cb2dc-180">Emojis</span></span>    | <span data-ttu-id="cb2dc-181">✖</span><span class="sxs-lookup"><span data-stu-id="cb2dc-181">✖</span></span>                | <span data-ttu-id="cb2dc-182">✔</span><span class="sxs-lookup"><span data-stu-id="cb2dc-182">✔</span></span>                | <span data-ttu-id="cb2dc-183">Teams prend actuellement en charge les emojis via UTF-16, par exemple U+1F600 pour le visage à l'aide du panoramique.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-183">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="cb2dc-184">Vous pouvez également ajouter des notifications à votre message à l'aide de la `Notification.Alert` propriété.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-184">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="cb2dc-185">Notifications à votre message</span><span class="sxs-lookup"><span data-stu-id="cb2dc-185">Notifications to your message</span></span>

<span data-ttu-id="cb2dc-186">Les notifications avertissent les utilisateurs des nouvelles tâches, mentions et commentaires.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-186">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="cb2dc-187">Ces alertes sont liées à ce sur quoi les utilisateurs travaillent ou ce qu'ils doivent examiner en insérant une notification dans leur flux d'activités.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-187">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="cb2dc-188">Pour que les notifications se déclenchent à partir de votre message bot, définissez la propriété `TeamsChannelData` des objets sur `Notification.Alert` *true*.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-188">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to *true*.</span></span> <span data-ttu-id="cb2dc-189">Le fait qu'une notification soit ou non élevée dépend des paramètres Teams de l'utilisateur individuel et vous ne pouvez pas remplacer ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-189">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="cb2dc-190">Le type de notification est soit une bannière, soit une bannière et un e-mail.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-190">The notification type is either a banner, or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="cb2dc-191">Le **champ Résumé** affiche tout texte de l'utilisateur en tant que message de notification dans le flux.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-191">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="cb2dc-192">Le code suivant montre un exemple d'ajout de notifications à votre message :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-192">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="cb2dc-193">C#</span><span class="sxs-lookup"><span data-stu-id="cb2dc-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cb2dc-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cb2dc-194">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="cb2dc-195">Python</span><span class="sxs-lookup"><span data-stu-id="cb2dc-195">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="cb2dc-196">JSON</span><span class="sxs-lookup"><span data-stu-id="cb2dc-196">JSON</span></span>](#tab/json)

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

<span data-ttu-id="cb2dc-197">Pour améliorer votre message, vous pouvez inclure des images en tant que pièces jointes à ce message.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-197">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="cb2dc-198">Messages image</span><span class="sxs-lookup"><span data-stu-id="cb2dc-198">Picture messages</span></span>

<span data-ttu-id="cb2dc-199">Les images sont envoyées en ajoutant des pièces jointes à un message.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-199">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="cb2dc-200">Pour plus d'informations sur les pièces jointes, voir [la documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-200">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="cb2dc-201">Les images peuvent être au maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-201">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="cb2dc-202">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-202">Animated GIF is not supported.</span></span>

<span data-ttu-id="cb2dc-203">Spécifiez la hauteur et la largeur de chaque image à l'aide de XML.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-203">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="cb2dc-204">Dans markdown, la taille par défaut de l'image est 256×256.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-204">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="cb2dc-205">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-205">For example:</span></span>

* <span data-ttu-id="cb2dc-206">Utilisez : `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="cb2dc-206">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="cb2dc-207">N'utilisez pas : `![Duck on a rock](http://aka.ms/Fo983c)` .</span><span class="sxs-lookup"><span data-stu-id="cb2dc-207">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="cb2dc-208">Un bot de conversation peut inclure des cartes adaptatives qui simplifient les flux de travail d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-208">A conversational bot can include Adaptive Cards that simplify business workflows.</span></span> <span data-ttu-id="cb2dc-209">Les cartes adaptatives offrent des champs de texte, de reconnaissance vocale, d'images, de boutons et d'entrée personnalisables enrichis.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-209">Adaptive Cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="cb2dc-210">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="cb2dc-210">Adaptive Cards</span></span>

<span data-ttu-id="cb2dc-211">Les cartes adaptatives peuvent être authored dans un bot et affichées dans plusieurs applications telles que Teams, votre site web, etc.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-211">Adaptive Cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="cb2dc-212">Pour plus d'informations, voir [Cartes adaptatives.](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-212">For more information, see [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="cb2dc-213">Le code suivant illustre un exemple d'envoi d'une carte adaptative simple :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-213">The following code shows an example of sending a simple Adaptive Card:</span></span>

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

<span data-ttu-id="cb2dc-214">Pour en savoir plus sur les cartes et les cartes dans les bots, consultez [la documentation des cartes.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-214">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="cb2dc-215">Réponses de code d'état</span><span class="sxs-lookup"><span data-stu-id="cb2dc-215">Status code responses</span></span>

<span data-ttu-id="cb2dc-216">Voici les codes d'état, leur code d'erreur et leurs valeurs de message :</span><span class="sxs-lookup"><span data-stu-id="cb2dc-216">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="cb2dc-217">Code d'état</span><span class="sxs-lookup"><span data-stu-id="cb2dc-217">Status code</span></span> | <span data-ttu-id="cb2dc-218">Code d'erreur et valeurs de message</span><span class="sxs-lookup"><span data-stu-id="cb2dc-218">Error code and message values</span></span> | <span data-ttu-id="cb2dc-219">Description</span><span class="sxs-lookup"><span data-stu-id="cb2dc-219">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="cb2dc-220">403</span><span class="sxs-lookup"><span data-stu-id="cb2dc-220">403</span></span> | <span data-ttu-id="cb2dc-221">**Code**: `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-221">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="cb2dc-222">**Message :** l'utilisateur a bloqué la conversation avec le bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-222">**Message**: User blocked the conversation with the bot.</span></span> | <span data-ttu-id="cb2dc-223">L'utilisateur a bloqué le bot dans une conversation en une:1 ou dans un canal via les paramètres de modération.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-223">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="cb2dc-224">403</span><span class="sxs-lookup"><span data-stu-id="cb2dc-224">403</span></span> | <span data-ttu-id="cb2dc-225">**Code**: `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-225">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="cb2dc-226">**Message :** le bot ne fait pas partie de la liste des conversations.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-226">**Message**: The bot is not part of the conversation roster.</span></span> | <span data-ttu-id="cb2dc-227">Le bot ne fait pas partie de la conversation.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-227">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="cb2dc-228">403</span><span class="sxs-lookup"><span data-stu-id="cb2dc-228">403</span></span> | <span data-ttu-id="cb2dc-229">**Code**: `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-229">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="cb2dc-230">**Message**: l'administrateur client a désactivé ce bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-230">**Message**: The tenant admin disabled this bot.</span></span> | <span data-ttu-id="cb2dc-231">Le client a bloqué le bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-231">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="cb2dc-232">401</span><span class="sxs-lookup"><span data-stu-id="cb2dc-232">401</span></span> | <span data-ttu-id="cb2dc-233">**Code**: `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-233">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="cb2dc-234">**Message**: aucune inscription trouvée pour ce bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-234">**Message**: No registration found for this bot.</span></span> | <span data-ttu-id="cb2dc-235">L'inscription pour ce bot est in trouvée.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-235">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="cb2dc-236">412</span><span class="sxs-lookup"><span data-stu-id="cb2dc-236">412</span></span> | <span data-ttu-id="cb2dc-237">**Code**: `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-237">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="cb2dc-238">**Message :** la condition préalable a échoué, veuillez essayer à nouveau.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-238">**Message**: Precondition failed, please try again.</span></span> | <span data-ttu-id="cb2dc-239">Une condition préalable a échoué sur l'une de nos dépendances en raison de plusieurs opérations simultanées sur la même conversation.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-239">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="cb2dc-240">404</span><span class="sxs-lookup"><span data-stu-id="cb2dc-240">404</span></span> | <span data-ttu-id="cb2dc-241">**Code**: `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-241">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="cb2dc-242">**Message :** Conversation in trouvée.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-242">**Message**: Conversation not found.</span></span> | <span data-ttu-id="cb2dc-243">La conversation est in trouvée.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-243">The conversation was not found.</span></span> |
| <span data-ttu-id="cb2dc-244">413</span><span class="sxs-lookup"><span data-stu-id="cb2dc-244">413</span></span> | <span data-ttu-id="cb2dc-245">**Code**: `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-245">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="cb2dc-246">**Message :** taille du message trop grande.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-246">**Message**: Message size too large.</span></span> | <span data-ttu-id="cb2dc-247">La taille de la demande entrante était trop importante.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-247">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="cb2dc-248">429</span><span class="sxs-lookup"><span data-stu-id="cb2dc-248">429</span></span> | <span data-ttu-id="cb2dc-249">**Code**: `Throttled`</span><span class="sxs-lookup"><span data-stu-id="cb2dc-249">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="cb2dc-250">**Message**: trop de demandes.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-250">**Message**: Too many requests.</span></span> <span data-ttu-id="cb2dc-251">Renvoie également quand réessayer après.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-251">Also returns when to retry after.</span></span> | <span data-ttu-id="cb2dc-252">Trop de demandes ont été envoyées par le bot.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-252">Too many requests were sent by the bot.</span></span> <span data-ttu-id="cb2dc-253">Pour plus d'informations, voir [limite de taux.](~/bots/how-to/rate-limit.md)</span><span class="sxs-lookup"><span data-stu-id="cb2dc-253">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

## <a name="code-sample"></a><span data-ttu-id="cb2dc-254">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="cb2dc-254">Code sample</span></span>

|<span data-ttu-id="cb2dc-255">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="cb2dc-255">Sample name</span></span> | <span data-ttu-id="cb2dc-256">Description</span><span class="sxs-lookup"><span data-stu-id="cb2dc-256">Description</span></span> | <span data-ttu-id="cb2dc-257">. NETCore</span><span class="sxs-lookup"><span data-stu-id="cb2dc-257">.NETCore</span></span> | <span data-ttu-id="cb2dc-258">Node.js</span><span class="sxs-lookup"><span data-stu-id="cb2dc-258">Node.js</span></span> | <span data-ttu-id="cb2dc-259">Python</span><span class="sxs-lookup"><span data-stu-id="cb2dc-259">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="cb2dc-260">Bot de conversation Teams</span><span class="sxs-lookup"><span data-stu-id="cb2dc-260">Teams conversation bot</span></span> | <span data-ttu-id="cb2dc-261">Gestion des événements de messagerie et de conversation.</span><span class="sxs-lookup"><span data-stu-id="cb2dc-261">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="cb2dc-262">View</span><span class="sxs-lookup"><span data-stu-id="cb2dc-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="cb2dc-263">View</span><span class="sxs-lookup"><span data-stu-id="cb2dc-263">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="cb2dc-264">View</span><span class="sxs-lookup"><span data-stu-id="cb2dc-264">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="cb2dc-265">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cb2dc-265">See also</span></span>

- [<span data-ttu-id="cb2dc-266">Envoyer des messages proactifs</span><span class="sxs-lookup"><span data-stu-id="cb2dc-266">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)

- [<span data-ttu-id="cb2dc-267">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="cb2dc-267">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="cb2dc-268">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="cb2dc-268">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb2dc-269">Menus de commande du bot</span><span class="sxs-lookup"><span data-stu-id="cb2dc-269">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
