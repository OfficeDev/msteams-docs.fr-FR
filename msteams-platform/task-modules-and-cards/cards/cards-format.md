---
title: Mise en forme du texte dans les cartes
description: Décrit la mise en forme du texte de la carte dans Microsoft Teams
keywords: Format de cartes de bots teams
ms.date: 03/29/2018
ms.openlocfilehash: d7016f8b954e885221c55bd6c29309fd90a1dcfc
ms.sourcegitcommit: d41da0b608327829b902aded6bc85c0d0016d068
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "51474998"
---
# <a name="format-cards-in-teams"></a>Mise en forme des cartes dans Teams

Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de Markdown ou html, en fonction du type de carte.

Les cartes ne supportent la mise en forme que dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre. La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de mise en forme XML (HTML) ou markdown en fonction du type de carte. Pour le développement actuel et le développement de cartes adaptatives utilisant la mise en forme Markdown est recommandé.

La prise en charge de la mise en forme diffère d’un type de carte à l’autre, et le rendu de la carte peut légèrement varier entre le bureau et les clients Teams mobiles, ainsi que Teams dans le navigateur de bureau.

Vous pouvez inclure une image inline avec n’importe quelle carte Teams. Images au format , ou fichiers, qui ne doivent pas dépasser  `.png` `.jpg` `.gif` 1 024 × 1 024 px ou 1 Mo. L’image GIF animée n’est pas officiellement prise en charge. *Voir la référence* [des cartes](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Mise en forme de cartes avec Markdown

Il existe deux types de cartes qui prisent en charge Markdown dans Teams :

> [!div class="checklist"]
> * **Cartes adaptatives**: Markdown est pris en charge dans le champ de carte `Textblock` adaptative, ainsi que dans `Fact.Title` `Fact.Value` . Le code HTML n’est pas pris en charge dans les cartes adaptatives.
> * **Cartes de connecteur O365**: Markdown et HTML limité sont pris en charge dans les cartes de connecteur Office 365 dans les champs de texte.

# <a name="markdown-formatting-adaptive-cards"></a>[**Mise en forme Markdown : cartes adaptatives**](#tab/adaptive-md)

 Les styles pris en charge `Textblock` pour et `Fact.Title` sont `Fact.Value` :

| Style | Exemple | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| liste non réordée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| liste ordered | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Liens hypertexte |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Les balises Markdown suivantes ne sont pas pris en charge :

* En-têtes
* Tableaux
* Des images
* Texte préformaté
* Blockquotes

> [!IMPORTANT]
> Les cartes adaptatives ne sont pas adaptées à la mise en forme HTML.

### <a name="newlines-for-adaptive-cards"></a>Nouvelles lignes pour les cartes adaptatives

Dans les listes, vous pouvez utiliser les `\r` `\n` séquences d’échappatoire pour les nouvelles lignes. L’utilisation dans une liste entraîne le retrait de l’élément suivant de `\n\n` la liste. Si vous avez besoin de nouvelles lignes ailleurs dans le textblock, utilisez `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes adaptatives

La mise en forme est légèrement différente entre le bureau et les versions mobiles de Teams.

Sur le bureau, la mise en forme Markdown de carte adaptative s’affiche comme ceci dans les navigateurs web et dans l’application cliente Teams :

![Mise en forme Markdown de carte adaptative dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

Sur iOS, la mise en forme Markdown de carte adaptative s’affiche comme ceci :

![Mise en forme Markdown de carte adaptative dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Sur Android, la mise en forme Markdown de carte adaptative s’affiche comme ceci :

![Mise en forme Markdown de carte adaptative dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Plus d’informations sur les cartes adaptatives

[Fonctionnalités de texte dans les cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans cette rubrique ne sont pas pris en charge dans Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Exemple de mise en forme pour les cartes adaptatives

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

### <a name="mention-support-within-adaptive-cards-v12"></a>Prise en charge des mentions dans les cartes adaptatives v1.2

Les mentions basées sur une carte sont pris en charge dans les clients web, de bureau et mobiles. Vous pouvez ajouter des mentions @ dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie.  Pour ajouter des mentions @ dans les cartes, suivez la même logique de notification et le même rendu que celle des [mentions basées](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )sur les messages dans les conversations de canal et de groupe.

Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la carte dans les éléments [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet.](https://adaptivecards.io/explorer/FactSet.html)

> [!NOTE]
> * [Les éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptatives v1.2 sur la plateforme Teams.
> * Les mentions &'équipe de canal ne sont pas pris en charge dans les messages de bot.

#### <a name="constructing-mentions"></a>Construction de mentions

Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :

* `<at>username</at>` dans les éléments de carte adaptative pris en charge
* `mention`L’objet à l’intérieur d’une propriété dans le contenu de la carte, qui inclut l’ID d’utilisateur `msteams` Teams de l’utilisateur mentionné

#### <a name="sample-adaptive-card-with-a-mention"></a>Exemple de carte adaptative avec une mention

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
Utilisez la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs au sein de l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de carte adaptative. 

> [!NOTE]
> La fonctionnalité prend uniquement en charge le masquage d’informations côté client, le texte d’entrée masqué est envoyé en tant que texte clair à l’adresse de point de terminaison https spécifiée lors de la [configuration du bot.](../../build-your-first-app/build-bot.md#4-configure-your-bot) 

> [!NOTE]
> La propriété de masquage d’informations est actuellement disponible dans l’aperçu développeur uniquement.

Pour masquer les informations dans les cartes adaptatives, ajoutez la propriété à taper et définissez `isMasked` sa valeur sur  `Input.Text` *true*.

#### <a name="sample-adaptive-card-with-masking-property"></a>Exemple de carte adaptative avec propriété de masquage

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

L’image suivante est un exemple de masquage d’informations dans les cartes adaptatives :

![Image d’informations de masquage](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Carte adaptative pleine largeur
Vous pouvez utiliser la propriété pour développer la largeur d’une carte adaptative et `msteams` utiliser de l’espace de dessin supplémentaire. Pour plus d’informations sur l’utilisation de la propriété, voir l’exemple suivant :

#### <a name="constructing-full-width-cards"></a>Construction de cartes pleine largeur
Pour créer une carte adaptative pleine largeur, l’objet dans la propriété dans le contenu de la carte `width` doit être définie sur `msteams` `Full` .
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

Une carte adaptative pleine largeur apparaît comme suit : affichage Carte ![ adaptative pleine largeur](../../assets/images/cards/full-width-adaptive-card.png)

Si vous n’avez pas donné la valeur Full à la propriété, l’affichage par défaut de la carte adaptative est le suivant : affichage Carte adaptative à petite `width`  ![ largeur](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Prise en charge de Typeahead

Dans l’élément de schéma, le fait de demander aux utilisateurs de filtrer et de sélectionner un nombre important de choix peut ralentir considérablement l’exécution [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de la tâche. La prise en charge de la tête de type dans les cartes adaptatives peut simplifier la sélection des entrées en axant ou en filtrant l’ensemble des choix d’entrée quand un utilisateur tape l’entrée. 

#### <a name="enable-typeahead-in-adaptive-cards"></a>Activer typeahead dans les cartes adaptatives

Pour activer typeahead dans `Input.Choiceset` l’ensemble `style` et vérifier `filtered` `isMultiSelect` qu’il est définie sur `false` . 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Exemple de carte adaptative avec prise en charge de typeahead

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Vue d’étape des images dans les cartes adaptatives

> [!NOTE]
> Cette fonctionnalité est actuellement disponible en prévisualisation pour les développeurs uniquement.
 
Dans une carte adaptative, vous pouvez utiliser la propriété pour ajouter la possibilité d’afficher des images en vue de la `msteams` scène de manière sélective. Lorsque les utilisateurs pointent sur les images, ils voient une icône développer, pour laquelle l’attribut `allowExpand` est définie sur `true` . Pour plus d’informations sur l’utilisation de la propriété, voir l’exemple suivant :

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

Lorsque les utilisateurs pointent sur l’image, une icône développer s’affiche dans le coin supérieur droit de l’image : carte adaptative ![ avec image expandable](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

L’image s’affiche en vue de la phase lorsque l’utilisateur sélectionne le bouton développer : ![ Image étendue en vue de la phase](../../assets/images/cards/adaptivecard-expand-image.png)

Dans la vue d’étape, les utilisateurs peuvent effectuer un zoom avant et un zoom arrière sur l’image. Vous pouvez sélectionner les images de votre carte adaptative qui doivent avoir cette fonctionnalité.

> [!NOTE]
> Les fonctionnalités de zoom avant et arrière s’appliquent uniquement aux éléments image (type d’image) dans une carte adaptative.

> [!NOTE]
> Pour les applications mobiles Teams, les fonctionnalités d’affichage de phase pour les images dans les cartes adaptatives sont disponibles par défaut et les utilisateurs pourront afficher des images de carte adaptative en mode étape en appuyant simplement sur l’image, que l’attribut soit présent ou `allowExpand` non.

# <a name="markdown-formatting-o365-connector-cards"></a>[**Mise en forme Markdown : cartes de connecteur O365**](#tab/connector-md)

Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML. La prise en charge HTML est décrite dans la dernière section.

| Style | Exemple | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| en-tête (niveaux 1 &ndash; 3) | **Texte** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| liste non réordée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| liste ordered | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| texte préformaté | `text` | ``preformatted text`` |
| blockquote | >blockquote | `>blockquote text` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| lien vers l’image |![Canet sur une bascule](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

Dans les cartes de connecteur, les nouvelles lignes sont restituer `\n\n` pour , mais pas pour ou `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur à l’aide de Markdown

Sur le bureau, la mise en forme Markdown pour les cartes de connecteur ressemble à ceci :

![Mise en forme Markdown pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/connector-desktop-markdown-combined.png)

Sur iOS, la mise en forme Markdown pour les cartes de connecteur ressemble à ceci :

![Mise en forme Markdown pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Problèmes :

* Le client iOS pour Teams ne restituera pas les images en ligne Markdown ou HTML dans les cartes de connecteur.
* Les blockquotes sont restituer en retrait, mais sans arrière-plan gris.

Sur Android, la mise en forme Markdown pour les cartes de connecteur ressemble à ceci :

![Mise en forme Markdown pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Exemple de mise en forme pour les cartes de connecteur Markdown

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

## <a name="formatting-cards-with-html"></a>Mise en forme de cartes au format HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Mise en forme HTML : cartes de connecteur O365**](#tab/connector-html)

Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML. Markdown est décrit dans la section suivante.

| Style | Exemple | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| en-tête (niveaux 1 &ndash; 3) | **Texte** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| liste non réordée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| liste ordered | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| lien vers l’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

Dans les cartes de connecteur, les nouvelles lignes sont restituer au format HTML à l’aide de la `<p>` balise.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur utilisant du code HTML

Sur le bureau, la mise en forme HTML pour les cartes de connecteur ressemble à ceci :

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/Connector-desktop-html-combined.png)

Sur iOS, la mise en forme HTML ressemble à ceci :

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Problèmes :

* Les images en ligne ne sont pas restituer sur iOS à l’aide de Markdown ou html dans les cartes de connecteur.
* Le texte préformaté est restituer, mais n’a pas d’arrière-plan gris.

Sur Android, la mise en forme HTML ressemble à ceci :

![Mise en forme HTML pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Exemple de mise en forme pour les cartes de connecteur HTML

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**Mise en forme HTML : cartes hero et miniatures**](#tab/simple-html)

Les balises HTML sont pris en charge pour les cartes simples telles que la carte hero et la carte miniature. Markdown n’est pas pris en charge.

| Style | Exemple | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| en-tête (niveaux 1 &ndash; 3) | **Texte** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| liste non réordée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| liste ordered | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| lien vers l’image |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes simples

En raison des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de Teams.

Sur le bureau, la mise en forme HTML s’affiche comme ceci :

![Mise en forme HTML dans le client de bureau](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

Sur iOS, la mise en forme HTML s’affiche comme ceci :

![Mise en forme HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Problèmes :

* La mise en forme de caractères en gras et en italique n’est pas restituer sur iOS.

Sur Android, la mise en forme HTML s’affiche comme ceci :

![Mise en forme HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

La mise en forme des caractères comme gras et italique s’affiche correctement sur Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Exemple de mise en forme pour la mise en forme HTML dans des cartes simples

Ces captures d’écran ont été créées à l’aide de Teams AppStudio, où la propriété de texte d’une carte Hero a été définie sur la chaîne suivante. Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
