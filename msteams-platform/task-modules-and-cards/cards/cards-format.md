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
# <a name="format-cards-in-teams"></a>Cartes formatées en Teams

Vous pouvez ajouter un formatage de texte riche à vos cartes en utilisant markdown ou HTML, selon le type de carte.

Les cartes supportent le formatage dans la propriété de texte seulement, pas dans les propriétés de titre ou de sous-titre. Le formatage peut être spécifié à l’aide d’un sous-ensemble de formatage XML (HTML) ou markdown selon le type de carte. Pour le développement actuel et futur, il est recommandé d’utiliser des cartes adaptatives utilisant le formatage Markdown.

Le formatage de la prise en charge diffère d’un type de carte à l’autre, et le rendu de la carte peut différer légèrement entre le bureau et les clients de Teams mobiles, ainsi que les Teams dans le navigateur de bureau.

Vous pouvez inclure une image en ligne avec n’importe quelle Teams carte. Images un être formaté comme  `.png` , ou des fichiers et ne doit pas dépasser `.jpg` `.gif` 1024 ×1024 px ou 1 Mo. Gif animé n’est pas officiellement pris en charge. Pour plus d’informations, voir [référence Cartes](./cards-reference.md#inline-card-images).

## <a name="formatting-cards-with-markdown"></a>Formater les cartes avec Markdown

Il existe deux types de cartes qui soutiennent Markdown dans Teams :

> [!div class="checklist"]
> * **Cartes adaptatives**: Markdown est pris en charge dans le `Textblock` champ de carte adaptative, ainsi `Fact.Title` que `Fact.Value` . Html n’est pas pris en charge dans les cartes adaptatives.
> * **Cartes connecteur O365**: Markdown et HTML limité sont pris en charge dans Office 365 cartes Connecteur dans les champs de texte.

# <a name="markdown-formatting-adaptive-cards"></a>[**Mise en forme Markdown : Cartes adaptatives**](#tab/adaptive-md)

 Les styles pris en charge `Textblock` pour , `Fact.Title` et `Fact.Value` sont:

| Style | Exemple | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| liste non ordonnée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| liste commandée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Liens hypertexte |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Les balises Markdown suivantes ne sont pas prises en charge :

* En-têtes
* Tables
* Des images
* Texte préformaté
* Blockquotes Blockquotes

> [!IMPORTANT]
> Les cartes adaptatives ne supportent pas le formatage HTML.

### <a name="newlines-for-adaptive-cards"></a>Nouvelles lignes pour cartes adaptatives

Dans les listes, vous pouvez utiliser `\r` les séquences ou les séquences `\n` d’évasion pour les nouvelles lignes. `\n\n`L’utilisation dans une liste provoquera l’indented du prochain élément de la liste. Si vous avez besoin de nouvelles lignes ailleurs dans le bloc de texte, utilisez `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Différences mobiles et de bureau pour les cartes adaptatives

Le formatage est légèrement différent entre le bureau et les versions mobiles de Teams.

Sur le bureau, le formatage markdown de carte adaptative apparaît ainsi dans les navigateurs Web et dans l’application Teams client :

![Formatage markdown de carte adaptative dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

Sur iOS, le formatage markdown de la carte adaptative apparaît comme ceci :

![Formatage markdown de carte adaptative dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Sur Android, le formatage adaptatif de Markdown de carte apparaît comme ceci :

![Carte adaptative Markdown formatage dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Plus d’informations sur les cartes adaptatives

[Fonctionnalités textuelles dans les cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans ce sujet ne sont pas prises en charge Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Exemple de mise en forme des cartes adaptatives

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

### <a name="mention-support-within-adaptive-cards-v12"></a>Mention de support dans les cartes adaptatives v1.2

Les mentions basées sur la carte sont prises en charge dans les clients web, bureau et mobiles. Vous pouvez ajouter @ mentions dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie. Pour ajouter @ mentions dans les cartes, suivez la même logique de notification et de rendu que celle des mentions basées sur les [messages dans les conversations de chat de canal et de groupe](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).

Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la [carte dans les éléments TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet.](https://adaptivecards.io/explorer/FactSet.html)

> [!NOTE]
> * [Les éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptatives v1.2 sur la Teams plateforme.
> * Les mentions &'équipe ne sont pas prises en charge dans les messages bot.

#### <a name="constructing-mentions"></a>Construction de mentions

Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :

* `<at>username</at>` dans les éléments de carte adaptatif pris en charge.
* `mention`L’objet à l’intérieur `msteams` d’une propriété dans le contenu de la carte, qui inclut Teams id utilisateur de l’utilisateur mentionné.
* Le `userId` est unique à votre id bot et un utilisateur particulier. Il peut être utilisé pour @mention un utilisateur particulier. Le `userId` peut être récupéré en utilisant l’une des options mentionnées pour obtenir [l’iD de l’utilisateur](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Exemple de carte adaptative avec mention

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

### <a name="information-masking-in-adaptive-cards"></a>Masquage d’informations dans les cartes adaptatives
Utilisez la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs dans l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de la carte Adaptative. 

> [!NOTE]
> La fonctionnalité prend en charge uniquement le masquage des informations secondaires du client, le texte d’entrée masqué est envoyé sous forme de texte clair à l’adresse de point de terminaison https qui a été spécifiée lors de [la configuration du bot.](../../build-your-first-app/build-bot.md) 

> [!NOTE]
> La propriété de masquage d’informations est actuellement disponible dans l’aperçu développeur seulement.

Pour masquer les informations contenues dans les cartes `isMasked` adaptatives, ajoutez **la propriété au type** et `Input.Text` réglez sa valeur à la *réalité.*

#### <a name="sample-adaptive-card-with-masking-property"></a>Exemple carte adaptative avec propriété de masquage

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

L’image suivante est un exemple d’information masquante dans les cartes adaptatives :

![Image d’information de masquage](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Carte adaptative pleine largeur
Vous pouvez utiliser la propriété `msteams` pour élargir la largeur d’une carte adaptative et utiliser de l’espace de toile supplémentaire. Pour plus d’informations sur la façon d’utiliser la propriété, voir l’exemple suivant :

#### <a name="constructing-full-width-cards"></a>Construction de cartes pleine largeur
Pour faire une carte adaptative pleine largeur, `width` l’objet `msteams` dans la propriété dans le contenu de la carte doit être réglé sur `Full` .
En outre, votre application doit inclure les éléments suivants :

#### <a name="sample-adaptive-card-with-full-width"></a>Exemple de carte adaptative avec pleine largeur

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

Une carte adaptative pleine largeur apparaît comme suit : ![ Vue de la carte adaptative pleine largeur](../../assets/images/cards/full-width-adaptive-card.png)

Si vous n’avez pas défini `width` la propriété à *plein*, alors la vue par défaut de la carte adaptative est la suivante: ![ Petite largeur Vue de carte adaptative](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Soutien typeahead

Dans [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) l’élément schéma, demander aux utilisateurs de filtrer à travers et de sélectionner à travers un nombre important de choix peut ralentir considérablement l’achèvement des tâches. La prise en charge typeahead dans les cartes adaptatives peut simplifier la sélection des entrées en rétrécissant ou en filtrant l’ensemble des choix d’entrée s’il tape l’entrée. 

#### <a name="enable-typeahead-in-adaptive-cards"></a>Activer typeahead dans les cartes adaptatives

Pour activer typeahead dans `Input.Choiceset` l’ensemble `style` et `filtered` s’assurer `isMultiSelect` est réglé sur `false` . 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Exemple de carte adaptative avec prise en charge typeahead

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Vue scénique pour les images dans cartes adaptatives

> [!NOTE]
> Cette fonctionnalité est actuellement disponible en aperçu développeur uniquement.
 
Dans une carte adaptative, vous pouvez utiliser la propriété `msteams` pour ajouter la possibilité d’afficher des images en vue de scène de manière sélective. Lorsque les utilisateurs planent au-dessus des images, ils voient une icône d’expansion, pour laquelle `allowExpand` l’attribut est défini à `true` . Pour plus d’informations sur la façon d’utiliser la propriété, voir l’exemple suivant :

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

Lorsque les utilisateurs planent au-dessus de l’image, une icône d’expansion apparaît en haut à droite de l’image : ![ carte adaptative avec image extensible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

L’image apparaît dans la vue de scène lorsque l’utilisateur sélectionne le bouton d’expansion : ![ Image étendue à la vue de scène](../../assets/images/cards/adaptivecard-expand-image.png)

Dans la vue scène, les utilisateurs peuvent zoomer et zoomer sur l’image. Vous pouvez sélectionner les images de votre carte Adaptative qui doivent avoir cette capacité.

> [!NOTE]
> La capacité de zoom avant et de zoom arrière ne s’applique qu’aux éléments d’image (type d’image) d’une carte adaptative.

> [!NOTE]
> Pour les applications mobiles Teams, les fonctionnalités de vue scénique pour les images des cartes adaptatives sont disponibles par défaut et les utilisateurs pourront afficher des images de carte adaptative en vue de la scène en appuyant simplement sur l’image, que `allowExpand` l’attribut soit présent ou non.

# <a name="markdown-formatting-o365-connector-cards"></a>[**Mise en forme Markdown : Cartes connecteur O365**](#tab/connector-md)

Les cartes connecteurs supportent le formatage Markdown et HTML limité. Le support HTML est décrit dans la dernière section.

| Style | Exemple | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| en-tête (niveaux 1 &ndash; 3) | **Text** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| liste non ordonnée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| liste commandée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| texte préformaté | `text` | ``preformatted text`` |
| blockquote | >texte blockquote | `>blockquote text` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| lien d’image |![Canard sur une roche](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

Dans les cartes de connecteur, les nouvelles lignes sont rendues `\n\n` pour, mais pas pour `\n` ou `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Différences mobiles et de bureau pour les cartes de connecteur utilisant Markdown

Sur le bureau, le formatage Markdown pour les cartes de connecteur ressemble à ceci :

![Mise en forme Markdown pour les cartes de connecteur dans le client Desktop](../../assets/images/cards/connector-desktop-markdown-combined.png)

Sur iOS, le formatage Markdown pour les cartes connecteurs ressemble à ceci :

![Mise en forme Markdown pour les cartes connecteurs dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Problèmes :

* Le client iOS pour Teams rend pas markdown ou html images en ligne dans les cartes connecteur.
* Les blockquotes sont rendus en tant qu’indented mais sans fond gris.

Sur Android, le formatage Markdown pour les cartes connecteurs ressemble à ceci :

![Mise en forme Markdown pour les cartes connecteurs dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Exemple de formatage pour les cartes connecteur Markdown

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

## <a name="formatting-cards-with-html"></a>Formater les cartes avec HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Formatage HTML : Cartes connecteur O365**](#tab/connector-html)

Les cartes connecteurs supportent le formatage Markdown et HTML limité. Markdown est décrit dans la section suivante.

| Style | Exemple | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| en-tête (niveaux 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| liste non ordonnée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| liste commandée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| lien d’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

Dans les cartes de connecteur, les nouvelles lignes sont rendues en HTML à l’aide de `<p>` la balise.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Différences mobiles et de bureau pour les cartes de connecteur utilisant HTML

Sur le bureau, le formatage HTML pour les cartes de connecteur ressemble à ceci :

![Formatage HTML pour les cartes de connecteur dans le client Desktop](../../assets/images/cards/Connector-desktop-html-combined.png)

Sur iOS, le formatage HTML ressemble à ceci :

![Formatage HTML pour les cartes connecteurs dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Problèmes :

* Les images en ligne ne sont pas rendues sur iOS à l’aide de Markdown ou html dans les cartes connecteurs.
* Le texte préformaté est rendu mais n’a pas de fond gris.

Sur Android, le formatage HTML ressemble à ceci :

![Formatage HTML pour les cartes connecteurs dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Exemple de formatage pour les cartes connecteurs HTML

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**Formatage HTML : cartes héros et vignettes**](#tab/simple-html)

Les balises HTML sont prises en charge pour les cartes simples telles que le héros et la carte miniature. Markdown n’est pas pris en charge.

| Style | Exemple | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| en-tête (niveaux 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| liste non ordonnée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| liste commandée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| lien d’image |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Différences mobiles et de bureau pour les cartes simples

En raison des différences de résolution entre le bureau et la plate-forme mobile, le formatage est différent entre le bureau et la version mobile de Teams.

Sur le bureau, le formatage HTML apparaît comme ceci :

![Formatage HTML dans le client Desktop](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

Sur iOS, le formatage HTML apparaît comme ceci :

![Formatage HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Problèmes :

* Le formatage des caractères comme gras et italique n’est pas rendu sur iOS.

Sur Android, le formatage HTML apparaît comme ceci :

![Formatage HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Formatage de caractères comme affichage gras et italique correctement sur Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Exemple de formatage pour le formatage HTML en cartes simples

Ces captures d’écran ont été créées Teams appstudio, où la propriété textuelle d’une carte héros a été réglée sur la chaîne suivante. Vous pouvez tester le formatage dans vos propres cartes en modifiant ce code.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
