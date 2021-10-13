---
title: Définir des commandes d’action d’extension de messagerie
author: surbhigupta
description: Vue d’ensemble des commandes d’action d’extension de messagerie
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 6f4dd3b68d1012b2abc6534fedaddcd76a2a9538
ms.sourcegitcommit: 37b1724bb0d2f1b087c356e0fd0ff80145671e22
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2021
ms.locfileid: "60291673"
---
# <a name="define-messaging-extension-action-commands"></a>Définir des commandes d’action d’extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes d’action vous permettent de présenter à vos utilisateurs une fenêtre popup modale appelée module de tâche dans Teams. Le module de tâche collecte ou affiche des informations, traite l’interaction et renvoie les informations Teams. Ce document vous guide sur la sélection d’emplacements d’appel de commande d’action, la création de votre module de tâche, l’envoi d’un message final ou d’une carte, la création d’une commande d’action à l’aide d’app studio ou sa création manuelle. 

Avant de créer la commande d’action, vous devez déterminer les facteurs suivants :

1. [À partir d’où la commande d’action peut-elle être déclenchée ?](#select-action-command-invoke-locations)
1. [Comment le module de tâche sera-t-il créé ?](#select-how-to-create-your-task-module)
1. [Le message final ou la carte sera-t-il envoyé au canal à partir d’un bot, ou le message ou la carte sera-t-il inséré dans la zone de composition du message à envoyer par l’utilisateur ?](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>Sélectionner des emplacements d’appel de commande d’action

Tout d’abord, vous devez déterminer l’emplacement à partir de lequel votre commande d’action doit être invoquée. En spécifiant le manifeste de votre application, votre commande peut être invoquée à partir d’un ou plusieurs `context` des emplacements suivants :

* Zone de composition de message : boutons situés en bas de la zone composer un message.
* Zone de commande : en @mentioning votre application dans la zone de commande. 
   > [!NOTE]
   > Si l’extension de messagerie est invoquée à partir de la zone de commande, vous ne pouvez pas répondre avec un message bot inséré directement dans la conversation.

* Message : directement à partir d’un message existant via le `...` menu de dépassement d’un message. 
    > [!NOTE] 
    > L’appel initial à votre bot inclut un objet JSON contenant le message à partir duquel il a été appelé. Vous pouvez traiter le message avant de lui présenter un module de tâche.

L’image suivante affiche les emplacements d’où la commande d’action est invoquée :

![emplacements d’appel de commande d’action](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>Sélectionnez comment créer votre module de tâche

En plus de sélectionner l’endroit à partir de lequel votre commande peut être invoquée, vous devez également sélectionner comment remplir le formulaire dans le module de tâche pour vos utilisateurs. Vous avez les trois options suivantes pour créer le formulaire qui est rendu à l’intérieur du module de tâche :   

* **Liste statique de paramètres**: il s’agit de la méthode la plus simple. Vous pouvez définir une liste de paramètres dans le manifeste de votre application que le client Teams rendu, mais ne peut pas contrôler la mise en forme dans ce cas.
* **Carte adaptative**: vous pouvez choisir d’utiliser une carte adaptative, qui offre un meilleur contrôle sur l’interface utilisateur, tout en vous limitant sur les contrôles disponibles et les options de mise en forme.
* **Affichage web incorporé**: vous pouvez choisir d’incorporer un affichage web personnalisé dans le module de tâche pour avoir un contrôle complet sur l’interface utilisateur et les contrôles. 

Si vous choisissez de créer le module de tâche avec une liste statique de paramètres et lorsque l’utilisateur soumet le module de tâche, l’extension de messagerie est appelée. Lorsque vous utilisez une vue web incorporée ou une carte adaptative, votre extension de messagerie doit gérer un événement d’appel initial de l’utilisateur, créer le module de tâche et le renvoyer au client.

## <a name="select-how-the-final-message-is-sent"></a>Sélectionner la façon dont le message final est envoyé

Dans la plupart des cas, la commande d’action entraîne l’insertion d’une carte dans la zone de composition du message. L’utilisateur peut l’envoyer dans le canal ou la conversation. Dans ce cas, le message provient de l’utilisateur et le bot ne peut ni modifier ni mettre à jour la carte.

Si l’extension de messagerie est invoquée à partir de la zone de composition ou directement à partir d’un message, votre service web peut insérer la réponse finale directement dans le canal ou la conversation. Dans ce cas, la carte adaptative provient du bot, le bot la met à jour et répond au thread de conversation si nécessaire. Vous devez ajouter l’objet au manifeste de l’application à l’aide du même ID et définir `bot` les étendues appropriées.

## <a name="add-the-action-command-to-your-app-manifest"></a>Ajouter la commande d’action au manifeste de votre application

Pour ajouter la commande d’action au manifeste de l’application, vous devez ajouter un nouvel objet au niveau supérieur `composeExtension` du manifeste d’application JSON. Pour ce faire, vous pouvez utiliser l’une des méthodes suivantes :

* [Créer une commande d’action à l’aide d’App Studio](#create-an-action-command-using-app-studio)
* [Créer une commande d’action manuellement](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>Créer une commande d’action à l’aide d’App Studio

Vous pouvez créer une commande d’action à l’aide **d’App Studio** ou **du portail du développeur.**

> [!NOTE]
> App Studio sera bientôt supprimé. Configurez, distribuez et gérez vos applications Teams avec le nouveau [portail du développeur.](https://dev.teams.microsoft.com/)

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> La condition préalable à la création d’une commande d’action est que vous avez déjà créé une extension de messagerie. Pour plus d’informations sur la création d’une extension de messagerie, voir [créer une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)

**Pour créer une commande d’action**

1. Ouvrez **App Studio** à partir Microsoft Teams client et sélectionnez **l’onglet Éditeur de** manifeste.
1. Si vous avez déjà créé votre package d’application dans **App Studio,** sélectionnez-le dans la liste. Si vous n’avez pas créé de package d’application, importez-en un existant.
1. Après avoir importé un package d’application, sélectionnez **les extensions de messagerie sous** **Fonctionnalités.** Vous obtenez une fenêtre instantanée pour configurer l’extension de messagerie.
1. Sélectionnez **Configurer dans** la fenêtre pour inclure l’extension de messagerie dans l’expérience de votre application. L’image suivante affiche la fenêtre de mise en place de l’extension de messagerie :

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. Pour créer une extension de messagerie, vous avez besoin d’un bot inscrit par Microsoft. Vous pouvez utiliser un bot existant ou en créer un. Sélectionnez Créer une option **de bot,** donnez un nom au nouveau bot, puis sélectionnez **Créer.** L’image suivante affiche la création d’un bot pour l’extension de messagerie :

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Sélectionnez **Ajouter** dans **la section Commande** de la page Extensions de messagerie pour inclure les commandes qui déterminent le comportement de l’extension de messagerie.   
L’image suivante affiche l’ajout de commande pour l’extension de messagerie :

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. Sélectionnez Autoriser les utilisateurs à déclencher des actions dans des services externes **à l’intérieur Teams**. L’image suivante affiche la sélection de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. Pour utiliser un ensemble statique de paramètres pour créer votre module de tâche, sélectionnez Définir un ensemble de **paramètres statiques pour la commande.** 

    L’image suivante affiche la sélection de paramètre statique de commande d’action :

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    L’image suivante affiche un exemple de paramètre statique : 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    L’image suivante affiche un exemple de test de paramètre statique :

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. Pour utiliser des paramètres dynamiques, sélectionnez **Récupérer un ensemble dynamique de paramètres à partir de votre bot.** L’image suivante affiche la sélection du paramètre de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. Ajoutez **un ID de commande** et un **titre.**
1. Sélectionnez l’emplacement à partir de lequel vous souhaitez appeler la commande d’action. L’image suivante affiche l’emplacement d’appel de commande d’action :

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. Sélectionnez **Enregistrer**.
1. Pour ajouter d’autres paramètres, sélectionnez **le bouton** Ajouter dans la section **Paramètres.**

# <a name="developer-portal"></a>[Portail du développeur](#tab/DP)

**Pour créer une commande d’action à l’aide du portail du développeur**

1. Go to **[Developer portal](https://dev.teams.microsoft.com/)**.
    
      ![Capture d’écran de TDP](~/assets/images/tdp/tdp_home_1.png)

1. Go to **Apps**.
    
    <img width="500px" alt="Screenshot of TDP Open" src="~/assets/images/tdp/screen2.png"/>
    
1. Si vous avez déjà créé votre package d’application dans **le Portail** du développeur, sélectionnez-le dans la liste. Si ce n’est pas **le cas, sélectionnez** Importer une application existante.

    <img width="500px" alt="Screenshot of import app in tdp" src="~/assets/images/tdp/screen3.png"/>

1. Allez aux **fonctionnalités de l’application.** 

    <img width="500px" alt="TDP messaging extension" src="~/assets/images/tdp/tdp-me.png"/>

1. Sélectionnez **les extensions de messagerie dans** les **fonctionnalités de l’application.** Une fenêtre instantanée s’affiche pour configurer l’extension de messagerie.
    
   <img width="500px" alt="TDP messaging extension set up" src="~/assets/images/tdp/tdp-app-me.png"/>
 
1. Sélectionnez **un bot d’extension de message** dans la liste bas sous **ID des extensions** de messagerie, puis **sélectionnez Enregistrer.**

    <img width="500px" alt="TDP messaging extension bot" src="~/assets/images/tdp/tdp-me-bot.png"/>

1. Sélectionnez **Ajouter une commande.** Une fenêtre pop-up s’affiche pour ajouter une commande.

    <img width="500px" alt="TDP messaging extension command" src="~/assets/images/tdp/tdp-me-add-command.png"/>

1. Sélectionnez le type de la commande en **fonction de l’action** pour configurer l’extension de messagerie. Sélectionnez **Paramètres dynamiques** pour créer une commande d’action dynamique.

    <img width="500px" alt="TDP messaging extension dynamic action command" src="~/assets/images/tdp/tdp-me-action-command-dynamic.png"/>

1. Sélectionnez **paramètres statiques** pour créer une commande d’action statique.   

    <img width="500px" alt="TDP messaging extension static action command" src="~/assets/images/tdp/tdp-me-action-command-static.png"/>

1. Entrez les champs de commande. 

    <img width="500px" alt="TDP messaging extension action command" src="~/assets/images/tdp/tdp-me-action-command.png"/>  

1. Entrez les champs de paramètre, puis **sélectionnez Enregistrer.**

    <img width="500px" alt="TDP messaging extension action parameter" src="~/assets/images/tdp/tdp-me-action-parameter.png"/>
 
---

### <a name="create-an-action-command-manually"></a>Créer une commande d’action manuellement

Pour ajouter manuellement votre commande d’extension de messagerie basée sur l’action au manifeste de votre application, vous devez ajouter les paramètres suivants au tableau `composeExtension.commands` d’objets :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | Cette propriété est un ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Cette propriété est un nom de commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Cette propriété doit être une `action` . | Non | 1.4 |
| `fetchTask` | Cette propriété est définie sur pour une carte adaptative ou un affichage web incorporé pour votre module de tâche, et pour une liste statique de paramètres ou lors du chargement de l’affichage `true` `false` web par un `taskInfo` . | Non | 1.4 |
| `context` | Cette propriété est un tableau facultatif de valeurs qui définit l’endroit d’où l’extension de messagerie est invoquée. Les valeurs possibles sont `message`, `compose` ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Si vous utilisez une liste statique de paramètres, vous devez également ajouter les paramètres suivants :

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Cette propriété décrit la liste statique des paramètres de la commande. Utilisez uniquement quand `fetchTask` `false` est . | Non | 1.0 |
| `parameter.name` | Cette propriété décrit le nom du paramètre. Cette information est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Cette propriété décrit les objectifs du paramètre ou un exemple de la valeur à fournir. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Cette propriété est un titre ou une étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Cette propriété est définie sur le type d’entrée requis. Les valeurs possibles `text` sont , , , , `textarea` `number` `date` `time` `toggle` . La valeur par défaut est définie sur `text` . | Non | 1.4 |

Si vous utilisez un affichage web incorporé, vous pouvez éventuellement ajouter l’objet pour récupérer votre affichage web sans appeler `taskInfo` directement votre bot. Si vous sélectionnez cette option, le comportement est similaire à celui de l’utilisation d’une liste statique de paramètres. Dans la mesure où la première interaction avec votre bot [répond à l’action d’soumission du module de tâche.](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md) Si vous utilisez un `taskInfo` objet, vous devez définir le `fetchTask` paramètre sur `false` .

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
|`taskInfo`|Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie. | Non | 1.4 |
|`taskInfo.title`|Titre du module de tâche initial. |Non | 1.4 |
|`taskInfo.width`|Largeur du module de tâche, soit un nombre en pixels, soit une disposition par défaut telle `large` que `medium` , ou `small` . |Non | 1.4 |
|`taskInfo.height`|Hauteur du module de tâche, soit un nombre en pixels, soit une disposition par défaut telle `large` que `medium` , ou `small` .|Non | 1.4 |
|`taskInfo.url`|URL d’affichage web initiale.|Non | 1.4 | 

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

La section suivante est un exemple `composeExtensions` d’objet définissant deux commandes d’action. Il ne s’agit pas d’un exemple de manifeste complet. Pour obtenir le schéma de manifeste d’application complet, voir schéma [de manifeste d’application](~/resources/schema/manifest-schema.md):

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
|Teams d’extension de messagerie| Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’soumission du module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams d’extension de messagerie   |  Décrit comment définir des commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Étape suivante

Si vous utilisez une carte adaptative ou un affichage web incorporé sans `taskInfo` objet, l’étape suivante consiste à :

> [!div class="nextstepaction"]
> [Créer et répondre avec un module de tâche](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si vous utilisez les paramètres ou un affichage web incorporé avec un `taskInfo` objet, l’étape suivante consiste à :

> [!div class="nextstepaction"]
> [Répondre à l’soumission du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

