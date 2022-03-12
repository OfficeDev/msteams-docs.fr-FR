---
title: Prise en charge de l’luiso pour vos extensions de messagerie
author: KirtiPereira
description: Découvrez comment activer la prise en charge de l’ation sso pour vos extensions de messagerie à l’aide d’exemples de code.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 3543d86d15755642a1617e07514db95a6a812313
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453466"
---
# <a name="single-sign-on-support-for-messaging-extensions"></a>Prise en charge de l’sign-on unique pour les extensions de messagerie

La prise en charge de l’sign-on unique (SSO) est désormais disponible pour les extensions de messagerie et le déploiement de liens. L’activation de l’authentification unique pour les extensions de messagerie par défaut actualise le jeton d’authentification, ce qui réduit le nombre de fois que vous devez entrer les informations d’identification de connexion pour Microsoft Teams.

Ce document vous guide sur la façon d’activer l’authentification sso et de stocker votre jeton d’authentification, si nécessaire.

## <a name="prerequisites"></a>Configuration requise

La condition préalable à l’activer pour les extensions de messagerie et le déploiement des liens est la suivante :

* Vous devez avoir un [compte Azure](https://azure.microsoft.com/free/) .
* Vous devez configurer votre application via le portail Azure AD et mettre à jour le manifeste de votre application Teams tel que défini dans enregistrer votre application via le portail [Azure AD.](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal)

> [!NOTE]
> Pour plus d’informations sur la création d’un compte Azure et la mise à jour du manifeste de votre application, consultez la prise en charge de [l’sign-on unique (SSO) pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>Activer l’ation SSO pour les extensions de messagerie et le déploiement de liens

Une fois les conditions préalables terminées, vous pouvez activer l’ingso pour les extensions de messagerie et le déploiement des liaisons.

Pour activer l’sso :

1. Mettez à jour les détails [de connexion OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) de vos bots dans le Microsoft Azure web.
2. Téléchargez [l’exemple d’extensions de messagerie](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) et suivez les instructions d’installation fournies par l’Assistant.
   > [!NOTE]
   > Utilisez la connexion OAuth de vos bots lors de la configuration de vos extensions de messagerie.
3. Dans le fichier [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) , mettez à jour la valeur de *l’th* à *silentAuth* `OnTeamsMessagingExtensionQueryAsync` dans et / ou `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > Nous ne tenons pas d’autres sso de handlers, `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` à l’exception du fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs.

4. Vous recevez le jeton dans `OnTeamsMessagingExtensionQueryAsync` le handler `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync`dans la charge utile ou dans le , en fonction du scénario pour lequel vous activez l’cesso :

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
                var userTokenClient = turnContext.TurnState.Get<UserTokenClient>();
                tokenExchangeResponse = await userTokenClient.ExchangeTokenAsync(
                                turnContext.Activity.From.Id,
                                 _connectionName,
                                 turnContext.Activity.ChannelId,
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

* [Ajouter l’authentification à vos extensions de messagerie](add-authentication.md)
* [Utiliser l’sso pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Déploiement de lien](link-unfurling.md)
