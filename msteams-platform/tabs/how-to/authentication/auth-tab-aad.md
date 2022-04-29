---
title: Authentification pour les onglets à l’aide de Azure Active Directory
description: Décrit l’authentification dans Teams et comment l’utiliser dans des onglets
ms.topic: how-to
ms.localizationpriority: high
keywords: onglets d’authentification teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 3341c7235e3fdbfeb401e6d22abf0869c1e9b181
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111674"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Authentifier un utilisateur dans un onglet Microsoft Teams

> [!Note]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez la version 1.4.1 ou ultérieure du Kit de développement logiciel (SDK) JavaScript Teams.

Il existe de nombreux services que vous pouvez utiliser dans votre application Teams, et la plupart de ces services nécessitent une authentification et une autorisation pour accéder au service. Les services incluent Facebook, Twitter et Teams. Les informations de profil utilisateur Teams sont stockées dans Azure AD à l’aide de Microsoft Graph et cet article se concentre sur l’authentification à l’aide de Azure AD pour accéder à ces informations.

OAuth 2.0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services. La compréhension d’OAuth 2.0 est un prérequis pour l’utilisation de l’authentification dans Teams et Azure AD. Les exemples ci-dessous utilisent le flux d’octroi implicite OAuth 2.0 dans le but de lire les informations de profil de l’utilisateur à partir de Azure AD et Microsoft Graph.

Le code de cet article provient de l’exemple d’application Teams [Exemple d’authentification par onglet Microsoft Teams (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node). Il contient un onglet statique qui demande un jeton d’accès pour Microsoft Graph et affiche les informations de profil de base de l’utilisateur actuel à partir de Azure AD.

Pour une vue d’ensemble du flux d’authentification pour les onglets, consultez [flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md).

Le flux d’authentification dans les onglets diffère légèrement du flux d’authentification dans les bots.

## <a name="configuring-identity-providers"></a>Configuration des fournisseurs d’identité

Consultez la rubrique [Configurer les fournisseurs d’identité](~/concepts/authentication/configure-identity-provider.md) pour obtenir des instructions détaillées sur la configuration des URL de redirection de rappel OAuth 2.0 lors de l’utilisation de Azure AD en tant que fournisseur d’identité.

## <a name="initiate-authentication-flow"></a>Lancer le flux d’authentification

Le flux d’authentification doit être déclenché par une action de l’utilisateur. Vous ne devez pas ouvrir la fenêtre contextuelle d’authentification automatiquement, car cela est susceptible de déclencher le bloqueur de fenêtres contextuelles du navigateur et de confondre l’utilisateur.

Ajoutez un bouton à votre page de configuration ou de contenu pour permettre à l’utilisateur de se connecter si nécessaire. Vous pouvez le faire dans l’onglet page de [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) ou dans n’importe quelle page de [contenu](~/tabs/how-to/create-tab-pages/content-page.md).

Azure AD, comme la plupart des fournisseurs d’identité, n’autorise pas son contenu à être placé dans une iFrame. Cela signifie que vous devez ajouter une page contextuelle pour héberger le fournisseur d’identité. Dans l’exemple suivant, cette page est `/tab-auth/simple-start`. Utilisez la fonction `microsoftTeams.authenticate()` du Kit de développement logiciel (SDK) client Microsoft Teams pour lancer cette page lorsque votre bouton est sélectionné.

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

### <a name="notes"></a>Notes

* L’URL que vous transmettez à `microsoftTeams.authentication.authenticate()` est la page de démarrage du flux d’authentification. Dans cet exemple, il s’agit de `/tab-auth/simple-start`. Cela doit correspondre à ce que vous avez inscrit dans le [Portail d’inscription des applications Azure AD](https://apps.dev.microsoft.com).

* Le flux d’authentification doit commencer sur une page qui se trouve sur votre domaine. Ce domaine doit également être répertorié dans la section [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) du manifeste. Si ce n’est pas le cas, une fenêtre contextuelle vide s’affiche.

* Si vous n’utilisez pas `microsoftTeams.authentication.authenticate()`, la fenêtre contextuelle ne se ferme pas à la fin du processus de connexion.

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>Accédez à la page d’autorisation à partir de votre page contextuelle

Lorsque votre page contextuelle (`/tab-auth/simple-start`) s’affiche, le code suivant est exécuté. L’objectif principal de cette page est de rediriger vers votre fournisseur d’identité afin que l’utilisateur puisse se connecter. Cette redirection peut être effectuée côté serveur à l’aide de HTTP 302, mais dans ce cas, elle est effectuée côté client à l’aide d’un appel à `window.location.assign()`. Cela permet également d’utiliser `microsoftTeams.getContext()` pour récupérer des informations d’indication, qui peuvent être passées à Azure AD.

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
        scope: "https://graph.microsoft.com/User.Read openid",
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

Une fois l’autorisation terminée, l’utilisateur est redirigé vers la page de rappel que vous avez spécifiée pour votre application à `/tab-auth/simple-end`.

### <a name="notes"></a>Notes

* Consultez [obtenir des informations de contexte utilisateur](~/tabs/how-to/access-teams-context.md) pour obtenir de l’aide sur la création de demandes d’authentification et d’URL. Par exemple, vous pouvez utiliser le nom de connexion de l’utilisateur comme valeur de `login_hint` pour Azure AD connexion, ce qui signifie que l’utilisateur peut avoir besoin de taper moins. N’oubliez pas que vous ne devez pas utiliser ce contexte directement comme preuve d’identité, car un attaquant pourrait charger votre page dans un navigateur malveillant et lui fournir les informations souhaitées.
* Bien que le contexte de l’onglet fournisse des informations utiles concernant l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur, que vous l’obteniez en tant que paramètres d’URL vers l’URL de contenu de votre onglet ou en appelant la fonction `microsoftTeams.getContext()` dans le Kit de développement logiciel (SDK) du client Microsoft Teams. Un acteur malveillant pourrait appeler l’URL de contenu de votre onglet avec ses propres paramètres, et une page web empruntant l’identité de Microsoft Teams pourrait charger l’URL de contenu de votre onglet dans une iFrame et retourner ses propres données à la fonction `getContext()`. Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet simplement comme des indicateurs et les valider avant de les utiliser.
* Le paramètre `state` est utilisé pour confirmer que le service appelant l’URI de rappel est le service que vous avez appelé. Si le paramètre `state` dans le rappel ne correspond pas au paramètre que vous avez envoyé pendant l’appel, l’appel de retour n’est pas vérifié et doit être arrêté.
* Il n’est pas nécessaire d’inclure le domaine du fournisseur d’identité dans la liste `validDomains` dans le fichier manifest.json de l’application.

## <a name="the-callback-page"></a>Page de rappel

Dans la dernière section, vous avez appelé le service d’autorisation Azure AD et transmis des informations sur l’utilisateur et l’application afin que Azure AD puisse présenter à l’utilisateur sa propre expérience d’autorisation monolithique. Votre application n’a aucun contrôle sur ce qui se passe dans cette expérience. Tout ce qu’il sait est ce qui est retourné quand Azure AD appelle la page de rappel que vous avez fournie (`/tab-auth/simple-end`).

Dans cette page, vous devez déterminer la réussite ou l’échec en fonction des informations retournées par Azure AD et appeler `microsoftTeams.authentication.notifySuccess()` ou `microsoftTeams.authentication.notifyFailure()`. Si la connexion a réussi, vous aurez accès aux ressources de service.

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

Ce code analyse les paires clé-valeur reçues de Azure AD dans `window.location.hash` à l’aide de la fonction d’assistance `getHashParameters()`. S’il trouve une `access_token`, et que la valeur `state` est identique à celle fournie au début du flux d’authentification, elle retourne le jeton d’accès à l’onglet en appelant `notifySuccess()`; sinon, il signale une erreur avec `notifyFailure()`.

### <a name="notes"></a>Notes

`NotifyFailure()` présente les raisons d’échec prédéfinies suivantes :

* `CancelledByUser` l’utilisateur a fermé la fenêtre contextuelle avant de terminer le flux d’authentification.
* `FailedToOpenWindow` la fenêtre contextuelle n’a pas pu être ouverte. Lors de l’exécution de Microsoft Teams dans un navigateur, cela signifie généralement que la fenêtre a été bloquée par un bloqueur de fenêtres contextuelles.

En cas de réussite, vous pouvez actualiser ou recharger la page et afficher le contenu pertinent pour l’utilisateur authentifié. Si l’authentification échoue, un message d’erreur s’affiche.

Votre application peut définir son propre cookie de session afin que l’utilisateur n’ait pas besoin de se reconnecter lorsqu’il revient à votre onglet sur l’appareil actuel.

> [!NOTE]
>
> * Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. *consultez* [Attribut de cookie SameSite (mise à jour 2020)](../../../resources/samesite-cookie-update.md).
> * Pour obtenir le jeton correct pour les utilisateurs Microsoft Teams gratuits et invités, il est important que les applications utilisent un point de terminaison spécifique au client `https://login.microsoftonline.com/**{tenantId}**`. Vous pouvez obtenir tenantId à partir du message du bot ou du contexte de l’onglet. Si les applications utilisent `https://login.microsoftonline.com/common`, les utilisateurs reçoivent des jetons incorrects et se connectent au client « d'origine » au lieu du client auquel ils sont actuellement connectés.

Pour plus d’informations sur l’authentification unique (SSO), consultez l’article [Authentification silencieuse](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification par onglet à l’aide de Azure AD :

| **Exemple de nom** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Authentification par onglet Microsoft Teams | Processus d’authentification par tabulation à l’aide de Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Planifier l’authentification des utilisateurs](../../../concepts/design/understand-use-cases.md)
* [Concevoir votre onglet pour Microsoft Teams](~/tabs/design/tabs.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-aad.md)
* [Ajouter l’authentification à votre extension de message](~/messaging-extensions/how-to/add-authentication.md)
* [Prise en charge de l’authentification unique pour les bots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
