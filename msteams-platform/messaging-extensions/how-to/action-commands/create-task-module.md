---
title: Créer et envoyer le module de tâches
author: clearab
description: Comment gérer l’action d’appel initiale et répondre avec un module de tâche à partir d’une commande d’extension de messagerie d’action
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072874"
---
# <a name="create-and-send-the-task-module"></a>Créer et envoyer le module de tâches

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Si vous ne remplissez pas le module de tâche avec les paramètres définis dans le manifeste de l’application, vous devez créer le module de tâche pour les utilisateurs. Utilisez une carte adaptative ou un affichage web incorporé.

## <a name="the-initial-invoke-request"></a>Demande d’appel initiale

À l’aide de cette méthode, votre service reçoit un objet de type et vous devez répondre avec un objet contenant la carte adaptative ou une URL vers `Activity` `composeExtension/fetchTask` l’affichage web `task` incorporé. Avec les propriétés d’activité standard du bot, la charge utile d’appel initiale contient les métadonnées de requête suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande. Il doit `invoke` l’être. |
|`name`| Type de commande qui est émis pour votre service. Il doit `composeExtension/fetchTask` l’être. |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| ID de canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| ID d’équipe (si la demande a été faite dans un canal). |
|`value.commandId` | Contient l’ID de la commande qui a été invoquée. |
|`value.commandContext` | Contexte qui a déclenché l’événement. Il doit `compose` l’être. |
|`value.context.theme` | Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé. Il doit `default` s’y `contrast` trouver, ou `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a>Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’une conversation 1:1 sont répertoriées dans la section suivante :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande. Il doit `invoke` l’être. |
|`name`| Type de commande qui est émis pour votre service. Il doit `composeExtension/fetchTask` l’être. |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.source.name`| Nom source de l’endroit où le module de tâche est appelé. |
|`ChannelData.legacy. replyToId`| Obtient ou définit l’ID du message auquel ce message est une réponse. |
|`value.commandId` | Contient l’ID de la commande qui a été invoquée. |
|`value.commandContext` | Contexte qui a déclenché l’événement. Il doit `compose` l’être. |
|`value.context.theme` | Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé. Il doit `default` s’y `contrast` trouver, ou `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a>Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’une conversation de groupe sont répertoriées dans la section suivante :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande. Il doit `invoke` l’être. |
|`name`| Type de commande qui est émis pour votre service. Il doit `composeExtension/fetchTask` l’être. |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.source.name`| Nom source de l’endroit où le module de tâche est appelé. |
|`ChannelData.legacy. replyToId`| Obtient ou définit l’ID du message auquel ce message est une réponse. |
|`value.commandId` | Contient l’ID de la commande qui a été invoquée. |
|`value.commandContext` | Contexte qui a déclenché l’événement. Il doit `compose` l’être. |
|`value.context.theme` | Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé. Il doit `default` s’y `contrast` trouver, ou `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a>Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’un canal (nouveau billet) sont répertoriées dans la section suivante :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande. Il doit `invoke` l’être. |
|`name`| Type de commande qui est émis pour votre service. Il doit `composeExtension/fetchTask` l’être. |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| ID de canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| ID d’équipe (si la demande a été faite dans un canal). |
|`channelData.source.name`| Nom source de l’endroit où le module de tâche est appelé. |
|`ChannelData.legacy. replyToId`| Obtient ou définit l’ID du message auquel ce message est une réponse. |
|`value.commandId` | Contient l’ID de la commande qui a été invoquée. |
|`value.commandContext` | Contexte qui a déclenché l’événement. Il doit `compose` l’être. |
|`value.context.theme` | Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé. Il doit `default` s’y `contrast` trouver, ou `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a>Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’un canal (réponse au thread) sont répertoriées dans la section suivante :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande. Il doit `invoke` l’être. |
|`name`| Type de commande qui est émis pour votre service. Il doit `composeExtension/fetchTask` l’être. |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| ID de canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| ID d’équipe (si la demande a été faite dans un canal). |
|`channelData.source.name`| Nom source de l’endroit où le module de tâche est appelé. |
|`ChannelData.legacy. replyToId`| Obtient ou définit l’ID du message auquel ce message est une réponse. |
|`value.commandId` | Contient l’ID de la commande qui a été invoquée. |
|`value.commandContext` | Contexte qui a déclenché l’événement. Il doit `compose` l’être. |
|`value.context.theme` | Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé. Il doit `default` s’y `contrast` trouver, ou `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a>Les propriétés de l’activité de charge utile lorsqu’un module de tâche est appelé à partir d’une zone de commande sont répertoriées dans la section suivante :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande. Il doit `invoke` l’être. |
|`name`| Type de commande qui est émis pour votre service. Il doit `composeExtension/fetchTask` l’être. |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d’objet Azure Active Directory de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.source.name`| Nom source de l’endroit où le module de tâche est appelé. |
|`value.commandId` | Contient l’ID de la commande qui a été invoquée. |
|`value.commandContext` | Contexte qui a déclenché l’événement. Il doit `compose` l’être. |
|`value.context.theme` | Thème client de l’utilisateur, utile pour la mise en forme de l’affichage web incorporé. Il doit `default` s’y `contrast` trouver, ou `dark` . |

### <a name="example-fetchtask-request"></a>Exemple de requête fetchTask

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
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
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>Demande d’appel initiale à partir d’un message

Lorsque votre bot est appelé à partir d’un message plutôt que de la zone de composition ou de la barre de commandes, l’objet de la demande initiale doit contenir les détails du message à partir de quel message votre extension de messagerie est `value` invoquée. Consultez la section suivante pour obtenir l’exemple de cet objet. Les tableaux et les tableaux sont facultatifs et ne sont pas présents s’il n’y a aucune réaction ou `reactions` mention dans le message `mentions` d’origine.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>Répondre à la tâche fetchTask

Répondez à la demande d’appel avec un objet qui contient un objet avec la carte adaptative ou l’URL web, ou `task` un message de chaîne `taskInfo` simple.

|Nom de la propriété|Objectif|
|---|---|
|`type`| Il peut `continue` s’agit de présenter un formulaire ou `message` d’utiliser une fenêtre popup simple. |
|`value`| Objet `taskInfo` d’un formulaire ou `string` d’un message. |

Le schéma de l’objet taskInfo est :

|Nom de la propriété|Objectif|
|---|---|
|`title`| Titre du module de tâche.|
|`height`| Il doit s’agit d’un nombre integer (en pixels) `small` ou , ou , `medium` `large` .|
|`width`| Il doit s’agit d’un nombre integer (en pixels) `small` ou , ou , `medium` `large` .|
|`card`| Carte adaptative définissant le formulaire (si vous en utilisez un).
|`url`| URL à ouvrir dans le module de tâche en tant qu’affichage web incorporé.|
|`fallbackUrl`| Si un client ne prend pas en charge la fonctionnalité de module de tâche, cette URL est ouverte dans un onglet de navigateur. |

### <a name="with-an-adaptive-card"></a>Avec une carte adaptative

Lorsque vous utilisez une carte adaptative, vous devez répondre avec un objet contenant `task` `value` une carte adaptative.

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a>Exemple de réponse fetchTask avec une carte adaptative

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Cet exemple utilise le [package NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) en plus du SDK Bot Framework.

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a>Avec un affichage web incorporé

Lorsque vous utilisez un affichage web incorporé, vous devez répondre avec un objet avec l’objet contenant l’URL du formulaire web que vous `task` `value` souhaitez charger. Les domaines d’une URL que vous souhaitez charger doivent être inclus dans le tableau dans le manifeste `validDomains` de votre application. Consultez la [documentation du module de](~/task-modules-and-cards/what-are-task-modules.md) tâche pour obtenir des informations complètes sur la création de votre affichage web incorporé.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>Demande d’installation de votre bot de conversation

Si l’application contient un bot de conversation, installez-le dans la conversation avant de charger le module de tâche. Il est utile d’obtenir un contexte supplémentaire pour le module de tâche. L’exemple type de ce scénario consiste à extraire la liste de membres pour remplir un contrôle de s picker de personnes ou la liste des canaux d’une équipe.

Lorsque l’extension de messagerie reçoit l’appel, vérifiez si le bot est installé dans le contexte actuel `composeExtension/fetchTask` pour faciliter le flux. Par exemple, vérifiez le flux avec un appel d’obtenir une liste de membres. Si le bot n’est pas installé, renvoyer une carte adaptative avec une action qui demande à l’utilisateur d’installer le bot. Voir l’action dans l’exemple suivant. L’utilisateur doit être autorisé à installer les applications à cet emplacement pour vérification. Si l’installation de l’application échoue, l’utilisateur reçoit un message pour contacter l’administrateur.

#### <a name="example-of-the-response"></a>Exemple de réponse :

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

Après l’installation, le bot reçoit un autre message d’appel avec `name = composeExtension/submitAction` , et `value.data.msteams.justInTimeInstall = true` .

#### <a name="example-of-the-invoke"></a>Exemple d’appel :

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

La réponse à la tâche à l’appel doit être similaire à celle du bot installé.

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a>Exemple d’installation juste-à-temps de l’application avec carte adaptative : 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a>Étapes suivantes

Si vous autorisez vos utilisateurs à renvoyer une réponse à partir du module de tâche, vous devez gérer l’action d’envoi.

* [Créer et répondre avec un module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
