---
title: Définir des commandes d’action d’extension de message
author: surbhigupta
description: Vue d’ensemble des commandes d’action d’extension de messagerie avec exemple de manifeste d’application
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ef9f1c45ec3b2d1df4bf5449885263034f19fde7
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111681"
---
# <a name="define-message-extension-action-commands"></a>Définir des commandes d’action d’extension de message

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes d’action vous permettent de présenter à vos utilisateurs une fenêtre contextuelle modale appelée module de tâche dans Teams. Le module de tâche collecte ou affiche des informations, traite l’interaction et les renvoie à Teams. Ce document vous guide sur la façon de sélectionner des emplacements d’appel de commande d’action, de créer votre module de tâche, d’envoyer un message final ou une carte, de créer une commande d’action à l’aide d’App Studio ou de le créer manuellement.

Avant de créer la commande d’action, vous devez décider des facteurs suivants :

1. [D’où la commande d’action peut-elle être déclenchée ?](#select-action-command-invoke-locations)
1. [Comment le module de tâche sera-t-il créé ?](#select-how-to-create-your-task-module)
1. [Le message final ou la carte sera-t-il envoyé au canal à partir d’un bot, ou le message ou la carte sera-t-il inséré dans la zone de composition de message que l’utilisateur doit envoyer ?](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>Sélectionner des emplacements d’appel de commande d’action

Tout d’abord, vous devez décider de l’emplacement à partir duquel votre commande d’action doit être appelée. En spécifiant le `context` dans le manifeste de votre application, votre commande peut être appelée à partir d’un ou plusieurs des emplacements suivants :

* Zone de rédaction du message : boutons situés en bas de la zone de rédaction du message.

    Contexte de commande = composer

* Zone de commande : en @mentioning votre application dans la zone de commande.

    Contexte des commandes = commandBox

   > [!NOTE]
   > Si l’extension de message est appelée à partir de la zone de commande, vous ne pouvez pas répondre avec un message de bot inséré directement dans la conversation.

* Message : directement à partir d’un message existant via le menu de dépassement de capacité `...` sur un message.

    Contexte des commandes = message

    > [!NOTE]
    > L’appel initial à votre bot inclut un objet JSON contenant le message à partir duquel il a été appelé. Vous pouvez traiter le message avant de lui présenter un module de tâche.

L’image suivante affiche les emplacements à partir desquels la commande d’action est appelée :

![appeler des emplacements par la commande action](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>Sélectionner comment créer votre module de tâche

En plus de sélectionner l’emplacement à partir duquel votre commande peut être appelée, vous devez également sélectionner comment remplir le formulaire dans le module de tâche pour vos utilisateurs. Vous disposez des trois options suivantes pour créer le formulaire rendu à l’intérieur du module de tâche :

* **Liste statique des paramètres** : il s’agit de la méthode la plus simple. Vous pouvez définir une liste de paramètres dans le manifeste de votre application rendu par le client Teams, mais vous ne pouvez pas contrôler la mise en forme dans ce cas.
* **Carte adaptative** : vous pouvez choisir d’utiliser une carte adaptative, qui offre un meilleur contrôle sur l’interface utilisateur, mais vous limite toujours sur les contrôles disponibles et les options de mise en forme.
* **Vue web incorporée** : vous pouvez choisir d’incorporer une vue web personnalisée dans le module de tâche pour avoir un contrôle total sur l’interface utilisateur et les contrôles.

Si vous choisissez de créer le module de tâche avec une liste statique de paramètres et que l’utilisateur envoie le module de tâche, l’extension de message est appelée. Lorsque vous utilisez une vue web incorporée ou une carte adaptative, votre extension de message doit gérer un événement d’appel initial de l’utilisateur, créer le module de tâche et le renvoyer au client.

## <a name="select-how-the-final-message-is-sent"></a>Sélectionner le mode d’envoi du message final

Dans la plupart des cas, la commande d’action entraîne l’insertion d’une carte dans la zone de composition du message. L’utilisateur peut l’envoyer dans le canal ou la conversation. Dans ce cas, le message provient de l’utilisateur et le bot ne peut pas modifier ou mettre à jour la carte.

Si l’extension de message est appelée à partir de la zone de composition ou directement à partir d’un message, votre service web peut insérer la réponse finale directement dans le canal ou la conversation. Dans ce cas, la carte adaptative provient du bot, le bot la met à jour et répond au thread de conversation si nécessaire. Vous devez ajouter l’objet `bot` au manifeste de l’application à l’aide du même ID et en définissant les étendues appropriées.

## <a name="add-the-action-command-to-your-app-manifest"></a>Ajouter la commande d’action au manifeste de votre application

Pour ajouter la commande d’action au manifeste de l’application, vous devez ajouter un nouvel objet `composeExtension` au niveau supérieur du manifeste d’application JSON. Pour ce faire, vous pouvez utiliser l’une des méthodes suivantes :

* [Créer une commande d’action à l’aide d’App Studio](#create-an-action-command-using-app-studio)
* [Créer une commande d’action manuellement](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>Créer une commande d’action à l’aide d’App Studio

Vous pouvez créer une commande d’action à l’aide **d’App Studio** ou **du portail des développeurs**.

> [!NOTE]
> App Studio sera bientôt déconseillé. Configurez, distribuez et gérez vos applications Teams avec la nouvelle [Developer Portal](https://dev.teams.microsoft.com/).

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> La configuration requise pour créer une commande d’action est que vous avez déjà créé une extension de message. Pour plus d’informations sur la création d’une extension de message, consultez [créer une extension de message](~/messaging-extensions/how-to/create-messaging-extension.md).

**Pour créer une commande d’action**

1. Ouvrez **App Studio** à partir du client Microsoft Teams et sélectionnez l’onglet **Éditeur de manifeste**.
1. Si vous avez déjà créé votre package d’application dans **App Studio**, sélectionnez-le dans la liste. Si vous n’avez pas créé de package d’application, importez-en un existant.
1. Après avoir importé un package d’application, sélectionnez **Extensions de message** sous **Fonctionnalités**. Vous obtenez une fenêtre contextuelle pour configurer l’extension de message.
1. Sélectionnez **Configurer** dans la fenêtre pour inclure l’extension de message dans votre expérience d’application. L’image suivante affiche la fenêtre de configuration de l’extension de message :

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. Pour créer une extension de message, vous avez besoin d’un bot inscrit par Microsoft. Vous pouvez utiliser un bot existant ou en créer un. Sélectionnez l’option **Créer un bot**, donnez un nom au nouveau bot, puis sélectionnez **Créer**. L’image suivante affiche la création de bot pour l’extension de message :

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Sélectionnez **Ajouter** dans la **section Commande** de la page Extensions de message pour inclure les commandes qui déterminent le comportement de l’extension de message.
L’image suivante affiche l’ajout de commande pour l’extension de message :

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. Sélectionnez **Autoriser les utilisateurs à déclencher des actions dans des services externes à l’intérieur de Teams**. L’image suivante affiche la sélection de la commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>

1. Pour utiliser un ensemble statique de paramètres pour créer votre module de tâche, sélectionnez **Définir un ensemble de paramètres statiques pour la commande**.

    L’image suivante affiche la sélection de paramètre statique de commande d’action :

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/>

    L’image suivante affiche un exemple de configuration de paramètre statique :

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    L’image suivante affiche un exemple de test de paramètres statiques :

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. Pour utiliser des paramètres dynamiques, sélectionnez pour **Extraire un jeu dynamique de paramètres à partir de votre bot**. L’image suivante affiche la sélection du paramètre de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>

1. Ajoutez un **ID de commande** et un **titre**.
1. Sélectionnez l’emplacement à partir duquel vous souhaitez appeler la commande d’action. L’image suivante affiche l’emplacement d’appel de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. Sélectionnez **Enregistrer**.
1. Pour ajouter d’autres paramètres, sélectionnez le bouton **Ajouter** dans la section **Paramètres**.

### <a name="create-an-action-command-manually"></a>Créer une commande d’action manuellement

Pour ajouter manuellement votre commande d’extension de message basée sur des actions au manifeste de votre application, vous devez ajouter les paramètres suivants au tableau d’objets `composeExtension.commands` :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | Cette propriété est un ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Cette propriété est un nom de commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Cette propriété doit être un `action`. | Non | 1.4 |
| `fetchTask` | Cette propriété est définie sur `true` pour une carte adaptative ou une vue web incorporée pour votre module de tâche, et`false` pour une liste statique de paramètres ou lors du chargement de la vue web par un `taskInfo`. | Non | 1.4 |
| `context` | Cette propriété est un tableau facultatif de valeurs qui définit l’emplacement à partir duquel l’extension de message est appelée. Les valeurs possibles sont `message`, `compose` ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Si vous utilisez une liste statique de paramètres, vous devez également ajouter les paramètres suivants :

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Cette propriété décrit la liste statique des paramètres de la commande. Utilisez uniquement lorsque `fetchTask` est `false`. | Non | 1.0 |
| `parameter.name` | Cette propriété décrit le nom du paramètre. Il est envoyé à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Cette propriété décrit les objectifs des paramètres ou l’exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Cette propriété est un titre ou une étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Cette propriété est définie sur le type d’entrée requis. Les valeurs possibles incluent `text`, `textarea`, `number`, `date`, `time`, `toggle`. La valeur par défaut est définie sur `text`. | Non | 1.4 |

Si vous utilisez une vue web incorporée, vous pouvez éventuellement ajouter l’objet `taskInfo` pour extraire votre vue web sans appeler directement votre bot. Si vous sélectionnez cette option, le comportement est similaire à celui de l’utilisation d’une liste statique de paramètres. Dans la mesure où la première interaction avec votre bot est [réponse au module de tâche envoyer l’action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md). Si vous utilisez un objet `taskInfo` , vous devez définir le paramètre `fetchTask` sur `false`.

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
|`taskInfo`|Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de message. | Non | 1.4 |
|`taskInfo.title`|Titre initial du module de tâche. |Non | 1.4 |
|`taskInfo.width`|Largeur du module de tâche, un nombre en pixels ou une disposition par défaut telle que `large`, `medium`ou `small`. |Non | 1.4 |
|`taskInfo.height`|Hauteur du module de tâche, un nombre en pixels ou une disposition par défaut telle que `large`, `medium`ou `small`.|Non | 1.4 |
|`taskInfo.url`|URL de la vue web initiale.|Non | 1.4 |

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

La section suivante est un exemple d’objet `composeExtensions` définissant deux commandes d’action. Il ne s’agit pas d’un exemple du manifeste complet. Pour obtenir le schéma complet du manifeste d’application, consultez [schéma de manifeste d’application](~/resources/schema/manifest-schema.md):

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
|Action d’extension de message Teams| Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’envoi du module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-meetingextension-action.yml) pour créer une extension de message basée sur des actions Teams.

## <a name="next-step"></a>Étape suivante

Si vous utilisez une carte adaptative ou une vue web incorporée sans objet `taskInfo`, l’étape suivante consiste à :

> [!div class="nextstepaction"]
> [Créer et répondre avec un module de tâche](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si vous utilisez les paramètres ou une vue web incorporée avec un objet `taskInfo`, l’étape suivante consiste à :

> [!div class="nextstepaction"]
> [Répondre à l’action d’envoi du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
