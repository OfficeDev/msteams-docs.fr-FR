---
title: Types de cartes
description: Décrit toutes les cartes et actions de carte disponibles pour les bots dans Teams
ms.localizationpriority: medium
keywords: Référence des cartes de bots
ms.topic: reference
ms.openlocfilehash: 424b21bb0d8b1d7a3aeb08cc9d6c521579bc7cc1
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156887"
---
# <a name="types-of-cards"></a>Types de cartes

Les cartes adaptatives, hero, list, Office 365 Connector, les cartes de réception, les cartes de connexion et les collections de cartes miniatures sont pris en charge dans les bots pour Microsoft Teams. Elles sont basées sur des cartes définies par Bot Framework, mais Teams ne prend pas en charge toutes les cartes Bot Framework et en a ajouté certaines.

Avant d’identifier les différents types de carte, comprenez comment créer une carte hero, une carte miniature ou une carte adaptative.

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a>Créer une carte Hero, une carte miniature ou une carte adaptative

**Pour créer une carte Hero, une carte miniature ou une carte adaptative à partir d’App Studio**

1. Go to **App Studio** from Teams.
1. Sélectionnez **l’éditeur de carte.**
1. Sélectionnez **Créer une carte.**
1. Sélectionnez **Créer** pour l’une des cartes **de la carte Hero,** de la carte **miniature** ou de la **carte adaptative.** Les exemples de code de métadonnées, boutons et json, csharp et nœud sont présentés pour cette carte.

    ![Détails de la carte Hero](~/assets/images/Cards/Herocarddetails.png)

1. Sélectionnez **M’envoyer cette carte.** La carte vous est envoyée en tant que message de conversation.

## <a name="card-examples"></a>Exemples de cartes

Vous trouverez des informations supplémentaires sur l’utilisation des cartes dans la documentation du SDK Bot Builder v3. Des exemples de code sont également disponibles dans le référentiel **Microsoft/BotBuilder-Samples** GitHub. Voici quelques exemples de cartes :

* .NET
  * [Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).

* Node.js
  * [Ajoutez des cartes en tant que pièces jointes à des messages.](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [Exemple de code cartes Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).

## <a name="card-types"></a>Types de carte

Vous pouvez identifier et utiliser différents types de cartes en fonction des besoins de votre application. Le tableau suivant indique les types de cartes disponibles :

| Type de carte | Description |
| --- | --- |
| [Carte adaptative](#adaptive-card) | Cette carte est hautement personnalisable et peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée. |
| [Carte Hero](#hero-card) | Cette carte contient généralement une seule grande image, un ou plusieurs boutons et une petite quantité de texte. |
| [Carte de liste](#list-card) | Cette carte contient une liste de défilement d’éléments. |
| [Office 365 Carte de connecteur](#office-365-connector-card) | Cette carte possède une disposition flexible avec plusieurs sections, champs, images et actions. |
| [Carte d’accusé de réception](#receipt-card) | Cette carte fournit un reçu à l’utilisateur. |
| [Carte de signature](#signin-card) | Cette carte permet à un bot de demander à un utilisateur de se rendre. |
| [Carte miniature](#thumbnail-card) | Cette carte contient généralement une seule image miniature, du texte court et un ou plusieurs boutons. |
| [Collections de cartes](#card-collections) | Cette collection de cartes est utilisée pour renvoyer plusieurs éléments en une seule réponse. |

## <a name="features-that-support-different-card-types"></a>Fonctionnalités qui prise en charge différents types de carte

| Type de carte | Bots | Aperçus des extensions de message | Résultats de l’extension de message | Modules de tâche | Webhooks sortants | Webhooks entrants | Connecteurs O365 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Carte adaptative | ✔ | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ |
| Carte connecteur O365 | ✔ | ✖ | ✔ | ✖ | ✔ | ✔ | ✔ |
| Carte Hero | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| Carte miniature | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| Carte de liste | ✔ | ✖ | ✖ | ✖ | ✔ | ✔ | ✖ |
| Carte d’accusé de réception | ✔ | ✖ | ✖ | ✖ | ✖ | ✔ | ✖ |
| Carte de signature | ✔ | ✖ | ✖ | ✖ | ✖ | ✖ | ✖ |

> [!NOTE]
> Pour les cartes adaptatives dans les webhooks entrants, tous les éléments de schéma de carte adaptative native, à l’exception `Action.Submit` de , sont entièrement pris en charge. Les actions prises en charge sont [**Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard,**](https://adaptivecards.io/explorer/Action.ShowCard.html) [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)et [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

## <a name="common-properties-for-all-cards"></a>Propriétés communes pour toutes les cartes

Vous pouvez passer par certaines propriétés communes applicables à toutes les cartes.

### <a name="inline-card-images"></a>Images de carte en ligne

La carte peut contenir une image fixe en incluant un lien vers l’image disponible publiquement. Pour des raisons de performances, il est vivement recommandé d’héberger l’image sur une réseau de distribution de contenu (CDN).

La taille des images est réduite ou réduite afin de maintenir les proportions pour couvrir la zone d’image. Les images sont ensuite rogées à partir du centre pour obtenir les proportions appropriées pour la carte.

Les images doivent être au maximum 1024×1024 et au format PNG, JPEG ou GIF. Gif animé non pris en charge.

Le tableau suivant fournit les propriétés des images de carte en ligne :

| Propriété | Type  | Description |
| --- | --- | --- |
| url | URL | URL HTTPS vers l’image. |
| alt | Chaîne | Description accessible de l’image. |

> [!NOTE]
> Si une carte inclut une URL d’image qui est redirigée avant l’image finale, la redirection dans l’URL de l’image n’est pas prise en charge. Cela se produit pour les images partagées sur le cloud public.

### <a name="buttons"></a>Boutons

Les boutons sont affichés empilés en bas de la carte. Le texte du bouton est toujours sur une seule ligne et tronqué si le texte dépasse la largeur du bouton. Les boutons supplémentaires au-delà du nombre maximal pris en charge par la carte ne sont pas affichés.

Pour plus d’informations, voir [actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)

### <a name="card-formatting"></a>Mise en forme de carte

Pour plus d’informations sur la mise en forme du texte dans les cartes, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)

Après avoir identifié les propriétés communes de toutes les cartes, vous pouvez désormais utiliser des cartes adaptatives, ce qui vous permet d’augmenter l’engagement et l’efficacité en ajoutant votre contenu actionnable directement dans les applications que vous utilisez.

## <a name="adaptive-card"></a>Carte adaptative

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

Une carte adaptative est une carte personnalisable qui peut contenir n’importe quelle combinaison de texte, de reconnaissance vocale, d’images, de boutons et de champs d’entrée. Pour plus d’informations, voir [Cartes adaptatives v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).

### <a name="support-for-adaptive-cards"></a>Prise en charge des cartes adaptatives

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes adaptatives :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teams plateforme prend en charge la v1.2 ou une antérieure des fonctionnalités de carte adaptative.
> * Le style d’action positive ou destructive n’est pas pris en charge dans les cartes adaptatives sur Teams plateforme.
> * Les éléments multimédias ne sont actuellement pas pris en charge dans la carte adaptative sur Teams plateforme.

### <a name="example-of-adaptive-card"></a>Exemple de carte adaptative

![Exemple de carte adaptative](~/assets/images/cards/adaptivecard.png)

Le code suivant illustre un exemple de carte adaptative :

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

Référence Bot Framework :

* [Nœud cartes adaptatives](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [Carte adaptative C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

Vous pouvez désormais utiliser une carte Hero, qui est une carte multi-usage utilisée pour mettre en évidence visuellement une sélection d’utilisateur potentielle.

## <a name="hero-card"></a>Carte Hero

Carte qui contient généralement une seule grande image, un ou plusieurs boutons et du texte.

### <a name="support-for-hero-cards"></a>Prise en charge des cartes Hero

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes Hero :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Propriétés d’une carte Hero

Le tableau suivant fournit les propriétés d’une carte Hero :

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum deux lignes. |
| subtitle | Texte enrichi  | Sous-titre de la carte. Maximum deux lignes.|
| text | Texte enrichi  | Le texte apparaît sous le sous-titre. Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md) |
| images | Tableau d’images | Image affichée en haut de la carte. Proportions 16:9. |
| buttons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Six maximum. |
| tap | Objet Action | Activé lorsque l’utilisateur tape sur la carte elle-même. |

### <a name="example-of-a-hero-card"></a>Exemple de carte Hero

![Exemple de carte Hero](~/assets/images/cards/hero.png)

Le code suivant montre un exemple de carte Hero :

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

### <a name="additional-information-on-hero-cards"></a>Informations supplémentaires sur les cartes Hero

Référence Bot Framework :

* [Carte Hero Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [Carte Hero C #](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>Carte de liste

La carte de liste a été ajoutée par Teams pour fournir des fonctions au-delà de ce que la collection de listes peut fournir. La carte de liste fournit une liste d’éléments à défilement.

### <a name="support-for-list-cards"></a>Prise en charge des cartes de liste

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de liste :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>Propriétés d’une carte de liste

Le tableau suivant fournit les propriétés d’une carte de liste :

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| éléments | Tableau d’éléments de liste | Ensemble d’éléments applicables à la carte.|
| buttons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |

### <a name="example-of-a-list-card"></a>Exemple de carte de liste

Le code suivant montre un exemple de carte de liste :

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

## <a name="office-365-connector-card"></a>carte Office 365 connecteur

Vous pouvez utiliser une carte connecteur Office 365 qui fournit une disposition flexible et constitue un excellent moyen d’obtenir des informations utiles. La carte Office 365 connecteur est prise en charge dans Teams, et non dans Bot Framework. Cette carte fournit une disposition flexible avec plusieurs sections, champs, images et actions. Cette carte contient une carte de connecteur afin qu’elle puisse être utilisée par des bots. Pour plus d’informations sur les différences entre les cartes de connecteur et la carte connecteur Office 365, consultez des informations supplémentaires [sur la carte Office 365 connecteur.](#additional-information-on-the-office-365-connector-card)

### <a name="support-for-office-365-connector-cards"></a>Prise en charge des cartes Office 365 connecteur de connexion

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge Office 365 cartes de connecteur :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Propriétés de la carte Office 365 Connector

Le tableau suivant fournit les propriétés de la carte Office 365 connecteur :

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum deux lignes. |
| résumé | Texte enrichi  | Résumé de la carte. Maximum deux lignes. |
| text | Texte enrichi  | Le texte apparaît sous le sous-titre. Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md) |
| themeColor | Chaîne HEX | Couleur qui remplace la couleur `accentColor` fournie à partir du manifeste de l’application. |

### <a name="additional-information-on-the-office-365-connector-card"></a>Informations supplémentaires sur la carte Office 365 Connector

Office 365 Les cartes de connecteur fonctionnent correctement Microsoft Teams, y compris les [ `ActionCard` actions.](/outlook/actionable-messages/card-reference#actioncard-action)

La différence importante entre l’utilisation de cartes de connecteur à partir d’un connecteur et l’utilisation de cartes de connecteur dans votre bot est la gestion des actions de carte. Le tableau suivant répertorie la différence :

| Connector | Bot |
| --- | --- |
| Le point de terminaison reçoit la charge utile de la carte via HTTP POST. | `HttpPOST`L’action déclenche une activité qui envoie uniquement `invoke` l’ID d’action et le corps au bot.|

Chaque carte de connecteur peut afficher un maximum de dix sections, et chaque section peut contenir un maximum de cinq images et cinq actions.

> [!NOTE]
> Les sections, images ou actions supplémentaires dans un message n’apparaissent pas.

Tous les champs de texte sont en charge markdown et HTML. Vous pouvez contrôler les sections qui utilisent Markdown ou HTML en fixant `markdown` la propriété dans un message. Par défaut, `markdown` est définie sur `true` . Si vous souhaitez utiliser du code HTML à la place, définissez `markdown` sur `false` .

Si vous spécifiez la propriété, elle remplace la `themeColor` propriété dans le manifeste de `accentColor` l’application.

Pour spécifier le style de rendu pour , vous pouvez définir `activityImage` comme indiqué dans le tableau suivant `activityImageType` :

| Valeur | Description |
| --- | --- |
| `avatar` | Par défaut, `activityImage` elle est rogcée sous la mesure d’un cercle. |
| `article` | `activityImage` est affiché sous forme de rectangle et conserve ses proportions. |

Pour plus d’informations sur les propriétés de carte de connecteur, voir la [référence de carte de message actionnable.](/outlook/actionable-messages/card-reference) Les seules propriétés de carte de connecteur que Teams ne prend pas en charge actuellement sont les suivantes :

* `heroImage`
* `hideOriginalBody`
* `startGroup`toujours traité comme dans `true` Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Exemple de carte Office 365 Connector

Le code suivant montre un exemple de carte Office 365 Connecteur :

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

Teams prend en charge la carte de réception. Il s’agit d’une carte qui permet à un bot de fournir un reçu à l’utilisateur. Il contient généralement la liste des éléments à inclure sur le reçu, par exemple les informations fiscales et totales.

### <a name="support-for-receipt-cards"></a>Prise en charge des cartes de réception

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de réception :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>Exemple de carte de reçu

![Exemple de carte de reçu](~/assets/images/cards/receipt.png)

Le code suivant montre un exemple de carte de réception :

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

Référence Bot Framework :

* [Carte de réception Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de réception C #](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>Carte de signature

La carte de Teams est similaire à la carte de signin dans Bot Framework, sauf que la carte de Teams ne prend en charge que deux actions `signin` et `openUrl` .

L’action de signin peut être utilisée à partir de n’importe quelle carte de Teams, et pas seulement de la carte de signature. Pour plus d’informations, [voir Teams’authentification pour les bots.](~/bots/how-to/authentication/auth-flow-bot.md)

### <a name="support-for-signin-cards"></a>Prise en charge des cartes de signature

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes de signature :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>Informations supplémentaires sur les cartes de signature

Référence Bot Framework :

* [Carte de Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte de signature C #](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>Carte miniature

Vous pouvez utiliser une carte miniature utilisée pour envoyer un message actionnable simple. Carte qui contient généralement une seule image miniature, un ou plusieurs boutons et du texte.

### <a name="support-for-thumbnail-cards"></a>Prise en charge des cartes miniatures

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des cartes miniatures :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![Exemple de carte miniature](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>Propriétés d’une carte miniature

Le tableau suivant fournit les propriétés d’une carte miniature :

| Propriété | Type  | Description |
| --- | --- | --- |
| title | Texte enrichi  | Titre de la carte. Maximum 2 lignes.|
| subtitle | Texte enrichi  | Sous-titre de la carte. Maximum 2 lignes.|
| text | Texte enrichi  | Le texte apparaît sous le sous-titre. Pour les options de mise en forme, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md) |
| images | Tableau d’images | Image affichée en haut de la carte. Proportions 1:1 carré. |
| buttons | Tableau d’objets d’action | Ensemble d’actions applicables à la carte actuelle. Maximum 6. |
| tap | Objet Action | Activé lorsque l’utilisateur tape sur la carte elle-même. |

### <a name="example-of-a-thumbnail-card"></a>Exemple de carte miniature

Le code suivant montre un exemple de carte miniature :

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

Référence Bot Framework :

* [Carte miniature Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [Carte miniature C #](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>Collections de cartes

Vous pouvez utiliser des collections de cartes qui incluent des collections de listes et de carrousels. Teams prend en charge les collections de cartes. Les collections de cartes incluent `builder.AttachmentLayout.carousel` et `builder.AttachmentLayout.list` . Ces collections contiennent des cartes adaptatives, hero ou miniatures.

### <a name="carousel-collection"></a>Collection de carrousels

La [disposition de carrousel](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) présente un carrousel de cartes, éventuellement avec des boutons d’action associés.

#### <a name="support-for-carousel-collections"></a>Prise en charge des collections de carrousels

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des collections de carrousels :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> Un carrousel peut afficher un maximum de dix cartes par message.

#### <a name="properties-of-a-carousel-card"></a>Propriétés d’une carte carrousel

Les propriétés d’une carte carrousel sont identiques aux cartes hero et miniatures.

#### <a name="example-of-a-carousel-collection"></a>Exemple de collection de carrousels

![Exemple de carrousel de cartes](~/assets/images/cards/carousel.png)

Le code suivant montre un exemple de collection de carrousels :

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

#### <a name="syntax-for-carousel-collections"></a>Syntaxe pour les collections de carrousels

`builder.AttachmentLayoutTypes.Carousel` est la syntaxe des collections de carrousels.

### <a name="list-collection"></a>Collection de listes

La disposition de liste affiche une liste empilée verticalement de cartes, éventuellement avec des boutons d’action associés.

#### <a name="support-for-list-collections"></a>Prise en charge des collections de listes

Le tableau suivant fournit les fonctionnalités qui assurent la prise en charge des collections de listes :

| Bots dans Teams | Extensions de messagerie  | Connecteurs | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

#### <a name="example-of-a-list-collection"></a>Exemple de collection de listes

![Exemple de liste de cartes](~/assets/images/cards/list.png)

Les propriétés des collections de listes sont identiques aux cartes hero ou miniatures.

Une liste peut afficher un maximum de dix cartes par message.

> [!NOTE]
> Certaines combinaisons de cartes de liste ne sont pas encore pris en charge sur iOS et Android.

#### <a name="syntax-for-list-collections"></a>Syntaxe pour les collections de listes

`builder.AttachmentLayout.list` est la syntaxe des collections de listes.

## <a name="cards-not-supported-in-teams"></a>Cartes non pris en charge dans Teams

Les cartes suivantes sont implémentées par Bot Framework, mais ne sont pas Teams :

* Cartes d’animation
* Cartes audio
* Cartes vidéo

## <a name="see-also"></a>Voir aussi

* [Modules de tâche](~/task-modules-and-cards/what-are-task-modules.md)
* [Format des cartes](~/task-modules-and-cards/cards/cards-format.md)
