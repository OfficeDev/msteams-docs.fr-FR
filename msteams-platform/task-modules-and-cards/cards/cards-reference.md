---
title: Référence de cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
localization_priority: Normal
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: 741980ea79dd23659dd2b8a240d767b8292ca251
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994384"
---
# <a name="cards-reference"></a><span data-ttu-id="b42e2-104">Référence de cartes</span><span class="sxs-lookup"><span data-stu-id="b42e2-104">Cards reference</span></span>

<span data-ttu-id="b42e2-105">Les cartes répertoriées dans ce document sont pris en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b42e2-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="b42e2-106">Elles sont basées sur des cartes définies par Bot Framework (BF), mais Teams ne prend pas en charge toutes les cartes Bot Framework et certaines cartes Teams ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="b42e2-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="b42e2-107">Les différences sont appelées dans les références de ce document.</span><span class="sxs-lookup"><span data-stu-id="b42e2-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="b42e2-108">Exemples de cartes</span><span class="sxs-lookup"><span data-stu-id="b42e2-108">Card examples</span></span>

<span data-ttu-id="b42e2-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="b42e2-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="b42e2-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples GitHub.</span><span class="sxs-lookup"><span data-stu-id="b42e2-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="b42e2-111">.NET</span><span class="sxs-lookup"><span data-stu-id="b42e2-111">.NET</span></span>
  * <span data-ttu-id="b42e2-112">[Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b42e2-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="b42e2-113">[Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="b42e2-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="b42e2-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="b42e2-114">Node.js</span></span>
  * <span data-ttu-id="b42e2-115">[Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b42e2-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="b42e2-116">[Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="b42e2-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="b42e2-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="b42e2-117">Types of cards</span></span>

<span data-ttu-id="b42e2-118">Ce tableau indique les types de cartes disponibles :</span><span class="sxs-lookup"><span data-stu-id="b42e2-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="b42e2-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="b42e2-119">Card type</span></span> | <span data-ttu-id="b42e2-120">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="b42e2-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="b42e2-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="b42e2-122">Cette carte est hautement personnalisable et peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b42e2-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="b42e2-123">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="b42e2-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="b42e2-124">Cette carte contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="b42e2-125">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="b42e2-125">List card</span></span>](#list-card) | <span data-ttu-id="b42e2-126">Cette carte est une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="b42e2-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="b42e2-127">carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="b42e2-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="b42e2-128">Cette carte possède une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="b42e2-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="b42e2-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="b42e2-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="b42e2-130">Cette carte fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b42e2-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="b42e2-131">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="b42e2-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="b42e2-132">Cette carte permet à un bot de demander à un utilisateur de se rendre.</span><span class="sxs-lookup"><span data-stu-id="b42e2-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="b42e2-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="b42e2-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="b42e2-134">Cette carte contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="b42e2-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="b42e2-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="b42e2-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="b42e2-136">Ces cartes sont utilisées pour renvoyer plusieurs éléments en une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="b42e2-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="b42e2-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="b42e2-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="b42e2-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="b42e2-138">Inline card images</span></span>

<span data-ttu-id="b42e2-139">La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="b42e2-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="b42e2-140">À des fins de performances, il est vivement recommandé d’héberger l’image sur un réseau public de distribution de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="b42e2-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="b42e2-141">Les images sont réduites ou réduites en taille tout en conservant les proportions pour couvrir la zone d’image.</span><span class="sxs-lookup"><span data-stu-id="b42e2-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="b42e2-142">Les images sont ensuite rogées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="b42e2-143">Les images doivent être au maximum 1024×1024, au format PNG, JPEG ou GIF, et ne pas prendre en charge les images GIF animées.</span><span class="sxs-lookup"><span data-stu-id="b42e2-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="b42e2-144">Propriété</span><span class="sxs-lookup"><span data-stu-id="b42e2-144">Property</span></span> | <span data-ttu-id="b42e2-145">Type</span><span class="sxs-lookup"><span data-stu-id="b42e2-145">Type</span></span>  | <span data-ttu-id="b42e2-146">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b42e2-147">url</span><span class="sxs-lookup"><span data-stu-id="b42e2-147">url</span></span> | <span data-ttu-id="b42e2-148">URL</span><span class="sxs-lookup"><span data-stu-id="b42e2-148">URL</span></span> | <span data-ttu-id="b42e2-149">URL HTTPS vers l’image.</span><span class="sxs-lookup"><span data-stu-id="b42e2-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="b42e2-150">alt</span><span class="sxs-lookup"><span data-stu-id="b42e2-150">alt</span></span> | <span data-ttu-id="b42e2-151">String</span><span class="sxs-lookup"><span data-stu-id="b42e2-151">String</span></span> | <span data-ttu-id="b42e2-152">Description accessible de l’image.</span><span class="sxs-lookup"><span data-stu-id="b42e2-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="b42e2-153">Si une carte inclut une URL d’image qui passe par une redirection avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b42e2-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="b42e2-154">Cela se produit pour les images partagées sur le cloud public.</span><span class="sxs-lookup"><span data-stu-id="b42e2-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="b42e2-155">Boutons</span><span class="sxs-lookup"><span data-stu-id="b42e2-155">Buttons</span></span>

<span data-ttu-id="b42e2-156">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="b42e2-157">Le texte du bouton est toujours sur une seule ligne et tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="b42e2-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="b42e2-158">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne sont pas affichés.</span><span class="sxs-lookup"><span data-stu-id="b42e2-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="b42e2-159">Pour plus d’informations, voir [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="b42e2-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="b42e2-160">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="b42e2-160">Card formatting</span></span>

<span data-ttu-id="b42e2-161">Pour plus d’informations sur la mise en forme du texte dans les cartes, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="b42e2-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="b42e2-162">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="b42e2-162">Adaptive card</span></span>

<span data-ttu-id="b42e2-163">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b42e2-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="b42e2-164">Pour plus d’informations, voir [cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="b42e2-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="b42e2-165">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="b42e2-165">Support for adaptive cards</span></span>

| <span data-ttu-id="b42e2-166">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-166">Bots in Teams</span></span> | <span data-ttu-id="b42e2-167">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-167">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-168">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-168">Connectors</span></span> | <span data-ttu-id="b42e2-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-170">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-170">✔</span></span> | <span data-ttu-id="b42e2-171">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-171">✔</span></span> | <span data-ttu-id="b42e2-172">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-172">✖</span></span> | <span data-ttu-id="b42e2-173">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="b42e2-174">Teams prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="b42e2-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="b42e2-175">Le style d’action positive ou destructive n’est pas pris en charge dans les cartes adaptatives sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="b42e2-175">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="b42e2-176">Les éléments multimédias ne sont actuellement pas pris en charge dans les cartes adaptatives sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="b42e2-176">Media elements are currently not supported in Adaptive Cards on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="b42e2-177">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="b42e2-177">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="b42e2-179">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="b42e2-179">Additional information on adaptive cards</span></span>

<span data-ttu-id="b42e2-180">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="b42e2-180">Bot Framework reference:</span></span>

* [<span data-ttu-id="b42e2-181">Cartes adaptatives Node.js</span><span class="sxs-lookup"><span data-stu-id="b42e2-181">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="b42e2-182">Carte adaptative C #</span><span class="sxs-lookup"><span data-stu-id="b42e2-182">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="b42e2-183">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="b42e2-183">Hero card</span></span>

<span data-ttu-id="b42e2-184">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-184">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="b42e2-185">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="b42e2-185">Support for hero cards</span></span>

| <span data-ttu-id="b42e2-186">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-186">Bots in Teams</span></span> | <span data-ttu-id="b42e2-187">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-187">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-188">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-188">Connectors</span></span> | <span data-ttu-id="b42e2-189">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-189">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-190">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-190">✔</span></span> | <span data-ttu-id="b42e2-191">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-191">✔</span></span> | <span data-ttu-id="b42e2-192">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-192">✖</span></span> | <span data-ttu-id="b42e2-193">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-193">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="b42e2-194">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="b42e2-194">Properties of a hero card</span></span>

| <span data-ttu-id="b42e2-195">Propriété</span><span class="sxs-lookup"><span data-stu-id="b42e2-195">Property</span></span> | <span data-ttu-id="b42e2-196">Type</span><span class="sxs-lookup"><span data-stu-id="b42e2-196">Type</span></span>  | <span data-ttu-id="b42e2-197">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b42e2-198">title</span><span class="sxs-lookup"><span data-stu-id="b42e2-198">title</span></span> | <span data-ttu-id="b42e2-199">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-199">Rich text</span></span> | <span data-ttu-id="b42e2-200">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-200">Title of the card.</span></span> <span data-ttu-id="b42e2-201">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-201">Maximum 2 lines.</span></span> |
| <span data-ttu-id="b42e2-202">subtitle</span><span class="sxs-lookup"><span data-stu-id="b42e2-202">subtitle</span></span> | <span data-ttu-id="b42e2-203">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-203">Rich text</span></span> | <span data-ttu-id="b42e2-204">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-204">Subtitle of the card.</span></span> <span data-ttu-id="b42e2-205">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-205">Maximum 2 lines.</span></span>|
| <span data-ttu-id="b42e2-206">text</span><span class="sxs-lookup"><span data-stu-id="b42e2-206">text</span></span> | <span data-ttu-id="b42e2-207">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-207">Rich text</span></span> | <span data-ttu-id="b42e2-208">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="b42e2-208">Text appears under the subtitle.</span></span> <span data-ttu-id="b42e2-209">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="b42e2-209">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="b42e2-210">images</span><span class="sxs-lookup"><span data-stu-id="b42e2-210">images</span></span> | <span data-ttu-id="b42e2-211">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="b42e2-211">Array of images</span></span> | <span data-ttu-id="b42e2-212">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-212">Image displayed at the top of the card.</span></span> <span data-ttu-id="b42e2-213">Proportions 16:9.</span><span class="sxs-lookup"><span data-stu-id="b42e2-213">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="b42e2-214">buttons</span><span class="sxs-lookup"><span data-stu-id="b42e2-214">buttons</span></span> | <span data-ttu-id="b42e2-215">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="b42e2-215">Array of action objects</span></span> | <span data-ttu-id="b42e2-216">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="b42e2-216">Set of actions applicable to the current card.</span></span> <span data-ttu-id="b42e2-217">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="b42e2-217">Maximum 6.</span></span> |
| <span data-ttu-id="b42e2-218">tap</span><span class="sxs-lookup"><span data-stu-id="b42e2-218">tap</span></span> | <span data-ttu-id="b42e2-219">Objet Action</span><span class="sxs-lookup"><span data-stu-id="b42e2-219">Action object</span></span> | <span data-ttu-id="b42e2-220">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="b42e2-220">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="b42e2-221">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="b42e2-221">Example of a hero card</span></span>

![Exemple de carte Hero](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="b42e2-223">Informations supplémentaires sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="b42e2-223">Additional information on hero cards</span></span>

<span data-ttu-id="b42e2-224">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="b42e2-224">Bot Framework reference:</span></span>

* [<span data-ttu-id="b42e2-225">Carte Hero Node.js</span><span class="sxs-lookup"><span data-stu-id="b42e2-225">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="b42e2-226">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="b42e2-226">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="b42e2-227">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="b42e2-227">List card</span></span>

<span data-ttu-id="b42e2-228">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="b42e2-228">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="b42e2-229">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="b42e2-229">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="b42e2-230">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="b42e2-230">Support for list cards</span></span>

| <span data-ttu-id="b42e2-231">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-231">Bots in Teams</span></span> | <span data-ttu-id="b42e2-232">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-232">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-233">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-233">Connectors</span></span> | <span data-ttu-id="b42e2-234">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-234">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-235">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-235">✔</span></span> | <span data-ttu-id="b42e2-236">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-236">✖</span></span> | <span data-ttu-id="b42e2-237">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-237">✖</span></span> |<span data-ttu-id="b42e2-238">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-238">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="b42e2-239">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="b42e2-239">Properties of a list card</span></span>

| <span data-ttu-id="b42e2-240">Propriété</span><span class="sxs-lookup"><span data-stu-id="b42e2-240">Property</span></span> | <span data-ttu-id="b42e2-241">Type</span><span class="sxs-lookup"><span data-stu-id="b42e2-241">Type</span></span>  | <span data-ttu-id="b42e2-242">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-242">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b42e2-243">title</span><span class="sxs-lookup"><span data-stu-id="b42e2-243">title</span></span> | <span data-ttu-id="b42e2-244">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-244">Rich text</span></span> | <span data-ttu-id="b42e2-245">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-245">Title of the card.</span></span> <span data-ttu-id="b42e2-246">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-246">Maximum 2 lines.</span></span>|
| <span data-ttu-id="b42e2-247">éléments</span><span class="sxs-lookup"><span data-stu-id="b42e2-247">items</span></span> | <span data-ttu-id="b42e2-248">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="b42e2-248">Array of list items</span></span> ||
| <span data-ttu-id="b42e2-249">buttons</span><span class="sxs-lookup"><span data-stu-id="b42e2-249">buttons</span></span> | <span data-ttu-id="b42e2-250">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="b42e2-250">Array of action objects</span></span> | <span data-ttu-id="b42e2-251">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="b42e2-251">Set of actions applicable to the current card.</span></span> <span data-ttu-id="b42e2-252">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="b42e2-252">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="b42e2-253">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="b42e2-253">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="b42e2-254">carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="b42e2-254">Office 365 connector card</span></span>

<span data-ttu-id="b42e2-255">La carte Office 365 connecteur est prise en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b42e2-255">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="b42e2-256">Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="b42e2-256">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="b42e2-257">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="b42e2-257">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="b42e2-258">Pour les différences entre les cartes de connecteur et la carte O365, voir remarques sur [la carte Office 365 connecteur.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="b42e2-258">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="b42e2-259">Prise en charge Office 365 cartes de connecteur</span><span class="sxs-lookup"><span data-stu-id="b42e2-259">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="b42e2-260">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-260">Bots in Teams</span></span> | <span data-ttu-id="b42e2-261">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-261">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-262">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-262">Connectors</span></span> | <span data-ttu-id="b42e2-263">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-263">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-264">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-264">✔</span></span> | <span data-ttu-id="b42e2-265">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-265">✔</span></span> | <span data-ttu-id="b42e2-266">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-266">✔</span></span> | <span data-ttu-id="b42e2-267">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-267">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="b42e2-268">Propriétés de la carte Office 365 connecteur de connexion</span><span class="sxs-lookup"><span data-stu-id="b42e2-268">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="b42e2-269">Propriété</span><span class="sxs-lookup"><span data-stu-id="b42e2-269">Property</span></span> | <span data-ttu-id="b42e2-270">Type</span><span class="sxs-lookup"><span data-stu-id="b42e2-270">Type</span></span>  | <span data-ttu-id="b42e2-271">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-271">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b42e2-272">title</span><span class="sxs-lookup"><span data-stu-id="b42e2-272">title</span></span> | <span data-ttu-id="b42e2-273">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-273">Rich text</span></span> | <span data-ttu-id="b42e2-274">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-274">Title of the card.</span></span> <span data-ttu-id="b42e2-275">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-275">Maximum 2 lines.</span></span> |
| <span data-ttu-id="b42e2-276">résumé</span><span class="sxs-lookup"><span data-stu-id="b42e2-276">summary</span></span> | <span data-ttu-id="b42e2-277">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-277">Rich text</span></span> | <span data-ttu-id="b42e2-278">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-278">Summary of the card.</span></span> <span data-ttu-id="b42e2-279">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-279">Maximum 2 lines.</span></span> |
| <span data-ttu-id="b42e2-280">text</span><span class="sxs-lookup"><span data-stu-id="b42e2-280">text</span></span> | <span data-ttu-id="b42e2-281">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-281">Rich text</span></span> | <span data-ttu-id="b42e2-282">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="b42e2-282">Text appears under the subtitle.</span></span> <span data-ttu-id="b42e2-283">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="b42e2-283">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="b42e2-284">themeColor</span><span class="sxs-lookup"><span data-stu-id="b42e2-284">themeColor</span></span> | <span data-ttu-id="b42e2-285">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="b42e2-285">HEX string</span></span> | <span data-ttu-id="b42e2-286">Couleur qui remplace l’accentColor fourni à partir du manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="b42e2-286">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="b42e2-287">Remarques sur la carte Office 365 connecteur</span><span class="sxs-lookup"><span data-stu-id="b42e2-287">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="b42e2-288">Office 365 cartes de connecteur fonctionnent correctement dans Microsoft Teams, y compris les [actions ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="b42e2-288">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="b42e2-289">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-289">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="b42e2-290">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="b42e2-290">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="b42e2-291">Pour un bot, l’action déclenche une activité qui envoie uniquement l’ID d’action et le `HttpPOST` `invoke` corps au bot.</span><span class="sxs-lookup"><span data-stu-id="b42e2-291">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="b42e2-292">Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.</span><span class="sxs-lookup"><span data-stu-id="b42e2-292">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="b42e2-293">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="b42e2-293">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="b42e2-294">Tous les champs de texte prise en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="b42e2-294">All text fields support markdown and HTML.</span></span> <span data-ttu-id="b42e2-295">Vous pouvez contrôler les sections qui utilisent markdown ou HTML en définition de `markdown` la propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="b42e2-295">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="b42e2-296">Par défaut, `markdown` est définie sur `true` .</span><span class="sxs-lookup"><span data-stu-id="b42e2-296">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="b42e2-297">Si vous souhaitez utiliser du code HTML à la place, définissez `markdown` sur `false` .</span><span class="sxs-lookup"><span data-stu-id="b42e2-297">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="b42e2-298">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="b42e2-298">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="b42e2-299">Pour spécifier le style de rendu `activityImage` pour , vous pouvez définir comme suit `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="b42e2-299">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="b42e2-300">Valeur</span><span class="sxs-lookup"><span data-stu-id="b42e2-300">Value</span></span> | <span data-ttu-id="b42e2-301">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-301">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="b42e2-302">Valeur par défaut ; `activityImage` est rogché en tant que cercle.</span><span class="sxs-lookup"><span data-stu-id="b42e2-302">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="b42e2-303">`activityImage` est affiché sous forme de rectangle et conserve ses proportions.</span><span class="sxs-lookup"><span data-stu-id="b42e2-303">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="b42e2-304">Pour plus d’informations sur les propriétés de carte de connecteur, voir la [référence de carte de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="b42e2-304">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="b42e2-305">Les seules propriétés de carte de connecteur non Microsoft Teams actuellement prise en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b42e2-305">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="b42e2-306">`startGroup`toujours traité comme dans `true` Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-306">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="b42e2-307">Exemple de carte de connecteur Office 365 de connexion</span><span class="sxs-lookup"><span data-stu-id="b42e2-307">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="b42e2-308">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="b42e2-308">Receipt card</span></span>

<span data-ttu-id="b42e2-309">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="b42e2-309">Teams supports receipt card.</span></span> <span data-ttu-id="b42e2-310">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b42e2-310">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="b42e2-311">Elle contient généralement la liste des éléments à inclure sur le reçu, telles que les taxes et le total des informations.</span><span class="sxs-lookup"><span data-stu-id="b42e2-311">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="b42e2-312">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="b42e2-312">Support for receipt cards</span></span>

| <span data-ttu-id="b42e2-313">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-313">Bots in Teams</span></span> | <span data-ttu-id="b42e2-314">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-314">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-315">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-315">Connectors</span></span> | <span data-ttu-id="b42e2-316">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-316">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-317">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-317">✔</span></span> | <span data-ttu-id="b42e2-318">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-318">✔</span></span> | <span data-ttu-id="b42e2-319">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-319">✖</span></span> | <span data-ttu-id="b42e2-320">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-320">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="b42e2-321">Exemple de carte de reçu</span><span class="sxs-lookup"><span data-stu-id="b42e2-321">Example of a receipt card</span></span>

![Exemple de carte de reçu](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="b42e2-323">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="b42e2-323">Additional information on receipt cards</span></span>

<span data-ttu-id="b42e2-324">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="b42e2-324">Bot Framework reference:</span></span>

* [<span data-ttu-id="b42e2-325">Carte de réception Node.js</span><span class="sxs-lookup"><span data-stu-id="b42e2-325">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="b42e2-326">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="b42e2-326">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="b42e2-327">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="b42e2-327">Signin card</span></span>

<span data-ttu-id="b42e2-328">La carte de signature permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="b42e2-328">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="b42e2-329">Elle est prise en charge Teams sous une forme légèrement différente de celle de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b42e2-329">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="b42e2-330">La carte de Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="b42e2-330">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="b42e2-331">L’action de signin peut être utilisée à partir de n’importe quelle carte de Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="b42e2-331">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="b42e2-332">Pour plus d’informations sur l’authentification, [Microsoft Teams flux d’authentification pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="b42e2-332">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="b42e2-333">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="b42e2-333">Support for signin cards</span></span>

| <span data-ttu-id="b42e2-334">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-334">Bots in Teams</span></span> | <span data-ttu-id="b42e2-335">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-335">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-336">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-336">Connectors</span></span> | <span data-ttu-id="b42e2-337">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-337">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-338">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-338">✔</span></span> | <span data-ttu-id="b42e2-339">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-339">✖</span></span> | <span data-ttu-id="b42e2-340">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-340">✖</span></span> | <span data-ttu-id="b42e2-341">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-341">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="b42e2-342">Informations supplémentaires sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="b42e2-342">Additional information on signin cards</span></span>

<span data-ttu-id="b42e2-343">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="b42e2-343">Bot Framework reference:</span></span>

* [<span data-ttu-id="b42e2-344">Carte de Node.js</span><span class="sxs-lookup"><span data-stu-id="b42e2-344">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="b42e2-345">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="b42e2-345">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="b42e2-346">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="b42e2-346">Thumbnail card</span></span>

<span data-ttu-id="b42e2-347">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-347">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="b42e2-348">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="b42e2-348">Support for thumbnail cards</span></span>

| <span data-ttu-id="b42e2-349">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-349">Bots in Teams</span></span> | <span data-ttu-id="b42e2-350">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-350">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-351">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-351">Connectors</span></span> | <span data-ttu-id="b42e2-352">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-352">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-353">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-353">✔</span></span> | <span data-ttu-id="b42e2-354">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-354">✔</span></span> | <span data-ttu-id="b42e2-355">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-355">✖</span></span> | <span data-ttu-id="b42e2-356">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-356">✔</span></span> |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="b42e2-358">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="b42e2-358">Properties of a thumbnail card</span></span>

| <span data-ttu-id="b42e2-359">Propriété</span><span class="sxs-lookup"><span data-stu-id="b42e2-359">Property</span></span> | <span data-ttu-id="b42e2-360">Type</span><span class="sxs-lookup"><span data-stu-id="b42e2-360">Type</span></span>  | <span data-ttu-id="b42e2-361">Description</span><span class="sxs-lookup"><span data-stu-id="b42e2-361">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b42e2-362">title</span><span class="sxs-lookup"><span data-stu-id="b42e2-362">title</span></span> | <span data-ttu-id="b42e2-363">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-363">Rich text</span></span> | <span data-ttu-id="b42e2-364">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-364">Title of the card.</span></span> <span data-ttu-id="b42e2-365">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-365">Maximum 2 lines.</span></span>|
| <span data-ttu-id="b42e2-366">subtitle</span><span class="sxs-lookup"><span data-stu-id="b42e2-366">subtitle</span></span> | <span data-ttu-id="b42e2-367">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-367">Rich text</span></span> | <span data-ttu-id="b42e2-368">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-368">Subtitle of the card.</span></span> <span data-ttu-id="b42e2-369">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-369">Maximum 2 lines.</span></span>|
| <span data-ttu-id="b42e2-370">text</span><span class="sxs-lookup"><span data-stu-id="b42e2-370">text</span></span> | <span data-ttu-id="b42e2-371">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="b42e2-371">Rich text</span></span> | <span data-ttu-id="b42e2-372">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="b42e2-372">Text appears under the subtitle.</span></span> <span data-ttu-id="b42e2-373">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="b42e2-373">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="b42e2-374">images</span><span class="sxs-lookup"><span data-stu-id="b42e2-374">images</span></span> | <span data-ttu-id="b42e2-375">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="b42e2-375">Array of images</span></span> | <span data-ttu-id="b42e2-376">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="b42e2-376">Image displayed at the top of the card.</span></span> <span data-ttu-id="b42e2-377">Proportions 1:1 carré.</span><span class="sxs-lookup"><span data-stu-id="b42e2-377">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="b42e2-378">buttons</span><span class="sxs-lookup"><span data-stu-id="b42e2-378">buttons</span></span> | <span data-ttu-id="b42e2-379">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="b42e2-379">Array of action objects</span></span> | <span data-ttu-id="b42e2-380">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="b42e2-380">Set of actions applicable to the current card.</span></span> <span data-ttu-id="b42e2-381">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="b42e2-381">Maximum 6.</span></span> |
| <span data-ttu-id="b42e2-382">tap</span><span class="sxs-lookup"><span data-stu-id="b42e2-382">tap</span></span> | <span data-ttu-id="b42e2-383">Objet Action</span><span class="sxs-lookup"><span data-stu-id="b42e2-383">Action object</span></span> | <span data-ttu-id="b42e2-384">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="b42e2-384">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="b42e2-385">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="b42e2-385">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="b42e2-386">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b42e2-386">Additional information</span></span>

<span data-ttu-id="b42e2-387">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="b42e2-387">Bot Framework reference:</span></span>

* [<span data-ttu-id="b42e2-388">Carte miniature Node.js</span><span class="sxs-lookup"><span data-stu-id="b42e2-388">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="b42e2-389">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="b42e2-389">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="b42e2-390">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="b42e2-390">Card collections</span></span>

<span data-ttu-id="b42e2-391">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-391">Teams supports Card collections.</span></span>

<span data-ttu-id="b42e2-392">Les collections de cartes incluent `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="b42e2-392">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="b42e2-393">Ces collections contiennent des cartes adaptatives, hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="b42e2-393">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="b42e2-394">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="b42e2-394">Carousel collection</span></span>

<span data-ttu-id="b42e2-395">La [disposition de carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="b42e2-395">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="b42e2-396">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="b42e2-396">Support for carousel collections</span></span>

| <span data-ttu-id="b42e2-397">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-397">Bots in Teams</span></span> | <span data-ttu-id="b42e2-398">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-398">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-399">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-399">Connectors</span></span> | <span data-ttu-id="b42e2-400">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-400">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-401">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-401">✔</span></span> | <span data-ttu-id="b42e2-402">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-402">✖</span></span> | <span data-ttu-id="b42e2-403">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-403">✖</span></span> | <span data-ttu-id="b42e2-404">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-404">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="b42e2-405">Un carrousel peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="b42e2-405">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="b42e2-406">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="b42e2-406">Properties of a carousel card</span></span>

<span data-ttu-id="b42e2-407">Les propriétés d’une carte carrousel sont identiques à celles des cartes hero et miniatures.</span><span class="sxs-lookup"><span data-stu-id="b42e2-407">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="b42e2-408">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="b42e2-408">Example of a carousel collection</span></span>

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="b42e2-410">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="b42e2-410">Syntax for carousel collections</span></span>

<span data-ttu-id="b42e2-411">`builder.AttachmentLayoutTypes.Carousel` est la syntaxe des collections de carrousels.</span><span class="sxs-lookup"><span data-stu-id="b42e2-411">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="b42e2-412">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="b42e2-412">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="b42e2-413">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="b42e2-413">Support for list collections</span></span>

<span data-ttu-id="b42e2-414">La disposition de liste affiche une liste de cartes empilées verticalement, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="b42e2-414">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="b42e2-415">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-415">Bots in Teams</span></span> | <span data-ttu-id="b42e2-416">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="b42e2-416">Messaging extensions</span></span>  | <span data-ttu-id="b42e2-417">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b42e2-417">Connectors</span></span> | <span data-ttu-id="b42e2-418">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b42e2-418">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b42e2-419">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-419">✔</span></span> | <span data-ttu-id="b42e2-420">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-420">✔</span></span> | <span data-ttu-id="b42e2-421">✖</span><span class="sxs-lookup"><span data-stu-id="b42e2-421">✖</span></span> | <span data-ttu-id="b42e2-422">✔</span><span class="sxs-lookup"><span data-stu-id="b42e2-422">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="b42e2-423">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="b42e2-423">Example of a list collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="b42e2-425">Les propriétés sont identiques à la carte hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="b42e2-425">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="b42e2-426">Une liste peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="b42e2-426">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="b42e2-427">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="b42e2-427">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="b42e2-428">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="b42e2-428">Syntax for list collections</span></span>

<span data-ttu-id="b42e2-429">`builder.AttachmentLayout.list` est la syntaxe des collections de listes.</span><span class="sxs-lookup"><span data-stu-id="b42e2-429">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="b42e2-430">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="b42e2-430">Cards not supported in Teams</span></span>

<span data-ttu-id="b42e2-431">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas Teams :</span><span class="sxs-lookup"><span data-stu-id="b42e2-431">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="b42e2-432">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="b42e2-432">Animation cards</span></span>
* <span data-ttu-id="b42e2-433">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="b42e2-433">Audio cards</span></span>
* <span data-ttu-id="b42e2-434">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="b42e2-434">Video cards</span></span>
