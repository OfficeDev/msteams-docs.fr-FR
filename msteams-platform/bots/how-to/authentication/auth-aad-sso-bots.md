---
title: Support de l'identification unique pour les robots
description: Décrit comment obtenir un jeton d’utilisateur. Actuellement, un développeur de bot peut utiliser une carte de signature ou le service de bot Azure avec la prise en charge de la carte OAuth.
keywords: token, user token, SSO support for bots
ms.topic: conceptual
ms.openlocfilehash: 8537cf41cdd7218b9bf7618fccf0e1704ac6b815
ms.sourcegitcommit: 92fa912a51f295bb8a2dc1593a46ce103752dcdd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/21/2021
ms.locfileid: "49917584"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Prise en charge de l' sign-on unique (SSO) pour les bots

L’authentification unique dans Azure Active Directory (AAD) réduit le nombre de fois que les utilisateurs doivent entrer leurs informations d’identification de connexion en actualisation silencieuse du jeton d’authentification. Si les utilisateurs acceptent d’utiliser votre application, ils n’ont pas besoin de donner à nouveau leur consentement sur un autre appareil et peuvent se connecter automatiquement. Le flux est similaire à celui de la prise en charge de l’oD [DSO](../../../tabs/how-to/authentication/auth-aad-sso.md)de l’onglet Microsoft Teams. Toutefois, la différence est dans le protocole pour la façon dont un [bot](#request-a-bot-token) demande des jetons et reçoit [des réponses.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 est une norme ouverte d’authentification et d’autorisation utilisée par AAD et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams.

## <a name="bot-sso-at-runtime"></a>SO du bot lors de l’runtime

![Bot SSO lors de l’runtime diagram](../../../assets/images/bots/bots-sso-diagram.png)

Pour obtenir l’authentification et les jetons d’application bot, complétez les étapes suivantes :

1. Le bot envoie un message avec un OAuthCard qui contient la `tokenExchangeResource` propriété. Il indique à Teams d’obtenir un jeton d’authentification pour l’application bot. L’utilisateur reçoit des messages à tous les points de terminaison de l’utilisateur actif.

    > [!NOTE]
    >* Un utilisateur peut avoir plusieurs points de terminaison actifs à la fois.
    >* Le jeton bot est reçu de chaque point de terminaison utilisateur actif.
    >* L’application doit être installée dans l’étendue personnelle pour la prise en charge de l' cesso.

2. Si l’utilisateur actuel utilise votre application bot pour la première fois, une invite de demande s’affiche demandant à l’utilisateur d’appliquer l’une des procédures suivantes :
    * Fournir le consentement, si nécessaire.
    * Gérer l’authentification par étapes, telle que l’authentification à deux facteurs.

3. Teams demande le jeton d’application bot au point de terminaison AAD pour l’utilisateur actuel.

4. AAD envoie le jeton d’application bot à l’application Teams.

5. Teams envoie le jeton au bot dans le cadre de l’objet de valeur renvoyé par l’activité d’appel avec le nom **sign-in/tokenExchange**.
  
6. Le jeton de l’application bot fournit les informations requises, telles que l’adresse e-mail de l’utilisateur.
  
## <a name="develop-an-sso-teams-bot"></a>Développer un bot sso teams
  
Pour développer un bot SSO Teams, complétez les étapes suivantes :

1. [Inscrivez votre application via le portail AAD.](#register-your-app-through-the-aad-portal)
2. [Mettez à jour le manifeste de votre application Teams pour votre bot.](#update-your-teams-application-manifest-for-your-bot)
3. [Ajoutez le code pour demander et recevoir un jeton de bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-aad-portal"></a>Inscrire votre application via le portail AAD

Les étapes d’inscription de votre application via le portail AAD sont similaires au flux d' utilisateur unique [de l’onglet.](../../../tabs/how-to/authentication/auth-aad-sso.md) Pour inscrire votre application, complétez les étapes suivantes :

1. Inscrivez une nouvelle application dans [le portail Azure Active Directory – Inscriptions des](https://go.microsoft.com/fwlink/?linkid=2083908) applications.
2. Sélectionnez **Nouvelle inscription.** La page **Inscrire une application** s’affiche.
3. Dans la page **Inscrire une application,** entrez les valeurs suivantes :
    1. Entrez un **nom** pour votre application.
    2. Choisissez les **types de comptes pris en** charge, sélectionnez le type de compte client unique ou multi-locataire.

        > [!NOTE]
        >
        > Les utilisateurs ne sont pas invités à donner leur consentement et se voir accorder des jetons d’accès immédiatement, si l’application AAD est inscrite dans le même client qu’ils font une demande d’authentification dans Teams. Toutefois, les utilisateurs doivent donner leur consentement aux autorisations, si l’application AAD est inscrite dans un autre client.

    3. Choisissez **Inscrire**.
4. Dans la page vue d’ensemble, copiez et enregistrez **l’ID de l’application (client).** Vous en aurez besoin ultérieurement lors de la mise à jour du manifeste de votre application Teams.
5. Sélectionnez **Exposer une API** sous **Gérer**. 

   > [!IMPORTANT]
    > * Si vous construisez un bot autonome, entrez l’URI d’ID d’application sous le nom `api://botid-{YourBotId}` . Ici, **YourBotId est** votre ID d’application AAD.
    > * Si vous construisez une application avec un bot et un onglet, entrez l’URI d’ID d’application sous le nom `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Sélectionnez les autorisations dont votre application a besoin pour le point de terminaison AAD et, éventuellement, pour Microsoft Graph.
6. [Accorder des autorisations](/azure/active-directory/develop/v2-permissions-and-consent) pour les applications de bureau, web et mobiles Teams.
7. Sélectionnez **Ajouter une étendue**.
8. Dans le panneau qui s’ouvre, ajoutez une application cliente en entrant `access_as_user` le nom de **l’étendue.**

    >[!NOTE]
    > L’étendue « access_as_user » utilisée pour ajouter une application cliente est pour « Administrateurs et utilisateurs ».
    >
    > Vous devez connaître les restrictions importantes suivantes :
    >
    > * Seules les autorisations de l’API Microsoft Graph au niveau de l’utilisateur, telles que la messagerie, le profil, offline_access et OpenId, sont pris en charge. Si vous avez besoin d’accéder à d’autres étendues Microsoft Graph, telles que ou , voir `User.Read` `Mail.Read` la solution de [contournement recommandée.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)
    > * Le nom de domaine de votre application doit être identique au nom de domaine que vous avez enregistré pour votre application AAD.
    > * Plusieurs domaines par application ne sont actuellement pas pris en charge.
    > * Les applications qui utilisent le domaine ne sont pas pris en charge `azurewebsites.net` car elles sont courantes et peuvent être un risque pour la sécurité.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Mettre à jour le portail Azure avec la connexion OAuth

Pour mettre à jour le portail Azure avec la connexion OAuth, effectuer les étapes suivantes :

1. Dans le portail Azure, accédez à **Enregistrement des canaux bots.**

2. Go to **API Permissions**. Sélectionnez **Ajouter une autorisation Autorisation**  >  déléguée Microsoft **Graph,** puis ajoutez les autorisations suivantes à partir de  >  l’API Microsoft Graph :
    * User.Read (activé par défaut)
    * email
    * offline_access
    * OpenId
    * profil

3. Sélectionnez **Paramètres** dans le volet gauche et **sélectionnez Ajouter** un paramètre dans la section Paramètres de connexion **OAuth.**

    ![Affichage SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

4. Pour remplir le formulaire Nouveau paramètre de connexion, effectuez les étapes **suivantes** :

    >[!NOTE]
    > **L’octroi** implicite peut être requis dans l’application AAD.

    1. Entrez un **nom dans** la page Nouveau paramètre **de connexion.** Il s’agit du nom qui est référent dans les paramètres de votre code de service de bot à l’étape *5* de l' sso du bot lors [de l’utilisation.](#bot-sso-at-runtime)
    2. Dans la **drop-down Fournisseur** de services, **sélectionnez Azure Active Directory v2**.
    3. Entrez les informations d’identification du client, telles que **l’ID client** et la **secret client** pour l’application AAD.
    4. Pour **l’URL d’Exchange** de jeton, utilisez la valeur d’étendue définie dans mettre à jour le manifeste de votre [application Teams pour votre bot.](#update-your-teams-application-manifest-for-your-bot) L’URL d’Exchange de jeton indique au SDK que cette application AAD est configurée pour l' cesso.
    5. Dans la **zone ID client,** entrez *commun*.
    6. Ajoutez toutes les **étendues configurées** lors de la spécification d’autorisations pour les API en aval pour votre application AAD. Avec l’ID client et la secret client fournis, le magasin de jetons échange le jeton contre un jeton graphique avec des autorisations définies.
    7. Sélectionnez **Enregistrer**.

    ![Affichage des paramètres VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Mettre à jour le manifeste de votre application Teams pour votre bot

Si l’application contient un bot autonome, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste de l’application Teams :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Si l’application contient un bot et un onglet, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste de l’application Teams :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** est le parent des éléments suivants :

* **id** : ID client de l’application. Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès d’AAD.
* **ressource** : domaine et sous-domaine de votre application. Il s’agit du même URI, y compris le protocole que vous avez enregistré lors de la création de votre dans Enregistrer votre `api://` application via le portail `scope` [AAD](#register-your-app-through-the-aad-portal). Vous ne devez pas inclure le `access_as_user` chemin d’accès dans votre ressource. La partie domaine de cet URI doit correspondre au domaine et aux sous-domaines utilisés dans les URL de votre manifeste d’application Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Ajouter le code pour demander et recevoir un jeton de bot

#### <a name="request-a-bot-token"></a>Demander un jeton de bot

La demande d’obtenir le jeton est une demande de message POST normale à l’aide du schéma de message existant. Il est inclus dans les pièces jointes d’un OAuthCard. Le schéma de la classe OAuthCard est défini dans [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) et est similaire à une carte de signature. Teams traite cette demande comme une acquisition de jeton silencieuse si la propriété `TokenExchangeResource` est remplie sur la carte. Pour le canal Teams, seule la propriété, qui identifie de manière unique une demande de `Id` jeton, est honorée.

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` ou microsoft est pris en charge pour `MultiProviderAuthDialog` l’authentification sso.

Si l’utilisateur utilise l’application pour la première fois et que le consentement de l’utilisateur est requis, la boîte de dialogue suivante s’affiche pour poursuivre l’expérience de consentement :

![Boîte de dialogue de consentement](../../../assets/images/bots/bots-consent-dialogbox.png)

Lorsque l’utilisateur sélectionne **Continuer,** les événements suivants se produisent :

* Si le bot définit un bouton de sign-in, le flux de se connectant pour les bots est déclenché de la même façon que le flux de la signature à partir d’un bouton de carte OAuth dans un flux de message. Le développeur doit déterminer les autorisations qui nécessitent le consentement de l’utilisateur. Cette approche est recommandée si vous avez besoin d’un jeton avec des autorisations `openId` au-delà. Par exemple, si vous souhaitez échanger le jeton pour les ressources graphiques.

* Si le bot ne fournit pas de bouton de sign-in sur la carte OAuth, le consentement de l’utilisateur est requis pour un ensemble minimal d’autorisations. Ce jeton est utile pour l’authentification de base et pour obtenir l’adresse e-mail de l’utilisateur.

##### <a name="c-token-request-without-a-sign-in-button"></a>Demande de jeton C# sans bouton de sign-in

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a>Recevoir le jeton du bot

La réponse avec le jeton est envoyée par le biais d’une activité d’appel avec le même schéma que les autres activités d’appel que les bots reçoivent aujourd’hui. La seule différence est le nom de l’appel, **la sign-in/tokenExchange** et le **champ valeur.** Le **champ** de valeur contient **l’ID**, une chaîne  de la demande initiale pour obtenir le jeton et le champ de jeton, une valeur de chaîne incluant le jeton.

>[!NOTE]
> Vous pouvez recevoir plusieurs réponses pour une demande donnée si l’utilisateur a plusieurs points de terminaison actifs. Vous devez déduplicer les réponses avec le jeton.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Code C# pour gérer l’activité d’appel

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

Il `turnContext.activity.value` est de type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) et contient le jeton qui peut être utilisé par votre bot. Vous devez stocker les jetons pour des raisons de performances et les actualiser.

### <a name="update-the-auth-sample"></a>Mettre à jour l’exemple d’th

Ouvrez [l’exemple d’th](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) teams, puis complétez les étapes suivantes pour le mettre à jour :

1. Mettez à jour TeamsBot pour gérer le déduping de la demande entrante en incluant le code suivant :

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. Mise à jour pour inclure le mot de passe, et le nom de connexion défini dans Mettre à jour le portail Azure avec `appsettings.json` `botId` la connexion [OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Mettez à jour le manifeste et `token.botframework.com` assurez-vous qu’il figure dans la liste des domaines valides. Pour plus d’informations, voir [l’exemple d’th teams.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)
4. Zip the manifest with the profile images and install it in Teams.

#### <a name="additional-code-samples"></a>Exemples de code supplémentaires

* [Exemple C# utilisant le SDK Bot Framework.](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)

* [Exemple C# utilisant le SDK Bot Framework pour déduplicer la demande de jeton](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).

* Exemple C# sans utiliser le magasin de jetons [du SDK Bot Framework.](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
