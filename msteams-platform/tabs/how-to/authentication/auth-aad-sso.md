---
title: Prise en charge de l'authentification unique pour les onglets
description: Décrit l'authentification unique (SSO)
ms.topic: how-to
ms.localizationpriority: high
keywords: Authentification unique Teams Azure AD api d’authentification unique
ms.openlocfilehash: fd11f1febf1fb919a201a56156c36dfe1ee4d7d8
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212355"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Prise en charge de l'authentification unique (SSO) pour les onglets

Les utilisateurs se connectent à Microsoft Teams via leur compte professionnel, scolaire ou Microsoft Office 365, Outlook, vous pouvez profiter de l'avantage en autorisant une connexion unique pour autoriser votre onglet Teams ou votre module de tâches sur les clients de bureau ou mobiles. Si un utilisateur se connecte une fois, il n'a pas besoin de se reconnecter sur un autre appareil car il se connecte automatiquement. De plus, votre jeton d’accès est déjà pré-accessible pour améliorer les performances et les temps de chargement.

> [!NOTE]
> **Versions du client mobile Teams prenant en charge l'authentification unique**  
>
> ✔Teams pour Android (1416/1.0.0.2020073101 et versions ultérieures)
>
> ✔Teams pour iOS (_Version_: 2.0.18 et versions ultérieures)  
> 
> ✔Teams JavaScript SDK (_Version_: 1.10 et versions ultérieures) pour que SSO fonctionne dans le panneau latéral de la réunion. 
>
> Pour une expérience optimale avec Teams, utilisez la dernière version d'iOS et d'Android.

> [!NOTE]
> **Démarrage rapide**  
>
> Le chemin le plus simple pour démarrer avec l'onglet SSO est avec la boîte à outils Teams pour Visual Studio Code. Pour plus d'informations, consultez [SSO avec la boîte à outils Teams et Visual Studio Code pour les onglets](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Mode de fonctionnement de l’authentification unique SSO en cours d’exécution

L'image suivante montre comment fonctionne le processus SSO :

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. Dans l’onglet, un appel JavaScript est effectué pour `getAuthToken()`. `getAuthToken()` indique à Teams d'obtenir un jeton d'accès pour l'application de l'onglet.
2. Si l'utilisateur actuel utilise votre application d'onglet pour la première fois, il y a une invite de demande de consentement si le consentement est requis. Alternativement, il existe une invite de demande pour gérer l'authentification renforcée telle que l'authentification à deux facteurs.
3. Teams demande le jeton d’accès à l’onglet à partir du point de terminaison Azure Active Directory pour l’utilisateur actuel.
4. Azure AD envoie le jeton d’accès à l’onglet à l’application Teams.
5. Teams envoie le jeton d'accès à l'onglet à l'onglet dans le cadre de l'objet de résultat renvoyé par l'`getAuthToken()` appel.
6. Le jeton est analysé dans l’application de l’onglet à l’aide de JavaScript, afin d’extraire les informations requises, telles que l’adresse de l’utilisateur.

> [!NOTE]
> Le `getAuthToken()` n'est valide que pour consentir à un ensemble limité d'API au niveau de l'utilisateur, à savoir e-mail, profil, offline_access et OpenId. Il n'est pas utilisé pour d'autres étendues de Graph telles que `User.Read` ou `Mail.Read` . Pour des solutions de contournement suggérées, consultez [Obtenir un jeton d'accès avec des autorisations Graph](#get-an-access-token-with-graph-permissions).

L'API SSO fonctionne également dans les [modules de tâches](../../../task-modules-and-cards/what-are-task-modules.md) qui intègrent du contenu Web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Développer un onglet SSO Microsoft Teams

Cette section décrit les tâches impliquées dans la création d'un onglet Teams qui utilise SSO. Ces tâches sont indépendantes du langage et du framework.

### <a name="1-create-your-azure-ad-application"></a>1. Créer votre application Azure AD

> [!NOTE]
> Il existe certaines restrictions importantes que vous devez connaître :
>
> * Seules les autorisations de l'API Graph au niveau de l'utilisateur sont prises en charge, c'est-à-dire e-mail, profil, offline_access, OpenId. Si vous devez avoir accès à d'autres étendues Graph telles que `User.Read` ou `Mail.Read`, consultez [Obtenir un jeton d'accès avec des autorisations Graph](#get-an-access-token-with-graph-permissions).
> * Il est important que le nom de domaine de votre application soit identique au nom de domaine que vous avez inscrit pour votre application Azure AD.
> * Actuellement, plusieurs domaines par application ne sont pas pris en charge.
> * L’utilisateur doit définir `accessTokenAcceptedVersion` sur `2` pour une nouvelle application.

**Pour inscrire votre application via le portail Azure AD web**

1. Inscrivez une nouvelle application dans le portail [Inscriptions Azure AD App](https://go.microsoft.com/fwlink/?linkid=2083908).
1. Sélectionnez **Nouvelle inscription**. La page **Inscrire une application** s’affiche.
1. Dans la page **Inscrire une application**, entrez les valeurs suivantes :
    1. Entrez un **Nom** pour votre application.
    2. Choisissez les **Types de compte pris en charge**, sélectionnez le type de compte client unique ou multi-locataire. ¹
    * Laissez **Redirect URI** vide.
    3. Choisissez **Inscrire**.
1. Sur la page de présentation, copiez et enregistrez l'**ID d'application (client)**. Vous devez l'avoir plus tard lors de la mise à jour de votre manifeste d'application Teams.
1. Sélectionnez **Exposer une API** sous **Gérer**.

    > [!NOTE]
    > Si vous créez une application avec un bot et un onglet, saisissez l'URI de l'ID d'application au format `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Sélectionnez le lien **Définir** pour générer l'URI de l'ID d'application sous la forme `api://{AppID}`. Insérez votre nom de domaine complet avec une barre oblique "/" ajoutée à la fin, entre les doubles barres obliques et le GUID. L'ID complet doit avoir la forme `api://fully-qualified-domain-name.com/{AppID}`. ² Par exemple, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`. Le nom de domaine complet est le nom de domaine lisible par l'homme à partir duquel votre application est servie. Si vous utilisez un service de tunnellisation tel que ngrok, vous devez mettre à jour cette valeur chaque fois que votre sous-domaine ngrok change.
1. Sélectionnez **Ajouter une étendue**. Dans le panneau qui s'ouvre, entrez **access_as_user** comme **Nom de l'étendue**.
1. Dans la section **Qui peut consentir ?**, saisissez **Administrateurs et utilisateurs**.
1. Entrez les détails dans les cases pour configurer les invites de consentement de l'administrateur et de l'utilisateur avec des valeurs adaptées à l'`access_as_user` étendue :
    * **Titre du consentement de l’administrateur :** Teams peut accéder au profil de l’utilisateur.
    * **Description du consentement de l'administrateur** : les équipes peuvent appeler les API Web de l'application en tant qu'utilisateur actuel.
    * **Titre de consentement de l'utilisateur** : les équipes peuvent accéder à votre profil et faire des demandes en votre nom.
    * **Description du consentement de l'utilisateur :** Teams peuvent appeler les API de cette application avec les mêmes droits que vous.
1. Vérifiez que **State** est défini comme **Enabled**.
1. Sélectionnez **Ajouter une étendue** pour enregistrer les détails. La partie domaine du **nom de l'étendue** affichée sous le champ de texte doit automatiquement correspondre à l'URI de l'**ID d'application** défini à l'étape précédente, avec `/access_as_user` ajouté à la fin `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.
1. Dans la section **Applications clientes autorisées**, identifiez les applications que vous souhaitez autoriser pour l'application Web de votre application. Sélectionnez **Ajouter une application cliente**. Entrez chacun des ID client suivants et sélectionnez la portée autorisée que vous avez créée à l'étape précédente :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` pour l'application mobile ou de bureau Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` pour l'application Web Teams.
1. Accédez à **Autorisations API**. Sélectionnez **Ajouter une autorisation** > **Microsoft Graph** > **Autorisations déléguées**, puis ajoutez les autorisations suivantes à partir de l'API Graph :
    * User.Read activé par défaut
    * email
    * offline_access
    * OpenID
    * profil

1. Accédez à **Authentification**.

    > [!IMPORTANT]
    > Si une application n'a pas reçu le consentement de l'administrateur informatique, les utilisateurs doivent donner leur consentement la première fois qu'ils utilisent une application.

    Pour saisir un URI de redirection :
    * Sélectionnez **Ajouter une plateforme**.
    * Sélectionnez **Web**.
    * Entrez l’**URI de redirection** de votre application. Cet URI est le même nom de domaine complet que vous avez entré à l'étape 5. Il est également suivi de la route API où une réponse d'authentification est envoyée. Si vous suivez l'un des exemples Teams, l'URI est `https://subdomain.example.com/auth-end`. Pour plus d'informations, consultez [Flux de code d'autorisation OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    > [!NOTE]
    > L'octroi implicite n'est pas requis pour l'onglet SSO.

Félicitations ! Vous avez rempli les conditions préalables d'enregistrement de l'application pour continuer avec votre application SSO d'onglet.

> [!NOTE]
>
> * ¹ Si votre application Azure AD est inscrite dans le même locataire que celui où vous effectuez une demande d’authentification dans Teams, l’utilisateur ne peut pas être invité à donner son consentement et se voit accorder immédiatement un jeton d’accès. Les utilisateurs consentent uniquement à ces autorisations si l’application Azure AD est inscrite dans un autre locataire.
> * ² Si le domaine personnalisé n’est pas ajouté à Azure AD, vous obtenez une erreur indiquant que le nom d’hôte ne doit pas être basé sur un domaine déjà détenu. Pour ajouter un domaine personnalisé à Azure AD et l’inscrire, suivez la procédure[ajoutez un nom de domaine personnalisé à Azure AD](/azure/active-directory/fundamentals/add-custom-domain), puis répétez l’étape 5. Vous pouvez également obtenir cette erreur si vous n'êtes pas connecté avec des informations d'identification d'administrateur dans la location Office 365.
> * Si vous ne recevez pas le nom d’utilisateur principal (UPN) dans le jeton d’accès retourné, vous pouvez l’ajouter en tant que [revendication facultative](/azure/active-directory/develop/active-directory-optional-claims)dans Azure AD.

### <a name="2-update-your-teams-application-manifest"></a>2. Mettez à jour le manifeste de votre application Teams

Utilisez le code suivant pour ajouter de nouvelles propriétés à votre manifeste Teams :

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** est le parent des éléments suivants :

> [!div class="checklist"]
> * **id** – ID client de l'application. Il s'agit de l'ID d'application que vous avez obtenu lors de l'inscription de l'application auprès d'Azure AD.
>* **ressource** – Le domaine et le sous-domaine de votre application. Il s'agit du même URI (y compris le `api://` protocole) que vous avez enregistré lors de la création de votre `scope` à l'étape 6. Vous ne devez pas inclure le `access_as_user` chemin dans votre ressource. La partie domaine de cet URI doit correspondre au domaine, y compris les sous-domaines, utilisés dans les URL de votre manifeste d'application Teams.

> [!NOTE]
>
>* La ressource d’une application Azure AD est généralement la racine de son URL de site et de l’ID d’application (par exemple, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`). Cette valeur est également utilisée pour garantir que votre demande provient du même domaine. Assurez-vous que le `contentURL` pour votre onglet utilise les mêmes domaines que votre propriété de ressource.
>* Vous devez utiliser la version 1.5 ou supérieure du manifeste pour implémenter le `webApplicationInfo` champ.

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. Obtenez un jeton d'accès à partir de votre code côté client

Utilisez l'API d'authentification suivante :

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Lorsque vous appelez `getAuthToken` et que le consentement de l'utilisateur est requis pour les autorisations au niveau de l'utilisateur, une boîte de dialogue s'affiche pour que l'utilisateur accorde son consentement.

Après avoir reçu le jeton d'accès dans le rappel de réussite, décodez le jeton d'accès pour afficher les revendications de ce jeton. Si vous le souhaitez, copiez et collez manuellement le jeton d'accès dans un outil, tel que [jwt.ms](https://jwt.ms/). Si vous ne recevez pas l’UPN dans le jeton d’accès retourné, ajoutez-le en tant que [revendication facultative](/azure/active-directory/develop/active-directory-optional-claims) dans Azure AD. Pour plus d'informations, consultez [jetons d'accès](/azure/active-directory/develop/access-tokens).

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-snippets"></a>Extraits de code

Le code suivant fournit un exemple de flux on-behalf-of pour récupérer le jeton d’accès à l’aide de la bibliothèque MSAL :

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

```javascript

// Exchange cliend side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenand id" >
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

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom**|**Description**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| Onglet SSO |Exemple d'application Microsoft Teams pour les onglets Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs) </br>[Toolkit Teams](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitations connues

### <a name="get-an-access-token-with-graph-permissions"></a>Obtenir un jeton d'accès avec les autorisations Graph

Notre implémentation actuelle pour SSO n'accorde le consentement que pour les autorisations au niveau de l'utilisateur qui ne sont pas utilisables pour effectuer des appels Graph. Pour obtenir les autorisations (étendues) nécessaires pour effectuer un appel Graph, les solutions SSO doivent implémenter un service Web personnalisé pour échanger le jeton reçu du SDK JavaScript Teams contre un jeton qui inclut les étendues nécessaires. Pour ce faire, utilisez le[flux on-behalf-of](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)Azure AD.

### <a name="tenant-admin-consent"></a>Consentement de l'administrateur du locataire

Un moyen simple de consentir au nom d'une organisation en tant qu'administrateur client consiste à se référer à `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`.

#### <a name="ask-for-consent-using-the-auth-api"></a>Demander le consentement à l'aide de l'API Auth

Une autre approche pour obtenir des étendues Graph consiste à présenter une boîte de dialogue de consentement à l'aide de notre [approche d'authentification Azure AD existante basée sur le Web](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page). Cette approche implique l'affichage d'une boîte de dialogue de consentement Azure AD.

**Pour demander un consentement supplémentaire à l'aide de l'API Auth**

1. Le jeton récupéré à l’aide de `getAuthToken()` doit être échangé côté serveur à l’aide du[flux on-behalf-of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Azure AD pour obtenir l’accès à ces autres API Graph. Assurez-vous d'utiliser le point de terminaison v2 Graph pour cet échange.
2. Si l’échange échoue, Azure AD retourne une exception d’octroi non valide. Il y a généralement l'un des deux messages d'erreur, `invalid_grant` ou `interaction_required`.
3. Lorsque l'échange échoue, vous devez demander le consentement. Afficher une interface utilisateur (UI) demandant à l'utilisateur d'accorder un autre consentement. Cette interface utilisateur doit inclure un bouton qui déclenche une boîte de dialogue de consentement Azure AD à l’aide de notre [API d’authentification Azure AD](~/concepts/authentication/auth-silent-aad.md).
4. Lorsque vous demandez un consentement supplémentaire à Azure AD, vous devez inclure `prompt=consent`dans votre [paramètre query-string](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) à Azure AD, sinon Azure AD ne demande pas les autres scopes.
    * Au lieu de `?scope={scopes}`
    * Utilisez ceci `?prompt=consent&scope={scopes}`
    * Assurez-vous que cela `{scopes}` inclut toutes les étendues pour lesquelles vous demandez à l'utilisateur, par exemple, Mail.Read ou User.Read.
5. Une fois que l'utilisateur a accordé plus d'autorisations, réessayez le flux au nom de pour accéder à ces autres API.

### <a name="non-azure-ad-authentication"></a>Authentification non Azure AD

La solution d’authentification décrite ci-dessus fonctionne uniquement pour les applications et les services qui prennent en charge Azure AD en tant que fournisseur d’identité. Les applications qui souhaitent s’authentifier à l’aide de services non Azure AD doivent continuer à utiliser le flux d’authentification web [contextuel](~/concepts/authentication.md).

> [!NOTE]
> L’authentification unique est prise en charge pour les applications appartenant au client au sein des locataires Azure AD B2C.

## <a name="step-by-step-guides"></a>Guides détaillés

* Suivez le [guide détaillé](../../../sbs-tabs-and-messaging-extensions-with-sso.yml) pour authentifier les onglets et les extensions de messagerie.
* Suivez le [guide détaillé](../../../sbs-tab-with-adaptive-cards.yml) pour créer un onglet avec des cartes adaptatives.

## <a name="see-also"></a>Voir aussi
[Teams Bot avec authentification unique](../../../sbs-bots-with-sso.yml)
