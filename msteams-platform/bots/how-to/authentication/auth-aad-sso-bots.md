---
title: Support de l'identification unique pour les robots
description: Décrit comment obtenir un jeton utilisateur. Actuellement, un développeur de bot peut utiliser une carte de visite ou le service azure bot avec le support de la carte OAuth.
keywords: jeton, jeton utilisateur, prise en charge SSO pour les bots
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a43c2a46561149ff97d039a3ba8fe9f4472e2073
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566084"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Prise en charge unique de la signalisation (SSO) pour les bots

L’authentification unique en Azure Active Directory (AAD) minimise le nombre de fois que les utilisateurs doivent entrer leur signe dans les informations d’identification en rafraichissant silencieusement le jeton d’authentification. Si les utilisateurs acceptent d’utiliser votre application, ils n’ont plus besoin d’accord pour un autre appareil et peuvent se connecter automatiquement. Le flux est similaire à celui [de l’onglet Microsoft Teams support SSO](../../../tabs/how-to/authentication/auth-aad-sso.md), cependant, la différence est dans le protocole pour la façon dont un bot [demande des jetons et](#request-a-bot-token) reçoit des [réponses](#receive-the-bot-token).

>[!NOTE]
> OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisées par l’AAD et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable pour travailler avec l’authentification Teams.

## <a name="bot-sso-at-runtime"></a>Bot SSO à l’heure d’exécution

![Bot SSO au diagramme de temps d’exécution](../../../assets/images/bots/bots-sso-diagram.png)

Complétez les étapes suivantes pour obtenir des jetons d’authentification et d’application bot :

1. Le robot envoie un message avec une carte OAuth qui contient la propriété `tokenExchangeResource`. Il indique aux Teams d’obtenir un jeton d’authentification pour l’application bot. L’utilisateur reçoit des messages sur tous les points de terminaison d’utilisateur actifs.

    > [!NOTE]
    >* Un utilisateur peut avoir plusieurs points de terminaison actifs à la fois.
    >* Le jeton bot est reçu de chaque point de terminaison d’utilisateur actif.
    >* L’application doit être installée dans l’étendue personnelle pour la prise en charge de l’authentification unique.

1. Si l’utilisateur actuel utilise votre application bot pour la première fois, une invite de demande apparaît demandant à l’utilisateur de faire l’un des éléments suivants :
    * Donner son consentement, au besoin.
    * Gérer l’authentification étape par étape, telle que l’authentification à deux facteurs.

1. Teams le jeton d’application bot à partir du point de terminaison AAD pour l’utilisateur actuel.

1. AAD envoie le jeton d’application bot à l’application Teams’application.

1. Teams envoie le jeton au bot dans le cadre de l’objet de valeur retourné par l’activité invoquer avec **le nom sign-in/tokenExchange**.
  
1. Le jeton analysée dans l’application bot fournit les informations requises, telles que l’adresse de l’utilisateur.
  
## <a name="develop-an-sso-teams-bot"></a>Développer un bot SSO Teams
  
Terminez les étapes suivantes pour développer un bot SSO Teams:

1. [Enregistrez votre application via le portail AAD](#register-your-app-through-the-aad-portal).
1. [Mettez à jour Teams manifeste d’application pour votre bot](#update-your-teams-application-manifest-for-your-bot).
1. [Ajoutez le code à la demande et recevez un jeton bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-aad-portal"></a>Inscrivez votre application via le portail AAD

Les étapes d’enregistrement de votre application via le portail AAD sont similaires au [flux SSO onglet](../../../tabs/how-to/authentication/auth-aad-sso.md). Remplissez les étapes suivantes pour enregistrer votre application :

1. Enregistrez une nouvelle application dans le [portail Azure Active Directory - Inscriptions d’applications.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Sélectionnez **Nouvelle inscription**. Le **Registre d’une** page de demande apparaît.
3. Dans le Registre, une page **de demande,** entrez les valeurs suivantes :
    1. Entrez **un** nom pour votre application.
    2. Choisissez les **types de compte pris en** charge, sélectionnez le type de compte unique ou multitenant.

        > [!NOTE]
        >
        > Les utilisateurs ne sont pas sollicités pour obtenir leur consentement et obtiennent immédiatement des jetons d’accès, si l’application AAD est enregistrée dans le même locataire lorsqu’ils font une demande d’authentification en Teams. Toutefois, les utilisateurs doivent donner leur consentement aux autorisations, si l’application AAD est enregistrée auprès d’un autre locataire.

    3. Choisissez **Inscrire**.
4. Sur la page d’aperçu, copiez et enregistrez **l’ID application (client).** Vous en avez besoin plus tard lors de la mise à jour Teams manifeste d’application.
5. Sélectionnez **Exposer une API** sous **Gérer**. 

   > [!IMPORTANT]
    > * Si vous construisez un bot autonome, entrez l’ID d’application URI comme `api://botid-{YourBotId}` . Ici **YourBotId est** votre identifiant d’application AAD.
    > * Si vous construisez une application avec un bot et un onglet, entrez l’ID d’application URI comme `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Sélectionnez les autorisations dont votre application a besoin pour le point de terminaison AAD et, en option, pour microsoft Graph.
6. [Accordez des autorisations](/azure/active-directory/develop/v2-permissions-and-consent) pour Teams applications de bureau, web et mobiles.
7. Sélectionnez **Ajouter une étendue**.
8. Dans le panneau qui s’ouvre, ajoutez une application client en entrant `access_as_user` comme **nom Scope**.

    >[!NOTE]
    > La portée « access_as_user » utilisée pour ajouter une application client s’œuvre pour les administrateurs et les utilisateurs.
    >
    > Vous devez être au courant des restrictions importantes suivantes :
    >
    > * Seules les autorisations Microsoft au niveau Graph’utilisateur et les autorisations api, telles que le courrier électronique, le profil, offline_access et OpenId, sont prises en charge. Si vous avez besoin d’accéder à d’autres Graph Microsoft, telles que `User.Read` ou , voir la solution de `Mail.Read` [contournement recommandée](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).
    > * Le nom de domaine de votre application doit être le même que le nom de domaine que vous avez enregistré pour votre application AAD.
    > * Plusieurs domaines par application ne sont actuellement pas pris en charge.
    > * Les applications qui utilisent le `azurewebsites.net` domaine ne sont pas prises en charge parce qu’elles sont courantes et peuvent être un risque pour la sécurité.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Mettre à jour le portail Azure avec la connexion OAuth

Complétez les étapes suivantes pour mettre à jour le portail Azure avec la connexion OAuth :

1. Dans le portail Azure, accédez aux **enregistrements d’applications**.

2. Aller à **autorisations API**. Sélectionnez **Ajouter une autorisation** Microsoft  >  **Graph**  >  **autorisations déléguées,** puis ajouter les autorisations suivantes de Microsoft Graph API :
    * User.Read (activé par défaut)
    * email
    * offline_access
    * OpenId (En)
    * profil

3. Dans le portail Azure, accédez à **l’enregistrement des canaux Bot**.

4. Sélectionnez **Paramètres** sur le volet gauche et choisissez **Ajouter le réglage** sous la section **OAuth Connection Paramètres.**

    ![Vue SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. Effectuez les étapes suivantes pour remplir le nouveau **formulaire de réglage de** connexion :

    >[!NOTE]
    > **Une subvention implicite** peut être exigée dans la demande de SAA.

    1. Entrez un **nom** dans la nouvelle page **de réglage de** connexion. C’est le nom qui est mentionné à l’intérieur des paramètres de votre code de service bot à *l’étape 5* [de Bot SSO à l’heure d’exécution](#bot-sso-at-runtime).
    2. À partir **du drop-down** du fournisseur de services, **sélectionnez Azure Active Directory v2**.
    3. Saisissez les informations d’identification du client, telles que **l’id client** et **le secret client** pour l’application AAD.
    4. Pour **l’URL Exchange jeton,** utilisez la valeur de portée définie dans Mise à [jour de votre Teams d’application pour votre bot](#update-your-teams-application-manifest-for-your-bot). L’URL Exchange jetons indique au SDK que cette application AAD est configurée pour SSO.
    5. Dans la boîte **d’identification** du locataire, entrez *commun*.
    6. Ajoutez toutes les **étendues configurées** lors de la spécifier des autorisations aux API en aval pour votre application AAD. Avec l’id client et le secret client fournis, le magasin de jetons échange le jeton contre un jeton graphique avec des autorisations définies.
    7. Sélectionnez **Enregistrer**.

    ![Vue de réglage VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Mettez à jour votre Teams d’application pour votre bot

Si l’application contient un bot autonome, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste d’application Teams’application :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Si l’application contient un bot et un onglet, utilisez le code suivant pour ajouter de nouvelles propriétés au manifeste d Teams’application :

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** est le parent des éléments suivants :

* **id** - L’identité client de l’application. Il s’agit de l’id de demande que vous avez obtenu dans le cadre de l’enregistrement de la demande auprès de l’AAD.
* **ressource** - Le domaine et la sous-main de votre application. Il s’agit du même URI, y compris le `api://` protocole que vous avez enregistré lors de la création de votre dans Enregistrer votre application via le `scope` portail [AAD](#register-your-app-through-the-aad-portal). Vous ne devez pas inclure `access_as_user` le chemin dans votre ressource. La partie domaine de cet URI doit correspondre au domaine et aux sous-domaines utilisés dans les URL de votre Teams d’application.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Ajouter le code à la demande et recevoir un jeton bot

#### <a name="request-a-bot-token"></a>Demander un jeton bot

La demande d’obtenir le jeton est une demande de message POST normale en utilisant le schéma de message existant. Il est inclus dans les pièces jointes d’une OAuthCard. Le schéma de la classe OAuthCard est défini dans [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) et il est similaire à une carte de connectement. Teams traite cette demande comme une acquisition de jeton silencieux si `TokenExchangeResource` la propriété est peuplée sur la carte. Pour le Teams, seule la `Id` propriété, qui identifie uniquement une demande symbolique, est honorée.

>[!NOTE]
> Le Microsoft Bot Framework ou `OAuthPrompt` le est pris en charge pour `MultiProviderAuthDialog` l’authentification SSO.

Si l’utilisateur utilise l’application pour la première fois et que le consentement de l’utilisateur est requis, la boîte de dialogue suivante semble se poursuivre avec l’expérience de consentement :

![Boîte de dialogue de consentement](../../../assets/images/bots/bots-consent-dialogbox.png)

Lorsque l’utilisateur sélectionne **Continuer**, ces événements se produisent :

* Si le bot définit un bouton de dédage, le flux de connectage pour les bots est déclenché de la même manière que le flux de signe à partir d’un bouton de carte OAuth dans un flux de messages. Le développeur doit décider des autorisations qui nécessitent le consentement de l’utilisateur. Cette approche est recommandée si vous avez besoin d’un jeton avec des autorisations au-delà `openId` . Par exemple, si vous souhaitez échanger le jeton contre des ressources graphiques.

* Si le bot ne fournit pas de bouton de dédage sur la carte OAuth, le consentement de l’utilisateur est requis pour un ensemble minimal d’autorisations. Ce jeton est utile pour l’authentification de base et pour obtenir l’adresse e-mail de l’utilisateur.

##### <a name="c-token-request-without-a-sign-in-button"></a>Demande de jeton C# sans bouton de déd connecte

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

#### <a name="receive-the-bot-token"></a>Recevez le jeton bot

La réponse avec le jeton est envoyée par une activité d’invocer avec le même schéma que d’autres invoquent les activités que les bots reçoivent aujourd’hui. La seule différence est le nom d’invocer, **le connectement/tokenExchange et** le **champ de** valeur. Le **champ** de valeur contient **l’Id**, une chaîne de la demande initiale pour obtenir le jeton et **le champ de jetons,** une valeur de chaîne incluant le jeton.

>[!NOTE]
> Vous pouvez recevoir plusieurs réponses pour une demande donnée si l’utilisateur a plusieurs paramètres actifs. Vous devez déduiser les réponses avec le jeton.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Code C# pour gérer l’activité invocant

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

`turnContext.activity.value`L’est de type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) et contient le jeton qui peut être utilisé par votre bot. Vous devez stocker les jetons pour des raisons de performances et les rafraîchir.

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

Pour comprendre ce que fait le bot lorsque l’échange de jetons ne déclenche pas une invite de consentement, voir les étapes suivantes :

>[!NOTE]
> Aucune action de l’utilisateur n’est nécessaire pour être prise car le bot prend les mesures lorsque l’échange de jetons échoue.

1. Le client commence une conversation avec le bot déclenchant un scénario OAuth.
2. Le bot renvoie une carte OAuth au client.
3. Le client intercepte la carte OAuth avant de l’afficher à l’utilisateur et vérifie si elle contient une `TokenExchangeResource` propriété.
4. Si la propriété existe, le client envoie `TokenExchangeInvokeRequest` un au bot. Le client doit avoir un jeton échangeable pour l’utilisateur, qui doit être un jeton Azure AD v2 et dont l’audience doit être la même que la `TokenExchangeResource.Uri` propriété. Le client envoie une activité d’invocer au bot avec le code suivant :

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

5. Le bot traite le `TokenExchangeInvokeRequest` et renvoie `TokenExchangeInvokeResponse` un dos au client. Le client doit attendre jusqu’à ce qu’il reçoive `TokenExchangeInvokeResponse` le .

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

6. Si le `TokenExchangeInvokeResponse` a un de , alors le client ne montre pas la carte `status` `200` OAuth. Voir [l’image de flux normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Pour tout autre `status` ou si le `TokenExchangeInvokeResponse` n’est pas reçu, alors le client montre la carte OAuth à l’utilisateur. Voir [l’image de flux de repli](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Cela garantit que le flux SSO retombe au flux normal d’OAuthCard en cas d’erreurs ou de dépendances non satisfaites comme le consentement de l’utilisateur.


### <a name="update-the-auth-sample"></a>Mettre à jour l’échantillon auth

Ouvrez [Teams échantillon auth,](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) puis terminez les étapes suivantes pour le mettre à jour :

1. Mettez à jour le TeamsBot pour gérer le dédupage de la demande entrante en incluant le code suivant :

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
  
2. Mise `appsettings.json` à jour pour inclure le , mot de `botId` passe, et le nom de connexion défini [dans Mettre à jour le portail Azure avec la connexion OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Mettez à jour le manifeste et `token.botframework.com` assurez-vous que c’est dans la liste des domaines valides. Pour plus d’informations, [Teams échantillon auth](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Zip le manifeste avec les images de profil et l’installer dans Teams.

## <a name="code-sample"></a>Exemple de code
|**Nom de l’échantillon** | **Description** |**.NET (en)** | 
|----------------|-----------------|--------------|
|Bot cadre SDK | Exemple pour l’utilisation du cadre de bot SDK. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
