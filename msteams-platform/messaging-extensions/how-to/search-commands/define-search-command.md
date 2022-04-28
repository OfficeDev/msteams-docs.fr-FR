---
title: Définir des commandes de recherche d’extension de message
author: surbhigupta
description: Découvrez les commandes de recherche d’extension de message pour Microsoft Teams applications, pour créer une commande de recherche via le manifeste de l’application et manuellement à l’aide d’exemples de code et d’exemples.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: none
ms.openlocfilehash: f7933b1ef7de40ac889e0ae6d8063f6b21991cc7
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104300"
---
# <a name="define-message-extension-search-commands"></a>Définir des commandes de recherche d’extension de message

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes de recherche d’extension de message permettent aux utilisateurs de rechercher des systèmes externes et d’insérer les résultats de cette recherche dans un message sous la forme d’une carte. Ce document vous guide sur la façon de sélectionner la commande de recherche appeler des emplacements et d’ajouter la commande de recherche au manifeste de votre application.

> [!NOTE]
> La limite de taille de la carte de résultat est de 28 Ko. La carte n’est pas envoyée si sa taille dépasse 28 Ko.

## <a name="select-search-command-invoke-locations"></a>Sélectionner des emplacements d’appel de commande de recherche

La commande de recherche est appelée à partir de n’importe quel emplacement ou des deux emplacements suivants :

* Zone de composition du message : boutons situés en bas de la zone de composition du message.
* Zone de commande : en @mentioning dans la zone de commande.

  Lorsque la commande de recherche est appelée à partir de la zone de message de composition, l’utilisateur envoie les résultats à la conversation. Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur interagit avec la carte résultante ou la copie pour l’utiliser ailleurs.

L’image suivante affiche les emplacements d’appel de la commande de recherche :

![rechercher des emplacements d’appel de commande](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a>Ajouter la commande de recherche au manifeste de votre application

Pour ajouter la commande de recherche au manifeste de votre application, vous devez ajouter un nouvel `composeExtension` objet au niveau supérieur de votre manifeste d’application JSON. Vous pouvez ajouter la commande de recherche à l’aide d’App Studio ou manuellement.

### <a name="create-a-search-command-using-app-studio"></a>Créer une commande de recherche à l’aide d’App Studio

La configuration requise pour créer une commande de recherche est que vous devez déjà avoir créé une extension de message. Pour plus d’informations sur la création d’une extension de message, consultez [créer une extension de message](~/messaging-extensions/how-to/create-messaging-extension.md).

Pour créer une commande de recherche :

1. Ouvrez **App Studio** à partir du client Microsoft Teams, puis sélectionnez l’onglet **Éditeur de manifeste**.
1. Si vous avez déjà créé votre package d’application dans **App Studio**, sélectionnez-le dans la liste. Si vous n’avez pas créé de package d’application, importez-en un existant.
1. Après avoir importé le package d’application, sélectionnez **Extensions de message** sous **Fonctionnalités**. Vous obtenez une fenêtre contextuelle pour configurer l’extension de message.
1. Sélectionnez **Configurer** dans la fenêtre pour inclure l’extension de message dans votre expérience d’application. L’image suivante affiche la page de configuration de l’extension de message :

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. Pour créer l’extension de message, vous avez besoin d’un bot inscrit par Microsoft. Vous pouvez utiliser un bot existant ou en créer un. Sélectionnez **l’option Créer un bot** , donnez un nom au nouveau bot, puis sélectionnez **Créer**. L’image suivante affiche la création du bot pour l’extension de message :

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Sélectionnez **Ajouter** dans la **section Commande** de la page Extensions de message pour inclure les commandes qui déterminent le comportement de l’extension de message.
L’image suivante affiche l’ajout de commandes pour l’extension de message :

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. Sélectionnez **Autoriser les utilisateurs à interroger votre service pour obtenir des informations et à les insérer dans un message**. L’image suivante affiche la sélection du paramètre de commande de recherche :

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. Ajoutez un **ID de commande** et un **titre**.
1. Sélectionnez l’emplacement à partir duquel votre commande de recherche doit être appelée. L’image suivante affiche l’emplacement d’appel de la commande de recherche :

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. Ajoutez votre paramètre de recherche, puis **sélectionnez Enregistrer**.

### <a name="create-a-search-command-manually"></a>Créer une commande de recherche manuellement

Pour ajouter manuellement votre commande de recherche d’extension de message au manifeste de votre application, vous devez ajouter les paramètres suivants à votre `composeExtension.commands` tableau d’objets :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | Cette propriété est un ID unique que vous affectez à la commande de recherche. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Cette propriété est un nom de commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Cette propriété est un texte d’aide indiquant ce que fait cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Cette propriété doit être un `query`. | Non | 1.4 |
|`initialRun` | Si cette propriété a la valeur **true**, elle indique que cette commande doit être exécutée dès que l’utilisateur sélectionne cette commande dans l’interface utilisateur. | Non | 1.0 |
| `context` | Cette propriété est un tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible. Les valeurs possibles sont `message`, `compose` ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Vous devez ajouter les détails du paramètre de recherche, qui définit le texte visible par votre utilisateur dans le client Teams.

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Cette propriété définit une liste statique de paramètres pour la commande. | Non | 1.0 |
| `parameter.name` | Cette propriété décrit le nom du paramètre. Il est envoyé à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Cette propriété décrit les objectifs du paramètre ou l’exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Cette propriété est un titre ou une étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Cette propriété est définie sur le type de l’entrée requise. Les valeurs possibles sont : `text`, `textarea`, `number``date`, `toggle``time`. La valeur par défaut est `text`. | Non | 1.4 |

#### <a name="example"></a>Exemple

La section suivante est un exemple de manifeste d’application simple de l’objet `composeExtensions` définissant une commande de recherche :

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

Pour obtenir le manifeste complet de l’application, consultez [le schéma de manifeste de l’application](~/resources/schema/manifest-schema.md).

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams recherche d’extension de message   |  Décrit comment définir des commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-messagingextension-searchcommand.yml) pour créer une extension de message basée sur la recherche.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Répondez aux commandes de recherche](~/messaging-extensions/how-to/search-commands/respond-to-search.md).
