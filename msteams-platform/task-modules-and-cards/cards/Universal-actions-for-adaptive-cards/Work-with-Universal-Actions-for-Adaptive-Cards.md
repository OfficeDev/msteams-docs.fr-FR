---
title: Travailler avec des actions universelles pour les cartes adaptatives
description: Travaillez avec les actions universelles pour les cartes adaptatives.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8c260a4893d38ad365cbb3bdd5a7613a1b42654f
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088839"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="bf9f7-103">Travailler avec des actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="bf9f7-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="bf9f7-104">Les actions universelles pour les cartes adaptatives offrent un moyen d'implémenter des scénarios basés sur la carte adaptative pour les cartes Teams et Outlook.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="bf9f7-105">Ce document couvre les sujets suivants :</span><span class="sxs-lookup"><span data-stu-id="bf9f7-105">This document covers the following:</span></span>

* [<span data-ttu-id="bf9f7-106">Schéma utilisé pour les actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="bf9f7-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="bf9f7-107">Modèle d'actualisation</span><span class="sxs-lookup"><span data-stu-id="bf9f7-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="bf9f7-108">`adaptiveCard/action` activité d'appel</span><span class="sxs-lookup"><span data-stu-id="bf9f7-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="bf9f7-109">Compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="bf9f7-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="bf9f7-110">Guide de démarrage rapide pour tirer parti des actions universelles pour les cartes adaptatives dans Teams</span><span class="sxs-lookup"><span data-stu-id="bf9f7-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="bf9f7-111">Remplacez toutes les instances `Action.Submit` de par pour mettre à jour un scénario existant sur `Action.Execute` Teams.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="bf9f7-112">Ajoutez une clause à votre carte adaptative si vous souhaitez tirer parti du modèle d'actualisation automatique ou si votre scénario nécessite des affichages `refresh` spécifiques de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="bf9f7-113">Spécifiez la `userIds` propriété à identifier et les utilisateurs qui obtiennent les mises à jour automatiques.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="bf9f7-114">Gérer `adaptiveCard/action` les demandes d'appel dans votre bot.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="bf9f7-115">Utilisez le contexte de la demande d'appel pour répondre à l'aide de cartes spécifiquement créées pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf9f7-116">Chaque fois que votre bot renvoie une nouvelle carte suite au traitement d'un , la réponse doit `Action.Execute` être conforme au format de réponse.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="bf9f7-117">Schéma des actions universelles pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="bf9f7-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="bf9f7-118">Les actions universelles pour les cartes adaptatives sont introduites dans le schéma de cartes adaptatives version 1.4.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="bf9f7-119">Pour utiliser efficacement la carte adaptative, la propriété de votre carte adaptative doit être définie `version` sur 1,4.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="bf9f7-120">La définition de la propriété sur 1.4 rend votre carte adaptative incompatible avec les clients plus anciens des plateformes ou des applications, tels que Outlook et Teams, car ils ne prend pas en charge les actions universelles pour les cartes `version` adaptatives.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="bf9f7-121">Si vous définissez la version de carte sur moins de 1.4 et utilisez l'une ou l'autre des deux, propriété et , les choses `refresh` `Action.Execute` suivantes se produisent :</span><span class="sxs-lookup"><span data-stu-id="bf9f7-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="bf9f7-122">Client</span><span class="sxs-lookup"><span data-stu-id="bf9f7-122">Client</span></span> | <span data-ttu-id="bf9f7-123">Comportement</span><span class="sxs-lookup"><span data-stu-id="bf9f7-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="bf9f7-124">Teams</span><span class="sxs-lookup"><span data-stu-id="bf9f7-124">Teams</span></span> | <span data-ttu-id="bf9f7-125">Votre carte cesse de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-125">Your card stops working.</span></span> <span data-ttu-id="bf9f7-126">La carte n'est pas actualisée et ne s'restituera pas en fonction de la `Action.Execute` version du client Teams client.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="bf9f7-127">Pour garantir la compatibilité maximale dans Teams, définissez avec un dans `Action.Execute` `Action.Submit` la propriété de fallback.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="bf9f7-128">Pour plus d'informations sur la prise en charge des clients plus anciens, voir [compatibilité ascendante.](#backward-compatibility)</span><span class="sxs-lookup"><span data-stu-id="bf9f7-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="bf9f7-129">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="bf9f7-129">Action.Execute</span></span>

<span data-ttu-id="bf9f7-130">Lors de la conception de cartes adaptatives, `Action.Submit` remplacez et `Action.Http` par `Action.Execute` .</span><span class="sxs-lookup"><span data-stu-id="bf9f7-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="bf9f7-131">Le schéma pour `Action.Execute` est similaire à celui de `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="bf9f7-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="bf9f7-132">Pour plus d'informations, [voirAction.Exeschéma et propriétés cute.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)</span><span class="sxs-lookup"><span data-stu-id="bf9f7-132">For more information, see [Action.Execute schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="bf9f7-133">À présent, vous pouvez utiliser le modèle d'actualisation pour permettre aux cartes adaptatives de se mettre à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="bf9f7-134">Modèle d'actualisation</span><span class="sxs-lookup"><span data-stu-id="bf9f7-134">Refresh model</span></span>

<span data-ttu-id="bf9f7-135">Pour actualiser automatiquement votre carte adaptative, définissez sa propriété, qui incorpore une `refresh` action de type et un `Action.Execute` `userIds` tableau.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="bf9f7-136">Pour plus d'informations, voir [le schéma d'actualisation et les propriétés.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)</span><span class="sxs-lookup"><span data-stu-id="bf9f7-136">For more information, see [refresh schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="bf9f7-137">ID utilisateur en cours d'actualisation</span><span class="sxs-lookup"><span data-stu-id="bf9f7-137">User IDs in refresh</span></span>

<span data-ttu-id="bf9f7-138">Les fonctionnalités des UserIds en actualisation sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf9f7-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="bf9f7-139">UserIds est un tableau d'utilisateurSIPL qui fait partie de la `refresh` propriété dans les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="bf9f7-140">Si la propriété de liste est spécifiée comme dans la section Actualiser de la carte, la carte n'est `userIds` `userIds: []` pas actualisée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="bf9f7-141">Au lieu de cela, une **option** Actualiser la carte s'affiche pour l'utilisateur dans le menu à trois points du site web ou de bureau, et dans le menu contextif long sur mobile, c'est-à-dire, Android ou iOS pour actualiser manuellement la carte.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="bf9f7-142">La propriété UserIds est ajoutée, car les canaux Teams peuvent inclure un grand nombre de membres.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="bf9f7-143">Si tous les membres voient le canal en même temps, une actualisation automatique inconditionnelle entraîne de nombreux appels simultanés au bot.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="bf9f7-144">Pour éviter cela, la propriété doit toujours être incluse pour identifier les utilisateurs devant obtenir une actualisation automatique avec un maximum de `userIds` *60 MRI d'utilisateurs (en particulier).*</span><span class="sxs-lookup"><span data-stu-id="bf9f7-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="bf9f7-145">Pour plus d'informations sur la façon d'extraire les MRI utilisateur d'un membre de la conversation Teams à ajouter à la liste userIds dans la section Actualiser de la carte adaptative, voir récupérer la liste ou le profil [utilisateur.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)</span><span class="sxs-lookup"><span data-stu-id="bf9f7-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="bf9f7-146">Exemple de Teams'utilisateurSYRY est`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span><span class="sxs-lookup"><span data-stu-id="bf9f7-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="bf9f7-147">La propriété est ignorée dans Outlook, et la propriété est `userIds` `refresh` toujours activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="bf9f7-148">Il n'existe aucun problème d'échelle Outlook car les utilisateurs visualisent la carte à différents moments.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="bf9f7-149">L'étape suivante consiste à utiliser `adaptiveCard/action` l'activité d'appel pour comprendre quelle demande doit être faite après `Action.Execute` l'exécution.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="bf9f7-150">`adaptiveCard/action` activité d'appel</span><span class="sxs-lookup"><span data-stu-id="bf9f7-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="bf9f7-151">Lorsqu'il est exécuté dans le client, un nouveau type d'activité `Action.Execute` Invoke est apporté à votre `adaptiveCard/action` bot.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="bf9f7-152">Pour plus d'informations, [voir le format de requête et les propriétés d'une activité `adaptiveCard/action` d'appel classique.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format)</span><span class="sxs-lookup"><span data-stu-id="bf9f7-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="bf9f7-153">Pour plus d'informations, voir le format de réponse et les propriétés [d'une activité `adaptiveCard/action` d'appel classique avec les types de réponse pris en charge.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format)</span><span class="sxs-lookup"><span data-stu-id="bf9f7-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="bf9f7-154">Ensuite, vous pouvez appliquer la compatibilité ascendante à des clients plus anciens sur différentes plateformes et rendre votre carte adaptative compatible.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="bf9f7-155">Compatibilité descendante</span><span class="sxs-lookup"><span data-stu-id="bf9f7-155">Backward compatibility</span></span>

<span data-ttu-id="bf9f7-156">Les actions universelles pour les cartes adaptatives vous permettent de définir des propriétés qui permettent la compatibilité ascendante avec les anciennes versions de Outlook et Teams.</span><span class="sxs-lookup"><span data-stu-id="bf9f7-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="bf9f7-157">Teams</span><span class="sxs-lookup"><span data-stu-id="bf9f7-157">Teams</span></span>

<span data-ttu-id="bf9f7-158">Pour garantir la compatibilité ascendante de vos cartes adaptatives avec les versions antérieures de Teams, vous devez inclure la propriété et définir `fallback` sa valeur sur `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="bf9f7-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="bf9f7-159">En outre, votre code de bot doit traiter les deux `Action.Execute` et `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="bf9f7-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="bf9f7-160">Pour plus d'informations, [voir compatibilité ascendante sur Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).</span><span class="sxs-lookup"><span data-stu-id="bf9f7-160">For more information, see [backward compatibility on Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="see-also"></a><span data-ttu-id="bf9f7-161">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bf9f7-161">See also</span></span>

* [<span data-ttu-id="bf9f7-162">Actions de carte adaptative dans Teams</span><span class="sxs-lookup"><span data-stu-id="bf9f7-162">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="bf9f7-163">Comment fonctionnent les bots ?</span><span class="sxs-lookup"><span data-stu-id="bf9f7-163">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
