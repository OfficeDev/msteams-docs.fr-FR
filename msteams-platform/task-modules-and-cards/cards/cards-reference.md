---
title: Référence de cartes
description: Décrit toutes les cartes et les actions de carte disponibles pour les bots dans Teams
localization_priority: Normal
keywords: bots cartes de référence
ms.topic: reference
ms.openlocfilehash: cab7f1659759f40beb1aba59531ee6c1a84662c1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566858"
---
# <a name="cards-reference"></a><span data-ttu-id="2fac1-104">Référence de cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-104">Cards reference</span></span>

<span data-ttu-id="2fac1-105">Les cartes énumérées dans ce document sont prises en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2fac1-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="2fac1-106">Ils sont basés sur des cartes définies par le cadre bot, mais Teams ne prend pas en charge toutes les cartes Bot Framework et au lieu de cela Teams cartes ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="2fac1-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="2fac1-107">Les différences sont appelées dans les références de ce document.</span><span class="sxs-lookup"><span data-stu-id="2fac1-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="2fac1-108">Exemples de cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-108">Card examples</span></span>

<span data-ttu-id="2fac1-109">Vous pouvez trouver des informations supplémentaires sur la façon d’utiliser les cartes dans la documentation pour le Bot Builder SDK v3.</span><span class="sxs-lookup"><span data-stu-id="2fac1-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="2fac1-110">Des échantillons de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="2fac1-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="2fac1-111">.NET</span><span class="sxs-lookup"><span data-stu-id="2fac1-111">.NET</span></span>
  * <span data-ttu-id="2fac1-112">[Ajoutez des cartes comme pièces jointes aux messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2fac1-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="2fac1-113">[Cartes échantillon code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="2fac1-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="2fac1-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="2fac1-114">Node.js</span></span>
  * <span data-ttu-id="2fac1-115">[Ajoutez des cartes comme pièces jointes aux messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2fac1-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="2fac1-116">[Cartes échantillon code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="2fac1-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="2fac1-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-117">Types of cards</span></span>

<span data-ttu-id="2fac1-118">Ce tableau affiche les types de cartes à votre disposition :</span><span class="sxs-lookup"><span data-stu-id="2fac1-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="2fac1-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="2fac1-119">Card type</span></span> | <span data-ttu-id="2fac1-120">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="2fac1-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="2fac1-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="2fac1-122">Cette carte est une carte hautement personnalisable qui peut contenir n’importe quelle combinaison de texte, de parole, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="2fac1-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="2fac1-123">Carte de héros</span><span class="sxs-lookup"><span data-stu-id="2fac1-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="2fac1-124">Cette carte contient généralement une seule grande image, un ou plusieurs boutons, et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="2fac1-125">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-125">List card</span></span>](#list-card) | <span data-ttu-id="2fac1-126">Cette carte est une liste de défilement d’éléments.</span><span class="sxs-lookup"><span data-stu-id="2fac1-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="2fac1-127">Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="2fac1-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="2fac1-128">Cette carte dispose d’une mise en page flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="2fac1-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="2fac1-129">Carte de réception</span><span class="sxs-lookup"><span data-stu-id="2fac1-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="2fac1-130">Cette carte fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2fac1-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="2fac1-131">Carte Signin</span><span class="sxs-lookup"><span data-stu-id="2fac1-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="2fac1-132">Cette carte permet à un bot de demander qu’un utilisateur se signe.</span><span class="sxs-lookup"><span data-stu-id="2fac1-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="2fac1-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="2fac1-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="2fac1-134">Cette carte contient généralement une seule image miniature, un texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="2fac1-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="2fac1-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="2fac1-136">Ces cartes sont utilisées pour renvoyer plusieurs éléments en une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="2fac1-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="2fac1-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="2fac1-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="2fac1-138">Inline card images</span></span>

<span data-ttu-id="2fac1-139">La carte peut contenir une image en ligne en incluant un lien vers l’image accessible au public.</span><span class="sxs-lookup"><span data-stu-id="2fac1-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="2fac1-140">À des fins de performances, il est fortement recommandé d’héberger l’image sur un réseau public de diffusion de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="2fac1-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="2fac1-141">Les images sont réduites en taille ou en baisse tout en conservant le rapport d’aspect pour couvrir la zone d’image.</span><span class="sxs-lookup"><span data-stu-id="2fac1-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="2fac1-142">Les images sont ensuite recadrées à partir du centre pour atteindre le rapport d’aspect approprié pour la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="2fac1-143">Les images doivent être tout au plus 1024×1024, en format PNG, JPEG ou GIF, et ne pas prendre en charge gif animé.</span><span class="sxs-lookup"><span data-stu-id="2fac1-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="2fac1-144">Propriété</span><span class="sxs-lookup"><span data-stu-id="2fac1-144">Property</span></span> | <span data-ttu-id="2fac1-145">Type</span><span class="sxs-lookup"><span data-stu-id="2fac1-145">Type</span></span>  | <span data-ttu-id="2fac1-146">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fac1-147">url</span><span class="sxs-lookup"><span data-stu-id="2fac1-147">url</span></span> | <span data-ttu-id="2fac1-148">URL</span><span class="sxs-lookup"><span data-stu-id="2fac1-148">URL</span></span> | <span data-ttu-id="2fac1-149">HTTPS URL à l’image.</span><span class="sxs-lookup"><span data-stu-id="2fac1-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="2fac1-150">alt</span><span class="sxs-lookup"><span data-stu-id="2fac1-150">alt</span></span> | <span data-ttu-id="2fac1-151">String</span><span class="sxs-lookup"><span data-stu-id="2fac1-151">String</span></span> | <span data-ttu-id="2fac1-152">Description accessible de l’image.</span><span class="sxs-lookup"><span data-stu-id="2fac1-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="2fac1-153">Si une carte inclut une URL d’image qui passe par une redirection avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2fac1-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="2fac1-154">Cela se produit pour les images partagées sur le nuage public.</span><span class="sxs-lookup"><span data-stu-id="2fac1-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="2fac1-155">Boutons</span><span class="sxs-lookup"><span data-stu-id="2fac1-155">Buttons</span></span>

<span data-ttu-id="2fac1-156">Les boutons sont empilés au bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="2fac1-157">Le texte du bouton est toujours sur une seule ligne et est tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="2fac1-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="2fac1-158">Tous les boutons supplémentaires au-delà du nombre maximum pris en charge par la carte ne sont pas affichés.</span><span class="sxs-lookup"><span data-stu-id="2fac1-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="2fac1-159">Pour plus d’informations, voir [les actions de carte](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="2fac1-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="2fac1-160">Formatage des cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-160">Card formatting</span></span>

<span data-ttu-id="2fac1-161">Pour plus d’informations sur le formatage du texte dans les cartes, voir [formatage de la carte](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="2fac1-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="2fac1-162">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="2fac1-162">Adaptive card</span></span>

<span data-ttu-id="2fac1-163">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de parole, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="2fac1-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="2fac1-164">Pour plus d’informations, [voir cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="2fac1-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="2fac1-165">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2fac1-165">Support for adaptive cards</span></span>

| <span data-ttu-id="2fac1-166">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-166">Bots in Teams</span></span> | <span data-ttu-id="2fac1-167">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-167">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-168">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-168">Connectors</span></span> | <span data-ttu-id="2fac1-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-170">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-170">✔</span></span> | <span data-ttu-id="2fac1-171">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-171">✔</span></span> | <span data-ttu-id="2fac1-172">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-172">✖</span></span> | <span data-ttu-id="2fac1-173">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="2fac1-174">Teams de la plate-forme prend en charge v1.2 ou plus tôt des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="2fac1-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="2fac1-175">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="2fac1-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="2fac1-176">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="2fac1-176">Example of an adaptive card</span></span>

![Exemple de carte adaptative](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="2fac1-178">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2fac1-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="2fac1-179">Bot Framework référence:</span><span class="sxs-lookup"><span data-stu-id="2fac1-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="2fac1-180">Cartes adaptatives Node.js</span><span class="sxs-lookup"><span data-stu-id="2fac1-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="2fac1-181">Carte adaptative C #</span><span class="sxs-lookup"><span data-stu-id="2fac1-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="2fac1-182">Carte de héros</span><span class="sxs-lookup"><span data-stu-id="2fac1-182">Hero card</span></span>

<span data-ttu-id="2fac1-183">Une carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="2fac1-184">Prise en charge des cartes héros</span><span class="sxs-lookup"><span data-stu-id="2fac1-184">Support for hero cards</span></span>

| <span data-ttu-id="2fac1-185">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-185">Bots in Teams</span></span> | <span data-ttu-id="2fac1-186">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-186">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-187">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-187">Connectors</span></span> | <span data-ttu-id="2fac1-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-189">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-189">✔</span></span> | <span data-ttu-id="2fac1-190">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-190">✔</span></span> | <span data-ttu-id="2fac1-191">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-191">✖</span></span> | <span data-ttu-id="2fac1-192">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="2fac1-193">Propriétés d’une carte de héros</span><span class="sxs-lookup"><span data-stu-id="2fac1-193">Properties of a hero card</span></span>

| <span data-ttu-id="2fac1-194">Propriété</span><span class="sxs-lookup"><span data-stu-id="2fac1-194">Property</span></span> | <span data-ttu-id="2fac1-195">Type</span><span class="sxs-lookup"><span data-stu-id="2fac1-195">Type</span></span>  | <span data-ttu-id="2fac1-196">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fac1-197">title</span><span class="sxs-lookup"><span data-stu-id="2fac1-197">title</span></span> | <span data-ttu-id="2fac1-198">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-198">Rich text</span></span> | <span data-ttu-id="2fac1-199">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-199">Title of the card.</span></span> <span data-ttu-id="2fac1-200">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="2fac1-201">sous-titre</span><span class="sxs-lookup"><span data-stu-id="2fac1-201">subtitle</span></span> | <span data-ttu-id="2fac1-202">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-202">Rich text</span></span> | <span data-ttu-id="2fac1-203">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-203">Subtitle of the card.</span></span> <span data-ttu-id="2fac1-204">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="2fac1-205">text</span><span class="sxs-lookup"><span data-stu-id="2fac1-205">text</span></span> | <span data-ttu-id="2fac1-206">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-206">Rich text</span></span> | <span data-ttu-id="2fac1-207">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="2fac1-207">Text appears under the subtitle.</span></span> <span data-ttu-id="2fac1-208">Pour les options de mise en forme, voir [formatage de carte](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="2fac1-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="2fac1-209">Images</span><span class="sxs-lookup"><span data-stu-id="2fac1-209">images</span></span> | <span data-ttu-id="2fac1-210">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="2fac1-210">Array of images</span></span> | <span data-ttu-id="2fac1-211">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="2fac1-212">Rapport d’aspect 16:9.</span><span class="sxs-lookup"><span data-stu-id="2fac1-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="2fac1-213">Boutons</span><span class="sxs-lookup"><span data-stu-id="2fac1-213">buttons</span></span> | <span data-ttu-id="2fac1-214">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="2fac1-214">Array of action objects</span></span> | <span data-ttu-id="2fac1-215">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="2fac1-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="2fac1-216">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="2fac1-216">Maximum 6.</span></span> |
| <span data-ttu-id="2fac1-217">robinet</span><span class="sxs-lookup"><span data-stu-id="2fac1-217">tap</span></span> | <span data-ttu-id="2fac1-218">Objet Action</span><span class="sxs-lookup"><span data-stu-id="2fac1-218">Action object</span></span> | <span data-ttu-id="2fac1-219">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="2fac1-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="2fac1-220">Exemple d’une carte de héros</span><span class="sxs-lookup"><span data-stu-id="2fac1-220">Example of a hero card</span></span>

![Exemple d’une carte de héros](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="2fac1-222">Informations supplémentaires sur les cartes de héros</span><span class="sxs-lookup"><span data-stu-id="2fac1-222">Additional information on hero cards</span></span>

<span data-ttu-id="2fac1-223">Bot Framework référence:</span><span class="sxs-lookup"><span data-stu-id="2fac1-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="2fac1-224">Carte de héros Node.js</span><span class="sxs-lookup"><span data-stu-id="2fac1-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="2fac1-225">Carte héros C #</span><span class="sxs-lookup"><span data-stu-id="2fac1-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="2fac1-226">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-226">List card</span></span>

<span data-ttu-id="2fac1-227">La carte de liste a été ajoutée par Teams fournir des fonctions au-delà de ce que la collection de liste peut fournir.</span><span class="sxs-lookup"><span data-stu-id="2fac1-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="2fac1-228">La carte de liste fournit une liste de défilement des éléments.</span><span class="sxs-lookup"><span data-stu-id="2fac1-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="2fac1-229">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-229">Support for list cards</span></span>

| <span data-ttu-id="2fac1-230">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-230">Bots in Teams</span></span> | <span data-ttu-id="2fac1-231">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-231">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-232">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-232">Connectors</span></span> | <span data-ttu-id="2fac1-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-234">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-234">✔</span></span> | <span data-ttu-id="2fac1-235">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-235">✖</span></span> | <span data-ttu-id="2fac1-236">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-236">✖</span></span> |<span data-ttu-id="2fac1-237">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="2fac1-238">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-238">Properties of a list card</span></span>

| <span data-ttu-id="2fac1-239">Propriété</span><span class="sxs-lookup"><span data-stu-id="2fac1-239">Property</span></span> | <span data-ttu-id="2fac1-240">Type</span><span class="sxs-lookup"><span data-stu-id="2fac1-240">Type</span></span>  | <span data-ttu-id="2fac1-241">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fac1-242">title</span><span class="sxs-lookup"><span data-stu-id="2fac1-242">title</span></span> | <span data-ttu-id="2fac1-243">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-243">Rich text</span></span> | <span data-ttu-id="2fac1-244">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-244">Title of the card.</span></span> <span data-ttu-id="2fac1-245">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="2fac1-246">éléments</span><span class="sxs-lookup"><span data-stu-id="2fac1-246">items</span></span> | <span data-ttu-id="2fac1-247">Tableau des éléments de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-247">Array of list items</span></span> ||
| <span data-ttu-id="2fac1-248">Boutons</span><span class="sxs-lookup"><span data-stu-id="2fac1-248">buttons</span></span> | <span data-ttu-id="2fac1-249">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="2fac1-249">Array of action objects</span></span> | <span data-ttu-id="2fac1-250">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="2fac1-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="2fac1-251">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="2fac1-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="2fac1-252">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="2fac1-253">Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="2fac1-253">Office 365 connector card</span></span>

<span data-ttu-id="2fac1-254">La Office 365 connecteur est prise en charge en Teams, pas dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2fac1-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="2fac1-255">Cette carte offre une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="2fac1-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="2fac1-256">Cette carte encapsule une carte connecteur afin qu’elle puisse être utilisée par les bots.</span><span class="sxs-lookup"><span data-stu-id="2fac1-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="2fac1-257">Pour les différences entre les cartes de connecteur et la carte O365, [voir Notes sur la carte Office 365 connecteur.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="2fac1-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="2fac1-258">Prise en charge Office 365 cartes connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="2fac1-259">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-259">Bots in Teams</span></span> | <span data-ttu-id="2fac1-260">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-260">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-261">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-261">Connectors</span></span> | <span data-ttu-id="2fac1-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-263">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-263">✔</span></span> | <span data-ttu-id="2fac1-264">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-264">✔</span></span> | <span data-ttu-id="2fac1-265">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-265">✔</span></span> | <span data-ttu-id="2fac1-266">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="2fac1-267">Propriétés de la carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="2fac1-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="2fac1-268">Propriété</span><span class="sxs-lookup"><span data-stu-id="2fac1-268">Property</span></span> | <span data-ttu-id="2fac1-269">Type</span><span class="sxs-lookup"><span data-stu-id="2fac1-269">Type</span></span>  | <span data-ttu-id="2fac1-270">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fac1-271">title</span><span class="sxs-lookup"><span data-stu-id="2fac1-271">title</span></span> | <span data-ttu-id="2fac1-272">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-272">Rich text</span></span> | <span data-ttu-id="2fac1-273">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-273">Title of the card.</span></span> <span data-ttu-id="2fac1-274">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="2fac1-275">résumé</span><span class="sxs-lookup"><span data-stu-id="2fac1-275">summary</span></span> | <span data-ttu-id="2fac1-276">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-276">Rich text</span></span> | <span data-ttu-id="2fac1-277">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-277">Summary of the card.</span></span> <span data-ttu-id="2fac1-278">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="2fac1-279">text</span><span class="sxs-lookup"><span data-stu-id="2fac1-279">text</span></span> | <span data-ttu-id="2fac1-280">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-280">Rich text</span></span> | <span data-ttu-id="2fac1-281">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="2fac1-281">Text appears under the subtitle.</span></span> <span data-ttu-id="2fac1-282">Pour les options de mise en forme, voir [formatage de carte](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="2fac1-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="2fac1-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="2fac1-283">themeColor</span></span> | <span data-ttu-id="2fac1-284">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="2fac1-284">HEX string</span></span> | <span data-ttu-id="2fac1-285">Couleur qui l’emporte sur l’accentColor fourni à partir du manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="2fac1-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="2fac1-286">Notes sur la carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="2fac1-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="2fac1-287">Office 365 connecteurs fonctionnent correctement dans les Microsoft Teams, y compris les [actions ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="2fac1-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="2fac1-288">Une différence importante entre l’utilisation de cartes connecteurs à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est le traitement des actions de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="2fac1-289">Pour un connecteur, le point final reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="2fac1-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="2fac1-290">Pour un bot, `HttpPOST` l’action déclenche une activité qui envoie uniquement `invoke` l’iD d’action et le corps au bot.</span><span class="sxs-lookup"><span data-stu-id="2fac1-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="2fac1-291">Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.</span><span class="sxs-lookup"><span data-stu-id="2fac1-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="2fac1-292">Toutes les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="2fac1-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="2fac1-293">Tous les champs de texte soutiennent la réduction des points et html.</span><span class="sxs-lookup"><span data-stu-id="2fac1-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="2fac1-294">Vous pouvez contrôler les sections qui utilisent markdown ou HTML en paramètre la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="2fac1-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="2fac1-295">Par défaut, `markdown` est défini sur `true` .</span><span class="sxs-lookup"><span data-stu-id="2fac1-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="2fac1-296">Si vous souhaitez utiliser HTML à la place, `markdown` définissez-le sur `false` .</span><span class="sxs-lookup"><span data-stu-id="2fac1-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="2fac1-297">Si vous `themeColor` spécifiez la propriété, elle l’emporte sur la `accentColor` propriété dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="2fac1-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="2fac1-298">Pour spécifier le style de `activityImage` rendu pour , vous pouvez définir comme `activityImageType` suit:</span><span class="sxs-lookup"><span data-stu-id="2fac1-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="2fac1-299">Valeur</span><span class="sxs-lookup"><span data-stu-id="2fac1-299">Value</span></span> | <span data-ttu-id="2fac1-300">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="2fac1-301">Par défaut; `activityImage` est recadrée comme un cercle.</span><span class="sxs-lookup"><span data-stu-id="2fac1-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="2fac1-302">`activityImage` s’affiche comme un rectangle et conserve son rapport d’aspect.</span><span class="sxs-lookup"><span data-stu-id="2fac1-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="2fac1-303">Pour tous les autres détails sur les propriétés de la carte connecteur, voir [référence actionnable de carte de message](/outlook/actionable-messages/card-reference).</span><span class="sxs-lookup"><span data-stu-id="2fac1-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="2fac1-304">Les seules propriétés de carte de connecteur Microsoft Teams ne prend pas actuellement en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2fac1-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="2fac1-305">`startGroup`toujours traité comme `true` dans Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="2fac1-306">Exemple d’une Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="2fac1-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="2fac1-307">Carte de réception</span><span class="sxs-lookup"><span data-stu-id="2fac1-307">Receipt card</span></span>

<span data-ttu-id="2fac1-308">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="2fac1-308">Teams supports receipt card.</span></span> <span data-ttu-id="2fac1-309">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2fac1-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="2fac1-310">Il contient généralement la liste des éléments à inclure sur le reçu, tels que l’impôt et l’information totale.</span><span class="sxs-lookup"><span data-stu-id="2fac1-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="2fac1-311">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="2fac1-311">Support for receipt cards</span></span>

| <span data-ttu-id="2fac1-312">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-312">Bots in Teams</span></span> | <span data-ttu-id="2fac1-313">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-313">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-314">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-314">Connectors</span></span> | <span data-ttu-id="2fac1-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-316">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-316">✔</span></span> | <span data-ttu-id="2fac1-317">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-317">✔</span></span> | <span data-ttu-id="2fac1-318">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-318">✖</span></span> | <span data-ttu-id="2fac1-319">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="2fac1-320">Exemple de carte de réception</span><span class="sxs-lookup"><span data-stu-id="2fac1-320">Example of a receipt card</span></span>

![Exemple de carte de réception](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="2fac1-322">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="2fac1-322">Additional information on receipt cards</span></span>

<span data-ttu-id="2fac1-323">Bot Framework référence:</span><span class="sxs-lookup"><span data-stu-id="2fac1-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="2fac1-324">Carte de réception Node.js</span><span class="sxs-lookup"><span data-stu-id="2fac1-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="2fac1-325">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="2fac1-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="2fac1-326">Carte Signin</span><span class="sxs-lookup"><span data-stu-id="2fac1-326">Signin card</span></span>

<span data-ttu-id="2fac1-327">La carte Signin permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="2fac1-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="2fac1-328">Il est pris en charge Teams sous une forme légèrement différente de celle que l’on trouve dans le cadre bot.</span><span class="sxs-lookup"><span data-stu-id="2fac1-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="2fac1-329">La carte de connexion en Teams est similaire à la carte signin dans le cadre Bot, sauf que la carte signin en Teams ne prend en charge que deux actions: `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="2fac1-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="2fac1-330">L’action signin peut être utilisée à partir de n’importe quelle carte Teams, pas seulement la carte de connexion.</span><span class="sxs-lookup"><span data-stu-id="2fac1-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="2fac1-331">Pour plus d’informations sur l’authentification, [Microsoft Teams flux d’authentification pour les bots](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="2fac1-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="2fac1-332">Prise en charge des cartes signin</span><span class="sxs-lookup"><span data-stu-id="2fac1-332">Support for signin cards</span></span>

| <span data-ttu-id="2fac1-333">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-333">Bots in Teams</span></span> | <span data-ttu-id="2fac1-334">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-334">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-335">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-335">Connectors</span></span> | <span data-ttu-id="2fac1-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-337">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-337">✔</span></span> | <span data-ttu-id="2fac1-338">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-338">✖</span></span> | <span data-ttu-id="2fac1-339">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-339">✖</span></span> | <span data-ttu-id="2fac1-340">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="2fac1-341">Informations supplémentaires sur les cartes de connexion</span><span class="sxs-lookup"><span data-stu-id="2fac1-341">Additional information on signin cards</span></span>

<span data-ttu-id="2fac1-342">Bot Framework référence:</span><span class="sxs-lookup"><span data-stu-id="2fac1-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="2fac1-343">Carte Signin Node.js</span><span class="sxs-lookup"><span data-stu-id="2fac1-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="2fac1-344">Carte Signin C #</span><span class="sxs-lookup"><span data-stu-id="2fac1-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="2fac1-345">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="2fac1-345">Thumbnail card</span></span>

<span data-ttu-id="2fac1-346">Une carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="2fac1-347">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="2fac1-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="2fac1-348">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-348">Bots in Teams</span></span> | <span data-ttu-id="2fac1-349">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-349">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-350">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-350">Connectors</span></span> | <span data-ttu-id="2fac1-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-352">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-352">✔</span></span> | <span data-ttu-id="2fac1-353">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-353">✔</span></span> | <span data-ttu-id="2fac1-354">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-354">✖</span></span> | <span data-ttu-id="2fac1-355">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-355">✔</span></span> |

![Exemple d’une carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="2fac1-357">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="2fac1-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="2fac1-358">Propriété</span><span class="sxs-lookup"><span data-stu-id="2fac1-358">Property</span></span> | <span data-ttu-id="2fac1-359">Type</span><span class="sxs-lookup"><span data-stu-id="2fac1-359">Type</span></span>  | <span data-ttu-id="2fac1-360">Description</span><span class="sxs-lookup"><span data-stu-id="2fac1-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fac1-361">title</span><span class="sxs-lookup"><span data-stu-id="2fac1-361">title</span></span> | <span data-ttu-id="2fac1-362">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-362">Rich text</span></span> | <span data-ttu-id="2fac1-363">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-363">Title of the card.</span></span> <span data-ttu-id="2fac1-364">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="2fac1-365">sous-titre</span><span class="sxs-lookup"><span data-stu-id="2fac1-365">subtitle</span></span> | <span data-ttu-id="2fac1-366">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-366">Rich text</span></span> | <span data-ttu-id="2fac1-367">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-367">Subtitle of the card.</span></span> <span data-ttu-id="2fac1-368">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="2fac1-369">text</span><span class="sxs-lookup"><span data-stu-id="2fac1-369">text</span></span> | <span data-ttu-id="2fac1-370">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="2fac1-370">Rich text</span></span> | <span data-ttu-id="2fac1-371">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="2fac1-371">Text appears under the subtitle.</span></span> <span data-ttu-id="2fac1-372">Pour les options de mise en forme, voir [formatage de carte](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="2fac1-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="2fac1-373">Images</span><span class="sxs-lookup"><span data-stu-id="2fac1-373">images</span></span> | <span data-ttu-id="2fac1-374">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="2fac1-374">Array of images</span></span> | <span data-ttu-id="2fac1-375">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="2fac1-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="2fac1-376">Rapport d’aspect 1:1 carré.</span><span class="sxs-lookup"><span data-stu-id="2fac1-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="2fac1-377">Boutons</span><span class="sxs-lookup"><span data-stu-id="2fac1-377">buttons</span></span> | <span data-ttu-id="2fac1-378">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="2fac1-378">Array of action objects</span></span> | <span data-ttu-id="2fac1-379">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="2fac1-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="2fac1-380">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="2fac1-380">Maximum 6.</span></span> |
| <span data-ttu-id="2fac1-381">robinet</span><span class="sxs-lookup"><span data-stu-id="2fac1-381">tap</span></span> | <span data-ttu-id="2fac1-382">Objet Action</span><span class="sxs-lookup"><span data-stu-id="2fac1-382">Action object</span></span> | <span data-ttu-id="2fac1-383">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="2fac1-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="2fac1-384">Exemple d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="2fac1-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="2fac1-385">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2fac1-385">Additional information</span></span>

<span data-ttu-id="2fac1-386">Bot Framework référence:</span><span class="sxs-lookup"><span data-stu-id="2fac1-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="2fac1-387">Carte miniature Node.js</span><span class="sxs-lookup"><span data-stu-id="2fac1-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="2fac1-388">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="2fac1-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="2fac1-389">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="2fac1-389">Card collections</span></span>

<span data-ttu-id="2fac1-390">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="2fac1-390">Teams supports Card collections.</span></span>

<span data-ttu-id="2fac1-391">Les collections de cartes `builder.AttachmentLayout.carousel` incluent et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="2fac1-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="2fac1-392">Ces collections contiennent des cartes adaptatives, héros ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="2fac1-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="2fac1-393">Collection Carrousel</span><span class="sxs-lookup"><span data-stu-id="2fac1-393">Carousel collection</span></span>

<span data-ttu-id="2fac1-394">La [disposition du carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) montre un carrousel de cartes, en option avec les boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="2fac1-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="2fac1-395">Prise en charge des collections de carrousel</span><span class="sxs-lookup"><span data-stu-id="2fac1-395">Support for carousel collections</span></span>

| <span data-ttu-id="2fac1-396">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-396">Bots in Teams</span></span> | <span data-ttu-id="2fac1-397">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-397">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-398">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-398">Connectors</span></span> | <span data-ttu-id="2fac1-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-400">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-400">✔</span></span> | <span data-ttu-id="2fac1-401">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-401">✖</span></span> | <span data-ttu-id="2fac1-402">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-402">✖</span></span> | <span data-ttu-id="2fac1-403">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="2fac1-404">Un carrousel peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="2fac1-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="2fac1-405">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="2fac1-405">Properties of a carousel card</span></span>

<span data-ttu-id="2fac1-406">Les propriétés d’une carte carrousel sont les mêmes que celles du héros et des cartes miniatures.</span><span class="sxs-lookup"><span data-stu-id="2fac1-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="2fac1-407">Exemple de collection de carrousel</span><span class="sxs-lookup"><span data-stu-id="2fac1-407">Example of a carousel collection</span></span>

![Exemple d’un carrousel de cartes](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="2fac1-409">Syntaxe pour les collections de carrousel</span><span class="sxs-lookup"><span data-stu-id="2fac1-409">Syntax for carousel collections</span></span>

<span data-ttu-id="2fac1-410">`builder.AttachmentLayoutTypes.Carousel` est la syntaxe pour les collections de carrousel.</span><span class="sxs-lookup"><span data-stu-id="2fac1-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="2fac1-411">Collection de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="2fac1-412">Prise en charge des collections de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-412">Support for list collections</span></span>

<span data-ttu-id="2fac1-413">La mise en page de liste affiche une liste verticalement empilée de cartes, en option avec les boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="2fac1-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="2fac1-414">Bots en Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-414">Bots in Teams</span></span> | <span data-ttu-id="2fac1-415">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="2fac1-415">Messaging extensions</span></span>  | <span data-ttu-id="2fac1-416">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="2fac1-416">Connectors</span></span> | <span data-ttu-id="2fac1-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fac1-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fac1-418">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-418">✔</span></span> | <span data-ttu-id="2fac1-419">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-419">✔</span></span> | <span data-ttu-id="2fac1-420">✖</span><span class="sxs-lookup"><span data-stu-id="2fac1-420">✖</span></span> | <span data-ttu-id="2fac1-421">✔</span><span class="sxs-lookup"><span data-stu-id="2fac1-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="2fac1-422">Exemple d’une collection de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-422">Example of a list collection</span></span>

![Exemple d’une liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="2fac1-424">Les propriétés sont les mêmes que pour le héros ou la carte miniature.</span><span class="sxs-lookup"><span data-stu-id="2fac1-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="2fac1-425">Une liste peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="2fac1-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="2fac1-426">Certaines combinaisons de cartes de liste ne sont pas encore prises en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="2fac1-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="2fac1-427">Syntaxe pour les collections de liste</span><span class="sxs-lookup"><span data-stu-id="2fac1-427">Syntax for list collections</span></span>

<span data-ttu-id="2fac1-428">`builder.AttachmentLayout.list` est la syntaxe pour les collections de liste.</span><span class="sxs-lookup"><span data-stu-id="2fac1-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="2fac1-429">Cartes non prises en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="2fac1-429">Cards not supported in Teams</span></span>

<span data-ttu-id="2fac1-430">Les cartes suivantes sont implémentées par le Cadre Bot, mais ne sont pas prises en charge par Teams :</span><span class="sxs-lookup"><span data-stu-id="2fac1-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="2fac1-431">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="2fac1-431">Animation cards</span></span>
* <span data-ttu-id="2fac1-432">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="2fac1-432">Audio cards</span></span>
* <span data-ttu-id="2fac1-433">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="2fac1-433">Video cards</span></span>
