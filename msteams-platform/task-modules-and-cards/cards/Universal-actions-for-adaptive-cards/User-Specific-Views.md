---
title: Affichages spécifiques à l’utilisateur
description: Exemple pour les vues spécifiques des utilisateurs à l’aide d’actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 696fc5ce25c79d749b301309bfe0c737e39ad294
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555443"
---
# <a name="user-specific-views"></a>Affichages spécifiques à l’utilisateur

Plus tôt, si adaptive cards a été envoyé dans Teams conversation, tous les utilisateurs voient exactement le même contenu de carte. Avec l’introduction du modèle Actions Universelles et des cartes `refresh` adaptatives, les développeurs de bots peuvent désormais fournir aux utilisateurs des vues spécifiques des cartes adaptatives. La même carte adaptative peut maintenant se rafraîchir à une carte adaptative spécifique à l’utilisateur.

Par exemple, Megan, inspectrice de sécurité chez Contoso, veut créer un incident et l’assigner à Alex. Elle veut aussi que tous les membres de l’équipe soient au courant de l’incident. Megan utilise l’extension de message de rapport d’incident Contoso alimentée par Universal Actions for Adaptive Cards.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur":::

## <a name="user-specific-views-for-adaptive-cards"></a>Vues spécifiques de l’utilisateur pour les cartes adaptatives

Le code suivant fournit un exemple de cartes adaptatives :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
              "refresh info": "<refresh info>"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

**Pour envoyer des cartes adaptatives, actualisez les vues spécifiques de l’utilisateur et invoquez les demandes au bot**

1. Lorsque Megan crée un nouvel incident, le bot envoie la carte adaptative ou la carte commune avec les détails de l’incident dans Teams conversation.
2. Maintenant, cette carte se rafraîchit automatiquement à l’utilisateur vue spécifique pour Megan et Alex. Les IRM utilisateur d’Alex et Megan sont ajoutées dans la `userIds` propriété de la carte `refresh` adaptative JSON. La carte reste la même pour les autres utilisateurs de la conversation.
3. Pour Megan, la mise à jour automatique déclenche une demande `adaptiveCard/action` d’invocisation au bot. Le bot peut retourner une carte de créateur d’incident avec `Edit` bouton en réponse à cette demande d’invocateur.
4. De même pour Alex, la mise à jour automatique déclenche une autre `adaptiveCard/action` demande d’invocisation au bot. Le bot peut retourner un bouton de carte propriétaire incident `Resolve` comme une réponse à cette demande d’invocateur.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Invoquer la demande envoyée Teams client au bot

Le code suivant fournit un exemple d’une demande d’invocer envoyée par alex et megan Teams client au bot:

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoquent la carte de réponse

Le code suivant fournit un exemple d’une carte adaptative / action invoquer carte de réponse pour Megan:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action invoquent la carte de réponse pour Alex

Le code suivant fournit un exemple de carte adaptative/action invoquer la carte de réponse pour Alex:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>Invoquer la réponse pour retourner les cartes adaptatives

Le code suivant fournit un exemple de réponse invocative pour renvoyer les cartes adaptatives :

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

Lignes directrices de conception de cartes à garder à l’esprit lors de la conception de vues spécifiques à l’utilisateur :

* Vous pouvez créer un maximum de **60 vues spécifiques à l’utilisateur** pour une carte particulière envoyée à un chat ou un canal en spécifier `userIds` leur dans la `refresh` section.
* **Carte de base:** La version de base de la carte que le développeur de bot envoie au chat. Il s’agit de la version de la carte adaptative pour tous les utilisateurs qui ne sont pas spécifiés dans `userIds` la section.
* Une mise à jour ou une modification de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique à l’utilisateur.

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Vues à jour](Up-To-Date-Views.md)
