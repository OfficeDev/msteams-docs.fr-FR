---
title: Utiliser des modules de tâche dans Microsoft Teams onglets
description: Explique comment appeler des modules de tâche à partir Teams onglets à l’aide Microsoft Teams SDK client.
localization_priority: Normal
ms.topic: how-to
keywords: sdk client des onglets des modules de tâche teams
ms.openlocfilehash: 8afd2c93261f28aa7ced4c98d29be27dca35f8b1
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140551"
---
# <a name="use-task-modules-in-tabs"></a><span data-ttu-id="3bc76-104">Utiliser des modules de tâche dans les onglets</span><span class="sxs-lookup"><span data-stu-id="3bc76-104">Use task modules in tabs</span></span>

<span data-ttu-id="3bc76-105">Ajoutez un module de tâche à votre onglet pour simplifier l’expérience de votre utilisateur pour les flux de travail qui nécessitent une entrée de données.</span><span class="sxs-lookup"><span data-stu-id="3bc76-105">Add a task module to your tab to simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="3bc76-106">Les modules de tâche vous permettent de collecter leurs entrées dans une fenêtre Teams-Aware microsoft.</span><span class="sxs-lookup"><span data-stu-id="3bc76-106">Task modules allow you to gather their input in a Microsoft Teams-Aware pop-up.</span></span> <span data-ttu-id="3bc76-107">La modification des cartes planificateur en est un bon exemple.</span><span class="sxs-lookup"><span data-stu-id="3bc76-107">A good example of this is editing Planner cards.</span></span> <span data-ttu-id="3bc76-108">Vous pouvez utiliser des modules de tâche pour créer une expérience similaire.</span><span class="sxs-lookup"><span data-stu-id="3bc76-108">You can use task modules to create a similar experience.</span></span>

<span data-ttu-id="3bc76-109">Pour prendre en charge la fonctionnalité de module de tâche, deux nouvelles fonctions sont ajoutées au [SDK Teams client.](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="3bc76-109">To support the task module feature, two new functions are added to the [Teams client SDK](/javascript/api/overview/msteams-client).</span></span> <span data-ttu-id="3bc76-110">Le code suivant montre un exemple de ces deux fonctions :</span><span class="sxs-lookup"><span data-stu-id="3bc76-110">The following code shows an example of these two functions:</span></span>

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

<span data-ttu-id="3bc76-111">Vous pouvez voir comment l’utilisation d’un module de tâche à partir d’un onglet et l’envoi du résultat d’un module de tâche fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="3bc76-111">You can see how invoking a task module from a tab and submitting the result of a task module works.</span></span>

## <a name="invoke-a-task-module-from-a-tab"></a><span data-ttu-id="3bc76-112">Appeler un module de tâche à partir d’un onglet</span><span class="sxs-lookup"><span data-stu-id="3bc76-112">Invoke a task module from a tab</span></span>

<span data-ttu-id="3bc76-113">Pour appeler un module de tâche à partir d’un onglet, utilisez la transmission d’un objet `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) et d’une fonction de `submitHandler` rappel facultative.</span><span class="sxs-lookup"><span data-stu-id="3bc76-113">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="3bc76-114">Deux cas sont à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="3bc76-114">There are two cases to consider:</span></span>

* <span data-ttu-id="3bc76-115">La valeur de `TaskInfo.url` est définie sur une URL.</span><span class="sxs-lookup"><span data-stu-id="3bc76-115">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="3bc76-116">La fenêtre du module de tâche s’affiche `TaskModule.url` et est chargée en tant `<iframe>` qu’intérieur.</span><span class="sxs-lookup"><span data-stu-id="3bc76-116">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="3bc76-117">JavaScript sur cette page appelle `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="3bc76-117">JavaScript on that page calls `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="3bc76-118">S’il existe une fonction sur la page et qu’il existe une erreur lors de l’appel, alors est appelé avec la chaîne d’erreur indiquant `submitHandler` `microsoftTeams.tasks.startTask()` la `submitHandler` `err` même.</span><span class="sxs-lookup"><span data-stu-id="3bc76-118">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the same.</span></span> <span data-ttu-id="3bc76-119">Pour plus d’informations, consultez les [erreurs d’appel du module de tâche.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="3bc76-119">For more information, see [task module invocation errors](#task-module-invocation-errors).</span></span>
* <span data-ttu-id="3bc76-120">La valeur est `taskInfo.card` le [JSON d’une carte adaptative.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="3bc76-120">The value of `taskInfo.card` is the [JSON for an Adaptive Card](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="3bc76-121">Il n’existe aucune fonction JavaScript à appeler lorsque l’utilisateur ferme ou appuie sur un `submitHandler` bouton de la carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="3bc76-121">There is no JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive Card.</span></span> <span data-ttu-id="3bc76-122">La seule façon de recevoir ce que l’utilisateur a entré consiste à transmettre le résultat à un bot.</span><span class="sxs-lookup"><span data-stu-id="3bc76-122">The only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="3bc76-123">Pour utiliser un module de tâche carte adaptative à partir d’un onglet, votre application doit inclure un bot pour obtenir une réponse de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3bc76-123">To use an Adaptive Card task module from a tab, your app must include a bot to get any response from the user.</span></span>

<span data-ttu-id="3bc76-124">La section suivante donne un exemple d’facturation d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="3bc76-124">The next section gives an example of invoking a task module.</span></span>

## <a name="example-of-invoking-a-task-module"></a><span data-ttu-id="3bc76-125">Exemple d’facturation d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="3bc76-125">Example of invoking a task module</span></span>

<span data-ttu-id="3bc76-126">L’image suivante affiche le module de tâche :</span><span class="sxs-lookup"><span data-stu-id="3bc76-126">The following image displays the task module:</span></span>

![Module de tâche - Formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="3bc76-128">Le code suivant est adapté à partir de [l’exemple de module de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):</span><span class="sxs-lookup"><span data-stu-id="3bc76-128">The following code is adapted from [the task module sample](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):</span></span>

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

<span data-ttu-id="3bc76-129">La méthode est très simple et elle fait écho à la valeur de la console ou `submitHandler` à celle de la `err` `result` console.</span><span class="sxs-lookup"><span data-stu-id="3bc76-129">The `submitHandler` is very simple and it echoes the value of `err` or `result` to the console.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="3bc76-130">Envoyer le résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="3bc76-130">Submit the result of a task module</span></span>

<span data-ttu-id="3bc76-131">La `submitHandler` fonction réside dans la page web et est utilisée avec `TaskInfo.url` `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="3bc76-131">The `submitHandler` function resides in the `TaskInfo.url` web page and is used with `TaskInfo.url`.</span></span> <span data-ttu-id="3bc76-132">En cas d’erreur lors de l’appel du module de tâche, votre fonction est immédiatement invoquée avec une chaîne indiquant quelle `submitHandler` erreur s’est `err` [produite.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="3bc76-132">If there is an error when invoking the task module, your `submitHandler` function is immediately invoked with an `err` string indicating what [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="3bc76-133">La fonction est également appelée avec une chaîne lorsque l’utilisateur sélectionne X en haut à droite du module de tâche `submitHandler` `err` pour le fermer.</span><span class="sxs-lookup"><span data-stu-id="3bc76-133">The `submitHandler` function is also called with an `err` string when the user selects X at the upper right of the task module to close it.</span></span>

<span data-ttu-id="3bc76-134">S’il n’y a aucune erreur d’appel et que l’utilisateur ne sélectionne pas X pour le faire disparaître, l’utilisateur choisit un bouton lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="3bc76-134">If there is no invocation error and the user does not select X to dismiss it, the user chooses a button when finished.</span></span> <span data-ttu-id="3bc76-135">Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâche, les sections suivantes fournissent des détails sur ce qui se produit.</span><span class="sxs-lookup"><span data-stu-id="3bc76-135">Depending on whether it is a URL or an Adaptive Card in the task module, the next sections provide details on what occurs.</span></span>

### <a name="html-or-javascript-taskinfourl"></a><span data-ttu-id="3bc76-136">HTML ou JavaScript `TaskInfo.url`</span><span class="sxs-lookup"><span data-stu-id="3bc76-136">HTML or JavaScript `TaskInfo.url`</span></span>

<span data-ttu-id="3bc76-137">Après avoir validé les entrées de l’utilisateur, appelez la fonction `microsoftTeams.tasks.submitTask()` SDK appelée `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="3bc76-137">After validating the user's inputs, call the `microsoftTeams.tasks.submitTask()` SDK function referred to as `submitTask()`.</span></span> <span data-ttu-id="3bc76-138">Appelez sans paramètre si vous souhaitez simplement Teams `submitTask()` le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="3bc76-138">Call `submitTask()` without any parameters if you just want Teams to close the task module.</span></span> <span data-ttu-id="3bc76-139">Vous pouvez transmettre un objet ou une chaîne à votre `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="3bc76-139">You can pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="3bc76-140">Passez votre résultat en tant que premier paramètre.</span><span class="sxs-lookup"><span data-stu-id="3bc76-140">Pass your result as the first parameter.</span></span> <span data-ttu-id="3bc76-141">Teams appelle où se trouve et `submitHandler` `err` est `null` `result` l’objet ou `submitTask()` la chaîne que vous avez transmis à .</span><span class="sxs-lookup"><span data-stu-id="3bc76-141">Teams invokes `submitHandler` where `err` is `null` and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="3bc76-142">Si vous `submitTask()` appelez avec `result` un paramètre, vous devez transmettre un ou `appId` plusieurs tableaux de `appId` chaînes.</span><span class="sxs-lookup"><span data-stu-id="3bc76-142">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="3bc76-143">Cela permet Teams vérifier que l’application envoyant le résultat est identique au module de tâche appelé.</span><span class="sxs-lookup"><span data-stu-id="3bc76-143">This permits Teams to validate that the app sending the result is same as the invoked task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="3bc76-144">Carte adaptative `TaskInfo.card`</span><span class="sxs-lookup"><span data-stu-id="3bc76-144">Adaptive Card `TaskInfo.card`</span></span>

<span data-ttu-id="3bc76-145">Lorsque vous voquez le module de tâche avec un bouton et que l’utilisateur sélectionne un bouton, les valeurs de la carte sont renvoyées en tant que `submitHandler` `Action.Submit` valeur de `result` .</span><span class="sxs-lookup"><span data-stu-id="3bc76-145">When you invoke the task module with a `submitHandler` and the user selects an `Action.Submit` button, the values in the card are returned as the value of `result`.</span></span> <span data-ttu-id="3bc76-146">Si l’utilisateur sélectionne la touche Échap ou X en haut à droite, `err` est renvoyé à la place.</span><span class="sxs-lookup"><span data-stu-id="3bc76-146">If the user selects the Esc key or X at the top right, `err` is returned instead.</span></span> <span data-ttu-id="3bc76-147">Si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure le bot comme valeur `appId` `completionBotId` dans `TaskInfo` l’objet.</span><span class="sxs-lookup"><span data-stu-id="3bc76-147">If your app contains a bot in addition to a tab, you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="3bc76-148">Le corps de la carte adaptative tel qu’il est rempli par l’utilisateur est envoyé au bot à l’aide d’un message lorsque l’utilisateur `task/submit invoke` sélectionne un `Action.Submit` bouton.</span><span class="sxs-lookup"><span data-stu-id="3bc76-148">The Adaptive Card body as filled in by the user is sent to the bot using a `task/submit invoke` message when the user selects an `Action.Submit` button.</span></span> <span data-ttu-id="3bc76-149">Le schéma de l’objet que vous recevez est très similaire au schéma que vous recevez pour les messages de tâche/extraction et de [tâche/soumission.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="3bc76-149">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="3bc76-150">La seule différence est que le schéma de l’objet JSON est un objet de carte adaptative par opposition à un objet contenant un objet De carte adaptative comme lorsque les cartes adaptatives sont utilisées avec des [bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="3bc76-150">The only difference is that the schema of the JSON object is an Adaptive Card object as opposed to an object containing an Adaptive Card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

<span data-ttu-id="3bc76-151">La section suivante donne un exemple d’envoi du résultat d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="3bc76-151">The next section gives an example of submitting the result of a task module.</span></span>

## <a name="example-of-submitting-the-result-of-a-task-module"></a><span data-ttu-id="3bc76-152">Exemple d’envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="3bc76-152">Example of submitting the result of a task module</span></span>

<span data-ttu-id="3bc76-153">Pour plus d’informations, voir le [formulaire HTML dans le module de tâche.](#example-of-invoking-a-task-module)</span><span class="sxs-lookup"><span data-stu-id="3bc76-153">For more information, see the [HTML form in the task module](#example-of-invoking-a-task-module).</span></span> <span data-ttu-id="3bc76-154">Le code suivant donne un exemple de l’endroit où le formulaire est défini :</span><span class="sxs-lookup"><span data-stu-id="3bc76-154">The following code gives an example of where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="3bc76-155">Il existe cinq champs sur ce formulaire, mais pour cet exemple, seules trois valeurs sont requises, `name` `email` et `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="3bc76-155">There are five fields on this form but for this example only three values are required, `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="3bc76-156">Le code suivant donne un exemple de la `validateForm()` fonction qui appelle `submitTask()` :</span><span class="sxs-lookup"><span data-stu-id="3bc76-156">The following code gives an example of the `validateForm()` function that calls `submitTask()`:</span></span>

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

<span data-ttu-id="3bc76-157">La section suivante fournit des problèmes d’appel de module de tâche et leurs messages d’erreur.</span><span class="sxs-lookup"><span data-stu-id="3bc76-157">The next section provides task module invocation problems and their error messages.</span></span>

## <a name="task-module-invocation-errors"></a><span data-ttu-id="3bc76-158">Erreurs d’invocation de module de tâche</span><span class="sxs-lookup"><span data-stu-id="3bc76-158">Task module invocation errors</span></span>

<span data-ttu-id="3bc76-159">Le tableau suivant fournit les valeurs possibles qui `err` peuvent être reçues par votre `submitHandler` :</span><span class="sxs-lookup"><span data-stu-id="3bc76-159">The following table provides the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="3bc76-160">Problème</span><span class="sxs-lookup"><span data-stu-id="3bc76-160">Problem</span></span> | <span data-ttu-id="3bc76-161">Message d’erreur de la valeur `err`</span><span class="sxs-lookup"><span data-stu-id="3bc76-161">Error message that is value of `err`</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="3bc76-162">Valeurs pour les `TaskInfo.url` deux et ont été `TaskInfo.card` spécifiées.</span><span class="sxs-lookup"><span data-stu-id="3bc76-162">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="3bc76-163">Les valeurs de la carte et de l’URL ont été spécifiées.</span><span class="sxs-lookup"><span data-stu-id="3bc76-163">Values for both card and URL were specified.</span></span> <span data-ttu-id="3bc76-164">L’un ou l’autre, mais pas les deux, est autorisé.</span><span class="sxs-lookup"><span data-stu-id="3bc76-164">One or the other, but not both, are allowed.</span></span> |
| <span data-ttu-id="3bc76-165">Ni `TaskInfo.url` `TaskInfo.card` spécifié.</span><span class="sxs-lookup"><span data-stu-id="3bc76-165">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="3bc76-166">Vous devez spécifier une valeur pour la carte ou l’URL.</span><span class="sxs-lookup"><span data-stu-id="3bc76-166">You must specify a value for either card or URL.</span></span> |
| <span data-ttu-id="3bc76-167">Non `appId` valide .</span><span class="sxs-lookup"><span data-stu-id="3bc76-167">Invalid `appId`.</span></span> | <span data-ttu-id="3bc76-168">ID d’application non valide.</span><span class="sxs-lookup"><span data-stu-id="3bc76-168">Invalid app ID.</span></span> |
| <span data-ttu-id="3bc76-169">L’utilisateur a sélectionné le bouton X, le fermant.</span><span class="sxs-lookup"><span data-stu-id="3bc76-169">User selected X button, closing it.</span></span> | <span data-ttu-id="3bc76-170">L’utilisateur a annulé ou fermé le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="3bc76-170">User cancelled or closed the task module.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="3bc76-171">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="3bc76-171">Code sample</span></span>

|<span data-ttu-id="3bc76-172">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="3bc76-172">Sample name</span></span> | <span data-ttu-id="3bc76-173">Description</span><span class="sxs-lookup"><span data-stu-id="3bc76-173">Description</span></span> | <span data-ttu-id="3bc76-174">.NET</span><span class="sxs-lookup"><span data-stu-id="3bc76-174">.NET</span></span> | <span data-ttu-id="3bc76-175">Node.js</span><span class="sxs-lookup"><span data-stu-id="3bc76-175">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="3bc76-176">Exemples d’onglets de module de tâche et bots-V3</span><span class="sxs-lookup"><span data-stu-id="3bc76-176">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="3bc76-177">Exemples de création de modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="3bc76-177">Samples for creating task modules.</span></span> |[<span data-ttu-id="3bc76-178">View</span><span class="sxs-lookup"><span data-stu-id="3bc76-178">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="3bc76-179">View</span><span class="sxs-lookup"><span data-stu-id="3bc76-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="3bc76-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3bc76-180">See also</span></span>

[<span data-ttu-id="3bc76-181">Appeler et ignorer des modules de tâche</span><span class="sxs-lookup"><span data-stu-id="3bc76-181">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a><span data-ttu-id="3bc76-182">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="3bc76-182">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3bc76-183">Utilisation de modules de tâche à partir de bots</span><span class="sxs-lookup"><span data-stu-id="3bc76-183">Using task modules from bots</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
