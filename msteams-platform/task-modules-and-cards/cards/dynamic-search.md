---
title: Recherche en saisie semi-automatique dans les Cartes adaptatives
author: Rajeshwari-v
description: Décrit la recherche en tête de type avec le contrôle Input.ChoiceSet dans les cartes adaptatives
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 1e302a74ceffb88989989b42aa8a202d1e79fb36
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103438"
---
# <a name="typeahead-search-in-adaptive-cards"></a>Recherche en saisie semi-automatique dans les Cartes adaptatives

La fonctionnalité de recherche en tête de type dans les cartes adaptatives offre une expérience de recherche améliorée sur le `input.choiceset` composant. Il fournit une liste de choix pour entrer du texte dans le champ de recherche. Vous pouvez incorporer la recherche en tête de type avec les cartes adaptatives pour rechercher et sélectionner des données.

Vous pouvez utiliser la recherche de typeahead pour les recherches suivantes :

* [Recherche statique](#static-typeahead-search)
* [Recherche dynamique](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>Recherche de typeahead statique

La recherche statique de typehead permet aux utilisateurs de rechercher à partir des valeurs spécifiées dans `input.choiceset` la charge utile de la carte adaptative. La recherche de tête de type statique peut être utilisée pour afficher plusieurs choix à l’utilisateur. La taille de la charge utile dans la recherche statique augmente avec le nombre de choix spécifiés dans la charge utile.
Lorsque l’utilisateur commence à entrer les textes, les choix sont filtrés, qui correspondent partiellement à l’entrée. La liste déroulante met en évidence les caractères d’entrée qui correspondent à la recherche.

L’image suivante illustre la recherche de typeahead statique :

![Recherche de typeahead statique](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>Recherche de typeahead dynamique

La recherche dynamique en tête de type est utile pour rechercher et sélectionner des données dans des jeux de données volumineux. Les jeux de données sont chargés dynamiquement à partir du jeu de données spécifié dans la charge utile de la carte. La fonctionnalité type ahead permet de filtrer les choix en fonction des types de l’utilisateur.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop.png" alt-text="Recherche de typeahead dynamique":::

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop-2.png" alt-text="Recherche dynamique de typehead 2":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

Les clients mobiles Android et iOS prennent en charge la recherche en tête de type dans les cartes adaptatives.

**Scénario**

John est un employé du magasin qui travaille dans un magasin xbox. Le magasin utilise un bot pour prendre de nouvelles demandes d’achat auprès des clients. Un client peut effectuer une recherche à partir des milliers de jeux disponibles. La recherche en tête de type dans les cartes adaptatives est utilisée pour rechercher et sélectionner les choix des clients.

**Pour utiliser la recherche de typeahead dans les cartes adaptatives**

1. L’utilisateur A ouvre le bot du store.
1. L’utilisateur A envoie une commande au bot pour une **nouvelle demande du client**. Le bot répond avec la carte adaptative qui a `Input.ChoiceSet` un composant.
1. L’utilisateur A utilise la recherche de typeahead pour rechercher et sélectionner les informations en fonction du choix du client.

L’image suivante illustre l’expérience mobile de la recherche de typeahead :

![Recherche de typeahead statique](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> Vous ne pouvez pas obtenir d’expériences de carte enrichies avec la recherche dynamique, comme les extensions de message basées sur des requêtes.

## <a name="implement-typeahead-search"></a>Implémenter la recherche de typeahead

`Input.ChoiceSet` est l’un des composants d’entrée importants dans les cartes adaptatives. Vous pouvez ajouter un contrôle de recherche de typehead au `Input.ChoiceSet` composant pour implémenter la recherche de typeahead. Vous pouvez rechercher et sélectionner les informations requises avec les sélections suivantes :

* Liste déroulante, telle que la sélection développée.
* Case d’option, telle qu’une sélection unique.
* Cases à cocher, telles que plusieurs sélections.

> [!NOTE]
> Le `Input.ChoiceSet` contrôle est basé sur le style et `isMultiSelect` les propriétés.

### <a name="schema-properties"></a>Propriétés du schéma

Les propriétés suivantes sont les nouveaux ajouts au schéma pour activer la [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) recherche de typeahead :

| Propriété| Type | Requis | Description |
|-----------|------|----------|-------------|
| style | Compact <br/> Étendu <br/> Filtrée | Non | Ajoute un style filtré à la liste des validations prises en charge pour le type statique à l’avance.|
| choices.data | Data.Query | Non | Active l’avance dynamique au fur et à mesure que l’utilisateur tape, en extrayant un ensemble distant de choix à partir d’un serveur principal. |

### <a name="dataquery-definition"></a>Définition de Data.Query

| Propriété| Type | Requis | Description |
|-----------|------|----------|-------------|
| type | Data.Query | Oui | Spécifie qu’il s’agit d’un objet Data.Query.|
| Dataset | Chaîne | Oui | Spécifie le type de données extraites dynamiquement. |
| value | Chaîne | Non | Remplit la demande d’appel au bot avec l’entrée que l’utilisateur a fournie au `ChoiceSet`. |
| count | Nombre | Non | Remplit la demande d’appel au bot pour spécifier le nombre d’éléments qui doivent être retournés. Le bot l’ignore si les utilisateurs souhaitent envoyer un montant différent. |
| skip | Nombre | Non | Remplit la demande d’appel au bot pour indiquer que les utilisateurs souhaitent paginer et avancer dans la liste. |

### <a name="example"></a>Exemple

L’exemple de charge utile qui contient la recherche de typehead statique et dynamique avec une seule & options de sélection multiple comme suit :

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

## <a name="code-snippets-for-invoke-request-and-response"></a>Extraits de code pour appeler la requête et la réponse

### <a name="invoke-request"></a>Appeler une demande

```json
{
    "name": "application/search",
    "type": "invoke",
    "value": {
        "queryText": "fluentui",
        "queryOptions": {
            "skip": 0,
            "top": 15
        },
        "dataset": "npm"
    },
    "locale": "en-US",
    "localTimezone": "America/Los_Angeles",
    // …. other fields
}
```

### <a name="response"></a>Réponse

#### <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Name == "application/search")
    {
 var packages = new[] {
   new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
   new { title = "Fluent UI Library", value = "FluentUI" }};

 var searchResponseData = new
 {
     type = "application/vnd.microsoft.search.searchResponse",
     value = new
     {
  results = packages
     }
 };
 var jsonString = JsonConvert.SerializeObject(searchResponseData);
 JObject jsonData = JObject.Parse(jsonString);
 return new InvokeResponse()
 {
     Status = 200,
     Body = jsonData
 };
    }

    return null;
}
```

#### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```nodejs
  async onInvokeActivity(context) {
    if (context._activity.name == 'application/search') {
      // let searchQuery = context._activity.value.queryText;  // This can be used to filter the results
      var successResult = {
        status: 200,
        body: {
          "type": "application/vnd.microsoft.search.searchResponse",
          "value": {
            "results": [
              {
                "value": "FluentAssertions",
                "title": "A very extensive set of extension methods"
              },
              {
                "value": "FluentUI",
                "title": "Fluent UI Library"
              }
            ]
          }
        }
      }

      return successResult;

    }
  }
```

#### <a name="json"></a>[JSON](#tab/json)

```json
{
    "status": 200,
    "body" : {
        "type": "application/vnd.microsoft.search.searchResponse",
        "value": {
           "results": [
                {
                    "value": "FluentAssertions",
                    "title": "A very extensive set of extension methods."
                },
                {
                    "value": "FluentUI",
                    "title": "Fluent UI Library"
                }
            ]
        }
    }
}
```

---

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom** | **Description** | **C#** | **Node.js** |
|----------------|-----------------|--------------|----------------|
| Contrôle de recherche en tête de type sur les cartes adaptatives | L’exemple montre les fonctionnalités du contrôle de recherche de type statique et dynamique dans les cartes adaptatives. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Actions universelles pour les cartes adaptatives](Universal-actions-for-adaptive-cards/Overview.md)
* [Modules de tâche](../what-are-task-modules.md)
