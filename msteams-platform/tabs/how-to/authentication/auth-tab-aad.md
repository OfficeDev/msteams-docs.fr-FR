---
title: Authentification pour les onglets à l’aide d’Azure Active Directory
description: Décrit l’authentification dans teams et son utilisation dans des onglets
keywords: onglets d’authentification de teams AAD
ms.openlocfilehash: a1d3a96e23706012b643b5827701b49e2306d847
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237782"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="11e6f-104">Authentifier un utilisateur sous un onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="11e6f-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="11e6f-105">Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez la version 1.4.1 ou une version ultérieure du kit de développement logiciel (SDK) JavaScript Teams.</span><span class="sxs-lookup"><span data-stu-id="11e6f-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="11e6f-106">Il est possible que vous souhaitiez consommer de nombreux services au sein de votre application teams et que la plupart de ces services requièrent une authentification et une autorisation pour accéder au service.</span><span class="sxs-lookup"><span data-stu-id="11e6f-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="11e6f-107">Les services incluent Facebook, Twitter et des équipes de cours.</span><span class="sxs-lookup"><span data-stu-id="11e6f-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="11e6f-108">Les utilisateurs de teams ont des informations de profil utilisateur stockées dans Azure Active Directory (Azure AD) à l’aide de Microsoft Graph et cet article se concentre sur l’authentification à l’aide d’Azure AD pour accéder à ces informations.</span><span class="sxs-lookup"><span data-stu-id="11e6f-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="11e6f-109">OAuth 2,0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services.</span><span class="sxs-lookup"><span data-stu-id="11e6f-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="11e6f-110">La présentation de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans teams et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11e6f-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="11e6f-111">Les exemples ci-dessous utilisent le flux d’octroi implicite OAuth 2,0 avec l’objectif de lire les informations de profil de l’utilisateur à partir d’Azure AD et de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="11e6f-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="11e6f-112">Le code de cet article provient de l’exemple [d’authentification de l’exemple d’application Microsoft teams](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)de teams Teams (nœud).</span><span class="sxs-lookup"><span data-stu-id="11e6f-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="11e6f-113">Elle contient un onglet statique qui demande un jeton d’accès pour Microsoft Graph et affiche les informations de base du profil de l’utilisateur actuel à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11e6f-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="11e6f-114">Pour obtenir une vue d’ensemble du flux d’authentification pour les onglets, consultez la rubrique [flux d’authentification dans des onglets](~/tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="11e6f-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="11e6f-115">Le flux d’authentification dans les onglets diffère légèrement du flux d’authentification dans les robots.</span><span class="sxs-lookup"><span data-stu-id="11e6f-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="11e6f-116">Configuration des fournisseurs d’identité</span><span class="sxs-lookup"><span data-stu-id="11e6f-116">Configuring identity providers</span></span>

<span data-ttu-id="11e6f-117">Consultez la rubrique [configure Identity Providers](~/concepts/authentication/configure-identity-provider.md) pour obtenir des instructions détaillées sur la configuration des URL de redirection de rappel OAuth 2,0 lors de l’utilisation d’Azure Active Directory en tant que fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="11e6f-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="11e6f-118">Activer le flux d’authentification</span><span class="sxs-lookup"><span data-stu-id="11e6f-118">Initiate authentication flow</span></span>

<span data-ttu-id="11e6f-119">Le flux d’authentification doit être déclenché par une action de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="11e6f-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="11e6f-120">Vous ne devez pas ouvrir automatiquement la fenêtre contextuelle d’authentification, car cela déclenchera probablement le blocage des fenêtres publicitaires intempestives du navigateur, ainsi que la confusion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="11e6f-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="11e6f-121">Ajoutez un bouton à votre page de configuration ou de contenu pour permettre à l’utilisateur de se connecter lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="11e6f-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="11e6f-122">Cette opération peut être exécutée sur la page de [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) de l’onglet ou sur une page de [contenu](~/tabs/how-to/create-tab-pages/content-page.md) .</span><span class="sxs-lookup"><span data-stu-id="11e6f-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="11e6f-123">Azure AD, comme la plupart des fournisseurs d’identité, ne permet pas de placer son contenu dans un IFRAME.</span><span class="sxs-lookup"><span data-stu-id="11e6f-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="11e6f-124">Cela signifie que vous devrez ajouter une page contextuelle pour héberger le fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="11e6f-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="11e6f-125">Dans l’exemple suivant, cette page est `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="11e6f-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="11e6f-126">Utilisez la `microsoftTeams.authenticate()` fonction du kit de développement logiciel (SDK) client Microsoft teams pour lancer cette page lorsque votre bouton est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="11e6f-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

```javascript
microsoftTeams.authentication.authenticate({
    url: window.location.origin + "/tab-auth/simple-start",
    width: 600,
    height: 535,
    successCallback: function (result) {
        getUserProfile(result.accessToken);
    },
    failureCallback: function (reason) {
        handleAuthError(reason);
    }
});
```

### <a name="notes"></a><span data-ttu-id="11e6f-127">Notes</span><span class="sxs-lookup"><span data-stu-id="11e6f-127">Notes</span></span>

* <span data-ttu-id="11e6f-128">L’URL que vous transmettez `microsoftTeams.authentication.authenticate()` est la page de démarrage du flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="11e6f-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="11e6f-129">Dans cet exemple, il s’agit de `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="11e6f-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="11e6f-130">Cela doit correspondre à ce que vous avez enregistré dans le [portail d’inscription des applications Azure ad](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="11e6f-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="11e6f-131">Le flux d’authentification doit démarrer sur une page qui se trouve sur votre domaine.</span><span class="sxs-lookup"><span data-stu-id="11e6f-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="11e6f-132">Ce domaine doit également figurer dans la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section du manifeste.</span><span class="sxs-lookup"><span data-stu-id="11e6f-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="11e6f-133">Si ce n’est pas le cas, une fenêtre contextuelle vide est générée.</span><span class="sxs-lookup"><span data-stu-id="11e6f-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="11e6f-134">Ne pas utiliser `microsoftTeams.authentication.authenticate()` provoque un problème : la fenêtre contextuelle ne se ferme pas à la fin du processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="11e6f-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="11e6f-135">Accéder à la page d’autorisation à partir de votre page contextuelle</span><span class="sxs-lookup"><span data-stu-id="11e6f-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="11e6f-136">Lorsque votre page contextuelle ( `/tab-auth/simple-start` ) s’affiche, le code suivant est exécuté.</span><span class="sxs-lookup"><span data-stu-id="11e6f-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="11e6f-137">L’objectif principal de cette page est de rediriger vers votre fournisseur d’identité afin que l’utilisateur puisse se connecter.</span><span class="sxs-lookup"><span data-stu-id="11e6f-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="11e6f-138">Cette redirection a pu être réalisée côté serveur à l’aide du protocole HTTP 302, mais dans ce cas, elle est exécutée côté client en utilisant un appel à `window.location.assign()` .</span><span class="sxs-lookup"><span data-stu-id="11e6f-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="11e6f-139">Cela permet également de `microsoftTeams.getContext()` récupérer des informations d’indication qui peuvent être transmises à Azure ad.</span><span class="sxs-lookup"><span data-stu-id="11e6f-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "YOUR_APP_ID_HERE",
        response_type: "id_token token",
        response_mode: "fragment",
        resource: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="11e6f-140">Une fois que l’utilisateur a terminé l’autorisation, l’utilisateur est redirigé vers la page de rappel que vous avez spécifiée pour votre application sur `/tab-auth/simple-end` .</span><span class="sxs-lookup"><span data-stu-id="11e6f-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="11e6f-141">Notes</span><span class="sxs-lookup"><span data-stu-id="11e6f-141">Notes</span></span>

* <span data-ttu-id="11e6f-142">Voir [obtenir des informations de contexte utilisateur pour obtenir](~/tabs/how-to/access-teams-context.md) de l’aide sur la création des requêtes d’authentification et des URL.</span><span class="sxs-lookup"><span data-stu-id="11e6f-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="11e6f-143">Par exemple, vous pouvez utiliser le nom de connexion de l’utilisateur comme `login_hint` valeur pour la connexion à Azure ad, ce qui signifie que l’utilisateur peut avoir besoin de taper moins.</span><span class="sxs-lookup"><span data-stu-id="11e6f-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="11e6f-144">N’oubliez pas que vous ne devez pas utiliser ce contexte directement comme preuve d’identité, car un agresseur pourrait charger votre page dans un navigateur malveillant et lui fournir toutes les informations dont il a besoin.</span><span class="sxs-lookup"><span data-stu-id="11e6f-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="11e6f-145">Bien que le contexte d’onglet fournit des informations utiles sur l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur, que vous l’obteniez comme paramètres d’URL de votre URL de contenu de tabulation ou en appelant la `microsoftTeams.getContext()` fonction dans le kit de développement logiciel (SDK) du client Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="11e6f-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="11e6f-146">Un acteur malveillant peut appeler votre URL de contenu de tabulation avec ses propres paramètres, et une page Web qui emprunte l’identité de Microsoft teams pourrait charger votre URL de contenu d’onglet dans un IFRAME et renvoyer ses propres données à la `getContext()` fonction.</span><span class="sxs-lookup"><span data-stu-id="11e6f-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="11e6f-147">Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet simplement comme des conseils et les valider avant de les utiliser.</span><span class="sxs-lookup"><span data-stu-id="11e6f-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="11e6f-148">Le `state` paramètre est utilisé pour confirmer que le service qui appelle l’URI de rappel est le service que vous avez appelé.</span><span class="sxs-lookup"><span data-stu-id="11e6f-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="11e6f-149">Si le `state` paramètre dans le rappel ne correspond pas au paramètre que vous avez envoyé pendant l’appel, l’appel de retour n’est pas vérifié et doit être arrêté.</span><span class="sxs-lookup"><span data-stu-id="11e6f-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="11e6f-150">Il n’est pas nécessaire d’inclure le domaine du fournisseur d’identité dans la `validDomains` liste dans le fichier manifest.jsde l’application.</span><span class="sxs-lookup"><span data-stu-id="11e6f-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="11e6f-151">Page de rappel</span><span class="sxs-lookup"><span data-stu-id="11e6f-151">The callback page</span></span>

<span data-ttu-id="11e6f-152">Dans la dernière section, vous avez appelé le service d’autorisation Azure AD et transmis des informations sur l’utilisateur et l’application de sorte qu’Azure AD puisse présenter son propre mode d’autorisation monolithique à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="11e6f-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="11e6f-153">Votre application n’a pas de contrôle sur ce qui se passe dans cette expérience.</span><span class="sxs-lookup"><span data-stu-id="11e6f-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="11e6f-154">Il sait qu’il est renvoyé lorsque Azure AD appelle la page de rappel que vous avez fournie ( `/tab-auth/simple-end` ).</span><span class="sxs-lookup"><span data-stu-id="11e6f-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="11e6f-155">Dans cette page, vous devez déterminer la réussite ou l’échec en fonction des informations renvoyées par Azure AD, appeler `microsoftTeams.authentication.notifySuccess()` ou `microsoftTeams.authentication.notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="11e6f-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="11e6f-156">Si la connexion a été établie, vous aurez accès aux ressources de service.</span><span class="sxs-lookup"><span data-stu-id="11e6f-156">If the login was successful you will have access to service resources.</span></span>

````javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Azure AD
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        microsoftTeams.authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success: return token information to the tab
        microsoftTeams.authentication.notifySuccess({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        })
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    microsoftTeams.authentication.notifyFailure("UnexpectedFailure");
}
````

<span data-ttu-id="11e6f-157">Ce code analyse les paires clé-valeur reçues à partir d’Azure AD à `window.location.hash` l’aide de la `getHashParameters()` fonction d’assistance.</span><span class="sxs-lookup"><span data-stu-id="11e6f-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="11e6f-158">S’il trouve un `access_token` et que la `state` valeur est la même que celle fournie au début du flux d’authentification, il renvoie le jeton d’accès à l’onglet en appelant `notifySuccess()` ; sinon, il signale une erreur avec `notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="11e6f-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="11e6f-159">Notes</span><span class="sxs-lookup"><span data-stu-id="11e6f-159">Notes</span></span>

<span data-ttu-id="11e6f-160">`NotifyFailure()` a les causes d’échec prédéfinies suivantes :</span><span class="sxs-lookup"><span data-stu-id="11e6f-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="11e6f-161">`CancelledByUser` l’utilisateur a fermé la fenêtre contextuelle avant de terminer le flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="11e6f-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="11e6f-162">`FailedToOpenWindow` la fenêtre contextuelle n’a pas pu être ouverte.</span><span class="sxs-lookup"><span data-stu-id="11e6f-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="11e6f-163">Lorsque Microsoft teams est exécuté dans un navigateur, cela signifie généralement que la fenêtre a été bloquée par un bloqueur de fenêtres publicitaires intempestives.</span><span class="sxs-lookup"><span data-stu-id="11e6f-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="11e6f-164">Si elle réussit, vous pouvez actualiser ou recharger la page et afficher le contenu pertinent pour l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="11e6f-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="11e6f-165">Si l’authentification échoue, un message d’erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="11e6f-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="11e6f-166">Votre application peut définir son propre cookie de session de sorte que l’utilisateur ne doive pas se connecter à nouveau lorsqu’il revient à votre onglet sur le périphérique actuel.</span><span class="sxs-lookup"><span data-stu-id="11e6f-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="11e6f-167">Chrome 80, planifié pour la publication au début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookies par défaut.</span><span class="sxs-lookup"><span data-stu-id="11e6f-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="11e6f-168">Il est recommandé de définir l’utilisation prévue pour vos cookies au lieu de vous appuyer sur le comportement par défaut du navigateur.</span><span class="sxs-lookup"><span data-stu-id="11e6f-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="11e6f-169">*Voir* [SameSite cookie Attribute (mise à jour 2020)](../../../resources/samesite-cookie-update.md).</span><span class="sxs-lookup"><span data-stu-id="11e6f-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

>[!NOTE]
><span data-ttu-id="11e6f-170">Pour obtenir le jeton approprié pour les utilisateurs gratuits et invités de Microsoft Teams, il est important que les applications utilisent un point de terminaison spécifique au client https://login.microsoftonline.com/ **{tenantId}**.</span><span class="sxs-lookup"><span data-stu-id="11e6f-170">To get the correct token for Microsoft Teams Free and guest users, it is important that the apps use tenant specific endpoint https://login.microsoftonline.com/**{tenantId}**.</span></span> <span data-ttu-id="11e6f-171">Vous pouvez obtenir tenantId à partir du message bot ou du contexte de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="11e6f-171">You can get tenantId from the bot message or tab context.</span></span> <span data-ttu-id="11e6f-172">Si les applications utilisent https://login.microsoftonline.com/common , les utilisateurs obtiennent des jetons incorrects et se connectent au client « Home » au lieu du client auquel ils sont actuellement connectés.</span><span class="sxs-lookup"><span data-stu-id="11e6f-172">If the apps use https://login.microsoftonline.com/common, the users will get incorrect tokens and will log on to the "home" tenant instead of the tenant that they are currently signed into.</span></span>

<span data-ttu-id="11e6f-173">Pour plus d’informations sur l’authentification unique (SSO), consultez l’article [authentification sans assistance](~/tabs/how-to/authentication/auth-silent-AAD.md).</span><span class="sxs-lookup"><span data-stu-id="11e6f-173">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="11e6f-174">Exemples</span><span class="sxs-lookup"><span data-stu-id="11e6f-174">Samples</span></span>

<span data-ttu-id="11e6f-175">Pour obtenir un exemple de code illustrant le processus d’authentification par onglet à l’aide d’Azure AD, voir :</span><span class="sxs-lookup"><span data-stu-id="11e6f-175">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="11e6f-176">Exemple d’authentification de l’onglet Microsoft Teams (nœud)</span><span class="sxs-lookup"><span data-stu-id="11e6f-176">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
