---
title: Affichages à jour
description: Exemple d’affichages à jour à l’aide du bot universel
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088843"
---
# <a name="up-to-date-cards"></a><span data-ttu-id="ee686-103">Cartes actualisées</span><span class="sxs-lookup"><span data-stu-id="ee686-103">Up to date cards</span></span>

<span data-ttu-id="ee686-104">Vous pouvez désormais fournir les dernières informations à vos utilisateurs sur les cartes adaptatives avec une combinaison de modifications d’actualisation et de message Teams.</span><span class="sxs-lookup"><span data-stu-id="ee686-104">You can now provide latest information to your users on Adaptive Cards with a combination of refresh and message edits in Teams.</span></span> <span data-ttu-id="ee686-105">Ainsi, vous pouvez mettre à jour dynamiquement les affichages spécifiques de l’utilisateur à leur état le plus récent en cas de modification de votre service.</span><span class="sxs-lookup"><span data-stu-id="ee686-105">With this you are able to update the User Specific Views dynamically to its latest state as and when there is a change on your service.</span></span> <span data-ttu-id="ee686-106">Par exemple, dans le cas de cartes de gestion de projet ou de tickets, vous pouvez mettre à jour les commentaires et l’état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="ee686-106">For example, in the case of project management or ticketing cards, you can update comments and the status of the task.</span></span> <span data-ttu-id="ee686-107">En cas d’approbation, le dernier état est reflété tout en fournissant des informations et des actions différenciées.</span><span class="sxs-lookup"><span data-stu-id="ee686-107">In case of approvals the latest state is reflected while also providing differentiated information and actions.</span></span>

<span data-ttu-id="ee686-108">Par exemple, un utilisateur peut créer une demande d’approbation de biens dans Teams conversation.</span><span class="sxs-lookup"><span data-stu-id="ee686-108">For example, a user can create an asset approval request in a Teams conversation.</span></span> <span data-ttu-id="ee686-109">Alex crée une demande d’approbation et l’affecte à Megan et Nestor.</span><span class="sxs-lookup"><span data-stu-id="ee686-109">Alex creates an approval request and assigns it to Megan and Nestor.</span></span> <span data-ttu-id="ee686-110">Voici les deux parties pour créer la demande d’approbation :</span><span class="sxs-lookup"><span data-stu-id="ee686-110">The following are the two parts to create the approval request:</span></span>

* <span data-ttu-id="ee686-111">Les vues spécifiques à l’utilisateur peuvent être exploitées à `refresh` l’aide de la propriété des cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="ee686-111">User Specific Views can be leveraged using the `refresh` property of the Adaptive Cards.</span></span>
<span data-ttu-id="ee686-112">À l’aide des affichages  spécifiques de l’utilisateur, vous pouvez afficher une carte avec des boutons Approuver ou Rejeter à un ensemble d’utilisateurs et afficher une carte sans ces boutons à d’autres utilisateurs. </span><span class="sxs-lookup"><span data-stu-id="ee686-112">Using User Specific Views one can show a card with **Approve** or **Reject** buttons to a set of users, and show a card without these buttons to other users.</span></span>

* <span data-ttu-id="ee686-113">Pour maintenir l’état de la carte à jour en permanence, Teams mécanisme de modification des messages peut être mis à profit.</span><span class="sxs-lookup"><span data-stu-id="ee686-113">To keep the card state updated at all times, Teams message edit mechanism can be leveraged.</span></span> <span data-ttu-id="ee686-114">Par exemple, chaque fois qu’une approbation est en place, le bot peut déclencher une modification de message pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ee686-114">For example, each time there is an approval, bot can trigger a message edit to all users.</span></span> <span data-ttu-id="ee686-115">Cette modification de message de bot déclenche une demande d’appel pour tous les utilisateurs d’actualisation automatique, à laquelle le bot peut répondre avec la carte utilisateur spécifique mise `adaptiveCard/action` à jour.</span><span class="sxs-lookup"><span data-stu-id="ee686-115">This bot message edit triggers an `adaptiveCard/action` invoke request for all automatic refresh users, to which the bot can respond with the updated user specific card.</span></span>

<span data-ttu-id="ee686-116">Pour plus d’informations, [voir comment modifier un message de bot.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)</span><span class="sxs-lookup"><span data-stu-id="ee686-116">For more information, see [how to do a bot message edit](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).</span></span>

## <a name="approval-base-card"></a><span data-ttu-id="ee686-117">Carte de base d’approbation</span><span class="sxs-lookup"><span data-stu-id="ee686-117">Approval base card</span></span>

<span data-ttu-id="ee686-118">Le code suivant fournit un exemple de carte de base d’approbation :</span><span class="sxs-lookup"><span data-stu-id="ee686-118">The following code provides an example of an approval base card:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a><span data-ttu-id="ee686-119">Carte d’approbation avec boutons Approuver et Rejeter</span><span class="sxs-lookup"><span data-stu-id="ee686-119">Approval card with Approve and Reject buttons</span></span>

<span data-ttu-id="ee686-120">Le code suivant fournit un exemple de carte d’approbation avec les boutons **Approuver** **et** Rejeter :</span><span class="sxs-lookup"><span data-stu-id="ee686-120">The following code provides an example of an approval card with **Approve** and **Reject** buttons:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="ee686-121">Voici les deux rôles présentés aux utilisateurs en fonction de leur implication dans la demande d’approbation :</span><span class="sxs-lookup"><span data-stu-id="ee686-121">Following are the two roles that are shown to users depending on their involvement in the approval request:</span></span>

* <span data-ttu-id="ee686-122">Carte de base d’approbation : présentée aux utilisateurs qui ne font pas partie de la liste des approuveurs et qui n’ont pas encore approuvé ou rejeté la demande et qui ne font pas partie de la liste dans la propriété du JSON de carte `userIds` `refresh` adaptative.</span><span class="sxs-lookup"><span data-stu-id="ee686-122">Approval base card: Shown to users who are not part of approvers list and have not yet approved or rejected the request, and are not part of `userIds` list in `refresh` property of the Adaptive Card JSON.</span></span>
* <span data-ttu-id="ee686-123">Carte d’approbation  avec **boutons** Approuver ou Rejeter : affichée aux utilisateurs qui font partie de la liste des approuveurs et à la liste dans la propriété du JSON de carte `userIds` adaptative. `refresh`</span><span class="sxs-lookup"><span data-stu-id="ee686-123">Approval card with **Approve** or **Reject** buttons: Shown to the users who are part of the approvers list and the `userIds` list in the `refresh` property of the Adaptive Card JSON.</span></span>

<span data-ttu-id="ee686-124">**Pour envoyer la demande d’approbation de biens**</span><span class="sxs-lookup"><span data-stu-id="ee686-124">**To send the asset approval request**</span></span>

1. <span data-ttu-id="ee686-125">Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.</span><span class="sxs-lookup"><span data-stu-id="ee686-125">Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.</span></span>
2. <span data-ttu-id="ee686-126">Le bot envoie la carte de base d’approbation dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="ee686-126">Bot sends the approval base card in the conversation.</span></span>
3. <span data-ttu-id="ee686-127">Tous les autres utilisateurs de la conversation voient la carte envoyée par le bot.</span><span class="sxs-lookup"><span data-stu-id="ee686-127">All other users in the conversation see the card sent by the bot.</span></span> <span data-ttu-id="ee686-128">L’actualisation automatique est déclenchée pour Megan et Nestor,  qui  voient désormais la carte spécifique de l’utilisateur avec des boutons Approuver ou Rejeter lorsque leurs MRIS utilisateur sont ajoutés à la liste dans la propriété de la carte `userIds` adaptative. `refresh`</span><span class="sxs-lookup"><span data-stu-id="ee686-128">Automatic refresh is triggered for Megan and Nestor, who now see the user specific card with **Approve** or **Reject** buttons as their user MRIs are added to the `userIds` list in the `refresh` property of the Adaptive Card.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="Affichages spécifiques à l’utilisateur":::

4. <span data-ttu-id="ee686-130">Nestor sélectionne le **bouton Approuver** qui est alimenté avec `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="ee686-130">Nestor selects the **Approve** button which is powered with `Action.Execute`.</span></span> <span data-ttu-id="ee686-131">Le bot obtient `adaptiveCard/action` une demande d’appel à laquelle il peut renvoyer une carte adaptative en réponse.</span><span class="sxs-lookup"><span data-stu-id="ee686-131">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
5. <span data-ttu-id="ee686-132">Le bot déclenche une modification de message avec une carte mise à jour qui indique que Nestor a approuvé la demande pendant que l’approbation de Megan est en attente.</span><span class="sxs-lookup"><span data-stu-id="ee686-132">The bot triggers a message edit with an updated card which says Nestor has approved the request while Megan's approval is pending.</span></span>
6. <span data-ttu-id="ee686-133">La modification du message du bot déclenche une actualisation automatique pour Megan et voit la carte spécifique de  l’utilisateur mise à jour, qui indique que Nestor a approuvé la demande, mais voit également les boutons Approuver ou Rejeter. </span><span class="sxs-lookup"><span data-stu-id="ee686-133">Bot message edit triggers an automatic refresh for Megan and she sees the updated user specific card, which says Nestor has approved the request, but also sees the **Approve** or **Reject** buttons.</span></span> <span data-ttu-id="ee686-134">L’utilisateur DE NEstor EST supprimé de la liste dans la propriété de cette carte adaptative JSON aux étapes `userIds` `refresh` 4 et 5.</span><span class="sxs-lookup"><span data-stu-id="ee686-134">Nestor's user MRI is removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 4 and 5.</span></span> <span data-ttu-id="ee686-135">À présent, l’actualisation automatique est déclenchée uniquement pour Megan.</span><span class="sxs-lookup"><span data-stu-id="ee686-135">Now, automatic refresh is only triggered for Megan.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="Affichages utilisateur spécifiques à jour":::

7. <span data-ttu-id="ee686-137">À présent, Megan sélectionne le **bouton Approuver,** qui est alimenté avec `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="ee686-137">Now, Megan selects the **Approve** button, which is powered with `Action.Execute`.</span></span> <span data-ttu-id="ee686-138">Le bot obtient `adaptiveCard/action` une demande d’appel à laquelle il peut renvoyer une carte adaptative en réponse.</span><span class="sxs-lookup"><span data-stu-id="ee686-138">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
8. <span data-ttu-id="ee686-139">Le bot déclenche une modification de message avec une carte mise à jour, ce qui indique que Nestor et Megan ont approuvé la demande.</span><span class="sxs-lookup"><span data-stu-id="ee686-139">The bot triggers a message edit with an updated card, which says Nestor and Megan have approved the request.</span></span>
9. <span data-ttu-id="ee686-140">La modification du message du bot ne déclenche aucune actualisation automatique.</span><span class="sxs-lookup"><span data-stu-id="ee686-140">Bot message edit does not trigger any automatic refresh.</span></span> <span data-ttu-id="ee686-141">L’utilisateur DE MEGAN EST également supprimé de la liste dans la propriété de cette carte adaptative JSON aux `userIds` `refresh` étapes 7 et 8.</span><span class="sxs-lookup"><span data-stu-id="ee686-141">Megan's user MRI is also removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 7 and 8.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="Affichages à jour":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a><span data-ttu-id="ee686-143">Carte adaptative envoyée en réponse à `adaptiveCard/action` et `message edit`</span><span class="sxs-lookup"><span data-stu-id="ee686-143">Adaptive Card sent as response of `adaptiveCard/action` and `message edit`</span></span>

<span data-ttu-id="ee686-144">Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse aux étapes `adaptiveCard/action` `message edit` 4 et 5 :</span><span class="sxs-lookup"><span data-stu-id="ee686-144">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 4 and 5:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

<span data-ttu-id="ee686-145">Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse à un appel via `adaptiveCard/action` l’actualisation automatique pour l’étape 6 :</span><span class="sxs-lookup"><span data-stu-id="ee686-145">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` invoke through automatic refresh for step 6:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="ee686-146">Le code suivant fournit un exemple de cartes adaptatives envoyées en réponse aux étapes `adaptiveCard/action` `message edit` 7 et 8 :</span><span class="sxs-lookup"><span data-stu-id="ee686-146">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 7 and 8:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="see-also"></a><span data-ttu-id="ee686-147">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ee686-147">See also</span></span>

* [<span data-ttu-id="ee686-148">Travailler avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="ee686-148">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="ee686-149">Affichages spécifiques à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ee686-149">User Specific Views</span></span>](User-Specific-Views.md)
