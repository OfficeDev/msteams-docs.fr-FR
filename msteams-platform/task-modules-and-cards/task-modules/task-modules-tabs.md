---
title: Utilisation des modules de tâches dans les onglets Microsoft teams
description: Explique comment appeler les modules de tâches à partir des onglets teams à l’aide du kit de développement logiciel client Microsoft Teams.
keywords: modules de tâches onglets teams du kit de développement logiciel client
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673973"
---
# <a name="using-task-modules-in-tabs"></a>Utilisation des modules de tâches dans les onglets

L’ajout d’un module de tâches à votre onglet permet de simplifier grandement l’expérience de vos utilisateurs pour tous les flux de travail qui nécessitent une entrée de données. Les modules de tâches vous permettent de recueillir leurs informations dans un menu contextuel qui prend en charge Teams. Par exemple, la modification des fiches du planificateur ; vous pouvez utiliser des modules de tâches pour créer une expérience similaire.

Pour prendre en charge la fonctionnalité de module de tâches, deux nouvelles fonctions ont été ajoutées au [Kit de développement logiciel client Microsoft teams](/javascript/api/overview/msteams-client):

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

## <a name="invoking-a-task-module-from-a-tab"></a>Appel d’un module de tâches à partir d’un onglet

Pour appeler un module de tâches à partir d' `microsoftTeams.tasks.startTask()` un onglet utilisé pour transmettre un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) et une fonction de rappel facultative `submitHandler` . Comme décrit précédemment, deux cas doivent être pris en compte :

1. La valeur de `TaskInfo.url` est définie sur une URL. La fenêtre du module tâches s' `TaskModule.url` affiche et est chargée `<iframe>` en tant que telle. JavaScript sur cette page doit appeler `microsoftTeams.initialize()`. S’il y a `submitHandler` une fonction sur la page et qu’il y a une erreur `microsoftTeams.tasks.startTask()`lors de `submitHandler` l’appel, le `err` est appelé avec la chaîne d’erreur indiquant l’erreur comme décrit [ci-dessous](#task-module-invocation-errors).
1. La valeur de `taskInfo.card` est le format [JSON pour une carte adaptative](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Dans ce cas, il n’y a évidemment `submitHandler` pas de fonction JavaScript à appeler lorsque l’utilisateur se ferme ou appuie sur un bouton de la carte adaptative ; le seul moyen de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un bot. Pour utiliser un module de tâches de carte adaptative à partir d’un onglet votre application doit inclure un bot pour récupérer toutes les informations de l’utilisateur. Cela est expliqué ci-dessous.

## <a name="example-invoking-a-task-module"></a>Exemple : appel d’un module de tâche

Le code ci-dessous est adapté à partir de [l’exemple de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples). Voici à quoi ressemble le module tâches :

![Module de tâche-formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

Le `submitHandler` est très simple ; elle renvoie simplement la valeur de `err` ou `result` vers la console :

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

La `submitHandler` fonction est utilisée avec `TaskInfo.url`. La `submitHandler` fonction réside dans la `TaskInfo.url` page Web. Si une erreur se produit lors de l’appel du module de `submitHandler` tâches, votre fonction est immédiatement appelée avec `err` une chaîne indiquant l' [erreur qui s’est produite](#task-module-invocation-errors). La `submitHandler` fonction est également appelée avec une `err` chaîne lorsque l’utilisateur appuie sur le X dans le coin supérieur droit du module de tâche.

S’il n’y a aucune erreur d’invocation et que l’utilisateur n’appuie pas sur X pour le masquer, l’utilisateur appuie sur un bouton lorsque vous avez terminé. Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâches, voici ce qui se passe :

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript (`TaskInfo.url`)

Une fois que vous avez validé ce que l’utilisateur a entré `microsoftTeams.tasks.submitTask()` , appelez la fonction SDK (désignée `submitTask()` ci-après, à des fins de lisibilité). Vous pouvez appeler `submitTask()` sans aucun paramètre si vous souhaitez simplement que teams ferme le module de tâches, mais la plupart du temps, vous souhaiterez passer un objet ou une chaîne `submitHandler`à votre.

Transmettez votre résultat en tant que premier paramètre. Teams appellera `submitHandler` l' `err` emplacement où `null` `result` sera l’objet/la chaîne que vous avez passée `submitTask()`. Si vous appelez `submitTask()` `result` avec un paramètre, vous **devez** transmettre un `appId` tableau de `appId` chaînes ou un tableau : cela permet à teams de valider le fait que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâches.

### <a name="adaptive-card-taskinfocard"></a>Carte adaptative (`TaskInfo.card`)

Si vous avez appelé le module de tâches avec `submitHandler`un, lorsque l’utilisateur appuie sur `Action.Submit` un bouton, les valeurs de la carte sont renvoyées comme valeur `result`de. Si l’utilisateur appuie sur le bouton Échap ou appuie sur la touche X `err` , il est renvoyé. Par ailleurs, si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure `appId` le du bot comme valeur de `completionBotId` dans l' `TaskInfo` objet. Le corps de la carte adaptative (tel qu’il est rempli par l’utilisateur) est envoyé au robot via `task/submit invoke` un message lorsque l’utilisateur appuie sur `Action.Submit` un bouton. Le schéma de l’objet que vous recevez est très similaire au [schéma que vous recevez pour les messages tâche/extraction et tâche/envoi](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la seule différence réside dans le fait que le schéma de l’objet JSON est un objet de carte adaptative contrairement à un objet *contenant* un objet de carte adaptative, comme [lorsque des cartes adaptatives sont utilisées avec des bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

## <a name="example-submitting-the-result-of-a-task-module"></a>Exemple : envoi du résultat d’un module de tâche

Rappelez le [formulaire dans le module de tâches ci-dessus](#example-invoking-a-task-module) avec un formulaire HTML. C’est ici que le formulaire est défini :

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Il y a cinq champs sur ce formulaire, mais nous les souhaitons uniquement dans les valeurs de trois d’entre eux pour `name`cet `email`exemple : `favoriteBook`,, et.

Voici la `validateForm()` fonction qui appelle `submitTask()`:

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

## <a name="task-module-invocation-errors"></a>Erreurs d’invocation du module de tâche

Voici les valeurs `err` possibles pouvant être reçues par votre `submitHandler`:

| Problème | Message d’erreur (valeur `err`de) |
| ------- | ------------------------------ |
| Valeurs pour les `TaskInfo.url` deux `TaskInfo.card` et spécifiés. | «Les valeurs de la carte et de l’URL ont été spécifiées. L’un ou l’autre, mais pas les deux, sont autorisés. " |
| Ni `TaskInfo.url` ni `TaskInfo.card` spécifié. | "Vous devez spécifier une valeur pour l’une ou l’autre de ces cartes ou URL." |
| Non `appId`valide. | « AppId non valide ». |
| Utilisateur a appuyé sur le bouton X, en le fermant. | « Utilisateur a annulé/fermé le module de tâches ». |
