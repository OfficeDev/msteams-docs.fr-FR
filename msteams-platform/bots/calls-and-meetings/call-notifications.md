---
title: Notifications d’appel entrant
description: Dans ce module, découvrez des informations techniques détaillées sur la gestion des notifications à partir d’appels entrants, la redirection et l’authentification des appels à l’aide d’exemples de code
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 04/02/2019
ms.openlocfilehash: fd68b85a3c6f5f4682a728461d792093bcd8cac0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143829"
---
# <a name="incoming-call-notifications"></a>Notifications d’appel entrant

Dans [l’inscription d’un bot d’appels et de réunions pour Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), le Webhook pour l’URL d’appel est mentionné. Cette URL est le point de terminaison de webhook pour tous les appels entrants à votre bot.

## <a name="protocol-determination"></a>Détermination du protocole

La notification entrante est fournie dans un format hérité pour la compatibilité avec le [protocole Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true) précédent. Pour convertir l’appel au protocole Microsoft Graph, votre bot doit déterminer si la notification est dans un format hérité et fournit la réponse suivante :

```http
HTTP/1.1 204 No Content
```

Votre bot reçoit à nouveau la notification, mais cette fois dans le protocole Microsoft Graph.

Dans une version ultérieure de la plateforme multimédia en temps réel, vous pouvez configurer le protocole pris en charge par votre application pour éviter de recevoir le rappel initial dans le format hérité.

La section suivante fournit des détails sur les notifications d’appel entrantes redirigées pour l’affinité de région vers votre déploiement.

## <a name="redirects-for-region-affinity"></a>Redirections pour l’affinité de région

Vous appelez votre webhook à partir du centre de données qui héberge l’appel. L’appel démarre dans n’importe quel centre de données et ne prend pas en compte les affinités de région. La notification est envoyée à votre déploiement en fonction de la résolution GeoDNS. Si votre application détermine, en inspectant la charge utile de notification initiale ou autre, qu’elle doit s’exécuter dans un déploiement différent, l’application fournit la réponse suivante :

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Permettre à votre bot de répondre à un appel entrant à l’aide de l’API [answer](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true). Vous pouvez spécifier le `callbackUri` pour gérer cet appel particulier. Cela est utile pour les instances avec état où votre appel est géré par une partition particulière, et vous souhaitez incorporer ces informations dans le `callbackUri` pour le routage vers l’instance appropriée.

La section suivante fournit des détails sur l’authentification du rappel en inspectant le jeton publié sur votre webhook.

## <a name="authenticate-the-callback"></a>Authentifier le rappel

Votre bot doit inspecter le jeton publié sur votre webhook pour valider la demande. Chaque fois que l’API publie sur le webhook, le message HTTP POST contient un jeton OAuth dans l’en-tête Authorization en tant que jeton porteur, avec l’audience comme ID d’application de votre application.

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

* `aud` où l’audience correspond à l’URI de l’ID d’application spécifié pour l’application.
* `tid` est l’ID de locataire pour Contoso.com.
* `iss` est l’émetteur du jeton, `https://api.botframework.com`.

Pour votre gestion du code, le webhook doit valider le jeton, s’assurer qu’il n’a pas expiré et vérifier s’il a été signé par la configuration OpenID publiée. Vous devez également vérifier si l’authentification correspond à votre ID d’application avant d’accepter la demande de rappel.

Pour plus d’informations, consultez [valider les demandes entrantes](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [exigences et considérations relatives aux bots multimédias hébergés par des applications](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)

## <a name="see-also"></a>Voir aussi

* [Configurer un standard automatique](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configurer la réponse automatique pour les salles Microsoft Teams sur les appareils mobiles vidéo Android et Teams](/microsoftteams/set-up-auto-answer-on-teams-android)