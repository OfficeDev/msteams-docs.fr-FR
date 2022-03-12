---
title: Déploiement de lien
author: surbhigupta
description: Découvrez comment ajouter un déploiement de lien avec une extension de messagerie dans une application Microsoft Teams avec le manifeste de l’application ou manuellement à l’aide d’exemples et d’exemples de code.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1ecab904f21d84cfa329e1c390d51ebade6a8e05
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453865"
---
# <a name="link-unfurling"></a>Déploiement de lien

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Ce document vous guide sur la façon d’ajouter le déploiement de lien au manifeste de votre application à l’aide d’App studio et manuellement. Avec le déploiement de lien, `invoke` votre application peut s’inscrire pour recevoir une activité lorsque des URL avec un domaine particulier sont passées dans la zone de composition du message. Contient `invoke` l’URL complète qui a été passée dans la zone de rédaction du message et vous pouvez répondre avec une carte que l’utilisateur peut déployer, fournissant des informations ou des actions supplémentaires. Cela fonctionne comme une commande de recherche avec l’URL servant de terme de recherche.

> [!NOTE]
>
> * Actuellement, le déploiement de liaison n’est pas pris en charge sur les clients mobiles.
> * Le résultat du déploiement du lien est mis en cache pendant 30 minutes.

L Azure DevOps de messagerie utilise le déploiement de liaison pour rechercher les URL qui sont passées dans la zone de composition du message pointant vers un élément de travail. Dans l’image suivante, un utilisateur a passé une URL pour un élément de travail dans Azure DevOps, que l’extension de messagerie a résolue en une carte :

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>Ajouter le déploiement de lien au manifeste de votre application

Pour ajouter le déploiement de lien au manifeste de votre application, ajoutez un nouveau `messageHandlers` `composeExtensions` tableau à la section du manifeste JSON de votre application. Vous pouvez ajouter le tableau à l’aide d’App Studio ou manuellement. Les listes de domaines peuvent inclure des caractères génériques, par exemple `*.example.com`. Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une correspondance, `a.b.example.com` utilisez `*.*.example.com`.

> [!NOTE]
> N’ajoutez pas de domaines qui ne sont pas dans votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais non `*.onmicrosoft.com` valide. En outre, les domaines de niveau supérieur sont interdits. Par exemple, `*.com`. `*.org`

### <a name="add-link-unfurling-using-app-studio"></a>Ajouter un déploiement de lien à l’aide d’App Studio

1. **Ouvrez App Studio** à partir Microsoft Teams client, puis sélectionnez **l’onglet Éditeur de** manifeste.
1. Chargez le manifeste de votre application.
1. Dans la page **Extension de** messagerie, ajoutez le domaine que vous souhaitez rechercher dans la section Des **handlers de** messages. L’image suivante explique le processus :

    ![section des handlers de messages dans App Studio](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>Ajouter manuellement le déploiement de lien

Pour permettre à votre extension de messagerie d’interagir avec des liens, vous devez d’abord ajouter le tableau `messageHandlers` au manifeste de votre application. L’exemple suivant explique comment ajouter manuellement le déploiement de lien :

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

Pour obtenir un exemple de manifeste complet, voir [la référence du manifeste](~/resources/schema/manifest-schema.md).

## <a name="handle-the-composeextensionquerylink-invoke"></a>Gérer l’appel `composeExtension/queryLink`

Après avoir ajouté le domaine au manifeste de l’application, vous devez mettre à jour votre code de service web pour gérer la demande d’appel. Utilisez l’URL reçue pour effectuer une recherche dans votre service et créer une réponse de carte. Si vous répondez avec plusieurs cartes, seule la première réponse de carte est utilisée.

Les types de carte suivants sont pris en charge :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte de bannière](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte Connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Pour plus d’informations, voir [Action type invoke](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).

### <a name="example"></a>Exemple

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

Voici un exemple de l’envoi `invoke` à votre bot :

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Voici un exemple de réponse :

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

## <a name="see-also"></a>Voir aussi

* [Cartes](~/task-modules-and-cards/what-are-cards.md)
* [Déploiement de liens d’onglets et vue d’étape](~/tabs/tabs-link-unfurling.md)
