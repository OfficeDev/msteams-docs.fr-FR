---
title: Utilisation des modules de tâches dans les robots Microsoft teams
description: Utilisation des modules de tâches avec les robots Microsoft Teams, y compris les cartes de l’infrastructure bot, des cartes adaptatives et des liens approfondis.
keywords: modules de tâches bots de teams
ms.openlocfilehash: 32fb6a4aa0a8bf2297a4f60331dc5c6c6aceb4e2
ms.sourcegitcommit: 214eccbadb7f3a67236b79a041ef487b7bf6dfbd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2020
ms.locfileid: "44801138"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Utilisation des modules de tâches dans les robots Microsoft teams

Les modules de tâches peuvent être appelés à partir de robots Microsoft teams à l’aide de boutons sur les cartes adaptatives et les cartes de l’infrastructure bot (connecteur héros, miniature et Office 365). Les modules de tâches sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation dans lesquelles vous êtes un développeur pour effectuer le suivi de l’état du bot et permettre à l’utilisateur d’interrompre/annuler la séquence.

Il existe deux façons d’appeler des modules de tâches :

* **Nouveau type de message d’appel `task/fetch` .** À l’aide de l' `invoke` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#invoke) pour les fiches de l’infrastructure bot ou de l' `Action.Submit` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) adaptative, avec `task/fetch` , le module de tâches (une URL ou une carte adaptative) est extrait dynamiquement à partir de votre bot.
* **URL de liens détaillés.** À l’aide de la [syntaxe de liens détaillés pour les modules de tâches](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), vous pouvez utiliser l' `openUrl` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#openurl) pour les cartes de l’infrastructure de robots ou l' `Action.OpenUrl` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) pour les cartes adaptatives, respectivement. Avec des URL de liens détaillés, l’URL du module de tâche ou le corps de la carte adaptative est évidemment connu à l’avance, ce qui évite d’effectuer un aller-retour de serveur par rapport à `task/fetch` .

>[!IMPORTANT]
>Pour garantir des communications sécurisées, chaque `url` et `fallbackUrl` doit implémenter le protocole de CHIFFREment HTTPS.

## <a name="invoking-a-task-module-via-taskfetch"></a>Appel d’un module de tâches via Task/Fetch

Lorsque l' `value` objet de l' `invoke` action de carte ou `Action.Submit` est initialisé de façon appropriée (expliqué en détail ci-dessous), lorsqu’un utilisateur appuie sur le bouton, un `invoke` message est envoyé au bot. Dans la réponse HTTP au `invoke` message, un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) est incorporé dans un objet de wrapper, que teams utilise pour afficher le module de tâches.

![demande/réponse de la tâche/de l’extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

Examinons chaque étape plus en détail :

1. Cet exemple illustre une carte héros de bot avec une action de carte « acheter » `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke). La valeur de la `type` propriété est `task/fetch` : le reste de l' `value` objet peut être ce que vous souhaitez.
2. Le bot reçoit le `invoke` message http post.
3. Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200. Le schéma des réponses est décrit [ci-dessous dans la discussion sur tâche/envoi](#the-flexibility-of-tasksubmit), mais il est important de se rappeler que le corps de la réponse http contient un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incorporé dans un objet de wrapper, par exemple :

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

    L' `task/fetch` événement et sa réponse pour les robots sont similaires, d’un plan conceptuel, à la `microsoftTeams.tasks.startTask()` fonction dans le kit de développement logiciel client.
4. Microsoft teams affiche le module tâches.

## <a name="submitting-the-result-of-a-task-module"></a>Envoi du résultat d’un module de tâche

Une fois que l’utilisateur a terminé d’utiliser le module de tâches, le fait de renvoyer le résultat au robot est similaire à celui de la [façon dont il fonctionne avec les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), mais il existe quelques différences, il est également décrit ici.

* **HTML/JavaScript ( `TaskInfo.url` )**. Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la `microsoftTeams.tasks.submitTask()` fonction SDK (désignée ci-dessous à des `submitTask()` fins de lisibilité). Vous pouvez appeler `submitTask()` sans aucun paramètre si vous souhaitez simplement que teams ferme le module de tâches, mais la plupart du temps, vous souhaiterez passer un objet ou une chaîne à votre `submitHandler` . Il suffit de la transmettre en tant que premier paramètre, `result` . Teams appellera `submitHandler` : `err` sera `null` et sera `result` l’objet/la chaîne que vous avez transmis `submitTask()` . Si vous appelez `submitTask()` avec un `result` paramètre, vous **devez** transmettre un `appId` tableau de chaînes ou un tableau `appId` : cela permet à teams de valider le fait que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâches. Votre bot recevra un `task/submit` message, `result` comme décrit [ci-dessous](#payload-of-taskfetch-and-tasksubmit-messages).
* **Carte adaptative ( `TaskInfo.card` )**. Le corps de la carte adaptative (tel qu’il est rempli par l’utilisateur) est envoyé au robot via un `task/submit` message lorsque l’utilisateur appuie sur n’importe quel `Action.Submit` bouton.

## <a name="the-flexibility-of-tasksubmit"></a>Flexibilité de la tâche/de l’envoi

Dans la section précédente, vous avez appris que lorsque l’utilisateur a terminé avec un module de tâche appelé à partir d’un bot, le bot reçoit toujours un `task/submit invoke` message. En tant que développeur, plusieurs options s’offrent à vous lorsque vous *répondez* au `task/submit` message :

| Réponse du corps HTTP                      | Scénario                                |
| --------------------------------------- | --------------------------------------- |
| Aucun (ignorer le `task/submit` message) | La réponse la plus simple n’est pas du tout. Votre robot n’est pas tenu de répondre lorsque l’utilisateur a terminé le module de tâches. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams affichera la valeur de `value` dans une boîte de message contextuel. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Vous permet de « chaîner » les séquences de cartes adaptatives dans un Assistant/une expérience en plusieurs étapes. _Notez que le chaînage de cartes adaptatives dans une séquence est un scénario avancé et n’est pas documenté ici. Toutefois, l’exemple d’application Node.js prend en charge cette méthode, mais elle est documentée dans [le fichier Readme.MD](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Charge utile des tâches/de l’extraction et des messages de tâches/d’envoi

Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit `task/fetch` un `task/submit` objet infrastructure de bot ou `Activity` . Le niveau le plus élevé s’affiche ci-dessous :

| Propriété | Description                          |
| -------- | ------------------------------------ |
| `type`   | Sera toujours`invoke`              |
| `name`   | Soit `task/fetch` ou`task/submit` |
| `value`  | Charge utile définie par le développeur. En règle générale, la structure de l' `value` objet reflète ce qui a été envoyé par Teams. Dans ce cas, toutefois, il est différent, car nous souhaitons prendre en charge l’extraction dynamique ( `task/fetch` ) à la fois de l’infrastructure bot ( `value` ) et des actions de carte adaptative `Action.Submit` ( `data` ), et nous avons besoin d’un moyen de communiquer teams `context` au robot en plus de ce qui a été inclus dans `value` / `data` .<br/><br/>Pour ce faire, nous combinons les deux dans un objet parent :<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Exemple : réception et réponse aux messages d’appel des tâches/extraction et tâches/envoi-Node.js

> [!NOTE]
> L’exemple de code ci-dessous a été modifié entre la version d’évaluation technique et la version finale de cette fonctionnalité : le schéma de la demande a été `task/fetch` modifié pour suivre ce qui a été [documenté dans la section précédente](#payload-of-taskfetch-and-tasksubmit-messages). Autrement dit, la documentation était correcte, mais l’implémentation ne l’était pas. Consultez les `// for Technical Preview [...]` commentaires ci-dessous pour en savoir plus sur ce qui a changé.

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
                    "type": "AdaptiveCard",
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Here is a ninja cat:"
                        },
                        {
                            "type": "Image",
                            "url": "http://adaptivecards.io/content/cats/1.png",
                            "size": "Medium"
                        }
                    ],
                    "version": "1.0"
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

*Voir aussi*l' [exemple de code du module de tâches de Microsoft Teams (NodeJS](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) et [robots](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)).

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Exemple : réception et réponse aux messages d’appel des tâches/extraction et tâches/envoi-C #

Dans les robots C#, `invoke` les messages sont traités par un `HttpResponseMessage()` contrôleur traitant un `Activity` message. Les `task/fetch` `task/submit` requêtes et réponses sont au format JSON. En C#, il n’est pas aussi commode de traiter le JSON brut en Node.js, donc vous avez besoin de classes wrapper pour gérer la sérialisation vers et à partir de JSON. Il n’existe pas encore de prise en charge directe de cette fonction dans le [Kit de développement logiciel (SDK) c#](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) de Microsoft Teams, mais vous pouvez voir un exemple de ce à quoi ressembleront ces classes wrapper simples dans l' [exemple d’application c#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).

Vous trouverez ci-dessous un exemple de code en C# pour `task/fetch` la gestion et les `task/submit` messages qui utilisent ces classes wrapper ( `TaskInfo` , `TaskEnvelope` ), extraits de l' [exemple](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

L’exemple ci-dessus ne montre pas la `SetTaskInfo()` fonction qui définit les `height` `width` Propriétés, et `title` de l' `TaskInfo` objet pour chaque cas. Voici le [code source pour SetTaskInfo ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Actions de carte d’infrastructure bot et action de carte adaptative. soumettre des actions

Le schéma des actions de carte de l’infrastructure de robots est légèrement différent des actions de carte adaptative `Action.Submit` . Par conséquent, le mode d’appel des modules de tâches est légèrement différent : l' `data` objet dans `Action.Submit` contient un `msteams` objet de sorte qu’il ne gêne pas les autres propriétés de la carte. Le tableau suivant montre un exemple de chacun :

| Action de carte de l’infrastructure bot                              | Action de carte adaptative. action d’envoi                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
