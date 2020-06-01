---
title: Authentification unique
description: Décrit l’authentification unique (SSO)
keywords: AAD SSO d’authentification des équipes
ms.openlocfilehash: 8f9d94346aad7c096e4310f80b6cda73856afc8c
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455512"
---
# <a name="single-sign-on"></a>Authentification unique

> [!NOTE]
> L’API d’authentification unique est actuellement prise en charge en _mode aperçu_ pour les développeurs uniquement.

Les utilisateurs se connectent à Microsoft teams à l’aide de leur compte professionnel ou scolaire (Office 365) et vous pouvez en tirer parti à l’aide de l’authentification unique (SSO) pour autoriser l’utilisateur à accéder à votre onglet Microsoft Teams. Cela signifie que si un utilisateur consent à utiliser votre application sur le bureau, il n’aura pas à se le consentir sur mobile et sera automatiquement connecté. 

## <a name="how-sso-works-at-runtime"></a>Mode de fonctionnement de l’authentification unique SSO en cours d’exécution

Le diagramme suivant illustre le fonctionnement du processus d’authentification unique :

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. Dans l’onglet, JavaScript appelle getAuthToken (). Cette option indique à l’application teams d’obtenir un jeton d’authentification pour l’application d’onglets.
2. S’il s’agit de la première fois que l’utilisateur actuel a utilisé votre application d’onglets, ils seront invités à consentir (si un consentement est requis) ou doivent gérer l’authentification par étape (par exemple, authentification à deux facteurs).
3. L’application Microsoft teams demande le jeton d’application d’onglets du point de terminaison Azure AD v 1.0 pour l’utilisateur actuel.
4. Azure AD envoie le jeton d’application d’onglet à l’application Teams.
5. L’application Microsoft teams envoie le jeton de l’application d’onglet à l’onglet dans le cadre de l’objet result renvoyé par l’appel getAuthToken ().
6. JavaScript dans l’application d’onglets peut analyser le jeton et extraire les informations dont il a besoin, telles que l’adresse de messagerie de l’utilisateur.
    * Remarque : ce jeton n’est valide que pour l’envoi à un ensemble limité d’API de niveau utilisateur (par exemple : e-mail, Profile, etc.) et non pour d’autres étendues de graphique (comme mail. Read). Consultez notre section à la fin de ce document pour obtenir des solutions de contournement si vous avez besoin d’autres étendues Graph.

## <a name="develop-an-sso-microsoft-teams-tab"></a>Développer un onglet Microsoft teams SSO

Cette section décrit les tâches impliquées dans la création d’un onglet Microsoft teams qui utilisent l’authentification unique. Ces tâches sont décrites ici indépendamment du langage et de l’infrastructure.

### <a name="1-create-your-aad-application-in-azure"></a>1. créer votre application AAD dans Azure

Inscrivez votre application sur le portail d’inscription pour le point de terminaison Azure AD v 1.0. Il s’agit d’un processus de 5 à 10 minutes qui inclut les tâches suivantes:

* Obtention de votre ID d’application AAD
* Spécifiez les autorisations dont votre application a besoin pour le point de terminaison AAD (et éventuellement pour Microsoft Graph). 
* Accorder à l’application Microsoft teams de bureau, Web et mobile une approbation pour votre application
* Pré-autorisez l’application Microsoft teams dans votre application avec le nom d’étendue par défaut `access_as_user` .

> [!NOTE]
> Vous devez tenir compte de certaines restrictions importantes :
>
> * Nous ne prenons en charge que les autorisations d’API graphique au niveau utilisateur, par exemple, email, Profile, offline_access, OpenID. Si vous avez besoin d’accéder à d’autres étendues Graph, lisez notre solution de contournement recommandée à la fin de cette documentation.
> * Il est important que le nom de domaine de votre application soit enregistré avec votre application Azure AD. Il doit s’agir du même nom de domaine que celui sur lequel votre application s’exécute lors de la demande d’un jeton d’authentification dans Teams, ainsi que de la spécification de la propriété de ressource dans votre manifeste Teams (plus d’informations dans la section suivante).
> * Nous ne prenons actuellement pas en charge plusieurs domaines par application
> * Nous ne prenons pas en charge les applications qui utilisent le `azurewebsites.net` domaine car ce domaine est trop courant et peuvent présenter un risque de sécurité.

#### <a name="steps"></a>Étapes

1. Enregistrer une nouvelle application dans [Azure Active Directory – portail d’inscription des applications](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Sélectionnez nouvelle inscription. Sur la page inscrire une application, définissez les valeurs comme suit :
    * Définir le **nom** de votre application
    * Définir les types de comptes **pris en charge** sur **les comptes de tous les comptes d’annuaire et de Microsoft personnels**
    * Laisser l' **URI de redirection** vide
    * Sélectionnez **Enregistrer**
3. Sur la page vue d’ensemble, copiez et enregistrez l’ID de l' **application (client)**. Vous en aurez besoin plus tard lors de la mise à jour de votre manifeste d’application Teams.
4. Sélectionnez **Exposer une API** sous **Gérer**. Sélectionnez le lien **définir** pour générer l’URI de l’ID de l’application sous la forme `api://{AppID}` . Insérez votre nom de domaine complet (avec une barre oblique « / » ajoutée à la fin) entre les deux barres obliques et le GUID. L’ID entier doit avoir la forme suivante :`api://fully-qualified-domain-name.com/{AppID}`
    * ex : `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` .

> [!NOTE]
> Si un message d’erreur s’affiche indiquant que le domaine appartient déjà à quelqu’un et que c’est vous qui en êtes le propriétaire, suivez la procédure décrite dans Quickstart [ : Ajouter votre nom de domaine personnalisé à l’aide du Portail Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) pour l’inscrire, puis répétez cette étape. (Cette erreur peut également se produire si vous n’êtes pas connecté avec des informations d’identification d’un administrateur dans le client Office 365 location).

5. Sélectionnez le bouton **Ajouter une étendue**. Dans le volet qui s’ouvre, entrez `access_as_user` en tant que **nom de l’étendue**.
6. Définir qui peut consentir ? pour les administrateurs et les utilisateurs
7. Renseignez les champs de configuration des invites de l’administrateur et du consentement de l’utilisateur avec des valeurs appropriées pour l' `access_as_user` étendue. Suggestions :
    * **Titre du consentement administratif :** Les équipes peuvent accéder au profil de l’utilisateur
    * **Description du consentement administratif**: permet à teams d’appeler les API Web de l’application en tant qu’utilisateur actuel.
    * **Titre du consentement**de l’utilisateur : teams peut accéder à votre profil utilisateur et faire des demandes à votre place.
    * **Description du consentement de l’utilisateur :** Permettre aux équipes d’appeler les API de cette application avec les mêmes droits que ceux que vous avez
8. Vérifiez que l' **État** est défini sur **activé** .
9. Sélectionnez **Ajouter une étendue**
    * Remarque : la partie domaine du **nom d’étendue** affiché juste en dessous du champ de texte doit correspondre automatiquement à l’URI d' **ID d’application** défini à l’étape précédente, avec `/access_as_user` ajouté à la fin, par exemple : 
        * `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`
10. Dans la section **applications clientes autorisées** , vous identifiez les applications que vous souhaitez autoriser dans l’application Web de votre application. Chacun des ID suivants doit être entré :
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`(Team mobile/application de bureau)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`(Application Web Teams)
11. Accédez à **autorisations d’API**et assurez-vous d’ajouter les autorisations suivantes :
    * User. Read (activé par défaut)
    * email
    * offline_access
    * openid
    * profil

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. mettre à jour le manifeste de votre application Microsoft teams

Ajoutez de nouvelles propriétés à votre manifeste Microsoft teams :

* **WebApplicationInfo**: le parent des éléments suivants.
* **ID** : ID client de l’application. Il s’agit d’un ID d’application que vous obtenez dans le cadre de l’inscription de l’application avec le point de terminaison Azure AD 1,0.
* **Ressource** -le domaine et le sous-domaine de votre application. Il s’agit du même URI (y compris le `api://` protocole) que vous avez utilisé lors de l’inscription de l’application dans AAD. La partie domaine de cet URI doit correspondre au domaine, y compris à tous les sous-domaines, utilisés dans les URL de la section du manifeste de votre application Teams.

```json
"webApplicationInfo": {
  "id": "<application_GUID here>",
  "resource": "<web_API resource here>"
}
```

Remarques :

* La ressource pour une application AAD sera généralement la racine de son URL de site et de l’appID (par exemple `api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` ). Nous utilisons également cette valeur pour vous assurer que votre demande provient du même domaine. Pour ce faire, vérifiez que votre `contentURL` onglet utilise les mêmes domaines que votre propriété de ressource.
* Vous devez utiliser le manifeste version 1,5 ou une version ultérieure pour que ces champs soient utilisés.
* Les étendues ne sont pas prises en charge dans le manifeste et doivent plutôt être spécifiées dans la section des autorisations d’API dans le portail Azure.

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

<img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>

## <a name="demo-code"></a>Code de démonstration

Pour l’instant, vous pouvez accéder à notre [tâche](https://github.com/ydogandjiev/taskmeow) d’application de test Meow et utiliser le manifeste SSO et extraire le `teams.auth.service.js` `sso.auth.service.js` fichier et pour voir comment nous manipulons le flux de travail d’authentification.

## <a name="known-limitations"></a>Limitations connues

### <a name="apps-that-require-additional-graph-scopes"></a>Applications qui requièrent des étendues Graph supplémentaires

Notre implémentation actuelle de l’authentification unique accorde uniquement le consentement pour les autorisations au niveau de l’utilisateur (courrier électronique, profil, offline_access, OpenID), mais pas pour les autres API (telles que mail. Read). Si votre application a besoin d’autres étendues de graphique, il existe des solutions de contournement pour l’activer.

#### <a name="tenant-admin-consent"></a>Consentement de l’administrateur client

L’approche la plus simple consisterait à obtenir de l’administrateur client le consentement préalable au nom de l’organisation. Cela signifie que les utilisateurs n’ont pas à consentir à ces étendues et vous pouvez alors être libre d’échanger le côté serveur de jetons à l’aide du flux de la [part de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)AAD. Cette solution de contournement est acceptable pour les applications métiers internes, mais peut ne pas suffire pour les éditeurs de logiciels indépendants qui ne peuvent pas compter sur l’approbation de l’administrateur client.

Une méthode simple d’envoi pour le compte d’une organisation (en tant qu’administrateur client) consiste à visiter :

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Demande de consentement supplémentaire à l’aide de l’API auth

Une autre approche pour obtenir des étendues Graph supplémentaires serait de présenter une boîte de dialogue de consentement à l’aide de notre [approche d’authentification AAD basée sur le Web existante,](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) qui implique de faire apparaître une boîte de dialogue de consentement AAD. Il existe des ajouts notables :

1. Le jeton récupéré à l’aide de getAuthToken doit être échangé côté serveur à l’aide [du flux de la part de](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow) AADS pour accéder à ces API Graph supplémentaires.
    * Veillez à utiliser le point de terminaison Graph v2 pour ce Exchange
2. Si l’échange échoue, AAD renvoie une exception Grant non valide. Il y a généralement l’un des deux messages d’erreur suivants : `ConsentRequired` ou`InteractionRequired`
3. Lorsque l’échange échoue, vous devez demander un consentement supplémentaire. Nous vous recommandons d’afficher une interface utilisateur demandant à l’utilisateur d’accorder un consentement supplémentaire. Cette interface utilisateur doit inclure un bouton qui déclenche une boîte de dialogue de consentement AAD à l’aide de notre [API d’authentification AAD](~/concepts/authentication/auth-silent-aad.md).
4. Lorsque vous demandez un consentement supplémentaire de AAD, vous devez inclure `prompt=consent` dans votre [paramètre de chaîne de requête](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) dans AAD sinon AAD ne demande pas les étendues supplémentaires.
    * Au lieu de:`?scope={scopes}`
    * Utilisez ce qui suit :`?prompt=consent&scope={scopes}`
    * Assurez- `{scopes}` vous que inclut toutes les étendues que vous invitez l’utilisateur (par exemple : mail. Read ou User. Read).
5. Une fois que l’utilisateur a accordé une autorisation supplémentaire, essayez de nouveau pour accéder à ces API supplémentaires.

### <a name="non-aad-authentication"></a>Authentification non AAD

La solution d’authentification décrite ci-dessus fonctionne uniquement pour les applications et les services qui prennent en charge Azure Active Directory en tant que fournisseur d’identité. Les applications qui souhaitent s’authentifier à l’aide de services non AAD doivent continuer à utiliser le [flux d’authentification Web](~/concepts/authentication.md)en fenêtre contextuelle.
