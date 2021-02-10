---
title: Prise en charge de l' sign-on unique pour les onglets
description: Décrit l' sign-on unique (SSO)
ms.topic: how-to
keywords: Api d’authentification unique SSO AAD d’authentification teams
ms.openlocfilehash: 72fbafe49e021b0cc23dcdaeee7eb5fe82ee23de
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162886"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>Prise en charge de l' sign-on unique (SSO) pour les onglets

Les utilisateurs se connectent à Microsoft Teams via leurs comptes professionnels, scolaires ou Microsoft (Office 365, Outlook, etc.). Vous pouvez en tirer parti en permettant à une sign-on unique d’autoriser votre onglet Microsoft Teams (ou module de tâche) sur les clients de bureau ou mobiles. Par conséquent, si un utilisateur consent à utiliser votre application, il n’aura pas à consentir à nouveau sur un autre appareil ; il sera connecté automatiquement. En outre, nous préréfions votre jeton d’accès pour améliorer les performances et les temps de chargement.

> [!NOTE]
> **Versions des clients mobiles Teams qui la prise en charge de l' sso**  
>
> ✔Teams pour Android (1416/1.0.0.2020073101 et ultérieures)
>
> ✔Teams pour iOS (_Version_: 2.0.18 et versions ultérieures)  
>
> Pour une expérience améliorée avec Teams, utilisez la dernière version d’iOS et Android.

> [!NOTE]
> **Démarrage rapide**  
>
> Le chemin d’accès le plus simple à la mise en route de l' sso tabulation est avec l’outil Microsoft Teams Shared Computer Toolkit pour Visual Studio Code. [En savoir plus](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>Mode de fonctionnement de l’authentification unique SSO en cours d’exécution

Le diagramme suivant illustre le fonctionnement du processus d' clés s’il s’agit :

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. Dans l’onglet, un appel JavaScript est effectué vers `getAuthToken()` . Cela indique à Teams d’obtenir un jeton d’authentification pour l’application onglet.
2. S’il s’agit de la première fois que l’utilisateur actuel utilise votre application d’onglet, une invite de demande de consentement (si le consentement est requis) ou de gérer l’authentification par étapes (par exemple, l’authentification à deux facteurs).
3. Teams demande le jeton d’application d’onglet au point de terminaison Azure AD pour l’utilisateur actuel.
4. Azure AD envoie le jeton d’application d’onglet à l’application Teams.
5. Teams envoie le jeton d’application d’onglet à l’onglet dans le cadre de l’objet de résultat renvoyé par `getAuthToken()` l’appel.
6. Le jeton est alors paré dans l’application d’onglet, via JavaScript, pour extraire les informations nécessaires, telles que l’adresse e-mail de l’utilisateur.

> [!NOTE]
> L’autorisation est uniquement valide pour consentir à un ensemble limité d’API de niveau utilisateur (messagerie, profil, offline_access et OpenId) et non pour d’autres `getAuthToken()` étendues Microsoft Graph telles que ou `User.Read` `Mail.Read` . Consultez notre section à la fin de ce document pour obtenir des solutions de contournement suggérées si vous avez besoin d’étendues [Graph supplémentaires.](#apps-that-require-additional-microsoft-graph-scopes)

L’API DSO fonctionne également dans les [modules de tâche](../../../task-modules-and-cards/what-are-task-modules.md) qui incorporent du contenu web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Développer un onglet SSO Microsoft Teams

Cette section décrit les tâches impliquées dans la création d’un onglet Teams qui utilise l' sso. Ces tâches sont décrites ici sans langue et sans infrastructure.

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. Créer votre application Azure Active Directory (Azure AD)

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>Inscription de votre application dans la vue[d’ensemble du portail Azure AD](https://azure.microsoft.com/features/azure-portal/) :

1. Obtenez votre [ID d’application Azure AD.](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)
2. Spécifiez les autorisations dont votre application a besoin pour le point de terminaison Azure AD et, éventuellement, Microsoft Graph.
3. [Accorder des autorisations](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) pour les applications de bureau, web et mobiles Teams.
4. Pré-autoriser Teams en sélectionnant le bouton Ajouter une étendue et dans le panneau qui s’ouvre, entrez le nom de  `access_as_user` **l’étendue.**

> [!NOTE]
> Vous devez connaître certaines restrictions importantes :
>
> * Nous 5 000 000 000 d’autorisations d’API Microsoft Graph au niveau de l’utilisateur, c’est-à-dire, e-mail, profil, offline_access, OpenId. Si vous avez besoin d’accéder à d’autres étendues Microsoft Graph (par exemple, ou ), consultez notre solution de contournement recommandée à la `User.Read` `Mail.Read` fin de cette documentation. [](#apps-that-require-additional-microsoft-graph-scopes)
> * Il est important que le nom de domaine de votre application soit identique au nom de domaine que vous avez inscrit pour votre application Azure AD.
> * Pour l’instant, nous ne prisent pas en charge plusieurs domaines par application.
> * Nous ne ons pas prendre en charge les applications qui utilisent le domaine, car il est trop courant et `azurewebsites.net` peut être un risque pour la sécurité. Toutefois, nous cherchons activement à supprimer cette restriction.

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>Inscription détaillée de votre application via le portail Azure Active Directory :

1. Inscrivez une nouvelle application dans [le portail Azure Active Directory – App Registrations.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Sélectionnez **Nouvelle inscription** et dans la page Inscrire *une application,* définissez les valeurs suivantes :
    * Définissez **le** nom sur le nom de votre application.
    * Choisir les **types de comptes pris en** charge (n’importe quel type de compte fonctionne) ¹
    * Laissez **Redirect URI** vide.
    * Choisissez **Inscrire**.
3. Dans la page vue d’ensemble, copiez et enregistrez **l’ID de l’application (client).** Vous en aurez besoin ultérieurement lors de la mise à jour du manifeste de votre application Teams.
4. Sélectionnez **Exposer une API** sous **Gérer**. 
5. Sélectionnez **le lien** Définir pour générer l’URI d’ID d’application sous la forme `api://{AppID}` . Insérez votre nom de domaine complet (avec une barre oblique « / » à la fin) entre les doubles barres obliques et le GUID. L’ID entier doit avoir la forme : `api://fully-qualified-domain-name.com/{AppID}` ²
    * ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
    
    Le nom de domaine complet est le nom de domaine lisible par l’homme à partir duquel votre application est servie. Si vous utilisez un service de tunneling tel que ngrok, vous devez mettre à jour cette valeur chaque fois que votre sous-domaine ngrok change. 
6. Sélectionnez le bouton **Ajouter une étendue**. Dans le volet qui s’ouvre, entrez `access_as_user` en tant que **nom de l’étendue**.
7. Définir **qui peut donner son consentement ?**`Admins and users`
8. Remplissez les champs pour configurer les invites de consentement de l’administrateur et de l’utilisateur avec des valeurs appropriées pour `access_as_user` l’étendue :
    * **Titre du consentement de l’administrateur :** Teams peut accéder au profil de l’utilisateur.
    * **Description du consentement de** l’administrateur : permet à Teams d’appeler les API web de l’application en tant qu’utilisateur actuel.
    * **Titre du consentement de l’utilisateur**: Teams peut accéder au profil utilisateur et effectuer des demandes au nom de l’utilisateur.
    * **Description du consentement de l’utilisateur :** Autorisez Teams à appeler les API de cette application avec les mêmes droits que l’utilisateur.
9. S’assurer **que l’état** **est** activé
10. Sélectionnez le **bouton Ajouter une étendue** à enregistrer 
    * La partie domaine  du nom d’étendue affichée juste en dessous du champ de texte doit automatiquement correspondre à l’URI **d’ID** d’application définie à l’étape précédente, avec ajouté à `/access_as_user` la fin :
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. Dans la section **Applications clientes autorisées,** identifiez les applications que vous souhaitez autoriser pour l’application web de votre application. Sélectionnez *Ajouter une application cliente.* Entrez chacun des ID client suivants et sélectionnez l’étendue autorisée que vous avez créée à l’étape précédente :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Application mobile/de bureau Teams)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Application web Teams)
12. Accédez aux **autorisations d’API.** Sélectionnez *Ajouter une autorisation Autorisation*  >  déléguée Microsoft *Graph,* puis ajoutez les autorisations suivantes à partir de  >  l’API Microsoft Graph :
    * User.Read (activé par défaut)
    * email
    * offline_access
    * OpenId
    * profil

13. Accéder à **l’authentification**

    Si une application n’a pas reçu le consentement de l’administrateur informatique, les utilisateurs doivent donner leur consentement la première fois qu’ils utilisent une application.

    Définissez un URI de redirection :
    * Sélectionnez **Ajouter une plateforme.**
    * Sélectionnez **web**.
    * Entrez **l’URI de redirection** de votre application. Il s’agit de la page dans laquelle un flux d’octroi implicite réussi redirige l’utilisateur. Il s’agit du même nom de domaine complet que celui que vous avez entré à l’étape 5, suivi de l’itinéraire d’API où une réponse d’authentification doit être envoyée. Si vous êtes en cours de suivi de l’un des exemples Teams, ce sera : `https://subdomain.example.com/auth-end`

    Ensuite, activez l’octroi implicite en cochant les cases suivantes :  
    jeton ✔ ID de l'✔  
    jeton ✔ d’accès  
    
Félicitations ! Vous avez rempli les conditions préalables à l’inscription de l’application pour poursuivre l’application d' ces onglets.     

> [!NOTE]
>
> * ¹ Si votre application Azure AD  est inscrite dans le même client que celui où vous faites une demande d’authentification dans Teams, l’utilisateur ne sera pas invité à donner son consentement et un jeton d’accès lui sera immédiatement accordé. Les utilisateurs doivent uniquement consentir à ces autorisations si l’application Azure AD est inscrite dans un autre client.
> * ² If you get an error stating that the domain is already owned and you are the owner, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register the domain, and then repeat step 5, above. (Cette erreur peut également se produire si vous n’êtes pas signé avec des informations d’identification d’administrateur dans la location Office 365).
> * Si vous ne recevez pas l’UPN (nom d’utilisateur principal) dans le jeton d’accès renvoyé, vous pouvez l’ajouter en tant que revendication facultative [dans](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) Azure AD.

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. Mettre à jour votre manifeste d’application Microsoft Teams

Ajoutez de nouvelles propriétés à votre manifeste Microsoft Teams :

* **WebApplicationInfo** : parent des éléments suivants :

> [!div class="checklist"]
> * **id** : ID client de l’application. Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès d’Azure AD.
>* **ressource** : domaine et sous-domaine de votre application. Il s’agit du même URI (y compris le protocole) que vous avez enregistré lors de la création de votre à `api://` `scope` l’étape 6 ci-dessus. Vous ne devez pas inclure le `access_as_user` chemin d’accès dans votre ressource. La partie domaine de cet URI doit correspondre au domaine, y compris les sous-domaines, utilisés dans les URL de votre manifeste d’application Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* La ressource d’une application AAD est généralement la racine de son URL de site et de l’appID (par exemple, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ). Nous utilisons également cette valeur pour nous assurer que votre demande est provenant du même domaine. Par conséquent, assurez-vous que l’onglet utilise `contentURL` les mêmes domaines que votre propriété de ressource.
>* Vous devez utiliser la version de manifeste 1.5 ou une version supérieure pour implémenter le `webApplicationInfo` champ.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. Obtenir un jeton d’authentification à partir de votre code côté client

Voici à quoi ressemble l’API d’authentification :

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Lorsque vous appelez et que le consentement de l’utilisateur supplémentaire est requis (pour les autorisations au niveau de l’utilisateur), nous montrons une boîte de dialogue à l’utilisateur pour l’inciter à accorder un `getAuthToken` consentement supplémentaire. 

Une fois que vous avez reçu le jeton d’accès dans le rappel de réussite, vous pouvez décoder le jeton d’accès pour afficher les revendications associées à ce jeton. (Si vous le souhaitez, vous pouvez copier/coller manuellement le jeton d’accès dans un outil tel que [JWT.io](https://jwt.io/) pour inspecter son contenu). Si vous ne recevez pas l’UPN (nom d’utilisateur principal) dans le jeton d’accès renvoyé, vous pouvez l’ajouter en tant que revendication facultative [dans](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) Azure AD.

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom**|**Description**|**C#**|**TypeScript**|
|---------------|---------------|------|--------------|
| SSO d’onglet |Exemple d’application Microsoft Teams pour les onglets Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[Affichage,](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs) </br>[Équipes Shared Computer Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>Limitations connues

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>Applications qui nécessitent des étendues Microsoft Graph supplémentaires

Notre implémentation actuelle pour l' utilisateur unique accorde uniquement le consentement pour les autorisations au niveau de l’utilisateur (e-mail, profil, offline_access, OpenId) et non pour d’autres API (par exemple, User.Read ou Mail.Read). Si votre application a besoin d’autres étendues Microsoft Graph, voici quelques solutions de contournement permettant d’y répondre :

#### <a name="tenant-admin-consent"></a>Consentement de l’administrateur client

L’approche la plus simple consiste à obtenir le consentement préalable d’un administrateur client au nom de l’organisation. Cela signifie que les utilisateurs n’auront pas à consentir à ces étendues et [](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)que vous pouvez ensuite être libre d’échanger le côté serveur de jetons à l’aide du flux De la part d’Azure AD. Cette solution de contournement est acceptable pour les applications métier internes, mais peut ne pas être suffisante pour les développeurs tiers qui ne peuvent pas s’appuyer sur l’approbation de l’administrateur client.

Une méthode simple de consentement au nom d’une organisation (en tant qu’administrateur client) consiste à visiter :

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Demande de consentement supplémentaire à l’aide de l’API Auth

Une autre approche pour obtenir des étendues Microsoft Graph supplémentaires consiste à présenter une boîte de dialogue de consentement à l’aide de notre approche d’authentification [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) basée sur le web existante qui implique l’obtention d’une boîte de dialogue de consentement Azure AD. Il existe quelques ajouts notables :

1. Le jeton récupéré à l’aide doit être échangé côté serveur à l’aide du flux Azure AD de la part de pour accéder à ces API `getAuthToken()` Microsoft Graph supplémentaires. [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
    * N’oubliez pas d’utiliser le point de terminaison Microsoft Graph v2 pour cet échange
2. Si l’échange échoue, Azure AD retourne une exception d’octroi non valide. Il existe généralement l’un des deux messages `invalid_grant` d’erreur : ou `interaction_required`
3. En cas d’échec de l’échange, vous devez demander un consentement supplémentaire. Nous vous recommandons d’afficher une interface utilisateur demandant à l’utilisateur d’accorder un consentement supplémentaire. Cette interface utilisateur doit inclure un bouton qui déclenche une boîte de dialogue de consentement Azure AD à l’aide de notre API d’authentification [Azure AD.](~/concepts/authentication/auth-silent-aad.md)
4. Lorsque vous demandez un consentement supplémentaire d’Azure AD, vous devez inclure dans votre paramètre de chaîne de requête à Azure AD, sinon Azure AD ne demandera pas les `prompt=consent` étendues supplémentaires. [](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)
    * Au lieu de: `?scope={scopes}`
    * Utilisez ceci : `?prompt=consent&scope={scopes}`
    * Assurez-vous qu’elle inclut toutes les étendues que vous invitez à l’utilisateur (par exemple `{scopes}` : Mail.Read ou User.Read).
5. Une fois que l’utilisateur a accordé des autorisations supplémentaires, réessayez le flux « de la part de » pour accéder à ces API supplémentaires.

### <a name="non-azure-ad-authentication"></a>Authentification non Azure AD

La solution d’authentification décrite ci-dessus fonctionne uniquement pour les applications et les services qui utilisent Azure AD en tant que fournisseur d’identité. Les applications qui souhaitent s’authentifier à l’aide de services non Azure AD doivent continuer à utiliser le flux d’authentification web basé sur les fenêtres [pop-up.](~/concepts/authentication.md)

> [!NOTE] 
> L’ation SSO est prise en charge pour les applications du client au sein des clients Azure AD B2C.
