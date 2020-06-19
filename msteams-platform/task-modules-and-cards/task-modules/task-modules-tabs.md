---
title: Utilisation des modules de tâches dans les onglets Microsoft teams
description: Explique comment appeler les modules de tâches à partir des onglets teams à l’aide du kit de développement logiciel client Microsoft Teams.
keywords: modules de tâches onglets teams du kit de développement logiciel client
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801067"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="1d95b-104">Utilisation des modules de tâches dans les onglets</span><span class="sxs-lookup"><span data-stu-id="1d95b-104">Using task modules in tabs</span></span>

<span data-ttu-id="1d95b-105">L’ajout d’un module de tâches à votre onglet permet de simplifier grandement l’expérience de vos utilisateurs pour tous les flux de travail qui nécessitent une entrée de données.</span><span class="sxs-lookup"><span data-stu-id="1d95b-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="1d95b-106">Les modules de tâches vous permettent de recueillir leurs informations dans un menu contextuel qui prend en charge Teams.</span><span class="sxs-lookup"><span data-stu-id="1d95b-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="1d95b-107">Par exemple, la modification des fiches du planificateur ; vous pouvez utiliser des modules de tâches pour créer une expérience similaire.</span><span class="sxs-lookup"><span data-stu-id="1d95b-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="1d95b-108">Pour prendre en charge la fonctionnalité de module de tâches, deux nouvelles fonctions ont été ajoutées au [Kit de développement logiciel client Microsoft teams](/javascript/api/overview/msteams-client):</span><span class="sxs-lookup"><span data-stu-id="1d95b-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="1d95b-109">Voyons comment chacun d’eux fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1d95b-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="1d95b-110">Appel d’un module de tâches à partir d’un onglet</span><span class="sxs-lookup"><span data-stu-id="1d95b-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="1d95b-111">Pour appeler un module de tâches à partir d’un onglet utilisé pour `microsoftTeams.tasks.startTask()` transmettre un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) et une `submitHandler` fonction de rappel facultative.</span><span class="sxs-lookup"><span data-stu-id="1d95b-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="1d95b-112">Comme décrit précédemment, deux cas doivent être pris en compte :</span><span class="sxs-lookup"><span data-stu-id="1d95b-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="1d95b-113">La valeur de `TaskInfo.url` est définie sur une URL.</span><span class="sxs-lookup"><span data-stu-id="1d95b-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="1d95b-114">La fenêtre du module tâches s’affiche et `TaskModule.url` est chargée en tant que telle `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="1d95b-115">JavaScript sur cette page doit appeler `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="1d95b-116">S’il y a une `submitHandler` fonction sur la page et qu’il y a une erreur lors de l’appel `microsoftTeams.tasks.startTask()` , `submitHandler` le est appelé avec `err` la chaîne d’erreur indiquant l’erreur comme décrit [ci-dessous](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="1d95b-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="1d95b-117">La valeur de `taskInfo.card` est le format [JSON pour une carte adaptative](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span><span class="sxs-lookup"><span data-stu-id="1d95b-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="1d95b-118">Dans ce cas, il n’y a évidemment pas de `submitHandler` fonction JavaScript à appeler lorsque l’utilisateur se ferme ou appuie sur un bouton de la carte adaptative ; la seule façon de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un bot.</span><span class="sxs-lookup"><span data-stu-id="1d95b-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="1d95b-119">Pour utiliser un module de tâches de carte adaptative à partir d’un onglet votre application doit inclure un bot pour récupérer toutes les informations de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1d95b-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="1d95b-120">Cela est expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1d95b-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="1d95b-121">Exemple : appel d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="1d95b-121">Example: Invoking a task module</span></span>

<span data-ttu-id="1d95b-122">Le code ci-dessous est adapté à partir de [l’exemple de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span><span class="sxs-lookup"><span data-stu-id="1d95b-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span></span> <span data-ttu-id="1d95b-123">Voici à quoi ressemble le module tâches :</span><span class="sxs-lookup"><span data-stu-id="1d95b-123">Here's what the task module looks like:</span></span>

![Module de tâche-formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="1d95b-125">Le `submitHandler` est très simple ; il renvoie simplement en écho la valeur de `err` ou `result` sur la console :</span><span class="sxs-lookup"><span data-stu-id="1d95b-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="1d95b-126">Envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="1d95b-126">Submitting the result of a task module</span></span>

<span data-ttu-id="1d95b-127">La `submitHandler` fonction est utilisée avec `TaskInfo.url` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="1d95b-128">La `submitHandler` fonction réside dans la `TaskInfo.url` page Web.</span><span class="sxs-lookup"><span data-stu-id="1d95b-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="1d95b-129">Si une erreur se produit lors de l’appel du module de tâches `submitHandler` , votre fonction est immédiatement appelée avec une `err` chaîne indiquant l' [erreur qui s’est produite](#task-module-invocation-errors).</span><span class="sxs-lookup"><span data-stu-id="1d95b-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="1d95b-130">La `submitHandler` fonction est également appelée avec une `err` chaîne lorsque l’utilisateur appuie sur le X dans le coin supérieur droit du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="1d95b-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="1d95b-131">S’il n’y a aucune erreur d’invocation et que l’utilisateur n’appuie pas sur X pour le masquer, l’utilisateur appuie sur un bouton lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="1d95b-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="1d95b-132">Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâches, voici ce qui se passe :</span><span class="sxs-lookup"><span data-stu-id="1d95b-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="1d95b-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="1d95b-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="1d95b-134">Une fois que vous avez validé ce que l’utilisateur a entré, appelez la `microsoftTeams.tasks.submitTask()` fonction SDK (désignée ci-après, à des `submitTask()` fins de lisibilité).</span><span class="sxs-lookup"><span data-stu-id="1d95b-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="1d95b-135">Vous pouvez appeler `submitTask()` sans aucun paramètre si vous souhaitez simplement que teams ferme le module de tâches, mais la plupart du temps, vous souhaiterez passer un objet ou une chaîne à votre `submitHandler` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="1d95b-136">Transmettez votre résultat en tant que premier paramètre.</span><span class="sxs-lookup"><span data-stu-id="1d95b-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="1d95b-137">Teams appellera `submitHandler` l’emplacement où sera `err` `null` `result` l’objet/la chaîne que vous avez passée `submitTask()` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="1d95b-138">Si vous appelez `submitTask()` avec un `result` paramètre, vous **devez** transmettre un `appId` tableau de chaînes ou un tableau `appId` : cela permet à teams de valider le fait que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâches.</span><span class="sxs-lookup"><span data-stu-id="1d95b-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="1d95b-139">Carte adaptative ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="1d95b-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="1d95b-140">Si vous avez appelé le module de tâches avec un `submitHandler` , lorsque l’utilisateur appuie sur un `Action.Submit` bouton, les valeurs de la carte sont renvoyées comme valeur de `result` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="1d95b-141">Si l’utilisateur appuie sur le bouton Échap ou appuie sur la touche X, il `err` est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="1d95b-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="1d95b-142">Par ailleurs, si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure le `appId` du bot comme valeur de `completionBotId` dans l' `TaskInfo` objet.</span><span class="sxs-lookup"><span data-stu-id="1d95b-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="1d95b-143">Le corps de la carte adaptative (tel qu’il est rempli par l’utilisateur) est envoyé au robot via un `task/submit invoke` message lorsque l’utilisateur appuie sur un `Action.Submit` bouton.</span><span class="sxs-lookup"><span data-stu-id="1d95b-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="1d95b-144">Le schéma de l’objet que vous recevez est très similaire au [schéma que vous recevez pour les messages tâche/extraction et tâche/envoi](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la seule différence réside dans le fait que le schéma de l’objet JSON est un objet de carte adaptative contrairement à un objet *contenant* un objet de carte adaptative, comme [lorsque des cartes adaptatives sont utilisées avec des bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span><span class="sxs-lookup"><span data-stu-id="1d95b-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="1d95b-145">Exemple : envoi du résultat d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="1d95b-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="1d95b-146">Rappelez le [formulaire dans le module de tâches ci-dessus](#example-invoking-a-task-module) avec un formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="1d95b-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="1d95b-147">C’est ici que le formulaire est défini :</span><span class="sxs-lookup"><span data-stu-id="1d95b-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="1d95b-148">Il y a cinq champs sur ce formulaire, mais nous les souhaitons uniquement dans les valeurs de trois d’entre eux pour cet exemple : `name` , `email` , et `favoriteBook` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="1d95b-149">Voici la `validateForm()` fonction qui appelle `submitTask()` :</span><span class="sxs-lookup"><span data-stu-id="1d95b-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="1d95b-150">Erreurs d’invocation de module de tâche</span><span class="sxs-lookup"><span data-stu-id="1d95b-150">Task module invocation errors</span></span>

<span data-ttu-id="1d95b-151">Voici les valeurs possibles pouvant `err` être reçues par votre `submitHandler` :</span><span class="sxs-lookup"><span data-stu-id="1d95b-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="1d95b-152">Problème</span><span class="sxs-lookup"><span data-stu-id="1d95b-152">Problem</span></span> | <span data-ttu-id="1d95b-153">Message d’erreur (valeur de `err` )</span><span class="sxs-lookup"><span data-stu-id="1d95b-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="1d95b-154">Valeurs pour les deux `TaskInfo.url` et `TaskInfo.card` spécifiés.</span><span class="sxs-lookup"><span data-stu-id="1d95b-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="1d95b-155">«Les valeurs de la carte et de l’URL ont été spécifiées.</span><span class="sxs-lookup"><span data-stu-id="1d95b-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="1d95b-156">L’un ou l’autre, mais pas les deux, sont autorisés. "</span><span class="sxs-lookup"><span data-stu-id="1d95b-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="1d95b-157">Ni `TaskInfo.url` ni `TaskInfo.card` spécifié.</span><span class="sxs-lookup"><span data-stu-id="1d95b-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="1d95b-158">"Vous devez spécifier une valeur pour l’une ou l’autre de ces cartes ou URL."</span><span class="sxs-lookup"><span data-stu-id="1d95b-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="1d95b-159">Non valide `appId` .</span><span class="sxs-lookup"><span data-stu-id="1d95b-159">Invalid `appId`.</span></span> | <span data-ttu-id="1d95b-160">« AppId non valide ».</span><span class="sxs-lookup"><span data-stu-id="1d95b-160">"Invalid appId."</span></span> |
| <span data-ttu-id="1d95b-161">Utilisateur a appuyé sur le bouton X, en le fermant.</span><span class="sxs-lookup"><span data-stu-id="1d95b-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="1d95b-162">« Utilisateur a annulé/fermé le module de tâches ».</span><span class="sxs-lookup"><span data-stu-id="1d95b-162">"User cancelled/closed the task module."</span></span> |
