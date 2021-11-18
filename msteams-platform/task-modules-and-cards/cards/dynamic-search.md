---
title: Recherche typeahead dans les cartes adaptatives
author: Rajeshwari-v
description: Décrit la recherche typeahead avec le contrôle Input.ChoiceSet dans les cartes adaptatives
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 95041b1a24ac083329a809b8a5989d77e2430e26
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075582"
---
# <a name="typeahead-search-in-adaptive-cards"></a>Recherche typeahead dans les cartes adaptatives

La fonctionnalité de recherche Typeahead dans les cartes adaptatives offre une expérience de recherche améliorée sur `input.choiceset` le composant. Il fournit une liste de choix pour entrer du texte dans le champ de recherche. Vous pouvez incorporer la recherche typeahead avec des cartes adaptatives pour rechercher et sélectionner des données.

Vous pouvez utiliser la recherche typeahead pour les recherches suivantes :

* [Recherche statique](#static-typeahead-search)
* [Recherche dynamique](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>Recherche de typeahead statique

La recherche de typeahead statique permet aux utilisateurs de rechercher à partir des valeurs spécifiées dans la charge utile de `input.choiceset` carte adaptative. La recherche de typeahead statique peut être utilisée pour afficher plusieurs choix à l’utilisateur. La taille de la charge utile dans la recherche statique augmente avec le nombre de choix spécifié dans la charge utile.
Lorsque l’utilisateur commence à entrer le texte, les choix sont filtrés, qui correspondent partiellement à l’entrée. La liste finale met en évidence les caractères d’entrée qui correspondent à la recherche.

L’image suivante illustre la recherche de typeahead statique :

![Recherche de typeahead statique](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>Recherche de typeahead dynamique

La recherche de typeahead dynamique est utile pour rechercher et sélectionner des données à partir de grands ensembles de données. Les jeux de données sont chargés dynamiquement à partir du jeu de données spécifié dans la charge utile de la carte. La fonctionnalité d’avance de type permet de filtrer les choix à mesure que l’utilisateur tape.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Recherche de typeahead dynamique](~/assets/images/Cards/dynamic-typeahead-search-desktop.png)

![Image de recherche de typeahead dynamique 2](~/assets/images/Cards/dynamic-typeahead-search-desktop-2.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

Les clients mobiles Android et iOS supportent la recherche typeahead dans les cartes adaptatives.

**Scénario**

John est un employé du Store qui travaille dans un magasin Xbox. Le magasin utilise un bot pour répondre aux nouvelles demandes d’achat des clients. Un client peut effectuer des recherches à partir des milliers de jeux disponibles. La recherche typeahead dans les cartes adaptatives est utilisée pour rechercher et sélectionner les choix des clients.

**Pour utiliser la recherche typeahead dans les cartes adaptatives**

1. L’utilisateur A ouvre le bot du magasin.
1. L’utilisateur A envoie une commande au bot pour une **nouvelle demande de client.** Le bot répond avec la carte adaptative qui possède un `Input.ChoiceSet` composant.
1. L’utilisateur A utilise la recherche typeahead pour rechercher et sélectionner les informations en fonction du choix du client.

L’image suivante illustre l’expérience mobile de la recherche typeahead :

![Recherche de typeahead statique](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> Vous ne pouvez pas obtenir des expériences de carte enrichies avec la recherche dynamique, telles que les extensions de messagerie basée sur une requête.

## <a name="implement-typeahead-search"></a>Implémenter la recherche typeahead

`Input.ChoiceSet` est l’un des composants d’entrée importants dans les cartes adaptatives. Vous pouvez ajouter un contrôle de recherche typeahead au composant `Input.ChoiceSet` pour implémenter la recherche typeahead. Vous pouvez rechercher et sélectionner les informations requises avec les sélections suivantes :

* Dropdown, telle que la sélection étendue.
* Bouton d’radio, tel qu’une sélection unique.
* Cases à cocher, telles que plusieurs sélections.

> [!NOTE]
> Le `Input.ChoiceSet` contrôle est basé sur le style et les `isMultiSelect` propriétés.

### <a name="schema-properties"></a>Propriétés du schéma

Les propriétés suivantes sont les nouveaux ajouts au schéma pour activer la [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) recherche typeahead :

| Propriété| Type | Requis | Description |
|-----------|------|----------|-------------|
| style | Compact <br/> Étendu <br/> Filtré | Non | Ajoute un style filtré à la liste des validations prise en charge pour l’avance de type statique.|
| choices.data | Data.Query | Non | Active l’avance de type dynamique à mesure que l’utilisateur tape, en extraire un ensemble de choix à distance à partir d’un système back-end. |

### <a name="dataquery-definition"></a>Définition data.query

| Propriété| Type | Requis | Description |
|-----------|------|----------|-------------|
| type | Data.Query | Oui | Spécifie qu’il s’agit d’un objet Data.Query.|
| dataset | Chaîne | Oui | Spécifie le type de données qui sont récupérées dynamiquement. |
| value | Chaîne | Non | Remplit pour la demande d’appel au bot avec l’entrée que l’utilisateur a fournie au `ChoiceSet` bot. |
| count | Nombre | Non | Remplit pour la demande d’appel au bot pour spécifier le nombre d’éléments qui doivent être renvoyés. Le bot l’ignore si les utilisateurs souhaitent envoyer une quantité différente. | 
| skip | Nombre | Non | Remplit pour la demande d’appel au bot pour indiquer que les utilisateurs souhaitent paginer et avancer dans la liste. |

### <a name="example"></a>Exemple

Exemple de charge utile qui contient une recherche de typeahead statique et dynamique avec une seule & options à sélection multiple comme suit :

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "columns": [
        {
          "width": "1",
          "items": [
            {
              "size": null,
              "url": "https://urlp.asm.skype.com/v1/url/content?url=https%3a%2f%2fi.imgur.com%2fhdOYxT8.png",
              "height": "auto",
              "type": "Image"
            }
          ],
          "type": "Column"
        },
        {
          "width": "2",
          "items": [
            {
              "size": "extraLarge",
              "text": "Game Purchase",
              "weight": "bolder",
              "wrap": true,
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Please fill out the below form to send a game purchase request.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Call of Duty",
                  "value": "call_of_duty"
                },
                {
                  "title": "Death's Door",
                  "value": "deaths_door"
                },
                {
                  "title": "Grand Theft Auto V",
                  "value": "grand_theft"
                },
                {
                  "title": "Minecraft",
                  "value": "minecraft"
                }
              ],
              "style": "filtered",
              "placeholder": "Search for a game",
              "id": "choiceGameSingle",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Multi-Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Static Option 1",
                  "value": "static_option_1"
                },
                {
                  "title": "Static Option 2",
                  "value": "static_option_2"
                },
                {
                  "title": "Static Option 3",
                  "value": "static_option_3"
                }
              ],
              "isMultiSelect": true,
              "style": "filtered",
              "choices.data": {
                "type": "Data.Query",
                "dataset": "xbox"
              },
              "id": "choiceGameMulti",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Needed by: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        },
        {
          "width": "stretch",
          "items": [
            {
              "id": "choiceDate",
              "type": "Input.Date"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Buy and download digital games and content directly from your Xbox console, Windows 10 PC, or at Xbox.com.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "text": "Earn points for what you already do on Xbox, then redeem your points on real rewards. Play more, get rewarded. Start earning today.",
      "wrap": true,
      "type": "TextBlock"
    }
  ],
  "actions": [
    {
      "data": {
        "msteams": {
          "type": "invoke",
          "value": {
            "type": "task/submit"
          }
        }
      },
      "title": "Request Purchase",
      "type": "Action.Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```

## <a name="see-also"></a>Voir aussi

* [Actions universelles pour les cartes adaptatives](Universal-actions-for-adaptive-cards/Overview.md)
* [Modules de tâche](../what-are-task-modules.md)