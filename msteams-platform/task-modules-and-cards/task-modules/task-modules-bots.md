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
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="254e5-104">Utilisation de modules de tâche à partir Microsoft Teams bots</span><span class="sxs-lookup"><span data-stu-id="254e5-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="254e5-105">Les modules de tâche peuvent être appelés à partir de bots Microsoft Teams à l’aide de boutons sur les cartes adaptatives et les cartes Bot Framework (Hero, Thumbnail et Office 365 Connector).</span><span class="sxs-lookup"><span data-stu-id="254e5-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="254e5-106">Les modules de tâche offrent souvent une meilleure expérience utilisateur que les étapes de conversation multiples où, en tant que développeur, vous devez suivre l’état du bot et permettre à l’utilisateur d’interrompre/d’annuler la séquence.</span><span class="sxs-lookup"><span data-stu-id="254e5-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="254e5-107">Il existe deux façons d’invoquer des modules de tâche :</span><span class="sxs-lookup"><span data-stu-id="254e5-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="254e5-108">**Nouveau type de message `task/fetch` d’appel.**</span><span class="sxs-lookup"><span data-stu-id="254e5-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="254e5-109">L’utilisation de l’action de carte pour les cartes Bot Framework ou de l’action de carte pour les cartes adaptatives, avec , le module de tâche (une URL ou une carte adaptative) est récupéré dynamiquement à partir de `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` votre bot.</span><span class="sxs-lookup"><span data-stu-id="254e5-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="254e5-110">**URL de lien profond.**</span><span class="sxs-lookup"><span data-stu-id="254e5-110">**Deep link URLs.**</span></span> <span data-ttu-id="254e5-111">À l’aide de la syntaxe de lien profond pour les [modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)de tâche, vous pouvez utiliser l’action de carte pour les cartes Bot Framework ou l’action de carte pour les cartes `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) adaptatives, respectivement.</span><span class="sxs-lookup"><span data-stu-id="254e5-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="254e5-112">Avec les URL de lien profond, l’URL du module de tâche ou le corps de la carte adaptative est évidemment connu à l’avance, ce qui évite un aller-retour serveur par rapport à `task/fetch` .</span><span class="sxs-lookup"><span data-stu-id="254e5-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="254e5-113">Pour garantir des communications sécurisées, `url` chacune d’elles `fallbackUrl` doit implémenter le protocole de chiffrement HTTPS.</span><span class="sxs-lookup"><span data-stu-id="254e5-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-through-taskfetch"></a><span data-ttu-id="254e5-114">L’vot d’un module de tâche par le biais de la tâche/extraction</span><span class="sxs-lookup"><span data-stu-id="254e5-114">Invoking a task module through task/fetch</span></span>

<span data-ttu-id="254e5-115">Lorsque l’objet de l’action de carte ou est initialisé correctement (expliqué plus en détail ci-dessous), lorsqu’un utilisateur appuie sur le bouton, un message est envoyé `value` `invoke` au `Action.Submit` `invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="254e5-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="254e5-116">Dans la réponse HTTP au message, il existe un objet TaskInfo incorporé dans un objet wrapper, que Teams utilise pour afficher `invoke` le module de tâche. [](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="254e5-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![demande/réponse de tâche/extraction](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="254e5-118">Examinons chaque étape plus en détail :</span><span class="sxs-lookup"><span data-stu-id="254e5-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="254e5-119">Cet exemple montre une carte Hero Bot Framework avec une action de carte « Acheter `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke)».</span><span class="sxs-lookup"><span data-stu-id="254e5-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="254e5-120">La valeur de `type` la propriété est - le reste de `task/fetch` `value` l’objet peut être ce que vous voulez.</span><span class="sxs-lookup"><span data-stu-id="254e5-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
1. <span data-ttu-id="254e5-121">Le bot reçoit le `invoke` message HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="254e5-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="254e5-122">Le bot crée un objet de réponse et le renvoie dans le corps de la réponse POST avec un code de réponse HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="254e5-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="254e5-123">Le schéma des réponses est décrit ci-dessous dans la discussion sur la [tâche/l’soumission,](#the-flexibility-of-tasksubmit)mais il est important de se souvenir maintenant que le corps de la réponse HTTP contient un objet [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) incorporé dans un objet wrapper.</span><span class="sxs-lookup"><span data-stu-id="254e5-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object.</span></span> <span data-ttu-id="254e5-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="254e5-124">For example:</span></span>

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

    <span data-ttu-id="254e5-125">L’événement et sa réponse pour les bots sont similaires, d’un point de vue conceptuel, à la `task/fetch` `microsoftTeams.tasks.startTask()` fonction dans le SDK client.</span><span class="sxs-lookup"><span data-stu-id="254e5-125">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
1. <span data-ttu-id="254e5-126">Microsoft Teams affiche le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="254e5-126">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="254e5-127">Envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="254e5-127">Submitting the result of a task module</span></span>

<span data-ttu-id="254e5-128">Lorsque l’utilisateur a terminé le module de tâche, l’envoi du résultat au bot est similaire à la façon dont il fonctionne avec les [onglets,](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)mais il existe quelques différences, il est donc également décrit ici.</span><span class="sxs-lookup"><span data-stu-id="254e5-128">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="254e5-129">**HTML/JavaScript ( `TaskInfo.url` )**.</span><span class="sxs-lookup"><span data-stu-id="254e5-129">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="254e5-130">Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK (appelée ci-après à des fins de `microsoftTeams.tasks.submitTask()` `submitTask()` lisibilité).</span><span class="sxs-lookup"><span data-stu-id="254e5-130">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="254e5-131">Vous pouvez appeler sans paramètre si vous souhaitez simplement Teams fermer le module de tâche, mais la plupart du temps vous souhaiterez passer un objet ou une chaîne à `submitTask()` votre `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="254e5-131">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="254e5-132">Passez-le simplement en tant que premier paramètre, `result` .</span><span class="sxs-lookup"><span data-stu-id="254e5-132">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="254e5-133">Teams appelle : `submitHandler` sera et sera `err` l’objet/chaîne `null` que vous avez transmis à `result` `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="254e5-133">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="254e5-134">Si vous appelez avec un paramètre, vous devez transmettre un ou plusieurs tableaux de chaînes : cela permet à Teams de vérifier que l’application qui envoie le résultat est la même que celle qui a appelé le module de `submitTask()` `result`  `appId` `appId` tâche.</span><span class="sxs-lookup"><span data-stu-id="254e5-134">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="254e5-135">Votre bot recevra un `task/submit` message, y compris `result` comme décrit [ci-dessous.](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="254e5-135">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="254e5-136">**Carte adaptative ( `TaskInfo.card` )**.</span><span class="sxs-lookup"><span data-stu-id="254e5-136">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="254e5-137">Le corps de la carte adaptative (tel que rempli par l’utilisateur) est envoyé au bot via un message lorsque l’utilisateur appuie sur `task/submit` un `Action.Submit` bouton.</span><span class="sxs-lookup"><span data-stu-id="254e5-137">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="254e5-138">Flexibilité de la tâche/de l’soumission</span><span class="sxs-lookup"><span data-stu-id="254e5-138">The flexibility of task/submit</span></span>

<span data-ttu-id="254e5-139">Dans la section précédente, vous avez appris que lorsque l’utilisateur termine avec un module de tâche appelé à partir d’un bot, il reçoit toujours un `task/submit invoke` message.</span><span class="sxs-lookup"><span data-stu-id="254e5-139">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="254e5-140">En tant que développeur, vous avez plusieurs options pour *répondre* au `task/submit` message :</span><span class="sxs-lookup"><span data-stu-id="254e5-140">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="254e5-141">Réponse du corps HTTP</span><span class="sxs-lookup"><span data-stu-id="254e5-141">HTTP Body Response</span></span>                      | <span data-ttu-id="254e5-142">Scénario</span><span class="sxs-lookup"><span data-stu-id="254e5-142">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="254e5-143">Aucun (ignorer le `task/submit` message)</span><span class="sxs-lookup"><span data-stu-id="254e5-143">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="254e5-144">La réponse la plus simple n’est pas du tout une réponse.</span><span class="sxs-lookup"><span data-stu-id="254e5-144">The simplest response is no response at all.</span></span> <span data-ttu-id="254e5-145">Votre bot n’est pas tenu de répondre lorsque l’utilisateur a terminé avec le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="254e5-145">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="254e5-146">Teams affiche la valeur `value` d’une zone de message électronique.</span><span class="sxs-lookup"><span data-stu-id="254e5-146">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="254e5-147">Vous permet de « chaîner » des séquences de cartes adaptatives ensemble dans une expérience d’Assistant/multi-étapes.</span><span class="sxs-lookup"><span data-stu-id="254e5-147">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="254e5-148">_Notez que le chaînage de cartes adaptatives dans une séquence est un scénario avancé et n’est pas documenté ici. LNode.js exemple d’application la prend en charge, toutefois, et son fonctionnement est documenté dans [son README.md.](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)_</span><span class="sxs-lookup"><span data-stu-id="254e5-148">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="254e5-149">Charge utile des messages de tâche/d’extraction et de tâche/d’soumission</span><span class="sxs-lookup"><span data-stu-id="254e5-149">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="254e5-150">Cette section définit le schéma de ce que votre bot reçoit lorsqu’il reçoit un `task/fetch` objet `task/submit` Bot `Activity` Framework.</span><span class="sxs-lookup"><span data-stu-id="254e5-150">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="254e5-151">Le niveau supérieur important apparaît ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="254e5-151">The important top-level appear below:</span></span>

| <span data-ttu-id="254e5-152">Propriété</span><span class="sxs-lookup"><span data-stu-id="254e5-152">Property</span></span> | <span data-ttu-id="254e5-153">Description</span><span class="sxs-lookup"><span data-stu-id="254e5-153">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="254e5-154">Toujours `invoke`</span><span class="sxs-lookup"><span data-stu-id="254e5-154">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="254e5-155">`task/fetch`L’une ou l’autre ou`task/submit`</span><span class="sxs-lookup"><span data-stu-id="254e5-155">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="254e5-156">Charge utile définie par le développeur.</span><span class="sxs-lookup"><span data-stu-id="254e5-156">The developer-defined payload.</span></span> <span data-ttu-id="254e5-157">Normalement, la structure de `value` l’objet reflète ce qui a été envoyé Teams.</span><span class="sxs-lookup"><span data-stu-id="254e5-157">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="254e5-158">Dans ce cas, toutefois, il est différent, car nous voulons prendre en charge la récupération dynamique ( ) à partir de Bot Framework ( ) et les actions de carte adaptative ( ), et nous avons besoin d’un moyen de communiquer Teams au bot en plus de ce qui a été inclus dans `task/fetch` `value` `Action.Submit` `data` `context` `value` / `data` .</span><span class="sxs-lookup"><span data-stu-id="254e5-158">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="254e5-159">Pour ce faire, nous combinons les deux en un objet parent :</span><span class="sxs-lookup"><span data-stu-id="254e5-159">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="254e5-160">Exemple : réception et réponse à des messages d’appel de tâche/extraction et de tâche/soumission - Node.js</span><span class="sxs-lookup"><span data-stu-id="254e5-160">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="254e5-161">L’exemple de code ci-dessous a été modifié entre Technical Preview et la version finale de cette fonctionnalité : le schéma de la demande a été modifié pour suivre ce qui a été documenté dans `task/fetch` [la section précédente](#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="254e5-161">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="254e5-162">Autrement dit, la documentation était correcte, mais pas l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="254e5-162">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="254e5-163">Consultez `// for Technical Preview [...]` les commentaires ci-dessous pour savoir ce qui a changé.</span><span class="sxs-lookup"><span data-stu-id="254e5-163">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="254e5-164">Exemple : réception et réponse à des messages d’appel de tâche/extraction et de tâche/soumission - C #</span><span class="sxs-lookup"><span data-stu-id="254e5-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="254e5-165">Dans C# bots, `invoke` les messages sont traitées par un contrôleur `HttpResponseMessage()` qui traite un `Activity` message.</span><span class="sxs-lookup"><span data-stu-id="254e5-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="254e5-166">Les `task/fetch` demandes et les réponses sont `task/submit` JSON.</span><span class="sxs-lookup"><span data-stu-id="254e5-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="254e5-167">Dans C#, il n’est pas aussi pratique de traiter du JSON brut que dans Node.js. Vous avez donc besoin de classes wrapper pour gérer la sérialisation vers et à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="254e5-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="254e5-168">Il n’existe pas de prise en charge directe pour cela dans le [SDK Microsoft Teams C#,](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) mais vous pouvez voir un exemple de ce à quoi ces classes de wrapper simples ressembleraient dans l’exemple d’application [C#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span><span class="sxs-lookup"><span data-stu-id="254e5-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="254e5-169">Voici un exemple de code C# pour la gestion et les messages à l’aide de ces `task/fetch` `task/submit` classes de wrapper ( , ), extrait `TaskInfo` de `TaskEnvelope` [l’exemple](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span><span class="sxs-lookup"><span data-stu-id="254e5-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="254e5-170">La fonction, qui définit les propriétés et les propriétés de l’objet pour chaque cas, n’est pas indiquée dans `SetTaskInfo()` `height` `width` `title` `TaskInfo` l’exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="254e5-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="254e5-171">Voici le [code source pour SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span><span class="sxs-lookup"><span data-stu-id="254e5-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="254e5-172">Actions de carte Bot Framework et actions Action.Submit de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="254e5-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="254e5-173">Le schéma des actions de carte Bot Framework est légèrement différent des actions de carte `Action.Submit` adaptative.</span><span class="sxs-lookup"><span data-stu-id="254e5-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="254e5-174">Par conséquent, la façon d’appeler des modules de tâche est légèrement différente : l’objet dans contient un objet afin `data` `Action.Submit` qu’il n’interfère pas avec les autres propriétés `msteams` de la carte.</span><span class="sxs-lookup"><span data-stu-id="254e5-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="254e5-175">Le tableau suivant présente un exemple de chacun d’eux :</span><span class="sxs-lookup"><span data-stu-id="254e5-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="254e5-176">Action de carte Bot Framework</span><span class="sxs-lookup"><span data-stu-id="254e5-176">Bot Framework card action</span></span>                              | <span data-ttu-id="254e5-177">Action Action.Submit de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="254e5-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a><span data-ttu-id="254e5-178">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="254e5-178">See also</span></span>

* [<span data-ttu-id="254e5-179">Microsoft Teams exemple de code du module de tâche : nodejs</span><span class="sxs-lookup"><span data-stu-id="254e5-179">Microsoft Teams task module sample code — nodejs</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* <span data-ttu-id="254e5-180">[Exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="254e5-180">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>