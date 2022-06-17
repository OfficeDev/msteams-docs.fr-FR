---
title: Affichages à jour
description: Dans ce module, découvrez les vues de cartes à jour à l’aide d’exemples de bot universel avec code dans Microsoft Teams
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5c6f7d13cd884baf9ffbc1fd30cafb7cfab33295
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143619"
---
# <a name="up-to-date-cards"></a>Cartes actualisées

Vous pouvez désormais fournir des informations les plus récentes à vos utilisateurs sur les cartes adaptatives. Incluez une combinaison d’actualisation et de modifications de messages dans Teams. Mettez à jour dynamiquement les vues spécifiques de l’utilisateur à son état le plus récent en cas de modification sur votre service. Par exemple, pour les cartes de gestion de projet ou de ticketing, mettez à jour les commentaires et l’état de la tâche. Pour les approbations, l’état le plus récent est reflété tout en fournissant des informations et des actions différenciées.

Par exemple, un utilisateur peut créer une demande d’approbation de ressource dans une conversation Teams. Alex crée une demande d’approbation et l’affecte à Megan et Nestor. Voici les deux parties permettant de créer la demande d’approbation :

* Les vues spécifiques à l’utilisateur peuvent être appliquées à l’aide de la `refresh` propriété des cartes adaptatives.
À l’aide de vues spécifiques à l’utilisateur, vous pouvez afficher une carte avec des boutons **Approuver** ou **Rejeter** pour un ensemble d’utilisateurs, et afficher une carte sans ces boutons à d’autres utilisateurs.

* Pour que l’état de la carte soit toujours mis à jour, Teams mécanisme de modification des messages peut être utilisé. Par exemple, pour chaque approbation, le bot peut déclencher une modification de message pour tous les utilisateurs. Cette modification du message du bot déclenche une demande d’appel `adaptiveCard/action` pour tous les utilisateurs d’actualisation automatique, à laquelle le bot peut répondre avec la carte spécifique de l’utilisateur mise à jour.

Pour plus d’informations, voir [comment modifier un message de bot](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).

## <a name="approval-base-card"></a>Carte de base d’approbation

Le code suivant fournit un exemple de carte de base d’approbation :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a>Carte d’approbation avec les boutons Approuver et Rejeter

Le code suivant fournit un exemple de carte d’approbation avec les boutons **Approuver** et **Rejeter** :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

Voici les deux rôles qui sont présentés aux utilisateurs en fonction de la demande d’approbation :

* Carte de base d’approbation : affichée aux utilisateurs ne faisant pas partie de la liste des approbateurs et la demande n’est pas encore approuvée ou rejetée, et ne fait pas partie de la `userIds` liste dans `refresh` la propriété du JSON de carte adaptative.
* Carte d’approbation avec les boutons **Approuver** ou **Refuser** : présentée aux utilisateurs qui font partie de la liste des approbateurs et à la `userIds` liste dans la `refresh` propriété du JSON de carte adaptative.

Pour envoyer la demande d’approbation de ressource :

1. Alex déclenche une demande d’approbation de ressource dans une conversation Teams et l’affecte à Megan et Nestor.
2. Le bot envoie la carte de base d’approbation dans la conversation.
3. Tous les autres utilisateurs de la conversation voient la carte envoyée par le bot. L’actualisation automatique est déclenchée pour Megan et Nestor, qui voient désormais la carte spécifique de l’utilisateur avec les boutons **Approuver** ou **Rejeter** lorsque leurs IRM utilisateur sont ajoutées à la `userIds` liste dans la `refresh` propriété de la carte adaptative.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Affichages spécifiques à l’utilisateur":::

4. Nestor sélectionne le bouton **Approuver** , qui est alimenté avec `Action.Execute`. Le bot obtient une demande d’appel `adaptiveCard/action` à laquelle il peut retourner une carte adaptative en réponse.
5. Le bot déclenche une modification de message avec une carte mise à jour, qui indique que Nestor a approuvé la demande pendant que l’approbation de Megan est en attente.
6. La modification du message du bot déclenche une actualisation automatique pour Megan et elle voit la carte spécifique de l’utilisateur mise à jour, qui indique que Nestor a approuvé la demande, mais voit également les boutons **Approuver** ou **Rejeter** . L’IRM utilisateur de Nestor est supprimée de la liste dans `refresh` la `userIds` propriété de ce JSON de carte adaptative aux étapes 4 et 5. Maintenant, l’actualisation automatique est déclenchée uniquement pour Megan.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Affichages spécifiques à l’utilisateur à jour":::

7. Maintenant, Megan sélectionne le bouton **Approuver** , qui est alimenté avec `Action.Execute`. Le bot obtient une demande d’appel `adaptiveCard/action` à laquelle il peut retourner une carte adaptative en réponse.
8. Le bot déclenche une modification de message avec une carte mise à jour, ce qui indique que Nestor et Megan ont approuvé la demande.
9. La modification du message du bot ne déclenche aucune actualisation automatique. L’IRM utilisateur de Megan est également supprimée de la liste dans `refresh` la `userIds` propriété de cette carte adaptative JSON dans les étapes 7 et 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Affichages à jour":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Carte adaptative envoyée comme réponse de `adaptiveCard/action` et `message edit`

Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse aux `adaptiveCard/action` `message edit` étapes 4 et 5 :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

Le code suivant fournit un exemple de cartes adaptatives envoyées comme réponse d’appel par le biais de `adaptiveCard/action` l’actualisation automatique pour l’étape 6 :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse aux `adaptiveCard/action` `message edit` étapes 7 et 8 :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Flux de travail séquentiels Cartes adaptatives | Montrez comment implémenter des flux de travail séquentiels, des vues spécifiques à l’utilisateur et des Cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Affichages spécifiques à l’utilisateur](User-Specific-Views.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
