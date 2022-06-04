---
title: Étendre l’application onglet avec des autorisations Microsoft Graph
description: Décrit la configuration des autorisations d’API avec Microsoft Graph
ms.topic: how-to
ms.localizationpriority: medium
keywords: onglets d’authentification teams Microsoft Azure Active Directory (Azure AD) Api Graph - Étendue du jeton d’accès délégué à l’autorisation
ms.openlocfilehash: 76b474f69b31d9c9b9925803ee7c0240f9e5a7c4
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888028"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>Étendre l’application onglet avec des autorisations et une étendue Microsoft Graph

Vous pouvez étendre votre application onglet à l’aide de Microsoft Graph pour autoriser les utilisateurs à disposer d’autorisations supplémentaires, telles que l’affichage du profil utilisateur de l’application, la lecture du courrier, etc. Votre application doit demander des étendues d’autorisation spécifiques pour obtenir les jetons d’accès sur le consentement de l’utilisateur de l’application.

Les étendues de graphe, telles que `User.Read` ou `Mail.Read`, vous permettent de spécifier comment votre application accède au compte d’un utilisateur Teams. Vous devez spécifier vos étendues dans la demande d’autorisation.

Dans cette section, vous allez apprendre à :

- [Configurer des autorisations d’API dans Azure AD](#configure-api-permissions-in-azure-ad)
- [Configurer l’authentification pour différentes plateformes](#configure-authentication-for-different-platforms)
- [Acquérir un jeton d’accès pour MS Graph](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>Configurer des autorisations d’API dans Azure AD

Vous pouvez configurer des étendues Graph supplémentaires dans Azure AD pour votre application. Il s’agit d’autorisations déléguées, qui sont utilisées par les applications qui nécessitent un accès connecté. Un utilisateur ou un administrateur d’application connecté doit y donner son consentement. Votre application onglet peut donner son consentement au nom de l’utilisateur connecté lorsqu’elle appelle Microsoft Graph.

### <a name="to-configure-api-permissions"></a>Pour configurer des autorisations d’API

1. Ouvrez l’application que vous avez inscrite dans le [portail Azure](https://ms.portal.azure.com/).

2. Sélectionnez **Gérer** > **l’autorisation d’API** dans le volet gauche.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="Option de menu Autorisations d’application." border="true":::

    La page **d’autorisations de l’API** s’affiche.

3. Sélectionnez **+ Ajouter des autorisations** pour ajouter des autorisations d’API Microsoft Graph.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="Page Autorisations de l’application." border="true":::

    La page **Demander des autorisations d’API** s’affiche.

4. Sélectionnez **Microsoft Graph**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="Page Demander des autorisations d’API." border="true":::

    Les options d’affichage des autorisations Graph.

5. Sélectionnez **Autorisations déléguées** pour afficher la liste des autorisations.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="Autorisations déléguées." border="true":::

6. Sélectionnez les autorisations appropriées pour votre application, puis sélectionnez **Ajouter des autorisations**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="Sélectionnez les autorisations." border="true":::

    Vous pouvez également entrer le nom d’autorisation dans la zone de recherche pour le trouver.

    Un message s’affiche sur le navigateur indiquant que les autorisations ont été mises à jour.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="Message de mise à jour des autorisations." border="false":::

    Les autorisations ajoutées sont affichées dans la page **d’autorisations de l’API** .

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="Les autorisations d’API sont configurées." border="true":::

    Vous avez configuré votre application avec des autorisations Microsoft Graph.

## <a name="configure-authentication-for-different-platforms"></a>Configurer l’authentification pour différentes plateformes

Selon la plateforme ou l’appareil sur lequel vous souhaitez cibler votre application, une configuration supplémentaire peut être nécessaire, comme des URI de redirection, des paramètres d’authentification spécifiques ou des détails spécifiques à la plateforme.

> [!NOTE]
>
> - Si votre application onglet n’a pas reçu le consentement de l’administrateur informatique, les utilisateurs de l’application doivent donner leur consentement la première fois qu’ils utilisent votre application sur une autre plateforme.
> - L’octroi implicite n’est pas nécessaire si l’authentification unique est activée sur une application onglet.

Vous pouvez configurer l’authentification pour plusieurs plateformes tant que l’URL est unique.

### <a name="to-configure-authentication-for-a-platform"></a>Pour configurer l’authentification pour une plateforme

1. Ouvrez l’application que vous avez inscrite dans le [portail Azure](https://ms.portal.azure.com/).

1. Sélectionnez **Gérer** > **l’authentification** dans le volet gauche.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="S’authentifier pour les plateformes" border="true":::

    La page **Configurations de la plateforme** s’affiche.

1. Sélectionnez **+ Ajouter une plateforme**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="Ajouter une plateforme" border="true":::

    La page **Configurer les plateformes** s’affiche.

1. Sélectionnez la plateforme que vous souhaitez configurer pour votre application onglet. Vous pouvez choisir le type de plateforme à partir du web ou de spa.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Sélectionner la plateforme web" border="true":::

    Vous pouvez configurer plusieurs plateformes pour un type de plateforme particulier. Vérifiez que l’URI de redirection est unique pour chaque plateforme que vous configurez.

    La page Configurer le site web s’affiche.

    > [!NOTE]
    > Les configurations seront différentes en fonction de la plateforme que vous sélectionnez.

1. Entrez les détails de configuration de la plateforme.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Configurer la plateforme web" border="true":::

    1. Entrez l’URI de redirection. L’URI doit être unique.
    2. Entrez l’URL de déconnexion du canal frontal.
    3. Sélectionnez les jetons que vous souhaitez qu’Azure AD envoie pour votre application.

1. Sélectionnez **Configurer**.

    La plateforme est configurée et affichée dans la page **Configurations** de la plateforme.

## <a name="acquire-access-token-for-ms-graph"></a>Acquérir un jeton d’accès pour MS Graph

Vous devez acquérir un jeton d’accès pour Microsoft Graph. Vous pouvez le faire à l’aide du flux OBO Azure AD.

L’implémentation actuelle de l’authentification unique accorde le consentement pour uniquement les autorisations au niveau de l’utilisateur qui ne sont pas utilisables pour effectuer des appels Graph. Pour obtenir les autorisations (étendues) nécessaires pour effectuer un appel Graph, les applications d’authentification unique doivent implémenter un service web personnalisé pour échanger le jeton reçu du Kit de développement logiciel (SDK) JavaScript Teams contre un jeton qui inclut les étendues nécessaires. Vous pouvez utiliser la bibliothèque d’authentification Microsoft (MSAL) pour extraire le jeton côté client.

Une fois que vous avez configuré les autorisations Graph dans Azure AD :

- [Configurer votre code côté client pour récupérer le jeton d’accès à l’aide de MSAL](#configure-code-to-fetch-access-token-using-msal)
- [Passer le jeton d’accès au code côté serveur](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>Configurer le code pour récupérer le jeton d’accès à l’aide de MSAL

Le code suivant fournit un exemple de flux OBO pour extraire le jeton d’accès du client Teams à l’aide de MSAL.

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```Node.js

// Exchange client Id side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenant id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```

---

### <a name="pass-the-access-token-to-server-side-code"></a>Passer le jeton d’accès au code côté serveur

Si vous devez accéder aux données Microsoft Graph, configurez votre code côté serveur pour :

1. Validez le jeton d’accès. Pour plus d’informations, voir [Valider le jeton d’accès](tab-sso-code.md#validate-the-access-token).
1. Lancez le flux OBO OAuth 2.0 avec un appel à la plateforme d’identités Microsoft qui inclut le jeton d’accès, certaines métadonnées sur l’utilisateur et les informations d’identification de l’application onglet (son ID d’application et sa clé secrète client). La plateforme d’identité Microsoft renverra un nouveau jeton d’accès qui peut être utilisé pour accéder à Microsoft Graph.
1. Obtenir des données à partir de Microsoft Graph en utilisant le nouveau jeton.
1. Utilisez la sérialisation du cache de jetons dans MSAL.NET pour mettre en cache le nouveau jeton d’accès pour plusieurs, si nécessaire.

> [!IMPORTANT]
> Pour des raisons de sécurité, utilisez toujours le code côté serveur pour effectuer des appels Microsoft Graph ou d’autres appels qui nécessitent le passage d’un jeton d’accès. Ne renvoyez jamais le jeton OBO au client pour permettre au client d’effectuer des appels directs vers Microsoft Graph. Cela aide à protéger le jeton contre l’interception ou la fuite.

## <a name="known-limitations"></a>Limitations connues

Consentement de l’administrateur client : un moyen simple de [donner son consentement au nom d’une organisation en tant qu’administrateur de locataire](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) consiste à obtenir [le consentement de l’administrateur](/azure/active-directory/manage-apps/grant-admin-consent).

Vous pouvez demander le consentement à l’aide de l’API d’authentification. Une autre approche pour obtenir des étendues Graph consiste à présenter une boîte de dialogue de consentement à l’aide de notre [approche d’authentification de fournisseur OAuth tierce](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page) existante. Cette approche implique l'affichage d'une boîte de dialogue de consentement Azure AD.

<details>
<summary>Pour demander un consentement supplémentaire à l'aide de l'API Auth, suivez ces étapes :</summary>

1. Le jeton récupéré à l’aide `getAuthToken()` doit être échangé côté serveur à l’aide [du flux on-behalf-of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Azure AD pour accéder à ces autres API Graph. Assurez-vous d'utiliser le point de terminaison v2 Graph pour cet échange.
2. Si l’échange échoue, Azure AD retourne une exception d’octroi non valide. Il répond généralement avec l’un des deux messages d’erreur, `invalid_grant` ou `interaction_required`.
3. Lorsque l'échange échoue, vous devez demander le consentement. Utilisez l’interface utilisateur pour demander à l’utilisateur de l’application d’accorder un autre consentement. Cette interface utilisateur doit inclure un bouton qui déclenche une boîte de dialogue de consentement Azure AD à l’aide de [l’authentification silencieuse](~/concepts/authentication/auth-silent-aad.md).
4. Lorsque vous demandez plus de consentement à Azure AD, vous devez inclure `prompt=consent` votre [paramètre de chaîne de requête](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) à Azure AD. Sinon, Azure AD ne demanderait pas d’autres étendues.
    - Au lieu de `?scope={scopes}`, utiliser `?prompt=consent&scope={scopes}`
    - Vérifiez que cela `{scopes}` inclut toutes les étendues pour lesquelles vous invitez l’utilisateur, par exemple, `Mail.Read` ou `User.Read`.
5. Une fois que l’utilisateur de l’application a accordé plus d’autorisations, réessayez le flux OBO pour accéder à ces autres API.

    </details>

## <a name="see-also"></a>Voir aussi

- [Flux On-Behalf-Of OAuth 2.0](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [Obtenir l’accès pour MS Graph](/graph/auth-v2-user)
- [Sérialisation du cache de jetons dans MSAL.NET](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
