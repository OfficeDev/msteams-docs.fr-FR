---
title: Détails techniques sur le traitement des notifications d’appel entrant
description: Informations techniques détaillées sur la gestion des notifications à partir des appels entrants
keywords: affinité des appels de la région de rappel des appels d’appel
ms.date: 04/02/2019
ms.openlocfilehash: be8860ff70cd7dff4fd9599079ea7aab4f454174
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673958"
---
# <a name="incoming-call-notifications-technical-details"></a>Notifications d’appel entrant : détails techniques

Lors de l' [inscription d’un robot d’appel et de réunion pour Microsoft teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), nous avons mentionné l’URL **de webhook (pour l’appel)** , le point de terminaison webhook pour tous les appels entrants vers votre bot. Cette rubrique décrit les détails techniques dont vous aurez besoin pour répondre à ces notifications.

## <a name="protocol-determination"></a>Détermination du protocole

La notification entrante est fournie au format hérité pour la compatibilité avec le [protocole Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)précédent. Pour convertir l’appel au protocole Microsoft Graph, votre robot doit déterminer si la notification est au format hérité et répondre avec :

```http
HTTP/1.1 204 No Content
```

Votre bot recevra de nouveau la notification, mais cette fois dans le protocole Microsoft Graph.

Dans une prochaine version de la plateforme multimédia en temps réel, nous allons vous permettre de configurer le protocole pris en charge par votre application pour éviter de recevoir le rappel initial dans le format hérité.

## <a name="redirects-for-region-affinity"></a>Redirections pour l’affinité de région

Vous appellerez votre webhook à partir du centre de données hébergeant l’appel. L’appel peut commencer dans n’importe quel centre de données et ne prend pas en compte les affinités de région. La notification sera envoyée à votre déploiement en fonction de la résolution GeoDNS. Si votre application détermine, en inspectant la charge utile de la notification initiale ou sinon, qu’elle doit s’exécuter dans un autre déploiement, l’application peut répondre avec :

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Permettre à votre robot de répondre à un appel entrant à l’aide de l’API de [réponse](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) . Vous pouvez spécifier le `callbackUri` pour gérer cet appel particulier. Cela est utile pour les instances d' _État_ où votre appel est géré par une partition particulière et que vous souhaitez incorporer ces informations `callbackUri` dans le pour le routage vers l’instance de droite.

## <a name="authenticating-the-callback"></a>Authentification du rappel

Votre bot doit inspecter le jeton publié vers votre webhook pour valider la demande. Chaque fois que l’API publie sur le webhook, le message HTTP POST contient un jeton OAuth dans l’en-tête Authorization en tant que jeton porteur, avec l’audience comme ID d’application de votre application.

Votre application doit valider ce jeton avant d’accepter la demande de rappel.

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

Le jeton OAuth aura des valeurs comme suit et sera signé par Skype. La configuration OpenID publiée à <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> l’adresse peut être utilisée pour vérifier le jeton.

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

* **audience obligatoire** est l’URI d’ID d’application spécifié pour l’application.
* **TID** est l’ID de client pour contoso.com.
* **ISS** est l’émetteur du jeton, `https://api.botframework.com`.

Votre code gérant le webhook doit valider le jeton, vérifier qu’il n’a pas expiré et vérifier s’il a été signé par notre configuration OpenID publiée. Vous devez également vérifier si la valeur de **AUD** correspond à l’ID de votre application avant d’accepter la demande de rappel.

[Exemple](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) montre comment valider des demandes entrantes.
