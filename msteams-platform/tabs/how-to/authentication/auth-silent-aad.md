---
title: Authentification en mode silencieux
description: Décrit l’authentification silencieuse, l’authentification unique, Azure AD pour les onglets
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Onglet silencieux de l’authentification Azure AD teams
ms.openlocfilehash: e59b7ff30a0659b670796c56b97eda437f907739
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821569"
---
# <a name="silent-authentication"></a>Authentification en mode silencieux

> [!IMPORTANT]
> Le support et le développement de Microsoft pour la bibliothèque d’authentification Active Directory (ADAL), y compris les correctifs de sécurité, se terminent le **30 juin 2022**. Mettez à jour vos applications pour utiliser la bibliothèque d’authentification Microsoft (MSAL) afin de continuer à recevoir du support. Voir [Migrer des applications vers la bibliothèque d’authentification Microsoft (MSAL).](/azure/active-directory/develop/msal-migration)

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, assurez-vous que vous utilisez Teams JavaScript SDK version 1.4.1 ou ultérieure.

L’authentification Azure AD réduit le nombre de fois qu’un utilisateur entre ses informations d’identification en actualisation silencieuse du jeton d’authentification. Pour obtenir une prise en charge de l’sign-on unique réelle, voir [la documentation de l’oD unique](~/tabs/how-to/authentication/auth-aad-sso.md).

Pour conserver votre code côté client, utilisez la bibliothèque d’authentification [Azure AD](/azure/active-directory/develop/active-directory-authentication-libraries) pour JavaScript pour obtenir un jeton d’accès Microsoft Azure Active Directory (Azure AD) en mode silencieux. Si l’utilisateur s’est récemment inscrit, il ne voit pas de boîte de dialogue de fenêtre pop-up.

Bien que la bibliothèque d’authentification Active Directory soit optimisée pour les applications AngularJS, elle fonctionne également avec les applications Mono-page (SPA) JavaScript.

> [!NOTE]
> Actuellement, l’authentification silencieuse fonctionne uniquement pour les onglets. Elle ne fonctionne pas lors de la signature à partir d’un bot.

## <a name="how-silent-authentication-works"></a>Fonctionnement de l’authentification silencieuse

La bibliothèque d’authentification Active Directory crée un iframe masqué pour le flux d’octroi implicite OAuth 2.0. Toutefois, la bibliothèque spécifie `prompt=none`, Azure AD n’affiche pas la page de signature. L’interaction utilisateur peut être nécessaire si l’utilisateur doit se connecter ou accorder l’accès à l’application. Si une interaction utilisateur est nécessaire, Azure AD renvoie une erreur que la bibliothèque signale à votre application. Si nécessaire, votre application peut désormais afficher une option de connect.

## <a name="how-to-do-silent-authentication"></a>Procédure d’authentification silencieuse

Le code de cet article provient de l’Teams exemple d’application qui [est Teams exemple d’authentification.](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)

[Lancez l’onglet configurable d’authentification](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) simple et silencieuse à l’Azure AD et suivez les instructions pour exécuter l’exemple sur votre ordinateur local.

### <a name="include-and-configure-active-directory-authentication-library"></a>Inclure et configurer la bibliothèque d’authentification Active Directory

Incluez la bibliothèque d’authentification Active Directory dans vos pages d’onglets et configurez la bibliothèque avec votre ID client et l’URL de redirection :

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // Active Directory Authentication Library configuration
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

Dans la page de contenu de l’onglet, `microsoftTeams.getContext()` appelez pour obtenir un conseil de connect pour l’utilisateur actuel. L’indication est utilisée comme un conseil `loginHint` dans l’appel Azure AD.

```javascript
// Set up extra query parameters for Active Directory Authentication Library
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>Authentifier

Si un jeton nonpiré est mis en cache pour l’utilisateur dans la bibliothèque d’authentification Active Directory, utilisez-le. Vous pourrez également appeler `acquireToken(resource, callback)` pour recevoir silencieusement un jeton. La bibliothèque appelle une fonction de rappel avec le jeton demandé ou génère une erreur en cas d’échec de l’authentification.

Si vous obtenez une erreur dans la fonction de rappel, affichez et utilisez une option de signature explicite.

```javascript
let authContext = new AuthenticationContext(config); // from Active Directory Authentication Library
// See if there is a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which Active Directory Authentication Library returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure Active Directory Authentication Library gave us an ID token
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

La bibliothèque d’authentification Active Directory `AuthenticationContext.handleWindowCallback(hash)` permet d’Azure AD en appelant dans la page de rappel de la signature.

Vérifiez que vous avez un utilisateur valide et que vous `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` appelez ou pour signaler l’état à votre page de contenu d’onglet principal.

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

### <a name="handle-the-sign-out-flow"></a>Gérer le flux de la signature

Utilisez le code suivant pour gérer le flux de Azure AD’authentification :

> [!NOTE]
> Lorsque vous vous déconnectez de Teams’onglet ou du bot, la session en cours est effacée.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>Voir aussi

* [Configurer les fournisseurs d’identité pour qu’ils utilisent Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [En savoir plus sur la bibliothèque d’authentification Microsoft (MSAL)](/azure/active-directory/develop/msal-overview)
