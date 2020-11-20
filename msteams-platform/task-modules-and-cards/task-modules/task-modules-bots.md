---
title: Utilisation des modules de tâches dans les robots Microsoft teams
description: Utilisation des modules de tâches avec les robots Microsoft Teams, y compris les cartes de l’infrastructure bot, des cartes adaptatives et des liens approfondis.
keywords: modules de tâches bots de teams
ms.openlocfilehash: 1400fec0ef86448f8632018c7675999b6b1881a0
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346720"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="6623a-104">Utilisation des modules de tâches dans les robots Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="6623a-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="6623a-105">Les modules de tâches peuvent être appelés à partir de robots Microsoft teams à l’aide de boutons sur les cartes adaptatives et les cartes de l’infrastructure bot (connecteur héros, miniature et Office 365).</span><span class="sxs-lookup"><span data-stu-id="6623a-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="6623a-106">Les modules de tâches sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation dans lesquelles vous êtes un développeur pour effectuer le suivi de l’état du bot et permettre à l’utilisateur d’interrompre/annuler la séquence.</span><span class="sxs-lookup"><span data-stu-id="6623a-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="6623a-107">Il existe deux façons d’appeler des modules de tâches :</span><span class="sxs-lookup"><span data-stu-id="6623a-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="6623a-108">**Nouveau type de message d’appel `task/fetch` .**</span><span class="sxs-lookup"><span data-stu-id="6623a-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="6623a-109">À l’aide de l' `invoke` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#invoke) pour les fiches de l’infrastructure bot ou de l' `Action.Submit` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) adaptative, avec `task/fetch` , le module de tâches (une URL ou une carte adaptative) est extrait dynamiquement à partir de votre bot.</span><span class="sxs-lookup"><span data-stu-id="6623a-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="6623a-110">**URL de liens détaillés.**</span><span class="sxs-lookup"><span data-stu-id="6623a-110">**Deep link URLs.**</span></span> <span data-ttu-id="6623a-111">À l’aide de la [syntaxe de liens détaillés pour les modules de tâches](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), vous pouvez utiliser l' `openUrl` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#openurl) pour les cartes de l’infrastructure de robots ou l' `Action.OpenUrl` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) pour les cartes adaptatives, respectivement.</span><span class="sxs-lookup"><span data-stu-id="6623a-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="6623a-112">Avec des URL de liens détaillés, l’URL du module de tâche ou le corps de la carte adaptative est évidemment connu à l’avance, ce qui évite d’effectuer un aller-retour de serveur par rapport à `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="6623a-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6623a-113">Pour garantir des communications sécurisées, chaque `url` et `fallbackUrl` doit implémenter le protocole de CHIFFREment HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6623a-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="6623a-114">Appel d’un module de tâches via Task/Fetch</span><span class="sxs-lookup"><span data-stu-id="6623a-114">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="6623a-115">Lorsque l' `value` objet de l' `invoke` action de carte ou `Action.Submit` est initialisé de façon appropriée (expliqué en détail ci-dessous), lorsqu’un utilisateur appuie sur le bouton, un `invoke` message est envoyé au bot.</span><span class="sxs-lookup"><span data-stu-id="6623a-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="6623a-116">Dans la réponse HTTP au `invoke` message, un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) est incorporé dans un objet de wrapper, que teams utilise pour afficher le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6623a-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![demande/réponse de la tâche/de l’extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="6623a-118">Examinons chaque étape plus en détail :</span><span class="sxs-lookup"><span data-stu-id="6623a-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="6623a-119">Cet exemple illustre une carte héros de bot avec une action de carte « acheter » `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span><span class="sxs-lookup"><span data-stu-id="6623a-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="6623a-120">La valeur de la `type` propriété est `task/fetch` : le reste de l' `value` objet peut être ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6623a-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="6623a-121">Le bot reçoit le `invoke` message http post.</span><span class="sxs-lookup"><span data-stu-id="6623a-121">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="6623a-122">Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="6623a-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="6623a-123">Le schéma des réponses est décrit [ci-dessous dans la discussion sur tâche/envoi](#the-flexibility-of-tasksubmit), mais il est important de se rappeler que le corps de la réponse http contient un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incorporé dans un objet de wrapper, par exemple :</span><span class="sxs-lookup"><span data-stu-id="6623a-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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

    <span data-ttu-id="6623a-124">L' `task/fetch` événement et sa réponse pour les robots sont similaires, d’un plan conceptuel, à la `microsoftTeams.tasks.startTask()` fonction dans le kit de développement logiciel client.</span><span class="sxs-lookup"><span data-stu-id="6623a-124">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="6623a-125">Microsoft teams affiche le module tâches.</span><span class="sxs-lookup"><span data-stu-id="6623a-125">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="6623a-126">Envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="6623a-126">Submitting the result of a task module</span></span>

<span data-ttu-id="6623a-127">Une fois que l’utilisateur a terminé d’utiliser le module de tâches, le fait de renvoyer le résultat au robot est similaire à celui de la [façon dont il fonctionne avec les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), mais il existe quelques différences, il est également décrit ici.</span><span class="sxs-lookup"><span data-stu-id="6623a-127">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="6623a-128">**HTML/JavaScript ( `TaskInfo.url` )**.</span><span class="sxs-lookup"><span data-stu-id="6623a-128">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="6623a-129">Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la `microsoftTeams.tasks.submitTask()` fonction SDK (désignée ci-dessous à des `submitTask()` fins de lisibilité).</span><span class="sxs-lookup"><span data-stu-id="6623a-129">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="6623a-130">Vous pouvez appeler `submitTask()` sans aucun paramètre si vous souhaitez simplement que teams ferme le module de tâches, mais la plupart du temps, vous souhaiterez passer un objet ou une chaîne à votre `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="6623a-130">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="6623a-131">Il suffit de la transmettre en tant que premier paramètre, `result` .</span><span class="sxs-lookup"><span data-stu-id="6623a-131">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="6623a-132">Teams appellera `submitHandler` : `err` sera `null` et sera `result` l’objet/la chaîne que vous avez transmis `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="6623a-132">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="6623a-133">Si vous appelez `submitTask()` avec un `result` paramètre, vous **devez** transmettre un `appId` tableau de chaînes ou un tableau `appId` : cela permet à teams de valider le fait que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6623a-133">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="6623a-134">Votre bot recevra un `task/submit` message, `result` comme décrit [ci-dessous](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="6623a-134">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="6623a-135">**Carte adaptative ( `TaskInfo.card` )**.</span><span class="sxs-lookup"><span data-stu-id="6623a-135">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="6623a-136">Le corps de la carte adaptative (tel qu’il est rempli par l’utilisateur) est envoyé au robot via un `task/submit` message lorsque l’utilisateur appuie sur n’importe quel `Action.Submit` bouton.</span><span class="sxs-lookup"><span data-stu-id="6623a-136">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="6623a-137">Flexibilité de la tâche/de l’envoi</span><span class="sxs-lookup"><span data-stu-id="6623a-137">The flexibility of task/submit</span></span>

<span data-ttu-id="6623a-138">Dans la section précédente, vous avez appris que lorsque l’utilisateur a terminé avec un module de tâche appelé à partir d’un bot, le bot reçoit toujours un `task/submit invoke` message.</span><span class="sxs-lookup"><span data-stu-id="6623a-138">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="6623a-139">En tant que développeur, plusieurs options s’offrent à vous lorsque vous *répondez* au `task/submit` message :</span><span class="sxs-lookup"><span data-stu-id="6623a-139">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="6623a-140">Réponse du corps HTTP</span><span class="sxs-lookup"><span data-stu-id="6623a-140">HTTP Body Response</span></span>                      | <span data-ttu-id="6623a-141">Scénario</span><span class="sxs-lookup"><span data-stu-id="6623a-141">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="6623a-142">Aucun (ignorer le `task/submit` message)</span><span class="sxs-lookup"><span data-stu-id="6623a-142">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="6623a-143">La réponse la plus simple n’est pas du tout.</span><span class="sxs-lookup"><span data-stu-id="6623a-143">The simplest response is no response at all.</span></span> <span data-ttu-id="6623a-144">Votre robot n’est pas tenu de répondre lorsque l’utilisateur a terminé le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="6623a-144">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="6623a-145">Teams affichera la valeur de `value` dans une boîte de message contextuel.</span><span class="sxs-lookup"><span data-stu-id="6623a-145">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="6623a-146">Vous permet de « chaîner » les séquences de cartes adaptatives dans un Assistant/une expérience en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="6623a-146">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="6623a-147">_Notez que le chaînage de cartes adaptatives dans une séquence est un scénario avancé et n’est pas documenté ici. Toutefois, l’exemple d’application Node.js prend en charge cette méthode, mais elle est documentée dans [le fichier Readme.MD](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span><span class="sxs-lookup"><span data-stu-id="6623a-147">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="6623a-148">Charge utile des tâches/de l’extraction et des messages de tâches/d’envoi</span><span class="sxs-lookup"><span data-stu-id="6623a-148">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="6623a-149">Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit `task/fetch` un `task/submit` objet infrastructure de bot ou `Activity` .</span><span class="sxs-lookup"><span data-stu-id="6623a-149">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="6623a-150">Le niveau le plus élevé s’affiche ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6623a-150">The important top-level appear below:</span></span>

| <span data-ttu-id="6623a-151">Propriété</span><span class="sxs-lookup"><span data-stu-id="6623a-151">Property</span></span> | <span data-ttu-id="6623a-152">Description</span><span class="sxs-lookup"><span data-stu-id="6623a-152">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="6623a-153">Sera toujours `invoke`</span><span class="sxs-lookup"><span data-stu-id="6623a-153">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="6623a-154">Soit `task/fetch` ou `task/submit`</span><span class="sxs-lookup"><span data-stu-id="6623a-154">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="6623a-155">Charge utile définie par le développeur.</span><span class="sxs-lookup"><span data-stu-id="6623a-155">The developer-defined payload.</span></span> <span data-ttu-id="6623a-156">En règle générale, la structure de l' `value` objet reflète ce qui a été envoyé par Teams.</span><span class="sxs-lookup"><span data-stu-id="6623a-156">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="6623a-157">Dans ce cas, toutefois, il est différent, car nous souhaitons prendre en charge l’extraction dynamique ( `task/fetch` ) à la fois de l’infrastructure bot ( `value` ) et des actions de carte adaptative `Action.Submit` ( `data` ), et nous avons besoin d’un moyen de communiquer teams `context` au robot en plus de ce qui a été inclus dans `value` / `data` .</span><span class="sxs-lookup"><span data-stu-id="6623a-157">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="6623a-158">Pour ce faire, nous combinons les deux dans un objet parent :</span><span class="sxs-lookup"><span data-stu-id="6623a-158">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="6623a-159">Exemple : réception et réponse aux messages d’appel des tâches/extraction et tâches/envoi-Node.js</span><span class="sxs-lookup"><span data-stu-id="6623a-159">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="6623a-160">L’exemple de code ci-dessous a été modifié entre la version d’évaluation technique et la version finale de cette fonctionnalité : le schéma de la demande a été `task/fetch` modifié pour suivre ce qui a été [documenté dans la section précédente](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="6623a-160">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="6623a-161">Autrement dit, la documentation était correcte, mais l’implémentation ne l’était pas.</span><span class="sxs-lookup"><span data-stu-id="6623a-161">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="6623a-162">Consultez les `// for Technical Preview [...]` commentaires ci-dessous pour en savoir plus sur ce qui a changé.</span><span class="sxs-lookup"><span data-stu-id="6623a-162">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
```
## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="6623a-163">Exemple : réception et réponse aux messages d’appel des tâches/extraction et tâches/envoi-C #</span><span class="sxs-lookup"><span data-stu-id="6623a-163">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="6623a-164">Dans les robots C#, `invoke` les messages sont traités par un `HttpResponseMessage()` contrôleur traitant un `Activity` message.</span><span class="sxs-lookup"><span data-stu-id="6623a-164">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="6623a-165">Les `task/fetch` `task/submit` requêtes et réponses sont au format JSON.</span><span class="sxs-lookup"><span data-stu-id="6623a-165">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="6623a-166">En C#, il n’est pas aussi commode de traiter le JSON brut en Node.js, donc vous avez besoin de classes wrapper pour gérer la sérialisation vers et à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="6623a-166">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="6623a-167">Il n’existe pas encore de prise en charge directe de cette fonction dans le [Kit de développement logiciel (SDK) c#](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) de Microsoft Teams, mais vous pouvez voir un exemple de ce à quoi ressembleront ces classes wrapper simples dans l' [exemple d’application c#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span><span class="sxs-lookup"><span data-stu-id="6623a-167">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="6623a-168">Vous trouverez ci-dessous un exemple de code en C# pour `task/fetch` la gestion et les `task/submit` messages qui utilisent ces classes wrapper ( `TaskInfo` , `TaskEnvelope` ), extraits de l' [exemple](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span><span class="sxs-lookup"><span data-stu-id="6623a-168">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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
```
## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---python"></a><span data-ttu-id="6623a-169">Exemple : réception et réponse aux messages d’appel des tâches/extraction et tâches/envoi-python</span><span class="sxs-lookup"><span data-stu-id="6623a-169">Example: Receiving and responding to task/fetch and task/submit invoke messages - Python</span></span>
```
async def on_teams_task_module_fetch(
        self, turn_context: TurnContext, task_module_request: TaskModuleRequest
    ) -> TaskModuleResponse:
        """
        Called when the user selects an options from the displayed HeroCard or
        AdaptiveCard.  The result is the action to perform.
        """

        card_task_fetch_value = task_module_request.data["data"]

        task_info = TaskModuleTaskInfo()
        if card_task_fetch_value == TaskModuleIds.YOUTUBE:
            # Display the YouTube.html page
            task_info.url = task_info.fallback_url = (
                self.__base_url + "/" + TaskModuleIds.YOUTUBE + ".html"
            )
            TeamsTaskModuleBot.__set_task_info(task_info, TaskModuleUIConstants.YOUTUBE)
        elif card_task_fetch_value == TaskModuleIds.CUSTOM_FORM:
            # Display the CustomForm.html page, and post the form data back via
            # on_teams_task_module_submit.
            task_info.url = task_info.fallback_url = (
                self.__base_url + "/" + TaskModuleIds.CUSTOM_FORM + ".html"
            )
            TeamsTaskModuleBot.__set_task_info(
                task_info, TaskModuleUIConstants.CUSTOM_FORM
            )
        elif card_task_fetch_value == TaskModuleIds.ADAPTIVE_CARD:
            # Display an AdaptiveCard to prompt user for text, and post it back via
            # on_teams_task_module_submit.
            task_info.card = TeamsTaskModuleBot.__create_adaptive_card_attachment()
            TeamsTaskModuleBot.__set_task_info(
                task_info, TaskModuleUIConstants.ADAPTIVE_CARD
            )

        return TaskModuleResponseFactory.to_task_module_response(task_info)

    async def on_teams_task_module_submit(
        self, turn_context: TurnContext, task_module_request: TaskModuleRequest
    ) -> TaskModuleResponse:
        """
        Called when data is being returned from the selected option (see `on_teams_task_module_fetch').
        """

        # Echo the users input back.  In a production bot, this is where you'd add behavior in
        # response to the input.
        await turn_context.send_activity(
            MessageFactory.text(
                f"on_teams_task_module_submit: {json.dumps(task_module_request.data)}"
            )
        )

        message_response = TaskModuleMessageResponse(value="Thanks!")
        return TaskModuleResponse(task=message_response)

Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case. Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).
```
### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="6623a-170">Actions de carte d’infrastructure bot et action de carte adaptative. soumettre des actions</span><span class="sxs-lookup"><span data-stu-id="6623a-170">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="6623a-171">Le schéma des actions de carte de l’infrastructure de robots est légèrement différent des actions de carte adaptative `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="6623a-171">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="6623a-172">Par conséquent, le mode d’appel des modules de tâches est légèrement différent : l' `data` objet dans `Action.Submit` contient un `msteams` objet de sorte qu’il ne gêne pas les autres propriétés de la carte.</span><span class="sxs-lookup"><span data-stu-id="6623a-172">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="6623a-173">Le tableau suivant montre un exemple de chacun :</span><span class="sxs-lookup"><span data-stu-id="6623a-173">The following table shows an example of each:</span></span>

| <span data-ttu-id="6623a-174">Action de carte de l’infrastructure bot</span><span class="sxs-lookup"><span data-stu-id="6623a-174">Bot Framework card action</span></span>                              | <span data-ttu-id="6623a-175">Action de carte adaptative. action d’envoi</span><span class="sxs-lookup"><span data-stu-id="6623a-175">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
