---
title: Conversations de groupe et de canal
author: clearab
description: Procédure d’envoi, de réception et de gestion des messages pour un bot dans un canal ou une conversation de groupe.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ccc27d7638820cfa3c2b7cfe12b91b3a3a9fef1d
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44801150"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversations par chat de canal et de groupe avec un robot Microsoft Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

En ajoutant l' `teams` `groupchat` étendue ou à votre robot, celle-ci peut être disponible pour être installée dans une conversation d’équipe ou de groupe. Cela permet à tous les membres de la conversation d’interagir avec votre robot. Une fois l’installation terminée, ils auront également accès aux métadonnées relatives à la conversation, telles que la liste des membres de la conversation. Si elle est installée dans une équipe, ils auront également accès aux détails de l’équipe et à la liste complète des canaux.

Les robots d’un groupe ou d’un canal reçoivent uniquement les messages lorsqu’ils sont mentionnés (« @botname »), mais ils ne reçoivent pas les autres messages envoyés à la conversation.

> [!NOTE]
> Le robot doit être @mentionné directement. Votre bot ne reçoit pas de message lorsque l’équipe ou le canal est mentionné, ou lorsqu’un utilisateur répond à un message de votre robot sans le @mentioning.

## <a name="design-considerations"></a>Considérations relatives à la conception

Un bot doit fournir des informations qui sont à la fois appropriées et pertinentes pour tous les membres d’un groupe ou d’un canal. Les conversations avec celles-ci sont visibles par tous les membres du groupe ou du canal. Un robot bien conçu peut ajouter de la valeur à tous les utilisateurs tout en ne partageant pas d’informations plus appropriées dans une conversation un-à-un. Les conversations à plusieurs tours comme les boîtes de dialogue doivent être évitées-utilisez des cartes et/ou des modules de tâches pour collecter des informations à la place.

## <a name="creating-new-conversation-threads"></a>Création de threads de conversation

Lorsque votre bot est installé dans une équipe, il est parfois nécessaire de créer un nouveau fil de conversation au lieu de répondre à un thread existant. Il s’agit d’une forme de [messagerie proactive](~/bots/how-to/conversations/send-proactive-messages.md).

## <a name="working-with-mentions"></a>Utilisation des mentions

Tous les messages à votre robot provenant d’un groupe ou d’un canal contiennent une @mention avec son propre nom dans le texte du message. Vous devez donc vous assurer que l’analyse de message gère cela. Votre robot peut également récupérer d’autres utilisateurs mentionnés dans un message et ajouter des mentions à tous les messages qu’il envoie.

### <a name="stripping-mentions-from-message-text"></a>Suppression des mentions du texte d’un message

Il se peut que vous deviez retirer les @mentions du texte du message reçu par votre robot.

### <a name="retrieving-mentions"></a>Récupération des mentions

Les mentions sont renvoyées dans l' `entities` objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de l’utilisateur mentionné. Le texte du message inclut également la mention telle que `<at>@John Smith<at>`. Toutefois, vous ne devez pas compter sur le texte du message pour récupérer des informations sur l’utilisateur ; Il est possible que la personne qui envoie le message le modifie. À la place, utilisez l' `entities` objet.

Vous pouvez récupérer toutes les mentions dans le message en appelant la `GetMentions` fonction dans le kit de développement logiciel (SDK) du générateur de robots, qui renvoie un tableau d' `Mention` objets.

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

Votre robot peut mentionner d’autres utilisateurs dans les messages publiés dans des canaux. Pour ce faire, votre message doit effectuer les opérations suivantes :

L' `Mention` objet possède deux propriétés que vous devrez définir :

* Inclure <at>@username</at> dans le texte du message
* Inclure l’objet « mention » à l’intérieur de la collection Entities

Le kit de développement logiciel (SDK) de l’infrastructure fournit des méthodes et des objets d’assistance pour faciliter la création de la mention.

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

Le `text` champ dans l’objet dans le `entities` tableau doit correspondre *exactement* à une partie du champ de message `text` . Si ce n’est pas le cas, la mention sera ignorée.

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

Lorsque votre bot est d’abord ajouté au groupe ou à l’équipe, il peut s’avérer utile d’envoyer un message le mettant en place. Le message doit fournir une brève description des fonctionnalités du bot et comment les utiliser. Vous pouvez vous abonner à l' `conversationUpdate` événement, avec le `teamMemberAdded` eventType.  Étant donné que l’événement est envoyé lorsqu’un nouveau membre d’équipe est ajouté, vous devez vérifier si le nouveau membre ajouté est le bot. Pour plus d’informations, consultez la rubrique [envoi d’un message de bienvenue à un nouveau membre](~/bots/how-to/conversations/send-proactive-messages.md) de l’équipe.

Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté. Pour ce faire, vous pouvez obtenir la liste de l’équipe et envoyer un message direct à chaque utilisateur.

Il n’est pas recommandé d’envoyer un message dans les situations suivantes :

* L’équipe est grande (évidemment subjective, mais par exemple, plus de 100 membres). Votre robot peut être considéré comme « spammer » et la personne qui l’a ajouté peut recevoir des plaintes, sauf si vous communiquez clairement la proposition de valeur de votre robot à tous ceux qui voient le message de bienvenue.
* Votre robot est d’abord mentionné dans un groupe ou un canal (et n’est pas d’abord ajouté à une équipe)
* Un groupe ou un canal est renommé.
* Un membre de l’équipe est ajouté à un groupe ou à un canal

## <a name="learn-more"></a>En savoir plus

Votre bot a accès à des informations supplémentaires sur la conversation de groupe ou sur l’équipe dans laquelle il est installé. Consultez la rubrique [obtenir le contexte teams](~/bots/how-to/get-teams-context.md) pour en savoir plus sur les API disponibles pour votre robot.

Il existe également des événements supplémentaires auxquels votre bot peut s’abonner et auquel il répond. Pour en savoir plus, consultez la rubrique [s’abonner aux événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md) .

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
