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
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a>Prise en charge unique de la signalisation (SSO) pour les extensions de messagerie
 
Une seule prise en charge de la connecte est maintenant disponible pour les extensions de messagerie et le déploiement de liens. L’activation d’une connexion unique (SSO) pour les extensions de messagerie actualise silencieusement le jeton d’authentification, ce qui minimise le nombre de fois que vous devez saisir votre connexion dans les informations d’identification pour Microsoft Teams.

Ce document vous guide sur la façon d’activer l’OSS et de stocker votre jeton d’authentification, si nécessaire.

## <a name="prerequisites"></a>Configuration requise

La condition préalable pour permettre sso pour les extensions de messagerie et le déploiement de lien sont les suivants:
* Vous devez avoir un [compte Azure.](https://azure.microsoft.com/en-us/free/)
* Vous devez configurer votre application via le portail AAD et mettre à jour votre manifeste d’application Teams pour votre bot tel que défini dans [l’enregistrement](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)de votre application via le portail AAD .

> [!NOTE]
> Pour plus d’informations sur la création d’un compte Azure et la mise à jour de votre manifeste d’application, consultez la prise en charge de la connecte [unique (SSO) pour les bots.](../../bots/how-to/authentication/auth-aad-sso-bots.md)

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>Activer SSO pour les extensions de messagerie et le déploiement de liens

Une fois les conditions préalables terminées, vous pouvez activer SSO pour les extensions de messagerie et le déploiement de liens.

**Pour activer SSO**
1. Mettez à jour les détails [de votre connexion Bots OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) sur le portail Azure.
2. Téléchargez [l’exemple d’extensions de](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) messagerie et suivez les instructions de configuration fournies par l’assistant.
   > [!NOTE]
   > Utilisez votre connexion OAuth bots lors de la configuration de vos extensions de messagerie.
3. Dans le [fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs,](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) mettez à jour la valeur *de l’auth* *à silentAuth* dans `OnTeamsMessagingExtensionQueryAsync` le et / ou `OnTeamsAppBasedLinkQueryAsync` .  

    > [!NOTE]
    > Nous ne prenons pas en charge d’autres gestionnaires SSO, sauf `OnTeamsMessagingExtensionQueryAsync` et à partir du fichier `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs.
   
4. Vous recevez le jeton dans `OnTeamsMessagingExtensionQueryAsync` le gestionnaire dans la charge utile ou dans le , selon le scénario que vous `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` activez le SSO pour:

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Si vous utilisez la connexion OAuth, ajoutez le code suivant au fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs pour mettre à jour ou ajouter le jeton dans le magasin :
    
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

## <a name="see-also"></a>Voir aussi

* [Ajoutez l’authentification à vos extensions de messagerie](add-authentication.md)
* [Utilisez SSO pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Déploiement de lien](link-unfurling.md)

