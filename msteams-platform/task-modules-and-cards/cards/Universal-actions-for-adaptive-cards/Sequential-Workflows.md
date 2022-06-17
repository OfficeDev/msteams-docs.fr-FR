---
title: Flux de travail séquentiels
description: Dans ce module, découvrez les flux de travail séquentiels pour les cartes adaptatives à l’aide d’actions universelles avec des exemples de code
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 40743ccd67386aae72685536ede1ae50d5aea907
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143311"
---
# <a name="sequential-workflows"></a>Flux de travail séquentiels

Les cartes adaptatives prennent désormais en charge les flux de travail séquentiels mis à jour lors de l’action de l’utilisateur. À l’aide de flux de travail séquentiels, les cartes adaptatives sont mises à jour sur l’action de l’utilisateur et l’utilisateur peut passer par une série de cartes qui nécessitent une entrée utilisateur. `Action.Execute` prend en charge les flux de travail séquentiels, qui permettent aux développeurs de bots de retourner des cartes adaptatives en réponse à une action de l’utilisateur.

Par exemple, prenez un scénario où la cafétéria souhaite prendre une commande pour une équipe ou un canal. Avec `Action.Execute` le choix de l’utilisateur pour différents éléments, tels que les aliments et les boissons peuvent être enregistrés séquentiellement. L’utilisateur peut également parcourir les cartes en fonction de la logique définie par le développeur du bot. <br/>

L’image suivante montre le flux de travail séquentiel :

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Un utilisateur peut progresser dans son flux de travail sans modifier la carte pour d’autres utilisateurs. Le flux de travail est également utile pour effectuer des questionnaires à l’aide de cartes adaptatives séquentielles. L’image suivante montre que différents utilisateurs peuvent se trouver à différentes étapes du flux de travail et des états de la carte :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> Pour synchroniser la progression de l’utilisateur sur les appareils, utilisez la `refresh` propriété dans le code JSON de carte adaptative.

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

`Action.Execute`L’appel du bot peut retourner des cartes adaptatives en tant que réponse, ce qui remplace la carte existante dans Teams.
L’exemple suivant fournit ce que le bot retourne en cas de sélection d’aliments ou de boissons ou de confirmation de commande :

* Sur la sélection de nourriture de la carte 1, bot peut retourner une carte pour la sélection de boissons qui est la carte 2.
* Sur la sélection de boissons de la carte 2, bot peut retourner une carte de confirmation de commande qui est la carte 3.
* Lors de la confirmation de commande à partir de la carte 3, le bot peut retourner une carte confirmée de commande qui est la carte 4.

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
| Bot de traiteur Teams | Créez un bot qui accepte la commande de nourriture à l’aide de Cartes adaptatives. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| N’est pas encore disponible. |
| Flux de travail séquentiels Cartes adaptatives | Montrez comment implémenter des flux de travail séquentiels, des vues spécifiques à l’utilisateur et des Cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
