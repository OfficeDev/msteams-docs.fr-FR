---
title: Initier des actions à l’aide des extensions de messagerie
description: Créer des extensions de messagerie basées sur des actions pour permettre aux utilisateurs de déclencher des services externes
keywords: extensions de messagerie teams
ms.openlocfilehash: 4eb5984f4a75f185accfe7ba87e9389361946959
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801372"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Initier des actions à l’aide des extensions de messagerie

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie basées sur les actions permettent à vos utilisateurs de déclencher des actions dans des services externes dans Teams.

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les sections suivantes décrivent la procédure à suivre.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Extensions de message de type d’action

Pour initier des actions à partir d’une extension de messagerie, définissez le `type` paramètre sur `action` . Voici un exemple de manifeste avec une recherche et une commande Create. Une extension de messagerie unique peut comporter jusqu’à 10 commandes différentes. Il peut s’agir de plusieurs commandes de recherche et de commandes basées sur une action.

#### <a name="complete-app-manifest-example"></a>Exemple de manifeste d’application complet

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a>Initier des actions à partir de messages

En plus d’initier des actions à partir de la zone de message de composition, vous pouvez également utiliser votre extension de messagerie pour initier une action à partir d’un message. Cela vous permettra d’envoyer le contenu du message à votre bot à des fins de traitement et, si vous le souhaitez, de répondre à ce message avec une réponse en utilisant la méthode décrite dans [réponse à envoyer](#responding-to-submit). La réponse est insérée en tant que réponse au message que vos utilisateurs peuvent modifier avant de les envoyer. Vos utilisateurs peuvent accéder à votre extension de messagerie à partir du menu de dépassement de capacité `...` , puis en sélectionnant `Take action` comme dans l’image ci-dessous.

![Exemple d’initiation d’une action à partir d’un message](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Pour permettre à votre extension de messagerie de fonctionner à partir d’un message, vous devez ajouter le `context` paramètre à l’objet de votre extension de messagerie `commands` dans votre manifeste de l’application, comme dans l’exemple ci-dessous. Les chaînes valides pour le `context` tableau sont `"message"` , `"commandBox"` et `"compose"` . La valeur par défaut est `["compose", "commandBox"]`. Pour plus d’informations sur le paramètre, reportez-vous à la section [define Commands](#define-commands) `context` .

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

Vous trouverez ci-dessous un exemple de l' `value` objet contenant les détails du message qui seront envoyés dans le cadre de l’envoi de la `composeExtension` demande à votre bot.

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
        "content": "this is the message"
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

### <a name="test-via-uploading"></a>Test via téléchargement

Vous pouvez tester votre extension de messagerie en téléchargeant votre application. Pour plus d’informations, consultez [la rubrique téléchargement de votre application dans une équipe](~/concepts/deploy-and-publish/apps-upload.md) .

Pour ouvrir votre extension de messagerie, accédez à l’une de vos conversations ou de vos canaux. Sélectionnez le bouton **autres options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de messagerie.

## <a name="collecting-input-from-users"></a>Collecte d’entrées auprès des utilisateurs

Il existe trois façons de collecter des informations auprès d’un utilisateur final dans Teams.

### <a name="static-parameter-list"></a>Liste de paramètres statiques

Dans cette méthode, tout ce que vous avez à faire est de définir une liste statique de paramètres dans le manifeste, comme indiqué ci-dessus dans la commande « créer une tâche ». Pour utiliser cette méthode, vérifiez que `fetchTask` la valeur est définie sur `false` et que vous définissez vos paramètres dans le manifeste.

Lorsqu’un utilisateur choisit une commande avec des paramètres statiques, teams génère un formulaire dans un module de tâches avec les paramètres définis dans le manifeste. Lors de l’envoi d’un `composeExtension/submitAction` est envoyé au bot. Pour plus d’informations sur le jeu de réponses attendu, reportez-vous à la rubrique [réponse à envoyer](#responding-to-submit) .

### <a name="dynamic-input-using-an-adaptive-card"></a>Entrée dynamique à l’aide d’une carte adaptative

Dans cette méthode, votre service peut définir une carte adaptative personnalisée pour collecter l’entrée de l’utilisateur final. Pour cette approche, définissez le `fetchTask` paramètre sur `true` dans le manifeste. Notez que si vous avez défini `fetchTask` sur `true` un paramètre statique défini pour la commande sera ignoré.

Dans cette méthode, votre service reçoit un `composeExtension/fetchTask` événement et doit répondre avec une [réponse de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basée sur une carte adaptative. Vous trouverez ci-dessous un exemple de réponse avec une carte adaptative :

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

Le bot peut également répondre avec une réponse auth/config si l’utilisateur doit authentifier ou configurer l’extension avant d’obtenir l’entrée de l’utilisateur.

### <a name="dynamic-input-using-a-web-view"></a>Entrée dynamique à l’aide d’une vue Web

Dans cette méthode, votre service peut afficher un `<iframe>` widget basé pour afficher une interface utilisateur personnalisée et collecter les données entrées par l’utilisateur. Pour cette approche, définissez le `fetchTask` paramètre sur `true` dans le manifeste.

Tout comme dans le flux de carte adaptative votre service enverra un `fetchTask` événement et doit répondre par une [réponse de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basée sur une URL. Vous trouverez ci-dessous un exemple de réponse avec une carte adaptative :

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a>Demande d’installation de votre bot de conversation

Si votre application contient également un bot de conversation, il peut s’avérer nécessaire de vous assurer que votre bot est installé dans la conversation avant de charger votre module de tâches. Cela peut être utile dans les situations où vous devez obtenir un contexte supplémentaire pour le module de tâches. Par exemple, il se peut que vous deviez extraire la liste pour remplir un contrôle sélecteur de personnes ou la liste des canaux d’une équipe.

Pour faciliter ce flux, lorsque votre extension de messagerie reçoit d’abord le `composeExtension/fetchTask` contrôle d’appel pour déterminer si votre bot est installé dans le contexte actuel (vous pouvez effectuer cette étape en tentant l’appel Get de la liste, par exemple). Si votre bot n’est pas installé, vous devez renvoyer une carte adaptative avec une action qui demande à l’utilisateur d’installer votre robot, comme dans l’exemple ci-dessous. Notez que l’utilisateur doit avoir l’autorisation d’installer des applications à cet emplacement ; s’ils ne peuvent pas se présenter, un message leur demande de contacter leur administrateur.

Voici un exemple de réponse :

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

Une fois l’installation terminée, votre bot reçoit un autre message d’appel avec `name = composeExtension/submitAction` , et `value.data.msteams.justInTimeInstall = true` .

Voici un exemple de l’appel :

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

Vous devez répondre à cet appel à l’aide de la même réponse de tâche que si le robot était déjà installé.

## <a name="responding-to-submit"></a>Réponse à l’envoi

Une fois qu’un utilisateur a terminé de saisir son entrée, le robot reçoit un `composeExtension/submitAction` événement avec l’ID de commande et les valeurs de paramètre définies.

Voici les différentes réponses attendues vers un `submitAction` .

### <a name="task-module-response"></a>Réponse du module de tâche

Elle est utilisée lorsque votre extension doit regrouper les boîtes de dialogue pour obtenir plus d’informations. La réponse est exactement la même que celle `fetchTask` mentionnée précédemment.

### <a name="compose-extension-authconfig-response"></a>Réponse d’authentification/configuration de l’extension de composition

Cette valeur est utilisée lorsque votre extension doit être authentifiée ou configurée pour continuer. Pour plus d’informations, consultez la [section authentification](~/resources/messaging-extension-v3/search-extensions.md#authentication) dans la section recherche.

### <a name="compose-extension-result-response"></a>Réponse aux résultats de l’extension de composition

Cette commande permet d’insérer une carte dans la zone de composition à la suite de la commande. Il s’agit de la même réponse que celle utilisée dans la commande de recherche, mais il est limité à une carte ou à un résultat dans la matrice.

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Répondre avec un message de carte adaptative envoyé à partir d’un bot

Vous pouvez également répondre à l’action d’envoi en insérant un message avec une carte adaptative dans le canal avec un bot. Votre utilisateur pourra prévisualiser le message avant de l’envoyer et éventuellement modifier/interagir avec. Cela peut être très utile dans les scénarios où vous devez recueillir des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative. Le scénario suivant montre comment vous pouvez utiliser ce flux pour configurer un sondage sans inclure les étapes de configuration dans le message du canal.

1. L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâches.
1. L’utilisateur utilise le module tâches pour configurer le sondage.
1. Après avoir soumis le module de tâches de configuration, l’application utilise les informations fournies dans le module de tâches pour concevoir une carte adaptative et l’envoie en `botMessagePreview` réponse au client.
1. L’utilisateur peut alors prévisualiser le message de la carte adaptative avant de l’insérer dans le canal. Si le bot n’est pas déjà membre du canal, le fait de cliquer sur `Send` ajoutera le bot.
1. L’interaction avec la carte adaptative modifiera le message avant de l’envoyer.
1. Une fois que l’utilisateur clique sur `Send` le bot, le message est publié vers le canal.

Pour activer ce flux, votre module de tâches doit répondre comme dans l’exemple ci-dessous, qui présente l’aperçu du message à l’utilisateur.

>[!Note]
>Le `activityPreview` doit contenir une `message` activité avec exactement 1 pièce jointe de carte adaptative.

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

Votre extension de message doit maintenant répondre à deux nouveaux types d’interactions `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` . Vous trouverez ci-dessous un exemple de l' `value` objet que vous devrez traiter :

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
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

Lors de la réponse à la `edit` demande, vous devez répondre avec une `task` réponse dont les valeurs sont remplies avec les informations que l’utilisateur a déjà envoyées. Lors de la réponse à la `send` demande, vous devez envoyer un message au canal contenant la carte adaptative finalisée.

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

*Voir aussi* [exemples de robots d’infrastructure](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Cet exemple illustre ce flux à l’aide du [Kit de développement logiciel (SDK) Microsoft. Bot. Connector. Teams (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```
