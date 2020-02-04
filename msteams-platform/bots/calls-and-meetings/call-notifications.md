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
# <a name="incoming-call-notifications-technical-details"></a><span data-ttu-id="ce4af-104">Notifications d’appel entrant : détails techniques</span><span class="sxs-lookup"><span data-stu-id="ce4af-104">Incoming call notifications: technical details</span></span>

<span data-ttu-id="ce4af-105">Lors de l' [inscription d’un robot d’appel et de réunion pour Microsoft teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), nous avons mentionné l’URL **de webhook (pour l’appel)** , le point de terminaison webhook pour tous les appels entrants vers votre bot.</span><span class="sxs-lookup"><span data-stu-id="ce4af-105">In [Registering a calling and meeting bot for Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), we mentioned the **Webhook (for calling)** URL — the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="ce4af-106">Cette rubrique décrit les détails techniques dont vous aurez besoin pour répondre à ces notifications.</span><span class="sxs-lookup"><span data-stu-id="ce4af-106">This topic discusses the technical details you'll need to respond to these notifications.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="ce4af-107">Détermination du protocole</span><span class="sxs-lookup"><span data-stu-id="ce4af-107">Protocol determination</span></span>

<span data-ttu-id="ce4af-108">La notification entrante est fournie au format hérité pour la compatibilité avec le [protocole Skype](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)précédent.</span><span class="sxs-lookup"><span data-stu-id="ce4af-108">The incoming notification is provided in legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="ce4af-109">Pour convertir l’appel au protocole Microsoft Graph, votre robot doit déterminer si la notification est au format hérité et répondre avec :</span><span class="sxs-lookup"><span data-stu-id="ce4af-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in legacy format and reply with:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="ce4af-110">Votre bot recevra de nouveau la notification, mais cette fois dans le protocole Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ce4af-110">Your bot will receive the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="ce4af-111">Dans une prochaine version de la plateforme multimédia en temps réel, nous allons vous permettre de configurer le protocole pris en charge par votre application pour éviter de recevoir le rappel initial dans le format hérité.</span><span class="sxs-lookup"><span data-stu-id="ce4af-111">In a future release of the Real-time Media Platform, we'll allow you to configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="ce4af-112">Redirections pour l’affinité de région</span><span class="sxs-lookup"><span data-stu-id="ce4af-112">Redirects for region affinity</span></span>

<span data-ttu-id="ce4af-113">Vous appellerez votre webhook à partir du centre de données hébergeant l’appel.</span><span class="sxs-lookup"><span data-stu-id="ce4af-113">You'll call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="ce4af-114">L’appel peut commencer dans n’importe quel centre de données et ne prend pas en compte les affinités de région.</span><span class="sxs-lookup"><span data-stu-id="ce4af-114">The call may start in any data center and doesn't take into account region affinities.</span></span> <span data-ttu-id="ce4af-115">La notification sera envoyée à votre déploiement en fonction de la résolution GeoDNS.</span><span class="sxs-lookup"><span data-stu-id="ce4af-115">The notification will be sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="ce4af-116">Si votre application détermine, en inspectant la charge utile de la notification initiale ou sinon, qu’elle doit s’exécuter dans un autre déploiement, l’application peut répondre avec :</span><span class="sxs-lookup"><span data-stu-id="ce4af-116">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application may reply with:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="ce4af-117">Permettre à votre robot de répondre à un appel entrant à l’aide de l’API de [réponse](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) .</span><span class="sxs-lookup"><span data-stu-id="ce4af-117">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="ce4af-118">Vous pouvez spécifier le `callbackUri` pour gérer cet appel particulier.</span><span class="sxs-lookup"><span data-stu-id="ce4af-118">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="ce4af-119">Cela est utile pour les instances d' _État_ où votre appel est géré par une partition particulière et que vous souhaitez incorporer ces informations `callbackUri` dans le pour le routage vers l’instance de droite.</span><span class="sxs-lookup"><span data-stu-id="ce4af-119">This is useful for _stateful_ instances where your call is handled by a particular partition and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

## <a name="authenticating-the-callback"></a><span data-ttu-id="ce4af-120">Authentification du rappel</span><span class="sxs-lookup"><span data-stu-id="ce4af-120">Authenticating the callback</span></span>

<span data-ttu-id="ce4af-121">Votre bot doit inspecter le jeton publié vers votre webhook pour valider la demande.</span><span class="sxs-lookup"><span data-stu-id="ce4af-121">Your bot should inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="ce4af-122">Chaque fois que l’API publie sur le webhook, le message HTTP POST contient un jeton OAuth dans l’en-tête Authorization en tant que jeton porteur, avec l’audience comme ID d’application de votre application.</span><span class="sxs-lookup"><span data-stu-id="ce4af-122">Whenever the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a Bearer token, with audience as your application's App ID.</span></span>

<span data-ttu-id="ce4af-123">Votre application doit valider ce jeton avant d’accepter la demande de rappel.</span><span class="sxs-lookup"><span data-stu-id="ce4af-123">Your application should validate this token before accepting the callback request.</span></span>

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

<span data-ttu-id="ce4af-124">Le jeton OAuth aura des valeurs comme suit et sera signé par Skype.</span><span class="sxs-lookup"><span data-stu-id="ce4af-124">The OAuth token will have values like the following, and will be signed by Skype.</span></span> <span data-ttu-id="ce4af-125">La configuration OpenID publiée à <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> l’adresse peut être utilisée pour vérifier le jeton.</span><span class="sxs-lookup"><span data-stu-id="ce4af-125">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span>

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

* <span data-ttu-id="ce4af-126">**audience obligatoire** est l’URI d’ID d’application spécifié pour l’application.</span><span class="sxs-lookup"><span data-stu-id="ce4af-126">**aud** audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="ce4af-127">**TID** est l’ID de client pour contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ce4af-127">**tid** is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="ce4af-128">**ISS** est l’émetteur du jeton, `https://api.botframework.com`.</span><span class="sxs-lookup"><span data-stu-id="ce4af-128">**iss** is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="ce4af-129">Votre code gérant le webhook doit valider le jeton, vérifier qu’il n’a pas expiré et vérifier s’il a été signé par notre configuration OpenID publiée.</span><span class="sxs-lookup"><span data-stu-id="ce4af-129">Your code handling the webhook should validate the token, ensure it hasn't expired, and check whether it has been signed by our published OpenID configuration.</span></span> <span data-ttu-id="ce4af-130">Vous devez également vérifier si la valeur de **AUD** correspond à l’ID de votre application avant d’accepter la demande de rappel.</span><span class="sxs-lookup"><span data-stu-id="ce4af-130">You should also check whether **aud** matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="ce4af-131">[Exemple](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) montre comment valider des demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="ce4af-131">[Sample](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) shows how to validate inbound requests.</span></span>
