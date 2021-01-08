---
title: Référence des cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
keywords: Référence des cartes de bots
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778393"
---
# <a name="cards-reference"></a>Référence des cartes

Les cartes répertoriées dans cette section sont pris en charge dans les bots pour Teams. Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines. Les différences sont appelées dans les références ci-dessous.

## <a name="card-examples"></a>Exemples de carte

Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder (v3). Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.

* .NET
  * [Ajouter des cartes en tant que pièces jointes à des messages](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [Exemple de code de cartes (Bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [Ajouter des cartes en tant que pièces jointes à des messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [Exemple de code de cartes (Bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>Types de cartes

Ce tableau indique les types de cartes à votre disposition.

| Type de carte | Description |
| --- | --- |
| [Carte adaptative](#adaptive-card) | Carte hautement personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée. |
| [Hero Card](#hero-card) | Contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte. |
| [List Card](#list-card) | Liste de défilement d’éléments. |
| [Carte de connecteur Office 365](#office-365-connector-card) | Disposition flexible avec plusieurs sections, champs, images et actions. |
| [Carte d’accusé de réception](#receipt-card) | Fournit un reçu à l’utilisateur. |
| [Signin Card](#signin-card) | Permet à un bot de demander à un utilisateur de se connecter. |
| [Carte miniature](#thumbnail-card) | Contient généralement une seule image miniature, du texte court et un ou plusieurs boutons. |
| [Collections de cartes](#card-collections) | Utilisé pour renvoyer plusieurs éléments dans une seule réponse |

## <a name="common-properties-for-all-cards"></a>Propriétés communes pour toutes les cartes

### <a name="inline-card-images"></a>Images de carte en ligne

Votre carte peut contenir une image fixe en incluant un lien vers votre image disponible publiquement. Pour des raisons de performances, nous vous recommandons vivement d’héberger votre image sur un réseau de distribution de contenu (CDN) public.

La taille des images est réduite ou monter en puissance tout en conservant les proportions pour couvrir la zone d’image, puis rognées à partir du centre pour obtenir les proportions appropriées pour la carte.

Les images doivent être au maximum 1024×1024 au format PNG, JPEG ou GIF ; Gif animé n’est pas officiellement pris en charge.

| Propriété | Type  | Description |
| --- | --- | --- |
| url | URL | URL HTTPS vers l’image |
| alt | String | Description accessible de l’image |

### <a name="buttons"></a>Boutons

Les boutons sont affichés empilés en bas de la carte. Le texte du bouton est toujours sur une seule ligne et est tronqué si le texte dépasse la largeur du bouton. Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne s’afficheront pas.

Pour plus [d’informations,](~/task-modules-and-cards/cards/cards-actions.md) voir Actions de carte.

### <a name="card-formatting"></a>Mise en forme de carte

Pour [plus d’informations](~/task-modules-and-cards/cards/cards-format.md) sur la mise en forme du texte dans les cartes, voir Formatage de carte.

## <a name="adaptive-card"></a>Carte adaptative

Carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée. *Voir* [Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Prise en charge des cartes adaptatives

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

> [!NOTE]
> * La plateforme Teams prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.
> * Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la plateforme Teams.
### <a name="example-adaptive-card"></a>Exemple de carte adaptative

![Exemple de carte carte adaptative](~/assets/images/cards/adaptivecard.png)

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="for-more-information-on-adaptive-cards"></a>Pour plus d’informations sur les cartes adaptatives

* [Vue d’ensemble des cartes adaptatives](/adaptive-cards/)
* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Carte Hero

Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.

### <a name="support-for-hero-cards"></a>Prise en charge des cartes Hero

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>Propriétés d’une carte Hero

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes. |
| subtitle | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme |
| images | Tableau d’images | Image affichée en haut de la carte. Proportions 16:9 |
| buttons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6 |
| tap | Objet Action | Cette action est activée lorsque l’utilisateur tape sur la carte elle-même. |
|

### <a name="example-hero-card"></a>Exemple de carte Hero

![Exemple de carte Hero](~/assets/images/cards/hero.png)

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="for-more-information-on-hero-cards"></a>Pour plus d’informations sur les cartes Hero

Référence Bot Framework :

* [Nœud de carte Hero](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Carte Hero C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a>Carte de liste

La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir. La carte de liste fournit une liste d’éléments à défilement.

### <a name="support-for-list-cards"></a>Prise en charge des cartes de liste

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>Propriétés d’une carte de liste

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| éléments | Tableau d’éléments de liste  ||
| buttons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |

### <a name="example-list-card"></a>Exemple de carte de liste

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a>Carte de connecteur Office 365

Pris en charge dans Teams, et non dans Bot Framework.

La carte connecteur Office 365 fournit une disposition flexible avec plusieurs sections, champs, images et actions. Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par des bots. Consultez la section remarques pour les différences entre les cartes de connecteur et la carte O365.

### <a name="support-for-office-365-connector-cards"></a>Prise en charge des cartes de connecteur Office 365

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Propriétés de la carte de connecteur Office 365

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes. |
| résumé | Texte enrichi  | Résumé de la carte. Maximum 2 lignes. |
| text | Texte enrichi  | Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme |
| themeColor | Chaîne HEX | couleur qui remplace l’accentColor fourni à partir du manifeste de l’application |

### <a name="notes-on-the-office-365-connector-card"></a>Remarques sur la carte de connecteur Office 365

Les cartes de connecteur Office 365 fonctionnent correctement sur Microsoft Teams, y compris les [actions ActionCard.](/outlook/actionable-messages/card-reference#actioncard-action)

Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.

* Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.
* Pour un bot, l’action déclenche une activité qui envoie uniquement l’ID d’action et le `HttpPOST` `invoke` corps au bot.

Chaque carte de connecteur peut afficher un maximum de 10 sections, et chaque section peut contenir un maximum de 5 images et 5 actions.

> [!NOTE]
> Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.

Tous les champs de texte sont en charge markdown et HTML. Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant la `markdown` propriété dans un message. Par défaut, `markdown` est définie sur ; si vous souhaitez utiliser html à la `true` place, définie sur `markdown` `false` .

Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.

Pour spécifier le style de `activityImage` rendu pour , vous pouvez définir comme `activityImageType` suit.

| Valeur | Description |
| --- | --- |
| `avatar` | Valeur par défaut ; `activityImage` sera rogcé en tant que cercle |
| `article` | `activityImage` sera affiché sous forme de rectangle et conservera ses proportions |

Pour plus d’informations sur les propriétés de carte de connecteur, voir la référence de carte [de message actionnable.](/outlook/actionable-messages/card-reference) Les seules propriétés de carte de connecteur que Microsoft Teams ne prend pas en charge actuellement sont les suivantes :

* `heroImage`
* `hideOriginalBody`
* `startGroup` (toujours traité comme `true` dans Teams)
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>Exemple de carte de connecteur Office 365

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a>Carte d’accusé de réception

Pris en charge dans Teams.

Carte qui permet à un bot de fournir un reçu à l’utilisateur. Il contient généralement la liste des éléments à inclure sur le reçu, les taxes et le total des informations, ainsi que d’autres informations.

### <a name="support-for-receipts-cards"></a>Prise en charge des cartes de reçus

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>Pour plus d’informations sur les cartes de réception

Référence Bot Framework :

* [Nœud de carte de réception](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de réception C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a>Carte de signature

Carte qui permet à un bot de demander à un utilisateur de se connecter. Pris en charge dans Teams sous une forme légèrement différente de celle de Bot Framework. La carte de signature dans Teams est similaire à la carte de signin dans l’infrastructure du bot, à l’exception du fait que la carte de signin dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .

*L’action de signin* peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement de la carte de signature. Consultez la rubrique [Flux d’authentification Microsoft Teams pour les bots](~/bots/how-to/authentication/auth-flow-bot.md) pour plus d’informations sur l’authentification.

### <a name="support-for-signin-cards"></a>Prise en charge des cartes de signature

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>Pour plus d’informations sur les cartes de signature

Référence Bot Framework :

* [Nœud de carte de signature](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de signature C #](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a>Carte miniature

Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.

### <a name="support-for-thumbnail-cards"></a>Prise en charge des cartes miniatures

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propriétés d’une carte miniature

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| subtitle | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît juste en dessous du sous-titre . voir [Mise en forme de carte pour](~/task-modules-and-cards/cards/cards-format.md) les options de mise en forme |
| images | Tableau d’images | Image affichée en haut de la carte. Proportions 1:1 (carré) |
| buttons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6 |
| tap | Objet Action | Cette action est activée lorsque l’utilisateur tape sur la carte elle-même. |
|

### <a name="example-thumbnail-card"></a>Exemple de carte miniature

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="for-more-information"></a>Pour plus d'informations

Référence Bot Framework :

* [Nœud de carte miniature](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte miniature C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a>Collections de cartes

Les collections de cartes sont pris en charge dans Teams.

Collections de cartes `builder.AttachmentLayout.carousel` : et `builder.AttachmentLayout.list` . Ces collections contiennent des cartes adaptatives, Hero ou Miniatures.

## <a name="carousel-collection"></a>Collection de carrousels

La [disposition de carrousel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.

### <a name="support-for-carousel-collections"></a>Prise en charge des collections de carrousels

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> Un carrousel peut afficher un maximum de 10 cartes par message.

### <a name="properties-of-a-carousel-card"></a>Propriétés d’une carte Carrousel

Les propriétés d’une carte Carrousel sont identiques à celles des cartes Hero et Thumbnail.

### <a name="example-carousel-collection"></a>Exemple de collection de carrousels

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

### <a name="syntax-for-carousel-collections"></a>Syntaxe pour les collections de carrousels

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a>Collection de listes

### <a name="support-for-list-collections"></a>Prise en charge des collections de listes

La disposition de liste affiche une liste de cartes empilées verticalement, éventuellement avec des boutons d’action associés.

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>Exemple de collection de listes

![Exemple de liste de cartes](~/assets/images/cards/list.png)

Les propriétés sont identiques à la carte hero ou miniature.

Une liste peut afficher un maximum de 10 cartes par message.

> [!NOTE]
> Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.

### <a name="syntax-for-list-collections"></a>Syntaxe pour les collections de listes

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Cartes non pris en charge dans Teams

Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas pris en charge par Teams.

* Cartes d’animation
* Cartes audio
* Cartes vidéo
