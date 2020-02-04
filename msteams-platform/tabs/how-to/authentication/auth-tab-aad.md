---
title: Authentification pour les onglets à l’aide d’Azure Active Directory
description: Décrit l’authentification dans teams et son utilisation dans des onglets
keywords: onglets d’authentification de teams AAD
ms.openlocfilehash: 760fce99a51dc722905035bade6db008072ee0b4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673792"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Authentifier un utilisateur sous un onglet Microsoft teams

> [!Note]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez la version 1.4.1 ou une version ultérieure du kit de développement logiciel (SDK) JavaScript Teams.

Il est possible que vous souhaitiez consommer de nombreux services au sein de votre application teams et que la plupart de ces services requièrent une authentification et une autorisation pour accéder au service. Les services incluent Facebook, Twitter et des équipes de cours. Les utilisateurs de teams ont des informations de profil utilisateur stockées dans Azure Active Directory (Azure AD) à l’aide de Microsoft Graph et cet article se concentre sur l’authentification à l’aide d’Azure AD pour accéder à ces informations.

OAuth 2,0 est une norme ouverte pour l’authentification utilisée par Azure AD et de nombreux autres fournisseurs de services. La présentation de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans teams et Azure AD. Les exemples ci-dessous utilisent le flux d’octroi implicite OAuth 2,0 avec l’objectif de lire les informations de profil de l’utilisateur à partir d’Azure AD et de Microsoft Graph.

Le code de cet article provient de l’exemple [d’authentification de l’exemple d’application Microsoft teams](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)de teams Teams (nœud). Elle contient un onglet statique qui demande un jeton d’accès pour Microsoft Graph et affiche les informations de base du profil de l’utilisateur actuel à partir d’Azure AD.

Pour obtenir une vue d’ensemble du flux d’authentification pour les onglets, consultez la rubrique [flux d’authentification dans des onglets](~/tabs/how-to/authentication/auth-flow-tab.md).

Le flux d’authentification dans les onglets diffère légèrement du flux d’authentification dans les robots.

## <a name="configuring-identity-providers"></a>Configuration des fournisseurs d’identité

Consultez la rubrique [configure Identity Providers](~/concepts/authentication/configure-identity-provider.md) pour obtenir des instructions détaillées sur la configuration des URL de redirection de rappel OAuth 2,0 lors de l’utilisation d’Azure Active Directory en tant que fournisseur d’identité.

## <a name="initiate-authentication-flow"></a>Activer le flux d’authentification

Le flux d’authentification doit être déclenché par une action de l’utilisateur. Vous ne devez pas ouvrir automatiquement la fenêtre contextuelle d’authentification, car cela déclenchera probablement le blocage des fenêtres publicitaires intempestives du navigateur, ainsi que la confusion de l’utilisateur.

Ajoutez un bouton à votre page de configuration ou de contenu pour permettre à l’utilisateur de se connecter lorsque cela est nécessaire. Cette opération peut être exécutée sur la page de [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) de l’onglet ou sur une page de [contenu](~/tabs/how-to/create-tab-pages/content-page.md) .

Azure AD, comme la plupart des fournisseurs d’identité, ne permet pas de placer son contenu dans un IFRAME. Cela signifie que vous devrez ajouter une page contextuelle pour héberger le fournisseur d’identité. Dans l’exemple suivant, cette page `/tab-auth/simple-start`est. Utilisez la `microsoftTeams.authenticate()` fonction du kit de développement logiciel (SDK) client Microsoft teams pour lancer cette page lorsque votre bouton est sélectionné.

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

* L’URL que vous transmettez `microsoftTeams.authentication.authenticate()` est la page de démarrage du flux d’authentification. Dans cet exemple, il `/tab-auth/simple-start`s’agit de. Cela doit correspondre à ce que vous avez enregistré dans le [portail d’inscription des applications Azure ad](https://apps.dev.microsoft.com).

* Le flux d’authentification doit démarrer sur une page qui se trouve sur votre domaine. Ce domaine doit également figurer dans la [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section du manifeste. Si ce n’est pas le cas, une fenêtre contextuelle vide est générée.

* Ne pas utiliser `microsoftTeams.authentication.authenticate()` provoque un problème : la fenêtre contextuelle ne se ferme pas à la fin du processus de connexion.

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>Accéder à la page d’autorisation à partir de votre page contextuelle

Lorsque votre page contextuelle (`/tab-auth/simple-start`) s’affiche, le code suivant est exécuté. L’objectif principal de cette page est de rediriger vers votre fournisseur d’identité afin que l’utilisateur puisse se connecter. Cette redirection a pu être réalisée côté serveur à l’aide du protocole HTTP 302, mais dans ce cas, elle est exécutée côté client en utilisant un `window.location.assign()`appel à. Cela permet `microsoftTeams.getContext()` également de récupérer des informations d’indication qui peuvent être transmises à Azure ad.

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

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

Une fois que l’utilisateur a terminé l’autorisation, l’utilisateur est redirigé vers la page de rappel que vous avez `/tab-auth/simple-end`spécifiée pour votre application sur.

### <a name="notes"></a>Notes

* Voir [obtenir des informations de contexte utilisateur pour obtenir](~/tabs/how-to/access-teams-context.md) de l’aide sur la création des requêtes d’authentification et des URL. Par exemple, vous pouvez utiliser le nom de connexion de l’utilisateur `login_hint` comme valeur pour la connexion à Azure ad, ce qui signifie que l’utilisateur peut avoir besoin de taper moins. N’oubliez pas que vous ne devez pas utiliser ce contexte directement comme preuve d’identité, car un agresseur pourrait charger votre page dans un navigateur malveillant et lui fournir toutes les informations dont il a besoin.
* Bien que le contexte d’onglet fournit des informations utiles sur l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur, que vous l’obteniez comme paramètres d’URL de `microsoftTeams.getContext()` votre URL de contenu de tabulation ou en appelant la fonction dans le kit de développement logiciel (SDK) du client Microsoft Teams. Un acteur malveillant peut appeler votre URL de contenu de tabulation avec ses propres paramètres, et une page Web qui emprunte l’identité de Microsoft teams pourrait charger votre URL de contenu d’onglet dans `getContext()` un IFRAME et renvoyer ses propres données à la fonction. Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet simplement comme des conseils et les valider avant de les utiliser.
* Le `state` paramètre est utilisé pour confirmer que le service qui appelle l’URI de rappel est le service que vous avez appelé. Si le `state` paramètre dans le rappel ne correspond pas au paramètre que vous avez envoyé pendant l’appel, l’appel de retour n’est pas vérifié et doit être arrêté.
* Il n’est pas nécessaire d’inclure le domaine du fournisseur d’identité `validDomains` dans la liste du fichier manifest. JSON de l’application.

## <a name="the-callback-page"></a>Page de rappel

Dans la dernière section, vous avez appelé le service d’autorisation Azure AD et transmis des informations sur l’utilisateur et l’application de sorte qu’Azure AD puisse présenter son propre mode d’autorisation monolithique à l’utilisateur. Votre application n’a pas de contrôle sur ce qui se passe dans cette expérience. Il sait qu’il est renvoyé lorsque Azure AD appelle la page de rappel que vous avez fournie`/tab-auth/simple-end`().

Dans cette page, vous devez déterminer la réussite ou l’échec en fonction des informations renvoyées par Azure `microsoftTeams.authentication.notifySuccess()` ad `microsoftTeams.authentication.notifyFailure()`, appeler ou. Si la connexion a été établie, vous aurez accès aux ressources de service.

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

Ce code analyse les paires clé-valeur reçues à partir d’Azure AD `window.location.hash` à l' `getHashParameters()` aide de la fonction d’assistance. S’il trouve un `access_token`et que la `state` valeur est la même que celle fournie au début du flux d’authentification, il renvoie le jeton d’accès à l’onglet en appelant `notifySuccess()`; dans le cas contraire, il `notifyFailure()`signale une erreur avec.

### <a name="notes"></a>Notes

`NotifyFailure()`a les causes d’échec prédéfinies suivantes :

* `CancelledByUser`l’utilisateur a fermé la fenêtre contextuelle avant de terminer le flux d’authentification.
* `FailedToOpenWindow`la fenêtre contextuelle n’a pas pu être ouverte. Lorsque Microsoft teams est exécuté dans un navigateur, cela signifie généralement que la fenêtre a été bloquée par un bloqueur de fenêtres publicitaires intempestives.

Si elle réussit, vous pouvez actualiser ou recharger la page et afficher le contenu pertinent pour l’utilisateur authentifié. Si l’authentification échoue, un message d’erreur s’affiche.

Votre application peut définir son propre cookie de session de sorte que l’utilisateur ne doive pas se connecter à nouveau lorsqu’il revient à votre onglet sur le périphérique actuel.

> [!NOTE]
> Chrome 80, planifié pour la publication au début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookies par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies au lieu de vous appuyer sur le comportement par défaut du navigateur. *Voir* [SameSite cookie Attribute (mise à jour 2020)](../../../resources/samesite-cookie-update.md).

Pour plus d’informations sur l’authentification unique (SSO), consultez l’article [authentification sans assistance](~/tabs/how-to/authentication/auth-silent-AAD.md).

## <a name="samples"></a>Exemples

Pour obtenir un exemple de code illustrant le processus d’authentification par onglet à l’aide d’Azure AD, voir :

* [Exemple d’authentification de l’onglet Microsoft Teams (nœud)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
