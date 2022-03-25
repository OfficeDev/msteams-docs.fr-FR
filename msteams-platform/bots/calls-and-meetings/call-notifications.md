---
title: Notifications d’appel entrant
description: En savoir plus sur les informations techniques détaillées sur la gestion des notifications des appels entrants, la redirection et l’authentification des appels à l’aide d’exemples de code
ms.topic: conceptual
ms.localizationpriority: medium
keywords: appel de l’affinité de région de rappel des notifications d’appel
ms.date: 04/02/2019
ms.openlocfilehash: d7939bd7fa613636d225e6f5437434c394a8c0bd
ms.sourcegitcommit: 6906ba7e2a6e957889530b0a117a852c43bc86a6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2022
ms.locfileid: "63783994"
---
# <a name="incoming-call-notifications"></a>Notifications d’appel entrant

Lors [de l’inscription d’un bot d’appels et de](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities) Microsoft Teams, le webhook pour l’URL d’appel est mentionné. Cette URL est le point de terminaison de webhook pour tous les appels entrants à votre bot.

## <a name="protocol-determination"></a>Détermination du protocole

La notification entrante est fournie dans un format hérité pour assurer la compatibilité avec le [protocole Skype précédent](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true). Pour convertir l’appel au protocole Microsoft Graph, votre bot doit déterminer si la notification est dans un format hérité et fournir la réponse suivante :

```http
HTTP/1.1 204 No Content
```

Votre bot reçoit de nouveau la notification, mais cette fois dans le protocole Microsoft Graph.

Dans une prochaine version de la plateforme Real-time Media, vous pouvez configurer le protocole que votre application prend en charge pour éviter de recevoir le rappel initial dans le format hérité.

La section suivante fournit des détails sur les notifications d’appels entrants redirigées pour l’affinité de région vers votre déploiement.

## <a name="redirects-for-region-affinity"></a>Redirections pour l’affinité de région

Vous appelez votre webhook à partir du centre de données hébergeant l’appel. L’appel démarre dans un centre de données et ne prend pas en compte les affinités de région. La notification est envoyée à votre déploiement en fonction de la résolution GeoDNS. Si votre application détermine, en inspectant la charge utile de notification initiale ou autrement, qu’elle doit s’exécuter dans un autre déploiement, l’application fournit la réponse suivante :

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Activez votre bot pour répondre à un appel entrant à l’aide de [l’API de](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true) réponse. Vous pouvez spécifier la situation `callbackUri` à utiliser pour gérer cet appel particulier. Cela est utile pour les instances avec état dans laquelle votre appel est géré par une partition particulière, `callbackUri` et vous souhaitez incorporer ces informations dans le routage vers l’instance de droite.

La section suivante fournit des détails sur l’authentification du rappel en inspectant le jeton publié sur votre webhook.

## <a name="authenticate-the-callback"></a>Authentifier le rappel

Votre bot doit inspecter le jeton publié sur votre webhook pour valider la demande. Chaque fois que l’API publie sur le webhook, le message HTTP POST contient un jeton OAuth dans l’en-tête Authorization en tant que jeton de support, avec l’audience comme ID d’application de votre application.

Votre application doit valider ce jeton avant d’accepter la demande de rappel.

L’exemple de code suivant est utilisé pour authentifier le rappel :

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

Le jeton OAuth a les valeurs suivantes et est signé par Skype :

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

La configuration OpenID publiée sur <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> peut être utilisée pour vérifier le jeton. Chaque valeur de jeton OAuth est utilisée comme suit :

* `aud` où audience est l’URI d’ID d’application spécifié pour l’application.
* `tid` est l’ID de client pour Contoso.com.
* `iss` est l’émetteur du jeton, `https://api.botframework.com`.

Pour votre gestion du code, le webhook doit valider le jeton, vérifier qu’il n’a pas expiré et vérifier s’il a été signé par la configuration OpenID publiée. Vous devez également vérifier si aud correspond à votre ID d’application avant d’accepter la demande de rappel.

Pour plus d’informations, voir [valider les demandes entrantes](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conditions requises et considérations pour les robots multimédias hébergés par l’application](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)

## <a name="see-also"></a>Voir aussi

* [Configurer un standard automatique](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configurer la réponse automatique pour les Salles Microsoft Teams sur les appareils de téléphone Teams android et vidéo](/microsoftteams/set-up-auto-answer-on-teams-android)