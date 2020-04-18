---
title: Mise en forme de texte dans les cartes
description: Décrit la mise en forme de texte de carte dans Microsoft teams
keywords: format des cartes robots teams
ms.date: 03/29/2018
ms.openlocfilehash: 9ced8a8956265322e91b9d40dc7dc7064ee4659f
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550951"
---
# <a name="format-cards-in-teams"></a>Cartes de format dans teams

Vous pouvez ajouter une mise en forme de texte enrichi à vos cartes à l’aide de la démarque ou du code HTML, selon le type de carte.

Les cartes prennent en charge la mise en forme uniquement dans la propriété Text, pas dans les propriétés Title ou title. La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de la mise en forme XML (HTML) ou de la démarque selon le type de carte. Pour les cartes adaptatives de développement actuelles et futures, il est recommandé d’utiliser la mise en forme de démarque.

La prise en charge de la mise en forme diffère selon les types de carte et le rendu de la carte peut légèrement varier entre le bureau et les clients teams mobiles, ainsi que teams dans le navigateur de bureau.

Vous pouvez inclure une image incluse avec n’importe quelle carte Teams. Images un format `.png`, `.jpg`ou `.gif` des fichiers, ne doit pas dépasser 1024 × 1024 PX ou 1 Mo. L’image GIF animée n’est pas officiellement prise en charge. *Voir* [référence des fiches](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Mise en forme de cartes avec démarque

Il existe deux types de cartes qui prennent en charge la démarque dans teams :

> [!div class="checklist"]
> * **Cartes adaptatives**: la démarque est prise en charge `Textblock` dans le champ carte adaptative `Fact.Title` , `Fact.Value`ainsi que et. HTML n’est pas pris en charge dans les cartes adaptatives.
> * **Cartes de connecteur O365**: la démarque et le code html limité sont pris en charge dans les cartes de connecteur Office 365 dans les champs de texte.

# <a name="markdown-formatting-adaptive-cards"></a>[**Mise en forme des démarques : cartes adaptatives**](#tab/adaptive-md)

 Les styles pris en `Textblock`charge `Fact.Title` pour `Fact.Value` et sont les suivants :

| Style | Exemple | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| liste non triée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| liste triée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Liens hypertexte |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Les balises de démarques suivantes ne sont pas prises en charge :

* En-têtes
* Tables
* Des images
* Texte déjà mis en forme
* Blockquotes

> [!IMPORTANT]
> Les cartes adaptatives ne prennent pas en charge la mise en forme HTML.

### <a name="newlines-for-adaptive-cards"></a>Nouvelles lignes de cartes adaptatives

Dans les listes, vous pouvez `\r` utiliser `\n` les séquences d’échappement ou pour les nouvelles lignes. L' `\n\n` utilisation d’une liste entraîne le retrait de l’élément suivant dans la liste. Si vous avez besoin de nouvelles lignes ailleurs dans TextBlock `\n\n`, utilisez.

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Différences entre les appareils mobiles et de bureau pour les cartes adaptatives

La mise en forme diffère légèrement entre le bureau et les versions mobiles de teams.

Sur le bureau, le format des démarques de carte adaptative apparaît comme dans les navigateurs Web et dans l’application cliente teams :

![Mise en forme adaptative de la démarque de carte dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

Sous iOS, la mise en forme adaptative de carte de visite apparaît comme suit :

![Mise en forme adaptative de la démarque de carte dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Sous Android, la mise en forme de la démarque de carte adaptative apparaît comme suit :

![Mise en forme adaptative de la démarque de carte dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>Plus d’informations sur les cartes adaptatives

[Fonctionnalités de texte dans des cartes adaptatives](/adaptive-cards/create/textfeatures) Les fonctionnalités de date et de localisation mentionnées dans cette rubrique ne sont pas prises en charge dans Teams.

### <a name="formatting-sample-for-adaptive-cards"></a>Exemple de mise en forme des cartes adaptatives

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

### <a name="mention-support-within-adaptive-cards"></a>Mentionner la prise en charge dans les cartes adaptatives

> [!NOTE]
> Mentionner la prise en charge des cartes est actuellement prise en charge en version préliminaire pour les [développeurs](../../resources/dev-preview/developer-preview-intro.md) .

Les robots et les extensions de messagerie peuvent désormais inclure des mentions dans le contenu des cartes dans les éléments bloc de texte et FactSet.

### <a name="constructing-mentions"></a>Création de mentions

Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants

* `<at>username</at>`dans les éléments de carte adaptative pris en charge
* `mention` Objet à l’intérieur d' `msteams` une propriété dans le contenu de la carte, qui inclut l’ID utilisateur teams de l’utilisateur mentionné

Notez que les cartes avec des mentions ne sont pas prises en charge sur les clients mobiles pour le moment.

### <a name="sample-adaptive-card-with-a-mention"></a>Exemple de carte adaptative avec une mention

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

# <a name="markdown-formatting-o365-connector-cards"></a>[**Mise en forme des démarques : cartes de connecteur O365**](#tab/connector-md)

Les cartes de connecteur prennent en charge la démarque limitée et la mise en forme HTML. La prise en charge du langage HTML est décrite dans la dernière section.

| Style | Exemple | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| en-tête (&ndash;niveaux 1 à 3) | **Texte** | `### Text`|
| doubles | ~~text~~ | `~~text~~` |
| liste non triée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| liste triée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| texte déjà mis en forme | `text` | ``preformatted text`` |
| blockquote | Texte >BLOCKQUOTE | `>blockquote text` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| lien de l’image |![Canard sur une roche](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

Dans les cartes de connecteur, les nouvelles `\n\n`lignes sont affichées pour `\n` , `\r`mais pas pour ou.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Différences de bureau et de téléphone pour les cartes de connecteur utilisant la démarque

Sur le bureau, la mise en forme de démarque pour les cartes de connecteur se présente comme suit :

![Mise en forme des démarques pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/connector-desktop-markdown-combined.png)

Sur iOS, la mise en forme de démarque pour les cartes de connecteur se présente comme suit :

![Mise en forme des démarques pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Problèmes :

* Le client iOS pour Teams ne restitue pas les images insérées de démarque ou HTML dans les cartes de connecteur.
* Les blockquotes sont affichés sous forme de retrait, mais sans arrière-plan gris.

Sur Android, la mise en forme des démarques pour les cartes de connecteur se présente comme suit :

![Mise en forme des démarques pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Exemple de mise en forme pour les fiches de connecteur de démarque

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

## <a name="formatting-cards-with-html"></a>Mise en forme de cartes avec HTML

# <a name="html-formatting-o365-connector-cards"></a>[**Mise en forme HTML : cartes de connecteur O365**](#tab/connector-html)

Les cartes de connecteur prennent en charge la démarque limitée et la mise en forme HTML. La démarque est décrite dans la section suivante.

| Style | Exemple | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| en-tête (&ndash;niveaux 1 à 3) | **Texte** | `<h3>Text</h3>` |
| doubles | ~~text~~ | `<strike>text</strike>` |
| liste non triée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| liste triée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texte déjà mis en forme | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| lien de l’image | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

Dans les cartes de connecteur, les nouvelles lignes sont affichées `<p>` en HTML à l’aide de la balise.

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>Différences entre les appareils mobiles et de bureau pour les cartes de connecteur à l’aide de HTML

Sur le bureau, la mise en forme HTML des cartes de connecteur se présente comme suit :

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/Connector-desktop-html-combined.png)

Sur iOS, la mise en forme HTML se présente comme suit :

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Problèmes :

* Les images en ligne ne sont pas rendues sur iOS à l’aide de la démarque ou du code HTML dans les cartes de connecteur.
* Le texte préformaté est affiché, mais il n’a pas d’arrière-plan gris.

Sur Android, la mise en forme HTML se présente comme suit :

![Mise en forme HTML pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>Exemple de mise en forme des cartes de connecteur HTML

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**Mise en forme HTML : cartes de héros et miniatures**](#tab/simple-html)

Les balises HTML sont prises en charge pour les cartes simples telles que le héros et la carte miniature. La démarque n’est pas prise en charge.

| Style | Exemple | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| en-tête (&ndash;niveaux 1 à 3) | **Texte** | `<h3>Text</h3>` |
| doubles | ~~text~~ | `<strike>text</strike>` |
| liste non triée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| liste triée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| texte déjà mis en forme | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| lien de l’image |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Différences entre les appareils mobiles et de bureau pour les cartes simples

En raison des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de teams.

Sur le bureau, la mise en forme HTML se présente comme suit :

![Mise en forme HTML dans le client de bureau](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

Sous iOS, la mise en forme HTML se présente comme suit :

![Mise en forme HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

Problèmes :

* La mise en forme des caractères, comme gras et italique, n’est pas restituée sur iOS.

Sous Android, la mise en forme HTML se présente comme suit :

![Mise en forme HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

La mise en forme des caractères comme gras et italique s’affiche correctement sur Android.

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>Exemple de mise en forme pour la mise en forme HTML dans les cartes simples

Ces captures d’écran ont été créées à l’aide de teams AppStudio, où la propriété Text d’une carte héros a été définie sur la chaîne suivante. Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
