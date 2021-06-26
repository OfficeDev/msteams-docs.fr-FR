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
# <a name="invoke-and-dismiss-task-modules"></a>Appeler et ignorer des modules de tâche

Les modules de tâche peuvent être appelés à partir d’onglets, de bots ou de liens profonds. La réponse peut être au format HTML, JavaScript ou sous forme de carte adaptative. La façon dont les modules de tâche sont appelés et la manière de traiter la réponse de l’interaction de l’utilisateur offrent beaucoup de souplesse. Le tableau suivant récapitule le fonctionnement :

| Appel à l’aide | Module de tâche avec HTML ou JavaScript | Module de tâche avec carte adaptative |
| --- | --- | --- |
| JavaScript dans un onglet | 1. Utilisez la fonction Teams SDK client `tasks.startTask()` avec une fonction de rappel `submitHandler(err, result)` facultative. <br/><br/> 2. Dans le code du module de tâche, lorsque l’utilisateur a effectué les actions, appelez la fonction Teams SDK avec un objet `tasks.submitTask()` `result` en tant que paramètre. Si un `submitHandler` rappel a été spécifié dans , Teams `tasks.startTask()` l’appelle avec `result` comme paramètre. Si une erreur s’est produite lors de l’appel, la fonction est `tasks.startTask()` appelée avec une chaîne à la `submitHandler` `err` place. <br/><br/> 3. Vous pouvez également spécifier un lorsque `completionBotId` vous appelez `teams.startTask()` . Ensuite, `result` il est envoyé au bot à la place. | 1. Appelez la fonction Teams client SDK avec un objet TaskInfo et contenant le JSON de la carte adaptative à afficher dans la fenêtre pop-up du module de `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` tâche. <br/><br/> 2. Si un rappel a été spécifié dans , Teams l’appelle avec une chaîne, s’il y a eu une erreur lors de l’appel ou si l’utilisateur ferme la fenêtre `submitHandler` pop-up du module de tâche à l’aide du X en haut à `tasks.startTask()` `err` `tasks.startTask()` droite. <br/><br/> 3. Si l’utilisateur appuie sur un `Action.Submit` bouton, son `data` objet est renvoyé en tant que valeur de `result` . |
| Bouton de carte bot | 1. Les boutons de carte bot, en fonction du type de bouton, peuvent appeler des modules de tâche de deux manières : une URL de lien profond ou en envoyant un `task/fetch` message. <br/><br/> 2. Si l’action du bouton est le type de bouton pour les cartes adaptatives, un événement qui est une demande HTTP POST est envoyé `type` `task/fetch` au `Action.Submit` `task/fetch invoke` bot. Le bot répond au POST avec HTTP 200 et le corps de la réponse contenant un wrapper autour de [l’objet TaskInfo](#the-taskinfo-object). Pour plus d’informations, [voir l’appel `task/fetch` d’un module de tâche à l’aide de ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams affiche le module de tâche. <br/><br/> 3. Une fois que l’utilisateur a effectué les actions, appelez la fonction Teams SDK avec un `tasks.submitTask()` objet en tant que `result` paramètre. Le bot reçoit un `task/submit invoke` message contenant `result` l’objet. <br/><br/> 4. Vous pouvez répondre au message de trois manières différentes, en ne faisant rien qui soit correctement effectué par la tâche, en affichant un message à l’utilisateur dans une fenêtre ou en invoquant une autre fenêtre de module de `task/submit` tâche. Pour plus d’informations, [voir la discussion détaillée sur `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> Comme les boutons sur les cartes Bot Framework, les boutons des cartes adaptatives offrent deux moyens d’appel des modules de tâche, d’URL de liens profonds avec des boutons et d’utilisation `Action.openUrl` `task/fetch` de `Action.Submit` boutons. </li></ul> <br/><br/> <ul><li> Les modules de tâche avec cartes adaptatives fonctionnent de manière très similaire au cas HTML ou JavaScript. La principale différence est que, étant donné qu’il n’existe pas de JavaScript lorsque vous utilisez des cartes adaptatives, il n’existe aucun moyen d’appeler `tasks.submitTask()` . Au lieu de cela, Teams l’objet et le renvoie en tant que `data` `Action.Submit` charge utile de `task/submit` l’événement. Pour plus d’informations, voir [flexibilité de `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). </li></ul> |
| URL du lien profond <br/>[Syntaxe d'URL](#task-module-deep-link-syntax) | 1. Teams le module de tâche qui est l’URL qui apparaît à l’intérieur du paramètre spécifié dans le `<iframe>` `url` paramètre du lien profond. Il n’y `submitHandler` a pas de rappel. <br/><br/> 2. Dans le JavaScript de la page dans le module de tâche, appelez pour le fermer avec un objet en tant que paramètre, comme lors de l’appel à partir d’un onglet ou d’un bouton de carte `tasks.submitTask()` `result` bot. Toutefois, la logique d’achèvement est légèrement différente. Si votre logique d’achèvement réside sur le client, c’est-à-dire s’il n’y a pas de bot, il n’y a pas de rappel, de sorte que toute logique d’achèvement doit se trouver dans le code précédant `submitHandler` l’appel vers `tasks.submitTask()` . Les erreurs d’appel sont uniquement signalées via la console. Si vous avez un bot, vous pouvez spécifier un paramètre dans le lien profond pour envoyer l’objet `completionBotId` `result` via un `task/submit` événement. | 1. Teams appelle le module de tâche qui est le corps de la carte JSON de la carte adaptative spécifiée en tant que valeur codée URL du paramètre du lien `card` profond. <br/><br/> 2. L’utilisateur ferme le module de tâche en sélectionnant le X en haut à droite du module de tâche ou en appuyant sur un bouton `Action.Submit` de la carte. Étant donné qu’il n’y a pas d’appel, l’utilisateur doit avoir un bot pour envoyer la valeur des champs de `submitHandler` carte adaptative. L’utilisateur doit utiliser le paramètre dans le lien profond pour spécifier le bot pour envoyer les données à l’aide `completionBotId` d’un `task/submit invoke` événement. |

> [!NOTE]
> L’vot d’un module de tâche à partir de JavaScript n’est pas pris en charge sur les appareils mobiles.

La section suivante spécifie `TaskInfo` l’objet qui définit certains attributs pour un module de tâche.

## <a name="the-taskinfo-object"></a>Objet TaskInfo

`TaskInfo`L’objet contient les métadonnées d’un module de tâche. Définissez `url` le pour un iFrame incorporé ou pour une carte `card` adaptative. Le tableau suivant fournit la définition d’objet :

| Attribut | Type | Description |
| --- | --- | --- |
| `title` | string | Cet attribut apparaît sous le nom de l’application et à droite de l’icône de l’application. |
| `height` | valeur numérique ou chaîne | Cet attribut peut être un nombre représentant la hauteur du module de tâche en pixels, `small` ou `medium` , ou `large` . Pour plus d’informations, [voir le resserrage du module de tâche.](#task-module-sizing) |
| `width` | valeur numérique ou chaîne | Cet attribut peut être un nombre représentant la largeur du module de tâche en pixels, `small` ou `medium` , ou `large` . Pour plus d’informations, [voir le resserrage du module de tâche.](#task-module-sizing) |
| `url` | chaîne | Cet attribut est l’URL de la page chargée en tant qu’url à `<iframe>` l’intérieur du module de tâche. Le domaine de l’URL doit se trouver dans le tableau [validDomains](~/resources/schema/manifest-schema.md#validdomains) de l’application dans le manifeste de votre application. |
| `card` | Pièce jointe d’une carte adaptative ou d’une carte adaptative | Cet attribut est le JSON de la carte adaptative à apparaître dans le module de tâche. Si l’utilisateur fait appel à partir d’un bot, utilisez le JSON de carte adaptative dans un objet Bot `attachment` Framework. À partir d’un onglet, l’utilisateur doit utiliser une carte adaptative. Pour plus d’informations, voir [carte adaptative ou pièce jointe de carte de bot de carte adaptative](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | chaîne | Cet attribut ouvre l’URL dans un onglet de navigateur, si un client ne prend pas en charge la fonctionnalité de module de tâche. |
| `completionBotId` | chaîne | Cet attribut spécifie un ID d’application de bot pour envoyer le résultat de l’interaction de l’utilisateur avec le module de tâche. S’il est spécifié, le bot reçoit un événement `task/submit invoke` avec un objet JSON dans la charge utile de l’événement. |

> [!NOTE]
> La fonctionnalité de module de tâche nécessite que les domaines des URL que vous souhaitez charger soient inclus dans le tableau dans le manifeste `validDomains` de votre application.

La section suivante spécifie le resserrage du module de tâche qui permet à l’utilisateur de définir la hauteur et la largeur du module de tâche.

## <a name="task-module-sizing"></a>Resserrage du module de tâche

L’utilisation d’nombres integers pour et , définit la hauteur et la largeur du `TaskInfo.width` module de tâche en `TaskInfo.height` pixels. Toutefois, en fonction de la taille de la fenêtre et de la résolution de l’écran de l’équipe, elles sont réduites proportionnellement tout en conservant les proportions de largeur ou de hauteur.

Si et sont , ou , la taille du rectangle rouge dans l’image suivante est une proportion de l’espace `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` disponible, 20 %, 50 % et 60 % pour et `width` 20 %, 50 % et 66 % `height` pour :

![Exemple de module de tâche](~/assets/images/task-module/task-module-example.png)

Les modules de tâche appelés à partir d’un onglet peuvent être resserrisés dynamiquement. Après l’appel, vous pouvez appeler l’endroit où les propriétés de hauteur et de largeur de l’objet newSize sont conformes à la spécification `tasks.startTask()` `tasks.updateTask(newSize)` TaskInfo, par `{ height: 'medium', width: 'medium' }` exemple.

La section suivante fournit des exemples d’incorporation de modules de tâche dans une vidéo YouTube et une application PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>Module de tâche CSS pour les modules de tâche HTML ou JavaScript

Les modules de tâche HTML ou JavaScript ont accès à toute la zone du module de tâche sous l’en-tête. Bien que cela offre beaucoup de flexibilité, si vous souhaitez que le remplissage autour des bords s’aligne sur les éléments d’en-tête et évite les barres de défilement inutiles, l’utilisateur doit fournir le bon CSS. Les sections suivantes fournissent quelques exemples pour quelques cas d’utilisation.

**Exemple 1 : vidéo YouTube**

YouTube offre la possibilité d’incorporer des vidéos sur des pages web. Il est facile d’incorporer des vidéos sur des pages web dans un module de tâche à l’aide d’une page web stub simple.

![Vidéo YouTube](~/assets/images/task-module/youtube-example.png)

Le code suivant fournit un exemple de code HTML pour la page web sans CSS :

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

Le code suivant fournit un exemple de CSS :

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

**Exemple 2 : PowerApp**

L’utilisateur peut également utiliser la même approche pour incorporer un PowerApp. Comme la hauteur ou la largeur d’un PowerApp individuel est personnalisable, l’utilisateur peut ajuster la hauteur et la largeur pour obtenir la présentation souhaitée.

![Gestion des biens PowerApp](~/assets/images/task-module/powerapp-example.png)

Le code suivant fournit un exemple de code HTML pour PowerApp :

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

Le code suivant fournit un exemple de CSS :

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

La section suivante fournit des détails sur l’appel de votre carte à l’aide d’une carte adaptative ou d’une pièce jointe de carte bot de carte adaptative.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Pièce jointe d’une carte adaptative ou d’une carte adaptative

Selon la façon dont vous voquer votre , vous devez utiliser une carte adaptative ou une pièce jointe de carte de bot de carte adaptative, qui est une carte adaptative wrapped dans un objet `card` pièce jointe.

Lorsque vous voquer à partir d’un onglet, l’utilisateur doit utiliser une carte adaptative.

Le code suivant fournit un exemple de carte adaptative :

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

Le code suivant fournit un exemple de pièce jointe d’une carte de bot de carte adaptative lorsque vous voquer à partir d’un bot :

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

La section suivante fournit des détails sur la syntaxe de lien profond du module de tâche, y compris `TaskInfo` l’objet et `APP_ID` `BOT_APP_ID` .

## <a name="task-module-deep-link-syntax"></a>Syntaxe de lien profond du module de tâche

Un lien profond de module de tâche est une sérialisation de l’objet TaskInfo avec les deux autres détails suivants, et `APP_ID` éventuellement les éléments suivants `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Pour les types de données et les valeurs permises pour `<TaskInfo.url>` , , et , voir `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [l’objet TaskInfo](#the-taskinfo-object).

> [!TIP]
> URL encoder le lien profond lors de `card` l’utilisation [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)du paramètre, par exemple, la fonction JavaScript .

Le tableau suivant fournit des informations sur `APP_ID` et `BOT_APP_ID` :

| Valeur | Type | Requis | Description |
| --- | --- | --- | --- |
| `APP_ID` | string | Oui | [ID de l’application](~/resources/schema/manifest-schema.md#id) qui invoquer le module de tâche. Le [tableau validDomains dans](~/resources/schema/manifest-schema.md#validdomains) le manifeste doit contenir le domaine pour si se trouve dans `APP_ID` `url` `url` l’URL. L’ID d’application est déjà connu lorsqu’un module de tâche est appelé à partir d’un onglet ou d’un bot, c’est pourquoi il n’est pas inclus dans `TaskInfo` . |
| `BOT_APP_ID` | string | Non | Si une valeur `completionBotId` est spécifiée, l’objet est envoyé à l’aide `result` d’un message au `task/submit invoke` bot spécifié. `BOT_APP_ID` doit être spécifié en tant que bot dans le manifeste de l’application, c’est-à-dire que vous ne pouvez pas l’envoyer à un bot. |

> [!NOTE]
> `APP_ID` et peut être identique dans de nombreux cas, si une application possède un bot recommandé à utiliser comme `BOT_APP_ID` ID d’application s’il en existe un.

La section suivante fournit des détails sur l’utilisation d’un clavier avec le module de tâche de votre application.

## <a name="keyboard-and-accessibility-guidelines"></a>Recommandations en matière de clavier et d’accessibilité

Avec les modules de tâche HTML ou JavaScript, vous devez vous assurer que le module de tâche de votre application peut être utilisé avec un clavier. Les programmes de lecteur d’écran dépendent également de la possibilité de naviguer à l’aide du clavier. Cela inclut les deux éléments suivants :

* Utilisation de [l’attribut tabindex dans](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) vos balises HTML pour contrôler les éléments qui peuvent être concentrés. En outre, utilisez l’attribut tabindex pour identifier l’endroit où il participe à la navigation séquentielle au clavier généralement avec les touches <kbd>Tab</kbd> et <kbd>Shift-Tab.</kbd>
* Gestion de la <kbd>touche Échap</kbd> dans javaScript pour votre module de tâche. Le code suivant fournit un exemple de la façon de gérer la touche <kbd>Échap</kbd> :

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams s’assure que la navigation au clavier fonctionne correctement à partir de l’en-tête du module de tâche dans votre code HTML et inversement.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples de module de tâche bots-V4 | Exemples de création de modules de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Exemples d’onglets de module de tâche et bots-V3 | Exemples de création de modules de tâche. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](~/concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer des fonctionnalités d’emplacement dans Teams](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utiliser des modules de tâche dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md)