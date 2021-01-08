---
title: Définir des commandes d’action d’extension de messagerie
author: clearab
description: Vue d’ensemble des commandes d’action d’extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778400"
---
# <a name="define-messaging-extension-action-commands"></a>Définir des commandes d’action d’extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes d’action vous permettent de présenter une fenêtre contextuelle modale (appelée module de tâches dans Teams) à vos utilisateurs afin de collecter ou d’afficher des informations, puis de traiter leur interaction et de renvoyer des informations à Teams. Avant de créer votre commande, vous devez décider :

1. À partir d’où la commande d’action peut-elle être déclenchée ?
1. Comment le module de tâche sera-t-il créé ?
1. Le message final ou la carte sera-t-il envoyé au canal à partir d’un bot, ou le message ou la carte sera-t-il inséré dans la zone de composition du message à envoyer par l’utilisateur ?

## <a name="choose-action-command-invoke-locations"></a>Choisir des emplacements d’appel de commande d’action

La première chose que vous devez déterminer est l’endroit à partir de lequel votre commande d’action peut être déclenchée (ou *plus* spécifiquement appelé). En spécifiant le manifeste de votre application, votre commande peut être invoquée à partir d’un ou plusieurs `context` des emplacements suivants :

* Boutons situés en bas de la zone composer un message.
* En @mentioning votre application dans la zone de commande. Remarque : vous ne pouvez pas répondre avec un message bot inséré directement dans la conversation si votre extension de messagerie est invoquée à partir de la zone de commande.
* Directement à partir d’un message existant via le ... menu de dépassement sur un message. Remarque : l’appel initial à votre bot inclut un objet JSON contenant le message à partir duquel il a été appelé, que vous pouvez traiter avant de le présenter avec un module de tâche.

## <a name="choose-how-to-build-your-task-module"></a>Choisir comment créer votre module de tâche

En plus de choisir l’endroit à partir de lequel votre commande peut être invoquée, vous devez également choisir comment remplir le formulaire dans le module de tâche pour vos utilisateurs. Vous avez trois options pour créer le formulaire qui est rendu à l’intérieur du module de tâche :

* **Liste statique des paramètres :** il s’agit de l’option la plus simple. Vous pouvez définir une liste de paramètres (champs d’entrée) dans le manifeste de votre application que le client Teams restituera. Vous ne pouvez pas contrôler la mise en forme avec cette option.
* **Carte adaptative** : vous pouvez choisir d’utiliser une carte adaptative, qui offre un meilleur contrôle sur l’interface utilisateur, mais vous limite aux contrôles disponibles et aux options de mise en forme.
* **Affichage web incorporé** : si vous avez besoin d’un contrôle complet sur l’interface utilisateur et les contrôles, vous pouvez choisir d’incorporer un affichage web personnalisé dans le module de tâche.

Si vous choisissez de créer votre module de tâche avec une liste statique de paramètres, le premier appel à votre extension de messagerie sera lorsqu’un utilisateur soumet le module de tâche. Lorsque vous utilisez une vue web incorporée ou une carte adaptative, votre extension de messagerie doit gérer un événement d’appel initial de l’utilisateur, créer le module de tâche et le renvoyer au client.

## <a name="choose-how-the-final-message-will-be-sent"></a>Choisir la façon dont le message final sera envoyé

Dans la plupart des cas, votre commande d’action entraîne l’insertion d’une carte dans la zone composer un message. Votre utilisateur peut ensuite décider de l’envoyer dans le canal ou la conversation. Dans ce cas, le message provient de l’utilisateur et votre bot ne peut ni modifier ni mettre à jour la carte.

Si votre extension de messagerie est déclenchée à partir de la zone de composition ou directement à partir d’un message, votre service web peut insérer la réponse finale directement dans le canal ou la conversation. Dans ce cas, la carte adaptative provient du bot, le bot peut la mettre à jour et le bot peut également répondre au thread de conversation si nécessaire. Vous devez ajouter l’objet au manifeste de votre application en utilisant le même ID et en `bot` définissant les étendues appropriées.

## <a name="add-the-command-to-your-app-manifest"></a>Ajouter la commande au manifeste de votre application

Maintenant que vous avez décidé de la façon dont les utilisateurs interagira avec votre commande d’action, il est temps de l’ajouter au manifeste de votre application. Pour ce faire, vous allez ajouter un nouvel objet au niveau `composeExtension` supérieur du manifeste JSON de votre application. Vous pouvez le faire à l’aide d’App Studio ou manuellement.

### <a name="create-a-command-using-app-studio"></a>Créer une commande à l’aide d’App Studio

Les étapes suivantes supposent que vous avez [déjà créé une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)

1. Dans le client Microsoft Teams, ouvrez **App Studio** et sélectionnez l’onglet **Éditeur de** manifeste.
2. Si vous avez déjà créé votre package d’application dans App Studio, choisissez-le dans la liste. Si ce n’est pas le cas, vous pouvez importer un package d’application existant.
3. Cliquez sur **le bouton** Ajouter dans la section Commande.
4. Choisissez **Autoriser les utilisateurs à déclencher des actions dans des services externes à l’intérieur de Teams.**
5. Si vous souhaitez utiliser un ensemble statique de paramètres pour créer votre module de tâche, sélectionnez cette option. Dans le cas contraire, choisissez **d’extraire un ensemble dynamique de paramètres à partir de votre bot.**
6. Ajoutez **un ID de commande** et un **titre.**
7. Sélectionnez l’endroit à partir de lequel vous souhaitez déclencher votre commande d’action.
8. Si vous utilisez des paramètres pour votre module de tâche, ajoutez le premier.
9. Cliquez sur Save (Enregistrer)
10. Si vous devez ajouter d’autres  paramètres, cliquez sur le bouton Ajouter dans la section **Paramètres** pour les ajouter.

### <a name="manually-create-a-command"></a>Créer manuellement une commande

Pour ajouter manuellement votre commande d’extension de messagerie basée sur l’action au manifeste de votre application, vous devez ajouter les paramètres de suivi à votre `composeExtension.commands` tableau d’objets.

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Doit être `action` | Non | 1.4 |
| `fetchTask` | `true` pour une carte adaptative ou un affichage web incorporé pour votre module de tâche, pour une liste statique de paramètres ou lors du chargement de l’affichage `false` web par un `taskInfo` | Non | 1.4 |
| `context` | Tableau facultatif de valeurs qui définit l’endroit à partir de lequel l’extension de messagerie peut être invoquée. Les valeurs possibles `message` sont `compose` , ou `commandBox` . La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Si vous utilisez une liste statique de paramètres, vous les ajouterez également.

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Liste statique des paramètres de la commande. Uniquement `fetchTask` lorsqu’il est utilisé `false` | Non | 1.0 |
| `parameter.name` | Le nom du paramètre. Cette information est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit les objectifs de ce paramètre ou un exemple de la valeur à fournir. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre ou étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Définir sur le type d’entrée requis. Les valeurs `text` possibles sont , , `textarea` `number` `date` `time` `toggle` . La valeur par défaut est définie sur `text` | Non | 1.4 |

Si vous utilisez un affichage web incorporé, vous pouvez éventuellement ajouter l’objet pour récupérer votre affichage web sans appeler `taskInfo` directement votre bot. Si vous choisissez d’utiliser cette option, le comportement est similaire à l’utilisation d’une liste statique de paramètres dans la mesure où la première interaction avec votre bot répondra à l’action d’soumission du module de [tâche.](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md) Si vous utilisez un objet, assurez-vous également de définir `taskInfo` le paramètre sur `fetchTask` `false` .

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
|`taskInfo`|Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie| Non | 1.4 |
|`taskInfo.title`|Titre du module de tâche initial|Non | 1.4 |
|`taskInfo.width`|Largeur du module de tâche : nombre en pixels ou disposition par défaut telle que « grande » ou « moyenne » ou « petite »|Non | 1.4 |
|`taskInfo.height`|Hauteur du module de tâche : nombre en pixels ou disposition par défaut telle que « grande » ou « moyenne » ou « petite »|Non | 1.4 |
|`taskInfo.url`|URL d’affichage web initiale|Non | 1.4 |

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

Voici un exemple d’objet `composeExtensions` définissant deux commandes d’action. Il ne s’agit pas d’un exemple de manifeste complet, pour le schéma de manifeste d’application complet, voir : [Schéma de manifeste d’application](~/resources/schema/manifest-schema.md).

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

## <a name="next-steps"></a>Étapes suivantes

Si vous utilisez une carte adaptative ou un affichage web incorporé sans objet, vous souhaiterez `taskInfo` :

* [Créer et répondre avec un module de tâche](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si vous utilisez des paramètres ou un affichage web incorporé avec un `taskInfo` objet, l’étape suivante consiste à :

* [Répondre à l’soumission du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
