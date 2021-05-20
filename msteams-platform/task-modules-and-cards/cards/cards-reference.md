---
title: Référence de cartes
description: Décrit toutes les cartes et les actions de carte disponibles pour les bots dans Teams
localization_priority: Normal
keywords: bots cartes de référence
ms.topic: reference
ms.openlocfilehash: cab7f1659759f40beb1aba59531ee6c1a84662c1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566858"
---
# <a name="cards-reference"></a>Référence de cartes

Les cartes énumérées dans ce document sont prises en charge dans les bots pour Microsoft Teams. Ils sont basés sur des cartes définies par le cadre bot, mais Teams ne prend pas en charge toutes les cartes Bot Framework et au lieu de cela Teams cartes ont été ajoutées. Les différences sont appelées dans les références de ce document.

## <a name="card-examples"></a>Exemples de cartes

Vous pouvez trouver des informations supplémentaires sur la façon d’utiliser les cartes dans la documentation pour le Bot Builder SDK v3. Des échantillons de code sont également disponibles dans le référentiel Microsoft/BotBuilder-Samples sur GitHub.

* .NET
  * [Ajoutez des cartes comme pièces jointes aux messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).
  * [Cartes échantillon code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).

* Node.js
  * [Ajoutez des cartes comme pièces jointes aux messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).
  * [Cartes échantillon code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).

## <a name="types-of-cards"></a>Types de cartes

Ce tableau affiche les types de cartes à votre disposition :

| Type de carte | Description |
| --- | --- |
| [Carte adaptative](#adaptive-card) | Cette carte est une carte hautement personnalisable qui peut contenir n’importe quelle combinaison de texte, de parole, d’images, de boutons et de champs d’entrée. |
| [Carte de héros](#hero-card) | Cette carte contient généralement une seule grande image, un ou plusieurs boutons, et une petite quantité de texte. |
| [Carte de liste](#list-card) | Cette carte est une liste de défilement d’éléments. |
| [Office 365 connecteur](#office-365-connector-card) | Cette carte dispose d’une mise en page flexible avec plusieurs sections, champs, images et actions. |
| [Carte de réception](#receipt-card) | Cette carte fournit un reçu à l’utilisateur. |
| [Carte Signin](#signin-card) | Cette carte permet à un bot de demander qu’un utilisateur se signe. |
| [Carte miniature](#thumbnail-card) | Cette carte contient généralement une seule image miniature, un texte court et un ou plusieurs boutons. |
| [Collections de cartes](#card-collections) | Ces cartes sont utilisées pour renvoyer plusieurs éléments en une seule réponse. |

## <a name="common-properties-for-all-cards"></a>Propriétés communes pour toutes les cartes

### <a name="inline-card-images"></a>Images de carte en ligne

La carte peut contenir une image en ligne en incluant un lien vers l’image accessible au public. À des fins de performances, il est fortement recommandé d’héberger l’image sur un réseau public de diffusion de contenu (CDN).

Les images sont réduites en taille ou en baisse tout en conservant le rapport d’aspect pour couvrir la zone d’image. Les images sont ensuite recadrées à partir du centre pour atteindre le rapport d’aspect approprié pour la carte.

Les images doivent être tout au plus 1024×1024, en format PNG, JPEG ou GIF, et ne pas prendre en charge gif animé.

| Propriété | Type  | Description |
| --- | --- | --- |
| url | URL | HTTPS URL à l’image. |
| alt | String | Description accessible de l’image. |

> [!NOTE]
> Si une carte inclut une URL d’image qui passe par une redirection avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge. Cela se produit pour les images partagées sur le nuage public.

### <a name="buttons"></a>Boutons

Les boutons sont empilés au bas de la carte. Le texte du bouton est toujours sur une seule ligne et est tronqué si le texte dépasse la largeur du bouton. Tous les boutons supplémentaires au-delà du nombre maximum pris en charge par la carte ne sont pas affichés.

Pour plus d’informations, voir [les actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

### <a name="card-formatting"></a>Formatage des cartes

Pour plus d’informations sur le formatage du texte dans les cartes, voir [formatage de la carte](~/task-modules-and-cards/cards/cards-format.md).

## <a name="adaptive-card"></a>Carte adaptative

Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de parole, d’images, de boutons et de champs d’entrée. Pour plus d’informations, [voir cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Prise en charge des cartes adaptatives

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teams de la plate-forme prend en charge v1.2 ou plus tôt des fonctionnalités de carte adaptative.
> * Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative v1.2 sur la Teams plateforme.

### <a name="example-of-an-adaptive-card"></a>Exemple de carte adaptative

![Exemple de carte adaptative](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a>Informations supplémentaires sur les cartes adaptatives

Bot Framework référence:

* [Cartes adaptatives Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [Carte adaptative C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a>Carte de héros

Une carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.

### <a name="support-for-hero-cards"></a>Prise en charge des cartes héros

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Propriétés d’une carte de héros

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes. |
| sous-titre | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît sous le sous-titre. Pour les options de mise en forme, voir [formatage de carte](~/task-modules-and-cards/cards/cards-format.md). |
| Images | Tableau d’images | Image affichée en haut de la carte. Rapport d’aspect 16:9. |
| Boutons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |
| robinet | Objet Action | Activé lorsque l’utilisateur tape sur la carte elle-même. |

### <a name="example-of-a-hero-card"></a>Exemple d’une carte de héros

![Exemple d’une carte de héros](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a>Informations supplémentaires sur les cartes de héros

Bot Framework référence:

* [Carte de héros Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [Carte héros C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>Carte de liste

La carte de liste a été ajoutée par Teams fournir des fonctions au-delà de ce que la collection de liste peut fournir. La carte de liste fournit une liste de défilement des éléments.

### <a name="support-for-list-cards"></a>Prise en charge des cartes de liste

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Propriétés d’une carte de liste

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| éléments | Tableau des éléments de liste ||
| Boutons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |

### <a name="example-of-a-list-card"></a>Exemple de carte de liste

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

## <a name="office-365-connector-card"></a>Office 365 connecteur

La Office 365 connecteur est prise en charge en Teams, pas dans Bot Framework. Cette carte offre une disposition flexible avec plusieurs sections, champs, images et actions. Cette carte encapsule une carte connecteur afin qu’elle puisse être utilisée par les bots. Pour les différences entre les cartes de connecteur et la carte O365, [voir Notes sur la carte Office 365 connecteur.](#notes-on-the-office-365-connector-card)

### <a name="support-for-office-365-connector-cards"></a>Prise en charge Office 365 cartes connecteurs

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Propriétés de la carte Office 365 connecteur

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes. |
| résumé | Texte enrichi  | Résumé de la carte. Maximum 2 lignes. |
| text | Texte enrichi  | Le texte apparaît sous le sous-titre. Pour les options de mise en forme, voir [formatage de carte](~/task-modules-and-cards/cards/cards-format.md). |
| themeColor | Chaîne HEX | Couleur qui l’emporte sur l’accentColor fourni à partir du manifeste d’application. |

### <a name="notes-on-the-office-365-connector-card"></a>Notes sur la carte Office 365 connecteur

Office 365 connecteurs fonctionnent correctement dans les Microsoft Teams, y compris les [actions ActionCard](/outlook/actionable-messages/card-reference#actioncard-action).

Une différence importante entre l’utilisation de cartes connecteurs à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est le traitement des actions de la carte.

* Pour un connecteur, le point final reçoit la charge utile de la carte via HTTP POST.
* Pour un bot, `HttpPOST` l’action déclenche une activité qui envoie uniquement `invoke` l’iD d’action et le corps au bot.

Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.

> [!NOTE]
> Toutes les sections, images ou actions supplémentaires dans un message n’apparaissent pas.

Tous les champs de texte soutiennent la réduction des points et html. Vous pouvez contrôler les sections qui utilisent markdown ou HTML en paramètre la `markdown` propriété dans un message. Par défaut, `markdown` est défini sur `true` . Si vous souhaitez utiliser HTML à la place, `markdown` définissez-le sur `false` .

Si vous `themeColor` spécifiez la propriété, elle l’emporte sur la `accentColor` propriété dans le manifeste de l’application.

Pour spécifier le style de `activityImage` rendu pour , vous pouvez définir comme `activityImageType` suit:

| Valeur | Description |
| --- | --- |
| `avatar` | Par défaut; `activityImage` est recadrée comme un cercle. |
| `article` | `activityImage` s’affiche comme un rectangle et conserve son rapport d’aspect. |

Pour tous les autres détails sur les propriétés de la carte connecteur, voir [référence actionnable de carte de message](/outlook/actionable-messages/card-reference). Les seules propriétés de carte de connecteur Microsoft Teams ne prend pas actuellement en charge sont les suivantes :

* `heroImage`
* `hideOriginalBody`
* `startGroup`toujours traité comme `true` dans Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Exemple d’une Office 365 connecteur

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

## <a name="receipt-card"></a>Carte de réception

Teams prend en charge la carte de réception. Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur. Il contient généralement la liste des éléments à inclure sur le reçu, tels que l’impôt et l’information totale.

### <a name="support-for-receipt-cards"></a>Prise en charge des cartes de réception

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Exemple de carte de réception

![Exemple de carte de réception](~/assets/images/cards/receipt.png)

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a>Informations supplémentaires sur les cartes de réception

Bot Framework référence:

* [Carte de réception Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de réception C #](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>Carte Signin

La carte Signin permet à un bot de demander à un utilisateur de se connecter. Il est pris en charge Teams sous une forme légèrement différente de celle que l’on trouve dans le cadre bot. La carte de connexion en Teams est similaire à la carte signin dans le cadre Bot, sauf que la carte signin en Teams ne prend en charge que deux actions: `signin` et `openUrl` .

L’action signin peut être utilisée à partir de n’importe quelle carte Teams, pas seulement la carte de connexion. Pour plus d’informations sur l’authentification, [Microsoft Teams flux d’authentification pour les bots](~/bots/how-to/authentication/auth-flow-bot.md).

### <a name="support-for-signin-cards"></a>Prise en charge des cartes signin

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Informations supplémentaires sur les cartes de connexion

Bot Framework référence:

* [Carte Signin Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte Signin C #](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>Carte miniature

Une carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.

### <a name="support-for-thumbnail-cards"></a>Prise en charge des cartes miniatures

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Exemple d’une carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propriétés d’une carte miniature

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| sous-titre | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît sous le sous-titre. Pour les options de mise en forme, voir [formatage de carte](~/task-modules-and-cards/cards/cards-format.md). |
| Images | Tableau d’images | Image affichée en haut de la carte. Rapport d’aspect 1:1 carré. |
| Boutons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |
| robinet | Objet Action | Activé lorsque l’utilisateur tape sur la carte elle-même. |

### <a name="example-of-a-thumbnail-card"></a>Exemple d’une carte miniature

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

### <a name="additional-information"></a>Informations supplémentaires

Bot Framework référence:

* [Carte miniature Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte miniature C #](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>Collections de cartes

Teams prend en charge les collections de cartes.

Les collections de cartes `builder.AttachmentLayout.carousel` incluent et `builder.AttachmentLayout.list` . Ces collections contiennent des cartes adaptatives, héros ou miniatures.

## <a name="carousel-collection"></a>Collection Carrousel

La [disposition du carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) montre un carrousel de cartes, en option avec les boutons d’action associés.

### <a name="support-for-carousel-collections"></a>Prise en charge des collections de carrousel

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Un carrousel peut afficher un maximum de dix cartes par message.

### <a name="properties-of-a-carousel-card"></a>Propriétés d’une carte carrousel

Les propriétés d’une carte carrousel sont les mêmes que celles du héros et des cartes miniatures.

### <a name="example-of-a-carousel-collection"></a>Exemple de collection de carrousel

![Exemple d’un carrousel de cartes](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a>Syntaxe pour les collections de carrousel

`builder.AttachmentLayoutTypes.Carousel` est la syntaxe pour les collections de carrousel.

## <a name="list-collection"></a>Collection de liste

### <a name="support-for-list-collections"></a>Prise en charge des collections de liste

La mise en page de liste affiche une liste verticalement empilée de cartes, en option avec les boutons d’action associés.

| Bots en Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-list-collection"></a>Exemple d’une collection de liste

![Exemple d’une liste de cartes](~/assets/images/cards/list.png)

Les propriétés sont les mêmes que pour le héros ou la carte miniature.

Une liste peut afficher un maximum de dix cartes par message.

> [!NOTE]
> Certaines combinaisons de cartes de liste ne sont pas encore prises en charge sur iOS et Android.

### <a name="syntax-for-list-collections"></a>Syntaxe pour les collections de liste

`builder.AttachmentLayout.list` est la syntaxe pour les collections de liste.

## <a name="cards-not-supported-in-teams"></a>Cartes non prises en charge dans Teams

Les cartes suivantes sont implémentées par le Cadre Bot, mais ne sont pas prises en charge par Teams :

* Cartes d’animation
* Cartes audio
* Cartes vidéo
