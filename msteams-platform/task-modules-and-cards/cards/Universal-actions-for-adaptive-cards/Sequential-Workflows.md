---
title: Flux de travail séquentiels
description: Exemple de flux de travail séquentiels utilisant des actions universelles
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: c3065080a0a470104fa2b7c06c9b0c8105a829a6
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155721"
---
# <a name="sequential-workflows"></a>Flux de travail séquentiels

Les cartes adaptatives peuvent désormais prendre en charge les flux de travail séquentiels qui sont mis à jour lors de l’action de l’utilisateur. À l’aide des flux de travail séquentiels, les cartes adaptatives sont mises à jour sur l’action de l’utilisateur et l’utilisateur peut avancer dans une série de cartes qui nécessitent une entrée utilisateur. `Action.Execute` prend en charge les flux de travail séquentiels, qui permettent aux développeurs de bots de retourner des cartes adaptatives en réponse à une action de l’utilisateur.

Par exemple, prenez un scénario dans lequel la salle d’information souhaite prendre une commande pour une équipe ou un canal. Avec le choix de l’utilisateur pour divers éléments, tels que des alimentations et des `Action.Execute` cuisines, peuvent être enregistrés séquentiellement. L’utilisateur peut également faire des allers-retours entre les cartes selon la logique définie par le développeur du bot. <br/>

L’image suivante illustre le flux de travail séquentiel :

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un utilisateur peut avancer dans son flux de travail sans modifier la carte d’autres utilisateurs. Le flux de travail est également utile pour la conduite de questionnaires à l’aide de cartes adaptatives séquentielles. L’image suivante montre que différents utilisateurs peuvent se trouver à différentes étapes du flux de travail et aux états de la carte :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration":::

> [!NOTE]
> Pour synchroniser la progression de l’utilisateur sur plusieurs appareils, utilisez la `refresh` propriété dans le JSON de carte adaptative.

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

`Action.Execute`l’vot du bot peut renvoyer des cartes adaptatives en tant que réponse, ce qui remplace la carte existante dans Teams.
L’exemple suivant fournit ce que le bot renvoie lors de la sélection de la cuisine, de l’éros ou de la confirmation de commande :

* Sur la sélection de la carte 1, le bot peut renvoyer une carte pour la sélection d’une carte de carte 2.
* Lors de la sélection à partir de la carte 2, le bot peut renvoyer une carte de confirmation de commande qui est la carte 3.
* Lors de la confirmation de commande à partir de la carte 3, le bot peut renvoyer une carte de commande confirmée qui est la carte 4.

## <a name="invoke-request-received-on-bot-side"></a>Appeler la demande reçue côté bot

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

## <a name="code-samples"></a>Exemples de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams bot de restauration | Créez un bot qui accepte l’ordre des produits à l’aide de cartes adaptatives. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| N’est pas encore disponible. |
| Cartes adaptatives de flux de travail séquentiels | Montrer comment implémenter des flux de travail séquentiels, des affichages spécifiques de l’utilisateur et des cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |


## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
