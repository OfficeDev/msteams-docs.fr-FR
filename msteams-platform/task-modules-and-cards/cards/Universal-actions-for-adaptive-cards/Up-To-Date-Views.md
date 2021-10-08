---
title: Affichages à jour
description: Exemple d’affichages à jour à l’aide du bot universel
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 96f87f8795fdd2fed2276b2d67e58d1c394b05f6
ms.sourcegitcommit: d0f1333d5dc5aede963dc59cfb1c2eca70aaf521
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/08/2021
ms.locfileid: "60238236"
---
# <a name="up-to-date-cards"></a>Cartes actualisées

Vous pouvez désormais fournir les dernières informations à vos utilisateurs sur les cartes adaptatives. Incluez une combinaison d’actualisation et de modification de message dans Teams. Mettez à jour dynamiquement les affichages spécifiques de l’utilisateur à leur état le plus récent en cas de modification de votre service. Par exemple, pour la gestion de projet ou les cartes de tickets, mettez à jour les commentaires et l’état de la tâche. Pour les approbations, l’état le plus récent est reflété tout en fournissant des informations et des actions différenciées.

Par exemple, un utilisateur peut créer une demande d’approbation de biens dans Teams conversation. Alex crée une demande d’approbation et l’affecte à Megan et Nestor. Voici les deux parties pour créer la demande d’approbation :

* Les affichages spécifiques à l’utilisateur peuvent être appliqués à `refresh` l’aide de la propriété des cartes adaptatives.
À l’aide des affichages  spécifiques de l’utilisateur, vous pouvez afficher une carte avec des boutons Approuver ou Rejeter à un ensemble d’utilisateurs et afficher une carte sans ces boutons à d’autres utilisateurs. 

* Pour que l’état de la carte reste toujours à jour, Teams mécanisme de modification de message peut être utilisé. Par exemple, pour chaque approbation, le bot peut déclencher une modification de message pour tous les utilisateurs. Cette modification de message de bot déclenche une demande d’appel pour tous les utilisateurs d’actualisation automatique, à laquelle le bot peut répondre avec la carte utilisateur spécifique mise `adaptiveCard/action` à jour.

Pour plus d’informations, [voir comment modifier un message de bot.](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)

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

## <a name="approval-card-with-approve-and-reject-buttons"></a>Carte d’approbation avec boutons Approuver et Rejeter

Le code suivant fournit un exemple de carte d’approbation avec les boutons **Approuver** **et** Rejeter :

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

Les deux rôles présentés aux utilisateurs en fonction de la demande d’approbation sont les suivants :

* Carte de base d’approbation : présentée aux utilisateurs qui ne font pas partie de la liste des approuveurs et que la demande n’est pas encore approuvée ou rejetée, et qu’elle ne fait pas partie de la liste dans la propriété du JSON de carte `userIds` `refresh` adaptative.
* Carte d’approbation  avec **boutons** Approuver ou Rejeter : affichée aux utilisateurs qui font partie de la liste des approuveurs et à la liste dans la propriété du JSON de carte `userIds` adaptative. `refresh`

**Pour envoyer la demande d’approbation de biens**

1. Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.
2. Le bot envoie la carte de base d’approbation dans la conversation.
3. Tous les autres utilisateurs de la conversation voient la carte envoyée par le bot. L’actualisation automatique est déclenchée pour Megan et Nestor,  qui  voient désormais la carte spécifique de l’utilisateur avec des boutons Approuver ou Rejeter lorsque leurs MRIS utilisateur sont ajoutés à la liste dans la propriété de la carte `userIds` adaptative. `refresh`

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Affichages spécifiques à l’utilisateur":::

4. Nestor sélectionne le **bouton Approuver,** qui est alimenté avec `Action.Execute` . Le bot obtient `adaptiveCard/action` une demande d’appel à laquelle il peut renvoyer une carte adaptative en réponse.
5. Le bot déclenche une modification de message avec une carte mise à jour, ce qui indique que Nestor a approuvé la demande pendant que l’approbation de Megan est en attente.
6. La modification du message du bot déclenche une actualisation automatique pour Megan et voit la carte spécifique de  l’utilisateur mise à jour, qui indique que Nestor a approuvé la demande, mais voit également les boutons Approuver ou Rejeter.  L’utilisateur DE NEstor EST supprimé de la liste dans la propriété de cette carte adaptative JSON aux étapes `userIds` `refresh` 4 et 5. À présent, l’actualisation automatique est déclenchée uniquement pour Megan.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Affichages utilisateur spécifiques à jour":::

7. À présent, Megan sélectionne le **bouton Approuver,** qui est alimenté avec `Action.Execute` . Le bot obtient `adaptiveCard/action` une demande d’appel à laquelle il peut renvoyer une carte adaptative en réponse.
8. Le bot déclenche une modification de message avec une carte mise à jour, ce qui indique que Nestor et Megan ont approuvé la demande.
9. La modification du message du bot ne déclenche aucune actualisation automatique. L’utilisateur DE MEGAN EST également supprimé de la liste dans la propriété de cette carte adaptative JSON aux `userIds` `refresh` étapes 7 et 8.

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Affichages à jour":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>Carte adaptative envoyée en réponse à `adaptiveCard/action` et `message edit`

Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse aux étapes `adaptiveCard/action` `message edit` 4 et 5 :

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

Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse à un appel via `adaptiveCard/action` l’actualisation automatique pour l’étape 6 :

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

Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse aux étapes `adaptiveCard/action` `message edit` 7 et 8 :

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
| Cartes adaptatives de flux de travail séquentiels | Montrer comment implémenter des flux de travail séquentiels, des affichages spécifiques à l’utilisateur et des cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Affichages spécifiques à l’utilisateur](User-Specific-Views.md)
