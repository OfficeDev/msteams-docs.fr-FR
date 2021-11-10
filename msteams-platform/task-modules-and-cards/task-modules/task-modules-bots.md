---
title: Utiliser des modules de tâche dans Microsoft Teams bots
description: Utilisation des modules de tâche avec Microsoft Teams bots, y compris les cartes Bot Framework, les cartes adaptatives et les liens profonds.
ms.localizationpriority: medium
ms.topic: how-to
keywords: modules de tâche teams bots carte adaptative liens profonds
ms.openlocfilehash: c46b647ca9fa446db6ae51ae6d33dbabdef18296
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888306"
---
# <a name="use-task-modules-from-bots"></a>Utiliser des modules de tâches à partir de bots
 
Les modules de tâche peuvent être appelés à partir de bots Microsoft Teams à l’aide de boutons sur les cartes adaptatives et les cartes Bot Framework qui sont hero, thumbnail et Office 365 Connector. Les modules de tâche sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation. Suivez l’état du bot et autorisez l’utilisateur à interrompre ou annuler la séquence.

Il existe deux façons d’invoquer des modules de tâche :

* Un nouveau type de message d’appel : l’utilisation de l’action de carte pour les cartes Bot Framework ou de l’action de carte pour les cartes adaptatives, avec un module de tâche, une URL ou une carte adaptative, est récupérée dynamiquement à partir de votre `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` bot.
* URL de lien profond : à l’aide de la syntaxe de lien profond pour les [modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)de tâche, vous pouvez utiliser l’action de carte pour les cartes Bot Framework ou l’action de carte pour les cartes adaptatives, `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) respectivement. Avec les URL de lien profond, l’URL du module de tâche ou le corps de la carte adaptative est déjà connu pour éviter un aller-retour serveur par rapport à `task/fetch` .

> [!IMPORTANT]
> Chacun `url` `fallbackUrl` d’eux doit implémenter le protocole de chiffrement HTTPS.

La section suivante fournit des détails sur l’appel d’un module de tâche à `task/fetch` l’aide.

## <a name="invoke-a-task-module-using-taskfetch"></a>Appeler un module de tâche à l’aide de la tâche/extraction

Lorsque `value` l’objet de l’action de carte ou est initialisé et lorsqu’un utilisateur sélectionne le bouton, un message est `invoke` `Action.Submit` envoyé au `invoke` bot. Dans la réponse HTTP au message, il existe un objet TaskInfo incorporé dans un objet wrapper, que Teams utilise pour afficher `invoke` le module de tâche. [](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)

![demande ou réponse de tâche/extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

Les étapes suivantes fournissent le module d’appel de tâche à l’aide de la tâche/extraction :

1. Cette image montre une carte Hero Bot Framework avec une action **acheter** `invoke` [une carte.](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) La valeur de `type` la propriété est et le reste de `task/fetch` l’objet `value` peut être de votre choix.
1. Le bot reçoit le `invoke` message HTTP POST.
1. Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200. Pour plus d’informations sur le schéma des réponses, voir [la discussion sur la tâche/envoyer.](#the-flexibility-of-tasksubmit) Le code suivant fournit un exemple de corps de la réponse HTTP qui contient un objet [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incorporé dans un objet wrapper :

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

    `task/fetch`L’événement et sa réponse pour les bots sont similaires à la fonction dans le `microsoftTeams.tasks.startTask()` SDK client.

1. Microsoft Teams affiche le module de tâche.

La section suivante fournit des détails sur l’envoi du résultat d’un module de tâche.

## <a name="submit-the-result-of-a-task-module"></a>Envoyer le résultat d’un module de tâche

Lorsque l’utilisateur a terminé le module de tâche, la soumission du résultat au bot est similaire à la façon dont il fonctionne avec les onglets. Pour plus d’informations, [voir l’exemple d’envoi du résultat d’un module de tâche.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module) Il existe quelques différences comme suit :

* HTML ou JavaScript c’est-à-dire : une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK appelée ci-après comme à des fins de `TaskInfo.url` `microsoftTeams.tasks.submitTask()` `submitTask()` lisibilité. Vous pouvez appeler sans paramètre si vous souhaitez Teams le module de tâche, mais vous devez transmettre un objet ou une `submitTask()` chaîne à votre `submitHandler` . Passez-le en tant que premier paramètre, `result` . Teams appelle , `submitHandler` `err` est `null` et est `result` l’objet ou la chaîne que vous avez transmis à `submitTask()` . Si vous `submitTask()` appelez avec `result` un paramètre, vous devez transmettre un ou `appId` plusieurs tableaux de `appId` chaînes. Cela permet Teams vérifier que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâche. Votre bot reçoit un `task/submit` message incluant `result` . Pour plus d’informations, [voir la charge utile des `task/fetch` `task/submit` messages.](#payload-of-taskfetch-and-tasksubmit-messages)
* Carte adaptative : le corps de la carte adaptative tel qu’il est rempli par l’utilisateur est envoyé au bot par le biais d’un message lorsque l’utilisateur `TaskInfo.card` `task/submit` sélectionne un `Action.Submit` bouton.

La section suivante fournit des détails sur la flexibilité de `task/submit` .

## <a name="the-flexibility-of-tasksubmit"></a>Flexibilité de la tâche/de l’soumission

Lorsque l’utilisateur termine avec un module de tâche appelé à partir d’un bot, le bot reçoit toujours un `task/submit invoke` message. Plusieurs options s’offrent à vous pour répondre `task/submit` au message comme suit :

| Réponse du corps HTTP                      | Scénario                                |
| --------------------------------------- | --------------------------------------- |
| Aucun ne ignore le `task/submit` message | La réponse la plus simple n’est pas du tout une réponse. Votre bot n’est pas tenu de répondre lorsque l’utilisateur a terminé avec le module de tâche. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams affiche la valeur d’un message dans `value` une boîte de message. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Vous permet de chaîner des séquences de cartes adaptatives ensemble dans un Assistant ou une expérience en plusieurs étapes. |

> [!NOTE]
> Le chaînage de cartes adaptatives dans une séquence est un scénario avancé. L'Node.js exemple d’application le prend en charge. Pour plus d’informations, [voir Microsoft Teams module de tâche Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).

La section suivante fournit des détails sur la charge utile `task/fetch` et les `task/submit` messages.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Charge utile des messages de tâche/d’extraction et de tâche/d’soumission

Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit un `task/fetch` objet `task/submit` Bot `Activity` Framework. Le tableau suivant fournit les propriétés de la charge utile `task/fetch` et des `task/submit` messages :

| Propriété | Description                          |
| -------- | ------------------------------------ |
| `type`   | Est toujours `invoke` .           |
| `name`   | Est soit `task/fetch` `task/submit` ou . |
| `value`  | Est la charge utile définie par le développeur. La structure de `value` l’objet est la même que ce qui est envoyé à partir Teams. Dans ce cas, toutefois, il est différent. Elle nécessite la prise en charge de l’extraction dynamique à partir de Bot Framework, c’est-à-dire les actions de carte `task/fetch` `value` `Action.Submit` adaptative, autrement dit. `data` Un moyen de communiquer Teams au bot est nécessaire en plus de ce `context` qui est inclus dans ou `value` `data` .<br/><br/>Combinez « value » et « data » dans un objet parent :<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

La section suivante fournit un exemple de réception et de réponse à des messages dans `task/fetch` `task/submit` Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Exemple de messages d’appel de tâche/extraction et de tâche/d'Node.js et C #

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Actions de carte Bot Framework et actions Action de carte adaptative.Submit

Le schéma des actions de carte Bot Framework est différent des actions de carte adaptative et la façon d’appeler des modules de `Action.Submit` tâche est également différente. `data`L’objet dans contient un objet afin `Action.Submit` `msteams` qu’il n’interfère pas avec les autres propriétés de la carte. Le tableau suivant présente un exemple de chaque action de carte :

| Action de carte Bot Framework                              | Action Action.Submit de carte adaptative                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples de module de tâche bots-V4 | Exemples de création de modules de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>Voir aussi

* [Microsoft Teams exemple de code de module de tâche dans Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
