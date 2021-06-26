---
title: Utiliser des modules de tâche dans Microsoft Teams bots
description: Utilisation des modules de tâche avec Microsoft Teams bots, y compris les cartes Bot Framework, les cartes adaptatives et les liens profonds.
localization_priority: Normal
ms.topic: how-to
keywords: bots d’équipes de modules de tâche
ms.openlocfilehash: 5d9aa2b651a4c99cee75aada62a4d1176a589d79
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140306"
---
# <a name="use-task-modules-from-bots"></a><span data-ttu-id="a31cb-104">Utiliser des modules de tâche à partir de bots</span><span class="sxs-lookup"><span data-stu-id="a31cb-104">Use task modules from bots</span></span>

<span data-ttu-id="a31cb-105">Les modules de tâche peuvent être appelés à partir de bots Microsoft Teams à l’aide de boutons sur les cartes adaptatives et les cartes Bot Framework qui sont hero, thumbnail et Office 365 Connector.</span><span class="sxs-lookup"><span data-stu-id="a31cb-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive Cards and Bot Framework cards that is hero, thumbnail, and Office 365 Connector.</span></span> <span data-ttu-id="a31cb-106">Les modules de tâche sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation.</span><span class="sxs-lookup"><span data-stu-id="a31cb-106">Task modules are often a better user experience than multiple conversation steps.</span></span> <span data-ttu-id="a31cb-107">Suivez l’état du bot et autorisez l’utilisateur à interrompre ou annuler la séquence.</span><span class="sxs-lookup"><span data-stu-id="a31cb-107">Keep track of bot state and allow the user to interrupt or cancel the sequence.</span></span>

<span data-ttu-id="a31cb-108">Il existe deux façons d’invoquer des modules de tâche :</span><span class="sxs-lookup"><span data-stu-id="a31cb-108">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="a31cb-109">Un nouveau type de message d’appel : l’utilisation de l’action de carte pour les cartes Bot Framework ou de l’action de carte pour les cartes adaptatives, avec , module de tâche, une URL ou une carte adaptative, est récupérée dynamiquement à partir de votre `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` bot.</span><span class="sxs-lookup"><span data-stu-id="a31cb-109">A new kind of invoke message `task/fetch`: Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, task module either a URL or an Adaptive Card, is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="a31cb-110">URL de lien profond : à l’aide de la syntaxe de lien profond pour les [modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)de tâche, vous pouvez utiliser l’action de carte pour les cartes Bot Framework ou l’action de carte pour les cartes adaptatives, `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) respectivement.</span><span class="sxs-lookup"><span data-stu-id="a31cb-110">Deep link URLs: Using the [deep link syntax for task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive Cards, respectively.</span></span> <span data-ttu-id="a31cb-111">Avec les URL de lien profond, l’URL du module de tâche ou le corps de la carte adaptative est déjà connu pour éviter un aller-retour serveur par rapport à `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-111">With deep link URLs, the task module URL or Adaptive Card body is already known to avoid a server round-trip relative to `task/fetch`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a31cb-112">Chacun `url` `fallbackUrl` d’eux doit implémenter le protocole de chiffrement HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a31cb-112">Each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

<span data-ttu-id="a31cb-113">La section suivante fournit des détails sur l’appel d’un module de tâche à `task/fetch` l’aide.</span><span class="sxs-lookup"><span data-stu-id="a31cb-113">The next section provides details on invoking a task module using `task/fetch`.</span></span>

## <a name="invoke-a-task-module-using-taskfetch"></a><span data-ttu-id="a31cb-114">Appeler un module de tâche à l’aide de la tâche/extraction</span><span class="sxs-lookup"><span data-stu-id="a31cb-114">Invoke a task module using task/fetch</span></span>

<span data-ttu-id="a31cb-115">Lorsque `value` l’objet de l’action de carte ou est initialisé et lorsqu’un utilisateur sélectionne le bouton, un message est `invoke` `Action.Submit` envoyé au `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="a31cb-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized and when a user selects the button, an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="a31cb-116">Dans la réponse HTTP au message, il existe un objet TaskInfo incorporé dans un objet wrapper, que Teams utilise pour afficher `invoke` le module de tâche. [](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="a31cb-116">In the HTTP response to the `invoke` message, there is a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![demande ou réponse de tâche/extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="a31cb-118">Les étapes suivantes fournissent le module d’appel de tâche à l’aide de la tâche/extraction :</span><span class="sxs-lookup"><span data-stu-id="a31cb-118">The following steps provides the invoke task module using task/fetch:</span></span>

1. <span data-ttu-id="a31cb-119">Cette image montre une carte Hero Bot Framework avec une action **acheter** `invoke` [une carte.](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)</span><span class="sxs-lookup"><span data-stu-id="a31cb-119">This image shows a Bot Framework hero card with a **Buy** `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).</span></span> <span data-ttu-id="a31cb-120">La valeur de `type` la propriété est et le reste de `task/fetch` l’objet `value` peut être de votre choix.</span><span class="sxs-lookup"><span data-stu-id="a31cb-120">The value of the `type` property is `task/fetch` and the rest of the `value` object can be of your choice.</span></span>
1. <span data-ttu-id="a31cb-121">Le bot reçoit le `invoke` message HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a31cb-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="a31cb-122">Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="a31cb-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="a31cb-123">Pour plus d’informations sur le schéma des réponses, consultez [la discussion sur la tâche/envoyer.](#the-flexibility-of-tasksubmit)</span><span class="sxs-lookup"><span data-stu-id="a31cb-123">For more information on schema for responses, see [the discussion on task/submit](#the-flexibility-of-tasksubmit).</span></span> <span data-ttu-id="a31cb-124">Le code suivant fournit un exemple de corps de la réponse HTTP qui contient un objet [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) incorporé dans un objet wrapper :</span><span class="sxs-lookup"><span data-stu-id="a31cb-124">The following code provides an example of body of the HTTP response that contains a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object:</span></span>

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

    <span data-ttu-id="a31cb-125">`task/fetch`L’événement et sa réponse pour les bots sont similaires à la fonction dans le `microsoftTeams.tasks.startTask()` SDK client.</span><span class="sxs-lookup"><span data-stu-id="a31cb-125">The `task/fetch` event and its response for bots is similar to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>

1. <span data-ttu-id="a31cb-126">Microsoft Teams affiche le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="a31cb-126">Microsoft Teams displays the task module.</span></span>

<span data-ttu-id="a31cb-127">La section suivante fournit des détails sur l’envoi du résultat d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="a31cb-127">The next section provides details on submitting the result of a task module.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="a31cb-128">Envoyer le résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="a31cb-128">Submit the result of a task module</span></span>

<span data-ttu-id="a31cb-129">Lorsque l’utilisateur a terminé le module de tâche, la soumission du résultat au bot est similaire à la façon dont il fonctionne avec les onglets.</span><span class="sxs-lookup"><span data-stu-id="a31cb-129">When the user is finished with the task module, submitting the result back to the bot is similar to the way it works with tabs.</span></span> <span data-ttu-id="a31cb-130">Pour plus d’informations, [voir l’exemple d’envoi du résultat d’un module de tâche.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)</span><span class="sxs-lookup"><span data-stu-id="a31cb-130">For more information, see [example of submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="a31cb-131">Il existe quelques différences comme suit :</span><span class="sxs-lookup"><span data-stu-id="a31cb-131">There are a few differences as follows:</span></span>

* <span data-ttu-id="a31cb-132">HTML ou JavaScript : une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK appelée ci-après comme à des fins de `TaskInfo.url` `microsoftTeams.tasks.submitTask()` `submitTask()` lisibilité.</span><span class="sxs-lookup"><span data-stu-id="a31cb-132">HTML or JavaScript that is `TaskInfo.url`: Once you have validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function referred to hereafter as `submitTask()` for readability purposes.</span></span> <span data-ttu-id="a31cb-133">Vous pouvez appeler sans paramètre si vous souhaitez Teams le module de tâche, mais vous devez transmettre un objet ou une `submitTask()` chaîne à votre `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-133">You can call `submitTask()` without any parameters if you want Teams to close the task module, but you must pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="a31cb-134">Passez-le en tant que premier paramètre, `result` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-134">Pass it as the first parameter, `result`.</span></span> <span data-ttu-id="a31cb-135">Teams appelle , `submitHandler` `err` est `null` et est `result` l’objet ou la chaîne que vous avez transmis à `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-135">Teams invokes `submitHandler`, `err` is `null`, and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="a31cb-136">Si vous `submitTask()` appelez avec `result` un paramètre, vous devez transmettre un ou `appId` plusieurs tableaux de `appId` chaînes.</span><span class="sxs-lookup"><span data-stu-id="a31cb-136">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="a31cb-137">Cela permet Teams vérifier que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="a31cb-137">This allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="a31cb-138">Votre bot reçoit un `task/submit` message incluant `result` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-138">Your bot receives a `task/submit` message including `result`.</span></span> <span data-ttu-id="a31cb-139">Pour plus d’informations, [voir la charge utile des `task/fetch` `task/submit` messages.](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="a31cb-139">For more information, see [payload of `task/fetch` and `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="a31cb-140">Carte adaptative : le corps de la carte adaptative tel qu’il est rempli par l’utilisateur est envoyé au bot par le biais d’un message lorsque l’utilisateur `TaskInfo.card` `task/submit` sélectionne un `Action.Submit` bouton.</span><span class="sxs-lookup"><span data-stu-id="a31cb-140">Adaptive Card that is `TaskInfo.card`: The Adaptive Card body as filled in by the user is sent to the bot through a `task/submit` message when the user selects any `Action.Submit` button.</span></span>

<span data-ttu-id="a31cb-141">La section suivante fournit des détails sur la flexibilité de `task/submit` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-141">The next section provides details on the flexibility of `task/submit`.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="a31cb-142">Flexibilité de la tâche/de l’soumission</span><span class="sxs-lookup"><span data-stu-id="a31cb-142">The flexibility of task/submit</span></span>

<span data-ttu-id="a31cb-143">Lorsque l’utilisateur termine avec un module de tâche appelé à partir d’un bot, le bot reçoit toujours un `task/submit invoke` message.</span><span class="sxs-lookup"><span data-stu-id="a31cb-143">When the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="a31cb-144">Plusieurs options s’offrent à vous pour répondre `task/submit` au message comme suit :</span><span class="sxs-lookup"><span data-stu-id="a31cb-144">You have several options when responding to the `task/submit` message as follows:</span></span>

| <span data-ttu-id="a31cb-145">Réponse du corps HTTP</span><span class="sxs-lookup"><span data-stu-id="a31cb-145">HTTP body response</span></span>                      | <span data-ttu-id="a31cb-146">Scénario</span><span class="sxs-lookup"><span data-stu-id="a31cb-146">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="a31cb-147">Aucun ne tient compte du `task/submit` message</span><span class="sxs-lookup"><span data-stu-id="a31cb-147">None ignore the `task/submit` message</span></span> | <span data-ttu-id="a31cb-148">La réponse la plus simple n’est pas du tout une réponse.</span><span class="sxs-lookup"><span data-stu-id="a31cb-148">The simplest response is no response at all.</span></span> <span data-ttu-id="a31cb-149">Votre bot n’est pas tenu de répondre lorsque l’utilisateur a terminé avec le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="a31cb-149">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="a31cb-150">Teams affiche la valeur d’un message dans `value` une boîte de message.</span><span class="sxs-lookup"><span data-stu-id="a31cb-150">Teams displays the value of `value` in a pop-up message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="a31cb-151">Vous permet de chaîner des séquences de cartes adaptatives ensemble dans un Assistant ou une expérience en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="a31cb-151">Allows you to chain sequences of Adaptive Cards together in a wizard or multi-step experience.</span></span> |

> [!NOTE]
> <span data-ttu-id="a31cb-152">Le chaînage de cartes adaptatives dans une séquence est un scénario avancé.</span><span class="sxs-lookup"><span data-stu-id="a31cb-152">Chaining Adaptive Cards into a sequence is an advanced scenario.</span></span> <span data-ttu-id="a31cb-153">L'Node.js exemple d’application le prend en charge.</span><span class="sxs-lookup"><span data-stu-id="a31cb-153">The Node.js sample app supports it.</span></span> <span data-ttu-id="a31cb-154">Pour plus d’informations, [voir Microsoft Teams module de tâche Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span><span class="sxs-lookup"><span data-stu-id="a31cb-154">For more information, see [Microsoft Teams task module Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span></span>

<span data-ttu-id="a31cb-155">La section suivante fournit des détails sur la charge utile `task/fetch` et les `task/submit` messages.</span><span class="sxs-lookup"><span data-stu-id="a31cb-155">The next section provides details on payload of `task/fetch` and `task/submit` messages.</span></span>

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="a31cb-156">Charge utile des messages de tâche/d’extraction et de tâche/d’soumission</span><span class="sxs-lookup"><span data-stu-id="a31cb-156">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="a31cb-157">Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit un `task/fetch` objet `task/submit` Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="a31cb-157">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="a31cb-158">Le tableau suivant fournit les propriétés de la charge utile `task/fetch` et des `task/submit` messages :</span><span class="sxs-lookup"><span data-stu-id="a31cb-158">The following table provides the properties of payload of `task/fetch` and `task/submit` messages:</span></span>

| <span data-ttu-id="a31cb-159">Propriété</span><span class="sxs-lookup"><span data-stu-id="a31cb-159">Property</span></span> | <span data-ttu-id="a31cb-160">Description</span><span class="sxs-lookup"><span data-stu-id="a31cb-160">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="a31cb-161">Est toujours `invoke` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-161">Is always `invoke`.</span></span>           |
| `name`   | <span data-ttu-id="a31cb-162">Est soit `task/fetch` `task/submit` ou .</span><span class="sxs-lookup"><span data-stu-id="a31cb-162">Is either `task/fetch` or `task/submit`.</span></span> |
| `value`  | <span data-ttu-id="a31cb-163">Est la charge utile définie par le développeur.</span><span class="sxs-lookup"><span data-stu-id="a31cb-163">Is the developer-defined payload.</span></span> <span data-ttu-id="a31cb-164">La structure de `value` l’objet est identique à ce qui est envoyé à partir Teams.</span><span class="sxs-lookup"><span data-stu-id="a31cb-164">The structure of the `value` object is the same as what is sent from Teams.</span></span> <span data-ttu-id="a31cb-165">Dans ce cas, toutefois, il est différent.</span><span class="sxs-lookup"><span data-stu-id="a31cb-165">In this case, however, it is different.</span></span> <span data-ttu-id="a31cb-166">Elle nécessite la prise en charge de l’extraction dynamique à partir de Bot Framework, c’est-à-dire les actions de carte `task/fetch` `value` `Action.Submit` adaptative, autrement dit. `data`</span><span class="sxs-lookup"><span data-stu-id="a31cb-166">It requires support for dynamic fetch that is `task/fetch` from both Bot Framework, which is `value` and Adaptive Card `Action.Submit` actions, which is `data`.</span></span> <span data-ttu-id="a31cb-167">Un moyen de communiquer Teams au bot est nécessaire en plus de ce `context` qui est inclus dans ou `value` `data` .</span><span class="sxs-lookup"><span data-stu-id="a31cb-167">A way to communicate Teams `context` to the bot is required in addition to what is included in `value` or `data`.</span></span><br/><br/><span data-ttu-id="a31cb-168">Combinez « value » et « data » dans un objet parent :</span><span class="sxs-lookup"><span data-stu-id="a31cb-168">Combine 'value' and 'data' into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

<span data-ttu-id="a31cb-169">La section suivante fournit un exemple de réception et de réponse à des messages dans `task/fetch` `task/submit` Node.js.</span><span class="sxs-lookup"><span data-stu-id="a31cb-169">The next section provides an example of receiving and responding to `task/fetch` and `task/submit` invoke messages in Node.js.</span></span>

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a><span data-ttu-id="a31cb-170">Exemple de messages d’appel de tâche/extraction et de tâche/d'Node.js et C #</span><span class="sxs-lookup"><span data-stu-id="a31cb-170">Example of task/fetch and task/submit invoke messages in Node.js and C#</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="a31cb-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="a31cb-171">Node.js</span></span>](#tab/nodejs)

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

# <a name="c"></a>[<span data-ttu-id="a31cb-172">C#</span><span class="sxs-lookup"><span data-stu-id="a31cb-172">C#</span></span>](#tab/csharp)

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="a31cb-173">Actions de carte Bot Framework et actions Action de carte adaptative.Submit</span><span class="sxs-lookup"><span data-stu-id="a31cb-173">Bot Framework card actions vs. Adaptive Card Action.Submit actions</span></span>

<span data-ttu-id="a31cb-174">Le schéma des actions de carte Bot Framework est différent des actions de carte adaptative et la façon d’appeler des modules de `Action.Submit` tâche est également différente.</span><span class="sxs-lookup"><span data-stu-id="a31cb-174">The schema for Bot Framework card actions is different from Adaptive Card `Action.Submit` actions and the way to invoke task modules is also different.</span></span> <span data-ttu-id="a31cb-175">`data`L’objet dans contient un objet afin `Action.Submit` `msteams` qu’il n’interfère pas avec les autres propriétés de la carte.</span><span class="sxs-lookup"><span data-stu-id="a31cb-175">The `data` object in `Action.Submit` contains an `msteams` object so it does not interfere with other properties in the card.</span></span> <span data-ttu-id="a31cb-176">Le tableau suivant présente un exemple de chaque action de carte :</span><span class="sxs-lookup"><span data-stu-id="a31cb-176">The following table shows an example of each card action:</span></span>

| <span data-ttu-id="a31cb-177">Action de carte Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a31cb-177">Bot Framework card action</span></span>                              | <span data-ttu-id="a31cb-178">Action Action.Submit de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="a31cb-178">Adaptive Card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a><span data-ttu-id="a31cb-179">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="a31cb-179">Code sample</span></span>

|<span data-ttu-id="a31cb-180">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="a31cb-180">Sample name</span></span> | <span data-ttu-id="a31cb-181">Description</span><span class="sxs-lookup"><span data-stu-id="a31cb-181">Description</span></span> | <span data-ttu-id="a31cb-182">.NET</span><span class="sxs-lookup"><span data-stu-id="a31cb-182">.NET</span></span> | <span data-ttu-id="a31cb-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="a31cb-183">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="a31cb-184">Exemples de module de tâche bots-V4</span><span class="sxs-lookup"><span data-stu-id="a31cb-184">Task module sample bots-V4</span></span> | <span data-ttu-id="a31cb-185">Exemples de création de modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="a31cb-185">Samples for creating task modules.</span></span> |[<span data-ttu-id="a31cb-186">View</span><span class="sxs-lookup"><span data-stu-id="a31cb-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="a31cb-187">View</span><span class="sxs-lookup"><span data-stu-id="a31cb-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a><span data-ttu-id="a31cb-188">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a31cb-188">See also</span></span>

* [<span data-ttu-id="a31cb-189">Microsoft Teams exemple de code de module de tâche dans Node.js</span><span class="sxs-lookup"><span data-stu-id="a31cb-189">Microsoft Teams task module sample code in Node.js</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [<span data-ttu-id="a31cb-190">Exemples Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a31cb-190">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
