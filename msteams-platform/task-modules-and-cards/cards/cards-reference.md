---
title: Types de cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
localization_priority: Normal
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: d3b84344eccee7c2595b0e978c72d7e331b198cb
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328071"
---
# <a name="types-of-cards"></a><span data-ttu-id="7cfe2-104">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-104">Types of cards</span></span>

<span data-ttu-id="7cfe2-105">Les cartes adaptatives, hero, list, Office 365 Connector, les cartes de réception, les cartes de connexion et les collections de cartes miniatures sont pris en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="7cfe2-106">Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="7cfe2-107">Avant d’identifier les différents types de carte, comprenez comment créer une carte hero, une carte miniature ou une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="7cfe2-108">Créer une carte Hero, une carte miniature ou une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7cfe2-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="7cfe2-109">**Pour créer une carte Hero, une carte miniature ou une carte adaptative à partir d’App Studio**</span><span class="sxs-lookup"><span data-stu-id="7cfe2-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="7cfe2-110">Go to **App Studio** from Teams.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="7cfe2-111">Sélectionnez **l’éditeur de carte.**</span><span class="sxs-lookup"><span data-stu-id="7cfe2-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="7cfe2-112">Sélectionnez **Créer une carte.**</span><span class="sxs-lookup"><span data-stu-id="7cfe2-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="7cfe2-113">Sélectionnez **Créer** pour l’une des cartes **de la carte Hero,** de la carte **miniature** ou de la **carte adaptative.**</span><span class="sxs-lookup"><span data-stu-id="7cfe2-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="7cfe2-114">Les exemples de code de métadonnées, boutons et json, csharp et nœud sont présentés pour cette carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Détails de la carte Hero](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="7cfe2-116">Sélectionnez **M’envoyer cette carte.**</span><span class="sxs-lookup"><span data-stu-id="7cfe2-116">Select **Send me this card**.</span></span> <span data-ttu-id="7cfe2-117">La carte vous est envoyée en tant que message de conversation.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="7cfe2-118">Exemples de carte</span><span class="sxs-lookup"><span data-stu-id="7cfe2-118">Card examples</span></span>

<span data-ttu-id="7cfe2-119">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="7cfe2-120">Des exemples de code sont également disponibles dans le référentiel **Microsoft/BotBuilder-Samples** GitHub.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="7cfe2-121">Voici quelques exemples de cartes :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-121">Following are a few card examples:</span></span>

* <span data-ttu-id="7cfe2-122">.NET</span><span class="sxs-lookup"><span data-stu-id="7cfe2-122">.NET</span></span>
  * <span data-ttu-id="7cfe2-123">[Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="7cfe2-124">[Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="7cfe2-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="7cfe2-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfe2-125">Node.js</span></span>
  * <span data-ttu-id="7cfe2-126">[Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="7cfe2-127">[Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="7cfe2-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="7cfe2-128">Types de carte</span><span class="sxs-lookup"><span data-stu-id="7cfe2-128">Card types</span></span>

<span data-ttu-id="7cfe2-129">Vous pouvez identifier et utiliser différents types de cartes en fonction des besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="7cfe2-130">Le tableau suivant indique les types de cartes disponibles :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="7cfe2-131">Type de carte</span><span class="sxs-lookup"><span data-stu-id="7cfe2-131">Card type</span></span> | <span data-ttu-id="7cfe2-132">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="7cfe2-133">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7cfe2-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="7cfe2-134">Cette carte est hautement personnalisable et peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="7cfe2-135">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="7cfe2-136">Cette carte contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="7cfe2-137">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-137">List card</span></span>](#list-card) | <span data-ttu-id="7cfe2-138">Cette carte contient une liste de défilement d’éléments.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="7cfe2-139">Office 365 Carte de connecteur</span><span class="sxs-lookup"><span data-stu-id="7cfe2-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="7cfe2-140">Cette carte possède une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="7cfe2-141">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="7cfe2-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="7cfe2-142">Cette carte fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="7cfe2-143">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="7cfe2-144">Cette carte permet à un bot de demander à un utilisateur de se rendre.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="7cfe2-145">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="7cfe2-146">Cette carte contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="7cfe2-147">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="7cfe2-148">Cette collection de cartes est utilisée pour renvoyer plusieurs éléments en une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="features-that-support-different-card-types"></a><span data-ttu-id="7cfe2-149">Fonctionnalités qui prise en charge différents types de carte</span><span class="sxs-lookup"><span data-stu-id="7cfe2-149">Features that support different card types</span></span>

| <span data-ttu-id="7cfe2-150">Type de carte</span><span class="sxs-lookup"><span data-stu-id="7cfe2-150">Card type</span></span> | <span data-ttu-id="7cfe2-151">Bots</span><span class="sxs-lookup"><span data-stu-id="7cfe2-151">Bots</span></span> | <span data-ttu-id="7cfe2-152">Aperçus des extensions de message</span><span class="sxs-lookup"><span data-stu-id="7cfe2-152">Message extension previews</span></span> | <span data-ttu-id="7cfe2-153">Résultats de l’extension de message</span><span class="sxs-lookup"><span data-stu-id="7cfe2-153">Message extension results</span></span> | <span data-ttu-id="7cfe2-154">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="7cfe2-154">Task modules</span></span> | <span data-ttu-id="7cfe2-155">Webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="7cfe2-155">Outgoing Webhooks</span></span> | <span data-ttu-id="7cfe2-156">Webhooks entrants</span><span class="sxs-lookup"><span data-stu-id="7cfe2-156">Incoming Webhooks</span></span> | <span data-ttu-id="7cfe2-157">Connecteurs O365</span><span class="sxs-lookup"><span data-stu-id="7cfe2-157">O365 Connectors</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-158">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7cfe2-158">Adaptive Card</span></span> | <span data-ttu-id="7cfe2-159">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-159">✔</span></span> | <span data-ttu-id="7cfe2-160">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-160">✖</span></span> | <span data-ttu-id="7cfe2-161">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-161">✔</span></span> | <span data-ttu-id="7cfe2-162">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-162">✔</span></span> | <span data-ttu-id="7cfe2-163">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-163">✔</span></span> | <span data-ttu-id="7cfe2-164">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-164">✔</span></span> | <span data-ttu-id="7cfe2-165">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-165">✖</span></span> |
| <span data-ttu-id="7cfe2-166">Carte connecteur O365</span><span class="sxs-lookup"><span data-stu-id="7cfe2-166">O365 Connector card</span></span> | <span data-ttu-id="7cfe2-167">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-167">✔</span></span> | <span data-ttu-id="7cfe2-168">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-168">✖</span></span> | <span data-ttu-id="7cfe2-169">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-169">✔</span></span> | <span data-ttu-id="7cfe2-170">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-170">✖</span></span> | <span data-ttu-id="7cfe2-171">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-171">✔</span></span> | <span data-ttu-id="7cfe2-172">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-172">✔</span></span> | <span data-ttu-id="7cfe2-173">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-173">✔</span></span> |
| <span data-ttu-id="7cfe2-174">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-174">Hero card</span></span> | <span data-ttu-id="7cfe2-175">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-175">✔</span></span> | <span data-ttu-id="7cfe2-176">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-176">✔</span></span> | <span data-ttu-id="7cfe2-177">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-177">✔</span></span> | <span data-ttu-id="7cfe2-178">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-178">✖</span></span> | <span data-ttu-id="7cfe2-179">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-179">✔</span></span> | <span data-ttu-id="7cfe2-180">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-180">✔</span></span> | <span data-ttu-id="7cfe2-181">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-181">✖</span></span> |
| <span data-ttu-id="7cfe2-182">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-182">Thumbnail card</span></span> | <span data-ttu-id="7cfe2-183">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-183">✔</span></span> | <span data-ttu-id="7cfe2-184">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-184">✔</span></span> | <span data-ttu-id="7cfe2-185">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-185">✔</span></span> | <span data-ttu-id="7cfe2-186">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-186">✖</span></span> | <span data-ttu-id="7cfe2-187">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-187">✔</span></span> | <span data-ttu-id="7cfe2-188">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-188">✔</span></span> | <span data-ttu-id="7cfe2-189">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-189">✖</span></span> |
| <span data-ttu-id="7cfe2-190">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-190">List card</span></span> | <span data-ttu-id="7cfe2-191">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-191">✔</span></span> | <span data-ttu-id="7cfe2-192">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-192">✖</span></span> | <span data-ttu-id="7cfe2-193">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-193">✖</span></span> | <span data-ttu-id="7cfe2-194">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-194">✖</span></span> | <span data-ttu-id="7cfe2-195">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-195">✔</span></span> | <span data-ttu-id="7cfe2-196">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-196">✔</span></span> | <span data-ttu-id="7cfe2-197">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-197">✖</span></span> |
| <span data-ttu-id="7cfe2-198">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="7cfe2-198">Receipt card</span></span> | <span data-ttu-id="7cfe2-199">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-199">✔</span></span> | <span data-ttu-id="7cfe2-200">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-200">✖</span></span> | <span data-ttu-id="7cfe2-201">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-201">✖</span></span> | <span data-ttu-id="7cfe2-202">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-202">✖</span></span> | <span data-ttu-id="7cfe2-203">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-203">✖</span></span> | <span data-ttu-id="7cfe2-204">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-204">✔</span></span> | <span data-ttu-id="7cfe2-205">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-205">✖</span></span> |
| <span data-ttu-id="7cfe2-206">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-206">Signin card</span></span> | <span data-ttu-id="7cfe2-207">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-207">✔</span></span> | <span data-ttu-id="7cfe2-208">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-208">✖</span></span> | <span data-ttu-id="7cfe2-209">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-209">✖</span></span> | <span data-ttu-id="7cfe2-210">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-210">✖</span></span> | <span data-ttu-id="7cfe2-211">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-211">✖</span></span> | <span data-ttu-id="7cfe2-212">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-212">✖</span></span> | <span data-ttu-id="7cfe2-213">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-213">✖</span></span> |

> [!NOTE]
> <span data-ttu-id="7cfe2-214">Pour les cartes adaptatives dans les webhooks entrants, tous les éléments de schéma de carte adaptative native, à l’exception `Action.Submit` de , sont entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-214">For Adaptive Cards in Incoming Webhooks, all native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span> <span data-ttu-id="7cfe2-215">Les actions prises en charge sont [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)et [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span><span class="sxs-lookup"><span data-stu-id="7cfe2-215">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="7cfe2-216">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-216">Common properties for all cards</span></span>

<span data-ttu-id="7cfe2-217">Vous pouvez passer par certaines propriétés communes qui s’appliquent à toutes les cartes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-217">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="7cfe2-218">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="7cfe2-218">Inline card images</span></span>

<span data-ttu-id="7cfe2-219">La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-219">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="7cfe2-220">À des fins de performances, il est vivement recommandé d’héberger l’image sur une réseau de distribution de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="7cfe2-220">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="7cfe2-221">La taille des images est réduite ou monter en puissance afin de maintenir les proportions pour couvrir la zone d’image.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-221">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="7cfe2-222">Les images sont ensuite rogées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-222">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="7cfe2-223">Les images doivent être au maximum 1024×1024 et au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-223">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="7cfe2-224">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-224">Animated GIF is not supported.</span></span>

<span data-ttu-id="7cfe2-225">Le tableau suivant fournit les propriétés des images de carte en ligne :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-225">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="7cfe2-226">Propriété</span><span class="sxs-lookup"><span data-stu-id="7cfe2-226">Property</span></span> | <span data-ttu-id="7cfe2-227">Type</span><span class="sxs-lookup"><span data-stu-id="7cfe2-227">Type</span></span>  | <span data-ttu-id="7cfe2-228">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-228">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cfe2-229">url</span><span class="sxs-lookup"><span data-stu-id="7cfe2-229">url</span></span> | <span data-ttu-id="7cfe2-230">URL</span><span class="sxs-lookup"><span data-stu-id="7cfe2-230">URL</span></span> | <span data-ttu-id="7cfe2-231">URL HTTPS vers l’image.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-231">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="7cfe2-232">alt</span><span class="sxs-lookup"><span data-stu-id="7cfe2-232">alt</span></span> | <span data-ttu-id="7cfe2-233">String</span><span class="sxs-lookup"><span data-stu-id="7cfe2-233">String</span></span> | <span data-ttu-id="7cfe2-234">Description accessible de l’image.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-234">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="7cfe2-235">Si une carte inclut une URL d’image qui est redirigée avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-235">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="7cfe2-236">Cela se produit pour les images partagées sur le cloud public.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-236">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="7cfe2-237">Boutons</span><span class="sxs-lookup"><span data-stu-id="7cfe2-237">Buttons</span></span>

<span data-ttu-id="7cfe2-238">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-238">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="7cfe2-239">Le texte du bouton est toujours sur une seule ligne et tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-239">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="7cfe2-240">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne sont pas affichés.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-240">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="7cfe2-241">Pour plus d’informations, voir [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-241">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="7cfe2-242">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="7cfe2-242">Card formatting</span></span>

<span data-ttu-id="7cfe2-243">Pour plus d’informations sur la mise en forme du texte dans les cartes, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-243">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="7cfe2-244">Après avoir identifié les propriétés communes de toutes les cartes, vous pouvez désormais utiliser des cartes adaptatives, ce qui vous permet d’augmenter l’engagement et l’efficacité en ajoutant votre contenu actionnable directement dans les applications que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-244">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="7cfe2-245">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7cfe2-245">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="7cfe2-246">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-246">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="7cfe2-247">Pour plus d’informations, [voir Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="7cfe2-247">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="7cfe2-248">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7cfe2-248">Support for Adaptive Cards</span></span>

<span data-ttu-id="7cfe2-249">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-249">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="7cfe2-250">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-250">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-251">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-251">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-252">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-252">Connectors</span></span> | <span data-ttu-id="7cfe2-253">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-253">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-254">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-254">✔</span></span> | <span data-ttu-id="7cfe2-255">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-255">✔</span></span> | <span data-ttu-id="7cfe2-256">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-256">✖</span></span> | <span data-ttu-id="7cfe2-257">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-257">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="7cfe2-258">Teams plateforme prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-258">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="7cfe2-259">Le style d’action positive ou destructive n’est pas pris en charge dans les cartes adaptatives sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-259">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="7cfe2-260">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-260">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="7cfe2-261">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7cfe2-261">Example of Adaptive Card</span></span>

![Exemple de carte adaptative](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="7cfe2-263">Le code suivant illustre un exemple de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-263">The following code shows an example of an Adaptive Card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="7cfe2-264">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7cfe2-264">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="7cfe2-265">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-265">Bot Framework reference:</span></span>

* [<span data-ttu-id="7cfe2-266">Nœud cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7cfe2-266">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="7cfe2-267">Carte adaptative C #</span><span class="sxs-lookup"><span data-stu-id="7cfe2-267">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="7cfe2-268">Vous pouvez désormais utiliser une carte Hero, qui est une carte multi-usage utilisée pour mettre en évidence visuellement une sélection d’utilisateur potentielle.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-268">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="7cfe2-269">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-269">Hero card</span></span>

<span data-ttu-id="7cfe2-270">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-270">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="7cfe2-271">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-271">Support for hero cards</span></span>

<span data-ttu-id="7cfe2-272">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes Hero :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-272">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="7cfe2-273">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-273">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-274">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-274">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-275">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-275">Connectors</span></span> | <span data-ttu-id="7cfe2-276">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-276">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-277">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-277">✔</span></span> | <span data-ttu-id="7cfe2-278">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-278">✔</span></span> | <span data-ttu-id="7cfe2-279">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-279">✖</span></span> | <span data-ttu-id="7cfe2-280">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-280">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="7cfe2-281">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-281">Properties of a hero card</span></span>

<span data-ttu-id="7cfe2-282">Le tableau suivant fournit les propriétés d’une carte Hero :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-282">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="7cfe2-283">Propriété</span><span class="sxs-lookup"><span data-stu-id="7cfe2-283">Property</span></span> | <span data-ttu-id="7cfe2-284">Type</span><span class="sxs-lookup"><span data-stu-id="7cfe2-284">Type</span></span>  | <span data-ttu-id="7cfe2-285">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-285">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cfe2-286">title</span><span class="sxs-lookup"><span data-stu-id="7cfe2-286">title</span></span> | <span data-ttu-id="7cfe2-287">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-287">Rich text</span></span> | <span data-ttu-id="7cfe2-288">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-288">Title of the card.</span></span> <span data-ttu-id="7cfe2-289">Deux lignes au maximum.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-289">Maximum two lines.</span></span> |
| <span data-ttu-id="7cfe2-290">subtitle</span><span class="sxs-lookup"><span data-stu-id="7cfe2-290">subtitle</span></span> | <span data-ttu-id="7cfe2-291">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-291">Rich text</span></span> | <span data-ttu-id="7cfe2-292">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-292">Subtitle of the card.</span></span> <span data-ttu-id="7cfe2-293">Deux lignes au maximum.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-293">Maximum two lines.</span></span>|
| <span data-ttu-id="7cfe2-294">text</span><span class="sxs-lookup"><span data-stu-id="7cfe2-294">text</span></span> | <span data-ttu-id="7cfe2-295">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-295">Rich text</span></span> | <span data-ttu-id="7cfe2-296">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-296">Text appears under the subtitle.</span></span> <span data-ttu-id="7cfe2-297">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-297">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="7cfe2-298">images</span><span class="sxs-lookup"><span data-stu-id="7cfe2-298">images</span></span> | <span data-ttu-id="7cfe2-299">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="7cfe2-299">Array of images</span></span> | <span data-ttu-id="7cfe2-300">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-300">Image displayed at the top of the card.</span></span> <span data-ttu-id="7cfe2-301">Proportions 16:9.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-301">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="7cfe2-302">buttons</span><span class="sxs-lookup"><span data-stu-id="7cfe2-302">buttons</span></span> | <span data-ttu-id="7cfe2-303">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="7cfe2-303">Array of action objects</span></span> | <span data-ttu-id="7cfe2-304">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-304">Set of actions applicable to the current card.</span></span> <span data-ttu-id="7cfe2-305">Six maximum.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-305">Maximum six.</span></span> |
| <span data-ttu-id="7cfe2-306">tap</span><span class="sxs-lookup"><span data-stu-id="7cfe2-306">tap</span></span> | <span data-ttu-id="7cfe2-307">Objet Action</span><span class="sxs-lookup"><span data-stu-id="7cfe2-307">Action object</span></span> | <span data-ttu-id="7cfe2-308">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-308">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="7cfe2-309">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-309">Example of a hero card</span></span>

![Exemple de carte Hero](~/assets/images/cards/hero.png)

<span data-ttu-id="7cfe2-311">Le code suivant montre un exemple de carte Hero :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-311">The following code shows an example of a hero card:</span></span>

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="7cfe2-312">Informations supplémentaires sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="7cfe2-312">Additional information on hero cards</span></span>

<span data-ttu-id="7cfe2-313">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="7cfe2-314">Carte Hero Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfe2-314">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="7cfe2-315">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="7cfe2-315">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="7cfe2-316">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-316">List card</span></span>

<span data-ttu-id="7cfe2-317">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-317">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="7cfe2-318">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-318">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="7cfe2-319">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-319">Support for list cards</span></span>

<span data-ttu-id="7cfe2-320">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de liste :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-320">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="7cfe2-321">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-321">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-322">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-322">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-323">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-323">Connectors</span></span> | <span data-ttu-id="7cfe2-324">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-324">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-325">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-325">✔</span></span> | <span data-ttu-id="7cfe2-326">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-326">✖</span></span> | <span data-ttu-id="7cfe2-327">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-327">✖</span></span> |<span data-ttu-id="7cfe2-328">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-328">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="7cfe2-329">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-329">Properties of a list card</span></span>

<span data-ttu-id="7cfe2-330">Le tableau suivant fournit les propriétés d’une carte de liste :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-330">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="7cfe2-331">Propriété</span><span class="sxs-lookup"><span data-stu-id="7cfe2-331">Property</span></span> | <span data-ttu-id="7cfe2-332">Type</span><span class="sxs-lookup"><span data-stu-id="7cfe2-332">Type</span></span>  | <span data-ttu-id="7cfe2-333">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-333">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cfe2-334">title</span><span class="sxs-lookup"><span data-stu-id="7cfe2-334">title</span></span> | <span data-ttu-id="7cfe2-335">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-335">Rich text</span></span> | <span data-ttu-id="7cfe2-336">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-336">Title of the card.</span></span> <span data-ttu-id="7cfe2-337">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-337">Maximum 2 lines.</span></span>|
| <span data-ttu-id="7cfe2-338">éléments</span><span class="sxs-lookup"><span data-stu-id="7cfe2-338">items</span></span> | <span data-ttu-id="7cfe2-339">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-339">Array of list items</span></span> | <span data-ttu-id="7cfe2-340">Ensemble d’éléments applicables à la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-340">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="7cfe2-341">buttons</span><span class="sxs-lookup"><span data-stu-id="7cfe2-341">buttons</span></span> | <span data-ttu-id="7cfe2-342">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="7cfe2-342">Array of action objects</span></span> | <span data-ttu-id="7cfe2-343">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-343">Set of actions applicable to the current card.</span></span> <span data-ttu-id="7cfe2-344">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-344">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="7cfe2-345">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="7cfe2-345">Example of a list card</span></span>

<span data-ttu-id="7cfe2-346">Le code suivant montre un exemple de carte de liste :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-346">The following code shows an example of a list card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a><span data-ttu-id="7cfe2-347">carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="7cfe2-347">Office 365 connector card</span></span>

<span data-ttu-id="7cfe2-348">Vous pouvez utiliser une carte connecteur Office 365 qui fournit une disposition flexible et constitue un excellent moyen d’obtenir des informations utiles.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-348">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="7cfe2-349">La carte Office 365 connecteur est prise en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-349">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="7cfe2-350">Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-350">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="7cfe2-351">Cette carte contient une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-351">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="7cfe2-352">Pour plus d’informations sur les différences entre les cartes de connecteur et la carte connecteur Office 365, consultez des informations supplémentaires sur [la carte Office 365 connecteur.](#additional-information-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-352">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="7cfe2-353">Prise en charge des cartes Office 365 connecteur de connexion</span><span class="sxs-lookup"><span data-stu-id="7cfe2-353">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="7cfe2-354">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge Office 365 cartes de connecteur :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-354">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="7cfe2-355">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-355">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-356">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-356">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-357">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-357">Connectors</span></span> | <span data-ttu-id="7cfe2-358">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-358">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-359">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-359">✔</span></span> | <span data-ttu-id="7cfe2-360">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-360">✔</span></span> | <span data-ttu-id="7cfe2-361">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-361">✔</span></span> | <span data-ttu-id="7cfe2-362">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-362">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="7cfe2-363">Propriétés de la carte Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="7cfe2-363">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="7cfe2-364">Le tableau suivant fournit les propriétés de la carte Office 365 connecteur :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-364">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="7cfe2-365">Propriété</span><span class="sxs-lookup"><span data-stu-id="7cfe2-365">Property</span></span> | <span data-ttu-id="7cfe2-366">Type</span><span class="sxs-lookup"><span data-stu-id="7cfe2-366">Type</span></span>  | <span data-ttu-id="7cfe2-367">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-367">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cfe2-368">title</span><span class="sxs-lookup"><span data-stu-id="7cfe2-368">title</span></span> | <span data-ttu-id="7cfe2-369">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-369">Rich text</span></span> | <span data-ttu-id="7cfe2-370">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-370">Title of the card.</span></span> <span data-ttu-id="7cfe2-371">Deux lignes au maximum.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-371">Maximum two lines.</span></span> |
| <span data-ttu-id="7cfe2-372">résumé</span><span class="sxs-lookup"><span data-stu-id="7cfe2-372">summary</span></span> | <span data-ttu-id="7cfe2-373">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-373">Rich text</span></span> | <span data-ttu-id="7cfe2-374">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-374">Summary of the card.</span></span> <span data-ttu-id="7cfe2-375">Deux lignes au maximum.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-375">Maximum two lines.</span></span> |
| <span data-ttu-id="7cfe2-376">text</span><span class="sxs-lookup"><span data-stu-id="7cfe2-376">text</span></span> | <span data-ttu-id="7cfe2-377">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-377">Rich text</span></span> | <span data-ttu-id="7cfe2-378">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-378">Text appears under the subtitle.</span></span> <span data-ttu-id="7cfe2-379">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-379">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="7cfe2-380">themeColor</span><span class="sxs-lookup"><span data-stu-id="7cfe2-380">themeColor</span></span> | <span data-ttu-id="7cfe2-381">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="7cfe2-381">HEX string</span></span> | <span data-ttu-id="7cfe2-382">Couleur qui remplace la couleur `accentColor` fournie à partir du manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-382">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="7cfe2-383">Informations supplémentaires sur la carte Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="7cfe2-383">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="7cfe2-384">Office 365 Les cartes de connecteur fonctionnent correctement Microsoft Teams, y compris les [ `ActionCard` actions.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-384">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="7cfe2-385">La différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-385">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="7cfe2-386">Le tableau suivant répertorie la différence :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-386">The following table lists the difference:</span></span>

| <span data-ttu-id="7cfe2-387">Connector</span><span class="sxs-lookup"><span data-stu-id="7cfe2-387">Connector</span></span> | <span data-ttu-id="7cfe2-388">Bot</span><span class="sxs-lookup"><span data-stu-id="7cfe2-388">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="7cfe2-389">Le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-389">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="7cfe2-390">`HttpPOST`L’action déclenche une activité qui envoie uniquement l’ID d’action et le `invoke` corps au bot.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-390">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="7cfe2-391">Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-391">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="7cfe2-392">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-392">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="7cfe2-393">Tous les champs de texte sont en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-393">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="7cfe2-394">Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-394">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="7cfe2-395">Par défaut, `markdown` est définie sur `true` .</span><span class="sxs-lookup"><span data-stu-id="7cfe2-395">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="7cfe2-396">Si vous souhaitez utiliser du code HTML à la place, définissez `markdown` sur `false` .</span><span class="sxs-lookup"><span data-stu-id="7cfe2-396">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="7cfe2-397">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-397">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="7cfe2-398">Pour spécifier le style de rendu pour , vous pouvez définir `activityImage` comme indiqué dans le tableau suivant `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-398">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="7cfe2-399">Valeur</span><span class="sxs-lookup"><span data-stu-id="7cfe2-399">Value</span></span> | <span data-ttu-id="7cfe2-400">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-400">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="7cfe2-401">Par défaut, `activityImage` il est rogcé sous la mesure d’un cercle.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-401">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="7cfe2-402">`activityImage` s’affiche sous la forme d’un rectangle et conserve ses proportions.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-402">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="7cfe2-403">Pour plus d’informations sur les propriétés de carte de connecteur, voir la [référence de carte de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-403">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="7cfe2-404">Les seules propriétés de carte de connecteur non Teams actuellement prise en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-404">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="7cfe2-405">`startGroup`toujours traité comme dans `true` Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-405">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="7cfe2-406">Exemple de carte Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="7cfe2-406">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="7cfe2-407">Le code suivant montre un exemple de carte Office 365 connecteur :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-407">The following code shows an example of an Office 365 Connector card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a><span data-ttu-id="7cfe2-408">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="7cfe2-408">Receipt card</span></span>

<span data-ttu-id="7cfe2-409">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-409">Teams supports receipt card.</span></span> <span data-ttu-id="7cfe2-410">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-410">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="7cfe2-411">Elle contient généralement la liste des éléments à inclure sur le reçu, telles que les taxes et le total des informations.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-411">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="7cfe2-412">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="7cfe2-412">Support for receipt cards</span></span>

<span data-ttu-id="7cfe2-413">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de réception :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-413">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="7cfe2-414">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-414">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-415">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-415">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-416">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-416">Connectors</span></span> | <span data-ttu-id="7cfe2-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-418">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-418">✔</span></span> | <span data-ttu-id="7cfe2-419">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-419">✔</span></span> | <span data-ttu-id="7cfe2-420">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-420">✖</span></span> | <span data-ttu-id="7cfe2-421">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-421">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="7cfe2-422">Exemple de carte de reçu</span><span class="sxs-lookup"><span data-stu-id="7cfe2-422">Example of a receipt card</span></span>

![Exemple de carte de reçu](~/assets/images/cards/receipt.png)

<span data-ttu-id="7cfe2-424">Le code suivant montre un exemple de carte de reçu :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-424">The following code shows an example of a receipt card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="7cfe2-425">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="7cfe2-425">Additional information on receipt cards</span></span>

<span data-ttu-id="7cfe2-426">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-426">Bot Framework reference:</span></span>

* [<span data-ttu-id="7cfe2-427">Carte de réception Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfe2-427">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="7cfe2-428">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="7cfe2-428">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="7cfe2-429">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-429">Signin card</span></span>

<span data-ttu-id="7cfe2-430">La carte de Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de Teams ne prend en charge que deux actions `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="7cfe2-430">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="7cfe2-431">L’action de signin peut être utilisée à partir de n’importe quelle carte Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-431">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="7cfe2-432">Pour plus d’informations, [Teams flux d’authentification pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-432">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="7cfe2-433">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-433">Support for signin cards</span></span>

<span data-ttu-id="7cfe2-434">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de signature :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-434">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="7cfe2-435">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-435">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-436">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-436">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-437">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-437">Connectors</span></span> | <span data-ttu-id="7cfe2-438">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-438">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-439">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-439">✔</span></span> | <span data-ttu-id="7cfe2-440">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-440">✖</span></span> | <span data-ttu-id="7cfe2-441">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-441">✖</span></span> | <span data-ttu-id="7cfe2-442">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-442">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="7cfe2-443">Informations supplémentaires sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-443">Additional information on signin cards</span></span>

<span data-ttu-id="7cfe2-444">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-444">Bot Framework reference:</span></span>

* [<span data-ttu-id="7cfe2-445">Carte de Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfe2-445">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="7cfe2-446">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="7cfe2-446">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="7cfe2-447">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-447">Thumbnail card</span></span>

<span data-ttu-id="7cfe2-448">Vous pouvez utiliser une carte miniature utilisée pour envoyer un message actionnable simple.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-448">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="7cfe2-449">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-449">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="7cfe2-450">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="7cfe2-450">Support for thumbnail cards</span></span>

<span data-ttu-id="7cfe2-451">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes miniatures :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-451">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="7cfe2-452">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-452">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-453">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-453">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-454">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-454">Connectors</span></span> | <span data-ttu-id="7cfe2-455">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-455">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-456">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-456">✔</span></span> | <span data-ttu-id="7cfe2-457">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-457">✔</span></span> | <span data-ttu-id="7cfe2-458">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-458">✖</span></span> | <span data-ttu-id="7cfe2-459">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-459">✔</span></span> |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="7cfe2-461">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-461">Properties of a thumbnail card</span></span>

<span data-ttu-id="7cfe2-462">Le tableau suivant fournit les propriétés d’une carte miniature :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-462">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="7cfe2-463">Propriété</span><span class="sxs-lookup"><span data-stu-id="7cfe2-463">Property</span></span> | <span data-ttu-id="7cfe2-464">Type</span><span class="sxs-lookup"><span data-stu-id="7cfe2-464">Type</span></span>  | <span data-ttu-id="7cfe2-465">Description</span><span class="sxs-lookup"><span data-stu-id="7cfe2-465">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cfe2-466">title</span><span class="sxs-lookup"><span data-stu-id="7cfe2-466">title</span></span> | <span data-ttu-id="7cfe2-467">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-467">Rich text</span></span> | <span data-ttu-id="7cfe2-468">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-468">Title of the card.</span></span> <span data-ttu-id="7cfe2-469">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-469">Maximum 2 lines.</span></span>|
| <span data-ttu-id="7cfe2-470">subtitle</span><span class="sxs-lookup"><span data-stu-id="7cfe2-470">subtitle</span></span> | <span data-ttu-id="7cfe2-471">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-471">Rich text</span></span> | <span data-ttu-id="7cfe2-472">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-472">Subtitle of the card.</span></span> <span data-ttu-id="7cfe2-473">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-473">Maximum 2 lines.</span></span>|
| <span data-ttu-id="7cfe2-474">text</span><span class="sxs-lookup"><span data-stu-id="7cfe2-474">text</span></span> | <span data-ttu-id="7cfe2-475">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7cfe2-475">Rich text</span></span> | <span data-ttu-id="7cfe2-476">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-476">Text appears under the subtitle.</span></span> <span data-ttu-id="7cfe2-477">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="7cfe2-477">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="7cfe2-478">images</span><span class="sxs-lookup"><span data-stu-id="7cfe2-478">images</span></span> | <span data-ttu-id="7cfe2-479">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="7cfe2-479">Array of images</span></span> | <span data-ttu-id="7cfe2-480">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-480">Image displayed at the top of the card.</span></span> <span data-ttu-id="7cfe2-481">Proportions 1:1 carré.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-481">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="7cfe2-482">buttons</span><span class="sxs-lookup"><span data-stu-id="7cfe2-482">buttons</span></span> | <span data-ttu-id="7cfe2-483">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="7cfe2-483">Array of action objects</span></span> | <span data-ttu-id="7cfe2-484">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-484">Set of actions applicable to the current card.</span></span> <span data-ttu-id="7cfe2-485">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-485">Maximum 6.</span></span> |
| <span data-ttu-id="7cfe2-486">tap</span><span class="sxs-lookup"><span data-stu-id="7cfe2-486">tap</span></span> | <span data-ttu-id="7cfe2-487">Objet Action</span><span class="sxs-lookup"><span data-stu-id="7cfe2-487">Action object</span></span> | <span data-ttu-id="7cfe2-488">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-488">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="7cfe2-489">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="7cfe2-489">Example of a thumbnail card</span></span>

<span data-ttu-id="7cfe2-490">Le code suivant montre un exemple de carte miniature :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-490">The following code shows an example of a thumbnail card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="additional-information"></a><span data-ttu-id="7cfe2-491">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7cfe2-491">Additional information</span></span>

<span data-ttu-id="7cfe2-492">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-492">Bot Framework reference:</span></span>

* [<span data-ttu-id="7cfe2-493">Carte miniature Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfe2-493">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="7cfe2-494">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="7cfe2-494">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="7cfe2-495">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-495">Card collections</span></span>

<span data-ttu-id="7cfe2-496">Vous pouvez utiliser des collections de cartes qui incluent des collections de carrousels et de listes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-496">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="7cfe2-497">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-497">Teams supports card collections.</span></span> <span data-ttu-id="7cfe2-498">Les collections de cartes incluent `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="7cfe2-498">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="7cfe2-499">Ces collections contiennent des cartes adaptatives, hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-499">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="7cfe2-500">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="7cfe2-500">Carousel collection</span></span>

<span data-ttu-id="7cfe2-501">La [disposition de carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) présente un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-501">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="7cfe2-502">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="7cfe2-502">Support for carousel collections</span></span>

<span data-ttu-id="7cfe2-503">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des collections de carrousels :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-503">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="7cfe2-504">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-504">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-505">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-505">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-506">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-506">Connectors</span></span> | <span data-ttu-id="7cfe2-507">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-507">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-508">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-508">✔</span></span> | <span data-ttu-id="7cfe2-509">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-509">✖</span></span> | <span data-ttu-id="7cfe2-510">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-510">✖</span></span> | <span data-ttu-id="7cfe2-511">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-511">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="7cfe2-512">Un carrousel peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-512">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="7cfe2-513">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="7cfe2-513">Properties of a carousel card</span></span>

<span data-ttu-id="7cfe2-514">Les propriétés d’une carte carrousel sont identiques aux cartes hero et miniatures.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-514">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="7cfe2-515">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="7cfe2-515">Example of a carousel collection</span></span>

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

<span data-ttu-id="7cfe2-517">Le code suivant montre un exemple de collection de carrousels :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-517">The following code shows an example of a carousel collection:</span></span>

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="7cfe2-518">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="7cfe2-518">Syntax for carousel collections</span></span>

<span data-ttu-id="7cfe2-519">`builder.AttachmentLayoutTypes.Carousel` est la syntaxe des collections de carrousels.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-519">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="7cfe2-520">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-520">List collection</span></span>

<span data-ttu-id="7cfe2-521">La disposition de liste affiche une liste de cartes empilées verticalement, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-521">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="7cfe2-522">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-522">Support for list collections</span></span>

<span data-ttu-id="7cfe2-523">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des collections de listes :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-523">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="7cfe2-524">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-524">Bots in Teams</span></span> | <span data-ttu-id="7cfe2-525">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7cfe2-525">Messaging extensions</span></span>  | <span data-ttu-id="7cfe2-526">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7cfe2-526">Connectors</span></span> | <span data-ttu-id="7cfe2-527">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="7cfe2-527">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7cfe2-528">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-528">✔</span></span> | <span data-ttu-id="7cfe2-529">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-529">✔</span></span> | <span data-ttu-id="7cfe2-530">✖</span><span class="sxs-lookup"><span data-stu-id="7cfe2-530">✖</span></span> | <span data-ttu-id="7cfe2-531">✔</span><span class="sxs-lookup"><span data-stu-id="7cfe2-531">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="7cfe2-532">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-532">Example of a list collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="7cfe2-534">Les propriétés des collections de listes sont identiques aux cartes hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-534">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="7cfe2-535">Une liste peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-535">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="7cfe2-536">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-536">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="7cfe2-537">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-537">Syntax for list collections</span></span>

<span data-ttu-id="7cfe2-538">`builder.AttachmentLayout.list` est la syntaxe des collections de listes.</span><span class="sxs-lookup"><span data-stu-id="7cfe2-538">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="7cfe2-539">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="7cfe2-539">Cards not supported in Teams</span></span>

<span data-ttu-id="7cfe2-540">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas Teams :</span><span class="sxs-lookup"><span data-stu-id="7cfe2-540">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="7cfe2-541">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="7cfe2-541">Animation cards</span></span>
* <span data-ttu-id="7cfe2-542">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="7cfe2-542">Audio cards</span></span>
* <span data-ttu-id="7cfe2-543">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="7cfe2-543">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="7cfe2-544">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7cfe2-544">See also</span></span>

* [<span data-ttu-id="7cfe2-545">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="7cfe2-545">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="7cfe2-546">Format des cartes</span><span class="sxs-lookup"><span data-stu-id="7cfe2-546">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
