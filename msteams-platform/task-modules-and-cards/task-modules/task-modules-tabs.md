---
title: Utilisation des modules de tâche dans les onglets Microsoft Teams
description: Explique comment appeler des modules de tâche à partir des onglets Teams à l’aide du SDK client Microsoft Teams.
keywords: sdk client des onglets des modules de tâche teams
ms.openlocfilehash: 3f1da4d5eec31638d69adc01a45831534d015f41
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449555"
---
# <a name="using-task-modules-in-tabs"></a>Utilisation des modules de tâche dans les onglets

L’ajout d’un module de tâche à votre onglet peut grandement simplifier l’expérience de votre utilisateur pour les flux de travail qui nécessitent une entrée de données. Les modules de tâche vous permettent de collecter leurs entrées dans une fenêtre popup teams. La modification des cartes planificateur en est un bon exemple . vous pouvez utiliser des modules de tâche pour créer une expérience similaire.

Pour prendre en charge la fonctionnalité de module de tâche, deux nouvelles fonctions ont été ajoutées au [SDK client Microsoft Teams](/javascript/api/overview/msteams-client):

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

Voyons comment chacun d’eux fonctionne.

## <a name="invoking-a-task-module-from-a-tab"></a>Facturation d’un module de tâche à partir d’un onglet

Pour appeler un module de tâche à partir d’un onglet, utilisez la transmission d’un objet `microsoftTeams.tasks.startTask()` [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) et d’une fonction de `submitHandler` rappel facultative. Comme décrit précédemment, deux cas sont à prendre en compte :

1. La valeur est `TaskInfo.url` définie sur une URL. La fenêtre du module de tâche s’affiche `TaskModule.url` et est chargée en tant `<iframe>` qu’intérieur. JavaScript sur cette page doit appeler `microsoftTeams.initialize()` . S’il existe une fonction sur la page et qu’il existe une erreur lors de l’appel, alors est appelé avec la chaîne d’erreur définie indiquant l’erreur comme décrit `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [ci-dessous](#task-module-invocation-errors).
1. La valeur est `taskInfo.card` le [JSON d’une carte adaptative.](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment) Dans ce cas, il n’existe évidemment pas de fonction JavaScript à appeler lorsque l’utilisateur ferme ou appuie sur un bouton de la carte adaptative ; le seul moyen de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un `submitHandler` bot. Pour utiliser un module de tâche de carte adaptative à partir d’un onglet, votre application doit inclure un bot pour obtenir des informations auprès de l’utilisateur. Ceci est expliqué ci-dessous.

## <a name="example-invoking-a-task-module"></a>Exemple : facturation d’un module de tâche

Le code ci-dessous est adapté à partir de [l’exemple de module de tâche.](~/task-modules-and-cards/what-are-task-modules.md#code-sample) Voici à quoi ressemble le module de tâche :

![Module de tâche - Formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

L’exemple est très simple ; il fait simplement écho à la `submitHandler` valeur de la console ou à celle de la console `err` `result` :

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

## <a name="submitting-the-result-of-a-task-module"></a>Envoi du résultat d’un module de tâche

La `submitHandler` fonction est utilisée avec `TaskInfo.url` . La `submitHandler` fonction réside dans la page `TaskInfo.url` web. En cas d’erreur lors de l’appel du module de tâche, votre fonction est immédiatement invoquée avec une chaîne indiquant quelle erreur s’est `submitHandler` `err` [produite.](#task-module-invocation-errors) La fonction est également appelée avec une chaîne lorsque l’utilisateur appuie sur le X en haut `submitHandler` à droite du module de `err` tâche.

S’il n’y a aucune erreur d’appel et que l’utilisateur n’appuie pas sur X pour le faire disparaître, l’utilisateur appuie sur un bouton lorsque vous avez terminé. Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâche, voici ce qui se produit :

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

Une fois que vous avez validé ce que l’utilisateur a entré, vous appelez la fonction SDK (appelée ci-après à des fins de `microsoftTeams.tasks.submitTask()` `submitTask()` lisibilité). Vous pouvez appeler sans paramètre si vous souhaitez simplement que Teams ferme le module de tâche, mais la plupart du temps vous souhaiterez passer un objet ou une chaîne `submitTask()` à votre `submitHandler` .

Passez votre résultat en tant que premier paramètre. Teams appelle où `submitHandler` `err` se `null` trouveront et seront `result` l’objet/chaîne que vous avez transmis à `submitTask()` . Si vous appelez avec un paramètre, vous devez transmettre un ou plusieurs tableaux de chaînes : cela permet à Teams de valider que l’application envoyant le résultat est la même que celle qui a appelé le module de `submitTask()` `result`  `appId` `appId` tâche.

### <a name="adaptive-card-taskinfocard"></a>Carte adaptative ( `TaskInfo.card` )

Si vous avez appelé le module de tâche avec un , lorsque l’utilisateur appuie sur un bouton, les valeurs de la carte sont renvoyées en tant que `submitHandler` `Action.Submit` valeur de `result` . Si l’utilisateur appuie sur le bouton Échap ou appuie sur le X, `err` il est renvoyé à la place. Par ailleurs, si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure le bot comme valeur `appId` `completionBotId` dans `TaskInfo` l’objet. Le corps de la carte adaptative (tel que rempli par l’utilisateur) est envoyé au bot via un message lorsque l’utilisateur `task/submit invoke` appuie sur un `Action.Submit` bouton. Le schéma de l’objet que vous recevez est très similaire au schéma que vous recevez pour les [messages de tâche/extraction](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)et de tâche/soumission ; La seule différence est que le schéma de l’objet JSON est  un objet de carte adaptative par opposition à un objet contenant un objet de carte adaptative comme lorsque des cartes adaptatives sont utilisées avec des [bots.](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)

## <a name="example-submitting-the-result-of-a-task-module"></a>Exemple : envoi du résultat d’un module de tâche

Rappelez le [formulaire dans le module de tâche ci-dessus](#example-invoking-a-task-module) avec un formulaire HTML. C’est ici que le formulaire est défini :

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Il existe cinq champs sur ce formulaire, mais nous nous intéressent uniquement aux valeurs de trois d’entre eux pour cet exemple : `name` `email` , et `favoriteBook` .

Voici la fonction `validateForm()` qui appelle `submitTask()` :

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

## <a name="task-module-invocation-errors"></a>Erreurs d’invocation de module de tâche

Voici les valeurs possibles `err` qui peuvent être reçues par votre `submitHandler` :

| Problème | Message d’erreur (valeur `err` de ) |
| ------- | ------------------------------ |
| Valeurs pour les `TaskInfo.url` deux et ont été `TaskInfo.card` spécifiées. | « Les valeurs de la carte et de l’URL ont été spécifiées. L’un ou l’autre, mais pas les deux, est autorisé. » |
| Ni `TaskInfo.url` `TaskInfo.card` spécifié. | « Vous devez spécifier une valeur pour la carte ou l’URL. » |
| Non `appId` valide . | « AppId non valide. » |
| L’utilisateur a enfoncé le bouton X, le fermant. | « L’utilisateur a annulé/fermé le module de tâche. » |
