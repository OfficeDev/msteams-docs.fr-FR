---
title: Authentification en mode silencieux
description: Décrit l’authentification silencieuse, l’authentification unique, Azure Active Directory pour les onglets
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Onglet silencieux de l’authentification AAD teams
ms.openlocfilehash: 2b3981ce43f09cc05bb2cb3837a90c0a92ef6deb
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888026"
---
# <a name="silent-authentication"></a>Authentification en mode silencieux

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, assurez-vous que vous utilisez au moins la version 1.4.1 du SDK JavaScript Teams.

L’authentification sans Azure Active Directory (AAD) réduit le nombre de fois qu’un utilisateur entre ses informations d’identification de connexion en actualisation silencieuse du jeton d’authentification. Pour obtenir une prise en charge de l' sign-on unique réelle, voir [la documentation de l’oD unique.](~/tabs/how-to/authentication/auth-aad-sso.md)

Si vous souhaitez conserver votre code entièrement côté client, vous pouvez utiliser la bibliothèque d’authentification [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) pour JavaScript pour obtenir un jeton d’accès AAD silencieusement. Si l’utilisateur s’est récemment inscrit, il ne voit jamais de boîte de dialogue de fenêtre pop-up.

Même si la bibliothèque ADAL.js est optimisée pour les applications AngularJS, elle fonctionne également avec des applications mono-page JavaScript pures.

> [!NOTE]
> Actuellement, l’authentification silencieuse fonctionne uniquement pour les onglets. Elle ne fonctionne pas lors de la signature à partir d’un bot.

## <a name="how-silent-authentication-works"></a>Fonctionnement de l’authentification silencieuse

La ADAL.js crée un iframe masqué pour le flux d’octroi implicite OAuth 2.0. Toutefois, la bibliothèque spécifie `prompt=none` , Azure AD affiche jamais la page de se connecte. Si l’interaction utilisateur est requise parce que l’utilisateur doit se connecter ou accorder l’accès à l’application, AAD renvoie immédiatement une erreur ADAL.js signale à votre application. À ce stade, votre application peut afficher un bouton de signature si nécessaire.

## <a name="how-to-do-silent-authentication"></a>Procédure d’authentification silencieuse

Le code de cet article provient de l’Teams exemple d’application qui est Teams [exemple d’authentification.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)

[Lancez l’onglet configurable](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) d’authentification simple et silencieuse à l’AAD et suivez les instructions pour exécuter l’exemple sur votre ordinateur local.

### <a name="include-and-configure-adal"></a>Inclure et configurer ADAL

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

Dans la page de contenu de l’onglet, appelez pour obtenir un conseil de connect `microsoftTeams.getContext()` pour l’utilisateur actuel. Il est utilisé comme loginHint dans l’appel AAD.

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

Si ADAL a un jeton mis en cache pour l’utilisateur qui n’a pas expiré, utilisez ce jeton. Vous pouvez également essayer d’obtenir un jeton silencieusement en appelant `acquireToken(resource, callback)` . ADAL.js appelle la fonction de rappel avec le jeton demandé ou donne une erreur en cas d’échec de l’authentification.

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

ADAL.js le résultat de l’AAD en appelant dans la page de rappel `AuthenticationContext.handleWindowCallback(hash)` de la signature.

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

### <a name="handle-sign-out-flow"></a>Gérer le flux de la signature

Utilisez le code suivant pour gérer le flux de la AAD th :

> [!NOTE]
> Lorsque vous vous déconnectez de Teams’onglet ou du bot, la session en cours est effacée.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
## <a name="see-also"></a>Voir aussi

[Configurer les fournisseurs d’identité pour qu’ils utilisent AAD](~/concepts/authentication/configure-identity-provider.md)
