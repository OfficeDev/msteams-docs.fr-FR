---
title: Référence des cartes
description: Décrit toutes les cartes et les actions de carte disponibles pour les robots dans teams
keywords: Référence des cartes robots
ms.openlocfilehash: 7bd1cbea0aec03913c9bce205ae68eedba284637
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434544"
---
# <a name="cards-reference"></a><span data-ttu-id="fc66a-104">Référence des cartes</span><span class="sxs-lookup"><span data-stu-id="fc66a-104">Cards Reference</span></span>

<span data-ttu-id="fc66a-105">Les cartes répertoriées dans cette section sont prises en charge dans les robots pour Teams.</span><span class="sxs-lookup"><span data-stu-id="fc66a-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="fc66a-106">Elles sont basées sur des cartes définies par l’infrastructure de robot, mais Teams ne prend pas en charge toutes les cartes de l’infrastructure bot et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="fc66a-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="fc66a-107">Les différences sont dénommées dans les références ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fc66a-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="fc66a-108">Exemples de carte</span><span class="sxs-lookup"><span data-stu-id="fc66a-108">Card examples</span></span>

<span data-ttu-id="fc66a-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du kit de développement logiciel (v3) du générateur de robots.</span><span class="sxs-lookup"><span data-stu-id="fc66a-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="fc66a-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="fc66a-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="fc66a-111">.NET</span><span class="sxs-lookup"><span data-stu-id="fc66a-111">.NET</span></span>
  * [<span data-ttu-id="fc66a-112">Ajouter des cartes en tant que pièces jointes aux messages</span><span class="sxs-lookup"><span data-stu-id="fc66a-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="fc66a-113">Exemple de code de carte (bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="fc66a-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="fc66a-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="fc66a-114">Node.js</span></span>
  * [<span data-ttu-id="fc66a-115">Ajouter des cartes en tant que pièces jointes aux messages</span><span class="sxs-lookup"><span data-stu-id="fc66a-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="fc66a-116">Exemple de code de carte (bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="fc66a-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="fc66a-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="fc66a-117">Types of cards</span></span>

<span data-ttu-id="fc66a-118">Ce tableau indique les types de cartes à votre disposition.</span><span class="sxs-lookup"><span data-stu-id="fc66a-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="fc66a-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="fc66a-119">Card Type</span></span> | <span data-ttu-id="fc66a-120">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fc66a-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fc66a-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="fc66a-122">Carte hautement personnalisable pouvant contenir n’importe quelle combinaison de texte, de paroles, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fc66a-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="fc66a-123">Carte héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="fc66a-124">Contient généralement une seule image de grande taille, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="fc66a-125">Fiche de liste</span><span class="sxs-lookup"><span data-stu-id="fc66a-125">List Card</span></span>](#list-card) | <span data-ttu-id="fc66a-126">Une liste déroulante d’éléments.</span><span class="sxs-lookup"><span data-stu-id="fc66a-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="fc66a-127">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fc66a-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="fc66a-128">Disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="fc66a-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="fc66a-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="fc66a-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="fc66a-130">Fournit un accusé de réception à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fc66a-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="fc66a-131">Carte de connexion</span><span class="sxs-lookup"><span data-stu-id="fc66a-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="fc66a-132">Permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="fc66a-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="fc66a-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="fc66a-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="fc66a-134">Contient généralement une seule image miniature, un texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="fc66a-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="fc66a-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="fc66a-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="fc66a-136">Utilisé pour retourner plusieurs éléments dans une seule réponse</span><span class="sxs-lookup"><span data-stu-id="fc66a-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="fc66a-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="fc66a-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="fc66a-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="fc66a-138">Inline card images</span></span>

<span data-ttu-id="fc66a-139">Votre carte peut contenir une image incluse en incluant un lien vers votre image accessible au public.</span><span class="sxs-lookup"><span data-stu-id="fc66a-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="fc66a-140">Pour des raisons de performances, nous vous recommandons vivement d’héberger votre image sur un réseau de distribution de contenu public (CDN).</span><span class="sxs-lookup"><span data-stu-id="fc66a-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="fc66a-141">Les images sont mises à l’horizontale ou verticalement tout en conservant les proportions pour redimensionner la zone d’image, puis rognées du Centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="fc66a-142">Les images doivent être d’au moins 1024 × 1024 et 1 Mo au format PNG, JPEG ou GIF ; l’image GIF animée n’est pas officiellement prise en charge.</span><span class="sxs-lookup"><span data-stu-id="fc66a-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="fc66a-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="fc66a-143">Property</span></span> | <span data-ttu-id="fc66a-144">Type</span><span class="sxs-lookup"><span data-stu-id="fc66a-144">Type</span></span>  | <span data-ttu-id="fc66a-145">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc66a-146">url</span><span class="sxs-lookup"><span data-stu-id="fc66a-146">url</span></span> | <span data-ttu-id="fc66a-147">URL</span><span class="sxs-lookup"><span data-stu-id="fc66a-147">URL</span></span> | <span data-ttu-id="fc66a-148">URL HTTPs vers l’image</span><span class="sxs-lookup"><span data-stu-id="fc66a-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="fc66a-149">alt</span><span class="sxs-lookup"><span data-stu-id="fc66a-149">alt</span></span> | <span data-ttu-id="fc66a-150">String</span><span class="sxs-lookup"><span data-stu-id="fc66a-150">String</span></span> | <span data-ttu-id="fc66a-151">Description accessible de l’image</span><span class="sxs-lookup"><span data-stu-id="fc66a-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="fc66a-152">Boutons</span><span class="sxs-lookup"><span data-stu-id="fc66a-152">Buttons</span></span>

<span data-ttu-id="fc66a-153">Les boutons sont affichés empilés au bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="fc66a-154">Le texte du bouton est toujours sur une seule ligne et sera tronqué s’il dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="fc66a-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="fc66a-155">Les boutons supplémentaires qui dépassent le nombre maximal pris en charge par la carte ne seront pas affichés.</span><span class="sxs-lookup"><span data-stu-id="fc66a-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="fc66a-156">Pour plus d’informations, consultez la rubrique [actions de carte](~/task-modules-and-cards/cards/cards-actions.md) .</span><span class="sxs-lookup"><span data-stu-id="fc66a-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="fc66a-157">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="fc66a-157">Card Formatting</span></span>

<span data-ttu-id="fc66a-158">Pour plus d’informations sur la mise en forme de texte dans les cartes, voir [format](~/task-modules-and-cards/cards/cards-format.md) des cartes.</span><span class="sxs-lookup"><span data-stu-id="fc66a-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="fc66a-159">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fc66a-159">Adaptive card</span></span>

<span data-ttu-id="fc66a-160">Carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de paroles, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fc66a-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="fc66a-161">*Voir* [cartes adaptatives v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="fc66a-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="fc66a-162">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fc66a-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="fc66a-163">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-163">Bots in Teams</span></span> | <span data-ttu-id="fc66a-164">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-164">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-165">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-165">Connectors</span></span> | <span data-ttu-id="fc66a-166">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-167">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-167">✔</span></span> | <span data-ttu-id="fc66a-168">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-168">✔</span></span> | <span data-ttu-id="fc66a-169">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-169">✖</span></span> | <span data-ttu-id="fc66a-170">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-170">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="fc66a-171">Les éléments multimédias ne sont actuellement pas pris en charge dans les cartes adaptative v 1.2 sur la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="fc66a-171">Media elements are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

### <a name="example-adaptive-card"></a><span data-ttu-id="fc66a-172">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fc66a-172">Example Adaptive card</span></span>

![Exemple de carte de carte adaptative](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="fc66a-174">Pour plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fc66a-174">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="fc66a-175">Vue d’ensemble des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fc66a-175">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="fc66a-176">Actions de carte adaptative dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-176">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="fc66a-177">Carte héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-177">Hero card</span></span>

<span data-ttu-id="fc66a-178">Une carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-178">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="fc66a-179">Prise en charge des cartes héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-179">Support for Hero cards</span></span>

| <span data-ttu-id="fc66a-180">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-180">Bots in Teams</span></span> | <span data-ttu-id="fc66a-181">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-181">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-182">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-182">Connectors</span></span> | <span data-ttu-id="fc66a-183">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-183">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-184">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-184">✔</span></span> | <span data-ttu-id="fc66a-185">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-185">✔</span></span> | <span data-ttu-id="fc66a-186">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-186">✖</span></span> | <span data-ttu-id="fc66a-187">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-187">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="fc66a-188">Propriétés d’une carte héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-188">Properties of a Hero card</span></span>

| <span data-ttu-id="fc66a-189">Propriété</span><span class="sxs-lookup"><span data-stu-id="fc66a-189">Property</span></span> | <span data-ttu-id="fc66a-190">Type</span><span class="sxs-lookup"><span data-stu-id="fc66a-190">Type</span></span>  | <span data-ttu-id="fc66a-191">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-191">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc66a-192">title</span><span class="sxs-lookup"><span data-stu-id="fc66a-192">title</span></span> | <span data-ttu-id="fc66a-193">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-193">Rich text</span></span> | <span data-ttu-id="fc66a-194">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-194">Title of the card.</span></span> <span data-ttu-id="fc66a-195">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-195">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-196">sous-titre</span><span class="sxs-lookup"><span data-stu-id="fc66a-196">subtitle</span></span> | <span data-ttu-id="fc66a-197">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-197">Rich text</span></span> | <span data-ttu-id="fc66a-198">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-198">Subtitle of the card.</span></span> <span data-ttu-id="fc66a-199">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-199">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-200">text</span><span class="sxs-lookup"><span data-stu-id="fc66a-200">text</span></span> | <span data-ttu-id="fc66a-201">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-201">Rich text</span></span> | <span data-ttu-id="fc66a-202">Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="fc66a-202">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="fc66a-203">images</span><span class="sxs-lookup"><span data-stu-id="fc66a-203">images</span></span> | <span data-ttu-id="fc66a-204">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="fc66a-204">Array of images</span></span> | <span data-ttu-id="fc66a-205">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-205">Image displayed at top of card.</span></span> <span data-ttu-id="fc66a-206">Proportions 16:9</span><span class="sxs-lookup"><span data-stu-id="fc66a-206">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="fc66a-207">descendre</span><span class="sxs-lookup"><span data-stu-id="fc66a-207">buttons</span></span> | <span data-ttu-id="fc66a-208">Tableau d’objets action</span><span class="sxs-lookup"><span data-stu-id="fc66a-208">Array of action objects</span></span> | <span data-ttu-id="fc66a-209">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="fc66a-209">Set of actions applicable to the current card.</span></span> <span data-ttu-id="fc66a-210">Maximum 6</span><span class="sxs-lookup"><span data-stu-id="fc66a-210">Maximum 6</span></span> |
| <span data-ttu-id="fc66a-211">taper</span><span class="sxs-lookup"><span data-stu-id="fc66a-211">tap</span></span> | <span data-ttu-id="fc66a-212">Objet Action</span><span class="sxs-lookup"><span data-stu-id="fc66a-212">Action object</span></span> | <span data-ttu-id="fc66a-213">Cette action est activée lorsque l’utilisateur appuie sur la carte proprement dite.</span><span class="sxs-lookup"><span data-stu-id="fc66a-213">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="fc66a-214">Exemple de carte héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-214">Example Hero card</span></span>

![Exemple de carte héros](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="fc66a-216">Pour plus d’informations sur les cartes héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-216">For more information on Hero cards</span></span>

<span data-ttu-id="fc66a-217">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="fc66a-217">Bot Framework reference:</span></span>

* [<span data-ttu-id="fc66a-218">Nœud de carte héros</span><span class="sxs-lookup"><span data-stu-id="fc66a-218">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="fc66a-219">Carte héros C #</span><span class="sxs-lookup"><span data-stu-id="fc66a-219">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="fc66a-220">Fiche de liste</span><span class="sxs-lookup"><span data-stu-id="fc66a-220">List card</span></span>

<span data-ttu-id="fc66a-221">La carte de liste a été ajoutée par teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="fc66a-221">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="fc66a-222">La carte de liste fournit une liste déroulante d’éléments.</span><span class="sxs-lookup"><span data-stu-id="fc66a-222">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="fc66a-223">Prise en charge des cartes de visite</span><span class="sxs-lookup"><span data-stu-id="fc66a-223">Support for List cards</span></span>

| <span data-ttu-id="fc66a-224">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-224">Bots in Teams</span></span> | <span data-ttu-id="fc66a-225">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-225">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-226">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-226">Connectors</span></span> | <span data-ttu-id="fc66a-227">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-227">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-228">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-228">✔</span></span> | <span data-ttu-id="fc66a-229">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-229">✖</span></span> | <span data-ttu-id="fc66a-230">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-230">✖</span></span> |<span data-ttu-id="fc66a-231">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-231">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="fc66a-232">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="fc66a-232">Properties of a List card</span></span>

| <span data-ttu-id="fc66a-233">Propriété</span><span class="sxs-lookup"><span data-stu-id="fc66a-233">Property</span></span> | <span data-ttu-id="fc66a-234">Type</span><span class="sxs-lookup"><span data-stu-id="fc66a-234">Type</span></span>  | <span data-ttu-id="fc66a-235">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc66a-236">title</span><span class="sxs-lookup"><span data-stu-id="fc66a-236">title</span></span> | <span data-ttu-id="fc66a-237">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-237">Rich text</span></span> | <span data-ttu-id="fc66a-238">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-238">Title of the card.</span></span> <span data-ttu-id="fc66a-239">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-239">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-240">éléments</span><span class="sxs-lookup"><span data-stu-id="fc66a-240">items</span></span> | <span data-ttu-id="fc66a-241">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="fc66a-241">Array of list items</span></span>  ||
| <span data-ttu-id="fc66a-242">descendre</span><span class="sxs-lookup"><span data-stu-id="fc66a-242">buttons</span></span> | <span data-ttu-id="fc66a-243">Tableau d’objets action</span><span class="sxs-lookup"><span data-stu-id="fc66a-243">Array of action objects</span></span> | <span data-ttu-id="fc66a-244">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="fc66a-244">Set of actions applicable to the current card.</span></span> <span data-ttu-id="fc66a-245">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="fc66a-245">Maximum 6.</span></span> <span data-ttu-id="fc66a-246">Ne s’affiche pas sur mobile.</span><span class="sxs-lookup"><span data-stu-id="fc66a-246">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="fc66a-247">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="fc66a-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="fc66a-248">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fc66a-248">Office 365 connector card</span></span>

<span data-ttu-id="fc66a-249">Pris en charge dans Teams, pas dans l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="fc66a-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="fc66a-250">La carte de connecteur Office 365 offre une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="fc66a-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="fc66a-251">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par les robots.</span><span class="sxs-lookup"><span data-stu-id="fc66a-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="fc66a-252">Consultez la section Remarques pour connaître les différences entre les cartes de connecteur et la carte O365.</span><span class="sxs-lookup"><span data-stu-id="fc66a-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="fc66a-253">Prise en charge des cartes de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fc66a-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="fc66a-254">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-254">Bots in Teams</span></span> | <span data-ttu-id="fc66a-255">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-255">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-256">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-256">Connectors</span></span> | <span data-ttu-id="fc66a-257">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-258">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-258">✔</span></span> | <span data-ttu-id="fc66a-259">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-259">✔</span></span> | <span data-ttu-id="fc66a-260">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-260">✔</span></span> | <span data-ttu-id="fc66a-261">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="fc66a-262">Propriétés de la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fc66a-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="fc66a-263">Propriété</span><span class="sxs-lookup"><span data-stu-id="fc66a-263">Property</span></span> | <span data-ttu-id="fc66a-264">Type</span><span class="sxs-lookup"><span data-stu-id="fc66a-264">Type</span></span>  | <span data-ttu-id="fc66a-265">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc66a-266">title</span><span class="sxs-lookup"><span data-stu-id="fc66a-266">title</span></span> | <span data-ttu-id="fc66a-267">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-267">Rich text</span></span> | <span data-ttu-id="fc66a-268">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-268">Title of the card.</span></span> <span data-ttu-id="fc66a-269">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-269">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-270">résumé</span><span class="sxs-lookup"><span data-stu-id="fc66a-270">summary</span></span> | <span data-ttu-id="fc66a-271">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-271">Rich text</span></span> | <span data-ttu-id="fc66a-272">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-272">Summary of the card.</span></span> <span data-ttu-id="fc66a-273">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-273">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-274">text</span><span class="sxs-lookup"><span data-stu-id="fc66a-274">text</span></span> | <span data-ttu-id="fc66a-275">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-275">Rich text</span></span> | <span data-ttu-id="fc66a-276">Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="fc66a-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="fc66a-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="fc66a-277">themeColor</span></span> | <span data-ttu-id="fc66a-278">Chaîne HEXADÉCIMALe</span><span class="sxs-lookup"><span data-stu-id="fc66a-278">HEX string</span></span> | <span data-ttu-id="fc66a-279">couleur qui remplace le accentColor fourni par le manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="fc66a-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="fc66a-280">Remarques sur la carte du connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fc66a-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="fc66a-281">Les cartes de connecteur Office 365 fonctionnent correctement sur Microsoft Teams, y compris les [actions ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="fc66a-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="fc66a-282">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="fc66a-283">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="fc66a-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="fc66a-284">Pour un bot, l' `HttpPOST` action déclenche une `invoke` activité qui envoie uniquement l’ID et le corps de l’action au bot.</span><span class="sxs-lookup"><span data-stu-id="fc66a-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="fc66a-285">Chaque carte de connecteur peut afficher un maximum de 10 sections et chaque section peut contenir un maximum de 5 images et 5 actions.</span><span class="sxs-lookup"><span data-stu-id="fc66a-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="fc66a-286">Les sections, images ou actions supplémentaires dans un message ne s’affichent pas.</span><span class="sxs-lookup"><span data-stu-id="fc66a-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="fc66a-287">Tous les champs de texte prennent en charge le démarque et le code HTML.</span><span class="sxs-lookup"><span data-stu-id="fc66a-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="fc66a-288">Vous pouvez contrôler les sections qui utilisent la démarque ou le code HTML en définissant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="fc66a-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="fc66a-289">Par défaut, `markdown` est défini sur `true` ; si vous préférez utiliser HTML à la place, définissez `markdown` sur `false` .</span><span class="sxs-lookup"><span data-stu-id="fc66a-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="fc66a-290">Si vous spécifiez la `themeColor` propriété, elle se substitue `accentColor` à la propriété dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="fc66a-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="fc66a-291">Pour spécifier le style de rendu de `activityImage` , vous pouvez définir `activityImageType` comme suit.</span><span class="sxs-lookup"><span data-stu-id="fc66a-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="fc66a-292">Valeur</span><span class="sxs-lookup"><span data-stu-id="fc66a-292">Value</span></span> | <span data-ttu-id="fc66a-293">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="fc66a-294">Default `activityImage`sera rognée en tant que cercle</span><span class="sxs-lookup"><span data-stu-id="fc66a-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="fc66a-295">`activityImage`s’affiche sous la forme d’un rectangle et conserve ses proportions</span><span class="sxs-lookup"><span data-stu-id="fc66a-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="fc66a-296">Pour tous les autres détails sur les propriétés de la carte de connecteur, consultez la [référence de carte de message](/outlook/actionable-messages/card-reference)intégrant des actions.</span><span class="sxs-lookup"><span data-stu-id="fc66a-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="fc66a-297">Les seules propriétés de la carte de connecteur que Microsoft Teams ne prend pas en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc66a-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="fc66a-298">`startGroup`(toujours traité comme `true` dans Teams)</span><span class="sxs-lookup"><span data-stu-id="fc66a-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="fc66a-299">Exemple de carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fc66a-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="fc66a-300">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="fc66a-300">Receipt card</span></span>

<span data-ttu-id="fc66a-301">Pris en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="fc66a-301">Supported in Teams.</span></span>

<span data-ttu-id="fc66a-302">Carte qui permet à un bot de fournir un accusé de réception à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fc66a-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="fc66a-303">Il contient généralement la liste des éléments à inclure dans le reçu, les informations fiscales et totales, ainsi que d’autres textes.</span><span class="sxs-lookup"><span data-stu-id="fc66a-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="fc66a-304">Prise en charge des fiches de réception</span><span class="sxs-lookup"><span data-stu-id="fc66a-304">Support for Receipts cards</span></span>

| <span data-ttu-id="fc66a-305">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-305">Bots in Teams</span></span> | <span data-ttu-id="fc66a-306">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-306">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-307">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-307">Connectors</span></span> | <span data-ttu-id="fc66a-308">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-309">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-309">✔</span></span> | <span data-ttu-id="fc66a-310">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-310">✔</span></span> | <span data-ttu-id="fc66a-311">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-311">✖</span></span> | <span data-ttu-id="fc66a-312">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="fc66a-313">Pour plus d’informations sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="fc66a-313">For more information on Receipt cards</span></span>

<span data-ttu-id="fc66a-314">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="fc66a-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="fc66a-315">Nœud carte de réception</span><span class="sxs-lookup"><span data-stu-id="fc66a-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="fc66a-316">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="fc66a-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="fc66a-317">Carte de connexion</span><span class="sxs-lookup"><span data-stu-id="fc66a-317">Signin card</span></span>

<span data-ttu-id="fc66a-318">Carte qui permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="fc66a-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="fc66a-319">Pris en charge dans teams sous une forme légèrement différente de celle de l’infrastructure de robot.</span><span class="sxs-lookup"><span data-stu-id="fc66a-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="fc66a-320">La carte de connexion dans teams est similaire à la carte de connexion dans l’infrastructure de robot, à l’exception que la carte de connexion dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="fc66a-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="fc66a-321">L' *action de connexion* peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement à partir de la carte de connexion.</span><span class="sxs-lookup"><span data-stu-id="fc66a-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="fc66a-322">Pour plus d’informations sur l’authentification, voir la rubrique [Microsoft teams Authentication Flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) .</span><span class="sxs-lookup"><span data-stu-id="fc66a-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="fc66a-323">Prise en charge des cartes de connexion</span><span class="sxs-lookup"><span data-stu-id="fc66a-323">Support for Signin cards</span></span>

| <span data-ttu-id="fc66a-324">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-324">Bots in Teams</span></span> | <span data-ttu-id="fc66a-325">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-325">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-326">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-326">Connectors</span></span> | <span data-ttu-id="fc66a-327">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-328">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-328">✔</span></span> | <span data-ttu-id="fc66a-329">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-329">✖</span></span> | <span data-ttu-id="fc66a-330">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-330">✖</span></span> | <span data-ttu-id="fc66a-331">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="fc66a-332">Pour plus d’informations sur les cartes de connexion</span><span class="sxs-lookup"><span data-stu-id="fc66a-332">For more information on Signin cards</span></span>

<span data-ttu-id="fc66a-333">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="fc66a-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="fc66a-334">Nœud de la carte de connexion</span><span class="sxs-lookup"><span data-stu-id="fc66a-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="fc66a-335">Carte de connexion C #</span><span class="sxs-lookup"><span data-stu-id="fc66a-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="fc66a-336">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="fc66a-336">Thumbnail card</span></span>

<span data-ttu-id="fc66a-337">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="fc66a-338">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="fc66a-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="fc66a-339">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-339">Bots in Teams</span></span> | <span data-ttu-id="fc66a-340">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-340">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-341">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-341">Connectors</span></span> | <span data-ttu-id="fc66a-342">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-343">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-343">✔</span></span> | <span data-ttu-id="fc66a-344">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-344">✔</span></span> | <span data-ttu-id="fc66a-345">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-345">✖</span></span> | <span data-ttu-id="fc66a-346">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-346">✔</span></span> |
|

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="fc66a-348">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="fc66a-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="fc66a-349">Propriété</span><span class="sxs-lookup"><span data-stu-id="fc66a-349">Property</span></span> | <span data-ttu-id="fc66a-350">Type</span><span class="sxs-lookup"><span data-stu-id="fc66a-350">Type</span></span>  | <span data-ttu-id="fc66a-351">Description</span><span class="sxs-lookup"><span data-stu-id="fc66a-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc66a-352">title</span><span class="sxs-lookup"><span data-stu-id="fc66a-352">title</span></span> | <span data-ttu-id="fc66a-353">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-353">Rich text</span></span> | <span data-ttu-id="fc66a-354">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-354">Title of the card.</span></span> <span data-ttu-id="fc66a-355">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-355">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-356">sous-titre</span><span class="sxs-lookup"><span data-stu-id="fc66a-356">subtitle</span></span> | <span data-ttu-id="fc66a-357">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-357">Rich text</span></span> | <span data-ttu-id="fc66a-358">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-358">Subtitle of the card.</span></span> <span data-ttu-id="fc66a-359">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="fc66a-359">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="fc66a-360">text</span><span class="sxs-lookup"><span data-stu-id="fc66a-360">text</span></span> | <span data-ttu-id="fc66a-361">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fc66a-361">Rich text</span></span> | <span data-ttu-id="fc66a-362">Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="fc66a-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="fc66a-363">images</span><span class="sxs-lookup"><span data-stu-id="fc66a-363">images</span></span> | <span data-ttu-id="fc66a-364">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="fc66a-364">Array of images</span></span> | <span data-ttu-id="fc66a-365">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="fc66a-365">Image displayed at top of card.</span></span> <span data-ttu-id="fc66a-366">Proportions 1:1 (carrés)</span><span class="sxs-lookup"><span data-stu-id="fc66a-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="fc66a-367">descendre</span><span class="sxs-lookup"><span data-stu-id="fc66a-367">buttons</span></span> | <span data-ttu-id="fc66a-368">Tableau d’objets action</span><span class="sxs-lookup"><span data-stu-id="fc66a-368">Array of action objects</span></span> | <span data-ttu-id="fc66a-369">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="fc66a-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="fc66a-370">Maximum 6</span><span class="sxs-lookup"><span data-stu-id="fc66a-370">Maximum 6</span></span> |
| <span data-ttu-id="fc66a-371">taper</span><span class="sxs-lookup"><span data-stu-id="fc66a-371">tap</span></span> | <span data-ttu-id="fc66a-372">Objet Action</span><span class="sxs-lookup"><span data-stu-id="fc66a-372">Action object</span></span> | <span data-ttu-id="fc66a-373">Cette action est activée lorsque l’utilisateur appuie sur la carte proprement dite.</span><span class="sxs-lookup"><span data-stu-id="fc66a-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="fc66a-374">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="fc66a-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="fc66a-375">Pour plus d'informations</span><span class="sxs-lookup"><span data-stu-id="fc66a-375">For more information</span></span>

<span data-ttu-id="fc66a-376">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="fc66a-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="fc66a-377">Nœud de la carte miniature</span><span class="sxs-lookup"><span data-stu-id="fc66a-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="fc66a-378">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="fc66a-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="fc66a-379">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="fc66a-379">Card collections</span></span>

<span data-ttu-id="fc66a-380">Les collections de cartes sont prises en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="fc66a-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="fc66a-381">Les collections de cartes sont fournies par l’infrastructure de robot : `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="fc66a-381">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="fc66a-382">Ces collections peuvent contenir des cartes adaptative, héros ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="fc66a-382">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="fc66a-383">Collection carrousel</span><span class="sxs-lookup"><span data-stu-id="fc66a-383">Carousel collection</span></span>

<span data-ttu-id="fc66a-384">La [disposition carrousel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="fc66a-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="fc66a-385">Prise en charge des regroupements de carrousel</span><span class="sxs-lookup"><span data-stu-id="fc66a-385">Support for Carousel collections</span></span>

| <span data-ttu-id="fc66a-386">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-386">Bots in Teams</span></span> | <span data-ttu-id="fc66a-387">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-387">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-388">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-388">Connectors</span></span> | <span data-ttu-id="fc66a-389">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-390">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-390">✔</span></span> | <span data-ttu-id="fc66a-391">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-391">✖</span></span> | <span data-ttu-id="fc66a-392">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-392">✖</span></span> | <span data-ttu-id="fc66a-393">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="fc66a-394">Un carrousel peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="fc66a-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="fc66a-395">Exemple de collection carrousel</span><span class="sxs-lookup"><span data-stu-id="fc66a-395">Example Carousel collection</span></span>

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

<span data-ttu-id="fc66a-397">Les propriétés sont les mêmes que pour la carte héros ou miniature.</span><span class="sxs-lookup"><span data-stu-id="fc66a-397">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="fc66a-398">Syntaxe des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="fc66a-398">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="fc66a-399">Liste, collection</span><span class="sxs-lookup"><span data-stu-id="fc66a-399">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="fc66a-400">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="fc66a-400">Support for List collections</span></span>

<span data-ttu-id="fc66a-401">La disposition liste affiche une liste de cartes verticalement empilées, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="fc66a-401">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="fc66a-402">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-402">Bots in Teams</span></span> | <span data-ttu-id="fc66a-403">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fc66a-403">Messaging Extensions</span></span>  | <span data-ttu-id="fc66a-404">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fc66a-404">Connectors</span></span> | <span data-ttu-id="fc66a-405">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="fc66a-405">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc66a-406">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-406">✔</span></span> | <span data-ttu-id="fc66a-407">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-407">✔</span></span> | <span data-ttu-id="fc66a-408">✖</span><span class="sxs-lookup"><span data-stu-id="fc66a-408">✖</span></span> | <span data-ttu-id="fc66a-409">✔</span><span class="sxs-lookup"><span data-stu-id="fc66a-409">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="fc66a-410">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="fc66a-410">Example List collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="fc66a-412">Les propriétés sont les mêmes que pour la carte héros ou miniature.</span><span class="sxs-lookup"><span data-stu-id="fc66a-412">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="fc66a-413">Une liste peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="fc66a-413">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="fc66a-414">Certaines combinaisons de cartes de visite ne sont pas encore prises en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="fc66a-414">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="fc66a-415">Syntaxe des collections de listes</span><span class="sxs-lookup"><span data-stu-id="fc66a-415">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="fc66a-416">Cartes non prises en charge dans teams</span><span class="sxs-lookup"><span data-stu-id="fc66a-416">Cards not supported in Teams</span></span>

<span data-ttu-id="fc66a-417">Les cartes suivantes sont implémentées par l’infrastructure de robot, mais ne sont pas prises en charge par Teams.</span><span class="sxs-lookup"><span data-stu-id="fc66a-417">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="fc66a-418">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="fc66a-418">Animation cards</span></span>
* <span data-ttu-id="fc66a-419">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="fc66a-419">Audio cards</span></span>
* <span data-ttu-id="fc66a-420">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="fc66a-420">Video cards</span></span>
