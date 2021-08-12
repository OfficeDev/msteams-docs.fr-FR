---
title: Affichages spécifiques à l’utilisateur
description: Exemple d’affichages spécifiques à l’utilisateur à l’aide d’actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 00d6c8e5109fdd9cdf83662f9585a9a2d9e7fd86
ms.sourcegitcommit: 6a41c529a423c81a184c7a79125dbaaed0179788
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/26/2021
ms.locfileid: "53585983"
---
# <a name="user-specific-views"></a>Affichages spécifiques à l’utilisateur

Auparavant, si des cartes adaptatives ont été envoyées dans Teams conversation, tous les utilisateurs voient exactement le même contenu de carte. Avec l’introduction du modèle Actions universelles et des cartes adaptatives, les développeurs de bots peuvent désormais fournir des affichages spécifiques aux utilisateurs de cartes `refresh` adaptatives aux utilisateurs. La même carte adaptative peut désormais être actualisée sur une carte adaptative spécifique à l’utilisateur. Un maximum de 60 utilisateurs différents peuvent voir une version différente de la carte avec des informations ou des actions supplémentaires. La carte adaptative fournit des scénarios puissants tels que les approbations, les contrôles de créateur de sondage, la gestion des tickets, la gestion des incidents et les cartes de gestion de projet.

Par exemple, Megan, inspecteur de sécurité chez Contoso, souhaite créer un incident et l’affecter à Alex. Megan souhaite également que tous les membres de l’équipe soient informés de l’incident. Megan utilise l’extension de message de rapport d’incident Contoso optimisée par les actions universelles pour les cartes adaptatives.

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Affichages spécifiques aux utilisateurs mobiles":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>Affichages spécifiques à l’utilisateur pour les cartes adaptatives

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

**Pour envoyer des cartes adaptatives, actualisez les affichages spécifiques de l’utilisateur et invoquez des demandes au bot**

1. Lorsque Megan crée un incident, le bot envoie la carte adaptative ou la carte commune avec les détails de l’incident dans Teams conversation.
2. Désormais, cette carte est automatiquement actualisée en vue spécifique de l’utilisateur pour Megan et Alex. Les MRI utilisateur d’Alex et Megan sont ajoutés dans la propriété de propriété du JSON de `userIds` `refresh` carte adaptative. La carte reste la même pour les autres utilisateurs de la conversation.
3. Pour Megan, l’actualisation automatique déclenche une `adaptiveCard/action` demande d’appel au bot. Le bot peut renvoyer une carte de créateur d’incident avec un bouton en réponse `Edit` à cette demande d’appel.
4. De même pour Alex, l’actualisation automatique déclenche une autre `adaptiveCard/action` demande d’appel au bot. Le bot peut renvoyer un bouton de carte de propriétaire d’incident en réponse `Resolve` à cette demande d’appel.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Appeler la demande envoyée depuis Teams client au bot

Le code suivant fournit un exemple d’une demande d’appel envoyée par le client d’Alex Teams Megan au bot :

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

## <a name="adaptivecardaction-invoke-response-card"></a>Carte de réponse d’appel adaptiveCard/action

Le code suivant fournit un exemple de carte de réponse d’appel adaptiveCard/action pour Megan :

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>Carte de réponse d’appel adaptiveCard/action pour Alex

Le code suivant fournit un exemple de carte de réponse d’appel adaptiveCard/action pour Alex :

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Appeler la réponse pour renvoyer des cartes adaptatives

Le code suivant fournit un exemple de réponse d’appel pour renvoyer des cartes adaptatives :

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

Recommandations en matière de conception de carte à garder à l’esprit lors de la conception d’affichages spécifiques à l’utilisateur :

* Vous pouvez créer un maximum de **60 affichages** spécifiques à l’utilisateur pour une carte spécifique envoyée à une conversation ou un canal en spécifiant leur `userIds` dans la `refresh` section.
* **Carte de base :** Version de base de la carte que le développeur du bot envoie à la conversation. La version de base est la version de la carte adaptative pour tous les utilisateurs qui ne sont pas spécifiés dans la `userIds` section.
* Une mise à jour de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique de l’utilisateur. L’ouverture de la conversation ou du canal actualisera également la carte pour les utilisateurs avec l’actualisation activée.
* Pour les scénarios avec des groupes plus importants dans lesquels les utilisateurs basculent vers une vue d’action, qui nécessite des mises à jour dynamiques pour les répondeurs, vous pouvez continuer à ajouter jusqu’à 60 utilisateurs à la `userIds` liste. Vous pouvez supprimer le premier répondeur de la liste lorsque le 61e utilisateur répond. Pour les utilisateurs qui sont supprimés de la liste, vous pouvez fournir un bouton d’actualisation manuelle ou utiliser le bouton Actualiser dans le menu options du message pour obtenir le `userIds` dernier résultat.
* Invitez les utilisateurs à obtenir un affichage spécifique de l’utilisateur, où ils voient uniquement un affichage particulier de la carte ou certaines actions.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Cartes adaptatives de flux de travail séquentiels | Montrer comment implémenter des flux de travail séquentiels, des affichages spécifiques de l’utilisateur et des cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Affichages à jour](Up-To-Date-Views.md)
