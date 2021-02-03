---
title: Concepts de base d’une conversation
author: clearab
description: Comment avoir une conversation avec un bot Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075692"
---
# <a name="conversation-basics"></a>Concepts de base d’une conversation

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs. Il existe trois types de conversations (ou portées) dans Teams :

* `teams` Également appelées conversations de canal, visibles par tous les membres du canal.
* `personal` Conversations entre les bots et un seul utilisateur.
* `groupChat` Discutez entre un bot et au moins deux utilisateurs. Active également votre bot dans les conversations de réunion.

Un bot se comporte légèrement différemment selon le type de conversation dans qui il est impliqué :

* Les bots dans les conversations de canal et de groupe nécessitent que l’utilisateur mentionne @ le bot pour l’appeler dans un canal.
* Les bots d’une conversation un-à-un ne nécessitent pas de mention @ . Tous les messages envoyés par l’utilisateur sont acheminés à votre bot.

Pour activer votre bot dans une étendue particulière, ajoutez cette étendue au manifeste [de votre application.](~/resources/schema/manifest-schema.md)

## <a name="activities"></a>Activités

Chaque message est un objet `Activity` de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot. Votre bot examine le message pour déterminer son type et répond en conséquence.

La conversation de base est gérée par le biais du connecteur Bot Framework, une API REST unique permettant à votre bot de communiquer avec Teams et d’autres canaux. Le SDK Bot Builder fournit un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux et l’état des conversations, ainsi que des moyens simples d’incorporer des services cognitives tels que le traitement du langage naturel (NLP).

## <a name="receive-a-message"></a>Recevoir un message

Pour recevoir un message texte, utilisez la propriété `Text` de l’objet `Activity`. Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.

Le code ci-dessous présente un exemple.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

## <a name="send-a-message"></a>Envoyer un message

Pour envoyer un message texte, spécifiez la chaîne que vous voulez envoyer en tant qu’activité. Dans le gestionnaire d’activités du bot, utilisez la méthode `SendActivityAsync` de l’objet de contexte de tour pour envoyer un seul message de réponse. Vous pouvez également utiliser la méthode de l’objet `SendActivitiesAsync` pour envoyer plusieurs réponses à la fois. Le code ci-dessous montre un exemple d’envoi d’un message lorsqu’une personne est ajoutée à une conversation.  

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

## <a name="teams-channel-data"></a>Données de canal Teams

L’objet contient des informations spécifiques à Teams et constitue la source définitive des ID d’équipe et `channelData` de canal. Vous devrez peut-être mettre en cache et utiliser ces ID comme clés pour le stockage local. Le SDK retire généralement des informations importantes de l’objet pour les rendre plus facilement accessibles, mais vous pouvez toujours accéder aux informations d’origine à partir de `TeamsActivityHandler` `channelData` `turnContext` l’objet.

`channelData`L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en dehors d’un canal.

Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :

* `eventType` Type d’événement Teams ; transmis uniquement en cas d’événements [de modification de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id` ID de client Azure Active Directory ; transmis dans tous les contextes
* `team` Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.
  * `id` GUID du canal
  * `name` Nom de l’équipe ; transmis uniquement en cas d’événements [de changement de nom d’équipe](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel` Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté
  * `id` GUID du canal
  * `name`Nom du canal ; transmis uniquement en cas d’événements [de modification de canal.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channelData.teamsTeamId` Deprecated. Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.
* `channelData.teamsChannelId` Deprecated. Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.

### <a name="example-channeldata-object-channelcreated-event"></a>Exemple d’objet channelData (événement channelCreated)

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

## <a name="message-content"></a>Contenu du message

Votre bot peut envoyer du texte enrichi, des images et des cartes. Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.

| Format    | De l’utilisateur au bot | Du bot à l’utilisateur | Notes                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texte enrichi  | ✔                | ✔                |                                                                                         |
| Images  | ✔                | ✔                | Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge  |
| Cartes     | ✖                | ✔                | Voir la référence [de carte Teams pour](~/task-modules-and-cards/cards/cards-reference.md) les cartes pris en charge |
| Emojis    | ✖                | ✔                | Teams prend actuellement en charge les emojis via UTF-16 (par exemple, U+1F600 pour le visage de panoramique)          |

## <a name="adding-notifications-to-your-message"></a>Ajout de notifications à votre message

Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed. Vous pouvez définir des notifications pour qu’ils se déclenchent à partir de votre message bot en réglant la propriété des objets `TeamsChannelData` `Notification.Alert` sur true. Le fait qu’une notification soit ou non élevée dépend en fin de compte des paramètres Teams de l’utilisateur individuel et vous ne pouvez pas remplacer ces paramètres par programme. Le type de notification sera soit une bannière, soit une bannière et un e-mail.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

## <a name="picture-messages"></a>Messages image

Les images sont envoyées en ajoutant des pièces jointes à un message. Vous trouverez plus d’informations sur les pièces jointes dans la [documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)

Les images peuvent être au maximum 1 024 × 1 024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge.

Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML. Si vous utilisez Markdown, la taille par défaut de l’image est 256×256. Par exemple :

* Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Ne pas utiliser - `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="code-sample"></a>Exemple de code
|**Exemple de nom** | **Description** | **. NETCore** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| Teams Conversation Bot | Gestion des événements de messagerie et de conversation. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a>Étapes suivantes

* [Envoi de messages proactifs](~/bots/how-to/conversations/send-proactive-messages.md)
* [S’abonner à des événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
