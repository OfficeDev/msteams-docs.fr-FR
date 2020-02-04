---
title: Répondre à l’action soumettre du module de tâche
author: clearab
description: Indique comment répondre à l’action d’envoi d’un module de tâche à partir d’une commande action d’extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 33a9388ee84dcf03a5bda59c5a5139c6f49bde6c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673853"
---
# <a name="respond-to-the-task-module-submit-action"></a>Répondre à l’action soumettre du module de tâche

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Une fois qu’un utilisateur soumet le module de tâche, votre service Web reçoit `composeExtension/submitAction` un message d’appel avec l’ID de commande et les valeurs de paramètre définies. Votre application disposera de cinq secondes pour répondre à l’appel, sinon l’utilisateur recevra un message d’erreur « Impossible d’atteindre l’application », et toute réponse à l’appel sera ignorée par le client Teams.

Vous disposez des options suivantes pour répondre.

* Aucune réponse : vous pouvez choisir d’utiliser l’action envoyer pour déclencher un processus dans un système externe et ne pas fournir de commentaires à l’utilisateur. Cela peut être utile pour les processus de longue durée et vous pouvez choisir de fournir des commentaires d’une autre manière (par exemple, avec un [message proactif](~/bots/how-to/conversations/send-proactive-messages.md).
* [Un autre module de tâches](#respond-with-another-task-module) -vous pouvez répondre avec un module de tâche supplémentaire dans le cadre d’une interaction en plusieurs étapes.
* [Réponse](#respond-with-a-card-inserted-into-the-compose-message-area) de la carte : vous pouvez répondre avec une carte à laquelle l’utilisateur peut interagir et/ou insérer dans un message.
* [Carte adaptative à partir de bot](#bot-response-with-adaptive-card) : Insérez une carte adaptative directement dans la conversation.
* [Demander à l’utilisateur de s’authentifier](~/messaging-extensions/how-to/add-authentication.md)
* [Demander à l’utilisateur de fournir une configuration supplémentaire](~/messaging-extensions/how-to/add-configuration-page.md)

Le tableau ci-dessous indique les types de réponses disponibles en fonction de l’emplacement`commandContext`d’appel () de l’extension de messagerie. Pour l’authentification ou la configuration, une fois que l’utilisateur a terminé le flux, l’appel d’origine sera renvoyé à votre service Web.

|Type de réponse | composition | barre de commande | message |
|--------------|:-------------:|:-------------:|:---------:|
|Réponse de carte | x | x | x |
|Un autre module de tâches | x | x | x |
|Robot avec carte adaptative | x |  | x |
| Aucune réponse | x | x | x |

## <a name="the-submitaction-invoke-event"></a>Événement d’appel submitAction

Vous trouverez ci-dessous des exemples de réception du message d’appel.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

Voici un exemple de l’objet JSON que vous recevrez. Le `commandContext` paramètre indique l’emplacement à partir duquel votre extension de messagerie a été déclenchée. L' `data` objet contient les champs du formulaire en tant que paramètres, ainsi que les valeurs que l’utilisateur a envoyées. L’objet JSON ici est raccourci pour mettre en surbrillance les champs les plus pertinents.

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Répondre avec une carte insérée dans la zone de message de composition

La façon la plus courante de répondre à `composeExtension/submitAction` la demande est d’insérer une carte insérée dans la zone de message de composition. L’utilisateur peut alors choisir de soumettre la carte à la conversation. Pour plus d’informations sur l’utilisation des cartes [, voir cartes et](~/task-modules-and-cards/cards/cards-actions.md)cartes.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    dynamic Data = JObject.Parse(action.Data.ToString());
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var card = new HeroCard
    {
        Title = Data["formField1"] as string,
        Subtitle = Data["formField2"]  as string,
        Text = Data["formField3"]  as string,
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

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

## <a name="respond-with-another-task-module"></a>Répondre à l’aide d’un autre module de tâches

Vous pouvez choisir de répondre à l' `submitAction` événement à l’aide d’un module de tâche supplémentaire. Cela peut être utile dans les cas suivants :

* Vous devez collecter de grandes quantités d’informations.
* Si vous devez modifier dynamiquement les informations que vous collectez en fonction de l’entrée de l’utilisateur
* Si vous devez valider les informations envoyées par l’utilisateur et éventuellement renvoyer le formulaire avec un message d’erreur si un problème se produit. 

La méthode pour la réponse est la même que pour [répondre à `fetchTask` l’événement initial](~/messaging-extensions/how-to/action-commands/create-task-module.md). Si vous utilisez le kit de développement logiciel (SDK) de robot, le même événement se déclenche pour les deux actions d’envoi. Cela signifie que vous devez être sûr d’ajouter une logique qui détermine la bonne réponse.

## <a name="bot-response-with-adaptive-card"></a>Réponse à un bot avec carte adaptative

>[!Note]
>Ce flux nécessite que vous ajoutiez `bot` l’objet à votre manifeste d’application et que vous disposez de l’étendue nécessaire définie pour le bot. Utilisez le même ID que votre extension de messagerie pour votre robot.

Vous pouvez également répondre à l’action d’envoi en insérant un message avec une carte adaptative dans le canal avec un bot. Votre utilisateur pourra prévisualiser le message avant de l’envoyer et éventuellement modifier/interagir avec. Cela peut être très utile dans les scénarios où vous devez recueillir des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative, ou lorsque vous devez mettre à jour la carte après qu’une personne interagit avec elle. Le scénario suivant montre comment l’application Polly utilise ce flux pour configurer un sondage sans inclure les étapes de configuration dans la conversation de canal.

1. L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâches.
2. L’utilisateur configure le sondage avec la tâche moudule.
3. Après avoir soumis le module de tâches, l’application utilise les informations fournies pour créer le sondage en tant que carte adaptative et l' `botMessagePreview` envoie en réponse au client.
4. L’utilisateur peut alors prévisualiser le message de la carte adaptative avant de l’insérer dans le canal. Si l’application n’est pas déjà membre du canal, le fait `Send` de cliquer sur l’ajoutera.
   1. L’utilisateur peut également choisir d' `Edit` utiliser le message, qui le renvoie au module de tâche d’origine.
5. L’interaction avec la carte adaptative modifie le message avant de l’envoyer.
6. Une fois que l' `Send` utilisateur clique sur le robot envoie le message au canal.

### <a name="respond-to-initial-submit-action"></a>Répondre à l’action d’envoi initiale

Pour activer ce flux, votre module de tâches doit répondre au `composeExtension/submitAction` message initial avec un aperçu de la carte que le bot enverra au canal. Cela permet à l’utilisateur de vérifier la carte avant de l’envoyer et d’essayer d’installer votre robot dans la conversation si celle-ci n’est pas déjà installée.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic Data = JObject.Parse(action.Data.ToString());
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

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

>[!Note]
>Le `activityPreview` doit contenir une `message` activité avec exactement 1 pièce jointe de carte adaptative. La `<< Card Payload >>` valeur est un espace réservé pour la carte que vous souhaitez envoyer.

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

Votre extension de message doit maintenant répondre à deux nouvelles variétés de l' `composeExtension/submitAction` appel, où `value.botMessagePreviewAction = "send"`et. `value.botMessagePreviewAction = "edit"`

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a>Répondre à botMessagePreview modifier

Si l’utilisateur décide de modifier la carte avant de l’envoyer en cliquant sur le bouton **modifier** , vous `composeExtension/submitAction` recevrez `value.botMessagePreviewAction = edit`un appel avec. Vous devez généralement répondre en renvoyant le module de tâches que vous avez envoyé en `composeExtension/fetchTask` réponse à l’appel initial qui a commencé l’interaction. Cela permet à l’utilisateur de commencer le processus en entrant de nouveau les informations d’origine. Vous devez également envisager d’utiliser les informations dont vous disposez maintenant pour pré-remplir le module de tâche afin que l’utilisateur n’ait pas rempli toutes les informations de toutes pièces.

Consultez [la rubrique relative à `fetchTask` la réponse à l’événement initial](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Répondre à l’envoi botMessagePreview

Une fois que l’utilisateur clique sur le bouton **Envoyer** , `composeExtension/submitAction` vous recevrez un appel avec `value.botMessagePreviewAction = send`. Votre service Web devra créer et envoyer un message proactif avec la carte adaptative à la conversation, ainsi que répondre à l’appel.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

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
      const responseActivity = { type: 'message', attachments: [adaptiveCard] };
    
      await context.sendActivity(responseActivity);
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

Vous recevrez un nouveau `composeExtension/submitAction` message similaire à celui ci-dessous.

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

## <a name="next-steps"></a>Étapes suivantes

Ajouter une commande de recherche

* [Définir des commandes de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
