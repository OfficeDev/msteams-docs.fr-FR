---
title: Conversations de canal et de groupe
author: clearab
description: Procédure d’envoi, de réception et de gestion des messages pour un bot dans un canal ou une conversation de groupe.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ada2839ba41e4004b5f48449f4e057830dd841b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673939"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="16e2e-103">Conversations de conversation de groupe et de canal avec un robot Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="16e2e-103">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="16e2e-104">En ajoutant l' `teams` étendue `groupchat` ou à votre robot, celle-ci peut être disponible pour être installée dans une conversation d’équipe ou de groupe.</span><span class="sxs-lookup"><span data-stu-id="16e2e-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="16e2e-105">Cela permet à tous les membres de la conversation d’interagir avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="16e2e-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="16e2e-106">Une fois installé, il aura accès aux métadonnées relatives à la conversation, comme la liste des membres de conversation, et, lorsqu’elle est installée dans une équipe, les détails de cette équipe et la liste complète des canaux.</span><span class="sxs-lookup"><span data-stu-id="16e2e-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="16e2e-107">Les robots d’un groupe ou d’un canal reçoivent uniquement les messages lorsqu’ils sont mentionnés (« @botname »), mais ils ne reçoivent pas les autres messages envoyés à la conversation.</span><span class="sxs-lookup"><span data-stu-id="16e2e-107">Bots in a group or channel only receive messages when they are mentioned ("@botname"), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="16e2e-108">Le bot doit être @mentioned directement.</span><span class="sxs-lookup"><span data-stu-id="16e2e-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="16e2e-109">Votre bot ne reçoit pas de message lorsque l’équipe ou le canal est mentionné, ou lorsqu’un utilisateur répond à un message de votre robot sans le @mentioning.</span><span class="sxs-lookup"><span data-stu-id="16e2e-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-considerations"></a><span data-ttu-id="16e2e-110">Considérations en matière de conception</span><span class="sxs-lookup"><span data-stu-id="16e2e-110">Design considerations</span></span>

<span data-ttu-id="16e2e-111">Un bot doit fournir des informations qui sont à la fois appropriées et pertinentes pour tous les membres d’un groupe ou d’un canal.</span><span class="sxs-lookup"><span data-stu-id="16e2e-111">A bot should provide information that is both appropriate and relevant to all members in a group or channel.</span></span> <span data-ttu-id="16e2e-112">Les conversations avec celles-ci sont visibles par tous les membres du groupe ou du canal.</span><span class="sxs-lookup"><span data-stu-id="16e2e-112">Conversations with it are visible to everyone that is a part of the group or channel.</span></span> <span data-ttu-id="16e2e-113">Un robot bien conçu peut ajouter de la valeur à tous les utilisateurs tout en ne partageant pas d’informations plus appropriées dans une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="16e2e-113">A well designed bot can add value to all users while not inadvertently sharing information that is more appropriate in a one-to-one conversation.</span></span> <span data-ttu-id="16e2e-114">Les conversations à plusieurs tours comme les boîtes de dialogue doivent être évitées-utilisez des cartes et/ou des modules de tâches pour collecter des informations à la place.</span><span class="sxs-lookup"><span data-stu-id="16e2e-114">Multi-turn conversations like dialogs should be avoided - use cards and/or task modules to collect information instead.</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="16e2e-115">Création de threads de conversation</span><span class="sxs-lookup"><span data-stu-id="16e2e-115">Creating new conversation threads</span></span>

<span data-ttu-id="16e2e-116">Lorsque votre bot est installé dans une équipe, il est parfois nécessaire de créer un nouveau fil de conversation au lieu de répondre à un thread existant.</span><span class="sxs-lookup"><span data-stu-id="16e2e-116">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="16e2e-117">Il s’agit d’une forme de [messagerie proactive](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="16e2e-117">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with--mentions"></a><span data-ttu-id="16e2e-118">Utilisation de @ mentions</span><span class="sxs-lookup"><span data-stu-id="16e2e-118">Working with @ Mentions</span></span>

<span data-ttu-id="16e2e-119">Chaque message de votre bot à partir d’un groupe ou d’un canal contient un @mention avec son propre nom dans le texte du message, vous devez donc veiller à ce que les handles d’analyse de message soient pris en charge.</span><span class="sxs-lookup"><span data-stu-id="16e2e-119">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="16e2e-120">Votre robot peut également récupérer d’autres utilisateurs mentionnés dans un message et ajouter des mentions aux messages qu’il envoie.</span><span class="sxs-lookup"><span data-stu-id="16e2e-120">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="16e2e-121">Suppression des mentions du texte d’un message</span><span class="sxs-lookup"><span data-stu-id="16e2e-121">Stripping mentions from message text</span></span>

<span data-ttu-id="16e2e-122">Il peut s’avérer nécessaire de supprimer le @mentions du texte du message reçu par votre robot.</span><span class="sxs-lookup"><span data-stu-id="16e2e-122">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="16e2e-123">Récupération des mentions</span><span class="sxs-lookup"><span data-stu-id="16e2e-123">Retrieving mentions</span></span>

<span data-ttu-id="16e2e-124">Les mentions sont renvoyées `entities` dans l’objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de l’utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="16e2e-124">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="16e2e-125">Le texte du message inclut également la mention like `<at>@John Smith<at>`.</span><span class="sxs-lookup"><span data-stu-id="16e2e-125">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="16e2e-126">Toutefois, vous ne devez pas compter sur le texte du message pour récupérer des informations sur l’utilisateur ; Il est possible que la personne qui envoie le message le modifie.</span><span class="sxs-lookup"><span data-stu-id="16e2e-126">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="16e2e-127">À la place, `entities` utilisez l’objet.</span><span class="sxs-lookup"><span data-stu-id="16e2e-127">Instead, use the `entities` object.</span></span>

<span data-ttu-id="16e2e-128">Vous pouvez récupérer toutes les mentions dans le message en appelant `GetMentions` la fonction dans le kit de développement logiciel (SDK) `Mention` du générateur de robots, qui renvoie un tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="16e2e-128">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="16e2e-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="16e2e-129">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="16e2e-130">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="16e2e-130">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="16e2e-131">JSON</span><span class="sxs-lookup"><span data-stu-id="16e2e-131">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="16e2e-132">Python</span><span class="sxs-lookup"><span data-stu-id="16e2e-132">Python</span></span>](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="16e2e-133">Ajout de mentions à vos messages</span><span class="sxs-lookup"><span data-stu-id="16e2e-133">Adding mentions to your messages</span></span>

<span data-ttu-id="16e2e-134">Votre robot peut mentionner d’autres utilisateurs dans les messages publiés dans des canaux.</span><span class="sxs-lookup"><span data-stu-id="16e2e-134">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="16e2e-135">Pour ce faire, votre message doit effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="16e2e-135">To do this, your message must do the following:</span></span>

<span data-ttu-id="16e2e-136">L' `Mention` objet possède deux propriétés que vous devrez définir :</span><span class="sxs-lookup"><span data-stu-id="16e2e-136">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="16e2e-137">Inclure <at>@username</at> dans le texte du message</span><span class="sxs-lookup"><span data-stu-id="16e2e-137">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="16e2e-138">Inclure l’objet « mention » à l’intérieur de la collection Entities</span><span class="sxs-lookup"><span data-stu-id="16e2e-138">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="16e2e-139">Le kit de développement logiciel (SDK) de l’infrastructure fournit des méthodes et des objets d’assistance pour faciliter la création de la mention.</span><span class="sxs-lookup"><span data-stu-id="16e2e-139">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="16e2e-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="16e2e-140">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="16e2e-141">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="16e2e-141">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="16e2e-142">JSON</span><span class="sxs-lookup"><span data-stu-id="16e2e-142">JSON</span></span>](#tab/json)

<span data-ttu-id="16e2e-143">Le `text` champ dans l’objet dans le `entities` tableau doit correspondre *exactement* à une partie du champ `text` de message.</span><span class="sxs-lookup"><span data-stu-id="16e2e-143">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="16e2e-144">Si ce n’est pas le cas, la mention sera ignorée.</span><span class="sxs-lookup"><span data-stu-id="16e2e-144">If it does not, the mention will be ignored.</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="16e2e-145">Python</span><span class="sxs-lookup"><span data-stu-id="16e2e-145">Python</span></span>](#tab/python)

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

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="16e2e-146">Envoi d’un message lors de l’installation</span><span class="sxs-lookup"><span data-stu-id="16e2e-146">Sending a message on installation</span></span>

<span data-ttu-id="16e2e-147">Lorsque votre bot est d’abord ajouté au groupe ou à l’équipe, il peut s’avérer utile d’envoyer un message le mettant en place.</span><span class="sxs-lookup"><span data-stu-id="16e2e-147">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="16e2e-148">Le message doit fournir une brève description des fonctionnalités du bot et comment les utiliser.</span><span class="sxs-lookup"><span data-stu-id="16e2e-148">The message should provide a brief description of the bot’s features, and how to use them.</span></span> <span data-ttu-id="16e2e-149">Vous pouvez vous abonner à l' `conversationUpdate` événement, avec le `teamMemberAdded` EventType.</span><span class="sxs-lookup"><span data-stu-id="16e2e-149">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="16e2e-150">Étant donné que l’événement est envoyé lorsqu’un nouveau membre d’équipe est ajouté, vous devez vérifier si le nouveau membre ajouté est le bot.</span><span class="sxs-lookup"><span data-stu-id="16e2e-150">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="16e2e-151">Pour plus d’informations, consultez la rubrique [envoi d’un message de bienvenue à un nouveau membre](~/bots/how-to/conversations/send-proactive-messages.md) de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="16e2e-151">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="16e2e-152">Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté.</span><span class="sxs-lookup"><span data-stu-id="16e2e-152">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="16e2e-153">Pour ce faire, vous pouvez obtenir la liste de l’équipe et envoyer un message direct à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="16e2e-153">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="16e2e-154">Il n’est pas recommandé d’envoyer un message dans les situations suivantes :</span><span class="sxs-lookup"><span data-stu-id="16e2e-154">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="16e2e-155">L’équipe est grande (évidemment subjective, mais par exemple, plus de 100 membres).</span><span class="sxs-lookup"><span data-stu-id="16e2e-155">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="16e2e-156">Votre robot peut être considéré comme « spammer » et la personne qui l’a ajouté peut recevoir des plaintes, sauf si vous communiquez clairement la proposition de valeur de votre robot à tous ceux qui voient le message de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="16e2e-156">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="16e2e-157">Votre robot est d’abord mentionné dans un groupe ou un canal (et n’est pas d’abord ajouté à une équipe)</span><span class="sxs-lookup"><span data-stu-id="16e2e-157">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="16e2e-158">Un groupe ou un canal est renommé.</span><span class="sxs-lookup"><span data-stu-id="16e2e-158">A group or channel is renamed</span></span>
* <span data-ttu-id="16e2e-159">Un membre de l’équipe est ajouté à un groupe ou à un canal</span><span class="sxs-lookup"><span data-stu-id="16e2e-159">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="16e2e-160">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="16e2e-160">Learn more</span></span>

<span data-ttu-id="16e2e-161">Votre bot a accès à des informations supplémentaires sur la conversation de groupe ou sur l’équipe dans laquelle il est installé.</span><span class="sxs-lookup"><span data-stu-id="16e2e-161">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="16e2e-162">Consultez la rubrique [obtenir le contexte teams](~/bots/how-to/get-teams-context.md) pour en savoir plus sur les API disponibles pour votre robot.</span><span class="sxs-lookup"><span data-stu-id="16e2e-162">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="16e2e-163">Il existe également des événements supplémentaires auxquels votre bot peut s’abonner et auquel il répond.</span><span class="sxs-lookup"><span data-stu-id="16e2e-163">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="16e2e-164">Pour en savoir plus, consultez la rubrique [s’abonner aux événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md) .</span><span class="sxs-lookup"><span data-stu-id="16e2e-164">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
