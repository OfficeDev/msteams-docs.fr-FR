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
# <a name="respond-to-the-search-command"></a><span data-ttu-id="3ee4c-103">Répondre à la commande de recherche</span><span class="sxs-lookup"><span data-stu-id="3ee4c-103">Respond to the search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="3ee4c-104">Votre service Web reçoit un `composeExtension/query` message d’appel qui contient un `value` objet avec les paramètres de recherche.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-104">Your web service will receive a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="3ee4c-105">Cet appel est déclenché :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-105">This invoke is triggered:</span></span>

* <span data-ttu-id="3ee4c-106">À mesure que des caractères sont entrés dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="3ee4c-107">Si `initialRun` est défini sur true dans votre manifeste de l’application, vous recevrez le message d’appel dès que la commande de recherche est appelée.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-107">If `initialRun` is set to true in your app manifest, you'll receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="3ee4c-108">Voir [requête par défaut](#default-query).</span><span class="sxs-lookup"><span data-stu-id="3ee4c-108">See [default query](#default-query).</span></span>

<span data-ttu-id="3ee4c-109">Les paramètres de la demande sont trouvés dans `value` l’objet de la demande, qui inclut les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-109">The request parameters itself are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="3ee4c-110">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="3ee4c-110">Property name</span></span> | <span data-ttu-id="3ee4c-111">Objectif</span><span class="sxs-lookup"><span data-stu-id="3ee4c-111">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="3ee4c-112">Nom de la commande appelée par l’utilisateur et correspondant à l’une des commandes déclarées dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-112">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="3ee4c-113">Tableau de paramètres.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-113">Array of parameters.</span></span> <span data-ttu-id="3ee4c-114">Chaque objet Parameter contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-114">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="3ee4c-115">Paramètres de pagination :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-115">Pagination parameters:</span></span> <br><span data-ttu-id="3ee4c-116">`skip`: ignorer le nombre pour cette requête</span><span class="sxs-lookup"><span data-stu-id="3ee4c-116">`skip`: skip count for this query</span></span> <br><span data-ttu-id="3ee4c-117">`count`: nombre d’éléments à renvoyer</span><span class="sxs-lookup"><span data-stu-id="3ee4c-117">`count`: number of elements to return</span></span> |

# <a name="cnettabdotnet"></a>[<span data-ttu-id="3ee4c-118">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3ee4c-118">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="3ee4c-119">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="3ee4c-119">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="3ee4c-120">JSON</span><span class="sxs-lookup"><span data-stu-id="3ee4c-120">JSON</span></span>](#tab/json)

<span data-ttu-id="3ee4c-121">Le JSON ci-dessous est raccourci pour mettre en évidence les sections les plus pertinentes.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-121">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="3ee4c-122">Répondre aux demandes de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="3ee4c-122">Respond to user requests</span></span>

<span data-ttu-id="3ee4c-123">Lorsque l’utilisateur effectue une requête, Microsoft teams émet une demande HTTP synchrone à votre service.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-123">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="3ee4c-124">À ce stade, votre code dispose de 5 secondes pour fournir une réponse HTTP à la demande.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-124">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="3ee4c-125">Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour traiter la demande.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-125">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="3ee4c-126">Votre service doit répondre avec les résultats correspondant à la requête de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-126">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="3ee4c-127">La réponse doit indiquer un code d’état HTTP `200 OK` de et un objet application/JSON valide avec le corps suivant :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-127">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="3ee4c-128">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="3ee4c-128">Property name</span></span>|<span data-ttu-id="3ee4c-129">Objectif</span><span class="sxs-lookup"><span data-stu-id="3ee4c-129">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="3ee4c-130">Enveloppe de réponse de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-130">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="3ee4c-131">Type de réponse.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-131">Type of response.</span></span> <span data-ttu-id="3ee4c-132">Les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-132">The following types are supported:</span></span> <br><span data-ttu-id="3ee4c-133">`result`: affiche une liste de résultats de recherche</span><span class="sxs-lookup"><span data-stu-id="3ee4c-133">`result`: displays a list of search results</span></span> <br><span data-ttu-id="3ee4c-134">`auth`: demande à l’utilisateur de s’authentifier</span><span class="sxs-lookup"><span data-stu-id="3ee4c-134">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="3ee4c-135">`config`: demande à l’utilisateur de configurer l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="3ee4c-135">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="3ee4c-136">`message`: affiche un message en texte brut.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-136">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="3ee4c-137">Spécifie la disposition des pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-137">Specifies the layout of the attachments.</span></span> <span data-ttu-id="3ee4c-138">Utilisé pour les réponses de `result`type.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-138">Used for responses of type `result`.</span></span> <br><span data-ttu-id="3ee4c-139">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-139">Currently the following types are supported:</span></span> <br><span data-ttu-id="3ee4c-140">`list`: liste d’objets Card contenant des champs de miniature, de titre et de texte</span><span class="sxs-lookup"><span data-stu-id="3ee4c-140">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="3ee4c-141">`grid`: grille d’images miniatures</span><span class="sxs-lookup"><span data-stu-id="3ee4c-141">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="3ee4c-142">Tableau d’objets Attachment valides.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-142">Array of valid attachment objects.</span></span> <span data-ttu-id="3ee4c-143">Utilisé pour les réponses de `result`type.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-143">Used for responses of type `result`.</span></span> <br><span data-ttu-id="3ee4c-144">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-144">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="3ee4c-145">Actions suggérées.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-145">Suggested actions.</span></span> <span data-ttu-id="3ee4c-146">Utilisé pour les réponses de `auth` type `config`ou.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-146">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="3ee4c-147">Message à afficher.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-147">Message to display.</span></span> <span data-ttu-id="3ee4c-148">Utilisé pour les réponses de `message`type.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-148">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="3ee4c-149">Types et aperçus des cartes de réponse</span><span class="sxs-lookup"><span data-stu-id="3ee4c-149">Response card types and previews</span></span>

<span data-ttu-id="3ee4c-150">Nous prenons en charge les types de pièces jointes suivants :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-150">We support the following attachment types:</span></span>

* [<span data-ttu-id="3ee4c-151">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="3ee4c-151">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="3ee4c-152">Carte héros</span><span class="sxs-lookup"><span data-stu-id="3ee4c-152">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="3ee4c-153">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="3ee4c-153">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="3ee4c-154">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="3ee4c-154">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="3ee4c-155">Voir [qu’est-ce que les cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-155">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="3ee4c-156">Pour en savoir plus sur l’utilisation des types de cartes miniature et héros, consultez la rubrique [Ajouter des cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="3ee4c-156">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="3ee4c-157">Pour plus d’informations sur la carte de connecteur Office 365, voir [using office 365 Connector Cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="3ee4c-157">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="3ee4c-158">La liste des résultats est affichée dans l’interface utilisateur Microsoft teams avec un aperçu de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-158">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="3ee4c-159">L’aperçu est généré de l’une des deux façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ee4c-159">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="3ee4c-160">À l' `preview` aide de la `attachment` propriété au sein de l’objet.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-160">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="3ee4c-161">La `preview` pièce jointe peut uniquement être une carte de héros ou de miniature.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-161">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="3ee4c-162">Extrait des propriétés de `title`base `text`, et `image` de la pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-162">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="3ee4c-163">Celles-ci sont utilisées uniquement `preview` si la propriété n’est pas définie et que ces propriétés sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-163">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="3ee4c-164">Vous pouvez afficher un aperçu d’une carte adaptative ou d’une carte de connecteur Office 365 dans la liste des résultats en fonction de sa propriété preview.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-164">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list simply by its preview property.</span></span> <span data-ttu-id="3ee4c-165">Cela n’est pas nécessaire si les résultats sont déjà des cartes de la héros ou des miniatures.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-165">This is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="3ee4c-166">Si vous utilisez la pièce jointe d’aperçu, il doit s’agir d’une carte de héros ou d’une carte miniature.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-166">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="3ee4c-167">Si aucune propriété Preview n’est spécifiée, l’aperçu de la carte échoue et rien ne s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-167">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="3ee4c-168">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="3ee4c-168">Response example</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="3ee4c-169">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3ee4c-169">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="3ee4c-170">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="3ee4c-170">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="3ee4c-171">JSON</span><span class="sxs-lookup"><span data-stu-id="3ee4c-171">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="3ee4c-172">Requête par défaut</span><span class="sxs-lookup"><span data-stu-id="3ee4c-172">Default query</span></span>

<span data-ttu-id="3ee4c-173">Si vous définissez `initialRun` dans `true` le manifeste, Microsoft teams émet une requête « par défaut » lorsque l’utilisateur ouvre l’extension de messagerie pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-173">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="3ee4c-174">Votre service peut répondre à cette requête avec un ensemble de résultats pré-renseignés.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-174">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="3ee4c-175">Cela peut être utile lorsque votre commande de recherche nécessite une authentification ou une configuration, en affichant les éléments récemment consultés, les favoris ou toute autre information qui ne dépend pas de l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-175">This can be useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="3ee4c-176">La requête par défaut a la même structure que toute requête utilisateur normale, avec `name` le champ défini `initialRun` sur `value` et défini `true` sur comme dans l’objet ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3ee4c-176">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as in the object below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3ee4c-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ee4c-177">Next Steps</span></span>

<span data-ttu-id="3ee4c-178">Ajouter une authentification et/ou une configuration</span><span class="sxs-lookup"><span data-stu-id="3ee4c-178">Add authentication and/or configuration</span></span>

* [<span data-ttu-id="3ee4c-179">Ajouter l’authentification à une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="3ee4c-179">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="3ee4c-180">Ajouter une configuration à une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="3ee4c-180">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="3ee4c-181">Déployer la configuration</span><span class="sxs-lookup"><span data-stu-id="3ee4c-181">Deploy configuration</span></span>

* [<span data-ttu-id="3ee4c-182">Déployer votre package d’application</span><span class="sxs-lookup"><span data-stu-id="3ee4c-182">Deploy your app package</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
