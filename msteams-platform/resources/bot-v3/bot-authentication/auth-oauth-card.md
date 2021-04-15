---
title: Utilisation d'Azure Bot Service pour l'authentification dans Teams
description: Décrit OAuthCard azure Bot Service et son utilisation pour l'authentification
ms.topic: conceptual
keywords: Authentification teams OAuthCard OAuth carte Azure Bot Service
ms.openlocfilehash: 6e609daba1374f4e971e1634810d3b217ce55371
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696674"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="1142a-104">Utilisation d'Azure Bot Service pour l'authentification dans Teams</span><span class="sxs-lookup"><span data-stu-id="1142a-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1142a-105">Sans OAuthCard du service Azure Bot, il est compliqué d'implémenter l'authentification dans un bot.</span><span class="sxs-lookup"><span data-stu-id="1142a-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="1142a-106">Il s'agit d'un défi de pile complète qui implique la création d'une expérience web, l'intégration avec des fournisseurs OAuth externes, la gestion des jetons et la gestion des appels d'API de serveur à serveur pour terminer le flux d'authentification en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="1142a-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="1142a-107">Cela peut entraîner des expériences complexes nécessitant l'entrée de « nombres magiques ».</span><span class="sxs-lookup"><span data-stu-id="1142a-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="1142a-108">Avec OAuthCard d'Azure Bot Service, il est plus facile pour votre bot Teams de se connecter à vos utilisateurs et d'accéder à des fournisseurs de données externes.</span><span class="sxs-lookup"><span data-stu-id="1142a-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="1142a-109">Que vous avez déjà implémenté l'authentification et que vous souhaitez basculer vers quelque chose de plus simple, ou si vous cherchez à ajouter l'authentification à votre service de bot pour la première fois, OAuthCard peut faciliter la tâche.</span><span class="sxs-lookup"><span data-stu-id="1142a-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="1142a-110">D'autres [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) rubriques de l'authentification décrivent l'authentification sans utiliser OAuthCard. Ainsi, si vous souhaitez comprendre plus en détail l'authentification dans Teams ou que vous ne pouvez pas utiliser OAuthCard, vous pouvez toujours vous référer à ces rubriques.</span><span class="sxs-lookup"><span data-stu-id="1142a-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="1142a-111">Prise en charge d'OAuthCard</span><span class="sxs-lookup"><span data-stu-id="1142a-111">Support for the OAuthCard</span></span>

<span data-ttu-id="1142a-112">Il existe actuellement certaines restrictions quant à l'endroit où vous pouvez utiliser OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="1142a-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="1142a-113">Cela inclut ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="1142a-113">These include:</span></span>

* <span data-ttu-id="1142a-114">La carte ne fonctionne pas avec [l'accès invité](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="1142a-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="1142a-115">Il ne fonctionne pas [gratuitement avec Microsoft Teams](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="1142a-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="1142a-116">Il peut uniquement être utilisé pour l'authentification bot</span><span class="sxs-lookup"><span data-stu-id="1142a-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="1142a-117">Elle fonctionne uniquement pour les bots inscrits dans [le service Azure Bot](https://azure.microsoft.com/services/bot-service/)</span><span class="sxs-lookup"><span data-stu-id="1142a-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="1142a-118">Comment azure Bot Service m'aide-t-il à m'authentifier ?</span><span class="sxs-lookup"><span data-stu-id="1142a-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="1142a-119">La documentation complète utilisant OAuthCard est disponible dans la rubrique : Ajouter [l'authentification](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)à votre bot via Azure Bot Service .</span><span class="sxs-lookup"><span data-stu-id="1142a-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="1142a-120">Notez que cette rubrique se trouve dans l'ensemble de documentation Azure Bot Framework et n'est pas spécifique à Teams.</span><span class="sxs-lookup"><span data-stu-id="1142a-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="1142a-121">Les sections suivantes indiquent comment utiliser OAuthCard dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1142a-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="1142a-122">Principaux avantages pour les développeurs Teams</span><span class="sxs-lookup"><span data-stu-id="1142a-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="1142a-123">OAuthCard facilite l'authentification des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="1142a-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="1142a-124">Fournit un flux d'authentification web pré-fourni : vous n'avez plus besoin d'écrire et d'héberger une page web pour diriger les utilisateurs vers des expériences de connexion externes ou fournir une redirection.</span><span class="sxs-lookup"><span data-stu-id="1142a-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="1142a-125">Est transparent pour les utilisateurs finaux : terminez l'expérience de se connectez entièrement directement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1142a-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="1142a-126">Inclut une gestion simple des jetons : vous n'avez plus besoin d'implémenter un système de stockage de jetons . Au lieu de cela, le service bot s'occupe de la mise en cache des jetons et fournit un mécanisme sécurisé pour récupérer ces jetons.</span><span class="sxs-lookup"><span data-stu-id="1142a-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="1142a-127">Est pris en charge par des SDK complets : faciles à intégrer et à utiliser à partir de votre service de bot.</span><span class="sxs-lookup"><span data-stu-id="1142a-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="1142a-128">Offre une prise en charge préétent e pour de nombreux fournisseurs OAuth populaires, tels qu'Azure AD/MSA, Facebook et Google.</span><span class="sxs-lookup"><span data-stu-id="1142a-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="1142a-129">Quand dois-je implémenter ma propre solution ?</span><span class="sxs-lookup"><span data-stu-id="1142a-129">When should I implement my own solution?</span></span>

<span data-ttu-id="1142a-130">Étant donné que les jetons d'accès sont des informations sensibles, vous ne souhaitez peut-être pas les stocker dans un service externe.</span><span class="sxs-lookup"><span data-stu-id="1142a-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="1142a-131">Dans ce cas, vous pouvez choisir d'implémenter votre propre système de gestion des jetons et votre expérience de connexion dans Teams, comme décrit dans le reste des rubriques d'authentification [Teams.](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="1142a-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="1142a-132">Mise en place d'OAuthCard dans Teams</span><span class="sxs-lookup"><span data-stu-id="1142a-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="1142a-133">Ce guide utilise le SDK Bot Framework v3.</span><span class="sxs-lookup"><span data-stu-id="1142a-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="1142a-134">Vous trouverez l'implémentation v4 [ici.](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1142a-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span> <span data-ttu-id="1142a-135">Vous devrez toujours créer un manifeste et inclure des token.botframework.com dans la section, car sinon, le bouton Se connecter n'ouvrira pas `validDomains` la fenêtre d'authentification.</span><span class="sxs-lookup"><span data-stu-id="1142a-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="1142a-136">Utilisez [App Studio pour](~/concepts/build-and-test/app-studio-overview.md) générer votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="1142a-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="1142a-137">Vous devez d'abord configurer votre service de bot Azure pour configurer des fournisseurs d'authentification externes.</span><span class="sxs-lookup"><span data-stu-id="1142a-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="1142a-138">Lisez [Configuration des fournisseurs d'identité pour](~/concepts/authentication/configure-identity-provider.md) obtenir la procédure détaillée.</span><span class="sxs-lookup"><span data-stu-id="1142a-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="1142a-139">Pour activer l'authentification à l'aide d'Azure Bot Service, vous devez ajouter ces ajouts à votre code :</span><span class="sxs-lookup"><span data-stu-id="1142a-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="1142a-140">Incluez token.botframework.com dans la section du manifeste de votre application, car Teams incorpore la page de connexion `validDomains` du bot Service.</span><span class="sxs-lookup"><span data-stu-id="1142a-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="1142a-141">Récupérer le jeton à partir du service bot chaque fois que votre bot doit accéder aux ressources authentifiées.</span><span class="sxs-lookup"><span data-stu-id="1142a-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="1142a-142">Si aucun jeton n'est disponible, envoyez un message avec un OAuthCard à l'utilisateur lui demandant de se connecter au service externe.</span><span class="sxs-lookup"><span data-stu-id="1142a-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="1142a-143">Gérer l'activité d'achèvement de connexion.</span><span class="sxs-lookup"><span data-stu-id="1142a-143">Handle the login completion activity.</span></span> <span data-ttu-id="1142a-144">Cela garantit que la demande d'authentification et le jeton sont associés à l'utilisateur qui interagit actuellement avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="1142a-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="1142a-145">Récupérez le jeton chaque fois que votre bot doit effectuer des actions authentifiées, telles que l'appel d'API REST externes.</span><span class="sxs-lookup"><span data-stu-id="1142a-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="1142a-146">Dans votre code de boîte de dialogue, vous devez ajouter cet extrait de code (C#), qui recherche un jeton d'accès existant :</span><span class="sxs-lookup"><span data-stu-id="1142a-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

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

<span data-ttu-id="1142a-147">Si un jeton d'accès n'existe pas, votre code envoie ensuite un message avec OAuthCard à l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="1142a-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="1142a-148">Pour gérer l'activité de connexion terminée, vous devez traiter cet appel :</span><span class="sxs-lookup"><span data-stu-id="1142a-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

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

<span data-ttu-id="1142a-149">Dans votre code de boîte de dialogue, vous pouvez ensuite récupérer le jeton à partir du service d'authentification bot :</span><span class="sxs-lookup"><span data-stu-id="1142a-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

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

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="1142a-150">Utilisation d'OAuthCard avec des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="1142a-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="1142a-151">Vous pouvez également utiliser Azure Bot Service pour connecter des fournisseurs tiers à votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="1142a-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="1142a-152">Le flux est le même qu'avec un bot, sauf qu'au lieu de renvoyer un OAuthCard, votre service retournera une invite de connexion.</span><span class="sxs-lookup"><span data-stu-id="1142a-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="1142a-153">L'extrait de code suivant (C#) illustre comment créer la réponse de connexion :</span><span class="sxs-lookup"><span data-stu-id="1142a-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

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

<span data-ttu-id="1142a-154">Notez que dans l'exemple ci-dessus, vous devez effectuer l'appel `GetSignInLinkAsync` directement par rapport à la `client.OAuthApi` propriété.</span><span class="sxs-lookup"><span data-stu-id="1142a-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="1142a-155">Lorsque l'utilisateur termine correctement la séquence de connexion, votre service reçoit une autre demande Invoke contenant la requête utilisateur d'origine, ainsi qu'une chaîne de paramètre d'état contenant le « code magique ».</span><span class="sxs-lookup"><span data-stu-id="1142a-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="1142a-156">Vous pouvez maintenant récupérer le jeton à l'aide de cette chaîne, ainsi que l'ID d'utilisateur et le nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="1142a-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

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
