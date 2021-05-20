---
title: Flux de travail séquentiels
description: Exemple pour les workflows séquentiels utilisant des actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 7f285bf76aac4f0ca276321aee2ce4b4e5c3e7e4
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555401"
---
# <a name="sequential-workflows"></a>Flux de travail séquentiels

Les cartes adaptatives supportent désormais les workflows séquentiels, c’est-à-dire lorsque les cartes adaptatives sont mises à jour sur l’action de l’utilisateur et que l’utilisateur peut progresser à travers une série de cartes qui nécessitent l’entrée de l’utilisateur. Ceci est pris en charge par `Action.Execute` le biais , qui permet aux développeurs de bots de retourner les cartes adaptatives en réponse à une action de l’utilisateur.

Par exemple, prenez un scénario où la cafétéria veut prendre une commande pour une équipe ou un canal. Avec `Action.Execute` le choix de l’utilisateur pour divers articles, tels que la nourriture, les boissons, et ainsi de suite peut être enregistré séquentiellement. L’utilisateur peut également aller et venir à travers les cartes selon la logique définie par le développeur de bot. <br/>

L’image suivante affiche le flux de travail séquentiel :

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un utilisateur peut progresser dans son flux de travail sans modifier la carte pour les autres utilisateurs. Ceci est également utile pour effectuer des quiz à l’aide de cartes adaptatives séquentielles. Comme indiqué dans l’image suivante, différents utilisateurs peuvent être à différents stades du flux de travail et ils voient différents états de la carte:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États bot traiteur":::

> [!NOTE]
> Afin de synchroniser les progrès de l’utilisateur entre les appareils, utilisez la `refresh` propriété dans Adaptive Card JSON.

## <a name="sequential-workflow-for-adaptive-cards"></a>Flux de travail séquentiel pour cartes adaptatives

Le code suivant fournit un exemple de cartes adaptatives :

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Select from food options"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Chicken",
          "verb": "food",
          "data": {
              "item": "chicken"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Beef",
          "verb": "food",
          "data": {
              "item": "beef"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Vegan",
          "verb": "food",
          "data": {
              "item": "vegan"
          }
        }
      ]
    }
  ]
}
```

`Action.Execute`invoquant le bot peut retourner les cartes adaptatives comme une réponse, qui remplace la carte existante dans Teams.
L’exemple suivant fournit ce que le bot retourne sur la sélection des aliments ou des boissons ou la confirmation de commande:

* Sur la sélection des aliments de la carte 1, bot peut retourner une carte pour la sélection des boissons qui est la carte 2.
* Lors de la sélection des boissons de la carte 2, bot peut retourner une carte de confirmation de commande qui est la carte 3.
* Sur commande confirmation de la carte 3, bot peut retourner une carte confirmée de commande qui est la carte 4.

## <a name="invoke-request-received-on-bot-side"></a>Invoquer la demande reçue du côté bot

Le code suivant fournit un exemple d’une demande d’invocer reçue du côté bot :

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "food",
      "data": { 
            "item": "vegan"
      } 
    },
    "trigger": "manual" 
  }
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

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative en Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
