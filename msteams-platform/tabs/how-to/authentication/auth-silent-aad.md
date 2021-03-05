---
title: Authentification en mode silencieux
description: Décrit l’authentification silencieuse
ms.topic: conceptual
keywords: Authentification SSO Teams AAD silencieuse
ms.openlocfilehash: db8409cd4a6edface6d5dc3b3de6698852eaaa24
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449227"
---
# <a name="silent-authentication"></a><span data-ttu-id="8bb16-104">Authentification en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="8bb16-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="8bb16-105">Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, assurez-vous que vous utilisez au moins la version 1.4.1 du SDK JavaScript teams.</span><span class="sxs-lookup"><span data-stu-id="8bb16-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="8bb16-106">L’authentification silencieuse dans Azure Active Directory (AAD) réduit le nombre de fois qu’un utilisateur entre ses informations d’identification de connexion en actualisation silencieuse du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8bb16-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="8bb16-107">Pour obtenir une prise en charge de l' sign-on unique réelle, voir [la documentation de l’oD unique.](~/tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="8bb16-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="8bb16-108">Si vous souhaitez conserver votre code entièrement côté client, vous pouvez utiliser la bibliothèque d’authentification [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) pour JavaScript pour obtenir un jeton d’accès AAD en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="8bb16-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="8bb16-109">Si l’utilisateur s’est récemment inscrit, il ne voit jamais de boîte de dialogue de fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="8bb16-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="8bb16-110">Même si la bibliothèque ADAL.js est optimisée pour les applications AngularJS, elle fonctionne également avec des applications mono-page JavaScript pures.</span><span class="sxs-lookup"><span data-stu-id="8bb16-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="8bb16-111">Actuellement, l’authentification silencieuse fonctionne uniquement pour les onglets.</span><span class="sxs-lookup"><span data-stu-id="8bb16-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="8bb16-112">Elle ne fonctionne pas lors de la signature à partir d’un bot.</span><span class="sxs-lookup"><span data-stu-id="8bb16-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="8bb16-113">Fonctionnement de l’authentification silencieuse</span><span class="sxs-lookup"><span data-stu-id="8bb16-113">How silent authentication works</span></span>

<span data-ttu-id="8bb16-114">La ADAL.js crée un iframe masqué pour le flux d’octroi implicite OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8bb16-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="8bb16-115">Mais la bibliothèque spécifie , donc `prompt=none` Azure AD n’affiche jamais la page de signature.</span><span class="sxs-lookup"><span data-stu-id="8bb16-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="8bb16-116">Si l’interaction utilisateur est requise parce que l’utilisateur doit se connecter ou accorder l’accès à l’application, AAD renvoie immédiatement une erreur qui ADAL.js à votre application.</span><span class="sxs-lookup"><span data-stu-id="8bb16-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="8bb16-117">À ce stade, votre application peut afficher un bouton de signature si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8bb16-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="8bb16-118">Procédure d’authentification silencieuse</span><span class="sxs-lookup"><span data-stu-id="8bb16-118">How to do silent authentication</span></span>

<span data-ttu-id="8bb16-119">Le code de cet article provient de l’exemple d’application Teams qui est un nœud [d’exemple d’authentification Teams.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)</span><span class="sxs-lookup"><span data-stu-id="8bb16-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="8bb16-120">inclure et configurer ADAL</span><span class="sxs-lookup"><span data-stu-id="8bb16-120">include and configure ADAL</span></span>

<span data-ttu-id="8bb16-121">Incluez la ADAL.js dans vos pages d’onglets et configurez ADAL avec votre ID client et l’URL de redirection :</span><span class="sxs-lookup"><span data-stu-id="8bb16-121">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="8bb16-122">Obtenir le contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="8bb16-122">Get the user context</span></span>

<span data-ttu-id="8bb16-123">Dans la page de contenu de l’onglet, appelez pour obtenir un conseil de connect `microsoftTeams.getContext()` pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="8bb16-123">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="8bb16-124">Il est utilisé comme loginHint dans l’appel à AAD.</span><span class="sxs-lookup"><span data-stu-id="8bb16-124">This is used as a loginHint in the call to AAD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="8bb16-125">Authentifier</span><span class="sxs-lookup"><span data-stu-id="8bb16-125">Authenticate</span></span>

<span data-ttu-id="8bb16-126">Si ADAL a un jeton nonpiré mis en cache pour l’utilisateur, utilisez le jeton.</span><span class="sxs-lookup"><span data-stu-id="8bb16-126">If ADAL has an unexpired token cached for the user, use the token.</span></span> <span data-ttu-id="8bb16-127">Vous pouvez également essayer d’obtenir un jeton silencieusement en appelant `acquireToken(resource, callback)` .</span><span class="sxs-lookup"><span data-stu-id="8bb16-127">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="8bb16-128">ADAL.js appelle votre fonction de rappel avec le jeton demandé ou donne une erreur en cas d’échec de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8bb16-128">ADAL.js will call your callback function with the requested token, or give an error if authentication fails.</span></span>

<span data-ttu-id="8bb16-129">Si vous obtenez une erreur dans la fonction de rappel, affichez un bouton de signature et revenir à une signature explicite.</span><span class="sxs-lookup"><span data-stu-id="8bb16-129">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="8bb16-130">Traiter la valeur de retour</span><span class="sxs-lookup"><span data-stu-id="8bb16-130">Process the return value</span></span>

<span data-ttu-id="8bb16-131">ADAL.js le résultat d’AAD en appelant la page de rappel `AuthenticationContext.handleWindowCallback(hash)` de la signature.</span><span class="sxs-lookup"><span data-stu-id="8bb16-131">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="8bb16-132">Vérifiez que vous avez un utilisateur valide et que vous appelez ou pour signaler l’état à votre page de contenu `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` d’onglet principal.</span><span class="sxs-lookup"><span data-stu-id="8bb16-132">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

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
