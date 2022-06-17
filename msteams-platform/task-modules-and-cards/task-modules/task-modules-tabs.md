---
title: Utiliser des modules de tâches dans les onglets Microsoft Teams
description: Découvrez comment appeler des modules de tâches à partir d’onglets Teams et envoyer son résultat à l’aide du SDK client Microsoft Teams. Il inclut des exemples de code.
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a55ea89e67bf70254d52791d1ed5f0a1c573e89e
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142065"
---
# <a name="use-task-modules-in-tabs"></a>Utiliser des modules de tâche dans les onglets

Ajoutez un module de tâche à votre onglet pour simplifier l’expérience de votre utilisateur pour tous les flux de travail nécessitant une entrée de données. Les modules de tâches vous permettent de recueillir leurs entrées dans une fenêtre contextuelle compatible Avec Microsoft Teams. La modification des cartes du Planificateur en est un bon exemple. Vous pouvez utiliser des modules de tâche pour créer une expérience similaire.

Pour prendre en charge la fonctionnalité de module de tâche, deux nouvelles fonctions sont ajoutées au [SDK client Teams](/javascript/api/overview/msteams-client). Le code suivant montre un exemple de ces deux fonctions :

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

Vous pouvez voir comment fonctionne l’appel d’un module de tâche à partir d’un onglet et l’envoi du résultat d’un module de tâche.

## <a name="invoke-a-task-module-from-a-tab"></a>Appeler un module de tâche à partir d’un onglet

Pour appeler un module de tâche à partir d’un onglet, utilisez `microsoftTeams.tasks.startTask()` transmettre un [objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) et une fonction de rappel `submitHandler` facultative. Il existe deux cas à prendre en compte :

* La valeur de `TaskInfo.url` est définie sur une URL. La fenêtre du module de tâche s’affiche et `TaskModule.url` est chargé en tant que classe `<iframe>` à l’intérieur. JavaScript sur cette page appelle `microsoftTeams.initialize()`. S’il existe une `submitHandler` fonction sur la page et qu’il y a une erreur lors de `microsoftTeams.tasks.startTask()`l’appel, elle `submitHandler` est appelée avec `err` la valeur définie sur la chaîne d’erreur indiquant la même chose. Pour plus d’informations, consultez [erreurs d’appel de module de tâche](#task-module-invocation-errors).
* La valeur de `taskInfo.card` est le JSON [pour une carte adaptative](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Il n’existe aucune fonction JavaScript `submitHandler` à appeler lorsque l’utilisateur ferme ou appuie sur un bouton sur la carte adaptative. La seule façon de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un bot. Pour utiliser un module de tâche de carte adaptative à partir d’un onglet, votre application doit inclure un bot pour obtenir une réponse de l’utilisateur.

La section suivante donne un exemple d’appel d’un module de tâche.

## <a name="example-of-invoking-a-task-module"></a>Exemple d’appel d’un module de tâche

L’image suivante affiche le module de tâche :

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="Formulaire personnalisé du module de tâches":::

Le code suivant est adapté à partir de [l’exemple de module de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):

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

L’opération `submitHandler` est simple et fait écho à la valeur de `err` ou `result` à la console.

## <a name="submit-the-result-of-a-task-module"></a>Envoyer le résultat d’un module de tâche

La fonction `submitHandler` réside dans la page web `TaskInfo.url` et est utilisée avec `TaskInfo.url`. En cas d’erreur lors de l’appel du module de tâche, votre `submitHandler` fonction est immédiatement appelée avec une `err` chaîne indiquant [l’erreur qui s’est produite](#task-module-invocation-errors). La fonction `submitHandler` est également appelée avec une chaîne `err` lorsque l’utilisateur sélectionne X en haut à droite du module de tâche pour la fermer.

S’il n’y a pas d’erreur d’appel et que l’utilisateur ne sélectionne pas X pour la ignorer, l’utilisateur choisit un bouton une fois terminé. Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâche, les sections suivantes fournissent des détails sur ce qui se produit.

### <a name="html-or-javascript-taskinfourl"></a>Html ou JavaScript `TaskInfo.url`

Après avoir validé les entrées de l’utilisateur, appelez la fonction SDK `microsoftTeams.tasks.submitTask()` appelée `submitTask()`. Appelez `submitTask()` sans paramètres si vous souhaitez simplement que Teams ferme le module de tâche. Vous pouvez passer un objet ou une chaîne à votre `submitHandler`.

Transmettez votre résultat comme premier paramètre. Teams appelle `submitHandler` où `err` est `null`> et `result` est l’objet ou la chaîne que vous avez passé à `submitTask()`. Si vous appelez `submitTask()` avec un paramètre `result`, vous devez passer un `appId` ou un tableau de chaînes `appId`. Cela permet à Teams de vérifier que l’application qui envoie le résultat est identique au module de tâche appelé.

### <a name="adaptive-card-taskinfocard"></a>Carte adaptative `TaskInfo.card`

Lorsque vous appelez le module de tâche avec un `submitHandler` et que l’utilisateur sélectionne un bouton `Action.Submit`, les valeurs de la carte sont retournées en tant que valeur de `result`. Si l’utilisateur sélectionne la touche Échap ou X en haut à droite, `err` est retourné à la place. Si votre application contient un bot en plus d’un onglet, vous pouvez inclure le `appId` bot comme valeur de `completionBotId` l’objet `TaskInfo` . Le corps de la carte adaptative tel que rempli par l’utilisateur est envoyé au bot à l’aide d’un message `task/submit invoke` lorsque l’utilisateur sélectionne un bouton `Action.Submit`. Le schéma de l’objet que vous recevez est similaire [au schéma que vous recevez pour les messages de tâche/récupération et de tâche/envoi](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). La seule différence est que le schéma de l’objet JSON est un objet de carte adaptative par opposition à un objet contenant un objet de carte adaptative comme [lorsque les cartes adaptatives sont utilisées avec des bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

La section suivante fournit un exemple d’envoi du résultat d’un module de tâche.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Exemple d’envoi du résultat d’un module de tâche

Pour plus d’informations, consultez [le formulaire HTML dans le module de tâche](#example-of-invoking-a-task-module). Le code suivant donne un exemple de l’emplacement où le formulaire est défini :

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Ce formulaire comporte cinq champs, mais pour cet exemple, seules trois valeurs sont requises: `name`, `email` et `favoriteBook`.

Le code suivant fournit un exemple de la fonction `validateForm()` qui appelle `submitTask()` :

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

La section suivante fournit les problèmes d’appel du module de tâche et leurs messages d’erreur.

## <a name="task-module-invocation-errors"></a>Erreurs d’invocation de module de tâche

Le tableau suivant fournit les valeurs possibles de `err` qui peuvent être reçues par votre `submitHandler` :

| Problème | Message d’erreur qui est la valeur de `err` |
| ------- | ------------------------------ |
| Les valeurs pour `TaskInfo.url` et `TaskInfo.card` ont été spécifiées. | Les valeurs de la carte et de l’URL ont été spécifiées. L’une ou l’autre, mais pas les deux, sont autorisées. |
| Ni `TaskInfo.url` ni `TaskInfo.card` spécifié. | Vous devez spécifier une valeur pour la carte ou l’URL. |
| `appId` non valide. | ID d'application non valide. |
| L’utilisateur a sélectionné le bouton X, en le fermant. | L’utilisateur a annulé ou fermé le module de tâche. |

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples d’onglets de module de tâche et bots-V3 | Exemples de création de modules de tâches |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [l’utilisation de modules de tâches de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Voir aussi

[Appeler et ignorer des modules de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
