---
title: Utiliser des modules de tâches dans les bots Microsoft Teams
description: Comment utiliser des modules de tâches avec des bots Microsoft Teams, notamment des cartes Bot Framework, des cartes adaptatives et des liens profonds.
ms.localizationpriority: high
ms.topic: how-to
keywords: modules de tâche teams bots liens profonds carte adaptative
ms.openlocfilehash: 1074eee616ca7a5d78a071fb42c23d0010a8300d
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111331"
---
# <a name="use-task-modules-from-bots"></a>Utiliser des modules de tâches à partir de bots

Les modules de tâches peuvent être appelés à partir de bots Microsoft Teams à l’aide de boutons sur Cartes adaptatives et Bot Framework cartes qui sont des bannières, des miniatures et un connecteur Office 365. Les modules de tâche sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation. Effectuez le suivi de l’état du bot et autorisez l’utilisateur à interrompre ou annuler la séquence.

Il existe deux façons d’appeler des modules de tâche :

* Un nouveau type de message d'invocation `task/fetch`: en utilisant  `invoke`l'action de carte[ ](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) pour les cartes Bot Framework, ou `Action.Submit`  l'action de carte[ ](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) pour les cartes Adaptive, avec `task/fetch`, le module de tâche, soit une URL, soit une carte Adaptive, est récupéré dynamiquement par votre robot.
* URL de liens profonds : En utilisant la [syntaxe de lien profond pour les modules de tâches](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), vous pouvez utiliser `openUrl`l'action de carte[ ](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) pour les cartes Bot Framework ou `Action.OpenUrl`l'action de carte[ ](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) pour les cartes adaptatives, respectivement. Avec les URL de liens profonds, l’URL du module de tâche ou le corps de la carte adaptative est déjà connu pour éviter un aller-retour serveur par rapport à `task/fetch`.

> [!IMPORTANT]
> Chaque `url` et `fallbackUrl` doit implémenter le protocole de chiffrement HTTPS.

La section suivante fournit des détails sur l’appel d’un module de tâche à l’aide de `task/fetch`.

## <a name="invoke-a-task-module-using-taskfetch"></a>Appeler un module de tâche à l’aide de la tâche/récupération

Lorsque l’objet `value` de l’action de carte `invoke` ou `Action.Submit` est initialisé et lorsqu’un utilisateur sélectionne le bouton, un message `invoke` est envoyé au bot. Dans la réponse HTTP au message `invoke`, il y a un [objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incorporé dans un objet wrapper, que Teams utilise pour afficher le module de tâche.

 :::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="requête ou réponse à une tâche/récupération":::

Les étapes suivantes fournissent le module de tâche d’appel à l’aide de la tâche/récupération :

1. Cette image montre une carte Bot Framework hero avec une action **Acheter**`invoke`[carte](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke). La valeur de la propriété `type` est `task/fetch` et le reste de l’objet `value` peut être de votre choix.
1. Le bot reçoit le message HTTP POST `invoke` HTTP POST.
1. Le bot crée un objet de réponse et le retourne dans le corps de la réponse POST avec un code de réponse HTTP 200. Pour plus d’informations sur le schéma des réponses, consultez [la discussion sur la tâche/envoyer](#the-flexibility-of-tasksubmit). Le code suivant fournit un exemple de corps de la réponse HTTP qui contient un objet [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incorporé dans un objet wrapper :

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

    L’événement `task/fetch` et sa réponse pour les bots est similaire à la fonction `microsoftTeams.tasks.startTask()` dans le SDK client.

1. Microsoft Teams affiche le module de tâche.

La section suivante fournit des détails sur l’envoi du résultat d’un module de tâche.

## <a name="submit-the-result-of-a-task-module"></a>Envoyer le résultat d’un module de tâche

Lorsque l’utilisateur a terminé le module de tâche, l’envoi du résultat au bot est similaire à la façon dont il fonctionne avec les onglets. Pour plus d’informations, consultez [exemple d’envoi du résultat d’un module de tâche](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module). Il existe quelques différences comme suit :

* HTML ou JavaScript `TaskInfo.url` : une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK `microsoftTeams.tasks.submitTask()` appelée ci-après `submitTask()` à des fins de lisibilité. Vous pouvez appeler `submitTask()` sans paramètres si vous souhaitez que Teams ferme le module de tâche, mais vous devez passer un objet ou une chaîne à votre `submitHandler`. Transmettez-le comme premier paramètre, `result`. Teams appelle `submitHandler`, `err` est `null` et `result` est l’objet ou la chaîne que vous avez passé à `submitTask()`. Si vous appelez `submitTask()` avec un paramètre `result`, vous devez passer un `appId` ou un tableau de chaînes `appId`. Cela permet à Teams de vérifier que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâche. Votre bot reçoit un message `task/submit` incluant `result`. Pour plus d'informations, voir la rubrique [charge utile de`task/fetch` et `task/submit`messages](#payload-of-taskfetch-and-tasksubmit-messages).
* Carte adaptative qui est `TaskInfo.card`: le corps de la carte adaptative tel que rempli par l’utilisateur est envoyé au bot via un message `task/submit` lorsque l’utilisateur sélectionne un bouton `Action.Submit`.

La section suivante fournit des détails sur la flexibilité de `task/submit`.

## <a name="the-flexibility-of-tasksubmit"></a>Flexibilité de la tâche/de l’envoi

Lorsque l’utilisateur termine avec un module de tâche appelé à partir d’un bot, le bot reçoit toujours un message `task/submit invoke`. Vous avez plusieurs options pour répondre au message `task/submit` comme suit :

| Réponse du corps HTTP                      | Scénario                                |
| --------------------------------------- | --------------------------------------- |
| Aucun n’ignore le message `task/submit` | La réponse la plus simple n’est pas du tout une réponse. Votre bot n’est pas obligé de répondre lorsque l’utilisateur a terminé le module de tâche. |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams affiche la valeur de `value` dans une boîte de message contextuelle. |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | Vous permet de chaîner des séquences de Cartes adaptatives dans un Assistant ou une expérience en plusieurs étapes. |

> [!NOTE]
> Le chaînage Cartes adaptatives dans une séquence est un scénario avancé. L’exemple d’application Node.js la prend en charge. Pour plus d’informations, consultez [module de tâches Microsoft Teams Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).

La section suivante fournit des détails sur la charge utile des messages `task/fetch` et `task/submit`.

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>Charge utile des messages de tâche/récupération et de tâche/envoi

Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit un objet `task/fetch` ou `task/submit` Bot Framework `Activity`. Le tableau suivant fournit les propriétés de la charge utile des messages `task/fetch` et `task/submit` :

| Propriété | Description                          |
| -------- | ------------------------------------ |
| `type`   | Est toujours `invoke`.           |
| `name`   | Est `task/fetch` ou `task/submit`. |
| `value`  | Charge utile définie par le développeur. La structure de l’objet `value` est identique à celle envoyée à partir de Teams. Dans ce cas, toutefois, il est différent. Elle nécessite la prise en charge de la récupération dynamique `task/fetch` des deux Bot Framework, qui est `value` et `Action.Submit` actions, qui est `data`. Un moyen de communiquer teams `context` au bot est requis en plus de ce qui est inclus dans `value` ou `data`.<br/><br/>Combinez 'value' et 'data' dans un objet parent :<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

La section suivante fournit un exemple de réception et de réponse à `task/fetch` et `task/submit` appeler des messages dans Node.js.

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Exemple de tâche/récupération et de messages d’appel de tâche/envoi dans Node.js et C #

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>actions de carte Bot Framework et action de carte adaptative.Envoyer des actions

Le schéma des actions de carte Bot Framework est différent des actions `Action.Submit` et la façon d’appeler des modules de tâches est également différente. L’objet `data` dans `Action.Submit` contient un objet `msteams` afin qu’il n’interfère pas avec d’autres propriétés de la carte. Le tableau suivant montre un exemple de chaque action de carte :

| action de carte Bot Framework                              | Action de carte adaptative.Envoyer l’action                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples de module de tâches bots-V4 | Exemples de création de modules de tâches |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas ](../../sbs-botbuilder-taskmodule.yml) pour créer et récupérer un bot de module de tâche dans Teams.

## <a name="see-also"></a>Voir aussi

* [code d’exemple de module de tâche Microsoft Teams dans Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
