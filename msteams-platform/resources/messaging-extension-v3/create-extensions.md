---
title: Lancer des actions avec des extensions de messagerie
description: Créer des extensions de messagerie basées sur l’action pour permettre aux utilisateurs de déclencher des services externes
localization_priority: Normal
ms.topic: how-to
keywords: équipes de messagerie extensions de recherche d’extensions de messagerie
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566739"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Lancer des actions avec des extensions de messagerie

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie basées sur l’action permettent à vos utilisateurs de déclencher des actions dans des services externes à l’intérieur Teams.

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les sections suivantes décrivent comment le faire.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Extensions de messages de type action

Pour lancer des actions à partir d’une extension de messagerie définir `type` le paramètre à `action` . Voici un exemple d’un manifeste avec une recherche et une commande de création. Une seule extension de messagerie peut avoir jusqu’à 10 commandes différentes. Cela peut inclure à la fois plusieurs recherches et plusieurs commandes basées sur l’action.

#### <a name="complete-app-manifest-example"></a>Exemple complet de manifeste d’application

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

### <a name="initiate-actions-from-messages"></a>Initier des actions à partir de messages

En plus d’initier des actions à partir de la zone de message de composition, vous pouvez également utiliser votre extension de messagerie pour lancer une action à partir d’un message. Cela vous permettra d’envoyer le contenu du message à votre bot pour le traitement, et en option répondre à ce message avec une réponse en utilisant la méthode décrite [dans Répondre à soumettre](#responding-to-submit). La réponse sera insérée en réponse au message que vos utilisateurs peuvent modifier avant de soumettre. Vos utilisateurs peuvent accéder à votre extension de messagerie à partir du `...` menu de débordement, puis choisir `Take action` comme dans l’image suivante :

![Exemple d’initiation d’une action à partir d’un message](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Pour activer votre extension de messagerie à partir d’un message, vous devrez ajouter le `context` paramètre à l’objet de votre extension de `commands` messagerie dans votre manifeste d’application comme dans l’exemple ci-dessous. Les chaînes valides pour `context` le tableau `"message"` `"commandBox"` sont, , et `"compose"` . La valeur par défaut est `["compose", "commandBox"]`. Consultez la section [définir les commandes pour](#define-commands) plus de détails sur le `context` paramètre.

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

Voici un exemple de `value` l’objet contenant les détails du message qui seront envoyés dans le cadre de la `composeExtension` demande être envoyé à votre bot.

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

Vous pouvez tester votre extension de messagerie en téléchargeant votre application. Pour plus d’informations, [voir Télécharger votre application dans une équipe](~/concepts/deploy-and-publish/apps-upload.md).

Pour ouvrir votre extension de messagerie, accédez à l’un de vos chats ou canaux. Choisissez le **bouton Plus d’options** **(&#8943;)** dans la boîte de composition, et choisissez votre extension de messagerie.

## <a name="collecting-input-from-users"></a>Collecte des commentaires des utilisateurs

Il existe trois façons de recueillir des informations auprès d’un utilisateur final dans Teams.

### <a name="static-parameter-list"></a>Liste de paramètres statiques

Dans cette méthode, tout ce que vous devez faire est de définir une liste statique de paramètres dans le manifeste comme indiqué ci-dessus dans la commande « Créer To Do ». Pour utiliser cette méthode `fetchTask` assurez-vous est `false` défini et que vous définissez vos paramètres dans le manifeste.

Lorsqu’un utilisateur choisit une commande avec des paramètres statiques, Teams générera un formulaire dans un module de tâches avec les paramètres définis dans le manifeste. En appuyant sur Soumettre un `composeExtension/submitAction` est envoyé au bot. Pour plus d’informations sur l’ensemble attendu des réponses, [voir Répondre à soumettre](#responding-to-submit).

### <a name="dynamic-input-using-an-adaptive-card"></a>Entrée dynamique à l’aide d’une carte adaptative

Dans cette méthode, votre service peut définir une carte adaptative personnalisée pour collecter l’entrée utilisateur final. Pour cette approche, définissez le `fetchTask` paramètre `true` dans le manifeste. Notez que si vous `fetchTask` définissez `true` des paramètres statiques définis pour la commande seront ignorés.

Dans cette méthode, votre service recevra un événement `composeExtension/fetchTask` et doit répondre par une réponse de module de tâche basée sur la carte [adaptative.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) Voici un exemple de réponse avec une carte adaptative :

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

Le bot peut également répondre par une réponse auth/config si l’utilisateur a besoin d’authentifier ou de configurer l’extension avant d’obtenir l’entrée de l’utilisateur.

### <a name="dynamic-input-using-a-web-view"></a>Entrée dynamique à l’aide d’une vue Web

Dans cette méthode, votre service peut afficher un widget basé `<iframe>` pour afficher n’importe quelle interface utilisateur personnalisée et collecter l’entrée de l’utilisateur. Pour cette approche, définissez le `fetchTask` paramètre `true` dans le manifeste.

Tout comme dans le flux de carte adaptative de votre service sera envoyer un événement et doit `fetchTask` répondre avec une réponse de module de tâche basée sur [l’URL](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object). Voici un exemple de réponse avec une carte adaptative :

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

### <a name="request-to-install-your-conversational-bot"></a>Demande d’installation de votre bot conversationnel

Si votre application contient également un bot conversationnel, il peut être nécessaire de s’assurer que votre bot est installé dans la conversation avant de charger votre module de tâches. Cela peut être utile dans les situations où vous devez obtenir un contexte supplémentaire pour votre module de tâche. Par exemple, vous devrez peut-être aller chercher la liste pour remplir un contrôle de ramasseur de personnes, ou la liste des canaux dans une équipe.

Pour faciliter ce flux, lorsque votre extension de messagerie reçoit pour la première fois la `composeExtension/fetchTask` vérification d’invocation pour voir si votre bot est installé dans le contexte actuel. Vous pouvez y parvenir en essayant d’obtenir l’appel de liste, par exemple, Si votre bot n’est pas installé, vous retournez une carte adaptative avec une action qui demande à l’utilisateur d’installer votre bot Voir l’exemple ci-dessous. Notez que cela nécessite que l’utilisateur a la permission d’installer des applications à cet endroit; s’ils ne peuvent pas, ils recevront un message leur demandant de contacter leur administrateur.

Voici un exemple de la réponse :

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

Une fois que l’utilisateur a terminé l’installation, votre bot recevra un autre message d’invocer `name = composeExtension/submitAction` avec , et `value.data.msteams.justInTimeInstall = true` .

Voici un exemple de l’invocant :

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

Vous devez répondre à cette invocant avec la même réponse de tâche que vous auriez répondu avec si le bot était déjà installé.

## <a name="responding-to-submit"></a>Répondre à soumettre

Une fois qu’un utilisateur a terminé la saisie de son entrée, votre bot recevra un événement `composeExtension/submitAction` avec l’id de commande et les valeurs de paramètres définies.

Ce sont les différentes réponses attendues à un `submitAction` .

### <a name="task-module-response"></a>Réponse du module de tâche

Ceci est utilisé lorsque votre extension a besoin d’enchaîner les dialogues ensemble pour obtenir plus d’informations. La réponse est exactement la même que mentionnée `fetchTask` précédemment.

### <a name="compose-extension-authconfig-response"></a>Composer l’extension auth/config réponse

Ceci est utilisé lorsque votre extension doit authentifier ou configurer afin de continuer. Pour plus d’informations, consultez la [section authentification](~/resources/messaging-extension-v3/search-extensions.md#authentication) dans la section recherche.

### <a name="compose-extension-result-response"></a>Composer la réponse de résultat d’extension

Cela a servi à insérer une carte dans la boîte de composition à la suite d’une commande. C’est la même réponse qui est utilisée dans la commande de recherche, mais elle est limitée à une carte ou un résultat dans le tableau.

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Répondez par un message de carte adaptative envoyé à partir d’un bot

Vous pouvez également répondre à l’action soumettre en insérant un message avec une carte adaptative dans le canal avec un bot. Votre utilisateur sera en mesure de prévisualiser le message avant de le soumettre, et potentiellement modifier / interagir avec lui ainsi. Cela peut être très utile dans les scénarios où vous devez recueillir des informations auprès de vos utilisateurs avant de créer une réponse de carte adaptative. Le scénario suivant montre comment vous pouvez utiliser ce flux pour configurer un sondage sans inclure les étapes de configuration dans le message du canal.

1. L’utilisateur clique sur l’extension de messagerie pour déclencher le module de tâches.
1. L’utilisateur utilise le module de tâches pour configurer le sondage.
1. Après avoir soumis le module de tâche de configuration, l’application utilise les informations fournies dans le module de tâches pour concevoir une carte adaptative et `botMessagePreview` l’envoie en réponse au client.
1. L’utilisateur peut alors prévisualiser le message de la carte adaptative avant que le bot ne l’insère dans le canal. Si le bot n’est pas déjà membre du canal, en cliquant `Send` ajoutera le bot.
1. Interagir avec la carte adaptative changera le message avant de l’envoyer.
1. Une fois que `Send` l’utilisateur clique sur le bot affichera le message sur le canal.

Pour activer ce flux, votre module de tâches doit répondre comme dans l’exemple ci-dessous, qui présentera le message d’aperçu à l’utilisateur.

>[!Note]
>Le `activityPreview` must contient une activité avec exactement `message` 1 pièce jointe de carte adaptative.

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

Votre extension de message devra maintenant répondre à deux nouveaux types d’interactions, `value.botMessagePreviewAction = "send"` et `value.botMessagePreviewAction = "edit"` . Voici un exemple de `value` l’objet que vous devrez traiter :

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

Lorsque vous répondez à `edit` la demande, vous devez répondre `task` par une réponse avec les valeurs remplies des informations que l’utilisateur a déjà soumises. Lorsque vous répondez à `send` la demande, vous devez envoyer un message au canal contenant la carte adaptative finalisée.

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

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Cet exemple montre ce flux à [l’aide de la Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

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

## <a name="see-also"></a>Voir aussi

[Échantillons de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)