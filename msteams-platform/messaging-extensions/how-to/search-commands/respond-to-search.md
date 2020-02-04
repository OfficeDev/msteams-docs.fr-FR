---
title: Répondre à la commande de recherche
author: clearab
description: Comment répondre à la commande de recherche à partir d’une extension de messagerie dans une application Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e8b40dd8f422ffbd2537e8fa76a38c15eb6208de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674035"
---
# <a name="respond-to-the-search-command"></a>Répondre à la commande de recherche

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Votre service Web reçoit un `composeExtension/query` message d’appel qui contient un `value` objet avec les paramètres de recherche. Cet appel est déclenché :

* À mesure que des caractères sont entrés dans la zone de recherche.
* Si `initialRun` est défini sur true dans votre manifeste de l’application, vous recevrez le message d’appel dès que la commande de recherche est appelée. Voir [requête par défaut](#default-query).

Les paramètres de la demande sont trouvés dans `value` l’objet de la demande, qui inclut les propriétés suivantes :

| Nom de la propriété | Objectif |
|---|---|
| `commandId` | Nom de la commande appelée par l’utilisateur et correspondant à l’une des commandes déclarées dans le manifeste de l’application. |
| `parameters` | Tableau de paramètres. Chaque objet Parameter contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur. |
| `queryOptions` | Paramètres de pagination : <br>`skip`: ignorer le nombre pour cette requête <br>`count`: nombre d’éléments à renvoyer |

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[Machine à écrire/node. js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

Le JSON ci-dessous est raccourci pour mettre en évidence les sections les plus pertinentes.

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
...
}
```

* * *

## <a name="respond-to-user-requests"></a>Répondre aux demandes de l’utilisateur

Lorsque l’utilisateur effectue une requête, Microsoft teams émet une demande HTTP synchrone à votre service. À ce stade, votre code dispose de 5 secondes pour fournir une réponse HTTP à la demande. Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour traiter la demande.

Votre service doit répondre avec les résultats correspondant à la requête de l’utilisateur. La réponse doit indiquer un code d’état HTTP `200 OK` de et un objet application/JSON valide avec le corps suivant :

|Nom de la propriété|Objectif|
|---|---|
|`composeExtension`|Enveloppe de réponse de niveau supérieur.|
|`composeExtension.type`|Type de réponse. Les types suivants sont pris en charge : <br>`result`: affiche une liste de résultats de recherche <br>`auth`: demande à l’utilisateur de s’authentifier <br>`config`: demande à l’utilisateur de configurer l’extension de messagerie <br>`message`: affiche un message en texte brut. |
|`composeExtension.attachmentLayout`|Spécifie la disposition des pièces jointes. Utilisé pour les réponses de `result`type. <br>Actuellement, les types suivants sont pris en charge : <br>`list`: liste d’objets Card contenant des champs de miniature, de titre et de texte <br>`grid`: grille d’images miniatures |
|`composeExtension.attachments`|Tableau d’objets Attachment valides. Utilisé pour les réponses de `result`type. <br>Actuellement, les types suivants sont pris en charge : <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Actions suggérées. Utilisé pour les réponses de `auth` type `config`ou. |
|`composeExtension.text`|Message à afficher. Utilisé pour les réponses de `message`type. |

### <a name="response-card-types-and-previews"></a>Types et aperçus des cartes de réponse

Nous prenons en charge les types de pièces jointes suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte héros](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte de connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Voir [qu’est-ce que les cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d’ensemble.

Pour en savoir plus sur l’utilisation des types de cartes miniature et héros, consultez la rubrique [Ajouter des cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

Pour plus d’informations sur la carte de connecteur Office 365, voir [using office 365 Connector Cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La liste des résultats est affichée dans l’interface utilisateur Microsoft teams avec un aperçu de chaque élément. L’aperçu est généré de l’une des deux façons suivantes :

* À l' `preview` aide de la `attachment` propriété au sein de l’objet. La `preview` pièce jointe peut uniquement être une carte de héros ou de miniature.
* Extrait des propriétés de `title`base `text`, et `image` de la pièce jointe. Celles-ci sont utilisées uniquement `preview` si la propriété n’est pas définie et que ces propriétés sont disponibles.

Vous pouvez afficher un aperçu d’une carte adaptative ou d’une carte de connecteur Office 365 dans la liste des résultats en fonction de sa propriété preview. Cela n’est pas nécessaire si les résultats sont déjà des cartes de la héros ou des miniatures. Si vous utilisez la pièce jointe d’aperçu, il doit s’agir d’une carte de héros ou d’une carte miniature. Si aucune propriété Preview n’est spécifiée, l’aperçu de la carte échoue et rien ne s’affiche.

### <a name="response-example"></a>Exemple de réponse

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejstabtypescript"></a>[Machine à écrire/node. js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

* * *

## <a name="default-query"></a>Requête par défaut

Si vous définissez `initialRun` dans `true` le manifeste, Microsoft teams émet une requête « par défaut » lorsque l’utilisateur ouvre l’extension de messagerie pour la première fois. Votre service peut répondre à cette requête avec un ensemble de résultats pré-renseignés. Cela peut être utile lorsque votre commande de recherche nécessite une authentification ou une configuration, en affichant les éléments récemment consultés, les favoris ou toute autre information qui ne dépend pas de l’entrée de l’utilisateur.

La requête par défaut a la même structure que toute requête utilisateur normale, avec `name` le champ défini `initialRun` sur `value` et défini `true` sur comme dans l’objet ci-dessous.

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="next-steps"></a>Étapes suivantes

Ajouter une authentification et/ou une configuration

* [Ajouter l’authentification à une extension de messagerie](~/messaging-extensions/how-to/add-authentication.md)
* [Ajouter une configuration à une extension de messagerie](~/messaging-extensions/how-to/add-configuration-page.md)

Déployer la configuration

* [Déployer votre package d’application](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
