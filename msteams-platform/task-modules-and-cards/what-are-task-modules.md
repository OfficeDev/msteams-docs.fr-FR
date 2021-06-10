---
title: Qu-est-ce qu’un module de tâche ?
author: clearab
description: Ajouter des expériences de fenêtres popup modales pour collecter ou afficher des informations à vos utilisateurs à partir de Microsoft Teams applications
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23157e30ce25c2dfa1c21e7f5c4ddd4f735b660f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566839"
---
# <a name="task-modules"></a>Modules de tâches

Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’intérieur de la fenêtre popup, vous pouvez exécuter votre propre code HTML/JavaScript personnalisé, afficher un widget basé sur un widget tel qu’une vidéo YouTube ou Microsoft Stream ou afficher une `<iframe>` [carte adaptative.](/adaptive-cards/) Ils sont particulièrement utiles pour initier et effectuer des tâches, ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Une expérience contextuelle est souvent plus naturelle pour les utilisateurs qui initient et effectuent des tâches, par rapport à une expérience d’onglet ou de bot basée sur une conversation.

Les modules de tâche s’appuient sur les bases Microsoft Teams onglets ; Il s’agit essentiellement d’un onglet à l’intérieur d’une fenêtre popup. Ils utilisent le même SDK, donc si vous avez créé un onglet, vous êtes déjà à 90 % de la façon de créer un module de tâche.

Les modules de tâche peuvent être appelés de trois façons :

* **Onglets** de canal ou personnels : à l’aide du SDK onglets Microsoft Teams, vous pouvez appeler des modules de tâche à partir de boutons, de liens ou de menus de votre onglet. Cette information est détaillée [ici.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bots :** boutons sur [les cartes envoyées](~/task-modules-and-cards/cards/cards-reference.md) à partir de votre bot. Ceci est particulièrement utile lorsque vous n’avez pas besoin que tout le monde dans un canal voie ce que vous faites avec un bot. Par exemple, lorsque des utilisateurs répondent à un sondage dans un canal, il n'est pas très utile de voir un enregistrement de ce sondage. [Ce sujet est abordé en détail ici.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **En dehors Teams à partir** d’un lien profond : vous pouvez également créer des URL pour appeler un module de tâche de n’importe où. [Ce sujet est abordé en détail ici.](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>Le module de tâche ressemble à

Voici à quoi ressemble un module de tâche lorsqu’il est appelé à partir d’un bot (sans les rectangles de couleur et les cercles numérotés, bien entendu) :

![Exemple de module de tâche](~/assets/images/task-module/task-module-example.png)

Examinons ce qui se passe :

1. Icône de votre [ `color` application.](~/resources/schema/manifest-schema.md#icons)
1. Nom de votre [ `short` application.](~/resources/schema/manifest-schema.md#name)
1. Titre du module de tâche spécifié dans la `title` propriété de [l’objet TaskInfo](#the-taskinfo-object).
1. Bouton fermer/annuler du module de tâche. Si l’utilisateur appuie sur cette touche, votre application recevra un `err` événement comme décrit [ici.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)
    > [!Note]
    > Il n’est actuellement pas possible de détecter cet événement lorsqu’un module de tâche est appelé à partir d’un bot.
1. Le rectangle bleu est l’endroit où votre page web apparaît si vous chargez votre propre page web à l’aide de la `url` propriété de [l’objet TaskInfo](#the-taskinfo-object). Pour plus d’informations, voir la section [de resserrisation](#task-module-sizing) du module de tâche ci-dessous.
1. Si vous affichez une carte adaptative via la propriété de `card` l’objet [TaskInfo,](#the-taskinfo-object) le remplissage est ajouté pour vous, sinon vous devrez gérer [cela vous-même.](#task-module-css-for-htmljavascript-task-modules)
1. Les boutons de carte adaptative s’restituera ici. Si vous utilisez votre propre page, vous devez créer vos propres boutons.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Vue d’ensemble de l’facturation et de l’annulation des modules de tâche

Les modules de tâche peuvent être appelés à partir d’onglets, de bots ou de liens profonds, et ce qui apparaît dans l’un d’eux peut être du code HTML ou une carte adaptative. Il existe donc beaucoup de flexibilité quant à la façon dont ils sont appelés et à gérer le résultat de l’interaction d’un utilisateur. Le tableau ci-dessous récapitule le fonctionnement :

| **Appelé via...** | **Module de tâche html/JavaScript** | **Le module de tâche est une carte adaptative** |
| --- | --- | --- |
| **JavaScript dans un onglet** | 1. Utilisez la fonction Teams SDK client `tasks.startTask()` avec une fonction de rappel `submitHandler(err, result)` facultative. <br/><br/> 2. Dans le code du module de tâche, lorsque l’utilisateur a terminé, appelez la fonction Teams SDK avec un objet `tasks.submitTask()` `result` en tant que paramètre. Si un `submitHandler` rappel a été spécifié dans , Teams `tasks.startTask()` l’appelle avec `result` comme paramètre.<br/><br/> 3. En cas d’erreur lors de l’appel, la fonction est `tasks.startTask()` appelée avec une chaîne à la `submitHandler` `err` place. <br/><br/> 4. Vous pouvez également spécifier un lorsque vous appelez , dans ce `completionBotId` cas est envoyé au bot à la `teams.startTask()` `result` place. | 1. Appelez la fonction Teams client SDK avec un objet TaskInfo et contenant le JSON de la carte adaptative à afficher dans la fenêtre popup du `tasks.startTask()` module de [](#the-taskinfo-object) `TaskInfo.card` tâche. <br/><br/> 2. Si un rappel a été spécifié dans , Teams l’appelle avec une chaîne en cas d’erreur lors de l’appel ou si l’utilisateur ferme la fenêtre popup du module de tâche à l’aide du X dans le coin supérieur `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` droit. <br/><br/> 3. Si l’utilisateur appuie sur un bouton Action.Submit, son objet est renvoyé `data` en tant que valeur de `result` . |
| **Bouton de carte bot** | 1. Les boutons de carte bot, en fonction du type de bouton, peuvent appeler des modules de tâche de deux manières : une URL de lien profond ou en envoyant un `task/fetch` message. Voir ci-dessous pour savoir comment fonctionnent les URL de liens profonds. <br/><br/> 2. Si l’action du bouton est ( type de bouton pour les cartes adaptatives), un événement (une DEMANDE HTTP en dessous) est envoyé au bot, et le bot répond au POST avec `type` `task/fetch` HTTP `Action.Submit` `task/fetch invoke` 200 [](#the-taskinfo-object)et le corps de la réponse contenant un wrapper autour de l’objet TaskInfo . Cela est expliqué en détail dans [l’facturation d’un module de tâche via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch).<br/><br/> 3. Teams le module de tâche ; Lorsque l’utilisateur a terminé, appelez la Teams SDK avec `tasks.submitTask()` `result` un objet comme paramètre. <br/><br/> 4. Le bot reçoit un `task/submit invoke` message contenant `result` l’objet. Vous pouvez répondre au message de trois manières différentes : en ne rien faire (la tâche s’est terminée correctement), en affichant un message à l’utilisateur dans une fenêtre popup ou en invoquant une autre fenêtre de module de tâche (c’est-à-dire en créant une expérience de `task/submit` l’Assistant). Ces trois options sont abordées plus en détail dans la [discussion détaillée sur la tâche/l’soumission.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) | 1. Comme les boutons des cartes Bot Framework, les boutons des cartes adaptatives offrent deux moyens d’appel des modules de tâche : les URL de liens profonds avec des boutons et l’utilisation de `Action.openUrl` `task/fetch` `Action.Submit` boutons. <br/><br/> 2. Les modules de tâche avec cartes adaptatives fonctionnent de manière très similaire au cas HTML/JavaScript (voir à gauche). La principale différence est que, étant donné qu’il n’existe pas de JavaScript lorsque vous utilisez des cartes adaptatives, il n’existe aucun moyen d’appeler `tasks.submitTask()` . Au lieu de cela, Teams l’objet et le renvoie en tant que charge utile de l’événement, `data` `Action.Submit` comme décrit `task/submit` [ici](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **URL du lien profond** <br/>[Syntaxe d'URL](#task-module-deep-link-syntax) | 1. Teams appelle le module de tâche ; URL qui apparaît à l’intérieur `<iframe>` de la valeur spécifiée dans le paramètre `url` du lien profond. Il n’y `submitHandler` a pas de rappel. <br/><br/> 2. Dans le JavaScript de la page dans le module de tâche, appelez pour le fermer avec un objet en tant que paramètre, comme lors de l’appel à partir d’un onglet ou d’un bouton de carte `tasks.submitTask()` `result` bot. La logique d’achèvement est toutefois légèrement différente. Si votre logique d’achèvement réside sur le client (c’est-à-dire, s’il n’y a pas de bot), il n’y a pas de rappel, de sorte que toute logique d’achèvement doit se trouver dans le code précédant l’appel vers `submitHandler` `tasks.submitTask()` . Les erreurs d’appel sont uniquement signalées via la console. Si vous avez un bot, vous pouvez spécifier un paramètre dans le lien profond pour envoyer l’objet `completionBotId` `result` via un `task/submit` événement. | 1. Teams appelle le module de tâche ; Le corps de la carte JSON de la carte adaptative est spécifié en tant que valeur codée URL du paramètre `card` du lien profond. <br/><br/> 2. L’utilisateur ferme le module de tâche en cliquant sur le X en haut à droite du module de tâche ou en appuyant sur un bouton `Action.Submit` de la carte. Étant donné qu’il n’y a pas d’appel, vous devez avoir un bot pour envoyer la valeur des champs de `submitHandler` carte adaptative. Vous utilisez le paramètre dans le lien profond pour spécifier le bot vers qui envoyer les `completionBotId` données via un `task/submit invoke` événement. |

## <a name="the-taskinfo-object"></a>Objet TaskInfo

`TaskInfo`L’objet contient les métadonnées d’un module de tâche. La définition d’objet est ci-dessous. Vous **devez définir** soit pour un `url` iFrame incorporé, `card` soit pour une carte adaptative.

| Attribut | Type | Description |
| --- | --- | --- |
| `title` | string | Apparaît sous le nom de l’application et à droite de l’icône de l’application. |
| `height` | valeur numérique ou chaîne | Il peut s’agit d’un nombre représentant la hauteur du module de tâche en pixels, `small` ou `medium` , ou `large` . [Voir ci-dessous comment la hauteur et la largeur sont gérées.](#task-module-sizing) |
| `width` | valeur numérique ou chaîne | Il peut s’agit d’un nombre représentant la largeur du module de tâche en pixels, `small` ou `medium` , ou `large` . [Voir ci-dessous comment la hauteur et la largeur sont gérées.](#task-module-sizing) |
| `url` | string | URL de la page chargée en tant qu’url `<iframe>` à l’intérieur du module de tâche. Le domaine de l’URL doit se trouver dans le tableau [validDomains](~/resources/schema/manifest-schema.md#validdomains) de l’application dans le manifeste de votre application. |
| `card` | Carte adaptative ou pièce jointe d’une carte de bot de carte adaptative | JSON de la carte adaptative à apparaître dans le module de tâche. Si vous voquer à partir d’un bot, vous devez utiliser la carte adaptative JSON dans un objet Bot `attachment` Framework. À partir d’un onglet, vous n’utiliserez qu’une carte adaptative. [Voici un exemple.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Si un client ne prend pas en charge la fonctionnalité de module de tâche, cette URL est ouverte dans un onglet de navigateur. |
| `completionBotId` | string | Spécifie un ID d’application de bot à envoyer au résultat de l’interaction de l’utilisateur avec le module de tâche. S’il est spécifié, le bot reçoit un événement avec un objet `task/submit invoke` JSON dans la charge utile de l’événement. |

> [!NOTE]
> La fonctionnalité de module de tâche nécessite que les domaines des URL que vous souhaitez charger soient inclus dans le tableau dans le manifeste `validDomains` de votre application.

## <a name="task-module-sizing"></a>Resserrage du module de tâche

À l’aide d’nombres integers `TaskInfo.width` pour et `TaskInfo.height` définira la hauteur et la largeur en pixels. Toutefois, en fonction de la taille de la fenêtre et de la résolution de l’écran de l’équipe, elles seront réduites proportionnellement tout en conservant les proportions (largeur/hauteur).

Si et sont , ou la taille du rectangle rouge dans l’image ci-dessus est une proportion de l’espace disponible `TaskInfo.width` `TaskInfo.height` : `"small"` `"medium"` `"large"` 20 %, 50 %, 60 % pour et `width` 20 %, 50 %, 66 % pour `height` .

Les modules de tâche appelés à partir d’un onglet peuvent être resserrisés dynamiquement. Après avoir appelé, vous pouvez appeler l’endroit où les propriétés de hauteur et de largeur de l’objet newSize sont conformes aux `tasks.startTask()` `tasks.updateTask(newSize)` spécifications TaskInfo (par exemple. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>Module de tâche CSS pour les modules de tâche HTML/JavaScript

Les modules de tâche HTML/JavaScript ont accès à toute la zone du module de tâche sous l’en-tête. Bien que cela offre beaucoup de flexibilité, si vous souhaitez que l’espacement autour des bords s’aligne sur les éléments d’en-tête et évite les barres de défilement inutiles, vous devez fournir le bon CSS. Voici quelques exemples pour quelques cas d’utilisation.

### <a name="example-1---youtube-video"></a>Exemple 1 - Vidéo YouTube

YouTube offre la possibilité d’incorporer des vidéos sur des pages web. À l’aide d’une page web stub simple, il est facile de l’afficher dans un module de tâche :

![Vidéo YouTube](~/assets/images/task-module/youtube-example.png)

Voici le code HTML de cette page, sans CSS :

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

Le CSS ressemble à ceci :

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

### <a name="example-2---powerapp"></a>Exemple 2 - PowerApp

Vous pouvez également utiliser la même approche pour incorporer un PowerApp. Comme la hauteur/largeur de n’importe quel PowerApp individuel est personnalisable, vous devrez peut-être ajuster la hauteur et la largeur pour obtenir la présentation souhaitée.

![PowerApp de gestion des biens](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

Et le CSS est :

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Carte adaptative ou pièce jointe de carte de bot de carte adaptative

Comme nous l’avons indiqué ci-dessus, selon la façon dont vous voquerez votre carte adaptative, vous devrez utiliser une carte adaptative ou une pièce jointe de carte de bot de carte adaptative (qui est simplement une carte adaptative wrapped dans un objet pièce `card` jointe).

Lorsque vous voquer à partir d’un onglet, vous devez utiliser une carte adaptative. Voici un exemple très simple :

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

Lorsque vous voquer à partir d’un bot, vous devez utiliser une pièce jointe de carte de bot de carte adaptative, comme dans l’exemple ci-dessous :

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

Vous devez vous souvenir si vous voquer un module de tâche contenant une carte adaptative à partir d’un bot ou d’un onglet.

## <a name="task-module-deep-link-syntax"></a>Syntaxe de lien profond du module de tâche

Un lien profond de module de tâche est simplement une sérialisation de l’objet [TaskInfo](#the-taskinfo-object) avec deux autres éléments d’informations, et éventuellement les éléments `APP_ID` suivants `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Voir [l’objet TaskInfo](#the-taskinfo-object) pour les types de données et les valeurs permises `<TaskInfo.url>` pour , , et `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Assurez-vous d’encoder l’URL du lien profond, en particulier lorsque vous utilisez le paramètre (par exemple, la fonction `card` JavaScript). [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

Voici les informations sur `APP_ID` et `BOT_APP_ID` :

| Valeur | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| `APP_ID` | string | Oui | ID [de l’application](~/resources/schema/manifest-schema.md#id) qui invoquer le module de tâche. Le [tableau validDomains dans](~/resources/schema/manifest-schema.md#validdomains) le manifeste doit contenir le domaine pour si se trouve dans `APP_ID` `url` `url` l’URL. (L’ID d’application est déjà connu lorsqu’un module de tâche est appelé à partir d’un onglet ou d’un bot, c’est pourquoi il n’est pas inclus `TaskInfo` dans .) |
| `BOT_APP_ID` | string | Non | Si une valeur `completionBotId` est spécifiée, l’objet est envoyé via un message au `result` bot `task/submit invoke` spécifié. `BOT_APP_ID` doit être spécifié en tant que bot dans le manifeste de l’application, c’est-à-dire que vous ne pouvez pas simplement l’envoyer à un bot. |

Notez qu’il est valide pour et doit être identique, et dans de nombreux cas, si une application possède un bot, car il est recommandé de `APP_ID` `BOT_APP_ID` l’utiliser comme ID d’application s’il en existe un.

## <a name="keyboard-and-accessibility-guidelines"></a>Recommandations en matière de clavier et d’accessibilité

Avec les modules de tâche HTML/JavaScript, il est de votre responsabilité de vous assurer que le module de tâche de votre application peut être utilisé avec un clavier. Les programmes de lecteur d’écran dépendent également de la possibilité de naviguer à l’aide du clavier. En pratique, cela signifie deux choses :

1. Utilisation de l’attribut [tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) dans vos balises HTML pour contrôler les éléments qui peuvent être focusés et si/où il participe à la navigation séquentielle au clavier (généralement avec les touches <kbd>Tab</kbd> et <kbd>Shift-Tab).</kbd>
2. Gestion de la <kbd>touche Échap</kbd> dans javaScript pour votre module de tâche. Voici un exemple de code montrant comment faire :

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams vous assurer que la navigation au clavier fonctionne correctement à partir de l’en-tête du module de tâche dans votre code HTML et inversement.

## <a name="code-sample"></a>Exemple de code
|**Exemple de nom** | **Description** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Exemple de module de tâche (Bots-V4) | Exemples de création de modules de tâche. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|Exemple de module de tâche (Onglets + Bots-V3) | Exemples de création de modules de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer des fonctionnalités d’emplacement dans Teams](../concepts/device-capabilities/location-capability.md)
