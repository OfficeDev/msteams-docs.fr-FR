---
title: Déploiement de lien
author: surbhigupta
description: Dans ce module, découvrez comment ajouter un déploiement de lien avec l’extension de messagerie dans une application Teams avec un manifeste d’application ou manuellement à l’aide d’exemples de code et d’exemples.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: debbcdcf4c22f63262e16fda70c0e778bffa9379
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190001"
---
# <a name="link-unfurling"></a>Déploiement de lien

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Ce document vous guide sur la façon d’ajouter un déploiement de lien à votre manifeste d’application à l’aide d’App Studio ou manuellement. Avec le déploiement de liens, votre application peut s’inscrire pour recevoir une activité de `invoke` lorsque les URL d’un domaine particulier sont collées dans la zone de composition des messages. Contient `invoke` l’URL complète collée dans la zone de message de composition. Vous pouvez répondre avec une carte que l’utilisateur peut déployer pour obtenir des informations ou des actions supplémentaires. Cela fonctionne comme une commande de recherche avec l’URL comme terme de recherche.

> [!NOTE]
>
> * Actuellement, le déploiement de liens n’est pas pris en charge sur les clients mobiles.
> * Le résultat du déploiement du lien est mis en cache pendant 30 minutes.

L’extension de message Azure DevOps utilise le déploiement de liens pour rechercher les URL collées dans la zone de message de composition pointant vers un élément de travail. Dans l’image suivante, un utilisateur a collé une URL pour un élément dans Azure DevOps que l’extension de message a résolue dans une carte :

:::image type="content" source="~/assets/images/compose-extensions/messagingextensions_linkunfurling.png" alt-text="Exemple de déploiement de lien":::

Consultez la vidéo suivante pour en savoir plus sur le déploiement de liens :
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OFZG]
<br>

## <a name="add-link-unfurling-to-your-app-manifest"></a>Ajouter un déploiement de lien au manifeste de votre application

Pour ajouter un déploiement de lien à votre manifeste d’application, ajoutez un nouveau tableau `messageHandlers` à la section `composeExtensions` de votre manifeste d’application JSON. Vous pouvez ajouter le tableau à l’aide d’App Studio ou manuellement. Les listes de domaines peuvent inclure des caractères génériques, par exemple `*.example.com`. Cela correspond exactement à un segment du domaine, si vous devez faire correspondre `a.b.example.com`, puis utilisez `*.*.example.com`.

> [!NOTE]
> N’ajoutez pas de domaines qui ne sont pas dans votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide. Les domaines de niveau supérieur sont interdits, par exemple, `*.com``*.org`.

### <a name="add-link-unfurling-using-app-studio"></a>Ajouter un déploiement de lien à l’aide d’App Studio

1. Ouvrez **App Studio** à partir du client Microsoft Teams, puis sélectionnez l’onglet **Éditeur de manifeste**.
1. Chargez le manifeste de votre application.
1. Dans la page **Extension de message**, ajoutez le domaine que vous souhaitez rechercher dans la section **Gestionnaires de messages**. L'image suivante explique le processus :

    :::image type="content" source="~/assets/images/link-unfurling.png" alt-text="Section gestionnaires de messages dans App Studio":::

### <a name="add-link-unfurling-manually"></a>Ajouter le déploiement manuel du lien

> [!NOTE]
> Si l’authentification est ajoutée via Azure AD, [unfurl links in Teams using bot](/microsoftteams/platform/sbs-botbuilder-linkunfurling?tabs=vs&tutorial-step=4).

Pour permettre à votre extension de message d’interagir avec des liens, vous devez d’abord ajouter le tableau `messageHandlers` au manifeste de votre application. L’exemple suivant explique comment ajouter manuellement un déploiement de lien :

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

Pour obtenir un exemple complet de manifeste, consultez [référence de manifeste](~/resources/schema/manifest-schema.md).

## <a name="handle-the-composeextensionquerylink-invoke"></a>Gérer l’appel `composeExtension/queryLink`

Après avoir ajouté le domaine au manifeste de l’application, vous devez mettre à jour votre code de service web pour gérer la demande d’appel. Utilisez l’URL reçue pour rechercher votre service et créer une réponse de carte. Si vous répondez avec plusieurs cartes, seule la première réponse de carte est utilisée.

Les types de champs suivants sont pris en charge :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte de bannière](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte Connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Pour plus d’informations, consultez [Invocation du type d’action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).

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

Voici un exemple de `invoke` envoyé à votre bot :

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

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../sbs-botbuilder-linkunfurling.yml) pour déployer des liens dans Teams à l’aide d’un bot.

## <a name="see-also"></a>Voir aussi

* [Cartes](~/task-modules-and-cards/what-are-cards.md)
* [Onglets lient le déploiement et l’affichage intermédiaire](~/tabs/tabs-link-unfurling.md)
