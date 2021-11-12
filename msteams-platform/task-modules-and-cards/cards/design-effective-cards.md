---
title: Conception de Cartes adaptatives pour votre application
description: Découvrez comment concevoir des Cartes adaptatives pour Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 86b5bdea89f49f6e98ce84920e3fbe1cdb4f378e
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948641"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Conception de Cartes adaptatives pour votre application Microsoft Teams

Une carte adaptative contient un corps libre d’éléments de carte et un ensemble facultatif d’actions. Les cartes adaptatives sont des extraits de contenu exploitables que vous pouvez ajouter à une conversation par le biais d'un bot ou d'une extension de messagerie. À l’aide de texte, de graphiques et de boutons, ces cartes fournissent une communication enrichie à votre public.

L’infrastructure de carte adaptative est utilisée dans de nombreux produits Microsoft, y compris Teams. Vous pouvez envoyer des cartes à l’intérieur des messages aux utilisateurs via des bots ou des extensions de messagerie. Les utilisateurs peuvent également effectuer des actions sur les cartes lorsqu’ils sont présents.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Exemple de vue d’ensemble d’une carte adaptative." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception plus complètes pour Cartes adaptatives dans Teams, y compris les éléments que vous pouvez récupérer et modifier en fonction des besoins, dans le Kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur couvre également des sujets essentiels tels que le thème, l’accessibilité et le dimensionnement réactif.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Vous pouvez également commencer à concevoir vos Cartes adaptatives directement dans le navigateur.

> [!div class="nextstepaction"]
> [Essayer le concepteur Cartes adaptatives](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Types de Cartes adaptatives

### <a name="hero"></a>Bannière

Notre carte la plus grande. À utiliser pour partager des articles ou des scénarios où une image indique la plupart de l’histoire.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Exemple montrant une carte de bannière de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Exemple montrant une carte de bannière de Carte adaptative." border="false":::

### <a name="thumbnail"></a>Miniature

Permet d’envoyer un message actionnable simple.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Exemple montrant une carte miniature de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Exemple montrant une carte miniature de Carte adaptative." border="false":::

### <a name="list"></a>Répertorier

Utilisez-le dans les scénarios où vous souhaitez que l’utilisateur choisisse un élément dans une liste, mais que les éléments n’ont pas besoin de beaucoup d’explications.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Exemple montrant une carte de liste de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Exemple montrant une carte de liste de Carte adaptative." border="false":::

### <a name="digest"></a>Digérer

À utiliser pour les résumés d'actualités et les articles de synthèse. Remarque : nous vous recommandons la carte miniature pour une simple mise à jour ou un élément d’actualités.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="L’exemple montre une carte de condensé de Carte adaptative sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="L’exemple montre une carte de condensé de Carte adaptative." border="false":::

### <a name="media"></a>Médias

À utiliser lorsque vous souhaitez combiner du texte et des médias, tels que l'audio ou la vidéo.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Exemple montrant une carte média de Carte adaptative sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Exemple montrant une carte média de Carte adaptative." border="false":::

### <a name="people"></a>Personnes

Meilleure utilisation lorsque vous communiquez efficacement les personnes impliquées dans une tâche.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Exemple montrant une carte de contacts de Carte adaptative sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Exemple montrant une carte de personnes de Carte adaptative." border="false":::

### <a name="request-ticket"></a>Ticket de demande

Permet d’obtenir des entrées rapides d’un utilisateur pour créer automatiquement une tâche ou un ticket.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Exemple montrant une carte de ticket de demande de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Exemple montrant une carte de ticket de demande de Carte adaptative." border="false":::

### <a name="imageset"></a>ImageSet

Permet d’envoyer plusieurs miniatures d’image.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Exemple montrant une carte de jeu d’image de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Exemple montrant une carte de jeu d’image de Carte adaptative." border="false":::

### <a name="actionset"></a>Exemple pour ActionSet

Utilisez cette option lorsque vous souhaitez que l’utilisateur sélectionne un bouton, puis recueille d'autres entrées utilisateur sur la même carte.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Exemple montrant une carte de jeu d’action de Carte adaptative sur un appareil mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Exemple montrant une carte de jeu d’action de Carte adaptative." border="false":::

### <a name="choiceset"></a>ChoiceSet

Permet de collecter plusieurs entrées de l’utilisateur.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Exemple montrant une carte d’ensemble de choix de Carte adaptative sur un appareil mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Exemple montrant une carte d’ensemble de choix de Carte adaptative." border="false":::

## <a name="anatomy"></a>Anatomie

Les cartes adaptatives ont une grande flexibilité. Mais au minimum, nous vous suggérons vivement d’inclure les composants suivants dans chaque carte.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Exemple illustrant l'anatomie de la Carte adaptative sur un appareil mobile." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**En-tête** : rendez vos en-têtes clairs et concis.|
|B|**Copie du corps** : transmettez des détails trop longs ou pas assez importants pour être inclus dans l’en-tête.|
|C|**Actions principales** : il est recommandé d’inclure entre 1 et 3 actions principales. Un groupe peut comporter jusqu’à six.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Exemple illustrant l'anatomie de la Carte adaptative." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**En-tête** : rendez vos en-têtes clairs et concis.|
|B|**Copie du corps** : transmettez des détails trop longs ou pas assez importants pour être inclus dans l’en-tête.|
|C|**Actions principales** : il est recommandé d’inclure entre 1 et 3 actions principales. Un groupe peut comporter jusqu’à six.|

## <a name="best-practices"></a>Meilleures pratiques

Cartes conçues pour une échelle d’écran étroite sur des écrans plus larges (l’inverse n’est pas vrai). Vous devez également supposer que les utilisateurs n’afficheront pas uniquement vos cartes sur le Bureau.

### <a name="column-layouts"></a>Mises en page des colonnes

Permet [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) de mettre en forme le contenu de votre carte dans un tableau ou une grille. Plusieurs options s’offrent à vous pour la mise en forme de la largeur des colonnes. Ces recommandations vous aident à comprendre quand utiliser chacune d’elles.

* `"width": "auto"`: dimensionne chaque colonne de l’application pour qu’elle corresponde au contenu de l’application `ColumnSet` que vous incluez dans cette colonne.
   * **À** faire : utilisez lorsque vous avez un contenu de largeur variable et n’avez pas besoin de hiérarchiser une colonne spécifique.
   * **À faire** : Pour chaque `TextBlock` , définir `"wrap": true` puisque le texte ne s’enveloppe pas par défaut.
   * **À ne pas faire**: définir `"width": "auto"` pour chaque conteneur de colonnes. Par exemple, si vous avez une entrée et un bouton côte à côte, le bouton peut être coupé sur certains écrans. Définissez plutôt la colonne avec des boutons et d’autres contenus qui `auto` doivent toujours être complètement visibles.
* `"width": "stretch"`: dimensionne les colonnes en fonction de la `ColumnSet` largeur disponible. Lorsque plusieurs colonnes `"stretch"` utilisent la valeur, elles partagent également la largeur disponible.
   * **À faire** : utilisez avec une colonne si toutes vos autres colonnes ont une largeur statique. Par exemple, vous avez des images miniatures dans une colonne d’une largeur de 50 pixels.
* `"width": "<number>"`: dimensionne les colonnes à l’aide d’une proportion de la `ColumnSet` largeur disponible. Par exemple, si vous définissez trois colonnes avec , et , les colonnes `"width": "1"`, `"width": "4"` et `"width": "5"`, prenons jusqu’à 10, 40 et 50 pour cent de la largeur disponible.
* `"width": "<number>px"`: dimensionne les colonnes à une largeur de pixel spécifique. Cette approche est utile lors de la création de tableaux.
   * **À faire** : utilisez lorsque la largeur de ce que vous affichez n’a pas besoin de changer (par exemple, les nombres et les pourcentages).
   * **Ne pas** : dépasser accidentellement la largeur de ce que la carte peut afficher. N’oubliez pas que la largeur d’écran disponible dépend de l’appareil. Teams pour téléphone ne prend pas non plus en charge le défilement horizontal comme Teams bureau.

#### <a name="example-knowing-when-to-stretch-columns"></a>Exemple : savoir quand étirer les colonnes

# <a name="design"></a>[Concevoir](#tab/design)

**À faire** : dans cet écran, il y a deux colonnes en bas de la carte. La largeur du composant d’entrée est définie sur `stretch`, tandis que la largeur du bouton **Sélectionner** est définie sur `auto` . Cela garantit que le bouton reste entièrement en vue.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="L’image montre comment définir la largeur de colonne dans les cartes adaptatives.":::

**À ne pas faire**: dans cet écran, les deux colonnes `width` ont été définies sur `auto` . Ainsi, **le bouton Sélectionner** à droite est légèrement coupé par rapport à l’entrée.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-dont.png" alt-text="L’image montre comment ne pas définir la largeur de colonne dans les cartes adaptatives.":::

# <a name="code"></a>[Code](#tab/code)

Voici le code pour l’implémentation de l’exemple de conception que vous devez suivre.

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.2",
  "body": [
    {
      "type": "TextBlock",
      "text": "I wasn't able to identify the type of expense. Select from the list:",
      "wrap": true,
      "id": "typePrompt",
      "spacing": "Medium",
      "size": "Medium"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Submit",
          "title": "Phone Bill",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Phone Bill",
              "action": "Phone Bill"
            },
            "action": "Phone Bill"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Taxi and Other Transportation",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Taxi and Other Transportation",
              "action": "Taxi and Other Transportation"
            },
            "action": "Taxi and Other Transportation"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Entertainment_misc",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Entertainment_misc",
              "action": "Entertainment_misc"
            },
            "action": "Entertainment_misc"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Car Rental",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Car Rental",
              "action": "Car Rental"
            },
            "action": "Car Rental"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Airfare",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Airfare",
              "action": "Airfare"
            },
            "action": "Airfare"
          }
        }
      ],
      "spacing": "Medium"
    },
    {
      "type": "TextBlock",
      "text": "     ",
      "wrap": true
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "Input.ChoiceSet",
              "choices": [
                {
                  "title": "Meals",
                  "value": "Meals"
                },
                {
                  "title": "Parking/Tolls",
                  "value": "Parking/Tolls"
                },
                {
                  "title": "Accomodation",
                  "value": "Accomodation"
                },
                {
                  "title": "Fuel-Gas/Petrol/Diesel",
                  "value": "Fuel-Gas/Petrol/Diesel"
                },
                {
                  "title": "Hotel",
                  "value": "Hotel"
                },
                {
                  "title": "Meals - Employees Only",
                  "value": "Meals - Employees Only"
                },
                {
                  "title": "Accomodations",
                  "value": "Accomodations"
                },
                {
                  "title": "Misc.Expenses",
                  "value": "Misc.Expenses"
                },
                {
                  "title": "Please Categorize",
                  "value": "Please Categorize"
                }
              ],
              "placeholder": "All",
              "id": "expenseTypes",
              "value": "Meals - Employees Only"
            }
          ]
        },
        {
          "type": "Column",
          "width": "auto",
          "items": [
            {
              "type": "ActionSet",
              "actions": [
                {
                  "type": "Action.Submit",
                  "title": "Select",
                  "data": {
                    "msteams": {
                      "type": "messageBack",
                      "displayText": "Select",
                      "action": "applyType"
                    },
                    "action": "applyType"
                  }
                }
              ]
            }
          ]
        }
      ],
      "spacing": "ExtraLarge"
    }
  ]
}
```

---

#### <a name="example-using-fewer-columns"></a>Exemple : utilisation de moins de colonnes

**À faire** : les dispositions ont tendance à s’afficher mieux sur les appareils mobiles avec moins de colonnes.

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-do.png" alt-text="L’image montre la quantité de colonnes adaptée dans les cartes adaptatives.":::

**À ne pas faire** : l’utilisation d’un trop grand nombre de colonnes peut encombrer le contenu de votre carte sur un appareil mobile.

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-dont.png" alt-text="L’image montre comment un trop grand nombre de colonnes peut avoir une incidence négative sur la disposition de la carte adaptative.":::

#### <a name="example-fixed-width-has-its-place"></a>Exemple : la largeur fixe a sa place

# <a name="design"></a>[Concevoir](#tab/design)

Lorsque la taille d’un affichage n’a pas besoin de changer, définissez les colonnes sur une largeur de pixel spécifique. Cet exemple montre la taille de la colonne de gauche à 50 pixels, tandis que les descriptions en dessous des miniatures étendent la longueur de la carte.

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="L’image montre comment définir la largeur de colonne dans les cartes adaptatives.":::

# <a name="code"></a>[Code](#tab/code)

Voici le code pour implémenter l’exemple de conception.

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "Pick up where you left off?",
      "weight": "bolder"
    },
    {
      "type": "ColumnSet",
      "spacing": "medium",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1083",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "Silver Star Mountain Range"
            },
            {
              "type": "TextBlock",
              "text": "Maps",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.msn.com"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1082",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "style": "emphasis",
          "items": [
            {
              "type": "TextBlock",
              "text": "Kitchen Remodel for Homes"
            },
            {
              "type": "TextBlock",
              "text": "With EMPHASIS",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.AdaptiveCards.io"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1080",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "The Witcher: A Series"
            },
            {
              "type": "TextBlock",
              "text": "Netflix",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.outlook.com"
      }
    }
  ],
  "actions": [
    {
      "type": "Action.OpenUrl",
      "title": "Resume all",
      "url": "ms-cortana:resume-all"
    },
    {
      "type": "Action.OpenUrl",
      "title": "More activities",
      "url": "ms-cortana:more-activities"
    }
  ]
}
```

---

### <a name="text"></a>Text

Que vous utilisiez [`TextBlock`](https://adaptivecards.io/explorer/TextBlock.html), [`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html), ou [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html), définissez`wrap` la propriété`true` de sorte que le texte de votre carte ne soit pas tronqué sur mobile.

#### <a name="example-making-sure-text-doesnt-truncate"></a>Exemple : s’assurer que le texte n’est pas tronqué

# <a name="design"></a>[Concevoir](#tab/design)

**À faire** : dans cet écran, la carte a une `wrap` propriété définie sur `true`. Cela permet au texte de s’ajuster à n’importe quelle taille d’écran.

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-true.png" alt-text="L’image montre comment encapsuler du texte dans des cartes adaptatives.":::

**N’utilisez pas**: dans cet écran, la carte n’utilise pas la propriété, de sorte que le texte se `wrap` coupe sur un écran mobile.

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-false.png" alt-text="L'image montre ce qui peut se passer si vous n'enroulez pas le texte dans les cartes adaptatives.":::

# <a name="code"></a>[Code](#tab/code)

Voici le code pour l’implémentation de l’exemple de conception que vous devez suivre.

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "What cuisine do you want?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor",
      "style": "compact",
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Chineese",
          "value": "1"
        },
        {
          "title": "Indian",
          "value": "2"
        },
        {
          "title": "Italian",
          "value": "3"
        }
      ]
    },
    {
      "type": "TextBlock",
      "text": "Select the dishes that you like?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor2",
      "style": "expanded",
      "wrap" : true,
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Cauliflower with potatoes sautéed with garam masala",
          "wrap" : true,
          "value": "1"
        },
        {
          "title": "Patties of potato mixed with some vegetables fried",
          "wrap" : true,
          "value": "2"
        },
        {
          "title": "Green capsicum with potatoes sautéed with cumin seeds",
          "wrap" : true,
          "value": "3"
        }
      ]
    }
  ]
}
```

---

### <a name="containers"></a>Containers

A `Container` vous permet de grouper un ensemble d’éléments associés.

* **À faire** : utilisez la `style` propriété pour mettre en avant un conteneur.
* **À faire** : utilisez `selectAction` la propriété pour associer une action aux autres éléments du conteneur.
* **À faire** : utilisez la `Action.ToggleVisibility` propriété pour rendre un groupe d’éléments réductible.
* **À ne pas faire** : utilisez des conteneurs pour une raison autre que celle mentionnée précédemment.

### <a name="images"></a>Des images

Suivez ces instructions lorsque vous insérez des images dans vos cartes.

* **À faire** : concevoir des images pour les écrans haute résolution afin d’éviter la pixelisation. Il est préférable d'afficher une image de 100x100 pixels en 50x50 pixels que l'inverse.
* **À faire** : si vous devez contrôler la taille exacte de vos images, utilisez les `width` propriétés et les `height` propriétés.
* **À ne pas faire** : incluez le remplissage avec vos images. Cela introduit généralement des problèmes d’espacement et de disposition indésirables.
* En ce qui concerne la couleur d’arrière-plan :
   * **À faire** : utilisez des arrière-plans transparents afin que vos images s’adaptent à n’importe Teams thème. 
   * **À ne pas faire** : inclure une couleur d’arrière-plan fixe, sauf si une couleur spécifique doit être visible pour vos utilisateurs.
   * **À ne pas faire** : ajoutez une couleur d’arrière-plan à une couleur `TextBlock` qui nuit à la lisibilité. Par exemple, si votre arrière-plan est sombre, utilisez une couleur de texte plus claire et inversement.

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Meilleure pratique concernant la façon dont vous ne devez inclure qu’un petit jeu d’actions sur une carte adaptative." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>À faire : utiliser jusqu’à six actions principales

Bien que Cartes adaptatives puisse prendre en charge six actions principales, la plupart des cartes n’en ont pas besoin. Les actions doivent être claires, concises et directes. Moins, c’est plus.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Meilleure pratique pour ne pas surcharger les utilisateurs avec un trop grand nombre d’actions sur une carte adaptative." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>À ne pas faire : utiliser plus de six actions principales

Les cartes adaptatives doivent présenter un contenu rapide et exploitable. Un trop grand nombre d’actions peut surcharger un utilisateur.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Fréquence

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Meilleure pratique concernant la fréquence des cartes adaptatives." border="false":::

#### <a name="do-be-concise"></a>À faire : être concis

Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes défilent hors de l’affichage, elles deviennent moins utiles. Essayez de vous limiter à l’essentiel. Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils considèrent comme du « bruit ».

## <a name="see-also"></a>Voir aussi

* [Cartes et modules de tâche](~/task-modules-and-cards/cards-and-task-modules.md)
* [Cartes et modules de tâches pris en charge dans un bot Teams](~/task-modules-and-cards/what-are-task-modules.md)
* [Travailler avec les actions universelles pour les cartes adaptatives](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [Répondre à l’action d’envoi du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Affichages spécifiques à l’utilisateur](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md)
