---
title: Authentification unique
description: Décrit l’authentification unique (SSO)
keywords: API SSO d’authentification unique AAD pour l’authentification de teams
ms.openlocfilehash: 849e2c357859a1e8980aaa4662a55319cd7b2493
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021602"
---
# <a name="single-sign-on-sso"></a>Authentification unique (SSO)

> [!NOTE]
> * L’API d’authentification unique (SSO) est généralement disponible sur le Web et sur le bureau. Mobile sera bientôt disponible. En attendant, nous vous recommandons de revenir en douceur à notre [API d’authentification classique](auth-flow-tab.md) sur mobile.

Les utilisateurs se connectent à Microsoft teams par le biais de leurs comptes professionnels, scolaires ou Microsoft (Office 365, Outlook, etc.). Vous pouvez en tirer parti en autorisant une authentification unique pour autoriser l’utilisation de votre onglet Microsoft Teams (ou module tâches) sur des clients de bureau ou mobiles. Par conséquent, si un utilisateur consent à utiliser votre application, il n’aura pas à s’accorder à nouveau un consentement sur un autre appareil : il se connectera automatiquement. De plus, nous récupérons votre jeton d’accès pour améliorer les performances et les temps de chargement.

## <a name="how-sso-works-at-runtime"></a>Mode de fonctionnement de l’authentification unique SSO en cours d’exécution

Le diagramme suivant illustre le fonctionnement du processus d’authentification unique :

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. Dans l’onglet, un appel JavaScript est effectué vers `getAuthToken()` . Cette option indique à teams d’obtenir un jeton d’authentification pour l’application d’onglets.
2. S’il s’agit de la première fois que l’utilisateur actuel a utilisé votre application d’onglets, une invite de demande est adressée au consentement (si le consentement est requis) ou à la gestion de l’authentification par étape (par exemple, authentification à deux facteurs).
3. Teams demande le jeton d’application d’onglets du point de terminaison Azure AD pour l’utilisateur actuel.
4. Azure AD envoie le jeton d’application d’onglet à l’application Teams.
5. Teams envoie le jeton de l’application d’onglet à l’onglet dans le cadre de l’objet de résultat renvoyé par l' `getAuthToken()` appel.
6. Le jeton sera analysé dans l’application d’onglets, via JavaScript, pour extraire les informations nécessaires, telles que l’adresse de messagerie de l’utilisateur.

> [!NOTE]
> Le `getAuthToken()` n’est valide que pour l’envoi à un ensemble limité d’API de niveau utilisateur (e-mail, Profile, offline_access et OpenID), et non pour d’autres étendues Microsoft Graph telles que `User.Read` ou `Mail.Read` . Consultez notre section à la fin de ce document pour obtenir des solutions de contournement si vous avez besoin d' [autres étendues Graph](#apps-that-require-additional-microsoft-graph-scopes).

L’API SSO fonctionne également dans les [modules de tâches](../../../task-modules-and-cards/what-are-task-modules.md) qui incorporent le contenu Web.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Développer un onglet Microsoft teams SSO

Cette section décrit les tâches impliquées dans la création d’un onglet teams qui utilise l’authentification unique. Ces tâches sont décrites ici sont indépendantes de la langue et de l’infrastructure.

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. créer votre application Azure Active Directory (Azure AD)

Enregistrez votre application dans le[portail Azure ad](https://azure.microsoft.com/features/azure-portal/). Il s’agit d’un processus de 5 à 10 minutes qui inclut les tâches suivantes:

1. Obtenir l' [ID de votre application Azure ad](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
2. Spécifiez les autorisations dont votre application a besoin pour le point de terminaison Azure AD et, éventuellement, Microsoft Graph.
3. [Accorder des autorisations](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) pour les applications de bureau, Web et mobiles Teams.
4. Pré-autoriser teams en sélectionnant le bouton **Ajouter une étendue** et dans le panneau qui s’ouvre, entrez `access_as_user` comme **nom d’étendue**.

> [!NOTE]
> Vous devez tenir compte de certaines restrictions importantes :
>
> * Nous ne prenons en charge que les autorisations d’API Microsoft Graph de niveau utilisateur, c’est-à-dire la messagerie, le profil, le offline_access OpenId. Si vous avez besoin d’accéder à d’autres étendues Microsoft Graph (telles que `User.Read` ou `Mail.Read` ), consultez notre [solution de contournement recommandée](#apps-that-require-additional-microsoft-graph-scopes) à la fin de cette documentation.
> * Il est important que le nom de domaine de votre application soit le même que le nom de domaine que vous avez enregistré pour votre application Azure AD.
> * Nous ne prenons actuellement pas en charge plusieurs domaines par application.
> * Nous ne prenons pas en charge les applications qui utilisent le `azurewebsites.net` domaine car elles sont trop courantes et peuvent présenter un risque de sécurité. Toutefois, nous cherchons activement à supprimer cette restriction.

#### <a name="steps"></a>Étapes

1. Enregistrez une nouvelle application dans le portail [Azure Active Directory-inscriptions des applications](https://go.microsoft.com/fwlink/?linkid=2083908) .
2. Sélectionnez **nouvelle inscription** et, dans la *page inscrire une application*, définissez les valeurs suivantes :
    * Définissez **Name** sur le nom de votre application.
    * Choisissez les **types de comptes pris en charge** (tout type de compte fonctionne) ¹
    * Laissez **Redirect URI** vide.
    * Choisissez **Inscrire**.
3. Sur la page vue d’ensemble, copiez et enregistrez l’ID de l' **application (client)**. Vous en aurez besoin plus tard lors de la mise à jour de votre manifeste d’application Teams.
4. Sélectionnez **Exposer une API** sous **Gérer**. 
5. Sélectionnez le lien **définir** pour générer l’URI de l’ID de l’application sous la forme `api://{AppID}` . Insérez votre nom de domaine complet (avec une barre oblique « / » ajoutée à la fin) entre les deux barres obliques et le GUID. L’ID entier doit avoir la forme suivante : `api://fully-qualified-domain-name.com/{AppID}` ²
    * ex : `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
6. Sélectionnez le bouton **Ajouter une étendue**. Dans le volet qui s’ouvre, entrez `access_as_user` en tant que **nom de l’étendue**.
7. Définir **qui peut consentir ?**`Admins and users`
8. Renseignez les champs de configuration des invites d’administrateur et de consentement de l’utilisateur avec des valeurs appropriées pour l' `access_as_user` étendue :
    * **Titre du consentement administratif :** Les équipes peuvent accéder au profil de l’utilisateur.
    * **Description du consentement administratif**: permet à teams d’appeler les API Web de l’application en tant qu’utilisateur actuel.
    * **Titre du consentement**de l’utilisateur : teams peut accéder au profil utilisateur et faire des demandes au nom de l’utilisateur.
    * **Description du consentement de l’utilisateur :** Permettre aux équipes d’appeler les API de cette application avec les mêmes droits que l’utilisateur.
9. Vérifiez que l' **État** est défini sur **activé** .
10. Sélectionnez **Ajouter une étendue**
    * La partie domaine du **nom d’étendue** affiché juste en dessous du champ de texte doit correspondre automatiquement à l’URI d' **ID d’application** défini à l’étape précédente, avec `/access_as_user` ajouté à la fin :
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. Dans la section **applications clientes autorisées** , identifiez les applications que vous souhaitez autoriser pour l’application Web de votre application. Chacun des ID suivants doit être entré :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`(Team mobile/application de bureau)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`(Application Web Teams)
12. Accédez à **autorisations d’API**et assurez-vous d’ajouter les autorisations suivantes :
    * User. Read (activé par défaut)
    * email
    * offline_access
    * OpenId
    * profil

> [!NOTE]
>
> * ¹ si votre application Azure AD est inscrite dans le _même_ client que celui où vous effectuez une demande d’authentification dans Teams, l’utilisateur ne sera pas invité à accorder son consentement et recevra immédiatement un jeton d’accès. Les utilisateurs doivent uniquement accepter ces autorisations si l’application Azure AD est inscrite dans un autre client.
> * ² si vous obtenez une erreur indiquant que le domaine est déjà détenu et que vous êtes le propriétaire, suivez la procédure lors du [démarrage rapide : ajoutez un nom de domaine personnalisé à Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) pour inscrire le domaine, puis répétez l’étape 5, ci-dessus. (Cette erreur peut également se produire si vous n’êtes pas connecté avec des informations d’identification d’administrateur dans le client Office 365 location).
> * Si vous ne recevez pas l’UPN (nom d’utilisateur principal) dans le jeton d’accès renvoyé, vous pouvez l’ajouter en tant que [revendication facultative](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) dans Azure ad.

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. mettre à jour le manifeste de votre application Microsoft teams

Ajoutez de nouvelles propriétés à votre manifeste Microsoft teams :

* **WebApplicationInfo** -parent des éléments suivants :

> [!div class="checklist"]
> * **ID** : ID client de l’application. Il s’agit de l’ID d’application que vous avez obtenu dans le cadre de l’inscription de l’application auprès d’Azure AD.
>* **ressource** -le domaine et le sous-domaine de votre application. Il s’agit du même URI (y compris le `api://` protocole) que vous avez enregistré lors de la création `scope` de votre étape ci-dessus. Vous ne devez pas inclure le `access_as_user` chemin d’accès dans votre ressource. La partie domaine de cet URI doit correspondre au domaine, y compris à tous les sous-domaines, utilisés dans les URL de votre manifeste d’application Teams.

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* La ressource d’une application AAD correspond généralement à la racine de son URL de site et de l’appID (par exemple `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ,). Nous utilisons également cette valeur pour vous assurer que votre demande provient du même domaine. Par conséquent, assurez-vous que l' `contentURL` pour votre onglet utilise les mêmes domaines que votre propriété de ressource.
>* Vous devez utiliser le manifeste version 1,5 ou une version ultérieure pour implémenter le `webApplicationInfo` champ.

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. obtenir un jeton d’authentification à partir de votre code côté client

Voici à quoi ressemble l’API d’authentification :

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

Lorsque vous appelez, `getAuthToken` un consentement d’utilisateur supplémentaire est requis (pour les autorisations au niveau de l’utilisateur)-une boîte de dialogue s’affichera pour que l’utilisateur les encourage à accorder un consentement supplémentaire. 

Une fois que vous avez reçu le jeton d’accès dans le rappel de réussite, vous pouvez décoder le jeton d’accès pour afficher les revendications associées à ce jeton. (Si vous le souhaitez, vous pouvez copier/coller manuellement le jeton d’accès dans un outil tel que [JWT.IO](https://jwt.io/) pour inspecter son contenu). Si vous ne recevez pas l’UPN (nom d’utilisateur principal) dans le jeton d’accès renvoyé, vous pouvez l’ajouter en tant que [revendication facultative](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) dans Azure ad.

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a>Exemple de code

Consultez notre exemple d’application : [MSTeams Tabs SSO Sample-NodeJS](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)

Le fichier Lisez-moi décrit la configuration de votre environnement de développement et la configuration de votre application dans Azure AD. Vous pouvez également trouver des informations supplémentaires sur la façon dont l’exemple est structuré dans la [section structure](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) de l’application pour vous aider à vous familiariser avec le code base.

## <a name="known-limitations"></a>Limitations connues

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>Applications qui requièrent des étendues Microsoft Graph supplémentaires

Notre implémentation actuelle de SSO accorde uniquement le consentement pour les autorisations au niveau de l’utilisateur : e-mail, Profile, offline_access, OpenId, et non pour d’autres API (telles que User. Read ou mail. Read). Si votre application a besoin d’autres étendues Microsoft Graph, voici quelques solutions d’activation :

#### <a name="tenant-admin-consent"></a>Consentement de l’administrateur client

L’approche la plus simple consiste à obtenir de l’administrateur client le consentement préalable au nom de l’organisation. Cela signifie que les utilisateurs n’ont pas à consentir à ces étendues et vous pouvez alors être libre d’échanger le côté serveur de jetons à l’aide du flux de la [part de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)Azure ad. Cette solution de contournement est acceptable pour les applications métiers internes, mais peut ne pas suffire pour les développeurs tiers qui ne pourront pas compter sur l’approbation de l’administrateur client.

Une méthode simple d’envoi pour le compte d’une organisation (en tant qu’administrateur client) consiste à visiter :

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Demande de consentement supplémentaire à l’aide de l’API auth

Une autre approche pour obtenir des étendues Microsoft Graph supplémentaires consiste à présenter une boîte de dialogue de consentement à l’aide de notre [approche d’authentification Web Azure ad existante,](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) qui implique de faire apparaître une boîte de dialogue d’autorisation Azure ad. Il existe des ajouts notables :

1. Le jeton récupéré à l’aide de `getAuthToken()` doit être échangé côté serveur à l’aide du flux Azure ad [de la part de](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) pour accéder à ces API Microsoft Graph supplémentaires.
    * Veillez à utiliser le point de terminaison Microsoft Graph v2 pour ce Exchange.
2. Si l’échange échoue, Azure AD renvoie une exception Grant non valide. Il y a généralement l’un des deux messages d’erreur suivants : `invalid_grant` ou`interaction_required`
3. Lorsque l’échange échoue, vous devez demander un consentement supplémentaire. Nous vous recommandons d’afficher une interface utilisateur demandant à l’utilisateur d’accorder un consentement supplémentaire. Cette interface utilisateur doit inclure un bouton qui déclenche une boîte de dialogue d’autorisation Azure AD à l’aide de notre [API d’authentification Azure ad](~/concepts/authentication/auth-silent-aad.md).
4. Lorsque vous demandez un consentement supplémentaire d’Azure AD, vous devez inclure `prompt=consent` dans votre [paramètre de chaîne de requête](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) dans Azure ad, sinon Azure ad ne demandera pas les étendues supplémentaires.
    * Au lieu de:`?scope={scopes}`
    * Utilisez ce qui suit :`?prompt=consent&scope={scopes}`
    * Assurez- `{scopes}` vous que inclut toutes les étendues que vous invitez l’utilisateur (par exemple : mail. Read ou User. Read).
5. Une fois que l’utilisateur a accordé une autorisation supplémentaire, essayez de nouveau pour accéder à ces API supplémentaires.

### <a name="non-azure-ad-authentication"></a>Authentification AD non Azure

La solution d’authentification décrite ci-dessus fonctionne uniquement pour les applications et les services qui prennent en charge Azure Active Directory en tant que fournisseur d’identité. Les applications qui souhaitent s’authentifier à l’aide de services non Azure AD doivent continuer à utiliser le flux de l' [authentification Web](~/concepts/authentication.md)contextuelle.
