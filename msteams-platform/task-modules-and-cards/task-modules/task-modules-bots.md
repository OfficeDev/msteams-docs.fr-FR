---
title: Utilisation de modules de tâches dans Microsoft Teams bots
description: Comment utiliser des modules de tâches avec des bots Microsoft Teams, y compris des cartes Bot Framework, des cartes adaptatives et des liens profonds
localization_priority: Normal
ms.topic: how-to
keywords: modules de tâches équipes bots
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566566"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Utilisation de modules de tâches Microsoft Teams bots

Les modules de tâches peuvent être invoqués à partir de bots Microsoft Teams utilisant des boutons sur les cartes Adaptatives et les cartes Bot Framework (Hero, Thumbnail et Office 365 Connecteur). Les modules de tâches sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation où vous, en tant que développeur, devez garder une trace de l’état du bot et permettre à l’utilisateur d’interrompre/annuler la séquence.

Il existe deux façons d’invoquer des modules de tâches :

* **Un nouveau type d’invoquer le message `task/fetch` .** En utilisant `invoke` [l’action de](~/task-modules-and-cards/cards/cards-actions.md#invoke) la carte pour les cartes Bot Framework, ou `Action.Submit` [l’action de la](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) carte pour les cartes `task/fetch` adaptatives, avec , le module de tâche (soit une URL ou une carte adaptative) est récupéré dynamiquement à partir de votre bot.
* **Urls de liaison profonde.** En utilisant la [syntaxe de lien profond pour les modules de](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)tâche, vous pouvez utiliser `openUrl` [l’action de la](~/task-modules-and-cards/cards/cards-actions.md#openurl) carte pour les cartes Bot Framework ou `Action.OpenUrl` [l’action de la](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) carte pour les cartes adaptatives, respectivement. Avec des URL de lien profond, l’URL du module de tâche ou le corps de carte adaptative est évidemment connu à l’avance, en évitant un serveur aller-retour par rapport à `task/fetch` .

>[!IMPORTANT]
>Pour assurer la sécurité des communications, chacun `url` d’eux doit `fallbackUrl` implémenter le protocole de cryptage HTTPS.

## <a name="invoking-a-task-module-through-taskfetch"></a>Invocation d’un module de tâches par tâche/extraction

Lorsque `value` l’objet de `invoke` l’action de la carte ou est paramélisé de `Action.Submit` la bonne manière (expliqué plus en détail ci-dessous), quand un utilisateur appuie sur le `invoke` bouton un message est envoyé au bot. Dans la réponse HTTP au `invoke` message, il y a un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) intégré dans un objet d’emballage, que Teams utilise pour afficher le module de tâche.

![tâche/chercher la demande/réponse](~/assets/images/task-module/task-module-invoke-request-response.png)

Examinons chaque étape un peu plus en détail :

1. Cet exemple montre une carte Bot Framework Hero avec une action de `invoke` [carte « Acheter ».](~/task-modules-and-cards/cards/cards-actions.md#invoke) La valeur de la `type` propriété est - le reste de `task/fetch` `value` l’objet peut être ce que vous voulez.
1. Le bot reçoit le `invoke` message HTTP POST.
1. Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200. Le schéma de réponses est décrit [ci-dessous dans la discussion sur la tâche / soumettre](#the-flexibility-of-tasksubmit), mais la chose importante à retenir maintenant est que le corps de la réponse HTTP contient un objet [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) intégré dans un objet d’emballage. Par exemple :

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

    `task/fetch`L’événement et sa réponse pour les bots est similaire, conceptuellement, à la fonction dans le client `microsoftTeams.tasks.startTask()` SDK.
1. Microsoft Teams affiche le module de tâches.

## <a name="submitting-the-result-of-a-task-module"></a>Soumettre le résultat d’un module de tâches

Lorsque l’utilisateur est terminé avec le module de tâche, soumettre le résultat de retour au bot est similaire [à la façon dont il fonctionne avec des onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), mais il ya quelques différences, il est donc décrit ici aussi.

* **HTML / JavaScript ( `TaskInfo.url` )**. Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez `microsoftTeams.tasks.submitTask()` la fonction SDK (appelée ci-après à des `submitTask()` fins de lisibilité). Vous pouvez appeler sans paramètres si vous voulez juste Teams pour fermer le module de tâche, mais la plupart `submitTask()` du temps vous aurez envie de passer un objet ou une chaîne à votre `submitHandler` . Il suffit de passer comme le premier paramètre, `result` . Teams `submitHandler` invoqueront : `err` sera et `null` sera `result` l’objet/chaîne que vous avez passé à `submitTask()` . Si vous appelez avec `submitTask()` un `result` paramètre, vous devez passer un ou un tableau de chaînes : cela permet à Teams de valider que  `appId` l’application envoyant le résultat est la même qui a `appId` invoqué le module de tâche. Votre bot recevra un `task/submit` message, y compris tel que `result` décrit [ci-dessous](#payload-of-taskfetch-and-tasksubmit-messages).
* **Carte adaptative ( `TaskInfo.card` )**. Le corps de la carte adaptative (tel que rempli par l’utilisateur) sera envoyé au bot via un message lorsque `task/submit` l’utilisateur appuie sur n’importe quel `Action.Submit` bouton.

## <a name="the-flexibility-of-tasksubmit"></a>La flexibilité de la tâche/soumettre

Dans la section précédente, vous avez appris que lorsque l’utilisateur termine avec un module de tâche invoqué à partir d’un bot, le bot reçoit toujours un `task/submit invoke` message. En tant que développeur, vous avez plusieurs options *pour* répondre au `task/submit` message :

| RÉPONSE DU CORPS HTTP                      | Scénario                                |
| --------------------------------------- | --------------------------------------- |
| Aucun (ignorer le `task/submit` message) | La réponse la plus simple n’est pas du tout une réponse. Votre bot n’est pas tenu de répondre lorsque l’utilisateur a terminé avec le module de tâche. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams affichera la valeur `value` d’une boîte de messages contexturation. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Vous permet de « chaîne » des séquences de cartes adaptatives ensemble dans une expérience assistant / multi-étapes. _Notez que l’enchaînement des cartes adaptatives dans une séquence est un scénario avancé et non documenté ici. LNode.js appruvre d’exemple de l’exemple le prend en charge, cependant, et comment il fonctionne [est documenté dans README.md fichier](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Charge utile de tâche/recherche et tâche/soumettre des messages

Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit un `task/fetch` objet ou un objet Bot `task/submit` `Activity` Framework. L’important niveau supérieur apparaît ci-dessous :

| Propriété | Description                          |
| -------- | ------------------------------------ |
| `type`   | Sera toujours `invoke`              |
| `name`   | L’un `task/fetch` ou l’autre ou `task/submit` |
| `value`  | La charge utile définie par le développeur. Normalement, la structure de `value` l’objet reflète ce qui a été envoyé de Teams. Dans ce cas, cependant, c’est différent parce que nous voulons prendre en charge dynamique chercher ( `task/fetch` ) à la fois bot cadre ( ) et les actions de carte adaptative ( ), et nous avons besoin `value` `Action.Submit` `data` d’un moyen de communiquer Teams au bot en plus de ce qui a `context` été inclus dans `value` / `data` .<br/><br/>Pour ce faire, nous conjuons les deux dans un objet parent :<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Exemple : Recevoir et répondre à la tâche/aller chercher et la tâche/soumettre des messages invoquent - Node.js

> [!NOTE]
> Le code d’échantillon ci-dessous a été modifié entre l’aperçu technique et la version finale de cette fonctionnalité : le schéma de `task/fetch` la demande a été modifié pour suivre ce qui a été documenté dans la section [précédente.](#payload-of-taskfetch-and-tasksubmit-messages) C’est-à-dire que la documentation était correcte, mais la mise en œuvre ne l’était pas. Voir les commentaires `// for Technical Preview [...]` ci-dessous pour ce qui a changé.

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Exemple : Réception et réponse à la tâche/extraction et tâche/soumettre des messages invocants - C #

Dans les bots C#, `invoke` les messages sont traités par un contrôleur `HttpResponseMessage()` traitant un `Activity` message. Les `task/fetch` demandes et les réponses sont `task/submit` JSON. En C#, il n’est pas aussi pratique de traiter avec JSON brut qu’il est en Node.js, de sorte que vous avez besoin de classes wrapper pour gérer la sérialisation à et à partir de JSON. Il n’y a pas encore de support direct pour cela dans le Microsoft Teams [C # SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) encore, mais vous pouvez voir un exemple de ce que ces classes d’emballage simple ressemblerait dans l’application [échantillon C #](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).

Voici le code d’exemple en C# pour la `task/fetch` manipulation et les messages en utilisant ces classes `task/submit` d’emballage `TaskInfo` ( , ), extrait de `TaskEnvelope` [l’échantillon:](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)

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

Pas montré dans l’exemple ci-dessus `SetTaskInfo()` est la fonction, qui définit `height` le , et les propriétés de `width` `title` `TaskInfo` l’objet pour chaque cas. Voici le [code source pour SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework card actions vs Adaptive card Action.Submit actions

Le schéma des actions de carte Bot Framework est légèrement différent des actions de carte `Action.Submit` adaptative. Par conséquent, la façon d’invoquer les modules de tâches est légèrement différente aussi : `data` `Action.Submit` l’objet contient un `msteams` objet de sorte qu’il n’interfère pas avec d’autres propriétés de la carte. Le tableau suivant montre un exemple de chacun :

| Action de carte bot framework                              | Action de carte adaptative.Soumettre l’action                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a>Voir aussi

* [Microsoft Teams module de tâche de travail code d’échantillon - nœuds](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Échantillons bot framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).