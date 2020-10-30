---
title: Authentification en mode silencieux
description: Décrit l’authentification sans assistance
keywords: authentification unique sans assistance d’authentification de teams
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796364"
---
# <a name="silent-authentication"></a><span data-ttu-id="c83a2-104">Authentification en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="c83a2-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="c83a2-105">Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du kit de développement logiciel (SDK) JavaScript Teams.</span><span class="sxs-lookup"><span data-stu-id="c83a2-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="c83a2-106">L’authentification sans assistance dans Azure Active Directory (Azure AD) minimise le nombre de fois qu’un utilisateur doit entrer ses informations d’identification de connexion en actualisant silencieusement le jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="c83a2-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="c83a2-107">(Pour une prise en charge de la fonctionnalité d’authentification unique réelle, consultez notre [documentation SSO](~/tabs/how-to/authentication/auth-aad-sso.md))</span><span class="sxs-lookup"><span data-stu-id="c83a2-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="c83a2-108">Si vous souhaitez conserver votre code entièrement côté client, vous pouvez utiliser la [bibliothèque d’authentification Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) pour que JavaScript tente d’acquérir un jeton d’accès Azure AD en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="c83a2-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="c83a2-109">Cela signifie que l’utilisateur peut ne jamais voir une boîte de dialogue contextuelle s’il s’y est connecté récemment.</span><span class="sxs-lookup"><span data-stu-id="c83a2-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="c83a2-110">Même si la bibliothèque de ADAL.js est optimisée pour les applications AngularJS, elle fonctionne également avec des applications JavaScript pures uniques.</span><span class="sxs-lookup"><span data-stu-id="c83a2-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c83a2-111">Actuellement, l’authentification sans assistance fonctionne uniquement pour les onglets.</span><span class="sxs-lookup"><span data-stu-id="c83a2-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="c83a2-112">Il ne fonctionne pas encore lors de la connexion à partir d’un bot.</span><span class="sxs-lookup"><span data-stu-id="c83a2-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="c83a2-113">Fonctionnement de l’authentification sans assistance</span><span class="sxs-lookup"><span data-stu-id="c83a2-113">How silent authentication works</span></span>

<span data-ttu-id="c83a2-114">La bibliothèque ADAL.js crée un IFRAME masqué pour le flux d’octroi implicite OAuth 2,0, mais il indique `prompt=none` de sorte qu’Azure ad n’affiche jamais la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="c83a2-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="c83a2-115">Si l’intervention de l’utilisateur est requise parce que l’utilisateur doit se connecter ou accorder l’accès à l’application, Azure AD renvoie immédiatement une erreur qui ADAL.js ensuite des rapports à votre application.</span><span class="sxs-lookup"><span data-stu-id="c83a2-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="c83a2-116">À ce stade, votre application peut afficher un bouton de connexion si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c83a2-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="c83a2-117">Procédure d’authentification sans assistance</span><span class="sxs-lookup"><span data-stu-id="c83a2-117">How to do silent authentication</span></span>

<span data-ttu-id="c83a2-118">Le code de cet article provient de l’exemple [d’authentification Microsoft teams](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)de l’application Teams (nœud).</span><span class="sxs-lookup"><span data-stu-id="c83a2-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="c83a2-119">inclure et configurer ADAL</span><span class="sxs-lookup"><span data-stu-id="c83a2-119">include and configure ADAL</span></span>

<span data-ttu-id="c83a2-120">Incluez la bibliothèque ADAL.js dans vos pages d’onglets et configurez ADAL avec votre ID client et l’URL de redirection :</span><span class="sxs-lookup"><span data-stu-id="c83a2-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // ADAL.js configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a><span data-ttu-id="c83a2-121">Obtenir le contexte de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c83a2-121">Get the user context</span></span>

<span data-ttu-id="c83a2-122">Dans la page de contenu de l’onglet, appelez `microsoftTeams.getContext()` pour obtenir une indication de connexion pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="c83a2-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="c83a2-123">Il sera utilisé comme un login_hint dans l’appel à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c83a2-123">This will be used as a login_hint in the call to Azure AD.</span></span>

```javascript
// Set up extra query parameters for ADAL
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a><span data-ttu-id="c83a2-124">Authentifier</span><span class="sxs-lookup"><span data-stu-id="c83a2-124">Authenticate</span></span>

<span data-ttu-id="c83a2-125">Si ADAL a un jeton non expiré mis en cache pour l’utilisateur, utilisez-le.</span><span class="sxs-lookup"><span data-stu-id="c83a2-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="c83a2-126">Sinon, essayez d’obtenir un jeton en mode silencieux en appelant `acquireToken(resource, callback)` .</span><span class="sxs-lookup"><span data-stu-id="c83a2-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="c83a2-127">ADAL.js appelle votre fonction de rappel avec le jeton demandé, ou une erreur en cas d’échec de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="c83a2-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="c83a2-128">Si vous obtenez une erreur dans la fonction de rappel, affichez un bouton de connexion et basculez vers une connexion explicite.</span><span class="sxs-lookup"><span data-stu-id="c83a2-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

```javascript
let authContext = new AuthenticationContext(config); // from the ADAL.js library
// See if there's a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which ADAL.js returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure ADAL gave us an id token
        if (tokenType !== authContext.CONSTANTS.ID_TOKEN) {
            token = authContext.getCachedToken(config.clientId);
        }
        showProfileInformation(idToken);
    } else {
        console.log("Renewal failed: " + err);
        // Failed to get the token silently; show the login button
        showLoginButton();
        // You could attempt to launch the login popup here, but in browsers this could be blocked by
        // a popup blocker, in which case the login attempt will fail with the reason FailedToOpenWindow.
    }
});
```

### <a name="process-the-return-value"></a><span data-ttu-id="c83a2-129">Traiter la valeur de retour</span><span class="sxs-lookup"><span data-stu-id="c83a2-129">Process the return value</span></span>

<span data-ttu-id="c83a2-130">Laissez ADAL.js prendre soin d’analyser le résultat d’Azure AD en appelant `AuthenticationContext.handleWindowCallback(hash)` la page de rappel de connexion.</span><span class="sxs-lookup"><span data-stu-id="c83a2-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="c83a2-131">Vérifiez que nous disposons d’un utilisateur et d’un appel valides ou que vous `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` revenez à la page de contenu de votre onglet principal.</span><span class="sxs-lookup"><span data-stu-id="c83a2-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

```javascript
if (authContext.isCallback(window.location.hash)) {
    authContext.handleWindowCallback(window.location.hash);
    if (window.parent === window) {
        if (authContext.getCachedUser()) {
            microsoftTeams.authentication.notifySuccess();
        } else {
            microsoftTeams.authentication.notifyFailure(authContext.getLoginError());
        }
    }
}
```
