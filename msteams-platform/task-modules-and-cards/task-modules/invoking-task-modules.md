---
title: Appeler et ignorer des modules de tâche
description: En savoir plus sur l’appel et le rejet de modules de tâches, l’objet d’informations de tâche, le dimensionnement du module de tâches, la syntaxe de lien profond du module de tâches à l’aide d’exemples de code
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: ae2eb0e1367feb5f1b31c47396277758e2385204
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111877"
---
# <a name="invoke-and-dismiss-task-modules"></a>Appeler et ignorer des modules de tâche

Les modules de tâche peuvent être appelés à partir d’onglets, de bots ou de liens profonds. La réponse peut être en HTML, JavaScript ou en tant que carte adaptative. La façon dont les modules de tâches sont appelés et la façon de gérer la réponse de l’interaction de l’utilisateur sont très flexibles. Le tableau suivant récapitule le mode de fonctionnement :

| Appelé à l’aide de | Module de tâche avec HTML ou JavaScript | Module de tâche avec carte adaptative |
| --- | --- | --- |
| JavaScript dans un onglet | 1. Utilisez la fonction `tasks.startTask()` Teams SDK client avec une fonction de rappel facultative`submitHandler(err, result)`. <br/><br/> 2. Dans le code du module de tâche, lorsque l’utilisateur a effectué les actions, appelez la fonction `tasks.submitTask()` Teams SDK avec un `result` objet comme paramètre. Si un `submitHandler` rappel a été spécifié dans `tasks.startTask()`, Teams l’appelle avec `result` comme paramètre. En cas d’erreur lors de l’appel`tasks.startTask()`, la fonction est appelée avec une `err` chaîne à la `submitHandler` place. <br/><br/> 3. Vous pouvez également spécifier un `completionBotId` lors de l’appel `teams.startTask()`. Ensuite, le `result` est envoyé au bot à la place. | 1. Appelez la fonction `tasks.startTask()` Teams SDK client avec un [objet TaskInfo](#the-taskinfo-object) et `TaskInfo.card` contenant le code JSON de la carte adaptative à afficher dans la fenêtre contextuelle du module de tâche. <br/><br/> 2. Si un `submitHandler` rappel a été spécifié dans `tasks.startTask()`, Teams l’appelle avec une `err` chaîne, s’il y a eu une erreur lors de l’appel `tasks.startTask()` ou si l’utilisateur ferme la fenêtre contextuelle du module de tâche à l’aide du X en haut à droite. <br/><br/> 3. Si l’utilisateur appuie sur un `Action.Submit` bouton, son `data` objet est retourné comme valeur de `result`. |
| Bouton carte bot | 1. Les boutons de carte de bot, selon le type de bouton, peuvent appeler des modules de tâches de deux manières : une URL de lien profond ou en envoyant un `task/fetch` message. <br/><br/> 2. Si l’action `type` du bouton est `task/fetch` le `Action.Submit` type de bouton pour les cartes adaptatives, un `task/fetch invoke` événement http post est envoyé au bot. Le bot répond à POST avec HTTP 200 et le corps de la réponse contenant un wrapper autour de [l’objet TaskInfo](#the-taskinfo-object). Pour plus d’informations, consultez [l’appel d’un module de tâche à l’aide `task/fetch` de ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch). Teams affiche le module de tâche. <br/><br/> 3. Une fois que l’utilisateur a effectué les actions, appelez la fonction `tasks.submitTask()` Teams SDK avec un `result` objet comme paramètre. Le bot reçoit un `task/submit invoke` message qui contient l’objet `result`. <br/><br/> 4. Vous avez trois façons différentes de répondre au `task/submit` message, en ne faisant rien qui soit la tâche terminée correctement, en affichant un message à l’utilisateur dans une fenêtre contextuelle ou en appelant une autre fenêtre de module de tâche. Pour plus d’informations, consultez [la discussion détaillée sur `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | <ul><li> À l’instar des boutons des cartes Bot Framework, les boutons des cartes adaptatives prennent en charge deux façons d’appeler des modules de tâches, d’établir des liens profonds avec `Action.openUrl` des boutons et `task/fetch` d’utiliser `Action.Submit` des boutons. </li></ul> <br/><br/> <ul><li> Les modules de tâches avec cartes adaptatives fonctionnent très de la même façon que le cas HTML ou JavaScript. La principale différence est que, étant donné qu’il n’y a pas de JavaScript lorsque vous utilisez des cartes adaptatives, il n’existe aucun moyen d’appeler `tasks.submitTask()`. Au lieu de `Action.Submit` cela, Teams prend l’objet `data` et le retourne comme charge utile de l’événement`task/submit`. Pour plus d’informations, consultez [la flexibilité de `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). </li></ul> |
| URL de lien profond <br/>[Syntaxe d'URL](#task-module-deep-link-syntax) | 1. Teams appelle le module de tâche qui est l’URL qui apparaît à l’intérieur du `<iframe>` spécifié dans le `url` paramètre du lien profond. Il n’y a pas `submitHandler` de rappel. <br/><br/> 2. Dans le Code JavaScript de la page du module de tâche, appelez-le `tasks.submitTask()` pour le fermer avec un `result` objet en tant que paramètre, comme lors de son appel à partir d’un onglet ou d’un bouton de carte de bot. Toutefois, la logique d’achèvement est légèrement différente. Si votre logique d’achèvement réside sur le client, c’est-à-dire s’il n’y a pas de bot, il n’y a pas `submitHandler` de rappel. Toute logique d’achèvement doit donc se trouver dans le code précédant l’appel à `tasks.submitTask()`. Les erreurs d’appel sont signalées uniquement via la console. Si vous avez un bot, vous pouvez spécifier un `completionBotId` paramètre dans le lien profond pour envoyer l’objet `result` via un `task/submit` événement. | 1. Teams appelle le module de tâche qui est le corps de la carte JSON de la carte adaptative spécifié comme valeur encodée en URL du `card` paramètre du lien profond. <br/><br/> 2. L’utilisateur ferme le module de tâche en sélectionnant le X en haut à droite du module de tâche ou en appuyant sur un `Action.Submit` bouton de la carte. Étant donné qu’il n’y a pas `submitHandler` pour appeler, l’utilisateur doit disposer d’un bot pour envoyer la valeur des champs de carte adaptative. L’utilisateur doit utiliser le paramètre`completionBotId` dans le lien profond pour spécifier le bot auquel envoyer les données à l’aide d’un `task/submit invoke` événement. |

La section suivante spécifie l’objet `TaskInfo` qui définit certains attributs pour un module de tâche.

## <a name="the-taskinfo-object"></a>Objet TaskInfo

L’objet `TaskInfo` contient les métadonnées d’un module de tâche. Définissez la `url` valeur d’un iFrame incorporé ou `card` d’une carte adaptative. Le tableau suivant fournit la définition de l’objet :

| Attribut | Type | Description |
| --- | --- | --- |
| `title` | string | Cet attribut s’affiche sous le nom de l’application, à droite de l’icône de l’application. |
| `height` | valeur numérique ou chaîne | Cet attribut peut être un nombre représentant la hauteur du module de tâche en pixels, ou `small`, `medium`ou `large`. Pour plus d'informations, consultez [Dimensionnement du module de tâches](#task-module-sizing). |
| `width` | valeur numérique ou chaîne | Cet attribut peut être un nombre représentant la profondeur du module de tâche en pixels, ou `small`, `medium`ou `large`. Pour plus d'informations, consultez [Dimensionnement du module de tâches](#task-module-sizing). |
| `url` | string | Cet attribut est l’URL de la page chargée en tant que `<iframe>` dans le module de tâche. Le domaine de l'URL doit se trouver dans le tableau [validDomains](~/resources/schema/manifest-schema.md#validdomains) de l'application dans le manifeste de votre application. |
| `card` | Pièce jointe d’une carte adaptative ou d’un bot de carte adaptative | Cet attribut est le JSON de la carte adaptative à afficher dans le module de tâche. Si l’utilisateur appelle à partir d’un bot, utilisez le code JSON de carte adaptative dans un objet Bot Framework `attachment` . Dans un onglet, l’utilisateur doit utiliser une carte adaptative. Pour plus d’informations, consultez la [pièce jointe de carte adaptative ou de bot de carte adaptative](#adaptive-card-or-adaptive-card-bot-card-attachment). |
| `fallbackUrl` | string | Cet attribut ouvre l’URL dans un onglet de navigateur, si un client ne prend pas en charge la fonctionnalité de module de tâche. |
| `completionBotId` | string | Cet attribut spécifie un ID d’application de bot pour envoyer le résultat de l’interaction de l’utilisateur avec le module de tâche. S’il est spécifié, le bot reçoit un événement `task/submit invoke` avec un objet JSON dans la charge utile de l’événement. |

> [!NOTE]
> La fonctionnalité de module de tâche nécessite que les domaines de toutes les URL que vous souhaitez charger soient inclus dans le tableau dans le `validDomains` manifeste de votre application.

La section suivante spécifie le dimensionnement du module de tâches qui permet à l’utilisateur de définir la hauteur et la largeur du module de tâche.

## <a name="task-module-sizing"></a>Dimensionnement du module de tâche

L’utilisation d’entiers pour `TaskInfo.width` et `TaskInfo.height`, définit la hauteur et la largeur du module de tâche en pixels. Toutefois, en fonction de la taille de la fenêtre et de la résolution de l’écran de l’équipe, elles sont réduites proportionnellement tout en conservant le rapport d’aspects qui est la largeur ou la hauteur.

Si `TaskInfo.width` et `TaskInfo.height` sont `"small"`, `"medium"`ou `"large"`, la taille du rectangle rouge dans l’image suivante est une proportion de l’espace disponible, 20 %, 50 % et 60 % pour `width` et 20 %, 50 % et 66 % pour `height`:

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="exemple de module de tâche":::

Les modules de tâches appelés à partir d’un onglet peuvent être redimensionnés dynamiquement. Après avoir appelé `tasks.startTask()` , vous pouvez appeler `tasks.updateTask(newSize)` où les propriétés de hauteur et de largeur de l’objet newSize sont conformes à la spécification TaskInfo, par exemple `{ height: 'medium', width: 'medium' }`.

La section suivante fournit des exemples d’incorporation de modules de tâches dans une vidéo YouTube et une Application PowerApp.

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>Module de tâche CSS pour les modules de tâche HTML ou JavaScript

Les modules de tâche HTML ou JavaScript ont accès à la zone entière du module de tâche sous l’en-tête. Bien que cela offre une grande flexibilité, si vous souhaitez que le remplissage autour des bords s’aligne sur les éléments d’en-tête et évite les barres de défilement inutiles, l’utilisateur doit fournir le CSS approprié. Les sections suivantes fournissent quelques exemples pour quelques cas d’usage.

### <a name="example-1-youtube-video"></a>Exemple 1 : Vidéo YouTube

YouTube offre la possibilité d’incorporer des vidéos sur des pages web. Il est facile d’incorporer des vidéos sur des pages web dans un module de tâches à l’aide d’une page web stub simple.

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="Exemple Youtube":::

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

### <a name="example-2-powerapp"></a>Exemple 2 : PowerApp

L’utilisateur peut également utiliser la même approche pour incorporer une application PowerApp. Comme la hauteur ou la largeur d’un PowerApp individuel est personnalisable, l’utilisateur peut ajuster la hauteur et la largeur pour obtenir la présentation souhaitée.

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="Powerapp":::

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

La section suivante fournit des détails sur l’appel de votre carte à l’aide d’une carte adaptative ou d’une pièce jointe de bot de carte adaptative.

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Pièce jointe d’une carte adaptative ou d’un bot de carte adaptative

Selon la façon dont vous invoquez votre `card`, vous devez utiliser une carte adaptative ou une pièce jointe de bot de carte adaptative, qui est une carte adaptative encapsulée dans un objet pièce jointe.

Lorsque vous invoquez à partir d’un onglet, l’utilisateur doit utiliser une carte adaptative.

Le code suivant fournit un exemple de carte adaptative :

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

Le code suivant fournit un exemple de pièce jointe de carte de bot de carte adaptative lorsque vous invoquez à partir d’un bot :

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

La section suivante fournit des détails sur la syntaxe de lien profond du module de tâche, y compris l’objet `TaskInfo` et `APP_ID` et `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>Syntaxe de lien profond du module de tâches

Un lien profond de module de tâche est une sérialisation de l’objet TaskInfo avec les deux autres détails suivants, `APP_ID` et éventuellement :`BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Pour les types de données et les valeurs autorisées pour `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.width>``<TaskInfo.height>`et `<TaskInfo.title>`, consultez l’objet [TaskInfo](#the-taskinfo-object).

> [!TIP]
> Url encoder le lien profond lors de l’utilisation du `card` paramètre, par exemple, [`encodeURI()`la fonction JavaScript](https://www.w3schools.com/jsref/jsref_encodeURI.asp).

Le tableau suivant fournit des informations sur `APP_ID` et `BOT_APP_ID` :

| Valeur | Type | Requis | Description |
| --- | --- | --- | --- |
| `APP_ID` | string | Oui | L’[ID](~/resources/schema/manifest-schema.md#id) de l’application appelant le module de tâche. Le [tableau validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le manifeste pour `APP_ID` doit contenir le domaine pour `url` si `url` se trouve dans l’URL. L’ID d’application est déjà connu lorsqu’un module de tâche est appelé à partir d’un onglet ou d’un bot, ce qui explique pourquoi il n’est pas inclus dans `TaskInfo`. |
| `BOT_APP_ID` | string | Non | Si une valeur est `completionBotId` spécifiée, l’objet est envoyé à l’aide `result` d’un `task/submit invoke` message au bot spécifié. `BOT_APP_ID` doit être spécifié en tant que bot dans le manifeste de l’application, c’est-à-dire que vous ne pouvez pas l’envoyer à un bot. |

> [!NOTE]
> `APP_ID` et `BOT_APP_ID` peut être identique dans de nombreux cas, si une application a un bot recommandé à utiliser comme ID d’application s’il en existe un.

La section suivante fournit des détails sur l’utilisation d’un clavier avec le module office de votre application.

## <a name="keyboard-and-accessibility-guidelines"></a>Instructions relatives au clavier et à l’accessibilité

Avec les modules de tâche HTML ou JavaScript, vous devez vous assurer que le module de tâches de votre application peut être utilisé avec un clavier. Les programmes de lecteur d’écran dépendent également de la possibilité de naviguer à l’aide du clavier. Ainsi, les deux points suivants ont plus de chances d'être vérifiés :

* Utilisation de [l’attribut tabindex](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) dans vos balises HTML pour contrôler quels éléments peuvent être concentrés. En outre, utilisez l’attribut tabindex pour identifier l’endroit où il participe à la navigation séquentielle du clavier généralement avec les touches <kbd>Tab</kbd> et <kbd>Maj-Tab</kbd> .
* Gestion de la clé <kbd>Échap</kbd> dans javaScript pour votre module de tâche. Le code suivant fournit un exemple de gestion de la clé <kbd>Échap</kbd> :

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams garantit que la navigation au clavier fonctionne correctement à partir de l’en-tête du module de tâche dans votre code HTML et inversement.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|Exemples de module de tâches bots-V4 | Exemples de création de modules de tâches |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|Exemples d’onglets de module de tâche et bots-V3 | Exemples de création de modules de tâches |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Utiliser des modules de tâche dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](~/concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer le QR ou la fonctionnalité de scanneur de code-barres dans Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement sur Teams](~/concepts/device-capabilities/location-capability.md)
