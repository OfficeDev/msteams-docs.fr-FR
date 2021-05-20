---
title: Qu-est-ce qu’un module de tâche ?
author: clearab
description: Ajoutez des expériences contextup modales pour collecter ou afficher des informations à vos utilisateurs à partir de vos applications Microsoft Teams vidéo
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

Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’intérieur du popup, vous pouvez exécuter votre propre code HTML/JavaScript personnalisé, afficher `<iframe>` un widget basé sur un YouTube ou une vidéo Microsoft Stream ou afficher une carte [adaptative.](/adaptive-cards/) Ils sont particulièrement utiles pour initier et effectuer des tâches, ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Une expérience contextuelle est souvent plus naturelle pour les utilisateurs qui initient et effectuent des tâches, par rapport à une expérience d’onglet ou de bot basée sur une conversation.

Les modules de tâches s’appuient sur la base Microsoft Teams onglets; ils sont essentiellement un onglet à l’intérieur d’une fenêtre popup. Ils utilisent le même SDK, donc si vous avez construit un onglet, vous êtes déjà 90% du chemin pour être en mesure de créer un module de tâche.

Les modules de tâche peuvent être appelés de trois façons :

* **Onglets canal ou personnels**: En utilisant le Microsoft Teams Tabs SDK, vous pouvez invoquer des modules de tâches à partir de boutons, de liens ou de menus sur votre [onglet. Ceci est couvert en détail ici.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bots**: Boutons sur les [cartes envoyées](~/task-modules-and-cards/cards/cards-reference.md) par votre bot. Ceci est particulièrement utile lorsque vous n’avez pas besoin de tout le monde dans un canal pour voir ce que vous faites avec un bot. Par exemple, lorsque des utilisateurs répondent à un sondage dans un canal, il n'est pas très utile de voir un enregistrement de ce sondage. [Ceci est couvert en détail ici.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **En dehors de Teams à partir d’un lien profond**: vous pouvez également créer des URL pour invoquer un module de tâches de n’importe où. [Ceci est couvert en détail ici.](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>Module de tâche ressemble

Voici à quoi ressemble un module de tâche lorsqu’il est invoqué à partir d’un bot (sans les rectangles colorés et les cercles numérotés, bien sûr):

![Exemple de module de tâche](~/assets/images/task-module/task-module-example.png)

Passons à travers elle:

1. Icône de votre [ `color` application](~/resources/schema/manifest-schema.md#icons).
1. Nom de votre [ `short` application](~/resources/schema/manifest-schema.md#name).
1. Le titre du module de tâche spécifié dans la `title` propriété de [l’objet TaskInfo](#the-taskinfo-object).
1. Le bouton fermer/annuler du module de tâches. Si l’utilisateur appuie sur cela, votre application recevra un `err` événement tel que décrit [ici](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).
    > [!Note]
    > Il n’est actuellement pas possible de détecter cet événement lorsqu’un module de tâche est invoqué à partir d’un bot.
1. Le rectangle bleu est l’endroit où votre page Web apparaît si vous chargez votre propre page Web en utilisant `url` la propriété de [l’objet TaskInfo](#the-taskinfo-object). Plus de détails se trouve dans la section [dimensionnement du module de tâches](#task-module-sizing) ci-dessous.
1. Si vous affichez une carte adaptative via la `card` propriété de [l’objet TaskInfo,](#the-taskinfo-object) le rembourrage est ajouté pour vous, sinon vous devrez [gérer cela vous-même.](#task-module-css-for-htmljavascript-task-modules)
1. Les boutons de carte adaptatifs s’rendront ici. Si vous utilisez votre propre page, vous devez créer vos propres boutons.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Vue d’ensemble de l’invocation et du rejet des modules de tâches

Les modules de tâches peuvent être invoqués à partir d’onglets, de bots ou de liens profonds et ce qui apparaît dans l’un d’eux peut être html ou une carte adaptative, il ya donc beaucoup de flexibilité en termes de la façon dont ils sont invoqués et comment traiter le résultat de l’interaction d’un utilisateur. Le tableau ci-dessous résume comment cela fonctionne :

| **Invoqué via...** | **Le module de tâche est HTML/JavaScript** | **Le module de tâche est carte adaptative** |
| --- | --- | --- |
| **JavaScript dans un onglet** | 1. Utilisez la fonction Teams client SDK avec `tasks.startTask()` une fonction de rappel `submitHandler(err, result)` optionnelle. <br/><br/> 2. Dans le code du module de tâche, lorsque l’utilisateur est terminé, appelez la fonction Teams SDK `tasks.submitTask()` avec un objet comme `result` paramètre. Si un `submitHandler` rappel a été `tasks.startTask()` spécifié, Teams l’appelle `result` comme paramètre.<br/><br/> 3. S’il y a eu une erreur lors de l’invocation, `tasks.startTask()` la fonction est appelée avec une chaîne à la `submitHandler` `err` place. <br/><br/> 4. Vous pouvez également spécifier un `completionBotId` lors de `teams.startTask()` l’appel - dans ce `result` cas est envoyé au bot à la place. | 1. Appelez la fonction Teams client SDK `tasks.startTask()` avec [un objet TaskInfo](#the-taskinfo-object) `TaskInfo.card` et contenant le JSON pour que la carte Adaptative s’affiche dans le popup du module de tâches. <br/><br/> 2. Si un rappel a été spécifié, Teams l’appelle avec une chaîne s’il y a eu une `submitHandler` `tasks.startTask()` erreur lors de `err` l’invocation ou si l’utilisateur ferme le module de tâche popup en `tasks.startTask()` utilisant le X en haut à droite. <br/><br/> 3. Si l’utilisateur appuie sur un bouton Action.Submit, son `data` objet est retourné comme valeur de `result` . |
| **Bouton de carte bot** | 1. Les boutons de carte Bot, selon le type de bouton, peuvent invoquer les modules de tâches de deux façons : une URL de lien profond ou en envoyant un `task/fetch` message. Voir ci-dessous pour savoir comment fonctionnent les URL de liaison profonde. <br/><br/> 2. Si l’action du bouton `type` est `task/fetch` `Action.Submit` (type de bouton pour les cartes adaptatives), `task/fetch invoke` un événement (un HTTP POST sous les couvertures) est envoyé au bot, et le bot répond au POST avec HTTP 200 et le corps de réponse contenant un emballage autour de l’objet [TaskInfo](#the-taskinfo-object). Ceci est expliqué en détail en [invoquant un module de tâche via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch).<br/><br/> 3. Teams le module de tâche; lorsque l’utilisateur est terminé, appelez Teams fonction SDK `tasks.submitTask()` avec un objet comme `result` paramètre. <br/><br/> 4. Le bot reçoit un `task/submit invoke` message qui contient `result` l’objet. Vous avez trois façons différentes de répondre au `task/submit` message : en ne faisant rien (la tâche accomplie avec succès), en affichant un message à l’utilisateur dans une fenêtre contexturée, ou en invoquant une autre fenêtre de module de tâche (c’est-à-dire en créant une expérience de type assistant). Ces trois options sont examinées plus [en détail dans la discussion sur la tâche / soumettre](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | 1. Comme les boutons sur les cartes Bot Framework, les boutons sur les cartes adaptatives soutiennent deux façons d’invoquer des modules de tâches : les URL de liaison profonde `Action.openUrl` avec boutons, et par l’utilisation `task/fetch` de `Action.Submit` boutons. <br/><br/> 2. Les modules de tâches avec cartes adaptatives fonctionnent de façon très similaire à l’étui HTML/JavaScript (voir à gauche). La principale différence est que puisqu’il n’y a pas de JavaScript lorsque vous utilisez des cartes adaptatives, il n’y a aucun moyen d’appeler `tasks.submitTask()` . Au lieu Teams, il prend `data` `Action.Submit` l’objet et le renvoie comme la charge utile de dans `task/submit` l’événement, comme décrit [ici](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **URL de lien profond** <br/>[Syntaxe d'URL](#task-module-deep-link-syntax) | 1. Teams invoque le module de tâche; l’URL qui apparaît à `<iframe>` l’intérieur du spécifié dans le `url` paramètre du lien profond. Il n’y a `submitHandler` pas de rappel. <br/><br/> 2. Dans le JavaScript de la page dans le module de tâche, appelez `tasks.submitTask()` pour le fermer avec un objet comme paramètre, le même que lors de son `result` invocation à partir d’un onglet ou d’un bouton de carte bot. La logique d’achèvement est légèrement différente, cependant. Si votre logique d’achèvement réside sur le client (c’est-à-dire s’il n’y a pas de bot), il n’y `submitHandler` a pas de rappel, donc toute logique d’achèvement doit être dans le code précédant l’appel à `tasks.submitTask()` . Les erreurs d’invocation ne sont signalées que via la console. Si vous avez un bot, alors vous pouvez spécifier `completionBotId` un paramètre dans le lien profond pour envoyer `result` l’objet via un `task/submit` événement. | 1. Teams invoque le module de tâche; le corps de la carte JSON de la carte Adaptative est spécifié comme une valeur codée par URL du `card` paramètre du lien profond. <br/><br/> 2. L’utilisateur ferme le module de tâche en cliquant sur le X en haut à droite du module de tâche ou en appuyant sur `Action.Submit` un bouton sur la carte. Comme il n’y `submitHandler` a pas d’appel, vous devez avoir un bot pour envoyer la valeur des champs de cartes adaptatives à. Vous utilisez le `completionBotId` paramètre dans le lien profond pour spécifier le bot pour envoyer les données via un `task/submit invoke` événement. |

## <a name="the-taskinfo-object"></a>L’objet TaskInfo

`TaskInfo`L’objet contient les métadonnées d’un module de tâches. La définition de l’objet est ci-dessous. Vous **devez** définir soit `url` pour un iFrame intégré, soit `card` pour une carte adaptative.

| Attribut | Type | Description |
| --- | --- | --- |
| `title` | string | Apparaît sous le nom de l’application et à droite de l’icône de l’application. |
| `height` | valeur numérique ou chaîne | Il peut s’agir d’un nombre représentant la hauteur du module de tâche en pixels, `small` ou `medium` , ou `large` . [Voir ci-dessous pour la façon dont la hauteur et la largeur sont traitées](#task-module-sizing). |
| `width` | valeur numérique ou chaîne | Il peut s’agir d’un nombre représentant la largeur du module de tâche en pixels, `small` ou `medium` , ou `large` . [Voir ci-dessous pour la façon dont la hauteur et la largeur sont traitées](#task-module-sizing). |
| `url` | string | L’URL de la page chargée comme un intérieur `<iframe>` du module de tâche. Le domaine de l’URL doit être dans le tableau [ValidDomains de l’application](~/resources/schema/manifest-schema.md#validdomains) dans le manifeste de votre application. |
| `card` | Carte adaptative ou pièce jointe de carte adaptative bot | Le JSON pour la carte Adaptative à apparaître dans le module de tâche. Si vous invoquez à partir d’un bot, vous devrez utiliser la carte adaptative JSON dans un objet Bot `attachment` Framework. À partir d’un onglet, vous n’utiliserez qu’une carte adaptative. [Voici un exemple.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Si un client ne prend pas en charge la fonction module de tâche, cette URL est ouverte dans un onglet navigateur. |
| `completionBotId` | string | Spécifie un ID d’application bot pour envoyer le résultat de l’interaction de l’utilisateur avec le module de tâche à. S’il est spécifié, le bot recevra `task/submit invoke` un événement avec un objet JSON dans la charge utile de l’événement. |

> [!NOTE]
> La fonction module de tâche exige que les domaines de toutes les URL que vous souhaitez charger soient inclus dans `validDomains` le tableau dans le manifeste de votre application.

## <a name="task-module-sizing"></a>Dimensionnement du module de tâches

Utilisation d’entiers pour `TaskInfo.width` et `TaskInfo.height` définira la hauteur et la largeur en pixels. Toutefois, selon la taille de la fenêtre et de la résolution de l’écran de l’équipe, ils seront réduits proportionnellement tout en maintenant le rapport d’aspect (largeur/hauteur).

Si `TaskInfo.width` et sont , ou la taille du rectangle rouge dans `TaskInfo.height` `"small"` `"medium"` `"large"` l’image ci-dessus est une proportion de l’espace disponible: 20%, 50%, 60% pour `width` et 20%, 50%, 66% pour `height` .

Les modules de tâches invoqués à partir d’un onglet peuvent être ressurés dynamiquement. Après avoir `tasks.startTask()` appelé, vous pouvez appeler `tasks.updateTask(newSize)` lorsque les propriétés de hauteur et de largeur sur le nouvel objet Size sont conformes à la spécification TaskInfo (ex. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>Module de tâches CSS pour modules de tâches HTML/JavaScript

Les modules de tâches html/JavaScript ont accès à toute la zone du module de tâches sous l’en-tête. Bien que cela offre beaucoup de flexibilité, si vous voulez rembourrage sur les bords pour s’aligner avec les éléments de l’en-tête et éviter les barres de défilement inutiles, vous aurez besoin de fournir le bon CSS. Voici quelques exemples pour quelques cas d’utilisation.

### <a name="example-1---youtube-video"></a>Exemple 1 - Vidéo YouTube

YouTube offre la possibilité d’intégrer des vidéos sur les pages Web. À l’aide d’une simple page Web stub, il est facile de le montrer dans un module de tâches :

![Vidéo YouTube](~/assets/images/task-module/youtube-example.png)

Voici le HTML pour cette page, sans le CSS:

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

Vous pouvez également utiliser la même approche pour intégrer un PowerApp. Comme la hauteur/largeur de n’importe quel PowerApp individuel est personnalisable, vous devrez peut-être ajuster la hauteur et la largeur pour atteindre la présentation souhaitée.

![PowerApp gestion d’actifs](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

Et le CSS est:

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Carte adaptative ou pièce jointe de carte adaptative bot

Comme nous l’avons mentionné ci-dessus, selon la façon dont vous invoquez votre `card` vous aurez besoin d’utiliser soit une carte adaptative, ou une pièce jointe de carte de bot carte adaptative (qui est juste une carte adaptative enveloppée dans un objet de pièce jointe).

Lorsque vous invoquez à partir d’un onglet, vous devrez utiliser une carte adaptative. Voici un exemple très simple :

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

Lorsque vous invoquez à partir d’un bot, vous devrez utiliser une pièce jointe de carte de bot de carte adaptative comme dans l’exemple ci-dessous :

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

Vous devez vous rappeler si vous invoquez un module de tâches contenant une carte adaptative à partir d’un bot ou d’un onglet.

## <a name="task-module-deep-link-syntax"></a>Syntaxe de lien profond de module de tâche

Un lien profond de module de tâche est juste une sérialisation de [l’objet TaskInfo](#the-taskinfo-object) avec deux autres éléments d’information, `APP_ID` et en option le `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Voir [l’objet TaskInfo](#the-taskinfo-object) pour les types de données et les valeurs `<TaskInfo.url>` permises pour `<TaskInfo.card>` , , , et `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` .

> [!TIP]
> Assurez-vous d’encoder le lien profond par URL, en particulier lors de `card` l’utilisation du [ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)paramètre (par exemple, la fonction JavaScript).

Voici les informations sur `APP_ID` et `BOT_APP_ID` :

| Valeur | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| `APP_ID` | string | Oui | [L’id](~/resources/schema/manifest-schema.md#id) de l’application invoquant le module de tâche. Le [tableau ValidDomains dans](~/resources/schema/manifest-schema.md#validdomains) le manifeste pour doit contenir le domaine pour si est dans `APP_ID` `url` `url` l’URL. (L’ID de l’application est déjà connu lorsqu’un module de tâche est invoqué à partir d’un onglet ou d’un bot, c’est pourquoi il n’est pas inclus `TaskInfo` dans .) |
| `BOT_APP_ID` | string | Non | Si une valeur est `completionBotId` spécifiée, `result` l’objet est envoyé via un `task/submit invoke` message au bot spécifié. `BOT_APP_ID` doit être spécifié comme un bot dans le manifeste de l’application, c’est-à-dire que vous ne pouvez pas simplement l’envoyer à n’importe quel bot. |

Notez qu’il est valable pour et `APP_ID` `BOT_APP_ID` d’être le même, et dans de nombreux cas sera si une application a un bot car il est recommandé d’utiliser cela comme id d’une application s’il ya un.

## <a name="keyboard-and-accessibility-guidelines"></a>Lignes directrices sur le clavier et l’accessibilité

Avec les modules de tâches html/JavaScript, il est de votre responsabilité de vous assurer que le module de tâches de votre application peut être utilisé avec un clavier. Les programmes de lecteur d’écran dépendent également de la capacité de naviguer à l’aide du clavier. En pratique, cela signifie deux choses :

1. Utilisation de [l’attribut tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) dans vos balises HTML pour contrôler quels éléments peuvent être ciblés et s’il participe à la navigation séquentielle du clavier (généralement avec <kbd>les touches Tab</kbd> et <kbd>Shift-Tab).</kbd>
2. Gestion de <kbd>la clé Esc</kbd> dans le JavaScript pour votre module de tâches. Voici un exemple de code montrant comment le faire :

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams vous assurerez que la navigation clavier fonctionne correctement à partir de l’en-tête du module de tâche dans votre HTML et vice-versa.

## <a name="code-sample"></a>Exemple de code
|**Nom de l’échantillon** | **Description** | **.NET (en)** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Exemple de module de tâche (Bots-V4) | Échantillons pour la création de modules de tâches. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|Exemple de module de tâche (Onglets + Bots-V3) | Échantillons pour la création de modules de tâches. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer la capacité de scanner QR ou de code à barres dans Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les capacités de localisation dans Teams](../concepts/device-capabilities/location-capability.md)
