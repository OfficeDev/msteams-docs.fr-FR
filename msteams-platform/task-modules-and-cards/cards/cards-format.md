---
title: Mise en forme du texte dans les cartes
description: Décrit la mise en forme du texte de la carte Microsoft Teams
keywords: Format de cartes de bots teams
ms.localizationpriority: medium
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: 8afbd5f4904a378a4433965c128136fa8b39590d
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475809"
---
# <a name="format-cards-in-microsoft-teams"></a>Mettre en forme des cartes dans Microsoft Teams

Voici les deux façons d’ajouter une mise en forme de texte enrichi à vos cartes :
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

Les cartes ne supportent la mise en forme que dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre. La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de formats XML ou HTML ou Markdown, en fonction du type de carte. Pour le développement actuel et futur des cartes adaptatives, la mise en forme Markdown est recommandée.

La prise en charge de la mise en forme diffère d’un type de carte à l’autre. Le rendu de la carte peut légèrement varier entre le bureau et les clients Microsoft Teams mobiles, ainsi que Teams dans le navigateur de bureau.

Vous pouvez inclure une image inline avec n’importe Teams carte. Les images peuvent être formatées en tant que fichiers ou en tant que fichiers et ne doivent pas dépasser `.png` `.jpg` `.gif` 1 024 × 1 024 px ou 1 Mo. Gif animé non pris en charge. Pour plus d’informations, voir [les types de cartes.](./cards-reference.md#inline-card-images)

Vous pouvez formater des cartes adaptatives et Office 365 connecteur avec Markdown qui incluent certains styles pris en charge.

## <a name="format-cards-with-markdown"></a>Formater des cartes avec Markdown

Les types de carte suivants prise en charge la mise en forme Markdown dans Teams :

* Cartes adaptatives : Markdown est pris en charge dans le champ de carte `Textblock` adaptative, ainsi que dans `Fact.Title` `Fact.Value` . Le code HTML n’est pas pris en charge dans les cartes adaptatives.
* Office 365 Cartes de connecteur : markdown et html limité sont pris en charge Office 365 cartes de connecteur dans les champs de texte.

Vous pouvez utiliser des nouvelles lignes pour les cartes adaptatives à l’aide ou des `\r` `\n` séquences d’échappatoire pour les nouvelles lignes dans les listes. La mise en forme est différente entre le bureau et les versions mobiles de Teams pour les cartes adaptatives. Les mentions basées sur une carte sont pris en charge dans les clients web, de bureau et mobiles. Vous pouvez utiliser la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs au sein de l’élément d’entrée `Input.Text` de carte adaptative. Vous pouvez développer la largeur d’une carte adaptative à l’aide de `width` l’objet. Vous pouvez activer la prise en charge des en-têtes de type dans les cartes adaptatives et filtrer l’ensemble des choix d’entrée à mesure que l’utilisateur tape l’entrée. Vous pouvez utiliser la propriété pour ajouter la possibilité d’afficher des images en vue de la `msteams` scène de manière sélective.

La mise en forme est différente entre le bureau et les versions mobiles de Teams cartes adaptatives et cartes de connecteur. Dans cette section, vous pouvez passer par l’exemple de format Markdown pour les cartes adaptatives et les cartes de connecteur.

# <a name="markdown-format-for-adaptive-cards"></a>[Format Markdown pour les cartes adaptatives](#tab/adaptive-md)

 Le tableau suivant fournit les styles pris en charge `Textblock` pour `Fact.Title` , et `Fact.Value` :

| Style | Exemple | Markdown |
| --- | --- | --- |
| Gras | **Bold** | ```**Bold**``` |
| Italic | _Italic_ | ```_Italic_``` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Liens hypertexte |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Les balises Markdown suivantes ne sont pas pris en charge :

* En-têtes
* Tables
* Des images
* Texte préformaté
* Blockquotes

### <a name="newlines-for-adaptive-cards"></a>Nouvelles lignes pour les cartes adaptatives

Vous pouvez utiliser les `\r` `\n` séquences d’échappatoire ou les séquences d’échappatoire pour les nouvelles lignes dans les listes. L’utilisation dans les listes entraîne le retrait de l’élément suivant dans `\n\n` la liste. Si vous avez besoin de lignes nouvelles ailleurs dans le TextBlock, utilisez `\n\n` .

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes adaptatives

Sur le bureau, la mise en forme de markdown de carte adaptative apparaît comme illustré dans l’image suivante dans les navigateurs web et dans l Teams application cliente :

![Mise en forme Markdown de carte adaptative dans le client de bureau](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

Sur iOS, la mise en forme markdown de carte adaptative apparaît comme illustré dans l’image suivante :

![Mise en forme markdown de carte adaptative dans iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Sur Android, la mise en forme markdown de carte adaptative apparaît comme illustré dans l’image suivante :

![Mise en forme markdown de carte adaptative dans Android](../../assets/images/cards/Adaptive-markdown-Android.png)

Pour plus d’informations, voir [les fonctionnalités de texte dans les cartes adaptatives.](/adaptive-cards/create/textfeatures)

> [!NOTE]
> Les fonctionnalités de date et de localisation mentionnées dans cette section ne sont pas Teams.

### <a name="adaptive-cards-format-sample"></a>Exemple de format de cartes adaptatives

Le code suivant illustre un exemple de mise en forme des cartes adaptatives :

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

### <a name="mention-support-within-adaptive-cards"></a>Prise en charge des mentions dans les cartes adaptatives 

Vous pouvez ajouter des @mentions dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie. Pour ajouter @mentions cartes, suivez la même logique de notification et le même rendu que celui des [mentions basées](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)sur les messages dans les conversations de canal et de groupe.

Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la carte dans les éléments [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet.](https://adaptivecards.io/explorer/FactSet.html)

> [!NOTE]
> * [Les éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptatives Teams plateforme.
> * Les mentions de canal et d’équipe ne sont pas pris en charge dans les messages de bot.

Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :

* `<at>username</at>` dans les éléments de carte adaptative pris en charge.
* L’objet à l’intérieur d’une propriété dans le contenu de la carte inclut `mention` `msteams` l’ID Teams’utilisateur de l’utilisateur mentionné.
* Il `userId` est propre à votre ID de bot et à un utilisateur particulier. Il peut être utilisé pour @mention un utilisateur particulier. Il `userId` peut être récupéré à l’aide de l’une des options mentionnées dans obtenir [l’ID utilisateur.](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)

#### <a name="sample-adaptive-card-with-a-mention"></a>Exemple de carte adaptative avec une mention

Le code suivant montre un exemple de carte adaptative avec une mention :

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

### <a name="aad-object-id-and-upn-in-user-mention"></a>ID d’objet AAD et UPN dans la mention utilisateur 

Teams permet de mentionner les utilisateurs avec leur ID d’objet AAD et leur nom d’utilisateur principal (UPN), en plus des ID de mention existants. Les bots avec cartes adaptatives et connecteurs avec webhooks entrants supportent les deux ID de mention utilisateur. 

Le tableau suivant décrit les nouveaux ID de mention d’utilisateur pris en charge :

|ID  | Fonctionnalités de prise en charge |   Description | Exemple |
|----------|--------|---------------|---------|
| ID d’objet AAD | Bot, Connecteur |  ID d’objet de l’utilisateur AAD |  49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | Bot, Connecteur | UPN de l’utilisateur AAD | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>Mention d’utilisateur dans les bots avec cartes adaptatives 

Les bots peuvent prendre en charge la mention utilisateur avec l’ID d’objet AAD et l’UPN, en plus des ID existants. La prise en charge de deux nouveaux ID est disponible dans les bots pour les messages texte, le corps des cartes adaptatives et la réponse d’extension de messagerie. Les bots supportent les ID de mention dans les conversations et `invoke` les scénarios. L’utilisateur reçoit une notification de flux d'@mentioned avec les ID. 

> [!NOTE]
> La mise à jour du schéma et les modifications de l’interface utilisateur/expérience utilisateur ne sont pas requises pour les mentions utilisateur avec des cartes adaptatives dans bot.

##### <a name="example"></a>Exemple 

Exemple de mention d’utilisateur dans les bots avec cartes adaptatives comme suit :

```json 
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
    }
  ],
  "msteams": {
    "entities": [
      {
        "type": "mention",
        "text": "<at>Adele UPN</at>",
        "mentioned": {
          "id": "AdeleV@contoso.onmicrosoft.com",
          "name": "Adele Vance"
        }
      },
      {
        "type": "mention",
        "text": "<at>Adele AAD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

L’image suivante illustre la mention utilisateur avec carte adaptative dans bot :

![Mention d’utilisateur dans un bot avec carte adaptative](~/assets/images/authentication/user-mention-in-bot.png)

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>Mention d’utilisateur dans le webhook entrant avec cartes adaptatives 

Les webhooks entrants commencent à prendre en charge la mention utilisateur dans les cartes adaptatives avec l’ID d’objet AAD et l’UPN.

> [!NOTE]    
> * Activez la mention utilisateur dans le schéma pour les webhooks entrants afin de prendre en charge l’ID d’objet AAD et l’UPN. 
> * Les modifications de l’interface utilisateur/expérience utilisateur ne sont pas requises pour les mentions utilisateur avec l’ID d’objet AAD et l’UPN.      
> * La notification de flux d’activités pour le webhook entrant avec mention d’utilisateur sera disponible dans la prochaine version.

##### <a name="example"></a>Exemple 

Exemple de mention d’utilisateur dans le webhook entrant comme suit :

```json
{
    "type": "message",
    "attachments": [
        {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
            "type": "AdaptiveCard",
            "body": [
                {
                    "type": "TextBlock",
                    "size": "Medium",
                    "weight": "Bolder",
                    "text": "Sample Adaptive Card with User Mention"
                },
                {
                    "type": "TextBlock",
                    "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
                }
            ],
            "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
            "version": "1.0",
            "msteams": {
                "entities": [
                    {
                        "type": "mention",
                        "text": "<at>Adele UPN</at>",
                        "mentioned": {
                          "id": "AdeleV@contoso.onmicrosoft.com",
                          "name": "Adele Vance"
                        }
                      },
                      {
                        "type": "mention",
                        "text": "<at>Adele AAD</at>",
                        "mentioned": {
                          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
                          "name": "Adele Vance"
                        }
                      }
                ]
            }
        }
    }]
}
```

L’image suivante illustre la mention de l’utilisateur dans le webhook entrant :

![Mention d’utilisateur dans le webhook entrant](~/assets/images/authentication/user-mention-in-incoming-webhook.png)

### <a name="information-masking-in-adaptive-cards"></a>Masquage d’informations dans les cartes adaptatives

Utilisez la propriété de masquage d’informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs au sein de l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) de carte adaptative.

> [!NOTE]
> La fonctionnalité prend uniquement en charge le masquage d’informations côté client. Le texte d’entrée masqué est envoyé en tant que texte clair à l’adresse de point de terminaison HTTPS spécifiée lors de la [configuration du bot.](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)

Pour masquer les informations dans les cartes adaptatives, ajoutez la propriété à taper et définissez `isMasked` sa valeur sur  `Input.Text` **true**.

#### <a name="sample-adaptive-card-with-masking-property"></a>Exemple de carte adaptative avec propriété de masquage

Le code suivant illustre un exemple de carte adaptative avec propriété de masquage :

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

L’image suivante est un exemple de masquage d’informations dans les cartes adaptatives :

![Image d’informations de masquage](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>Carte adaptative pleine largeur

Vous pouvez utiliser la propriété pour développer la largeur d’une carte adaptative et `msteams` utiliser de l’espace de dessin supplémentaire. La section suivante fournit des informations sur l’utilisation de la propriété.

#### <a name="construct-full-width-cards"></a>Créer des cartes pleine largeur

Pour créer une carte adaptative pleine largeur, l’objet dans la propriété dans le contenu de la carte `width` doit être définie sur `msteams` `Full` .

#### <a name="sample-adaptive-card-with-full-width"></a>Exemple de carte adaptative avec pleine largeur

Pour effectuer une carte adaptative pleine largeur, votre application doit inclure les éléments de l’exemple de code suivant :

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

L’image suivante illustre une carte adaptative pleine largeur :

![Affichage carte adaptative pleine largeur](../../assets/images/cards/full-width-adaptive-card.png)

L’image suivante montre l’affichage par défaut de la carte adaptative lorsque vous n’avez pas fixé la valeur `width` Full à la **propriété**:

![Affichage carte adaptative à petite largeur](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Prise en charge de Typeahead

Dans l’élément de schéma, le fait de demander aux utilisateurs de filtrer et de sélectionner un nombre important de choix peut ralentir considérablement l’exécution [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de la tâche. La prise en charge de la tête de type dans les cartes adaptatives peut simplifier la sélection des entrées en axant ou en filtrant l’ensemble des choix d’entrée à mesure que l’utilisateur tape l’entrée.

Pour activer typeahead dans `Input.Choiceset` le , définie sur et `style` `filtered` `isMultiSelect` assurez-vous qu’elle est définie sur `false` .

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Exemple de carte adaptative avec prise en charge de typeahead

Le code suivant illustre un exemple de carte adaptative avec prise en charge de typeahead :

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

Dans une carte adaptative, vous pouvez utiliser la propriété pour ajouter la possibilité d’afficher des images en vue de la `msteams` scène de manière sélective. Lorsque les utilisateurs pointent sur les images, ils peuvent voir une icône de développement, pour laquelle l’attribut `allowExpand` est définie sur `true` . Pour plus d’informations sur l’utilisation de la propriété, voir l’exemple suivant :

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

Lorsque les utilisateurs pointent sur l’image, une icône développer s’affiche dans le coin supérieur droit, comme illustré dans l’image suivante :

![Carte adaptative avec image expandable](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

L’image apparaît en mode Étape lorsque l’utilisateur sélectionne l’icône développer, comme illustré dans l’image suivante :

![Image étendue en vue de la phase](../../assets/images/cards/adaptivecard-expand-image.png)

Dans la vue d’étape, les utilisateurs peuvent effectuer un zoom avant et un zoom arrière sur l’image. Vous pouvez sélectionner dans votre carte adaptative les images qui doivent avoir cette fonctionnalité.

> [!NOTE]
> * Les fonctionnalités de zoom avant et arrière s’appliquent uniquement aux éléments image de type image dans une carte adaptative.
> * Pour Teams applications mobiles, la fonctionnalité d’affichage de la scène pour les images dans les cartes adaptatives est disponible par défaut. Les utilisateurs peuvent afficher des images de carte adaptative en vue de l’étape en appuyant simplement sur l’image, que l’attribut `allowExpand` soit présent ou non.

# <a name="markdown-format-for-office-365-connector-cards"></a>[Format Markdown pour les cartes Office 365 Connector](#tab/connector-md)

Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML.

| Style | Exemple | Markdown |
| --- | --- | --- |
| Gras | **text** | `**text**` |
| Italic | *text* | `*text*` |
| En-tête (niveaux 1 &ndash; 3) | **Text** | `### Text`|
| Barré | ~~text~~ | `~~text~~` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Texte préformaté | `text` | ``preformatted text`` |
| Blockquote | >blockquote | `>blockquote text` |
| Lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Lien vers l’image |![Canet sur une bascule](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

Dans les cartes de connecteur, les nouvelles lignes sont restituer `\n\n` pour , mais pas pour ou `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur

Sur le bureau, la mise en forme Markdown pour les cartes de connecteur apparaît comme illustré dans l’image suivante :

![Mise en forme Markdown pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/connector-desktop-markdown-combined.png)

Sur iOS, la mise en forme Markdown pour les cartes de connecteur apparaît comme illustré dans l’image suivante :

![Mise en forme Markdown pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

Les cartes de connecteur utilisant Markdown pour iOS incluent les problèmes suivants :

* Le client iOS pour Teams ne restituera pas les images en ligne Markdown ou HTML dans les cartes de connecteur.
* Les blockquotes sont restituer en retrait, mais sans arrière-plan gris.

Sur Android, la mise en forme Markdown pour les cartes de connecteur apparaît comme illustré dans l’image suivante :

![Mise en forme Markdown pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Exemple de format pour les cartes de connecteur Markdown

Le code suivant montre un exemple de mise en forme pour les cartes de connecteur Markdown :

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

## <a name="format-cards-with-html"></a>Formater des cartes avec html

Les types de carte suivants peuvent être formaté au format HTML Teams :

* Office 365 Cartes de connecteur : le markdown limité et la mise en forme HTML sont pris en charge Office 365 cartes connecteur.
* Cartes Hero et miniatures : les balises HTML sont pris en charge pour les cartes simples, telles que les cartes hero et miniatures.

La mise en forme est différente entre le bureau et les versions mobiles de Teams pour les cartes Office 365 connecteur et les cartes simples. Dans cette section, vous pouvez passer par l’exemple de format HTML pour les cartes de connecteur et les cartes simples.

# <a name="html-format-for-office-365-connector-cards"></a>[Format HTML pour les cartes Office 365 connecteur de connexion](#tab/connector-html)

Les cartes de connecteurs prise en charge la mise en forme Limitée markdown et HTML.

| Style | Exemple | HTML |
| --- | --- | --- |
| Gras | **text** | `<strong>text</strong>` |
| Italic | *text* | `<em>text</em>` |
| En-tête (niveaux 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| Barré | ~~text~~ | `<strike>text</strike>` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texte préformaté | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Lien vers l’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

Dans les cartes de connecteur, les nouvelles lignes sont restituer au format HTML à l’aide de la `<p>` balise.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes de connecteur

Sur le bureau, la mise en forme HTML pour les cartes de connecteur s’affiche comme illustré dans l’image suivante :

![Mise en forme HTML pour les cartes de connecteur dans le client de bureau](../../assets/images/cards/Connector-desktop-html-combined.png)

Sur iOS, la mise en forme HTML apparaît comme illustré dans l’image suivante :

![Mise en forme HTML pour les cartes de connecteur dans le client iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

Les cartes de connecteur utilisant html pour iOS incluent les problèmes suivants :

* Les images en ligne ne sont pas restituer sur iOS à l’aide de Markdown ou html dans les cartes de connecteur.
* Le texte préformaté est restituer, mais n’a pas d’arrière-plan gris.

Sur Android, la mise en forme HTML apparaît comme illustré dans l’image suivante :

![Mise en forme HTML pour les cartes de connecteur dans le client Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>Exemple de format pour les cartes de connecteur HTML

Le code suivant montre un exemple de mise en forme pour les cartes de connecteur HTML :

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[Format HTML pour les cartes hero et miniatures](#tab/simple-html)

Les balises HTML sont pris en charge pour les cartes simples, telles que les cartes hero et miniatures. Markdown n’est pas pris en charge.

| Style | Exemple | HTML |
| --- | --- | --- |
| Gras | **text** | `<strong>text</strong>` |
| Italic | *text* | `<em>text</em>` |
| En-tête (niveaux 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| Barré | ~~text~~ | `<strike>text</strike>` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texte préformaté | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Lien hypertexte | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Lien vers l’image |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes simples

Comme il existe des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de Teams.

Sur le bureau, la mise en forme HTML apparaît comme illustré dans l’image suivante :

![Mise en forme HTML dans le client de bureau](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

Sur iOS, la mise en forme HTML apparaît comme illustré dans l’image suivante :

![Mise en forme HTML dans le client iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

La mise en forme des caractères, telle que le gras et l’italique, n’est pas restituer sur iOS.

Sur Android, la mise en forme HTML apparaît comme illustré dans l’image suivante :

![Mise en forme HTML dans le client Android](../../assets/images/cards/card-formatting-xml-android-60.png)

Mise en forme des caractères, telle que l’affichage en gras et en italique sur Android.

### <a name="format-example-for-simple-cards"></a>Exemple de format pour les cartes simples

Les images de la section précédente ont été créées à l’Teams **App Studio**, où la propriété de texte d’une carte Hero est définie sur la chaîne suivante :

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.

---

## <a name="see-also"></a>Voir aussi

* [Actions de carte](./cards-actions.md)
* [Modules de tâche](~/task-modules-and-cards/cards/cards-format.md)
