---
title: Conversations de canal et de groupe avec un bot
author: clearab
description: Comment envoyer, recevoir et gérer des messages pour un bot dans une conversation de canal ou de groupe.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797840"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="6779b-103">Conversations de canal et de groupe avec un bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6779b-103">Channel and group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="6779b-104">En ajoutant `teams` l’étendue ou l’étendue à votre bot, elle peut être installée dans une conversation d’équipe `groupchat` ou de groupe.</span><span class="sxs-lookup"><span data-stu-id="6779b-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="6779b-105">Cela permet à tous les membres de la conversation d’interagir avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="6779b-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="6779b-106">Une fois l’installation terminée, ils auront également accès aux métadonnées relatives à la conversation, telles que la liste des membres de la conversation. Si elle est installée dans une équipe, ils auront également accès aux détails de l’équipe et à la liste complète des canaux.</span><span class="sxs-lookup"><span data-stu-id="6779b-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="6779b-107">Les bots d’un groupe ou d’un canal reçoivent des messages uniquement lorsqu’ils sont mentionnés (@botname), ils ne reçoivent aucun autre message envoyé à la conversation.</span><span class="sxs-lookup"><span data-stu-id="6779b-107">Bots in a group or channel only receive messages when they are mentioned (@botname), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="6779b-108">Le robot doit être @mentionné directement.</span><span class="sxs-lookup"><span data-stu-id="6779b-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="6779b-109">Votre bot ne reçoit pas de message lorsque l’équipe ou le canal est mentionné, ou lorsqu’une personne répond à un message de votre bot sans @mentioning le.</span><span class="sxs-lookup"><span data-stu-id="6779b-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="6779b-110">Instructions de conception</span><span class="sxs-lookup"><span data-stu-id="6779b-110">Design guidelines</span></span>

<span data-ttu-id="6779b-111">Découvrez comment concevoir [des conversations de bot dans des canaux et des conversations.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="6779b-111">See how to [design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="6779b-112">Création de threads de conversation</span><span class="sxs-lookup"><span data-stu-id="6779b-112">Creating new conversation threads</span></span>

<span data-ttu-id="6779b-113">Lorsque votre bot est installé dans une équipe, il peut parfois être nécessaire de créer un thread de conversation plutôt que de répondre à un thread existant.</span><span class="sxs-lookup"><span data-stu-id="6779b-113">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="6779b-114">Il s’agit d’une [forme de messagerie proactive.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="6779b-114">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="6779b-115">Travailler avec des mentions</span><span class="sxs-lookup"><span data-stu-id="6779b-115">Working with mentions</span></span>

<span data-ttu-id="6779b-116">Tous les messages à votre robot provenant d’un groupe ou d’un canal contiennent une @mention avec son propre nom dans le texte du message. Vous devez donc vous assurer que l’analyse de message gère cela.</span><span class="sxs-lookup"><span data-stu-id="6779b-116">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="6779b-117">Votre robot peut également récupérer d’autres utilisateurs mentionnés dans un message et ajouter des mentions à tous les messages qu’il envoie.</span><span class="sxs-lookup"><span data-stu-id="6779b-117">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="6779b-118">Faire trébucher des mentions à partir du texte du message</span><span class="sxs-lookup"><span data-stu-id="6779b-118">Stripping mentions from message text</span></span>

<span data-ttu-id="6779b-119">Il se peut que vous deviez retirer les @mentions du texte du message reçu par votre robot.</span><span class="sxs-lookup"><span data-stu-id="6779b-119">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="6779b-120">Récupération des mentions</span><span class="sxs-lookup"><span data-stu-id="6779b-120">Retrieving mentions</span></span>

<span data-ttu-id="6779b-121">Les mentions sont renvoyées dans l’objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de `entities` l’utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="6779b-121">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="6779b-122">Le texte du message inclut également la mention telle que `<at>@John Smith<at>`.</span><span class="sxs-lookup"><span data-stu-id="6779b-122">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="6779b-123">Toutefois, vous ne devez pas vous appuyer sur le texte du message pour récupérer des informations sur l’utilisateur . il est possible pour la personne qui envoie le message de le modifier.</span><span class="sxs-lookup"><span data-stu-id="6779b-123">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="6779b-124">Utilisez plutôt `entities` l’objet.</span><span class="sxs-lookup"><span data-stu-id="6779b-124">Instead, use the `entities` object.</span></span>

<span data-ttu-id="6779b-125">Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction dans le SDK Bot Builder qui renvoie `GetMentions` un tableau `Mention` d’objets.</span><span class="sxs-lookup"><span data-stu-id="6779b-125">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6779b-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6779b-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6779b-127">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6779b-127">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="6779b-128">JSON</span><span class="sxs-lookup"><span data-stu-id="6779b-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="6779b-129">Python</span><span class="sxs-lookup"><span data-stu-id="6779b-129">Python</span></span>](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="6779b-130">Ajout de mentions à vos messages</span><span class="sxs-lookup"><span data-stu-id="6779b-130">Adding mentions to your messages</span></span>

<span data-ttu-id="6779b-131">Votre bot peut mentionner d’autres utilisateurs dans les messages publiés dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="6779b-131">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="6779b-132">Pour ce faire, votre message doit :</span><span class="sxs-lookup"><span data-stu-id="6779b-132">To do this, your message must do the following:</span></span>

<span data-ttu-id="6779b-133">`Mention`L’objet possède deux propriétés que vous devrez définir :</span><span class="sxs-lookup"><span data-stu-id="6779b-133">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="6779b-134">Inclure <at>@username</at> dans le texte du message</span><span class="sxs-lookup"><span data-stu-id="6779b-134">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="6779b-135">Inclure l’objet mention à l’intérieur de la collection entities</span><span class="sxs-lookup"><span data-stu-id="6779b-135">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="6779b-136">Le SDK Bot Framework fournit des méthodes d’aide et des objets pour faciliter la construction de la mention.</span><span class="sxs-lookup"><span data-stu-id="6779b-136">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6779b-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6779b-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6779b-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6779b-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="6779b-139">JSON</span><span class="sxs-lookup"><span data-stu-id="6779b-139">JSON</span></span>](#tab/json)

<span data-ttu-id="6779b-140">Le champ de l’objet dans le tableau doit correspondre exactement à une `text` partie du champ de `entities`  `text` message.</span><span class="sxs-lookup"><span data-stu-id="6779b-140">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="6779b-141">Si ce n’est pas le cas, la mention sera ignorée.</span><span class="sxs-lookup"><span data-stu-id="6779b-141">If it does not, the mention will be ignored.</span></span>

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="6779b-142">Python</span><span class="sxs-lookup"><span data-stu-id="6779b-142">Python</span></span>](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="6779b-143">Envoi d’un message lors de l’installation</span><span class="sxs-lookup"><span data-stu-id="6779b-143">Sending a message on installation</span></span>

<span data-ttu-id="6779b-144">Lorsque votre bot est ajouté pour la première fois au groupe ou à l’équipe, il peut être utile d’envoyer un message le présentant.</span><span class="sxs-lookup"><span data-stu-id="6779b-144">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="6779b-145">Le message doit fournir une brève description des fonctionnalités du bot et de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="6779b-145">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="6779b-146">Vous souhaiterez vous abonner à `conversationUpdate` l’événement, avec `teamMemberAdded` eventType.</span><span class="sxs-lookup"><span data-stu-id="6779b-146">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="6779b-147">Étant donné que l’événement est envoyé lorsqu’un nouveau membre d’équipe est ajouté, vous devez vérifier si le nouveau membre ajouté est le bot.</span><span class="sxs-lookup"><span data-stu-id="6779b-147">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="6779b-148">Pour [plus d’informations, voir](~/bots/how-to/conversations/send-proactive-messages.md) Envoyer un message de bienvenue à un nouveau membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="6779b-148">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="6779b-149">Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté.</span><span class="sxs-lookup"><span data-stu-id="6779b-149">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="6779b-150">Pour ce faire, vous pouvez obtenir la liste de l’équipe et envoyer un message direct à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6779b-150">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="6779b-151">Il n’est pas recommandé d’envoyer un message dans les situations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6779b-151">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="6779b-152">L’équipe est volumineuse (évidemment subjectif, mais par exemple plus de 100 membres).</span><span class="sxs-lookup"><span data-stu-id="6779b-152">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="6779b-153">Votre bot peut être considéré comme « spammy » et la personne qui l’a ajouté peut obtenir des réclamations, sauf si vous communiquez clairement la proposition de valeur de votre bot à toutes les personnes qui voient le message de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="6779b-153">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="6779b-154">Votre bot est d’abord mentionné dans un groupe ou un canal (plutôt que d’être ajouté pour la première fois à une équipe)</span><span class="sxs-lookup"><span data-stu-id="6779b-154">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="6779b-155">Un groupe ou un canal est renommé</span><span class="sxs-lookup"><span data-stu-id="6779b-155">A group or channel is renamed</span></span>
* <span data-ttu-id="6779b-156">Un membre d’équipe est ajouté à un groupe ou un canal</span><span class="sxs-lookup"><span data-stu-id="6779b-156">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="6779b-157">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="6779b-157">Learn more</span></span>

<span data-ttu-id="6779b-158">Votre bot a accès à des informations supplémentaires sur la conversation de groupe ou l’équipe dans qui il est installé.</span><span class="sxs-lookup"><span data-stu-id="6779b-158">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="6779b-159">Consultez [le contexte teams pour](~/bots/how-to/get-teams-context.md) obtenir des API supplémentaires disponibles pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="6779b-159">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="6779b-160">Votre bot peut également s’abonner à des événements supplémentaires et y répondre.</span><span class="sxs-lookup"><span data-stu-id="6779b-160">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="6779b-161">Pour savoir [comment s’abonner aux événements de conversation,](~/bots/how-to/conversations/subscribe-to-conversation-events.md) voir s’abonner à des événements de conversation.</span><span class="sxs-lookup"><span data-stu-id="6779b-161">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
