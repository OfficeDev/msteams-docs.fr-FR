---
title: Utilisation des modules de tâches dans les robots Microsoft teams
description: Utilisation des modules de tâches avec les robots Microsoft Teams, y compris les cartes de l’infrastructure bot, des cartes adaptatives et des liens approfondis.
keywords: modules de tâches bots de teams
ms.openlocfilehash: 09b0ede85c613d5724c6ecddbccd2a59c43cad74
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228093"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="f8c99-104">Utilisation des modules de tâches dans les robots Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="f8c99-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="f8c99-105">Les modules de tâches peuvent être appelés à partir de robots Microsoft teams à l’aide de boutons sur les cartes adaptatives et les cartes de l’infrastructure bot (connecteur héros, miniature et Office 365).</span><span class="sxs-lookup"><span data-stu-id="f8c99-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="f8c99-106">Les modules de tâches sont souvent une meilleure expérience utilisateur que plusieurs étapes de conversation dans lesquelles vous êtes un développeur pour effectuer le suivi de l’état du bot et permettre à l’utilisateur d’interrompre/annuler la séquence.</span><span class="sxs-lookup"><span data-stu-id="f8c99-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="f8c99-107">Il existe deux façons d’appeler des modules de tâches :</span><span class="sxs-lookup"><span data-stu-id="f8c99-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="f8c99-108">**Nouveau type de message `task/fetch`d’appel.**</span><span class="sxs-lookup"><span data-stu-id="f8c99-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="f8c99-109">À l' `invoke` aide de l' [action de carte](~/task-modules-and-cards/cards/cards-actions.md#invoke) pour les fiches `Action.Submit` de l’infrastructure bot ou de l’action `task/fetch`de [carte](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) adaptative, avec, le module de tâches (une URL ou une carte adaptative) est extrait dynamiquement à partir de votre bot.</span><span class="sxs-lookup"><span data-stu-id="f8c99-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="f8c99-110">**URL de liens détaillés.**</span><span class="sxs-lookup"><span data-stu-id="f8c99-110">**Deep link URLs.**</span></span> <span data-ttu-id="f8c99-111">À l’aide de la [syntaxe de liens détaillés pour les modules de tâches](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), vous pouvez utiliser l' `openUrl` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#openurl) pour les cartes de l’infrastructure de robots ou l' `Action.OpenUrl` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) pour les cartes adaptatives, respectivement.</span><span class="sxs-lookup"><span data-stu-id="f8c99-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="f8c99-112">Avec des URL de liens détaillés, l’URL du module de tâche ou le corps de la carte adaptative est évidemment connu à l’avance, `task/fetch`ce qui évite d’effectuer un aller-retour de serveur par rapport à.</span><span class="sxs-lookup"><span data-stu-id="f8c99-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="f8c99-113">Appel d’un module de tâches via Task/Fetch</span><span class="sxs-lookup"><span data-stu-id="f8c99-113">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="f8c99-114">Lorsque l' `value` objet de l' `invoke` action de carte `Action.Submit` ou est initialisé de façon appropriée (expliqué en détail ci-dessous), lorsqu’un utilisateur appuie sur le bouton, `invoke` un message est envoyé au bot.</span><span class="sxs-lookup"><span data-stu-id="f8c99-114">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="f8c99-115">Dans la réponse HTTP au `invoke` message, un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) est incorporé dans un objet de wrapper, que teams utilise pour afficher le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="f8c99-115">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![demande/réponse de la tâche/de l’extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="f8c99-117">Examinons chaque étape plus en détail :</span><span class="sxs-lookup"><span data-stu-id="f8c99-117">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="f8c99-118">Cet exemple illustre une carte héros de bot avec une `invoke` [action de carte](~/task-modules-and-cards/cards/cards-actions.md#invoke)« acheter ».</span><span class="sxs-lookup"><span data-stu-id="f8c99-118">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="f8c99-119">La valeur de la `type` propriété est `task/fetch` : le reste de l' `value` objet peut être ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="f8c99-119">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="f8c99-120">Le bot reçoit le `invoke` message http post.</span><span class="sxs-lookup"><span data-stu-id="f8c99-120">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="f8c99-121">Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="f8c99-121">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="f8c99-122">Le schéma des réponses est décrit [ci-dessous dans la discussion sur tâche/envoi](#the-flexibility-of-tasksubmit), mais il est important de se rappeler que le corps de la réponse http contient un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incorporé dans un objet de wrapper, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f8c99-122">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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
    
    <span data-ttu-id="f8c99-123">L' `task/fetch` événement et sa réponse pour les robots sont similaires, d’un plan conceptuel `microsoftTeams.tasks.startTask()` , à la fonction dans le kit de développement logiciel client.</span><span class="sxs-lookup"><span data-stu-id="f8c99-123">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="f8c99-124">Microsoft teams affiche le module tâches.</span><span class="sxs-lookup"><span data-stu-id="f8c99-124">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="f8c99-125">Envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="f8c99-125">Submitting the result of a task module</span></span>

<span data-ttu-id="f8c99-126">Une fois que l’utilisateur a terminé d’utiliser le module de tâches, le fait de renvoyer le résultat au robot est similaire à celui de la [façon dont il fonctionne avec les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), mais il existe quelques différences, il est également décrit ici.</span><span class="sxs-lookup"><span data-stu-id="f8c99-126">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="f8c99-127">**HTML/JavaScript (`TaskInfo.url`)**.</span><span class="sxs-lookup"><span data-stu-id="f8c99-127">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="f8c99-128">Une fois que vous avez validé ce que l’utilisateur a entré, `microsoftTeams.tasks.submitTask()` vous appelez la fonction SDK (désignée `submitTask()` ci-dessous à des fins de lisibilité).</span><span class="sxs-lookup"><span data-stu-id="f8c99-128">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="f8c99-129">Vous pouvez appeler `submitTask()` sans aucun paramètre si vous souhaitez simplement que teams ferme le module de tâches, mais la plupart du temps, vous souhaiterez passer un objet ou une chaîne `submitHandler`à votre.</span><span class="sxs-lookup"><span data-stu-id="f8c99-129">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="f8c99-130">Il suffit de la transmettre en tant que `result`premier paramètre,.</span><span class="sxs-lookup"><span data-stu-id="f8c99-130">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="f8c99-131">Teams appellera `submitHandler`: `err` sera `null` et `result` sera l’objet/la chaîne que vous avez transmis `submitTask()`.</span><span class="sxs-lookup"><span data-stu-id="f8c99-131">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="f8c99-132">Si vous appelez `submitTask()` `result` avec un paramètre, vous **devez** transmettre un `appId` tableau de `appId` chaînes ou un tableau : cela permet à teams de valider le fait que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="f8c99-132">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="f8c99-133">Votre bot recevra un `task/submit` message, `result` comme décrit [ci-dessous](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="f8c99-133">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="f8c99-134">**Carte adaptative (`TaskInfo.card`)**.</span><span class="sxs-lookup"><span data-stu-id="f8c99-134">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="f8c99-135">Le corps de la carte adaptative (tel qu’il est rempli par l’utilisateur) est envoyé au robot via `task/submit` un message lorsque l’utilisateur appuie sur `Action.Submit` n’importe quel bouton.</span><span class="sxs-lookup"><span data-stu-id="f8c99-135">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="f8c99-136">Flexibilité de la tâche/de l’envoi</span><span class="sxs-lookup"><span data-stu-id="f8c99-136">The flexibility of task/submit</span></span>

<span data-ttu-id="f8c99-137">Dans la section précédente, vous avez appris que lorsque l’utilisateur a terminé avec un module de tâche appelé à partir d’un bot, le `task/submit invoke` bot reçoit toujours un message.</span><span class="sxs-lookup"><span data-stu-id="f8c99-137">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="f8c99-138">En tant que développeur, plusieurs options s’offrent à vous lorsque `task/submit` vous *répondez* au message :</span><span class="sxs-lookup"><span data-stu-id="f8c99-138">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="f8c99-139">Réponse du corps HTTP</span><span class="sxs-lookup"><span data-stu-id="f8c99-139">HTTP Body Response</span></span>                      | <span data-ttu-id="f8c99-140">Scénario</span><span class="sxs-lookup"><span data-stu-id="f8c99-140">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="f8c99-141">Aucun (ignorer le `task/submit` message)</span><span class="sxs-lookup"><span data-stu-id="f8c99-141">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="f8c99-142">La réponse la plus simple n’est pas du tout.</span><span class="sxs-lookup"><span data-stu-id="f8c99-142">The simplest response is no response at all.</span></span> <span data-ttu-id="f8c99-143">Votre robot n’est pas tenu de répondre lorsque l’utilisateur a terminé le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="f8c99-143">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="f8c99-144">Teams affichera la valeur `value` de dans une boîte de message contextuel.</span><span class="sxs-lookup"><span data-stu-id="f8c99-144">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="f8c99-145">Vous permet de « chaîner » les séquences de cartes adaptatives dans un Assistant/une expérience en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="f8c99-145">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="f8c99-146">_Notez que le chaînage de cartes adaptatives dans une séquence est un scénario avancé et n’est pas documenté ici. L’exemple d’application node. js le prend en charge, mais son fonctionnement est documenté dans [son fichier Readme.MD](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span><span class="sxs-lookup"><span data-stu-id="f8c99-146">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="f8c99-147">Charge utile des tâches/de l’extraction et des messages de tâches/d’envoi</span><span class="sxs-lookup"><span data-stu-id="f8c99-147">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="f8c99-148">Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit `task/fetch` un `task/submit` objet infrastructure `Activity` de bot ou.</span><span class="sxs-lookup"><span data-stu-id="f8c99-148">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="f8c99-149">Le niveau le plus élevé s’affiche ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f8c99-149">The important top-level appear below:</span></span>

| <span data-ttu-id="f8c99-150">Propriété</span><span class="sxs-lookup"><span data-stu-id="f8c99-150">Property</span></span> | <span data-ttu-id="f8c99-151">Description</span><span class="sxs-lookup"><span data-stu-id="f8c99-151">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="f8c99-152">Sera toujours`invoke`</span><span class="sxs-lookup"><span data-stu-id="f8c99-152">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="f8c99-153">Soit `task/fetch` ou`task/submit`</span><span class="sxs-lookup"><span data-stu-id="f8c99-153">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="f8c99-154">Charge utile définie par le développeur.</span><span class="sxs-lookup"><span data-stu-id="f8c99-154">The developer-defined payload.</span></span> <span data-ttu-id="f8c99-155">En règle générale, la `value` structure de l’objet reflète ce qui a été envoyé par Teams.</span><span class="sxs-lookup"><span data-stu-id="f8c99-155">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="f8c99-156">Dans ce cas, toutefois, il est différent, car nous souhaitons prendre en charge l'`task/fetch`extraction dynamique () à la`value`fois de l’infrastructure bot `Action.Submit` ()`data`et des actions de carte adaptative (), et `context` nous avons besoin d’un moyen de communiquer teams `value` / `data`au robot en plus de ce qui a été inclus dans.</span><span class="sxs-lookup"><span data-stu-id="f8c99-156">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="f8c99-157">Pour ce faire, nous combinons les deux dans un objet parent :</span><span class="sxs-lookup"><span data-stu-id="f8c99-157">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="f8c99-158">Exemple : réception et réponse aux messages d’appel des tâches/extractions et tâches/envoi-node. js</span><span class="sxs-lookup"><span data-stu-id="f8c99-158">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="f8c99-159">L’exemple de code ci-dessous a été modifié entre la version d’évaluation technique et la version finale `task/fetch` de cette fonctionnalité : le schéma de la demande a été modifié pour suivre ce qui a été [documenté dans la section précédente](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="f8c99-159">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="f8c99-160">Autrement dit, la documentation était correcte, mais l’implémentation ne l’était pas.</span><span class="sxs-lookup"><span data-stu-id="f8c99-160">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="f8c99-161">Consultez les `// for Technical Preview [...]` commentaires ci-dessous pour en savoir plus sur ce qui a changé.</span><span class="sxs-lookup"><span data-stu-id="f8c99-161">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

<span data-ttu-id="f8c99-162">*Voir aussi*l' [exemple de code du module de tâches de Microsoft Teams (NodeJS](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) et [robots](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="f8c99-162">*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="f8c99-163">Exemple : réception et réponse aux messages d’appel des tâches/extraction et tâches/envoi-C #</span><span class="sxs-lookup"><span data-stu-id="f8c99-163">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="f8c99-164">Dans les robots C# `invoke` , les messages sont traités `HttpResponseMessage()` par un contrôleur `Activity` traitant un message.</span><span class="sxs-lookup"><span data-stu-id="f8c99-164">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="f8c99-165">Les `task/fetch` `task/submit` requêtes et réponses sont au format JSON.</span><span class="sxs-lookup"><span data-stu-id="f8c99-165">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="f8c99-166">En C#, il n’est pas aussi commode de traiter le JSON brut comme dans node. js que si vous avez besoin de classes wrapper pour gérer la sérialisation vers et à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="f8c99-166">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="f8c99-167">Il n’existe pas encore de prise en charge directe de cette fonction dans le [Kit de développement logiciel (SDK) c#](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) de Microsoft Teams, mais vous pouvez voir un exemple de ce à quoi ressembleront ces classes wrapper simples dans l' [exemple d’application c#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span><span class="sxs-lookup"><span data-stu-id="f8c99-167">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="f8c99-168">Vous trouverez ci-dessous un exemple de `task/fetch` code `task/submit` en C# pour la gestion et`TaskInfo`les `TaskEnvelope`messages qui utilisent ces classes wrapper (,), extraits de l' [exemple](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span><span class="sxs-lookup"><span data-stu-id="f8c99-168">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="f8c99-169">L’exemple ci-dessus ne montre pas `SetTaskInfo()` la fonction qui définit les `height`propriétés `width`, et `title` de l' `TaskInfo` objet pour chaque cas.</span><span class="sxs-lookup"><span data-stu-id="f8c99-169">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="f8c99-170">Voici le [code source pour SetTaskInfo ()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span><span class="sxs-lookup"><span data-stu-id="f8c99-170">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="f8c99-171">Actions de carte d’infrastructure bot et action de carte adaptative. soumettre des actions</span><span class="sxs-lookup"><span data-stu-id="f8c99-171">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="f8c99-172">Le schéma des actions de carte de l’infrastructure de robots est légèrement différent `Action.Submit` des actions de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="f8c99-172">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="f8c99-173">Par conséquent, le mode d’appel des modules de tâches est légèrement différent : l' `data` objet dans `Action.Submit` contient un `msteams` objet de sorte qu’il ne gêne pas les autres propriétés de la carte.</span><span class="sxs-lookup"><span data-stu-id="f8c99-173">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="f8c99-174">Le tableau suivant montre un exemple de chacun :</span><span class="sxs-lookup"><span data-stu-id="f8c99-174">The following table shows an example of each:</span></span>

| <span data-ttu-id="f8c99-175">Action de carte de l’infrastructure bot</span><span class="sxs-lookup"><span data-stu-id="f8c99-175">Bot Framework card action</span></span>                              | <span data-ttu-id="f8c99-176">Action de carte adaptative. action d’envoi</span><span class="sxs-lookup"><span data-stu-id="f8c99-176">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
