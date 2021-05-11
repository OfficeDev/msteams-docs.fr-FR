---
title: Affichages spécifiques à l'utilisateur
description: Exemple d'affichages spécifiques à l'utilisateur à l'aide d'actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 984b32511dda544942df11f7c5d8a25cca8e9a8a
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088836"
---
# <a name="user-specific-views"></a><span data-ttu-id="25923-103">Affichages spécifiques à l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="25923-103">User Specific Views</span></span>

<span data-ttu-id="25923-104">Auparavant, si des cartes adaptatives ont été envoyées dans Teams conversation, tous les utilisateurs voient exactement le même contenu de carte.</span><span class="sxs-lookup"><span data-stu-id="25923-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="25923-105">Avec l'introduction du modèle Actions universelles et des cartes adaptatives, les développeurs de bots peuvent désormais fournir des affichages spécifiques aux utilisateurs de cartes `refresh` adaptatives aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="25923-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="25923-106">La même carte adaptative peut désormais être actualisée sur une carte adaptative spécifique à l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="25923-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span>

<span data-ttu-id="25923-107">Par exemple, Megan, inspecteur de sécurité chez Contoso, souhaite créer un incident et l'affecter à Alex.</span><span class="sxs-lookup"><span data-stu-id="25923-107">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="25923-108">Elle souhaite également que tous les membres de l'équipe soient informés de l'incident.</span><span class="sxs-lookup"><span data-stu-id="25923-108">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="25923-109">Megan utilise l'extension de message de rapport d'incident Contoso optimisée par les actions universelles pour les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="25923-109">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l'utilisateur":::

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="25923-111">Affichages spécifiques à l'utilisateur pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="25923-111">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="25923-112">Le code suivant fournit un exemple de cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="25923-112">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="25923-113">**Pour envoyer des cartes adaptatives, actualisez les affichages spécifiques de l'utilisateur et invoquez des demandes au bot**</span><span class="sxs-lookup"><span data-stu-id="25923-113">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="25923-114">Lorsque Megan crée un incident, le bot envoie la carte adaptative ou la carte commune avec les détails de l'incident dans Teams conversation.</span><span class="sxs-lookup"><span data-stu-id="25923-114">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="25923-115">À présent, cette carte est automatiquement actualisée en vue spécifique de l'utilisateur pour Megan et Alex.</span><span class="sxs-lookup"><span data-stu-id="25923-115">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="25923-116">Les MRI utilisateur d'Alex et Megan sont ajoutés dans la propriété de propriété du JSON de `userIds` `refresh` carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="25923-116">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="25923-117">La carte reste la même pour les autres utilisateurs de la conversation.</span><span class="sxs-lookup"><span data-stu-id="25923-117">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="25923-118">Pour Megan, l'actualisation automatique déclenche une `adaptiveCard/action` demande d'appel au bot.</span><span class="sxs-lookup"><span data-stu-id="25923-118">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="25923-119">Le bot peut renvoyer une carte de créateur d'incident avec un bouton en réponse `Edit` à cette demande d'appel.</span><span class="sxs-lookup"><span data-stu-id="25923-119">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="25923-120">De même pour Alex, l'actualisation automatique déclenche une autre `adaptiveCard/action` demande d'appel au bot.</span><span class="sxs-lookup"><span data-stu-id="25923-120">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="25923-121">Le bot peut renvoyer un bouton de carte de propriétaire d'incident en réponse `Resolve` à cette demande d'appel.</span><span class="sxs-lookup"><span data-stu-id="25923-121">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="25923-122">Appeler la demande envoyée depuis Teams client au bot</span><span class="sxs-lookup"><span data-stu-id="25923-122">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="25923-123">Le code suivant fournit un exemple d'une demande d'appel envoyée par le client d'Alex Teams Megan au bot :</span><span class="sxs-lookup"><span data-stu-id="25923-123">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="25923-124">Carte de réponse d'appel adaptiveCard/action</span><span class="sxs-lookup"><span data-stu-id="25923-124">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="25923-125">Le code suivant fournit un exemple de carte de réponse d'appel adaptiveCard/action pour Megan :</span><span class="sxs-lookup"><span data-stu-id="25923-125">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="25923-126">Carte de réponse d'appel adaptiveCard/action pour Alex</span><span class="sxs-lookup"><span data-stu-id="25923-126">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="25923-127">Le code suivant fournit un exemple de carte de réponse d'appel adaptiveCard/action pour Alex :</span><span class="sxs-lookup"><span data-stu-id="25923-127">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="25923-128">Appeler la réponse pour renvoyer des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="25923-128">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="25923-129">Le code suivant fournit un exemple de réponse d'appel pour renvoyer des cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="25923-129">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.card.adaptive",
    value = card
 });
```

<span data-ttu-id="25923-130">Recommandations en matière de conception de carte à garder à l'esprit lors de la conception d'affichages spécifiques à l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="25923-130">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="25923-131">Vous pouvez créer un maximum de **60 affichages** spécifiques à l'utilisateur pour une carte particulière envoyée à une conversation ou un canal en spécifiant leur dans `userIds` la `refresh` section.</span><span class="sxs-lookup"><span data-stu-id="25923-131">You can create a maximum of **60 User Specific Views** for a particular card being sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="25923-132">**Carte de base :** Version de base de la carte que le développeur du bot envoie à la conversation.</span><span class="sxs-lookup"><span data-stu-id="25923-132">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="25923-133">Il s'agit de la version de la carte adaptative pour tous les utilisateurs qui ne sont pas spécifiés dans la `userIds` section.</span><span class="sxs-lookup"><span data-stu-id="25923-133">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="25923-134">Une mise à jour ou une modification de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="25923-134">A message update or edit can be used to update the base card and simultaneously refresh the User Specific Card.</span></span>

## <a name="see-also"></a><span data-ttu-id="25923-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="25923-135">See also</span></span>

* [<span data-ttu-id="25923-136">Travailler avec des actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="25923-136">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="25923-137">Affichages à jour</span><span class="sxs-lookup"><span data-stu-id="25923-137">Up to date views</span></span>](Up-To-Date-Views.md)