---
title: Flux de travail séquentiels
description: Dans ce module, découvrez les flux de travail séquentiels pour les cartes adaptatives à l’aide d’actions universelles avec des exemples de code
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: bd3fbf560099487ba45c2454460b82b852b675fa
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833190"
---
# <a name="sequential-workflows"></a>Flux de travail séquentiels

Les cartes adaptatives prennent désormais en charge les flux de travail séquentiels qui sont mis à jour en fonction de l’action de l’utilisateur. À l’aide de flux de travail séquentiels, les cartes adaptatives sont mises à jour sur l’action de l’utilisateur et l’utilisateur peut passer à une série de cartes qui nécessitent une entrée utilisateur. `Action.Execute` prend en charge les flux de travail séquentiels, ce qui permet aux développeurs de bots de retourner des cartes adaptatives en réponse à une action de l’utilisateur.

Par exemple, prenons un scénario où la cafétéria souhaite prendre une commande pour une équipe ou un canal. Avec `Action.Execute` le choix de l’utilisateur pour divers éléments, tels que les aliments et les boissons peuvent être enregistrés séquentiellement. L’utilisateur peut également parcourir les cartes selon la logique définie par le développeur du bot. <br/>

L’image suivante montre le flux de travail séquentiel :

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un utilisateur peut progresser dans son workflow sans modifier la carte pour d’autres utilisateurs. Le flux de travail est également utile pour effectuer des questionnaires à l’aide de cartes adaptatives séquentielles. L’image suivante montre que différents utilisateurs peuvent se trouver à différentes étapes du flux de travail et des états de la carte :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> Pour synchroniser la progression de l’utilisateur entre les appareils, utilisez la `refresh` propriété dans la carte adaptative JSON.

## <a name="sequential-workflow-for-adaptive-cards"></a>Flux de travail séquentiel pour les cartes adaptatives

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

`Action.Execute` l’appel du bot peut retourner des cartes adaptatives en tant que réponse, ce qui remplace la carte existante dans Teams.
L’exemple suivant fournit ce que le bot retourne lors de la sélection d’aliments ou de boissons ou de la confirmation de commande :

* Sur la sélection d’aliments à partir de la carte 1, le bot peut retourner une carte pour la sélection des boissons qui est carte 2.
* Lors de la sélection de boisson à partir de la carte 2, le bot peut retourner une carte de confirmation de commande qui est la carte 3.
* Sur la confirmation de commande de la carte 3, le bot peut retourner une carte de commande confirmée qui est la carte 4.

## <a name="invoke-request-received-on-bot-side"></a>Demande d’appel reçue côté bot

Le code suivant fournit un exemple de demande d’appel reçue côté bot :

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Appeler la réponse pour retourner des cartes adaptatives

Le code suivant fournit un exemple de réponse d’appel pour retourner des cartes adaptatives :

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

## <a name="code-samples"></a>Exemples de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Bot de traiteur Teams | Créez un bot qui accepte la commande de nourriture à l’aide de Cartes adaptatives. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| N/A |
| Flux de travail séquentiels Cartes adaptatives | Montrez comment implémenter des flux de travail séquentiels, des vues spécifiques à l’utilisateur et des Cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
