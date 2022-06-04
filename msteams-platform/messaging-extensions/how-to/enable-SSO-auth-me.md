---
title: Prise en charge de l’authentification unique pour vos extensions de messages
author: KirtiPereira
description: Découvrez comment activer la prise en charge de l’authentification unique pour vos extensions de messagerie avec des exemples de code.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 900723ca77d4178a6a2ded46617ed53d985d83e3
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887701"
---
# <a name="single-sign-on-support-for-message-extensions"></a>Prise en charge de l’authentification unique pour les extensions de messages

La prise en charge de l’authentification unique (SSO) est désormais disponible pour les extensions de message et le déploiement de liens. L’activation de l’authentification unique pour les extensions de message par défaut actualise le jeton d’authentification, ce qui réduit le nombre de fois où vous devez saisir les informations d’identification de connexion pour Microsoft Teams.

Ce document vous guide sur la façon d’activer l’authentification unique et de stocker votre jeton d’authentification, si nécessaire.

## <a name="prerequisites"></a>Configuration requise

La configuration requise pour activer l’authentification unique pour les extensions de messages et le déploiement de liens est la suivante :

* Vous devez disposer d’un compte [Azure](https://azure.microsoft.com/free/).
* Vous devez configurer votre application via le portail Azure AD et mettre à jour le manifeste de l’application Teams tel que défini dans [Inscrire votre application via le portail Azure AD](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal).

> [!NOTE]
> Pour plus d’informations sur la création d’un compte Azure et la mise à jour du manifeste de votre application, consultez la rubrique [Prise en charge de l’authentification unique (SSO) pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>Activer l’authentification unique pour les extensions de messages et le déploiement de liens

Une fois les prérequis remplis, vous pouvez activer l’authentification unique pour les extensions de messages et le déploiement de liens.

Activer l’authentification unique :

1. Mettez à jour les détails de la [connexion OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) de vos bots dans le portail Microsoft Azure.
2. Téléchargez l’[exemple d’extensions de messages](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config), puis suivez les instructions d’installation fournies par l’Assistant.
   > [!NOTE]
   > Utilisez la connexion OAuth de vos bots lors de la configuration de vos extensions de messages.
3. Dans le fichier [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs), mettez à jour la valeur de *auth* en *silentAuth* dans le `OnTeamsMessagingExtensionQueryAsync` et / ou `OnTeamsAppBasedLinkQueryAsync`.  

    > [!NOTE]
    > Nous ne prenons pas en charge l’authentification unique d’autres gestionnaires, à l’exception de `OnTeamsMessagingExtensionQueryAsync` et `OnTeamsAppBasedLinkQueryAsync` du fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs.

4. Vous recevez le jeton dans `OnTeamsMessagingExtensionQueryAsync` le gestionnaire dans la `turnContext.Activity.Value` charge utile ou dans le , selon le `OnTeamsAppBasedLinkQueryAsync`scénario dans lequel vous activez l’authentification unique pour :

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    Si vous utilisez la connexion OAuth, ajoutez le code suivant au fichier TeamsMessagingExtensionsSearchAuthConfigBot.cs pour mettre à jour ou ajouter le jeton dans le magasin :

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

## <a name="code-sample"></a>Exemple de code

Cette section fournit un exemple de Kit de développement logiciel (SDK) d’authentification de bot v3.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Authentification du bot | Cet exemple montre comment prendre en main l’authentification dans un bot pour Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Authentification unique Tab, Bot and Message Extension (ME) | Cet exemple montre l’authentification unique pour Tab, Bot et ME – recherche, action, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Non disponible |

## <a name="see-also"></a>Voir aussi

* [Ajouter l’authentification à vos extension de messages](add-authentication.md)
* [Utiliser l’authentification unique pour les bots](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [Déploiement de lien](link-unfurling.md)
