---
title: Support de l'identification unique pour les robots
description: Découvrez comment obtenir un jeton utilisateur et qu’un développeur de bots peut utiliser une carte de connexion ou le service de bot Azure avec la prise en charge de la carte OAuth.
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: ea0c7efff7c5d31097226cd689d8988d5ef51694
ms.sourcegitcommit: 4d1740b235000d51711a9170ac0f026c63c945ac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2022
ms.locfileid: "66611498"
---
# <a name="use-sso-authentication-for-bots"></a>Utiliser l’authentification unique pour les bots

L'authentification par authentification unique dans Microsoft Azure Active Directory (Azure AD) rafraîchit silencieusement le jeton d'authentification afin de réduire le nombre de fois où les utilisateurs doivent saisir leurs informations d'identification. Si les utilisateurs acceptent d'utiliser votre application, ils n'ont pas besoin de donner à nouveau leur consentement sur un autre appareil car ils sont automatiquement connectés. Les onglets et les bots ont un flux similaire pour la prise en charge de l’authentification unique. Mais le bot [demande des jetons](#request-a-bot-token) et [reçoit des réponses](#receive-the-bot-token) avec un protocole différent.

>[!NOTE]
> OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure AD et de nombreux autres fournisseurs d’identité. Une compréhension de base du flux d’octroi implicite OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans les onglets Microsoft Teams.

Consultez la vidéo suivante pour en savoir plus sur la prise en charge de l’authentification unique (SSO) pour les bots :
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OASc]
<br>

## <a name="bot-sso-at-runtime"></a>Bot SSO au moment de l’exécution

L'image suivante illustre le flux du SSO dans les bots :

![Diagramme de l’authentification unique bot au moment de l’exécution](../../../assets/images/bots/bots-sso-diagram.png)

Les étapes suivantes vous aident avec l’authentification et les jetons d’application de bot :

1. Le bot envoie un message à Teams avec un OAuthCard qui contient `tokenExchangeResource` pour obtenir un jeton d’authentification pour l’application de bot. L’utilisateur reçoit des messages sur tous les points de terminaison d’utilisateur actifs.

   > [!NOTE]
   >
   > * Un utilisateur peut avoir plusieurs points de terminaison actifs à la fois.
   > * Le jeton bot est reçu de chaque point de terminaison d’utilisateur actif.
   > * L’application doit être installée dans l’étendue personnelle pour la prise en charge de l’authentification unique.

1. Si l'utilisateur actuel utilise l'application bot pour la première fois, une demande lui est adressée pour qu'il effectue l'une des actions suivantes :
    * Donner l’autorisation, si nécessaire.
    * Gérer l’authentification étape par étape, telle que l’authentification à deux facteurs.

1. Teams demande le jeton d’application bot à partir du point de terminaison Azure AD pour l’utilisateur actuel.

1. Azure AD envoie le jeton d’application bot à l’application Teams.

1. Teams envoie le jeton au robot en tant que partie de l'objet de valeur renvoyé par l'invocation avec **sign in/tokenExchange**.
  
1. Le jeton analysée dans l’application bot fournit les informations requises, telles que l’adresse de l’utilisateur.
  
## <a name="develop-an-sso-teams-bot"></a>Développer un onglet SSO Microsoft Teams
  
Les étapes suivantes vous guident pour développer l’authentification unique Teams bot :

1. [Inscrire votre application via le portail Azure AD web](#register-your-app-through-the-azure-ad-portal)
1. [Mettez à jour votre manifeste d’application Teams pour votre bot](#update-your-teams-application-manifest-for-your-bot).
1. [Ajoutez le code pour demander et recevoir un jeton de bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-azure-ad-portal"></a>Inscrire votre application via le portail Azure AD web

Les étapes d’inscription de votre application via le portail Azure AD sont similaires au [flux d’authentification unique de l’onglet](../../../tabs/how-to/authentication/tab-sso-overview.md). Les étapes suivantes vous guident pour inscrire votre application :

1. Inscrivez une nouvelle application dans le portail [Microsoft Azure Active Directory - Enregistrer une application](https://go.microsoft.com/fwlink/?linkid=2083908).

1. Sélectionnez **Nouvelle inscription**. La page **Inscrire une application** s’affiche.

    ![Nouvelle inscription](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. Sur la page **Enregistrer une application**, procédez comme suit :

   > [!NOTE]
   >
   > Les utilisateurs ne sont pas invités à donner leur consentement et reçoivent immédiatement des jetons d'accès si l'application Azure AD est enregistrée dans le même locataire que celui où ils font une demande d'authentification dans Teams. Toutefois, les utilisateurs doivent donner leur consentement aux autorisations, si l'application Azure AD est enregistrée dans un autre locataire.

    * Entrez un **Nom** pour votre application.
    * Sélectionnez **les types de comptes pris en charge**, tels que le locataire unique ou le multilocataire.
    * Sélectionnez **Inscrire**.

    ![Enregistrer une application](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. Accédez à la page de vue d’ensemble.
1. Copiez la valeur de **l’ID d’application (client**).
1. Sélectionnez **Exposer une API** sous **Gérer**.

   > [!TIP]
   > Pour mettre à jour votre manifeste d’application ultérieurement, enregistrez la valeur de **l’ID d’application (client** ).

   > [!IMPORTANT]
   >
   > * Si vous créez une application avec un bot et un onglet, saisissez l'URI de l'ID d'application au format `api://botid-{YourBotId}`. Ici *, YourBotId* est votre ID d’application Azure AD.
   > * Si vous créez une application avec un bot et un onglet, saisissez l'URI de l'ID d'application au format `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Sélectionnez **Ajouter une étendue**.
1. Dans le volet qui s’ouvre, entrez `access_as_user` en tant que **nom de l’étendue**.

   >[!NOTE]
   > L’étendue « access_as_user » utilisée pour ajouter une application cliente est destinée aux « administrateurs et utilisateurs ».
   >
   > Vous devez connaître les restrictions importantes suivantes :
   >
   > * Seules les autorisations Microsoft API Graph au niveau de l’utilisateur, telles que l’e-mail, le profil, offline_access et OpenId, sont prises en charge. Si vous avez besoin d’accéder à d’autres étendues Microsoft Graph, telles que `User.Read` ou `Mail.Read`, consultez [Étendre l’application onglet avec des autorisations et une étendue Microsoft Graph](../../../tabs/how-to/authentication/tab-sso-graph-api.md).
   > * Le nom de domaine de votre application doit être le même que le nom de domaine que vous avez enregistré pour votre application Azure AD.
   > * Les domaines multiples par application ne sont actuellement pas pris en charge.
   > * Les applications qui utilisent le `azurewebsites.net` domaine ne sont pas prises en charge, car elles sont courantes et peuvent constituer un risque pour la sécurité.

1. Dans la section **Qui peut consentir ?**, saisissez **Administrateurs et utilisateurs**.
1. Entrez les détails suivants pour configurer les invites de consentement de l'administrateur et de l'utilisateur avec des valeurs appropriées à la portée `access_as_user`.
    * **Nom d’affichage du consentement de l’administrateur :** Teams peut accéder au profil de l’utilisateur.
    * **Description du consentement de l'administrateur** : les équipes peuvent appeler les API Web de l'application en tant qu'utilisateur actuel.
    * **Nom d’affichage de consentement de l'utilisateur** : les équipes peuvent accéder à votre profil et faire des demandes en votre nom.
    * **Description du consentement de l'utilisateur :** Teams peuvent appeler les API de cette application avec les mêmes droits que vous.

    ![administrateur et utilisateurs](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. Assurez-vous que l'état est défini sur **Activé**.

    ![État](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. Sélectionnez **ajouter une portée** pour enregistrer les détails. La **partie domaine du nom** de l'application affichée doit automatiquement correspondre à l' URI de **l' ID de l'application** défini à l'étape précédente, avec `/access_as_user`un ajout à la fin`api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.

1. Dans **Applications clientes autorisées**, identifiez les applications que vous souhaitez autoriser pour l'application Web de votre application.
1. Sélectionnez **Ajouter une application cliente**.

    ![Application cliente](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. Entrez chacun des ID client suivants et sélectionnez la portée autorisée que vous avez créée à l'étape précédente :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` pour l'application mobile ou de bureau Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` pour l'application Web Teams.

    ![ID du client](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. Accédez à **l’authentification**.
1. Dans la section **Configurations de plateforme**, sélectionnez le bouton **Ajouter une plateforme**.

    ![platform](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. Sélectionnez **Web**.

    ![Configurer la plateforme](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. Entrez les **URI de redirection** de votre application.

   >[!NOTE]
   > Cet URI doit être un nom de domaine complet. Il est également suivi de la route API où une réponse d'authentification est envoyée. Si vous suivez l'un des exemples Teams, l'URI est `https://token.botframework.com/.auth/web/redirect`. Pour plus d'informations, consultez [Flux de code d'autorisation OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    ![Uris de redirection](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. Les étapes suivantes vous aideront à activer l’octroi implicite :
    * Sélectionnez **Applications** dans le volet gauche.
    * Cochez les cases **Jetons d’accès** et **jetons d’ID** .

    ![Flux d’octroi](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)

    * Sélectionnez **Enregistrer** pour enregistrer vos modifications.

1. Ajoutez **les autorisations API** nécessaires.
    * Sélectionnez **les autorisations d’API** dans le volet gauche.
    * Sélectionnez **Ajouter une plateforme** pour ajouter les autorisations dont votre application a besoin pour les API en aval, par exemple, User.Read.

#### <a name="update-manifest-in-microsoft-azure-portal"></a>Mettre à jour le manifeste dans Microsoft Azure portail

Les étapes suivantes vous guideront pour mettre à jour le manifeste du bot dans Portail Azure :

1. Sélectionnez **Manifeste** dans le volet gauche.
1. Vérifiez que l’élément de configuration est défini sur **« accessTokenAcceptedVersion » : 2**. Si ce n’est pas le cas, remplacez sa valeur par **2**.

    ![Mise à jour du manifeste](~/assets/images/bots/update-manifest.png)

   >[!NOTE]
   > Si vous testez déjà votre bot dans Teams, vous devez vous déconnecter de cette application et vous déconnecter de Teams. Ensuite, reconnectez-vous pour voir cette modification.

1. Sélectionnez **Enregistrer**.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Mettre à jour le Portail Azure avec la connexion OAuth

Les étapes suivantes vous guideront pour mettre à jour le portail Azure avec la connexion OAuth :

1. Dans le portail Azure, accédez à [**AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot).
1. Accédez à **Configuration** dans le volet gauche.
1. Sélectionnez le bouton **Ajouter des paramètres de connexion OAuth**.

    ![Paramètre de configuration](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. Les étapes suivantes vous guideront pour remplir le formulaire **Nouveau paramètre de connexion** :

   >[!NOTE]
   > **L’octroi implicite** peut être requis dans l’application Azure AD.

    * Entrez **le nom** dans la page **Nouveau paramètre de connexion** .

    >[!NOTE]
    > Le **nom** est référencé aux paramètres de votre code de service de bot à *l’étape 5* de l’authentification unique bot [au moment de l’exécution](#bot-sso-at-runtime).

    * Dans la liste déroulante **Fournisseur de** services, sélectionnez **Azure Active Directory v2**.
    * Entrez les informations d’identification du client, telles que **l’ID client** et la **clé secrète client** pour l’application Azure AD.
    * Pour **l’URL Exchange** jeton, utilisez la valeur d’étendue définie dans [Mettre à jour votre manifeste d’application Teams pour votre bot](#update-your-teams-application-manifest-for-your-bot), par exemple. `api://botid-<your-app-id>/` L'URL d’Exchange de jetons indique au SDK que cette application Azure AD est configurée pour le SSO.
    * Dans **l’ID de locataire**, entrez *common*.
    * Ajoutez toutes les **étendues** configurées lors de la spécification d’autorisations aux API en aval pour votre application Azure AD. Avec l’ID client et la clé secrète client fournis, le magasin de jetons échange le jeton contre un jeton de graphe avec des autorisations définies.
    * Sélectionnez **Enregistrer**.
    * Sélectionnez **Appliquer**.

    ![Paramètre de connexion](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Mettre à jour votre manifeste d’application Teams pour votre bot

Si l’application contient un bot autonome, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste d’application Teams :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```

Si l’application contient un bot et un onglet, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste d’application Teams :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** est le parent des éléments suivants :

* **id** – ID client de l'application. Il s'agit de l'ID d'application que vous avez obtenu lors de l'inscription de l'application auprès d'Azure AD. Ne partagez pas cet ID d’application avec plusieurs applications Teams. Créez une application Azure AD pour chaque manifeste d’application qui utilise `webApplicationInfo`.
* **ressource** – Le domaine et le sous-domaine de votre application. Il s’agit du même URI, y compris le protocole que vous avez inscrit lors de la `api://` création de votre `scope` dans [application dans Inscrire votre application via le portail Azure AD](#register-your-app-through-the-azure-ad-portal). Ne pas inclure le `access_as_user` chemin dans votre ressource La partie domaine de cet URI doit correspondre au domaine et aux sous-domaines utilisés dans les URL de votre manifeste d'application Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Ajouter le code pour demander et recevoir un jeton de bot

#### <a name="request-a-bot-token"></a>Demander un jeton de bot

La demande d’obtenir un jeton d’accès implique la soumission d’une demande de message HTTP POST à l’aide du schéma de message existant. Il est inclus dans les pièces jointes d'une carte OAuthCard. Le schéma de la classe OAuthCard est défini dans [Microsoft Bot Schema 4.0 ](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true)et son semblable à une carte d'identification. Teams traite cette demande comme une acquisition de jeton silencieux si la propriété `TokenExchangeResource` est remplie sur la carte. Pour le canal Teams, seule la`Id` propriété, qui identifie de manière unique une demande de jeton, est honorée.

>[!NOTE]
> Le Microsoft Bot Framework `OAuthPrompt` ou `MultiProviderAuthDialog` est pris en charge pour l’authentification unique.

Si l’utilisateur utilise l’application pour la première fois et que le consentement de l’utilisateur est requis, la boîte de dialogue suivante s’affiche pour poursuivre l’expérience de consentement :

![Boîte de dialogue Consentement](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

Lorsque l’utilisateur sélectionne **Continuer**, ces événements se produisent :

* Si le robot définit un bouton d'ouverture de session, le flux d'ouverture de session pour les robots est activé et est similaire au flux d'ouverture de session d'un bouton de carte OAuth dans un flux de messages. Le développeur doit décider des autorisations qui nécessitent le consentement de l’utilisateur. Cette approche est recommandée si vous avez besoin d'un jeton avec des autorisations supérieures à `openId`. Par exemple, si vous souhaitez échanger le jeton contre des ressources de graphe.

* Si le robot ne fournit pas de bouton de connexion sur la carte OAuth, l’autorisation de l’utilisateur est requise pour un ensemble minimal d’autorisations. Ce jeton est utile pour l’authentification de base et pour obtenir l’adresse e-mail de l’utilisateur.

##### <a name="c-token-request-without-a-sign-in-button"></a>Demande de jeton C# sans bouton de connexion

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

La réponse avec le jeton est envoyée par le biais d’une activité d’appel avec le même schéma que les autres activités d’appel que les bots reçoivent aujourd’hui. La seule différence est le nom d’appel, la **connexion/tokenExchange** et le champ **valeur** . Le champ **valeur** contient **l’ID**, une chaîne de la requête initiale pour obtenir le jeton et le champ **de jeton** , une valeur de chaîne incluant le jeton.

>[!NOTE]
> Vous pouvez recevoir plusieurs réponses pour une requête donnée si l’utilisateur a plusieurs points de terminaison actifs. Vous devez dédupliquer les réponses avec le jeton.

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

De `turnContext.activity.value` type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) , il contient le jeton qui peut être utilisé par votre bot. Vous devez stocker les jetons pour des raisons de performances et les actualiser.

### <a name="token-exchange-failure"></a>Échec de l’échange de jetons

En cas d’échec de l’échange de jetons, utilisez le code suivant :

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

Pour comprendre ce que fait le bot lorsque l’échange de jetons ne déclenche pas d’invite de consentement, consultez les étapes suivantes :

>[!NOTE]
> Aucune action de l’utilisateur n’est requise, car le bot effectue les actions en cas d’échec de l’échange de jetons.

1. Le client démarre une conversation avec le bot déclenchant un scénario OAuth.
2. Le bot renvoie une carte OAuth au client.
3. Le client intercepte la carte OAuth avant de l’afficher à l’utilisateur et vérifie si elle contient une `TokenExchangeResource` propriété.
4. Si la propriété existe, le client envoie un `TokenExchangeInvokeRequest` message au bot. Le client doit avoir un jeton échangeable pour l’utilisateur, qui doit être un jeton Azure AD v2 et dont l’audience doit être identique à la propriété `TokenExchangeResource.Uri`. Le client envoie une activité d’appel au bot avec le code suivant :

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

5. Le bot traite et `TokenExchangeInvokeRequest` retourne un `TokenExchangeInvokeResponse` retour au client. Le client doit attendre jusqu’à ce qu’il reçoive le `TokenExchangeInvokeResponse`.

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

6. Si la `TokenExchangeInvokeResponse` valeur est `status` de `200`, le client n’affiche pas la carte OAuth. Afficher [l’image de flux normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Pour tout autre ou `status` si le `TokenExchangeInvokeResponse` n’est pas reçu, le client affiche la carte OAuth à l’utilisateur. Afficher [l’image de flux de secours](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) En cas d’erreurs ou de dépendances non satisfaites telles que le consentement de l’utilisateur, cette activité garantit que le flux d’authentification unique revient au flux OAuthCard normal.

### <a name="update-the-auth-sample"></a>Mettre à jour l’exemple d’authentification

Ouvrez [l’exemple d’authentification Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth), puis effectuez les étapes suivantes pour le mettre à jour :

1. Mettez à jour TeamsBot pour gérer la déduplication de la requête entrante en incluant le code suivant :

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
  
2. Mise à jour `appsettings.json` pour inclure le `botId`mot de passe et le nom de connexion définis dans [Mettre à jour le Portail Azure avec la connexion OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Mettez à jour le manifeste et vérifiez qu’il `token.botframework.com` figure dans la liste des domaines valides. Pour plus d'informations, voir [l'exemple de Teams auth](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Compressez le manifeste avec les images de profil et installez-le dans Teams.

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom** | **Description** |**.NET** |**C#** |**Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
|Kit de développement logiciel (SDK) Bot Framework | Cet exemple de code montre comment commencer à utiliser l’authentification dans un bot pour Microsoft Teams. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/csharp_dotnetcore/BotConversationSsoQuickstart)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/js)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-bots-with-sso.yml) pour créer un bot avec l’authentification unique.
