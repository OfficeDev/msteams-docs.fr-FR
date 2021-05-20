---
title: Formatage de texte dans les cartes
description: Décrit le formatage du texte de la carte dans Microsoft Teams
keywords: équipes bots format cartes
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
# <a name="format-cards-in-teams"></a><span data-ttu-id="eb2c3-104">Cartes formatées en Teams</span><span class="sxs-lookup"><span data-stu-id="eb2c3-104">Format cards in Teams</span></span>

<span data-ttu-id="eb2c3-105">Vous pouvez ajouter un formatage de texte riche à vos cartes en utilisant markdown ou HTML, selon le type de carte.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="eb2c3-106">Les cartes supportent le formatage dans la propriété de texte seulement, pas dans les propriétés de titre ou de sous-titre.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="eb2c3-107">Le formatage peut être spécifié à l’aide d’un sous-ensemble de formatage XML (HTML) ou markdown selon le type de carte.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="eb2c3-108">Pour le développement actuel et futur, il est recommandé d’utiliser des cartes adaptatives utilisant le formatage Markdown.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="eb2c3-109">Le formatage de la prise en charge diffère d’un type de carte à l’autre, et le rendu de la carte peut différer légèrement entre le bureau et les clients de Teams mobiles, ainsi que les Teams dans le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="eb2c3-110">Vous pouvez inclure une image en ligne avec n’importe quelle Teams carte.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="eb2c3-111">Images un être formaté comme  `.png` , ou des fichiers et ne doit pas dépasser `.jpg` `.gif` 1024 ×1024 px ou 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="eb2c3-112">Gif animé n’est pas officiellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="eb2c3-113">Pour plus d’informations, voir [référence Cartes](./cards-reference.md#inline-card-images).</span><span class="sxs-lookup"><span data-stu-id="eb2c3-113">For more information, see [Cards reference](./cards-reference.md#inline-card-images).</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="eb2c3-114">Formater les cartes avec Markdown</span><span class="sxs-lookup"><span data-stu-id="eb2c3-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="eb2c3-115">Il existe deux types de cartes qui soutiennent Markdown dans Teams :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb2c3-116">**Cartes adaptatives**: Markdown est pris en charge dans le `Textblock` champ de carte adaptative, ainsi `Fact.Title` que `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="eb2c3-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="eb2c3-117">Html n’est pas pris en charge dans les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="eb2c3-118">**Cartes connecteur O365**: Markdown et HTML limité sont pris en charge dans Office 365 cartes Connecteur dans les champs de texte.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="eb2c3-119">**Mise en forme Markdown : Cartes adaptatives**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="eb2c3-120">Les styles pris en charge `Textblock` pour , `Fact.Title` et `Fact.Value` sont:</span><span class="sxs-lookup"><span data-stu-id="eb2c3-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="eb2c3-121">Style</span><span class="sxs-lookup"><span data-stu-id="eb2c3-121">Style</span></span> | <span data-ttu-id="eb2c3-122">Exemple</span><span class="sxs-lookup"><span data-stu-id="eb2c3-122">Example</span></span> | <span data-ttu-id="eb2c3-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="eb2c3-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb2c3-124">bold</span><span class="sxs-lookup"><span data-stu-id="eb2c3-124">bold</span></span> | <span data-ttu-id="eb2c3-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="eb2c3-126">italic</span><span class="sxs-lookup"><span data-stu-id="eb2c3-126">italic</span></span> | <span data-ttu-id="eb2c3-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="eb2c3-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="eb2c3-128">liste non ordonnée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-128">unordered list</span></span> | <ul><li><span data-ttu-id="eb2c3-129">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-129">text</span></span></li><li><span data-ttu-id="eb2c3-130">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="eb2c3-131">liste commandée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-131">ordered list</span></span> | <ol><li><span data-ttu-id="eb2c3-132">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-132">text</span></span></li><li><span data-ttu-id="eb2c3-133">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="eb2c3-134">Liens hypertexte</span><span class="sxs-lookup"><span data-stu-id="eb2c3-134">Hyperlinks</span></span> |[<span data-ttu-id="eb2c3-135">Bing</span><span class="sxs-lookup"><span data-stu-id="eb2c3-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="eb2c3-136">Les balises Markdown suivantes ne sont pas prises en charge :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="eb2c3-137">En-têtes</span><span class="sxs-lookup"><span data-stu-id="eb2c3-137">Headers</span></span>
* <span data-ttu-id="eb2c3-138">Tables</span><span class="sxs-lookup"><span data-stu-id="eb2c3-138">Tables</span></span>
* <span data-ttu-id="eb2c3-139">Des images</span><span class="sxs-lookup"><span data-stu-id="eb2c3-139">Images</span></span>
* <span data-ttu-id="eb2c3-140">Texte préformaté</span><span class="sxs-lookup"><span data-stu-id="eb2c3-140">Preformatted text</span></span>
* <span data-ttu-id="eb2c3-141">Blockquotes Blockquotes</span><span class="sxs-lookup"><span data-stu-id="eb2c3-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eb2c3-142">Les cartes adaptatives ne supportent pas le formatage HTML.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="eb2c3-143">Nouvelles lignes pour cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="eb2c3-144">Dans les listes, vous pouvez utiliser `\r` les séquences ou les séquences `\n` d’évasion pour les nouvelles lignes.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="eb2c3-145">`\n\n`L’utilisation dans une liste provoquera l’indented du prochain élément de la liste.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="eb2c3-146">Si vous avez besoin de nouvelles lignes ailleurs dans le bloc de texte, utilisez `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="eb2c3-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="eb2c3-147">Différences mobiles et de bureau pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="eb2c3-148">Le formatage est légèrement différent entre le bureau et les versions mobiles de Teams.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="eb2c3-149">Sur le bureau, le formatage markdown de carte adaptative apparaît ainsi dans les navigateurs Web et dans l’application Teams client :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Formatage markdown de carte adaptative dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="eb2c3-151">Sur iOS, le formatage markdown de la carte adaptative apparaît comme ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Formatage markdown de carte adaptative dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="eb2c3-153">Sur Android, le formatage adaptatif de Markdown de carte apparaît comme ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Carte adaptative Markdown formatage dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="eb2c3-155">Plus d’informations sur les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-155">More information on Adaptive cards</span></span>

<span data-ttu-id="eb2c3-156">[Fonctionnalités textuelles dans les cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans ce sujet ne sont pas prises en charge Teams.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="eb2c3-157">Exemple de mise en forme des cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="eb2c3-158">Mention de support dans les cartes adaptatives v1.2</span><span class="sxs-lookup"><span data-stu-id="eb2c3-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="eb2c3-159">Les mentions basées sur la carte sont prises en charge dans les clients web, bureau et mobiles.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="eb2c3-160">Vous pouvez ajouter @ mentions dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="eb2c3-161">Pour ajouter @ mentions dans les cartes, suivez la même logique de notification et de rendu que celle des mentions basées sur les [messages dans les conversations de chat de canal et de groupe](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span><span class="sxs-lookup"><span data-stu-id="eb2c3-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="eb2c3-162">Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la [carte dans les éléments TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="eb2c3-163">[Les éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptatives v1.2 sur la Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="eb2c3-164">Les mentions &'équipe ne sont pas prises en charge dans les messages bot.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="eb2c3-165">Construction de mentions</span><span class="sxs-lookup"><span data-stu-id="eb2c3-165">Constructing mentions</span></span>

<span data-ttu-id="eb2c3-166">Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="eb2c3-167">`<at>username</at>` dans les éléments de carte adaptatif pris en charge.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="eb2c3-168">`mention`L’objet à l’intérieur `msteams` d’une propriété dans le contenu de la carte, qui inclut Teams id utilisateur de l’utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="eb2c3-169">Le `userId` est unique à votre id bot et un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="eb2c3-170">Il peut être utilisé pour @mention un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="eb2c3-171">Le `userId` peut être récupéré en utilisant l’une des options mentionnées pour obtenir [l’iD de l’utilisateur](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="eb2c3-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="eb2c3-172">Exemple de carte adaptative avec mention</span><span class="sxs-lookup"><span data-stu-id="eb2c3-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="eb2c3-173">Masquage d’informations dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="eb2c3-174">Utilisez la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs dans l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de la carte Adaptative.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb2c3-175">La fonctionnalité prend en charge uniquement le masquage des informations secondaires du client, le texte d’entrée masqué est envoyé sous forme de texte clair à l’adresse de point de terminaison https qui a été spécifiée lors de [la configuration du bot.](../../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="eb2c3-176">La propriété de masquage d’informations est actuellement disponible dans l’aperçu développeur seulement.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="eb2c3-177">Pour masquer les informations contenues dans les cartes `isMasked` adaptatives, ajoutez **la propriété au type** et `Input.Text` réglez sa valeur à la *réalité.*</span><span class="sxs-lookup"><span data-stu-id="eb2c3-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="eb2c3-178">Exemple carte adaptative avec propriété de masquage</span><span class="sxs-lookup"><span data-stu-id="eb2c3-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="eb2c3-179">L’image suivante est un exemple d’information masquante dans les cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-179">The following image is an example of masking information in Adaptive cards:</span></span>

![Image d’information de masquage](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="eb2c3-181">Carte adaptative pleine largeur</span><span class="sxs-lookup"><span data-stu-id="eb2c3-181">Full width Adaptive card</span></span>
<span data-ttu-id="eb2c3-182">Vous pouvez utiliser la propriété `msteams` pour élargir la largeur d’une carte adaptative et utiliser de l’espace de toile supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="eb2c3-183">Pour plus d’informations sur la façon d’utiliser la propriété, voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="eb2c3-184">Construction de cartes pleine largeur</span><span class="sxs-lookup"><span data-stu-id="eb2c3-184">Constructing full width cards</span></span>
<span data-ttu-id="eb2c3-185">Pour faire une carte adaptative pleine largeur, `width` l’objet `msteams` dans la propriété dans le contenu de la carte doit être réglé sur `Full` .</span><span class="sxs-lookup"><span data-stu-id="eb2c3-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="eb2c3-186">En outre, votre application doit inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="eb2c3-187">Exemple de carte adaptative avec pleine largeur</span><span class="sxs-lookup"><span data-stu-id="eb2c3-187">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="eb2c3-188">Une carte adaptative pleine largeur apparaît comme suit : ![ Vue de la carte adaptative pleine largeur](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="eb2c3-189">Si vous n’avez pas défini `width` la propriété à *plein*, alors la vue par défaut de la carte adaptative est la suivante: ![ Petite largeur Vue de carte adaptative](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="eb2c3-190">Soutien typeahead</span><span class="sxs-lookup"><span data-stu-id="eb2c3-190">Typeahead support</span></span>

<span data-ttu-id="eb2c3-191">Dans [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) l’élément schéma, demander aux utilisateurs de filtrer à travers et de sélectionner à travers un nombre important de choix peut ralentir considérablement l’achèvement des tâches.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="eb2c3-192">La prise en charge typeahead dans les cartes adaptatives peut simplifier la sélection des entrées en rétrécissant ou en filtrant l’ensemble des choix d’entrée s’il tape l’entrée.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="eb2c3-193">Activer typeahead dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="eb2c3-194">Pour activer typeahead dans `Input.Choiceset` l’ensemble `style` et `filtered` s’assurer `isMultiSelect` est réglé sur `false` .</span><span class="sxs-lookup"><span data-stu-id="eb2c3-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="eb2c3-195">Exemple de carte adaptative avec prise en charge typeahead</span><span class="sxs-lookup"><span data-stu-id="eb2c3-195">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="eb2c3-196">Vue scénique pour les images dans cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="eb2c3-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="eb2c3-197">Cette fonctionnalité est actuellement disponible en aperçu développeur uniquement.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="eb2c3-198">Dans une carte adaptative, vous pouvez utiliser la propriété `msteams` pour ajouter la possibilité d’afficher des images en vue de scène de manière sélective.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="eb2c3-199">Lorsque les utilisateurs planent au-dessus des images, ils voient une icône d’expansion, pour laquelle `allowExpand` l’attribut est défini à `true` .</span><span class="sxs-lookup"><span data-stu-id="eb2c3-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="eb2c3-200">Pour plus d’informations sur la façon d’utiliser la propriété, voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-200">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="eb2c3-201">Lorsque les utilisateurs planent au-dessus de l’image, une icône d’expansion apparaît en haut à droite de l’image : ![ carte adaptative avec image extensible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="eb2c3-202">L’image apparaît dans la vue de scène lorsque l’utilisateur sélectionne le bouton d’expansion : ![ Image étendue à la vue de scène](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="eb2c3-203">Dans la vue scène, les utilisateurs peuvent zoomer et zoomer sur l’image.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="eb2c3-204">Vous pouvez sélectionner les images de votre carte Adaptative qui doivent avoir cette capacité.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="eb2c3-205">La capacité de zoom avant et de zoom arrière ne s’applique qu’aux éléments d’image (type d’image) d’une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="eb2c3-206">Pour les applications mobiles Teams, les fonctionnalités de vue scénique pour les images des cartes adaptatives sont disponibles par défaut et les utilisateurs pourront afficher des images de carte adaptative en vue de la scène en appuyant simplement sur l’image, que `allowExpand` l’attribut soit présent ou non.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="eb2c3-207">**Mise en forme Markdown : Cartes connecteur O365**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="eb2c3-208">Les cartes connecteurs supportent le formatage Markdown et HTML limité.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="eb2c3-209">Le support HTML est décrit dans la dernière section.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="eb2c3-210">Style</span><span class="sxs-lookup"><span data-stu-id="eb2c3-210">Style</span></span> | <span data-ttu-id="eb2c3-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="eb2c3-211">Example</span></span> | <span data-ttu-id="eb2c3-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="eb2c3-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb2c3-213">bold</span><span class="sxs-lookup"><span data-stu-id="eb2c3-213">bold</span></span> | <span data-ttu-id="eb2c3-214">**text**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="eb2c3-215">italic</span><span class="sxs-lookup"><span data-stu-id="eb2c3-215">italic</span></span> | <span data-ttu-id="eb2c3-216">*text*</span><span class="sxs-lookup"><span data-stu-id="eb2c3-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="eb2c3-217">en-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="eb2c3-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="eb2c3-219">strikethrough</span><span class="sxs-lookup"><span data-stu-id="eb2c3-219">strikethrough</span></span> | <span data-ttu-id="eb2c3-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="eb2c3-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="eb2c3-221">liste non ordonnée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-221">unordered list</span></span> | <ul><li><span data-ttu-id="eb2c3-222">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-222">text</span></span></li><li><span data-ttu-id="eb2c3-223">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="eb2c3-224">liste commandée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-224">ordered list</span></span> | <ol><li><span data-ttu-id="eb2c3-225">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-225">text</span></span></li><li><span data-ttu-id="eb2c3-226">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="eb2c3-227">texte préformaté</span><span class="sxs-lookup"><span data-stu-id="eb2c3-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="eb2c3-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="eb2c3-228">blockquote</span></span> | <span data-ttu-id="eb2c3-229">>texte blockquote</span><span class="sxs-lookup"><span data-stu-id="eb2c3-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="eb2c3-230">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="eb2c3-230">hyperlink</span></span> | [<span data-ttu-id="eb2c3-231">Bing</span><span class="sxs-lookup"><span data-stu-id="eb2c3-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="eb2c3-232">lien d’image</span><span class="sxs-lookup"><span data-stu-id="eb2c3-232">image link</span></span> |![Canard sur une roche](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="eb2c3-234">Dans les cartes de connecteur, les nouvelles lignes sont rendues `\n\n` pour, mais pas pour `\n` ou `\r` .</span><span class="sxs-lookup"><span data-stu-id="eb2c3-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="eb2c3-235">Différences mobiles et de bureau pour les cartes de connecteur utilisant Markdown</span><span class="sxs-lookup"><span data-stu-id="eb2c3-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="eb2c3-236">Sur le bureau, le formatage Markdown pour les cartes de connecteur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="eb2c3-238">Sur iOS, le formatage Markdown pour les cartes connecteurs ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme Markdown pour les cartes connecteurs dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="eb2c3-240">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-240">Issues:</span></span>

* <span data-ttu-id="eb2c3-241">Le client iOS pour Teams rend pas markdown ou html images en ligne dans les cartes connecteur.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="eb2c3-242">Les blockquotes sont rendus en tant qu’indented mais sans fond gris.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="eb2c3-243">Sur Android, le formatage Markdown pour les cartes connecteurs ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Mise en forme Markdown pour les cartes connecteurs dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="eb2c3-245">Exemple de formatage pour les cartes connecteur Markdown</span><span class="sxs-lookup"><span data-stu-id="eb2c3-245">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="eb2c3-246">Formater les cartes avec HTML</span><span class="sxs-lookup"><span data-stu-id="eb2c3-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="eb2c3-247">**Formatage HTML : Cartes connecteur O365**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="eb2c3-248">Les cartes connecteurs supportent le formatage Markdown et HTML limité.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="eb2c3-249">Markdown est décrit dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="eb2c3-250">Style</span><span class="sxs-lookup"><span data-stu-id="eb2c3-250">Style</span></span> | <span data-ttu-id="eb2c3-251">Exemple</span><span class="sxs-lookup"><span data-stu-id="eb2c3-251">Example</span></span> | <span data-ttu-id="eb2c3-252">HTML</span><span class="sxs-lookup"><span data-stu-id="eb2c3-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb2c3-253">bold</span><span class="sxs-lookup"><span data-stu-id="eb2c3-253">bold</span></span> | <span data-ttu-id="eb2c3-254">**text**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="eb2c3-255">italic</span><span class="sxs-lookup"><span data-stu-id="eb2c3-255">italic</span></span> | <span data-ttu-id="eb2c3-256">*text*</span><span class="sxs-lookup"><span data-stu-id="eb2c3-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="eb2c3-257">en-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="eb2c3-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="eb2c3-259">strikethrough</span><span class="sxs-lookup"><span data-stu-id="eb2c3-259">strikethrough</span></span> | <span data-ttu-id="eb2c3-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="eb2c3-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="eb2c3-261">liste non ordonnée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-261">unordered list</span></span> | <ul><li><span data-ttu-id="eb2c3-262">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-262">text</span></span></li><li><span data-ttu-id="eb2c3-263">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="eb2c3-264">liste commandée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-264">ordered list</span></span> | <ol><li><span data-ttu-id="eb2c3-265">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-265">text</span></span></li><li><span data-ttu-id="eb2c3-266">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="eb2c3-267">texte préformaté</span><span class="sxs-lookup"><span data-stu-id="eb2c3-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="eb2c3-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="eb2c3-268">blockquote</span></span> | <blockquote><span data-ttu-id="eb2c3-269">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="eb2c3-270">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="eb2c3-270">hyperlink</span></span> | [<span data-ttu-id="eb2c3-271">Bing</span><span class="sxs-lookup"><span data-stu-id="eb2c3-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="eb2c3-272">lien d’image</span><span class="sxs-lookup"><span data-stu-id="eb2c3-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="eb2c3-273">Dans les cartes de connecteur, les nouvelles lignes sont rendues en HTML à l’aide de `<p>` la balise.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="eb2c3-274">Différences mobiles et de bureau pour les cartes de connecteur utilisant HTML</span><span class="sxs-lookup"><span data-stu-id="eb2c3-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="eb2c3-275">Sur le bureau, le formatage HTML pour les cartes de connecteur ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Formatage HTML pour les cartes de connecteur dans le client Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="eb2c3-277">Sur iOS, le formatage HTML ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-277">On iOS, HTML formatting looks like this:</span></span>

![Formatage HTML pour les cartes connecteurs dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="eb2c3-279">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-279">Issues:</span></span>

* <span data-ttu-id="eb2c3-280">Les images en ligne ne sont pas rendues sur iOS à l’aide de Markdown ou html dans les cartes connecteurs.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="eb2c3-281">Le texte préformaté est rendu mais n’a pas de fond gris.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="eb2c3-282">Sur Android, le formatage HTML ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-282">On Android, HTML formatting looks like this:</span></span>

![Formatage HTML pour les cartes connecteurs dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="eb2c3-284">Exemple de formatage pour les cartes connecteurs HTML</span><span class="sxs-lookup"><span data-stu-id="eb2c3-284">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="eb2c3-285">**Formatage HTML : cartes héros et vignettes**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="eb2c3-286">Les balises HTML sont prises en charge pour les cartes simples telles que le héros et la carte miniature.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="eb2c3-287">Markdown n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-287">Markdown is not supported.</span></span>

| <span data-ttu-id="eb2c3-288">Style</span><span class="sxs-lookup"><span data-stu-id="eb2c3-288">Style</span></span> | <span data-ttu-id="eb2c3-289">Exemple</span><span class="sxs-lookup"><span data-stu-id="eb2c3-289">Example</span></span> | <span data-ttu-id="eb2c3-290">HTML</span><span class="sxs-lookup"><span data-stu-id="eb2c3-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb2c3-291">bold</span><span class="sxs-lookup"><span data-stu-id="eb2c3-291">bold</span></span> | <span data-ttu-id="eb2c3-292">**text**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="eb2c3-293">italic</span><span class="sxs-lookup"><span data-stu-id="eb2c3-293">italic</span></span> | <span data-ttu-id="eb2c3-294">*text*</span><span class="sxs-lookup"><span data-stu-id="eb2c3-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="eb2c3-295">en-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="eb2c3-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="eb2c3-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="eb2c3-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="eb2c3-297">strikethrough</span><span class="sxs-lookup"><span data-stu-id="eb2c3-297">strikethrough</span></span> | <span data-ttu-id="eb2c3-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="eb2c3-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="eb2c3-299">liste non ordonnée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-299">unordered list</span></span> | <ul><li><span data-ttu-id="eb2c3-300">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-300">text</span></span></li><li><span data-ttu-id="eb2c3-301">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="eb2c3-302">liste commandée</span><span class="sxs-lookup"><span data-stu-id="eb2c3-302">ordered list</span></span> | <ol><li><span data-ttu-id="eb2c3-303">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-303">text</span></span></li><li><span data-ttu-id="eb2c3-304">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="eb2c3-305">texte préformaté</span><span class="sxs-lookup"><span data-stu-id="eb2c3-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="eb2c3-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="eb2c3-306">blockquote</span></span> | <blockquote><span data-ttu-id="eb2c3-307">text</span><span class="sxs-lookup"><span data-stu-id="eb2c3-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="eb2c3-308">lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="eb2c3-308">hyperlink</span></span> | [<span data-ttu-id="eb2c3-309">Bing</span><span class="sxs-lookup"><span data-stu-id="eb2c3-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="eb2c3-310">lien d’image</span><span class="sxs-lookup"><span data-stu-id="eb2c3-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="eb2c3-311">Différences mobiles et de bureau pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="eb2c3-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="eb2c3-312">En raison des différences de résolution entre le bureau et la plate-forme mobile, le formatage est différent entre le bureau et la version mobile de Teams.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="eb2c3-313">Sur le bureau, le formatage HTML apparaît comme ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-313">On the desktop, HTML formatting appears like this:</span></span>

![Formatage HTML dans le client Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="eb2c3-315">Sur iOS, le formatage HTML apparaît comme ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-315">On iOS, HTML formatting appears like this:</span></span>

![Formatage HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="eb2c3-317">Problèmes :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-317">Issues:</span></span>

* <span data-ttu-id="eb2c3-318">Le formatage des caractères comme gras et italique n’est pas rendu sur iOS.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="eb2c3-319">Sur Android, le formatage HTML apparaît comme ceci :</span><span class="sxs-lookup"><span data-stu-id="eb2c3-319">On Android, HTML formatting appears like this:</span></span>

![Formatage HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="eb2c3-321">Formatage de caractères comme affichage gras et italique correctement sur Android.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="eb2c3-322">Exemple de formatage pour le formatage HTML en cartes simples</span><span class="sxs-lookup"><span data-stu-id="eb2c3-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="eb2c3-323">Ces captures d’écran ont été créées Teams appstudio, où la propriété textuelle d’une carte héros a été réglée sur la chaîne suivante.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="eb2c3-324">Vous pouvez tester le formatage dans vos propres cartes en modifiant ce code.</span><span class="sxs-lookup"><span data-stu-id="eb2c3-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
