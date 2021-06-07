---
title: Prise en charge de l' sign-on unique pour les onglets
description: Décrit l' sign-on unique (SSO)
ms.topic: how-to
localization_priority: Normal
keywords: Api d’authentification unique SSO AAD d’authentification teams
ms.openlocfilehash: 681481d4d4f764c260729d37d7b5f5f2ce58d0ec
ms.sourcegitcommit: d9274ac2f32880e861b206ac6ce29467d631177f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2021
ms.locfileid: "52760880"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Prise en charge de l' sign-on unique (SSO) pour les onglets

Les utilisateurs se connectent Microsoft Teams via leurs comptes professionnels, scolaires ou Microsoft qui sont Office 365, Outlook, etc. Vous pouvez en tirer parti en permettant à une sign-on unique d’autoriser votre onglet Teams ou module de tâche sur les clients de bureau ou mobiles. Si un utilisateur consent à utiliser votre application, il n’a pas à consentir à nouveau sur un autre appareil, car il est connecté automatiquement. En outre, votre jeton d’accès est préréférable pour améliorer les performances et les temps de chargement.

> [!NOTE]
> **Teams versions de client mobile avec prise en charge de l' sso**  
>
> ✔Teams pour Android (1416/1.0.0.2020073101 et ultérieures)
>
> ✔Teams pour iOS (_Version_: 2.0.18 et versions ultérieures)  
>
> Pour une expérience de Teams, utilisez la dernière version d’iOS et Android.

> [!NOTE]
> **Démarrage rapide**  
>
> Le chemin d’accès le plus simple à la mise en route de l' sso tabulation est d’utiliser le kit Teams outils pour Visual Studio Code. Pour plus d’informations, [voir SSO avec Teams toolkit et Visual Studio Code pour les onglets](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Mode de fonctionnement de l’authentification unique SSO en cours d’exécution

L’image suivante illustre le fonctionnement du processus DSO :

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. Dans l’onglet, un appel JavaScript est effectué pour `getAuthToken()`. Cela indique Teams obtenir un jeton d’authentification pour l’application onglet.
2. Si c’est la première fois que l’utilisateur actuel utilise votre application d’onglet, une invite de demande de consentement s’impose ou permet de gérer l’authentification par étapes, telle que l’authentification à deux facteurs.
3. Teams demande le jeton d’application d’onglet Azure Active Directory point de terminaison (AAD) pour l’utilisateur actuel.
4. AAD envoie le jeton d’application d’onglet à l Teams application.
5. Teams envoie le jeton d’application d’onglet à l’onglet dans le cadre de l’objet de résultat renvoyé par `getAuthToken()` l’appel.
6. Le jeton est analysé dans l’application de l’onglet à l’aide de JavaScript, afin d’extraire les informations requises, telles que l’adresse de l’utilisateur.

> [!NOTE]
> La licence n’est valide que pour donner son consentement à un ensemble limité d’API au niveau de l’utilisateur , à savoir la messagerie, le `getAuthToken()` profil, offline_access et OpenId. Il n’est pas utilisé pour d’autres Graph étendues telles que `User.Read` ou `Mail.Read` . Pour obtenir des solutions de contournement suggérées, voir [les Graph supplémentaires.](#apps-that-require-additional-graph-scopes)

L’API DSO fonctionne également dans les [modules de tâche](../../../task-modules-and-cards/what-are-task-modules.md) qui incorporent du contenu web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Développer un onglet d’Microsoft Teams sso

Cette section décrit les tâches impliquées dans la création d’un onglet Teams qui utilise l' sso. Ces tâches sont spécifiques à la langue et à l’infrastructure.

### <a name="1-create-your-aad-application"></a>1. Créer votre application AAD

**Pour inscrire votre application dans la vue [d’ensemble du portail AAD](https://azure.microsoft.com/features/azure-portal/)**

1. Obtenez votre [ID d’application AAD.](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) 
1. Spécifiez les autorisations dont votre application a besoin pour le point de terminaison AAD et, éventuellement, Graph.
1. [Accordez des autorisations](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) Teams applications mobiles, web et de bureau.
1. Pré-autoriser les Teams en sélectionnant  le bouton Ajouter une étendue et dans le panneau qui s’ouvre, entrez **access_as_user** comme nom **d’étendue.**

> [!NOTE]
> Vous devez connaître certaines restrictions importantes :
>
> * Seules les autorisations d’API Graph niveau utilisateur sont pris en charge, à l’image, e-mail, profil, offline_access, OpenId. Si vous devez avoir accès à d’Graph étendues telles que ou , voir `User.Read` `Mail.Read` la solution de [contournement recommandée.](#apps-that-require-additional-graph-scopes)
> * Il est important que le nom de domaine de votre application soit identique au nom de domaine que vous avez enregistré pour votre application AAD.
> * Actuellement, plusieurs domaines par application ne sont pas pris en charge.

**Pour inscrire votre application via le portail AAD**

1. Inscrivez une nouvelle application dans le portail [d’inscription des applications AAD.](https://go.microsoft.com/fwlink/?linkid=2083908)
1. Sélectionnez **Nouvelle inscription**. La page **Inscrire une application** s’affiche.
1. Dans la page **Inscrire une application,** entrez les valeurs suivantes :
    1. Entrez un **nom** pour votre application.
    2. Choisissez les **types de comptes pris en** charge, sélectionnez le type de compte client unique ou multi-locataire. ¹
    * Laissez **Redirect URI** vide.
    3. Choisissez **Inscrire**.
1. Dans la page vue d’ensemble, copiez et enregistrez **l’ID de l’application (client).** Vous devez l’avoir ultérieurement lors de la mise à jour Teams manifeste de l’application.
1. Sélectionnez **Exposer une API** sous **Gérer**.

    > [!NOTE]
    > Si vous construisez une application avec un bot et un onglet, entrez l’URI d’ID d’application sous le nom `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

1. Sélectionnez **le lien** Définir pour générer l’URI d’ID d’application sous la forme `api://{AppID}` . Insérez votre nom de domaine complet avec une barre oblique « / » à la fin, entre les doubles barres obliques et le GUID. L’ID entier doit avoir la forme de `api://fully-qualified-domain-name.com/{AppID}` . ² Par exemple, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` . Le nom de domaine complet est le nom de domaine lisible par l’homme à partir duquel votre application est servie. Si vous utilisez un service de tunneling tel que ngrok, vous devez mettre à jour cette valeur chaque fois que votre sous-domaine ngrok change.
1. Sélectionnez **Ajouter une étendue**. Dans le panneau qui s’ouvre, **entrez access_as_user** comme **nom d’étendue.**
1. In the **Qui can consent?** box, enter **Admins and users**.
1. Entrez les détails dans les zones pour configurer les invites de consentement de l’administrateur et de l’utilisateur avec des valeurs appropriées pour `access_as_user` l’étendue :
    * **Titre du consentement de l’administrateur :** Teams peut accéder au profil de l’utilisateur.
    * **Description du consentement de** l’administrateur : Teams peut appeler les API web de l’application en tant qu’utilisateur actuel.
    * **Titre de consentement utilisateur**: Teams pouvez accéder à votre profil et effectuer des demandes en votre nom.
    * **Description du consentement de l’utilisateur** : Teams pouvez appeler les API de cette application avec les mêmes droits que vous.
1. Vérifiez que **State** est défini comme **Enabled**.
1. Sélectionnez **Ajouter une étendue** pour enregistrer les détails. La partie domaine  du nom d’étendue affichée sous le champ de texte doit automatiquement correspondre à l’URI **d’ID** d’application définie à l’étape précédente, avec ajouté à `/access_as_user` la `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` fin.
1. Dans la section **Applications clientes autorisées,** identifiez les applications que vous souhaitez autoriser pour l’application web de votre application. Sélectionnez **Ajouter une application cliente.** Entrez chacun des ID clients suivants et sélectionnez l’étendue autorisée que vous avez créée à l’étape précédente :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`pour Teams application mobile ou de bureau.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`pour Teams application web.
1. Accédez aux **autorisations d’API.** Sélectionnez **Ajouter une autorisation** Microsoft  >  **Graph**  >  **autorisations déléguées,** puis ajoutez les autorisations suivantes à partir Graph API :
    * User.Read activé par défaut
    * email
    * offline_access
    * OpenId
    * profil

1. Accédez à **l’authentification.**

    Si une application n’a pas reçu le consentement de l’administrateur informatique, les utilisateurs doivent donner leur consentement la première fois qu’ils utilisent une application.

    Pour entrer un URI de redirection :
    * Sélectionnez **Ajouter une plateforme.**
    * Sélectionnez **web**.
    * Entrez **l’URI de redirection** de votre application. Il s’agit de la page dans laquelle un flux d’octroi implicite réussi redirige l’utilisateur. Il s’agit du même nom de domaine complet que celui que vous avez entré à l’étape 5, suivi de l’itinéraire d’API où une réponse d’authentification est envoyée. Si vous êtes en cours de suivi de l’un Teams exemples, il s’agit de `https://subdomain.example.com/auth-end` .

    Activez l’octroi implicite en cochant les cases suivantes : ✔ ID de ✔'accès

Félicitations ! Vous avez rempli les conditions préalables à l’inscription de l’application pour poursuivre l’application d' ces onglets.

> [!NOTE]
>
> * ¹ Si votre application AAD est inscrite dans le même client que celui où vous faites une demande d’authentification dans Teams, l’utilisateur ne peut pas être invité à donner son consentement et un jeton d’accès lui est accordé immédiatement. Les utilisateurs consentent uniquement à ces autorisations si l’application AAD est inscrite dans un autre client.
> * ² Si le domaine personnalisé n’est pas ajouté à AAD, vous obtenez une erreur indiquant que le nom d’hôte ne doit pas être basé sur un domaine déjà propriétaire. Pour ajouter un domaine personnalisé à AAD et l’enregistrer, suivez la procédure d’ajout d’un nom de domaine personnalisé à [la procédure AAD,](/azure/active-directory/fundamentals/add-custom-domain) puis répétez l’étape 5. Vous pouvez également obtenir cette erreur si vous n’êtes pas signé avec des informations d’identification d’administrateur dans Office 365 location.
> * Si vous ne recevez pas le nom d’utilisateur principal (UPN) dans le jeton d’accès renvoyé, vous pouvez l’ajouter en tant que revendication facultative [dans](/azure/active-directory/develop/active-directory-optional-claims) AAD.

### <a name="2-update-your-teams-application-manifest"></a>2. Mettre à jour votre manifeste Teams’application

Utilisez le code suivant pour ajouter de nouvelles propriétés à Teams manifeste :

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** est le parent des éléments suivants :

> [!div class="checklist"]
> * **id** : ID client de l’application. Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès d’Azure AD.
>* **ressource** : domaine et sous-domaine de votre application. Il s’agit du même URI (y compris le protocole) que vous avez enregistré lors de la création de votre étape `api://` `scope` 6. Vous ne devez pas inclure le `access_as_user` chemin d’accès dans votre ressource. La partie domaine de cet URI doit correspondre au domaine, y compris les sous-domaines, utilisés dans les URL de votre manifeste d Teams’application.

> [!NOTE]
>
>* La ressource d’une application AAD est généralement la racine de son URL de site et de l’appID (par exemple, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ). Cette valeur est également utilisée pour vous assurer que votre demande est provenant du même domaine. Assurez-vous `contentURL` que l’onglet utilise les mêmes domaines que votre propriété de ressource.
>* Vous devez utiliser la version de manifeste 1.5 ou une version supérieure pour implémenter le `webApplicationInfo` champ.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. Obtenir un jeton d’authentification à partir de votre code côté client

Utilisez l’API d’authentification suivante :

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Lorsque vous appelez et que le consentement de l’utilisateur supplémentaire est requis pour les autorisations au niveau de l’utilisateur, une boîte de dialogue s’affiche pour accorder un `getAuthToken` consentement supplémentaire.

Après avoir reçu le jeton d’accès dans le rappel de réussite, vous pouvez décoder le jeton d’accès pour afficher les revendications associées à ce jeton. Si vous le souhaitez, vous pouvez copier et coller manuellement le jeton d’accès dans un outil, par exemple jwt.ms [pour](https://jwt.ms/) inspecter son contenu. Si vous ne recevez pas l’UPN dans le jeton d’accès renvoyé, vous pouvez l’ajouter en tant que [revendication facultative](/azure/active-directory/develop/active-directory-optional-claims) dans AAD.

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom**|**Description**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| SSO d’onglet |Microsoft Teams exemple d’application pour les onglets Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Affichage,](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs) </br>[Teams Shared Computer Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitations connues

### <a name="apps-that-require-additional-graph-scopes"></a>Applications qui nécessitent des étendues Graph supplémentaires

Notre implémentation actuelle pour l' utilisateur unique accorde uniquement le consentement pour les autorisations au niveau de l’utilisateur ( e-mail, profil, offline_access, OpenId et non pour d’autres API telles que User.Read ou Mail.Read). Si votre application a besoin d’Graph étendues supplémentaires, la section suivante fournit des solutions de contournement.

#### <a name="tenant-admin-consent"></a>Consentement de l’administrateur client

L’approche la plus simple consiste à obtenir le consentement préalable d’un administrateur client au nom de l’organisation. Cela signifie que les utilisateurs n’ont pas à consentir à ces étendues et [](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)que vous pouvez ensuite être libre d’échanger le côté serveur de jetons à l’aide du flux de la part d’AAD. Cette solution de contournement est acceptable pour les applications métier internes, mais pas pour les développeurs tiers qui ne peuvent pas compter sur l’approbation de l’administrateur client.

Une méthode simple de consentement pour le compte d’une organisation en tant qu’administrateur client consiste à faire référence à `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` .

#### <a name="ask-for-additional-consent-using-the-auth-api"></a>Demander un consentement supplémentaire à l’aide de l’API Auth

Une autre approche pour obtenir des étendues Graph supplémentaires consiste à présenter une boîte de dialogue de consentement à l’aide de notre approche d’authentification [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) basée sur le web existante qui implique l’obtention d’une boîte de dialogue de consentement Azure AD. 

**Pour demander un consentement supplémentaire à l’aide de l’API Auth**

1. Le jeton récupéré à l’aide doit être échangé côté serveur à l’aide du flux AAD de la part de pour accéder à ces API Graph `getAuthToken()` supplémentaires. [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Veillez à utiliser le point de terminaison Graph v2 pour cet échange.
2. Si l’échange échoue, AAD renvoie une exception d’octroi non valide. Il existe généralement l’un des deux messages `invalid_grant` d’erreur, ou `interaction_required` .
3. En cas d’échec de l’échange, vous devez demander un consentement supplémentaire. Affichez une interface utilisateur (IU) demandant à l’utilisateur d’accorder un consentement supplémentaire. Cette interface utilisateur doit inclure un bouton qui déclenche une boîte de dialogue de consentement AAD à l’aide de notre [API d’authentification AAD.](~/concepts/authentication/auth-silent-aad.md)
4. Lorsque vous demandez le consentement supplémentaire d’AAD, vous devez inclure dans votre paramètre de chaîne de requête à AAD, sinon AAD ne demande pas les `prompt=consent` étendues supplémentaires. [](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)
    * Au lieu de `?scope={scopes}`
    * Utilisez cette `?prompt=consent&scope={scopes}`
    * Assurez-vous qu’il inclut toutes les étendues que vous invitez à l’utilisateur, par `{scopes}` exemple, Mail.Read ou User.Read.
5. Une fois que l’utilisateur a accordé des autorisations supplémentaires, réessayez le flux « de la part de » pour accéder à ces API supplémentaires.

### <a name="non-aad-authentication"></a>Authentification non-AAD

La solution d’authentification décrite ci-dessus fonctionne uniquement pour les applications et services qui utilisent AAD en tant que fournisseur d’identité. Les applications qui souhaitent s’authentifier à l’aide de services non basés sur AAD doivent continuer à utiliser le flux d’authentification web basé sur les fenêtres [pop-up.](~/concepts/authentication.md)

> [!NOTE]
> L' sso est prise en charge pour les applications du client au sein des clients AAD B2C.
