---
title: Conversations de canal et de groupe avec un bot
author: clearab
description: Comment envoyer, recevoir et gérer des messages pour un bot dans une conversation de canal ou de groupe.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 2d7eece1fc74781456024f6dcb9414fefbadb8f4
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075751"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>Conversations de canal et de groupe avec un bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Pour installer le bot Microsoft Teams dans une conversation d'équipe ou de groupe, ajoutez l'étendue `teams` `groupchat` ou l'étendue à votre bot. Cela permet à tous les membres de la conversation d’interagir avec votre robot. Une fois le bot installé, il a accès aux métadonnées sur la conversation, telles que la liste des membres de la conversation. En outre, lorsqu'il est installé dans une équipe, le bot a accès aux détails de cette équipe et à la liste complète des canaux.

Les bots d'un groupe ou d'un canal reçoivent uniquement des messages lorsqu'ils sont `@botname` mentionnés. Ils ne reçoivent aucun autre message envoyé à la conversation.

> [!NOTE]
> Le bot doit être `@mentioned` directement. Votre bot ne reçoit pas de message lorsque l'équipe ou le canal est mentionné, ou lorsqu'une personne répond à un message de votre bot sans @mentioning lui.

## <a name="design-guidelines"></a>Instructions de conception

Contrairement aux conversations personnelles, dans les conversations de groupe et les canaux, votre bot doit fournir une présentation rapide. Vous devez suivre ces recommandations et d'autres recommandations en matière de conception de bot. Pour plus d'informations sur la conception de bots dans Teams, voir comment concevoir des conversations de bot dans des canaux [et des conversations.](~/bots/design/bots.md)

À présent, vous pouvez créer de nouveaux threads de conversation et gérer facilement différentes conversations dans les canaux.

## <a name="create-new-conversation-threads"></a>Créer des threads de conversation

Lorsque votre bot est installé dans une équipe, vous devez créer un thread de conversation plutôt que de répondre à un thread existant. Parfois, il est difficile de différencier deux conversations. Si la conversation est threadée, il est plus facile d'organiser et de gérer différentes conversations dans les canaux. Il s'agit d'une [forme de messagerie proactive.](~/bots/how-to/conversations/send-proactive-messages.md)

Ensuite, vous pouvez récupérer des mentions à l'aide de l'objet et ajouter des `entities` mentions à vos messages à l'aide de `Mention` l'objet.

## <a name="work-with-mentions"></a>Travailler avec des mentions

Chaque message envoyé à votre bot à partir d'un groupe ou d'un canal contient un @mention avec son nom dans le texte du message. Assurez-vous que l'@mention. Votre bot peut également récupérer d'autres utilisateurs mentionnés dans un message et ajouter des mentions à tous les messages qu'il envoie.

Vous devez également les @mentions du contenu du message reçu par votre bot.

### <a name="retrieve-mentions"></a>Récupérer des mentions

Les mentions sont renvoyées dans l'objet dans la charge utile et contiennent l'ID unique de l'utilisateur et le nom `entities` de l'utilisateur mentionné. Le texte du message inclut également la mention, telle que `<at>@John Smith<at>` . Toutefois, ne comptez pas sur le texte du message pour récupérer des informations sur l'utilisateur. Il est possible pour la personne qui envoie le message de le modifier. Par conséquent, utilisez `entities` l'objet.

Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction dans le SDK Bot Builder, qui renvoie un `GetMentions` tableau `Mention` d'objets.

Le code suivant montre un exemple d'extraction de mentions :

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

### <a name="add-mentions-to-your-messages"></a>Ajouter des mentions à vos messages

Votre bot peut mentionner d'autres utilisateurs dans les messages publiés dans les canaux.

`Mention`L'objet possède deux propriétés que vous devez définir à l'aide des propriétés suivantes :

* Incluez <at>@username</at> dans le texte du message.
* Incluez l'objet mention à l'intérieur de la collection entities.

Le SDK Bot Framework fournit des méthodes d'aide et des objets pour créer des mentions.

Le code suivant montre un exemple d'ajout de mentions à vos messages :

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Le `text` champ de l'objet dans le `entities` tableau doit correspondre à une partie du champ de `text` message. Si ce n'est pas le cas, la mention est ignorée.

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

Vous pouvez maintenant envoyer un message d'introduction lorsque votre bot est installé ou ajouté pour la première fois à un groupe ou à une équipe.

## <a name="send-a-message-on-installation"></a>Envoyer un message lors de l'installation

Lorsque votre bot est ajouté pour la première fois au groupe ou à l'équipe, un message d'introduction doit être envoyé. Le message doit fournir une brève description des fonctionnalités du bot et de leur utilisation. Vous devez vous abonner à `conversationUpdate` l'événement avec `teamMemberAdded` eventType.  L'événement est envoyé lorsqu'un nouveau membre d'équipe est ajouté. Vérifiez si le nouveau membre ajouté est le bot. Pour plus d'informations, [voir l'envoi d'un message de bienvenue à un nouveau membre de l'équipe.](~/bots/how-to/conversations/send-proactive-messages.md)

Envoyez un message personnel à chaque membre de l'équipe lorsque le bot est ajouté. Pour ce faire, obtenez la liste de l'équipe et envoyez un message direct à chaque utilisateur.

N'envoyez pas de message dans les cas suivants :

* L'équipe est volumineuse, par exemple, plus de 100 membres. Votre bot peut être considéré comme du courrier indésirable et la personne qui l'a ajouté peut obtenir des réclamations. Vous devez clairement communiquer la proposition de valeur de votre bot à toutes les personnes qui voient le message de bienvenue.
* Votre bot est d'abord mentionné dans un groupe ou un canal au lieu d'être ajouté pour la première fois à une équipe.
* Un groupe ou un canal est renommé.
* Un membre d'équipe est ajouté à un groupe ou un canal.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a>Voir aussi

[Obtenir le contexte Teams](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [S’abonner à des événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
