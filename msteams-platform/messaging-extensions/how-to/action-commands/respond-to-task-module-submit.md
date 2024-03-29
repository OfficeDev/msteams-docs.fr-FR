---
title: Répondre à l’action d’envoi du module de tâche
author: surbhigupta
description: Découvrez comment répondre à l’action d’envoi du module de tâche à partir d’une commande d’action d’extension de message avec un message proactif. Définissez les commandes de recherche et répondez aux recherches.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 96ba10d59eccbc95a73455641425a01a9f3f2c47
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820142"
---
# <a name="respond-to-the-task-module-submit-action"></a>Répondre à l’action d’envoi du module de tâche

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Ce document vous guide sur la façon dont votre application répond aux commandes d’action, telles que l’action d’envoi du module de tâche de l’utilisateur.
Une fois qu’un utilisateur a envoyé le module de tâche, votre service web reçoit un message `composeExtension/submitAction` appeler avec l’ID de commande et les valeurs de paramètre. Votre application dispose de cinq secondes pour répondre à l’appel.  

Vous disposez des options suivantes pour répondre :

* Aucune réponse : utilisez l’action d’envoi pour déclencher un processus dans un système externe et ne fournir aucun commentaire à l’utilisateur. Il est utile pour les processus de longue durée et pour fournir des commentaires alternativement. Par exemple, vous pouvez envoyer des commentaires avec un [message proactif](~/bots/how-to/conversations/send-proactive-messages.md).
* [Un autre module de tâche](#respond-with-another-task-module): vous pouvez répondre avec un module de tâche supplémentaire dans le cadre d’une interaction en plusieurs étapes.
* [Réponse de la carte](#respond-with-a-card-inserted-into-the-compose-message-area): vous pouvez répondre avec une carte avec laquelle l’utilisateur peut interagir ou l’insérer dans un message.
* [Carte adaptative de bot](#bot-response-with-adaptive-card): insérez une carte adaptative directement dans la conversation.
* [Demandez à l’utilisateur d’authentifier](~/messaging-extensions/how-to/add-authentication.md).
* [Demandez à l’utilisateur de fournir une configuration supplémentaire](~/get-started/first-message-extension.md).

Si l’application ne répond pas dans les cinq secondes, le client Teams retentera la demande deux fois avant d’envoyer un message d’erreur **Impossible d’atteindre l’application**. Si le bot répond après le délai d’expiration, la réponse est ignorée.

> [!NOTE]
> L’application doit différer toutes les actions de longue durée une fois que le bot a répondu à la demande d’appel. Les résultats de l’action de longue durée peuvent être remis sous forme de message.

Pour l’authentification ou la configuration, une fois que l’utilisateur a terminé le processus, l’appel d’origine est renvoyé à votre service web. Le tableau suivant indique les types de réponses disponibles, en fonction de l’emplacement `commandContext` d’appel de l’extension de message :

|Type de réponse | Composition | Barre de commandes | Message |
|--------------|:-------------:|:-------------:|:---------:|
|Réponse de la carte | ✔️ | ✔️ | ✔️ |
|Un autre module de tâche | ✔️ | ✔️ | ✔️ |
|Bot avec carte adaptative | ✔️ | ❌ | ✔️ |
| Aucune réponse | ✔️ | ✔️ | ✔️ |

> [!NOTE]
>
> * Lorsque vous sélectionnez **Action.Submit** via des cartes ME, il envoie l’activité invoke avec le nom **composeExtension**, où la valeur est égale à la charge utile habituelle.
> * Lorsque vous sélectionnez **Action.Submit** via la conversation, vous recevez une activité de message portant le nom **onCardButtonClicked**, où la valeur est égale à la charge utile habituelle.

Si l’application contient un bot conversationnel, installez-le dans la conversation, puis chargez le module de tâche. Le bot est utile pour obtenir un contexte supplémentaire pour le module de tâche. Pour installer le bot conversationnel, consultez [Demande d’installation de votre bot conversationnel](create-task-module.md#request-to-install-your-conversational-bot).

## <a name="the-submitaction-invoke-event"></a>Événement d’appel submitAction

Voici des exemples de réception du message d’appel :

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

Il s’agit d’un exemple de l’objet JSON que vous recevez. Le paramètre `commandContext` indique d’où votre extension de message a été déclenchée. L’objet `data` contient les champs du formulaire en tant que paramètres et les valeurs soumises par l’utilisateur. L’objet JSON met en évidence les champs les plus pertinents.

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Répondre avec une carte insérée dans la zone de composition du message

La méthode la plus courante pour répondre à la demande de `composeExtension/submitAction` consiste à insérer une carte dans la zone de composition du message. L’utilisateur envoie la carte à la conversation. Pour plus d’informations sur l’utilisation des cartes, consultez [cartes et actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
};
    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });
    response.ComposeExtension.Attachments = attachments;
    return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a>Répondre avec un autre module de tâche

Vous pouvez choisir de répondre à l’événement `submitAction` avec un module de tâche supplémentaire. Cela est utile lorsque vous avez besoin des éléments suivants :

* Collectez de grandes quantités d’informations.
* Modifiez dynamiquement la collecte d’informations en fonction de l’entrée utilisateur.
* Validez les informations envoyées par l’utilisateur et renvoyez le formulaire avec un message d’erreur en cas de problème.

La méthode de réponse est la même que [réponse à l’événement `fetchTask` initial](~/messaging-extensions/how-to/action-commands/create-task-module.md). Si vous utilisez le SDK Bot Framework, les mêmes déclencheurs d’événements sont utilisés pour les deux actions d’envoi. Pour que cela fonctionne, vous devez ajouter une logique qui détermine la réponse correcte.

## <a name="bot-response-with-adaptive-card"></a>Réponse du bot avec carte adaptative

> [!NOTE]
> The prerequisite to get the bot response with an Adaptive card is that you must add the `bot` object to your app manifest, and define the required scope for the bot. Use the same ID as your message extension for your bot.

Vous pouvez également répondre au `submitAction` en insérant un message avec une carte adaptative dans le canal avec un bot. L’utilisateur peut afficher un aperçu du message avant de l’envoyer. Cela est utile dans les scénarios où vous collectez des informations auprès des utilisateurs avant de créer une réponse de carte adaptative, ou lorsque vous mettez à jour la carte après qu’une personne interagit avec elle.

Le scénario suivant montre comment l’application Polly configure un sondage sans inclure les étapes de configuration dans la conversation de canal :

Pour configurer le sondage :

1. L’utilisateur sélectionne l’extension de message pour appeler le module de tâche.
1. L’utilisateur configure le sondage avec le module de tâche.
1. Après avoir soumis le module de tâche, l’application utilise les informations fournies pour générer le sondage en tant que carte adaptative et l’envoie en tant que réponse `botMessagePreview` au client.
1. L’utilisateur peut ensuite afficher un aperçu du message de carte adaptative avant que le bot ne l’insère dans le canal. Si l’application n’est pas membre du canal, sélectionnez `Send` pour l’ajouter.

    > [!NOTE]
    >
    > * Les utilisateurs peuvent également choisir de `Edit` le message, ce qui les renvoie au module de tâche d’origine.
    > * L’interaction avec la carte adaptative modifie le message avant de l’envoyer.
    >
1. Une fois que l’utilisateur a `Send`sélectionné , le bot publie le message sur le canal.

## <a name="respond-to-initial-submit-action"></a>Répondre à l’action d’envoi initiale

Votre module de tâche doit répondre au message de `composeExtension/submitAction` initial avec un aperçu de la carte que le bot envoie au canal. L’utilisateur peut vérifier la carte avant de l’envoyer et essayer d’installer votre bot dans la conversation si le bot est déjà installé.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

> [!NOTE]
>
> * Le `activityPreview` doit contenir une activité `message` avec exactement une pièce jointe de carte adaptative. La valeur `<< Card Payload >>` est un espace réservé pour la carte que vous souhaitez envoyer.

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a>Événements d’envoi et de modification botMessagePreview

Votre extension de message doit répondre à deux nouveaux types de l’appel `composeExtension/submitAction` , où `value.botMessagePreviewAction = "send"`et `value.botMessagePreviewAction = "edit"`.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="respond-to-botmessagepreview-edit"></a>Répondre à la modification botMessagePreview

Si l’utilisateur modifie la carte avant de l’envoyer, en sélectionnant **Modifier**, vous recevez un appel `composeExtension/submitAction` avec `value.botMessagePreviewAction = edit`. Répondez en retournant le module de tâche que vous avez envoyé, en réponse à l’appel initial `composeExtension/fetchTask` qui a commencé l’interaction. Cela permet à l’utilisateur de démarrer le processus en entrant à nouveau les informations d’origine. Utilisez les informations disponibles pour mettre à jour le module de tâche afin que l’utilisateur n’ait pas besoin de renseigner toutes les informations à partir de zéro.
Pour plus d’informations sur la réponse à l’événement de `fetchTask` initial, consultez [réponse à l’événement `fetchTask` initial](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Répondre à botMessagePreview envoyer

Une fois que l’utilisateur a sélectionné **Envoyer**, vous recevez un appel `composeExtension/submitAction` avec `value.botMessagePreviewAction = send`. Votre service web doit créer et envoyer un message proactif avec la carte adaptative à la conversation, et également répondre à l’appel.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];

      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };

      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Vous recevez un nouveau message de `composeExtension/submitAction` semblable à ce qui suit :

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="user-attribution-for-bots-messages"></a>Attribution d’utilisateur pour les messages de bots

Dans les scénarios où un bot envoie des messages pour le compte d’un utilisateur, l’attribution du message à cet utilisateur aide à l’engagement et présente un flux d’interaction plus naturel. Cette fonctionnalité vous permet d’attribuer un message de votre bot à un utilisateur au nom duquel il a été envoyé.

Dans l’image suivante, à gauche se trouve un message de carte envoyé par un bot sans attribution d’utilisateur et à droite une carte envoyée par un bot avec attribution d’utilisateur.

:::image type="content" source="../../../assets/images/messaging-extension/user-attribution-bots.png" alt-text="Bots d’attribution d’utilisateur":::

Pour utiliser l’attribution d’utilisateur dans teams, vous devez ajouter l’entité de mention`OnBehalfOf` à `ChannelData` dans votre charge utile `Activity` envoyée à Teams.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[JSON](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

#### <a name="details-of--onbehalfof-entity-schema"></a>Détails du schéma d’entité `OnBehalfOf`

La section suivante est une description des entités dans le tableau `OnBehalfOf` :

|Champ|Type|Description|
|:---|:---|:---|
|`itemId`|Entier|Décrit l’identification de l’élément. Sa valeur doit être `0`.|
|`mentionType`|Chaîne|Décrit la mention d’une « personne ».|
|`mri`|Chaîne|Identificateur de ressource de message (IRM) de la personne au nom de laquelle le message est envoyé. Le nom de l’expéditeur du message s’affiche comme «\<user\> via \<bot name\>».|
|`displayName`|Chaîne|Name of the person. Used as fallback in case name resolution is unavailable.|
  
## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Action d’extension de message Teams| Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’envoi du module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Recherche d'extension des messages Teams   |  Décrit comment définir les commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Définir les commandes de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="see-also"></a>Voir aussi

* [Schéma du manifeste d’application pour Teams](../../../resources/schema/manifest-schema.md)
* [Répondre à la commande de recherche](../search-commands/respond-to-search.md)
* [Extensions de messages](../../what-are-messaging-extensions.md)
