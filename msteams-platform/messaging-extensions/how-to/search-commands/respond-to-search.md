---
title: Répondre à la commande de recherche
author: clearab
description: Comment répondre à la commande de recherche à partir d’une extension de messagerie dans une Microsoft Teams app.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 15b48b135f656feeb3cfb28ffbe12852ddb66359
ms.sourcegitcommit: e50cdeb6b7f481e12911b2bb74a8da22af0bffac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2021
ms.locfileid: "52710633"
---
# <a name="respond-to-search-command"></a><span data-ttu-id="934a7-103">Répondre à la commande de recherche</span><span class="sxs-lookup"><span data-stu-id="934a7-103">Respond to search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="934a7-104">Une fois que l’utilisateur a soumis la commande de recherche, votre service web reçoit un message d’appel qui contient un objet avec `composeExtension/query` `value` les paramètres de recherche.</span><span class="sxs-lookup"><span data-stu-id="934a7-104">After the user submits the search command, your web service receives a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="934a7-105">Cet appel est déclenché dans les conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="934a7-105">This invoke is triggered with the following conditions:</span></span>

* <span data-ttu-id="934a7-106">À mesure que des caractères sont entrés dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="934a7-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="934a7-107">`initialRun` est définie sur true dans le manifeste de votre application, vous recevez le message d’appel dès que la commande de recherche est invoquée.</span><span class="sxs-lookup"><span data-stu-id="934a7-107">`initialRun` is set to true in your app manifest, you receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="934a7-108">Pour plus d’informations, [voir la requête par défaut.](#default-query)</span><span class="sxs-lookup"><span data-stu-id="934a7-108">For more information, see [default query](#default-query).</span></span>

<span data-ttu-id="934a7-109">Ce document vous guide sur la façon de répondre aux demandes des utilisateurs sous forme de cartes et d’aperçus, ainsi que sur les conditions dans lesquelles Microsoft Teams une requête par défaut.</span><span class="sxs-lookup"><span data-stu-id="934a7-109">This document guides you on how to respond to user requests in the form of cards and previews, and the conditions under which Microsoft Teams issues a default query.</span></span>

<span data-ttu-id="934a7-110">Les paramètres de requête se trouvent dans `value` l’objet de la demande, qui inclut les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="934a7-110">The request parameters are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="934a7-111">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="934a7-111">Property name</span></span> | <span data-ttu-id="934a7-112">Objectif</span><span class="sxs-lookup"><span data-stu-id="934a7-112">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="934a7-113">Nom de la commande invoquée par l’utilisateur, correspondant à l’une des commandes déclarées dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="934a7-113">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="934a7-114">Tableau de paramètres.</span><span class="sxs-lookup"><span data-stu-id="934a7-114">Array of parameters.</span></span> <span data-ttu-id="934a7-115">Chaque objet parameter contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="934a7-115">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="934a7-116">Paramètres de pagination :</span><span class="sxs-lookup"><span data-stu-id="934a7-116">Pagination parameters:</span></span> <br><span data-ttu-id="934a7-117">`skip`: Ignorer le nombre pour cette requête</span><span class="sxs-lookup"><span data-stu-id="934a7-117">`skip`: Skip count for this query</span></span> <br><span data-ttu-id="934a7-118">`count`: Nombre d’éléments à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="934a7-118">`count`: Number of elements to return.</span></span> |

# <a name="cnet"></a>[<span data-ttu-id="934a7-119">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="934a7-119">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="934a7-120">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="934a7-120">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[<span data-ttu-id="934a7-121">JSON</span><span class="sxs-lookup"><span data-stu-id="934a7-121">JSON</span></span>](#tab/json)

<span data-ttu-id="934a7-122">Le JSON ci-dessous est raccourci pour mettre en évidence les sections les plus pertinentes.</span><span class="sxs-lookup"><span data-stu-id="934a7-122">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="934a7-123">Répondre aux demandes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="934a7-123">Respond to user requests</span></span>

<span data-ttu-id="934a7-124">Lorsque l’utilisateur effectue une requête, Microsoft Teams une requête HTTP synchrone à votre service.</span><span class="sxs-lookup"><span data-stu-id="934a7-124">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="934a7-125">À ce stade, votre code dispose de `5` secondes pour fournir une réponse HTTP à la demande.</span><span class="sxs-lookup"><span data-stu-id="934a7-125">At that point, your code has `5` seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="934a7-126">Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="934a7-126">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="934a7-127">Votre service doit répondre avec les résultats correspondant à la requête de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="934a7-127">Your service must respond with the results matching the user query.</span></span> <span data-ttu-id="934a7-128">La réponse doit indiquer un code d’état HTTP et un objet JSON ou application valide avec `200 OK` les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="934a7-128">The response must indicate an HTTP status code of `200 OK` and a valid application or JSON object with the following properties:</span></span>

|<span data-ttu-id="934a7-129">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="934a7-129">Property name</span></span>|<span data-ttu-id="934a7-130">Objectif</span><span class="sxs-lookup"><span data-stu-id="934a7-130">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="934a7-131">Enveloppe de réponse de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="934a7-131">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="934a7-132">Type de réponse.</span><span class="sxs-lookup"><span data-stu-id="934a7-132">Type of response.</span></span> <span data-ttu-id="934a7-133">Les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="934a7-133">The following types are supported:</span></span> <br><span data-ttu-id="934a7-134">`result`: affiche une liste de résultats de recherche</span><span class="sxs-lookup"><span data-stu-id="934a7-134">`result`: Displays a list of search results</span></span> <br><span data-ttu-id="934a7-135">`auth`: Demande à l’utilisateur de s’authentifier</span><span class="sxs-lookup"><span data-stu-id="934a7-135">`auth`: Asks the user to authenticate</span></span> <br><span data-ttu-id="934a7-136">`config`: Demande à l’utilisateur de configurer l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="934a7-136">`config`: Asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="934a7-137">`message`: affiche un message en texte simple</span><span class="sxs-lookup"><span data-stu-id="934a7-137">`message`: Displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="934a7-138">Spécifie la disposition des pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="934a7-138">Specifies the layout of the attachments.</span></span> <span data-ttu-id="934a7-139">Utilisé pour les réponses de type `result` .</span><span class="sxs-lookup"><span data-stu-id="934a7-139">Used for responses of type `result`.</span></span> <br><span data-ttu-id="934a7-140">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="934a7-140">Currently, the following types are supported:</span></span> <br><span data-ttu-id="934a7-141">`list`: Liste d’objets de carte contenant des champs de miniature, de titre et de texte</span><span class="sxs-lookup"><span data-stu-id="934a7-141">`list`: A list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="934a7-142">`grid`: grille d’images miniatures</span><span class="sxs-lookup"><span data-stu-id="934a7-142">`grid`: A grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="934a7-143">Tableau d’objets pièce jointe valides.</span><span class="sxs-lookup"><span data-stu-id="934a7-143">Array of valid attachment objects.</span></span> <span data-ttu-id="934a7-144">Utilisé pour les réponses de type `result` .</span><span class="sxs-lookup"><span data-stu-id="934a7-144">Used for responses of type `result`.</span></span> <br><span data-ttu-id="934a7-145">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="934a7-145">Currently, the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="934a7-146">Actions suggérées.</span><span class="sxs-lookup"><span data-stu-id="934a7-146">Suggested actions.</span></span> <span data-ttu-id="934a7-147">Utilisé pour les réponses de type `auth` `config` ou .</span><span class="sxs-lookup"><span data-stu-id="934a7-147">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="934a7-148">Message à afficher.</span><span class="sxs-lookup"><span data-stu-id="934a7-148">Message to display.</span></span> <span data-ttu-id="934a7-149">Utilisé pour les réponses de type `message` .</span><span class="sxs-lookup"><span data-stu-id="934a7-149">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="934a7-150">Types et aperçus de cartes de réponse</span><span class="sxs-lookup"><span data-stu-id="934a7-150">Response card types and previews</span></span>

<span data-ttu-id="934a7-151">Teams prend en charge les types de carte suivants :</span><span class="sxs-lookup"><span data-stu-id="934a7-151">Teams supports the following card types:</span></span>

* [<span data-ttu-id="934a7-152">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="934a7-152">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="934a7-153">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="934a7-153">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="934a7-154">Office 365 Carte de connecteur</span><span class="sxs-lookup"><span data-stu-id="934a7-154">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="934a7-155">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="934a7-155">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="934a7-156">Pour avoir une meilleure compréhension et une meilleure vue d’ensemble des cartes, voyez [ce que sont les cartes.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="934a7-156">To have a better understanding and overview on cards, see [what are cards](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="934a7-157">Pour découvrir comment utiliser les types de carte miniature et hero, voir ajouter des cartes et [des actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="934a7-157">To learn how to use the thumbnail and hero card types, see [add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="934a7-158">Pour plus d’informations sur la carte connecteur Office 365, voir Utilisation de [cartes Office 365 connecteur.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="934a7-158">For additional information regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="934a7-159">La liste des résultats s’affiche dans l Microsoft Teams’interface utilisateur avec un aperçu de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="934a7-159">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="934a7-160">L’aperçu est généré de l’une des deux manières :</span><span class="sxs-lookup"><span data-stu-id="934a7-160">The preview is generated in one of the two ways:</span></span>

* <span data-ttu-id="934a7-161">Utilisation de la `preview` propriété dans `attachment` l’objet.</span><span class="sxs-lookup"><span data-stu-id="934a7-161">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="934a7-162">La `preview` pièce jointe ne peut être qu’une carte hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="934a7-162">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="934a7-163">Extrait de la base `title` et `text` des `image` propriétés de la pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="934a7-163">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="934a7-164">Elles sont utilisées uniquement si la `preview` propriété n’est pas définie et que ces propriétés sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="934a7-164">These are used only if the `preview` property is not set and these properties are available.</span></span>
* <span data-ttu-id="934a7-165">Les actions d’appui et de bouton de carte Hero ou Miniature, sauf appel, ne sont pas prises en charge dans la carte d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="934a7-165">The Hero or Thumbnail card button and tap actions, except invoke, are not supported in the preview card.</span></span>

<span data-ttu-id="934a7-166">Vous pouvez afficher un aperçu d’une carte adaptative ou d’une carte connecteur Office 365 dans la liste des résultats à l’aide de sa propriété d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="934a7-166">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list using its preview property.</span></span> <span data-ttu-id="934a7-167">La propriété d’aperçu n’est pas nécessaire si les résultats sont déjà des cartes Hero ou Thumbnail.</span><span class="sxs-lookup"><span data-stu-id="934a7-167">The preview property is not necessary if the results are already Hero or Thumbnail cards.</span></span> <span data-ttu-id="934a7-168">Si vous utilisez la pièce jointe d’aperçu, il doit s’agit d’une carte Hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="934a7-168">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="934a7-169">Si aucune propriété d’aperçu n’est spécifiée, l’aperçu de la carte échoue et rien n’est affiché.</span><span class="sxs-lookup"><span data-stu-id="934a7-169">If no preview property is specified, the preview of the card fails and nothing is displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="934a7-170">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="934a7-170">Response example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="934a7-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="934a7-171">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="934a7-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="934a7-172">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="934a7-173">JSON</span><span class="sxs-lookup"><span data-stu-id="934a7-173">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="934a7-174">Requête par défaut</span><span class="sxs-lookup"><span data-stu-id="934a7-174">Default query</span></span>

<span data-ttu-id="934a7-175">Si vous l’avez définie dans le manifeste, Microsoft Teams une requête par défaut lorsque l’utilisateur ouvre l’extension de messagerie pour la `initialRun` `true` première fois. </span><span class="sxs-lookup"><span data-stu-id="934a7-175">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a **default** query when the user first opens the messaging extension.</span></span> <span data-ttu-id="934a7-176">Votre service peut répondre à cette requête avec un ensemble de résultats pré-rempli.</span><span class="sxs-lookup"><span data-stu-id="934a7-176">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="934a7-177">Cela est utile lorsque votre commande de recherche nécessite une authentification ou une configuration, en affichant les éléments récemment affichés, les favoris ou toute autre information qui ne dépend pas de l’entrée utilisateur.</span><span class="sxs-lookup"><span data-stu-id="934a7-177">This is useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="934a7-178">La requête par défaut a la même structure que n’importe quelle requête utilisateur normale, avec le champ définie sur et définie sur comme indiqué `name` `initialRun` dans `value` `true` l’objet suivant :</span><span class="sxs-lookup"><span data-stu-id="934a7-178">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as shown in the following object:</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="934a7-179">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="934a7-179">Code sample</span></span>

| <span data-ttu-id="934a7-180">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="934a7-180">Sample Name</span></span>           | <span data-ttu-id="934a7-181">Description</span><span class="sxs-lookup"><span data-stu-id="934a7-181">Description</span></span> | <span data-ttu-id="934a7-182">.NET</span><span class="sxs-lookup"><span data-stu-id="934a7-182">.NET</span></span>    | <span data-ttu-id="934a7-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="934a7-183">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="934a7-184">Teams d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="934a7-184">Teams messaging extension action</span></span>| <span data-ttu-id="934a7-185">Décrit comment définir des commandes d’action, créer un module de tâche et répondre à une action d’soumission de module de tâche.</span><span class="sxs-lookup"><span data-stu-id="934a7-185">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="934a7-186">View</span><span class="sxs-lookup"><span data-stu-id="934a7-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="934a7-187">View</span><span class="sxs-lookup"><span data-stu-id="934a7-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="934a7-188">Teams d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="934a7-188">Teams messaging extension search</span></span>   |  <span data-ttu-id="934a7-189">Décrit comment définir des commandes de recherche et répondre aux recherches.</span><span class="sxs-lookup"><span data-stu-id="934a7-189">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="934a7-190">View</span><span class="sxs-lookup"><span data-stu-id="934a7-190">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="934a7-191">View</span><span class="sxs-lookup"><span data-stu-id="934a7-191">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="934a7-192">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="934a7-192">See also</span></span>

[<span data-ttu-id="934a7-193">Ajouter une configuration à une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="934a7-193">Add configuration to a messaging extension</span></span>](~/get-started/first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="934a7-194">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="934a7-194">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="934a7-195">Ajouter l’authentification à une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="934a7-195">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)



