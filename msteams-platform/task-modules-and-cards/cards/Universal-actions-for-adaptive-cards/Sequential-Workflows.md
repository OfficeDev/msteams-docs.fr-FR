---
title: Flux de travail séquentiels
description: Exemple de flux de travail séquentiels utilisant des actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: f36e65133572569cd01de1053044336c810656f3
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649644"
---
# <a name="sequential-workflows"></a>Flux de travail séquentiels

Les cartes adaptatives peuvent désormais prendre en charge les flux de travail séquentiels, c’est-à-dire lorsque les cartes adaptatives sont mises à jour lors de l’action de l’utilisateur et que l’utilisateur peut avancer dans une série de cartes qui nécessitent une entrée utilisateur. Ceci est pris en charge par le biais de , qui permet aux développeurs de bot de retourner des `Action.Execute` cartes adaptatives en réponse à une action de l’utilisateur.

Par exemple, prenez un scénario dans lequel la salle d’information souhaite prendre une commande pour une équipe ou un canal. Avec le choix de l’utilisateur pour divers éléments, tels que la cuisine, les `Action.Execute` cuisines, etc. peuvent être enregistrés séquentiellement. L’utilisateur peut également faire des allers-retours entre les cartes selon la logique définie par le développeur du bot. <br/>

L’image suivante illustre le flux de travail séquentiel :

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un utilisateur peut avancer dans son flux de travail sans modifier la carte d’autres utilisateurs. Cela est également utile pour la conduite de questionnaires à l’aide de cartes adaptatives séquentielles. Comme illustré dans l’image suivante, différents utilisateurs peuvent se trouver à différentes étapes du flux de travail et ils voient différents états de la carte :

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

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore |
|----------------|-----------------|--------------|
| Teams bot de restauration | Créez un bot simple qui accepte la commande de la restauration à l’aide de cartes adaptatives. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
