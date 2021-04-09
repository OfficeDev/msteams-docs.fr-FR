---
title: Référence de cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: b9e11a6a6cb6de370323a3b07e2451a3abc41f12
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634536"
---
# <a name="cards-reference"></a><span data-ttu-id="e704f-104">Référence de cartes</span><span class="sxs-lookup"><span data-stu-id="e704f-104">Cards reference</span></span>

<span data-ttu-id="e704f-105">Les cartes répertoriées dans ce document sont pris en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e704f-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="e704f-106">Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et certaines cartes Teams ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="e704f-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="e704f-107">Les différences sont appelées dans les références de ce document.</span><span class="sxs-lookup"><span data-stu-id="e704f-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="e704f-108">Exemples de cartes</span><span class="sxs-lookup"><span data-stu-id="e704f-108">Card examples</span></span>

<span data-ttu-id="e704f-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder v3.</span><span class="sxs-lookup"><span data-stu-id="e704f-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="e704f-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="e704f-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="e704f-111">.NET</span><span class="sxs-lookup"><span data-stu-id="e704f-111">.NET</span></span>
  * [<span data-ttu-id="e704f-112">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="e704f-112">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="e704f-113">Exemple de code cartes Bot Builder v4</span><span class="sxs-lookup"><span data-stu-id="e704f-113">Cards sample code Bot Builder v4</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* <span data-ttu-id="e704f-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="e704f-114">Node.js</span></span>
  * [<span data-ttu-id="e704f-115">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="e704f-115">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="e704f-116">Exemple de code cartes Bot Builder v4</span><span class="sxs-lookup"><span data-stu-id="e704f-116">Cards sample code Bot Builder v4</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a><span data-ttu-id="e704f-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="e704f-117">Types of cards</span></span>

<span data-ttu-id="e704f-118">Ce tableau indique les types de cartes disponibles :</span><span class="sxs-lookup"><span data-stu-id="e704f-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="e704f-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="e704f-119">Card type</span></span> | <span data-ttu-id="e704f-120">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e704f-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="e704f-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="e704f-122">Cette carte est hautement personnalisable et peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e704f-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="e704f-123">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="e704f-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="e704f-124">Cette carte contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="e704f-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="e704f-125">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="e704f-125">List card</span></span>](#list-card) | <span data-ttu-id="e704f-126">Cette carte est une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="e704f-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="e704f-127">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e704f-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="e704f-128">Cette carte possède une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="e704f-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="e704f-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="e704f-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="e704f-130">Cette carte fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e704f-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="e704f-131">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="e704f-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="e704f-132">Cette carte permet à un bot de demander à un utilisateur de se rendre.</span><span class="sxs-lookup"><span data-stu-id="e704f-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="e704f-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="e704f-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="e704f-134">Cette carte contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="e704f-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="e704f-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="e704f-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="e704f-136">Ces cartes sont utilisées pour renvoyer plusieurs éléments en une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="e704f-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="e704f-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="e704f-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="e704f-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="e704f-138">Inline card images</span></span>

<span data-ttu-id="e704f-139">La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="e704f-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="e704f-140">Pour des raisons de performances, il est vivement recommandé d’héberger l’image sur un réseau de distribution de contenu (CDN) public.</span><span class="sxs-lookup"><span data-stu-id="e704f-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="e704f-141">La taille des images est réduite ou réduite tout en conservant les proportions pour couvrir la zone d’image.</span><span class="sxs-lookup"><span data-stu-id="e704f-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="e704f-142">Les images sont ensuite rogées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="e704f-143">Les images doivent être au maximum 1024×1024, au format PNG, JPEG ou GIF, et ne pas prendre en charge les images GIF animées.</span><span class="sxs-lookup"><span data-stu-id="e704f-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="e704f-144">Propriété</span><span class="sxs-lookup"><span data-stu-id="e704f-144">Property</span></span> | <span data-ttu-id="e704f-145">Type</span><span class="sxs-lookup"><span data-stu-id="e704f-145">Type</span></span>  | <span data-ttu-id="e704f-146">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e704f-147">url</span><span class="sxs-lookup"><span data-stu-id="e704f-147">url</span></span> | <span data-ttu-id="e704f-148">URL</span><span class="sxs-lookup"><span data-stu-id="e704f-148">URL</span></span> | <span data-ttu-id="e704f-149">URL HTTPS vers l’image.</span><span class="sxs-lookup"><span data-stu-id="e704f-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="e704f-150">alt</span><span class="sxs-lookup"><span data-stu-id="e704f-150">alt</span></span> | <span data-ttu-id="e704f-151">Chaîne</span><span class="sxs-lookup"><span data-stu-id="e704f-151">String</span></span> | <span data-ttu-id="e704f-152">Description accessible de l’image.</span><span class="sxs-lookup"><span data-stu-id="e704f-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="e704f-153">Si une carte inclut une URL d’image qui passe par une redirection avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="e704f-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="e704f-154">Cela se produit pour les images partagées sur le cloud public.</span><span class="sxs-lookup"><span data-stu-id="e704f-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="e704f-155">Boutons</span><span class="sxs-lookup"><span data-stu-id="e704f-155">Buttons</span></span>

<span data-ttu-id="e704f-156">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="e704f-157">Le texte du bouton est toujours sur une seule ligne et tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="e704f-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="e704f-158">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne sont pas affichés.</span><span class="sxs-lookup"><span data-stu-id="e704f-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="e704f-159">Pour plus d’informations, voir [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="e704f-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="e704f-160">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="e704f-160">Card formatting</span></span>

<span data-ttu-id="e704f-161">Pour plus d’informations sur la mise en forme du texte dans les cartes, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="e704f-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="e704f-162">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="e704f-162">Adaptive card</span></span>

<span data-ttu-id="e704f-163">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e704f-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="e704f-164">Voir [cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="e704f-164">See [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="e704f-165">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="e704f-165">Support for adaptive cards</span></span>

| <span data-ttu-id="e704f-166">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-166">Bots in Teams</span></span> | <span data-ttu-id="e704f-167">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-167">Messaging extensions</span></span>  | <span data-ttu-id="e704f-168">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-168">Connectors</span></span> | <span data-ttu-id="e704f-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-170">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-170">✔</span></span> | <span data-ttu-id="e704f-171">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-171">✔</span></span> | <span data-ttu-id="e704f-172">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-172">✖</span></span> | <span data-ttu-id="e704f-173">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="e704f-174">La plateforme Teams prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="e704f-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="e704f-175">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="e704f-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="e704f-176">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="e704f-176">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="e704f-178">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="e704f-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="e704f-179">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="e704f-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="e704f-180">Cartes adaptatives Node.js</span><span class="sxs-lookup"><span data-stu-id="e704f-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="e704f-181">Carte adaptative C #</span><span class="sxs-lookup"><span data-stu-id="e704f-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="e704f-182">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="e704f-182">Hero card</span></span>

<span data-ttu-id="e704f-183">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="e704f-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="e704f-184">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="e704f-184">Support for hero cards</span></span>

| <span data-ttu-id="e704f-185">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-185">Bots in Teams</span></span> | <span data-ttu-id="e704f-186">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-186">Messaging extensions</span></span>  | <span data-ttu-id="e704f-187">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-187">Connectors</span></span> | <span data-ttu-id="e704f-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-189">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-189">✔</span></span> | <span data-ttu-id="e704f-190">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-190">✔</span></span> | <span data-ttu-id="e704f-191">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-191">✖</span></span> | <span data-ttu-id="e704f-192">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="e704f-193">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="e704f-193">Properties of a hero card</span></span>

| <span data-ttu-id="e704f-194">Propriété</span><span class="sxs-lookup"><span data-stu-id="e704f-194">Property</span></span> | <span data-ttu-id="e704f-195">Type</span><span class="sxs-lookup"><span data-stu-id="e704f-195">Type</span></span>  | <span data-ttu-id="e704f-196">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e704f-197">title</span><span class="sxs-lookup"><span data-stu-id="e704f-197">title</span></span> | <span data-ttu-id="e704f-198">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-198">Rich text</span></span> | <span data-ttu-id="e704f-199">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-199">Title of the card.</span></span> <span data-ttu-id="e704f-200">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="e704f-201">subtitle</span><span class="sxs-lookup"><span data-stu-id="e704f-201">subtitle</span></span> | <span data-ttu-id="e704f-202">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-202">Rich text</span></span> | <span data-ttu-id="e704f-203">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-203">Subtitle of the card.</span></span> <span data-ttu-id="e704f-204">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e704f-205">text</span><span class="sxs-lookup"><span data-stu-id="e704f-205">text</span></span> | <span data-ttu-id="e704f-206">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-206">Rich text</span></span> | <span data-ttu-id="e704f-207">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="e704f-207">Text appears under the subtitle.</span></span> <span data-ttu-id="e704f-208">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="e704f-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="e704f-209">images</span><span class="sxs-lookup"><span data-stu-id="e704f-209">images</span></span> | <span data-ttu-id="e704f-210">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="e704f-210">Array of images</span></span> | <span data-ttu-id="e704f-211">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="e704f-212">Proportions 16:9.</span><span class="sxs-lookup"><span data-stu-id="e704f-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="e704f-213">buttons</span><span class="sxs-lookup"><span data-stu-id="e704f-213">buttons</span></span> | <span data-ttu-id="e704f-214">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="e704f-214">Array of action objects</span></span> | <span data-ttu-id="e704f-215">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="e704f-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="e704f-216">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="e704f-216">Maximum 6.</span></span> |
| <span data-ttu-id="e704f-217">tap</span><span class="sxs-lookup"><span data-stu-id="e704f-217">tap</span></span> | <span data-ttu-id="e704f-218">Objet Action</span><span class="sxs-lookup"><span data-stu-id="e704f-218">Action object</span></span> | <span data-ttu-id="e704f-219">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="e704f-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="e704f-220">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="e704f-220">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="e704f-222">Informations supplémentaires sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="e704f-222">Additional information on hero cards</span></span>

<span data-ttu-id="e704f-223">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="e704f-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="e704f-224">Carte Hero Node.js</span><span class="sxs-lookup"><span data-stu-id="e704f-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="e704f-225">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="e704f-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="e704f-226">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="e704f-226">List card</span></span>

<span data-ttu-id="e704f-227">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="e704f-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="e704f-228">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="e704f-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="e704f-229">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="e704f-229">Support for list cards</span></span>

| <span data-ttu-id="e704f-230">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-230">Bots in Teams</span></span> | <span data-ttu-id="e704f-231">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-231">Messaging extensions</span></span>  | <span data-ttu-id="e704f-232">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-232">Connectors</span></span> | <span data-ttu-id="e704f-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-234">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-234">✔</span></span> | <span data-ttu-id="e704f-235">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-235">✖</span></span> | <span data-ttu-id="e704f-236">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-236">✖</span></span> |<span data-ttu-id="e704f-237">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="e704f-238">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="e704f-238">Properties of a list card</span></span>

| <span data-ttu-id="e704f-239">Propriété</span><span class="sxs-lookup"><span data-stu-id="e704f-239">Property</span></span> | <span data-ttu-id="e704f-240">Type</span><span class="sxs-lookup"><span data-stu-id="e704f-240">Type</span></span>  | <span data-ttu-id="e704f-241">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e704f-242">title</span><span class="sxs-lookup"><span data-stu-id="e704f-242">title</span></span> | <span data-ttu-id="e704f-243">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-243">Rich text</span></span> | <span data-ttu-id="e704f-244">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-244">Title of the card.</span></span> <span data-ttu-id="e704f-245">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e704f-246">éléments</span><span class="sxs-lookup"><span data-stu-id="e704f-246">items</span></span> | <span data-ttu-id="e704f-247">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="e704f-247">Array of list items</span></span> ||
| <span data-ttu-id="e704f-248">buttons</span><span class="sxs-lookup"><span data-stu-id="e704f-248">buttons</span></span> | <span data-ttu-id="e704f-249">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="e704f-249">Array of action objects</span></span> | <span data-ttu-id="e704f-250">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="e704f-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="e704f-251">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="e704f-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="e704f-252">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="e704f-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="e704f-253">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e704f-253">Office 365 connector card</span></span>

<span data-ttu-id="e704f-254">La carte de connecteur Office 365 est prise en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e704f-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="e704f-255">Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="e704f-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="e704f-256">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="e704f-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="e704f-257">Pour les différences entre les cartes de connecteur et la carte O365, voir remarques sur la carte de [connecteur Office 365.](#notes-on-the-office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="e704f-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="e704f-258">Prise en charge des cartes de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e704f-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="e704f-259">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-259">Bots in Teams</span></span> | <span data-ttu-id="e704f-260">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-260">Messaging extensions</span></span>  | <span data-ttu-id="e704f-261">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-261">Connectors</span></span> | <span data-ttu-id="e704f-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-263">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-263">✔</span></span> | <span data-ttu-id="e704f-264">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-264">✔</span></span> | <span data-ttu-id="e704f-265">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-265">✔</span></span> | <span data-ttu-id="e704f-266">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="e704f-267">Propriétés de la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e704f-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="e704f-268">Propriété</span><span class="sxs-lookup"><span data-stu-id="e704f-268">Property</span></span> | <span data-ttu-id="e704f-269">Type</span><span class="sxs-lookup"><span data-stu-id="e704f-269">Type</span></span>  | <span data-ttu-id="e704f-270">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e704f-271">title</span><span class="sxs-lookup"><span data-stu-id="e704f-271">title</span></span> | <span data-ttu-id="e704f-272">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-272">Rich text</span></span> | <span data-ttu-id="e704f-273">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-273">Title of the card.</span></span> <span data-ttu-id="e704f-274">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="e704f-275">résumé</span><span class="sxs-lookup"><span data-stu-id="e704f-275">summary</span></span> | <span data-ttu-id="e704f-276">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-276">Rich text</span></span> | <span data-ttu-id="e704f-277">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-277">Summary of the card.</span></span> <span data-ttu-id="e704f-278">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="e704f-279">text</span><span class="sxs-lookup"><span data-stu-id="e704f-279">text</span></span> | <span data-ttu-id="e704f-280">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-280">Rich text</span></span> | <span data-ttu-id="e704f-281">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="e704f-281">Text appears under the subtitle.</span></span> <span data-ttu-id="e704f-282">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="e704f-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="e704f-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="e704f-283">themeColor</span></span> | <span data-ttu-id="e704f-284">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="e704f-284">HEX string</span></span> | <span data-ttu-id="e704f-285">Couleur qui remplace l’accentColor fourni à partir du manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="e704f-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="e704f-286">Remarques sur la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e704f-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="e704f-287">Les cartes de connecteur Office 365 fonctionnent correctement dans Microsoft Teams, y compris les [actions ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="e704f-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="e704f-288">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="e704f-289">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e704f-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="e704f-290">Pour un bot, l’action déclenche une activité qui envoie uniquement l’ID d’action et le `HttpPOST` `invoke` corps au bot.</span><span class="sxs-lookup"><span data-stu-id="e704f-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="e704f-291">Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.</span><span class="sxs-lookup"><span data-stu-id="e704f-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="e704f-292">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="e704f-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="e704f-293">Tous les champs de texte prise en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="e704f-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="e704f-294">Vous pouvez contrôler les sections qui utilisent markdown ou HTML en fixant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="e704f-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="e704f-295">Par défaut, `markdown` est définie sur `true` .</span><span class="sxs-lookup"><span data-stu-id="e704f-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="e704f-296">Si vous souhaitez utiliser du code HTML à la place, définissez `markdown` sur `false` .</span><span class="sxs-lookup"><span data-stu-id="e704f-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="e704f-297">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="e704f-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="e704f-298">Pour spécifier le style de rendu `activityImage` pour , vous pouvez définir comme suit `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="e704f-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="e704f-299">Valeur</span><span class="sxs-lookup"><span data-stu-id="e704f-299">Value</span></span> | <span data-ttu-id="e704f-300">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="e704f-301">Valeur par défaut ; `activityImage` est rogché en tant que cercle.</span><span class="sxs-lookup"><span data-stu-id="e704f-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="e704f-302">`activityImage` est affiché sous forme de rectangle et conserve ses proportions.</span><span class="sxs-lookup"><span data-stu-id="e704f-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="e704f-303">Pour plus d’informations sur les propriétés de carte de connecteur, voir la [référence de carte de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="e704f-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="e704f-304">Les seules propriétés de carte de connecteur que Microsoft Teams ne prend pas en charge actuellement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e704f-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="e704f-305">`startGroup` toujours traité comme `true` dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="e704f-306">Exemple de carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e704f-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="e704f-307">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="e704f-307">Receipt card</span></span>

<span data-ttu-id="e704f-308">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="e704f-308">Teams supports receipt card.</span></span> <span data-ttu-id="e704f-309">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e704f-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="e704f-310">Il contient généralement la liste des éléments à inclure sur le reçu, par exemple les informations fiscales et totales.</span><span class="sxs-lookup"><span data-stu-id="e704f-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="e704f-311">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="e704f-311">Support for receipt cards</span></span>

| <span data-ttu-id="e704f-312">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-312">Bots in Teams</span></span> | <span data-ttu-id="e704f-313">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-313">Messaging extensions</span></span>  | <span data-ttu-id="e704f-314">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-314">Connectors</span></span> | <span data-ttu-id="e704f-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-316">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-316">✔</span></span> | <span data-ttu-id="e704f-317">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-317">✔</span></span> | <span data-ttu-id="e704f-318">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-318">✖</span></span> | <span data-ttu-id="e704f-319">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="e704f-320">Exemple de carte de reçu</span><span class="sxs-lookup"><span data-stu-id="e704f-320">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="e704f-322">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="e704f-322">Additional information on receipt cards</span></span>

<span data-ttu-id="e704f-323">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="e704f-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="e704f-324">Carte de réception Node.js</span><span class="sxs-lookup"><span data-stu-id="e704f-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="e704f-325">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="e704f-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="e704f-326">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="e704f-326">Signin card</span></span>

<span data-ttu-id="e704f-327">La carte de signature permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="e704f-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="e704f-328">Il est pris en charge dans Teams sous une forme légèrement différente de celle de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e704f-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="e704f-329">La carte de signin dans Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de signin dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="e704f-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="e704f-330">L’action de signin peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="e704f-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="e704f-331">Pour plus d’informations sur l’authentification, voir [flux d’authentification Microsoft Teams pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="e704f-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="e704f-332">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="e704f-332">Support for signin cards</span></span>

| <span data-ttu-id="e704f-333">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-333">Bots in Teams</span></span> | <span data-ttu-id="e704f-334">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-334">Messaging extensions</span></span>  | <span data-ttu-id="e704f-335">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-335">Connectors</span></span> | <span data-ttu-id="e704f-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-337">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-337">✔</span></span> | <span data-ttu-id="e704f-338">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-338">✖</span></span> | <span data-ttu-id="e704f-339">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-339">✖</span></span> | <span data-ttu-id="e704f-340">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="e704f-341">Informations supplémentaires sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="e704f-341">Additional information on signin cards</span></span>

<span data-ttu-id="e704f-342">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="e704f-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="e704f-343">Carte de Node.js</span><span class="sxs-lookup"><span data-stu-id="e704f-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="e704f-344">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="e704f-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="e704f-345">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="e704f-345">Thumbnail card</span></span>

<span data-ttu-id="e704f-346">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="e704f-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="e704f-347">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="e704f-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="e704f-348">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-348">Bots in Teams</span></span> | <span data-ttu-id="e704f-349">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-349">Messaging extensions</span></span>  | <span data-ttu-id="e704f-350">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-350">Connectors</span></span> | <span data-ttu-id="e704f-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-352">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-352">✔</span></span> | <span data-ttu-id="e704f-353">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-353">✔</span></span> | <span data-ttu-id="e704f-354">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-354">✖</span></span> | <span data-ttu-id="e704f-355">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-355">✔</span></span> |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="e704f-357">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="e704f-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="e704f-358">Propriété</span><span class="sxs-lookup"><span data-stu-id="e704f-358">Property</span></span> | <span data-ttu-id="e704f-359">Type</span><span class="sxs-lookup"><span data-stu-id="e704f-359">Type</span></span>  | <span data-ttu-id="e704f-360">Description</span><span class="sxs-lookup"><span data-stu-id="e704f-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e704f-361">title</span><span class="sxs-lookup"><span data-stu-id="e704f-361">title</span></span> | <span data-ttu-id="e704f-362">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-362">Rich text</span></span> | <span data-ttu-id="e704f-363">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-363">Title of the card.</span></span> <span data-ttu-id="e704f-364">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e704f-365">subtitle</span><span class="sxs-lookup"><span data-stu-id="e704f-365">subtitle</span></span> | <span data-ttu-id="e704f-366">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-366">Rich text</span></span> | <span data-ttu-id="e704f-367">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-367">Subtitle of the card.</span></span> <span data-ttu-id="e704f-368">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="e704f-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="e704f-369">text</span><span class="sxs-lookup"><span data-stu-id="e704f-369">text</span></span> | <span data-ttu-id="e704f-370">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="e704f-370">Rich text</span></span> | <span data-ttu-id="e704f-371">Le texte apparaît sous le sous-titre.</span><span class="sxs-lookup"><span data-stu-id="e704f-371">Text appears under the subtitle.</span></span> <span data-ttu-id="e704f-372">Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)</span><span class="sxs-lookup"><span data-stu-id="e704f-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="e704f-373">images</span><span class="sxs-lookup"><span data-stu-id="e704f-373">images</span></span> | <span data-ttu-id="e704f-374">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="e704f-374">Array of images</span></span> | <span data-ttu-id="e704f-375">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="e704f-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="e704f-376">Proportions 1:1 carré.</span><span class="sxs-lookup"><span data-stu-id="e704f-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="e704f-377">buttons</span><span class="sxs-lookup"><span data-stu-id="e704f-377">buttons</span></span> | <span data-ttu-id="e704f-378">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="e704f-378">Array of action objects</span></span> | <span data-ttu-id="e704f-379">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="e704f-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="e704f-380">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="e704f-380">Maximum 6.</span></span> |
| <span data-ttu-id="e704f-381">tap</span><span class="sxs-lookup"><span data-stu-id="e704f-381">tap</span></span> | <span data-ttu-id="e704f-382">Objet Action</span><span class="sxs-lookup"><span data-stu-id="e704f-382">Action object</span></span> | <span data-ttu-id="e704f-383">Activé lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="e704f-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="e704f-384">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="e704f-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="e704f-385">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e704f-385">Additional information</span></span>

<span data-ttu-id="e704f-386">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="e704f-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="e704f-387">Carte miniature Node.js</span><span class="sxs-lookup"><span data-stu-id="e704f-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="e704f-388">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="e704f-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="e704f-389">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="e704f-389">Card collections</span></span>

<span data-ttu-id="e704f-390">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="e704f-390">Teams supports Card collections.</span></span>

<span data-ttu-id="e704f-391">Les collections de cartes incluent `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="e704f-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="e704f-392">Ces collections contiennent des cartes adaptatives, hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="e704f-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="e704f-393">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="e704f-393">Carousel collection</span></span>

<span data-ttu-id="e704f-394">La [disposition de carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) présente un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="e704f-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="e704f-395">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="e704f-395">Support for carousel collections</span></span>

| <span data-ttu-id="e704f-396">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-396">Bots in Teams</span></span> | <span data-ttu-id="e704f-397">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-397">Messaging extensions</span></span>  | <span data-ttu-id="e704f-398">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-398">Connectors</span></span> | <span data-ttu-id="e704f-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-400">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-400">✔</span></span> | <span data-ttu-id="e704f-401">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-401">✖</span></span> | <span data-ttu-id="e704f-402">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-402">✖</span></span> | <span data-ttu-id="e704f-403">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="e704f-404">Un carrousel peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="e704f-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="e704f-405">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="e704f-405">Properties of a carousel card</span></span>

<span data-ttu-id="e704f-406">Les propriétés d’une carte carrousel sont identiques à celles des cartes hero et miniatures.</span><span class="sxs-lookup"><span data-stu-id="e704f-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="e704f-407">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="e704f-407">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="e704f-409">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="e704f-409">Syntax for carousel collections</span></span>

<span data-ttu-id="e704f-410">`builder.AttachmentLayoutTypes.Carousel` est la syntaxe des collections de carrousels.</span><span class="sxs-lookup"><span data-stu-id="e704f-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="e704f-411">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="e704f-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="e704f-412">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="e704f-412">Support for list collections</span></span>

<span data-ttu-id="e704f-413">La disposition de liste affiche une liste empilée verticalement de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="e704f-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="e704f-414">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-414">Bots in Teams</span></span> | <span data-ttu-id="e704f-415">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="e704f-415">Messaging extensions</span></span>  | <span data-ttu-id="e704f-416">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e704f-416">Connectors</span></span> | <span data-ttu-id="e704f-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e704f-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e704f-418">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-418">✔</span></span> | <span data-ttu-id="e704f-419">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-419">✔</span></span> | <span data-ttu-id="e704f-420">✖</span><span class="sxs-lookup"><span data-stu-id="e704f-420">✖</span></span> | <span data-ttu-id="e704f-421">✔</span><span class="sxs-lookup"><span data-stu-id="e704f-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="e704f-422">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="e704f-422">Example of a list collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="e704f-424">Les propriétés sont identiques à la carte hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="e704f-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="e704f-425">Une liste peut afficher un maximum de dix cartes par message.</span><span class="sxs-lookup"><span data-stu-id="e704f-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="e704f-426">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="e704f-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="e704f-427">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="e704f-427">Syntax for list collections</span></span>

<span data-ttu-id="e704f-428">`builder.AttachmentLayout.list` est la syntaxe des collections de listes.</span><span class="sxs-lookup"><span data-stu-id="e704f-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="e704f-429">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="e704f-429">Cards not supported in Teams</span></span>

<span data-ttu-id="e704f-430">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas pris en charge par Teams :</span><span class="sxs-lookup"><span data-stu-id="e704f-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="e704f-431">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="e704f-431">Animation cards</span></span>
* <span data-ttu-id="e704f-432">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="e704f-432">Audio cards</span></span>
* <span data-ttu-id="e704f-433">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="e704f-433">Video cards</span></span>
