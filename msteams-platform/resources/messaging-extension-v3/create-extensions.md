---
title: Lancer des actions avec des extensions de messagerie
description: Créer des extensions de messagerie basées sur l'action pour permettre aux utilisateurs de déclencher des services externes
localization_priority: Normal
ms.topic: how-to
keywords: teams messaging extensions messaging extensions search
ms.openlocfilehash: a3122dbaf79f57054cfec2e8aef2ed4f687338be
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019733"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Lancer des actions avec des extensions de messagerie

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie basées sur des actions permettent à vos utilisateurs de déclencher des actions dans des services externes à l'intérieur de Teams.

![Exemple de carte d'extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les sections suivantes décrivent comment faire.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Extensions de message de type d'action

Pour lancer des actions à partir d'une extension de messagerie, définissez `type` le paramètre sur `action` . Voici un exemple de manifeste avec une recherche et une commande de création. Une seule extension de messagerie peut avoir jusqu'à 10 commandes différentes. Cela peut inclure à la fois plusieurs commandes de recherche et plusieurs commandes basées sur l'action.

#### <a name="complete-app-manifest-example"></a>Exemple de manifeste d'application complet

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a>Lancer des actions à partir de messages

En plus de lancer des actions à partir de la zone composer un message, vous pouvez également utiliser votre extension de messagerie pour lancer une action à partir d'un message. Cela vous permettra d'envoyer le contenu du message à votre bot pour traitement et éventuellement de répondre à ce message avec une réponse à l'aide de la méthode décrite dans Répondre à [l'envoi.](#responding-to-submit) La réponse est insérée en tant que réponse au message que vos utilisateurs peuvent modifier avant d'envoyer. Vos utilisateurs peuvent accéder à votre extension de messagerie à partir du menu de dépassement, puis en sélectionnant comme `...` `Take action` dans l'image ci-dessous.

![Exemple de début d'une action à partir d'un message](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Pour que votre extension de messagerie fonctionne à partir d'un message, vous devez ajouter le paramètre à l'objet de votre extension de messagerie dans le manifeste de votre application, comme dans `context` `commands` l'exemple ci-dessous. Les chaînes `context` valides pour le tableau `"message"` sont , et `"commandBox"` `"compose"` . La valeur par défaut est `["compose", "commandBox"]`. Consultez la section [Définir des commandes](#define-commands) pour obtenir des détails complets sur le `context` paramètre.

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

Voici un exemple de l'objet contenant les détails du message qui sera envoyé dans le cadre de la `value` `composeExtension` demande à votre bot.

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

### <a name="test-via-uploading"></a>Test via le téléchargement

Vous pouvez tester votre extension de messagerie en chargeant votre application. Pour [plus d'informations, voir](~/concepts/deploy-and-publish/apps-upload.md) Chargement de votre application dans une équipe.

Pour ouvrir votre extension de messagerie, accédez à vos conversations ou canaux. Choisissez le **bouton Plus d'options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de messagerie.

## <a name="collecting-input-from-users"></a>Collecte des entrées des utilisateurs

Il existe trois façons de collecter des informations auprès d'un utilisateur final dans Teams.

### <a name="static-parameter-list"></a>Liste des paramètres statiques

Dans cette méthode, il vous suffit de définir une liste statique de paramètres dans le manifeste, comme illustré ci-dessus dans la commande « Créer pour faire ». Pour utiliser cette méthode, `fetchTask` assurez-vous que vous définissez vos `false` paramètres dans le manifeste.

Lorsqu'un utilisateur choisit une commande avec des paramètres statiques, Teams génère un formulaire dans un module de tâche avec les paramètres définis dans le manifeste. Sur la touche Envoyer, a `composeExtension/submitAction` est envoyé au bot. Pour plus [d'informations](#responding-to-submit) sur l'ensemble de réponses attendu, voir la rubrique Répondant à envoyer.

### <a name="dynamic-input-using-an-adaptive-card"></a>Entrée dynamique à l'aide d'une carte adaptative

Dans cette méthode, votre service peut définir une carte adaptative personnalisée pour collecter les entrées de l'utilisateur final. Pour cette approche, définissez `fetchTask` le paramètre sur dans le `true` manifeste. Notez que si vous `fetchTask` définissez des `true` paramètres statiques définis pour la commande, ils seront ignorés.

Dans cette méthode, votre service recevra un événement et devra répondre avec une réponse de module de tâche basée sur une carte `composeExtension/fetchTask` [adaptative.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) Voici un exemple de réponse avec une carte adaptative :

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

Le bot peut également répondre avec une réponse d'authentification/configuration si l'utilisateur doit authentifier ou configurer l'extension avant d'obtenir l'entrée de l'utilisateur.

### <a name="dynamic-input-using-a-web-view"></a>Entrée dynamique à l'aide d'un affichage web

Dans cette méthode, votre service peut afficher un widget basé pour afficher n'importe quelle interface utilisateur personnalisée `<iframe>` et collecter les entrées utilisateur. Pour cette approche, définissez `fetchTask` le paramètre sur dans le `true` manifeste.

Tout comme dans le flux de carte adaptative, votre service enverra un événement et doit répondre avec une réponse de module de tâche basée sur `fetchTask` [une](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)URL. Voici un exemple de réponse avec une carte adaptative :

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

### <a name="request-to-install-your-conversational-bot"></a>Demande d'installation de votre bot de conversation

Si votre application contient également un bot de conversation, il peut être nécessaire de s'assurer que votre bot est installé dans la conversation avant de charger votre module de tâche. Cela peut être utile dans les situations où vous devez obtenir un contexte supplémentaire pour votre module de tâche. Par exemple, vous devrez peut-être extraire la liste de membres pour remplir un contrôle de s picker de personnes ou la liste des canaux d'une équipe.

Pour faciliter ce flux, lorsque votre extension de messagerie reçoit d'abord la vérification d'appel pour voir si votre bot est installé dans le contexte actuel (vous pouvez le faire en essayant d'obtenir un appel de liste, par `composeExtension/fetchTask` exemple). Si votre bot n'est pas installé, vous renvoyez une carte adaptative avec une action qui demande à l'utilisateur d'installer votre bot. Consultez l'exemple ci-dessous. Notez que l'utilisateur doit avoir l'autorisation d'installer des applications à cet emplacement . Si ce n'est pas le cas, un message leur demande de contacter leur administrateur.

Voici un exemple de réponse :

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

Une fois que l'utilisateur a terminé l'installation, votre bot reçoit un autre message d'appel `name = composeExtension/submitAction` avec , et `value.data.msteams.justInTimeInstall = true` .

Voici un exemple d'appel :

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

Vous devez répondre à cet appel avec la même réponse à la tâche avec qui vous ariez répondu si le bot était déjà installé.

## <a name="responding-to-submit"></a>Réponse à l'soumission

Une fois qu'un utilisateur a entré son entrée, votre bot reçoit un événement avec l'ID de commande et les valeurs `composeExtension/submitAction` de paramètre définies.

Voici les différentes réponses attendues à un `submitAction` .

### <a name="task-module-response"></a>Réponse du module de tâche

Cette valeur est utilisée lorsque votre extension doit chaîner des boîtes de dialogue pour obtenir plus d'informations. La réponse est identique à ce qui a `fetchTask` été mentionné précédemment.

### <a name="compose-extension-authconfig-response"></a>Réponse d'th/config d'extension de composition

Il est utilisé lorsque votre extension doit s'authentifier ou configurer pour continuer. Pour plus [d'informations,](~/resources/messaging-extension-v3/search-extensions.md#authentication) voir la section sur l'authentification dans la section de recherche.

### <a name="compose-extension-result-response"></a>Réponse aux résultats de l'extension de composition

Cette commande sert à insérer une carte dans la zone de composition à la suite d'une commande. Il s'agit de la même réponse que celle utilisée dans la commande de recherche, mais elle est limitée à une carte ou à un résultat dans le tableau.

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Répondre avec un message de carte adaptative envoyé à partir d'un bot

Vous pouvez également répondre à l'action d'envoyer en insérant un message avec une carte adaptative dans le canal avec un bot. Votre utilisateur pourra prévisualiser le message avant de l'envoyer, et éventuellement le modifier/interagir avec celui-ci. Cela peut être très utile dans les scénarios où vous devez collecter des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative. Le scénario suivant montre comment utiliser ce flux pour configurer un sondage sans inclure les étapes de configuration dans le message de canal.

1. L'utilisateur clique sur l'extension de messagerie pour déclencher le module de tâche.
1. L'utilisateur utilise le module de tâche pour configurer le sondage.
1. Après avoir soumis le module de tâche de configuration, l'application utilise les informations fournies dans le module de tâche pour créer une carte adaptative et l'envoie en réponse `botMessagePreview` au client.
1. L'utilisateur peut ensuite afficher un aperçu du message de carte adaptative avant que le bot l'insère dans le canal. Si le bot n'est pas déjà membre du canal, un clic `Send` ajoute le bot.
1. L'interaction avec la carte adaptative modifie le message avant de l'envoyer.
1. Une fois que l'utilisateur `Send` clique sur le bot, il publie le message sur le canal.

Pour activer ce flux, votre module de tâche doit répondre comme dans l'exemple ci-dessous, qui présente le message d'aperçu à l'utilisateur.

>[!Note]
>Le `activityPreview` doit contenir une activité avec exactement 1 pièce jointe `message` de carte adaptative.

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

Votre extension de message devra désormais répondre à deux nouveaux types d'interactions, `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` . Voici un exemple de `value` l'objet que vous devrez traiter :

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

Lorsque vous répondez à la demande, vous devez répondre par une réponse avec les valeurs remplies avec les informations que `edit` `task` l'utilisateur a déjà envoyées. Lorsque vous répondez à la demande, vous devez envoyer un message au canal `send` contenant la carte adaptative finalisée.

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

*Voir aussi des* [exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Cet exemple illustre ce flux à l'aide du [SDK Microsoft.Bot.Connector.Teams (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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
