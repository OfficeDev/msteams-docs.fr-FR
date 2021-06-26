---
title: Types de cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
localization_priority: Normal
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: be38454daac519530d0fdf10b5170e128219f6fc
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140486"
---
# <a name="types-of-cards"></a><span data-ttu-id="36f58-104">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="36f58-104">Types of cards</span></span>

<span data-ttu-id="36f58-105">Les cartes adaptatives, hero, list, Office 365 Connector, les cartes de réception, les cartes de connexion et les collections de cartes miniatures sont pris en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="36f58-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="36f58-106">Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="36f58-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="36f58-107">Avant d’identifier les différents types de carte, comprenez comment créer une carte hero, une carte miniature ou une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="36f58-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="36f58-108">Créer une carte Hero, une carte miniature ou une carte adaptative</span><span class="sxs-lookup"><span data-stu-id="36f58-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="36f58-109">**Pour créer une carte Hero, une carte miniature ou une carte adaptative à partir d’App Studio**</span><span class="sxs-lookup"><span data-stu-id="36f58-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="36f58-110">Go to **App Studio** from Teams.</span><span class="sxs-lookup"><span data-stu-id="36f58-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="36f58-111">Sélectionnez **l’éditeur de carte.**</span><span class="sxs-lookup"><span data-stu-id="36f58-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="36f58-112">Sélectionnez **Créer une carte.**</span><span class="sxs-lookup"><span data-stu-id="36f58-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="36f58-113">Sélectionnez **Créer** pour l’une des cartes **de la carte Hero,** de la carte **miniature** ou de la **carte adaptative.**</span><span class="sxs-lookup"><span data-stu-id="36f58-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="36f58-114">Les exemples de code de métadonnées, boutons et json, csharp et nœud sont présentés pour cette carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Détails de la carte Hero](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="36f58-116">Sélectionnez **M’envoyer cette carte.**</span><span class="sxs-lookup"><span data-stu-id="36f58-116">Select **Send me this card**.</span></span> <span data-ttu-id="36f58-117">La carte vous est envoyée en tant que message de conversation.</span><span class="sxs-lookup"><span data-stu-id="36f58-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="36f58-118">Exemples de cartes</span><span class="sxs-lookup"><span data-stu-id="36f58-118">Card examples</span></span>

<span data-ttu-id="36f58-119">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="36f58-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="36f58-120">Des exemples de code sont également disponibles dans le référentiel **Microsoft/BotBuilder-Samples** GitHub.</span><span class="sxs-lookup"><span data-stu-id="36f58-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="36f58-121">Voici quelques exemples de cartes :</span><span class="sxs-lookup"><span data-stu-id="36f58-121">Following are a few card examples:</span></span>

* <span data-ttu-id="36f58-122">.NET</span><span class="sxs-lookup"><span data-stu-id="36f58-122">.NET</span></span>
  * <span data-ttu-id="36f58-123">[Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="36f58-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="36f58-124">[Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="36f58-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="36f58-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="36f58-125">Node.js</span></span>
  * <span data-ttu-id="36f58-126">[Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="36f58-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="36f58-127">[Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="36f58-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="36f58-128">Types de carte</span><span class="sxs-lookup"><span data-stu-id="36f58-128">Card types</span></span>

<span data-ttu-id="36f58-129">Vous pouvez identifier et utiliser différents types de cartes en fonction des besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="36f58-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="36f58-130">Le tableau suivant indique les types de cartes disponibles :</span><span class="sxs-lookup"><span data-stu-id="36f58-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="36f58-131">Type de carte</span><span class="sxs-lookup"><span data-stu-id="36f58-131">Card type</span></span> | <span data-ttu-id="36f58-132">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="36f58-133">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="36f58-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="36f58-134">Cette carte est hautement personnalisable et peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="36f58-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="36f58-135">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="36f58-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="36f58-136">Cette carte contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="36f58-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="36f58-137">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="36f58-137">List card</span></span>](#list-card) | <span data-ttu-id="36f58-138">Cette carte contient une liste de défilement d’éléments.</span><span class="sxs-lookup"><span data-stu-id="36f58-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="36f58-139">Office 365 Carte de connecteur</span><span class="sxs-lookup"><span data-stu-id="36f58-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="36f58-140">Cette carte possède une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="36f58-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="36f58-141">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="36f58-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="36f58-142">Cette carte fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="36f58-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="36f58-143">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="36f58-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="36f58-144">Cette carte permet à un bot de demander à un utilisateur de se rendre.</span><span class="sxs-lookup"><span data-stu-id="36f58-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="36f58-145">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="36f58-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="36f58-146">Cette carte contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="36f58-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="36f58-147">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="36f58-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="36f58-148">Cette collection de cartes est utilisée pour renvoyer plusieurs éléments en une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="36f58-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="36f58-149">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="36f58-149">Common properties for all cards</span></span>

<span data-ttu-id="36f58-150">Vous pouvez passer par certaines propriétés communes applicables à toutes les cartes.</span><span class="sxs-lookup"><span data-stu-id="36f58-150">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="36f58-151">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="36f58-151">Inline card images</span></span>

<span data-ttu-id="36f58-152">La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="36f58-152">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="36f58-153">Pour des raisons de performances, il est vivement recommandé d’héberger l’image sur une réseau de distribution de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="36f58-153">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="36f58-154">La taille des images est réduite ou réduite afin de maintenir les proportions pour couvrir la zone d’image.</span><span class="sxs-lookup"><span data-stu-id="36f58-154">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="36f58-155">Les images sont ensuite rogées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-155">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="36f58-156">Les images doivent être au maximum 1024×1024 et au format PNG, JPEG ou GIF.</span><span class="sxs-lookup"><span data-stu-id="36f58-156">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="36f58-157">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="36f58-157">Animated GIF is not supported.</span></span>

<span data-ttu-id="36f58-158">Le tableau suivant fournit les propriétés des images de carte en ligne :</span><span class="sxs-lookup"><span data-stu-id="36f58-158">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="36f58-159">Propriété</span><span class="sxs-lookup"><span data-stu-id="36f58-159">Property</span></span> | <span data-ttu-id="36f58-160">Type</span><span class="sxs-lookup"><span data-stu-id="36f58-160">Type</span></span>  | <span data-ttu-id="36f58-161">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36f58-162">url</span><span class="sxs-lookup"><span data-stu-id="36f58-162">url</span></span> | <span data-ttu-id="36f58-163">URL</span><span class="sxs-lookup"><span data-stu-id="36f58-163">URL</span></span> | <span data-ttu-id="36f58-164">URL HTTPS vers l’image.</span><span class="sxs-lookup"><span data-stu-id="36f58-164">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="36f58-165">alt</span><span class="sxs-lookup"><span data-stu-id="36f58-165">alt</span></span> | <span data-ttu-id="36f58-166">String</span><span class="sxs-lookup"><span data-stu-id="36f58-166">String</span></span> | <span data-ttu-id="36f58-167">Description accessible de l’image.</span><span class="sxs-lookup"><span data-stu-id="36f58-167">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="36f58-168">Si une carte inclut une URL d’image qui est redirigée avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="36f58-168">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="36f58-169">Cela se produit pour les images partagées sur le cloud public.</span><span class="sxs-lookup"><span data-stu-id="36f58-169">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="36f58-170">Boutons</span><span class="sxs-lookup"><span data-stu-id="36f58-170">Buttons</span></span>

<span data-ttu-id="36f58-171">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-171">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="36f58-172">Le texte du bouton est toujours sur une seule ligne et tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="36f58-172">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="36f58-173">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne sont pas affichés.</span><span class="sxs-lookup"><span data-stu-id="36f58-173">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="36f58-174">Pour plus d’informations, voir [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="36f58-174">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="36f58-175">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="36f58-175">Card formatting</span></span>

<span data-ttu-id="36f58-176">Pour plus d’informations sur la mise en forme du texte dans les cartes, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="36f58-176">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="36f58-177">Après avoir identifié les propriétés communes de toutes les cartes, vous pouvez désormais utiliser des cartes adaptatives, ce qui vous permet d’augmenter l’engagement et l’efficacité en ajoutant votre contenu actionnable directement dans les applications que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="36f58-177">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="36f58-178">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="36f58-178">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="36f58-179">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="36f58-179">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="36f58-180">Pour plus d’informations, voir [Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="36f58-180">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="36f58-181">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="36f58-181">Support for Adaptive Cards</span></span>

<span data-ttu-id="36f58-182">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="36f58-182">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="36f58-183">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-183">Bots in Teams</span></span> | <span data-ttu-id="36f58-184">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-184">Messaging extensions</span></span>  | <span data-ttu-id="36f58-185">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-185">Connectors</span></span> | <span data-ttu-id="36f58-186">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-186">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-187">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-187">✔</span></span> | <span data-ttu-id="36f58-188">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-188">✔</span></span> | <span data-ttu-id="36f58-189">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-189">✖</span></span> | <span data-ttu-id="36f58-190">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-190">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="36f58-191">Teams plateforme prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="36f58-191">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="36f58-192">Le style d’action positive ou destructive n’est pas pris en charge dans les cartes adaptatives sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="36f58-192">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="36f58-193">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="36f58-193">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="36f58-194">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="36f58-194">Example of Adaptive Card</span></span>

![Exemple de carte adaptative](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="36f58-196">Le code suivant illustre un exemple de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="36f58-196">The following code shows an example of an Adaptive Card:</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="36f58-197">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="36f58-197">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="36f58-198">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="36f58-198">Bot Framework reference:</span></span>

* [<span data-ttu-id="36f58-199">Nœud cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="36f58-199">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="36f58-200">Carte adaptative C #</span><span class="sxs-lookup"><span data-stu-id="36f58-200">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="36f58-201">Vous pouvez désormais utiliser une carte Hero, qui est une carte multi-usage utilisée pour mettre en évidence visuellement une sélection d’utilisateur potentielle.</span><span class="sxs-lookup"><span data-stu-id="36f58-201">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="36f58-202">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="36f58-202">Hero card</span></span>

<span data-ttu-id="36f58-203">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="36f58-203">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="36f58-204">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="36f58-204">Support for hero cards</span></span>

<span data-ttu-id="36f58-205">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes Hero :</span><span class="sxs-lookup"><span data-stu-id="36f58-205">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="36f58-206">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-206">Bots in Teams</span></span> | <span data-ttu-id="36f58-207">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-207">Messaging extensions</span></span>  | <span data-ttu-id="36f58-208">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-208">Connectors</span></span> | <span data-ttu-id="36f58-209">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-209">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-210">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-210">✔</span></span> | <span data-ttu-id="36f58-211">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-211">✔</span></span> | <span data-ttu-id="36f58-212">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-212">✖</span></span> | <span data-ttu-id="36f58-213">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-213">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="36f58-214">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="36f58-214">Properties of a hero card</span></span>

<span data-ttu-id="36f58-215">Le tableau suivant fournit les propriétés d’une carte Hero :</span><span class="sxs-lookup"><span data-stu-id="36f58-215">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="36f58-216">Propriété</span><span class="sxs-lookup"><span data-stu-id="36f58-216">Property</span></span> | <span data-ttu-id="36f58-217">Type</span><span class="sxs-lookup"><span data-stu-id="36f58-217">Type</span></span>  | <span data-ttu-id="36f58-218">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36f58-219">title</span><span class="sxs-lookup"><span data-stu-id="36f58-219">title</span></span> | <span data-ttu-id="36f58-220">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-220">Rich text</span></span> | <span data-ttu-id="36f58-221">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-221">Title of the card.</span></span> <span data-ttu-id="36f58-222">Maximum deux lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-222">Maximum two lines.</span></span> |
| <span data-ttu-id="36f58-223">subtitle</span><span class="sxs-lookup"><span data-stu-id="36f58-223">subtitle</span></span> | <span data-ttu-id="36f58-224">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-224">Rich text</span></span> | <span data-ttu-id="36f58-225">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-225">Subtitle of the card.</span></span> <span data-ttu-id="36f58-226">Maximum deux lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-226">Maximum two lines.</span></span>|
| <span data-ttu-id="36f58-227">text</span><span class="sxs-lookup"><span data-stu-id="36f58-227">text</span></span> | <span data-ttu-id="36f58-228">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-228">Rich text</span></span> | <span data-ttu-id="36f58-229">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="36f58-229">Text appears under the subtitle.</span></span> <span data-ttu-id="36f58-230">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="36f58-230">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="36f58-231">images</span><span class="sxs-lookup"><span data-stu-id="36f58-231">images</span></span> | <span data-ttu-id="36f58-232">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="36f58-232">Array of images</span></span> | <span data-ttu-id="36f58-233">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-233">Image displayed at the top of the card.</span></span> <span data-ttu-id="36f58-234">Proportions 16:9.</span><span class="sxs-lookup"><span data-stu-id="36f58-234">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="36f58-235">buttons</span><span class="sxs-lookup"><span data-stu-id="36f58-235">buttons</span></span> | <span data-ttu-id="36f58-236">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="36f58-236">Array of action objects</span></span> | <span data-ttu-id="36f58-237">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="36f58-237">Set of actions applicable to the current card.</span></span> <span data-ttu-id="36f58-238">Six maximum.</span><span class="sxs-lookup"><span data-stu-id="36f58-238">Maximum six.</span></span> |
| <span data-ttu-id="36f58-239">tap</span><span class="sxs-lookup"><span data-stu-id="36f58-239">tap</span></span> | <span data-ttu-id="36f58-240">Objet Action</span><span class="sxs-lookup"><span data-stu-id="36f58-240">Action object</span></span> | <span data-ttu-id="36f58-241">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="36f58-241">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="36f58-242">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="36f58-242">Example of a hero card</span></span>

![Exemple de carte Hero](~/assets/images/cards/hero.png)

<span data-ttu-id="36f58-244">Le code suivant montre un exemple de carte Hero :</span><span class="sxs-lookup"><span data-stu-id="36f58-244">The following code shows an example of a hero card:</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="36f58-245">Informations supplémentaires sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="36f58-245">Additional information on hero cards</span></span>

<span data-ttu-id="36f58-246">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="36f58-246">Bot Framework reference:</span></span>

* [<span data-ttu-id="36f58-247">Carte Hero Node.js</span><span class="sxs-lookup"><span data-stu-id="36f58-247">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="36f58-248">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="36f58-248">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="36f58-249">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="36f58-249">List card</span></span>

<span data-ttu-id="36f58-250">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="36f58-250">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="36f58-251">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="36f58-251">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="36f58-252">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="36f58-252">Support for list cards</span></span>

<span data-ttu-id="36f58-253">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de liste :</span><span class="sxs-lookup"><span data-stu-id="36f58-253">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="36f58-254">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-254">Bots in Teams</span></span> | <span data-ttu-id="36f58-255">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-255">Messaging extensions</span></span>  | <span data-ttu-id="36f58-256">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-256">Connectors</span></span> | <span data-ttu-id="36f58-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-258">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-258">✔</span></span> | <span data-ttu-id="36f58-259">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-259">✖</span></span> | <span data-ttu-id="36f58-260">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-260">✖</span></span> |<span data-ttu-id="36f58-261">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-261">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="36f58-262">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="36f58-262">Properties of a list card</span></span>

<span data-ttu-id="36f58-263">Le tableau suivant fournit les propriétés d’une carte de liste :</span><span class="sxs-lookup"><span data-stu-id="36f58-263">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="36f58-264">Propriété</span><span class="sxs-lookup"><span data-stu-id="36f58-264">Property</span></span> | <span data-ttu-id="36f58-265">Type</span><span class="sxs-lookup"><span data-stu-id="36f58-265">Type</span></span>  | <span data-ttu-id="36f58-266">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36f58-267">title</span><span class="sxs-lookup"><span data-stu-id="36f58-267">title</span></span> | <span data-ttu-id="36f58-268">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-268">Rich text</span></span> | <span data-ttu-id="36f58-269">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-269">Title of the card.</span></span> <span data-ttu-id="36f58-270">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-270">Maximum 2 lines.</span></span>|
| <span data-ttu-id="36f58-271">éléments</span><span class="sxs-lookup"><span data-stu-id="36f58-271">items</span></span> | <span data-ttu-id="36f58-272">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="36f58-272">Array of list items</span></span> | <span data-ttu-id="36f58-273">Ensemble d’éléments applicables à la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-273">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="36f58-274">buttons</span><span class="sxs-lookup"><span data-stu-id="36f58-274">buttons</span></span> | <span data-ttu-id="36f58-275">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="36f58-275">Array of action objects</span></span> | <span data-ttu-id="36f58-276">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="36f58-276">Set of actions applicable to the current card.</span></span> <span data-ttu-id="36f58-277">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="36f58-277">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="36f58-278">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="36f58-278">Example of a list card</span></span>

<span data-ttu-id="36f58-279">Le code suivant montre un exemple de carte de liste :</span><span class="sxs-lookup"><span data-stu-id="36f58-279">The following code shows an example of a list card:</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="36f58-280">carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="36f58-280">Office 365 connector card</span></span>

<span data-ttu-id="36f58-281">Vous pouvez utiliser une carte connecteur Office 365 qui fournit une disposition flexible et constitue un excellent moyen d’obtenir des informations utiles.</span><span class="sxs-lookup"><span data-stu-id="36f58-281">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="36f58-282">La carte Office 365 connecteur est prise en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="36f58-282">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="36f58-283">Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="36f58-283">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="36f58-284">Cette carte contient une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="36f58-284">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="36f58-285">Pour plus d’informations sur les différences entre les cartes de connecteur et la carte connecteur Office 365, consultez des informations supplémentaires [sur la carte Office 365 connecteur.](#additional-information-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="36f58-285">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="36f58-286">Prise en charge des cartes Office 365 connecteur de connexion</span><span class="sxs-lookup"><span data-stu-id="36f58-286">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="36f58-287">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge Office 365 cartes de connecteur :</span><span class="sxs-lookup"><span data-stu-id="36f58-287">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="36f58-288">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-288">Bots in Teams</span></span> | <span data-ttu-id="36f58-289">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-289">Messaging extensions</span></span>  | <span data-ttu-id="36f58-290">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-290">Connectors</span></span> | <span data-ttu-id="36f58-291">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-291">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-292">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-292">✔</span></span> | <span data-ttu-id="36f58-293">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-293">✔</span></span> | <span data-ttu-id="36f58-294">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-294">✔</span></span> | <span data-ttu-id="36f58-295">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-295">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="36f58-296">Propriétés de la carte Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="36f58-296">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="36f58-297">Le tableau suivant fournit les propriétés de la carte Office 365 connecteur :</span><span class="sxs-lookup"><span data-stu-id="36f58-297">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="36f58-298">Propriété</span><span class="sxs-lookup"><span data-stu-id="36f58-298">Property</span></span> | <span data-ttu-id="36f58-299">Type</span><span class="sxs-lookup"><span data-stu-id="36f58-299">Type</span></span>  | <span data-ttu-id="36f58-300">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-300">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36f58-301">title</span><span class="sxs-lookup"><span data-stu-id="36f58-301">title</span></span> | <span data-ttu-id="36f58-302">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-302">Rich text</span></span> | <span data-ttu-id="36f58-303">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-303">Title of the card.</span></span> <span data-ttu-id="36f58-304">Maximum deux lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-304">Maximum two lines.</span></span> |
| <span data-ttu-id="36f58-305">résumé</span><span class="sxs-lookup"><span data-stu-id="36f58-305">summary</span></span> | <span data-ttu-id="36f58-306">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-306">Rich text</span></span> | <span data-ttu-id="36f58-307">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-307">Summary of the card.</span></span> <span data-ttu-id="36f58-308">Maximum deux lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-308">Maximum two lines.</span></span> |
| <span data-ttu-id="36f58-309">text</span><span class="sxs-lookup"><span data-stu-id="36f58-309">text</span></span> | <span data-ttu-id="36f58-310">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-310">Rich text</span></span> | <span data-ttu-id="36f58-311">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="36f58-311">Text appears under the subtitle.</span></span> <span data-ttu-id="36f58-312">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="36f58-312">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="36f58-313">themeColor</span><span class="sxs-lookup"><span data-stu-id="36f58-313">themeColor</span></span> | <span data-ttu-id="36f58-314">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="36f58-314">HEX string</span></span> | <span data-ttu-id="36f58-315">Couleur qui remplace la couleur `accentColor` fournie à partir du manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="36f58-315">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="36f58-316">Informations supplémentaires sur la carte Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="36f58-316">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="36f58-317">Office 365 Les cartes de connecteur fonctionnent correctement Microsoft Teams, y compris les [ `ActionCard` actions.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="36f58-317">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="36f58-318">La différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-318">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="36f58-319">Le tableau suivant répertorie la différence :</span><span class="sxs-lookup"><span data-stu-id="36f58-319">The following table lists the difference:</span></span>

| <span data-ttu-id="36f58-320">Connecteur</span><span class="sxs-lookup"><span data-stu-id="36f58-320">Connector</span></span> | <span data-ttu-id="36f58-321">Bot</span><span class="sxs-lookup"><span data-stu-id="36f58-321">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="36f58-322">Le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="36f58-322">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="36f58-323">`HttpPOST`L’action déclenche une activité qui envoie uniquement `invoke` l’ID d’action et le corps au bot.</span><span class="sxs-lookup"><span data-stu-id="36f58-323">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="36f58-324">Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.</span><span class="sxs-lookup"><span data-stu-id="36f58-324">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="36f58-325">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="36f58-325">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="36f58-326">Tous les champs de texte sont en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="36f58-326">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="36f58-327">Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant `markdown` la propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="36f58-327">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="36f58-328">Par défaut, `markdown` est définie sur `true` .</span><span class="sxs-lookup"><span data-stu-id="36f58-328">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="36f58-329">Si vous souhaitez utiliser du code HTML à la place, définissez `markdown` sur `false` .</span><span class="sxs-lookup"><span data-stu-id="36f58-329">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="36f58-330">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="36f58-330">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="36f58-331">Pour spécifier le style de rendu pour , vous pouvez définir `activityImage` comme indiqué dans le tableau suivant `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="36f58-331">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="36f58-332">Valeur</span><span class="sxs-lookup"><span data-stu-id="36f58-332">Value</span></span> | <span data-ttu-id="36f58-333">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-333">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="36f58-334">Par défaut, `activityImage` elle est rogcée sous la mesure d’un cercle.</span><span class="sxs-lookup"><span data-stu-id="36f58-334">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="36f58-335">`activityImage` est affiché sous forme de rectangle et conserve ses proportions.</span><span class="sxs-lookup"><span data-stu-id="36f58-335">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="36f58-336">Pour plus d’informations sur les propriétés de carte de connecteur, voir la [référence de carte de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="36f58-336">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="36f58-337">Les seules propriétés de carte de connecteur que Teams ne prend pas en charge actuellement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="36f58-337">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="36f58-338">`startGroup`toujours traité comme dans `true` Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-338">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="36f58-339">Exemple de carte Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="36f58-339">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="36f58-340">Le code suivant montre un exemple de carte Office 365 Connecteur :</span><span class="sxs-lookup"><span data-stu-id="36f58-340">The following code shows an example of an Office 365 Connector card:</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="36f58-341">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="36f58-341">Receipt card</span></span>

<span data-ttu-id="36f58-342">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="36f58-342">Teams supports receipt card.</span></span> <span data-ttu-id="36f58-343">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="36f58-343">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="36f58-344">Elle contient généralement la liste des éléments à inclure sur le reçu, telles que les taxes et le total des informations.</span><span class="sxs-lookup"><span data-stu-id="36f58-344">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="36f58-345">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="36f58-345">Support for receipt cards</span></span>

<span data-ttu-id="36f58-346">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de réception :</span><span class="sxs-lookup"><span data-stu-id="36f58-346">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="36f58-347">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-347">Bots in Teams</span></span> | <span data-ttu-id="36f58-348">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-348">Messaging extensions</span></span>  | <span data-ttu-id="36f58-349">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-349">Connectors</span></span> | <span data-ttu-id="36f58-350">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-350">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-351">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-351">✔</span></span> | <span data-ttu-id="36f58-352">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-352">✔</span></span> | <span data-ttu-id="36f58-353">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-353">✖</span></span> | <span data-ttu-id="36f58-354">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-354">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="36f58-355">Exemple de carte de reçu</span><span class="sxs-lookup"><span data-stu-id="36f58-355">Example of a receipt card</span></span>

![Exemple de carte de reçu](~/assets/images/cards/receipt.png)

<span data-ttu-id="36f58-357">Le code suivant montre un exemple de carte de réception :</span><span class="sxs-lookup"><span data-stu-id="36f58-357">The following code shows an example of a receipt card:</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="36f58-358">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="36f58-358">Additional information on receipt cards</span></span>

<span data-ttu-id="36f58-359">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="36f58-359">Bot Framework reference:</span></span>

* [<span data-ttu-id="36f58-360">Carte de réception Node.js</span><span class="sxs-lookup"><span data-stu-id="36f58-360">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="36f58-361">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="36f58-361">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="36f58-362">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="36f58-362">Signin card</span></span>

<span data-ttu-id="36f58-363">La carte de Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de Teams ne prend en charge que deux actions `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="36f58-363">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="36f58-364">L’action de signin peut être utilisée à partir de n’importe quelle carte de Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="36f58-364">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="36f58-365">Pour plus d’informations, [voir Teams’authentification pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="36f58-365">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="36f58-366">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="36f58-366">Support for signin cards</span></span>

<span data-ttu-id="36f58-367">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de signature :</span><span class="sxs-lookup"><span data-stu-id="36f58-367">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="36f58-368">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-368">Bots in Teams</span></span> | <span data-ttu-id="36f58-369">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-369">Messaging extensions</span></span>  | <span data-ttu-id="36f58-370">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-370">Connectors</span></span> | <span data-ttu-id="36f58-371">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-371">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-372">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-372">✔</span></span> | <span data-ttu-id="36f58-373">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-373">✖</span></span> | <span data-ttu-id="36f58-374">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-374">✖</span></span> | <span data-ttu-id="36f58-375">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-375">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="36f58-376">Informations supplémentaires sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="36f58-376">Additional information on signin cards</span></span>

<span data-ttu-id="36f58-377">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="36f58-377">Bot Framework reference:</span></span>

* [<span data-ttu-id="36f58-378">Carte de Node.js</span><span class="sxs-lookup"><span data-stu-id="36f58-378">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="36f58-379">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="36f58-379">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="36f58-380">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="36f58-380">Thumbnail card</span></span>

<span data-ttu-id="36f58-381">Vous pouvez utiliser une carte miniature utilisée pour envoyer un message actionnable simple.</span><span class="sxs-lookup"><span data-stu-id="36f58-381">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="36f58-382">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="36f58-382">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="36f58-383">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="36f58-383">Support for thumbnail cards</span></span>

<span data-ttu-id="36f58-384">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes miniatures :</span><span class="sxs-lookup"><span data-stu-id="36f58-384">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="36f58-385">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-385">Bots in Teams</span></span> | <span data-ttu-id="36f58-386">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-386">Messaging extensions</span></span>  | <span data-ttu-id="36f58-387">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-387">Connectors</span></span> | <span data-ttu-id="36f58-388">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-389">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-389">✔</span></span> | <span data-ttu-id="36f58-390">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-390">✔</span></span> | <span data-ttu-id="36f58-391">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-391">✖</span></span> | <span data-ttu-id="36f58-392">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-392">✔</span></span> |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="36f58-394">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="36f58-394">Properties of a thumbnail card</span></span>

<span data-ttu-id="36f58-395">Le tableau suivant fournit les propriétés d’une carte miniature :</span><span class="sxs-lookup"><span data-stu-id="36f58-395">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="36f58-396">Propriété</span><span class="sxs-lookup"><span data-stu-id="36f58-396">Property</span></span> | <span data-ttu-id="36f58-397">Type</span><span class="sxs-lookup"><span data-stu-id="36f58-397">Type</span></span>  | <span data-ttu-id="36f58-398">Description</span><span class="sxs-lookup"><span data-stu-id="36f58-398">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36f58-399">title</span><span class="sxs-lookup"><span data-stu-id="36f58-399">title</span></span> | <span data-ttu-id="36f58-400">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-400">Rich text</span></span> | <span data-ttu-id="36f58-401">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-401">Title of the card.</span></span> <span data-ttu-id="36f58-402">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-402">Maximum 2 lines.</span></span>|
| <span data-ttu-id="36f58-403">subtitle</span><span class="sxs-lookup"><span data-stu-id="36f58-403">subtitle</span></span> | <span data-ttu-id="36f58-404">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-404">Rich text</span></span> | <span data-ttu-id="36f58-405">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-405">Subtitle of the card.</span></span> <span data-ttu-id="36f58-406">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="36f58-406">Maximum 2 lines.</span></span>|
| <span data-ttu-id="36f58-407">text</span><span class="sxs-lookup"><span data-stu-id="36f58-407">text</span></span> | <span data-ttu-id="36f58-408">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="36f58-408">Rich text</span></span> | <span data-ttu-id="36f58-409">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="36f58-409">Text appears under the subtitle.</span></span> <span data-ttu-id="36f58-410">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="36f58-410">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="36f58-411">images</span><span class="sxs-lookup"><span data-stu-id="36f58-411">images</span></span> | <span data-ttu-id="36f58-412">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="36f58-412">Array of images</span></span> | <span data-ttu-id="36f58-413">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="36f58-413">Image displayed at the top of the card.</span></span> <span data-ttu-id="36f58-414">Proportions 1:1 carré.</span><span class="sxs-lookup"><span data-stu-id="36f58-414">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="36f58-415">buttons</span><span class="sxs-lookup"><span data-stu-id="36f58-415">buttons</span></span> | <span data-ttu-id="36f58-416">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="36f58-416">Array of action objects</span></span> | <span data-ttu-id="36f58-417">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="36f58-417">Set of actions applicable to the current card.</span></span> <span data-ttu-id="36f58-418">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="36f58-418">Maximum 6.</span></span> |
| <span data-ttu-id="36f58-419">tap</span><span class="sxs-lookup"><span data-stu-id="36f58-419">tap</span></span> | <span data-ttu-id="36f58-420">Objet Action</span><span class="sxs-lookup"><span data-stu-id="36f58-420">Action object</span></span> | <span data-ttu-id="36f58-421">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="36f58-421">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="36f58-422">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="36f58-422">Example of a thumbnail card</span></span>

<span data-ttu-id="36f58-423">Le code suivant montre un exemple de carte miniature :</span><span class="sxs-lookup"><span data-stu-id="36f58-423">The following code shows an example of a thumbnail card:</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="36f58-424">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="36f58-424">Additional information</span></span>

<span data-ttu-id="36f58-425">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="36f58-425">Bot Framework reference:</span></span>

* [<span data-ttu-id="36f58-426">Carte miniature Node.js</span><span class="sxs-lookup"><span data-stu-id="36f58-426">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="36f58-427">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="36f58-427">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="36f58-428">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="36f58-428">Card collections</span></span>

<span data-ttu-id="36f58-429">Vous pouvez utiliser des collections de cartes qui incluent des collections de listes et de carrousels.</span><span class="sxs-lookup"><span data-stu-id="36f58-429">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="36f58-430">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="36f58-430">Teams supports card collections.</span></span> <span data-ttu-id="36f58-431">Les collections de cartes incluent `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="36f58-431">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="36f58-432">Ces collections contiennent des cartes adaptatives, hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="36f58-432">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="36f58-433">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="36f58-433">Carousel collection</span></span>

<span data-ttu-id="36f58-434">La [disposition de carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) présente un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="36f58-434">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="36f58-435">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="36f58-435">Support for carousel collections</span></span>

<span data-ttu-id="36f58-436">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des collections de carrousels :</span><span class="sxs-lookup"><span data-stu-id="36f58-436">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="36f58-437">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-437">Bots in Teams</span></span> | <span data-ttu-id="36f58-438">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-438">Messaging extensions</span></span>  | <span data-ttu-id="36f58-439">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-439">Connectors</span></span> | <span data-ttu-id="36f58-440">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-440">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-441">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-441">✔</span></span> | <span data-ttu-id="36f58-442">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-442">✖</span></span> | <span data-ttu-id="36f58-443">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-443">✖</span></span> | <span data-ttu-id="36f58-444">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-444">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="36f58-445">Un carrousel peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="36f58-445">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="36f58-446">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="36f58-446">Properties of a carousel card</span></span>

<span data-ttu-id="36f58-447">Les propriétés d’une carte carrousel sont identiques aux cartes hero et miniatures.</span><span class="sxs-lookup"><span data-stu-id="36f58-447">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="36f58-448">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="36f58-448">Example of a carousel collection</span></span>

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

<span data-ttu-id="36f58-450">Le code suivant montre un exemple de collection de carrousels :</span><span class="sxs-lookup"><span data-stu-id="36f58-450">The following code shows an example of a carousel collection:</span></span>

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

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="36f58-451">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="36f58-451">Syntax for carousel collections</span></span>

<span data-ttu-id="36f58-452">`builder.AttachmentLayoutTypes.Carousel` est la syntaxe des collections de carrousels.</span><span class="sxs-lookup"><span data-stu-id="36f58-452">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="36f58-453">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="36f58-453">List collection</span></span>

<span data-ttu-id="36f58-454">La disposition de liste affiche une liste de cartes empilées verticalement, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="36f58-454">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="36f58-455">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="36f58-455">Support for list collections</span></span>

<span data-ttu-id="36f58-456">Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des collections de listes :</span><span class="sxs-lookup"><span data-stu-id="36f58-456">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="36f58-457">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-457">Bots in Teams</span></span> | <span data-ttu-id="36f58-458">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="36f58-458">Messaging extensions</span></span>  | <span data-ttu-id="36f58-459">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="36f58-459">Connectors</span></span> | <span data-ttu-id="36f58-460">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36f58-460">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36f58-461">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-461">✔</span></span> | <span data-ttu-id="36f58-462">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-462">✔</span></span> | <span data-ttu-id="36f58-463">✖</span><span class="sxs-lookup"><span data-stu-id="36f58-463">✖</span></span> | <span data-ttu-id="36f58-464">✔</span><span class="sxs-lookup"><span data-stu-id="36f58-464">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="36f58-465">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="36f58-465">Example of a list collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="36f58-467">Les propriétés des collections de listes sont identiques aux cartes hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="36f58-467">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="36f58-468">Une liste peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="36f58-468">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="36f58-469">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="36f58-469">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="36f58-470">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="36f58-470">Syntax for list collections</span></span>

<span data-ttu-id="36f58-471">`builder.AttachmentLayout.list` est la syntaxe des collections de listes.</span><span class="sxs-lookup"><span data-stu-id="36f58-471">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="36f58-472">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="36f58-472">Cards not supported in Teams</span></span>

<span data-ttu-id="36f58-473">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas Teams :</span><span class="sxs-lookup"><span data-stu-id="36f58-473">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="36f58-474">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="36f58-474">Animation cards</span></span>
* <span data-ttu-id="36f58-475">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="36f58-475">Audio cards</span></span>
* <span data-ttu-id="36f58-476">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="36f58-476">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="36f58-477">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="36f58-477">See also</span></span>

* [<span data-ttu-id="36f58-478">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="36f58-478">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="36f58-479">Format des cartes</span><span class="sxs-lookup"><span data-stu-id="36f58-479">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
