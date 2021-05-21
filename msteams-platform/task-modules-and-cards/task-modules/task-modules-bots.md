---
title: Utilisation de modules de tâche dans Microsoft Teams bots
description: Utilisation des modules de tâche avec Microsoft Teams bots, notamment les cartes Bot Framework, les cartes adaptatives et les liens profonds
localization_priority: Normal
ms.topic: how-to
keywords: bots d’équipes de modules de tâche
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566566"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Utilisation de modules de tâche à partir Microsoft Teams bots

Les modules de tâche peuvent être appelés à partir de bots Microsoft Teams à l’aide de boutons sur les cartes adaptatives et les cartes Bot Framework (Hero, Thumbnail et Office 365 Connector). Les modules de tâche offrent souvent une meilleure expérience utilisateur que les étapes de conversation multiples où, en tant que développeur, vous devez suivre l’état du bot et permettre à l’utilisateur d’interrompre/d’annuler la séquence.

Il existe deux façons d’invoquer des modules de tâche :

* **Nouveau type de message `task/fetch` d’appel.** L’utilisation de l’action de carte pour les cartes Bot Framework ou de l’action de carte pour les cartes adaptatives, avec , le module de tâche (une URL ou une carte adaptative) est récupéré dynamiquement à partir de `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` votre bot.
* **URL de lien profond.** À l’aide de la syntaxe de lien profond pour les [modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)de tâche, vous pouvez utiliser l’action de carte pour les cartes Bot Framework ou l’action de carte pour les cartes `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) adaptatives, respectivement. Avec les URL de lien profond, l’URL du module de tâche ou le corps de la carte adaptative est évidemment connu à l’avance, ce qui évite un aller-retour serveur par rapport à `task/fetch` .

>[!IMPORTANT]
>Pour garantir des communications sécurisées, `url` chacune `fallbackUrl` d’elles doit implémenter le protocole de chiffrement HTTPS.

## <a name="invoking-a-task-module-through-taskfetch"></a>L’vot d’un module de tâche par le biais de la tâche/extraction

Lorsque l’objet de l’action de carte ou est initialisé correctement (expliqué plus en détail ci-dessous), lorsqu’un utilisateur appuie sur le bouton, un message est envoyé `value` `invoke` au `Action.Submit` `invoke` bot. Dans la réponse HTTP au message, il existe un objet TaskInfo incorporé dans un objet wrapper, que Teams utilise pour afficher `invoke` le module de tâche. [](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)

![demande/réponse de tâche/extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

Examinons chaque étape plus en détail :

1. Cet exemple montre une carte Hero Bot Framework avec une action de carte « Acheter `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke)». La valeur de `type` la propriété est - le reste de `task/fetch` `value` l’objet peut être ce que vous voulez.
1. Le bot reçoit le `invoke` message HTTP POST.
1. Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200. Le schéma des réponses est décrit ci-dessous dans la discussion sur la [tâche/l’soumission,](#the-flexibility-of-tasksubmit)mais il est important de se souvenir maintenant que le corps de la réponse HTTP contient un objet [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incorporé dans un objet wrapper. Par exemple :

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

    L’événement et sa réponse pour les bots sont similaires, d’un point de vue conceptuel, à la `task/fetch` `microsoftTeams.tasks.startTask()` fonction dans le SDK client.
1. Microsoft Teams affiche le module de tâche.

## <a name="submitting-the-result-of-a-task-module"></a>Envoi du résultat d’un module de tâche

Lorsque l’utilisateur a terminé le module de tâche, l’envoi du résultat au bot est similaire à la façon dont il fonctionne avec les [onglets,](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)mais il existe quelques différences, il est donc également décrit ici.

* **HTML/JavaScript ( `TaskInfo.url` )**. Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK (appelée ci-après à des fins de `microsoftTeams.tasks.submitTask()` `submitTask()` lisibilité). Vous pouvez appeler sans paramètre si vous souhaitez simplement Teams fermer le module de tâche, mais la plupart du temps vous souhaiterez passer un objet ou une chaîne à `submitTask()` votre `submitHandler` . Passez-le simplement en tant que premier paramètre, `result` . Teams appelle : `submitHandler` sera et sera `err` l’objet/chaîne `null` que vous avez transmis à `result` `submitTask()` . Si vous appelez avec un paramètre, vous devez transmettre un ou plusieurs tableaux de chaînes : cela permet à Teams de valider que l’application qui envoie le résultat est la même que celle qui a appelé le module de `submitTask()` `result`  `appId` `appId` tâche. Votre bot recevra un `task/submit` message, y compris `result` comme décrit [ci-dessous.](#payload-of-taskfetch-and-tasksubmit-messages)
* **Carte adaptative ( `TaskInfo.card` )**. Le corps de la carte adaptative (tel que rempli par l’utilisateur) est envoyé au bot via un message lorsque l’utilisateur appuie sur `task/submit` un `Action.Submit` bouton.

## <a name="the-flexibility-of-tasksubmit"></a>Flexibilité de la tâche/de l’soumission

Dans la section précédente, vous avez appris que lorsque l’utilisateur termine avec un module de tâche appelé à partir d’un bot, le bot reçoit toujours un `task/submit invoke` message. En tant que développeur, vous avez plusieurs options pour *répondre* au `task/submit` message :

| Réponse du corps HTTP                      | Scénario                                |
| --------------------------------------- | --------------------------------------- |
| Aucun (ignorer le `task/submit` message) | La réponse la plus simple n’est pas du tout une réponse. Votre bot n’est pas tenu de répondre lorsque l’utilisateur a terminé avec le module de tâche. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams affiche la valeur `value` d’une zone de message électronique. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Vous permet de « chaîner » des séquences de cartes adaptatives ensemble dans une expérience d’Assistant/multi-étapes. _Notez que le chaînage de cartes adaptatives dans une séquence est un scénario avancé et n’est pas documenté ici. LNode.js exemple d’application la prend en charge, toutefois, et son fonctionnement est documenté dans [son README.md.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Charge utile des messages de tâche/d’extraction et de tâche/d’soumission

Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit un `task/fetch` objet `task/submit` Bot `Activity` Framework. Le niveau supérieur important apparaît ci-dessous :

| Propriété | Description                          |
| -------- | ------------------------------------ |
| `type`   | Toujours `invoke`              |
| `name`   | `task/fetch`L’une ou l’autre ou`task/submit` |
| `value`  | Charge utile définie par le développeur. Normalement, la structure de `value` l’objet reflète ce qui a été envoyé Teams. Dans ce cas, toutefois, il est différent, car nous voulons prendre en charge la récupération dynamique ( ) à partir de Bot Framework ( ) et les actions de carte adaptative ( ), et nous avons besoin d’un moyen de communiquer Teams au bot en plus de ce qui a été inclus dans `task/fetch` `value` `Action.Submit` `data` `context` `value` / `data` .<br/><br/>Pour ce faire, nous combinons les deux en un objet parent :<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>Exemple : réception et réponse à des messages d’appel de tâche/extraction et de tâche/soumission - Node.js

> [!NOTE]
> L’exemple de code ci-dessous a été modifié entre Technical Preview et la version finale de cette fonctionnalité : le schéma de la demande a été modifié pour suivre ce qui a été documenté dans `task/fetch` [la section précédente](#payload-of-taskfetch-and-tasksubmit-messages). Autrement dit, la documentation était correcte, mais pas l’implémentation. Consultez `// for Technical Preview [...]` les commentaires ci-dessous pour savoir ce qui a changé.

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>Exemple : réception et réponse à des messages d’appel de tâche/extraction et de tâche/soumission - C #

Dans C# bots, `invoke` les messages sont traitées par un contrôleur `HttpResponseMessage()` qui traite un `Activity` message. Les `task/fetch` demandes et les réponses sont `task/submit` JSON. Dans C#, il n’est pas aussi pratique de traiter du JSON brut que dans Node.js. Vous avez donc besoin de classes wrapper pour gérer la sérialisation vers et à partir de JSON. Il n’existe pas de prise en charge directe pour cela dans le [SDK Microsoft Teams C#,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) mais vous pouvez voir un exemple de ce à quoi ces classes de wrapper simples ressembleraient dans l’exemple d’application [C#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).

Voici un exemple de code C# pour la gestion et les messages à l’aide de ces `task/fetch` `task/submit` classes de wrapper ( , ), extrait `TaskInfo` de `TaskEnvelope` [l’exemple](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):

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

La fonction, qui définit les propriétés et les propriétés de l’objet pour chaque cas, n’est pas indiquée dans `SetTaskInfo()` `height` `width` `title` `TaskInfo` l’exemple ci-dessus. Voici le [code source pour SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Actions de carte Bot Framework et actions Action.Submit de carte adaptative

Le schéma des actions de carte Bot Framework est légèrement différent des actions de carte `Action.Submit` adaptative. Par conséquent, la façon d’appeler des modules de tâche est légèrement différente : l’objet dans contient un objet afin `data` `Action.Submit` qu’il n’interfère pas avec les autres propriétés `msteams` de la carte. Le tableau suivant présente un exemple de chacun d’eux :

| Action de carte Bot Framework                              | Action Action.Submit de carte adaptative                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a>Voir aussi

* [Microsoft Teams exemple de code du module de tâche : nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)