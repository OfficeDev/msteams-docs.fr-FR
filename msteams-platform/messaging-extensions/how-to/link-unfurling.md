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
# <a name="link-unfurling"></a>Déploiement de lien

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> Actuellement, le déploiement de liens n’est pas pris en charge sur les clients mobiles.

Avec de déploiement de lien, votre application peut s’inscrire pour recevoir une activité `invoke` lorsque les URL avec un domaine particulier sont collées dans la zone rédaction d’un message. Celui-ci contient l’URL complète qui a été passée dans la zone de rédaction du message, et vous pouvez répondre avec une carte que l’utilisateur peut déployer, fournissant des informations ou `invoke` des actions supplémentaires.  Cela fonctionne de manière très similaire à une [commande de](~/messaging-extensions/how-to/search-commands/define-search-command.md)recherche, avec l’URL servant de terme de recherche.

L’extension de messagerie Azure DevOps utilise le déploiement de lien pour rechercher les URL qui sont passées dans la zone de composition du message pointant vers un élément de travail. Dans la capture d’écran ci-dessous, un utilisateur a passé une URL pour un élément de travail dans Azure DevOps que l’extension de messagerie a résolue en une carte.

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Ajouter le déploiement de lien au manifeste de votre application

 Pour ajouter le déploiement de lien au manifeste de votre application, ajoutez un nouveau tableau à la `messageHandlers` `composeExtensions` section du manifeste JSON de votre application. Vous pouvez ajouter le tableau à l’aide d’App Studio ou manuellement. Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple. Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .

> [!NOTE]
> N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques. Par exemple, yourapp.onmicrosoft.com est valide, mais *.onmicrosoft.com n’est pas valide. En outre, les domaines de niveau supérieur sont interdits. Par exemple, *.com, *.org.

### <a name="using-app-studio"></a>Utilisation de App Studio

1. Dans App Studio, sous l’onglet Éditeur de manifeste, chargez le manifeste de votre application.
1. Dans la page **Extension de** messagerie, ajoutez le domaine que vous souhaitez rechercher dans la section Des **handlers** de messages, comme dans la capture d’écran ci-dessous.

![section des handlers de messages dans App Studio](~/assets/images/link-unfurling.png)

### <a name="manually"></a>Manuellement

Pour permettre à votre extension de messagerie d’interagir avec les liens de cette façon, vous devez d’abord ajouter le tableau au manifeste de votre application, comme dans `messageHandlers` l’exemple ci-dessous. Cet exemple n’est pas le manifeste complet, voir [la référence de](~/resources/schema/manifest-schema.md) manifeste pour obtenir un exemple de manifeste complet.

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>Gérer `composeExtension/queryLink` l’appel

Une fois que vous avez ajouté le domaine pour écouter le manifeste de l’application, vous devez mettre à jour votre code de service web pour gérer la demande d’appel. Utilisez l’URL que vous recevez pour effectuer une recherche dans votre service et créer une réponse de carte. Si vous répondez avec plusieurs cartes, seule la première sera utilisée.

Nous prise en charge les types de carte suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte Hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Voir [Quelles sont les cartes pour](~/task-modules-and-cards/what-are-cards.md) obtenir une vue d’ensemble .

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

Voici un exemple de `invoke` l’envoi à votre bot.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Un exemple de réponse est illustré ci-dessous.

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
