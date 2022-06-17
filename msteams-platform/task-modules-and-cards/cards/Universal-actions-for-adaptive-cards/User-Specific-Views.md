---
title: Affichages spécifiques à l’utilisateur
description: Dans ce module, découvrez les vues spécifiques à l’utilisateur à l’aide d’actions universelles avec l’exemple de code et la carte de réponse adaptiveCard/action invoke
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: a3fdc937ba1528a2bf9aa304bf484bbcae68b5c6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143920"
---
# <a name="user-specific-views"></a>Affichages spécifiques à l’utilisateur

Plus tôt, si les cartes adaptatives étaient envoyées dans une conversation Teams, tous les utilisateurs verraient exactement le même contenu de carte. Avec l’introduction du modèle Actions universelles et `refresh` des cartes adaptatives, les développeurs de bots peuvent désormais fournir aux utilisateurs des vues spécifiques aux utilisateurs des cartes adaptatives. La même carte adaptative peut désormais être actualisée pour une carte adaptative spécifique à l’utilisateur. La carte adaptative fournit des scénarios puissants tels que les approbations, les contrôles de créateur de sondage, la création de tickets, la gestion des incidents et les cartes de gestion de projet.

> [!NOTE]
>
> * La vue spécifique à l’utilisateur est prise en charge pour les cartes adaptatives envoyées par un bot et dépend des actions universelles.
> * Au maximum 60 utilisateurs différents peuvent voir une version différente de la carte avec des informations ou des actions supplémentaires.

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

La liste suivante fournit des instructions de conception de carte pour les vues spécifiques à l’utilisateur :

* Comportement d’actualisation : vous pouvez créer un maximum de 60 vues spécifiques à l’utilisateur pour une carte particulière envoyée à une conversation en spécifiant leur `userIds` valeur dans la `Refresh` propriété.

  * Si le `userIds` champ n’est pas spécifié dans la `Refresh` propriété, Teams client peut déclencher automatiquement l’actualisation pour tous les utilisateurs lorsqu’il y a moins ou égal à 60 membres dans la conversation.

  * Pour que les utilisateurs déclenchent manuellement l’actualisation de la carte, ils peuvent sélectionner **Actualiser** dans le menu des options de message. Cela se produit pour tous les utilisateurs lorsqu’il y a moins de 60 membres dans une conversation, ou pour l’ensemble d’utilisateurs non spécifiés dans la `userIds` liste lorsqu’il y a tous ou moins de 60 utilisateurs dans une conversation.

* Carte de base : le bot envoie le message, qui est incorporé avec la version de base de la carte. Tous les membres de la conversation peuvent afficher la même chose. Par la suite, le bot extrait la carte spécifique à l’utilisateur via l’actualisation pour les utilisateurs spécifiés dans la `userIds` section.

* Délai d’expiration de l’actualisation : Teams client déclenche une actualisation de deux manières, par le biais de **l’option Actualiser** ou en sélectionnant **Exécuter**. L’actualisation se déclenche uniquement si la carte du dernier appel est antérieure à une minute. Vous pouvez contrôler le comportement d’actualisation en ajoutant un horodatage au conteneur de données et en le vérifiant avant d’envoyer la carte actualisée.

* Une mise à jour de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique à l’utilisateur. L’ouverture de la conversation ou du canal actualise également la carte pour les utilisateurs avec **l’option Actualiser** activée.

* Pour les scénarios avec des groupes plus grands où les utilisateurs basculent vers une vue en action, qui a besoin de mises à jour dynamiques pour les répondeurs, vous pouvez continuer à ajouter jusqu’à 60 utilisateurs à la `userIds` liste. Vous pouvez supprimer le premier répondeur de la liste lorsque le 61e utilisateur répond. Pour les utilisateurs qui sont supprimés de la `userIds` liste, vous pouvez fournir une **actualisation** manuelle pour obtenir le dernier résultat.

* Invitez les utilisateurs à obtenir un affichage spécifique à l’utilisateur, où ils ne voient qu’une vue particulière de la carte ou certaines actions.

> [!NOTE]
> La carte spécifique à l’utilisateur retournée par le bot est envoyée uniquement au client spécifique qui l’a demandée. Par exemple, si un utilisateur bascule vers un autre client, par exemple de bureau en mobile, un autre événement d’appel est déclenché pour extraire la carte actualisée.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Flux de travail séquentiels Cartes adaptatives | Montrez comment implémenter des flux de travail séquentiels, des vues spécifiques à l’utilisateur et des Cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Affichages à jour](Up-To-Date-Views.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
