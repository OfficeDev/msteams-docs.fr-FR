---
title: Messages dans les conversations des robots
description: Découvrez comment envoyer un message, des actions suggérées, une notification, des pièces jointes, des images, une carte adaptative et des réponses de code d’erreur d’état.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 16849a9e8ed97854e91934aef9de463eb355fec5
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833204"
---
# <a name="messages-in-bot-conversations"></a>Messages dans les conversations des robots

Chaque message d’une conversation est un `Activity` objet de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Microsoft Teams le publie sur votre bot. Teams envoie un objet JSON au point de terminaison de messagerie de votre bot et Teams n’autorise qu’un seul point de terminaison pour la messagerie. Votre bot examine le message pour déterminer son type et répond en conséquence.

Les conversations de base sont gérées via le connecteur Bot Framework, une seule API REST. Cette API permet à votre bot de communiquer avec Teams et d’autres canaux. Le Kit de développement logiciel (SDK) Bot Builder fournit les fonctionnalités suivantes :

* Accès facile au connecteur Bot Framework.
* Fonctionnalité permettant de gérer l’état et le flux de conversation.
* Moyens simples d’incorporer des services cognitifs, tels que le traitement du langage naturel (NLP).

Votre bot reçoit des messages de Teams à l’aide de la `Text` propriété et envoie un ou plusieurs messages aux utilisateurs.

Pour plus d’informations, consultez [Attribution d’utilisateurs pour les messages de bot](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages).

## <a name="receive-a-message"></a>Recevoir un message

Pour recevoir un sms, utilisez la `Text` propriété d’un `Activity` objet . Dans le gestionnaire d’activités du bot, utilisez l’`Activity` de l’objet de contexte de tour pour lire un seul message de demande.

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

Pour envoyer un sms, spécifiez la chaîne que vous souhaitez envoyer en tant qu’activité. Dans le gestionnaire d’activités du bot, utilisez la méthode de `SendActivityAsync` l’objet de contexte de tour pour envoyer une réponse de message unique. Utilisez la méthode de l’objet `SendActivitiesAsync` pour envoyer plusieurs réponses.

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

    this.onMembersAddedActivity(async (context, next) => {
        await Promise.all((context.activity.membersAdded || []).map(async (member) => {
            if (member.id !== context.activity.recipient.id) {
                await context.sendActivity(
                    `Welcome to the team ${member.givenName} ${member.surname}`
                );
            }
        }));

        await next();
    });
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
    "type": "message",
    "from": {
        "id": "28:c9e8c047-2a34-40a1-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "conversation": {
        "id": "a:17I0kl8EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-",
        "name": "Convo1"
   },
   "recipient": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB25ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen"
    },
    "text": "My bot's reply",
    "replyToId": "1632474074231"
}

```

---

> [!NOTE]
>
>* Le fractionnement des messages se produit lorsqu’un sms et une pièce jointe sont envoyés dans la même charge utile d’activité. Teams divise cette activité en deux activités distinctes, l’une avec un SMS et l’autre avec une pièce jointe. Comme l’activité est fractionnée, vous ne recevez pas l’ID de message en réponse, qui est utilisé pour [mettre à jour ou supprimer](~/bots/how-to/update-and-delete-bot-messages.md) le message de manière proactive. Il est recommandé d’envoyer des activités distinctes au lieu de dépendre du fractionnement des messages.
>* Les messages envoyés peuvent être localisés pour fournir une personnalisation. Pour plus d’informations, consultez [Localiser votre application](../../../concepts/build-and-test/apps-localization.md).

Les messages envoyés entre les utilisateurs et les bots incluent des données de canal interne dans le message. Ces données permettent au bot de communiquer correctement sur ce canal. Le Kit de développement logiciel (SDK) Bot Builder vous permet de modifier la structure des messages.

## <a name="send-suggested-actions"></a>Envoyer des actions suggérées

Les actions suggérées permettent à votre bot de présenter des boutons que l’utilisateur peut sélectionner pour fournir une entrée. Les actions suggérées améliorent l’expérience utilisateur en permettant à l’utilisateur de répondre à une question ou de faire un choix en sélectionnant un bouton, plutôt que de taper une réponse avec un clavier.
Lorsque l’utilisateur sélectionne un bouton, celui-ci reste visible et accessible dans les cartes enrichies, mais pas pour les actions suggérées. Cela empêche l’utilisateur de sélectionner des boutons obsolètes dans une conversation.

Pour ajouter des actions suggérées à un message, définissez la `suggestedActions` propriété d’un objet [d’activité](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) pour spécifier la liste des objets [d’action de carte](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) qui représentent les boutons à présenter à l’utilisateur. Pour plus dʼinformations, reportez-vous à [`sugestedActions`](/dotnet/api/microsoft.bot.builder.messagefactory.suggestedactions).

Voici un exemple d’implémentation et d’expérience des actions suggérées :

``` json
"suggestedActions": {
    "actions": [
      {
        "type": "imBack",
        "title": "Action 1",
        "value": "Action 1"
      },
      {
        "type": "imBack",
        "title": "Action 2",
        "value": "Action 2"
      }
    ],
    "to": [<list of recepientIds>]
  }
```

Voici un exemple d’actions suggérées :

:::image type="content" source="~/assets/images/Cards/suggested-actions.png" alt-text="Actions suggérées par le bot" border="true":::

> [!NOTE]
>
> * `SuggestedActions` sont uniquement pris en charge pour les bots de conversation en un-à-un et les messages texte, et non pour les cartes adaptatives ou les pièces jointes.
> * `imBack` est le seul type d’action pris en charge et Teams affiche jusqu’à trois actions suggérées.

## <a name="teams-channel-data"></a>Données du canal Teams

L’objet `channelData` contient des informations spécifiques à Teams et constitue une source définitive pour les ID d’équipe et de canal. Si vous le souhaitez, vous pouvez mettre en cache et utiliser ces ID comme clés pour le stockage local. Dans `TeamsActivityHandler` le SDK, le extrait les informations importantes de l’objet pour le `channelData` rendre accessible. Toutefois, vous pouvez toujours accéder aux données d’origine à partir de l’objet `turnContext` .

L’objet `channelData` n’est pas inclus dans les messages dans les conversations personnelles, car celles-ci ont lieu en dehors d’un canal.

Un objet classique `channelData` d’une activité envoyée à votre bot contient les informations suivantes :

* `eventType`: type d’événement Teams transmis uniquement en cas [d’événements de modification de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id`: id de locataire Microsoft Azure Active Directory (Azure AD) passé dans tous les contextes.
* `team`: transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.
  * `id`: GUID du canal.
  * `name`: nom de l’équipe passé uniquement en cas [d’événements de renommage d’équipe](subscribe-to-conversation-events.md#team-renamed).
* `channel`: transmis uniquement dans les contextes de canal, lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes, où le bot a été ajouté.
  * `id`: GUID du canal.
  * `name`: nom de canal transmis uniquement en cas [d’événements de modification de canal](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`:Déconseillée. Cette propriété est incluse uniquement pour la compatibilité descendante.
* `channelData.teamsChannelId`:Déconseillée. Cette propriété est incluse uniquement pour la compatibilité descendante.

### <a name="example-channeldata-object-channelcreated-event"></a>Exemple d’objet channelData (événement channelCreated)

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

## <a name="message-content"></a>Contenu du message

Les messages reçus ou envoyés à votre bot peuvent inclure différents types de contenu de message.

| Format    | De l’utilisateur au bot | Du bot à l’utilisateur | Notes                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Texte enrichi  | ✔️                | ✔️                | Votre bot peut envoyer du texte enrichi, des images et des cartes. Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot.                                                                                        |
| Images  | ✔️                | ✔️                | Maximum 1 024 × 1 024 pixels et 1 Mo au format PNG, JPEG ou GIF. Ne prend pas en charge le GIF animé. |
| Cartes     | ❌                | ✔️                | Consultez [Informations de référence sur les cartes Teams](~/task-modules-and-cards/cards/cards-reference.md) pour connaître les cartes prises en charge. |
| Emojis    | ✔️                | ✔️                | Teams prend actuellement en charge les emojis via UTF-16, tels que U+1F600 pour le sourire. |

### <a name="picture-messages"></a>Messages d’image

Pour améliorer votre message, vous pouvez inclure des images en tant que pièces jointes à ce message. Pour plus d’informations sur les pièces jointes, consultez [Ajouter des pièces jointes multimédias aux messages](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).

Les images peuvent être au maximum 1024 × 1 024 pixels et 1 Mo au format PNG, JPEG ou GIF. Le GIF animé n’est pas pris en charge.

Spécifiez la hauteur et la largeur de chaque image à l’aide de XML. Dans Markdown, la taille d’image par défaut est 256×256. Par exemple :

* Utilisez : `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* N’utilisez pas : `![Duck on a rock](http://aka.ms/Fo983c)`.

Un bot conversationnel peut inclure des cartes adaptatives qui simplifient les workflows métier. Les cartes adaptatives offrent du texte, de la parole, des images, des boutons et des champs d’entrée personnalisables enrichis.

### <a name="adaptive-cards"></a>Cartes adaptatives

Les cartes adaptatives peuvent être créées dans un bot et affichées dans plusieurs applications telles que Teams, votre site web, etc. Pour plus d’informations, voir [Cartes adaptatives](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).

Le code suivant montre un exemple d’envoi d’une carte adaptative simple :

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

#### <a name="form-completion-feedback"></a>Commentaires sur l’achèvement du formulaire

Vous pouvez générer des commentaires sur la saisie semi-automatique des formulaires à l’aide d’une carte adaptative. Le message de saisie semi-automatique du formulaire s’affiche dans cartes adaptatives lors de l’envoi d’une réponse au bot. Le message peut être de deux types, erreur ou réussite :

* **Erreur** : Lorsqu’une réponse envoyée au bot échoue, **un problème s’est produit, le message Réessayer** s’affiche.

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="Message d’erreur"border="true":::

* **Réussite** : lorsqu’une réponse envoyée au bot réussit, **votre réponse a été envoyée au message de l’application s’affiche** .

     :::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="Message de réussite"border="true":::

     Vous pouvez sélectionner **Fermer** ou basculer la conversation pour ignorer le message.

     Si vous ne souhaitez pas afficher le message de réussite, définissez l’attribut `hide` `true` sur dans la `msTeams` `feedback` propriété . Voici un exemple :

     ```json
        "content": {
            "type": "AdaptiveCard",
            "title": "Card with hidden footer messages",
            "version": "1.0",
            "actions": [
            {
                "type": "Action.Submit",
                "title": "Submit",
                "msTeams": {
                    "feedback": {
                    "hide": true
                    }
                }
            }
            ]
        } 
     ```

Pour plus d’informations sur les cartes et les cartes dans les bots, consultez [la documentation](~/task-modules-and-cards/what-are-cards.md) sur les cartes.

## <a name="add-notifications-to-your-message"></a>Ajouter des notifications à votre message

Il existe deux façons d’envoyer une notification à partir de votre application :

* En définissant la propriété sur le `Notification.Alert` message du bot.
* En envoyant une notification de flux d’activité à l’aide du API Graph.

Vous pouvez ajouter des notifications à votre message à l’aide de la `Notification.Alert` propriété . Les notifications alertent les utilisateurs d’un événement dans votre application, tel que de nouvelles tâches, mentions ou commentaires. Ces alertes sont liées à ce sur quoi les utilisateurs travaillent ou à ce qu’ils doivent examiner en insérant un avis dans leur flux d’activité. Pour que les notifications se déclenchent à partir de votre message de bot, définissez la `TeamsChannelData` propriété objects `Notification.Alert` sur *true*. Si une notification est déclenchée dépend des paramètres Teams de l’utilisateur individuel, et vous ne pouvez pas remplacer ces paramètres.

Si vous souhaitez générer une notification arbitraire sans envoyer de message à l’utilisateur, vous pouvez utiliser la API Graph. Pour plus d’informations, consultez [comment envoyer des notifications de flux d’activité à l’aide de API Graph](/graph/teams-send-activityfeednotifications) ainsi que les [meilleures pratiques](/graph/teams-activity-feed-notifications-best-practices).

> [!NOTE]
> Le champ **Résumé** affiche n’importe quel texte de l’utilisateur sous forme de message de notification dans le flux.

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

## <a name="status-codes-from-bot-conversational-apis"></a>Codes d’état des API conversationnelles de bot

Veillez à gérer ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d’erreur et les descriptions sous lesquels les erreurs sont générées :

| Code d'état | Code d’erreur et valeurs de message | Description | Demande de nouvelle tentative | Action du développeur |
|----------------|-----------------|-----------------|----------------|----------------|
| 400 | **Code** : `Bad Argument` <br/> **Message** : *spécifique au scénario | Charge utile de requête non valide fournie par le bot. Pour plus d’informations, consultez le message d’erreur. | Non | Réévaluez la charge utile de la demande pour les erreurs. Consultez le message d’erreur retourné pour plus d’informations. |
| 401 | **Code** : `BotNotRegistered` <br/> **Message** : Aucune inscription n’a été trouvée pour ce bot. | L’inscription de ce bot est introuvable. | Non | Vérifiez l’ID et le mot de passe du bot. Vérifiez que l’ID de bot (ID AAD) est inscrit dans le portail des développeurs Teams ou via l’inscription du canal de bot Azure dans Azure avec le canal « Teams » activé.|
| 403 | **Code** : `BotDisabledByAdmin` <br/> **Message** : L’administrateur du locataire a désactivé ce bot | L’administrateur client a bloqué les interactions entre l’utilisateur et l’application bot. L’administrateur de locataire doit autoriser l’application pour l’utilisateur à l’intérieur des stratégies d’application. Pour plus [d’informations, consultez Stratégies d’application](/microsoftteams/app-policies). | Non | Arrêtez la publication dans la conversation jusqu’à ce que l’interaction avec le bot soit explicitement initiée par un utilisateur dans la conversation indiquant que le bot n’est plus bloqué. |
| 403 | **Code** : `BotNotInConversationRoster` <br/> **Message** : Le bot ne fait pas partie de la liste de conversation. | Le bot ne fait pas partie de la conversation. L’application doit être réinstallée dans la conversation. | Non | Avant de tenter d’envoyer une autre demande de conversation, attendez un [`installationUpdate`](~/bots/how-to/conversations/subscribe-to-conversation-events.md#install-update-event) événement, qui indique que le bot a été rajouté.|
| 403 | **Code** : `ConversationBlockedByUser` <br/> **Message** : L’utilisateur a bloqué la conversation avec le bot. | L’utilisateur a bloqué le bot dans une conversation personnelle ou un canal via les paramètres de modération. | Non | Supprimez la conversation du cache. Arrêtez la tentative de publication dans les conversations jusqu’à ce que l’interaction avec le bot soit explicitement initiée par un utilisateur dans la conversation, ce qui indique que le bot n’est plus bloqué. |
| 403 |**Code** : `InvalidBotApiHost` <br/> **Message** : Hôte d’API de bot non valide. Pour les locataires GCC, appelez `https://smba.infra.gcc.teams.microsoft.com`.|Le bot a appelé le point de terminaison d’API public pour une conversation qui appartient à un locataire GCC.| Non | Mettez à jour l’URL du service pour la conversation `https://smba.infra.gcc.teams.microsoft.com` et réessayez la demande.|
| 403 | **Code** : `NotEnoughPermissions` <br/> **Message** : *spécifique au scénario | Le bot ne dispose pas des autorisations requises pour effectuer l’action demandée. | Non | Déterminez l’action requise à partir du message d’erreur. |
| 404  | **Code** : `ActivityNotFoundInConversation` <br/> **Message** : Conversation introuvable. | L’ID de message fourni est introuvable dans la conversation. Le message n’existe pas ou il a été supprimé. | Non | Vérifiez si l’ID de message envoyé est une valeur attendue. Supprimez l’ID s’il a été mis en cache. |
| 404  | **Code** : `ConversationNotFound` <br/> **Message** : Conversation introuvable. | La conversation n’a pas été trouvée, car elle n’existe pas ou a été supprimée. | Non | Vérifiez si l’ID de conversation envoyé est une valeur attendue. Supprimez l’ID s’il a été mis en cache. |
| 412 | **Code** : `PreconditionFailed` <br/> **Message** : Échec de la condition préalable. Réessayez. | Une condition préalable a échoué sur l’une de nos dépendances en raison de plusieurs opérations simultanées sur la même conversation. | Oui | Réessayez avec un backoff exponentiel. |
| 413 | **Code** : `MessageSizeTooBig` <br/> **Message** : taille du message trop grande. | La taille de la requête entrante était trop grande. Pour plus d’informations, consultez [Mettre en forme vos messages de bot](/microsoftteams/platform/bots/how-to/format-your-bot-messages). | Non | Réduisez la taille de la charge utile. |
| 429 | **Code** : `Throttled` <br/> **Message** : Trop de demandes. Retourne également quand réessayer après. | Trop de demandes ont été envoyées par le bot. Pour plus d’informations, consultez [Limite de débit](/microsoftteams/platform/bots/how-to/rate-limit). | Oui | Réessayez à l’aide de `Retry-After` l’en-tête pour déterminer le temps d’interruption. |
| 500 | **Code** : `ServiceError` <br/> **Message** : *divers | Erreur interne au serveur. | Non | Signalez le problème dans la [communauté des développeurs](~/feedback.md#developer-community-help). |
| 502 | **Code** : `ServiceError` <br/> **Message** : *divers | Problème de dépendance de service. | Oui | Réessayez avec un backoff exponentiel. Si le problème persiste, signalez le problème dans la [communauté des développeurs](~/feedback.md#developer-community-help). |
| 503 | | Le service n’est pas disponible. | Oui | Réessayez avec un backoff exponentiel. Si le problème persiste, signalez le problème dans la [communauté des développeurs](~/feedback.md#developer-community-help). |
| 504 | | Délai d’expiration de la passerelle. | Oui | Réessayez avec un backoff exponentiel. Si le problème persiste, signalez le problème dans la [communauté des développeurs](~/feedback.md#developer-community-help). |

### <a name="status-codes-retry-guidance"></a>Conseils sur les nouvelles tentatives de codes d’état

Les instructions générales relatives aux nouvelles tentatives pour chaque code d’état sont répertoriées dans le tableau suivant. Le bot doit éviter de réessayer les codes d’état qui ne sont pas spécifiés :

|Code d'état | Stratégie de nouvelle tentative |
|----------------|-----------------|
| 403 | Réessayez en appelant l’API `https://smba.infra.gcc.teams.microsoft.com` GCC pour `InvalidBotApiHost`.|
| 412 | Réessayez à l’aide d’un backoff exponentiel. |
| 429 | Réessayez à l’aide `Retry-After` de l’en-tête pour déterminer le temps d’attente en secondes et entre les requêtes, le cas échéant. Sinon, réessayez à l’aide d’une interruption exponentielle avec l’ID de thread, si possible. |
| 502 | Réessayez à l’aide d’un backoff exponentiel. |
| 503 | Réessayez à l’aide d’un backoff exponentiel. |
| 504 | Réessayez à l’aide d’un backoff exponentiel. |

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | Node.js | . NETCore | Python | .NET |
|----------------|-----------------|--------------|----------------|-----------|-----|
| Bot de conversation Teams | Gestion des événements de messagerie et de conversation. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) | N/A |
| Localisation des applications Teams | Localisation d’applications Teams à l’aide du bot et de l’onglet. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) | N/A | N/A | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Menus de commandes Bot](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>Voir aussi

* [Envoyer des messages proactifs](~/bots/how-to/conversations/send-proactive-messages.md)
* [S’abonner à des événements de conversation](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Envoyer et recevoir des fichiers via le bot](~/bots/how-to/bots-filesv4.md)
* [Envoyer l’ID de locataire et l’ID de conversation aux en-têtes de demande du bot](~/bots/how-to/conversations/request-headers-of-the-bot.md)
* [Localiser votre application](../../../concepts/build-and-test/apps-localization.md)
