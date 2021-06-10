---
title: Notifications d’appel entrant
description: Informations techniques détaillées sur la gestion des notifications des appels entrants
ms.topic: conceptual
localization_priority: Normal
keywords: appel de l’affinité de région de rappel des notifications d’appel
ms.date: 04/02/2019
ms.openlocfilehash: 06068c13d27598b9a7b5e70181c69f9efb2c0afb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020175"
---
# <a name="incoming-call-notifications"></a><span data-ttu-id="bdc60-104">Notifications d’appel entrant</span><span class="sxs-lookup"><span data-stu-id="bdc60-104">Incoming call notifications</span></span>

<span data-ttu-id="bdc60-105">Lors [de l’inscription d’un bot d’appels](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)et de réunions pour Microsoft Teams, le webhook pour l’URL d’appel est mentionné.</span><span class="sxs-lookup"><span data-stu-id="bdc60-105">In [registering a calls and meetings bot for Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), the Webhook for calling URL is mentioned.</span></span> <span data-ttu-id="bdc60-106">Cette URL est le point de terminaison de webhook pour tous les appels entrants à votre bot.</span><span class="sxs-lookup"><span data-stu-id="bdc60-106">This URL is the webhook endpoint for all incoming calls to your bot.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="bdc60-107">Détermination du protocole</span><span class="sxs-lookup"><span data-stu-id="bdc60-107">Protocol determination</span></span>

<span data-ttu-id="bdc60-108">La notification entrante est fournie dans un format hérité pour assurer la compatibilité avec le [protocole Skype précédent.](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="bdc60-108">The incoming notification is provided in a legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="bdc60-109">Pour convertir l’appel au protocole Microsoft Graph, votre bot doit déterminer si la notification est dans un format hérité et fournir la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="bdc60-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in a legacy format and provide the following response:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="bdc60-110">Votre bot reçoit de nouveau la notification, mais cette fois dans le protocole Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="bdc60-110">Your bot receives the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="bdc60-111">Dans une prochaine version de la plateforme Real-time Media, vous pouvez configurer le protocole que votre application prend en charge pour éviter de recevoir le rappel initial dans le format hérité.</span><span class="sxs-lookup"><span data-stu-id="bdc60-111">In a future release of the Real-time Media Platform, you can configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

<span data-ttu-id="bdc60-112">La section suivante fournit des détails sur les notifications d’appels entrants redirigées pour l’affinité de région vers votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="bdc60-112">The next section provides details on incoming call notifications redirected for region affinity to your deployment.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="bdc60-113">Redirections pour l’affinité de région</span><span class="sxs-lookup"><span data-stu-id="bdc60-113">Redirects for region affinity</span></span>

<span data-ttu-id="bdc60-114">Vous appelez votre webhook à partir du centre de données hébergeant l’appel.</span><span class="sxs-lookup"><span data-stu-id="bdc60-114">You call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="bdc60-115">L’appel démarre dans un centre de données et ne prend pas en compte les affinités de région.</span><span class="sxs-lookup"><span data-stu-id="bdc60-115">The call starts in any data center and does not take into account region affinities.</span></span> <span data-ttu-id="bdc60-116">La notification est envoyée à votre déploiement en fonction de la résolution GeoDNS.</span><span class="sxs-lookup"><span data-stu-id="bdc60-116">The notification is sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="bdc60-117">Si votre application détermine, en inspectant la charge utile de notification initiale ou autrement, qu’elle doit s’exécuter dans un autre déploiement, l’application fournit la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="bdc60-117">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application provides the following response:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="bdc60-118">Activez votre bot pour répondre à un appel entrant à l’aide de [l’API de](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) réponse.</span><span class="sxs-lookup"><span data-stu-id="bdc60-118">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="bdc60-119">Vous pouvez spécifier `callbackUri` la situation à utiliser pour gérer cet appel particulier.</span><span class="sxs-lookup"><span data-stu-id="bdc60-119">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="bdc60-120">Cela est utile pour les instances avec état dans laquelle votre appel est géré par une partition particulière, et vous souhaitez incorporer ces informations dans le routage vers `callbackUri` l’instance de droite.</span><span class="sxs-lookup"><span data-stu-id="bdc60-120">This is useful for stateful instances where your call is handled by a particular partition, and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

<span data-ttu-id="bdc60-121">La section suivante fournit des détails sur l’authentification du rappel en inspectant le jeton publié sur votre webhook.</span><span class="sxs-lookup"><span data-stu-id="bdc60-121">The next section provides details on authenticating the callback by inspecting the token posted to your webhook.</span></span>

## <a name="authenticate-the-callback"></a><span data-ttu-id="bdc60-122">Authentifier le rappel</span><span class="sxs-lookup"><span data-stu-id="bdc60-122">Authenticate the callback</span></span>

<span data-ttu-id="bdc60-123">Votre bot doit inspecter le jeton publié sur votre webhook pour valider la demande.</span><span class="sxs-lookup"><span data-stu-id="bdc60-123">Your bot must inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="bdc60-124">Chaque fois que l’API publie sur le webhook, le message HTTP POST contient un jeton OAuth dans l’en-tête Authorization en tant que jeton de support, avec l’audience comme ID d’application de votre application.</span><span class="sxs-lookup"><span data-stu-id="bdc60-124">Every time the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a bearer token, with the audience as your application's App ID.</span></span>

<span data-ttu-id="bdc60-125">Votre application doit valider ce jeton avant d’accepter la demande de rappel.</span><span class="sxs-lookup"><span data-stu-id="bdc60-125">Your application must validate this token before accepting the callback request.</span></span>

<span data-ttu-id="bdc60-126">L’exemple de code suivant est utilisé pour authentifier le rappel :</span><span class="sxs-lookup"><span data-stu-id="bdc60-126">The following sample code is used to authenticate the callback:</span></span>

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

<span data-ttu-id="bdc60-127">Le jeton OAuth a les valeurs suivantes et est signé par Skype :</span><span class="sxs-lookup"><span data-stu-id="bdc60-127">The OAuth token has the following values, and is signed by Skype:</span></span>

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

<span data-ttu-id="bdc60-128">La configuration OpenID publiée sur <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> peut être utilisée pour vérifier le jeton.</span><span class="sxs-lookup"><span data-stu-id="bdc60-128">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span> <span data-ttu-id="bdc60-129">Chaque valeur de jeton OAuth est utilisée comme suit :</span><span class="sxs-lookup"><span data-stu-id="bdc60-129">Each OAuth token value is used as follows:</span></span>

* <span data-ttu-id="bdc60-130">`aud` où audience est l’URI d’ID d’application spécifié pour l’application.</span><span class="sxs-lookup"><span data-stu-id="bdc60-130">`aud` where audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="bdc60-131">`tid` est l’ID de client pour Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bdc60-131">`tid` is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="bdc60-132">`iss` est l’émetteur du jeton, `https://api.botframework.com` .</span><span class="sxs-lookup"><span data-stu-id="bdc60-132">`iss` is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="bdc60-133">Pour votre gestion du code, le webhook doit valider le jeton, vérifier qu’il n’a pas expiré et vérifier s’il a été signé par la configuration OpenID publiée.</span><span class="sxs-lookup"><span data-stu-id="bdc60-133">For your code handling, the webhook must validate the token, ensure it has not expired, and check whether it has been signed by the published OpenID configuration.</span></span> <span data-ttu-id="bdc60-134">Vous devez également vérifier si aud correspond à votre ID d’application avant d’accepter la demande de rappel.</span><span class="sxs-lookup"><span data-stu-id="bdc60-134">You must also check whether aud matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="bdc60-135">Pour plus d’informations, voir [valider les demandes entrantes.](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)</span><span class="sxs-lookup"><span data-stu-id="bdc60-135">For more information, see [validate inbound requests](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).</span></span>

## <a name="next-step"></a><span data-ttu-id="bdc60-136">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="bdc60-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bdc60-137">Conditions requises et considérations pour les robots multimédias hébergés par l’application</span><span class="sxs-lookup"><span data-stu-id="bdc60-137">Requirements and considerations for application-hosted media bots</span></span>](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
