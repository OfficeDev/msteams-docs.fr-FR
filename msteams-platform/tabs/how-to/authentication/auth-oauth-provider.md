---
title: Utiliser des fournisseurs OAuth externes
description: Décrit l’authentification à l’aide de fournisseurs OAuth externes
ms.topic: how-to
ms.localizationpriority: high
keywords: Authentification Teams à l’aide d’un fournisseur OAuth externe
ms.openlocfilehash: c9327eb731d537d0f4eff04cc381a883bde5d98e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2022
ms.locfileid: "63360522"
---
# <a name="use-external-oauth-providers"></a>Utiliser des fournisseurs OAuth externes

Vous pouvez prendre en charge des fournisseurs OAuth externes ou tiers (3P), tels que Google, GitHub, LinkedIn et Facebook en utilisant l’API `authenticate()` mise à jour :

```JavaScript
function authenticate(authenticateParameters?: AuthenticateParameters)
``` 

Les éléments suivants sont ajoutés à l’API `authenticate()` pour prendre en charge les fournisseurs OAuth externes :

* Paramètre `isExternal`
* Deux valeurs d’espace réservé dans le paramètre `url` existant

Le tableau suivant fournit la liste des paramètres et fonctions de l’API `authenticate()`, ainsi que leur description :

| Paramètre| Description|
| --- | --- |
|`isExternal` | Le type de paramètre est booléen, ce qui indique que la fenêtre d’authentification s’ouvre dans un navigateur externe.|
|`failureCallback`| La fonction est appelée si l’authentification échoue et que la fenêtre contextuelle d’authentification indique la raison de l’échec.|
|`height` |Hauteur préférée pour la fenêtre contextuelle. La valeur peut être ignorée en dehors des limites acceptables.|
|`successCallback`| La fonction est appelée si l’authentification réussit, avec le résultat renvoyé à partir de la fenêtre contextuelle d’authentification. Authcode est le résultat.|
|`url`  <br>|URL du serveur d’applications 3P pour la fenêtre contextuelle d’authentification, avec les deux espaces réservés de paramètre suivants :</br> <br> - `oauthRedirectMethod`: transmettre l’espace réservé dans `{}`. Cet espace réservé est remplacé par un lien profond ou une page web par une plateforme Teams, qui informe le serveur d’applications si l’appel provient de la plateforme mobile.</br> <br> - `authId`: Cet espace réservé est remplacé par UUID. Le serveur d’applications l’utilise pour conserver la session.| 
|`width`|Largeur préférée pour la fenêtre contextuelle. La valeur peut être ignorée en dehors des limites acceptables.|

Pour plus d’informations sur les paramètres, voir [interface des paramètres d’authentification](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true).

## <a name="add-authentication-to-external-browsers"></a>Ajouter l’authentification à des navigateurs externes

> [!NOTE]
> * Actuellement, vous pouvez ajouter l’authentification à des navigateurs externes pour les onglets dans des mobiles uniquement. 
> * Utilisez la version bêta du Kit de développement logiciel (SDK) pour tirer parti des fonctionnalités. Les versions bêta sont disponibles via [NPM](https://www.npmjs.com/package/@microsoft/teams-js/v/1.12.0-beta.2).

L’image suivante fournit le flux pour ajouter l’authentification aux navigateurs externes :

 :::image type="content" source="../../../assets/images/tabs/tabs-authenticate-OAuth.PNG" alt-text="authenticate-OAuth" border="true":::

### <a name="steps-to-perform-authentication-to-external-browsers"></a>Procédure pour effectuer l’authentification sur les navigateurs externes

<!-- #### 1. Pass `isExternal` and placeholders in `url` -->
**1. Lancer le processus auth-login externe**

L’application 3P appelle la fonction `microsoftTeams.authentication.authenticate` du Kit de développement logiciel (SDK) avec `isExternal` défini sur true pour lancer le processus auth-login externe. 

Le `url` transmis contient des espaces réservés pour `{authId}` et `{oauthRedirectMethod}`.  


```JavaScript
microsoftTeams.authentication.authenticate({
   url: 'https://3p.app.server/auth?oauthRedirectMethod={oauthRedirectMethod}&authId={authId}',
   isExternal: true,
   successCallback: function (result) {
   //sucess 
   } failureCallback: function (reason) {
   //failure 
    }
});
```

**2. Lien Teams dans un navigateur externe**

Les clients Teams ouvrir l’URL dans un navigateur externe après avoir remplacé les espaces réservés pour `oauthRedirectMethod` et `authId` par des valeurs appropriées. 

#### <a name="example"></a>Exemple

```http
 https://3p.app.server/auth?oauthRedirectMethod=deeplink&authId=1234567890 
```

**3. Réponse du serveur d’applications 3P**

Le serveur d’applications 3P reçoit et enregistre `url` avec les deux paramètres de requête suivants :

| Paramètre | Description|
| --- | --- |
| `oauthRedirectMethod` |Indique comment l’application 3P doit renvoyer la réponse de la demande d’authentification à Teams, avec l’une des deux valeurs : lien profond ou page.|
|`authId` | L’ID de demande que Teams a créé pour cette demande d’authentification spécifique qui doit être renvoyée à Teams via un lien profond.|

> [!TIP]
> L’application 3P peut maintenir `authId`, `oauthRedirectMethod` dans le paramètre de requête `state` OAuth lors de la génération de l’URL de connexion pour OAuthProvider. `state` contient `authId` et `oauthRedirectMethod` transmis lorsque OAuthProvider redirige vers le serveur 3P et que l’application 3P utilise les valeurs pour renvoyer la réponse d’authentification à Teams comme décrit dans **6. Réponse du serveur d’applications 3P à Teams**. 

**4. Le serveur d’applications 3P redirige vers `url`** spécifié

Le serveur d’applications 3P redirige vers la page d’authentification des fournisseurs OAuth dans le navigateur externe. `redirect_uri` est un itinéraire dédié sur le serveur d’applications 3P. Vous pouvez inscrire `redirect_uri` dans la console de développement du fournisseur OAuth en tant que statique. Les paramètres doivent être envoyés via l’objet d’état. 

#### <a name="example"></a>Exemple

```http
https://accounts.google.com/o/oauth2/v2/auth?redirect_uri=https://3p.app.server/authredirect&state={"authId":"…","oauthRedirectMethod":"…"}&client_id=…&response_type=code&access_type=offline&scope= … 
```

**5. Connexion au navigateur externe**

L’utilisateur se connecte au navigateur externe. Les fournisseurs OAuth redirigent vers `redirect_uri` avec le code d’authentification et l’objet d’état.

**6. Réponse du serveur d’applications 3P à Teams** 

Le serveur d’applications 3P gère la réponse et vérifie `oauthRedirectMethod`, qui est renvoyé par le fournisseur OAuth externe dans l’objet d’état pour déterminer si la réponse doit être renvoyée via un lien profond auth-callback ou par le biais d’une page web qui appelle `notifySuccess()`.

```JavaScript
const state = JSON.parse(req.query.state)
if (state.oauthRedirectMethod === 'deeplink') {
   return res.redirect('msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&code=${req.query.code}')
}
else {
// continue redirecting to a web-page that will call notifySuccsss() – usually this method is used in Teams-Web
…
```

**7. L’application 3P génère un lien profond**

L’application 3P génère un lien profond pour Teams mobile au format suivant et renvoie le code d’authentification avec l’ID de session à Teams.
 
```JavaScript
return res.redirect(`msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&code=${req.query.code}`)
```

 **8. Résultats de rappel de réussite Teams**

Teams appelle le rappel de réussite et envoie le résultat (code d’authentification) à l’application 3P. L’application 3P reçoit le code dans le rappel de réussite et utilise le code pour récupérer le jeton, puis les informations utilisateur et mettre à jour l’interface utilisateur.

```JavaScript
successCallback: function (result) { 
… 
} 
```

## <a name="see-also"></a>Voir aussi

* [Configurer les fournisseurs d’identité](../../../concepts/authentication/configure-identity-provider.md)
* [Flux d’authentification Microsoft Teams pour les onglets](auth-flow-tab.md)