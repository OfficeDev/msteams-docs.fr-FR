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
# <a name="link-unfurling"></a>Déploiement de lien

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> Actuellement, Link unfurling n’est pas pris en charge sur les clients mobiles.

Avec de déploiement de lien, votre application peut s’inscrire pour recevoir une activité `invoke` lorsque les URL avec un domaine particulier sont collées dans la zone rédaction d’un message. L' `invoke` contient l’URL complète qui a été collée dans la zone de message de composition, et vous pouvez répondre avec une carte que l’utilisateur peut *Unfurl*, fournissant des informations ou des actions supplémentaires. Cela fonctionne de façon très similaire à une [commande de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md), avec l’URL servant de terme de recherche.

L’extension de messagerie Azure DevOps utilise le lien unfurling pour rechercher les URL collées dans la zone de message de composition pointant vers un élément de travail. Dans la capture d’écran ci-dessous, un utilisateur a collé une URL pour un élément de travail dans Azure DevOps laquelle l’extension de messagerie a été résolue en carte.

![Exemple de lien unfurling](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Ajouter un lien unfurling à votre manifeste d’application

Pour ce faire, vous allez ajouter un nouveau `messageHandlers` tableau à la `composeExtensions` section de votre manifeste d’application JSON. Vous pouvez le faire à l’aide de l’aide d’App Studio ou manuellement. Les listes de domaine peuvent inclure des caractères génériques, par exemple `*.example.com` . Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com` .

### <a name="using-app-studio"></a>Utilisation de App Studio

1. Dans App Studio, sous l’onglet Éditeur de manifeste, chargez votre manifeste d’application.
1. Sur la page **extension de messagerie** , ajoutez le domaine que vous souhaitez rechercher dans la section gestionnaires de **messages** , comme dans la capture d’écran ci-dessous.

![section gestionnaires de messages dans App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a>Manuellement

Pour activer votre extension de messagerie de cette façon, vous devez d’abord ajouter le `messageHandlers` tableau à votre manifeste d’application, comme dans l’exemple ci-dessous. Cet exemple n’est pas le manifeste complet, consultez la [référence de manifeste](~/resources/schema/manifest-schema.md) pour obtenir un exemple de manifeste complet.

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>Gérer l' `composeExtension/queryLink` appel

Une fois que vous avez ajouté le domaine pour écouter le manifeste de l’application, vous devez mettre à jour votre code de service Web pour gérer la demande d’appel. Utilisez l’URL que vous recevez pour effectuer une recherche dans votre service et créer une réponse de carte. Si vous répondez avec plusieurs cartes, seule la première est utilisée.

Nous prenons en charge les types de carte suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte héros](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte de connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Voir [qu’est-ce que les cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d’ensemble.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

Voici un exemple de l' `invoke` envoi à votre bot.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Vous trouverez ci-dessous un exemple de la réponse.

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
