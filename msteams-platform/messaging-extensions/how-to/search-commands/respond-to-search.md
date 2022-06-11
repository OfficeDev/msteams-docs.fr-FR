---
title: Répondre à la commande de recherche
author: surbhigupta
description: Découvrez comment répondre à la commande de recherche à partir d’une extension de message dans une application Microsoft Teams à l’aide d’exemples de code et d’exemples
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 9e7dbfb6eed724fb56e7ae1e03a2132d7450947a
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032801"
---
# <a name="respond-to-search-command"></a>Répondre à la commande de recherche

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Une fois que l’utilisateur a envoyé la commande de recherche, votre service web reçoit un `composeExtension/query` message d’appel qui contient un `value` objet avec les paramètres de recherche. Cet appel est déclenché avec les conditions suivantes :

* Lorsque des caractères sont entrés dans la zone de recherche.
* `initialRun` est défini sur true dans le manifeste de votre application, vous recevez le message d’appel dès que la commande de recherche est appelée. Pour plus d’informations, consultez [la requête par défaut](#default-query).

Ce document vous guide sur la façon de répondre aux demandes des utilisateurs sous la forme de cartes et d’aperçus, ainsi que sur les conditions dans lesquelles Microsoft Teams émet une requête par défaut.

Les paramètres de requête se trouvent dans l’objet `value` de la requête, qui inclut les propriétés suivantes :

| Nom de la propriété | Objectif |
|---|---|
| `commandId` | Nom de la commande appelée par l’utilisateur, correspondant à l’une des commandes déclarées dans le manifeste de l’application. |
| `parameters` | Tableau de paramètres. Chaque objet de paramètre contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur. |
| `queryOptions` | Paramètres de pagination : <br>`skip`: Nombre d’skips pour cette requête <br>`count`: nombre d’éléments à retourner. |

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Le JSON ci-dessous est raccourci pour mettre en surbrillance les sections les plus pertinentes.

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

## <a name="respond-to-user-requests"></a>Répondre aux demandes des utilisateurs

Lorsque l’utilisateur exécute une requête, Microsoft Teams émet une requête HTTP synchrone à votre service. À ce stade, votre code dispose `5` de secondes pour fournir une réponse HTTP à la requête. Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour traiter la demande.

Votre service doit répondre avec les résultats correspondant à la requête utilisateur. La réponse doit indiquer un code d’état HTTP et `200 OK` une application valide ou un objet JSON avec les propriétés suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`composeExtension`|Enveloppe de réponse de niveau supérieur.|
|`composeExtension.type`|Type de réponse. Les types suivants sont pris en charge : <br>`result`: affiche une liste de résultats de recherche <br>`auth`: invite l’utilisateur à s’authentifier <br>`config`: invite l’utilisateur à configurer l’extension de message <br>`message`: affiche un message texte brut |
|`composeExtension.attachmentLayout`|Spécifie la disposition des pièces jointes. Utilisé pour les réponses de type `result`. <br>Actuellement, les types suivants sont pris en charge : <br>`list`: liste d’objets de carte contenant des champs miniature, titre et texte <br>`grid`: Grille d’images miniatures |
|`composeExtension.attachments`|Tableau d’objets pièce jointe valides. Utilisé pour les réponses de type `result`. <br>Actuellement, les types suivants sont pris en charge : <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Actions suggérées. Utilisé pour les réponses de type `auth` ou `config`. |
|`composeExtension.text`|Message à afficher. Utilisé pour les réponses de type `message`. |

### <a name="response-card-types-and-previews"></a>Types de cartes de réponse et aperçus

Teams prend en charge les types de cartes suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte de bannière](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte Connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Pour avoir une meilleure compréhension et une meilleure vue d’ensemble des cartes, découvrez [ce qu’il s’agit de cartes](~/task-modules-and-cards/what-are-cards.md).

Pour savoir comment utiliser les types de miniatures et de cartes de héros, consultez [ajouter des cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

Pour plus d’informations sur la carte de connecteur Office 365, consultez [Utilisation des cartes de connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La liste des résultats s’affiche dans l’interface utilisateur Microsoft Teams avec un aperçu de chaque élément. La préversion est générée de l’une des deux manières suivantes :

* Utilisation de la `preview` propriété dans l’objet `attachment` . La `preview` pièce jointe ne peut être qu’un héros ou une carte miniature.
* Extraction des propriétés de base `title``text`et `image` de l’objet`attachment`. Les propriétés de base sont utilisées uniquement si la `preview` propriété n’est pas spécifiée.

Pour la carte Hero ou Thumbnail, à l’exception de l’action d’appel, d’autres actions telles que bouton et appui ne sont pas prises en charge dans la carte d’aperçu.

Pour envoyer une carte adaptative ou une carte de connecteur Office 365, vous devez inclure un aperçu. La `preview` propriété doit être une carte Hero ou Miniature. Si vous ne spécifiez pas la propriété d’aperçu dans l’objet `attachment` , aucun aperçu n’est généré.

Pour les cartes Hero et Thumbnail, vous n’avez pas besoin de spécifier une propriété d’aperçu. Une préversion est générée par défaut.

### <a name="response-example"></a>Exemple de réponse

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

### <a name="enable-and-handle-tap-actions"></a>Activer et gérer les actions d’appui

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
{
    // The Preview card's Tap should have a Value property assigned, this will be returned to the bot in this event. 
    var (packageId, version, description, projectUrl, iconUrl) = query.ToObject<(string, string, string, string, string)>();

    var card = new ThumbnailCard
    {
        Title = "Card Select Item",
        Subtitle = description
    };

    var attachment = new MessagingExtensionAttachment
    {
        ContentType = ThumbnailCard.ContentType,
        Content = card,
    };

    return Task.FromResult(new MessagingExtensionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            Type = "result",
            AttachmentLayout = "list",
            Attachments = new List<MessagingExtensionAttachment> { attachment }
        }
    });
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
async handleTeamsMessagingExtensionSelectItem(context, obj) {
        return {
            composeExtension: {
                  type: 'result',
                  attachmentLayout: 'list',
                  attachments: [CardFactory.thumbnailCard(obj.Item3)]
            }
        };
    } 
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "name": "composeExtension/selectItem",
    "type": "invoke",
    "value": {
        "Item1": "Package_Name",
        "Item2": "Version",
        "Item3": "Package Description"
    },
    .
    .
    .
}
```

* * *

> [!NOTE]
> `OnTeamsMessagingExtensionSelectItemAsync` n’est pas déclenché dans l’application Teams mobile.

## <a name="default-query"></a>Requête par défaut

Si vous avez la valeur définie `initialRun` `true` dans le manifeste, Microsoft Teams émet une requête **par défaut** lorsque l’utilisateur ouvre l’extension de message pour la première fois. Votre service peut répondre à cette requête avec un ensemble de résultats préremplis. Cela est utile lorsque votre commande de recherche nécessite une authentification ou une configuration, en affichant des éléments récemment consultés, des favoris ou toute autre information qui ne dépend pas de l’entrée utilisateur.

La requête par défaut a la même structure que n’importe quelle requête utilisateur normale, avec le `name` champ défini `initialRun` sur et `value` défini `true` sur comme indiqué dans l’objet suivant :

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

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Action d’extension de message Teams| Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’envoi du module de tâche. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Recherche d'extension des messages Teams   |  Décrit comment définir les commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Ajouter l’authentification à une extension de message](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>Voir aussi

[Ajouter une configuration à une extension de message](~/get-started/first-message-extension.md)
