---
title: Affichages spécifiques à l’utilisateur
description: Exemple pour les vues spécifiques des utilisateurs à l’aide d’actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 696fc5ce25c79d749b301309bfe0c737e39ad294
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555443"
---
# <a name="user-specific-views"></a><span data-ttu-id="38a92-103">Affichages spécifiques à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="38a92-103">User Specific Views</span></span>

<span data-ttu-id="38a92-104">Plus tôt, si adaptive cards a été envoyé dans Teams conversation, tous les utilisateurs voient exactement le même contenu de carte.</span><span class="sxs-lookup"><span data-stu-id="38a92-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="38a92-105">Avec l’introduction du modèle Actions Universelles et des cartes `refresh` adaptatives, les développeurs de bots peuvent désormais fournir aux utilisateurs des vues spécifiques des cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="38a92-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="38a92-106">La même carte adaptative peut maintenant se rafraîchir à une carte adaptative spécifique à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="38a92-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span>

<span data-ttu-id="38a92-107">Par exemple, Megan, inspectrice de sécurité chez Contoso, veut créer un incident et l’assigner à Alex.</span><span class="sxs-lookup"><span data-stu-id="38a92-107">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="38a92-108">Elle veut aussi que tous les membres de l’équipe soient au courant de l’incident.</span><span class="sxs-lookup"><span data-stu-id="38a92-108">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="38a92-109">Megan utilise l’extension de message de rapport d’incident Contoso alimentée par Universal Actions for Adaptive Cards.</span><span class="sxs-lookup"><span data-stu-id="38a92-109">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur":::

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="38a92-111">Vues spécifiques de l’utilisateur pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="38a92-111">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="38a92-112">Le code suivant fournit un exemple de cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="38a92-112">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="38a92-113">**Pour envoyer des cartes adaptatives, actualisez les vues spécifiques de l’utilisateur et invoquez les demandes au bot**</span><span class="sxs-lookup"><span data-stu-id="38a92-113">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="38a92-114">Lorsque Megan crée un nouvel incident, le bot envoie la carte adaptative ou la carte commune avec les détails de l’incident dans Teams conversation.</span><span class="sxs-lookup"><span data-stu-id="38a92-114">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="38a92-115">Maintenant, cette carte se rafraîchit automatiquement à l’utilisateur vue spécifique pour Megan et Alex.</span><span class="sxs-lookup"><span data-stu-id="38a92-115">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="38a92-116">Les IRM utilisateur d’Alex et Megan sont ajoutées dans la `userIds` propriété de la carte `refresh` adaptative JSON.</span><span class="sxs-lookup"><span data-stu-id="38a92-116">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="38a92-117">La carte reste la même pour les autres utilisateurs de la conversation.</span><span class="sxs-lookup"><span data-stu-id="38a92-117">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="38a92-118">Pour Megan, la mise à jour automatique déclenche une demande `adaptiveCard/action` d’invocisation au bot.</span><span class="sxs-lookup"><span data-stu-id="38a92-118">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="38a92-119">Le bot peut retourner une carte de créateur d’incident avec `Edit` bouton en réponse à cette demande d’invocateur.</span><span class="sxs-lookup"><span data-stu-id="38a92-119">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="38a92-120">De même pour Alex, la mise à jour automatique déclenche une autre `adaptiveCard/action` demande d’invocisation au bot.</span><span class="sxs-lookup"><span data-stu-id="38a92-120">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="38a92-121">Le bot peut retourner un bouton de carte propriétaire incident `Resolve` comme une réponse à cette demande d’invocateur.</span><span class="sxs-lookup"><span data-stu-id="38a92-121">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="38a92-122">Invoquer la demande envoyée Teams client au bot</span><span class="sxs-lookup"><span data-stu-id="38a92-122">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="38a92-123">Le code suivant fournit un exemple d’une demande d’invocer envoyée par alex et megan Teams client au bot:</span><span class="sxs-lookup"><span data-stu-id="38a92-123">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="38a92-124">adaptiveCard/action invoquent la carte de réponse</span><span class="sxs-lookup"><span data-stu-id="38a92-124">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="38a92-125">Le code suivant fournit un exemple d’une carte adaptative / action invoquer carte de réponse pour Megan:</span><span class="sxs-lookup"><span data-stu-id="38a92-125">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="38a92-126">adaptiveCard/action invoquent la carte de réponse pour Alex</span><span class="sxs-lookup"><span data-stu-id="38a92-126">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="38a92-127">Le code suivant fournit un exemple de carte adaptative/action invoquer la carte de réponse pour Alex:</span><span class="sxs-lookup"><span data-stu-id="38a92-127">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="38a92-128">Invoquer la réponse pour retourner les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="38a92-128">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="38a92-129">Le code suivant fournit un exemple de réponse invocative pour renvoyer les cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="38a92-129">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="38a92-130">Lignes directrices de conception de cartes à garder à l’esprit lors de la conception de vues spécifiques à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="38a92-130">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="38a92-131">Vous pouvez créer un maximum de **60 vues spécifiques à l’utilisateur** pour une carte particulière envoyée à un chat ou un canal en spécifier `userIds` leur dans la `refresh` section.</span><span class="sxs-lookup"><span data-stu-id="38a92-131">You can create a maximum of **60 User Specific Views** for a particular card being sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="38a92-132">**Carte de base:** La version de base de la carte que le développeur de bot envoie au chat.</span><span class="sxs-lookup"><span data-stu-id="38a92-132">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="38a92-133">Il s’agit de la version de la carte adaptative pour tous les utilisateurs qui ne sont pas spécifiés dans `userIds` la section.</span><span class="sxs-lookup"><span data-stu-id="38a92-133">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="38a92-134">Une mise à jour ou une modification de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="38a92-134">A message update or edit can be used to update the base card and simultaneously refresh the User Specific Card.</span></span>

## <a name="see-also"></a><span data-ttu-id="38a92-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="38a92-135">See also</span></span>

* [<span data-ttu-id="38a92-136">Travailler avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="38a92-136">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="38a92-137">Vues à jour</span><span class="sxs-lookup"><span data-stu-id="38a92-137">Up to date views</span></span>](Up-To-Date-Views.md)
