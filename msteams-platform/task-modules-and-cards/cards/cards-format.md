---
title: Mise en forme de texte dans les cartes
description: Décrit la mise en forme de texte de carte dans Microsoft teams
keywords: format des cartes robots teams
ms.date: 03/29/2018
ms.openlocfilehash: 0c723c436346498ed2e5704db6f6401204530165
ms.sourcegitcommit: 646a8224523be7db96f9686e22d420d62d55d4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "42365247"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="88011-104">Cartes de format dans teams</span><span class="sxs-lookup"><span data-stu-id="88011-104">Format cards in Teams</span></span>

<span data-ttu-id="88011-105">Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de la démarque ou du code HTML, selon le type de carte.</span><span class="sxs-lookup"><span data-stu-id="88011-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="88011-106">Les cartes prennent en charge la mise en forme uniquement dans la propriété Text, pas dans les propriétés Title ou title.</span><span class="sxs-lookup"><span data-stu-id="88011-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="88011-107">La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de la mise en forme XML (HTML) ou de la démarque selon le type de carte.</span><span class="sxs-lookup"><span data-stu-id="88011-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="88011-108">Pour les cartes adaptatives de développement actuelles et futures, il est recommandé d’utiliser la mise en forme de démarque.</span><span class="sxs-lookup"><span data-stu-id="88011-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="88011-109">La prise en charge de la mise en forme diffère selon les types de carte et le rendu de la carte peut légèrement varier entre le bureau et les clients teams mobiles, ainsi que teams dans le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="88011-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="88011-110">Vous pouvez inclure une image incluse avec n’importe quelle carte Teams.</span><span class="sxs-lookup"><span data-stu-id="88011-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="88011-111">Images un format `.png`, `.jpg`ou `.gif` des fichiers, ne doit pas dépasser 1024 × 1024 PX ou 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="88011-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="88011-112">L’image GIF animée n’est pas officiellement prise en charge.</span><span class="sxs-lookup"><span data-stu-id="88011-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="88011-113">*Voir* [référence des fiches](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="88011-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="88011-114">Mise en forme de cartes avec démarque</span><span class="sxs-lookup"><span data-stu-id="88011-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="88011-115">Il existe deux types de cartes qui prennent en charge la démarque dans teams :</span><span class="sxs-lookup"><span data-stu-id="88011-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88011-116">**Cartes adaptatives**: la démarque est prise en charge `Textblock` dans le champ carte adaptative `Fact.Title` , `Fact.Value`ainsi que et.</span><span class="sxs-lookup"><span data-stu-id="88011-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="88011-117">HTML n’est pas pris en charge dans les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="88011-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="88011-118">**Cartes de connecteur O365**: la démarque et le code html limité sont pris en charge dans les cartes de connecteur Office 365 dans les champs de texte.</span><span class="sxs-lookup"><span data-stu-id="88011-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="88011-119">**Mise en forme des démarques : cartes adaptatives**</span><span class="sxs-lookup"><span data-stu-id="88011-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="88011-120">Les styles pris en `Textblock`charge `Fact.Title` pour `Fact.Value` et sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88011-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="88011-121">Style</span><span class="sxs-lookup"><span data-stu-id="88011-121">Style</span></span> | <span data-ttu-id="88011-122">Exemple</span><span class="sxs-lookup"><span data-stu-id="88011-122">Example</span></span> | <span data-ttu-id="88011-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="88011-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88011-124">bold</span><span class="sxs-lookup"><span data-stu-id="88011-124">bold</span></span> | <span data-ttu-id="88011-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="88011-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="88011-126">italic</span><span class="sxs-lookup"><span data-stu-id="88011-126">italic</span></span> | <span data-ttu-id="88011-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="88011-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="88011-128">liste non triée</span><span class="sxs-lookup"><span data-stu-id="88011-128">unordered list</span></span> | <ul><li><span data-ttu-id="88011-129">text</span><span class="sxs-lookup"><span data-stu-id="88011-129">text</span></span></li><li><span data-ttu-id="88011-130">text</span><span class="sxs-lookup"><span data-stu-id="88011-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="88011-131">liste triée</span><span class="sxs-lookup"><span data-stu-id="88011-131">ordered list</span></span> | <ol><li><span data-ttu-id="88011-132">text</span><span class="sxs-lookup"><span data-stu-id="88011-132">text</span></span></li><li><span data-ttu-id="88011-133">text</span><span class="sxs-lookup"><span data-stu-id="88011-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="88011-134">Liens hypertexte</span><span class="sxs-lookup"><span data-stu-id="88011-134">Hyperlinks</span></span> |[<span data-ttu-id="88011-135">Bing</span><span class="sxs-lookup"><span data-stu-id="88011-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="88011-136">Les balises de démarques suivantes ne sont pas prises en charge :</span><span class="sxs-lookup"><span data-stu-id="88011-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="88011-137">En-têtes</span><span class="sxs-lookup"><span data-stu-id="88011-137">Headers</span></span>
* <span data-ttu-id="88011-138">Tables</span><span class="sxs-lookup"><span data-stu-id="88011-138">Tables</span></span>
* <span data-ttu-id="88011-139">Des images</span><span class="sxs-lookup"><span data-stu-id="88011-139">Images</span></span>
* <span data-ttu-id="88011-140">Texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="88011-140">Preformatted text</span></span>
* <span data-ttu-id="88011-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="88011-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88011-142">Les cartes adaptatives ne prennent pas en charge la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="88011-142">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="88011-143">Nouvelles lignes de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88011-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="88011-144">Dans les listes, vous pouvez `\r` utiliser `\n` les séquences d’échappement ou pour les nouvelles lignes.</span><span class="sxs-lookup"><span data-stu-id="88011-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="88011-145">L' `\n\n` utilisation d’une liste entraîne le retrait de l’élément suivant dans la liste.</span><span class="sxs-lookup"><span data-stu-id="88011-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="88011-146">Si vous avez besoin de nouvelles lignes ailleurs dans TextBlock `\n\n`, utilisez.</span><span class="sxs-lookup"><span data-stu-id="88011-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="88011-147">Différences entre les appareils mobiles et de bureau pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88011-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="88011-148">La mise en forme diffère légèrement entre le bureau et les versions mobiles de teams.</span><span class="sxs-lookup"><span data-stu-id="88011-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="88011-149">Sur le bureau, le format des démarques de carte adaptative apparaît comme dans les navigateurs Web et dans l’application cliente teams :</span><span class="sxs-lookup"><span data-stu-id="88011-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Mise en forme adaptative de la démarque de carte dans le client de bureau](/assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="88011-151">Sous iOS, la mise en forme adaptative de carte de visite apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![Mise en forme adaptative de la démarque de carte dans iOS](/assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="88011-153">Sous Android, la mise en forme de la démarque de carte adaptative apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Mise en forme adaptative de la démarque de carte dans Android](/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="88011-155">Plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88011-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="88011-156">[Fonctionnalités de texte dans des cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans cette rubrique ne sont pas prises en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="88011-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="88011-157">Exemple de mise en forme des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88011-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="88011-158">Mentionner la prise en charge dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88011-158">Mention support within Adaptive cards</span></span>

> [!NOTE]
> <span data-ttu-id="88011-159">Mentionner la prise en charge des cartes est actuellement prise en charge en version préliminaire pour les [développeurs](../../resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="88011-159">Mention support in cards is currently supported in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="88011-160">Les robots et les extensions de messagerie peuvent désormais inclure des mentions dans le contenu des cartes dans les éléments bloc de texte et FactSet.</span><span class="sxs-lookup"><span data-stu-id="88011-160">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="88011-161">Création de mentions</span><span class="sxs-lookup"><span data-stu-id="88011-161">Constructing mentions</span></span>

<span data-ttu-id="88011-162">Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants</span><span class="sxs-lookup"><span data-stu-id="88011-162">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="88011-163">`<at>username</at>`dans les éléments de carte adaptative pris en charge</span><span class="sxs-lookup"><span data-stu-id="88011-163">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="88011-164">`mention` Objet à l’intérieur d' `msteams` une propriété dans le contenu de la carte, qui inclut l’ID utilisateur teams de l’utilisateur mentionné</span><span class="sxs-lookup"><span data-stu-id="88011-164">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="88011-165">Notez que les cartes avec des mentions ne sont pas prises en charge sur les clients mobiles pour le moment.</span><span class="sxs-lookup"><span data-stu-id="88011-165">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="88011-166">Exemple de carte adaptative avec une mention</span><span class="sxs-lookup"><span data-stu-id="88011-166">Sample Adaptive card with a mention</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="88011-167">**Mise en forme des démarques : cartes de connecteur O365**</span><span class="sxs-lookup"><span data-stu-id="88011-167">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="88011-168">Les cartes de connecteur prennent en charge la démarque limitée et la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="88011-168">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="88011-169">La prise en charge du langage HTML est décrite dans la dernière section.</span><span class="sxs-lookup"><span data-stu-id="88011-169">HTML support is described in the last section.</span></span>

| <span data-ttu-id="88011-170">Style</span><span class="sxs-lookup"><span data-stu-id="88011-170">Style</span></span> | <span data-ttu-id="88011-171">Exemple</span><span class="sxs-lookup"><span data-stu-id="88011-171">Example</span></span> | <span data-ttu-id="88011-172">Markdown</span><span class="sxs-lookup"><span data-stu-id="88011-172">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88011-173">bold</span><span class="sxs-lookup"><span data-stu-id="88011-173">bold</span></span> | <span data-ttu-id="88011-174">**text**</span><span class="sxs-lookup"><span data-stu-id="88011-174">**text**</span></span> | `**text**` |
| <span data-ttu-id="88011-175">italic</span><span class="sxs-lookup"><span data-stu-id="88011-175">italic</span></span> | <span data-ttu-id="88011-176">*text*</span><span class="sxs-lookup"><span data-stu-id="88011-176">*text*</span></span> | `*text*` |
| <span data-ttu-id="88011-177">en-tête (&ndash;niveaux 1 à 3)</span><span class="sxs-lookup"><span data-stu-id="88011-177">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="88011-178">**Text**</span><span class="sxs-lookup"><span data-stu-id="88011-178">**Text**</span></span> | `### Text`|
| <span data-ttu-id="88011-179">doubles</span><span class="sxs-lookup"><span data-stu-id="88011-179">strikethrough</span></span> | <span data-ttu-id="88011-180">~~text~~</span><span class="sxs-lookup"><span data-stu-id="88011-180">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="88011-181">liste non triée</span><span class="sxs-lookup"><span data-stu-id="88011-181">unordered list</span></span> | <ul><li><span data-ttu-id="88011-182">text</span><span class="sxs-lookup"><span data-stu-id="88011-182">text</span></span></li><li><span data-ttu-id="88011-183">text</span><span class="sxs-lookup"><span data-stu-id="88011-183">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="88011-184">liste triée</span><span class="sxs-lookup"><span data-stu-id="88011-184">ordered list</span></span> | <ol><li><span data-ttu-id="88011-185">text</span><span class="sxs-lookup"><span data-stu-id="88011-185">text</span></span></li><li><span data-ttu-id="88011-186">text</span><span class="sxs-lookup"><span data-stu-id="88011-186">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="88011-187">texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="88011-187">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="88011-188">blockquote</span><span class="sxs-lookup"><span data-stu-id="88011-188">blockquote</span></span> | <span data-ttu-id="88011-189">Texte >BLOCKQUOTE</span><span class="sxs-lookup"><span data-stu-id="88011-189">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="88011-190">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="88011-190">hyperlink</span></span> | [<span data-ttu-id="88011-191">Bing</span><span class="sxs-lookup"><span data-stu-id="88011-191">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="88011-192">lien de l’image</span><span class="sxs-lookup"><span data-stu-id="88011-192">image link</span></span> |![Canard sur une roche](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="88011-194">Dans les cartes de connecteur, les nouvelles `\n\n`lignes sont affichées pour `\n` , `\r`mais pas pour ou.</span><span class="sxs-lookup"><span data-stu-id="88011-194">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="88011-195">Différences de bureau et de téléphone pour les cartes de connecteur utilisant la démarque</span><span class="sxs-lookup"><span data-stu-id="88011-195">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="88011-196">Sur le bureau, la mise en forme de démarque pour les cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-196">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme des démarques pour les cartes de connecteur dans le client de bureau](/assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="88011-198">Sur iOS, la mise en forme de démarque pour les cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-198">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme des démarques pour les cartes de connecteur dans le client iOS](/assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="88011-200">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="88011-200">Issues:</span></span>

* <span data-ttu-id="88011-201">Le client iOS pour Teams ne restitue pas les images insérées de démarque ou HTML dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="88011-201">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="88011-202">Les blockquotes sont affichés sous forme de retrait, mais sans arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="88011-202">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="88011-203">Sur Android, la mise en forme des démarques pour les cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-203">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme des démarques pour les cartes de connecteur dans le client Android](/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="88011-205">Exemple de mise en forme pour les fiches de connecteur de démarque</span><span class="sxs-lookup"><span data-stu-id="88011-205">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="88011-206">Mise en forme de cartes avec HTML</span><span class="sxs-lookup"><span data-stu-id="88011-206">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="88011-207">**Mise en forme HTML : cartes de connecteur O365**</span><span class="sxs-lookup"><span data-stu-id="88011-207">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="88011-208">Les cartes de connecteur prennent en charge la démarque limitée et la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="88011-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="88011-209">La démarque est décrite dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="88011-209">Markdown is described in the next section.</span></span>

| <span data-ttu-id="88011-210">Style</span><span class="sxs-lookup"><span data-stu-id="88011-210">Style</span></span> | <span data-ttu-id="88011-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="88011-211">Example</span></span> | <span data-ttu-id="88011-212">HTML</span><span class="sxs-lookup"><span data-stu-id="88011-212">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88011-213">bold</span><span class="sxs-lookup"><span data-stu-id="88011-213">bold</span></span> | <span data-ttu-id="88011-214">**text**</span><span class="sxs-lookup"><span data-stu-id="88011-214">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="88011-215">italic</span><span class="sxs-lookup"><span data-stu-id="88011-215">italic</span></span> | <span data-ttu-id="88011-216">*text*</span><span class="sxs-lookup"><span data-stu-id="88011-216">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="88011-217">en-tête (&ndash;niveaux 1 à 3)</span><span class="sxs-lookup"><span data-stu-id="88011-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="88011-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="88011-218">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="88011-219">doubles</span><span class="sxs-lookup"><span data-stu-id="88011-219">strikethrough</span></span> | <span data-ttu-id="88011-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="88011-220">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="88011-221">liste non triée</span><span class="sxs-lookup"><span data-stu-id="88011-221">unordered list</span></span> | <ul><li><span data-ttu-id="88011-222">text</span><span class="sxs-lookup"><span data-stu-id="88011-222">text</span></span></li><li><span data-ttu-id="88011-223">text</span><span class="sxs-lookup"><span data-stu-id="88011-223">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="88011-224">liste triée</span><span class="sxs-lookup"><span data-stu-id="88011-224">ordered list</span></span> | <ol><li><span data-ttu-id="88011-225">text</span><span class="sxs-lookup"><span data-stu-id="88011-225">text</span></span></li><li><span data-ttu-id="88011-226">text</span><span class="sxs-lookup"><span data-stu-id="88011-226">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="88011-227">texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="88011-227">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="88011-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="88011-228">blockquote</span></span> | <blockquote><span data-ttu-id="88011-229">text</span><span class="sxs-lookup"><span data-stu-id="88011-229">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="88011-230">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="88011-230">hyperlink</span></span> | [<span data-ttu-id="88011-231">Bing</span><span class="sxs-lookup"><span data-stu-id="88011-231">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="88011-232">lien de l’image</span><span class="sxs-lookup"><span data-stu-id="88011-232">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="88011-233">Dans les cartes de connecteur, les nouvelles lignes sont affichées `<p>` en HTML à l’aide de la balise.</span><span class="sxs-lookup"><span data-stu-id="88011-233">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="88011-234">Différences entre les appareils mobiles et de bureau pour les cartes de connecteur à l’aide de HTML</span><span class="sxs-lookup"><span data-stu-id="88011-234">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="88011-235">Sur le bureau, la mise en forme HTML des cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-235">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](/assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="88011-237">Sur iOS, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-237">On iOS, HTML formatting looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](/assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="88011-239">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="88011-239">Issues:</span></span>

* <span data-ttu-id="88011-240">Les images en ligne ne sont pas rendues sur iOS à l’aide de la démarque ou du code HTML dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="88011-240">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="88011-241">Le texte préformaté est affiché, mais il n’a pas d’arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="88011-241">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="88011-242">Sur Android, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-242">On Android, HTML formatting looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client Android](/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="88011-244">Exemple de mise en forme des cartes de connecteur HTML</span><span class="sxs-lookup"><span data-stu-id="88011-244">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="88011-245">**Mise en forme HTML : cartes de héros et miniatures**</span><span class="sxs-lookup"><span data-stu-id="88011-245">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="88011-246">Les balises HTML sont prises en charge pour les cartes simples telles que le héros et la carte miniature.</span><span class="sxs-lookup"><span data-stu-id="88011-246">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="88011-247">La démarque n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="88011-247">Markdown is not supported.</span></span>

| <span data-ttu-id="88011-248">Style</span><span class="sxs-lookup"><span data-stu-id="88011-248">Style</span></span> | <span data-ttu-id="88011-249">Exemple</span><span class="sxs-lookup"><span data-stu-id="88011-249">Example</span></span> | <span data-ttu-id="88011-250">HTML</span><span class="sxs-lookup"><span data-stu-id="88011-250">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88011-251">bold</span><span class="sxs-lookup"><span data-stu-id="88011-251">bold</span></span> | <span data-ttu-id="88011-252">**text**</span><span class="sxs-lookup"><span data-stu-id="88011-252">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="88011-253">italic</span><span class="sxs-lookup"><span data-stu-id="88011-253">italic</span></span> | <span data-ttu-id="88011-254">*text*</span><span class="sxs-lookup"><span data-stu-id="88011-254">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="88011-255">en-tête (&ndash;niveaux 1 à 3)</span><span class="sxs-lookup"><span data-stu-id="88011-255">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="88011-256">**Text**</span><span class="sxs-lookup"><span data-stu-id="88011-256">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="88011-257">doubles</span><span class="sxs-lookup"><span data-stu-id="88011-257">strikethrough</span></span> | <span data-ttu-id="88011-258">~~text~~</span><span class="sxs-lookup"><span data-stu-id="88011-258">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="88011-259">liste non triée</span><span class="sxs-lookup"><span data-stu-id="88011-259">unordered list</span></span> | <ul><li><span data-ttu-id="88011-260">text</span><span class="sxs-lookup"><span data-stu-id="88011-260">text</span></span></li><li><span data-ttu-id="88011-261">text</span><span class="sxs-lookup"><span data-stu-id="88011-261">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="88011-262">liste triée</span><span class="sxs-lookup"><span data-stu-id="88011-262">ordered list</span></span> | <ol><li><span data-ttu-id="88011-263">text</span><span class="sxs-lookup"><span data-stu-id="88011-263">text</span></span></li><li><span data-ttu-id="88011-264">text</span><span class="sxs-lookup"><span data-stu-id="88011-264">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="88011-265">texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="88011-265">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="88011-266">blockquote</span><span class="sxs-lookup"><span data-stu-id="88011-266">blockquote</span></span> | <blockquote><span data-ttu-id="88011-267">text</span><span class="sxs-lookup"><span data-stu-id="88011-267">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="88011-268">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="88011-268">hyperlink</span></span> | [<span data-ttu-id="88011-269">Bing</span><span class="sxs-lookup"><span data-stu-id="88011-269">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="88011-270">lien de l’image</span><span class="sxs-lookup"><span data-stu-id="88011-270">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="88011-271">Différences entre les appareils mobiles et de bureau pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="88011-271">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="88011-272">En raison des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de teams.</span><span class="sxs-lookup"><span data-stu-id="88011-272">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="88011-273">Sur le bureau, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-273">On the desktop, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client de bureau](/assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="88011-275">Sous iOS, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-275">On iOS, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client iOS](/assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="88011-277">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="88011-277">Issues:</span></span>

* <span data-ttu-id="88011-278">La mise en forme des caractères, comme gras et italique, n’est pas restituée sur iOS.</span><span class="sxs-lookup"><span data-stu-id="88011-278">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="88011-279">Sous Android, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88011-279">On Android, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client Android](/assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="88011-281">La mise en forme des caractères comme gras et italique s’affiche correctement sur Android.</span><span class="sxs-lookup"><span data-stu-id="88011-281">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="88011-282">Exemple de mise en forme pour la mise en forme HTML dans les cartes simples</span><span class="sxs-lookup"><span data-stu-id="88011-282">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="88011-283">Ces captures d’écran ont été créées à l’aide de teams AppStudio, où la propriété Text d’une carte héros a été définie sur la chaîne suivante.</span><span class="sxs-lookup"><span data-stu-id="88011-283">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="88011-284">Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.</span><span class="sxs-lookup"><span data-stu-id="88011-284">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
