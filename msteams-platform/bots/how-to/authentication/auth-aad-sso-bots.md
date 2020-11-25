---
title: Support de l'identification unique pour les robots
description: Indique comment obtenir un jeton utilisateur. Actuellement, un développeur de robots peut utiliser une carte de connexion ou le service de robot Azure avec la prise en charge de la carte OAuth.
keywords: jeton, jeton d’utilisateur, prise en charge de l’authentification unique pour les robots
ms.openlocfilehash: f2f04cefdea874c42961404339f54b8eb581c7ee
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409098"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="ac451-105">Prise en charge de l’authentification unique (SSO) pour les robots</span><span class="sxs-lookup"><span data-stu-id="ac451-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="ac451-106">L’authentification unique dans Azure Active Directory (Azure AD) minimise le nombre de fois que les utilisateurs doivent entrer leurs informations d’identification de connexion en actualisant silencieusement le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="ac451-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="ac451-107">Si les utilisateurs s’engagent à utiliser votre application, ils n’ont pas besoin de consentir à nouveau sur un autre appareil et seront connectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ac451-107">If users agrees to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="ac451-108">Le flux est très similaire à la [prise en charge de l’authentification unique de l’onglet teams]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="ac451-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="ac451-109">La différence est le protocole qui permet à un bot de demander des jetons et de recevoir des réponses.</span><span class="sxs-lookup"><span data-stu-id="ac451-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="ac451-110">OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="ac451-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="ac451-111">Une compréhension de base de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ac451-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="ac451-112">SSO bot lors de l’exécution</span><span class="sxs-lookup"><span data-stu-id="ac451-112">Bot SSO at runtime</span></span>

![Autosso du robot au diagramme Runtime](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="ac451-114">Le bot envoie un message avec une OAuthCard qui contient la `tokenExchangeResource` propriété.</span><span class="sxs-lookup"><span data-stu-id="ac451-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="ac451-115">Il indique à teams d’obtenir un jeton d’authentification pour l’application bot.</span><span class="sxs-lookup"><span data-stu-id="ac451-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="ac451-116">L’utilisateur reçoit les messages à tous les points de terminaison actifs de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac451-116">The user receives messages at all the active endpoints of the user.</span></span>

> [!NOTE]
>* <span data-ttu-id="ac451-117">Un utilisateur peut avoir plus d’un point de terminaison actif à la fois.</span><span class="sxs-lookup"><span data-stu-id="ac451-117">A user can have more than one active endpoint at a time.</span></span>  
>* <span data-ttu-id="ac451-118">Le jeton bot est reçu à partir de chaque point de terminaison actif de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac451-118">The bot token is received from every active endpoint of the user.</span></span>
>* <span data-ttu-id="ac451-119">La prise en charge de l’authentification unique requiert actuellement que l’application soit installée dans l’étendue personnelle.</span><span class="sxs-lookup"><span data-stu-id="ac451-119">Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="ac451-120">Si c’est la première fois que l’utilisateur actuel a utilisé votre application bot, une invite de demande s’affichera (si un consentement est requis) ou pour gérer l’authentification par étape (par exemple, authentification à deux facteurs).</span><span class="sxs-lookup"><span data-stu-id="ac451-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="ac451-121">Microsoft teams demande le jeton de l’application bot à partir du point de terminaison Azure AD pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="ac451-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="ac451-122">Azure AD envoie le jeton de l’application bot à l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="ac451-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="ac451-123">Microsoft teams envoie le jeton au bot dans le cadre de l’objet value renvoyé par l’activité Invoke avec le nom se connecter/tokenExchange.</span><span class="sxs-lookup"><span data-stu-id="ac451-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="ac451-124">Le jeton sera analysé dans l’application bot pour extraire les informations nécessaires, telles que l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac451-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="ac451-125">Développer une authentification unique Microsoft teams bot</span><span class="sxs-lookup"><span data-stu-id="ac451-125">Develop a Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="ac451-126">Les étapes suivantes : sont nécessaires pour développer un robot Microsoft teams de Microsoft teams :</span><span class="sxs-lookup"><span data-stu-id="ac451-126">The following steps: are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="ac451-127">Créer un compte Azure gratuit</span><span class="sxs-lookup"><span data-stu-id="ac451-127">Create an Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="ac451-128">Mettre à jour le manifeste d’application de teams</span><span class="sxs-lookup"><span data-stu-id="ac451-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="ac451-129">Ajouter le code pour demander et recevoir le jeton bot</span><span class="sxs-lookup"><span data-stu-id="ac451-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="ac451-130">Créer un compte Azure</span><span class="sxs-lookup"><span data-stu-id="ac451-130">Create an Azure account</span></span>

<span data-ttu-id="ac451-131">Cette étape est similaire au [flux d’authentification unique](../../../tabs/how-to/authentication/auth-aad-sso.md)de l’onglet :</span><span class="sxs-lookup"><span data-stu-id="ac451-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md):</span></span>

1. <span data-ttu-id="ac451-132">Obtenir l' [ID de votre application Azure ad](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) pour Team Desktop, Web ou mobile client.</span><span class="sxs-lookup"><span data-stu-id="ac451-132">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) for Teams desktop, web, or mobile client.</span></span>
2. <span data-ttu-id="ac451-133">Spécifiez les autorisations dont votre application a besoin pour le point de terminaison Azure AD et, éventuellement, Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ac451-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="ac451-134">[Accorder des autorisations](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) pour les applications de bureau, Web et mobiles Teams.</span><span class="sxs-lookup"><span data-stu-id="ac451-134">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="ac451-135">Ajoutez une application cliente en sélectionnant le bouton **Ajouter une étendue** et dans le volet qui s’ouvre, entrez `access_as_user` comme **nom d’étendue**.</span><span class="sxs-lookup"><span data-stu-id="ac451-135">Add a client app by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

>[!NOTE]
> <span data-ttu-id="ac451-136">L’étendue « access_as_user » utilisée pour ajouter une application cliente est pour « administrateurs et utilisateurs ».</span><span class="sxs-lookup"><span data-stu-id="ac451-136">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="ac451-137">Si vous créez un bot autonome, définissez l’URI de l’ID d’application sur `api://botid-{YourBotId}` ici, **YourBotId** fait référence à votre ID d’application Azure ad.</span><span class="sxs-lookup"><span data-stu-id="ac451-137">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` Here, **YourBotId** refers to your Azure AD application ID.</span></span>
> * <span data-ttu-id="ac451-138">Si vous créez une application avec un bot et un onglet, définissez l’URI de l’ID d’application sur `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="ac451-138">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="ac451-139">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="ac451-139">Update your app manifest</span></span>

<span data-ttu-id="ac451-140">Ajoutez de nouvelles propriétés à votre manifeste Microsoft teams :</span><span class="sxs-lookup"><span data-stu-id="ac451-140">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="ac451-141">**WebApplicationInfo** -parent des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ac451-141">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ac451-142">**ID** : ID client de l’application.</span><span class="sxs-lookup"><span data-stu-id="ac451-142">**id** - The client ID of the application.</span></span> <span data-ttu-id="ac451-143">Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac451-143">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="ac451-144">**ressource** -le domaine et le sous-domaine de votre application.</span><span class="sxs-lookup"><span data-stu-id="ac451-144">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="ac451-145">Il s’agit du même URI (y compris le `api://` protocole) que vous avez enregistré lors de la création `scope` de votre étape ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ac451-145">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="ac451-146">Vous ne devez pas inclure le `access_as_user` chemin d’accès dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="ac451-146">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="ac451-147">La partie domaine de cet URI doit correspondre au domaine, y compris à tous les sous-domaines, utilisés dans les URL de votre manifeste d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="ac451-147">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="ac451-148">Demander un jeton de robot</span><span class="sxs-lookup"><span data-stu-id="ac451-148">Request a bot token</span></span>

<span data-ttu-id="ac451-149">La demande d’obtention du jeton est une demande POST message normale (à l’aide du schéma de message existant).</span><span class="sxs-lookup"><span data-stu-id="ac451-149">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="ac451-150">Il est inclus dans les pièces jointes d’un OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="ac451-150">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="ac451-151">Le schéma de la classe OAuthCard est défini dans le [schéma Microsoft Bot 4,0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) et est très similaire à une carte de connexion.</span><span class="sxs-lookup"><span data-stu-id="ac451-151">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="ac451-152">Teams traitera cette demande comme une acquisition en mode silencieux si la `TokenExchangeResource` propriété est renseignée sur la carte.</span><span class="sxs-lookup"><span data-stu-id="ac451-152">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="ac451-153">Pour le canal Teams, nous honorons uniquement la `Id` propriété, qui identifie de manière unique une demande de jeton.</span><span class="sxs-lookup"><span data-stu-id="ac451-153">For the Teams channel we honor only the `Id` property, which uniquely identifies a token request.</span></span>

>[!NOTE]
> <span data-ttu-id="ac451-154">L’infrastructure bot `OAuthPrompt` ou le `MultiProviderAuthDialog` est pris en charge pour l’authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="ac451-154">The Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for single sign-on (SSO) authentication.</span></span>

<span data-ttu-id="ac451-155">S’il s’agit de la première fois que l’utilisateur utilise votre application et que le consentement de l’utilisateur est requis, une boîte de dialogue s’affiche pour poursuivre l’expérience de consentement semblable à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ac451-155">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="ac451-156">Lorsque l’utilisateur sélectionne **Continuer**, deux choses différentes se produisent selon que le bot est défini ou non et qu’un bouton de connexion est présent sur le OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="ac451-156">When the user selects **Continue**, two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

![Boîte de dialogue de consentement](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="ac451-158">Si le bot définit un bouton de connexion, le flux de connexion des robots se déclenchera de la même manière que le flux de connexion à partir d’un bouton de carte dans un flux de message.</span><span class="sxs-lookup"><span data-stu-id="ac451-158">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="ac451-159">Il incombe au développeur de décider des autorisations à demander à l’utilisateur pour le consentement.</span><span class="sxs-lookup"><span data-stu-id="ac451-159">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="ac451-160">Cette approche est recommandée si vous avez besoin d’un jeton avec des autorisations au-delà `openId` , par exemple, si vous souhaitez échanger le jeton pour les ressources Graph.</span><span class="sxs-lookup"><span data-stu-id="ac451-160">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="ac451-161">Si le bot ne fournit pas de bouton de connexion sur la carte, il déclenche le consentement de l’utilisateur pour un ensemble minimal d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="ac451-161">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="ac451-162">Ce jeton est utile pour l’authentification de base et l’obtention de l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac451-162">This token is useful for basic authentication and getting the user email address.</span></span>

<span data-ttu-id="ac451-163">**Demande de jeton C# sans bouton de connexion**:</span><span class="sxs-lookup"><span data-stu-id="ac451-163">**C# token request without a sign-in button**:</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="ac451-164">Réception du jeton</span><span class="sxs-lookup"><span data-stu-id="ac451-164">Receiving the token</span></span>

<span data-ttu-id="ac451-165">La réponse avec le jeton est envoyée par le biais d’une activité Invoke avec le même schéma que les autres utilisateurs appellent des activités que les robots reçoivent aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="ac451-165">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="ac451-166">La seule différence est le nom d’appel, la **connexion/tokenExchange** et le champ de **valeur** qui contient l' **ID** (une chaîne) de la requête initiale pour obtenir le jeton et le champ de **jeton** (une valeur de chaîne incluant le jeton).</span><span class="sxs-lookup"><span data-stu-id="ac451-166">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="ac451-167">Notez que vous pouvez recevoir plusieurs réponses pour une demande donnée si l’utilisateur dispose de plusieurs points de terminaison actifs.</span><span class="sxs-lookup"><span data-stu-id="ac451-167">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="ac451-168">Il vous revient de dédupliquer les réponses avec le jeton.</span><span class="sxs-lookup"><span data-stu-id="ac451-168">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="ac451-169">**Code C# pour répondre à la gestion de l’activité d’appel**:</span><span class="sxs-lookup"><span data-stu-id="ac451-169">**C# code to respond to handle the invoke activity**:</span></span>

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

<span data-ttu-id="ac451-170">Le `turnContext.activity.value` est de type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) et contient le jeton qui peut être utilisé par votre bot.</span><span class="sxs-lookup"><span data-stu-id="ac451-170">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="ac451-171">Stockez les jetons de manière sécurisée pour des raisons de performances et actualisez-les.</span><span class="sxs-lookup"><span data-stu-id="ac451-171">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="ac451-172">Mettre à jour le portail Azure avec la connexion OAuth</span><span class="sxs-lookup"><span data-stu-id="ac451-172">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="ac451-173">Dans le portail Azure, revenez à l' **inscription des canaux de robots**.</span><span class="sxs-lookup"><span data-stu-id="ac451-173">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="ac451-174">Basculez vers le panneau **paramètres** , puis choisissez **Ajouter un paramètre** sous la section paramètres de connexion OAuth.</span><span class="sxs-lookup"><span data-stu-id="ac451-174">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

![Vue SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="ac451-176">Complétez le formulaire de **paramètre de connexion** :</span><span class="sxs-lookup"><span data-stu-id="ac451-176">Complete the **Connection Setting** form:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ac451-177">Entrez un nom pour votre nouveau paramètre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ac451-177">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="ac451-178">Il s’agit du nom qui est référencé à l’intérieur des paramètres de votre code de service bot à l' **étape 5**.</span><span class="sxs-lookup"><span data-stu-id="ac451-178">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
> * <span data-ttu-id="ac451-179">Dans la liste déroulante fournisseur de services, sélectionnez **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="ac451-179">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
>* <span data-ttu-id="ac451-180">Entrez les informations d’identification du client pour l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="ac451-180">Enter the client credentials for the AAD application.</span></span>

>[!NOTE]
> <span data-ttu-id="ac451-181">Une **subvention implicite** peut être requise dans l’application AAD.</span><span class="sxs-lookup"><span data-stu-id="ac451-181">**Implicit grant** may be required in the AAD application.</span></span>

>* <span data-ttu-id="ac451-182">Pour l’URL d’échange de jetons, utilisez la valeur de portée définie à l’étape précédente de votre application AAD.</span><span class="sxs-lookup"><span data-stu-id="ac451-182">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="ac451-183">La présence de l’URL d’échange de jetons indique au SDK que cette application AAD est configurée pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ac451-183">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
>* <span data-ttu-id="ac451-184">Spécifiez « Common » comme **ID de client**.</span><span class="sxs-lookup"><span data-stu-id="ac451-184">Specify "common" as the **Tenant ID**.</span></span>
>* <span data-ttu-id="ac451-185">Ajoutez toutes les étendues configurées lors de la spécification des autorisations pour les API en aval de votre application AAD.</span><span class="sxs-lookup"><span data-stu-id="ac451-185">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="ac451-186">Avec l’ID client et la clé secrète client fournis, le magasin de jetons échangera le jeton pour un jeton de graphique avec des autorisations définies pour vous.</span><span class="sxs-lookup"><span data-stu-id="ac451-186">With the client id and client secret provided, token store will exchange the token for a graph token with defined permissions for you.</span></span>
>* <span data-ttu-id="ac451-187">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ac451-187">Select **Save**.</span></span>

![Vue de paramètre VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="ac451-189">Mettre à jour l’exemple d’authentification</span><span class="sxs-lookup"><span data-stu-id="ac451-189">Update the auth sample</span></span>

<span data-ttu-id="ac451-190">Commencez par l' [exemple d’authentification teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="ac451-190">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="ac451-191">Mettez à jour l’TeamsBot pour inclure les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="ac451-191">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="ac451-192">Pour gérer le deduping de la demande entrante, voir ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ac451-192">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="ac451-193">Mettez à jour le `appsettings.json` pour inclure le `botId` , le mot de passe et le nom de connexion définis ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ac451-193">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="ac451-194">Mettez à jour le manifeste et assurez-vous qu' `token.botframework.com` il se trouve dans la section domaines valides.</span><span class="sxs-lookup"><span data-stu-id="ac451-194">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="ac451-195">Compressez le manifeste avec les images de profil et installez-le dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ac451-195">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="ac451-196">Exemples de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ac451-196">Additional code samples</span></span>

* <span data-ttu-id="ac451-197">[Exemple C# utilisant le kit de développement logiciel (SDK) de robot Framework](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span><span class="sxs-lookup"><span data-stu-id="ac451-197">[C# sample using the Bot Framework SDK](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span></span>

* <span data-ttu-id="ac451-198">[Exemple C# utilisant le kit de développement logiciel (SDK) de l’infrastructure bot pour dédupliquer la demande de jeton](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span><span class="sxs-lookup"><span data-stu-id="ac451-198">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* [<span data-ttu-id="ac451-199">Exemple C# sans utiliser le magasin de jetons du kit de développement logiciel de robot Framework</span><span class="sxs-lookup"><span data-stu-id="ac451-199">C# sample without using the Bot Framework SDK token store</span></span>](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
