---
title: Flux d’authentification pour les onglets
description: Décrit le flux d’authentification dans les onglets, OAuth par Azure AD et fournit un exemple de code
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Onglets de flux d’authentification Teams
ms.openlocfilehash: c0a3617332d3392c36f21645d4fb0074008ced40
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821373"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teams’authentification pour les onglets

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du SDK JavaScript Microsoft Teams.  
> Teams SDK ouvre une fenêtre distincte pour le flux d’authentification. Définissez l’attribut `SameSite` **sur Lax**. Teams client de bureau ou des versions antérieures de Chrome ou Safari ne sont pas en charge `SameSite`=Aucun.

OAuth 2.0 est une norme ouverte d’authentification et d’autorisation utilisée par Microsoft Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams. Pour plus d’informations, [voir OAuth 2 simplifié](https://aaronparecki.com/oauth-2-simplified/) et plus facile à suivre que la [spécification formelle](https://oauth.net/2/). Le flux d’authentification pour les onglets et les bots est différent, car les onglets sont similaires aux sites web afin qu’ils peuvent utiliser OAuth 2.0 directement. Les bots font certaines choses différemment, mais les concepts de base sont identiques.

Par exemple, le flux d’authentification pour les onglets et les bots utilisant Node et le type d’octroi implicite [OAuth 2.0](https://oauth.net/2/grant-types/implicit/), voir démarrer le flux d’authentification pour [les onglets](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow).

> [!NOTE]
> Avant **d’afficher** `microsoftTeams.authentication.authenticate` un bouton de connexion à l’utilisateur et d’appeler l’API en réponse à la sélection du bouton, vous devez attendre la fin de l’initialisation du SDK. Vous pouvez transmettre un rappel à l’API `microsoftTeams.initialize` qui est appelé à la fin de l’initialisation.

![Diagramme de séquence d’authentification par onglet](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. L’utilisateur interagit avec le contenu de la page de configuration ou de contenu de  l’onglet, généralement un bouton Se connecter **ou Se connecter**.
2. L’onglet construit l’URL de sa page de démarrage d’th. Éventuellement, il utilise des informations provenant d’espaces `microsoftTeams.getContext()` réservé d’URL ou appelle Teams SDK client pour simplifier l’expérience d’authentification de l’utilisateur. Par exemple, lors de l’authentification avec A Azure AD, `login_hint` si le paramètre est définie sur l’adresse e-mail de l’utilisateur, l’utilisateur n’a pas besoin de se connecter s’il l’a fait récemment. Cela est dû au Azure AD utilise les informations d’identification mises en cache de l’utilisateur. La fenêtre pop-up s’affiche brièvement, puis disparaît.
3. L’onglet appelle ensuite la méthode `microsoftTeams.authentication.authenticate()` et inscrit les fonctions `successCallback` et `failureCallback`.
4. Teams ouvre la page d’accueil dans un iframe dans une fenêtre fenêtre pop-up. La page de démarrage génère des données aléatoires`state`, les enregistre pour une validation future et les redirige vers le point de terminaison du fournisseur d’identité`/authorize`, `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` par exemple pour Azure AD. Remplacez `<tenant id>` par votre propre ID de client context.tid.
Comme d’autres flux d’th d’application dans Teams, la page `validDomains` de démarrage doit se trouver sur un domaine qui se trouve dans sa liste et sur le même domaine que la page de redirection de la publication de la signature.

    > [!NOTE]
    > Le flux d’octroi implicite OAuth 2.0 `state` appelle un paramètre dans la demande d’authentification, qui contient des données de session uniques pour empêcher une attaque par falsification de demande entre [sites](https://en.wikipedia.org/wiki/Cross-site_request_forgery). Les exemples utilisent un GUID généré de manière aléatoire pour les `state` données.

5. Sur le site du fournisseur, l’utilisateur se connecte et accorde l’accès à l’onglet.
6. Le fournisseur redirige l’utilisateur vers la page de redirection OAuth 2.0 de l’onglet avec un jeton d’accès.
7. L’onglet vérifie que la `state` valeur renvoyée correspond à ce qui a été enregistré précédemment et `microsoftTeams.authentication.notifySuccess()`appelle, `successCallback` ce qui appelle à son tour la fonction inscrite à l’étape 3.
8. Teams ferme la fenêtre pop-up.
9. L’onglet affiche l’interface utilisateur de configuration, actuale ou recharge le contenu des onglets, selon l’endroit à partir de lequel l’utilisateur a commencé.

## <a name="treat-tab-context-as-hints"></a>Traiter le contexte de l’onglet comme des conseils

Bien que le contexte de l’onglet fournit des informations utiles concernant l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur. Authentifier l’utilisateur même si vous obtenez les informations en tant que paramètres d’URL pour l’URL `microsoftTeams.getContext()` de contenu de votre onglet ou en appelant la fonction dans le SDK client Microsoft Teams. Un acteur malveillant peut appeler l’URL de contenu de votre onglet avec ses propres paramètres. L’acteur peut également appeler une page web usurpant l’identité Microsoft Teams pour charger l’URL de contenu de l’onglet dans un iframe et renvoyer ses propres données à la `getContext()` fonction. Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet comme un conseil et les valider avant d’utiliser. Reportez-vous aux notes [pour accéder à la page d’autorisation à partir de votre page de fenêtre pop-up](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page).

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification par onglet :

| **Exemple de nom** | **Description** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Authentification Teams onglets | Processus d’authentification pour les onglets utilisant Azure AD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>Voir aussi

Pour une implémentation détaillée de l’authentification par tabulation à l Azure AD, voir :

* [Authentifier un utilisateur dans un onglet Teams’accès](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-AAD.md)
