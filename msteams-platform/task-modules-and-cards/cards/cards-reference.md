---
title: Référence des cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
keywords: Référence des cartes de bots
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778393"
---
# <a name="cards-reference"></a><span data-ttu-id="fd2e5-104">Référence des cartes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-104">Cards Reference</span></span>

<span data-ttu-id="fd2e5-105">Les cartes répertoriées dans cette section sont pris en charge dans les bots pour Teams.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="fd2e5-106">Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="fd2e5-107">Les différences sont appelées dans les références ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="fd2e5-108">Exemples de carte</span><span class="sxs-lookup"><span data-stu-id="fd2e5-108">Card examples</span></span>

<span data-ttu-id="fd2e5-109">Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder (v3).</span><span class="sxs-lookup"><span data-stu-id="fd2e5-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="fd2e5-110">Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="fd2e5-111">.NET</span><span class="sxs-lookup"><span data-stu-id="fd2e5-111">.NET</span></span>
  * [<span data-ttu-id="fd2e5-112">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="fd2e5-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="fd2e5-113">Exemple de code de cartes (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="fd2e5-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="fd2e5-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="fd2e5-114">Node.js</span></span>
  * [<span data-ttu-id="fd2e5-115">Ajouter des cartes en tant que pièces jointes à des messages</span><span class="sxs-lookup"><span data-stu-id="fd2e5-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="fd2e5-116">Exemple de code de cartes (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="fd2e5-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="fd2e5-117">Types de cartes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-117">Types of cards</span></span>

<span data-ttu-id="fd2e5-118">Ce tableau indique les types de cartes à votre disposition.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="fd2e5-119">Type de carte</span><span class="sxs-lookup"><span data-stu-id="fd2e5-119">Card Type</span></span> | <span data-ttu-id="fd2e5-120">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fd2e5-121">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fd2e5-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="fd2e5-122">Carte hautement personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="fd2e5-123">Hero Card</span><span class="sxs-lookup"><span data-stu-id="fd2e5-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="fd2e5-124">Contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="fd2e5-125">List Card</span><span class="sxs-lookup"><span data-stu-id="fd2e5-125">List Card</span></span>](#list-card) | <span data-ttu-id="fd2e5-126">Liste de défilement d’éléments.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="fd2e5-127">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fd2e5-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="fd2e5-128">Disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="fd2e5-129">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="fd2e5-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="fd2e5-130">Fournit un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="fd2e5-131">Signin Card</span><span class="sxs-lookup"><span data-stu-id="fd2e5-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="fd2e5-132">Permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="fd2e5-133">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="fd2e5-134">Contient généralement une seule image miniature, du texte court et un ou plusieurs boutons.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="fd2e5-135">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="fd2e5-136">Utilisé pour renvoyer plusieurs éléments dans une seule réponse</span><span class="sxs-lookup"><span data-stu-id="fd2e5-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="fd2e5-137">Propriétés communes pour toutes les cartes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="fd2e5-138">Images de carte en ligne</span><span class="sxs-lookup"><span data-stu-id="fd2e5-138">Inline card images</span></span>

<span data-ttu-id="fd2e5-139">Votre carte peut contenir une image fixe en incluant un lien vers votre image disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="fd2e5-140">Pour des raisons de performances, nous vous recommandons vivement d’héberger votre image sur un réseau de distribution de contenu (CDN) public.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="fd2e5-141">La taille des images est réduite ou monter en puissance tout en conservant les proportions pour couvrir la zone d’image, puis rognées à partir du centre pour obtenir les proportions appropriées pour la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="fd2e5-142">Les images doivent être au maximum 1024×1024 au format PNG, JPEG ou GIF ; Gif animé n’est pas officiellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-142">Images must be at most 1024×1024 in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="fd2e5-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd2e5-143">Property</span></span> | <span data-ttu-id="fd2e5-144">Type</span><span class="sxs-lookup"><span data-stu-id="fd2e5-144">Type</span></span>  | <span data-ttu-id="fd2e5-145">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd2e5-146">url</span><span class="sxs-lookup"><span data-stu-id="fd2e5-146">url</span></span> | <span data-ttu-id="fd2e5-147">URL</span><span class="sxs-lookup"><span data-stu-id="fd2e5-147">URL</span></span> | <span data-ttu-id="fd2e5-148">URL HTTPS vers l’image</span><span class="sxs-lookup"><span data-stu-id="fd2e5-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="fd2e5-149">alt</span><span class="sxs-lookup"><span data-stu-id="fd2e5-149">alt</span></span> | <span data-ttu-id="fd2e5-150">String</span><span class="sxs-lookup"><span data-stu-id="fd2e5-150">String</span></span> | <span data-ttu-id="fd2e5-151">Description accessible de l’image</span><span class="sxs-lookup"><span data-stu-id="fd2e5-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="fd2e5-152">Boutons</span><span class="sxs-lookup"><span data-stu-id="fd2e5-152">Buttons</span></span>

<span data-ttu-id="fd2e5-153">Les boutons sont affichés empilés en bas de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="fd2e5-154">Le texte du bouton est toujours sur une seule ligne et est tronqué si le texte dépasse la largeur du bouton.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="fd2e5-155">Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne s’afficheront pas.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="fd2e5-156">Pour plus [d’informations,](~/task-modules-and-cards/cards/cards-actions.md) voir Actions de carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="fd2e5-157">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="fd2e5-157">Card Formatting</span></span>

<span data-ttu-id="fd2e5-158">Pour [plus d’informations](~/task-modules-and-cards/cards/cards-format.md) sur la mise en forme du texte dans les cartes, voir Formatage de carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="fd2e5-159">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fd2e5-159">Adaptive card</span></span>

<span data-ttu-id="fd2e5-160">Carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="fd2e5-161">*Voir* [Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span><span class="sxs-lookup"><span data-stu-id="fd2e5-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="fd2e5-162">Prise en charge des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fd2e5-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="fd2e5-163">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-163">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-164">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-164">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-165">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-165">Connectors</span></span> | <span data-ttu-id="fd2e5-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-167">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-167">✔</span></span> | <span data-ttu-id="fd2e5-168">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-168">✔</span></span> | <span data-ttu-id="fd2e5-169">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-169">✖</span></span> | <span data-ttu-id="fd2e5-170">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-170">✔</span></span> |
|

> [!NOTE]
> * <span data-ttu-id="fd2e5-171">La plateforme Teams prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="fd2e5-172">Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>
### <a name="example-adaptive-card"></a><span data-ttu-id="fd2e5-173">Exemple de carte adaptative</span><span class="sxs-lookup"><span data-stu-id="fd2e5-173">Example Adaptive card</span></span>

![Exemple de carte carte adaptative](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="fd2e5-175">Pour plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fd2e5-175">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="fd2e5-176">Vue d’ensemble des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fd2e5-176">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="fd2e5-177">Actions de carte adaptative dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="fd2e5-178">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="fd2e5-178">Hero card</span></span>

<span data-ttu-id="fd2e5-179">Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="fd2e5-180">Prise en charge des cartes Hero</span><span class="sxs-lookup"><span data-stu-id="fd2e5-180">Support for Hero cards</span></span>

| <span data-ttu-id="fd2e5-181">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-181">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-182">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-182">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-183">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-183">Connectors</span></span> | <span data-ttu-id="fd2e5-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-185">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-185">✔</span></span> | <span data-ttu-id="fd2e5-186">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-186">✔</span></span> | <span data-ttu-id="fd2e5-187">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-187">✖</span></span> | <span data-ttu-id="fd2e5-188">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-188">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="fd2e5-189">Propriétés d’une carte Hero</span><span class="sxs-lookup"><span data-stu-id="fd2e5-189">Properties of a Hero card</span></span>

| <span data-ttu-id="fd2e5-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd2e5-190">Property</span></span> | <span data-ttu-id="fd2e5-191">Type</span><span class="sxs-lookup"><span data-stu-id="fd2e5-191">Type</span></span>  | <span data-ttu-id="fd2e5-192">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd2e5-193">title</span><span class="sxs-lookup"><span data-stu-id="fd2e5-193">title</span></span> | <span data-ttu-id="fd2e5-194">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-194">Rich text</span></span> | <span data-ttu-id="fd2e5-195">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-195">Title of the card.</span></span> <span data-ttu-id="fd2e5-196">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="fd2e5-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="fd2e5-197">subtitle</span></span> | <span data-ttu-id="fd2e5-198">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-198">Rich text</span></span> | <span data-ttu-id="fd2e5-199">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-199">Subtitle of the card.</span></span> <span data-ttu-id="fd2e5-200">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="fd2e5-201">text</span><span class="sxs-lookup"><span data-stu-id="fd2e5-201">text</span></span> | <span data-ttu-id="fd2e5-202">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-202">Rich text</span></span> | <span data-ttu-id="fd2e5-203">Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="fd2e5-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="fd2e5-204">images</span><span class="sxs-lookup"><span data-stu-id="fd2e5-204">images</span></span> | <span data-ttu-id="fd2e5-205">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="fd2e5-205">Array of images</span></span> | <span data-ttu-id="fd2e5-206">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-206">Image displayed at top of card.</span></span> <span data-ttu-id="fd2e5-207">Proportions 16:9</span><span class="sxs-lookup"><span data-stu-id="fd2e5-207">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="fd2e5-208">buttons</span><span class="sxs-lookup"><span data-stu-id="fd2e5-208">buttons</span></span> | <span data-ttu-id="fd2e5-209">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="fd2e5-209">Array of action objects</span></span> | <span data-ttu-id="fd2e5-210">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="fd2e5-211">Maximum 6</span><span class="sxs-lookup"><span data-stu-id="fd2e5-211">Maximum 6</span></span> |
| <span data-ttu-id="fd2e5-212">tap</span><span class="sxs-lookup"><span data-stu-id="fd2e5-212">tap</span></span> | <span data-ttu-id="fd2e5-213">Objet Action</span><span class="sxs-lookup"><span data-stu-id="fd2e5-213">Action object</span></span> | <span data-ttu-id="fd2e5-214">Cette action est activée lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-214">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="fd2e5-215">Exemple de carte Hero</span><span class="sxs-lookup"><span data-stu-id="fd2e5-215">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="fd2e5-217">Pour plus d’informations sur les cartes Hero</span><span class="sxs-lookup"><span data-stu-id="fd2e5-217">For more information on Hero cards</span></span>

<span data-ttu-id="fd2e5-218">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="fd2e5-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="fd2e5-219">Nœud de carte Hero</span><span class="sxs-lookup"><span data-stu-id="fd2e5-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="fd2e5-220">Carte Hero C #</span><span class="sxs-lookup"><span data-stu-id="fd2e5-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="fd2e5-221">Carte de liste</span><span class="sxs-lookup"><span data-stu-id="fd2e5-221">List card</span></span>

<span data-ttu-id="fd2e5-222">La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="fd2e5-223">La carte de liste fournit une liste d’éléments à défilement.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="fd2e5-224">Prise en charge des cartes de liste</span><span class="sxs-lookup"><span data-stu-id="fd2e5-224">Support for List cards</span></span>

| <span data-ttu-id="fd2e5-225">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-225">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-226">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-226">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-227">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-227">Connectors</span></span> | <span data-ttu-id="fd2e5-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-229">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-229">✔</span></span> | <span data-ttu-id="fd2e5-230">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-230">✖</span></span> | <span data-ttu-id="fd2e5-231">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-231">✖</span></span> |<span data-ttu-id="fd2e5-232">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-232">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="fd2e5-233">Propriétés d’une carte de liste</span><span class="sxs-lookup"><span data-stu-id="fd2e5-233">Properties of a List card</span></span>

| <span data-ttu-id="fd2e5-234">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd2e5-234">Property</span></span> | <span data-ttu-id="fd2e5-235">Type</span><span class="sxs-lookup"><span data-stu-id="fd2e5-235">Type</span></span>  | <span data-ttu-id="fd2e5-236">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd2e5-237">title</span><span class="sxs-lookup"><span data-stu-id="fd2e5-237">title</span></span> | <span data-ttu-id="fd2e5-238">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-238">Rich text</span></span> | <span data-ttu-id="fd2e5-239">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-239">Title of the card.</span></span> <span data-ttu-id="fd2e5-240">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="fd2e5-241">éléments</span><span class="sxs-lookup"><span data-stu-id="fd2e5-241">items</span></span> | <span data-ttu-id="fd2e5-242">Tableau d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="fd2e5-242">Array of list items</span></span>  ||
| <span data-ttu-id="fd2e5-243">buttons</span><span class="sxs-lookup"><span data-stu-id="fd2e5-243">buttons</span></span> | <span data-ttu-id="fd2e5-244">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="fd2e5-244">Array of action objects</span></span> | <span data-ttu-id="fd2e5-245">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="fd2e5-246">Maximum 6.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-246">Maximum 6.</span></span> |

### <a name="example-list-card"></a><span data-ttu-id="fd2e5-247">Exemple de carte de liste</span><span class="sxs-lookup"><span data-stu-id="fd2e5-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="fd2e5-248">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fd2e5-248">Office 365 connector card</span></span>

<span data-ttu-id="fd2e5-249">Pris en charge dans Teams, et non dans Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="fd2e5-250">La carte connecteur Office 365 fournit une disposition flexible avec plusieurs sections, champs, images et actions.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="fd2e5-251">Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par des bots.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="fd2e5-252">Consultez la section remarques pour les différences entre les cartes de connecteur et la carte O365.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="fd2e5-253">Prise en charge des cartes de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fd2e5-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="fd2e5-254">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-254">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-255">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-255">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-256">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-256">Connectors</span></span> | <span data-ttu-id="fd2e5-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-258">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-258">✔</span></span> | <span data-ttu-id="fd2e5-259">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-259">✔</span></span> | <span data-ttu-id="fd2e5-260">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-260">✔</span></span> | <span data-ttu-id="fd2e5-261">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="fd2e5-262">Propriétés de la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fd2e5-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="fd2e5-263">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd2e5-263">Property</span></span> | <span data-ttu-id="fd2e5-264">Type</span><span class="sxs-lookup"><span data-stu-id="fd2e5-264">Type</span></span>  | <span data-ttu-id="fd2e5-265">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd2e5-266">title</span><span class="sxs-lookup"><span data-stu-id="fd2e5-266">title</span></span> | <span data-ttu-id="fd2e5-267">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-267">Rich text</span></span> | <span data-ttu-id="fd2e5-268">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-268">Title of the card.</span></span> <span data-ttu-id="fd2e5-269">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="fd2e5-270">résumé</span><span class="sxs-lookup"><span data-stu-id="fd2e5-270">summary</span></span> | <span data-ttu-id="fd2e5-271">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-271">Rich text</span></span> | <span data-ttu-id="fd2e5-272">Résumé de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-272">Summary of the card.</span></span> <span data-ttu-id="fd2e5-273">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="fd2e5-274">text</span><span class="sxs-lookup"><span data-stu-id="fd2e5-274">text</span></span> | <span data-ttu-id="fd2e5-275">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-275">Rich text</span></span> | <span data-ttu-id="fd2e5-276">Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="fd2e5-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="fd2e5-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="fd2e5-277">themeColor</span></span> | <span data-ttu-id="fd2e5-278">Chaîne HEX</span><span class="sxs-lookup"><span data-stu-id="fd2e5-278">HEX string</span></span> | <span data-ttu-id="fd2e5-279">couleur qui remplace l’accentColor fourni à partir du manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="fd2e5-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="fd2e5-280">Remarques sur la carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fd2e5-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="fd2e5-281">Les cartes de connecteur Office 365 fonctionnent correctement sur Microsoft Teams, y compris les [actions ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)</span><span class="sxs-lookup"><span data-stu-id="fd2e5-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="fd2e5-282">Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="fd2e5-283">Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="fd2e5-284">Pour un bot, l’action déclenche une activité qui envoie uniquement l’ID d’action et le `HttpPOST` `invoke` corps au bot.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="fd2e5-285">Chaque carte de connecteur peut afficher un maximum de 10 sections, et chaque section peut contenir un maximum de 5 images et 5 actions.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="fd2e5-286">Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="fd2e5-287">Tous les champs de texte sont en charge markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="fd2e5-288">Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant la `markdown` propriété dans un message.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="fd2e5-289">Par défaut, `markdown` est définie sur ; si vous souhaitez utiliser html à la `true` place, définie sur `markdown` `false` .</span><span class="sxs-lookup"><span data-stu-id="fd2e5-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="fd2e5-290">Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="fd2e5-291">Pour spécifier le style de `activityImage` rendu pour , vous pouvez définir comme `activityImageType` suit.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="fd2e5-292">Valeur</span><span class="sxs-lookup"><span data-stu-id="fd2e5-292">Value</span></span> | <span data-ttu-id="fd2e5-293">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="fd2e5-294">Valeur par défaut ; `activityImage` sera rogcé en tant que cercle</span><span class="sxs-lookup"><span data-stu-id="fd2e5-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="fd2e5-295">`activityImage` sera affiché sous forme de rectangle et conservera ses proportions</span><span class="sxs-lookup"><span data-stu-id="fd2e5-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="fd2e5-296">Pour plus d’informations sur les propriétés de carte de connecteur, voir la référence de carte [de message actionnable.](/outlook/actionable-messages/card-reference)</span><span class="sxs-lookup"><span data-stu-id="fd2e5-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="fd2e5-297">Les seules propriétés de carte de connecteur que Microsoft Teams ne prend pas en charge actuellement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd2e5-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="fd2e5-298">`startGroup` (toujours traité comme `true` dans Teams)</span><span class="sxs-lookup"><span data-stu-id="fd2e5-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="fd2e5-299">Exemple de carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="fd2e5-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="fd2e5-300">Carte d’accusé de réception</span><span class="sxs-lookup"><span data-stu-id="fd2e5-300">Receipt card</span></span>

<span data-ttu-id="fd2e5-301">Pris en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-301">Supported in Teams.</span></span>

<span data-ttu-id="fd2e5-302">Carte qui permet à un bot de fournir un reçu à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="fd2e5-303">Il contient généralement la liste des éléments à inclure sur le reçu, les taxes et le total des informations, ainsi que d’autres informations.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="fd2e5-304">Prise en charge des cartes de reçus</span><span class="sxs-lookup"><span data-stu-id="fd2e5-304">Support for Receipts cards</span></span>

| <span data-ttu-id="fd2e5-305">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-305">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-306">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-306">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-307">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-307">Connectors</span></span> | <span data-ttu-id="fd2e5-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-309">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-309">✔</span></span> | <span data-ttu-id="fd2e5-310">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-310">✔</span></span> | <span data-ttu-id="fd2e5-311">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-311">✖</span></span> | <span data-ttu-id="fd2e5-312">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="fd2e5-313">Pour plus d’informations sur les cartes de réception</span><span class="sxs-lookup"><span data-stu-id="fd2e5-313">For more information on Receipt cards</span></span>

<span data-ttu-id="fd2e5-314">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="fd2e5-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="fd2e5-315">Nœud de carte de réception</span><span class="sxs-lookup"><span data-stu-id="fd2e5-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="fd2e5-316">Carte de réception C #</span><span class="sxs-lookup"><span data-stu-id="fd2e5-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="fd2e5-317">Carte de signature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-317">Signin card</span></span>

<span data-ttu-id="fd2e5-318">Carte qui permet à un bot de demander à un utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="fd2e5-319">Pris en charge dans Teams sous une forme légèrement différente de celle de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="fd2e5-320">La carte de signature dans Teams est similaire à la carte de signin dans l’infrastructure du bot, à l’exception du fait que la carte de signin dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .</span><span class="sxs-lookup"><span data-stu-id="fd2e5-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="fd2e5-321">*L’action de signin* peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement de la carte de signature.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="fd2e5-322">Consultez la rubrique [Flux d’authentification Microsoft Teams pour les bots](~/bots/how-to/authentication/auth-flow-bot.md) pour plus d’informations sur l’authentification.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="fd2e5-323">Prise en charge des cartes de signature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-323">Support for Signin cards</span></span>

| <span data-ttu-id="fd2e5-324">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-324">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-325">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-325">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-326">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-326">Connectors</span></span> | <span data-ttu-id="fd2e5-327">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-328">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-328">✔</span></span> | <span data-ttu-id="fd2e5-329">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-329">✖</span></span> | <span data-ttu-id="fd2e5-330">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-330">✖</span></span> | <span data-ttu-id="fd2e5-331">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="fd2e5-332">Pour plus d’informations sur les cartes de signature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-332">For more information on Signin cards</span></span>

<span data-ttu-id="fd2e5-333">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="fd2e5-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="fd2e5-334">Nœud de carte de signature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="fd2e5-335">Carte de signature C #</span><span class="sxs-lookup"><span data-stu-id="fd2e5-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="fd2e5-336">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-336">Thumbnail card</span></span>

<span data-ttu-id="fd2e5-337">Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="fd2e5-338">Prise en charge des cartes miniatures</span><span class="sxs-lookup"><span data-stu-id="fd2e5-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="fd2e5-339">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-339">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-340">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-340">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-341">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-341">Connectors</span></span> | <span data-ttu-id="fd2e5-342">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-343">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-343">✔</span></span> | <span data-ttu-id="fd2e5-344">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-344">✔</span></span> | <span data-ttu-id="fd2e5-345">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-345">✖</span></span> | <span data-ttu-id="fd2e5-346">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-346">✔</span></span> |
|

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="fd2e5-348">Propriétés d’une carte miniature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="fd2e5-349">Propriété</span><span class="sxs-lookup"><span data-stu-id="fd2e5-349">Property</span></span> | <span data-ttu-id="fd2e5-350">Type</span><span class="sxs-lookup"><span data-stu-id="fd2e5-350">Type</span></span>  | <span data-ttu-id="fd2e5-351">Description</span><span class="sxs-lookup"><span data-stu-id="fd2e5-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd2e5-352">title</span><span class="sxs-lookup"><span data-stu-id="fd2e5-352">title</span></span> | <span data-ttu-id="fd2e5-353">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-353">Rich text</span></span> | <span data-ttu-id="fd2e5-354">Titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-354">Title of the card.</span></span> <span data-ttu-id="fd2e5-355">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-355">Maximum 2 lines.</span></span>|
| <span data-ttu-id="fd2e5-356">subtitle</span><span class="sxs-lookup"><span data-stu-id="fd2e5-356">subtitle</span></span> | <span data-ttu-id="fd2e5-357">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-357">Rich text</span></span> | <span data-ttu-id="fd2e5-358">Sous-titre de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-358">Subtitle of the card.</span></span> <span data-ttu-id="fd2e5-359">Maximum 2 lignes.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-359">Maximum 2 lines.</span></span>|
| <span data-ttu-id="fd2e5-360">text</span><span class="sxs-lookup"><span data-stu-id="fd2e5-360">text</span></span> | <span data-ttu-id="fd2e5-361">Texte enrichi </span><span class="sxs-lookup"><span data-stu-id="fd2e5-361">Rich text</span></span> | <span data-ttu-id="fd2e5-362">Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme</span><span class="sxs-lookup"><span data-stu-id="fd2e5-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="fd2e5-363">images</span><span class="sxs-lookup"><span data-stu-id="fd2e5-363">images</span></span> | <span data-ttu-id="fd2e5-364">Tableau d’images</span><span class="sxs-lookup"><span data-stu-id="fd2e5-364">Array of images</span></span> | <span data-ttu-id="fd2e5-365">Image affichée en haut de la carte.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-365">Image displayed at top of card.</span></span> <span data-ttu-id="fd2e5-366">Proportions 1:1 (carré)</span><span class="sxs-lookup"><span data-stu-id="fd2e5-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="fd2e5-367">buttons</span><span class="sxs-lookup"><span data-stu-id="fd2e5-367">buttons</span></span> | <span data-ttu-id="fd2e5-368">Tableau d’objets d’action</span><span class="sxs-lookup"><span data-stu-id="fd2e5-368">Array of action objects</span></span> | <span data-ttu-id="fd2e5-369">Ensemble d’actions applicables à la carte actuelle.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="fd2e5-370">Maximum 6</span><span class="sxs-lookup"><span data-stu-id="fd2e5-370">Maximum 6</span></span> |
| <span data-ttu-id="fd2e5-371">tap</span><span class="sxs-lookup"><span data-stu-id="fd2e5-371">tap</span></span> | <span data-ttu-id="fd2e5-372">Objet Action</span><span class="sxs-lookup"><span data-stu-id="fd2e5-372">Action object</span></span> | <span data-ttu-id="fd2e5-373">Cette action est activée lorsque l’utilisateur tape sur la carte elle-même.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="fd2e5-374">Exemple de carte miniature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="fd2e5-375">Pour plus d'informations</span><span class="sxs-lookup"><span data-stu-id="fd2e5-375">For more information</span></span>

<span data-ttu-id="fd2e5-376">Référence Bot Framework :</span><span class="sxs-lookup"><span data-stu-id="fd2e5-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="fd2e5-377">Nœud de carte miniature</span><span class="sxs-lookup"><span data-stu-id="fd2e5-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="fd2e5-378">Carte miniature C #</span><span class="sxs-lookup"><span data-stu-id="fd2e5-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="fd2e5-379">Collections de cartes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-379">Card collections</span></span>

<span data-ttu-id="fd2e5-380">Les collections de cartes sont pris en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="fd2e5-381">Collections de cartes `builder.AttachmentLayout.carousel` : et `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="fd2e5-381">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="fd2e5-382">Ces collections contiennent des cartes adaptatives, Hero ou Miniatures.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-382">These collections contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="fd2e5-383">Collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="fd2e5-383">Carousel collection</span></span>

<span data-ttu-id="fd2e5-384">La [disposition de carrousel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="fd2e5-385">Prise en charge des collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="fd2e5-385">Support for Carousel collections</span></span>

| <span data-ttu-id="fd2e5-386">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-386">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-387">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-387">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-388">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-388">Connectors</span></span> | <span data-ttu-id="fd2e5-389">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-390">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-390">✔</span></span> | <span data-ttu-id="fd2e5-391">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-391">✖</span></span> | <span data-ttu-id="fd2e5-392">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-392">✖</span></span> | <span data-ttu-id="fd2e5-393">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="fd2e5-394">Un carrousel peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="fd2e5-395">Propriétés d’une carte Carrousel</span><span class="sxs-lookup"><span data-stu-id="fd2e5-395">Properties of a Carousel card</span></span>

<span data-ttu-id="fd2e5-396">Les propriétés d’une carte Carrousel sont identiques à celles des cartes Hero et Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-396">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="fd2e5-397">Exemple de collection de carrousels</span><span class="sxs-lookup"><span data-stu-id="fd2e5-397">Example Carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="fd2e5-399">Syntaxe pour les collections de carrousels</span><span class="sxs-lookup"><span data-stu-id="fd2e5-399">Syntax for Carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="fd2e5-400">Collection de listes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-400">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="fd2e5-401">Prise en charge des collections de listes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-401">Support for List collections</span></span>

<span data-ttu-id="fd2e5-402">La disposition de liste affiche une liste de cartes empilées verticalement, éventuellement avec des boutons d’action associés.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-402">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="fd2e5-403">Bots dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-403">Bots in Teams</span></span> | <span data-ttu-id="fd2e5-404">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="fd2e5-404">Messaging Extensions</span></span>  | <span data-ttu-id="fd2e5-405">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="fd2e5-405">Connectors</span></span> | <span data-ttu-id="fd2e5-406">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fd2e5-406">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fd2e5-407">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-407">✔</span></span> | <span data-ttu-id="fd2e5-408">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-408">✔</span></span> | <span data-ttu-id="fd2e5-409">✖</span><span class="sxs-lookup"><span data-stu-id="fd2e5-409">✖</span></span> | <span data-ttu-id="fd2e5-410">✔</span><span class="sxs-lookup"><span data-stu-id="fd2e5-410">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="fd2e5-411">Exemple de collection de listes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-411">Example List collection</span></span>

![Exemple de liste de cartes](~/assets/images/cards/list.png)

<span data-ttu-id="fd2e5-413">Les propriétés sont identiques à la carte hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-413">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="fd2e5-414">Une liste peut afficher un maximum de 10 cartes par message.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-414">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="fd2e5-415">Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-415">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="fd2e5-416">Syntaxe pour les collections de listes</span><span class="sxs-lookup"><span data-stu-id="fd2e5-416">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="fd2e5-417">Cartes non pris en charge dans Teams</span><span class="sxs-lookup"><span data-stu-id="fd2e5-417">Cards not supported in Teams</span></span>

<span data-ttu-id="fd2e5-418">Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas pris en charge par Teams.</span><span class="sxs-lookup"><span data-stu-id="fd2e5-418">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="fd2e5-419">Cartes d’animation</span><span class="sxs-lookup"><span data-stu-id="fd2e5-419">Animation cards</span></span>
* <span data-ttu-id="fd2e5-420">Cartes audio</span><span class="sxs-lookup"><span data-stu-id="fd2e5-420">Audio cards</span></span>
* <span data-ttu-id="fd2e5-421">Cartes vidéo</span><span class="sxs-lookup"><span data-stu-id="fd2e5-421">Video cards</span></span>
