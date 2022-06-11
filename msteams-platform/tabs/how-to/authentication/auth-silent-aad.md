---
title: Authentification en mode silencieux
description: Décrit l’authentification silencieuse, l’authentification unique Azure AD pour les onglets
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Onglet Azure AD silencieux de l’authentification unique Teams
ms.openlocfilehash: 50d5d5327ee31286c7124f23b8fd4c8b07c71639
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2022
ms.locfileid: "66033021"
---
# <a name="silent-authentication"></a>Authentification en mode silencieux

> [!IMPORTANT]
> Le support et le développement Microsoft pour la bibliothèque d’authentification Active Directory (ADAL), y compris les correctifs de sécurité, se terminent le **30 juin 2022**. Pour continuer à recevoir du support, mettez à jour vos applications pour utiliser la bibliothèque d’authentification Microsoft (MSAL). Consultez [Migrer des applications vers la bibliothèque d’authentification Microsoft (MSAL).](/azure/active-directory/develop/msal-migration)

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, assurez-vous que vous utilisez le Kit de développement logiciel (SDK) JavaScript Teams version 1.4.1 ou ultérieure.

L’authentification silencieuse dans Azure AD réduit le nombre de fois qu’un utilisateur entre ses informations d’identification en actualisant silencieusement le jeton d’authentification. Pour obtenir la prise en charge de l’authentification unique réelle, consultez [la documentation de l’authentification](~/tabs/how-to/authentication/tab-sso-overview.md) unique.

Pour conserver votre code côté client, utilisez la bibliothèque d’authentification [Azure AD](/azure/active-directory/develop/active-directory-authentication-libraries) pour JavaScript afin d’obtenir un jeton d’accès Microsoft Azure Active Directory (Azure AD) en mode silencieux. Si l’utilisateur s’est connecté récemment, il ne voit pas de boîte de dialogue contextuelle.

Bien que Bibliothèque d'authentification Active Directory soit optimisé pour les applications AngularJS, il fonctionne également avec les applications monopages (SPA) JavaScript.

> [!NOTE]
> Actuellement, l’authentification silencieuse fonctionne uniquement pour les onglets. Il ne fonctionne pas lors de la connexion à partir d’un bot.

## <a name="how-silent-authentication-works"></a>Fonctionnement de l’authentification silencieuse

La bibliothèque d’authentification Active Directory crée un iframe masqué pour le flux d’octroi implicite OAuth 2.0. Mais la bibliothèque spécifie `prompt=none`, de sorte que Azure AD n’affiche pas la page de connexion. Une interaction utilisateur peut être nécessaire si l’utilisateur doit se connecter ou accorder l’accès à l’application. Si l’interaction utilisateur est nécessaire, Azure AD renvoie une erreur que la bibliothèque signale à votre application. Si nécessaire, votre application peut désormais afficher une option de connexion.

## <a name="how-to-do-silent-authentication"></a>Procédure d’authentification silencieuse

Le code de cet article provient de l’exemple d’application Teams qui est [nœud d’exemple d’authentification Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).

[Lancer l’onglet configurable d’authentification silencieuse et simple à l’aide de Azure AD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) et suivez les instructions pour exécuter l’exemple sur votre ordinateur local.

### <a name="include-and-configure-active-directory-authentication-library"></a>Inclure et configurer Bibliothèque d'authentification Active Directory

Incluez Bibliothèque d'authentification Active Directory dans vos pages d’onglets et configurez la bibliothèque avec votre ID client et l’URL de redirection :

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

### <a name="get-the-user-context"></a>Obtenir l'utilisateur pour le contexte actuel

Dans la page de contenu de l’onglet, appelez `microsoftTeams.getContext()` pour obtenir un indicateur de connexion pour l’utilisateur actuel. L’indicateur est utilisé comme un `loginHint` appel à Azure AD.

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

Si un jeton non expiré est mis en cache pour la bibliothèque d’authentification Active Directory pour l’utilisateur, utilisez le jeton. Vous pouvez également appeler `acquireToken(resource, callback)` pour recevoir un jeton en mode silencieux. La bibliothèque appelle une fonction de rappel avec le jeton demandé ou génère une erreur en cas d’échec de l’authentification.

Si vous obtenez une erreur dans la fonction de rappel, affichez et utilisez une option de connexion explicite.

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

La bibliothèque d’authentification Active Directory analyse le résultat de Azure AD en appelant `AuthenticationContext.handleWindowCallback(hash)` la page de rappel de connexion.

Vérifiez que vous disposez d’un utilisateur valide et appelez `microsoftTeams.authentication.notifySuccess()` ou `microsoftTeams.authentication.notifyFailure()` pour signaler l’état à votre page de contenu de l’onglet principal.

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

### <a name="handle-the-sign-out-flow"></a>Gérer le flux de déconnexion

Utilisez le code suivant pour gérer le flux de déconnexion dans Azure AD l’authentification :

> [!NOTE]
> Lorsque vous déconnexion à partir de Teams onglet ou bot, la session active est désactivée.

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>Voir aussi

* [Configurer des fournisseurs d’identité pour utiliser Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [Connaître la bibliothèque d'authentification de Microsoft (MSAL)](/azure/active-directory/develop/msal-overview) 
