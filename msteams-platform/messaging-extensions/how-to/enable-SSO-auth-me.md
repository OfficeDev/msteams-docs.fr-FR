---
title: Prise en charge de l' sso pour vos extensions de messagerie
author: KirtiPereira
description: Comment activer la prise en charge de l' sso pour vos extensions de messagerie
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: f7dc689da3f0e3e06b8f9c68836b6449c2ae9120
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020701"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="ee68f-103">Prise en charge de l' sign-on unique (SSO) pour les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="ee68f-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="ee68f-104">La prise en charge de l' sign-on unique est désormais disponible pour les extensions de messagerie et le déploiement de liens.</span><span class="sxs-lookup"><span data-stu-id="ee68f-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="ee68f-105">L'activation de l'authentification unique (SSO) pour les extensions de messagerie actualisent silencieusement le jeton d'authentification, ce qui réduit le nombre de fois que vous devez entrer vos informations d'identification de connexion pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ee68f-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="ee68f-106">Ce document vous guide sur la façon d'activer l'authentification sso et de stocker votre jeton d'authentification, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ee68f-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee68f-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee68f-107">Prerequisites</span></span>

<span data-ttu-id="ee68f-108">La condition préalable à l'activer pour les extensions de messagerie et le déploiement des liens est la suivante :</span><span class="sxs-lookup"><span data-stu-id="ee68f-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="ee68f-109">Vous devez avoir un [compte Azure.](https://azure.microsoft.com/en-us/free/)</span><span class="sxs-lookup"><span data-stu-id="ee68f-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="ee68f-110">Vous devez configurer votre application via le portail AAD et mettre à jour le manifeste de votre application Teams pour votre bot, comme défini dans l'inscription de votre application via le [portail AAD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="ee68f-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="ee68f-111">Pour plus d'informations sur la création d'un compte Azure et la mise à jour du manifeste de votre application, consultez la prise en charge de l' [sign-on unique (SSO) pour les bots.](../../bots/how-to/authentication/auth-aad-sso-bots.md)</span><span class="sxs-lookup"><span data-stu-id="ee68f-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="ee68f-112">Activer l'ation SSO pour les extensions de messagerie et le déploiement de liens</span><span class="sxs-lookup"><span data-stu-id="ee68f-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="ee68f-113">Une fois les conditions préalables terminées, vous pouvez activer l'ingso pour les extensions de messagerie et le déploiement des liaisons.</span><span class="sxs-lookup"><span data-stu-id="ee68f-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="ee68f-114">**Pour activer l' utilisateur SSO**</span><span class="sxs-lookup"><span data-stu-id="ee68f-114">**To enable SSO**</span></span>
1. <span data-ttu-id="ee68f-115">Mettez à jour les détails [de connexion OAuth de](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) vos bots dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ee68f-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="ee68f-116">Téléchargez [l'exemple d'extensions de messagerie](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) et suivez les instructions d'installation fournies par l'Assistant.</span><span class="sxs-lookup"><span data-stu-id="ee68f-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="ee68f-117">Utilisez la connexion OAuth de vos bots lors de la configuration de vos extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ee68f-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="ee68f-118">Dans le fichier [TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) mettez à jour la valeur de *l'th* à *silentAuth* dans et / ou `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="ee68f-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="ee68f-119">Nous ne prise en charge pas d'autres ssO de handlers, à l'exception du fichier `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.</span><span class="sxs-lookup"><span data-stu-id="ee68f-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="ee68f-120">Vous recevez le jeton dans le handler dans la charge utile ou dans le , en fonction du scénario pour lequel vous activez l' `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` cesso pour `OnTeamsAppBasedLinkQueryAsync` :</span><span class="sxs-lookup"><span data-stu-id="ee68f-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="ee68f-121">Si vous utilisez la connexion OAuth, ajoutez le code suivant au fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs pour mettre à jour ou ajouter le jeton dans le magasin :</span><span class="sxs-lookup"><span data-stu-id="ee68f-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
   ```C#
   protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
            if (valueObject["authentication"] != null)
            {
                JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
                if (authenticationObject["token"] != null)
                {
                    //If the token is NOT exchangeable, then return 412 to require user consent
                    if (await TokenIsExchangeable(turnContext, cancellationToken))
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                    }
                    else
                    {
                        var response = new InvokeResponse();
                        response.Status = 412;
                        return response;
                    }
                }
            }
            return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
        }
        private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
        {
            TokenResponse tokenExchangeResponse = null;
            try
            {
                JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
                var tokenExchangeRequest =
                ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
                tokenExchangeResponse = await (turnContext.Adapter as IExtendedUserTokenProvider).ExchangeTokenAsync(
                 turnContext,
                 _connectionName,
                 turnContext.Activity.From.Id,
                 new TokenExchangeRequest
                 {
                     Token = tokenExchangeRequest.Token,
                 },
                 cancellationToken).ConfigureAwait(false);
            }
    #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
            catch
    #pragma warning restore CA1031 //Do not catch general exception types
            {
                //ignore exceptions
                //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
                //This ensures the caller knows that the invoke has failed.
            }
            if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
            {
                return false;
            }
            return true;
        }
    
    ```    

## <a name="see-also"></a><span data-ttu-id="ee68f-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ee68f-122">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee68f-123">Ajouter l'authentification à vos extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="ee68f-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee68f-124">Utiliser l' sso pour les bots</span><span class="sxs-lookup"><span data-stu-id="ee68f-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee68f-125">Déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="ee68f-125">Link unfurling</span></span>](link-unfurling.md)

