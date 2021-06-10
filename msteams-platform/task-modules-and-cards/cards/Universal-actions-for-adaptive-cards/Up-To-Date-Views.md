---
title: Affichages à jour
description: Exemple d’affichages à jour à l’aide du bot universel
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088843"
---
# <a name="up-to-date-cards"></a>Cartes actualisées

Vous pouvez désormais fournir les dernières informations à vos utilisateurs sur les cartes adaptatives avec une combinaison de modifications d’actualisation et de message Teams. Ainsi, vous pouvez mettre à jour dynamiquement les affichages spécifiques de l’utilisateur à leur état le plus récent en cas de modification de votre service. Par exemple, dans le cas de cartes de gestion de projet ou de tickets, vous pouvez mettre à jour les commentaires et l’état de la tâche. En cas d’approbation, le dernier état est reflété tout en fournissant des informations et des actions différenciées.

Par exemple, un utilisateur peut créer une demande d’approbation de biens dans Teams conversation. Alex crée une demande d’approbation et l’affecte à Megan et Nestor. Voici les deux parties pour créer la demande d’approbation :

* Les vues spécifiques à l’utilisateur peuvent être exploitées à `refresh` l’aide de la propriété des cartes adaptatives.
À l’aide des affichages  spécifiques de l’utilisateur, vous pouvez afficher une carte avec des boutons Approuver ou Rejeter à un ensemble d’utilisateurs et afficher une carte sans ces boutons à d’autres utilisateurs. 

* Pour maintenir l’état de la carte à jour en permanence, Teams mécanisme de modification des messages peut être mis à profit. Par exemple, chaque fois qu’une approbation est en place, le bot peut déclencher une modification de message pour tous les utilisateurs. Cette modification de message de bot déclenche une demande d’appel pour tous les utilisateurs d’actualisation automatique, à laquelle le bot peut répondre avec la carte utilisateur spécifique mise `adaptiveCard/action` à jour.

Pour plus d’informations, [voir comment modifier un message de bot.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)

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

Voici les deux rôles présentés aux utilisateurs en fonction de leur implication dans la demande d’approbation :

* Carte de base d’approbation : présentée aux utilisateurs qui ne font pas partie de la liste des approuveurs et qui n’ont pas encore approuvé ou rejeté la demande et qui ne font pas partie de la liste dans la propriété du JSON de carte `userIds` `refresh` adaptative.
* Carte d’approbation  avec **boutons** Approuver ou Rejeter : affichée aux utilisateurs qui font partie de la liste des approuveurs et à la liste dans la propriété du JSON de carte `userIds` adaptative. `refresh`

**Pour envoyer la demande d’approbation de biens**

1. Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.
2. Le bot envoie la carte de base d’approbation dans la conversation.
3. Tous les autres utilisateurs de la conversation voient la carte envoyée par le bot. L’actualisation automatique est déclenchée pour Megan et Nestor,  qui  voient désormais la carte spécifique de l’utilisateur avec des boutons Approuver ou Rejeter lorsque leurs MRIS utilisateur sont ajoutés à la liste dans la propriété de la carte `userIds` adaptative. `refresh`

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Affichages spécifiques à l’utilisateur":::

4. Nestor sélectionne le **bouton Approuver** qui est alimenté avec `Action.Execute` . Le bot obtient `adaptiveCard/action` une demande d’appel à laquelle il peut renvoyer une carte adaptative en réponse.
5. Le bot déclenche une modification de message avec une carte mise à jour qui indique que Nestor a approuvé la demande pendant que l’approbation de Megan est en attente.
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

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Affichages spécifiques à l’utilisateur](User-Specific-Views.md)
