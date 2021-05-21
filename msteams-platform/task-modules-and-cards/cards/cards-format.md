---
title: Mise en forme du texte dans les cartes
description: Décrit la mise en forme du texte de la carte Microsoft Teams
keywords: Format de cartes de bots teams
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 848656097f2c865705cc0d91dece93049d8c6790
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566580"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="88efb-104">Formater des cartes dans Teams</span><span class="sxs-lookup"><span data-stu-id="88efb-104">Format cards in Teams</span></span>

<span data-ttu-id="88efb-105">Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de Markdown ou html, en fonction du type de carte.</span><span class="sxs-lookup"><span data-stu-id="88efb-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="88efb-106">Les cartes ne supportent la mise en forme que dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre.</span><span class="sxs-lookup"><span data-stu-id="88efb-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="88efb-107">La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de mise en forme XML (HTML) ou markdown en fonction du type de carte.</span><span class="sxs-lookup"><span data-stu-id="88efb-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="88efb-108">Pour le développement actuel et le développement de cartes adaptatives utilisant la mise en forme Markdown est recommandé.</span><span class="sxs-lookup"><span data-stu-id="88efb-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="88efb-109">La prise en charge de la mise en forme diffère d’un type de carte à l’autre, et le rendu de la carte peut légèrement varier entre les clients de bureau et de Teams mobiles, ainsi que les Teams dans le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="88efb-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="88efb-110">Vous pouvez inclure une image inline avec n’importe Teams carte.</span><span class="sxs-lookup"><span data-stu-id="88efb-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="88efb-111">Images au format , ou fichiers, qui ne doivent pas dépasser  `.png` `.jpg` `.gif` 1 024 × 1 024 px ou 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="88efb-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="88efb-112">L’image GIF animée n’est pas officiellement prise en charge.</span><span class="sxs-lookup"><span data-stu-id="88efb-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="88efb-113">Pour plus d’informations, consultez la référence [des cartes.](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="88efb-113">For more information, see [Cards reference](./cards-reference.md#inline-card-images).</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="88efb-114">Mise en forme de cartes avec Markdown</span><span class="sxs-lookup"><span data-stu-id="88efb-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="88efb-115">Il existe deux types de cartes qui prisent en charge Markdown dans Teams :</span><span class="sxs-lookup"><span data-stu-id="88efb-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88efb-116">**Cartes adaptatives**: Markdown est pris en charge dans le champ de carte `Textblock` adaptative, ainsi que dans `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="88efb-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="88efb-117">Le code HTML n’est pas pris en charge dans les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="88efb-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="88efb-118">**Cartes de connecteur O365**: markdown et html limité sont pris en charge dans les cartes Office 365 connecteur dans les champs de texte.</span><span class="sxs-lookup"><span data-stu-id="88efb-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="88efb-119">**Mise en forme Markdown : cartes adaptatives**</span><span class="sxs-lookup"><span data-stu-id="88efb-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="88efb-120">Les styles pris en charge `Textblock` pour et `Fact.Title` sont `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="88efb-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="88efb-121">Style</span><span class="sxs-lookup"><span data-stu-id="88efb-121">Style</span></span> | <span data-ttu-id="88efb-122">Exemple</span><span class="sxs-lookup"><span data-stu-id="88efb-122">Example</span></span> | <span data-ttu-id="88efb-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="88efb-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88efb-124">bold</span><span class="sxs-lookup"><span data-stu-id="88efb-124">bold</span></span> | <span data-ttu-id="88efb-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="88efb-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="88efb-126">italic</span><span class="sxs-lookup"><span data-stu-id="88efb-126">italic</span></span> | <span data-ttu-id="88efb-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="88efb-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="88efb-128">liste non réordée</span><span class="sxs-lookup"><span data-stu-id="88efb-128">unordered list</span></span> | <ul><li><span data-ttu-id="88efb-129">text</span><span class="sxs-lookup"><span data-stu-id="88efb-129">text</span></span></li><li><span data-ttu-id="88efb-130">text</span><span class="sxs-lookup"><span data-stu-id="88efb-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="88efb-131">liste ordered</span><span class="sxs-lookup"><span data-stu-id="88efb-131">ordered list</span></span> | <ol><li><span data-ttu-id="88efb-132">text</span><span class="sxs-lookup"><span data-stu-id="88efb-132">text</span></span></li><li><span data-ttu-id="88efb-133">text</span><span class="sxs-lookup"><span data-stu-id="88efb-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="88efb-134">Liens hypertexte</span><span class="sxs-lookup"><span data-stu-id="88efb-134">Hyperlinks</span></span> |[<span data-ttu-id="88efb-135">Bing</span><span class="sxs-lookup"><span data-stu-id="88efb-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="88efb-136">Les balises Markdown suivantes ne sont pas pris en charge :</span><span class="sxs-lookup"><span data-stu-id="88efb-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="88efb-137">En-têtes</span><span class="sxs-lookup"><span data-stu-id="88efb-137">Headers</span></span>
* <span data-ttu-id="88efb-138">Tables</span><span class="sxs-lookup"><span data-stu-id="88efb-138">Tables</span></span>
* <span data-ttu-id="88efb-139">Des images</span><span class="sxs-lookup"><span data-stu-id="88efb-139">Images</span></span>
* <span data-ttu-id="88efb-140">Texte préformaté</span><span class="sxs-lookup"><span data-stu-id="88efb-140">Preformatted text</span></span>
* <span data-ttu-id="88efb-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="88efb-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88efb-142">Les cartes adaptatives ne sont pas adaptées à la mise en forme HTML.</span><span class="sxs-lookup"><span data-stu-id="88efb-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="88efb-143">Nouvelles lignes pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="88efb-144">Dans les listes, vous pouvez utiliser les `\r` `\n` séquences d’échappatoire pour les nouvelles lignes.</span><span class="sxs-lookup"><span data-stu-id="88efb-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="88efb-145">L’utilisation dans une liste entraîne le retrait de l’élément suivant de `\n\n` la liste.</span><span class="sxs-lookup"><span data-stu-id="88efb-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="88efb-146">Si vous avez besoin de nouvelles lignes ailleurs dans le textblock, utilisez `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="88efb-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="88efb-147">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="88efb-148">La mise en forme est légèrement différente entre le bureau et les versions mobiles de Teams.</span><span class="sxs-lookup"><span data-stu-id="88efb-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="88efb-149">Sur le bureau, la mise en forme Markdown de carte adaptative s’affiche comme ceci dans les navigateurs web et dans Teams application cliente :</span><span class="sxs-lookup"><span data-stu-id="88efb-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Mise en forme Markdown de carte adaptative dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="88efb-151">Sur iOS, la mise en forme Markdown de carte adaptative s’affiche comme ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Mise en forme Markdown de carte adaptative dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="88efb-153">Sur Android, la mise en forme Markdown de carte adaptative s’affiche comme ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Mise en forme Markdown de carte adaptative dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="88efb-155">Plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-155">More information on Adaptive cards</span></span>

<span data-ttu-id="88efb-156">[Fonctionnalités de texte dans les cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans cette rubrique ne sont pas Teams.</span><span class="sxs-lookup"><span data-stu-id="88efb-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="88efb-157">Exemple de mise en forme pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="88efb-158">Prise en charge des mentions dans les cartes adaptatives v1.2</span><span class="sxs-lookup"><span data-stu-id="88efb-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="88efb-159">Les mentions basées sur la carte sont pris en charge dans les clients web, de bureau et mobiles.</span><span class="sxs-lookup"><span data-stu-id="88efb-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="88efb-160">Vous pouvez ajouter des mentions @ dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="88efb-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="88efb-161">Pour ajouter des mentions @ dans les cartes, suivez la même logique de notification et le même rendu que celui des [mentions basées](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)sur les messages dans les conversations de canal et de groupe.</span><span class="sxs-lookup"><span data-stu-id="88efb-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="88efb-162">Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la carte dans les éléments [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="88efb-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="88efb-163">[Les éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptatives v1.2 sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="88efb-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="88efb-164">Les mentions &'équipe de canal ne sont pas pris en charge dans les messages de bot.</span><span class="sxs-lookup"><span data-stu-id="88efb-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="88efb-165">Construction de mentions</span><span class="sxs-lookup"><span data-stu-id="88efb-165">Constructing mentions</span></span>

<span data-ttu-id="88efb-166">Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="88efb-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="88efb-167">`<at>username</at>` dans les éléments de carte adaptative pris en charge.</span><span class="sxs-lookup"><span data-stu-id="88efb-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="88efb-168">Objet à l’intérieur d’une propriété dans le contenu de la carte, qui inclut `mention` l’ID Teams’utilisateur de l’utilisateur `msteams` mentionné.</span><span class="sxs-lookup"><span data-stu-id="88efb-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="88efb-169">Il `userId` est propre à votre ID de bot et à un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="88efb-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="88efb-170">Il peut être utilisé pour @mention un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="88efb-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="88efb-171">Il `userId` peut être récupéré à l’aide de l’une des options mentionnées dans obtenir [l’ID utilisateur.](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)</span><span class="sxs-lookup"><span data-stu-id="88efb-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="88efb-172">Exemple de carte adaptative avec une mention</span><span class="sxs-lookup"><span data-stu-id="88efb-172">Sample Adaptive card with a mention</span></span>

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
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="88efb-173">Masquage d’informations dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="88efb-174">Utilisez la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs au sein de l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="88efb-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="88efb-175">La fonctionnalité prend uniquement en charge le masquage d’informations côté client, le texte d’entrée masqué est envoyé en tant que texte clair à l’adresse de point de terminaison https spécifiée lors de la [configuration du bot.](../../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="88efb-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="88efb-176">La propriété de masquage d’informations est actuellement disponible dans l’aperçu développeur uniquement.</span><span class="sxs-lookup"><span data-stu-id="88efb-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="88efb-177">Pour masquer les informations dans les cartes adaptatives, ajoutez la propriété à taper et définissez `isMasked` sa valeur sur  `Input.Text` *true*.</span><span class="sxs-lookup"><span data-stu-id="88efb-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="88efb-178">Exemple de carte adaptative avec propriété de masquage</span><span class="sxs-lookup"><span data-stu-id="88efb-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="88efb-179">L’image suivante est un exemple de masquage d’informations dans les cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="88efb-179">The following image is an example of masking information in Adaptive cards:</span></span>

![Image d’informations de masquage](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="88efb-181">Carte adaptative pleine largeur</span><span class="sxs-lookup"><span data-stu-id="88efb-181">Full width Adaptive card</span></span>
<span data-ttu-id="88efb-182">Vous pouvez utiliser la propriété pour développer la largeur d’une carte adaptative et `msteams` utiliser de l’espace de dessin supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="88efb-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="88efb-183">Pour plus d’informations sur l’utilisation de la propriété, voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="88efb-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="88efb-184">Construction de cartes pleine largeur</span><span class="sxs-lookup"><span data-stu-id="88efb-184">Constructing full width cards</span></span>
<span data-ttu-id="88efb-185">Pour créer une carte adaptative pleine largeur, l’objet dans la propriété dans le contenu de la carte `width` doit être définie sur `msteams` `Full` .</span><span class="sxs-lookup"><span data-stu-id="88efb-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="88efb-186">En outre, votre application doit inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="88efb-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="88efb-187">Exemple de carte adaptative avec pleine largeur</span><span class="sxs-lookup"><span data-stu-id="88efb-187">Sample adaptive card with full width</span></span>

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="88efb-188">Une carte adaptative pleine largeur apparaît comme suit : affichage Carte ![ adaptative pleine largeur](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="88efb-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="88efb-189">Si vous n’avez pas donné la valeur Full à la propriété, l’affichage par défaut de la carte adaptative est le suivant : affichage Carte adaptative à petite `width`  ![ largeur](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="88efb-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="88efb-190">Prise en charge de Typeahead</span><span class="sxs-lookup"><span data-stu-id="88efb-190">Typeahead support</span></span>

<span data-ttu-id="88efb-191">Dans l’élément de schéma, le fait de demander aux utilisateurs de filtrer et de sélectionner un nombre important de choix peut ralentir considérablement l’exécution [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de la tâche.</span><span class="sxs-lookup"><span data-stu-id="88efb-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="88efb-192">La prise en charge de la tête de type dans les cartes adaptatives peut simplifier la sélection des entrées en axant ou en filtrant l’ensemble des choix d’entrée quand un utilisateur tape l’entrée.</span><span class="sxs-lookup"><span data-stu-id="88efb-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="88efb-193">Activer typeahead dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="88efb-194">Pour activer la tête de type dans `Input.Choiceset` l’ensemble `style` et `filtered` vérifier `isMultiSelect` qu’elle est définie sur `false` .</span><span class="sxs-lookup"><span data-stu-id="88efb-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="88efb-195">Exemple de carte adaptative avec prise en charge de typeahead</span><span class="sxs-lookup"><span data-stu-id="88efb-195">Sample adaptive card with typeahead support</span></span>

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="88efb-196">Vue d’étape des images dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="88efb-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="88efb-197">Cette fonctionnalité est actuellement disponible en prévisualisation pour les développeurs uniquement.</span><span class="sxs-lookup"><span data-stu-id="88efb-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="88efb-198">Dans une carte adaptative, vous pouvez utiliser la propriété pour ajouter la possibilité d’afficher des images en vue de la `msteams` scène de manière sélective.</span><span class="sxs-lookup"><span data-stu-id="88efb-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="88efb-199">Lorsque les utilisateurs pointent sur les images, ils voient une icône développer, pour laquelle l’attribut `allowExpand` est définie sur `true` .</span><span class="sxs-lookup"><span data-stu-id="88efb-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="88efb-200">Pour plus d’informations sur l’utilisation de la propriété, voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="88efb-200">For information on how to use the property, see the following example:</span></span>

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="88efb-201">Lorsque les utilisateurs pointent sur l’image, une icône développer s’affiche dans le coin supérieur droit de l’image : carte ![ adaptative avec image expandable](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="88efb-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="88efb-202">L’image s’affiche en vue de la phase lorsque l’utilisateur sélectionne le bouton Développer : ![ Image étendue en vue de la phase](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="88efb-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="88efb-203">Dans la vue d’étape, les utilisateurs peuvent effectuer un zoom avant et un zoom arrière sur l’image.</span><span class="sxs-lookup"><span data-stu-id="88efb-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="88efb-204">Vous pouvez sélectionner les images de votre carte adaptative qui doivent avoir cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="88efb-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="88efb-205">Les fonctionnalités de zoom avant et arrière s’appliquent uniquement aux éléments image (type d’image) dans une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="88efb-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="88efb-206">Pour les applications mobiles Teams, les fonctionnalités d’affichage de scène pour les images dans les cartes adaptatives sont disponibles par défaut et les utilisateurs peuvent afficher des images de carte adaptative en mode étape en appuyant simplement sur l’image, que l’attribut soit présent ou `allowExpand` non.</span><span class="sxs-lookup"><span data-stu-id="88efb-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="88efb-207">**Mise en forme Markdown : cartes de connecteur O365**</span><span class="sxs-lookup"><span data-stu-id="88efb-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="88efb-208">Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="88efb-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="88efb-209">La prise en charge HTML est décrite dans la dernière section.</span><span class="sxs-lookup"><span data-stu-id="88efb-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="88efb-210">Style</span><span class="sxs-lookup"><span data-stu-id="88efb-210">Style</span></span> | <span data-ttu-id="88efb-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="88efb-211">Example</span></span> | <span data-ttu-id="88efb-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="88efb-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88efb-213">bold</span><span class="sxs-lookup"><span data-stu-id="88efb-213">bold</span></span> | <span data-ttu-id="88efb-214">**text**</span><span class="sxs-lookup"><span data-stu-id="88efb-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="88efb-215">italic</span><span class="sxs-lookup"><span data-stu-id="88efb-215">italic</span></span> | <span data-ttu-id="88efb-216">*text*</span><span class="sxs-lookup"><span data-stu-id="88efb-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="88efb-217">en-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="88efb-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="88efb-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="88efb-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="88efb-219">strikethrough</span><span class="sxs-lookup"><span data-stu-id="88efb-219">strikethrough</span></span> | <span data-ttu-id="88efb-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="88efb-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="88efb-221">liste non réordée</span><span class="sxs-lookup"><span data-stu-id="88efb-221">unordered list</span></span> | <ul><li><span data-ttu-id="88efb-222">text</span><span class="sxs-lookup"><span data-stu-id="88efb-222">text</span></span></li><li><span data-ttu-id="88efb-223">text</span><span class="sxs-lookup"><span data-stu-id="88efb-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="88efb-224">liste ordered</span><span class="sxs-lookup"><span data-stu-id="88efb-224">ordered list</span></span> | <ol><li><span data-ttu-id="88efb-225">text</span><span class="sxs-lookup"><span data-stu-id="88efb-225">text</span></span></li><li><span data-ttu-id="88efb-226">text</span><span class="sxs-lookup"><span data-stu-id="88efb-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="88efb-227">texte préformaté</span><span class="sxs-lookup"><span data-stu-id="88efb-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="88efb-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="88efb-228">blockquote</span></span> | <span data-ttu-id="88efb-229">>blockquote</span><span class="sxs-lookup"><span data-stu-id="88efb-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="88efb-230">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="88efb-230">hyperlink</span></span> | [<span data-ttu-id="88efb-231">Bing</span><span class="sxs-lookup"><span data-stu-id="88efb-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="88efb-232">lien vers l’image</span><span class="sxs-lookup"><span data-stu-id="88efb-232">image link</span></span> |![Canet sur une bascule](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="88efb-234">Dans les cartes de connecteur, les nouvelles lignes sont restituer `\n\n` pour , mais pas pour ou `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="88efb-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="88efb-235">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur à l’aide de Markdown</span><span class="sxs-lookup"><span data-stu-id="88efb-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="88efb-236">Sur le bureau, la mise en forme Markdown pour les cartes de connecteur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="88efb-238">Sur iOS, la mise en forme Markdown pour les cartes de connecteur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="88efb-240">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="88efb-240">Issues:</span></span>

* <span data-ttu-id="88efb-241">Le client iOS pour Teams ne restituera pas les images en ligne Markdown ou HTML dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="88efb-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="88efb-242">Les blockquotes sont restituer en retrait, mais sans arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="88efb-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="88efb-243">Sur Android, la mise en forme Markdown pour les cartes de connecteur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="88efb-245">Exemple de mise en forme pour les cartes de connecteur Markdown</span><span class="sxs-lookup"><span data-stu-id="88efb-245">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="88efb-246">Mise en forme de cartes au format HTML</span><span class="sxs-lookup"><span data-stu-id="88efb-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="88efb-247">**Mise en forme HTML : cartes de connecteur O365**</span><span class="sxs-lookup"><span data-stu-id="88efb-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="88efb-248">Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="88efb-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="88efb-249">Markdown est décrit dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="88efb-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="88efb-250">Style</span><span class="sxs-lookup"><span data-stu-id="88efb-250">Style</span></span> | <span data-ttu-id="88efb-251">Exemple</span><span class="sxs-lookup"><span data-stu-id="88efb-251">Example</span></span> | <span data-ttu-id="88efb-252">HTML</span><span class="sxs-lookup"><span data-stu-id="88efb-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88efb-253">bold</span><span class="sxs-lookup"><span data-stu-id="88efb-253">bold</span></span> | <span data-ttu-id="88efb-254">**text**</span><span class="sxs-lookup"><span data-stu-id="88efb-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="88efb-255">italic</span><span class="sxs-lookup"><span data-stu-id="88efb-255">italic</span></span> | <span data-ttu-id="88efb-256">*text*</span><span class="sxs-lookup"><span data-stu-id="88efb-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="88efb-257">en-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="88efb-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="88efb-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="88efb-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="88efb-259">strikethrough</span><span class="sxs-lookup"><span data-stu-id="88efb-259">strikethrough</span></span> | <span data-ttu-id="88efb-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="88efb-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="88efb-261">liste non réordée</span><span class="sxs-lookup"><span data-stu-id="88efb-261">unordered list</span></span> | <ul><li><span data-ttu-id="88efb-262">text</span><span class="sxs-lookup"><span data-stu-id="88efb-262">text</span></span></li><li><span data-ttu-id="88efb-263">text</span><span class="sxs-lookup"><span data-stu-id="88efb-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="88efb-264">liste ordered</span><span class="sxs-lookup"><span data-stu-id="88efb-264">ordered list</span></span> | <ol><li><span data-ttu-id="88efb-265">text</span><span class="sxs-lookup"><span data-stu-id="88efb-265">text</span></span></li><li><span data-ttu-id="88efb-266">text</span><span class="sxs-lookup"><span data-stu-id="88efb-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="88efb-267">texte préformaté</span><span class="sxs-lookup"><span data-stu-id="88efb-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="88efb-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="88efb-268">blockquote</span></span> | <blockquote><span data-ttu-id="88efb-269">text</span><span class="sxs-lookup"><span data-stu-id="88efb-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="88efb-270">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="88efb-270">hyperlink</span></span> | [<span data-ttu-id="88efb-271">Bing</span><span class="sxs-lookup"><span data-stu-id="88efb-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="88efb-272">lien vers l’image</span><span class="sxs-lookup"><span data-stu-id="88efb-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="88efb-273">Dans les cartes de connecteur, les nouvelles lignes sont restituer au format HTML à l’aide de la `<p>` balise.</span><span class="sxs-lookup"><span data-stu-id="88efb-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="88efb-274">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur utilisant du code HTML</span><span class="sxs-lookup"><span data-stu-id="88efb-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="88efb-275">Sur le bureau, la mise en forme HTML pour les cartes de connecteur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="88efb-277">Sur iOS, la mise en forme HTML ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-277">On iOS, HTML formatting looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="88efb-279">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="88efb-279">Issues:</span></span>

* <span data-ttu-id="88efb-280">Les images en ligne ne sont pas restituer sur iOS à l’aide de Markdown ou html dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="88efb-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="88efb-281">Le texte préformaté est restituer, mais n’a pas d’arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="88efb-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="88efb-282">Sur Android, la mise en forme HTML ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-282">On Android, HTML formatting looks like this:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="88efb-284">Exemple de mise en forme pour les cartes de connecteur HTML</span><span class="sxs-lookup"><span data-stu-id="88efb-284">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
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
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="88efb-285">**Mise en forme HTML : cartes hero et miniatures**</span><span class="sxs-lookup"><span data-stu-id="88efb-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="88efb-286">Les balises HTML sont pris en charge pour les cartes simples telles que la carte hero et la carte miniature.</span><span class="sxs-lookup"><span data-stu-id="88efb-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="88efb-287">Markdown n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="88efb-287">Markdown is not supported.</span></span>

| <span data-ttu-id="88efb-288">Style</span><span class="sxs-lookup"><span data-stu-id="88efb-288">Style</span></span> | <span data-ttu-id="88efb-289">Exemple</span><span class="sxs-lookup"><span data-stu-id="88efb-289">Example</span></span> | <span data-ttu-id="88efb-290">HTML</span><span class="sxs-lookup"><span data-stu-id="88efb-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88efb-291">bold</span><span class="sxs-lookup"><span data-stu-id="88efb-291">bold</span></span> | <span data-ttu-id="88efb-292">**text**</span><span class="sxs-lookup"><span data-stu-id="88efb-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="88efb-293">italic</span><span class="sxs-lookup"><span data-stu-id="88efb-293">italic</span></span> | <span data-ttu-id="88efb-294">*text*</span><span class="sxs-lookup"><span data-stu-id="88efb-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="88efb-295">en-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="88efb-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="88efb-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="88efb-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="88efb-297">strikethrough</span><span class="sxs-lookup"><span data-stu-id="88efb-297">strikethrough</span></span> | <span data-ttu-id="88efb-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="88efb-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="88efb-299">liste non réordée</span><span class="sxs-lookup"><span data-stu-id="88efb-299">unordered list</span></span> | <ul><li><span data-ttu-id="88efb-300">text</span><span class="sxs-lookup"><span data-stu-id="88efb-300">text</span></span></li><li><span data-ttu-id="88efb-301">text</span><span class="sxs-lookup"><span data-stu-id="88efb-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="88efb-302">liste ordered</span><span class="sxs-lookup"><span data-stu-id="88efb-302">ordered list</span></span> | <ol><li><span data-ttu-id="88efb-303">text</span><span class="sxs-lookup"><span data-stu-id="88efb-303">text</span></span></li><li><span data-ttu-id="88efb-304">text</span><span class="sxs-lookup"><span data-stu-id="88efb-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="88efb-305">texte préformaté</span><span class="sxs-lookup"><span data-stu-id="88efb-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="88efb-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="88efb-306">blockquote</span></span> | <blockquote><span data-ttu-id="88efb-307">text</span><span class="sxs-lookup"><span data-stu-id="88efb-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="88efb-308">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="88efb-308">hyperlink</span></span> | [<span data-ttu-id="88efb-309">Bing</span><span class="sxs-lookup"><span data-stu-id="88efb-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="88efb-310">lien vers l’image</span><span class="sxs-lookup"><span data-stu-id="88efb-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="88efb-311">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="88efb-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="88efb-312">En raison des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de Teams.</span><span class="sxs-lookup"><span data-stu-id="88efb-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="88efb-313">Sur le bureau, la mise en forme HTML s’affiche comme ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-313">On the desktop, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client de bureau](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="88efb-315">Sur iOS, la mise en forme HTML s’affiche comme ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-315">On iOS, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="88efb-317">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="88efb-317">Issues:</span></span>

* <span data-ttu-id="88efb-318">La mise en forme de caractères en gras et en italique n’est pas restituer sur iOS.</span><span class="sxs-lookup"><span data-stu-id="88efb-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="88efb-319">Sur Android, la mise en forme HTML s’affiche comme ceci :</span><span class="sxs-lookup"><span data-stu-id="88efb-319">On Android, HTML formatting appears like this:</span></span>

![Mise en forme HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="88efb-321">La mise en forme des caractères comme gras et italique s’affiche correctement sur Android.</span><span class="sxs-lookup"><span data-stu-id="88efb-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="88efb-322">Exemple de mise en forme pour la mise en forme HTML dans des cartes simples</span><span class="sxs-lookup"><span data-stu-id="88efb-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="88efb-323">Ces captures d’écran ont été créées Teams AppStudio, où la propriété de texte d’une carte Hero a été définie sur la chaîne suivante.</span><span class="sxs-lookup"><span data-stu-id="88efb-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="88efb-324">Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.</span><span class="sxs-lookup"><span data-stu-id="88efb-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
