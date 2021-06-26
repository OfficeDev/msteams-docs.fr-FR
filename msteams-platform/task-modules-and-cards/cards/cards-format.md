---
title: Mise en forme du texte dans les cartes
description: Décrit la mise en forme du texte de la carte Microsoft Teams
keywords: Format de cartes de bots Teams
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 877a16f884e91138dc656434438a5fe1dd2ffd6e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140602"
---
# <a name="format-cards-in-microsoft-teams"></a><span data-ttu-id="33ea4-104">Formater les cartes dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="33ea4-104">Format cards in Microsoft Teams</span></span>

<span data-ttu-id="33ea4-105">Voici les deux façons d’ajouter une mise en forme de texte enrichi à vos cartes :</span><span class="sxs-lookup"><span data-stu-id="33ea4-105">Following are the two ways to add rich text formatting to your cards:</span></span>
* [<span data-ttu-id="33ea4-106">Markdown</span><span class="sxs-lookup"><span data-stu-id="33ea4-106">Markdown</span></span>](#format-cards-with-markdown)
* [<span data-ttu-id="33ea4-107">HTML</span><span class="sxs-lookup"><span data-stu-id="33ea4-107">HTML</span></span>](#format-cards-with-html)

<span data-ttu-id="33ea4-108">Les cartes ne supportent la mise en forme que dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre.</span><span class="sxs-lookup"><span data-stu-id="33ea4-108">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="33ea4-109">La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de formats XML ou HTML ou Markdown, en fonction du type de carte.</span><span class="sxs-lookup"><span data-stu-id="33ea4-109">Formatting can be specified using a subset of XML or HTML formatting or Markdown, depending on the card type.</span></span> <span data-ttu-id="33ea4-110">Pour le développement actuel et futur des cartes adaptatives, la mise en forme Markdown est recommandée.</span><span class="sxs-lookup"><span data-stu-id="33ea4-110">For current and future development of Adaptive Cards, Markdown formatting is recommended.</span></span>

<span data-ttu-id="33ea4-111">La prise en charge de la mise en forme diffère d’un type de carte à l’autre.</span><span class="sxs-lookup"><span data-stu-id="33ea4-111">Formatting support differs between card types.</span></span> <span data-ttu-id="33ea4-112">Le rendu de la carte peut légèrement varier entre le bureau et les clients Microsoft Teams mobiles, ainsi que Teams dans le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="33ea4-112">Rendering of the card can differ slightly between the desktop and the mobile Microsoft Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="33ea4-113">Vous pouvez inclure une image inline avec n’importe Teams carte.</span><span class="sxs-lookup"><span data-stu-id="33ea4-113">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="33ea4-114">Les images peuvent être formatées en tant que fichiers ou en tant que fichiers et ne doivent pas dépasser `.png` `.jpg` `.gif` 1 024 × 1 024 px ou 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="33ea4-114">Images can be formatted as `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="33ea4-115">Gif animé non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="33ea4-115">Animated GIF is not supported.</span></span> <span data-ttu-id="33ea4-116">Pour plus d’informations, voir [les types de cartes.](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="33ea4-116">For more information, see [types of cards](./cards-reference.md#inline-card-images).</span></span>

<span data-ttu-id="33ea4-117">Vous pouvez formater des cartes adaptatives et Office 365 connecteur avec Markdown qui incluent certains styles pris en charge.</span><span class="sxs-lookup"><span data-stu-id="33ea4-117">You can format Adaptive Cards and Office 365 Connector cards with Markdown that include certain supported styles.</span></span>

## <a name="format-cards-with-markdown"></a><span data-ttu-id="33ea4-118">Formater des cartes avec Markdown</span><span class="sxs-lookup"><span data-stu-id="33ea4-118">Format cards with Markdown</span></span>

<span data-ttu-id="33ea4-119">Les types de carte suivants prise en charge la mise en forme Markdown dans Teams :</span><span class="sxs-lookup"><span data-stu-id="33ea4-119">The following card types support Markdown formatting in Teams:</span></span>

* <span data-ttu-id="33ea4-120">Cartes adaptatives : Markdown est pris en charge dans le champ de carte `Textblock` adaptative, ainsi que dans `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="33ea4-120">Adaptive Cards: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="33ea4-121">Le code HTML n’est pas pris en charge dans les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="33ea4-121">HTML is not supported in Adaptive Cards.</span></span>
* <span data-ttu-id="33ea4-122">Cartes de connecteur O365 : Markdown et html limité sont pris en charge dans les cartes de connecteur O365 dans les champs de texte.</span><span class="sxs-lookup"><span data-stu-id="33ea4-122">O365 Connector cards: Markdown and limited HTML is supported in O365 Connector cards in the text fields.</span></span>

<span data-ttu-id="33ea4-123">Vous pouvez utiliser des nouvelles lignes pour les cartes adaptatives à l’aide ou des `\r` `\n` séquences d’échappatoire pour les nouvelles lignes dans les listes.</span><span class="sxs-lookup"><span data-stu-id="33ea4-123">You can use newlines for Adaptive Cards using `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="33ea4-124">La mise en forme est différente entre le bureau et les versions mobiles de Teams pour les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="33ea4-124">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards.</span></span> <span data-ttu-id="33ea4-125">Les mentions basées sur une carte sont pris en charge dans les clients web, de bureau et mobiles.</span><span class="sxs-lookup"><span data-stu-id="33ea4-125">Card-based mentions are supported in web, desktop, and mobile clients.</span></span> <span data-ttu-id="33ea4-126">Vous pouvez utiliser la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs au sein de l’élément d’entrée `Input.Text` de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="33ea4-126">You can use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card `Input.Text` input element.</span></span> <span data-ttu-id="33ea4-127">Vous pouvez développer la largeur d’une carte adaptative à l’aide de `width` l’objet.</span><span class="sxs-lookup"><span data-stu-id="33ea4-127">You can expand the width of an Adaptive Card using the `width` object.</span></span> <span data-ttu-id="33ea4-128">Vous pouvez activer la prise en charge des en-têtes de type dans les cartes adaptatives et filtrer l’ensemble des choix d’entrée à mesure que l’utilisateur tape l’entrée.</span><span class="sxs-lookup"><span data-stu-id="33ea4-128">You can enable typeahead support within Adaptive Cards and filter the set of input choices as the user types the input.</span></span> <span data-ttu-id="33ea4-129">Vous pouvez utiliser la propriété pour ajouter la possibilité d’afficher des images en vue de la `msteams` scène de manière sélective.</span><span class="sxs-lookup"><span data-stu-id="33ea4-129">You can use the `msteams` property to add the ability to display images in stage view selectively.</span></span>

<span data-ttu-id="33ea4-130">La mise en forme est différente entre le bureau et les versions mobiles de Teams cartes adaptatives et cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="33ea4-130">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards and connector cards.</span></span> <span data-ttu-id="33ea4-131">Dans cette section, vous pouvez passer par l’exemple de format Markdown pour les cartes adaptatives et les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="33ea4-131">In this section, you can go through the Markdown format example for Adaptive Cards and connector cards.</span></span>

# <a name="markdown-format-for-adaptive-cards"></a>[<span data-ttu-id="33ea4-132">Format Markdown pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="33ea4-132">Markdown format for Adaptive Cards</span></span>](#tab/adaptive-md)

 <span data-ttu-id="33ea4-133">Le tableau suivant fournit les styles pris en charge `Textblock` pour `Fact.Title` , et `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="33ea4-133">The following table provides the supported styles for `Textblock`, `Fact.Title`, and `Fact.Value`:</span></span>

| <span data-ttu-id="33ea4-134">Style</span><span class="sxs-lookup"><span data-stu-id="33ea4-134">Style</span></span> | <span data-ttu-id="33ea4-135">Exemple</span><span class="sxs-lookup"><span data-stu-id="33ea4-135">Example</span></span> | <span data-ttu-id="33ea4-136">Markdown</span><span class="sxs-lookup"><span data-stu-id="33ea4-136">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33ea4-137">Gras</span><span class="sxs-lookup"><span data-stu-id="33ea4-137">Bold</span></span> | <span data-ttu-id="33ea4-138">**Bold**</span><span class="sxs-lookup"><span data-stu-id="33ea4-138">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="33ea4-139">Italic</span><span class="sxs-lookup"><span data-stu-id="33ea4-139">Italic</span></span> | <span data-ttu-id="33ea4-140">_Italic_</span><span class="sxs-lookup"><span data-stu-id="33ea4-140">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="33ea4-141">Liste non triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-141">Unordered list</span></span> | <ul><li><span data-ttu-id="33ea4-142">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-142">text</span></span></li><li><span data-ttu-id="33ea4-143">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-143">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="33ea4-144">Liste triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-144">Ordered list</span></span> | <ol><li><span data-ttu-id="33ea4-145">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-145">text</span></span></li><li><span data-ttu-id="33ea4-146">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-146">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="33ea4-147">Liens hypertexte</span><span class="sxs-lookup"><span data-stu-id="33ea4-147">Hyperlinks</span></span> |[<span data-ttu-id="33ea4-148">Bing</span><span class="sxs-lookup"><span data-stu-id="33ea4-148">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="33ea4-149">Les balises Markdown suivantes ne sont pas pris en charge :</span><span class="sxs-lookup"><span data-stu-id="33ea4-149">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="33ea4-150">En-têtes</span><span class="sxs-lookup"><span data-stu-id="33ea4-150">Headers</span></span>
* <span data-ttu-id="33ea4-151">Tables</span><span class="sxs-lookup"><span data-stu-id="33ea4-151">Tables</span></span>
* <span data-ttu-id="33ea4-152">Des images</span><span class="sxs-lookup"><span data-stu-id="33ea4-152">Images</span></span>
* <span data-ttu-id="33ea4-153">Texte préformaté</span><span class="sxs-lookup"><span data-stu-id="33ea4-153">Preformatted text</span></span>
* <span data-ttu-id="33ea4-154">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="33ea4-154">Blockquotes</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="33ea4-155">Nouvelles lignes pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="33ea4-155">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="33ea4-156">Vous pouvez utiliser les `\r` `\n` séquences d’échappatoire ou les séquences d’échappatoire pour les nouvelles lignes dans les listes.</span><span class="sxs-lookup"><span data-stu-id="33ea4-156">You can use the `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="33ea4-157">L’utilisation dans les listes entraîne le retrait de l’élément suivant dans `\n\n` la liste.</span><span class="sxs-lookup"><span data-stu-id="33ea4-157">Using `\n\n` in lists causes the next element in the list to be indented.</span></span> <span data-ttu-id="33ea4-158">Si vous avez besoin de lignes nouvelles ailleurs dans le TextBlock, utilisez `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="33ea4-158">If you require newlines elsewhere in the TextBlock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="33ea4-159">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="33ea4-159">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="33ea4-160">Sur le bureau, la mise en forme de markdown de carte adaptative apparaît comme illustré dans l’image suivante dans les navigateurs web et dans l Teams application cliente :</span><span class="sxs-lookup"><span data-stu-id="33ea4-160">On the desktop, Adaptive Card Markdown formatting appears as shown in the following image in both web browsers and in the Teams client application:</span></span>

![Mise en forme Markdown de carte adaptative dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="33ea4-162">Sur iOS, la mise en forme Markdown de carte adaptative apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-162">On iOS, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Mise en forme markdown de carte adaptative dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="33ea4-164">Sur Android, la mise en forme markdown de carte adaptative apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-164">On Android, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Mise en forme markdown de carte adaptative dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

<span data-ttu-id="33ea4-166">Pour plus d’informations, voir [les fonctionnalités de texte dans les cartes adaptatives.](/adaptive-cards/create/textfeatures)</span><span class="sxs-lookup"><span data-stu-id="33ea4-166">For more information, see [text features in Adaptive Cards](/adaptive-cards/create/textfeatures).</span></span>

> [!NOTE]
> <span data-ttu-id="33ea4-167">Les fonctionnalités de date et de localisation mentionnées dans cette section ne sont pas Teams.</span><span class="sxs-lookup"><span data-stu-id="33ea4-167">The date and localization features mentioned in this section are not supported in Teams.</span></span>

### <a name="adaptive-cards-format-sample"></a><span data-ttu-id="33ea4-168">Exemple de format de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="33ea4-168">Adaptive Cards format sample</span></span>

<span data-ttu-id="33ea4-169">Le code suivant illustre un exemple de mise en forme des cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="33ea4-169">The following code shows an example of Adaptive Cards formatting:</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="33ea4-170">Prise en charge des mentions dans les cartes adaptatives v1.2</span><span class="sxs-lookup"><span data-stu-id="33ea4-170">Mention support within Adaptive Cards v1.2</span></span>

<span data-ttu-id="33ea4-171">Vous pouvez ajouter des @mentions dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="33ea4-171">You can add @mentions within an Adaptive Card body for bots and messaging extension responses.</span></span> <span data-ttu-id="33ea4-172">Pour ajouter @mentions cartes, suivez la même logique de notification et le même rendu que celui des [mentions basées](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)sur les messages dans les conversations de canal et de groupe.</span><span class="sxs-lookup"><span data-stu-id="33ea4-172">To add @mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="33ea4-173">Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la carte dans les éléments [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="33ea4-173">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="33ea4-174">[Les éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptatives v1.2 sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="33ea4-174">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive Cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="33ea4-175">Les mentions de canal et d’équipe ne sont pas pris en charge dans les messages de bot.</span><span class="sxs-lookup"><span data-stu-id="33ea4-175">Channel and team mentions are not supported in bot messages.</span></span>

<span data-ttu-id="33ea4-176">Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="33ea4-176">To include a mention in an Adaptive Card, your app needs to include the following elements:</span></span>

* <span data-ttu-id="33ea4-177">`<at>username</at>` dans les éléments de carte adaptative pris en charge.</span><span class="sxs-lookup"><span data-stu-id="33ea4-177">`<at>username</at>` in the supported Adaptive Card elements.</span></span>
* <span data-ttu-id="33ea4-178">L’objet à l’intérieur d’une propriété dans le contenu de la carte inclut `mention` `msteams` l’ID Teams’utilisateur de l’utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="33ea4-178">The `mention` object inside of an `msteams` property in the card content includes the Teams user ID of the user being mentioned.</span></span>
* <span data-ttu-id="33ea4-179">Il `userId` est propre à votre ID de bot et à un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="33ea4-179">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="33ea4-180">Il peut être utilisé pour @mention un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="33ea4-180">It can be used to @mention a particular user.</span></span> <span data-ttu-id="33ea4-181">Il `userId` peut être récupéré à l’aide de l’une des options mentionnées dans obtenir [l’ID utilisateur.](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)</span><span class="sxs-lookup"><span data-stu-id="33ea4-181">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="33ea4-182">Exemple de carte adaptative avec une mention</span><span class="sxs-lookup"><span data-stu-id="33ea4-182">Sample Adaptive Card with a mention</span></span>

<span data-ttu-id="33ea4-183">Le code suivant montre un exemple de carte adaptative avec une mention :</span><span class="sxs-lookup"><span data-stu-id="33ea4-183">The following code shows an example of Adaptive Card with a mention:</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="33ea4-184">Masquage d’informations dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="33ea4-184">Information masking in Adaptive Cards</span></span>

<span data-ttu-id="33ea4-185">Utilisez la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs au sein de l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="33ea4-185">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span>

> [!NOTE]
> <span data-ttu-id="33ea4-186">La fonctionnalité prend uniquement en charge le masquage d’informations côté client.</span><span class="sxs-lookup"><span data-stu-id="33ea4-186">The feature only supports client side information masking.</span></span> <span data-ttu-id="33ea4-187">Le texte d’entrée masqué est envoyé en tant que texte clair à l’adresse de point de terminaison HTTPS spécifiée lors de la [configuration du bot.](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)</span><span class="sxs-lookup"><span data-stu-id="33ea4-187">The masked input text is sent as clear text to the HTTPS endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).</span></span>

<span data-ttu-id="33ea4-188">Pour masquer les informations dans les cartes adaptatives, ajoutez la propriété à taper et définissez `isMasked` sa valeur sur  `Input.Text` **true**.</span><span class="sxs-lookup"><span data-stu-id="33ea4-188">To mask information in Adaptive Cards, add the `isMasked` property to **type** `Input.Text`, and set its value to **true**.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="33ea4-189">Exemple de carte adaptative avec propriété de masquage</span><span class="sxs-lookup"><span data-stu-id="33ea4-189">Sample Adaptive Card with masking property</span></span>

<span data-ttu-id="33ea4-190">Le code suivant illustre un exemple de carte adaptative avec propriété de masquage :</span><span class="sxs-lookup"><span data-stu-id="33ea4-190">The following code shows an example of Adaptive Card with masking property:</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

<span data-ttu-id="33ea4-191">L’image suivante est un exemple de masquage d’informations dans les cartes adaptatives :</span><span class="sxs-lookup"><span data-stu-id="33ea4-191">The following image is an example of masking information in Adaptive Cards:</span></span>

![Image d’informations de masquage](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="33ea4-193">Carte adaptative pleine largeur</span><span class="sxs-lookup"><span data-stu-id="33ea4-193">Full width Adaptive Card</span></span>

<span data-ttu-id="33ea4-194">Vous pouvez utiliser la propriété pour développer la largeur d’une carte adaptative et `msteams` utiliser de l’espace de dessin supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="33ea4-194">You can use the `msteams` property to expand the width of an Adaptive Card and make use of additional canvas space.</span></span> <span data-ttu-id="33ea4-195">La section suivante fournit des informations sur l’utilisation de la propriété.</span><span class="sxs-lookup"><span data-stu-id="33ea4-195">The next section provides information on how to use the property.</span></span>

#### <a name="construct-full-width-cards"></a><span data-ttu-id="33ea4-196">Créer des cartes pleine largeur</span><span class="sxs-lookup"><span data-stu-id="33ea4-196">Construct full width cards</span></span>

<span data-ttu-id="33ea4-197">Pour créer une carte adaptative pleine largeur, l’objet dans la propriété dans le contenu de la carte `width` doit être définie sur `msteams` `Full` .</span><span class="sxs-lookup"><span data-stu-id="33ea4-197">To make a full width Adaptive Card, the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="33ea4-198">Exemple de carte adaptative avec pleine largeur</span><span class="sxs-lookup"><span data-stu-id="33ea4-198">Sample Adaptive Card with full width</span></span>

<span data-ttu-id="33ea4-199">Pour effectuer une carte adaptative pleine largeur, votre application doit inclure les éléments de l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="33ea4-199">To make a full width Adaptive Card, your app must include the elements from the following code sample:</span></span>

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

<span data-ttu-id="33ea4-200">L’image suivante illustre une carte adaptative pleine largeur :</span><span class="sxs-lookup"><span data-stu-id="33ea4-200">The following image shows a full width Adaptive Card:</span></span>

![Affichage carte adaptative pleine largeur](../../assets/images/cards/full-width-adaptive-card.png)

<span data-ttu-id="33ea4-202">L’image suivante montre l’affichage par défaut de la carte adaptative lorsque vous n’avez pas fixé la valeur `width` Full à la **propriété**:</span><span class="sxs-lookup"><span data-stu-id="33ea4-202">The following image shows the default view of the Adaptive Card when you have not set the `width` property to **Full**:</span></span>

![Affichage carte adaptative à petite largeur](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a><span data-ttu-id="33ea4-204">Prise en charge de Typeahead</span><span class="sxs-lookup"><span data-stu-id="33ea4-204">Typeahead support</span></span>

<span data-ttu-id="33ea4-205">Dans l’élément de schéma, le fait de demander aux utilisateurs de filtrer et de sélectionner un nombre important de choix peut ralentir considérablement l’exécution [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de la tâche.</span><span class="sxs-lookup"><span data-stu-id="33ea4-205">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter and select a sizeable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="33ea4-206">La prise en charge de la tête de type dans les cartes adaptatives peut simplifier la sélection des entrées en axant ou en filtrant l’ensemble des choix d’entrée à mesure que l’utilisateur tape l’entrée.</span><span class="sxs-lookup"><span data-stu-id="33ea4-206">Typeahead support within Adaptive Cards can simplify input selection by narrowing or filtering the set of input choices as the user types the input.</span></span>

<span data-ttu-id="33ea4-207">Pour activer typeahead dans `Input.Choiceset` le , définie sur et `style` `filtered` `isMultiSelect` assurez-vous qu’elle est définie sur `false` .</span><span class="sxs-lookup"><span data-stu-id="33ea4-207">To enable typeahead within the `Input.Choiceset`, set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span>

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="33ea4-208">Exemple de carte adaptative avec prise en charge de typeahead</span><span class="sxs-lookup"><span data-stu-id="33ea4-208">Sample Adaptive Card with typeahead support</span></span>

<span data-ttu-id="33ea4-209">Le code suivant illustre un exemple de carte adaptative avec prise en charge de typeahead :</span><span class="sxs-lookup"><span data-stu-id="33ea4-209">The following code shows an example of Adaptive Card with typeahead support:</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="33ea4-210">Vue d’étape des images dans les cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="33ea4-210">Stage view for images in Adaptive Cards</span></span>

<span data-ttu-id="33ea4-211">Dans une carte adaptative, vous pouvez utiliser la propriété pour ajouter la possibilité d’afficher des images en vue de la `msteams` scène de manière sélective.</span><span class="sxs-lookup"><span data-stu-id="33ea4-211">In an Adaptive Card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="33ea4-212">Lorsque les utilisateurs pointent sur les images, ils peuvent voir une icône de développement, pour laquelle l’attribut `allowExpand` est définie sur `true` .</span><span class="sxs-lookup"><span data-stu-id="33ea4-212">When users hover over the images, they can see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="33ea4-213">Pour plus d’informations sur l’utilisation de la propriété, voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="33ea4-213">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="33ea4-214">Lorsque les utilisateurs pointent sur l’image, une icône développer s’affiche dans le coin supérieur droit, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-214">When users hover over the image, an expand icon appears at the top right corner as shown in the following image:</span></span>

![Carte adaptative avec image expandable](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

<span data-ttu-id="33ea4-216">L’image apparaît en mode Étape lorsque l’utilisateur sélectionne l’icône développer, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-216">The image appears in stage view when the user selects the expand icon as shown in the following image:</span></span>

![Image étendue en vue de la phase](../../assets/images/cards/adaptivecard-expand-image.png)

<span data-ttu-id="33ea4-218">Dans la vue d’étape, les utilisateurs peuvent effectuer un zoom avant et un zoom arrière sur l’image.</span><span class="sxs-lookup"><span data-stu-id="33ea4-218">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="33ea4-219">Vous pouvez sélectionner dans votre carte adaptative les images qui doivent avoir cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="33ea4-219">You can select the images in your Adaptive Card that must have this capability.</span></span>

> [!NOTE]
> * <span data-ttu-id="33ea4-220">Les fonctionnalités de zoom avant et arrière s’appliquent uniquement aux éléments image de type image dans une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="33ea4-220">Zoom in and zoom out capability applies only to the image elements that is image type in an Adaptive Card.</span></span>
> * <span data-ttu-id="33ea4-221">Pour Teams applications mobiles, la fonctionnalité d’affichage de la scène pour les images dans les cartes adaptatives est disponible par défaut.</span><span class="sxs-lookup"><span data-stu-id="33ea4-221">For Teams mobile apps, stage view functionality for images in Adaptive Cards is available by default.</span></span> <span data-ttu-id="33ea4-222">Les utilisateurs peuvent afficher des images de carte adaptative en vue de l’étape en appuyant simplement sur l’image, que l’attribut `allowExpand` soit présent ou non.</span><span class="sxs-lookup"><span data-stu-id="33ea4-222">Users can view Adaptive Card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-format-for-o365-connector-cards"></a>[<span data-ttu-id="33ea4-223">Format Markdown pour les cartes de connecteur O365</span><span class="sxs-lookup"><span data-stu-id="33ea4-223">Markdown format for O365 Connector cards</span></span>](#tab/connector-md)

<span data-ttu-id="33ea4-224">Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="33ea4-224">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="33ea4-225">Style</span><span class="sxs-lookup"><span data-stu-id="33ea4-225">Style</span></span> | <span data-ttu-id="33ea4-226">Exemple</span><span class="sxs-lookup"><span data-stu-id="33ea4-226">Example</span></span> | <span data-ttu-id="33ea4-227">Markdown</span><span class="sxs-lookup"><span data-stu-id="33ea4-227">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33ea4-228">Gras</span><span class="sxs-lookup"><span data-stu-id="33ea4-228">Bold</span></span> | <span data-ttu-id="33ea4-229">**text**</span><span class="sxs-lookup"><span data-stu-id="33ea4-229">**text**</span></span> | `**text**` |
| <span data-ttu-id="33ea4-230">Italic</span><span class="sxs-lookup"><span data-stu-id="33ea4-230">Italic</span></span> | <span data-ttu-id="33ea4-231">*text*</span><span class="sxs-lookup"><span data-stu-id="33ea4-231">*text*</span></span> | `*text*` |
| <span data-ttu-id="33ea4-232">En-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="33ea4-232">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="33ea4-233">**Texte**</span><span class="sxs-lookup"><span data-stu-id="33ea4-233">**Text**</span></span> | `### Text`|
| <span data-ttu-id="33ea4-234">Barré</span><span class="sxs-lookup"><span data-stu-id="33ea4-234">Strikethrough</span></span> | <span data-ttu-id="33ea4-235">~~text~~</span><span class="sxs-lookup"><span data-stu-id="33ea4-235">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="33ea4-236">Liste non triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-236">Unordered list</span></span> | <ul><li><span data-ttu-id="33ea4-237">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-237">text</span></span></li><li><span data-ttu-id="33ea4-238">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-238">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="33ea4-239">Liste triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-239">Ordered list</span></span> | <ol><li><span data-ttu-id="33ea4-240">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-240">text</span></span></li><li><span data-ttu-id="33ea4-241">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-241">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="33ea4-242">Texte préformaté</span><span class="sxs-lookup"><span data-stu-id="33ea4-242">Preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="33ea4-243">Blockquote</span><span class="sxs-lookup"><span data-stu-id="33ea4-243">Blockquote</span></span> | <span data-ttu-id="33ea4-244">>blockquote</span><span class="sxs-lookup"><span data-stu-id="33ea4-244">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="33ea4-245">Lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="33ea4-245">Hyperlink</span></span> | [<span data-ttu-id="33ea4-246">Bing</span><span class="sxs-lookup"><span data-stu-id="33ea4-246">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="33ea4-247">Lien vers l’image</span><span class="sxs-lookup"><span data-stu-id="33ea4-247">Image link</span></span> |![Canet sur une bascule](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="33ea4-249">Dans les cartes de connecteur, les nouvelles lignes sont restituer `\n\n` pour , mais pas pour ou `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="33ea4-249">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="33ea4-250">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur</span><span class="sxs-lookup"><span data-stu-id="33ea4-250">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="33ea4-251">Sur le bureau, la mise en forme Markdown pour les cartes de connecteur apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-251">On the desktop, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="33ea4-253">Sur iOS, la mise en forme Markdown pour les cartes de connecteur apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-253">On iOS, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="33ea4-255">Les cartes de connecteur utilisant Markdown pour iOS incluent les problèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="33ea4-255">Connector cards using Markdown for iOS include the following issues:</span></span>

* <span data-ttu-id="33ea4-256">Le client iOS pour Teams ne restituera pas les images en ligne Markdown ou HTML dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="33ea4-256">The iOS client for Teams does not render Markdown or HTML inline images in connector cards.</span></span>
* <span data-ttu-id="33ea4-257">Les blockquotes sont restituer en retrait, mais sans arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="33ea4-257">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="33ea4-258">Sur Android, la mise en forme Markdown pour les cartes de connecteur apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-258">On Android, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Mise en forme Markdown pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a><span data-ttu-id="33ea4-260">Exemple de format pour les cartes de connecteur Markdown</span><span class="sxs-lookup"><span data-stu-id="33ea4-260">Format example for Markdown connector cards</span></span>

<span data-ttu-id="33ea4-261">Le code suivant montre un exemple de mise en forme pour les cartes de connecteur Markdown :</span><span class="sxs-lookup"><span data-stu-id="33ea4-261">The following code shows an example of formatting for Markdown connector cards:</span></span>

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

## <a name="format-cards-with-html"></a><span data-ttu-id="33ea4-262">Formater des cartes avec html</span><span class="sxs-lookup"><span data-stu-id="33ea4-262">Format cards with HTML</span></span>

<span data-ttu-id="33ea4-263">Les types de carte suivants peuvent être formaté au format HTML Teams :</span><span class="sxs-lookup"><span data-stu-id="33ea4-263">The following card types support HTML formatting in Teams:</span></span>

* <span data-ttu-id="33ea4-264">Cartes de connecteur O365 : la mise en forme limitée markdown et HTML est prise en charge dans les Office 365 connecteur.</span><span class="sxs-lookup"><span data-stu-id="33ea4-264">O365 Connector cards: Limited Markdown and HTML formatting is supported in Office 365 Connector cards.</span></span>
* <span data-ttu-id="33ea4-265">Cartes Hero et miniatures : les balises HTML sont pris en charge pour les cartes simples, telles que les cartes hero et miniatures.</span><span class="sxs-lookup"><span data-stu-id="33ea4-265">Hero and thumbnail cards: HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span>

<span data-ttu-id="33ea4-266">La mise en forme est différente entre le bureau et les versions mobiles de Teams pour les cartes de connecteur O365 et les cartes simples.</span><span class="sxs-lookup"><span data-stu-id="33ea4-266">Formatting is different between the desktop and the mobile versions of Teams for O365 Connector cards and simple cards.</span></span> <span data-ttu-id="33ea4-267">Dans cette section, vous pouvez passer par l’exemple de format HTML pour les cartes de connecteur et les cartes simples.</span><span class="sxs-lookup"><span data-stu-id="33ea4-267">In this section, you can go through the HTML format example for connector cards and simple cards.</span></span>

# <a name="html-format-for-o365-connector-cards"></a>[<span data-ttu-id="33ea4-268">Format HTML pour les cartes de connecteur O365</span><span class="sxs-lookup"><span data-stu-id="33ea4-268">HTML format for O365 Connector cards</span></span>](#tab/connector-html)

<span data-ttu-id="33ea4-269">Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML.</span><span class="sxs-lookup"><span data-stu-id="33ea4-269">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="33ea4-270">Style</span><span class="sxs-lookup"><span data-stu-id="33ea4-270">Style</span></span> | <span data-ttu-id="33ea4-271">Exemple</span><span class="sxs-lookup"><span data-stu-id="33ea4-271">Example</span></span> | <span data-ttu-id="33ea4-272">HTML</span><span class="sxs-lookup"><span data-stu-id="33ea4-272">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33ea4-273">Gras</span><span class="sxs-lookup"><span data-stu-id="33ea4-273">Bold</span></span> | <span data-ttu-id="33ea4-274">**text**</span><span class="sxs-lookup"><span data-stu-id="33ea4-274">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="33ea4-275">Italic</span><span class="sxs-lookup"><span data-stu-id="33ea4-275">Italic</span></span> | <span data-ttu-id="33ea4-276">*text*</span><span class="sxs-lookup"><span data-stu-id="33ea4-276">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="33ea4-277">En-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="33ea4-277">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="33ea4-278">**Texte**</span><span class="sxs-lookup"><span data-stu-id="33ea4-278">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="33ea4-279">Barré</span><span class="sxs-lookup"><span data-stu-id="33ea4-279">Strikethrough</span></span> | <span data-ttu-id="33ea4-280">~~text~~</span><span class="sxs-lookup"><span data-stu-id="33ea4-280">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="33ea4-281">Liste non triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-281">Unordered list</span></span> | <ul><li><span data-ttu-id="33ea4-282">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-282">text</span></span></li><li><span data-ttu-id="33ea4-283">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-283">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="33ea4-284">Liste triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-284">Ordered list</span></span> | <ol><li><span data-ttu-id="33ea4-285">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-285">text</span></span></li><li><span data-ttu-id="33ea4-286">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-286">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="33ea4-287">Texte préformaté</span><span class="sxs-lookup"><span data-stu-id="33ea4-287">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="33ea4-288">Blockquote</span><span class="sxs-lookup"><span data-stu-id="33ea4-288">Blockquote</span></span> | <blockquote><span data-ttu-id="33ea4-289">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-289">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="33ea4-290">Lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="33ea4-290">Hyperlink</span></span> | [<span data-ttu-id="33ea4-291">Bing</span><span class="sxs-lookup"><span data-stu-id="33ea4-291">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="33ea4-292">Lien vers l’image</span><span class="sxs-lookup"><span data-stu-id="33ea4-292">Image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="33ea4-293">Dans les cartes de connecteur, les nouvelles lignes sont restituer au format HTML à l’aide de la `<p>` balise.</span><span class="sxs-lookup"><span data-stu-id="33ea4-293">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="33ea4-294">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur</span><span class="sxs-lookup"><span data-stu-id="33ea4-294">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="33ea4-295">Sur le bureau, la mise en forme HTML pour les cartes de connecteur apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-295">On the desktop, HTML formatting for connector cards appears as shown in the following image:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="33ea4-297">Sur iOS, la mise en forme HTML apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-297">On iOS, HTML formatting appears as shown in the following image:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="33ea4-299">Les cartes de connecteur utilisant du code HTML pour iOS comportent les problèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="33ea4-299">Connector cards using HTML for iOS include the following issues:</span></span>

* <span data-ttu-id="33ea4-300">Les images en ligne ne sont pas restituer sur iOS à l’aide de Markdown ou html dans les cartes de connecteur.</span><span class="sxs-lookup"><span data-stu-id="33ea4-300">Inline images are not rendered on iOS using either Markdown or HTML in connector cards.</span></span>
* <span data-ttu-id="33ea4-301">Le texte préformaté est restituer, mais n’a pas d’arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="33ea4-301">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="33ea4-302">Sur Android, la mise en forme HTML apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-302">On Android, HTML formatting appears as shown in the following image:</span></span>

![Mise en forme HTML pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a><span data-ttu-id="33ea4-304">Exemple de format pour les cartes de connecteur HTML</span><span class="sxs-lookup"><span data-stu-id="33ea4-304">Format sample for HTML connector cards</span></span>

<span data-ttu-id="33ea4-305">Le code suivant montre un exemple de mise en forme pour les cartes de connecteur HTML :</span><span class="sxs-lookup"><span data-stu-id="33ea4-305">The following code shows an example of formatting for HTML connector cards:</span></span>

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[<span data-ttu-id="33ea4-306">Format HTML pour les cartes hero et miniatures</span><span class="sxs-lookup"><span data-stu-id="33ea4-306">HTML format for hero and thumbnail cards</span></span>](#tab/simple-html)

<span data-ttu-id="33ea4-307">Les balises HTML sont pris en charge pour les cartes simples, telles que les cartes hero et miniatures.</span><span class="sxs-lookup"><span data-stu-id="33ea4-307">HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span> <span data-ttu-id="33ea4-308">Markdown n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="33ea4-308">Markdown is not supported.</span></span>

| <span data-ttu-id="33ea4-309">Style</span><span class="sxs-lookup"><span data-stu-id="33ea4-309">Style</span></span> | <span data-ttu-id="33ea4-310">Exemple</span><span class="sxs-lookup"><span data-stu-id="33ea4-310">Example</span></span> | <span data-ttu-id="33ea4-311">HTML</span><span class="sxs-lookup"><span data-stu-id="33ea4-311">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33ea4-312">Gras</span><span class="sxs-lookup"><span data-stu-id="33ea4-312">Bold</span></span> | <span data-ttu-id="33ea4-313">**text**</span><span class="sxs-lookup"><span data-stu-id="33ea4-313">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="33ea4-314">Italic</span><span class="sxs-lookup"><span data-stu-id="33ea4-314">Italic</span></span> | <span data-ttu-id="33ea4-315">*text*</span><span class="sxs-lookup"><span data-stu-id="33ea4-315">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="33ea4-316">En-tête (niveaux 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="33ea4-316">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="33ea4-317">**Texte**</span><span class="sxs-lookup"><span data-stu-id="33ea4-317">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="33ea4-318">Barré</span><span class="sxs-lookup"><span data-stu-id="33ea4-318">Strikethrough</span></span> | <span data-ttu-id="33ea4-319">~~text~~</span><span class="sxs-lookup"><span data-stu-id="33ea4-319">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="33ea4-320">Liste non triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-320">Unordered list</span></span> | <ul><li><span data-ttu-id="33ea4-321">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-321">text</span></span></li><li><span data-ttu-id="33ea4-322">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-322">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="33ea4-323">Liste triée</span><span class="sxs-lookup"><span data-stu-id="33ea4-323">Ordered list</span></span> | <ol><li><span data-ttu-id="33ea4-324">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-324">text</span></span></li><li><span data-ttu-id="33ea4-325">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-325">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="33ea4-326">Texte préformaté</span><span class="sxs-lookup"><span data-stu-id="33ea4-326">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="33ea4-327">Blockquote</span><span class="sxs-lookup"><span data-stu-id="33ea4-327">Blockquote</span></span> | <blockquote><span data-ttu-id="33ea4-328">text</span><span class="sxs-lookup"><span data-stu-id="33ea4-328">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="33ea4-329">Lien hypertexte</span><span class="sxs-lookup"><span data-stu-id="33ea4-329">Hyperlink</span></span> | [<span data-ttu-id="33ea4-330">Bing</span><span class="sxs-lookup"><span data-stu-id="33ea4-330">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="33ea4-331">Lien vers l’image</span><span class="sxs-lookup"><span data-stu-id="33ea4-331">Image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="33ea4-332">Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="33ea4-332">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="33ea4-333">Comme il existe des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de Teams.</span><span class="sxs-lookup"><span data-stu-id="33ea4-333">As there are resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="33ea4-334">Sur le bureau, la mise en forme HTML apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-334">On the desktop, HTML formatting appears as shown in the following image:</span></span>

![Mise en forme HTML dans le client de bureau](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="33ea4-336">Sur iOS, la mise en forme HTML apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-336">On iOS, HTML formatting appears as shown in the following image:</span></span>

![Mise en forme HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="33ea4-338">La mise en forme des caractères, telle que le gras et l’italique, n’est pas restituer sur iOS.</span><span class="sxs-lookup"><span data-stu-id="33ea4-338">Character formatting, such as bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="33ea4-339">Sur Android, la mise en forme HTML apparaît comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-339">On Android, HTML formatting appears as shown in the following image:</span></span>

![Mise en forme HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="33ea4-341">Mise en forme des caractères, telle que l’affichage en gras et en italique sur Android.</span><span class="sxs-lookup"><span data-stu-id="33ea4-341">Character formatting, such as bold and italic display correctly on Android.</span></span>

### <a name="format-example-for-simple-cards"></a><span data-ttu-id="33ea4-342">Exemple de format pour les cartes simples</span><span class="sxs-lookup"><span data-stu-id="33ea4-342">Format example for simple cards</span></span>

<span data-ttu-id="33ea4-343">Les images de la section précédente ont été créées à l’Teams **App Studio**, où la propriété de texte d’une carte Hero est définie sur la chaîne suivante :</span><span class="sxs-lookup"><span data-stu-id="33ea4-343">The images in the previous section were created using Teams **App Studio**, where the text property of a hero card is set to the following string:</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

<span data-ttu-id="33ea4-344">Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.</span><span class="sxs-lookup"><span data-stu-id="33ea4-344">You can test formatting in your own cards by modifying this code.</span></span>

---

## <a name="see-also"></a><span data-ttu-id="33ea4-345">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="33ea4-345">See also</span></span>

* [<span data-ttu-id="33ea4-346">Actions de carte</span><span class="sxs-lookup"><span data-stu-id="33ea4-346">Card actions</span></span>](./cards-actions.md)
* [<span data-ttu-id="33ea4-347">Modules de tâche</span><span class="sxs-lookup"><span data-stu-id="33ea4-347">Task modules</span></span>](~/task-modules-and-cards/cards/cards-format.md)
