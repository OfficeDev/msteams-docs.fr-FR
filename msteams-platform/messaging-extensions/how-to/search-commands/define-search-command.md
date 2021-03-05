---
title: Définir les commandes de recherche d’extension de messagerie
author: clearab
description: Définissez les commandes de recherche d’extension de messagerie pour les applications Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449268"
---
# <a name="define-messaging-extension-search-commands"></a>Définir les commandes de recherche d’extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes de recherche d’extension de messagerie permettent à vos utilisateurs d’effectuer une recherche dans des systèmes externes et d’insérer les résultats de la recherche dans un message sous la forme d’une carte.

> [!NOTE]
> La limite de taille de carte de résultat est de 28 Ko. La carte n’est pas envoyée si sa taille dépasse 28 Ko. 

## <a name="choose-messaging-extension-invoke-locations"></a>Choisir les emplacements d’appel d’extension de messagerie

La première chose que vous devez déterminer est l’endroit à partir de lequel votre commande de recherche peut être déclenchée (ou spécifiquement *invoquée).* Votre commande de recherche peut être invoquée à partir de l’un des emplacements suivants ou des deux :

* Boutons situés en bas de la zone composer un message
* En @mentioning dans la zone de commande

Lorsqu’il est appelé à partir de la zone de composition du message, votre utilisateur a la possibilité d’envoyer les résultats à la conversation. Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur peut interagir avec la carte résultante ou la copier pour l’utiliser ailleurs.

## <a name="add-the-command-to-your-app-manifest"></a>Ajouter la commande au manifeste de votre application

Maintenant que vous avez décidé de la façon dont les utilisateurs interagira avec votre commande de recherche, il est temps de l’ajouter au manifeste de votre application. Pour ce faire, vous allez ajouter un nouvel objet au niveau `composeExtension` supérieur du manifeste JSON de votre application. Vous pouvez le faire à l’aide d’App Studio ou manuellement.

### <a name="create-a-command-using-app-studio"></a>Créer une commande à l’aide d’App Studio

La condition préalable à la création d’une commande de recherche est que vous devez déjà créer une extension de messagerie. Pour plus d’informations sur la création d’une extension de messagerie, voir [créer une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)

**Pour créer une commande de recherche**

1. Dans le client Microsoft Teams, ouvrez **App Studio** et sélectionnez l’onglet **Éditeur de** manifeste.
1. Si vous avez déjà créé un package d’application dans **App Studio,** choisissez-le dans la liste. Si vous n’avez pas créé de package d’application, importez-en un existant.
1. Après avoir importé un package d’application, sélectionnez **les extensions de messagerie sous** **Fonctionnalités.**
1. Sélectionnez **Ajouter** dans la section **Commande** de la page Extensions de messagerie.
1. Choisissez **Autoriser les utilisateurs à interroger votre service pour obtenir des informations et à les insérer dans un message.**
1. Ajoutez **un ID de commande** et un **titre.**
1. Sélectionnez l’emplacement à partir de lequel votre commande de recherche doit être déclenchée. La sélection **d’un message** ne modifie pas actuellement le comportement de votre commande de recherche.
1. Ajoutez votre paramètre de recherche et sélectionnez **Enregistrer.**
 
### <a name="manually-create-a-command"></a>Créer manuellement une commande

Pour ajouter manuellement votre commande de recherche d’extension de messagerie au manifeste de votre application, vous devez ajouter les paramètres suivants à votre `composeExtension.commands` tableau d’objets.

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Texte d’aide indiquant ce que fait cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Doit être `query` | Non | 1.4 |
|`initialRun` | Si la valeur **est true,** indique que cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur. | Non | 1.0 |
| `context` | Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible. Les valeurs possibles `message` sont , `compose` ou `commandBox` . La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Vous devez également ajouter les détails du paramètre de recherche, qui définit le texte visible pour votre utilisateur dans le client Teams.

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Liste statique des paramètres de la commande. | Non | 1.0 |
| `parameter.name` | Le nom du paramètre. Cette information est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit les objectifs de ce paramètre ou un exemple de la valeur à fournir. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre ou étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Définir sur le type d’entrée requis. Les valeurs `text` possibles sont , , , , `textarea` `number` `date` `time` `toggle` . La valeur par défaut est définie sur `text` | Non | 1.4 |

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

Vous trouverez ci-dessous un exemple `composeExtensions` d’objet définissant une commande de recherche. Il ne s’agit pas d’un exemple de manifeste complet, pour le schéma de manifeste d’application complet, voir : [Schéma de manifeste d’application](~/resources/schema/manifest-schema.md).

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

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez ajouté votre commande de recherche, vous devez gérer [la demande de recherche.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
