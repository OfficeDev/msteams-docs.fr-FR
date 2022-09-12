---
title: Créer des bots de conversation pour une conversation de canal ou de groupe
author: surbhigupta
description: Découvrez comment envoyer, recevoir et gérer des messages pour un bot dans un canal ou une conversation de groupe. Découvrez les instructions de conception et bien plus encore.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 91e696644698a609f6870aad9f4242e797b8e6bc
ms.sourcegitcommit: 2d48459e0cdf92c097954ecc785f0ea257d423b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2022
ms.locfileid: "67646138"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>Conversations de canal et de groupe avec un bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Pour installer le bot Microsoft Teams dans une conversation d’équipe ou de groupe, ajoutez l’étendue `teams` ou `groupchat` à votre bot. Cela permet à tous les membres de la conversation d’interagir avec votre robot. Une fois le bot installé, il a accès aux métadonnées relatives à la conversation, telles que la liste des membres de la conversation. En outre, lorsqu’il est installé dans une équipe, le bot a accès aux détails de cette équipe et à la liste complète des canaux.

Les bots d’un groupe ou d’un canal reçoivent uniquement des messages lorsqu’ils sont mentionnés @botname. Ils ne reçoivent aucun autre message envoyé à la conversation. Le robot doit être @mentionné directement. Votre bot ne reçoit pas de message lorsque l’équipe ou le canal est mentionné, ou quand quelqu’un répond à un message de votre bot sans l'@mentioning.

> [!NOTE]
> Cette fonctionnalité est actuellement disponible dans [préversion publique des développeurs](../../../resources/dev-preview/developer-preview-intro.md) uniquement.
>
> À l’aide du consentement spécifique à la ressource (RSC), les bots peuvent recevoir tous les messages de canal dans les équipes dans lesquelles il est installé sans être @mentioned. Pour plus d’informations, consultez [recevoir tous les messages de canal avec RSC](channel-messages-with-rsc.md).
>
> La publication d’un message ou d’une carte adaptative sur un canal privé n’est actuellement pas prise en charge.

Consultez la vidéo suivante pour en savoir plus sur les conversations de canal et de groupe avec un bot :
<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4NzEs>]
<br>

## <a name="design-guidelines"></a>Instructions de conception

Contrairement aux conversations personnelles, dans les conversations de groupe et les canaux, votre bot doit fournir une présentation rapide. Vous devez suivre ces instructions de conception de bot et d’autres. Pour plus d’informations sur la conception de bots dans Teams, consultez [comment concevoir des conversations de bot dans des canaux et des conversations](~/bots/design/bots.md).

À présent, vous pouvez créer des threads de conversation et gérer facilement différentes conversations dans les canaux.

## <a name="create-new-conversation-threads"></a>Créer des threads de conversation

Lorsque votre bot est installé dans une équipe, vous devez créer un thread de conversation au lieu de répondre à un thread existant. Parfois, il est difficile de faire la distinction entre deux conversations. Si la conversation est threadée, il est plus facile d’organiser et de gérer différentes conversations dans les canaux. Il s’agit d’une forme de [messagerie proactive](~/bots/how-to/conversations/send-proactive-messages.md).

Ensuite, vous pouvez récupérer des mentions à l’aide de l’objet `entities` et ajouter des mentions à vos messages à l’aide de l’objet `Mention` .

## <a name="work-with-mentions"></a>Utiliser des mentions

Chaque message envoyé à votre bot à partir d’un groupe ou d’un canal contient un @mention avec son nom dans le texte du message. Votre bot peut également récupérer d’autres utilisateurs mentionnés dans un message et ajouter des mentions à tous les messages qu’il envoie.

Vous devez également supprimer les @mentions du contenu du message que votre bot reçoit.

### <a name="retrieve-mentions"></a>Récupérer les mentions

Les mentions sont retournées dans l’objet `entities` dans la charge utile et contiennent à la fois l’ID unique de l’utilisateur et le nom de l’utilisateur mentionné. Le texte du message inclut également la mention, par exemple `<at>@John Smith<at>`. Toutefois, ne vous fiez pas au texte du message pour récupérer des informations sur l’utilisateur. Il est possible que la personne qui envoie le message le modifie. Par conséquent, utilisez l’objet `entities`.

Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction `GetMentions` dans le SDK Bot Builder, qui retourne un tableau d’objets `Mention` .

Le code suivant montre un exemple de récupération des mentions :

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

Votre bot peut mentionner d’autres utilisateurs dans les messages publiés dans les canaux.

L’objet `Mention` a deux propriétés que vous devez définir à l’aide des éléments suivants :

* Incluez *@username* dans le texte du message.
* Incluez l’objet mention dans la collection d’entités.

Le SDK Bot Framework fournit des méthodes d’assistance et des objets pour créer des mentions.

Le code suivant montre un exemple d’ajout de mentions à vos messages :

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

Le champ `text` dans l’objet du tableau `entities` doit correspondre à une partie du champ `text`. Si ce n’est pas le cas, la mention est ignorée.

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

Vous pouvez maintenant envoyer un message d’introduction lorsque votre bot est installé ou ajouté pour la première fois à un groupe ou à une équipe.

## <a name="send-a-message-on-installation"></a>Envoyer un message lors de l’installation

Lorsque votre bot est ajouté pour la première fois au groupe ou à l’équipe, un message d’introduction doit être envoyé. Le message doit fournir une brève description des fonctionnalités du bot et comment les utiliser. Vous devez vous abonner à l’événement `conversationUpdate` avec le `teamMemberAdded` eventType.  L’événement est envoyé lorsqu’un nouveau membre d’équipe est ajouté. Vérifiez si le nouveau membre ajouté est le bot. Pour plus d’informations, consultez [envoyer un message de bienvenue à un nouveau membre de l’équipe](~/bots/how-to/conversations/send-proactive-messages.md).

Vous pouvez envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté. Pour ce faire, [récupérez la liste d’équipe](../../../resources/bot-v3/bots-context.md#fetch-the-team-roster) et envoyez un [message direct](../../../resources/bot-v3/bot-conversations/bots-conv-proactive.md) à chaque utilisateur.

>[!NOTE]
> Assurez-vous que le message envoyé par le bot est pertinent et ajoute de la valeur au message initial et qu’il n’envoie pas de courrier indésirable aux utilisateurs.

N’envoyez pas de message dans les cas suivants :

* Lorsque l’équipe est grande, par exemple, plus de 100 membres. Votre bot peut être considéré comme du courrier indésirable et la personne qui l’a ajouté peut recevoir des plaintes. Vous devez communiquer clairement la proposition de valeur de votre bot à toutes les personnes qui voient le message d’accueil.
* Votre bot est mentionné pour la première fois dans un groupe ou un canal au lieu d’être ajouté en premier à une équipe.
* Un groupe ou un canal est renommé.
* Un membre d’équipe est ajouté à un groupe ou à un canal.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-teams-conversation-bot.yml), pour créer un bot de conversation Teams.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [S’abonner à des événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="see-also"></a>Voir aussi

* [obtenir des de contexte Teams](~/bots/how-to/get-teams-context.md)
* [Créer un canal privé pour le compte de l’utilisateur](/graph/api/channel-post#example-2-create-private-channel-on-behalf-of-user)
* [Connecter un bot à Chat Web canal](/azure/bot-service/bot-service-channel-connect-webchat)
