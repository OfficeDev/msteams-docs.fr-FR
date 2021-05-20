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
# <a name="sequential-workflows"></a><span data-ttu-id="ae426-103">Flux de travail séquentiels</span><span class="sxs-lookup"><span data-stu-id="ae426-103">Sequential Workflows</span></span>

<span data-ttu-id="ae426-104">Les cartes adaptatives supportent désormais les workflows séquentiels, c’est-à-dire lorsque les cartes adaptatives sont mises à jour sur l’action de l’utilisateur et que l’utilisateur peut progresser à travers une série de cartes qui nécessitent l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ae426-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="ae426-105">Ceci est pris en charge par `Action.Execute` le biais , qui permet aux développeurs de bots de retourner les cartes adaptatives en réponse à une action de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ae426-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="ae426-106">Par exemple, prenez un scénario où la cafétéria veut prendre une commande pour une équipe ou un canal.</span><span class="sxs-lookup"><span data-stu-id="ae426-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="ae426-107">Avec `Action.Execute` le choix de l’utilisateur pour divers articles, tels que la nourriture, les boissons, et ainsi de suite peut être enregistré séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="ae426-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="ae426-108">L’utilisateur peut également aller et venir à travers les cartes selon la logique définie par le développeur de bot.</span><span class="sxs-lookup"><span data-stu-id="ae426-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="ae426-109">L’image suivante affiche le flux de travail séquentiel :</span><span class="sxs-lookup"><span data-stu-id="ae426-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="ae426-110">Un utilisateur peut progresser dans son flux de travail sans modifier la carte pour les autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ae426-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="ae426-111">Ceci est également utile pour effectuer des quiz à l’aide de cartes adaptatives séquentielles.</span><span class="sxs-lookup"><span data-stu-id="ae426-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="ae426-112">Comme indiqué dans l’image suivante, différents utilisateurs peuvent être à différents stades du flux de travail et ils voient différents états de la carte:</span><span class="sxs-lookup"><span data-stu-id="ae426-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États bot traiteur":::

> [!NOTE]
> <span data-ttu-id="ae426-114">Afin de synchroniser les progrès de l’utilisateur entre les appareils, utilisez la `refresh` propriété dans Adaptive Card JSON.</span><span class="sxs-lookup"><span data-stu-id="ae426-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="ae426-115">Flux de travail séquentiel pour cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="ae426-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="ae426-116">Le code suivant fournit un exemple de cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="ae426-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="ae426-117">`Action.Execute`invoquant le bot peut retourner les cartes adaptatives comme une réponse, qui remplace la carte existante dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ae426-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="ae426-118">L’exemple suivant fournit ce que le bot retourne sur la sélection des aliments ou des boissons ou la confirmation de commande:</span><span class="sxs-lookup"><span data-stu-id="ae426-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="ae426-119">Sur la sélection des aliments de la carte 1, bot peut retourner une carte pour la sélection des boissons qui est la carte 2.</span><span class="sxs-lookup"><span data-stu-id="ae426-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="ae426-120">Lors de la sélection des boissons de la carte 2, bot peut retourner une carte de confirmation de commande qui est la carte 3.</span><span class="sxs-lookup"><span data-stu-id="ae426-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="ae426-121">Sur commande confirmation de la carte 3, bot peut retourner une carte confirmée de commande qui est la carte 4.</span><span class="sxs-lookup"><span data-stu-id="ae426-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="ae426-122">Invoquer la demande reçue du côté bot</span><span class="sxs-lookup"><span data-stu-id="ae426-122">Invoke request received on bot side</span></span>

<span data-ttu-id="ae426-123">Le code suivant fournit un exemple d’une demande d’invocer reçue du côté bot :</span><span class="sxs-lookup"><span data-stu-id="ae426-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="ae426-124">Invoquer la réponse pour retourner les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="ae426-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="ae426-125">Le code suivant fournit un exemple de réponse invocative pour renvoyer les cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="ae426-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ae426-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ae426-126">See also</span></span>

* [<span data-ttu-id="ae426-127">Actions de carte adaptative en Teams</span><span class="sxs-lookup"><span data-stu-id="ae426-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="ae426-128">Comment fonctionnent les bots ?</span><span class="sxs-lookup"><span data-stu-id="ae426-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="ae426-129">Travailler avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="ae426-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
