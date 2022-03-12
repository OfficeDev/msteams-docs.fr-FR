---
title: Utiliser des modules de tâche dans Microsoft Teams onglets
description: Explique comment appeler des modules de tâche à partir Teams onglets et comment envoyer son résultat à l’aide du SDK Microsoft Teams client. Il inclut des exemples de code.
ms.localizationpriority: medium
ms.topic: how-to
keywords: sdk client des onglets des modules de tâche teams
ms.openlocfilehash: 43b58a4f8ec1176c2d931f130a33c6610a078187
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453641"
---
# <a name="use-task-modules-in-tabs"></a>Utiliser des modules de tâche dans les onglets

Ajoutez un module de tâche à votre onglet pour simplifier l’expérience utilisateur pour les flux de travail qui nécessitent une entrée de données. Les modules de tâche vous permettent de collecter leurs entrées dans une fenêtre Teams-Aware Microsoft. La modification des cartes planificateur en est un bon exemple. Vous pouvez utiliser des modules de tâche pour créer une expérience similaire.

Pour prendre en charge la fonctionnalité de module de tâche, deux nouvelles fonctions sont ajoutées [au SDK Teams client.](/javascript/api/overview/msteams-client) Le code suivant montre un exemple de ces deux fonctions :

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

Vous pouvez voir comment l’utilisation d’un module de tâche à partir d’un onglet et l’envoi du résultat d’un module de tâche fonctionnent.

## <a name="invoke-a-task-module-from-a-tab"></a>Appeler un module de tâche à partir d’un onglet

Pour appeler un module de tâche à partir d’un onglet, utilisez `microsoftTeams.tasks.startTask()` la transmission d’un objet [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) et d’une fonction de `submitHandler` rappel facultative. Deux cas sont à prendre en compte :

* La valeur est `TaskInfo.url` définie sur une URL. La fenêtre du module de tâche s’affiche `TaskModule.url` et est chargée en tant qu’intérieur `<iframe>` . JavaScript sur cette page appelle `microsoftTeams.initialize()`. S’il existe une `submitHandler` fonction sur la page `microsoftTeams.tasks.startTask()`et qu’une erreur s’affiche lors de l’appel, `err` `submitHandler` elle est alors invoquée avec la chaîne d’erreur indiquant la même. Pour plus d’informations, voir [erreurs d’appel du module de tâche](#task-module-invocation-errors).
* La valeur est `taskInfo.card` le [JSON d’une carte adaptative](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Il n’existe aucune fonction JavaScript `submitHandler` à appeler lorsque l’utilisateur ferme ou appuie sur un bouton de la carte adaptative. La seule façon de recevoir ce que l’utilisateur a entré consiste à transmettre le résultat à un bot. Pour utiliser un module de tâche carte adaptative à partir d’un onglet, votre application doit inclure un bot pour obtenir une réponse de l’utilisateur.

La section suivante donne un exemple d’facturation d’un module de tâche.

## <a name="example-of-invoking-a-task-module"></a>Exemple d’facturation d’un module de tâche

L’image suivante affiche le module de tâche :

![Module de tâche - Formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

Le code suivant est adapté à partir de [l’exemple de module de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample) :

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

L’exemple `submitHandler` est très simple et il fait écho à la valeur de `err` la `result` console ou à celle de celle-ci.

## <a name="submit-the-result-of-a-task-module"></a>Envoyer le résultat d’un module de tâche

La `submitHandler` fonction réside dans la `TaskInfo.url` page web et est utilisée avec `TaskInfo.url`. En cas d’erreur lors de l’appel du module de tâche, `submitHandler` `err` votre fonction est immédiatement invoquée avec une chaîne indiquant quelle [erreur s’est produite](#task-module-invocation-errors). La `submitHandler` fonction est également appelée avec une `err` chaîne lorsque l’utilisateur sélectionne X en haut à droite du module de tâche pour le fermer.

S’il n’y a aucune erreur d’appel et que l’utilisateur ne sélectionne pas X pour le faire disparaître, l’utilisateur choisit un bouton lorsque vous avez terminé. Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâche, les sections suivantes fournissent des détails sur ce qui se produit.

### <a name="html-or-javascript-taskinfourl"></a>HTML ou JavaScript `TaskInfo.url`

Après avoir validé les entrées de l’utilisateur, appelez `microsoftTeams.tasks.submitTask()` la fonction SDK `submitTask()`appelée . Appelez `submitTask()` sans paramètre si vous souhaitez simplement Teams le module de tâche. Vous pouvez transmettre un objet ou une chaîne à votre `submitHandler`.

Passez votre résultat en tant que premier paramètre. Teams appelle où `submitHandler` se `null` `result` trouve `err` et est l’objet ou la chaîne que vous avez transmis à `submitTask()`. Si vous appelez `submitTask()` avec un `result` paramètre, vous devez transmettre un `appId` ou plusieurs tableaux de chaînes `appId` . Cela permet Teams vérifier que l’application envoyant le résultat est identique au module de tâche appelé.

### <a name="adaptive-card-taskinfocard"></a>Carte adaptative `TaskInfo.card`

Lorsque vous voquez le module de tâche avec un `submitHandler` bouton et que l’utilisateur sélectionne un bouton, les valeurs `Action.Submit` de la carte sont renvoyées en tant que valeur de `result`. Si l’utilisateur sélectionne la touche Échap ou X en haut à droite, `err` est renvoyé à la place. Si votre application contient un bot en plus d’un onglet, `appId` vous pouvez simplement inclure le bot `completionBotId` comme valeur dans l’objet `TaskInfo` . Le corps de la carte adaptative tel qu’il est rempli par l’utilisateur est envoyé au bot `task/submit invoke` à l’aide d’un message lorsque l’utilisateur sélectionne un `Action.Submit` bouton. Le schéma de l’objet que vous recevez est très similaire au schéma que vous recevez pour les [messages de tâche/extraction et de tâche/soumission](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). La seule différence est que le schéma de l’objet JSON est un objet de carte adaptative par opposition à un objet contenant un objet De carte adaptative comme lorsque les cartes adaptatives sont utilisées avec des [bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

La section suivante donne un exemple d’envoi du résultat d’un module de tâche.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Exemple d’envoi du résultat d’un module de tâche

Pour plus d’informations, voir le [formulaire HTML dans le module de tâche](#example-of-invoking-a-task-module). Le code suivant donne un exemple de l’endroit où le formulaire est défini :

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Il existe cinq champs sur ce formulaire, mais pour cet exemple, seules trois valeurs sont requises, `name`et `email``favoriteBook`.

Le code suivant donne un exemple de la `validateForm()` fonction qui appelle `submitTask()`:

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

La section suivante fournit des problèmes d’appel de module de tâche et leurs messages d’erreur.

## <a name="task-module-invocation-errors"></a>Erreurs d’invocation de module de tâche

Le tableau suivant fournit les valeurs `err` possibles qui peuvent être reçues par votre :`submitHandler`

| Problème | Message d’erreur de la valeur `err` |
| ------- | ------------------------------ |
| Valeurs pour les deux `TaskInfo.url` et `TaskInfo.card` ont été spécifiées. | Les valeurs de la carte et de l’URL ont été spécifiées. L’un ou l’autre, mais pas les deux, est autorisé. |
| Ni `TaskInfo.url` spécifié `TaskInfo.card` . | Vous devez spécifier une valeur pour la carte ou l’URL. |
| Non valide `appId`. | ID d’application non valide. |
| L’utilisateur a sélectionné le bouton X, le fermant. | L’utilisateur a annulé ou fermé le module de tâche. |

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples d’onglets de module de tâche et bots-V3 | Exemples de création de modules de tâche. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utilisation de modules de tâche à partir de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Voir aussi

[Appeler et ignorer des modules de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
