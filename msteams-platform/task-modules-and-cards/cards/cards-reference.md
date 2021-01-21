---
title: Référence des cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: 839430baa5ce5e8950a21a1472036c6fd96f4edf
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911896"
---
# <a name="cards-reference"></a><span data-ttu-id="4f731-104">Référence de cartes</span><span class="sxs-lookup"><span data-stu-id="4f731-104">Cards reference</span></span>

<span data-ttu-id="4f731-105">Les cartes répertoriées dans cette section sont pris en charge dans les bots pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4f731-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="4f731-106">Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="4f731-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="4f731-107">Les différences sont appelées dans les références de ce document.</span><span class="sxs-lookup"><span data-stu-id="4f731-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="4f731-108">Exemples de cartes</span><span class="sxs-lookup"><span data-stu-id="4f731-108">Card examples</span></span>

<span data-ttu-id="4f731-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="4f731-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="4f731-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="4f731-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="4f731-111">.NET</span><span class="sxs-lookup"><span data-stu-id="4f731-111">.NET</span></span>
  * [<span data-ttu-id="4f731-112">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="4f731-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="4f731-113">Exemple de code de cartes (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="4f731-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="4f731-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="4f731-114">Node.js</span></span>
  * [<span data-ttu-id="4f731-115">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="4f731-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="4f731-116">Exemple de code de cartes (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="4f731-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="4f731-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="4f731-117">Types of cards</span></span>

<span data-ttu-id="4f731-118">Ce tableau indique les types de cartes disponibles :</span><span class="sxs-lookup"><span data-stu-id="4f731-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="4f731-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="4f731-119">Card type</span></span> | <span data-ttu-id="4f731-120">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="4f731-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="4f731-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="4f731-122">Carte hautement personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4f731-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="4f731-123">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="4f731-124">Contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="4f731-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="4f731-125">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="4f731-125">List card</span></span>](#list-card) | <span data-ttu-id="4f731-126">Liste de défilement d’éléments.</span><span class="sxs-lookup"><span data-stu-id="4f731-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="4f731-127">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="4f731-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="4f731-128">Disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="4f731-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="4f731-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="4f731-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="4f731-130">Fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f731-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="4f731-131">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="4f731-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="4f731-132">Permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="4f731-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="4f731-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="4f731-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="4f731-134">Contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="4f731-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="4f731-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="4f731-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="4f731-136">Utilisé pour renvoyer plusieurs éléments dans une seule réponse.</span><span class="sxs-lookup"><span data-stu-id="4f731-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="4f731-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="4f731-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="4f731-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="4f731-138">Inline card images</span></span>

<span data-ttu-id="4f731-139">La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="4f731-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="4f731-140">Pour des raisons de performances, il est vivement recommandé d’héberger l’image sur un réseau de distribution de contenu (CDN) public.</span><span class="sxs-lookup"><span data-stu-id="4f731-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="4f731-141">La taille des images est réduite ou monter en puissance tout en conservant les proportions pour couvrir la zone d’image, puis rognées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="4f731-142">Les images doivent être au maximum 1024×1024, au format PNG, JPEG ou GIF, et l’image GIF animée n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="4f731-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="4f731-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="4f731-143">Property</span></span> | <span data-ttu-id="4f731-144">Type</span><span class="sxs-lookup"><span data-stu-id="4f731-144">Type</span></span>  | <span data-ttu-id="4f731-145">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f731-146">url</span><span class="sxs-lookup"><span data-stu-id="4f731-146">url</span></span> | <span data-ttu-id="4f731-147">URL</span><span class="sxs-lookup"><span data-stu-id="4f731-147">URL</span></span> | <span data-ttu-id="4f731-148">URL HTTPS vers l’image</span><span class="sxs-lookup"><span data-stu-id="4f731-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="4f731-149">alt</span><span class="sxs-lookup"><span data-stu-id="4f731-149">alt</span></span> | <span data-ttu-id="4f731-150">Chaîne</span><span class="sxs-lookup"><span data-stu-id="4f731-150">String</span></span> | <span data-ttu-id="4f731-151">Description accessible de l’image</span><span class="sxs-lookup"><span data-stu-id="4f731-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="4f731-152">Boutons</span><span class="sxs-lookup"><span data-stu-id="4f731-152">Buttons</span></span>

<span data-ttu-id="4f731-153">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="4f731-154">Le texte du bouton est toujours sur une seule ligne et est tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="4f731-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="4f731-155">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne s’afficheront pas.</span><span class="sxs-lookup"><span data-stu-id="4f731-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="4f731-156">Pour plus [d’informations,](~/task-modules-and-cards/cards/cards-actions.md) voir Actions de carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="4f731-157">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="4f731-157">Card formatting</span></span>

<span data-ttu-id="4f731-158">Pour [plus d’informations](~/task-modules-and-cards/cards/cards-format.md) sur la mise en forme du texte dans les cartes, voir Formatage de carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="4f731-159">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="4f731-159">Adaptive card</span></span>

<span data-ttu-id="4f731-160">Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4f731-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="4f731-161">Voir [Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="4f731-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="4f731-162">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="4f731-162">Support for adaptive cards</span></span>

| <span data-ttu-id="4f731-163">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-163">Bots in Teams</span></span> | <span data-ttu-id="4f731-164">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-164">Messaging extensions</span></span>  | <span data-ttu-id="4f731-165">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-165">Connectors</span></span> | <span data-ttu-id="4f731-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-167">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-167">✔</span></span> | <span data-ttu-id="4f731-168">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-168">✔</span></span> | <span data-ttu-id="4f731-169">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-169">✖</span></span> | <span data-ttu-id="4f731-170">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="4f731-171">La plateforme Teams prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="4f731-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="4f731-172">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="4f731-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="4f731-173">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="4f731-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="4f731-175">Informations supplémentaires sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="4f731-175">Additional information on adaptive cards</span></span>

* [<span data-ttu-id="4f731-176">Vue d’ensemble des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="4f731-176">Adaptive cards overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="4f731-177">Actions de carte adaptative dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="4f731-178">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-178">Hero card</span></span>

<span data-ttu-id="4f731-179">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="4f731-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="4f731-180">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-180">Support for hero cards</span></span>

| <span data-ttu-id="4f731-181">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-181">Bots in Teams</span></span> | <span data-ttu-id="4f731-182">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-182">Messaging Extensions</span></span>  | <span data-ttu-id="4f731-183">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-183">Connectors</span></span> | <span data-ttu-id="4f731-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-185">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-185">✔</span></span> | <span data-ttu-id="4f731-186">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-186">✔</span></span> | <span data-ttu-id="4f731-187">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-187">✖</span></span> | <span data-ttu-id="4f731-188">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-188">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="4f731-189">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-189">Properties of a hero card</span></span>

| <span data-ttu-id="4f731-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="4f731-190">Property</span></span> | <span data-ttu-id="4f731-191">Type</span><span class="sxs-lookup"><span data-stu-id="4f731-191">Type</span></span>  | <span data-ttu-id="4f731-192">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f731-193">title</span><span class="sxs-lookup"><span data-stu-id="4f731-193">title</span></span> | <span data-ttu-id="4f731-194">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-194">Rich text</span></span> | <span data-ttu-id="4f731-195">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-195">Title of the card.</span></span> <span data-ttu-id="4f731-196">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="4f731-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="4f731-197">subtitle</span></span> | <span data-ttu-id="4f731-198">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-198">Rich text</span></span> | <span data-ttu-id="4f731-199">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-199">Subtitle of the card.</span></span> <span data-ttu-id="4f731-200">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f731-201">text</span><span class="sxs-lookup"><span data-stu-id="4f731-201">text</span></span> | <span data-ttu-id="4f731-202">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-202">Rich text</span></span> | <span data-ttu-id="4f731-203">Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="4f731-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="4f731-204">images</span><span class="sxs-lookup"><span data-stu-id="4f731-204">images</span></span> | <span data-ttu-id="4f731-205">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="4f731-205">Array of images</span></span> | <span data-ttu-id="4f731-206">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-206">Image displayed at top of card.</span></span> <span data-ttu-id="4f731-207">Proportions 16:9.</span><span class="sxs-lookup"><span data-stu-id="4f731-207">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="4f731-208">buttons</span><span class="sxs-lookup"><span data-stu-id="4f731-208">buttons</span></span> | <span data-ttu-id="4f731-209">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="4f731-209">Array of action objects</span></span> | <span data-ttu-id="4f731-210">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="4f731-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="4f731-211">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="4f731-211">Maximum 6.</span></span> |
| <span data-ttu-id="4f731-212">tap</span><span class="sxs-lookup"><span data-stu-id="4f731-212">tap</span></span> | <span data-ttu-id="4f731-213">Objet Action</span><span class="sxs-lookup"><span data-stu-id="4f731-213">Action object</span></span> | <span data-ttu-id="4f731-214">Cette action est activée lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="4f731-214">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="4f731-215">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-215">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="4f731-217">Informations supplémentaires sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-217">Additional information on hero cards</span></span>

<span data-ttu-id="4f731-218">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="4f731-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f731-219">Nœud de carte Hero</span><span class="sxs-lookup"><span data-stu-id="4f731-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="4f731-220">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="4f731-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="4f731-221">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="4f731-221">List card</span></span>

<span data-ttu-id="4f731-222">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="4f731-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="4f731-223">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="4f731-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="4f731-224">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="4f731-224">Support for list cards</span></span>

| <span data-ttu-id="4f731-225">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-225">Bots in Teams</span></span> | <span data-ttu-id="4f731-226">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-226">Messaging extensions</span></span>  | <span data-ttu-id="4f731-227">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-227">Connectors</span></span> | <span data-ttu-id="4f731-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-229">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-229">✔</span></span> | <span data-ttu-id="4f731-230">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-230">✖</span></span> | <span data-ttu-id="4f731-231">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-231">✖</span></span> |<span data-ttu-id="4f731-232">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-232">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="4f731-233">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="4f731-233">Properties of a list card</span></span>

| <span data-ttu-id="4f731-234">Propriété</span><span class="sxs-lookup"><span data-stu-id="4f731-234">Property</span></span> | <span data-ttu-id="4f731-235">Type</span><span class="sxs-lookup"><span data-stu-id="4f731-235">Type</span></span>  | <span data-ttu-id="4f731-236">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f731-237">title</span><span class="sxs-lookup"><span data-stu-id="4f731-237">title</span></span> | <span data-ttu-id="4f731-238">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-238">Rich text</span></span> | <span data-ttu-id="4f731-239">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-239">Title of the card.</span></span> <span data-ttu-id="4f731-240">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f731-241">éléments</span><span class="sxs-lookup"><span data-stu-id="4f731-241">items</span></span> | <span data-ttu-id="4f731-242">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="4f731-242">Array of list items</span></span>  ||
| <span data-ttu-id="4f731-243">buttons</span><span class="sxs-lookup"><span data-stu-id="4f731-243">buttons</span></span> | <span data-ttu-id="4f731-244">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="4f731-244">Array of action objects</span></span> | <span data-ttu-id="4f731-245">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="4f731-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="4f731-246">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="4f731-246">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="4f731-247">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="4f731-247">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="4f731-248">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="4f731-248">Office 365 connector card</span></span>

<span data-ttu-id="4f731-249">La carte connecteur Office 365 est prise en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="4f731-249">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="4f731-250">Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="4f731-250">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="4f731-251">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="4f731-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="4f731-252">Consultez la section remarques pour les différences entre les cartes de connecteur et la carte O365.</span><span class="sxs-lookup"><span data-stu-id="4f731-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="4f731-253">Prise en charge des cartes de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="4f731-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="4f731-254">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-254">Bots in Teams</span></span> | <span data-ttu-id="4f731-255">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-255">Messaging extensions</span></span>  | <span data-ttu-id="4f731-256">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-256">Connectors</span></span> | <span data-ttu-id="4f731-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-258">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-258">✔</span></span> | <span data-ttu-id="4f731-259">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-259">✔</span></span> | <span data-ttu-id="4f731-260">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-260">✔</span></span> | <span data-ttu-id="4f731-261">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-261">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="4f731-262">Propriétés de la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="4f731-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="4f731-263">Propriété</span><span class="sxs-lookup"><span data-stu-id="4f731-263">Property</span></span> | <span data-ttu-id="4f731-264">Type</span><span class="sxs-lookup"><span data-stu-id="4f731-264">Type</span></span>  | <span data-ttu-id="4f731-265">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f731-266">title</span><span class="sxs-lookup"><span data-stu-id="4f731-266">title</span></span> | <span data-ttu-id="4f731-267">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-267">Rich text</span></span> | <span data-ttu-id="4f731-268">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-268">Title of the card.</span></span> <span data-ttu-id="4f731-269">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="4f731-270">résumé</span><span class="sxs-lookup"><span data-stu-id="4f731-270">summary</span></span> | <span data-ttu-id="4f731-271">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-271">Rich text</span></span> | <span data-ttu-id="4f731-272">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-272">Summary of the card.</span></span> <span data-ttu-id="4f731-273">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="4f731-274">text</span><span class="sxs-lookup"><span data-stu-id="4f731-274">text</span></span> | <span data-ttu-id="4f731-275">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-275">Rich text</span></span> | <span data-ttu-id="4f731-276">Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="4f731-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="4f731-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="4f731-277">themeColor</span></span> | <span data-ttu-id="4f731-278">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="4f731-278">HEX string</span></span> | <span data-ttu-id="4f731-279">Couleur qui remplace l’accentColor fourni à partir du manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="4f731-279">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="4f731-280">Remarques sur la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="4f731-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="4f731-281">Les cartes de connecteur Office 365 fonctionnent correctement dans Microsoft Teams, y compris les [actions ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="4f731-281">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="4f731-282">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-282">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="4f731-283">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="4f731-283">For a connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="4f731-284">Pour un bot, l’action déclenche une activité qui envoie uniquement l’ID d’action et le `HttpPOST` `invoke` corps au bot.</span><span class="sxs-lookup"><span data-stu-id="4f731-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="4f731-285">Chaque carte de connecteur peut afficher un maximum de 10 sections, et chaque section peut contenir un maximum de 5 images et 5 actions.</span><span class="sxs-lookup"><span data-stu-id="4f731-285">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="4f731-286">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="4f731-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="4f731-287">Tous les champs de texte sont en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="4f731-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="4f731-288">Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="4f731-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="4f731-289">Par défaut, `markdown` est définie sur ; si vous souhaitez utiliser html à la `true` place, définie sur `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="4f731-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="4f731-290">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="4f731-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="4f731-291">Pour spécifier le style de `activityImage` rendu pour , vous pouvez définir comme suit `activityImageType` :</span><span class="sxs-lookup"><span data-stu-id="4f731-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="4f731-292">Valeur</span><span class="sxs-lookup"><span data-stu-id="4f731-292">Value</span></span> | <span data-ttu-id="4f731-293">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="4f731-294">Valeur par défaut ; `activityImage` sera rognée sous la mesure d’un cercle.</span><span class="sxs-lookup"><span data-stu-id="4f731-294">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="4f731-295">`activityImage` s’affiche sous la forme d’un rectangle et conserve ses proportions.</span><span class="sxs-lookup"><span data-stu-id="4f731-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="4f731-296">Pour plus d’informations sur les propriétés de carte de connecteur, voir la référence de carte [de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="4f731-296">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="4f731-297">Les seules propriétés de carte de connecteur que Microsoft Teams ne prend pas en charge actuellement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f731-297">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="4f731-298">`startGroup` (toujours traité comme `true` dans Teams)</span><span class="sxs-lookup"><span data-stu-id="4f731-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="4f731-299">Exemple de carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="4f731-299">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="4f731-300">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="4f731-300">Receipt card</span></span>

<span data-ttu-id="4f731-301">Teams prend en charge la carte de réception.</span><span class="sxs-lookup"><span data-stu-id="4f731-301">Teams supports receipt card.</span></span> <span data-ttu-id="4f731-302">Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f731-302">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="4f731-303">Elle contient généralement la liste des éléments à inclure sur le reçu, telles que les taxes et le total des informations.</span><span class="sxs-lookup"><span data-stu-id="4f731-303">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="4f731-304">Prise en charge des cartes de réception</span><span class="sxs-lookup"><span data-stu-id="4f731-304">Support for receipt cards</span></span>

| <span data-ttu-id="4f731-305">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-305">Bots in Teams</span></span> | <span data-ttu-id="4f731-306">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-306">Messaging extensions</span></span>  | <span data-ttu-id="4f731-307">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-307">Connectors</span></span> | <span data-ttu-id="4f731-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-309">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-309">✔</span></span> | <span data-ttu-id="4f731-310">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-310">✔</span></span> | <span data-ttu-id="4f731-311">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-311">✖</span></span> | <span data-ttu-id="4f731-312">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-312">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="4f731-313">Exemple de carte de reçu</span><span class="sxs-lookup"><span data-stu-id="4f731-313">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="4f731-315">Informations supplémentaires sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="4f731-315">Additional information on receipt cards</span></span>

<span data-ttu-id="4f731-316">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="4f731-316">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f731-317">Nœud de carte de réception</span><span class="sxs-lookup"><span data-stu-id="4f731-317">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="4f731-318">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="4f731-318">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="4f731-319">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="4f731-319">Signin card</span></span>

<span data-ttu-id="4f731-320">La carte de signature permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="4f731-320">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="4f731-321">Pris en charge dans Teams sous une forme légèrement différente de celle de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="4f731-321">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="4f731-322">La carte de signin dans Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de signin dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="4f731-322">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="4f731-323">*L’action de signin* peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="4f731-323">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="4f731-324">Pour plus d’informations sur l’authentification, voir [flux d’authentification Microsoft Teams pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="4f731-324">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="4f731-325">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="4f731-325">Support for Signin cards</span></span>

| <span data-ttu-id="4f731-326">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-326">Bots in Teams</span></span> | <span data-ttu-id="4f731-327">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-327">Messaging extensions</span></span>  | <span data-ttu-id="4f731-328">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-328">Connectors</span></span> | <span data-ttu-id="4f731-329">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-329">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-330">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-330">✔</span></span> | <span data-ttu-id="4f731-331">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-331">✖</span></span> | <span data-ttu-id="4f731-332">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-332">✖</span></span> | <span data-ttu-id="4f731-333">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-333">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="4f731-334">Informations supplémentaires sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="4f731-334">Additional information on signin cards</span></span>

<span data-ttu-id="4f731-335">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="4f731-335">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f731-336">Nœud de carte de signature</span><span class="sxs-lookup"><span data-stu-id="4f731-336">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="4f731-337">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="4f731-337">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="4f731-338">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="4f731-338">Thumbnail card</span></span>

<span data-ttu-id="4f731-339">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="4f731-339">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="4f731-340">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="4f731-340">Support for thumbnail cards</span></span>

| <span data-ttu-id="4f731-341">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-341">Bots in Teams</span></span> | <span data-ttu-id="4f731-342">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-342">Messaging extensions</span></span>  | <span data-ttu-id="4f731-343">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-343">Connectors</span></span> | <span data-ttu-id="4f731-344">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-344">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-345">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-345">✔</span></span> | <span data-ttu-id="4f731-346">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-346">✔</span></span> | <span data-ttu-id="4f731-347">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-347">✖</span></span> | <span data-ttu-id="4f731-348">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-348">✔</span></span> |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="4f731-350">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="4f731-350">Properties of a thumbnail card</span></span>

| <span data-ttu-id="4f731-351">Propriété</span><span class="sxs-lookup"><span data-stu-id="4f731-351">Property</span></span> | <span data-ttu-id="4f731-352">Type</span><span class="sxs-lookup"><span data-stu-id="4f731-352">Type</span></span>  | <span data-ttu-id="4f731-353">Description</span><span class="sxs-lookup"><span data-stu-id="4f731-353">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f731-354">title</span><span class="sxs-lookup"><span data-stu-id="4f731-354">title</span></span> | <span data-ttu-id="4f731-355">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-355">Rich text</span></span> | <span data-ttu-id="4f731-356">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-356">Title of the card.</span></span> <span data-ttu-id="4f731-357">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-357">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f731-358">subtitle</span><span class="sxs-lookup"><span data-stu-id="4f731-358">subtitle</span></span> | <span data-ttu-id="4f731-359">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-359">Rich text</span></span> | <span data-ttu-id="4f731-360">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-360">Subtitle of the card.</span></span> <span data-ttu-id="4f731-361">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="4f731-361">Maximum 2 lines.</span></span>|
| <span data-ttu-id="4f731-362">text</span><span class="sxs-lookup"><span data-stu-id="4f731-362">text</span></span> | <span data-ttu-id="4f731-363">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="4f731-363">Rich text</span></span> | <span data-ttu-id="4f731-364">Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="4f731-364">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="4f731-365">images</span><span class="sxs-lookup"><span data-stu-id="4f731-365">images</span></span> | <span data-ttu-id="4f731-366">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="4f731-366">Array of images</span></span> | <span data-ttu-id="4f731-367">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="4f731-367">Image displayed at top of card.</span></span> <span data-ttu-id="4f731-368">Proportions 1:1 (carré).</span><span class="sxs-lookup"><span data-stu-id="4f731-368">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="4f731-369">buttons</span><span class="sxs-lookup"><span data-stu-id="4f731-369">buttons</span></span> | <span data-ttu-id="4f731-370">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="4f731-370">Array of action objects</span></span> | <span data-ttu-id="4f731-371">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="4f731-371">Set of actions applicable to the current card.</span></span> <span data-ttu-id="4f731-372">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="4f731-372">Maximum 6.</span></span> |
| <span data-ttu-id="4f731-373">tap</span><span class="sxs-lookup"><span data-stu-id="4f731-373">tap</span></span> | <span data-ttu-id="4f731-374">Objet Action</span><span class="sxs-lookup"><span data-stu-id="4f731-374">Action object</span></span> | <span data-ttu-id="4f731-375">Cette action est activée lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="4f731-375">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="4f731-376">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="4f731-376">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="4f731-377">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4f731-377">Additional information</span></span>

<span data-ttu-id="4f731-378">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="4f731-378">Bot Framework reference:</span></span>

* [<span data-ttu-id="4f731-379">Nœud de carte miniature</span><span class="sxs-lookup"><span data-stu-id="4f731-379">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="4f731-380">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="4f731-380">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="4f731-381">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="4f731-381">Card collections</span></span>

<span data-ttu-id="4f731-382">Teams prend en charge les collections de cartes.</span><span class="sxs-lookup"><span data-stu-id="4f731-382">Teams supports Card collections.</span></span>

<span data-ttu-id="4f731-383">Collections de cartes `builder.AttachmentLayout.carousel` : et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="4f731-383">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="4f731-384">Ces collections contiennent des cartes adaptatives, hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="4f731-384">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="4f731-385">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="4f731-385">Carousel collection</span></span>

<span data-ttu-id="4f731-386">La [disposition de carrousel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) présente un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="4f731-386">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="4f731-387">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="4f731-387">Support for carousel collections</span></span>

| <span data-ttu-id="4f731-388">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-388">Bots in Teams</span></span> | <span data-ttu-id="4f731-389">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-389">Messaging extensions</span></span>  | <span data-ttu-id="4f731-390">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-390">Connectors</span></span> | <span data-ttu-id="4f731-391">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-391">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-392">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-392">✔</span></span> | <span data-ttu-id="4f731-393">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-393">✖</span></span> | <span data-ttu-id="4f731-394">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-394">✖</span></span> | <span data-ttu-id="4f731-395">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-395">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="4f731-396">Un carrousel peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="4f731-396">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="4f731-397">Propriétés d’une carte carrousel</span><span class="sxs-lookup"><span data-stu-id="4f731-397">Properties of a carousel card</span></span>

<span data-ttu-id="4f731-398">Les propriétés d’une carte Carrousel sont identiques à celles des cartes Hero et Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="4f731-398">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="4f731-399">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="4f731-399">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="4f731-401">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="4f731-401">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="4f731-402">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="4f731-402">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="4f731-403">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="4f731-403">Support for list collections</span></span>

<span data-ttu-id="4f731-404">La disposition de liste affiche une liste empilée verticalement de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="4f731-404">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="4f731-405">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-405">Bots in Teams</span></span> | <span data-ttu-id="4f731-406">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4f731-406">Messaging extensions</span></span>  | <span data-ttu-id="4f731-407">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="4f731-407">Connectors</span></span> | <span data-ttu-id="4f731-408">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="4f731-408">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f731-409">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-409">✔</span></span> | <span data-ttu-id="4f731-410">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-410">✔</span></span> | <span data-ttu-id="4f731-411">✖</span><span class="sxs-lookup"><span data-stu-id="4f731-411">✖</span></span> | <span data-ttu-id="4f731-412">✔</span><span class="sxs-lookup"><span data-stu-id="4f731-412">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="4f731-413">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="4f731-413">Example of a list collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="4f731-415">Les propriétés sont identiques à la carte hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="4f731-415">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="4f731-416">Une liste peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="4f731-416">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="4f731-417">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="4f731-417">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="4f731-418">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="4f731-418">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="4f731-419">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="4f731-419">Cards not supported in Teams</span></span>

<span data-ttu-id="4f731-420">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas pris en charge par Teams.</span><span class="sxs-lookup"><span data-stu-id="4f731-420">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="4f731-421">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="4f731-421">Animation cards</span></span>
* <span data-ttu-id="4f731-422">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="4f731-422">Audio cards</span></span>
* <span data-ttu-id="4f731-423">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="4f731-423">Video cards</span></span>
