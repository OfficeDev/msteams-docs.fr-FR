---
title: Appeler et ignorer des modules de tâche
description: Appeler et ignorer les modules de tâche.
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a23d5cee3f13967772a4b58ed973bf08906e36a6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140771"
---
# <a name="invoke-and-dismiss-task-modules"></a><span data-ttu-id="fe8e2-103">Appeler et ignorer des modules de tâche</span><span class="sxs-lookup"><span data-stu-id="fe8e2-103">Invoke and dismiss task modules</span></span>

<span data-ttu-id="fe8e2-104">Les modules de tâche peuvent être appelés à partir d’onglets, de bots ou de liens profonds.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-104">Task modules can be invoked from tabs, bots, or deep links.</span></span> <span data-ttu-id="fe8e2-105">La réponse peut être au format HTML, JavaScript ou sous forme de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-105">The response can be either in HTML, JavaScript, or as an Adaptive Card.</span></span> <span data-ttu-id="fe8e2-106">La façon dont les modules de tâche sont appelés et la manière de traiter la réponse de l’interaction de l’utilisateur offrent beaucoup de souplesse.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-106">There is a lot of flexibility in terms of how task modules are invoked and how to deal with the response of the user's interaction.</span></span> <span data-ttu-id="fe8e2-107">Le tableau suivant récapitule le fonctionnement :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-107">The following table summarizes how this works:</span></span>

| <span data-ttu-id="fe8e2-108">Appel à l’aide</span><span class="sxs-lookup"><span data-stu-id="fe8e2-108">Invoked using</span></span> | <span data-ttu-id="fe8e2-109">Module de tâche avec HTML ou JavaScript</span><span class="sxs-lookup"><span data-stu-id="fe8e2-109">Task module with HTML or JavaScript</span></span> | <span data-ttu-id="fe8e2-110">Module de tâche avec carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fe8e2-110">Task module with Adaptive Card</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe8e2-111">JavaScript dans un onglet</span><span class="sxs-lookup"><span data-stu-id="fe8e2-111">JavaScript in a tab</span></span> | <span data-ttu-id="fe8e2-112">1. Utilisez la fonction Teams SDK client `tasks.startTask()` avec une fonction de rappel `submitHandler(err, result)` facultative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-112">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function.</span></span> <br/><br/> <span data-ttu-id="fe8e2-113">2. Dans le code du module de tâche, lorsque l’utilisateur a effectué les actions, appelez la fonction Teams SDK avec un objet `tasks.submitTask()` `result` en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-113">2. In the task module code, when the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="fe8e2-114">Si un `submitHandler` rappel a été spécifié dans , Teams `tasks.startTask()` l’appelle avec `result` comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-114">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span> <span data-ttu-id="fe8e2-115">Si une erreur s’est produite lors de l’appel, la fonction est `tasks.startTask()` appelée avec une chaîne à la `submitHandler` `err` place.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-115">If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="fe8e2-116">3. Vous pouvez également spécifier un lorsque `completionBotId` vous appelez `teams.startTask()` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-116">3. You can also specify a `completionBotId` when calling `teams.startTask()`.</span></span> <span data-ttu-id="fe8e2-117">Ensuite, `result` il est envoyé au bot à la place.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-117">Then the `result` is sent to the bot instead.</span></span> | <span data-ttu-id="fe8e2-118">1. Appelez la fonction Teams client SDK avec un objet TaskInfo et contenant le JSON de la carte adaptative à afficher dans la fenêtre pop-up du module de `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-118">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive Card to show in the task module pop-up.</span></span> <br/><br/> <span data-ttu-id="fe8e2-119">2. Si un rappel a été spécifié dans , Teams l’appelle avec une chaîne, s’il y a eu une erreur lors de l’appel ou si l’utilisateur ferme la fenêtre `submitHandler` pop-up du module de tâche à l’aide du X en haut à `tasks.startTask()` `err` `tasks.startTask()` droite.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-119">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string, if there was an error when invoking `tasks.startTask()` or if the user closes the task module pop-up using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="fe8e2-120">3. Si l’utilisateur appuie sur un `Action.Submit` bouton, son `data` objet est renvoyé en tant que valeur de `result` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-120">3. If the user presses an `Action.Submit` button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="fe8e2-121">Bouton de carte bot</span><span class="sxs-lookup"><span data-stu-id="fe8e2-121">Bot card button</span></span> | <span data-ttu-id="fe8e2-122">1. Les boutons de carte bot, en fonction du type de bouton, peuvent appeler des modules de tâche de deux manières : une URL de lien profond ou en envoyant un `task/fetch` message.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-122">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways, a deep link URL or by sending a `task/fetch` message.</span></span> <br/><br/> <span data-ttu-id="fe8e2-123">2. Si l’action du bouton est le type de bouton pour les cartes adaptatives, un événement qui est une demande HTTP POST est envoyé `type` `task/fetch` au `Action.Submit` `task/fetch invoke` bot.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-123">2. If the button's action `type` is `task/fetch` that is `Action.Submit` button type for Adaptive Cards, a `task/fetch invoke` event that is an HTTP POST is sent to the bot.</span></span> <span data-ttu-id="fe8e2-124">Le bot répond au POST avec HTTP 200 et le corps de la réponse contenant un wrapper autour de [l’objet TaskInfo](#the-taskinfo-object).</span><span class="sxs-lookup"><span data-stu-id="fe8e2-124">The bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="fe8e2-125">Pour plus d’informations, [voir l’appel `task/fetch` d’un module de tâche à l’aide de ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span><span class="sxs-lookup"><span data-stu-id="fe8e2-125">For more information, see [invoking a task module using `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span></span> <span data-ttu-id="fe8e2-126">Teams affiche le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-126">Teams displays the task module.</span></span> <br/><br/> <span data-ttu-id="fe8e2-127">3. Une fois que l’utilisateur a effectué les actions, appelez la fonction Teams SDK avec un `tasks.submitTask()` objet en tant que `result` paramètre.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-127">3. After the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="fe8e2-128">Le bot reçoit un `task/submit invoke` message contenant `result` l’objet.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-128">The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <br/><br/> <span data-ttu-id="fe8e2-129">4. Vous pouvez répondre au message de trois manières différentes, en ne faisant rien qui soit correctement effectué par la tâche, en affichant un message à l’utilisateur dans une fenêtre ou en invoquant une autre fenêtre de module de `task/submit` tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-129">4. You have three different ways to respond to the `task/submit` message, by doing nothing that is the task completed successfully, by displaying a message to the user in a pop-up window, or by invoking another task module window.</span></span> <span data-ttu-id="fe8e2-130">Pour plus d’informations, [voir la discussion détaillée sur `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span><span class="sxs-lookup"><span data-stu-id="fe8e2-130">For more information, see [detailed discussion on `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <ul><li> <span data-ttu-id="fe8e2-131">Comme les boutons sur les cartes Bot Framework, les boutons des cartes adaptatives offrent deux moyens d’appel des modules de tâche, d’URL de liens profonds avec des boutons et d’utilisation `Action.openUrl` `task/fetch` de `Action.Submit` boutons.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-131">Like buttons on Bot Framework cards, buttons on Adaptive Cards support two ways of invoking task modules, deep link URLs with `Action.openUrl` buttons, and `task/fetch` using `Action.Submit` buttons.</span></span> </li></ul> <br/><br/> <ul><li> <span data-ttu-id="fe8e2-132">Les modules de tâche avec cartes adaptatives fonctionnent de manière très similaire au cas HTML ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-132">Task modules with Adaptive Cards work very similarly to the HTML or JavaScript case.</span></span> <span data-ttu-id="fe8e2-133">La principale différence est que, étant donné qu’il n’existe pas de JavaScript lorsque vous utilisez des cartes adaptatives, il n’existe aucun moyen d’appeler `tasks.submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-133">The major difference is that since there is no JavaScript when you are using Adaptive Cards, there is no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="fe8e2-134">Au lieu de cela, Teams l’objet et le renvoie en tant que `data` `Action.Submit` charge utile de `task/submit` l’événement.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-134">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of the `task/submit` event.</span></span> <span data-ttu-id="fe8e2-135">Pour plus d’informations, voir [flexibilité de `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span><span class="sxs-lookup"><span data-stu-id="fe8e2-135">For more information, see [flexibility of `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> </li></ul> |
| <span data-ttu-id="fe8e2-136">URL du lien profond</span><span class="sxs-lookup"><span data-stu-id="fe8e2-136">Deep link URL</span></span> <br/>[<span data-ttu-id="fe8e2-137">Syntaxe d'URL</span><span class="sxs-lookup"><span data-stu-id="fe8e2-137">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="fe8e2-138">1. Teams le module de tâche qui est l’URL qui apparaît à l’intérieur du paramètre spécifié dans le `<iframe>` `url` paramètre du lien profond.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-138">1. Teams invokes the task module that is the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="fe8e2-139">Il n’y `submitHandler` a pas de rappel.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-139">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="fe8e2-140">2. Dans le JavaScript de la page dans le module de tâche, appelez pour le fermer avec un objet en tant que paramètre, comme lors de l’appel à partir d’un onglet ou d’un bouton de carte `tasks.submitTask()` `result` bot.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-140">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="fe8e2-141">Toutefois, la logique d’achèvement est légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-141">However, completion logic is slightly different.</span></span> <span data-ttu-id="fe8e2-142">Si votre logique d’achèvement réside sur le client, c’est-à-dire s’il n’y a pas de bot, il n’y a pas de rappel, de sorte que toute logique d’achèvement doit se trouver dans le code précédant `submitHandler` l’appel vers `tasks.submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-142">If your completion logic resides on the client that is if there is no bot, there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="fe8e2-143">Les erreurs d’appel sont uniquement signalées via la console.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-143">Invocation errors are only reported through the console.</span></span> <span data-ttu-id="fe8e2-144">Si vous avez un bot, vous pouvez spécifier un paramètre dans le lien profond pour envoyer l’objet `completionBotId` `result` via un `task/submit` événement.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-144">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object through a `task/submit` event.</span></span> | <span data-ttu-id="fe8e2-145">1. Teams appelle le module de tâche qui est le corps de la carte JSON de la carte adaptative spécifiée en tant que valeur codée URL du paramètre du lien `card` profond.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-145">1. Teams invokes the task module that is the JSON card body of the Adaptive Card that is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="fe8e2-146">2. L’utilisateur ferme le module de tâche en sélectionnant le X en haut à droite du module de tâche ou en appuyant sur un bouton `Action.Submit` de la carte.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-146">2. The user closes the task module by selecting the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="fe8e2-147">Étant donné qu’il n’y a pas d’appel, l’utilisateur doit avoir un bot pour envoyer la valeur des champs de `submitHandler` carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-147">Since there is no `submitHandler` to call, the user must have a bot to send the value of the Adaptive Card fields.</span></span> <span data-ttu-id="fe8e2-148">L’utilisateur doit utiliser le paramètre dans le lien profond pour spécifier le bot pour envoyer les données à l’aide `completionBotId` d’un `task/submit invoke` événement.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-148">The user must use the `completionBotId` parameter in the deep link to specify the bot to send the data to using a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="fe8e2-149">L’vot d’un module de tâche à partir de JavaScript n’est pas pris en charge sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-149">Invoking a task module from JavaScript is not supported on mobile.</span></span>

<span data-ttu-id="fe8e2-150">La section suivante spécifie `TaskInfo` l’objet qui définit certains attributs pour un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-150">The next section specifies the `TaskInfo` object that defines certain attributes for a task module.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="fe8e2-151">Objet TaskInfo</span><span class="sxs-lookup"><span data-stu-id="fe8e2-151">The TaskInfo object</span></span>

<span data-ttu-id="fe8e2-152">`TaskInfo`L’objet contient les métadonnées d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-152">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="fe8e2-153">Définissez `url` le pour un iFrame incorporé ou pour une carte `card` adaptative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-153">Define the `url` for an embedded iFrame or `card` for an Adaptive Card.</span></span> <span data-ttu-id="fe8e2-154">Le tableau suivant fournit la définition d’objet :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-154">The following table provides the object definition:</span></span>

| <span data-ttu-id="fe8e2-155">Attribut</span><span class="sxs-lookup"><span data-stu-id="fe8e2-155">Attribute</span></span> | <span data-ttu-id="fe8e2-156">Type</span><span class="sxs-lookup"><span data-stu-id="fe8e2-156">Type</span></span> | <span data-ttu-id="fe8e2-157">Description</span><span class="sxs-lookup"><span data-stu-id="fe8e2-157">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="fe8e2-158">string</span><span class="sxs-lookup"><span data-stu-id="fe8e2-158">string</span></span> | <span data-ttu-id="fe8e2-159">Cet attribut apparaît sous le nom de l’application et à droite de l’icône de l’application.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-159">This attribute appears below the app name and to the right of the app icon.</span></span> |
| `height` | <span data-ttu-id="fe8e2-160">valeur numérique ou chaîne</span><span class="sxs-lookup"><span data-stu-id="fe8e2-160">number or string</span></span> | <span data-ttu-id="fe8e2-161">Cet attribut peut être un nombre représentant la hauteur du module de tâche en pixels, `small` ou `medium` , ou `large` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-161">This attribute can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="fe8e2-162">Pour plus d’informations, [voir le resserrage du module de tâche.](#task-module-sizing)</span><span class="sxs-lookup"><span data-stu-id="fe8e2-162">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="fe8e2-163">valeur numérique ou chaîne</span><span class="sxs-lookup"><span data-stu-id="fe8e2-163">number or string</span></span> | <span data-ttu-id="fe8e2-164">Cet attribut peut être un nombre représentant la largeur du module de tâche en pixels, `small` ou `medium` , ou `large` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-164">This attribute can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="fe8e2-165">Pour plus d’informations, [voir le resserrage du module de tâche.](#task-module-sizing)</span><span class="sxs-lookup"><span data-stu-id="fe8e2-165">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="fe8e2-166">chaîne</span><span class="sxs-lookup"><span data-stu-id="fe8e2-166">string</span></span> | <span data-ttu-id="fe8e2-167">Cet attribut est l’URL de la page chargée en tant qu’url à `<iframe>` l’intérieur du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-167">This attribute is the URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="fe8e2-168">Le domaine de l’URL doit se trouver dans le tableau [validDomains](~/resources/schema/manifest-schema.md#validdomains) de l’application dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-168">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="fe8e2-169">Pièce jointe d’une carte adaptative ou d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fe8e2-169">Adaptive Card or Adaptive Card bot card attachment</span></span> | <span data-ttu-id="fe8e2-170">Cet attribut est le JSON de la carte adaptative à apparaître dans le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-170">This attribute is the JSON for the Adaptive Card to appear in the task module.</span></span> <span data-ttu-id="fe8e2-171">Si l’utilisateur fait appel à partir d’un bot, utilisez le JSON de carte adaptative dans un objet Bot `attachment` Framework.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-171">If the user is invoking from a bot, use the Adaptive Card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="fe8e2-172">À partir d’un onglet, l’utilisateur doit utiliser une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-172">From a tab, the user must use an Adaptive Card.</span></span> <span data-ttu-id="fe8e2-173">Pour plus d’informations, voir [carte adaptative ou pièce jointe de carte de bot de carte adaptative](#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="fe8e2-173">For more information, see [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment)</span></span> |
| `fallbackUrl` | <span data-ttu-id="fe8e2-174">chaîne</span><span class="sxs-lookup"><span data-stu-id="fe8e2-174">string</span></span> | <span data-ttu-id="fe8e2-175">Cet attribut ouvre l’URL dans un onglet de navigateur, si un client ne prend pas en charge la fonctionnalité de module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-175">This attribute opens the URL in a browser tab, if a client does not support the task module feature.</span></span> |
| `completionBotId` | <span data-ttu-id="fe8e2-176">chaîne</span><span class="sxs-lookup"><span data-stu-id="fe8e2-176">string</span></span> | <span data-ttu-id="fe8e2-177">Cet attribut spécifie un ID d’application de bot pour envoyer le résultat de l’interaction de l’utilisateur avec le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-177">This attribute specifies a bot App ID to send the result of the user's interaction with the task module.</span></span> <span data-ttu-id="fe8e2-178">S’il est spécifié, le bot reçoit un événement `task/submit invoke` avec un objet JSON dans la charge utile de l’événement.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-178">If specified, the bot receives a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="fe8e2-179">La fonctionnalité de module de tâche nécessite que les domaines des URL que vous souhaitez charger soient inclus dans le tableau dans le manifeste `validDomains` de votre application.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-179">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

<span data-ttu-id="fe8e2-180">La section suivante spécifie le resserrage du module de tâche qui permet à l’utilisateur de définir la hauteur et la largeur du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-180">The next section specifies task module sizing that enables the user to set the height and width of the task module.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="fe8e2-181">Resserrage du module de tâche</span><span class="sxs-lookup"><span data-stu-id="fe8e2-181">Task module sizing</span></span>

<span data-ttu-id="fe8e2-182">L’utilisation d’nombres integers pour et , définit la hauteur et la largeur du `TaskInfo.width` module de tâche en `TaskInfo.height` pixels.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-182">Using integers for `TaskInfo.width` and `TaskInfo.height`, sets the height and width of the task module in pixels.</span></span> <span data-ttu-id="fe8e2-183">Toutefois, en fonction de la taille de la fenêtre et de la résolution de l’écran de l’équipe, elles sont réduites proportionnellement tout en conservant les proportions de largeur ou de hauteur.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-183">However, depending on the size of the Team's window and screen resolution they are reduced proportionally while maintaining the aspect ratio that is width or height.</span></span>

<span data-ttu-id="fe8e2-184">Si et sont , ou , la taille du rectangle rouge dans l’image suivante est une proportion de l’espace `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` disponible, 20 %, 50 % et 60 % pour et `width` 20 %, 50 % et 66 % `height` pour :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-184">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"`, or `"large"`, the size of the red rectangle in the following image is a proportion of the available space, 20%, 50%, and 60% for `width` and 20%, 50%, and 66% for `height`:</span></span>

![Exemple de module de tâche](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="fe8e2-186">Les modules de tâche appelés à partir d’un onglet peuvent être resserrisés dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-186">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="fe8e2-187">Après l’appel, vous pouvez appeler l’endroit où les propriétés de hauteur et de largeur de l’objet newSize sont conformes à la spécification `tasks.startTask()` `tasks.updateTask(newSize)` TaskInfo, par `{ height: 'medium', width: 'medium' }` exemple.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-187">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo specification, for example `{ height: 'medium', width: 'medium' }`.</span></span>

<span data-ttu-id="fe8e2-188">La section suivante fournit des exemples d’incorporation de modules de tâche dans une vidéo YouTube et une application PowerApp.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-188">The next section provides examples of embedding task modules in a YouTube video and a PowerApp.</span></span>

## <a name="task-module-css-for-html-or-javascript-task-modules"></a><span data-ttu-id="fe8e2-189">Module de tâche CSS pour les modules de tâche HTML ou JavaScript</span><span class="sxs-lookup"><span data-stu-id="fe8e2-189">Task module CSS for HTML or JavaScript task modules</span></span>

<span data-ttu-id="fe8e2-190">Les modules de tâche HTML ou JavaScript ont accès à toute la zone du module de tâche sous l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-190">HTML or JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="fe8e2-191">Bien que cela offre beaucoup de flexibilité, si vous souhaitez que le remplissage autour des bords s’aligne sur les éléments d’en-tête et évite les barres de défilement inutiles, l’utilisateur doit fournir le bon CSS.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-191">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scroll bars, the user must provide the right CSS.</span></span> <span data-ttu-id="fe8e2-192">Les sections suivantes fournissent quelques exemples pour quelques cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-192">The next sections provide some examples for a few use cases.</span></span>

<span data-ttu-id="fe8e2-193">**Exemple 1 : vidéo YouTube**</span><span class="sxs-lookup"><span data-stu-id="fe8e2-193">**Example 1: YouTube video**</span></span>

<span data-ttu-id="fe8e2-194">YouTube offre la possibilité d’incorporer des vidéos sur des pages web.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-194">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="fe8e2-195">Il est facile d’incorporer des vidéos sur des pages web dans un module de tâche à l’aide d’une page web stub simple.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-195">It is easy to embed videos on web pages in a task module using a simple stub web page.</span></span>

![Vidéo YouTube](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="fe8e2-197">Le code suivant fournit un exemple de code HTML pour la page web sans CSS :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-197">The following code provides an example of the HTML for the web page without the CSS:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

<span data-ttu-id="fe8e2-198">Le code suivant fournit un exemple de CSS :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-198">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="fe8e2-199">**Exemple 2 : PowerApp**</span><span class="sxs-lookup"><span data-stu-id="fe8e2-199">**Example 2: PowerApp**</span></span>

<span data-ttu-id="fe8e2-200">L’utilisateur peut également utiliser la même approche pour incorporer un PowerApp.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-200">The user can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="fe8e2-201">Comme la hauteur ou la largeur d’un PowerApp individuel est personnalisable, l’utilisateur peut ajuster la hauteur et la largeur pour obtenir la présentation souhaitée.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-201">As the height or width of any individual PowerApp is customizable, the user can adjust the height and width to achieve the desired presentation.</span></span>

![Gestion des biens PowerApp](~/assets/images/task-module/powerapp-example.png)

<span data-ttu-id="fe8e2-203">Le code suivant fournit un exemple de code HTML pour PowerApp :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-203">The following code provides an example of the HTML for PowerApp:</span></span>

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="fe8e2-204">Le code suivant fournit un exemple de CSS :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-204">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="fe8e2-205">La section suivante fournit des détails sur l’appel de votre carte à l’aide d’une carte adaptative ou d’une pièce jointe de carte bot de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-205">The next section provides details on invoking your card using Adaptive Card or Adaptive Card bot card attachment.</span></span>

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="fe8e2-206">Pièce jointe d’une carte adaptative ou d’une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fe8e2-206">Adaptive Card or Adaptive Card bot card attachment</span></span>

<span data-ttu-id="fe8e2-207">Selon la façon dont vous voquer votre , vous devez utiliser une carte adaptative ou une pièce jointe de carte de bot de carte adaptative, qui est une carte adaptative wrapped dans un objet `card` pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-207">Depending on how you are invoking your `card`, you must use either an Adaptive Card or an Adaptive Card bot card attachment, which is an Adaptive Card wrapped in an attachment object.</span></span>

<span data-ttu-id="fe8e2-208">Lorsque vous voquer à partir d’un onglet, l’utilisateur doit utiliser une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-208">When you are invoking from a tab, the user must use an Adaptive Card.</span></span>

<span data-ttu-id="fe8e2-209">Le code suivant fournit un exemple de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-209">The following code provides an example of an Adaptive Card:</span></span>

```json
{
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
}
```

<span data-ttu-id="fe8e2-210">Le code suivant fournit un exemple de pièce jointe d’une carte de bot de carte adaptative lorsque vous voquer à partir d’un bot :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-210">The following code provides an example of an Adaptive Card bot card attachment when you are invoking from a bot:</span></span>

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
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
    }
}
```

<span data-ttu-id="fe8e2-211">La section suivante fournit des détails sur la syntaxe de lien profond du module de tâche, y compris `TaskInfo` l’objet et `APP_ID` `BOT_APP_ID` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-211">The next section provides details on task module deep link syntax including the `TaskInfo` object and `APP_ID` and `BOT_APP_ID`.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="fe8e2-212">Syntaxe de lien profond du module de tâche</span><span class="sxs-lookup"><span data-stu-id="fe8e2-212">Task module deep link syntax</span></span>

<span data-ttu-id="fe8e2-213">Un lien profond de module de tâche est une sérialisation de l’objet TaskInfo avec les deux autres détails suivants, et `APP_ID` éventuellement les éléments suivants `BOT_APP_ID` :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-213">A task module deep link is a serialization of the TaskInfo object with the following two other details, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="fe8e2-214">Pour les types de données et les valeurs permises pour `<TaskInfo.url>` , , et , voir `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [l’objet TaskInfo](#the-taskinfo-object).</span><span class="sxs-lookup"><span data-stu-id="fe8e2-214">For the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`, see [TaskInfo object](#the-taskinfo-object).</span></span>

> [!TIP]
> <span data-ttu-id="fe8e2-215">URL encoder le lien profond lors de `card` l’utilisation [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)du paramètre, par exemple, la fonction JavaScript .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-215">URL encode the deep link when using the `card` parameter, for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp).</span></span>

<span data-ttu-id="fe8e2-216">Le tableau suivant fournit des informations sur `APP_ID` et `BOT_APP_ID` :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-216">The following table provides information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="fe8e2-217">Valeur</span><span class="sxs-lookup"><span data-stu-id="fe8e2-217">Value</span></span> | <span data-ttu-id="fe8e2-218">Type</span><span class="sxs-lookup"><span data-stu-id="fe8e2-218">Type</span></span> | <span data-ttu-id="fe8e2-219">Requis</span><span class="sxs-lookup"><span data-stu-id="fe8e2-219">Required</span></span> | <span data-ttu-id="fe8e2-220">Description</span><span class="sxs-lookup"><span data-stu-id="fe8e2-220">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="fe8e2-221">string</span><span class="sxs-lookup"><span data-stu-id="fe8e2-221">string</span></span> | <span data-ttu-id="fe8e2-222">Oui</span><span class="sxs-lookup"><span data-stu-id="fe8e2-222">Yes</span></span> | <span data-ttu-id="fe8e2-223">[ID de l’application](~/resources/schema/manifest-schema.md#id) qui invoquer le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-223">The [ID](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="fe8e2-224">Le [tableau validDomains dans](~/resources/schema/manifest-schema.md#validdomains) le manifeste doit contenir le domaine pour si se trouve dans `APP_ID` `url` `url` l’URL.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-224">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="fe8e2-225">L’ID d’application est déjà connu lorsqu’un module de tâche est appelé à partir d’un onglet ou d’un bot, c’est pourquoi il n’est pas inclus dans `TaskInfo` .</span><span class="sxs-lookup"><span data-stu-id="fe8e2-225">The app ID is already known when a task module is invoked from a tab or a bot, which is why it is not included in `TaskInfo`.</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="fe8e2-226">string</span><span class="sxs-lookup"><span data-stu-id="fe8e2-226">string</span></span> | <span data-ttu-id="fe8e2-227">Non</span><span class="sxs-lookup"><span data-stu-id="fe8e2-227">No</span></span> | <span data-ttu-id="fe8e2-228">Si une valeur `completionBotId` est spécifiée, l’objet est envoyé à l’aide `result` d’un message au `task/submit invoke` bot spécifié.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-228">If a value for `completionBotId` is specified, the `result` object is sent using a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="fe8e2-229">`BOT_APP_ID` doit être spécifié en tant que bot dans le manifeste de l’application, c’est-à-dire que vous ne pouvez pas l’envoyer à un bot.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-229">`BOT_APP_ID` must be specified as a bot in the app's manifest, that is you cannot send it to any bot.</span></span> |

> [!NOTE]
> <span data-ttu-id="fe8e2-230">`APP_ID` et peut être identique dans de nombreux cas, si une application possède un bot recommandé à utiliser comme `BOT_APP_ID` ID d’application s’il en existe un.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-230">`APP_ID` and `BOT_APP_ID` can be the same in many cases, if an app has a recommended bot to use as an app's ID if there is one.</span></span>

<span data-ttu-id="fe8e2-231">La section suivante fournit des détails sur l’utilisation d’un clavier avec le module de tâche de votre application.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-231">The next section provides details on using a keyboard with your app's task module.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="fe8e2-232">Recommandations en matière de clavier et d’accessibilité</span><span class="sxs-lookup"><span data-stu-id="fe8e2-232">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="fe8e2-233">Avec les modules de tâche HTML ou JavaScript, vous devez vous assurer que le module de tâche de votre application peut être utilisé avec un clavier.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-233">With HTML or JavaScript-based task modules, you must ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="fe8e2-234">Les programmes de lecteur d’écran dépendent également de la possibilité de naviguer à l’aide du clavier.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-234">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="fe8e2-235">Cela inclut les deux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-235">This includes the following two things:</span></span>

* <span data-ttu-id="fe8e2-236">Utilisation de [l’attribut tabindex dans](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) vos balises HTML pour contrôler les éléments qui peuvent être concentrés.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-236">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused.</span></span> <span data-ttu-id="fe8e2-237">En outre, utilisez l’attribut tabindex pour identifier l’endroit où il participe à la navigation séquentielle au clavier généralement avec les touches <kbd>Tab</kbd> et <kbd>Shift-Tab.</kbd></span><span class="sxs-lookup"><span data-stu-id="fe8e2-237">Also, use tabindex attribute to identify where it participates in sequential keyboard navigation usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys.</span></span>
* <span data-ttu-id="fe8e2-238">Gestion de la <kbd>touche Échap</kbd> dans javaScript pour votre module de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-238">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="fe8e2-239">Le code suivant fournit un exemple de la façon de gérer la touche <kbd>Échap</kbd> :</span><span class="sxs-lookup"><span data-stu-id="fe8e2-239">The following code provides an example of how to handle the <kbd>Esc</kbd> key:</span></span>

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

<span data-ttu-id="fe8e2-240">Microsoft Teams s’assure que la navigation au clavier fonctionne correctement à partir de l’en-tête du module de tâche dans votre code HTML et inversement.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-240">Microsoft Teams ensures that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="code-sample"></a><span data-ttu-id="fe8e2-241">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="fe8e2-241">Code sample</span></span>

|<span data-ttu-id="fe8e2-242">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="fe8e2-242">Sample name</span></span> | <span data-ttu-id="fe8e2-243">Description</span><span class="sxs-lookup"><span data-stu-id="fe8e2-243">Description</span></span> | <span data-ttu-id="fe8e2-244">.NET</span><span class="sxs-lookup"><span data-stu-id="fe8e2-244">.NET</span></span> | <span data-ttu-id="fe8e2-245">Node.js</span><span class="sxs-lookup"><span data-stu-id="fe8e2-245">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="fe8e2-246">Exemples de module de tâche bots-V4</span><span class="sxs-lookup"><span data-stu-id="fe8e2-246">Task module sample bots-V4</span></span> | <span data-ttu-id="fe8e2-247">Exemples de création de modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-247">Samples for creating task modules.</span></span> |[<span data-ttu-id="fe8e2-248">View</span><span class="sxs-lookup"><span data-stu-id="fe8e2-248">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="fe8e2-249">View</span><span class="sxs-lookup"><span data-stu-id="fe8e2-249">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|<span data-ttu-id="fe8e2-250">Exemples d’onglets de module de tâche et bots-V3</span><span class="sxs-lookup"><span data-stu-id="fe8e2-250">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="fe8e2-251">Exemples de création de modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe8e2-251">Samples for creating task modules.</span></span> |[<span data-ttu-id="fe8e2-252">View</span><span class="sxs-lookup"><span data-stu-id="fe8e2-252">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="fe8e2-253">View</span><span class="sxs-lookup"><span data-stu-id="fe8e2-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="fe8e2-254">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fe8e2-254">See also</span></span>

* [<span data-ttu-id="fe8e2-255">Demande des autorisations d’appareil</span><span class="sxs-lookup"><span data-stu-id="fe8e2-255">Request device permissions</span></span>](~/concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="fe8e2-256">Intégrer les fonctionnalités médias</span><span class="sxs-lookup"><span data-stu-id="fe8e2-256">Integrate media capabilities</span></span>](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="fe8e2-257">Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="fe8e2-257">Integrate QR or barcode scanner capability in Teams</span></span>](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="fe8e2-258">Intégrer des fonctionnalités d’emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="fe8e2-258">Integrate location capabilities in Teams</span></span>](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="fe8e2-259">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="fe8e2-259">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe8e2-260">Utiliser des modules de tâche dans les onglets</span><span class="sxs-lookup"><span data-stu-id="fe8e2-260">Use task modules in tabs</span></span>](~/task-modules-and-cards/task-modules/task-modules-tabs.md)