---
title: Mise en forme du texte dans les cartes
description: Dans ce module, découvrez ce qu’est la mise en forme du texte de carte dans Microsoft Teams et mettez en forme des cartes avec Markdown.
ms.localizationpriority: high
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: b019c95b6cd8be32ef8d6d3ab10934cc8bcc56a1
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144207"
---
# <a name="format-cards-in-microsoft-teams"></a>Mettre en forme des cartes dans Microsoft Teams

Voici les deux façons d’ajouter une mise en forme de texte enrichi à vos cartes :

* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

Les cartes prennent uniquement en charge la mise en forme dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre. La mise en forme peut être spécifiée à l’aide d’un sous-ensemble de mise en forme XML ou HTML ou Markdown, selon le type de carte. Pour le développement actuel et futur de Cartes adaptatives, la mise en forme Markdown est recommandée.

La prise en charge du formatage diffère selon les types de cartes. Le rendu de la carte peut différer légèrement entre le client Microsoft Teams de bureau et le client Microsoft Teams mobile, ainsi qu'entre Teams et le navigateur de bureau.

Vous pouvez inclure une image incluse avec n’importe quelle carte Teams. Les formats d'image pris en charge sont les formats .png, .jpg ou .gif. Les dimensions ne doivent pas dépasser 1024 x 1024 px et la taille du fichier doit être inférieure à 1 Mo. Les images .gif animées ne sont pas prises en charge. Pour plus d’informations, consultez [types de cartes](./cards-reference.md#inline-card-images).

Vous pouvez mettre en forme Cartes adaptatives et les cartes connecteur Office 365 avec Markdown qui incluent certains styles pris en charge.

## <a name="format-cards-with-markdown"></a>Mettre en forme des cartes avec Markdown

Les types de cartes suivants prennent en charge la mise en forme Markdown dans Teams :

* Cartes adaptatives : Markdown est pris en charge dans le champ `Textblock` carte adaptative, ainsi que `Fact.Title` et `Fact.Value`. HTML n’est pas pris en charge dans Cartes adaptatives.
* Cartes de connecteur Office 365 : Markdown et HTML limité sont pris en charge dans les cartes connecteur Office 365 dans les champs de texte.

Vous pouvez utiliser des sauts de ligne pour Cartes adaptatives à l’aide de séquences d’échappement `\r` ou `\n` pour les sauts de ligne dans les listes. La mise en forme est différente entre le bureau et les versions mobiles de Teams pour Cartes adaptatives. Les mentions basées sur des cartes sont prises en charge dans les clients web, de bureau et mobiles. Vous pouvez utiliser la propriété de masquage des informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs dans l’élément d’entrée `Input.Text` carte adaptative. Vous pouvez développer la largeur d’une carte adaptative à l’aide de l’objet `width` . Vous pouvez activer la prise en charge de typeahead dans Cartes adaptatives et filtrer l’ensemble des choix d’entrée à mesure que l’utilisateur tape l’entrée. Vous pouvez utiliser la propriété `msteams` pour ajouter la possibilité d’afficher des images en mode intermédiaire de manière sélective.

La mise en forme est différente entre le bureau et les versions mobiles de Teams pour les cartes de Cartes adaptatives et de connecteur. Dans cette section, vous pouvez consulter l’exemple de format Markdown pour Cartes adaptatives et les cartes de connecteur.

# <a name="markdown-format-for-adaptive-cards"></a>[format Markdown pour Cartes adaptatives](#tab/adaptive-md)

 Le tableau suivant fournit les styles pris en charge pour `Textblock`, `Fact.Title`et `Fact.Value`:

| Style | Exemple | Markdown |
| --- | --- | --- |
| Gras | **Bold** | ```**Bold**``` |
| Italic | _Italic_ | ```_Italic_``` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Liens hypertexte |[Bing](https://www.bing.com/)| ```[Title](url)``` |

Les balises Markdown suivantes ne sont pas prises en charge :

* En-têtes
* Tables
* Des images
* Texte préformaté
* Blocs de guillemets

### <a name="newlines-for-adaptive-cards"></a>Sauts de ligne pour Cartes adaptatives

Vous pouvez utiliser les séquences d’échappement `\r` ou `\n` pour les sauts de ligne dans les listes. L’utilisation de `\n\n` dans les listes entraîne la mise en retrait de l’élément suivant dans la liste. Si vous avez besoin de sauts de ligne ailleurs dans TextBlock, utilisez `\n\n`.

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les Cartes adaptatives

Sur le bureau, la mise en forme du markdown de carte adaptative s’affiche comme indiqué dans l’image suivante dans les navigateurs web et dans l’application cliente Teams :

:::image type="content" source="../../assets/images/Cards/Adaptive-markdown-desktop-client.png" alt-text="client de bureau markdown adaptatif":::

Sur iOS, la mise en forme markdown de carte adaptative s’affiche comme illustré dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/Adaptive-markdown-iOS-75.png" alt-text="Mise en forme markdown de carte adaptative dans iOS":::

Sur Android, la mise en forme markdown de carte adaptative s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/Adaptive-markdown-Android.png" alt-text="Mise en forme markdown de carte adaptative dans Android":::

Pour plus d’informations, consultez [fonctionnalités de texte dans Cartes adaptatives](/adaptive-cards/create/textfeatures).

> [!NOTE]
> Les fonctionnalités de date et de localisation mentionnées dans cette section ne sont pas prises en charge dans Teams.

### <a name="adaptive-cards-format-sample"></a>Eexemple de format Cartes adaptatives

Le code suivant montre un exemple de mise en forme Cartes adaptatives :

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

Les cartes adaptatives supportent les emoji. Le code suivant montre un exemple de cartes adaptatives avec un emoji :

``` json
{ "$schema": "http://adaptivecards.io/schemas/adaptive-card.json", "type": "AdaptiveCard", "version": "1.0", "body": [ { "type": "Container", "items": [ { "type": "TextBlock", "text": "Publish Adaptive Card with emojis 🥰 ", "weight": "bolder", "size": "medium" }, ] }, ], }
```

:::image type="content" source="../../assets/images/Cards/adaptive-card-emoji.png" alt-text="Emoji de carte adaptative":::

### <a name="mention-support-within-adaptive-cards"></a>Mentionner la prise en charge dans Cartes adaptatives

Vous pouvez ajouter @mentions dans un corps de carte adaptative pour les bots et les réponses d’extension de messagerie. Pour ajouter @mentions dans les cartes, suivez la même logique de notification et de rendu que celle des mentions de [basées sur les messages dans les conversations de canal et de groupe](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).

Les bots et les extensions de messagerie peuvent inclure des mentions dans le contenu de la carte dans les éléments[TextBlock](https://adaptivecards.io/explorer/TextBlock.html) et [FactSet](https://adaptivecards.io/explorer/FactSet.html) .

> [!NOTE]
>
> * [éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans Cartes adaptatives sur la plateforme Teams.
> * Les mentions de canal et d’équipe ne sont pas prises en charge dans les messages de bot.

Pour inclure une mention dans une carte adaptative, votre application doit inclure les éléments suivants :

* `<at>username</at>` dans les éléments de carte adaptative pris en charge.
* L’objet `mention` à l’intérieur d’une propriété `msteams` dans le contenu de la carte inclut l’ID d’utilisateur Teams de l’utilisateur mentionné.
* Le `userId` est propre à votre ID de bot et à un utilisateur particulier. Il peut être utilisé pour @mention un utilisateur particulier. La `userId` peut être récupérée à l’aide de l’une des options mentionnées dans [obtenir l’ID utilisateur](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).

#### <a name="sample-adaptive-card-with-a-mention"></a>Exemple de carte adaptative avec mention

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

### <a name="microsoft-azure-active-directory-azure-ad-object-id-and-upn-in-user-mention"></a>Microsoft Azure Active Directory Domain Services (Azure AD) ID d’objet et UPN dans la mention utilisateur

La plateforme Teams permet de mentionner des utilisateurs avec leur ID d’objet Azure AD et leur nom d’utilisateur principal (UPN), en plus des ID de mention existants. Les bots avec Cartes adaptatives et connecteurs avec des webhooks entrants prennent en charge les deux ID de mention utilisateur.

Le tableau suivant décrit les ID de mention utilisateur qui viennent d’être pris en charge :

|Id  | Fonctionnalités de prise en charge | Description | Exemple |
|----------|--------|---------------|---------|
| ID d’objet Azure AD | Bot, Connecteur |  ID d’objet de l’utilisateur Azure AD | 49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | Bot, Connecteur | UPN de l’utilisateur Azure AD | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>Mention utilisateur dans les bots avec Cartes adaptatives

Les bots prennent en charge la mention utilisateur avec l’ID d’objet Azure AD et l’UPN, en plus des ID existants. La prise en charge de deux nouveaux ID est disponible dans les bots pour les SMS, le corps, Cartes adaptatives et la réponse d’extension de messagerie. Les bots prennent en charge les ID de mention dans les scénarios de conversation et de `invoke` . L’utilisateur reçoit une notification de flux d’activité lorsqu’il est @mentioned avec les ID.

> [!NOTE]
> La mise à jour du schéma et les modifications de l’interface utilisateur/de l’expérience utilisateur ne sont pas nécessaires pour les mentions utilisateur avec Cartes adaptatives dans bot.

##### <a name="example"></a>Exemple

Exemple de mention utilisateur dans les bots avec Cartes adaptatives comme suit :

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele Azure AD</at>"
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
        "text": "<at>Adele Azure AD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

L’image suivante illustre la mention utilisateur avec la carte adaptative dans bot :

:::image type="content" source="../../assets/images/authentication/user-mention-in-bot.png" alt-text="Mention utilisateur dans le bot avec carte adaptative":::

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>Mention utilisateur dans le webhook entrant avec Cartes adaptatives

Les webhooks entrants commencent à prendre en charge la mention utilisateur dans Cartes adaptatives avec l’ID d’objet Azure AD et l’UPN.

> [!NOTE]
>
> * Activez la mention utilisateur dans le schéma des webhooks entrants pour prendre en charge Azure AD’ID d’objet et l’UPN.
> * Les modifications de l’interface utilisateur/expérience utilisateur ne sont pas requises pour les mentions utilisateur avec Azure AD’ID d’objet et l’UPN.

##### <a name="example"></a>Exemple

Exemple de mention utilisateur dans le webhook entrant comme suit :

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
                    "text": "Hi <at>Adele UPN</at>, <at>Adele Azure AD</at>"
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
                        "text": "<at>Adele Azure AD</at>",
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

:::image type="content" source="../../assets/images/authentication/user-mention-in-incoming-webhook.png" alt-text="Mention utilisateur dans le webhook entrant":::

### <a name="information-masking-in-adaptive-cards"></a>Masquage des informations dans Cartes adaptatives

Utilisez la propriété de masquage des informations pour masquer des informations spécifiques, telles que le mot de passe ou les informations sensibles des utilisateurs dans l’élément d’entrée [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) carte adaptative.

> [!NOTE]
> Cette fonction ne prend en charge que le masquage des informations côté client. Le texte d'entrée masqué est envoyé en clair à l'adresse du point de terminaison HTTPS qui a été spécifiée lors de [la configuration du bot](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).

Pour masquer les informations dans Cartes adaptatives, ajoutez la propriété `style` à **type**`input.text`et définissez sa valeur sur **mot de passe**.

#### <a name="sample-adaptive-card-with-masking-property"></a>Exemple de carte adaptative avec propriété de masquage

Le code suivant montre un exemple de carte adaptative avec propriété de masquage :

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

L’image suivante est un exemple d’informations de masquage dans Cartes adaptatives :

:::image type="content" source="../../assets/images/Cards/masking-information-view.png" alt-text="Image des informations de masquage":::

### <a name="full-width-adaptive-card"></a>Carte adaptative pleine largeur

Vous pouvez utiliser la propriété `msteams` pour étendre la largeur d’une carte adaptative et utiliser de l’espace canevas supplémentaire. La section suivante fournit des informations sur l’utilisation de la propriété.

#### <a name="construct-full-width-cards"></a>Construire des cartes pleine largeur

Pour créer une carte adaptative de pleine largeur, l’objet `width` dans `msteams` propriété dans le contenu de la carte doit être défini sur `Full`.

#### <a name="sample-adaptive-card-with-full-width"></a>Exemple de carte adaptative avec pleine largeur

Pour créer une carte adaptative pleine largeur, votre application doit inclure les éléments de l’exemple de code suivant :

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

L’image suivante montre une carte adaptative pleine largeur :

:::image type="content" source="../../assets/images/Cards/full-width-adaptive-card.png" alt-text="Vue Carte adaptative pleine largeur":::

L’image suivante montre l’affichage par défaut de la carte adaptative lorsque vous n’avez pas défini la propriété `width` sur **Complète** :

:::image type="content" source="../../assets/images/Cards/small-width-adaptive-card.png" alt-text="Vue Carte adaptative à petite largeur":::

### <a name="typeahead-support"></a>Prise en charge de Typeahead

Dans l’élément de schéma [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html), demander aux utilisateurs de filtrer et de sélectionner un nombre important de choix peut ralentir considérablement l’achèvement des tâches. La prise en charge de typeahead dans Cartes adaptatives peut simplifier la sélection d’entrée en limitant ou en filtrant l’ensemble des choix d’entrée à mesure que l’utilisateur tape l’entrée.

Pour activer typeahead dans le `Input.Choiceset`, définissez `style` sur `filtered` et vérifiez que `isMultiSelect` est défini sur `false`.

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Exemple de carte adaptative avec prise en charge de typeahead

Le code suivant montre un exemple de carte adaptative avec prise en charge de typeahead :

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>Vue intermédiaire pour les images dans Cartes adaptatives

Dans une carte adaptative, vous pouvez utiliser la propriété `msteams` pour ajouter la possibilité d’afficher des images en mode intermédiaire de manière sélective. Lorsque les utilisateurs pointent sur les images, ils peuvent voir une icône développer, pour laquelle l’attribut `allowExpand` est défini sur `true`. Pour plus d’informations sur l’utilisation de la propriété, consultez l’exemple suivant :

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
          }
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

Lorsque les utilisateurs pointent sur l’image, une icône développer apparaît dans le coin supérieur droit, comme illustré dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/adaptivecard-hover-expand-icon.png" alt-text="Carte adaptative avec image extensible":::

L’image s’affiche en mode intermédiaire lorsque l’utilisateur sélectionne l’icône développer, comme illustré dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/adaptivecard-expand-image.png" alt-text="Image développée en mode Intermédiaire":::

Dans l’affichage intermédiaire, les utilisateurs peuvent effectuer un zoom avant et un zoom arrière sur l’image. Vous pouvez sélectionner les images de votre carte adaptative qui doivent avoir cette fonctionnalité.

> [!NOTE]
>
> * La fonctionnalité de zoom avant et de zoom arrière s’applique uniquement aux éléments d’image qui sont du type d’image dans une carte adaptative.
> * Pour les applications mobiles Teams, la fonctionnalité d’affichage intermédiaire pour les images dans Cartes adaptatives est disponible par défaut. Les utilisateurs peuvent afficher les images de carte adaptative en mode intermédiaire en appuyant simplement sur l’image, que l’attribut `allowExpand` soit présent ou non.

# <a name="markdown-format-for-office-365-connector-cards"></a>[format Markdown pour les cartes de connecteur Office 365](#tab/connector-md)

Les cartes de connecteur prennent en charge des formats Markdown et HTML limités.

| Style | Exemple | Markdown |
| --- | --- | --- |
| Gras | **text** | `**text**` |
| Italic | _text_ | `*text*` |
| En-tête (niveaux 1&ndash;3) | **Text** | `### Text`|
| Barré | ~~text~~ | `~~text~~` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Texte préformaté | `text` | ``preformatted text`` |
| Blockquote | texte >blockquote | `>blockquote text` |
| Hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| Lien d’image |![Canet sur un rocher](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

Dans les cartes de connecteur, les sauts de ligne sont affichés pour `\n\n`, mais pas pour `\n` ou `\r`.

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Différences entre les cartes de connecteur pour les appareils mobiles et les ordinateurs de bureau

Sur le Bureau, la mise en forme Markdown pour les cartes de connecteur s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/connector-desktop-markdown-combined.png" alt-text="Mise en forme markdown pour les cartes de connecteur":::

Sur iOS, la mise en forme Markdown pour les cartes de connecteur s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/connector-iphone-html-combined-80.png" alt-text="Mise en forme Markdown pour les cartes de connecteur dans le client iOS":::

Les cartes de connecteur utilisant Markdown pour iOS incluent les problèmes suivants :

* Le client iOS pour Teams n’affiche pas les images markdown ou HTML incluses dans les cartes de connecteur.
* Les guillemets sont rendus en retrait, mais sans arrière-plan gris.

Sur Android, la mise en forme Markdown pour les cartes de connecteur s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/connector-android-markdown-combined.png" alt-text="Mise en forme Markdown pour les cartes de connecteur dans le client Android":::

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

## <a name="format-cards-with-html"></a>Mettre en forme des cartes avec HTML

Les types de cartes suivants prennent en charge la mise en forme HTML dans Teams :

* Cartes de connecteur Office 365 : la mise en forme Markdown et HTML limitée est prise en charge dans les cartes connecteur Office 365.
* Cartes de bannière et miniatures : les balises HTML sont prises en charge pour les cartes simples, telles que les cartes de bannière et de miniatures.

La mise en forme est différente entre le bureau et les versions mobiles des cartes de connecteur Teams pour Office 365 et des cartes simples. Dans cette section, vous pouvez consulter l’exemple de format HTML pour les cartes de connecteur et les cartes simples.

# <a name="html-format-for-office-365-connector-cards"></a>[format HTML pour les cartes de connecteur Office 365](#tab/connector-html)

Les cartes de connecteur prennent en charge des formats Markdown et HTML limités.

| Style | Exemple | HTML |
| --- | --- | --- |
| Gras | **text** | `<strong>text</strong>` |
| Italic | _text_ | `<em>text</em>` |
| En-tête (niveaux 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| Barré | ~~text~~ | `<strike>text</strike>` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texte préformaté | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Lien d’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

Dans les cartes de connecteur, les sauts de ligne sont rendus au format HTML à l’aide de la balise `<p>` .

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>Différences entre les cartes de connecteur pour les appareils mobiles et les ordinateurs de bureau

Sur le Bureau, la mise en forme HTML des cartes de connecteur s’affiche comme illustré dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/Connector-desktop-html-combined.png" alt-text="Mise en forme HTML pour les cartes de connecteur dans le client de bureau":::

Sur iOS, la mise en forme HTML s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/connector-iphone-html-combined-80.png" alt-text="Mise en forme HTML pour les cartes de connecteur dans le client iOS":::

Les cartes de connecteur utilisant HTML pour iOS incluent les problèmes suivants :

* Les images incluses ne sont pas rendues sur iOS à l’aide de Markdown ou HTML dans les cartes de connecteur.
* Le texte préformaté est rendu, mais n’a pas d’arrière-plan gris.

Sur Android, la mise en forme HTML s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/connector-android-html-combined.png" alt-text="Mise en forme HTML pour les cartes de connecteur dans le client Android":::

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[format HTML pour les cartes](#tab/simple-html) de bannière et de miniatures

Les balises HTML sont prises en charge pour les cartes simples, telles que les cartes héros et vignettes. Le format Markdown n'est pas pris en charge.

| Style | Exemple | HTML |
| --- | --- | --- |
| Gras | **text** | `<strong>text</strong>` |
| Italic | _text_ | `<em>text</em>` |
| En-tête (niveaux 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| Barré | ~~text~~ | `<strike>text</strike>` |
| Liste non triée | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| Liste triée | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| Texte préformaté | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| Lien d’image |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>Différences entre les appareils mobiles et les ordinateurs de bureau pour les cartes simples

Étant donné qu’il existe des différences de résolution entre le bureau et la plateforme mobile, la mise en forme est différente entre le bureau et la version mobile de Teams.

Sur le Bureau, la mise en forme HTML s’affiche comme illustré dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/card-formatting-xml-desktop-v2.png" alt-text="Mise en forme HTML dans le client de bureau":::

Sur iOS, la mise en forme HTML s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/card-formatting-xml-mobile-v2.png" alt-text="Mise en forme HTML dans le client iOS":::

La mise en forme des caractères, telle que le gras et l’italique, n’est pas rendue sur iOS.

Sur Android, la mise en forme HTML s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../../assets/images/Cards/card-formatting-xml-android-60.png" alt-text="Mise en forme HTML dans le client Android":::

La mise en forme des caractères, telle que le gras et l’italique, s’affiche correctement sur Android.

### <a name="format-example-for-simple-cards"></a>Exemple de format pour les cartes simples

Les images de la section précédente ont été créées à l’aide de Teams **App Studio**, où la propriété de texte d’une carte de bannière est définie sur la chaîne suivante :

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

Vous pouvez tester la mise en forme dans vos propres cartes en modifiant ce code.

---

## <a name="see-also"></a>Voir aussi

* [Actions de carte](./cards-actions.md)
* [Utiliser des modules de tâches à partir de bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Modules de tâche](~/task-modules-and-cards/cards/cards-format.md)
* [Formatez vos messages robots.](~/bots/how-to/format-your-bot-messages.md)
* [Explorateur de schémas pour les cartes adaptatives](https://adaptivecards.io/explorer/TextBlock.html)
