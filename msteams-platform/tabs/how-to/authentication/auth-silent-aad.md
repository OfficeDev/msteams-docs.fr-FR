---
title: Authentification en mode silencieux
description: Décrit l’authentification sans assistance
keywords: authentification unique sans assistance d’authentification de teams
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673552"
---
# <a name="silent-authentication"></a>Authentification en mode silencieux

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du kit de développement logiciel (SDK) JavaScript Teams.

L’authentification sans assistance dans Azure Active Directory (Azure AD) minimise le nombre de fois qu’un utilisateur doit entrer ses informations d’identification de connexion en actualisant silencieusement le jeton d’authentification. (Pour une prise en charge de la fonctionnalité d’authentification unique réelle, consultez notre [documentation SSO](~/tabs/how-to/authentication/auth-aad-sso.md))

Si vous souhaitez conserver votre code entièrement côté client, vous pouvez utiliser la [bibliothèque d’authentification Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) pour que JavaScript tente d’acquérir un jeton d’accès Azure AD en mode silencieux. Cela signifie que l’utilisateur peut ne jamais voir une boîte de dialogue contextuelle s’il s’y est connecté récemment.

Même si la bibliothèque ADAL. js est optimisée pour les applications AngularJS, elle fonctionne également avec des applications JavaScript pures uniques.

> [!NOTE]
> Actuellement, l’authentification sans assistance fonctionne uniquement pour les onglets. Il ne fonctionne pas encore lors de la connexion à partir d’un bot.

## <a name="how-silent-authentication-works"></a>Fonctionnement de l’authentification sans assistance

La bibliothèque ADAL. js crée un IFRAME masqué pour le flux d’octroi implicite OAuth 2,0, `prompt=none` mais il indique de sorte qu’Azure ad n’affiche jamais la page de connexion. Si l’intervention de l’utilisateur est requise parce que l’utilisateur doit se connecter ou accorder l’accès à l’application, Azure AD renvoie immédiatement une erreur indiquant que ADAL. js fait état de votre application. À ce stade, votre application peut afficher un bouton de connexion si nécessaire.

## <a name="how-to-do-silent-authentication"></a>Procédure d’authentification sans assistance

Le code de cet article provient de l’exemple [d’authentification Microsoft teams](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)de l’application Teams (nœud).

### <a name="include-and-configure-adal"></a>inclure et configurer ADAL

Incluez la bibliothèque ADAL. js dans vos pages d’onglets et configurez ADAL avec votre ID client et l’URL de redirection :

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

### <a name="get-the-user-context"></a>Obtenir le contexte de l’utilisateur

Dans la page de contenu de l’onglet `microsoftTeams.getContext()` , appelez pour obtenir une indication de connexion pour l’utilisateur actuel. Il sera utilisé comme un login_hint dans l’appel à Azure AD.

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

Si ADAL a un jeton non expiré mis en cache pour l’utilisateur, utilisez-le. Sinon, essayez d’obtenir un jeton en mode silencieux en `acquireToken(resource, callback)`appelant. ADAL. js appelle votre fonction de rappel avec le jeton demandé, ou une erreur en cas d’échec de l’authentification.

Si vous obtenez une erreur dans la fonction de rappel, affichez un bouton de connexion et basculez vers une connexion explicite.

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

Laissez ADAL. js prendre en charge l’analyse du résultat à partir d’Azure AD `AuthenticationContext.handleWindowCallback(hash)` en appelant la page de rappel de connexion.

Vérifiez que nous disposons d’un utilisateur et d' `microsoftTeams.authentication.notifySuccess()` un `microsoftTeams.authentication.notifyFailure()` appel valides ou que vous revenez à la page de contenu de votre onglet principal.

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
