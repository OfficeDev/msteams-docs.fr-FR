---
title: Affichages spécifiques à l’utilisateur
description: En savoir plus sur les vues spécifiques à l’utilisateur à l’aide d’actions universelles avec l’exemple de code
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b2e5b8d6dd00104fab819ba7d05d5913bb891d83
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073679"
---
# <a name="user-specific-views"></a>Affichages spécifiques à l’utilisateur

Plus tôt, si les cartes adaptatives ont été envoyées dans une conversation Teams, tous les utilisateurs voient exactement le même contenu de carte. Avec l’introduction du modèle Actions universelles et `refresh` des cartes adaptatives, les développeurs de bots peuvent désormais fournir aux utilisateurs des vues spécifiques aux utilisateurs des cartes adaptatives. La même carte adaptative peut désormais être actualisée pour une carte adaptative spécifique à l’utilisateur. Au maximum 60 utilisateurs différents peuvent voir une version différente de la carte avec des informations ou des actions supplémentaires. La carte adaptative fournit des scénarios puissants tels que les approbations, les contrôles de créateur de sondage, la création de tickets, la gestion des incidents et les cartes de gestion de projet.

> [!NOTE]
> La vue spécifique à l’utilisateur est prise en charge pour les cartes adaptatives envoyées par un bot et dépend des actions universelles.

Par exemple, Megan, inspecteur de sécurité chez Contoso, souhaite créer un incident et l’affecter à Alex. Megan veut également que tous les membres de l’équipe soient au courant de l’incident. Megan utilise l’extension de message de rapport d’incidents Contoso optimisée par actions universelles pour les cartes adaptatives.

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vues spécifiques à l’utilisateur mobile" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>Vues spécifiques à l’utilisateur pour les cartes adaptatives

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
      }
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

Pour envoyer des cartes adaptatives, actualisez les vues spécifiques à l’utilisateur et  invokez les demandes au bot :

1. Lorsque Megan crée un incident, le bot envoie la carte adaptative ou la carte commune avec les détails de l’incident dans la conversation Teams.
2. À présent, cette carte est automatiquement actualisée en mode spécifique à l’utilisateur pour Megan et Alex. Les MRIS utilisateur d’Alex et Megan sont ajoutés dans `userIds` la propriété de `refresh` propriété du JSON de carte adaptative. La carte reste la même pour les autres utilisateurs de la conversation.
3. Pour Megan, l’actualisation automatique déclenche une demande d’appel `adaptiveCard/action` au bot. Le bot peut retourner une carte de créateur d’incident avec `Edit` le bouton comme réponse à cette demande d’appel.
4. De même pour Alex, l’actualisation automatique déclenche une autre `adaptiveCard/action` demande d’appel au bot. Le bot peut retourner un bouton de carte `Resolve` propriétaire d’incident en réponse à cette demande d’appel.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Appeler une requête envoyée par Teams client au bot

Le code suivant fournit un exemple de demande d’appel envoyée par le client Teams d’Alex et Megan au bot :

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

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoke response card

Le code suivant fournit un exemple de carte de réponse adaptiveCard/action invoke pour Megan :

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action invoke response card for Alex

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Appeler la réponse pour retourner des cartes adaptatives

Le code suivant fournit un exemple de réponse d’appel pour retourner des cartes adaptatives :

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

***

Instructions de conception de carte à garder à l’esprit lors de la conception de vues spécifiques à l’utilisateur :

* Vous pouvez créer un maximum de **60 vues spécifiques à l’utilisateur** pour une carte particulière envoyée à une conversation ou à un canal en spécifiant leur `userIds` contenu dans la `refresh` section.
* **Carte de base :** Version de base de la carte que le développeur du bot envoie à la conversation. La version de base est la version de la carte adaptative pour tous les utilisateurs qui ne sont pas spécifiés dans la `userIds` section.
* Une mise à jour de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique à l’utilisateur. L’ouverture de la conversation ou du canal actualise également la carte pour les utilisateurs avec l’actualisation activée.
* Pour les scénarios avec des groupes plus grands où les utilisateurs basculent vers une vue en action, qui a besoin de mises à jour dynamiques pour les répondeurs, vous pouvez continuer à ajouter jusqu’à 60 utilisateurs à la `userIds` liste. Vous pouvez supprimer le premier répondeur de la liste lorsque le 61e utilisateur répond. Pour les utilisateurs qui sont supprimés de la `userIds` liste, vous pouvez fournir un bouton d’actualisation manuelle ou utiliser le bouton Actualiser dans le menu des options de message pour obtenir le dernier résultat.
* Invitez les utilisateurs à obtenir un affichage spécifique à l’utilisateur, où ils ne voient qu’une vue particulière de la carte ou certaines actions.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Cartes adaptatives des flux de travail séquentiels | Montrez comment implémenter des flux de travail séquentiels, des vues spécifiques à l’utilisateur et des cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Affichages à jour](Up-To-Date-Views.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
