---
title: Définir les commandes de recherche d'extension de messagerie
author: clearab
description: Définissez les commandes de recherche d'extension de messagerie pour Microsoft Teams applications.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 19f1fdf7bd4efdbb0de11d1abad341ec24bc27bd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696794"
---
# <a name="define-messaging-extension-search-commands"></a>Définir les commandes de recherche d'extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes de recherche d'extension de messagerie permettent aux utilisateurs de rechercher des systèmes externes et d'insérer les résultats de cette recherche dans un message sous la forme d'une carte. Ce document vous guide sur la sélection des emplacements d'appel de commande de recherche et ajoute la commande de recherche au manifeste de votre application.

> [!NOTE]
> La limite de taille de carte de résultat est de 28 Ko. La carte n'est pas envoyée si sa taille dépasse 28 Ko.

## <a name="select-search-command-invoke-locations"></a>Sélectionner des emplacements d'appel de commande de recherche

La commande de recherche est invoquée à partir de l'un des emplacements suivants ou des deux :

* Zone de composition de message : boutons situés en bas de la zone composer un message.
* Zone de commande : en @mentioning dans la zone de commande.

Lorsque la commande de recherche est invoquée à partir de la zone composer un message, l'utilisateur envoie les résultats à la conversation. Lorsqu'il est appelé à partir de la zone de commande, l'utilisateur interagit avec la carte résultante ou la copie pour l'utiliser ailleurs.

L'image suivante affiche les emplacements d'appel de la commande de recherche :

![emplacements d'appel de commande de recherche](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a>Ajouter la commande de recherche au manifeste de votre application

Pour ajouter la commande de recherche au manifeste de votre application, vous devez ajouter un nouvel objet au niveau supérieur du manifeste JSON de `composeExtension` votre application. Vous pouvez ajouter la commande de recherche à l'aide d'App Studio ou manuellement.

### <a name="create-a-search-command-using-app-studio"></a>Créer une commande de recherche à l'aide d'App Studio

La condition préalable à la création d'une commande de recherche est que vous devez déjà avoir créé une extension de messagerie. Pour plus d'informations sur la création d'une extension de messagerie, voir [créer une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)

**Pour créer une commande de recherche**

1. Ouvrez **App Studio** à partir Microsoft Teams client, puis sélectionnez l'onglet **Éditeur de** manifeste.
1.  Si vous avez déjà créé votre package d'application **dans App Studio,** sélectionnez-le dans la liste. Si vous n'avez pas créé de package d'application, importez-en un existant.
1. Après avoir importé le package d'application, **sélectionnez les extensions de messagerie sous** **Fonctionnalités.** Vous obtenez une fenêtre instantanée pour configurer l'extension de messagerie.
1. Sélectionnez **Configurer dans** la fenêtre pour inclure l'extension de messagerie dans l'expérience de votre application. L'image suivante affiche la page de mise en place de l'extension de messagerie : 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. Pour créer l'extension de messagerie, vous avez besoin d'un bot inscrit par Microsoft. Vous pouvez utiliser un bot existant ou en créer un nouveau. Sélectionnez Créer une option **de bot,** donnez un nom au nouveau bot, puis sélectionnez **Créer.** L'image suivante affiche la création d'un bot pour l'extension de messagerie :

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Sélectionnez **Ajouter** dans **la section Commande** de la page Extensions de messagerie pour inclure les commandes qui déterminent le comportement de l'extension de messagerie.   
L'image suivante affiche l'ajout de commande pour l'extension de messagerie :

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. Sélectionnez **Autoriser les utilisateurs à interroger votre service pour obtenir des informations** et à les insérer dans un message. L'image suivante affiche la sélection du paramètre de commande de recherche :

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. Ajoutez **un ID de commande** et un **titre.**
1. Sélectionnez l'emplacement à partir de lequel votre commande de recherche doit être invoquée. La sélection **d'un message** ne modifie pas actuellement le comportement de votre commande de recherche. L'image suivante affiche l'emplacement d'appel de commande de recherche :

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. Ajoutez votre paramètre de recherche et sélectionnez **Enregistrer.**

### <a name="create-a-search-command-manually"></a>Créer une commande de recherche manuellement 

Pour ajouter manuellement votre commande de recherche d'extension de messagerie au manifeste de votre application, vous devez ajouter les paramètres suivants à votre `composeExtension.commands` tableau d'objets :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | Cette propriété est un ID unique que vous affectez à la commande de recherche. La demande de l'utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Cette propriété est un nom de commande. Cette valeur apparaît dans l'interface utilisateur. | Oui | 1.0 |
| `description` | Cette propriété est un texte d'aide indiquant ce que fait cette commande. Cette valeur apparaît dans l'interface utilisateur. | Oui | 1.0 |
| `type` | Cette propriété doit être une `query` . | Non | 1.4 |
|`initialRun` | Si cette propriété est définie sur **true,** elle indique que cette commande doit être exécutée dès que l'utilisateur sélectionne cette commande dans l'interface utilisateur. | Non | 1.0 |
| `context` | Cette propriété est un tableau facultatif de valeurs qui définit le contexte dans lequel l'action de recherche est disponible. Les valeurs possibles sont `message`, `compose` ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Vous devez ajouter les détails du paramètre de recherche, qui définit le texte visible pour votre utilisateur dans le client Teams recherche.

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Cette propriété définit une liste statique de paramètres pour la commande. | Non | 1.0 |
| `parameter.name` | Cette propriété décrit le nom du paramètre. Cette information est envoyée à votre service dans la demande de l'utilisateur. | Oui | 1.0 |
| `parameter.description` | Cette propriété décrit les objectifs du paramètre ou un exemple de la valeur à fournir. Cette valeur apparaît dans l'interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Cette propriété est un titre ou une étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Cette propriété est définie sur le type d'entrée requis. Les valeurs `text` possibles sont , , , , `textarea` `number` `date` `time` `toggle` . La valeur par défaut est définie sur `text` . | Non | 1.4 |

#### <a name="example"></a>Exemple

La section suivante est un exemple du manifeste d'application simple de `composeExtensions` l'objet définissant une commande de recherche : 

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```
Pour obtenir le manifeste complet de l'application, voir [schéma de manifeste d'application.](~/resources/schema/manifest-schema.md)

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams d'extension de messagerie| Décrit comment définir des commandes d'action, créer un module de tâche et répondre à une action d'soumission de module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams d'extension de messagerie   |  Décrit comment définir des commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Répondez aux commandes de recherche.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)

