---
title: Mise en forme de texte dans les cartes
description: Décrit la mise en forme de texte de carte dans Microsoft teams
keywords: format des cartes robots teams
ms.date: 03/29/2018
ms.openlocfilehash: 4a467c5b0b21cc3c19977bf7caa25e6790904b10
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673980"
---
# <a name="card-formatting"></a><span data-ttu-id="2ae3c-104">Mise en forme de carte</span><span class="sxs-lookup"><span data-stu-id="2ae3c-104">Card formatting</span></span>

<span data-ttu-id="2ae3c-105">Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de la démarque ou du code HTML, selon le type de carte.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-105">You can add rich text formatting to your cards using either markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="2ae3c-106">Les cartes prennent en charge la mise en forme uniquement dans la propriété Text, pas dans les propriétés Title ou title.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="2ae3c-107">La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de la mise en forme XML (HTML) ou de la démarque selon le type de carte.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="2ae3c-108">Pour les cartes adaptatives actuelles de développement à l’avenir, l’utilisation de la mise en forme de démarque est recommandée.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-108">For current amd future development Adaptive cards using markdown formatting is recommended.</span></span>

<span data-ttu-id="2ae3c-109">La prise en charge de la mise en forme diffère selon les types de carte et le rendu de la carte peut légèrement varier entre le bureau et les clients teams mobiles, ainsi que teams dans le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

## <a name="card-types"></a><span data-ttu-id="2ae3c-110">Types de carte</span><span class="sxs-lookup"><span data-stu-id="2ae3c-110">Card types</span></span>

<span data-ttu-id="2ae3c-111">Il existe trois types de cartes qui prennent en charge la démarque dans teams :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-111">There are three types of cards that support Markdown in Teams:</span></span>

* <span data-ttu-id="2ae3c-112">**Cartes adaptatives**: la démarque est prise en charge `Textblock` dans le champ carte adaptative `Fact.Title` , `Fact.Value`ainsi que et.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-112">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="2ae3c-113">HTML n’est pas pris en charge dans les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-113">HTML is not supported in adaptive cards.</span></span>
* <span data-ttu-id="2ae3c-114">**Cartes de connecteur O365**: la démarque et le code html limité sont pris en charge dans les cartes de connecteur Office 365 dans les champs de texte.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-114">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>
* <span data-ttu-id="2ae3c-115">**Cartes simples**: le code html limité est pris en charge, mais la démarque n’est pas prise en charge dans les cartes simples.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-115">**Simple Cards**: Limited HTML is supported, but markdown is not supported in simple cards.</span></span>

## <a name="markdown-formatting-for-adaptive-cards"></a><span data-ttu-id="2ae3c-116">Mise en forme des démarques pour cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ae3c-116">Markdown formatting for Adaptive Cards</span></span>

 <span data-ttu-id="2ae3c-117">Les styles pris en `Textblock`charge `Fact.Title` pour `Fact.Value` et sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-117">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="2ae3c-118">Style</span><span class="sxs-lookup"><span data-stu-id="2ae3c-118">Style</span></span> | <span data-ttu-id="2ae3c-119">Exemple</span><span class="sxs-lookup"><span data-stu-id="2ae3c-119">Example</span></span> | <span data-ttu-id="2ae3c-120">Markdown</span><span class="sxs-lookup"><span data-stu-id="2ae3c-120">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3c-121">bold</span><span class="sxs-lookup"><span data-stu-id="2ae3c-121">bold</span></span> | <span data-ttu-id="2ae3c-122">**Bold**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-122">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="2ae3c-123">italic</span><span class="sxs-lookup"><span data-stu-id="2ae3c-123">italic</span></span> | <span data-ttu-id="2ae3c-124">_Italic_</span><span class="sxs-lookup"><span data-stu-id="2ae3c-124">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="2ae3c-125">liste non triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-125">unordered list</span></span> | <ul><li><span data-ttu-id="2ae3c-126">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-126">text</span></span></li><li><span data-ttu-id="2ae3c-127">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-127">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="2ae3c-128">liste triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-128">ordered list</span></span> | <ol><li><span data-ttu-id="2ae3c-129">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-129">text</span></span></li><li><span data-ttu-id="2ae3c-130">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-130">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="2ae3c-131">Liens hypertexte</span><span class="sxs-lookup"><span data-stu-id="2ae3c-131">Hyperlinks</span></span> |[<span data-ttu-id="2ae3c-132">Bing</span><span class="sxs-lookup"><span data-stu-id="2ae3c-132">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="2ae3c-133">Les balises de démarques suivantes ne sont pas prises en charge :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-133">The following markdown tags are not supported:</span></span>

* <span data-ttu-id="2ae3c-134">En-têtes</span><span class="sxs-lookup"><span data-stu-id="2ae3c-134">Headers</span></span>
* <span data-ttu-id="2ae3c-135">Tables</span><span class="sxs-lookup"><span data-stu-id="2ae3c-135">Tables</span></span>
* <span data-ttu-id="2ae3c-136">Des images</span><span class="sxs-lookup"><span data-stu-id="2ae3c-136">Images</span></span>
* <span data-ttu-id="2ae3c-137">Texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="2ae3c-137">Preformatted text</span></span>
* <span data-ttu-id="2ae3c-138">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="2ae3c-138">Blockquotes</span></span>

<span data-ttu-id="2ae3c-139">Les cartes adaptatives ne prennent pas en charge la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-139">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="2ae3c-140">Nouvelles lignes de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ae3c-140">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="2ae3c-141">Dans les listes, vous pouvez `\r` utiliser `\n` les séquences d’échappement ou pour les nouvelles lignes.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-141">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="2ae3c-142">L' `\n\n` utilisation d’une liste entraîne le retrait de l’élément suivant dans la liste.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-142">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="2ae3c-143">Si vous avez besoin de nouvelles lignes ailleurs dans TextBlock `\n\n`, utilisez.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-143">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="2ae3c-144">Différences entre les appareils mobiles et de bureau pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ae3c-144">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="2ae3c-145">La mise en forme diffère légèrement entre le bureau et les versions mobiles de teams.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-145">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="2ae3c-146">Sur le bureau, le format des démarques de carte adaptative apparaît comme dans les navigateurs Web et dans l’application cliente teams :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-146">On the desktop, Adaptive Card markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Mise en forme adaptative de la démarque de carte dans le client de bureau](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="2ae3c-148">Sous iOS, la mise en forme adaptative de carte de visite apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-148">On iOS, Adaptive Card markdown formatting appears like this:</span></span>

![Mise en forme adaptative de la démarque de carte dans iOS](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="2ae3c-150">Sous Android, la mise en forme de la démarque de carte adaptative apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-150">On Android, Adaptive Card markdown formatting appears like this:</span></span>

![Mise en forme adaptative de la démarque de carte dans Android](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="2ae3c-152">Pour plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ae3c-152">For more information on Adaptive Cards</span></span>

<span data-ttu-id="2ae3c-153">[Fonctionnalités de texte dans des cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans cette rubrique ne sont pas prises en charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-153">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="2ae3c-154">Exemple de mise en forme des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ae3c-154">Formatting sample for Adaptive cards</span></span>

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
## <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="2ae3c-155">Mentionner la prise en charge dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ae3c-155">Mention support within Adaptive cards</span></span> 

> [!NOTE]
> <span data-ttu-id="2ae3c-156">Mentionner la prise en charge des cartes est actuellement prise en charge en version préliminaire pour les [développeurs](~/resources/dev-preview/developer-preview-intro) .</span><span class="sxs-lookup"><span data-stu-id="2ae3c-156">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro) only.</span></span>

<span data-ttu-id="2ae3c-157">Les robots et les extensions de messagerie peuvent désormais inclure des mentions dans le contenu des cartes dans les éléments bloc de texte et FactSet.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-157">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span> 

### <a name="constructing-mentions"></a><span data-ttu-id="2ae3c-158">Création de mentions</span><span class="sxs-lookup"><span data-stu-id="2ae3c-158">Constructing mentions</span></span>
<span data-ttu-id="2ae3c-159">Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants</span><span class="sxs-lookup"><span data-stu-id="2ae3c-159">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="2ae3c-160">`<at>username</at>`dans les éléments de carte adaptative pris en charge</span><span class="sxs-lookup"><span data-stu-id="2ae3c-160">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="2ae3c-161">`mention` Objet à l’intérieur d' `msteams` une propriété dans le contenu de la carte, qui inclut l’ID utilisateur teams de l’utilisateur mentionné</span><span class="sxs-lookup"><span data-stu-id="2ae3c-161">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="2ae3c-162">Notez que les cartes avec des mentions ne sont pas prises en charge sur les clients mobiles pour le moment.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-162">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="2ae3c-163">Exemple de carte adaptative avec une mention</span><span class="sxs-lookup"><span data-stu-id="2ae3c-163">Sample Adaptive card with a mention</span></span>
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

## <a name="html-formatting-for-connector-cards"></a><span data-ttu-id="2ae3c-164">Mise en forme HTML pour les cartes de connecteur</span><span class="sxs-lookup"><span data-stu-id="2ae3c-164">HTML formatting for Connector Cards</span></span>

<span data-ttu-id="2ae3c-165">Les cartes de connecteur prennent en charge la démarque limitée et la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-165">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="2ae3c-166">La démarque est décrite dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-166">Markdown is described in the next section.</span></span>

| <span data-ttu-id="2ae3c-167">Style</span><span class="sxs-lookup"><span data-stu-id="2ae3c-167">Style</span></span> | <span data-ttu-id="2ae3c-168">Exemple</span><span class="sxs-lookup"><span data-stu-id="2ae3c-168">Example</span></span> | <span data-ttu-id="2ae3c-169">HTML</span><span class="sxs-lookup"><span data-stu-id="2ae3c-169">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3c-170">bold</span><span class="sxs-lookup"><span data-stu-id="2ae3c-170">bold</span></span> | <span data-ttu-id="2ae3c-171">**text**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-171">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="2ae3c-172">italic</span><span class="sxs-lookup"><span data-stu-id="2ae3c-172">italic</span></span> | <span data-ttu-id="2ae3c-173">*text*</span><span class="sxs-lookup"><span data-stu-id="2ae3c-173">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="2ae3c-174">en-tête (&ndash;niveaux 1 à 3)</span><span class="sxs-lookup"><span data-stu-id="2ae3c-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="2ae3c-175">**Text**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-175">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="2ae3c-176">doubles</span><span class="sxs-lookup"><span data-stu-id="2ae3c-176">strikethrough</span></span> | <span data-ttu-id="2ae3c-177">~~text~~</span><span class="sxs-lookup"><span data-stu-id="2ae3c-177">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="2ae3c-178">liste non triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-178">unordered list</span></span> | <ul><li><span data-ttu-id="2ae3c-179">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-179">text</span></span></li><li><span data-ttu-id="2ae3c-180">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-180">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="2ae3c-181">liste triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-181">ordered list</span></span> | <ol><li><span data-ttu-id="2ae3c-182">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-182">text</span></span></li><li><span data-ttu-id="2ae3c-183">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-183">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="2ae3c-184">texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="2ae3c-184">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="2ae3c-185">blockquote</span><span class="sxs-lookup"><span data-stu-id="2ae3c-185">blockquote</span></span> | <blockquote><span data-ttu-id="2ae3c-186">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-186">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="2ae3c-187">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="2ae3c-187">hyperlink</span></span> | [<span data-ttu-id="2ae3c-188">Bing</span><span class="sxs-lookup"><span data-stu-id="2ae3c-188">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="2ae3c-189">lien de l’image</span><span class="sxs-lookup"><span data-stu-id="2ae3c-189">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="2ae3c-190">Dans les cartes de connecteur, les nouvelles lignes sont affichées `<p>` en HTML à l’aide de la balise.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-190">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="2ae3c-191">Différences entre les appareils mobiles et de bureau pour les cartes de connecteur à l’aide de HTML</span><span class="sxs-lookup"><span data-stu-id="2ae3c-191">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="2ae3c-192">Sur le bureau, la mise en forme HTML des cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-192">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](~/assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="2ae3c-194">Sur iOS, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-194">On iOS, HTML formatting looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](~/assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="2ae3c-196">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-196">Issues:</span></span>

* <span data-ttu-id="2ae3c-197">Les images en ligne ne sont pas rendues sur iOS à l’aide de la démarque ou du code HTML dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-197">Inline images are not rendered on iOS using either markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="2ae3c-198">Le texte préformaté est affiché, mais il n’a pas d’arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-198">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="2ae3c-199">Sur Android, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-199">On Android, HTML formatting looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client Android](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="2ae3c-201">Exemple de mise en forme des cartes de connecteur HTML</span><span class="sxs-lookup"><span data-stu-id="2ae3c-201">Formatting sample for HTML Connector Cards</span></span>

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

## <a name="markdown-formatting-for-connector-cards"></a><span data-ttu-id="2ae3c-202">Mise en forme des démarques pour les cartes de connecteur</span><span class="sxs-lookup"><span data-stu-id="2ae3c-202">Markdown formatting for Connector Cards</span></span>

<span data-ttu-id="2ae3c-203">Les cartes de connecteur prennent en charge la démarque limitée et la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-203">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="2ae3c-204">Le code HTML est décrit dans la dernière section.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-204">HTML is described in the last section.</span></span>

| <span data-ttu-id="2ae3c-205">Style</span><span class="sxs-lookup"><span data-stu-id="2ae3c-205">Style</span></span> | <span data-ttu-id="2ae3c-206">Exemple</span><span class="sxs-lookup"><span data-stu-id="2ae3c-206">Example</span></span> | <span data-ttu-id="2ae3c-207">Markdown</span><span class="sxs-lookup"><span data-stu-id="2ae3c-207">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3c-208">bold</span><span class="sxs-lookup"><span data-stu-id="2ae3c-208">bold</span></span> | <span data-ttu-id="2ae3c-209">**text**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-209">**text**</span></span> | `**text**` |
| <span data-ttu-id="2ae3c-210">italic</span><span class="sxs-lookup"><span data-stu-id="2ae3c-210">italic</span></span> | <span data-ttu-id="2ae3c-211">*text*</span><span class="sxs-lookup"><span data-stu-id="2ae3c-211">*text*</span></span> | `*text*` |
| <span data-ttu-id="2ae3c-212">en-tête (&ndash;niveaux 1 à 3)</span><span class="sxs-lookup"><span data-stu-id="2ae3c-212">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="2ae3c-213">**Text**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-213">**Text**</span></span> | `### Text`|
| <span data-ttu-id="2ae3c-214">doubles</span><span class="sxs-lookup"><span data-stu-id="2ae3c-214">strikethrough</span></span> | <span data-ttu-id="2ae3c-215">~~text~~</span><span class="sxs-lookup"><span data-stu-id="2ae3c-215">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="2ae3c-216">liste non triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-216">unordered list</span></span> | <ul><li><span data-ttu-id="2ae3c-217">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-217">text</span></span></li><li><span data-ttu-id="2ae3c-218">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-218">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="2ae3c-219">liste triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-219">ordered list</span></span> | <ol><li><span data-ttu-id="2ae3c-220">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-220">text</span></span></li><li><span data-ttu-id="2ae3c-221">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-221">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="2ae3c-222">texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="2ae3c-222">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="2ae3c-223">blockquote</span><span class="sxs-lookup"><span data-stu-id="2ae3c-223">blockquote</span></span> | <span data-ttu-id="2ae3c-224">Texte >BLOCKQUOTE</span><span class="sxs-lookup"><span data-stu-id="2ae3c-224">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="2ae3c-225">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="2ae3c-225">hyperlink</span></span> | [<span data-ttu-id="2ae3c-226">Bing</span><span class="sxs-lookup"><span data-stu-id="2ae3c-226">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="2ae3c-227">lien de l’image</span><span class="sxs-lookup"><span data-stu-id="2ae3c-227">image link</span></span> |![Canard sur une roche](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="2ae3c-229">Dans les cartes de connecteur, les nouvelles `\n\n`lignes sont affichées pour `\n` , `\r`mais pas pour ou.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-229">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="2ae3c-230">Différences de bureau et de téléphone pour les cartes de connecteur utilisant la démarque</span><span class="sxs-lookup"><span data-stu-id="2ae3c-230">Mobile and desktop differences for connector cards using markdown</span></span>

<span data-ttu-id="2ae3c-231">Sur le bureau, la mise en forme de démarque pour les cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-231">On the desktop, markdown formatting for connector cards looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](~/assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="2ae3c-233">Sur iOS, la mise en forme de démarque pour les cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-233">On iOS, markdown formatting for connector cards looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="2ae3c-235">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-235">Issues:</span></span>

* <span data-ttu-id="2ae3c-236">Le client iOS pour Teams ne restitue pas les images insérées de démarque ou HTML dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-236">The iOS client for Teams does not render markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="2ae3c-237">Les blockquotes sont affichés sous forme de retrait, mais sans arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-237">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="2ae3c-238">Sur Android, la mise en forme des démarques pour les cartes de connecteur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-238">On Android, markdown formatting for connector cards looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client Android](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="2ae3c-240">Exemple de mise en forme pour les fiches de connecteur de démarque</span><span class="sxs-lookup"><span data-stu-id="2ae3c-240">Formatting example for markdown Connector Cards</span></span>

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

## <a name="html-formatting-for-simple-cards"></a><span data-ttu-id="2ae3c-241">Mise en forme HTML pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="2ae3c-241">HTML Formatting for simple cards</span></span>

<span data-ttu-id="2ae3c-242">Ces balises HTML sont prises en charge pour les cartes simples telles que le héros et la carte miniature.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-242">These HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="2ae3c-243">La démarque n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-243">Markdown is not supported.</span></span>

| <span data-ttu-id="2ae3c-244">Style</span><span class="sxs-lookup"><span data-stu-id="2ae3c-244">Style</span></span> | <span data-ttu-id="2ae3c-245">Exemple</span><span class="sxs-lookup"><span data-stu-id="2ae3c-245">Example</span></span> | <span data-ttu-id="2ae3c-246">HTML</span><span class="sxs-lookup"><span data-stu-id="2ae3c-246">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3c-247">bold</span><span class="sxs-lookup"><span data-stu-id="2ae3c-247">bold</span></span> | <span data-ttu-id="2ae3c-248">**text**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-248">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="2ae3c-249">italic</span><span class="sxs-lookup"><span data-stu-id="2ae3c-249">italic</span></span> | <span data-ttu-id="2ae3c-250">*text*</span><span class="sxs-lookup"><span data-stu-id="2ae3c-250">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="2ae3c-251">en-tête (&ndash;niveaux 1 à 3)</span><span class="sxs-lookup"><span data-stu-id="2ae3c-251">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="2ae3c-252">**Text**</span><span class="sxs-lookup"><span data-stu-id="2ae3c-252">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="2ae3c-253">doubles</span><span class="sxs-lookup"><span data-stu-id="2ae3c-253">strikethrough</span></span> | <span data-ttu-id="2ae3c-254">~~text~~</span><span class="sxs-lookup"><span data-stu-id="2ae3c-254">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="2ae3c-255">liste non triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-255">unordered list</span></span> | <ul><li><span data-ttu-id="2ae3c-256">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-256">text</span></span></li><li><span data-ttu-id="2ae3c-257">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-257">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="2ae3c-258">liste triée</span><span class="sxs-lookup"><span data-stu-id="2ae3c-258">ordered list</span></span> | <ol><li><span data-ttu-id="2ae3c-259">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-259">text</span></span></li><li><span data-ttu-id="2ae3c-260">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-260">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="2ae3c-261">texte déjà mis en forme</span><span class="sxs-lookup"><span data-stu-id="2ae3c-261">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="2ae3c-262">blockquote</span><span class="sxs-lookup"><span data-stu-id="2ae3c-262">blockquote</span></span> | <blockquote><span data-ttu-id="2ae3c-263">text</span><span class="sxs-lookup"><span data-stu-id="2ae3c-263">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="2ae3c-264">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="2ae3c-264">hyperlink</span></span> | [<span data-ttu-id="2ae3c-265">Bing</span><span class="sxs-lookup"><span data-stu-id="2ae3c-265">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="2ae3c-266">lien de l’image</span><span class="sxs-lookup"><span data-stu-id="2ae3c-266">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="2ae3c-267">Différences entre les appareils mobiles et de bureau pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="2ae3c-267">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="2ae3c-268">En raison des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de teams.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-268">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="2ae3c-269">Sur le bureau, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-269">On the desktop, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client de bureau](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="2ae3c-271">Sous iOS, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-271">On iOS, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client iOS](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="2ae3c-273">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-273">Issues:</span></span>

* <span data-ttu-id="2ae3c-274">La mise en forme des caractères, comme gras et italique, n’est pas restituée sur iOS.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-274">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="2ae3c-275">Sous Android, la mise en forme HTML se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ae3c-275">On Android, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client Android](~/assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="2ae3c-277">La mise en forme des caractères comme gras et italique s’affiche correctement sur Android.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-277">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="2ae3c-278">Exemple de mise en forme pour la mise en forme HTML dans les cartes simples</span><span class="sxs-lookup"><span data-stu-id="2ae3c-278">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="2ae3c-279">Ces captures d’écran ont été créées à l’aide de teams AppStudio, où la propriété Text d’une carte héros a été définie sur la chaîne suivante.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-279">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="2ae3c-280">Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.</span><span class="sxs-lookup"><span data-stu-id="2ae3c-280">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
