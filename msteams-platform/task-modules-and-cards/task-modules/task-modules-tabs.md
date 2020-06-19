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

Pour appeler un module de tâches à partir d’un onglet utilisé pour `microsoftTeams.tasks.startTask()` transmettre un [objet TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) et une `submitHandler` fonction de rappel facultative. Comme décrit précédemment, deux cas doivent être pris en compte :

1. La valeur de `TaskInfo.url` est définie sur une URL. La fenêtre du module tâches s’affiche et `TaskModule.url` est chargée en tant que telle `<iframe>` . JavaScript sur cette page doit appeler `microsoftTeams.initialize()` . S’il y a une `submitHandler` fonction sur la page et qu’il y a une erreur lors de l’appel `microsoftTeams.tasks.startTask()` , `submitHandler` le est appelé avec `err` la chaîne d’erreur indiquant l’erreur comme décrit [ci-dessous](#task-module-invocation-errors).
1. La valeur de `taskInfo.card` est le format [JSON pour une carte adaptative](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Dans ce cas, il n’y a évidemment pas de `submitHandler` fonction JavaScript à appeler lorsque l’utilisateur se ferme ou appuie sur un bouton de la carte adaptative ; la seule façon de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un bot. Pour utiliser un module de tâches de carte adaptative à partir d’un onglet votre application doit inclure un bot pour récupérer toutes les informations de l’utilisateur. Cela est expliqué ci-dessous.

## <a name="example-invoking-a-task-module"></a>Exemple : appel d’un module de tâche

Le code ci-dessous est adapté à partir de [l’exemple de module de tâche](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples). Voici à quoi ressemble le module tâches :

![Module de tâche-formulaire personnalisé](~/assets/images/task-module/task-module-custom-form.png)

Le `submitHandler` est très simple ; il renvoie simplement en écho la valeur de `err` ou `result` sur la console :

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

La `submitHandler` fonction est utilisée avec `TaskInfo.url` . La `submitHandler` fonction réside dans la `TaskInfo.url` page Web. Si une erreur se produit lors de l’appel du module de tâches `submitHandler` , votre fonction est immédiatement appelée avec une `err` chaîne indiquant l' [erreur qui s’est produite](#task-module-invocation-errors). La `submitHandler` fonction est également appelée avec une `err` chaîne lorsque l’utilisateur appuie sur le X dans le coin supérieur droit du module de tâche.

S’il n’y a aucune erreur d’invocation et que l’utilisateur n’appuie pas sur X pour le masquer, l’utilisateur appuie sur un bouton lorsque vous avez terminé. Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâches, voici ce qui se passe :

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

Une fois que vous avez validé ce que l’utilisateur a entré, appelez la `microsoftTeams.tasks.submitTask()` fonction SDK (désignée ci-après, à des `submitTask()` fins de lisibilité). Vous pouvez appeler `submitTask()` sans aucun paramètre si vous souhaitez simplement que teams ferme le module de tâches, mais la plupart du temps, vous souhaiterez passer un objet ou une chaîne à votre `submitHandler` .

Transmettez votre résultat en tant que premier paramètre. Teams appellera `submitHandler` l’emplacement où sera `err` `null` `result` l’objet/la chaîne que vous avez passée `submitTask()` . Si vous appelez `submitTask()` avec un `result` paramètre, vous **devez** transmettre un `appId` tableau de chaînes ou un tableau `appId` : cela permet à teams de valider le fait que l’application qui envoie le résultat est la même que celle qui a appelé le module de tâches.

### <a name="adaptive-card-taskinfocard"></a>Carte adaptative ( `TaskInfo.card` )

Si vous avez appelé le module de tâches avec un `submitHandler` , lorsque l’utilisateur appuie sur un `Action.Submit` bouton, les valeurs de la carte sont renvoyées comme valeur de `result` . Si l’utilisateur appuie sur le bouton Échap ou appuie sur la touche X, il `err` est renvoyé. Par ailleurs, si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure le `appId` du bot comme valeur de `completionBotId` dans l' `TaskInfo` objet. Le corps de la carte adaptative (tel qu’il est rempli par l’utilisateur) est envoyé au robot via un `task/submit invoke` message lorsque l’utilisateur appuie sur un `Action.Submit` bouton. Le schéma de l’objet que vous recevez est très similaire au [schéma que vous recevez pour les messages tâche/extraction et tâche/envoi](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); la seule différence réside dans le fait que le schéma de l’objet JSON est un objet de carte adaptative contrairement à un objet *contenant* un objet de carte adaptative, comme [lorsque des cartes adaptatives sont utilisées avec des bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

## <a name="example-submitting-the-result-of-a-task-module"></a>Exemple : envoi du résultat d’un module de tâche

Rappelez le [formulaire dans le module de tâches ci-dessus](#example-invoking-a-task-module) avec un formulaire HTML. C’est ici que le formulaire est défini :

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Il y a cinq champs sur ce formulaire, mais nous les souhaitons uniquement dans les valeurs de trois d’entre eux pour cet exemple : `name` , `email` , et `favoriteBook` .

Voici la `validateForm()` fonction qui appelle `submitTask()` :

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

Voici les valeurs possibles pouvant `err` être reçues par votre `submitHandler` :

| Problème | Message d’erreur (valeur de `err` ) |
| ------- | ------------------------------ |
| Valeurs pour les deux `TaskInfo.url` et `TaskInfo.card` spécifiés. | «Les valeurs de la carte et de l’URL ont été spécifiées. L’un ou l’autre, mais pas les deux, sont autorisés. " |
| Ni `TaskInfo.url` ni `TaskInfo.card` spécifié. | "Vous devez spécifier une valeur pour l’une ou l’autre de ces cartes ou URL." |
| Non valide `appId` . | « AppId non valide ». |
| Utilisateur a appuyé sur le bouton X, en le fermant. | « Utilisateur a annulé/fermé le module de tâches ». |
