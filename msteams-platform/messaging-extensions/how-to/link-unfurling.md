---
title: Déploiement de lien
author: clearab
description: Comment effectuer un déploiement de lien avec l’extension de messagerie dans une application Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845636"
---
# <a name="link-unfurling"></a><span data-ttu-id="7aeb5-103">Déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="7aeb5-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="7aeb5-104">Actuellement, le déploiement de liens n’est pas pris en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="7aeb5-105">Avec de déploiement de lien, votre application peut s’inscrire pour recevoir une activité `invoke` lorsque les URL avec un domaine particulier sont collées dans la zone rédaction d’un message.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="7aeb5-106">Celui-ci contient l’URL complète qui a été passée dans la zone de rédaction du message, et vous pouvez répondre avec une carte que l’utilisateur peut déployer, fournissant des informations ou `invoke` des actions supplémentaires. </span><span class="sxs-lookup"><span data-stu-id="7aeb5-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="7aeb5-107">Cela fonctionne de manière très similaire à une [commande de](~/messaging-extensions/how-to/search-commands/define-search-command.md)recherche, avec l’URL servant de terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="7aeb5-108">L’extension de messagerie Azure DevOps utilise le déploiement de lien pour rechercher les URL qui sont passées dans la zone de composition du message pointant vers un élément de travail.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="7aeb5-109">Dans la capture d’écran ci-dessous, un utilisateur a passé une URL pour un élément de travail dans Azure DevOps que l’extension de messagerie a résolue en une carte.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="7aeb5-111">Ajouter le déploiement de lien au manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="7aeb5-111">Add link unfurling to your app manifest</span></span>

 <span data-ttu-id="7aeb5-112">Pour ajouter le déploiement de lien au manifeste de votre application, ajoutez un nouveau tableau à la `messageHandlers` `composeExtensions` section du manifeste JSON de votre application.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-112">To add link unfurling to your app manifest add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="7aeb5-113">Vous pouvez ajouter le tableau à l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-113">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="7aeb5-114">Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="7aeb5-115">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="7aeb5-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="7aeb5-116">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-116">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="7aeb5-117">Par exemple, yourapp.onmicrosoft.com est valide, mais \*.onmicrosoft.com n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-117">For example, yourapp.onmicrosoft.com is valid, but \*.onmicrosoft.com is not valid.</span></span> <span data-ttu-id="7aeb5-118">En outre, les domaines de niveau supérieur sont interdits.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-118">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="7aeb5-119">Par exemple, \*.com, \*.org.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-119">For example, \*.com, \*.org.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="7aeb5-120">Utilisation de App Studio</span><span class="sxs-lookup"><span data-stu-id="7aeb5-120">Using App Studio</span></span>

1. <span data-ttu-id="7aeb5-121">Dans App Studio, sous l’onglet Éditeur de manifeste, chargez le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-121">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="7aeb5-122">Dans la page **Extension de** messagerie, ajoutez le domaine que vous souhaitez rechercher dans la section Des **handlers** de messages, comme dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-122">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![section des handlers de messages dans App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="7aeb5-124">Manuellement</span><span class="sxs-lookup"><span data-stu-id="7aeb5-124">Manually</span></span>

<span data-ttu-id="7aeb5-125">Pour permettre à votre extension de messagerie d’interagir avec les liens de cette façon, vous devez d’abord ajouter le tableau au manifeste de votre application, comme dans `messageHandlers` l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-125">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="7aeb5-126">Cet exemple n’est pas le manifeste complet, voir [la référence de](~/resources/schema/manifest-schema.md) manifeste pour obtenir un exemple de manifeste complet.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-126">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="7aeb5-127">Gérer `composeExtension/queryLink` l’appel</span><span class="sxs-lookup"><span data-stu-id="7aeb5-127">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="7aeb5-128">Une fois que vous avez ajouté le domaine pour écouter le manifeste de l’application, vous devez mettre à jour votre code de service web pour gérer la demande d’appel.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-128">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="7aeb5-129">Utilisez l’URL que vous recevez pour effectuer une recherche dans votre service et créer une réponse de carte.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-129">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="7aeb5-130">Si vous répondez avec plusieurs cartes, seule la première sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-130">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="7aeb5-131">Nous prise en charge les types de carte suivants :</span><span class="sxs-lookup"><span data-stu-id="7aeb5-131">We support the following card types:</span></span>

* [<span data-ttu-id="7aeb5-132">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="7aeb5-132">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="7aeb5-133">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="7aeb5-133">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="7aeb5-134">Carte connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="7aeb5-134">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="7aeb5-135">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="7aeb5-135">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="7aeb5-136">Voir [Quelles sont les cartes pour](~/task-modules-and-cards/what-are-cards.md) obtenir une vue d’ensemble .</span><span class="sxs-lookup"><span data-stu-id="7aeb5-136">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7aeb5-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7aeb5-137">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7aeb5-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7aeb5-138">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="7aeb5-139">JSON</span><span class="sxs-lookup"><span data-stu-id="7aeb5-139">JSON</span></span>](#tab/json)

<span data-ttu-id="7aeb5-140">Voici un exemple de `invoke` l’envoi à votre bot.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-140">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="7aeb5-141">Un exemple de réponse est illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7aeb5-141">An example of the response is shown below.</span></span>

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
