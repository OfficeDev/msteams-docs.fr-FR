---
title: Utilisation du service Microsoft Azure bot pour l’authentification dans teams
description: Décrit le OAuthCard du service de robots Azure et son utilisation pour l’authentification
keywords: authentification teams OAuthCard service Azure bot de la carte OAuth
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673845"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="c90a5-104">Utilisation du service Microsoft Azure bot pour l’authentification dans teams</span><span class="sxs-lookup"><span data-stu-id="c90a5-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c90a5-105">Sans le OAuthCard du service Azure bot, il est compliqué d’implémenter l’authentification dans un bot.</span><span class="sxs-lookup"><span data-stu-id="c90a5-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="c90a5-106">Il s’agit d’un défi de pile complète qui implique la création d’une expérience Web, l’intégration avec des fournisseurs OAuth externes, la gestion des jetons et la gestion des appels d’API de serveur à serveur adéquats pour effectuer un flux d’authentification sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c90a5-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="c90a5-107">Cela peut entraîner des expériences dépendantes qui nécessitent l’entrée de « nombres magiques ».</span><span class="sxs-lookup"><span data-stu-id="c90a5-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="c90a5-108">Avec le OAuthCard du service Azure bot, il est plus facile pour votre robot de se connecter à vos utilisateurs et d’accéder aux fournisseurs de données externes.</span><span class="sxs-lookup"><span data-stu-id="c90a5-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="c90a5-109">Que vous ayez déjà implémenté l’authentification et que vous souhaitiez passer à un autre résultat plus simple ou si vous souhaitez ajouter une authentification à votre service bot pour la première fois, le OAuthCard peut faciliter la tâche.</span><span class="sxs-lookup"><span data-stu-id="c90a5-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="c90a5-110">Les autres rubriques de [l’authentification](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) décrivent l’authentification sans utiliser l’OAuthCard, donc si vous voulez comprendre l’authentification dans teams plus profondément ou si vous ne pouvez pas utiliser le OAuthCard, vous pouvez toujours consulter ces rubriques.</span><span class="sxs-lookup"><span data-stu-id="c90a5-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="c90a5-111">Prise en charge du OAuthCard</span><span class="sxs-lookup"><span data-stu-id="c90a5-111">Support for the OAuthCard</span></span>

<span data-ttu-id="c90a5-112">Il existe actuellement des restrictions quant à l’emplacement où vous pouvez utiliser le OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="c90a5-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="c90a5-113">Cela inclut ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="c90a5-113">These include:</span></span>

* <span data-ttu-id="c90a5-114">La carte ne fonctionne pas avec l' [accès invité](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="c90a5-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="c90a5-115">Il ne fonctionnera pas avec [Microsoft teams gratuitement](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="c90a5-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="c90a5-116">Il peut uniquement être utilisé pour l’authentification de robot.</span><span class="sxs-lookup"><span data-stu-id="c90a5-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="c90a5-117">Elle fonctionne uniquement pour les robots inscrits dans le [service Azure bot](https://azure.microsoft.com/services/bot-service/) .</span><span class="sxs-lookup"><span data-stu-id="c90a5-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="c90a5-118">Comment le service Azure bot m’aide-t-il à m’authentifier ?</span><span class="sxs-lookup"><span data-stu-id="c90a5-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="c90a5-119">Une documentation complète à l’aide de l’OAuthCard est disponible dans la rubrique : [Add Authentication to your bot by Azure bot service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="c90a5-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="c90a5-120">Notez que cette rubrique se trouve dans l’ensemble de la documentation de l’infrastructure Azure bot et n’est pas propre à Teams.</span><span class="sxs-lookup"><span data-stu-id="c90a5-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="c90a5-121">Les sections suivantes indiquent comment utiliser le OAuthCard dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c90a5-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="c90a5-122">Principaux avantages pour les développeurs de teams</span><span class="sxs-lookup"><span data-stu-id="c90a5-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="c90a5-123">L’OAuthCard aide à l’authentification des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="c90a5-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="c90a5-124">Fournit un flux d’authentification Web out-of-Box : vous n’avez plus à écrire et à héberger une page Web pour diriger vers des expériences de connexion externes ou fournir une redirection.</span><span class="sxs-lookup"><span data-stu-id="c90a5-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="c90a5-125">Est transparent pour les utilisateurs finals : effectuez l’expérience de connexion complète directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c90a5-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="c90a5-126">Inclut une gestion des jetons simplifiée : vous n’avez plus besoin d’implémenter un système de stockage des jetons : le service bot prend en charge la mise en cache des jetons et fournit un mécanisme sécurisé pour l’extraction de ces jetons.</span><span class="sxs-lookup"><span data-stu-id="c90a5-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="c90a5-127">Est pris en charge par les kits de développement logiciel complets : facile à intégrer et à consommer à partir de votre service bot.</span><span class="sxs-lookup"><span data-stu-id="c90a5-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="c90a5-128">Dispose de la prise en charge de nombreux fournisseurs OAuth populaires, comme Azure AD/MSA, Facebook et Google.</span><span class="sxs-lookup"><span data-stu-id="c90a5-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="c90a5-129">Quand dois-je implémenter ma propre solution ?</span><span class="sxs-lookup"><span data-stu-id="c90a5-129">When should I implement my own solution?</span></span>

<span data-ttu-id="c90a5-130">Étant donné que les jetons d’accès sont des informations sensibles, il est possible que vous ne souhaitiez pas les stocker dans un service externe.</span><span class="sxs-lookup"><span data-stu-id="c90a5-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="c90a5-131">Dans ce cas, vous pouvez toujours implémenter votre propre système de gestion des jetons et l’expérience de connexion dans Teams, comme décrit dans les autres rubriques relatives à l' [authentification](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="c90a5-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="c90a5-132">Prise en main de OAuthCard dans teams</span><span class="sxs-lookup"><span data-stu-id="c90a5-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="c90a5-133">Ce guide utilise le kit de développement logiciel (SDK) de robot v3.</span><span class="sxs-lookup"><span data-stu-id="c90a5-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="c90a5-134">Vous pouvez trouver l’implémentation v4 [ici](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp).</span><span class="sxs-lookup"><span data-stu-id="c90a5-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp).</span></span> <span data-ttu-id="c90a5-135">Vous devrez tout de même créer un manifeste et inclure token.botframework.com dans la `validDomains` section, car dans le cas contraire, le bouton de connexion n’ouvrira pas la fenêtre d’authentification.</span><span class="sxs-lookup"><span data-stu-id="c90a5-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="c90a5-136">Utilisez l' [application Studio](~/concepts/build-and-test/app-studio-overview.md) pour générer votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="c90a5-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="c90a5-137">Vous devez tout d’abord configurer votre service Azure bot pour configurer des fournisseurs d’authentification externes.</span><span class="sxs-lookup"><span data-stu-id="c90a5-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="c90a5-138">Pour plus d’informations, consultez la procédure de [Configuration des fournisseurs d’identité](~/concepts/authentication/configure-identity-provider.md) .</span><span class="sxs-lookup"><span data-stu-id="c90a5-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="c90a5-139">Pour activer l’authentification à l’aide du service Azure bot, vous devez effectuer ces ajouts à votre code :</span><span class="sxs-lookup"><span data-stu-id="c90a5-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="c90a5-140">Incluez token.botframework.com dans `validDomains` la section du manifeste de votre application car teams intégrera la page de connexion du service bot.</span><span class="sxs-lookup"><span data-stu-id="c90a5-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="c90a5-141">Récupérez le jeton du service bot chaque fois que votre bot a besoin d’accéder à des ressources authentifiées.</span><span class="sxs-lookup"><span data-stu-id="c90a5-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="c90a5-142">Si aucun jeton n’est disponible, envoyez un message avec un OAuthCard à l’utilisateur pour lui demander de se connecter au service externe.</span><span class="sxs-lookup"><span data-stu-id="c90a5-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="c90a5-143">Gérer l’activité de fin de connexion.</span><span class="sxs-lookup"><span data-stu-id="c90a5-143">Handle the login completion activity.</span></span> <span data-ttu-id="c90a5-144">Cela garantit que la demande d’authentification et le jeton sont associés à l’utilisateur qui interagit actuellement avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="c90a5-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="c90a5-145">Récupérez le jeton chaque fois que votre bot doit effectuer des actions authentifiées, telles que l’appel d’API REST externes.</span><span class="sxs-lookup"><span data-stu-id="c90a5-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="c90a5-146">Dans votre code de boîte de dialogue, vous devez ajouter cet extrait de code (C#), qui recherche un jeton d’accès existant :</span><span class="sxs-lookup"><span data-stu-id="c90a5-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

<span data-ttu-id="c90a5-147">S’il n’existe pas de jeton d’accès, votre code enverra un message avec un OAuthCard à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c90a5-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="c90a5-148">Pour gérer l’activité de connexion terminée, vous devez traiter cet appel :</span><span class="sxs-lookup"><span data-stu-id="c90a5-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="c90a5-149">Dans votre code de boîte de dialogue, vous pouvez ensuite récupérer le jeton à partir du service d’authentification du robot :</span><span class="sxs-lookup"><span data-stu-id="c90a5-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="c90a5-150">Utilisation de OAuthCard avec les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="c90a5-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="c90a5-151">Vous pouvez également utiliser le service de robot Azure pour connecter des fournisseurs tiers à votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c90a5-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="c90a5-152">Le flux est le même qu’avec un bot, sauf au lieu de renvoyer un OAuthCard, votre service renverra une invite de connexion.</span><span class="sxs-lookup"><span data-stu-id="c90a5-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="c90a5-153">L’extrait de code suivant (C#) illustre comment concevoir la réponse de connexion :</span><span class="sxs-lookup"><span data-stu-id="c90a5-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

<span data-ttu-id="c90a5-154">Notez que dans l’exemple ci-dessus, vous devez passer l' `GetSignInLinkAsync` appel directement par `client.OAuthApi` rapport à la propriété.</span><span class="sxs-lookup"><span data-stu-id="c90a5-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="c90a5-155">Lorsque l’utilisateur réussit la séquence de connexion, votre service reçoit une autre demande d’appel contenant la requête de l’utilisateur d’origine, ainsi qu’une chaîne de paramètres d’état contenant le « code magique ».</span><span class="sxs-lookup"><span data-stu-id="c90a5-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="c90a5-156">Vous pouvez maintenant extraire le jeton à l’aide de cette chaîne, ainsi que l’ID d’utilisateur et le nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="c90a5-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
