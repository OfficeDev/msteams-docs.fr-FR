---
title: Activer l’authentification à l’aide d’un fournisseur OAuth tiers
description: Découvrez le flux d’authentification Teams sous des onglets à l’aide d’un fournisseur OAuth tiers avec des exemples de code et de configuration Azure AD.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: c9969e154dae2f0d2439c1d8513af34970723e5c
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605039"
---
# <a name="enable-authentication-using-third-party-oauth-provider"></a>Activer l’authentification à l’aide d’un fournisseur OAuth tiers

Vous pouvez activer l’authentification dans votre application d’onglet à l’aide d’un fournisseurs d’identité (IdP) OAuth tiers. Dans cette méthode, l’identité de l’utilisateur de l’application est validée et l’accès est accordé par un fournisseur d’identité OAuth, tel que Azure AD, Google, Facebook, GitHub ou tout autre fournisseur. Vous devez configurer une relation d’approbation avec le fournisseur d’identité, et les utilisateurs de votre application doivent également être inscrits auprès de celui-ci.

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du Kit de développement logiciel (SDK) JavaScript Microsoft Teams.  
> Le Kit de développement logiciel (SDK) Teams lance une fenêtre distincte pour le flux d’authentification. Définissez l’attribut `SameSite` sur **lax**. Le client de bureau Teams ou les versions antérieures de Chrome ou Safari ne prennent pas en charge `SameSite`=None.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="use-oauth-idp-to-enable-authentication"></a>Utiliser le fournisseur d’identité OAuth pour activer l’authentification

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Microsoft Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base du flux d’octroi implicite OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans les onglets Microsoft Teams. Pour plus d’informations, consultez [OAuth 2 simplifié](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que la [spécification formelle](https://oauth.net/2/). Le flux d’authentification pour les onglets et les bots est différent, car les onglets sont similaires aux sites web afin qu’ils puissent utiliser OAuth 2.0 directement. Les bots effectuent quelques opérations différemment, mais les concepts de base sont identiques.

Par exemple, le flux d’authentification pour les onglets et les bots utilisant Node et le [type d’octroi implicite OAuth 2.0](https://oauth.net/2/grant-types/implicit/), consultez [lancer le flux d’authentification pour les onglets](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow).

Cette section utilise Azure AD comme exemple de fournisseur OAuth tiers pour activer l’authentification dans une application onglet.

> [!NOTE]
> Avant d’afficher un bouton **Login** à l’utilisateur et d’appeler l’API `authentication.authenticate` en réponse à la sélection du bouton, vous devez attendre la fin de l’initialisation du Kit de développement logiciel (SDK). Vous pouvez chaîner un `.then()` gestionnaire ou `await` pour que la `app.initialize()` fonction se termine.

![Diagramme de séquence d’authentification par tabulation](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. L’utilisateur interagit avec le contenu de la page de configuration ou de contenu de l’onglet, généralement un bouton de **connexion** ou de **connexion** .
2. L’onglet construit l’URL de sa page de démarrage d’authentification. Si vous le souhaitez, il utilise des informations provenant d’espaces réservés d’URL ou d’appels `app.getContext()` méthode du Kit de développement logiciel (SDK) client Teams pour simplifier l’expérience d’authentification de l’utilisateur. Par exemple, lors de l’authentification auprès d’Azure AD, si le `login_hint` paramètre est défini sur l’adresse e-mail de l’utilisateur, l’utilisateur n’a pas à se connecter s’il l’a fait récemment. Cela est dû au fait que Azure AD utilise les informations d’identification mises en cache de l’utilisateur. La fenêtre contextuelle s’affiche brièvement, puis disparaît.
3. L’onglet appelle ensuite la `authentication.authenticate()` méthode.
4. Teams ouvre la page de démarrage dans un iframe dans une fenêtre contextuelle. La page de démarrage génère des données de `state` aléatoires, les enregistre pour une validation ultérieure et les redirige vers le point de terminaison `/authorize` du fournisseur d’identité, tel que `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` pour Azure AD. Remplacez `<tenant id>` par votre propre ID de locataire qui est context.tid.
Comme pour les autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver sur un domaine figurant dans sa liste `validDomains` et sur le même domaine que la page de redirection de la publication de connexion.

    > [!NOTE]
    > Le flux d’octroi implicite OAuth 2.0 appelle un paramètre `state` dans la demande d’authentification, qui contient des données de session uniques pour empêcher une [attaque par falsification de requête intersites](https://en.wikipedia.org/wiki/Cross-site_request_forgery). Les exemples utilisent un GUID généré de manière aléatoire pour les données `state` .

5. Sur le site du fournisseur, l’utilisateur se connecte et accorde l’accès à l’onglet.
6. Le fournisseur dirige l’utilisateur vers la page de redirection OAuth 2.0 de l’onglet avec un jeton d’accès.
7. L’onglet vérifie que la valeur retournée `state` correspond à ce qui a été enregistré précédemment, et appelle `authentication.notifySuccess()`, qui à son tour appelle le gestionnaire de réussite (`.then()`) pour la méthode basée sur `authenticate()` la promesse de l’étape 3.
8. Teams ferme la fenêtre contextuelle.
9. L’onglet affiche l’interface utilisateur de configuration, actualise ou recharge le contenu des onglets, selon l’emplacement à partir duquel l’utilisateur a démarré.

> [!NOTE]
> Si l’application prend en charge l’authentification unique SAML, le jeton JWT généré par tabulation ne peut pas être utilisé, car il n’est pas pris en charge.

## <a name="treat-tab-context-as-hints"></a>Traiter le contexte de tabulation comme des indicateurs

Bien que le contexte de l’onglet fournisse des informations utiles concernant l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur. Authentifiez l’utilisateur même si vous obtenez les informations en tant que paramètres d’URL vers l’URL de contenu de votre onglet ou en appelant la fonction `app.getContext()` dans le Kit de développement logiciel (SDK) client Microsoft Teams. Un acteur malveillant peut appeler l’URL de contenu de votre onglet avec ses propres paramètres. L’acteur peut également appeler une page web empruntant l’identité de Microsoft Teams pour charger l’URL de contenu de votre onglet dans un iframe et retourner ses propres données à la fonction `getContext()` . Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet comme un indicateur et les valider avant de les utiliser. Reportez-vous aux notes de [accédez à la page d’autorisation à partir de votre page contextuelle](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page).

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification par onglet :

| **Exemple de nom** | **Description** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Authentification par onglet Teams | Processus d’authentification pour les onglets à l’aide de Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>Voir aussi

Pour obtenir une implémentation détaillée de l’authentification par onglet à l’aide de Azure AD, consultez :

* [authentifier un utilisateur dans un onglet Teams](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-AAD.md)
