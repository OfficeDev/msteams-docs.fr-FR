---
title: Messages dans les conversations des robots
description: Décrit comment avoir une conversation avec un bot Microsoft Teams de travail
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: b46ce611ca09c4d5883cc66e0078291422e2b65a
ms.sourcegitcommit: 211f2eaa05494a11b8c2a050d7f1a9ca1c1c78a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2021
ms.locfileid: "59491673"
---
# <a name="messages-in-bot-conversations"></a>Messages dans les conversations des robots

Chaque message d’une conversation est `Activity` un objet de type `messageType: message` . Lorsqu’un utilisateur envoie un message, Teams publie le message à votre bot. Teams envoie un objet JSON au point de terminaison de messagerie de votre bot. Votre bot examine le message pour déterminer son type et répond en conséquence.

Les conversations de base sont gérées via le connecteur Bot Framework, une API REST unique. Cette API permet à votre bot de communiquer avec Teams et d’autres canaux. Le SDK Bot Builder fournit les fonctionnalités suivantes :

* Accès facile au connecteur Bot Framework.
* Fonctionnalités supplémentaires pour gérer le flux et l’état des conversations.
* Méthodes simples pour incorporer des services cognitives, tels que le traitement du langage naturel (NLP).

Votre bot reçoit des messages Teams à l’aide de la propriété et envoie des réponses de message unique ou `Text` multiples aux utilisateurs.

## <a name="receive-a-message"></a>Recevoir un message

Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`. Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.

Le code suivant montre un exemple de réception d’un message :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[JSON](#tab/json)

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
    "text": "Hello Teams TestBot.Sending bold-italic rich text",
    "attachments": [
      {
            "contentType": "text/html",
            "content": "<div><div>Hello Teams TestBot. Sending <strong>bold</strong>-<em>italic</em> rich text.</div>\n</div>"
      } 
    ],
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

## <a name="send-a-message"></a>Envoyer un message

Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité. Dans le handler d’activité du bot, utilisez la méthode de l’objet de contexte turn pour `SendActivityAsync` envoyer une seule réponse de message. Utilisez la méthode de `SendActivitiesAsync` l’objet pour envoyer plusieurs réponses à la fois.

Le code suivant montre un exemple d’envoi d’un message lorsqu’un utilisateur est ajouté à une conversation :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[JSON](#tab/json)

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
> Le fractionnement de message se produit lorsqu’un message texte et une pièce jointe sont envoyés dans la même charge utile d’activité. Cette activité est divisée en activités distinctes par Microsoft Teams, l’une avec un simple message texte et l’autre avec une pièce jointe. Lorsque l’activité est fractionée, vous ne recevez pas l’ID de message en réponse, qui est utilisé pour mettre à jour ou supprimer [le](~/bots/how-to/update-and-delete-bot-messages.md) message de manière proactive. Il est recommandé d’envoyer des activités distinctes au lieu de dépendre du fractionnement des messages.

Les messages envoyés entre les utilisateurs et les bots incluent des données de canal interne dans le message. Ces données permettent au bot de communiquer correctement sur ce canal. Le SDK Bot Builder vous permet de modifier la structure des messages.

## <a name="teams-channel-data"></a>Teams canal de distribution

L’objet contient des Teams spécifiques et constitue une source définitive pour les ID d’équipe et `channelData` de canal. Si vous le souhaitez, vous pouvez mettre en cache et utiliser ces ID comme clés pour le stockage local. Le `TeamsActivityHandler` SDK dans le SDK retire des informations importantes de `channelData` l’objet pour les rendre facilement accessibles. Toutefois, vous pouvez toujours accéder aux données d’origine à partir de `turnContext` l’objet.

L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en `channelData` dehors d’un canal.

Un objet `channelData` type dans une activité envoyée à votre bot contient les informations suivantes :

* `eventType`: Teams type d’événement transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id`: Azure Active Directory ID de client transmis dans tous les contextes.
* `team`: Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.
  * `id`: GUID du canal.
  * `name`: nom de l’équipe transmis uniquement en cas d’événements [de changement de nom d’équipe.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel`: Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté.
  * `id`: GUID du canal.
  * `name`: Nom du canal transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channelData.teamsTeamId`: Deprecated. Cette propriété est incluse uniquement pour la compatibilité ascendante.
* `channelData.teamsChannelId`: Deprecated. Cette propriété est incluse uniquement pour la compatibilité ascendante.

### <a name="example-channeldata-object-or-channelcreated-event"></a>Exemple d’objet channelData ou d’événement channelCreated

Le code suivant montre un exemple d’objet channelData :

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

Les messages reçus ou envoyés à votre bot peuvent inclure différents types de contenu de message.

## <a name="message-content"></a>Contenu du message

| Format    | De l’utilisateur au bot | Du bot à l’utilisateur | Remarques                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texte enrichi  | ✔                | ✔                | Votre bot peut envoyer du texte enrichi, des images et des cartes. Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.                                                                                        |
| Images  | ✔                | ✔                | Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF. Gif animé non pris en charge.  |
| Cartes     | ✖                | ✔                | Consultez la référence [Teams carte de visite](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes pris en charge. |
| Emojis    | ✖                | ✔                | Teams prend actuellement en charge les emojis via UTF-16, par exemple U+1F600 pour le visage. |

Vous pouvez également ajouter des notifications à votre message à l’aide de la `Notification.Alert` propriété.

## <a name="notifications-to-your-message"></a>Notifications à votre message

Les notifications avertissent les utilisateurs des nouvelles tâches, mentions et commentaires. Ces alertes sont liées à ce sur quoi les utilisateurs travaillent ou ce qu’ils doivent examiner en insérant une notification dans leur flux d’activités. Pour que les notifications se déclenchent à partir de votre message bot, définissez la propriété `TeamsChannelData` des objets sur `Notification.Alert` *true*. Le fait qu’une notification soit ou non élevée dépend des paramètres de Teams de l’utilisateur individuel et vous ne pouvez pas remplacer ces paramètres. Le type de notification est soit une bannière, soit une bannière et un e-mail.

> [!NOTE]
> Le **champ Résumé** affiche tout texte de l’utilisateur en tant que message de notification dans le flux.

Le code suivant montre un exemple d’ajout de notifications à votre message :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[JSON](#tab/json)

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

Pour améliorer votre message, vous pouvez inclure des images en tant que pièces jointes à ce message.

## <a name="picture-messages"></a>Messages image

Les images sont envoyées en ajoutant des pièces jointes à un message. Pour plus d’informations sur les pièces jointes, voir [la documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)

Les images peuvent être au maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF. Gif animé non pris en charge.

Spécifiez la hauteur et la largeur de chaque image à l’aide de XML. Dans markdown, la taille par défaut de l’image est 256×256. Par exemple :

* Utilisez : `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .
* N’utilisez pas : `![Duck on a rock](http://aka.ms/Fo983c)` .

Un bot de conversation peut inclure des cartes adaptatives qui simplifient les flux de travail d’entreprise. Les cartes adaptatives offrent des champs de texte, de reconnaissance vocale, d’images, de boutons et d’entrée personnalisables enrichis.

## <a name="adaptive-cards"></a>Cartes adaptatives

Les cartes adaptatives peuvent être authored dans un bot et affichées dans plusieurs applications telles que Teams, votre site web, etc. Pour plus d’informations, voir [Cartes adaptatives.](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Le code suivant illustre un exemple d’envoi d’une carte adaptative simple :

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

Pour en savoir plus sur les cartes et les cartes dans les bots, consultez [la documentation des cartes.](~/task-modules-and-cards/what-are-cards.md)

## <a name="status-code-responses"></a>Réponses de code d’état

Voici les codes d’état, leur code d’erreur et leurs valeurs de message :

| Code d'état | Code d’erreur et valeurs de message | Description |
|----------------|-----------------|-----------------|
| 403 | **Code**: `ConversationBlockedByUser` <br/> **Message :** l’utilisateur a bloqué la conversation avec le bot. | L’utilisateur a bloqué le bot dans une conversation 1:1 ou un canal via les paramètres de modération. |
| 403 | **Code**: `BotNotInConversationRoster` <br/> **Message :** le bot ne fait pas partie de la liste des conversations. | Le bot ne fait pas partie de la conversation. |
| 403 | **Code**: `BotDisabledByAdmin` <br/> **Message :** l’administrateur client a désactivé ce bot. | Le client a bloqué le bot. |
| 401 | **Code**: `BotNotRegistered` <br/> **Message**: aucune inscription trouvée pour ce bot. | L’inscription de ce bot est in trouvée. |
| 412 | **Code**: `PreconditionFailed` <br/> **Message :** la condition préalable a échoué, veuillez essayer à nouveau. | Une condition préalable a échoué sur l’une de nos dépendances en raison de plusieurs opérations simultanées sur la même conversation. |
| 404 | **Code**: `ConversationNotFound` <br/> **Message :** Conversation in trouvée. | La conversation est in trouvée. |
| 413 | **Code**: `MessageSizeTooBig` <br/> **Message :** taille du message trop grande. | La taille de la demande entrante était trop importante. |
| 429 | **Code**: `Throttled` <br/> **Message**: trop de demandes. Renvoie également quand réessayer après. | Trop de demandes ont été envoyées par le bot. Pour plus d’informations, voir [limite de taux.](~/bots/how-to/rate-limit.md) |

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Bot de conversation Teams | Gestion des événements de messagerie et de conversation. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a>Voir aussi

- [Envoyer des messages proactifs](~/bots/how-to/conversations/send-proactive-messages.md)

- [S’abonner à des événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Menus de commande du bot](~/bots/how-to/create-a-bot-commands-menu.md)
