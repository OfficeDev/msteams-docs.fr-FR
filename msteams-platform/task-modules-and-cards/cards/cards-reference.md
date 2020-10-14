---
title: Référence des cartes
description: Décrit toutes les cartes et les actions de carte disponibles pour les robots dans teams
keywords: Référence des cartes robots
ms.openlocfilehash: 0bcc905f3d5b678700a396ff3e5b8b5f0232046f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452609"
---
# <a name="cards-reference"></a>Référence des cartes

Les cartes répertoriées dans cette section sont prises en charge dans les robots pour Teams. Elles sont basées sur des cartes définies par l’infrastructure de robot, mais Teams ne prend pas en charge toutes les cartes de l’infrastructure bot et en a ajouté certaines. Les différences sont dénommées dans les références ci-dessous.

## <a name="card-examples"></a>Exemples de carte

Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du kit de développement logiciel (v3) du générateur de robots. Des exemples de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.

* .NET
  * [Ajouter des cartes en tant que pièces jointes aux messages](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [Exemple de code de carte (bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [Ajouter des cartes en tant que pièces jointes aux messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [Exemple de code de carte (bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>Types de cartes

Ce tableau indique les types de cartes à votre disposition.

| Type de carte | Description |
| --- | --- |
| [Carte adaptative](#adaptive-card) | Carte hautement personnalisable pouvant contenir n’importe quelle combinaison de texte, de paroles, d’images, de boutons et de champs d’entrée. |
| [Carte héros](#hero-card) | Contient généralement une seule image de grande taille, un ou plusieurs boutons et une petite quantité de texte. |
| [Fiche de liste](#list-card) | Une liste déroulante d’éléments. |
| [Carte de connecteur Office 365](#office-365-connector-card) | Disposition flexible avec plusieurs sections, champs, images et actions. |
| [Carte d’accusé de réception](#receipt-card) | Fournit un accusé de réception à l’utilisateur. |
| [Carte de connexion](#signin-card) | Permet à un bot de demander à un utilisateur de se connecter. |
| [Carte miniature](#thumbnail-card) | Contient généralement une seule image miniature, un texte court et un ou plusieurs boutons. |
| [Collections de cartes](#card-collections) | Utilisé pour retourner plusieurs éléments dans une seule réponse |

## <a name="common-properties-for-all-cards"></a>Propriétés communes pour toutes les cartes

### <a name="inline-card-images"></a>Images de carte en ligne

Votre carte peut contenir une image incluse en incluant un lien vers votre image accessible au public. Pour des raisons de performances, nous vous recommandons vivement d’héberger votre image sur un réseau de distribution de contenu public (CDN).

Les images sont mises à l’horizontale ou verticalement tout en conservant les proportions pour redimensionner la zone d’image, puis rognées du Centre pour obtenir les proportions appropriées pour la carte.

Les images doivent être d’au moins 1024 × 1024 et 1 Mo au format PNG, JPEG ou GIF ; l’image GIF animée n’est pas officiellement prise en charge.

| Propriété | Type  | Description |
| --- | --- | --- |
| url | URL | URL HTTPs vers l’image |
| alt | String | Description accessible de l’image |

### <a name="buttons"></a>Boutons

Les boutons sont affichés empilés au bas de la carte. Le texte du bouton est toujours sur une seule ligne et sera tronqué s’il dépasse la largeur du bouton. Les boutons supplémentaires qui dépassent le nombre maximal pris en charge par la carte ne seront pas affichés.

Pour plus d’informations, consultez la rubrique [actions de carte](~/task-modules-and-cards/cards/cards-actions.md) .

### <a name="card-formatting"></a>Mise en forme de carte

Pour plus d’informations sur la mise en forme de texte dans les cartes, voir [format](~/task-modules-and-cards/cards/cards-format.md) des cartes.

## <a name="adaptive-card"></a>Carte adaptative

Carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de paroles, d’images, de boutons et de champs d’entrée. *Voir* [cartes adaptatives v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Prise en charge des cartes adaptatives

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

> [!NOTE]
> Les éléments multimédias ne sont actuellement pas pris en charge dans les cartes adaptative v 1.2 sur la plateforme Teams.

### <a name="example-adaptive-card"></a>Exemple de carte adaptative

![Exemple de carte de carte adaptative](~/assets/images/cards/adaptivecard.png)

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
* [Actions de carte adaptative dans teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Carte héros

Une carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.

### <a name="support-for-hero-cards"></a>Prise en charge des cartes héros

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>Propriétés d’une carte héros

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes. |
| sous-titre | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme |
| images | Tableau d’images | Image affichée en haut de la carte. Proportions 16:9 |
| descendre | Tableau d’objets action | Ensemble d’actions applicables à la carte actuelle. Maximum 6 |
| taper | Objet Action | Cette action est activée lorsque l’utilisateur appuie sur la carte proprement dite. |
|

### <a name="example-hero-card"></a>Exemple de carte héros

![Exemple de carte héros](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a>Pour plus d’informations sur les cartes héros

Référence de l’infrastructure bot :

* [Nœud de carte héros](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Carte héros C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a>Fiche de liste

La carte de liste a été ajoutée par teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir. La carte de liste fournit une liste déroulante d’éléments.

### <a name="support-for-list-cards"></a>Prise en charge des cartes de visite

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>Propriétés d’une carte de liste

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| éléments | Tableau d’éléments de liste  ||
| descendre | Tableau d’objets action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |

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

Pris en charge dans Teams, pas dans l’infrastructure bot.

La carte de connecteur Office 365 offre une disposition flexible avec plusieurs sections, champs, images et actions. Cette carte encapsule une carte de connecteur afin qu’elle puisse être utilisée par les robots. Consultez la section Remarques pour connaître les différences entre les cartes de connecteur et la carte O365.

### <a name="support-for-office-365-connector-cards"></a>Prise en charge des cartes de connecteur Office 365

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Propriétés de la carte de connecteur Office 365

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes. |
| résumé | Texte enrichi  | Résumé de la carte. Maximum 2 lignes. |
| text | Texte enrichi  | Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme |
| themeColor | Chaîne HEXADÉCIMALe | couleur qui remplace le accentColor fourni par le manifeste de l’application |

### <a name="notes-on-the-office-365-connector-card"></a>Remarques sur la carte du connecteur Office 365

Les cartes de connecteur Office 365 fonctionnent correctement sur Microsoft Teams, y compris les [actions ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).

Une différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte.

* Pour un connecteur, le point de terminaison reçoit la charge utile de la carte via HTTP POST.
* Pour un bot, l' `HttpPOST` action déclenche une `invoke` activité qui envoie uniquement l’ID et le corps de l’action au bot.

Chaque carte de connecteur peut afficher un maximum de 10 sections et chaque section peut contenir un maximum de 5 images et 5 actions.

> [!NOTE]
> Les sections, images ou actions supplémentaires dans un message ne s’affichent pas.

Tous les champs de texte prennent en charge le démarque et le code HTML. Vous pouvez contrôler les sections qui utilisent la démarque ou le code HTML en définissant la `markdown` propriété dans un message. Par défaut, `markdown` est défini sur `true` ; si vous préférez utiliser HTML à la place, définissez `markdown` sur `false` .

Si vous spécifiez la `themeColor` propriété, elle se substitue `accentColor` à la propriété dans le manifeste de l’application.

Pour spécifier le style de rendu de `activityImage` , vous pouvez définir `activityImageType` comme suit.

| Valeur | Description |
| --- | --- |
| `avatar` | Default `activityImage` sera rognée en tant que cercle |
| `article` | `activityImage` s’affiche sous la forme d’un rectangle et conserve ses proportions |

Pour tous les autres détails sur les propriétés de la carte de connecteur, consultez la [référence de carte de message](/outlook/actionable-messages/card-reference)intégrant des actions. Les seules propriétés de la carte de connecteur que Microsoft Teams ne prend pas en charge sont les suivantes :

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

Carte qui permet à un bot de fournir un accusé de réception à l’utilisateur. Il contient généralement la liste des éléments à inclure dans le reçu, les informations fiscales et totales, ainsi que d’autres textes.

### <a name="support-for-receipts-cards"></a>Prise en charge des fiches de réception

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>Pour plus d’informations sur les cartes de réception

Référence de l’infrastructure bot :

* [Nœud carte de réception](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de réception C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a>Carte de connexion

Carte qui permet à un bot de demander à un utilisateur de se connecter. Pris en charge dans teams sous une forme légèrement différente de celle de l’infrastructure de robot. La carte de connexion dans teams est similaire à la carte de connexion dans l’infrastructure de robot, à l’exception que la carte de connexion dans Teams ne prend en charge que deux actions : `signin` et `openUrl` .

L' *action de connexion* peut être utilisée à partir de n’importe quelle carte dans Teams, et pas seulement à partir de la carte de connexion. Pour plus d’informations sur l’authentification, voir la rubrique [Microsoft teams Authentication Flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) .

### <a name="support-for-signin-cards"></a>Prise en charge des cartes de connexion

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>Pour plus d’informations sur les cartes de connexion

Référence de l’infrastructure bot :

* [Nœud de la carte de connexion](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de connexion C #](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a>Carte miniature

Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.

### <a name="support-for-thumbnail-cards"></a>Prise en charge des cartes miniatures

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propriétés d’une carte miniature

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| sous-titre | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît juste en dessous du sous-titre ; Voir [format des cartes](~/task-modules-and-cards/cards/cards-format.md) pour les options de mise en forme |
| images | Tableau d’images | Image affichée en haut de la carte. Proportions 1:1 (carrés) |
| descendre | Tableau d’objets action | Ensemble d’actions applicables à la carte actuelle. Maximum 6 |
| taper | Objet Action | Cette action est activée lorsque l’utilisateur appuie sur la carte proprement dite. |
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

Référence de l’infrastructure bot :

* [Nœud de la carte miniature](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte miniature C #](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a>Collections de cartes

Les collections de cartes sont prises en charge dans Teams.

Les collections de cartes sont fournies par l’infrastructure de robot : `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` . Ces collections peuvent contenir des cartes adaptative, héros ou miniatures.

## <a name="carousel-collection"></a>Collection carrousel

La [disposition carrousel](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) affiche un carrousel de cartes, éventuellement avec des boutons d’action associés.

### <a name="support-for-carousel-collections"></a>Prise en charge des regroupements de carrousel

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> Un carrousel peut afficher un maximum de 10 cartes par message.

### <a name="example-carousel-collection"></a>Exemple de collection carrousel

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

Les propriétés sont les mêmes que pour la carte héros ou miniature.

### <a name="syntax-for-carousel-collections"></a>Syntaxe des collections de carrousels

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a>Liste, collection

### <a name="support-for-list-collections"></a>Prise en charge des collections de listes

La disposition liste affiche une liste de cartes verticalement empilées, éventuellement avec des boutons d’action associés.

| Robots dans teams | Extensions de messagerie  | Connecteurs | Infrastructure de robot |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>Exemple de collection de listes

![Exemple de liste de cartes](~/assets/images/cards/list.png)

Les propriétés sont les mêmes que pour la carte héros ou miniature.

Une liste peut afficher un maximum de 10 cartes par message.

> [!NOTE]
> Certaines combinaisons de cartes de visite ne sont pas encore prises en charge sur iOS et Android.

### <a name="syntax-for-list-collections"></a>Syntaxe des collections de listes

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Cartes non prises en charge dans teams

Les cartes suivantes sont implémentées par l’infrastructure de robot, mais ne sont pas prises en charge par Teams.

* Cartes d’animation
* Cartes audio
* Cartes vidéo
