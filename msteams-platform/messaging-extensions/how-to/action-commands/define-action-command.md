---
title: Définir des commandes d’action d’extension de messagerie
author: surbhigupta
description: Vue d’ensemble des commandes d’action d’extension de messagerie avec un exemple de manifeste d’application
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 938e37fac8cd27257e378fa1177916462b331023
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399267"
---
# <a name="define-messaging-extension-action-commands"></a>Définir des commandes d’action d’extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes d’action vous permettent de présenter à vos utilisateurs une fenêtre popup modale appelée module de tâche dans Teams. Le module de tâche collecte ou affiche des informations, traite l’interaction et renvoie les informations à Teams. Ce document vous guide sur la sélection d’emplacements d’appel de commande d’action, la création de votre module de tâche, l’envoi d’un message final ou d’une carte, la création d’une commande d’action à l’aide d’app studio ou sa création manuelle.

Avant de créer la commande d’action, vous devez déterminer les facteurs suivants :

1. [À partir d’où la commande d’action peut-elle être déclenchée ?](#select-action-command-invoke-locations)
1. [Comment le module de tâche sera-t-il créé ?](#select-how-to-create-your-task-module)
1. [Le message final ou la carte sera-t-il envoyé au canal à partir d’un bot, ou le message ou la carte sera-t-il inséré dans la zone de composition du message à envoyer par l’utilisateur ?](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>Sélectionner des emplacements d’appel de commande d’action

Tout d’abord, vous devez déterminer l’emplacement à partir de lequel votre commande d’action doit être invoquée. En spécifiant le `context` manifeste de votre application, votre commande peut être invoquée à partir d’un ou plusieurs des emplacements suivants :

* Zone de composition de message : boutons situés en bas de la zone composer un message.

    Contexte de commande = composer

* Zone de commande : en @mentioning votre application dans la zone de commande.

    Contexte de commandes = commandBox

   > [!NOTE]
   > Si l’extension de messagerie est invoquée à partir de la zone de commande, vous ne pouvez pas répondre par un message bot inséré directement dans la conversation.

* Message : directement à partir d’un message existant via le menu de `...` dépassement d’un message.

    Contexte des commandes = message

    > [!NOTE]
    > L’appel initial à votre bot inclut un objet JSON contenant le message à partir duquel il a été appelé. Vous pouvez traiter le message avant de le présenter avec un module de tâche.

L’image suivante affiche les emplacements d’où la commande d’action est invoquée :

![emplacements d’appel de commande d’action](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>Sélectionnez comment créer votre module de tâche

En plus de sélectionner l’endroit à partir de lequel votre commande peut être invoquée, vous devez également sélectionner comment remplir le formulaire dans le module de tâche pour vos utilisateurs. Vous avez les trois options suivantes pour créer le formulaire qui est rendu à l’intérieur du module de tâche :

* **Liste statique des paramètres** : il s’agit de la méthode la plus simple. Vous pouvez définir une liste de paramètres dans le manifeste de votre application que le client Teams rendu, mais ne peut pas contrôler la mise en forme dans ce cas.
* **Carte adaptative** : vous pouvez choisir d’utiliser une carte adaptative, qui offre un meilleur contrôle sur l’interface utilisateur, mais vous limite aux contrôles et options de mise en forme disponibles.
* **Affichage web incorporé** : vous pouvez choisir d’incorporer un affichage web personnalisé dans le module de tâche pour avoir un contrôle complet sur l’interface utilisateur et les contrôles.

Si vous choisissez de créer le module de tâche avec une liste statique de paramètres et lorsque l’utilisateur soumet le module de tâche, l’extension de messagerie est appelée. Lorsque vous utilisez une vue web incorporée ou une carte adaptative, votre extension de messagerie doit gérer un événement d’appel initial de l’utilisateur, créer le module de tâche et le renvoyer au client.

## <a name="select-how-the-final-message-is-sent"></a>Sélectionner la façon dont le message final est envoyé

Dans la plupart des cas, la commande d’action entraîne l’insertion d’une carte dans la zone composer un message. L’utilisateur peut l’envoyer dans le canal ou la conversation. Dans ce cas, le message provient de l’utilisateur et le bot ne peut ni modifier ni mettre à jour la carte.

Si l’extension de messagerie est invoquée à partir de la zone de composition ou directement à partir d’un message, votre service web peut insérer la réponse finale directement dans le canal ou la conversation. Dans ce cas, la carte adaptative provient du bot, le bot la met à jour et répond au thread de conversation si nécessaire. Vous devez ajouter l’objet `bot` au manifeste de l’application en utilisant le même ID et en définissant les étendues appropriées.

## <a name="add-the-action-command-to-your-app-manifest"></a>Ajouter la commande d’action au manifeste de votre application

Pour ajouter la commande d’action au manifeste de l’application, `composeExtension` vous devez ajouter un nouvel objet au niveau supérieur du manifeste d’application JSON. Pour ce faire, vous pouvez utiliser l’une des méthodes suivantes :

* [Créer une commande d’action à l’aide d’App Studio](#create-an-action-command-using-app-studio)
* [Créer une commande d’action manuellement](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>Créer une commande d’action à l’aide d’App Studio

Vous pouvez créer une commande d’action à **l’aide d’App Studio** **ou du portail du développeur**.

> [!NOTE]
> App Studio sera bientôt supprimé. Configurez, distribuez et gérez vos applications Teams avec le nouveau [portail du développeur](https://dev.teams.microsoft.com/).

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> La condition préalable à la création d’une commande d’action est que vous avez déjà créé une extension de messagerie. Pour plus d’informations sur la création d’une extension de messagerie, voir [créer une extension de messagerie](~/messaging-extensions/how-to/create-messaging-extension.md).

**Pour créer une commande d’action**

1. **Ouvrez App Studio** à partir Microsoft Teams client et sélectionnez **l’onglet Éditeur de** manifeste.
1. Si vous avez déjà créé votre package d’application **dans App Studio**, sélectionnez-le dans la liste. Si vous n’avez pas créé de package d’application, importez-en un existant.
1. Après avoir importé un package d’application, sélectionnez **extensions de messagerie sous** **Fonctionnalités**. Vous obtenez une fenêtre instantanée pour configurer l’extension de messagerie.
1. **Sélectionnez Configurer dans** la fenêtre pour inclure l’extension de messagerie dans l’expérience de votre application. L’image suivante affiche la fenêtre de mise en place de l’extension de messagerie :

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. Pour créer une extension de messagerie, vous avez besoin d’un bot inscrit par Microsoft. Vous pouvez utiliser un bot existant ou en créer un nouveau. **Sélectionnez Créer un bot**, donnez un nom au nouveau bot, puis sélectionnez **Créer**. L’image suivante affiche la création d’un bot pour l’extension de messagerie :

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. **Sélectionnez Ajouter** dans **la section Commande** de la page Extensions de messagerie pour inclure les commandes qui déterminent le comportement de l’extension de messagerie.
L’image suivante affiche l’ajout de commande pour l’extension de messagerie :

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. **Sélectionnez Autoriser les utilisateurs à déclencher des actions dans des services externes à l’intérieur Teams**. L’image suivante affiche la sélection de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>

1. Pour utiliser un ensemble statique de paramètres pour créer votre module de tâche, sélectionnez Définir un ensemble de **paramètres statiques pour la commande**.

    L’image suivante affiche la sélection de paramètre statique de commande d’action :

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/>

    L’image suivante affiche un exemple de paramètre statique :

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    L’image suivante affiche un exemple de test de paramètre statique :

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. Pour utiliser des paramètres dynamiques, sélectionnez **Récupérer un ensemble dynamique de paramètres à partir de votre bot**. L’image suivante affiche la sélection du paramètre de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>

1. Ajoutez **un ID de commande** et un **titre**.
1. Sélectionnez l’emplacement à partir de lequel vous souhaitez appeler la commande d’action. L’image suivante affiche l’emplacement d’appel de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. Sélectionnez **Enregistrer**.
1. Pour ajouter d’autres paramètres, sélectionnez **le bouton Ajouter** dans la section **Paramètres** .

### <a name="create-an-action-command-manually"></a>Créer une commande d’action manuellement

Pour ajouter manuellement votre commande d’extension de messagerie basée sur l’action au manifeste de votre application, vous devez ajouter les paramètres suivants `composeExtension.commands` au tableau d’objets :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | Cette propriété est un ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Cette propriété est un nom de commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Cette propriété doit être une `action`. | Non | 1.4 |
| `fetchTask` | Cette propriété est définie `true` pour une carte adaptative ou un affichage web incorporé pour votre module de tâche,`false` et pour une liste statique de paramètres ou lors du chargement de l’affichage web par un `taskInfo`. | Non | 1.4 |
| `context` | Cette propriété est un tableau facultatif de valeurs qui définit l’endroit d’où l’extension de messagerie est invoquée. Les valeurs possibles sont `message`, `compose` ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Si vous utilisez une liste statique de paramètres, vous devez également ajouter les paramètres suivants :

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Cette propriété décrit la liste statique des paramètres de la commande. Utilisez uniquement quand `fetchTask` est `false`. | Non | 1.0 |
| `parameter.name` | Cette propriété décrit le nom du paramètre. Cette information est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Cette propriété décrit les objectifs du paramètre ou un exemple de la valeur à fournir. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Cette propriété est un titre ou une étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Cette propriété est définie sur le type d’entrée requis. Les valeurs possibles sont `text`, `textarea`, `number`, `date`, `toggle``time`. La valeur par défaut est définie sur `text`. | Non | 1.4 |

Si vous utilisez un affichage web incorporé, `taskInfo` vous pouvez éventuellement ajouter l’objet pour récupérer votre affichage web sans appeler directement votre bot. Si vous sélectionnez cette option, le comportement est similaire à celui de l’utilisation d’une liste statique de paramètres. Dans la mesure où la première interaction avec votre bot [répond à l’action d’soumission du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md). Si vous utilisez un objet `taskInfo` , vous devez définir le `fetchTask` paramètre sur `false`.

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
|`taskInfo`|Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie. | Non | 1.4 |
|`taskInfo.title`|Titre du module de tâche initial. |Non | 1.4 |
|`taskInfo.width`|Largeur du module de tâche, soit un nombre en pixels, soit une disposition par défaut telle `large`que , `medium`ou `small`. |Non | 1.4 |
|`taskInfo.height`|Hauteur du module de tâche, soit un nombre en pixels, soit une disposition par défaut telle `large`que , `medium`ou `small`.|Non | 1.4 |
|`taskInfo.url`|URL d’affichage web initiale.|Non | 1.4 |

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

La section suivante est un exemple d’objet `composeExtensions` définissant deux commandes d’action. Il ne s’agit pas d’un exemple de manifeste complet. Pour obtenir le schéma de manifeste d’application complet, voir schéma [de manifeste d’application](~/resources/schema/manifest-schema.md) :

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": true,
        "parameters": [
          {
            "name": "Name",
            "description": "To Do Title",
            "title": "Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "description": "Description of the task",
            "title": "Description",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "description": "Due date for the task",
            "title": "Date",
            "inputType": "date"
          }
        ]
      },
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Reassign a todo item",
        "type": "action",
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams d’extension de messagerie| Décrit comment définir des commandes d’action, créer un module de tâche et répondre à une action d’soumission de module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-meetingextension-action.yml) pour créer Teams extension de messagerie basée sur une action.

## <a name="next-step"></a>Étape suivante

Si vous utilisez une carte adaptative ou un affichage web `taskInfo` incorporé sans objet, l’étape suivante consiste à :

> [!div class="nextstepaction"]
> [Créer et répondre avec un module de tâche](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si vous utilisez les paramètres ou un affichage web `taskInfo` incorporé avec un objet, l’étape suivante consiste à :

> [!div class="nextstepaction"]
> [Répondre à l’soumission du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
