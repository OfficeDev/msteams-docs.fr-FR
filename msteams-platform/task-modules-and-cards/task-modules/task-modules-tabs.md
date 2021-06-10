---
title: Utilisation des modules de tâche dans Microsoft Teams onglets
description: Explique comment appeler des modules de tâche à partir Teams onglets à l’aide Microsoft Teams client SDK
localization_priority: Normal
ms.topic: how-to
keywords: modules de tâche teams tabs client sdk
ms.openlocfilehash: 5e85fd0662b8a15d6b98d9c2d2dfa5137b05fa39
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019523"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="a192f-104">Utilisation des modules de tâche dans les onglets</span><span class="sxs-lookup"><span data-stu-id="a192f-104">Using task modules in tabs</span></span>

<span data-ttu-id="a192f-105">L’ajout d’un module de tâche à votre onglet peut grandement simplifier l’expérience de votre utilisateur pour les flux de travail qui nécessitent une entrée de données.</span><span class="sxs-lookup"><span data-stu-id="a192f-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="a192f-106">Les modules de tâche vous permettent de collecter leurs entrées dans une fenêtre Teams fenêtre popup.</span><span class="sxs-lookup"><span data-stu-id="a192f-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="a192f-107">La modification des cartes planificateur en est un bon exemple . vous pouvez utiliser des modules de tâche pour créer une expérience similaire.</span><span class="sxs-lookup"><span data-stu-id="a192f-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="a192f-108">Pour prendre en charge la fonctionnalité de module de tâche, deux nouvelles fonctions ont été ajoutées [au SDK Microsoft Teams client :](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="a192f-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="a192f-109">Voyons comment chacun d’eux fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a192f-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="a192f-110">Facturation d’un module de tâche à partir d’un onglet</span><span class="sxs-lookup"><span data-stu-id="a192f-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="a192f-111">Pour appeler un module de tâche à partir d’un onglet, utilisez la transmission d’un objet `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) et d’une fonction de `submitHandler` rappel facultative.</span><span class="sxs-lookup"><span data-stu-id="a192f-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="a192f-112">Comme décrit précédemment, deux cas sont à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="a192f-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="a192f-113">La valeur est `TaskInfo.url` définie sur une URL.</span><span class="sxs-lookup"><span data-stu-id="a192f-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="a192f-114">La fenêtre du module de tâche s’affiche `TaskModule.url` et est chargée en tant `<iframe>` qu’intérieur.</span><span class="sxs-lookup"><span data-stu-id="a192f-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="a192f-115">JavaScript sur cette page doit appeler `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="a192f-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="a192f-116">S’il existe une fonction sur la page et qu’il existe une erreur lors de l’appel, alors est appelé avec la chaîne d’erreur définie indiquant l’erreur comme décrit `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [ci-dessous](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="a192f-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="a192f-117">La valeur est `taskInfo.card` le [JSON d’une carte adaptative.](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="a192f-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="a192f-118">Dans ce cas, il n’existe évidemment pas de fonction JavaScript à appeler lorsque l’utilisateur ferme ou appuie sur un bouton de la carte adaptative ; le seul moyen de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un `submitHandler` bot.</span><span class="sxs-lookup"><span data-stu-id="a192f-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="a192f-119">Pour utiliser un module de tâche de carte adaptative à partir d’un onglet, votre application doit inclure un bot pour obtenir des informations auprès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a192f-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="a192f-120">Ceci est expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a192f-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="a192f-121">Exemple : facturation d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="a192f-121">Example: Invoking a task module</span></span>

<span data-ttu-id="a192f-122">Le code ci-dessous est adapté à partir de [l’exemple de module de tâche.](~/task-modules-and-cards/what-are-task-modules.md#code-sample)</span><span class="sxs-lookup"><span data-stu-id="a192f-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span></span> <span data-ttu-id="a192f-123">Voici à quoi ressemble le module de tâche :</span><span class="sxs-lookup"><span data-stu-id="a192f-123">Here's what the task module looks like:</span></span>

![Module de tâche - Formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="a192f-125">L’exemple est très simple ; il fait simplement écho à la `submitHandler` valeur de la console ou à celle de la console `err` `result` :</span><span class="sxs-lookup"><span data-stu-id="a192f-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="a192f-126">Envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="a192f-126">Submitting the result of a task module</span></span>

<span data-ttu-id="a192f-127">La `submitHandler` fonction est utilisée avec `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="a192f-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="a192f-128">La `submitHandler` fonction réside dans la page `TaskInfo.url` web.</span><span class="sxs-lookup"><span data-stu-id="a192f-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="a192f-129">En cas d’erreur lors de l’appel du module de tâche, votre fonction est immédiatement invoquée avec une chaîne indiquant quelle erreur s’est `submitHandler` `err` [produite.](#task-module-invocation-errors)</span><span class="sxs-lookup"><span data-stu-id="a192f-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="a192f-130">La fonction est également appelée avec une chaîne lorsque l’utilisateur appuie sur le X en haut `submitHandler` à droite du module de `err` tâche.</span><span class="sxs-lookup"><span data-stu-id="a192f-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="a192f-131">S’il n’y a aucune erreur d’appel et que l’utilisateur n’appuie pas sur X pour le faire disparaître, l’utilisateur appuie sur un bouton lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="a192f-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="a192f-132">Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâche, voici ce qui se produit :</span><span class="sxs-lookup"><span data-stu-id="a192f-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="a192f-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="a192f-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="a192f-134">Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK (appelée ci-après à des fins de `microsoftTeams.tasks.submitTask()` `submitTask()` lisibilité).</span><span class="sxs-lookup"><span data-stu-id="a192f-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="a192f-135">Vous pouvez appeler sans paramètre si vous souhaitez simplement Teams fermer le module de tâche, mais la plupart du temps vous souhaiterez passer un objet ou une chaîne à `submitTask()` votre `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="a192f-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="a192f-136">Passez votre résultat en tant que premier paramètre.</span><span class="sxs-lookup"><span data-stu-id="a192f-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="a192f-137">Teams appelle où `submitHandler` `err` se `null` trouveront et `result` seront l’objet/chaîne que vous avez transmis à `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="a192f-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="a192f-138">Si vous appelez avec un paramètre, vous devez transmettre un ou plusieurs tableaux de chaînes : cela permet à Teams de vérifier que l’application qui envoie le résultat est la même que celle qui a appelé le module de `submitTask()` `result`  `appId` `appId` tâche.</span><span class="sxs-lookup"><span data-stu-id="a192f-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="a192f-139">Carte adaptative ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="a192f-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="a192f-140">Si vous avez appelé le module de tâche avec un , lorsque l’utilisateur appuie sur un bouton, les valeurs de la carte sont renvoyées en tant que `submitHandler` `Action.Submit` valeur de `result` .</span><span class="sxs-lookup"><span data-stu-id="a192f-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="a192f-141">Si l’utilisateur appuie sur le bouton Échap ou appuie sur le X, `err` il est renvoyé à la place.</span><span class="sxs-lookup"><span data-stu-id="a192f-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="a192f-142">Par ailleurs, si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure le bot comme valeur `appId` `completionBotId` dans `TaskInfo` l’objet.</span><span class="sxs-lookup"><span data-stu-id="a192f-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="a192f-143">Le corps de la carte adaptative (tel que rempli par l’utilisateur) est envoyé au bot via un message lorsque l’utilisateur `task/submit invoke` appuie sur un `Action.Submit` bouton.</span><span class="sxs-lookup"><span data-stu-id="a192f-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="a192f-144">Le schéma de l’objet que vous recevez est très similaire au schéma que vous recevez pour les [messages de tâche/extraction](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)et de tâche/soumission ; La seule différence est que le schéma de l’objet JSON est  un objet de carte adaptative par opposition à un objet contenant un objet de carte adaptative comme lorsque des cartes adaptatives sont utilisées avec des [bots.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="a192f-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="a192f-145">Exemple : envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="a192f-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="a192f-146">Rappelez le [formulaire dans le module de tâche ci-dessus](#example-invoking-a-task-module) avec un formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="a192f-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="a192f-147">C’est ici que le formulaire est défini :</span><span class="sxs-lookup"><span data-stu-id="a192f-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="a192f-148">Il existe cinq champs sur ce formulaire, mais nous nous intéressent uniquement aux valeurs de trois d’entre eux pour cet exemple : `name` `email` , et `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="a192f-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="a192f-149">Voici la fonction `validateForm()` qui appelle `submitTask()` :</span><span class="sxs-lookup"><span data-stu-id="a192f-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="a192f-150">Erreurs d’invocation de module de tâche</span><span class="sxs-lookup"><span data-stu-id="a192f-150">Task module invocation errors</span></span>

<span data-ttu-id="a192f-151">Voici les valeurs possibles `err` qui peuvent être reçues par votre `submitHandler` :</span><span class="sxs-lookup"><span data-stu-id="a192f-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="a192f-152">Problème</span><span class="sxs-lookup"><span data-stu-id="a192f-152">Problem</span></span> | <span data-ttu-id="a192f-153">Message d’erreur (valeur `err` de )</span><span class="sxs-lookup"><span data-stu-id="a192f-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="a192f-154">Valeurs pour les `TaskInfo.url` deux et ont été `TaskInfo.card` spécifiées.</span><span class="sxs-lookup"><span data-stu-id="a192f-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="a192f-155">« Les valeurs de la carte et de l’URL ont été spécifiées.</span><span class="sxs-lookup"><span data-stu-id="a192f-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="a192f-156">L’un ou l’autre, mais pas les deux, est autorisé. »</span><span class="sxs-lookup"><span data-stu-id="a192f-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="a192f-157">Ni `TaskInfo.url` `TaskInfo.card` spécifié.</span><span class="sxs-lookup"><span data-stu-id="a192f-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="a192f-158">« Vous devez spécifier une valeur pour la carte ou l’URL. »</span><span class="sxs-lookup"><span data-stu-id="a192f-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="a192f-159">Non `appId` valide .</span><span class="sxs-lookup"><span data-stu-id="a192f-159">Invalid `appId`.</span></span> | <span data-ttu-id="a192f-160">« AppId non valide. »</span><span class="sxs-lookup"><span data-stu-id="a192f-160">"Invalid appId."</span></span> |
| <span data-ttu-id="a192f-161">L’utilisateur a enfoncé le bouton X, le fermant.</span><span class="sxs-lookup"><span data-stu-id="a192f-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="a192f-162">« L’utilisateur a annulé/fermé le module de tâche. »</span><span class="sxs-lookup"><span data-stu-id="a192f-162">"User cancelled/closed the task module."</span></span> |
