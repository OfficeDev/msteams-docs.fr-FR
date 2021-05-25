---
title: Conversations de canal et de groupe avec un bot
author: clearab
description: Comment envoyer, recevoir et gérer des messages pour un bot dans une conversation de canal ou de groupe.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: ef5cf8464fa0e93d5ea3840003a2b0c04a4a5ef5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630998"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a><span data-ttu-id="21616-103">Conversations de canal et de groupe avec un bot</span><span class="sxs-lookup"><span data-stu-id="21616-103">Channel and group chat conversations with a bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="21616-104">Pour installer le bot Microsoft Teams dans une conversation d’équipe ou de groupe, ajoutez l’étendue `teams` `groupchat` ou l’étendue à votre bot.</span><span class="sxs-lookup"><span data-stu-id="21616-104">To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot.</span></span> <span data-ttu-id="21616-105">Cela permet à tous les membres de la conversation d’interagir avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="21616-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="21616-106">Une fois le bot installé, il a accès aux métadonnées sur la conversation, telles que la liste des membres de la conversation.</span><span class="sxs-lookup"><span data-stu-id="21616-106">After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members.</span></span> <span data-ttu-id="21616-107">En outre, lorsqu’il est installé dans une équipe, le bot a accès aux détails de cette équipe et à la liste complète des canaux.</span><span class="sxs-lookup"><span data-stu-id="21616-107">Also, when it is installed in a team, the bot has access to details about that team and the full list of channels.</span></span>

<span data-ttu-id="21616-108">Les bots d’un groupe ou d’un canal reçoivent uniquement des messages lorsqu’ils sont mentionnés @botname.</span><span class="sxs-lookup"><span data-stu-id="21616-108">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="21616-109">Ils ne reçoivent aucun autre message envoyé à la conversation.</span><span class="sxs-lookup"><span data-stu-id="21616-109">They do not receive any other messages sent to the conversation.</span></span> <span data-ttu-id="21616-110">Le robot doit être @mentionné directement.</span><span class="sxs-lookup"><span data-stu-id="21616-110">The bot must be @mentioned directly.</span></span> <span data-ttu-id="21616-111">Votre bot ne reçoit pas de message lorsque l’équipe ou le canal est mentionné, ou lorsqu’une personne répond à un message de votre bot sans @mentioning lui.</span><span class="sxs-lookup"><span data-stu-id="21616-111">Your bot does not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

> [!NOTE]
> <span data-ttu-id="21616-112">Cette fonctionnalité est actuellement disponible en prévisualisation [pour les développeurs publics](../../../resources/dev-preview/developer-preview-intro.md) uniquement.</span><span class="sxs-lookup"><span data-stu-id="21616-112">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>
>
> <span data-ttu-id="21616-113">À l’aide du consentement spécifique aux ressources ( RSC), les bots peuvent recevoir tous les messages de canal dans les équipes dans qui il est installé sans être @mentioned.</span><span class="sxs-lookup"><span data-stu-id="21616-113">Using resource-specific consent (RSC), bots can receive all channel messages in teams that it is installed in without being @mentioned.</span></span> <span data-ttu-id="21616-114">Pour plus d’informations, [voir recevoir tous les messages de canal avec RSC.](channel-messages-with-rsc.md)</span><span class="sxs-lookup"><span data-stu-id="21616-114">For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="21616-115">Instructions de conception</span><span class="sxs-lookup"><span data-stu-id="21616-115">Design guidelines</span></span>

<span data-ttu-id="21616-116">Contrairement aux conversations personnelles, dans les conversations de groupe et les canaux, votre bot doit fournir une présentation rapide.</span><span class="sxs-lookup"><span data-stu-id="21616-116">Unlike personal chats, in group chats and channels, your bot must provide a quick introduction.</span></span> <span data-ttu-id="21616-117">Vous devez suivre ces instructions et d’autres recommandations en matière de conception de bot.</span><span class="sxs-lookup"><span data-stu-id="21616-117">You must follow these and more bot design guidelines.</span></span> <span data-ttu-id="21616-118">Pour plus d’informations sur la conception de bots dans Teams, voir comment concevoir des conversations de bot dans des canaux [et des conversations.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="21616-118">For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

<span data-ttu-id="21616-119">À présent, vous pouvez créer de nouveaux threads de conversation et gérer facilement différentes conversations dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="21616-119">Now, you can create new conversation threads and easily manage different conversations in channels.</span></span>

## <a name="create-new-conversation-threads"></a><span data-ttu-id="21616-120">Créer des threads de conversation</span><span class="sxs-lookup"><span data-stu-id="21616-120">Create new conversation threads</span></span>

<span data-ttu-id="21616-121">Lorsque votre bot est installé dans une équipe, vous devez créer un thread de conversation plutôt que de répondre à un thread existant.</span><span class="sxs-lookup"><span data-stu-id="21616-121">When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one.</span></span> <span data-ttu-id="21616-122">Parfois, il est difficile de différencier deux conversations.</span><span class="sxs-lookup"><span data-stu-id="21616-122">At times it is difficult to differentiate between two conversations.</span></span> <span data-ttu-id="21616-123">Si la conversation est threadée, il est plus facile d’organiser et de gérer différentes conversations dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="21616-123">If the conversation is threaded, it is easier to organize and manage different conversations in channels.</span></span> <span data-ttu-id="21616-124">Il s’agit d’une [forme de messagerie proactive.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="21616-124">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="21616-125">Ensuite, vous pouvez récupérer des mentions à l’aide de l’objet et ajouter des `entities` mentions à vos messages à l’aide de `Mention` l’objet.</span><span class="sxs-lookup"><span data-stu-id="21616-125">Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.</span></span>

## <a name="work-with-mentions"></a><span data-ttu-id="21616-126">Travailler avec des mentions</span><span class="sxs-lookup"><span data-stu-id="21616-126">Work with mentions</span></span>

<span data-ttu-id="21616-127">Chaque message envoyé à votre bot à partir d’un groupe ou d’un canal contient un @mention dont le nom est dans le texte du message.</span><span class="sxs-lookup"><span data-stu-id="21616-127">Every message to your bot from a group or channel contains an @mention with its name in the message text.</span></span> <span data-ttu-id="21616-128">Votre bot peut également récupérer d’autres utilisateurs mentionnés dans un message et ajouter des mentions à tous les messages qu’il envoie.</span><span class="sxs-lookup"><span data-stu-id="21616-128">Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.</span></span>

<span data-ttu-id="21616-129">Vous devez également les @mentions du contenu du message reçu par votre bot.</span><span class="sxs-lookup"><span data-stu-id="21616-129">You must also strip out the @mentions from the content of the message your bot receives.</span></span>

### <a name="retrieve-mentions"></a><span data-ttu-id="21616-130">Récupérer des mentions</span><span class="sxs-lookup"><span data-stu-id="21616-130">Retrieve mentions</span></span>

<span data-ttu-id="21616-131">Les mentions sont renvoyées dans l’objet dans la charge utile et contiennent l’ID unique de l’utilisateur et le nom `entities` de l’utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="21616-131">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned.</span></span> <span data-ttu-id="21616-132">Le texte du message inclut également la mention, telle que `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="21616-132">The text of the message also includes the mention, such as `<at>@John Smith<at>`.</span></span> <span data-ttu-id="21616-133">Toutefois, ne comptez pas sur le texte du message pour récupérer des informations sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="21616-133">However, do not rely on the text in the message to retrieve any information about the user.</span></span> <span data-ttu-id="21616-134">Il est possible pour la personne qui envoie le message de le modifier.</span><span class="sxs-lookup"><span data-stu-id="21616-134">It is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="21616-135">Par conséquent, utilisez `entities` l’objet.</span><span class="sxs-lookup"><span data-stu-id="21616-135">Therefore, use the `entities` object.</span></span>

<span data-ttu-id="21616-136">Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction dans le SDK Bot Builder, qui renvoie un `GetMentions` tableau `Mention` d’objets.</span><span class="sxs-lookup"><span data-stu-id="21616-136">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.</span></span>

<span data-ttu-id="21616-137">Le code suivant montre un exemple d’extraction de mentions :</span><span class="sxs-lookup"><span data-stu-id="21616-137">The following code shows an example of retrieving mentions:</span></span>

# <a name="c"></a>[<span data-ttu-id="21616-138">C#</span><span class="sxs-lookup"><span data-stu-id="21616-138">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="21616-139">TypeScript</span><span class="sxs-lookup"><span data-stu-id="21616-139">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="21616-140">JSON</span><span class="sxs-lookup"><span data-stu-id="21616-140">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="21616-141">Python</span><span class="sxs-lookup"><span data-stu-id="21616-141">Python</span></span>](#tab/python)

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

### <a name="add-mentions-to-your-messages"></a><span data-ttu-id="21616-142">Ajouter des mentions à vos messages</span><span class="sxs-lookup"><span data-stu-id="21616-142">Add mentions to your messages</span></span>

<span data-ttu-id="21616-143">Votre bot peut mentionner d’autres utilisateurs dans les messages publiés dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="21616-143">Your bot can mention other users in messages posted into channels.</span></span>

<span data-ttu-id="21616-144">`Mention`L’objet possède deux propriétés que vous devez définir à l’aide des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="21616-144">The `Mention` object has two properties that you must set using the following:</span></span>

* <span data-ttu-id="21616-145">Incluez <at>@username</at> dans le texte du message.</span><span class="sxs-lookup"><span data-stu-id="21616-145">Include <at>@username</at> in the message text.</span></span>
* <span data-ttu-id="21616-146">Incluez l’objet mention à l’intérieur de la collection entities.</span><span class="sxs-lookup"><span data-stu-id="21616-146">Include the mention object inside the entities collection.</span></span>

<span data-ttu-id="21616-147">Le SDK Bot Framework fournit des méthodes d’aide et des objets pour créer des mentions.</span><span class="sxs-lookup"><span data-stu-id="21616-147">The Bot Framework SDK provides helper methods and objects to create mentions.</span></span>

<span data-ttu-id="21616-148">Le code suivant montre un exemple d’ajout de mentions à vos messages :</span><span class="sxs-lookup"><span data-stu-id="21616-148">The following code shows an example of adding mentions to your messages:</span></span>

# <a name="c"></a>[<span data-ttu-id="21616-149">C#</span><span class="sxs-lookup"><span data-stu-id="21616-149">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="21616-150">TypeScript</span><span class="sxs-lookup"><span data-stu-id="21616-150">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="21616-151">JSON</span><span class="sxs-lookup"><span data-stu-id="21616-151">JSON</span></span>](#tab/json)

<span data-ttu-id="21616-152">Le `text` champ de l’objet dans le `entities` tableau doit correspondre à une partie du champ de `text` message.</span><span class="sxs-lookup"><span data-stu-id="21616-152">The `text` field in the object in the `entities` array must match a portion of the message `text` field.</span></span> <span data-ttu-id="21616-153">Si ce n’est pas le cas, la mention est ignorée.</span><span class="sxs-lookup"><span data-stu-id="21616-153">If it does not, the mention is ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="21616-154">Python</span><span class="sxs-lookup"><span data-stu-id="21616-154">Python</span></span>](#tab/python)

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

<span data-ttu-id="21616-155">Vous pouvez maintenant envoyer un message d’introduction lorsque votre bot est installé ou ajouté pour la première fois à un groupe ou à une équipe.</span><span class="sxs-lookup"><span data-stu-id="21616-155">Now you can send an introduction message when your bot is first installed or added to a group or team.</span></span>

## <a name="send-a-message-on-installation"></a><span data-ttu-id="21616-156">Envoyer un message lors de l’installation</span><span class="sxs-lookup"><span data-stu-id="21616-156">Send a message on installation</span></span>

<span data-ttu-id="21616-157">Lorsque votre bot est ajouté pour la première fois au groupe ou à l’équipe, un message d’introduction doit être envoyé.</span><span class="sxs-lookup"><span data-stu-id="21616-157">When your bot is first added to the group or team, an introduction message must be sent.</span></span> <span data-ttu-id="21616-158">Le message doit fournir une brève description des fonctionnalités du bot et de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="21616-158">The message must provide a brief description of the bot's features and how to use them.</span></span> <span data-ttu-id="21616-159">Vous devez vous abonner à `conversationUpdate` l’événement avec `teamMemberAdded` eventType.</span><span class="sxs-lookup"><span data-stu-id="21616-159">You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="21616-160">L’événement est envoyé lorsqu’un nouveau membre d’équipe est ajouté.</span><span class="sxs-lookup"><span data-stu-id="21616-160">The event is sent when any new team member is added.</span></span> <span data-ttu-id="21616-161">Vérifiez si le nouveau membre ajouté est le bot.</span><span class="sxs-lookup"><span data-stu-id="21616-161">Check if the new member added is the bot.</span></span> <span data-ttu-id="21616-162">Pour plus d’informations, [voir l’envoi d’un message de bienvenue à un nouveau membre de l’équipe.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="21616-162">For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="21616-163">Envoyez un message personnel à chaque membre de l’équipe lorsque le bot est ajouté.</span><span class="sxs-lookup"><span data-stu-id="21616-163">Send a personal message to each team member when the bot is added.</span></span> <span data-ttu-id="21616-164">Pour ce faire, obtenez la liste de l’équipe et envoyez un message direct à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="21616-164">To do this, get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="21616-165">N’envoyez pas de message dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="21616-165">Do not send a message in the following cases:</span></span>

* <span data-ttu-id="21616-166">L’équipe est volumineuse, par exemple, plus de 100 membres.</span><span class="sxs-lookup"><span data-stu-id="21616-166">The team is large, for example, larger than 100 members.</span></span> <span data-ttu-id="21616-167">Votre bot peut être considéré comme du courrier indésirable et la personne qui l’a ajouté peut obtenir des réclamations.</span><span class="sxs-lookup"><span data-stu-id="21616-167">Your bot can be seen as spam and the person who added it can get complaints.</span></span> <span data-ttu-id="21616-168">Vous devez clairement communiquer la proposition de valeur de votre bot à toutes les personnes qui voient le message de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="21616-168">You must clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="21616-169">Votre bot est d’abord mentionné dans un groupe ou un canal au lieu d’être ajouté pour la première fois à une équipe.</span><span class="sxs-lookup"><span data-stu-id="21616-169">Your bot is first mentioned in a group or channel instead of being first added to a team.</span></span>
* <span data-ttu-id="21616-170">Un groupe ou un canal est renommé.</span><span class="sxs-lookup"><span data-stu-id="21616-170">A group or channel is renamed.</span></span>
* <span data-ttu-id="21616-171">Un membre d’équipe est ajouté à un groupe ou un canal.</span><span class="sxs-lookup"><span data-stu-id="21616-171">A team member is added to a group or channel.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a><span data-ttu-id="21616-172">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="21616-172">See also</span></span>

[<span data-ttu-id="21616-173">Obtenir Teams contexte</span><span class="sxs-lookup"><span data-stu-id="21616-173">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a><span data-ttu-id="21616-174">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="21616-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21616-175">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="21616-175">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
