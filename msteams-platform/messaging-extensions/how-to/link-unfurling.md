---
title: Déploiement de lien
author: clearab
description: Comment effectuer un déploiement de lien avec l’extension de messagerie dans une Microsoft Teams application.
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 405b320b887300837d51332a9548ff60aff450d0
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630683"
---
# <a name="link-unfurling"></a><span data-ttu-id="ca5fe-103">Déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="ca5fe-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="ca5fe-104">Ce document vous guide sur la façon d’ajouter le déploiement de lien au manifeste de votre application à l’aide d’App studio et manuellement.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="ca5fe-105">Avec de déploiement de lien, votre application peut s’inscrire pour recevoir une activité `invoke` lorsque les URL avec un domaine particulier sont collées dans la zone rédaction d’un message.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="ca5fe-106">Contient l’URL complète qui a été passée dans la zone de rédaction du message et vous pouvez répondre avec une carte que l’utilisateur peut déployer, fournissant des informations ou `invoke` des actions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="ca5fe-107">Cela fonctionne comme une commande de recherche avec l’URL servant de terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> <span data-ttu-id="ca5fe-108">Actuellement, le déploiement de liaison n’est pas pris en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-108">Currently, link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="ca5fe-109">L Azure DevOps de messagerie utilise le déploiement de liaison pour rechercher les URL qui sont passées dans la zone de composition du message pointant vers un élément de travail.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-109">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="ca5fe-110">Dans l’image suivante, un utilisateur a passé une URL pour un élément de travail dans Azure DevOps, que l’extension de messagerie a résolue en une carte :</span><span class="sxs-lookup"><span data-stu-id="ca5fe-110">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="ca5fe-112">Ajouter le déploiement de lien au manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="ca5fe-112">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="ca5fe-113">Pour ajouter le déploiement de lien au manifeste de votre application, ajoutez un nouveau tableau à la `messageHandlers` `composeExtensions` section du manifeste JSON de votre application.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-113">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="ca5fe-114">Vous pouvez ajouter le tableau à l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-114">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="ca5fe-115">Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-115">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="ca5fe-116">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="ca5fe-116">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="ca5fe-117">Donot add domains that are not in your control, either directly or through wildcards.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-117">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="ca5fe-118">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` non valide.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-118">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="ca5fe-119">En outre, les domaines de niveau supérieur sont interdits.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-119">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="ca5fe-120">Par exemple, `*.com` . `*.org`</span><span class="sxs-lookup"><span data-stu-id="ca5fe-120">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="ca5fe-121">Ajouter un déploiement de lien à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="ca5fe-121">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="ca5fe-122">Ouvrez **App Studio** à partir Microsoft Teams client, puis sélectionnez l’onglet **Éditeur de** manifeste.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-122">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="ca5fe-123">Chargez le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-123">Load your app manifest.</span></span>
1. <span data-ttu-id="ca5fe-124">Dans la page **Extension de** messagerie, ajoutez le domaine que vous souhaitez rechercher dans la section Des **handlers de** messages.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-124">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="ca5fe-125">L’image suivante explique le processus :</span><span class="sxs-lookup"><span data-stu-id="ca5fe-125">The following image explains the process:</span></span>

    ![section des handlers de messages dans App Studio](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="ca5fe-127">Ajouter manuellement le déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="ca5fe-127">Add link unfurling manually</span></span>

<span data-ttu-id="ca5fe-128">Pour permettre à votre extension de messagerie d’interagir avec des liens, vous devez d’abord ajouter le `messageHandlers` tableau au manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-128">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="ca5fe-129">L’exemple suivant explique comment ajouter manuellement le déploiement de lien :</span><span class="sxs-lookup"><span data-stu-id="ca5fe-129">The following example explains how to add link unfurling manually:</span></span> 


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

<span data-ttu-id="ca5fe-130">Pour obtenir un exemple de manifeste complet, voir [la référence de manifeste.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="ca5fe-130">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="ca5fe-131">Gérer `composeExtension/queryLink` l’appel</span><span class="sxs-lookup"><span data-stu-id="ca5fe-131">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="ca5fe-132">Après avoir ajouté le domaine au manifeste de l’application, vous devez mettre à jour votre code de service web pour gérer la demande d’appel.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-132">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="ca5fe-133">Utilisez l’URL reçue pour effectuer une recherche dans votre service et créer une réponse de carte.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-133">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="ca5fe-134">Si vous répondez avec plusieurs cartes, seule la première réponse de carte est utilisée.</span><span class="sxs-lookup"><span data-stu-id="ca5fe-134">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="ca5fe-135">Les types de carte suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="ca5fe-135">The following card types are supported:</span></span>

* [<span data-ttu-id="ca5fe-136">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="ca5fe-136">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="ca5fe-137">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="ca5fe-137">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="ca5fe-138">Office 365 Carte de connecteur</span><span class="sxs-lookup"><span data-stu-id="ca5fe-138">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="ca5fe-139">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="ca5fe-139">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="ca5fe-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="ca5fe-140">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ca5fe-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ca5fe-141">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ca5fe-142">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca5fe-142">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="ca5fe-143">JSON</span><span class="sxs-lookup"><span data-stu-id="ca5fe-143">JSON</span></span>](#tab/json)

<span data-ttu-id="ca5fe-144">Voici un exemple de `invoke` l’envoi à votre bot :</span><span class="sxs-lookup"><span data-stu-id="ca5fe-144">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="ca5fe-145">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="ca5fe-145">Following is an example of the response:</span></span>

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
        }
      }
    ]
  }
}
```

* * *

## <a name="see-also"></a><span data-ttu-id="ca5fe-146">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ca5fe-146">See also</span></span> 

* [<span data-ttu-id="ca5fe-147">Cartes</span><span class="sxs-lookup"><span data-stu-id="ca5fe-147">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="ca5fe-148">Déploiement de liens d’onglets et vue d’étape</span><span class="sxs-lookup"><span data-stu-id="ca5fe-148">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
