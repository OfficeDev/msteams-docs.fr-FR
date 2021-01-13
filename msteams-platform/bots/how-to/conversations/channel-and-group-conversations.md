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
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversations de canal et de groupe avec un bot Microsoft Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

En ajoutant `teams` l’étendue ou l’étendue à votre bot, elle peut être installée dans une conversation d’équipe `groupchat` ou de groupe. Cela permet à tous les membres de la conversation d’interagir avec votre robot. Une fois l’installation terminée, ils auront également accès aux métadonnées relatives à la conversation, telles que la liste des membres de la conversation. Si elle est installée dans une équipe, ils auront également accès aux détails de l’équipe et à la liste complète des canaux.

Les bots d’un groupe ou d’un canal reçoivent des messages uniquement lorsqu’ils sont mentionnés (@botname), ils ne reçoivent aucun autre message envoyé à la conversation.

> [!NOTE]
> Le robot doit être @mentionné directement. Votre bot ne reçoit pas de message lorsque l’équipe ou le canal est mentionné, ou lorsqu’une personne répond à un message de votre bot sans @mentioning le.

## <a name="design-guidelines"></a>Instructions de conception

Découvrez comment concevoir [des conversations de bot dans des canaux et des conversations.](~/bots/design/bots.md)

## <a name="creating-new-conversation-threads"></a>Création de threads de conversation

Lorsque votre bot est installé dans une équipe, il peut parfois être nécessaire de créer un thread de conversation plutôt que de répondre à un thread existant. Il s’agit d’une [forme de messagerie proactive.](~/bots/how-to/conversations/send-proactive-messages.md)

## <a name="working-with-mentions"></a>Travailler avec des mentions

Tous les messages à votre robot provenant d’un groupe ou d’un canal contiennent une @mention avec son propre nom dans le texte du message. Vous devez donc vous assurer que l’analyse de message gère cela. Votre robot peut également récupérer d’autres utilisateurs mentionnés dans un message et ajouter des mentions à tous les messages qu’il envoie.

### <a name="stripping-mentions-from-message-text"></a>Faire trébucher des mentions à partir du texte du message

Il se peut que vous deviez retirer les @mentions du texte du message reçu par votre robot.

### <a name="retrieving-mentions"></a>Récupération des mentions

Les mentions sont renvoyées dans l’objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de `entities` l’utilisateur mentionné. Le texte du message inclut également la mention telle que `<at>@John Smith<at>`. Toutefois, vous ne devez pas vous appuyer sur le texte du message pour récupérer des informations sur l’utilisateur . il est possible pour la personne qui envoie le message de le modifier. Utilisez plutôt `entities` l’objet.

Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction dans le SDK Bot Builder qui renvoie `GetMentions` un tableau `Mention` d’objets.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

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

# <a name="python"></a>[Python](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a>Ajout de mentions à vos messages

Votre bot peut mentionner d’autres utilisateurs dans les messages publiés dans les canaux. Pour ce faire, votre message doit :

`Mention`L’objet possède deux propriétés que vous devrez définir :

* Inclure <at>@username</at> dans le texte du message
* Inclure l’objet mention à l’intérieur de la collection entities

Le SDK Bot Framework fournit des méthodes d’aide et des objets pour faciliter la construction de la mention.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

Le champ de l’objet dans le tableau doit correspondre exactement à une `text` partie du champ de `entities`  `text` message. Si ce n’est pas le cas, la mention sera ignorée.

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

# <a name="python"></a>[Python](#tab/python)

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

## <a name="sending-a-message-on-installation"></a>Envoi d’un message lors de l’installation

Lorsque votre bot est ajouté pour la première fois au groupe ou à l’équipe, il peut être utile d’envoyer un message le présentant. Le message doit fournir une brève description des fonctionnalités du bot et de leur utilisation. Vous souhaiterez vous abonner à `conversationUpdate` l’événement, avec `teamMemberAdded` eventType.  Étant donné que l’événement est envoyé lorsqu’un nouveau membre d’équipe est ajouté, vous devez vérifier si le nouveau membre ajouté est le bot. Pour [plus d’informations, voir](~/bots/how-to/conversations/send-proactive-messages.md) Envoyer un message de bienvenue à un nouveau membre de l’équipe.

Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté. Pour ce faire, vous pouvez obtenir la liste de l’équipe et envoyer un message direct à chaque utilisateur.

Il n’est pas recommandé d’envoyer un message dans les situations suivantes :

* L’équipe est volumineuse (évidemment subjectif, mais par exemple plus de 100 membres). Votre bot peut être considéré comme « spammy » et la personne qui l’a ajouté peut obtenir des réclamations, sauf si vous communiquez clairement la proposition de valeur de votre bot à toutes les personnes qui voient le message de bienvenue.
* Votre bot est d’abord mentionné dans un groupe ou un canal (plutôt que d’être ajouté pour la première fois à une équipe)
* Un groupe ou un canal est renommé
* Un membre d’équipe est ajouté à un groupe ou un canal

## <a name="learn-more"></a>En savoir plus

Votre bot a accès à des informations supplémentaires sur la conversation de groupe ou l’équipe dans qui il est installé. Consultez [le contexte teams pour](~/bots/how-to/get-teams-context.md) obtenir des API supplémentaires disponibles pour votre bot.

Votre bot peut également s’abonner à des événements supplémentaires et y répondre. Pour savoir [comment s’abonner aux événements de conversation,](~/bots/how-to/conversations/subscribe-to-conversation-events.md) voir s’abonner à des événements de conversation.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
