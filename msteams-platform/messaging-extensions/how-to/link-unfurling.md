---
title: Lien unfurling
author: clearab
description: Comment effectuer un lien unfurling avec l’extension de messagerie dans une application Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5b20ea303a2c3d085651a53b01af4bb449d386de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674038"
---
# <a name="link-unfurling"></a><span data-ttu-id="8b6b0-103">Lien unfurling</span><span class="sxs-lookup"><span data-stu-id="8b6b0-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="8b6b0-104">Avec Link unfurling, votre application peut s’inscrire pour `invoke` recevoir une activité lorsque des URL avec un domaine particulier sont collées dans la zone de message de composition.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-104">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="8b6b0-105">L `invoke` 'contient l’URL complète qui a été collée dans la zone de message de composition, et vous pouvez répondre avec une carte que l’utilisateur peut *Unfurl*, fournissant des informations ou des actions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-105">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="8b6b0-106">Cela fonctionne de façon très similaire à une [commande de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md), avec l’URL servant de terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-106">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="8b6b0-107">L’extension de messagerie Azure DevOps utilise le lien unfurling pour rechercher les URL collées dans la zone de message de composition pointant vers un élément de travail.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-107">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="8b6b0-108">Dans la capture d’écran ci-dessous, un utilisateur a collé une URL pour un élément de travail dans Azure DevOps laquelle l’extension de messagerie a été résolue en carte.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-108">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Exemple de lien unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="8b6b0-110">Ajouter un lien unfurling à votre manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="8b6b0-110">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="8b6b0-111">Pour ce faire, vous allez ajouter un `messageHandlers` nouveau tableau à `composeExtensions` la section de votre manifeste d’application JSON.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-111">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="8b6b0-112">Vous pouvez le faire à l’aide de l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-112">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="8b6b0-113">Les listes de domaine peuvent inclure des caractères génériques `*.example.com`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-113">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="8b6b0-114">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-114">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="8b6b0-115">Utilisation d’App Studio</span><span class="sxs-lookup"><span data-stu-id="8b6b0-115">Using App Studio</span></span>

1. <span data-ttu-id="8b6b0-116">Dans App Studio, sous l’onglet Éditeur de manifeste, chargez votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-116">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="8b6b0-117">Sur la page **extension de messagerie** , ajoutez le domaine que vous souhaitez rechercher dans la section gestionnaires de **messages** , comme dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-117">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![section gestionnaires de messages dans App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="8b6b0-119">Manuellement</span><span class="sxs-lookup"><span data-stu-id="8b6b0-119">Manually</span></span>

<span data-ttu-id="8b6b0-120">Pour activer votre extension de messagerie de cette façon, vous devez d’abord ajouter le `messageHandlers` tableau à votre manifeste d’application, comme dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-120">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="8b6b0-121">Cet exemple n’est pas le manifeste complet, consultez la [référence de manifeste](~/resources/schema/manifest-schema.md) pour obtenir un exemple de manifeste complet.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-121">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
],
...
```

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="8b6b0-122">Gérer l' `composeExtension/queryLink` appel</span><span class="sxs-lookup"><span data-stu-id="8b6b0-122">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="8b6b0-123">Une fois que vous avez ajouté le domaine pour écouter le manifeste de l’application, vous devez mettre à jour votre code de service Web pour gérer la demande d’appel.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-123">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="8b6b0-124">Utilisez l’URL que vous recevez pour effectuer une recherche dans votre service et créer une réponse de carte.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-124">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="8b6b0-125">Si vous répondez avec plusieurs cartes, seule la première est utilisée.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-125">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="8b6b0-126">Nous prenons en charge les types de carte suivants :</span><span class="sxs-lookup"><span data-stu-id="8b6b0-126">We support the following card types:</span></span>

* [<span data-ttu-id="8b6b0-127">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="8b6b0-127">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="8b6b0-128">Carte héros</span><span class="sxs-lookup"><span data-stu-id="8b6b0-128">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="8b6b0-129">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="8b6b0-129">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="8b6b0-130">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="8b6b0-130">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="8b6b0-131">Voir [qu’est-ce que les cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-131">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="8b6b0-132">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8b6b0-132">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var heroCard = new ThumbnailCard
    {
        Title = "Thumbnail Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, heroCard);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="8b6b0-133">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="8b6b0-133">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="8b6b0-134">JSON</span><span class="sxs-lookup"><span data-stu-id="8b6b0-134">JSON</span></span>](#tab/json)

<span data-ttu-id="8b6b0-135">Voici un exemple de l' `invoke` envoi à votre bot.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-135">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="8b6b0-136">Vous trouverez ci-dessous un exemple de la réponse.</span><span class="sxs-lookup"><span data-stu-id="8b6b0-136">An example of the response is shown below.</span></span>

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
        }
      }
    ]
  }
}
```

* * *
