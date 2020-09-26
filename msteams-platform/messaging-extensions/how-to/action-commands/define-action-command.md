---
title: Définir les commandes d’action d’extension de messagerie
author: clearab
description: Vue d’ensemble des extensions de messagerie sur la plateforme Microsoft teams
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 89cf92260418701ef4809f5a13750b991b9f7acb
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279680"
---
# <a name="define-messaging-extension-action-commands"></a>Définir les commandes d’action d’extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes d’action vous permettent de présenter une fenêtre contextuelle modale (appelée module de tâches dans Teams) à vos utilisateurs afin de collecter ou d’afficher des informations, puis de traiter leur interaction et de renvoyer des informations à Teams. Avant de créer votre commande, vous devez décider :

1. À partir de quel emplacement la commande d’action peut-elle être déclenchée ?
1. Comment le module de tâche sera-t-il créé ?
1. Le message final ou la carte sera-t-il envoyé à la chaîne à partir d’un bot ou sera-t-il inséré dans la zone de message de composition pour que l’utilisateur l’envoie ?

## <a name="choose-action-command-invoke-locations"></a>Choisir les emplacements d’appel de commande d’action

La première chose que vous devez décider est l’emplacement où votre commande d’action peut être déclenchée (ou plus spécifiquement *appelée*). En spécifiant le `context` dans votre manifeste d’application, votre commande peut être appelée à partir d’un ou plusieurs des emplacements suivants :

* Boutons situés en bas de la zone de message de composition.
* En @mentioning votre application dans la zone commande. Remarque : vous ne pouvez pas répondre avec un message bot inséré directement dans la conversation si votre extension de messagerie est appelée à partir de la zone de commande.
* Directement à partir d’un message existant via le... menu débordement sur un message. Remarque : l’appel initial de votre bot inclut un objet JSON contenant le message à partir duquel il a été appelé, que vous pouvez traiter avant de les présenter avec un module de tâches.

## <a name="choose-how-to-build-your-task-module"></a>Choisir comment créer votre module de tâches

En plus de choisir l’emplacement à partir duquel votre commande peut être appelée, vous devez également choisir comment remplir le formulaire dans le module de tâches pour vos utilisateurs. Vous disposez de trois options pour créer le formulaire qui est affiché à l’intérieur du module de tâche :

* **Liste statique des paramètres** : il s’agit de l’option la plus simple. Vous pouvez définir une liste de paramètres (champs de saisie) dans le manifeste de votre application que le client teams affichera. Vous ne pouvez pas contrôler la mise en forme avec cette option.
* **Carte adaptative** : vous pouvez choisir d’utiliser une carte adaptative, qui offre un meilleur contrôle de l’interface utilisateur, mais qui vous permet toujours de vous limiter aux contrôles disponibles et aux options de mise en forme.
* **Vue Web incorporée** : Si vous avez besoin d’un contrôle total sur l’interface utilisateur et les contrôles, vous pouvez choisir d’incorporer une vue Web personnalisée dans le module de tâches.

Si vous choisissez de créer votre module de tâches avec une liste statique de paramètres, le premier appel à votre extension de messagerie se fera lorsqu’un utilisateur soumet le module de tâche. Lorsque vous utilisez une vue Web incorporée ou une carte adaptative, votre extension de messagerie doit gérer un événement d’appel initial de la part de l’utilisateur, créer le module de tâche et le renvoyer au client.

## <a name="choose-how-the-final-message-will-be-sent"></a>Choisir le mode d’envoi du message final

Dans la plupart des cas, la commande action entraîne l’insertion d’une carte insérée dans la boîte de message composer. Votre utilisateur peut alors décider de l’envoyer au canal ou à la conversation. Dans ce cas, le message provient de l’utilisateur et votre bot ne pourra plus modifier ou mettre à jour la carte.

Si votre extension de messagerie est déclenchée à partir de la zone de composition ou directement à partir d’un message, votre service Web peut insérer la réponse finale directement dans le canal ou la conversation. Dans ce cas, la carte adaptative provient du bot, le bot pourra le mettre à jour, et le robot peut également répondre au thread de conversation si nécessaire. Vous devrez ajouter l' `bot` objet à votre manifeste d’application à l’aide du même ID et en définissant les étendues appropriées.

## <a name="add-the-command-to-your-app-manifest"></a>Ajouter la commande à votre manifeste d’application

Maintenant que vous avez décidé de la façon dont les utilisateurs interagissent avec votre commande action, il est temps de l’ajouter à votre manifeste d’application. Pour ce faire, vous allez ajouter un nouvel `composeExtension` objet au niveau supérieur de votre fichier JSON de manifeste d’application. Vous pouvez le faire à l’aide de l’aide d’App Studio ou manuellement.

### <a name="create-a-command-using-app-studio"></a>Créer une commande à l’aide d’App Studio

Les étapes suivantes supposent que vous avez déjà [créé une extension de messagerie](~/messaging-extensions/how-to/create-messaging-extension.md).

1. À partir du client Microsoft Teams, ouvrez l' **application Studio** et sélectionnez l’onglet **éditeur de manifeste** .
2. Si vous avez déjà créé votre package d’application dans l’application Studio, sélectionnez-le dans la liste. Si ce n’est pas le cas, vous pouvez importer un package d’application existant.
3. Cliquez sur le bouton **Ajouter** dans la section commande.
4. Choisissez **autoriser les utilisateurs à déclencher des actions dans les services externes dans teams**.
5. Si vous souhaitez utiliser un ensemble statique de paramètres pour créer votre module de tâches, sélectionnez cette option. Dans le cas contraire, choisissez d' **extraire un ensemble dynamique de paramètres de votre bot**.
6. Ajoutez un **ID de commande** et un **titre**.
7. Sélectionnez l’emplacement à partir duquel vous souhaitez déclencher la commande d’action.
8. Si vous utilisez des paramètres pour votre module de tâches, ajoutez le premier.
9. Cliquez sur Save (Enregistrer)
10. Si vous avez besoin d’ajouter d’autres paramètres, cliquez sur le bouton **Ajouter** dans la section **paramètres** pour les ajouter.

### <a name="manually-create-a-command"></a>Créer manuellement une commande

Pour ajouter manuellement votre commande d’extension de messagerie basée sur une action à votre manifeste d’application, vous devez ajouter les paramètres follow à votre `composeExtension.commands` tableau d’objets.

| Nom de la propriété | Objectif | Obligatoire ? | Version de manifeste minimale |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur contiendra cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Doivent être `action` | Non | 1.4 |
| `fetchTask` | `true` pour une carte adaptative ou une vue Web incorporée pour votre module de tâches, `false` pour une liste statique de paramètres ou lors du chargement de l’affichage Web par un `taskInfo` | Non | 1.4 |
| `context` | Tableau facultatif de valeurs qui définit l’emplacement à partir duquel l’extension de messagerie peut être appelée. Les valeurs possibles sont `message` , `compose` ou `commandBox` . La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Si vous utilisez une liste statique de paramètres, vous allez également les ajouter.

| Nom de la propriété | Objectif | Obligatoire ? | Version de manifeste minimale |
|---|---|---|---|
| `parameters` | Liste statique des paramètres de la commande. Utilisez uniquement lorsque `fetchTask` est `false` | Non | 1.0 |
| `parameter.name` | Le nom du paramètre. Cette adresse est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit ce paramètre ou un exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre de paramètre court convivial ou étiquette. | Oui | 1.0 |
| `parameter.inputType` | Défini sur le type d’entrée requis. Les valeurs possibles sont `text` ,,,, `textarea` `number` `date` `time` et `toggle` . La valeur par défaut est définie sur `text` | Non | 1.4 |

Si vous utilisez une vue Web incorporée, vous pouvez éventuellement ajouter l' `taskInfo` objet pour récupérer votre vue Web sans appeler directement votre bot. Si vous choisissez d’utiliser cette option, le comportement est similaire à l’utilisation d’une liste statique de paramètres dans la mesure où la première interaction avec votre bot [répond à l’action de soumission du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md). Si vous utilisez un `taskInfo` objet, veillez à définir également le `fetchTask` paramètre sur `false` .

| Nom de la propriété | Objectif | Obligatoire ? | Version de manifeste minimale |
|---|---|---|---|
|`taskInfo`|Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie| Non | 1.4 |
|`taskInfo.title`|Titre du module de tâche initiale|Non | 1.4 |
|`taskInfo.width`|Largeur du module de tâche-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »|Non | 1.4 |
|`taskInfo.height`|Hauteur du module de tâche-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »|Non | 1.4 |
|`taskInfo.url`|URL d’affichage Web initiale|Non | 1.4 |

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

Voici un exemple d' `composeExtensions` objet qui définit deux commandes action. Il ne s’agit pas d’un exemple du manifeste complet, pour le schéma de manifeste d’application complet, voir : [schéma de manifeste d’application](~/resources/schema/manifest-schema.md).

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
        "fetchTask": false,
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

Si vous utilisez une carte adaptative ou une vue Web incorporée sans `taskInfo` objet, vous devez :

* [Créer et répondre à l’aide d’un module de tâches](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si vous utilisez des paramètres ou une vue Web incorporée avec un `taskInfo` objet, l’étape suivante consiste à :

* [Répondre à l’envoi du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
