---
title: Authentification en mode silencieux
description: Décrit l’authentification silencieuse
ms.topic: conceptual
localization_priority: Normal
keywords: Authentification SSO Teams AAD silencieuse
ms.openlocfilehash: 0c75c6d50fd1191b6ea8548d65c9df4ce8453898
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019600"
---
# <a name="silent-authentication"></a><span data-ttu-id="24d2a-104">Authentification en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="24d2a-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="24d2a-105">Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, assurez-vous que vous utilisez au moins la version 1.4.1 du SDK JavaScript Teams.</span><span class="sxs-lookup"><span data-stu-id="24d2a-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="24d2a-106">L’authentification silencieuse dans Azure Active Directory (AAD) réduit le nombre de fois qu’un utilisateur entre ses informations d’identification de connexion en actualisation silencieuse du jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="24d2a-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="24d2a-107">Pour obtenir une véritable prise en charge de l' sign-on unique, voir [la documentation de l’oD unique.](~/tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="24d2a-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="24d2a-108">Si vous souhaitez conserver votre code entièrement côté client, vous pouvez utiliser la bibliothèque d’authentification [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) pour JavaScript pour obtenir un jeton d’accès AAD en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="24d2a-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="24d2a-109">Si l’utilisateur s’est récemment inscrit, il ne voit jamais de boîte de dialogue de fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="24d2a-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="24d2a-110">Même si la bibliothèque ADAL.js est optimisée pour les applications AngularJS, elle fonctionne également avec des applications mono-page JavaScript pures.</span><span class="sxs-lookup"><span data-stu-id="24d2a-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="24d2a-111">Actuellement, l’authentification silencieuse fonctionne uniquement pour les onglets.</span><span class="sxs-lookup"><span data-stu-id="24d2a-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="24d2a-112">Elle ne fonctionne pas lors de la signature à partir d’un bot.</span><span class="sxs-lookup"><span data-stu-id="24d2a-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="24d2a-113">Fonctionnement de l’authentification silencieuse</span><span class="sxs-lookup"><span data-stu-id="24d2a-113">How silent authentication works</span></span>

<span data-ttu-id="24d2a-114">La ADAL.js crée un iframe masqué pour le flux d’octroi implicite OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="24d2a-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="24d2a-115">Toutefois, la bibliothèque spécifie `prompt=none` , de sorte qu’Azure AD n’affiche jamais la page de se connecte.</span><span class="sxs-lookup"><span data-stu-id="24d2a-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="24d2a-116">Si l’interaction utilisateur est requise parce que l’utilisateur doit se connecter ou accorder l’accès à l’application, AAD renvoie immédiatement une erreur qui ADAL.js rapport à votre application.</span><span class="sxs-lookup"><span data-stu-id="24d2a-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="24d2a-117">À ce stade, votre application peut afficher un bouton de signature si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="24d2a-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="24d2a-118">Procédure d’authentification silencieuse</span><span class="sxs-lookup"><span data-stu-id="24d2a-118">How to do silent authentication</span></span>

<span data-ttu-id="24d2a-119">Le code de cet article provient de l’Teams exemple d’application qui est Teams [exemple d’authentification.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)</span><span class="sxs-lookup"><span data-stu-id="24d2a-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

<span data-ttu-id="24d2a-120">[Lancez l’onglet configurable d’authentification](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) simple et silencieuse à l’aide d’AAD et suivez les instructions pour exécuter l’exemple sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="24d2a-120">[Initiate silent and simple authentication configurable tab using AAD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) and follow the instructions to run the sample on your local machine.</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="24d2a-121">Inclure et configurer ADAL</span><span class="sxs-lookup"><span data-stu-id="24d2a-121">Include and configure ADAL</span></span>

<span data-ttu-id="24d2a-122">Incluez la ADAL.js dans vos pages d’onglets et configurez ADAL avec votre ID client et l’URL de redirection :</span><span class="sxs-lookup"><span data-stu-id="24d2a-122">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="24d2a-123">Obtenir le contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="24d2a-123">Get the user context</span></span>

<span data-ttu-id="24d2a-124">Dans la page de contenu de l’onglet, appelez pour obtenir un conseil de connect `microsoftTeams.getContext()` pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="24d2a-124">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="24d2a-125">Il est utilisé comme loginHint dans l’appel à AAD.</span><span class="sxs-lookup"><span data-stu-id="24d2a-125">This is used as a loginHint in the call to AAD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="24d2a-126">Authentifier</span><span class="sxs-lookup"><span data-stu-id="24d2a-126">Authenticate</span></span>

<span data-ttu-id="24d2a-127">Si ADAL a un jeton mis en cache pour l’utilisateur qui n’a pas expiré, utilisez ce jeton.</span><span class="sxs-lookup"><span data-stu-id="24d2a-127">If ADAL has a token cached for the user that has not expired, use that token.</span></span> <span data-ttu-id="24d2a-128">Vous pouvez également essayer d’obtenir un jeton silencieusement en appelant `acquireToken(resource, callback)` .</span><span class="sxs-lookup"><span data-stu-id="24d2a-128">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="24d2a-129">ADAL.js appelle la fonction de rappel avec le jeton demandé ou donne une erreur en cas d’échec de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="24d2a-129">ADAL.js calls the callback function with the requested token, or gives an error if authentication fails.</span></span>

<span data-ttu-id="24d2a-130">Si vous obtenez une erreur dans la fonction de rappel, affichez un bouton de signature et revenir à une signature explicite.</span><span class="sxs-lookup"><span data-stu-id="24d2a-130">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="24d2a-131">Traiter la valeur de retour</span><span class="sxs-lookup"><span data-stu-id="24d2a-131">Process the return value</span></span>

<span data-ttu-id="24d2a-132">ADAL.js le résultat d’AAD en appelant dans la page de rappel `AuthenticationContext.handleWindowCallback(hash)` de la signature.</span><span class="sxs-lookup"><span data-stu-id="24d2a-132">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="24d2a-133">Vérifiez que vous avez un utilisateur valide et que vous appelez ou pour signaler l’état à votre page de contenu `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` d’onglet principal.</span><span class="sxs-lookup"><span data-stu-id="24d2a-133">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

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

### <a name="handle-sign-out-flow"></a><span data-ttu-id="24d2a-134">Gérer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="24d2a-134">Handle sign out flow</span></span>

<span data-ttu-id="24d2a-135">Utilisez le code suivant pour gérer le flux de la signature dans l’th auth AAD :</span><span class="sxs-lookup"><span data-stu-id="24d2a-135">Use the following code to handle sign out flow in AAD Auth:</span></span>

> [!NOTE]
> <span data-ttu-id="24d2a-136">Pendant que la connexion Teams’onglet ou du bot est effectuée, la session en cours est également effacée.</span><span class="sxs-lookup"><span data-stu-id="24d2a-136">While logout for Teams tab or bot is done, the current session is also cleared.</span></span>

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
