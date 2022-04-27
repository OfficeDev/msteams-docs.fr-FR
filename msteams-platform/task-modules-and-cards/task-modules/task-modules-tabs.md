---
title: Utiliser des modules de tâches dans Microsoft Teams onglets
description: Explique comment appeler des modules de tâches à partir d’onglets Teams et envoyer son résultat à l’aide du SDK client Microsoft Teams. Il inclut des exemples de code.
ms.localizationpriority: medium
ms.topic: how-to
keywords: Kit de développement logiciel (SDK) client onglets teams des modules de tâches
ms.openlocfilehash: 63ac1df5b9cdbbba46ba204103a9a5c989b3a323
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073755"
---
# <a name="use-task-modules-in-tabs"></a>Utiliser des modules de tâche dans les onglets

Ajoutez un module de tâche à votre onglet pour simplifier l’expérience de votre utilisateur pour tous les flux de travail nécessitant une entrée de données. Les modules de tâche vous permettent de collecter leurs entrées dans une fenêtre contextuelle Microsoft Teams-Aware. La modification des cartes du Planificateur en est un bon exemple. Vous pouvez utiliser des modules de tâches pour créer une expérience similaire.

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

Pour appeler un module de tâche à partir d’un onglet, utilisez `microsoftTeams.tasks.startTask()` le passage d’un [objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) et d’une fonction de rappel facultative `submitHandler` . Il existe deux cas à prendre en compte :

* La valeur est `TaskInfo.url` définie sur une URL. La fenêtre du module de tâche s’affiche et `TaskModule.url` est chargée en tant qu’intérieur `<iframe>` . JavaScript sur cette page appelle `microsoftTeams.initialize()`. S’il existe une `submitHandler` fonction sur la page et qu’il y a une erreur lors de `microsoftTeams.tasks.startTask()`l’appel, elle `submitHandler` est appelée avec `err` la valeur définie sur la chaîne d’erreur indiquant la même chose. Pour plus d’informations, consultez [les erreurs d’appel du module de tâche](#task-module-invocation-errors).
* La valeur est `taskInfo.card` le [JSON pour une carte adaptative](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment). Il n’existe aucune fonction JavaScript `submitHandler` à appeler lorsque l’utilisateur ferme ou appuie sur un bouton sur la carte adaptative. La seule façon de recevoir ce que l’utilisateur a entré est de transmettre le résultat à un bot. Pour utiliser un module de tâche de carte adaptative à partir d’un onglet, votre application doit inclure un bot pour obtenir une réponse de l’utilisateur.

La section suivante fournit un exemple d’appel d’un module de tâche.

## <a name="example-of-invoking-a-task-module"></a>Exemple d’appel d’un module de tâche

L’image suivante affiche le module de tâche :

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="Formulaire personnalisé du module de tâches":::

Le code suivant est adapté à partir de [l’exemple de module de tâche :](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)

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

L’est `submitHandler` très simple et il fait écho à la valeur de `err` ou `result` à la console.

## <a name="submit-the-result-of-a-task-module"></a>Envoyer le résultat d’un module de tâche

La `submitHandler` fonction réside dans la `TaskInfo.url` page web et est utilisée avec `TaskInfo.url`. En cas d’erreur lors de l’appel du module de tâche, votre `submitHandler` fonction est immédiatement appelée avec une `err` chaîne indiquant [l’erreur qui s’est produite](#task-module-invocation-errors). La `submitHandler` fonction est également appelée avec une `err` chaîne lorsque l’utilisateur sélectionne X en haut à droite du module de tâche pour la fermer.

S’il n’y a aucune erreur d’appel et que l’utilisateur ne sélectionne pas X pour la faire ignorer, l’utilisateur choisit un bouton une fois terminé. Selon qu’il s’agit d’une URL ou d’une carte adaptative dans le module de tâche, les sections suivantes fournissent des détails sur ce qui se produit.

### <a name="html-or-javascript-taskinfourl"></a>HTML ou JavaScript `TaskInfo.url`

Après avoir validé les entrées de l’utilisateur, appelez la `microsoftTeams.tasks.submitTask()` fonction SDK appelée `submitTask()`. Appelez `submitTask()` sans paramètres si vous souhaitez simplement Teams fermer le module de tâche. Vous pouvez passer un objet ou une chaîne à votre `submitHandler`.

Transmettez votre résultat comme premier paramètre. Teams appelle `submitHandler` où `err` se trouve `null` et `result` est l’objet ou la chaîne à `submitTask()`laquelle vous avez passé . Si vous appelez `submitTask()` avec un `result` paramètre, vous devez passer un `appId` ou un tableau de `appId` chaînes. Cela permet à Teams de vérifier que l’application qui envoie le résultat est identique au module de tâche appelé.

### <a name="adaptive-card-taskinfocard"></a>Carte adaptative `TaskInfo.card`

Lorsque vous invokez le module de tâche avec a `submitHandler` et que l’utilisateur sélectionne un `Action.Submit` bouton, les valeurs de la carte sont retournées en tant que valeur de `result`. Si l’utilisateur sélectionne la touche Échap ou X en haut à droite, `err` elle est retournée à la place. Si votre application contient un bot en plus d’un onglet, vous pouvez simplement inclure le `appId` bot comme valeur de `completionBotId` l’objet `TaskInfo` . Le corps de la carte adaptative tel que rempli par l’utilisateur est envoyé au bot à l’aide d’un `task/submit invoke` message lorsque l’utilisateur sélectionne un `Action.Submit` bouton. Le schéma de l’objet que vous recevez est très similaire [au schéma que vous recevez pour les messages de tâche/récupération et de tâche/envoi](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages). La seule différence est que le schéma de l’objet JSON est un objet de carte adaptative, par opposition à un objet contenant un objet De carte adaptative comme [lorsque des cartes adaptatives sont utilisées avec des bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).

La section suivante fournit un exemple d’envoi du résultat d’un module de tâche.

## <a name="example-of-submitting-the-result-of-a-task-module"></a>Exemple d’envoi du résultat d’un module de tâche

Pour plus d’informations, consultez le [formulaire HTML dans le module de tâche](#example-of-invoking-a-task-module). Le code suivant donne un exemple de l’endroit où le formulaire est défini :

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

Ce formulaire comporte cinq champs, mais pour cet exemple, seules trois valeurs sont requises, `name`, `email`et `favoriteBook`.

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

Le tableau suivant fournit les valeurs possibles qui `err` peuvent être reçues par votre `submitHandler`:

| Problème | Message d’erreur dont la valeur est `err` |
| ------- | ------------------------------ |
| Valeurs pour les deux `TaskInfo.url` et `TaskInfo.card` ont été spécifiées. | Des valeurs pour la carte et l’URL ont été spécifiées. L’un ou l’autre, mais pas les deux, sont autorisés. |
| Ni `TaskInfo.url` spécifié `TaskInfo.card` . | Vous devez spécifier une valeur pour la carte ou l’URL. |
| Non valide `appId`. | ID d’application non valide. |
| Bouton X sélectionné par l’utilisateur, le fermant. | L’utilisateur a annulé ou fermé le module de tâche. |

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples d’onglets de module de tâche et bots-V3 | Exemples de création de modules de tâches. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utilisation de modules de tâches à partir de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>Voir aussi

[Appeler et ignorer des modules de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
