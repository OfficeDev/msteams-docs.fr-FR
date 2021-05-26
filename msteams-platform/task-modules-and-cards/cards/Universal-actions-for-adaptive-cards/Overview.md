---
title: Vue d’ensemble des actions universelles pour les cartes adaptatives
description: Vue d’ensemble rapide des actions universelles pour les cartes adaptatives.
ms.topic: overview
localization_priority: Normal
ms.openlocfilehash: 8bdbc488c68bf9bef79363f1a22d66e63ec32e08
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649715"
---
# <a name="universal-actions-for-adaptive-cards"></a><span data-ttu-id="92789-103">Actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="92789-103">Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="92789-104">Les actions universelles pour les cartes adaptatives ont évolué à partir d’un retour du développeur qui, même si la disposition et le rendu des cartes adaptatives étaient universels, la gestion des actions n’était pas.</span><span class="sxs-lookup"><span data-stu-id="92789-104">Universal Actions for Adaptive Cards evolved from developer feedback that even though layout and rendering for Adaptive Cards was universal, action handling was not.</span></span> <span data-ttu-id="92789-105">Même si un développeur souhaitait envoyer la même carte à différents endroits, il doit gérer les actions différemment.</span><span class="sxs-lookup"><span data-stu-id="92789-105">Even if a developer wanted to send the same card to different places, they have to handle actions differently.</span></span>

<span data-ttu-id="92789-106">Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute` which works across apps, such as Teams and Outlook.</span><span class="sxs-lookup"><span data-stu-id="92789-106">Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute`, which works across apps, such as Teams and Outlook.</span></span>

<span data-ttu-id="92789-107">Ce document vous aide à comprendre comment utiliser le modèle Actions universelles pour améliorer l’expérience utilisateur lors de l’interaction avec les cartes adaptatives sur les plateformes et les applications.</span><span class="sxs-lookup"><span data-stu-id="92789-107">This document helps you to understand how you can use Universal Actions model to enhance user experience of interacting with Adaptive Cards across platforms and applications.</span></span>

> [!NOTE]
> <span data-ttu-id="92789-108">La prise en charge des actions universelles pour les cartes adaptatives est disponible uniquement pour les cartes envoyées par le bot.</span><span class="sxs-lookup"><span data-stu-id="92789-108">Support for Universal Actions for Adaptive Cards is only available for cards sent by bot.</span></span> <span data-ttu-id="92789-109">La prise en charge des cartes envoyées par le biais de la zone de composition et des cartes de déploiement de liens sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="92789-109">Support for cards sent through compose box and link unfurling cards is coming soon.</span></span>

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="92789-110">Améliorer les expériences utilisateur avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="92789-110">Enhance user experiences with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="92789-111">Les actions universelles pour les cartes adaptatives améliorent l’expérience utilisateur en activant les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="92789-111">Universal Actions for Adaptive Cards enhances user experience by enabling the following scenarios:</span></span>

* [<span data-ttu-id="92789-112">Actions universelles</span><span class="sxs-lookup"><span data-stu-id="92789-112">Universal Actions</span></span>](#universal-actions)
* [<span data-ttu-id="92789-113">Affichages spécifiques à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="92789-113">User Specific Views</span></span>](#user-specific-views)
* [<span data-ttu-id="92789-114">Prise en charge séquentielle du flux de travail</span><span class="sxs-lookup"><span data-stu-id="92789-114">Sequential Workflow support</span></span>](#sequential-workflow-support)
* [<span data-ttu-id="92789-115">Affichages à jour</span><span class="sxs-lookup"><span data-stu-id="92789-115">Up to date views</span></span>](#up-to-date-views)

### <a name="universal-actions"></a><span data-ttu-id="92789-116">Actions universelles</span><span class="sxs-lookup"><span data-stu-id="92789-116">Universal Actions</span></span>

<span data-ttu-id="92789-117">Avant les actions universelles pour les cartes adaptatives, différents hôtes fournissaient différents modèles d’action comme suit :</span><span class="sxs-lookup"><span data-stu-id="92789-117">Before the Universal Actions for Adaptive Cards, different hosts provided different action models as follows:</span></span>

* <span data-ttu-id="92789-118">Teams ou bots utilisés, une approche qui reporte le modèle de communication réel `Action.Submit` au canal sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="92789-118">Teams or bots used `Action.Submit`, an approach which defers the actual communication model to the underlying channel.</span></span>
* <span data-ttu-id="92789-119">Outlook utilisé pour communiquer avec le service backend spécifié explicitement dans la charge utile de `Action.Http` carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="92789-119">Outlook used `Action.Http` to communicate with the backend service explicitly specified in the Adaptive Card payload.</span></span>

<span data-ttu-id="92789-120">L’image suivante illustre le modèle d’action incohérent actuel :</span><span class="sxs-lookup"><span data-stu-id="92789-120">The following image shows the current inconsistent action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Modèle d’action incohérent":::

<span data-ttu-id="92789-122">Avec les actions universelles pour les cartes adaptatives, vous pouvez utiliser la gestion des `Action.Execute` actions sur différentes plateformes.</span><span class="sxs-lookup"><span data-stu-id="92789-122">With the Universal Actions for Adaptive Cards, you can use `Action.Execute` for action handling across different platforms.</span></span> <span data-ttu-id="92789-123">`Action.Execute`fonctionne sur les hubs, notamment Teams et Outlook.</span><span class="sxs-lookup"><span data-stu-id="92789-123">`Action.Execute` works across hubs including Teams and Outlook.</span></span> <span data-ttu-id="92789-124">En outre, une carte adaptative peut être renvoyée en réponse à une `Action.Execute` demande d’appel déclenchée.</span><span class="sxs-lookup"><span data-stu-id="92789-124">In addition, an Adaptive Card can be returned as response for an `Action.Execute` triggered invoke request.</span></span>

<span data-ttu-id="92789-125">L’image suivante montre le nouveau modèle d’action universelle :</span><span class="sxs-lookup"><span data-stu-id="92789-125">The following image shows the new Universal Action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Nouvelles actions universelles pour les cartes adaptatives":::

<span data-ttu-id="92789-127">Vous pouvez désormais envoyer la même carte aux deux Teams et Outlook et les synchroniser les unes avec les autres à l’aide du bot sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="92789-127">You can now send the same card to both, Teams and Outlook, and keep them in sync with each other using the underlying bot.</span></span> <span data-ttu-id="92789-128">Toute action entreprise sur l’une ou l’autre plateforme est reflétée dans l’autre avec cette build une seule *fois,* déployer n’importe où (Actions universelles pour les cartes adaptatives).</span><span class="sxs-lookup"><span data-stu-id="92789-128">Any action taken on either platform is reflected to the other with this *build once, deploy anywhere* (Universal Actions for Adaptive Cards) model.</span></span>

<span data-ttu-id="92789-129">L’image suivante illustre les actions universelles pour les cartes adaptatives pour Teams et Outlook :</span><span class="sxs-lookup"><span data-stu-id="92789-129">The following image depicts the Universal Actions for Adaptive Cards for both Teams and Outlook:</span></span>

# <a name="mobile"></a>[<span data-ttu-id="92789-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="92789-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-teams-outlook.jpg" alt-text="Même carte mobile pour Teams et Outlook":::

# <a name="desktop"></a>[<span data-ttu-id="92789-132">Desktop</span><span class="sxs-lookup"><span data-stu-id="92789-132">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Même carte pour Teams et Outlook":::

* * *

### <a name="user-specific-views"></a><span data-ttu-id="92789-134">Affichages spécifiques à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="92789-134">User Specific Views</span></span>

<span data-ttu-id="92789-135">Aujourd’hui, tous les utilisateurs Teams chat ou canal voient exactement les mêmes actions d’affichage et de bouton sur la carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="92789-135">Today every user in the Teams chat or channel sees the exact same view and button actions on the Adaptive Card.</span></span> <span data-ttu-id="92789-136">Toutefois, dans certains scénarios, certains utilisateurs doivent agir différemment et avoir accès à différentes informations au sein de la même conversation ou canal.</span><span class="sxs-lookup"><span data-stu-id="92789-136">However, in certain scenarios there is a requirement for certain users to act differently and have access to different information within the same chat or channel.</span></span>

<span data-ttu-id="92789-137">Par exemple, si vous envoyez une carte de rapport d’incident dans une conversation ou un canal, seul l’utilisateur affecté à l’incident doit voir un **bouton Résoudre.**</span><span class="sxs-lookup"><span data-stu-id="92789-137">For example, if you send an incident reporting card in a chat or channel, only the user who is assigned the incident must see a **Resolve** button.</span></span> <span data-ttu-id="92789-138">En revanche, le créateur de  l’incident doit voir un bouton Modifier et tous les autres utilisateurs doivent uniquement être en mesure d’afficher les détails de l’incident.</span><span class="sxs-lookup"><span data-stu-id="92789-138">On the other hand, the incident creator must see an **Edit** button and all other users must only be able to view details of the incident.</span></span> <span data-ttu-id="92789-139">Cela est rendu possible par les affichages spécifiques de l’utilisateur qui sont activés par la `refresh` propriété.</span><span class="sxs-lookup"><span data-stu-id="92789-139">This is made possible by User Specific Views that is enabled by the `refresh` property.</span></span>

<span data-ttu-id="92789-140">L’image suivante montre un exemple d’extension de messagerie de ticket dans laquelle différents utilisateurs de la conversation sont affichés différentes actions en fonction de l’exigence :</span><span class="sxs-lookup"><span data-stu-id="92789-140">The following image shows an example of a ticketing messaging extension (ME) where different users in the chat are shown different actions based on the requirement:</span></span>

# <a name="mobile"></a>[<span data-ttu-id="92789-141">Mobile</span><span class="sxs-lookup"><span data-stu-id="92789-141">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Affichages spécifiques aux utilisateurs mobiles":::

# <a name="desktop"></a>[<span data-ttu-id="92789-143">Desktop</span><span class="sxs-lookup"><span data-stu-id="92789-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur":::

* * *

<span data-ttu-id="92789-145">Pour plus d’informations, voir [l’exemple pour les affichages spécifiques de l’utilisateur.](User-Specific-Views.md)</span><span class="sxs-lookup"><span data-stu-id="92789-145">For more information, see [sample for User Specific Views](User-Specific-Views.md).</span></span>

### <a name="sequential-workflow-support"></a><span data-ttu-id="92789-146">Prise en charge séquentielle du flux de travail</span><span class="sxs-lookup"><span data-stu-id="92789-146">Sequential Workflow support</span></span>

<span data-ttu-id="92789-147">Avec la prise en charge séquentielle du flux de travail, les utilisateurs peuvent avancer dans une série de flux de travail sans envoyer différentes cartes séparément.</span><span class="sxs-lookup"><span data-stu-id="92789-147">With Sequential Workflow support, users can progress through a series of workflows without sending different cards separately.</span></span> <span data-ttu-id="92789-148">Cela est rendu possible par la possibilité de renvoyer une carte adaptative `Action.Execute` en réponse à une action.</span><span class="sxs-lookup"><span data-stu-id="92789-148">This is made possible by the ability of `Action.Execute` to return an Adaptive Card in response to an action.</span></span> <span data-ttu-id="92789-149">En outre, tout utilisateur de la conversation ou du canal peut avancer dans son flux de travail sans modifier la carte pour les autres utilisateurs de la conversation.</span><span class="sxs-lookup"><span data-stu-id="92789-149">Also, any user in the chat or channel can progress through their workflow without modifying the card for other users in the chat.</span></span>

<span data-ttu-id="92789-150">L’image suivante illustre un exemple de robot de commande de produits :</span><span class="sxs-lookup"><span data-stu-id="92789-150">The following image illustrates a food ordering bot example:</span></span> <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="92789-151">L’image suivante montre les différents états pour les différents utilisateurs dans la conversation ou le canal :</span><span class="sxs-lookup"><span data-stu-id="92789-151">The following image shows the various states for different users in the chat or channel:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration":::

<span data-ttu-id="92789-153">Pour plus d’informations, voir [l’exemple de flux de travail séquentiel.](Sequential-Workflows.md)</span><span class="sxs-lookup"><span data-stu-id="92789-153">For more information, see [sample for Sequential Workflow](Sequential-Workflows.md).</span></span>

### <a name="up-to-date-views"></a><span data-ttu-id="92789-154">Affichages à jour</span><span class="sxs-lookup"><span data-stu-id="92789-154">Up to date views</span></span>

<span data-ttu-id="92789-155">Vous pouvez créer des cartes adaptatives qui se met à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="92789-155">You can create Adaptive Cards that update automatically.</span></span> <span data-ttu-id="92789-156">Par exemple, il peut s’agit d’une demande d’approbation envoyée par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92789-156">For example, it can be an approval request sent by a user.</span></span> <span data-ttu-id="92789-157">Après l’approbation, la carte doit afficher automatiquement les détails sur l’heure d’approbation de la demande et sur les personnes qui ont approuvé la demande.</span><span class="sxs-lookup"><span data-stu-id="92789-157">After approval, the card must automatically display details about the request approval time and who approved the request.</span></span> <span data-ttu-id="92789-158">Le modèle d’actualisation vous permet de fournir ces affichages à jour.</span><span class="sxs-lookup"><span data-stu-id="92789-158">The refresh model enables you to provide such up to date views.</span></span> <span data-ttu-id="92789-159">L’image suivante illustre un flux d’approbation en plusieurs étapes et la façon dont les vues de différents utilisateurs sont affichées.</span><span class="sxs-lookup"><span data-stu-id="92789-159">The following image shows a multi-step approval flow and how the views for different users is shown.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="Affichages utilisateur spécifiques à jour":::

<span data-ttu-id="92789-161">Pour plus d’informations, voir [l’exemple d’affichages à jour.](Up-To-Date-Views.md)</span><span class="sxs-lookup"><span data-stu-id="92789-161">For more information, see [sample for up to date views](Up-To-Date-Views.md).</span></span>

<span data-ttu-id="92789-162">À présent, vous pouvez comprendre comment les cartes adaptatives peuvent être transformées avec le nouveau modèle Actions universelles pour offrir une expérience utilisateur unique et améliorée.</span><span class="sxs-lookup"><span data-stu-id="92789-162">Now, you can understand how Adaptive Cards can be transformed with the new Universal Actions model to provide a unique and enhanced user experience.</span></span>

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a><span data-ttu-id="92789-163">Cartes adaptatives et nouveau modèle Actions universelles</span><span class="sxs-lookup"><span data-stu-id="92789-163">Adaptive Cards and the new Universal Actions model</span></span>

<span data-ttu-id="92789-164">Les cartes adaptatives sont une combinaison de contenu, tel que du texte et des graphiques, et d’actions qui peuvent être effectuées par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92789-164">Adaptive Cards are a combination of content, such as text and graphics, and actions that can be performed by a user.</span></span> <span data-ttu-id="92789-165">Pour plus d’informations, voir [Cartes adaptatives.](http://adaptivecards.io/)</span><span class="sxs-lookup"><span data-stu-id="92789-165">For more information, see [Adaptive Cards](http://adaptivecards.io/).</span></span> <span data-ttu-id="92789-166">Les nouvelles actions universelles pour les cartes adaptatives permettent une gestion courante des actions de carte adaptative sur les plateformes et les applications.</span><span class="sxs-lookup"><span data-stu-id="92789-166">The new Universal Actions for Adaptive Cards enables a common handling of the Adaptive Card actions across platforms and applications.</span></span> <span data-ttu-id="92789-167">Pour plus d’informations, voir [Modèle d’action universelle.](/adaptive-cards/authoring-cards/universal-action-model)</span><span class="sxs-lookup"><span data-stu-id="92789-167">For more information, see [Universal Action Model](/adaptive-cards/authoring-cards/universal-action-model).</span></span>

<span data-ttu-id="92789-168">Le document [Actions universelles pour cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md) vous permet d’utiliser les fonctionnalités des actions universelles pour les cartes adaptatives pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="92789-168">[Work with Universal Actions for Adaptive Cards](Work-with-universal-actions-for-adaptive-cards.md) document takes you through the steps to use the capabilities of Universal Actions for Adaptive Cards for your solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="92789-169">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="92789-169">See also</span></span>

* [<span data-ttu-id="92789-170">Qu’est-ce que les robots ?</span><span class="sxs-lookup"><span data-stu-id="92789-170">What are bots</span></span>](~/bots/what-are-bots.md)
* [<span data-ttu-id="92789-171">Vue d’ensemble des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="92789-171">Adaptive Cards overview</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="92789-172">Cartes adaptatives @ Microsoft Build 2020</span><span class="sxs-lookup"><span data-stu-id="92789-172">Adaptive Cards @ Microsoft Build 2020</span></span>](https://youtu.be/hEBhwB72Qn4?t=1393)
* [<span data-ttu-id="92789-173">Cartes adaptatives @ Ignite 2020</span><span class="sxs-lookup"><span data-stu-id="92789-173">Adaptive Cards @ Ignite 2020</span></span>](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a><span data-ttu-id="92789-174">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="92789-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92789-175">Travailler avec les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="92789-175">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
