---
title: Référence des cartes
description: Décrit toutes les cartes et les actions de carte disponibles pour les robots dans teams
keywords: Référence des cartes robots
ms.openlocfilehash: 9cd868e504e426cbe56ed1c5d05c8e6adc1e1ddf
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801114"
---
# <a name="cards-reference"></a><span data-ttu-id="7e6ee-104">Référence des cartes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-104">Cards Reference</span></span>

<span data-ttu-id="7e6ee-105">Les cartes répertoriées dans cette section sont prises en charge dans les robots pour Teams.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="7e6ee-106">Elles sont basées sur des cartes définies par l’infrastructure de robot, mais Teams ne prend pas en charge toutes les cartes de l’infrastructure bot et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="7e6ee-107">Les différences sont dénommées dans les références ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="7e6ee-108">Exemples de carte</span><span class="sxs-lookup"><span data-stu-id="7e6ee-108">Card examples</span></span>

<span data-ttu-id="7e6ee-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du kit de développement logiciel (v3) du générateur de robots.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="7e6ee-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="7e6ee-111">.NET</span><span class="sxs-lookup"><span data-stu-id="7e6ee-111">.NET</span></span>
  * [<span data-ttu-id="7e6ee-112">Ajouter des cartes en tant que pièces jointes aux messages</span><span class="sxs-lookup"><span data-stu-id="7e6ee-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="7e6ee-113">Exemple de code de carte (bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="7e6ee-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="7e6ee-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="7e6ee-114">Node.js</span></span>
  * [<span data-ttu-id="7e6ee-115">Ajouter des cartes en tant que pièces jointes aux messages</span><span class="sxs-lookup"><span data-stu-id="7e6ee-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="7e6ee-116">Exemple de code de carte (bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="7e6ee-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="7e6ee-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-117">Types of cards</span></span>

<span data-ttu-id="7e6ee-118">Ce tableau indique les types de cartes à votre disposition.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="7e6ee-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="7e6ee-119">Card Type</span></span> | <span data-ttu-id="7e6ee-120">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="7e6ee-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7e6ee-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="7e6ee-122">Carte hautement personnalisable pouvant contenir n’importe quelle combinaison de texte, de paroles, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="7e6ee-123">Carte héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="7e6ee-124">Contient généralement une seule image de grande taille, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="7e6ee-125">Fiche de liste</span><span class="sxs-lookup"><span data-stu-id="7e6ee-125">List Card</span></span>](#list-card) | <span data-ttu-id="7e6ee-126">Une liste déroulante d’éléments.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="7e6ee-127">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7e6ee-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="7e6ee-128">Disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="7e6ee-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="7e6ee-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="7e6ee-130">Fournit un accusé de réception à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="7e6ee-131">Carte de connexion</span><span class="sxs-lookup"><span data-stu-id="7e6ee-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="7e6ee-132">Permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="7e6ee-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="7e6ee-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="7e6ee-134">Contient généralement une seule image miniature, un texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="7e6ee-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="7e6ee-136">Utilisé pour retourner plusieurs éléments dans une seule réponse</span><span class="sxs-lookup"><span data-stu-id="7e6ee-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="7e6ee-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="7e6ee-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="7e6ee-138">Inline card images</span></span>

<span data-ttu-id="7e6ee-139">Votre carte peut contenir une image incluse en incluant un lien vers votre image accessible au public.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="7e6ee-140">Pour des raisons de performances, nous vous recommandons vivement d’héberger votre image sur un réseau de distribution de contenu public (CDN).</span><span class="sxs-lookup"><span data-stu-id="7e6ee-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="7e6ee-141">Les images sont mises à l’horizontale ou verticalement tout en conservant les proportions pour redimensionner la zone d’image, puis rognées du Centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="7e6ee-142">Les images doivent être d’au moins 1024 × 1024 et 1 Mo au format PNG, JPEG ou GIF ; l’image GIF animée n’est pas officiellement prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="7e6ee-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e6ee-143">Property</span></span> | <span data-ttu-id="7e6ee-144">Type</span><span class="sxs-lookup"><span data-stu-id="7e6ee-144">Type</span></span>  | <span data-ttu-id="7e6ee-145">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e6ee-146">url</span><span class="sxs-lookup"><span data-stu-id="7e6ee-146">url</span></span> | <span data-ttu-id="7e6ee-147">URL</span><span class="sxs-lookup"><span data-stu-id="7e6ee-147">URL</span></span> | <span data-ttu-id="7e6ee-148">URL HTTPs vers l’image</span><span class="sxs-lookup"><span data-stu-id="7e6ee-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="7e6ee-149">alt</span><span class="sxs-lookup"><span data-stu-id="7e6ee-149">alt</span></span> | <span data-ttu-id="7e6ee-150">String</span><span class="sxs-lookup"><span data-stu-id="7e6ee-150">String</span></span> | <span data-ttu-id="7e6ee-151">Description accessible de l’image</span><span class="sxs-lookup"><span data-stu-id="7e6ee-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="7e6ee-152">Boutons</span><span class="sxs-lookup"><span data-stu-id="7e6ee-152">Buttons</span></span>

<span data-ttu-id="7e6ee-153">Les boutons sont affichés empilés au bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="7e6ee-154">Le texte du bouton est toujours sur une seule ligne et sera tronqué s’il dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="7e6ee-155">Les boutons supplémentaires qui dépassent le nombre maximal pris en charge par la carte ne seront pas affichés.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="7e6ee-156">Pour plus d’informations, consultez la rubrique [actions de carte](~/task-modules-and-cards/cards/cards-actions.md) .</span><span class="sxs-lookup"><span data-stu-id="7e6ee-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="7e6ee-157">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="7e6ee-157">Card Formatting</span></span>

<span data-ttu-id="7e6ee-158">Pour plus d’informations sur la mise en forme de texte dans les cartes, voir [format](~/task-modules-and-cards/cards/cards-format.md) des cartes.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="7e6ee-159">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7e6ee-159">Adaptive card</span></span>

<span data-ttu-id="7e6ee-160">Carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de paroles, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="7e6ee-161">*Voir* [cartes adaptatives v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="7e6ee-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="7e6ee-162">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7e6ee-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="7e6ee-163">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-163">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-164">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-164">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-165">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-165">Connectors</span></span> | <span data-ttu-id="7e6ee-166">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-167">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-167">✔</span></span> | <span data-ttu-id="7e6ee-168">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-168">✔</span></span> | <span data-ttu-id="7e6ee-169">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-169">✖</span></span> | <span data-ttu-id="7e6ee-170">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-170">✔</span></span> |
|

### <a name="example-adaptive-card"></a><span data-ttu-id="7e6ee-171">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7e6ee-171">Example Adaptive card</span></span>

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="7e6ee-173">Pour plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7e6ee-173">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="7e6ee-174">Vue d’ensemble des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="7e6ee-174">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="7e6ee-175">Actions de carte adaptative dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-175">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="7e6ee-176">Carte héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-176">Hero card</span></span>

<span data-ttu-id="7e6ee-177">Une carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-177">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="7e6ee-178">Prise en charge des cartes héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-178">Support for Hero cards</span></span>

| <span data-ttu-id="7e6ee-179">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-179">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-180">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-180">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-181">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-181">Connectors</span></span> | <span data-ttu-id="7e6ee-182">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-182">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-183">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-183">✔</span></span> | <span data-ttu-id="7e6ee-184">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-184">✔</span></span> | <span data-ttu-id="7e6ee-185">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-185">✖</span></span> | <span data-ttu-id="7e6ee-186">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-186">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="7e6ee-187">Propriétés d’une carte héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-187">Properties of a Hero card</span></span>

| <span data-ttu-id="7e6ee-188">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e6ee-188">Property</span></span> | <span data-ttu-id="7e6ee-189">Type</span><span class="sxs-lookup"><span data-stu-id="7e6ee-189">Type</span></span>  | <span data-ttu-id="7e6ee-190">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-190">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e6ee-191">title</span><span class="sxs-lookup"><span data-stu-id="7e6ee-191">title</span></span> | <span data-ttu-id="7e6ee-192">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-192">Rich text</span></span> | <span data-ttu-id="7e6ee-193">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-193">Title of the card.</span></span> <span data-ttu-id="7e6ee-194">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-194">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-195">sous-titre</span><span class="sxs-lookup"><span data-stu-id="7e6ee-195">subtitle</span></span> | <span data-ttu-id="7e6ee-196">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-196">Rich text</span></span> | <span data-ttu-id="7e6ee-197">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-197">Subtitle of the card.</span></span> <span data-ttu-id="7e6ee-198">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-198">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-199">text</span><span class="sxs-lookup"><span data-stu-id="7e6ee-199">text</span></span> | <span data-ttu-id="7e6ee-200">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-200">Rich text</span></span> | <span data-ttu-id="7e6ee-201">Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="7e6ee-201">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="7e6ee-202">images</span><span class="sxs-lookup"><span data-stu-id="7e6ee-202">images</span></span> | <span data-ttu-id="7e6ee-203">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="7e6ee-203">Array of images</span></span> | <span data-ttu-id="7e6ee-204">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-204">Image displayed at top of card.</span></span> <span data-ttu-id="7e6ee-205">Proportions 16:9</span><span class="sxs-lookup"><span data-stu-id="7e6ee-205">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="7e6ee-206">descendre</span><span class="sxs-lookup"><span data-stu-id="7e6ee-206">buttons</span></span> | <span data-ttu-id="7e6ee-207">Tableau d’objets action</span><span class="sxs-lookup"><span data-stu-id="7e6ee-207">Array of action objects</span></span> | <span data-ttu-id="7e6ee-208">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-208">Set of actions applicable to the current card.</span></span> <span data-ttu-id="7e6ee-209">Maximum 6</span><span class="sxs-lookup"><span data-stu-id="7e6ee-209">Maximum 6</span></span> |
| <span data-ttu-id="7e6ee-210">taper</span><span class="sxs-lookup"><span data-stu-id="7e6ee-210">tap</span></span> | <span data-ttu-id="7e6ee-211">Objet Action</span><span class="sxs-lookup"><span data-stu-id="7e6ee-211">Action object</span></span> | <span data-ttu-id="7e6ee-212">Cette action est activée lorsque l’utilisateur appuie sur la carte proprement dite.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-212">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="7e6ee-213">Exemple de carte héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-213">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="7e6ee-215">Pour plus d’informations sur les cartes héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-215">For more information on Hero cards</span></span>

<span data-ttu-id="7e6ee-216">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="7e6ee-216">Bot Framework reference:</span></span>

* [<span data-ttu-id="7e6ee-217">Nœud de carte héros</span><span class="sxs-lookup"><span data-stu-id="7e6ee-217">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="7e6ee-218">Carte héros C #</span><span class="sxs-lookup"><span data-stu-id="7e6ee-218">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="7e6ee-219">Fiche de liste</span><span class="sxs-lookup"><span data-stu-id="7e6ee-219">List card</span></span>

<span data-ttu-id="7e6ee-220">La carte de liste a été ajoutée par teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-220">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="7e6ee-221">La carte de liste fournit une liste déroulante d’éléments.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-221">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="7e6ee-222">Prise en charge des cartes de visite</span><span class="sxs-lookup"><span data-stu-id="7e6ee-222">Support for List cards</span></span>

| <span data-ttu-id="7e6ee-223">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-223">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-224">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-224">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-225">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-225">Connectors</span></span> | <span data-ttu-id="7e6ee-226">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-226">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-227">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-227">✔</span></span> | <span data-ttu-id="7e6ee-228">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-228">✖</span></span> | <span data-ttu-id="7e6ee-229">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-229">✖</span></span> |<span data-ttu-id="7e6ee-230">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-230">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="7e6ee-231">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="7e6ee-231">Properties of a List card</span></span>

| <span data-ttu-id="7e6ee-232">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e6ee-232">Property</span></span> | <span data-ttu-id="7e6ee-233">Type</span><span class="sxs-lookup"><span data-stu-id="7e6ee-233">Type</span></span>  | <span data-ttu-id="7e6ee-234">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-234">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e6ee-235">title</span><span class="sxs-lookup"><span data-stu-id="7e6ee-235">title</span></span> | <span data-ttu-id="7e6ee-236">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-236">Rich text</span></span> | <span data-ttu-id="7e6ee-237">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-237">Title of the card.</span></span> <span data-ttu-id="7e6ee-238">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-238">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-239">éléments</span><span class="sxs-lookup"><span data-stu-id="7e6ee-239">items</span></span> | <span data-ttu-id="7e6ee-240">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="7e6ee-240">Array of list items</span></span>  ||
| <span data-ttu-id="7e6ee-241">descendre</span><span class="sxs-lookup"><span data-stu-id="7e6ee-241">buttons</span></span> | <span data-ttu-id="7e6ee-242">Tableau d’objets action</span><span class="sxs-lookup"><span data-stu-id="7e6ee-242">Array of action objects</span></span> | <span data-ttu-id="7e6ee-243">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-243">Set of actions applicable to the current card.</span></span> <span data-ttu-id="7e6ee-244">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-244">Maximum 6.</span></span> <span data-ttu-id="7e6ee-245">Ne s’affiche pas sur mobile.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-245">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="7e6ee-246">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="7e6ee-246">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="7e6ee-247">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7e6ee-247">Office 365 connector card</span></span>

<span data-ttu-id="7e6ee-248">Pris en charge dans Teams, pas dans l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-248">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="7e6ee-249">La carte de connecteur Office 365 offre une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-249">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="7e6ee-250">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par les robots.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-250">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="7e6ee-251">Consultez la section Remarques pour connaître les différences entre les cartes de connecteur et la carte O365.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-251">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="7e6ee-252">Prise en charge des cartes de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7e6ee-252">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="7e6ee-253">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-253">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-254">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-254">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-255">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-255">Connectors</span></span> | <span data-ttu-id="7e6ee-256">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-256">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-257">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-257">✔</span></span> | <span data-ttu-id="7e6ee-258">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-258">✔</span></span> | <span data-ttu-id="7e6ee-259">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-259">✔</span></span> | <span data-ttu-id="7e6ee-260">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-260">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="7e6ee-261">Propriétés de la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7e6ee-261">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="7e6ee-262">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e6ee-262">Property</span></span> | <span data-ttu-id="7e6ee-263">Type</span><span class="sxs-lookup"><span data-stu-id="7e6ee-263">Type</span></span>  | <span data-ttu-id="7e6ee-264">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-264">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e6ee-265">title</span><span class="sxs-lookup"><span data-stu-id="7e6ee-265">title</span></span> | <span data-ttu-id="7e6ee-266">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-266">Rich text</span></span> | <span data-ttu-id="7e6ee-267">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-267">Title of the card.</span></span> <span data-ttu-id="7e6ee-268">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-268">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-269">résumé</span><span class="sxs-lookup"><span data-stu-id="7e6ee-269">summary</span></span> | <span data-ttu-id="7e6ee-270">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-270">Rich text</span></span> | <span data-ttu-id="7e6ee-271">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-271">Summary of the card.</span></span> <span data-ttu-id="7e6ee-272">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-272">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-273">text</span><span class="sxs-lookup"><span data-stu-id="7e6ee-273">text</span></span> | <span data-ttu-id="7e6ee-274">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-274">Rich text</span></span> | <span data-ttu-id="7e6ee-275">Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="7e6ee-275">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="7e6ee-276">themeColor</span><span class="sxs-lookup"><span data-stu-id="7e6ee-276">themeColor</span></span> | <span data-ttu-id="7e6ee-277">Chaîne HEXADÉCIMALe</span><span class="sxs-lookup"><span data-stu-id="7e6ee-277">HEX string</span></span> | <span data-ttu-id="7e6ee-278">couleur qui remplace le accentColor fourni par le manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="7e6ee-278">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="7e6ee-279">Remarques sur la carte du connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7e6ee-279">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="7e6ee-280">Les cartes de connecteur Office 365 fonctionnent correctement sur Microsoft Teams, y compris les [actions ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).</span><span class="sxs-lookup"><span data-stu-id="7e6ee-280">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="7e6ee-281">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-281">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="7e6ee-282">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-282">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="7e6ee-283">Pour un bot, l' `HttpPOST` action déclenche une `invoke` activité qui envoie uniquement l’ID et le corps de l’action au bot.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-283">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="7e6ee-284">Chaque carte de connecteur peut afficher un maximum de 10 sections et chaque section peut contenir un maximum de 5 images et 5 actions.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-284">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="7e6ee-285">Les sections, images ou actions supplémentaires dans un message ne s’affichent pas.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-285">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="7e6ee-286">Tous les champs de texte prennent en charge le démarque et le code HTML.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-286">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="7e6ee-287">Vous pouvez contrôler les sections qui utilisent la démarque ou le code HTML en définissant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-287">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="7e6ee-288">Par défaut, `markdown` est défini sur `true` ; si vous préférez utiliser HTML à la place, définissez `markdown` sur `false` .</span><span class="sxs-lookup"><span data-stu-id="7e6ee-288">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="7e6ee-289">Si vous spécifiez la `themeColor` propriété, elle se substitue `accentColor` à la propriété dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-289">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="7e6ee-290">Pour spécifier le style de rendu de `activityImage` , vous pouvez définir `activityImageType` comme suit.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-290">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="7e6ee-291">Valeur</span><span class="sxs-lookup"><span data-stu-id="7e6ee-291">Value</span></span> | <span data-ttu-id="7e6ee-292">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-292">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="7e6ee-293">Default `activityImage`sera rognée en tant que cercle</span><span class="sxs-lookup"><span data-stu-id="7e6ee-293">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="7e6ee-294">`activityImage`s’affiche sous la forme d’un rectangle et conserve ses proportions</span><span class="sxs-lookup"><span data-stu-id="7e6ee-294">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="7e6ee-295">Pour tous les autres détails sur les propriétés de la carte de connecteur, consultez la [référence de carte de message](/outlook/actionable-messages/card-reference)intégrant des actions.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-295">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="7e6ee-296">Les seules propriétés de la carte de connecteur que Microsoft Teams ne prend pas en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7e6ee-296">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="7e6ee-297">`startGroup`(toujours traité comme `true` dans Teams)</span><span class="sxs-lookup"><span data-stu-id="7e6ee-297">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="7e6ee-298">Exemple de carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7e6ee-298">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="7e6ee-299">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="7e6ee-299">Receipt card</span></span>

<span data-ttu-id="7e6ee-300">Pris en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-300">Supported in Teams.</span></span>

<span data-ttu-id="7e6ee-301">Carte qui permet à un bot de fournir un accusé de réception à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-301">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="7e6ee-302">Il contient généralement la liste des éléments à inclure dans le reçu, les informations fiscales et totales, ainsi que d’autres textes.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-302">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="7e6ee-303">Prise en charge des fiches de réception</span><span class="sxs-lookup"><span data-stu-id="7e6ee-303">Support for Receipts cards</span></span>

| <span data-ttu-id="7e6ee-304">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-304">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-305">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-305">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-306">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-306">Connectors</span></span> | <span data-ttu-id="7e6ee-307">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-307">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-308">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-308">✔</span></span> | <span data-ttu-id="7e6ee-309">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-309">✔</span></span> | <span data-ttu-id="7e6ee-310">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-310">✖</span></span> | <span data-ttu-id="7e6ee-311">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-311">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="7e6ee-312">Pour plus d’informations sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="7e6ee-312">For more information on Receipt cards</span></span>

<span data-ttu-id="7e6ee-313">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="7e6ee-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="7e6ee-314">Nœud carte de réception</span><span class="sxs-lookup"><span data-stu-id="7e6ee-314">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="7e6ee-315">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="7e6ee-315">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="7e6ee-316">Carte de connexion</span><span class="sxs-lookup"><span data-stu-id="7e6ee-316">Signin card</span></span>

<span data-ttu-id="7e6ee-317">Carte qui permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-317">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="7e6ee-318">Pris en charge dans teams sous une forme légèrement différente de celle de l’infrastructure de robot.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-318">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="7e6ee-319">La carte de connexion dans teams est similaire à la carte de connexion dans l’infrastructure de robot, à l’exception que la carte de connexion dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="7e6ee-319">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="7e6ee-320">L' *action de connexion* peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement à partir de la carte de connexion.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-320">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="7e6ee-321">Pour plus d’informations sur l’authentification, voir la rubrique [Microsoft teams Authentication Flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) .</span><span class="sxs-lookup"><span data-stu-id="7e6ee-321">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="7e6ee-322">Prise en charge des cartes de connexion</span><span class="sxs-lookup"><span data-stu-id="7e6ee-322">Support for Signin cards</span></span>

| <span data-ttu-id="7e6ee-323">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-323">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-324">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-324">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-325">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-325">Connectors</span></span> | <span data-ttu-id="7e6ee-326">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-326">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-327">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-327">✔</span></span> | <span data-ttu-id="7e6ee-328">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-328">✖</span></span> | <span data-ttu-id="7e6ee-329">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-329">✖</span></span> | <span data-ttu-id="7e6ee-330">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-330">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="7e6ee-331">Pour plus d’informations sur les cartes de connexion</span><span class="sxs-lookup"><span data-stu-id="7e6ee-331">For more information on Signin cards</span></span>

<span data-ttu-id="7e6ee-332">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="7e6ee-332">Bot Framework reference:</span></span>

* [<span data-ttu-id="7e6ee-333">Nœud de la carte de connexion</span><span class="sxs-lookup"><span data-stu-id="7e6ee-333">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="7e6ee-334">Carte de connexion C #</span><span class="sxs-lookup"><span data-stu-id="7e6ee-334">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="7e6ee-335">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="7e6ee-335">Thumbnail card</span></span>

<span data-ttu-id="7e6ee-336">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-336">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="7e6ee-337">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="7e6ee-337">Support for Thumbnail cards</span></span>

| <span data-ttu-id="7e6ee-338">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-338">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-339">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-339">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-340">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-340">Connectors</span></span> | <span data-ttu-id="7e6ee-341">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-341">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-342">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-342">✔</span></span> | <span data-ttu-id="7e6ee-343">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-343">✔</span></span> | <span data-ttu-id="7e6ee-344">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-344">✖</span></span> | <span data-ttu-id="7e6ee-345">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-345">✔</span></span> |
|

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="7e6ee-347">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="7e6ee-347">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="7e6ee-348">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e6ee-348">Property</span></span> | <span data-ttu-id="7e6ee-349">Type</span><span class="sxs-lookup"><span data-stu-id="7e6ee-349">Type</span></span>  | <span data-ttu-id="7e6ee-350">Description</span><span class="sxs-lookup"><span data-stu-id="7e6ee-350">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e6ee-351">title</span><span class="sxs-lookup"><span data-stu-id="7e6ee-351">title</span></span> | <span data-ttu-id="7e6ee-352">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-352">Rich text</span></span> | <span data-ttu-id="7e6ee-353">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-353">Title of the card.</span></span> <span data-ttu-id="7e6ee-354">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-354">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-355">sous-titre</span><span class="sxs-lookup"><span data-stu-id="7e6ee-355">subtitle</span></span> | <span data-ttu-id="7e6ee-356">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-356">Rich text</span></span> | <span data-ttu-id="7e6ee-357">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-357">Subtitle of the card.</span></span> <span data-ttu-id="7e6ee-358">Maximum 2 lignes ; la mise en forme n’est pas prise en charge actuellement</span><span class="sxs-lookup"><span data-stu-id="7e6ee-358">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="7e6ee-359">text</span><span class="sxs-lookup"><span data-stu-id="7e6ee-359">text</span></span> | <span data-ttu-id="7e6ee-360">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="7e6ee-360">Rich text</span></span> | <span data-ttu-id="7e6ee-361">Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="7e6ee-361">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="7e6ee-362">images</span><span class="sxs-lookup"><span data-stu-id="7e6ee-362">images</span></span> | <span data-ttu-id="7e6ee-363">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="7e6ee-363">Array of images</span></span> | <span data-ttu-id="7e6ee-364">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-364">Image displayed at top of card.</span></span> <span data-ttu-id="7e6ee-365">Proportions 1:1 (carrés)</span><span class="sxs-lookup"><span data-stu-id="7e6ee-365">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="7e6ee-366">descendre</span><span class="sxs-lookup"><span data-stu-id="7e6ee-366">buttons</span></span> | <span data-ttu-id="7e6ee-367">Tableau d’objets action</span><span class="sxs-lookup"><span data-stu-id="7e6ee-367">Array of action objects</span></span> | <span data-ttu-id="7e6ee-368">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-368">Set of actions applicable to the current card.</span></span> <span data-ttu-id="7e6ee-369">Maximum 6</span><span class="sxs-lookup"><span data-stu-id="7e6ee-369">Maximum 6</span></span> |
| <span data-ttu-id="7e6ee-370">taper</span><span class="sxs-lookup"><span data-stu-id="7e6ee-370">tap</span></span> | <span data-ttu-id="7e6ee-371">Objet Action</span><span class="sxs-lookup"><span data-stu-id="7e6ee-371">Action object</span></span> | <span data-ttu-id="7e6ee-372">Cette action est activée lorsque l’utilisateur appuie sur la carte proprement dite.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-372">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="7e6ee-373">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="7e6ee-373">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="7e6ee-374">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="7e6ee-374">For more information</span></span>

<span data-ttu-id="7e6ee-375">Référence de l’infrastructure bot :</span><span class="sxs-lookup"><span data-stu-id="7e6ee-375">Bot Framework reference:</span></span>

* [<span data-ttu-id="7e6ee-376">Nœud de la carte miniature</span><span class="sxs-lookup"><span data-stu-id="7e6ee-376">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="7e6ee-377">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="7e6ee-377">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="7e6ee-378">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-378">Card collections</span></span>

<span data-ttu-id="7e6ee-379">Les collections de cartes sont prises en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-379">Card collections are supported in Teams.</span></span>

<span data-ttu-id="7e6ee-380">Les collections de cartes sont fournies par l’infrastructure de robot : `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="7e6ee-380">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="7e6ee-381">Ces collections peuvent contenir des cartes adaptative, héros ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-381">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="7e6ee-382">Collection carrousel</span><span class="sxs-lookup"><span data-stu-id="7e6ee-382">Carousel collection</span></span>

<span data-ttu-id="7e6ee-383">La [disposition carrousel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-383">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="7e6ee-384">Prise en charge des regroupements de carrousel</span><span class="sxs-lookup"><span data-stu-id="7e6ee-384">Support for Carousel collections</span></span>

| <span data-ttu-id="7e6ee-385">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-385">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-386">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-386">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-387">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-387">Connectors</span></span> | <span data-ttu-id="7e6ee-388">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-389">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-389">✔</span></span> | <span data-ttu-id="7e6ee-390">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-390">✖</span></span> | <span data-ttu-id="7e6ee-391">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-391">✖</span></span> | <span data-ttu-id="7e6ee-392">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-392">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="7e6ee-393">Un carrousel peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-393">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="7e6ee-394">Exemple de collection carrousel</span><span class="sxs-lookup"><span data-stu-id="7e6ee-394">Example Carousel collection</span></span>

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

<span data-ttu-id="7e6ee-396">Les propriétés sont les mêmes que pour la carte héros ou miniature.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-396">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="7e6ee-397">Syntaxe des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="7e6ee-397">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="7e6ee-398">Liste, collection</span><span class="sxs-lookup"><span data-stu-id="7e6ee-398">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="7e6ee-399">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-399">Support for List collections</span></span>

<span data-ttu-id="7e6ee-400">La disposition liste affiche une liste de cartes verticalement empilées, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-400">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="7e6ee-401">Robots dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-401">Bots in Teams</span></span> | <span data-ttu-id="7e6ee-402">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7e6ee-402">Messaging Extensions</span></span>  | <span data-ttu-id="7e6ee-403">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="7e6ee-403">Connectors</span></span> | <span data-ttu-id="7e6ee-404">Infrastructure de robot</span><span class="sxs-lookup"><span data-stu-id="7e6ee-404">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e6ee-405">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-405">✔</span></span> | <span data-ttu-id="7e6ee-406">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-406">✔</span></span> | <span data-ttu-id="7e6ee-407">✖</span><span class="sxs-lookup"><span data-stu-id="7e6ee-407">✖</span></span> | <span data-ttu-id="7e6ee-408">✔</span><span class="sxs-lookup"><span data-stu-id="7e6ee-408">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="7e6ee-409">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-409">Example List collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="7e6ee-411">Les propriétés sont les mêmes que pour la carte héros ou miniature.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-411">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="7e6ee-412">Une liste peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-412">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="7e6ee-413">Certaines combinaisons de cartes de visite ne sont pas encore prises en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-413">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="7e6ee-414">Syntaxe des collections de listes</span><span class="sxs-lookup"><span data-stu-id="7e6ee-414">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="7e6ee-415">Cartes non prises en charge dans teams</span><span class="sxs-lookup"><span data-stu-id="7e6ee-415">Cards not supported in Teams</span></span>

<span data-ttu-id="7e6ee-416">Les cartes suivantes sont implémentées par l’infrastructure de robot, mais ne sont pas prises en charge par Teams.</span><span class="sxs-lookup"><span data-stu-id="7e6ee-416">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="7e6ee-417">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="7e6ee-417">Animation cards</span></span>
* <span data-ttu-id="7e6ee-418">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="7e6ee-418">Audio cards</span></span>
* <span data-ttu-id="7e6ee-419">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="7e6ee-419">Video cards</span></span>
