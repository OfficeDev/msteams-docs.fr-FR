---
title: Référence des cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: 5cb289738f379dedf53f3a96a7dcff61b908e901
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827934"
---
# <a name="cards-reference"></a><span data-ttu-id="127d6-104">Référence de cartes</span><span class="sxs-lookup"><span data-stu-id="127d6-104">Cards reference</span></span>

<span data-ttu-id="127d6-105">Les cartes répertoriées dans cette section sont pris en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="127d6-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="127d6-106">Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="127d6-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="127d6-107">Les différences sont appelées dans les références de ce document.</span><span class="sxs-lookup"><span data-stu-id="127d6-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="127d6-108">Exemples de carte</span><span class="sxs-lookup"><span data-stu-id="127d6-108">Card examples</span></span>

<span data-ttu-id="127d6-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="127d6-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="127d6-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="127d6-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="127d6-111">.NET</span><span class="sxs-lookup"><span data-stu-id="127d6-111">.NET</span></span>
  * [<span data-ttu-id="127d6-112">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="127d6-112">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="127d6-113">Exemple de code de cartes (Bot Builder v4)</span><span class="sxs-lookup"><span data-stu-id="127d6-113">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* <span data-ttu-id="127d6-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="127d6-114">Node.js</span></span>
  * [<span data-ttu-id="127d6-115">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="127d6-115">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="127d6-116">Exemple de code de cartes (Bot Builder v4)</span><span class="sxs-lookup"><span data-stu-id="127d6-116">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a><span data-ttu-id="127d6-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="127d6-117">Types of cards</span></span>

<span data-ttu-id="127d6-118">Ce tableau indique les types de cartes disponibles :</span><span class="sxs-lookup"><span data-stu-id="127d6-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="127d6-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="127d6-119">Card type</span></span> | <span data-ttu-id="127d6-120">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="127d6-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="127d6-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="127d6-122">Carte hautement personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="127d6-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="127d6-123">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="127d6-124">Contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="127d6-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="127d6-125">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="127d6-125">List card</span></span>](#list-card) | <span data-ttu-id="127d6-126">Liste de défilement d’éléments.</span><span class="sxs-lookup"><span data-stu-id="127d6-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="127d6-127">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="127d6-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="127d6-128">Disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="127d6-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="127d6-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="127d6-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="127d6-130">Fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="127d6-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="127d6-131">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="127d6-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="127d6-132">Permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="127d6-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="127d6-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="127d6-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="127d6-134">Contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="127d6-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="127d6-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="127d6-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="127d6-136">Utilisé pour renvoyer plusieurs éléments dans une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="127d6-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="127d6-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="127d6-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="127d6-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="127d6-138">Inline card images</span></span>

<span data-ttu-id="127d6-139">La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="127d6-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="127d6-140">Pour des raisons de performances, il est vivement recommandé d’héberger l’image sur un réseau de distribution de contenu (CDN) public.</span><span class="sxs-lookup"><span data-stu-id="127d6-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="127d6-141">La taille des images est réduite ou monter en puissance tout en conservant les proportions pour couvrir la zone d’image, puis rognées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="127d6-142">Les images doivent être au maximum 1024×1024, au format PNG, JPEG ou GIF, et l’image GIF animée n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="127d6-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="127d6-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="127d6-143">Property</span></span> | <span data-ttu-id="127d6-144">Type</span><span class="sxs-lookup"><span data-stu-id="127d6-144">Type</span></span>  | <span data-ttu-id="127d6-145">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="127d6-146">url</span><span class="sxs-lookup"><span data-stu-id="127d6-146">url</span></span> | <span data-ttu-id="127d6-147">URL</span><span class="sxs-lookup"><span data-stu-id="127d6-147">URL</span></span> | <span data-ttu-id="127d6-148">URL HTTPS vers l’image</span><span class="sxs-lookup"><span data-stu-id="127d6-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="127d6-149">alt</span><span class="sxs-lookup"><span data-stu-id="127d6-149">alt</span></span> | <span data-ttu-id="127d6-150">String</span><span class="sxs-lookup"><span data-stu-id="127d6-150">String</span></span> | <span data-ttu-id="127d6-151">Description accessible de l’image</span><span class="sxs-lookup"><span data-stu-id="127d6-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="127d6-152">Boutons</span><span class="sxs-lookup"><span data-stu-id="127d6-152">Buttons</span></span>

<span data-ttu-id="127d6-153">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="127d6-154">Le texte du bouton est toujours sur une seule ligne et est tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="127d6-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="127d6-155">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne s’afficheront pas.</span><span class="sxs-lookup"><span data-stu-id="127d6-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="127d6-156">Pour plus [d’informations,](~/task-modules-and-cards/cards/cards-actions.md) voir Actions de carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="127d6-157">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="127d6-157">Card formatting</span></span>

<span data-ttu-id="127d6-158">Pour [plus d’informations](~/task-modules-and-cards/cards/cards-format.md) sur la mise en forme du texte dans les cartes, voir Formatage de carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="127d6-159">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="127d6-159">Adaptive card</span></span>

<span data-ttu-id="127d6-160">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="127d6-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="127d6-161">Voir [Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="127d6-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="127d6-162">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="127d6-162">Support for adaptive cards</span></span>

| <span data-ttu-id="127d6-163">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-163">Bots in Teams</span></span> | <span data-ttu-id="127d6-164">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-164">Messaging extensions</span></span>  | <span data-ttu-id="127d6-165">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-165">Connectors</span></span> | <span data-ttu-id="127d6-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-167">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-167">✔</span></span> | <span data-ttu-id="127d6-168">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-168">✔</span></span> | <span data-ttu-id="127d6-169">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-169">✖</span></span> | <span data-ttu-id="127d6-170">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="127d6-171">La plateforme Teams prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="127d6-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="127d6-172">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="127d6-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="127d6-173">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="127d6-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="127d6-175">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="127d6-175">Additional information on adaptive cards</span></span>

<span data-ttu-id="127d6-176">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="127d6-176">Bot Framework reference:</span></span>

* [<span data-ttu-id="127d6-177">Nœud cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="127d6-177">Adaptive cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="127d6-178">Carte adaptative C #</span><span class="sxs-lookup"><span data-stu-id="127d6-178">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="127d6-179">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-179">Hero card</span></span>

<span data-ttu-id="127d6-180">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="127d6-180">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="127d6-181">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-181">Support for hero cards</span></span>

| <span data-ttu-id="127d6-182">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-182">Bots in Teams</span></span> | <span data-ttu-id="127d6-183">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-183">Messaging Extensions</span></span>  | <span data-ttu-id="127d6-184">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-184">Connectors</span></span> | <span data-ttu-id="127d6-185">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-185">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-186">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-186">✔</span></span> | <span data-ttu-id="127d6-187">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-187">✔</span></span> | <span data-ttu-id="127d6-188">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-188">✖</span></span> | <span data-ttu-id="127d6-189">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-189">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="127d6-190">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-190">Properties of a hero card</span></span>

| <span data-ttu-id="127d6-191">Propriété</span><span class="sxs-lookup"><span data-stu-id="127d6-191">Property</span></span> | <span data-ttu-id="127d6-192">Type</span><span class="sxs-lookup"><span data-stu-id="127d6-192">Type</span></span>  | <span data-ttu-id="127d6-193">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-193">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="127d6-194">title</span><span class="sxs-lookup"><span data-stu-id="127d6-194">title</span></span> | <span data-ttu-id="127d6-195">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-195">Rich text</span></span> | <span data-ttu-id="127d6-196">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-196">Title of the card.</span></span> <span data-ttu-id="127d6-197">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-197">Maximum 2 lines.</span></span> |
| <span data-ttu-id="127d6-198">subtitle</span><span class="sxs-lookup"><span data-stu-id="127d6-198">subtitle</span></span> | <span data-ttu-id="127d6-199">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-199">Rich text</span></span> | <span data-ttu-id="127d6-200">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-200">Subtitle of the card.</span></span> <span data-ttu-id="127d6-201">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-201">Maximum 2 lines.</span></span>|
| <span data-ttu-id="127d6-202">text</span><span class="sxs-lookup"><span data-stu-id="127d6-202">text</span></span> | <span data-ttu-id="127d6-203">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-203">Rich text</span></span> | <span data-ttu-id="127d6-204">Le texte apparaît sous le sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="127d6-204">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="127d6-205">images</span><span class="sxs-lookup"><span data-stu-id="127d6-205">images</span></span> | <span data-ttu-id="127d6-206">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="127d6-206">Array of images</span></span> | <span data-ttu-id="127d6-207">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-207">Image displayed at top of card.</span></span> <span data-ttu-id="127d6-208">Proportions 16:9.</span><span class="sxs-lookup"><span data-stu-id="127d6-208">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="127d6-209">buttons</span><span class="sxs-lookup"><span data-stu-id="127d6-209">buttons</span></span> | <span data-ttu-id="127d6-210">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="127d6-210">Array of action objects</span></span> | <span data-ttu-id="127d6-211">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="127d6-211">Set of actions applicable to the current card.</span></span> <span data-ttu-id="127d6-212">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="127d6-212">Maximum 6.</span></span> |
| <span data-ttu-id="127d6-213">tap</span><span class="sxs-lookup"><span data-stu-id="127d6-213">tap</span></span> | <span data-ttu-id="127d6-214">Objet Action</span><span class="sxs-lookup"><span data-stu-id="127d6-214">Action object</span></span> | <span data-ttu-id="127d6-215">Cette action est activée lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="127d6-215">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="127d6-216">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-216">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="127d6-218">Informations supplémentaires sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-218">Additional information on hero cards</span></span>

<span data-ttu-id="127d6-219">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="127d6-219">Bot Framework reference:</span></span>

* [<span data-ttu-id="127d6-220">Nœud de carte Hero</span><span class="sxs-lookup"><span data-stu-id="127d6-220">Hero card Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="127d6-221">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="127d6-221">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="127d6-222">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="127d6-222">List card</span></span>

<span data-ttu-id="127d6-223">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="127d6-223">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="127d6-224">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="127d6-224">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="127d6-225">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="127d6-225">Support for list cards</span></span>

| <span data-ttu-id="127d6-226">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-226">Bots in Teams</span></span> | <span data-ttu-id="127d6-227">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-227">Messaging extensions</span></span>  | <span data-ttu-id="127d6-228">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-228">Connectors</span></span> | <span data-ttu-id="127d6-229">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-229">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-230">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-230">✔</span></span> | <span data-ttu-id="127d6-231">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-231">✖</span></span> | <span data-ttu-id="127d6-232">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-232">✖</span></span> |<span data-ttu-id="127d6-233">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-233">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="127d6-234">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="127d6-234">Properties of a list card</span></span>

| <span data-ttu-id="127d6-235">Propriété</span><span class="sxs-lookup"><span data-stu-id="127d6-235">Property</span></span> | <span data-ttu-id="127d6-236">Type</span><span class="sxs-lookup"><span data-stu-id="127d6-236">Type</span></span>  | <span data-ttu-id="127d6-237">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="127d6-238">title</span><span class="sxs-lookup"><span data-stu-id="127d6-238">title</span></span> | <span data-ttu-id="127d6-239">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-239">Rich text</span></span> | <span data-ttu-id="127d6-240">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-240">Title of the card.</span></span> <span data-ttu-id="127d6-241">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-241">Maximum 2 lines.</span></span>|
| <span data-ttu-id="127d6-242">éléments</span><span class="sxs-lookup"><span data-stu-id="127d6-242">items</span></span> | <span data-ttu-id="127d6-243">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="127d6-243">Array of list items</span></span>  ||
| <span data-ttu-id="127d6-244">buttons</span><span class="sxs-lookup"><span data-stu-id="127d6-244">buttons</span></span> | <span data-ttu-id="127d6-245">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="127d6-245">Array of action objects</span></span> | <span data-ttu-id="127d6-246">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="127d6-246">Set of actions applicable to the current card.</span></span> <span data-ttu-id="127d6-247">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="127d6-247">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="127d6-248">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="127d6-248">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="127d6-249">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="127d6-249">Office 365 connector card</span></span>

<span data-ttu-id="127d6-250">La carte connecteur Office 365 est prise en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="127d6-250">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="127d6-251">Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="127d6-251">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="127d6-252">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="127d6-252">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="127d6-253">Consultez la section remarques pour les différences entre les cartes de connecteur et la carte O365.</span><span class="sxs-lookup"><span data-stu-id="127d6-253">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="127d6-254">Prise en charge des cartes de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="127d6-254">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="127d6-255">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-255">Bots in Teams</span></span> | <span data-ttu-id="127d6-256">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-256">Messaging extensions</span></span>  | <span data-ttu-id="127d6-257">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-257">Connectors</span></span> | <span data-ttu-id="127d6-258">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-258">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-259">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-259">✔</span></span> | <span data-ttu-id="127d6-260">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-260">✔</span></span> | <span data-ttu-id="127d6-261">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-261">✔</span></span> | <span data-ttu-id="127d6-262">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-262">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="127d6-263">Propriétés de la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="127d6-263">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="127d6-264">Propriété</span><span class="sxs-lookup"><span data-stu-id="127d6-264">Property</span></span> | <span data-ttu-id="127d6-265">Type</span><span class="sxs-lookup"><span data-stu-id="127d6-265">Type</span></span>  | <span data-ttu-id="127d6-266">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="127d6-267">title</span><span class="sxs-lookup"><span data-stu-id="127d6-267">title</span></span> | <span data-ttu-id="127d6-268">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-268">Rich text</span></span> | <span data-ttu-id="127d6-269">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-269">Title of the card.</span></span> <span data-ttu-id="127d6-270">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-270">Maximum 2 lines.</span></span> |
| <span data-ttu-id="127d6-271">résumé</span><span class="sxs-lookup"><span data-stu-id="127d6-271">summary</span></span> | <span data-ttu-id="127d6-272">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-272">Rich text</span></span> | <span data-ttu-id="127d6-273">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-273">Summary of the card.</span></span> <span data-ttu-id="127d6-274">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="127d6-275">text</span><span class="sxs-lookup"><span data-stu-id="127d6-275">text</span></span> | <span data-ttu-id="127d6-276">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-276">Rich text</span></span> | <span data-ttu-id="127d6-277">Le texte apparaît sous le sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="127d6-277">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="127d6-278">themeColor</span><span class="sxs-lookup"><span data-stu-id="127d6-278">themeColor</span></span> | <span data-ttu-id="127d6-279">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="127d6-279">HEX string</span></span> | <span data-ttu-id="127d6-280">Couleur qui remplace l’accentColor fourni à partir du manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="127d6-280">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="127d6-281">Remarques sur la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="127d6-281">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="127d6-282">Les cartes de connecteur Office 365 fonctionnent correctement dans Microsoft Teams, y compris les [actions ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="127d6-282">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="127d6-283">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-283">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="127d6-284">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="127d6-284">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="127d6-285">Pour un bot, l’action déclenche une activité qui envoie uniquement l’ID d’action et le `HttpPOST` `invoke` corps au bot.</span><span class="sxs-lookup"><span data-stu-id="127d6-285">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="127d6-286">Chaque carte de connecteur peut afficher un maximum de 10 sections, et chaque section peut contenir un maximum de 5 images et 5 actions.</span><span class="sxs-lookup"><span data-stu-id="127d6-286">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="127d6-287">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="127d6-287">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="127d6-288">Tous les champs de texte sont en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="127d6-288">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="127d6-289">Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="127d6-289">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="127d6-290">Par défaut, `markdown` est définie sur ; si vous souhaitez utiliser html à la `true` place, définie sur `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="127d6-290">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="127d6-291">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="127d6-291">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="127d6-292">Pour spécifier le style de `activityImage` rendu pour , vous pouvez définir comme suit `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="127d6-292">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="127d6-293">Valeur</span><span class="sxs-lookup"><span data-stu-id="127d6-293">Value</span></span> | <span data-ttu-id="127d6-294">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-294">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="127d6-295">Valeur par défaut ; `activityImage` sera rognée sous la mesure d’un cercle.</span><span class="sxs-lookup"><span data-stu-id="127d6-295">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="127d6-296">`activityImage` s’affiche sous la forme d’un rectangle et conserve ses proportions.</span><span class="sxs-lookup"><span data-stu-id="127d6-296">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="127d6-297">Pour plus d’informations sur les propriétés de carte de connecteur, voir la référence de carte [de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="127d6-297">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="127d6-298">Les seules propriétés de carte de connecteur que Microsoft Teams ne prend pas en charge actuellement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="127d6-298">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="127d6-299">`startGroup` (toujours traité comme `true` dans Teams)</span><span class="sxs-lookup"><span data-stu-id="127d6-299">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="127d6-300">Exemple de carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="127d6-300">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="127d6-301">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="127d6-301">Receipt card</span></span>

<span data-ttu-id="127d6-302">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="127d6-302">Teams supports receipt card.</span></span> <span data-ttu-id="127d6-303">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="127d6-303">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="127d6-304">Elle contient généralement la liste des éléments à inclure sur le reçu, telles que les taxes et le total des informations.</span><span class="sxs-lookup"><span data-stu-id="127d6-304">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="127d6-305">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="127d6-305">Support for receipt cards</span></span>

| <span data-ttu-id="127d6-306">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-306">Bots in Teams</span></span> | <span data-ttu-id="127d6-307">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-307">Messaging extensions</span></span>  | <span data-ttu-id="127d6-308">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-308">Connectors</span></span> | <span data-ttu-id="127d6-309">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-309">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-310">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-310">✔</span></span> | <span data-ttu-id="127d6-311">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-311">✔</span></span> | <span data-ttu-id="127d6-312">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-312">✖</span></span> | <span data-ttu-id="127d6-313">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-313">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="127d6-314">Exemple de carte de reçu</span><span class="sxs-lookup"><span data-stu-id="127d6-314">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="127d6-316">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="127d6-316">Additional information on receipt cards</span></span>

<span data-ttu-id="127d6-317">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="127d6-317">Bot Framework reference:</span></span>

* [<span data-ttu-id="127d6-318">Nœud de carte de réception</span><span class="sxs-lookup"><span data-stu-id="127d6-318">Receipt card Node</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="127d6-319">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="127d6-319">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="127d6-320">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="127d6-320">Signin card</span></span>

<span data-ttu-id="127d6-321">La carte de signature permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="127d6-321">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="127d6-322">Pris en charge dans Teams sous une forme légèrement différente de celle de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="127d6-322">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="127d6-323">La carte de signin dans Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de signin dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="127d6-323">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="127d6-324">**L’action de signin** peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="127d6-324">The **signin action** can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="127d6-325">Pour plus d’informations sur l’authentification, voir [flux d’authentification Microsoft Teams pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="127d6-325">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="127d6-326">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="127d6-326">Support for Signin cards</span></span>

| <span data-ttu-id="127d6-327">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-327">Bots in Teams</span></span> | <span data-ttu-id="127d6-328">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-328">Messaging extensions</span></span>  | <span data-ttu-id="127d6-329">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-329">Connectors</span></span> | <span data-ttu-id="127d6-330">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-330">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-331">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-331">✔</span></span> | <span data-ttu-id="127d6-332">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-332">✖</span></span> | <span data-ttu-id="127d6-333">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-333">✖</span></span> | <span data-ttu-id="127d6-334">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-334">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="127d6-335">Informations supplémentaires sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="127d6-335">Additional information on signin cards</span></span>

<span data-ttu-id="127d6-336">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="127d6-336">Bot Framework reference:</span></span>

* [<span data-ttu-id="127d6-337">Nœud de carte de signature</span><span class="sxs-lookup"><span data-stu-id="127d6-337">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="127d6-338">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="127d6-338">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="127d6-339">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="127d6-339">Thumbnail card</span></span>

<span data-ttu-id="127d6-340">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="127d6-340">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="127d6-341">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="127d6-341">Support for thumbnail cards</span></span>

| <span data-ttu-id="127d6-342">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-342">Bots in Teams</span></span> | <span data-ttu-id="127d6-343">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-343">Messaging extensions</span></span>  | <span data-ttu-id="127d6-344">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-344">Connectors</span></span> | <span data-ttu-id="127d6-345">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-345">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-346">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-346">✔</span></span> | <span data-ttu-id="127d6-347">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-347">✔</span></span> | <span data-ttu-id="127d6-348">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-348">✖</span></span> | <span data-ttu-id="127d6-349">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-349">✔</span></span> |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="127d6-351">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="127d6-351">Properties of a thumbnail card</span></span>

| <span data-ttu-id="127d6-352">Propriété</span><span class="sxs-lookup"><span data-stu-id="127d6-352">Property</span></span> | <span data-ttu-id="127d6-353">Type</span><span class="sxs-lookup"><span data-stu-id="127d6-353">Type</span></span>  | <span data-ttu-id="127d6-354">Description</span><span class="sxs-lookup"><span data-stu-id="127d6-354">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="127d6-355">title</span><span class="sxs-lookup"><span data-stu-id="127d6-355">title</span></span> | <span data-ttu-id="127d6-356">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-356">Rich text</span></span> | <span data-ttu-id="127d6-357">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-357">Title of the card.</span></span> <span data-ttu-id="127d6-358">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-358">Maximum 2 lines.</span></span>|
| <span data-ttu-id="127d6-359">subtitle</span><span class="sxs-lookup"><span data-stu-id="127d6-359">subtitle</span></span> | <span data-ttu-id="127d6-360">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-360">Rich text</span></span> | <span data-ttu-id="127d6-361">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-361">Subtitle of the card.</span></span> <span data-ttu-id="127d6-362">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="127d6-362">Maximum 2 lines.</span></span>|
| <span data-ttu-id="127d6-363">text</span><span class="sxs-lookup"><span data-stu-id="127d6-363">text</span></span> | <span data-ttu-id="127d6-364">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="127d6-364">Rich text</span></span> | <span data-ttu-id="127d6-365">Le texte apparaît sous le sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="127d6-365">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="127d6-366">images</span><span class="sxs-lookup"><span data-stu-id="127d6-366">images</span></span> | <span data-ttu-id="127d6-367">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="127d6-367">Array of images</span></span> | <span data-ttu-id="127d6-368">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="127d6-368">Image displayed at top of card.</span></span> <span data-ttu-id="127d6-369">Proportions 1:1 (carré).</span><span class="sxs-lookup"><span data-stu-id="127d6-369">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="127d6-370">buttons</span><span class="sxs-lookup"><span data-stu-id="127d6-370">buttons</span></span> | <span data-ttu-id="127d6-371">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="127d6-371">Array of action objects</span></span> | <span data-ttu-id="127d6-372">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="127d6-372">Set of actions applicable to the current card.</span></span> <span data-ttu-id="127d6-373">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="127d6-373">Maximum 6.</span></span> |
| <span data-ttu-id="127d6-374">tap</span><span class="sxs-lookup"><span data-stu-id="127d6-374">tap</span></span> | <span data-ttu-id="127d6-375">Objet Action</span><span class="sxs-lookup"><span data-stu-id="127d6-375">Action object</span></span> | <span data-ttu-id="127d6-376">Cette action est activée lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="127d6-376">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="127d6-377">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="127d6-377">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="127d6-378">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="127d6-378">Additional information</span></span>

<span data-ttu-id="127d6-379">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="127d6-379">Bot Framework reference:</span></span>

* [<span data-ttu-id="127d6-380">Nœud de carte miniature</span><span class="sxs-lookup"><span data-stu-id="127d6-380">Thumbnail card Node</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="127d6-381">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="127d6-381">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="127d6-382">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="127d6-382">Card collections</span></span>

<span data-ttu-id="127d6-383">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="127d6-383">Teams supports Card collections.</span></span>

<span data-ttu-id="127d6-384">Collections de cartes `builder.AttachmentLayout.carousel` : et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="127d6-384">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="127d6-385">Ces collections contiennent des cartes adaptatives, hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="127d6-385">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="127d6-386">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="127d6-386">Carousel collection</span></span>

<span data-ttu-id="127d6-387">La [disposition de carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="127d6-387">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="127d6-388">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="127d6-388">Support for carousel collections</span></span>

| <span data-ttu-id="127d6-389">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-389">Bots in Teams</span></span> | <span data-ttu-id="127d6-390">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-390">Messaging extensions</span></span>  | <span data-ttu-id="127d6-391">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-391">Connectors</span></span> | <span data-ttu-id="127d6-392">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-392">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-393">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-393">✔</span></span> | <span data-ttu-id="127d6-394">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-394">✖</span></span> | <span data-ttu-id="127d6-395">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-395">✖</span></span> | <span data-ttu-id="127d6-396">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-396">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="127d6-397">Un carrousel peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="127d6-397">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="127d6-398">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="127d6-398">Properties of a carousel card</span></span>

<span data-ttu-id="127d6-399">Les propriétés d’une carte Carrousel sont identiques à celles des cartes Hero et Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="127d6-399">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="127d6-400">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="127d6-400">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="127d6-402">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="127d6-402">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="127d6-403">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="127d6-403">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="127d6-404">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="127d6-404">Support for list collections</span></span>

<span data-ttu-id="127d6-405">La disposition de liste affiche une liste de cartes empilées verticalement, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="127d6-405">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="127d6-406">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-406">Bots in Teams</span></span> | <span data-ttu-id="127d6-407">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="127d6-407">Messaging extensions</span></span>  | <span data-ttu-id="127d6-408">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="127d6-408">Connectors</span></span> | <span data-ttu-id="127d6-409">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="127d6-409">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="127d6-410">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-410">✔</span></span> | <span data-ttu-id="127d6-411">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-411">✔</span></span> | <span data-ttu-id="127d6-412">✖</span><span class="sxs-lookup"><span data-stu-id="127d6-412">✖</span></span> | <span data-ttu-id="127d6-413">✔</span><span class="sxs-lookup"><span data-stu-id="127d6-413">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="127d6-414">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="127d6-414">Example of a list collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="127d6-416">Les propriétés sont identiques à la carte hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="127d6-416">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="127d6-417">Une liste peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="127d6-417">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="127d6-418">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="127d6-418">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="127d6-419">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="127d6-419">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="127d6-420">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="127d6-420">Cards not supported in Teams</span></span>

<span data-ttu-id="127d6-421">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas pris en charge par Teams.</span><span class="sxs-lookup"><span data-stu-id="127d6-421">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="127d6-422">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="127d6-422">Animation cards</span></span>
* <span data-ttu-id="127d6-423">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="127d6-423">Audio cards</span></span>
* <span data-ttu-id="127d6-424">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="127d6-424">Video cards</span></span>
