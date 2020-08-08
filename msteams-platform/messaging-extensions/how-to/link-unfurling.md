---
title: Déploiement de lien
author: clearab
description: Comment effectuer un lien unfurling avec l’extension de messagerie dans une application Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 32d19fcd44f2475047539350706d2745aeec3691
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587803"
---
# <a name="link-unfurling"></a><span data-ttu-id="9f55c-103">Déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="9f55c-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="9f55c-104">Actuellement, Link unfurling n’est pas pris en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="9f55c-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="9f55c-105">Avec de déploiement de lien, votre application peut s’inscrire pour recevoir une activité `invoke` lorsque les URL avec un domaine particulier sont collées dans la zone rédaction d’un message.</span><span class="sxs-lookup"><span data-stu-id="9f55c-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="9f55c-106">L' `invoke` contient l’URL complète qui a été collée dans la zone de message de composition, et vous pouvez répondre avec une carte que l’utilisateur peut *Unfurl*, fournissant des informations ou des actions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9f55c-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="9f55c-107">Cela fonctionne de façon très similaire à une [commande de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md), avec l’URL servant de terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="9f55c-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="9f55c-108">L’extension de messagerie Azure DevOps utilise le lien unfurling pour rechercher les URL collées dans la zone de message de composition pointant vers un élément de travail.</span><span class="sxs-lookup"><span data-stu-id="9f55c-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="9f55c-109">Dans la capture d’écran ci-dessous, un utilisateur a collé une URL pour un élément de travail dans Azure DevOps laquelle l’extension de messagerie a été résolue en carte.</span><span class="sxs-lookup"><span data-stu-id="9f55c-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Exemple de lien unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="9f55c-111">Ajouter un lien unfurling à votre manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="9f55c-111">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="9f55c-112">Pour ce faire, vous allez ajouter un nouveau `messageHandlers` tableau à la `composeExtensions` section de votre manifeste d’application JSON.</span><span class="sxs-lookup"><span data-stu-id="9f55c-112">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="9f55c-113">Vous pouvez le faire à l’aide de l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="9f55c-113">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="9f55c-114">Les listes de domaine peuvent inclure des caractères génériques, par exemple `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="9f55c-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="9f55c-115">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="9f55c-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="9f55c-116">Utilisation de App Studio</span><span class="sxs-lookup"><span data-stu-id="9f55c-116">Using App Studio</span></span>

1. <span data-ttu-id="9f55c-117">Dans App Studio, sous l’onglet Éditeur de manifeste, chargez votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="9f55c-117">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="9f55c-118">Sur la page **extension de messagerie** , ajoutez le domaine que vous souhaitez rechercher dans la section gestionnaires de **messages** , comme dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9f55c-118">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![section gestionnaires de messages dans App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="9f55c-120">Manuellement</span><span class="sxs-lookup"><span data-stu-id="9f55c-120">Manually</span></span>

<span data-ttu-id="9f55c-121">Pour activer votre extension de messagerie de cette façon, vous devez d’abord ajouter le `messageHandlers` tableau à votre manifeste d’application, comme dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9f55c-121">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="9f55c-122">Cet exemple n’est pas le manifeste complet, consultez la [référence de manifeste](~/resources/schema/manifest-schema.md) pour obtenir un exemple de manifeste complet.</span><span class="sxs-lookup"><span data-stu-id="9f55c-122">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="9f55c-123">Gérer l' `composeExtension/queryLink` appel</span><span class="sxs-lookup"><span data-stu-id="9f55c-123">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="9f55c-124">Une fois que vous avez ajouté le domaine pour écouter le manifeste de l’application, vous devez mettre à jour votre code de service Web pour gérer la demande d’appel.</span><span class="sxs-lookup"><span data-stu-id="9f55c-124">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="9f55c-125">Utilisez l’URL que vous recevez pour effectuer une recherche dans votre service et créer une réponse de carte.</span><span class="sxs-lookup"><span data-stu-id="9f55c-125">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="9f55c-126">Si vous répondez avec plusieurs cartes, seule la première est utilisée.</span><span class="sxs-lookup"><span data-stu-id="9f55c-126">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="9f55c-127">Nous prenons en charge les types de carte suivants :</span><span class="sxs-lookup"><span data-stu-id="9f55c-127">We support the following card types:</span></span>

* [<span data-ttu-id="9f55c-128">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="9f55c-128">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="9f55c-129">Carte héros</span><span class="sxs-lookup"><span data-stu-id="9f55c-129">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="9f55c-130">Carte de connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="9f55c-130">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="9f55c-131">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="9f55c-131">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="9f55c-132">Voir [qu’est-ce que les cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="9f55c-132">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9f55c-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9f55c-133">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9f55c-134">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9f55c-134">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="9f55c-135">JSON</span><span class="sxs-lookup"><span data-stu-id="9f55c-135">JSON</span></span>](#tab/json)

<span data-ttu-id="9f55c-136">Voici un exemple de l' `invoke` envoi à votre bot.</span><span class="sxs-lookup"><span data-stu-id="9f55c-136">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="9f55c-137">Vous trouverez ci-dessous un exemple de la réponse.</span><span class="sxs-lookup"><span data-stu-id="9f55c-137">An example of the response is shown below.</span></span>

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
