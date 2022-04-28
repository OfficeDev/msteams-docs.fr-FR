---
title: Prise en charge de l’authentification unique pour vos extensions de message
author: KirtiPereira
description: Découvrez comment activer la prise en charge de l’authentification unique pour vos extensions de message avec des exemples de code.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4ee49b349d287325bb029aa155a61219a8656e22
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104391"
---
# <a name="single-sign-on-support-for-message-extensions"></a>Prise en charge de l’authentification unique pour les extensions de message

La prise en charge de l’authentification unique (SSO) est désormais disponible pour les extensions de message et le déploiement de liens. L’activation de l’authentification unique pour les extensions de message par défaut actualise le jeton d’authentification, ce qui réduit le nombre de fois où vous devez entrer les informations d’identification de connexion pour Microsoft Teams.

Ce document vous guide sur la façon d’activer l’authentification unique et de stocker votre jeton d’authentification, si nécessaire.

## <a name="prerequisites"></a>Conditions préalables

La configuration requise pour activer l’authentification unique pour les extensions de message et le déploiement de liens est la suivante :

* Vous devez disposer d’un compte [Azure](https://azure.microsoft.com/free/) .
* Vous devez configurer votre application via le portail Azure AD et mettre à jour Teams manifeste d’application tel que défini dans [l’inscription de votre application via le portail Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Pour plus d’informations sur la création d’un compte Azure et la mise à jour du manifeste de votre application, consultez la prise en charge de l’authentification [unique (SSO) pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>Activer l’authentification unique pour les extensions de message et le déploiement de liens

Une fois les prérequis remplis, vous pouvez activer l’authentification unique pour les extensions de message et le déploiement de liens.

Pour activer l’authentification unique :

1. Mettez à jour les détails de la [connexion OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) de vos bots dans le portail Microsoft Azure.
2. Téléchargez [l’exemple d’extensions de message](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) et suivez les instructions d’installation fournies par l’Assistant.
   > [!NOTE]
   > Utilisez votre connexion OAuth bots lors de la configuration de vos extensions de message.
3. Dans le fichier [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) , mettez à jour la valeur de *l’authentification* à *silentAuth* dans le `OnTeamsMessagingExtensionQueryAsync` et / ou `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > Nous ne prenons pas en charge l’authentification unique d’autres gestionnaires, à l’exception `OnTeamsMessagingExtensionQueryAsync` du `OnTeamsAppBasedLinkQueryAsync` fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs.

4. Vous recevez le jeton dans `OnTeamsMessagingExtensionQueryAsync` le gestionnaire dans la `turnContext.Activity.Value` charge utile ou dans le , selon le `OnTeamsAppBasedLinkQueryAsync`scénario dans lequel vous activez l’authentification unique pour :

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

* [Ajouter l’authentification à vos extensions de message](add-authentication.md)
* [Utiliser l’authentification unique pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Déploiement de lien](link-unfurling.md)
