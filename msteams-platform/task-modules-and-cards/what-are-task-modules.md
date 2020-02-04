---
title: Qu’est-ce qu’un module de tâches ?
author: clearab
description: Ajoutez des expériences contextuelles modales pour collecter ou afficher des informations pour vos utilisateurs à partir de vos applications Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 22fdc7a9dab1ff6f27e2b0d144e54676b6cca50e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673974"
---
# <a name="what-are-task-modules"></a>Qu’est-ce qu’un module de tâches ?

Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’intérieur de la fenêtre contextuelle, vous pouvez exécuter votre propre code HTML/ `<iframe>`JavaScript personnalisé, afficher un widget basé sur une vidéo YouTube ou une vidéo Microsoft Stream, ou afficher une [carte adaptative](/adaptive-cards/). Elles sont particulièrement utiles pour lancer et effectuer des tâches ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Une expérience contextuelle est souvent plus naturelle pour les utilisateurs qui initient et effectuent des tâches par rapport à un onglet ou à une expérience de robot basée sur une conversation.

Les modules de tâches sont présentés sous la base des onglets Microsoft teams ; Il s’agit essentiellement d’un onglet à l’intérieur d’une fenêtre contextuelle. Ils utilisent le même Kit de développement logiciel (SDK), donc si vous avez créé un onglet, vous avez déjà 90% de la façon de créer un module de tâches.

Les modules de tâches peuvent être appelés de trois façons :

* **Onglets de canal ou personnel.** À l’aide du kit de développement Microsoft Teams, vous pouvez appeler des modules de tâches à partir des boutons, des liens ou des menus de votre onglet. [cette information est décrite en détail ici.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bots.** Boutons sur les [cartes](~/task-modules-and-cards/cards/cards-reference.md) envoyées à partir de votre robot. Ceci est particulièrement utile lorsque vous n’avez pas besoin de tous les utilisateurs d’un canal pour voir ce que vous faites avec un bot. Par exemple, lorsque les utilisateurs répondent à un sondage dans un canal, il n’est pas très utile de voir un enregistrement de cette interrogation en cours de création. [Cette information est décrite en détail ici.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **En dehors de teams à partir d’un lien profond.** Vous pouvez également créer des URL pour appeler un module de tâches depuis n’importe quel endroit. [Cette information est décrite en détail ici.](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>À quoi ressemble un module de tâche ?

Voici à quoi ressemble un module de tâche lorsqu’il est appelé à partir d’un bot (sans les rectangles de couleur et les cercles numérotés, bien entendu) :

![Exemple de module de tâche](~/assets/images/task-module/task-module-example.png)

Passons en revue les éléments suivants :

1. [ `color` Icône](~/resources/schema/manifest-schema.md#icons)de votre application.
2. [ `short` Nom](~/resources/schema/manifest-schema.md#name)de votre application.
3. Titre du module de tâche spécifié dans la `title` propriété de l' [objet TaskInfo](#the-taskinfo-object).
4. Bouton Fermer/annuler du module tâches. Si l’utilisateur appuie sur cette touche, votre application reçoit un `err` événement tel que décrit [ici](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module). (**Remarque :** il n’est pas possible de détecter cet événement actuellement lorsqu’un module de tâche est appelé à partir d’un bot.)
5. Le rectangle bleu est l’emplacement où votre page Web apparaît si vous chargez votre page Web à l' `url` aide de la propriété de l' [objet TaskInfo](#the-taskinfo-object). Vous trouverez plus de détails dans la section [dimensionnement du module tâches](#task-module-sizing) ci-dessous.
6. Si vous affichez une carte adaptative via la `card` propriété de l' [objet TaskInfo](#the-taskinfo-object) auquel le remplissage est ajouté, dans le cas contraire, vous devrez le [gérer vous-même](#task-module-css-for-htmljavascript-task-modules).
7. Les boutons de carte adaptative s’affichent ici. Si vous utilisez votre propre page, vous devez créer vos propres boutons.

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>Vue d’ensemble des modules de tâches d’appel et de disparition

Les modules de tâches peuvent être appelés à partir de tabulations, robots ou liens détaillés et ce qui apparaît dans un peut être soit du code HTML, soit une carte adaptative, de sorte qu’il dispose de beaucoup de flexibilité quant à l’appel et à la façon de traiter le résultat de l’interaction d’un utilisateur. Le tableau ci-dessous récapitule le fonctionnement :

| **Appelé via...** | **Le module de tâches est HTML/JavaScript** | **Le module de tâche est une carte adaptative** |
| --- | --- | --- |
| **JavaScript dans un onglet** | 1. utiliser la fonction `tasks.startTask()` de kit de développement logiciel client `submitHandler(err, result)` teams avec une fonction de rappel facultative <br/><br/> 2. dans le code du module de tâche, lorsque l’utilisateur a terminé, appelez la fonction `tasks.submitTask()` Kit de `result` développement logiciel (SDK) teams avec un objet en tant que paramètre. Si un `submitHandler` rappel a été spécifié `tasks.startTask()`dans, teams l' `result` appelle en tant que paramètre.<br/><br/> 3. Si une erreur s’est produite lors de `tasks.startTask()`l’appel `submitHandler` , la fonction est appelée `err` avec une chaîne à la place. <br/><br/> 4. vous pouvez également spécifier un `completionBotId` lors de `teams.startTask()` l’appel, ce `result` qui est envoyé au robot à la place. | 1. appelez la fonction `tasks.startTask()` de kit de développement logiciel client teams avec un [objet TaskInfo](#the-taskinfo-object) et `TaskInfo.card` contenant le JSON de la carte adaptative à afficher dans le menu contextuel du module de tâche. <br/><br/> 2. Si un `submitHandler` rappel a été spécifié `tasks.startTask()`dans, teams l’appelle `err` avec une chaîne si une erreur s’est produite `tasks.startTask()` lors de l’appel ou si l’utilisateur ferme le menu contextuel du module de tâche en utilisant le X en haut à droite. <br/><br/> 3. si l’utilisateur appuie sur un bouton action. Submit, son `data` objet est renvoyé comme valeur de `result`. |
| **Bouton de carte bot** | 1 les boutons de carte. bot, selon le type de bouton, peuvent appeler des modules de tâches de deux manières : une URL de lien hypertexte ou `task/fetch` l’envoi d’un message. Voir ci-dessous pour savoir comment fonctionnent les URL de liens. <br/><br/> 2. Si `type` l’action du bouton est `task/fetch` (`Action.Submit` type de bouton pour les cartes adaptatives) `task/fetch invoke` , un événement (un billet http sous les couvertures) est envoyé au bot, et le bot répond au billet avec http 200 et le corps de la réponse contenant un wrapper entourant l' [objet TaskInfo](#the-taskinfo-object). Cette étape est expliquée en détail dans l' [appel d’un module de tâches via Task/FETCH](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).<br/><br/> 3. teams affiche le module tâches ; une fois l’utilisateur terminé, appelez la fonction `tasks.submitTask()` Team SDK avec un `result` objet en tant que paramètre. <br/><br/> 4. le bot reçoit un `task/submit invoke` message qui contient l' `result` objet. Vous disposez de trois façons différentes de répondre au `task/submit` message : en ne faisant rien (la tâche s’est terminée correctement), en affichant un message pour l’utilisateur dans une fenêtre contextuelle ou en appelant une autre fenêtre de module de tâche (c’est-à-dire en créant une expérience de type assistant). Ces trois options sont décrites plus [en détail dans la rubrique discussion détaillée sur la tâche/l’envoi](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). | 1. comme les boutons sur les cartes de l’infrastructure bot, les boutons sur les cartes adaptatives prennent en charge deux façons d’appeler `Action.openUrl` des modules de tâches `task/fetch` : `Action.Submit` URL de liens en profondeur avec boutons et via à l’aide de boutons. <br/><br/> 2. les modules de tâches avec cartes adaptatives fonctionnent de façon très similaire à la casse HTML/JavaScript (voir Left). La principale différence est qu’étant donné qu’il n’y a aucun code JavaScript lorsque vous utilisez des cartes adaptatives, il `tasks.submitTask()`n’existe aucun moyen d’appeler. En revanche, teams `data` prend l' `Action.Submit` objet de et le renvoie comme charge utile de `task/submit` dans l’événement, comme décrit [ici](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit). |
| **URL de liens détaillés** <br/>[Syntaxe d'URL](#task-module-deep-link-syntax) | 1. teams appelle le module tâches ; URL qui apparaît à l’intérieur `<iframe>` du paramètre spécifié `url` dans le paramètre du lien profond. Il n’y `submitHandler` a pas de rappel. <br/><br/> 2. dans le code JavaScript de la page dans le module de tâche `tasks.submitTask()` , appelez pour le fermer `result` avec un objet en tant que paramètre, de la même manière que lors de son appel à partir d’un bouton de la carte ou d’un bouton de carte de robot. La logique de fin est légèrement différente. Si votre logique de saisie réside sur le client (c’est-à-dire s’il n’y a aucun bot), il n' `submitHandler` y a aucun rappel, de sorte que toute logique d’achèvement doit se trouver `tasks.submitTask()`dans le code précédant l’appel à. Les erreurs d’invocation sont uniquement signalées via la console. Si vous avez un bot, vous pouvez spécifier un `completionBotId` paramètre dans le lien profond pour envoyer l' `result` objet via un `task/submit` événement. | 1. teams appelle le module tâches ; le corps de la carte JSON de la carte adaptative est spécifié en tant que valeur codée URL du `card` paramètre du lien profond. <br/><br/> 2. l’utilisateur ferme le module de tâche en cliquant sur le X dans le coin supérieur droit du module de tâches ou en `Action.Submit` appuyant sur un bouton de la carte. Étant donné qu’il `submitHandler` n’y a pas à appeler, vous devez disposer d’un bot pour envoyer la valeur des champs de carte adaptative à. Vous utilisez le `completionBotId` paramètre dans le lien profond pour spécifier le bot auquel envoyer les données via un `task/submit invoke` événement. |

> [!NOTE]
> L’appel d’un module de tâches à partir de JavaScript n’est pas pris en charge sur mobile.

## <a name="the-taskinfo-object"></a>L’objet TaskInfo

L' `TaskInfo` objet contient les métadonnées d’un module de tâche. La définition de l’objet est ci-dessous. Vous **devez** définir soit `url` (pour un IFRAME en Embedded `card` ), soit (pour une carte adaptative).

| Attribut | Type | Description |
| --- | --- | --- |
| `title` | string | Apparaît sous le nom de l’application et à droite de l’icône de l’application |
| `height` | valeur numérique ou chaîne | Il peut s’agir d’un nombre représentant la hauteur du module de tâche en `small`pixels `medium`, ou `large`, ou. [Voir ci-dessous la manière dont la hauteur et la largeur sont gérées](#task-module-sizing). |
| `width` | valeur numérique ou chaîne | Il peut s’agir d’un nombre représentant la largeur du module de tâche en `small`pixels `medium`, ou `large`, ou. [Voir ci-dessous la manière dont la hauteur et la largeur sont gérées](#task-module-sizing). |
| `url` | string | URL de la page chargée en tant que `<iframe>` module dans le module de tâches. Le domaine de l’URL doit se trouver dans le [tableau validDomains](~/resources/schema/manifest-schema.md#validdomains) de l’application dans le manifeste de votre application. |
| `card` | Carte adaptative ou pièce jointe de carte de robot de carte adaptative | JSON de la carte adaptative à apparaître dans le module de tâches. Si vous appelez à partir d’un bot, vous devrez utiliser le JSON de la carte adaptative dans un objet de l' `attachment` infrastructure bot. À partir d’un onglet, vous n’utiliserez qu’une carte adaptative. [Voici un exemple.](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | Si un client ne prend pas en charge la fonctionnalité de module de tâche, cette URL est ouverte dans un onglet de navigateur. |
| `completionBotId` | string | Spécifie un ID d’application bot pour envoyer le résultat de l’interaction de l’utilisateur avec le module de tâche. S’il est spécifié, le bot reçoit `task/submit invoke` un événement avec un objet JSON dans la charge utile de l’événement. |

> [!NOTE]
> La fonctionnalité de module de tâche nécessite que les domaines des URL que vous souhaitez charger soient inclus dans `validDomains` le tableau dans le manifeste de votre application.

## <a name="task-module-sizing"></a>Dimensionnement du module de tâche

En utilisant des `TaskInfo.width` entiers `TaskInfo.height` pour et définira la hauteur et la largeur en pixels. Toutefois, en fonction de la taille de la fenêtre de l’équipe et de la résolution de l’écran, elles seront réduites proportionnellement tout en conservant les proportions (largeur/hauteur).

Si `TaskInfo.width` et `TaskInfo.height` est `"small"`, `"medium"` ou `"large"` si la taille du rectangle rouge dans l’image ci-dessus est une proportion de l’espace disponible : 20%, 50%, 60 `width` % pour et 20%, 50%, 66 `height`% pour.

Les modules de tâches appelés à partir d’un onglet peuvent être redimensionnés dynamiquement. Après l' `tasks.startTask()` appel, vous `tasks.updateTask(newSize)` pouvez appeler les propriétés Height et Width de l’objet NewSize conformément aux spécifications de TaskInfo (par exemple, `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>Module de tâches CSS pour les modules de tâches HTML/JavaScript

Les modules de tâches HTML/JavaScript ont accès à toute la zone du module tâches sous l’en-tête. Bien que cela offre une grande flexibilité, si vous voulez que le remplissage des bords s’aligne sur les éléments d’en-tête et éviter les barres de défilement inutiles, vous devrez fournir le CSS approprié. Voici quelques exemples pour quelques cas d’utilisation.

### <a name="example-1---youtube-video"></a>Exemple 1 : vidéo YouTube

YouTube offre la possibilité d’incorporer des vidéos sur des pages Web. À l’aide d’une page Web stub simple, il est facile de l’afficher dans un module de tâches :

![Vidéo YouTube](~/assets/images/task-module/youtube-example.png)

Voici le code HTML de cette page, sans la feuille de style CSS :

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

La feuille de style CSS se présente comme suit :

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

### <a name="example-2---powerapp"></a>Exemple 2 : PowerApp

Vous pouvez également utiliser la même approche pour intégrer un PowerApp. La hauteur et la largeur de chaque PowerApp étant personnalisables, il se peut que vous deviez ajuster la hauteur et la largeur pour obtenir la présentation souhaitée.

![Gestion des biens PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

Et la feuille de style CSS est la suivante :

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Carte adaptative ou pièce jointe de carte de carte adaptative

Comme indiqué ci-dessus, en fonction de la façon dont vous appelez `card` votre, vous devrez utiliser une carte adaptative ou une pièce jointe de carte de carte de carte adaptative (qui n’est qu’une carte adaptative dans un objet Attachment).

Lorsque vous appelez à partir d’un onglet, vous devez utiliser une carte adaptative. Voici un exemple très simple :

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

Lorsque vous appelez à partir d’un robot, vous devez utiliser une pièce jointe de carte de carte adaptative comme dans l’exemple ci-dessous :

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

Vous devez garder à l’esprit si vous appelez un module de tâches contenant une carte adaptative à partir d’un bot ou d’un onglet.

## <a name="task-module-deep-link-syntax"></a>Syntaxe des liens détaillés des modules de tâches

Un lien détaillé de module de tâches est simplement une sérialisation de l' [objet TaskInfo](#the-taskinfo-object) avec deux autres informations, `APP_ID` et éventuellement : `BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

Voir [objet TaskInfo](#the-taskinfo-object) pour les types de données et les valeurs autorisées `<TaskInfo.url>`pour `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, et `<TaskInfo.title>`.

> [!TIP]
> Assurez-vous que l’URL Encode le lien profond, en `card` particulier lorsque vous utilisez le paramètre (par exemple, la [ `encodeURI()` fonction](https://www.w3schools.com/jsref/jsref_encodeURI.asp)de JavaScript).

Voici les informations sur `APP_ID` et : `BOT_APP_ID`

| Valeur | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| `APP_ID` | string | Oui | [ID](~/resources/schema/manifest-schema.md#id) de l’application appelant le module de tâches. Le [tableau validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le manifeste de `APP_ID` doit contenir le domaine pour `url` si `url` se trouve dans l’URL. (L’ID de l’application est déjà connu lorsqu’un module de tâche est appelé à partir d’un onglet ou d’un bot, c’est pourquoi `TaskInfo`il n’est pas inclus dans.) |
| `BOT_APP_ID` | string | Non | Si une valeur `completionBotId` est spécifiée, l' `result` objet est envoyé par le biais d' `task/submit invoke` un message au bot spécifié. `BOT_APP_ID`doit être spécifié en tant que bot dans le manifeste de l’application, autrement dit, vous ne pouvez pas simplement l’envoyer à un bot. |

Notez qu’il est valide pour `APP_ID` le `BOT_APP_ID` même nom et, dans de nombreux cas, s’il s’agit d’un robot, car il est recommandé de l’utiliser comme ID d’une application s’il en existe un.

## <a name="keyboard-and-accessibility-guidelines"></a>Instructions pour le clavier et l’accessibilité

Avec les modules de tâches HTML/JavaScript, il est de votre responsabilité de s’assurer que le module de tâches de votre application peut être utilisé avec un clavier. Les programmes de lecteur d’écran dépendent également de la possibilité de naviguer à l’aide du clavier. Pour des raisons pratiques, cela signifie deux choses :

1. Utilisation de l' [attribut TabIndex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) dans vos balises HTML pour contrôler les éléments qui peuvent être concentrés et si/là où ils participent à la navigation séquentielle du clavier (généralement avec les touches <kbd>Tab</kbd> et <kbd>MAJ-TAB</kbd> ).
2. Gestion de la touche <kbd>Échap</kbd> dans le code JavaScript pour votre module de tâches. Voici un exemple de code illustrant la procédure :

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft teams garantit que la navigation au clavier fonctionne correctement à partir de l’en-tête du module de tâches dans votre code HTML et inversement.

## <a name="task-module-samples"></a>Exemples de modules de tâches

* [Exemple node. js/dactylographié](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [Exemple de/.NET C#](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)
