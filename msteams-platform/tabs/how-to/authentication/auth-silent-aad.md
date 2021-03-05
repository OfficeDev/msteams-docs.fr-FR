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
# <a name="silent-authentication"></a>Authentification en mode silencieux

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, assurez-vous que vous utilisez au moins la version 1.4.1 du SDK JavaScript teams.

L’authentification silencieuse dans Azure Active Directory (AAD) réduit le nombre de fois qu’un utilisateur entre ses informations d’identification de connexion en actualisation silencieuse du jeton d’authentification. Pour obtenir une prise en charge de l' sign-on unique réelle, voir [la documentation de l’oD unique.](~/tabs/how-to/authentication/auth-aad-sso.md)

Si vous souhaitez conserver votre code entièrement côté client, vous pouvez utiliser la bibliothèque d’authentification [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) pour JavaScript pour obtenir un jeton d’accès AAD en mode silencieux. Si l’utilisateur s’est récemment inscrit, il ne voit jamais de boîte de dialogue de fenêtre pop-up.

Même si la bibliothèque ADAL.js est optimisée pour les applications AngularJS, elle fonctionne également avec des applications mono-page JavaScript pures.

> [!NOTE]
> Actuellement, l’authentification silencieuse fonctionne uniquement pour les onglets. Elle ne fonctionne pas lors de la signature à partir d’un bot.

## <a name="how-silent-authentication-works"></a>Fonctionnement de l’authentification silencieuse

La ADAL.js crée un iframe masqué pour le flux d’octroi implicite OAuth 2.0. Mais la bibliothèque spécifie , donc `prompt=none` Azure AD n’affiche jamais la page de signature. Si l’interaction utilisateur est requise parce que l’utilisateur doit se connecter ou accorder l’accès à l’application, AAD renvoie immédiatement une erreur qui ADAL.js à votre application. À ce stade, votre application peut afficher un bouton de signature si nécessaire.

## <a name="how-to-do-silent-authentication"></a>Procédure d’authentification silencieuse

Le code de cet article provient de l’exemple d’application Teams qui est un nœud [d’exemple d’authentification Teams.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)

### <a name="include-and-configure-adal"></a>inclure et configurer ADAL

Incluez la ADAL.js dans vos pages d’onglets et configurez ADAL avec votre ID client et l’URL de redirection :

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

### <a name="get-the-user-context"></a>Obtenir le contexte utilisateur

Dans la page de contenu de l’onglet, appelez pour obtenir un conseil de connect `microsoftTeams.getContext()` pour l’utilisateur actuel. Il est utilisé comme loginHint dans l’appel à AAD.

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

### <a name="authenticate"></a>Authentifier

Si ADAL a un jeton nonpiré mis en cache pour l’utilisateur, utilisez le jeton. Vous pouvez également essayer d’obtenir un jeton silencieusement en appelant `acquireToken(resource, callback)` . ADAL.js appelle votre fonction de rappel avec le jeton demandé ou donne une erreur en cas d’échec de l’authentification.

Si vous obtenez une erreur dans la fonction de rappel, affichez un bouton de signature et revenir à une signature explicite.

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

### <a name="process-the-return-value"></a>Traiter la valeur de retour

ADAL.js le résultat d’AAD en appelant la page de rappel `AuthenticationContext.handleWindowCallback(hash)` de la signature.

Vérifiez que vous avez un utilisateur valide et que vous appelez ou pour signaler l’état à votre page de contenu `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` d’onglet principal.

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
