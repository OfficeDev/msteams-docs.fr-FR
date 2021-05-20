---
title: Prise en charge SSO de vos extensions de messagerie
author: KirtiPereira
description: Comment activer le support SSO pour vos extensions de messagerie
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 02d08506a07e955693531908f4f3cf16573a02c0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566200"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="78c4e-103">Prise en charge unique de la signalisation (SSO) pour les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="78c4e-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="78c4e-104">Une seule prise en charge de la connecte est maintenant disponible pour les extensions de messagerie et le déploiement de liens.</span><span class="sxs-lookup"><span data-stu-id="78c4e-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="78c4e-105">L’activation d’une connexion unique (SSO) pour les extensions de messagerie actualise silencieusement le jeton d’authentification, ce qui minimise le nombre de fois que vous devez saisir votre connexion dans les informations d’identification pour Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="78c4e-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="78c4e-106">Ce document vous guide sur la façon d’activer l’OSS et de stocker votre jeton d’authentification, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="78c4e-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78c4e-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="78c4e-107">Prerequisites</span></span>

<span data-ttu-id="78c4e-108">La condition préalable pour permettre sso pour les extensions de messagerie et le déploiement de lien sont les suivants:</span><span class="sxs-lookup"><span data-stu-id="78c4e-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="78c4e-109">Vous devez avoir un [compte Azure.](https://azure.microsoft.com/en-us/free/)</span><span class="sxs-lookup"><span data-stu-id="78c4e-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="78c4e-110">Vous devez configurer votre application via le portail AAD et mettre à jour votre manifeste d’application Teams pour votre bot tel que défini dans [l’enregistrement](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)de votre application via le portail AAD .</span><span class="sxs-lookup"><span data-stu-id="78c4e-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="78c4e-111">Pour plus d’informations sur la création d’un compte Azure et la mise à jour de votre manifeste d’application, consultez la prise en charge de la connecte [unique (SSO) pour les bots.](../../bots/how-to/authentication/auth-aad-sso-bots.md)</span><span class="sxs-lookup"><span data-stu-id="78c4e-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="78c4e-112">Activer SSO pour les extensions de messagerie et le déploiement de liens</span><span class="sxs-lookup"><span data-stu-id="78c4e-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="78c4e-113">Une fois les conditions préalables terminées, vous pouvez activer SSO pour les extensions de messagerie et le déploiement de liens.</span><span class="sxs-lookup"><span data-stu-id="78c4e-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="78c4e-114">**Pour activer SSO**</span><span class="sxs-lookup"><span data-stu-id="78c4e-114">**To enable SSO**</span></span>
1. <span data-ttu-id="78c4e-115">Mettez à jour les détails [de votre connexion Bots OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="78c4e-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="78c4e-116">Téléchargez [l’exemple d’extensions de](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) messagerie et suivez les instructions de configuration fournies par l’assistant.</span><span class="sxs-lookup"><span data-stu-id="78c4e-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="78c4e-117">Utilisez votre connexion OAuth bots lors de la configuration de vos extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="78c4e-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="78c4e-118">Dans le [fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) mettez à jour la valeur *de l’auth* *à silentAuth* dans `OnTeamsMessagingExtensionQueryAsync` le et / ou `OnTeamsAppBasedLinkQueryAsync` .</span><span class="sxs-lookup"><span data-stu-id="78c4e-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="78c4e-119">Nous ne prenons pas en charge d’autres gestionnaires SSO, sauf `OnTeamsMessagingExtensionQueryAsync` et à partir du fichier `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.</span><span class="sxs-lookup"><span data-stu-id="78c4e-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="78c4e-120">Vous recevez le jeton dans `OnTeamsMessagingExtensionQueryAsync` le gestionnaire dans la charge utile ou dans le , selon le scénario que vous `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` activez le SSO pour:</span><span class="sxs-lookup"><span data-stu-id="78c4e-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="78c4e-121">Si vous utilisez la connexion OAuth, ajoutez le code suivant au fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs pour mettre à jour ou ajouter le jeton dans le magasin :</span><span class="sxs-lookup"><span data-stu-id="78c4e-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
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

## <a name="see-also"></a><span data-ttu-id="78c4e-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="78c4e-122">See also</span></span>

* [<span data-ttu-id="78c4e-123">Ajoutez l’authentification à vos extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="78c4e-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)
* [<span data-ttu-id="78c4e-124">Utilisez SSO pour les bots</span><span class="sxs-lookup"><span data-stu-id="78c4e-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [<span data-ttu-id="78c4e-125">Déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="78c4e-125">Link unfurling</span></span>](link-unfurling.md)

