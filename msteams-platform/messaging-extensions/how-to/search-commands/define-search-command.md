---
title: Définir les commandes de recherche d’extension de messagerie
author: clearab
description: Définir les commandes de recherche d’extension de messagerie pour les applications Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673848"
---
# <a name="define-messaging-extension-search-commands"></a>Définir les commandes de recherche d’extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes de recherche d’extension de messagerie permettent à vos utilisateurs d’effectuer des recherches dans des systèmes externes et d’insérer les résultats de cette recherche dans un message sous la forme d’une carte.

## <a name="choose-messaging-extension-invoke-locations"></a>Choisir les emplacements d’appel d’extension de messagerie

La première chose que vous devez décider est l’emplacement où votre commande de recherche peut être déclenchée (ou plus spécifiquement *appelée*). Votre commande de recherche peut être appelée à partir de l’un des emplacements suivants (ou les deux) :

* Les boutons situés en bas de la zone de message de composition
* Par @mentioning dans la zone de commande

Lorsqu’il est appelé à partir de la zone de message de composition, votre utilisateur a la possibilité d’envoyer les résultats à la conversation. Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur peut interagir avec la carte résultante ou la copier pour une utilisation ailleurs.

## <a name="add-the-command-to-your-app-manifest"></a>Ajouter la commande à votre manifeste d’application

Maintenant que vous avez décidé de la façon dont les utilisateurs vont interagir avec votre commande de recherche, il est temps de l’ajouter à votre manifeste d’application. Pour ce faire, vous allez ajouter un `composeExtension` nouvel objet au niveau supérieur de votre fichier JSON de manifeste d’application. Vous pouvez le faire à l’aide de l’aide d’App Studio ou manuellement.

### <a name="create-a-command-using-app-studio"></a>Créer une commande à l’aide d’App Studio

Les étapes suivantes supposent que vous avez déjà [créé une extension de messagerie](~/messaging-extensions/how-to/create-messaging-extension.md).

1. À partir du client Microsoft Teams, ouvrez l' **application Studio** et sélectionnez l’onglet **éditeur de manifeste** .
2. Si vous avez déjà créé votre package d’application dans l’application Studio, sélectionnez-le dans la liste. Si ce n’est pas le cas, vous pouvez importer un package d’application existant.
3. Cliquez sur le bouton **Ajouter** dans la section commande.
4. Choisissez **autoriser les utilisateurs à interroger votre service pour obtenir des informations et les insérer dans un message**.
5. Ajoutez un **ID de commande** et un **titre**.
6. Sélectionnez l’emplacement à partir duquel vous souhaitez déclencher la commande de recherche. La sélection de **message** ne modifie actuellement pas le comportement de votre commande de recherche.
7. Ajoutez votre paramètre de recherche.
8. Cliquez sur Enregistrer.

### <a name="manually-create-a-command"></a>Créer manuellement une commande

Pour ajouter manuellement votre commande de recherche d’extension de messagerie à votre manifeste d’application, vous devez ajouter les paramètres follow `composeExtension.commands` à votre tableau d’objets.

| Nom de la propriété | Objectif | Obligatoire ? | Version de manifeste minimale |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur contiendra cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Texte d’aide indiquant la signification de cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Doivent être`query` | Non | 1.4 |
|`initialRun` | Si la valeur est définie sur **true**, cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur. | Non | 1.0 |
| `context` | Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible. Les valeurs possibles `message`sont `compose`, ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Vous devrez également ajouter les détails du paramètre de recherche, qui définira le texte visible par votre utilisateur dans le client Teams.

| Nom de la propriété | Objectif | Obligatoire ? | Version de manifeste minimale |
|---|---|---|---|
| `parameters` | Liste statique des paramètres de la commande. | Non | 1.0 |
| `parameter.name` | Le nom du paramètre. Cette adresse est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit ce paramètre ou un exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre de paramètre court convivial ou étiquette. | Oui | 1.0 |
| `parameter.inputType` | Défini sur le type d’entrée requis. Les valeurs possibles `text`sont `textarea`, `number`, `date`, `time`, `toggle`et. La valeur par défaut est définie sur`text` | Non | 1.4 |

#### <a name="app-manifest-example"></a>Exemple de manifeste d’application

Voici un exemple d’un `composeExtensions` objet qui définit une commande de recherche. Il ne s’agit pas d’un exemple du manifeste complet, pour le schéma de manifeste d’application complet, voir : [schéma de manifeste d’application](~/resources/schema/manifest-schema.md).

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

À présent que vous avez ajouté votre commande de recherche, vous devez [gérer la demande de recherche](~/messaging-extensions/how-to/search-commands/respond-to-search.md).

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]