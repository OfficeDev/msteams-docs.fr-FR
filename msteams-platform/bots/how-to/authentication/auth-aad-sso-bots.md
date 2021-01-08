---
title: Support de l'identification unique pour les robots
description: Indique comment obtenir un jeton utilisateur. Actuellement, un développeur de robots peut utiliser une carte de connexion ou le service de robot Azure avec la prise en charge de la carte OAuth.
keywords: jeton, jeton d’utilisateur, prise en charge de l’authentification unique pour les robots
ms.openlocfilehash: ee9dbee063acf90f5596fc95d002caf53f88a08a
ms.sourcegitcommit: 0a9e91c65d88512eda895c21371b3cd4051dca0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2020
ms.locfileid: "49729071"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Prise en charge de l’authentification unique (SSO) pour les robots

L’authentification unique dans Azure Active Directory (Azure AD) minimise le nombre de fois que les utilisateurs doivent entrer leurs informations d’identification de connexion en actualisant silencieusement le jeton d’authentification. Si les utilisateurs s’engagent à utiliser votre application, ils ne doivent plus avoir à consentir sur un autre appareil et se connecteront automatiquement. Le flux est très similaire à la [prise en charge de l’authentification unique de l’onglet teams]( ../../../tabs/how-to/authentication/auth-aad-sso.md). La différence est le protocole qui permet à un bot de demander des jetons et de recevoir des réponses.

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans Teams.

## <a name="bot-sso-at-runtime"></a>SSO bot lors de l’exécution

![Autosso du robot au diagramme Runtime](../../../assets/images/bots/bots-sso-diagram.png)

1. Le bot envoie un message avec une OAuthCard qui contient la `tokenExchangeResource` propriété. Il indique à teams d’obtenir un jeton d’authentification pour l’application bot. L’utilisateur reçoit les messages à tous les points de terminaison actifs de l’utilisateur.

    > [!NOTE]
    >* Un utilisateur peut avoir plus d’un point de terminaison actif à la fois.  
    >* Le jeton bot est reçu à partir de chaque point de terminaison actif de l’utilisateur.
    >* La prise en charge de l’authentification unique requiert actuellement que l’application soit installée dans l’étendue personnelle.

2. Si c’est la première fois que l’utilisateur actuel a utilisé votre application bot, une invite de demande s’affichera (si un consentement est requis) ou pour gérer l’authentification par étape (par exemple, authentification à deux facteurs).

3. Microsoft teams demande le jeton de l’application bot à partir du point de terminaison Azure AD pour l’utilisateur actuel.

4. Azure AD envoie le jeton de l’application bot à l’application Teams.

5. Microsoft teams envoie le jeton au bot dans le cadre de l’objet value renvoyé par l’activité Invoke avec le nom se connecter/tokenExchange.
  
6. Le jeton sera analysé dans l’application bot pour extraire les informations nécessaires, telles que l’adresse de messagerie de l’utilisateur.
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a>Développer une authentification unique Microsoft teams bot
  
Les étapes suivantes sont nécessaires pour développer un robot Microsoft teams de Microsoft teams :

1. [Créer un compte Azure gratuit](#create-an-azure-account)
2. [Mettre à jour le manifeste d’application de teams](#update-your-app-manifest)
3. [Ajouter le code pour demander et recevoir le jeton bot](#request-a-bot-token)

### <a name="create-an-azure-account"></a>Créer un compte Azure

Cette étape est similaire au [flux d’authentification unique](../../../tabs/how-to/authentication/auth-aad-sso.md)de l’onglet :

1. Obtenir l' [ID de votre application Azure ad](/graph/concepts/auth-register-app-v2) pour Team Desktop, Web ou mobile client.
2. Spécifiez les autorisations dont votre application a besoin pour le point de terminaison Azure AD et, éventuellement, Microsoft Graph.
3. [Accorder des autorisations](/azure/active-directory/develop/v2-permissions-and-consent) pour les applications de bureau, Web et mobiles Teams.
4. Sélectionnez **Ajouter une étendue**.
5. Dans le panneau qui s’ouvre, ajoutez une application cliente en saisissant `access_as_user` comme **nom d’étendue**.

    >[!NOTE]
    > L’étendue « access_as_user » utilisée pour ajouter une application cliente est pour « administrateurs et utilisateurs ».

    > [!IMPORTANT]
    > * Si vous créez un bot autonome, définissez l’URI de l’ID d’application sur `api://botid-{YourBotId}` ici, **YourBotId** fait référence à votre ID d’application Azure ad.
    > * Si vous créez une application avec un bot et un onglet, définissez l’URI de l’ID d’application sur `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Ajoutez de nouvelles propriétés à votre manifeste Microsoft teams :

**WebApplicationInfo** -parent des éléments suivants :

> [!div class="checklist"]
>
> * **ID** : ID client de l’application. Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès d’Azure AD.
>* **ressource** -le domaine et le sous-domaine de votre application. Il s’agit du même URI (y compris le `api://` protocole) que vous avez enregistré lors de la création `scope` de votre étape ci-dessus. Vous ne devez pas inclure le `access_as_user` chemin d’accès dans votre ressource. La partie domaine de cet URI doit correspondre au domaine, y compris à tous les sous-domaines, utilisés dans les URL de votre manifeste d’application Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a>Demander un jeton de robot

La demande d’obtention du jeton est une demande POST message normale (à l’aide du schéma de message existant). Il est inclus dans les pièces jointes d’un OAuthCard. Le schéma de la classe OAuthCard est défini dans le [schéma Microsoft Bot 4,0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) et est très similaire à une carte de connexion. Teams traitera cette demande comme une acquisition en mode silencieux si la `TokenExchangeResource` propriété est renseignée sur la carte. Pour le canal Teams, nous n’honorons que la `Id` propriété, qui identifie de manière unique une demande de jeton.

>[!NOTE]
> L’infrastructure bot `OAuthPrompt` ou le `MultiProviderAuthDialog` est pris en charge pour l’authentification unique (SSO).

S’il s’agit de la première fois que l’utilisateur utilise votre application et que le consentement de l’utilisateur est requis, une boîte de dialogue s’affiche pour poursuivre l’expérience de consentement semblable à celle ci-dessous. Lorsque l’utilisateur sélectionne **Continuer**, deux choses différentes se produisent selon que le bot est défini ou non et qu’un bouton de connexion est présent sur le OAuthCard.

![Boîte de dialogue de consentement](../../../assets/images/bots/bots-consent-dialogbox.png)

Si le bot définit un bouton de connexion, le flux de connexion des robots se déclenchera de la même manière que le flux de connexion à partir d’un bouton de carte dans un flux de message. Il incombe au développeur de décider des autorisations à demander à l’utilisateur pour le consentement. Cette approche est recommandée si vous avez besoin d’un jeton avec des autorisations au-delà `openId` , par exemple, si vous souhaitez échanger le jeton pour les ressources Graph.

Si le bot ne fournit pas de bouton de connexion sur la carte, il déclenche le consentement de l’utilisateur pour un ensemble minimal d’autorisations. Ce jeton est utile pour l’authentification de base et l’obtention de l’adresse de messagerie de l’utilisateur.

**Demande de jeton C# sans bouton de connexion**:

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

#### <a name="receiving-the-token"></a>Réception du jeton

La réponse avec le jeton est envoyée par le biais d’une activité Invoke avec le même schéma que les autres utilisateurs appellent des activités que les robots reçoivent aujourd’hui. La seule différence est le nom d’appel, la **connexion/tokenExchange** et le champ de **valeur** qui contient l' **ID** (une chaîne) de la requête initiale pour obtenir le jeton et le champ de **jeton** (une valeur de chaîne incluant le jeton). Notez que vous pouvez recevoir plusieurs réponses pour une demande donnée si l’utilisateur dispose de plusieurs points de terminaison actifs. Il vous revient de dédupliquer les réponses avec le jeton.

**Code C# pour répondre à la gestion de l’activité d’appel**:

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

Le `turnContext.activity.value` est de type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) et contient le jeton qui peut être utilisé par votre bot. Stockez les jetons de manière sécurisée pour des raisons de performances et actualisez-les.

### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Mettre à jour le portail Azure avec la connexion OAuth

1. Dans le portail Azure, revenez à l' **inscription des canaux de robots**.

2. Basculez vers le panneau **paramètres** , puis choisissez **Ajouter un paramètre** sous la section paramètres de connexion OAuth.

    ![Vue SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. Complétez le formulaire de **paramètre de connexion** :

    > [!div class="checklist"]
    >
    > * Entrez un nom pour votre nouveau paramètre de connexion. Il s’agit du nom qui est référencé à l’intérieur des paramètres de votre code de service bot à l' **étape 5**.
    > * Dans la liste déroulante fournisseur de services, sélectionnez **Azure Active Directory v2**.
    >* Entrez les informations d’identification du client pour l’application AAD.

    >[!NOTE]
    > Une **subvention implicite** peut être requise dans l’application AAD.

    >* Pour l’URL d’échange de jetons, utilisez la valeur de portée définie à l’étape précédente de votre application AAD. La présence de l’URL d’échange de jetons indique au SDK que cette application AAD est configurée pour l’authentification unique.
    >* Spécifiez « Common » comme **ID de client**.
    >* Ajoutez toutes les étendues configurées lors de la spécification des autorisations pour les API en aval de votre application AAD. Avec l’ID client et la clé secrète client fournis, le magasin de jetons échangera le jeton pour un jeton de graphique avec des autorisations définies pour vous.
    >* Cliquez sur **Enregistrer**.

    ![Vue de paramètre VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a>Mettre à jour l’exemple d’authentification

Commencez par l' [exemple d’authentification teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).

1. Mettez à jour l’TeamsBot pour inclure les éléments suivants. Pour gérer le deduping de la demande entrante, voir ci-dessous :

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
  
2. Mettez à jour le `appsettings.json` pour inclure le `botId` , le mot de passe et le nom de connexion définis ci-dessus.
3. Mettez à jour le manifeste et assurez-vous qu' `token.botframework.com` il se trouve dans la section domaines valides.
4. Compressez le manifeste avec les images de profil et installez-le dans Teams.

#### <a name="additional-code-samples"></a>Exemples de code supplémentaires

* [Exemple C# utilisant le kit de développement logiciel (SDK) de robot Framework](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).

* [Exemple C# utilisant le kit de développement logiciel (SDK) de l’infrastructure bot pour dédupliquer la demande de jeton](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).

* [Exemple C# sans utiliser le magasin de jetons du kit de développement logiciel de robot Framework](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw).
