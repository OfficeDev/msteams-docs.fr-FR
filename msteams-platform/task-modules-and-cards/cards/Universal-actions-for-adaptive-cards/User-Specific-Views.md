---
title: Affichages spécifiques à l’utilisateur
description: Exemple d’affichages spécifiques à l’utilisateur à l’aide d’actions universelles
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: c24697b300d07ed53a172df162d0d3851361f579
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853514"
---
# <a name="user-specific-views"></a><span data-ttu-id="f5b19-103">Affichages spécifiques à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f5b19-103">User Specific Views</span></span>

<span data-ttu-id="f5b19-104">Auparavant, si des cartes adaptatives ont été envoyées dans Teams conversation, tous les utilisateurs voient exactement le même contenu de carte.</span><span class="sxs-lookup"><span data-stu-id="f5b19-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="f5b19-105">Avec l’introduction du modèle Actions universelles et des cartes adaptatives, les développeurs de bots peuvent désormais fournir des affichages spécifiques aux utilisateurs de cartes `refresh` adaptatives aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f5b19-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="f5b19-106">La même carte adaptative peut désormais être actualisée sur une carte adaptative spécifique à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f5b19-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span> <span data-ttu-id="f5b19-107">Un maximum de 60 utilisateurs différents peuvent voir une version différente de la carte avec des informations ou des actions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f5b19-107">Maximum 60 different users can see a different version of the card with additional information or actions.</span></span> <span data-ttu-id="f5b19-108">Cela fournit des scénarios puissants tels que les approbations, les contrôles de créateur de sondage, la gestion des tickets, la gestion des incidents et les cartes de gestion de projet.</span><span class="sxs-lookup"><span data-stu-id="f5b19-108">This provides powerful scenarios like approvals, poll creator controls, ticketing, incident management, and project management cards.</span></span>

<span data-ttu-id="f5b19-109">Par exemple, Megan, inspecteur de sécurité chez Contoso, souhaite créer un incident et l’affecter à Alex.</span><span class="sxs-lookup"><span data-stu-id="f5b19-109">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="f5b19-110">Elle souhaite également que tous les membres de l’équipe soient informés de l’incident.</span><span class="sxs-lookup"><span data-stu-id="f5b19-110">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="f5b19-111">Megan utilise l’extension de message de rapport d’incident Contoso optimisée par les actions universelles pour les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="f5b19-111">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

# <a name="mobile"></a>[<span data-ttu-id="f5b19-112">Mobile</span><span class="sxs-lookup"><span data-stu-id="f5b19-112">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Affichages spécifiques aux utilisateurs mobiles":::

# <a name="desktop"></a>[<span data-ttu-id="f5b19-114">Desktop</span><span class="sxs-lookup"><span data-stu-id="f5b19-114">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="f5b19-116">Affichages spécifiques à l’utilisateur pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="f5b19-116">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="f5b19-117">Le code suivant fournit un exemple de cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="f5b19-117">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="f5b19-118">**Pour envoyer des cartes adaptatives, actualisez les affichages spécifiques de l’utilisateur et invoquez des demandes au bot**</span><span class="sxs-lookup"><span data-stu-id="f5b19-118">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="f5b19-119">Lorsque Megan crée un incident, le bot envoie la carte adaptative ou la carte commune avec les détails de l’incident dans Teams conversation.</span><span class="sxs-lookup"><span data-stu-id="f5b19-119">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="f5b19-120">À présent, cette carte est automatiquement actualisée en vue spécifique de l’utilisateur pour Megan et Alex.</span><span class="sxs-lookup"><span data-stu-id="f5b19-120">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="f5b19-121">Les MRI utilisateur d’Alex et Megan sont ajoutés dans la propriété de propriété du JSON de `userIds` `refresh` carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="f5b19-121">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="f5b19-122">La carte reste la même pour les autres utilisateurs de la conversation.</span><span class="sxs-lookup"><span data-stu-id="f5b19-122">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="f5b19-123">Pour Megan, l’actualisation automatique déclenche une `adaptiveCard/action` demande d’appel au bot.</span><span class="sxs-lookup"><span data-stu-id="f5b19-123">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="f5b19-124">Le bot peut renvoyer une carte de créateur d’incident avec un bouton en réponse `Edit` à cette demande d’appel.</span><span class="sxs-lookup"><span data-stu-id="f5b19-124">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="f5b19-125">De même pour Alex, l’actualisation automatique déclenche une autre `adaptiveCard/action` demande d’appel au bot.</span><span class="sxs-lookup"><span data-stu-id="f5b19-125">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="f5b19-126">Le bot peut renvoyer un bouton de carte de propriétaire d’incident en réponse `Resolve` à cette demande d’appel.</span><span class="sxs-lookup"><span data-stu-id="f5b19-126">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="f5b19-127">Appeler la demande envoyée depuis Teams client au bot</span><span class="sxs-lookup"><span data-stu-id="f5b19-127">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="f5b19-128">Le code suivant fournit un exemple d’une demande d’appel envoyée par le client d’Alex Teams Megan au bot :</span><span class="sxs-lookup"><span data-stu-id="f5b19-128">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="f5b19-129">Carte de réponse d’appel adaptiveCard/action</span><span class="sxs-lookup"><span data-stu-id="f5b19-129">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="f5b19-130">Le code suivant fournit un exemple de carte de réponse d’appel adaptiveCard/action pour Megan :</span><span class="sxs-lookup"><span data-stu-id="f5b19-130">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="f5b19-131">Carte de réponse d’appel adaptiveCard/action pour Alex</span><span class="sxs-lookup"><span data-stu-id="f5b19-131">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="f5b19-132">Le code suivant fournit un exemple de carte de réponse d’appel adaptiveCard/action pour Alex :</span><span class="sxs-lookup"><span data-stu-id="f5b19-132">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="f5b19-133">Appeler la réponse pour renvoyer des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="f5b19-133">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="f5b19-134">Le code suivant fournit un exemple de réponse d’appel pour renvoyer des cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="f5b19-134">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="f5b19-135">Recommandations en matière de conception de carte à garder à l’esprit lors de la conception d’affichages spécifiques à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="f5b19-135">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="f5b19-136">Vous pouvez créer un maximum de **60 affichages** spécifiques à l’utilisateur pour une carte spécifique envoyée à une conversation ou un canal en spécifiant leur `userIds` dans la `refresh` section.</span><span class="sxs-lookup"><span data-stu-id="f5b19-136">You can create a maximum of **60 User Specific Views** for a particular card sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="f5b19-137">**Carte de base :** Version de base de la carte que le développeur du bot envoie à la conversation.</span><span class="sxs-lookup"><span data-stu-id="f5b19-137">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="f5b19-138">Il s’agit de la version de la carte adaptative pour tous les utilisateurs qui ne sont pas spécifiés dans la `userIds` section.</span><span class="sxs-lookup"><span data-stu-id="f5b19-138">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="f5b19-139">Une mise à jour de message peut être utilisée pour mettre à jour la carte de base et actualiser simultanément la carte spécifique de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f5b19-139">A message update can be used to update the base card and simultaneously refresh the User Specific Card.</span></span> <span data-ttu-id="f5b19-140">L’ouverture de la conversation ou du canal actualisera également la carte pour les utilisateurs avec l’actualisation activée.</span><span class="sxs-lookup"><span data-stu-id="f5b19-140">Opening the chat or channel also refreshes the card for users with refresh enabled.</span></span>
* <span data-ttu-id="f5b19-141">Pour les scénarios avec des groupes plus importants dans lesquels les utilisateurs basculent vers une vue d’action, qui nécessite des mises à jour dynamiques pour les répondeurs, vous pouvez continuer à ajouter jusqu’à 60 utilisateurs à la `userIds` liste.</span><span class="sxs-lookup"><span data-stu-id="f5b19-141">For scenarios with larger groups where users switch to a view on action, which needs dynamic updates for responders, you can keep adding up to 60 users to the `userIds` list.</span></span> <span data-ttu-id="f5b19-142">Vous pouvez supprimer le premier répondeur de la liste lorsque le 61e utilisateur répond.</span><span class="sxs-lookup"><span data-stu-id="f5b19-142">You can remove the first responder from the list when the 61st user responds.</span></span> <span data-ttu-id="f5b19-143">Pour les utilisateurs qui sont supprimés de la liste, vous pouvez fournir un bouton d’actualisation manuelle ou utiliser le bouton Actualiser dans le menu options du message pour obtenir le `userIds` dernier résultat.</span><span class="sxs-lookup"><span data-stu-id="f5b19-143">For the users who get removed from the `userIds` list, you can provide a manual refresh button or use the refresh button in the message options menu to get the latest result.</span></span>
* <span data-ttu-id="f5b19-144">Invitez les utilisateurs à obtenir un affichage spécifique de l’utilisateur, où ils voient uniquement un affichage particulier de la carte ou certaines actions.</span><span class="sxs-lookup"><span data-stu-id="f5b19-144">Give a prompt to users to get a User Specific View, where they see only a particular view of the card or some actions.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5b19-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f5b19-145">See also</span></span>

* [<span data-ttu-id="f5b19-146">Travailler avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="f5b19-146">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="f5b19-147">Affichages à jour</span><span class="sxs-lookup"><span data-stu-id="f5b19-147">Up to date views</span></span>](Up-To-Date-Views.md)
