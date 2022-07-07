---
title: Configuration du code pour l’activation de l’authentification unique pour les onglets
description: Décrit la configuration du code pour l’activation de l’authentification unique pour les onglets
ms.topic: how-to
ms.localizationpriority: high
keywords: onglets d’authentification teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 466da3cbd879ed2546adcad87f6f55620d54256d
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658937"
---
# <a name="add-code-to-enable-sso"></a>Ajouter du code pour activer l’authentification unique

Avant d’ajouter du code pour activer l’authentification unique, vérifiez que vous avez inscrit votre application auprès de Azure AD.

> [!div class="nextstepaction"]
> [S’inscrire auprès de Azure AD](tab-sso-register-aad.md)

Vous devez configurer le code côté client de votre application tabulation pour obtenir un jeton d’accès auprès de Azure AD. Le jeton d’accès est émis pour le compte de l’application d’onglet. Si votre application onglet requiert des autorisations de Microsoft Graph supplémentaires, vous devez transmettre le jeton d’accès côté serveur et l’échanger contre Microsoft Graph jeton.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="Configurer le code pour la gestion du jeton d’accès":::

Cette section traite des sujets suivants :

- [Ajouter du code côté client](#add-client-side-code)
- [Passer le jeton d’accès au code côté serveur](#pass-the-access-token-to-server-side-code)
- [Valider le jeton d’accès](#validate-the-access-token)

## <a name="add-client-side-code"></a>Ajouter du code côté client

Pour obtenir l’accès à l’application pour l’utilisateur actuel de l’application, votre code côté client doit appeler Teams pour obtenir un jeton d’accès. Vous devez mettre à jour le code côté client pour utiliser `getAuthToken()` pour lancer le processus de validation.

<br>
<details>
<summary>En savoir plus sur getAuthToken()</summary>
<br>
`getAuthToken()` est une méthode du Kit de développement logiciel (SDK) JavaScript Microsoft Teams. Il demande l’émission d’un jeton d’accès Azure AD pour le compte de l’application. Le jeton est acquis à partir du cache, s’il n’a pas expiré. Si elle a expiré, une demande est envoyée à Azure AD pour obtenir un nouveau jeton d’accès.

 Pour plus d’informations, consultez [getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true).
</details>

### <a name="when-to-call-getauthtoken"></a>Quand appeler getAuthToken

Utilisez `getAuthToken()` au moment où vous avez besoin d’un jeton d’accès pour l’utilisateur actuel de l’application :

| Si un jeton d’accès est nécessaire... | Appeler getAuthToken()... |
| --- | --- |
| Lorsque l’utilisateur de l’application accède à l’application | De l’intérieur `microsoftTeams.initialize()`. |
| Pour utiliser une fonctionnalité particulière de l’application | Lorsque l’utilisateur de l’application effectue une action qui nécessite une connexion. |

### <a name="add-code-for-getauthtoken"></a>Ajouter du code pour getAuthToken

Ajoutez un extrait de code JavaScript à l’application d’onglet pour :

- Appel `getAuthToken()`.
- Analysez le jeton d’accès ou transmettez-le au code côté serveur.

L’extrait de code suivant montre un exemple d’appel de `getAuthToken()`.

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Vous pouvez ajouter des appels de `getAuthToken()` à toutes les fonctions et gestionnaires qui lancent une action où le jeton est nécessaire.

<br>
<details>
<summary>Voici un exemple de code côté client :</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="Configurer le code client" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

Lorsque Teams reçoit le jeton d’accès, il est mis en cache et réutilisé en fonction des besoins. Ce jeton peut être utilisé chaque fois que `getAuthToken()` est appelé, jusqu’à ce qu’il expire, sans effectuer d’autre appel à Azure AD.

> [!IMPORTANT]
> Comme meilleure pratique pour la sécurité des jetons d’accès :
>
> - Appelez toujours `getAuthToken()` uniquement lorsque vous avez besoin d’un jeton d’accès.
> - Teams met en cache le jeton d’accès pour vous. Ne le mettez pas en cache ou ne le stockez pas dans le code de votre application.

### <a name="consent-dialog-for-getting-access-token"></a>Boîte de dialogue de consentement pour l’obtention du jeton d’accès

Lorsque vous appelez `getAuthToken()` et que le consentement de l’utilisateur de l’application est requis pour les autorisations au niveau de l’utilisateur, une boîte de dialogue Azure AD s’affiche à l’utilisateur de l’application actuellement connecté.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="Onglet - Invite de dialogue d’authentification unique":::

La boîte de dialogue de consentement qui s’affiche concerne les étendues open-id définies dans Azure AD. L’utilisateur de l’application ne doit donner son consentement qu’une seule fois. Après avoir donné son consentement, l’utilisateur de l’application peut accéder à votre application d’onglet et l’utiliser pour les autorisations et étendues accordées.

> [!IMPORTANT]
> Scénarios où les dialogues de consentement ne sont pas nécessaires :
>
> - Si l’administrateur client a donné son consentement pour le compte du locataire, les utilisateurs de l’application n’ont pas besoin d’être invités à donner leur consentement. Cela signifie que les utilisateurs de l’application ne voient pas les dialogues de consentement et peuvent accéder à l’application en toute transparence.
> - Si votre application Azure AD est inscrite dans le même locataire que celui à partir duquel vous demandez une authentification dans Teams, l’utilisateur de l’application ne peut pas être invité à donner son consentement et reçoit immédiatement un jeton d’accès. Les utilisateurs de l’application consentent à ces autorisations uniquement si l’application Azure AD est inscrite dans un autre locataire.

Si vous rencontrez des erreurs, consultez [Résolution des problèmes d’authentification unique dans Teams](tab-sso-troubleshooting.md).

### <a name="use-the-access-token-as-an-identity-token"></a>Utiliser le jeton d'accès comme jeton d’identité

Le jeton retourné à l’application d’onglet est à la fois un jeton d’accès et un jeton d’ID. L’application d’onglet peut utiliser le jeton comme jeton d’accès pour effectuer des requêtes HTTPS authentifiées aux API côté serveur.

Le jeton d’accès retourné par `getAuthToken()` peut être utilisé pour établir l’identité de l’utilisateur de l’application à l’aide des revendications suivantes dans le jeton :

- `name` : nom complet de l’utilisateur de l’application.
- `preferred_username` : adresse e-mail de l’utilisateur de l’application.
- `oid` : GUID représentant l’ID de l’utilisateur de l’application.
- `tid`: GUID représentant le locataire auquel l’utilisateur de l’application se connecte.

Teams peut mettre en cache ces informations associées à l’identité de l’utilisateur de l’application, telles que les préférences de l’utilisateur.

> [!NOTE]
> Si vous devez construire un ID unique pour représenter l’utilisateur de l’application dans votre système, consultez [Utilisation des revendications pour identifier de manière fiable un utilisateur](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id).

## <a name="pass-the-access-token-to-server-side-code"></a>Passer le jeton d’accès au code côté serveur

Si vous devez accéder aux API web sur votre serveur, vous devez transmettre le jeton d’accès à votre code côté serveur. Les API web doivent décoder le jeton d’accès pour afficher les revendications de ce jeton.

> [!NOTE]
> Si vous ne recevez pas le nom d’utilisateur principal (UPN) dans le jeton d’accès retourné, ajoutez-le en tant que [revendication facultative](/azure/active-directory/develop/active-directory-optional-claims) dans Azure AD.
> Pour plus d’informations, consultez [Jetons d’accès](/azure/active-directory/develop/access-tokens).

Le jeton d’accès reçu lors du rappel de réussite de `getAuthToken()` fournit l’accès (pour l’utilisateur d’application authentifié) à vos API web. Le code côté serveur peut également analyser le jeton pour les [informations d’identité](#use-the-access-token-as-an-identity-token), si nécessaire.

Si vous devez transmettre le jeton d’accès pour obtenir Microsoft Graph données, consultez [Étendre l’application onglet avec des autorisations Microsoft Graph](tab-sso-graph-api.md).

### <a name="code-for-passing-access-token-to-server-side"></a>Code pour le passage du jeton d’accès côté serveur

Le code suivant montre un exemple de transmission du jeton d’accès côté serveur. Le jeton est transmis dans un en-tête `Authorization` lors de l’envoi d’une requête à une API Web côté serveur. Cet exemple envoie des données JSON, de sorte qu’il utilise la méthode `POST`. Le `GET` est suffisant pour envoyer le jeton d’accès lorsque vous n’écrivez pas sur le serveur.

```javascript
$.ajax({
    type: "POST",
    url: "/api/DoSomething",
    headers: {
        "Authorization": "Bearer " + accessToken
    },
    data: { /* some JSON payload */ },
    contentType: "application/json; charset=utf-8"
}).done(function (data) {
    // Handle success
}).fail(function (error) {
    // Handle error
}).always(function () {
    // Cleanup
});
```

### <a name="validate-the-access-token"></a>Valider le jeton d’accès

Les API web sur votre serveur doivent décoder le jeton d’accès et vérifier s’il est envoyé à partir du client. Le jeton est un jeton JWT. En d’autres termes, la validation se déroule comme dans la plupart des flux OAuth standard. Les API web doivent décoder le jeton d’accès. Si vous le souhaitez, vous pouvez copier et coller le jeton d’accès manuellement dans un outil, tel que jwt.ms.

Il existe un certain nombre de bibliothèques disponibles qui peuvent gérer la validation JWT. La validation de base inclut :

- vérifier que le jeton est bien formé ;
- vérifier que le jeton a été émis par l’autorité souhaitée ;
- Vérification que le jeton est destiné à l’API web

Suivez les recommandations suivantes quand vous validez le jeton :

- Les jetons d’authentification unique valides sont émis par Azure AD. La revendication `iss` dans le jeton doit commencer par cette valeur.
- Le paramètre `aud1` du jeton est défini sur l’ID d’application généré lors de Azure AD inscription de l’application.
- Le paramètre `scp` du jeton devra correspondre à `access_as_user`.

#### <a name="example-access-token"></a>Exemple de token

Voici une charge utile d?cod?e typique de token.

```javascript
{
    aud: "2c3caa80-93f9-425e-8b85-0745f50c0d24",
    iss: "https://login.microsoftonline.com/fec4f964-8bc9-4fac-b972-1c1da35adbcd/v2.0",
    iat: 1521143967,
    nbf: 1521143967,
    exp: 1521147867,
    aio: "ATQAy/8GAAAA0agfnU4DTJUlEqGLisMtBk5q6z+6DB+sgiRjB/Ni73q83y0B86yBHU/WFJnlMQJ8",
    azp: "e4590ed6-62b3-5102-beff-bad2292ab01c",
    azpacr: "0",
    e_exp: 262800,
    name: "Mila Nikolova",
    oid: "6467882c-fdfd-4354-a1ed-4e13f064be25",
    preferred_username: "milan@contoso.com",
    scp: "access_as_user",
    sub: "XkjgWjdmaZ-_xDmhgN1BMP2vL2YOfeVxfPT_o8GRWaw",
    tid: "fec4f964-8bc9-4fac-b972-1c1da35adbcd",
    uti: "MICAQyhrH02ov54bCtIDAA",
    ver: "2.0"
}
```

## <a name="code-samples"></a>Exemples de code

| Exemple de nom | Description | C#/.NET| Node.js |
|---------------|---------------|------|--------------|
| Onglet SSO |Exemple d'application Microsoft Teams pour les onglets Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs) </br>[Toolkit Teams](../../../toolkit/visual-studio-code-tab-sso.md)|
| Authentification unique Tab, Bot and Message Extension (ME) | Cet exemple montre l’authentification unique pour Tab, Bot et ME – recherche, action, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Mettre à jour le manifeste de l’application Teams et afficher un aperçu de l’application](tab-sso-manifest.md)

## <a name="see-also"></a>Voir aussi

- [jwt.ms](https://jwt.ms/)
- [Revendication facultative Active Directory](/azure/active-directory/develop/active-directory-optional-claims)
- [Jetons d’accès](/azure/active-directory/develop/access-tokens)
- [Vue d’ensemble de la bibliothèque d’authentification Microsoft (MSAL)](/azure/active-directory/develop/msal-overview)
- [Jetons d’ID de plateforme d’identités Microsoft](/azure/active-directory/develop/id-tokens)
- [Jetons d’accès de plateforme d’identité Microsoft](/azure/active-directory/develop/access-tokens#validating-tokens)
