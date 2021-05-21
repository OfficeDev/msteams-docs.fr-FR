---
title: Flux de travail séquentiels
description: Exemple de flux de travail séquentiels utilisant des actions universelles
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
# <a name="sequential-workflows"></a><span data-ttu-id="6fa6b-103">Flux de travail séquentiels</span><span class="sxs-lookup"><span data-stu-id="6fa6b-103">Sequential Workflows</span></span>

<span data-ttu-id="6fa6b-104">Les cartes adaptatives peuvent désormais prendre en charge les flux de travail séquentiels, c’est-à-dire lorsque les cartes adaptatives sont mises à jour lors de l’action de l’utilisateur et que l’utilisateur peut avancer dans une série de cartes qui nécessitent une entrée utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="6fa6b-105">Ceci est pris en charge par le biais de , qui permet aux développeurs de bot de retourner des `Action.Execute` cartes adaptatives en réponse à une action de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="6fa6b-106">Par exemple, prenez un scénario dans lequel la salle d’information souhaite prendre une commande pour une équipe ou un canal.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="6fa6b-107">Avec le choix de l’utilisateur pour divers éléments, tels que la cuisine, les `Action.Execute` cuisines, etc. peuvent être enregistrés séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="6fa6b-108">L’utilisateur peut également faire des allers-retours entre les cartes selon la logique définie par le développeur du bot.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="6fa6b-109">L’image suivante illustre le flux de travail séquentiel :</span><span class="sxs-lookup"><span data-stu-id="6fa6b-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="6fa6b-110">Un utilisateur peut avancer dans son flux de travail sans modifier la carte d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="6fa6b-111">Cela est également utile pour la conduite de questionnaires à l’aide de cartes adaptatives séquentielles.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="6fa6b-112">Comme illustré dans l’image suivante, différents utilisateurs peuvent se trouver à différentes étapes du flux de travail et ils voient différents états de la carte :</span><span class="sxs-lookup"><span data-stu-id="6fa6b-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration":::

> [!NOTE]
> <span data-ttu-id="6fa6b-114">Pour synchroniser la progression de l’utilisateur sur plusieurs appareils, utilisez la `refresh` propriété dans le JSON de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="6fa6b-115">Flux de travail séquentiel pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="6fa6b-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="6fa6b-116">Le code suivant fournit un exemple de cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="6fa6b-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="6fa6b-117">`Action.Execute`l’vot du bot peut renvoyer des cartes adaptatives en tant que réponse, ce qui remplace la carte existante dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="6fa6b-118">L’exemple suivant fournit ce que le bot renvoie lors de la sélection de la cuisine, de l’éros ou de la confirmation de commande :</span><span class="sxs-lookup"><span data-stu-id="6fa6b-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="6fa6b-119">Sur la sélection de la carte 1, le bot peut renvoyer une carte pour la sélection d’une carte de carte 2.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="6fa6b-120">Lors de la sélection à partir de la carte 2, le bot peut renvoyer une carte de confirmation de commande qui est la carte 3.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="6fa6b-121">Lors de la confirmation de commande à partir de la carte 3, le bot peut renvoyer une carte de commande confirmée qui est la carte 4.</span><span class="sxs-lookup"><span data-stu-id="6fa6b-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="6fa6b-122">Appeler la demande reçue côté bot</span><span class="sxs-lookup"><span data-stu-id="6fa6b-122">Invoke request received on bot side</span></span>

<span data-ttu-id="6fa6b-123">Le code suivant fournit un exemple de demande d’appel reçue côté bot :</span><span class="sxs-lookup"><span data-stu-id="6fa6b-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="6fa6b-124">Appeler la réponse pour renvoyer des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="6fa6b-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="6fa6b-125">Le code suivant fournit un exemple de réponse d’appel pour renvoyer des cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="6fa6b-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="6fa6b-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6fa6b-126">See also</span></span>

* [<span data-ttu-id="6fa6b-127">Actions de carte adaptative dans Teams</span><span class="sxs-lookup"><span data-stu-id="6fa6b-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="6fa6b-128">Comment fonctionnent les bots ?</span><span class="sxs-lookup"><span data-stu-id="6fa6b-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="6fa6b-129">Travailler avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="6fa6b-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
