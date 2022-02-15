---
title: Support de l'identification unique pour les robots
description: Décrit comment obtenir un jeton d’utilisateur. Actuellement, un développeur de bot peut utiliser une carte de visite ou le service de bot Azure avec la prise en charge de la carte OAuth.
keywords: token, user token, SSO support for bots, permission, Microsoft Graph, Azure AD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 760c9f964298e120dfaf5cfadd199f5a7d02454f
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821597"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Prise en charge de l’sign-on unique (SSO) pour les bots

L’authentification unique dans Azure Active Directory actualisez silencieusement le jeton d’authentification pour réduire le nombre de fois que les utilisateurs doivent entrer leurs informations d’identification de connexion. Si les utilisateurs acceptent d’utiliser votre application, ils n’ont pas à donner à nouveau leur consentement sur un autre appareil, car ils sont connectés automatiquement. Les onglets et les bots ont un flux similaire pour la prise en charge de l’cesso. Toutefois [, le bot demande des jetons](#request-a-bot-token) et [reçoit des réponses](#receive-the-bot-token) avec un protocole différent.

>[!NOTE]
> OAuth 2.0 est une norme ouverte d’authentification et d’autorisation utilisée par Azure AD et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams.

## <a name="bot-sso-at-runtime"></a>SO du bot lors de l’runtime

L’image suivante illustre le flux de l’sso dans les bots :

![Bot SSO lors de l’runtime diagram](../../../assets/images/bots/bots-sso-diagram.png)

Les étapes suivantes vous aident à l’authentification et aux jetons d’application bot :

1. Le bot envoie un message à Teams avec un OAuthCard `tokenExchangeResource` qui contient pour obtenir un jeton d’authentification pour l’application bot. L’utilisateur reçoit des messages sur tous les points de terminaison d’utilisateur actifs.

   > [!NOTE]
   >
   > * Un utilisateur peut avoir plusieurs points de terminaison actifs à la fois.
   > * Le jeton bot est reçu de chaque point de terminaison d’utilisateur actif.
   > * L’application doit être installée dans l’étendue personnelle pour la prise en charge de l’authentification unique.


1. Si l’utilisateur actuel utilise votre application bot pour la première fois, une invite de demande s’affiche pour lui demander d’appliquer l’une des actions suivantes :
    * Donner l’autorisation, si nécessaire.
    * Gérer l’authentification étape par étape, telle que l’authentification à deux facteurs.

1. Teams demande le jeton d’application bot au Azure AD point de terminaison de l’utilisateur actuel.

1. Azure AD envoie le jeton d’application bot à l’Teams application.

1. Teams envoie le jeton au bot dans le cadre de l’objet de valeur renvoyé par l’facturation avec **sign-in/tokenExchange**.
  
1. Le jeton analysée dans l’application bot fournit les informations requises, telles que l’adresse de l’utilisateur.
  
## <a name="develop-an-sso-teams-bot"></a>Développer un bot d’Teams sso
  
Les étapes suivantes vous guident pour développer des bots d’Teams d’lui-même :

1. [Inscrivez votre application via le portail Azure AD web](#register-your-app-through-the-azure-ad-portal).
1. [Mettez à jour Teams manifeste d’application pour votre bot](#update-your-teams-application-manifest-for-your-bot).
1. [Ajoutez le code pour demander et recevoir un jeton de bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-azure-ad-portal"></a>Inscrire votre application via le portail Azure AD web

Les étapes d’inscription de votre application via Azure AD portail sont similaires au flux [d’utilisateur unique de l’onglet](../../../tabs/how-to/authentication/auth-aad-sso.md). Les étapes suivantes vous guident pour inscrire votre application :

1. Inscrivez une nouvelle application dans le [portail Azure Active Directory – Inscriptions des](https://go.microsoft.com/fwlink/?linkid=2083908) applications.

1. Sélectionnez **Nouvelle inscription**. La page **Inscrire une application** s’affiche.

    ![Nouvelle inscription](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. Dans **l’enregistrement d’une application**, faites les étapes suivantes :

   > [!NOTE]
   >
   > Les utilisateurs ne sont pas invités à donner leur consentement et se voir accorder des jetons d’accès immédiatement, si l’application Azure AD est inscrite dans le même client qu’il fait une demande d’authentification dans Teams. Toutefois, les utilisateurs doivent donner leur consentement aux autorisations, si l’application Azure AD est inscrite dans un autre client.

    * Entrez **le nom** de votre application.
    * **Sélectionnez les types de comptes pris** en charge, tels que le client unique ou le multi-locataire.
    * Sélectionnez **Inscrire**.

    ![Enregistrer une application](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. Go to overview page.
1. Copiez la valeur de **l’ID d’application (client**).
1. Sous **Gérer**, allez sur **Exposer une API**

   > [!TIP]
   > Pour mettre à jour le manifeste de votre application ultérieurement, enregistrez la valeur **de l’ID de l’application (** client).

   > [!IMPORTANT]
   > * Si vous construisez un bot autonome, entrez l’URI d’ID d’application sous le nom `api://botid-{YourBotId}`. Ici *, YourBotId est* votre ID Azure AD’application.
   > * Si vous créez une application avec un bot et un onglet, saisissez l'URI de l'ID d'application au format `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Sélectionnez les autorisations dont votre application a besoin pour Azure AD point de terminaison et, éventuellement, pour Microsoft Graph.
1. [Accordez des autorisations](/azure/active-directory/develop/v2-permissions-and-consent) Teams applications mobiles, web et de bureau.
1. Sélectionnez **Ajouter une étendue**.
1. Dans le panneau qui vous invite, entrez `access_as_user` le nom de **l’étendue**.

   >[!NOTE]
   > L’étendue « access_as_user » utilisée pour ajouter une application cliente est pour « Administrateurs et utilisateurs ».
   >
   > Vous devez connaître les restrictions importantes suivantes :
   >
   > * Seules les autorisations de l’API microsoft Graph de niveau utilisateur, telles que la messagerie, le profil, offline_access et OpenId, sont pris en charge. Si vous avez besoin d’accéder à d’autres Graph Microsoft, `User.Read` `Mail.Read`telles que ou , voir Obtenir un jeton d’accès [avec Graph autorisations](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions).
   > * Le nom de domaine de votre application doit être identique au nom de domaine que vous avez inscrit pour Azure AD application.
   > * Plusieurs domaines par application ne sont actuellement pas pris en charge.
   > * Les applications qui utilisent le `azurewebsites.net` domaine ne sont pas pris en charge car elles sont courantes et peuvent être un risque pour la sécurité.

1. Dans la **Qui pouvez-vous consentir ?**, entrez **Administrateurs et utilisateurs**.
1. Entrez les détails suivants pour configurer les invites de consentement de l’administrateur et de l’utilisateur avec des valeurs appropriées pour l’étendue `access_as_user`.
    * **Nom complet du consentement de** l’administrateur : Teams pouvez accéder au profil de l’utilisateur.
    * **Description du consentement de l'administrateur** : les équipes peuvent appeler les API Web de l'application en tant qu'utilisateur actuel.
    * **Nom complet du consentement de** l’utilisateur : Teams pouvez accéder à votre profil et effectuer des demandes en votre nom.
    * **Description du consentement de** l’utilisateur : Teams pouvez appeler les API de cette application avec les mêmes droits que vous.

    ![administrateur et utilisateurs](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. Assurez-vous que l’état **est activé**.

    ![State](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. Sélectionnez **Ajouter une étendue** pour enregistrer les détails. La partie domaine du nom  d’étendue affiché doit automatiquement correspondre à l’URI **d’ID d’application** définie à l’étape précédente, `/access_as_user` avec ajouté à la fin.`api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`

1. Dans les **applications clientes autorisées**, identifiez les applications que vous souhaitez autoriser pour l’application web de votre application.
1. Sélectionnez **Ajouter une application cliente**.

    ![application cliente](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. Entrez chacun des ID client suivants et sélectionnez la portée autorisée que vous avez créée à l'étape précédente :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` pour l'application mobile ou de bureau Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` pour l'application Web Teams.

    ![id client](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. Allez à **l’authentification**.
1. Dans **configurations de plateforme**, **sélectionnez Ajouter une plateforme**.

    ![platform](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. Sélectionnez **Web**.

    ![Configurer la plateforme](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. Entrez les **URIs de redirection** pour votre application.

   >[!NOTE]
   > Cet URI doit être un nom de domaine complet. Il est également suivi de la route API où une réponse d'authentification est envoyée. Si vous suivez l'un des exemples Teams, l'URI est `https://token.botframework.com/.auth/web/redirect`. Pour plus d'informations, consultez [Flux de code d'autorisation OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    ![URI de redirection](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. Ajoutez les **autorisations d’API nécessaires**.
    * Sélectionnez **les autorisations d’API** dans le plan de gauche.
    * **Sélectionnez Ajouter une plateforme** pour ajouter les autorisations déléguées utilisateur dont votre application a besoin pour les API en aval, par exemple, User.Read.

1. Les étapes suivantes vous aideront à activer l’octroi implicite :
    * Sélectionnez **Authentification** dans le volet gauche.
    * Cochez **les jetons Access** et **les jetons d’ID** .
    
    ![Flux d’octroi](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)
    
    * **Sélectionnez Enregistrer** pour enregistrer les modifications.

#### <a name="update-manifest-in-microsoft-azure-portal"></a>Mettre à jour le manifeste dans Microsoft Azure portail

Les étapes suivantes vous guident pour mettre à jour le manifeste du bot dans le portail Azure :

1. **Sélectionnez Manifeste** dans le volet gauche.
1. Assurez-vous que l’élément de config est définie sur **« accessTokenAcceptedVersion » : 2**. Si ce n’est pas le cas, modifiez sa valeur sur **2**.

    ![Mettre à jour le manifeste](~/assets/images/bots/update-manifest.png)


   >[!NOTE]
   > Si vous êtes déjà en cours de test de votre bot dans Teams, vous devez vous dé connectez à partir de cette application et dé sign out de Teams. Connectez-vous à nouveau pour voir cette modification.

1. Sélectionnez **Enregistrer**.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Mettre à jour le portail Azure avec la connexion OAuth

Les étapes suivantes vous guident pour mettre à jour le portail Azure avec la connexion OAuth :

1. Dans le portail Azure, allez à [**AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
1. Go to **Configuration** on the left pane.
1. **Sélectionnez Ajouter une connexion OAuth Paramètres**.

    ![Paramètre de configuration](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. Les étapes suivantes vous guident pour remplir le formulaire **Nouveau paramètre de** connexion :

   >[!NOTE]
   > **Un octroi implicite** peut être requis dans l’application Azure AD’application.

    * Entrez **le nom** dans la page **Nouveau paramètre de connexion** .

    >[!NOTE]
    > Le **nom** est référent aux paramètres de votre code de service de bot à *l’étape 5* de [l’sso bot lors de l’utilisation](#bot-sso-at-runtime).

    * Dans la **drop-down Fournisseur** de services, **sélectionnez Azure Active Directory v2**.
    * Entrez les informations d’identification du client, telles que **l’ID client** et la secret **client** pour l’application Azure AD client.
    * Pour **l’URL Exchange jeton**, utilisez la valeur d’étendue définie dans Mettre à jour [Teams manifeste d’application pour votre bot](#update-your-teams-application-manifest-for-your-bot). L’URL Exchange de jeton indique au SDK que cette application Azure AD est configurée pour l’sso.
    * Dans **l’ID de client**, entrez *common*.
    * Ajoutez toutes les **étendues configurées** lors de la spécification d’autorisations pour les API en aval pour Azure AD application. Avec l’ID client et la secret client fournis, le magasin de jetons échange le jeton contre un jeton graphique avec des autorisations définies.
    * Sélectionnez **Enregistrer**.
    * Sélectionnez **Appliquer**.
   
    ![Paramètre de connexion](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Mettre à jour Teams manifeste d’application pour votre bot

Si l’application contient un bot autonome, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste Teams’application :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Si l’application contient un bot et un onglet, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste Teams’application :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** est le parent des éléments suivants :

* **id** – ID client de l'application. Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès Azure AD. Ne partagez pas cet ID d’application avec plusieurs Teams applications. Créez une application Azure AD pour chaque manifeste d’application qui utilise `webApplicationInfo`.
* **ressource** – Le domaine et le sous-domaine de votre application. Il s’agit du même URI, `api://` `scope` y compris le protocole que vous avez inscrit lors de la création de votre application dans Enregistrer votre application [via le portail Azure AD.](#register-your-app-through-the-azure-ad-portal) N’incluez pas le chemin `access_as_user` d’accès dans votre ressource. La partie domaine de cet URI doit correspondre au domaine et aux sous-domaines utilisés dans les URL de votre manifeste Teams’application.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Ajouter le code pour demander et recevoir un jeton de bot

#### <a name="request-a-bot-token"></a>Demander un jeton de bot

La demande d’obtenir le jeton est une demande de message POST normale à l’aide du schéma de message existant. Il est inclus dans les pièces jointes d’un OAuthCard. Le schéma de la classe OAuthCard est défini dans [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) et est similaire à une carte de signature. Teams traite cette demande comme une acquisition de jeton silencieuse `TokenExchangeResource` si la propriété est remplie sur la carte. Pour le Teams, seule `Id` la propriété, qui identifie de manière unique une demande de jeton, est honorée.

>[!NOTE]
> Le Microsoft Bot Framework `OAuthPrompt` ou est pris `MultiProviderAuthDialog` en charge pour l’authentification sso.

Si l’utilisateur utilise l’application pour la première fois et que le consentement de l’utilisateur est requis, la boîte de dialogue suivante s’affiche pour poursuivre l’expérience de consentement :

![Boîte de dialogue de consentement](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

Lorsque l’utilisateur sélectionne **Continuer**, ces événements se produisent :

* Si le bot définit un bouton de sign-in, le flux de se connectant pour les bots est activé de la même manière que le flux de sign-in à partir d’un bouton de carte OAuth dans un flux de message. Le développeur doit décider des autorisations qui nécessitent le consentement de l’utilisateur. Cette approche est recommandée si vous avez besoin d’un jeton avec des autorisations au-delà `openId`. Par exemple, si vous souhaitez échanger le jeton pour les ressources graphiques.

* Si le robot ne fournit pas de bouton de connexion sur la carte OAuth, l’autorisation de l’utilisateur est requise pour un ensemble minimal d’autorisations. Ce jeton est utile pour l’authentification de base et pour obtenir l’adresse e-mail de l’utilisateur.

##### <a name="c-token-request-without-a-sign-in-button"></a>C# demande de jeton sans bouton de sign-in

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

La réponse avec le jeton est envoyée par le biais d’une activité d’appel avec le même schéma que les autres activités d’appel que les bots reçoivent aujourd’hui. La seule différence est le nom de l’appel, **la sign-in/tokenExchange** et le **champ valeur** . Le **champ** valeur contient **l’ID**, une chaîne de la demande initiale pour obtenir le jeton  et le champ de jeton, une valeur de chaîne incluant le jeton.

>[!NOTE]
> Vous pouvez recevoir plusieurs réponses pour une demande donnée si l’utilisateur a plusieurs points de terminaison actifs. Vous devez déduplicer les réponses avec le jeton.

##### <a name="c-code-to-handle-the-invoke-activity"></a>C# code pour gérer l’activité d’appel

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

### <a name="token-exchange-failure"></a>Échec de l’échange de jetons

En cas d’échec d’échange de jetons, utilisez le code suivant :

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

Pour comprendre ce que fait le bot lorsque l’échange de jetons ne parvient pas à déclencher une invite de consentement, consultez les étapes suivantes :

>[!NOTE]
> Aucune action de l’utilisateur n’est requise car le bot prend les mesures en cas d’échec de l’échange de jetons.

1. Le client démarre une conversation avec le bot déclenchant un scénario OAuth.
2. Le bot renvoie une carte OAuth au client.
3. Le client intercepte la carte OAuth avant de l’afficher à l’utilisateur et vérifie si elle contient une `TokenExchangeResource` propriété.
4. Si la propriété existe, le client envoie un message `TokenExchangeInvokeRequest` au bot. Le client doit avoir un jeton échangeable pour l’utilisateur, qui doit être un jeton Azure AD v2 et dont l’audience doit être identique à la `TokenExchangeResource.Uri` propriété. Le client envoie une activité d’appel au bot avec le code suivant :

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. Le bot traite le `TokenExchangeInvokeRequest` client et renvoie un `TokenExchangeInvokeResponse` retour au client. Le client doit attendre qu’il reçoit le `TokenExchangeInvokeResponse`.

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. S’il `TokenExchangeInvokeResponse` en possède `200``status` une, le client n’affiche pas la carte OAuth. Voir [l’image de flux normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Pour toute autre carte `status` ou si elle n’est `TokenExchangeInvokeResponse` pas reçue, le client affiche la carte OAuth à l’utilisateur. Voir [l’image de flux de récupération](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). S’il existe des erreurs ou des dépendances non satisfaits, telles que le consentement de l’utilisateur, cette activité garantit que le flux DSO revient au flux OAuthCard normal.


### <a name="update-the-auth-sample"></a>Mettre à jour l’exemple d’th

[Ouvrez Teams exemple d’th,](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) puis complétez les étapes suivantes pour le mettre à jour :

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
  
2. Mise `appsettings.json` à jour pour inclure le `botId`mot de passe et le nom de connexion définis dans Mettre à jour le portail [Azure avec la connexion OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Mettez à jour le manifeste et assurez-vous qu’il `token.botframework.com` figure dans la liste des domaines valides. Pour plus d’informations, [voir Teams auth.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)
4. Zip the manifest with the profile images and install it in Teams.

## <a name="code-sample"></a>Exemple de code
|**Exemple de nom** | **Description** |**.NET** | 
|----------------|-----------------|--------------|
|Bot framework SDK | Exemple d’utilisation du SDK Bot Framework. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-bots-with-sso.yml), qui vous aide à créer un bot avec l’authentification sso activée.
