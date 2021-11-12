---
title: Flux d’authentification pour les onglets
description: Décrit le flux d’authentification dans les onglets, OAuth par AAD et fournit un exemple de code
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Onglets de flux d’authentification Teams
ms.openlocfilehash: 2d054ef841bf4f05be4e662d77b999c654670f45
ms.sourcegitcommit: 58fe8a87b988850ae6219c55062ac34cd8bdbf66
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949648"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teams’authentification pour les onglets

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du SDK JavaScript Microsoft Teams.  
> Teams SDK ouvre une fenêtre distincte pour le flux d’authentification. Définissez `SameSite` l’attribut **sur Lax**. Teams client de bureau ou des versions antérieures de Chrome ou Safari ne sont pas en charge `SameSite` =Aucun.

OAuth 2.0 est une norme ouverte d’authentification et d’autorisation utilisée par Azure Active Directory (AAD) et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams. Pour plus d’informations, [voir OAuth 2 simplifié](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que la [spécification formelle](https://oauth.net/2/). Le flux d’authentification pour les onglets et les bots est différent, car les onglets sont similaires aux sites web afin qu’ils peuvent utiliser OAuth 2.0 directement. Les bots font certaines choses différemment, mais les concepts de base sont identiques.

Par exemple, le flux d’authentification pour les onglets et les bots utilisant Node et le type d’octroi implicite [OAuth 2.0](https://oauth.net/2/grant-types/implicit/), voir démarrer le flux d’authentification pour les [onglets](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow).

> [!NOTE]
> Avant **d’afficher** un bouton de connexion à l’utilisateur et d’appeler l’API en réponse à la sélection du bouton, vous devez attendre la fin de l’initialisation du `microsoftTeams.authentication.authenticate` SDK. Vous pouvez transmettre un rappel à l’API qui est appelé à la `microsoftTeams.initialize` fin de l’initialisation.

![Diagramme de séquence d’authentification par onglet](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. L’utilisateur interagit avec le contenu de la  page de configuration ou de contenu de l’onglet, généralement un bouton Se connecter ou **Se** connecter.
2. L’onglet construit l’URL de sa page de démarrage d’th. Éventuellement, il utilise des informations provenant d’espaces réservé d’URL ou appelle Teams SDK client pour simplifier l’expérience d’authentification `microsoftTeams.getContext()` de l’utilisateur. Par exemple, lors de l’authentification avec AAD, si le paramètre est définie sur l’adresse e-mail de `login_hint` l’utilisateur, l’utilisateur n’a pas besoin de se connecter s’il l’a fait récemment. Cela est dû au AAD utilise les informations d’identification mises en cache de l’utilisateur. La fenêtre pop-up s’affiche brièvement, puis disparaît.
3. L’onglet appelle ensuite la méthode `microsoftTeams.authentication.authenticate()` et inscrit les fonctions `successCallback` et `failureCallback`.
4. Teams ouvre la page d’accueil dans un iFrame dans une fenêtre fenêtre pop-up. La page de démarrage génère des données aléatoires, les enregistre pour une validation future et les redirige vers le point de terminaison du fournisseur d’identité, par exemple pour `state` `/authorize` `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` Azure AD. Remplacez `<tenant id>` par votre propre ID de client context.tid.
Comme d’autres flux d’th d’application dans Teams, la page de démarrage doit se trouver sur un domaine qui se trouve dans sa liste et sur le même domaine que la page de redirection de la publication `validDomains` de la signature.

    > [!NOTE]
    > Le flux d’octroi implicite OAuth 2.0 appelle un paramètre dans la demande d’authentification, qui contient des données de session uniques pour empêcher une attaque par falsification de demande entre `state` [sites.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) Les exemples utilisent un GUID généré de manière aléatoire pour les `state` données.

5. Sur le site du fournisseur, l’utilisateur se connecte et accorde l’accès à l’onglet.
6. Le fournisseur redirige l’utilisateur vers la page de redirection OAuth 2.0 de l’onglet avec un jeton d’accès.
7. L’onglet vérifie que la valeur renvoyée correspond à ce qui a été enregistré précédemment et appelle, ce qui appelle à son tour la fonction inscrite à `state` `microsoftTeams.authentication.notifySuccess()` l’étape `successCallback` 3.
8. Teams ferme la fenêtre pop-up.
9. L’onglet affiche l’interface utilisateur de configuration, actuale ou recharge le contenu des onglets, en fonction de l’origine de l’utilisateur.

## <a name="treat-tab-context-as-hints"></a>Traiter le contexte de l’onglet comme des conseils

Bien que le contexte de l’onglet fournit des informations utiles concernant l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur. Authentifier l’utilisateur même si vous obtenez les informations en tant que paramètres d’URL de l’URL de contenu de l’onglet ou en appelant la fonction dans le `microsoftTeams.getContext()` SDK client Microsoft Teams. Un acteur malveillant peut appeler l’URL de contenu de votre onglet avec ses propres paramètres. L’acteur peut également appeler une page web usurpant l’Microsoft Teams pour charger l’URL de contenu de l’onglet dans un iframe et renvoyer ses propres données à la `getContext()` fonction. Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet comme un conseil et les valider avant d’utiliser. Reportez-vous aux notes [pour accéder à la page d’autorisation à partir de votre page de fenêtre pop-up.](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification par onglet :

| **Exemple de nom** | **Description** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Authentification Teams onglets | Processus d’authentification pour les onglets utilisant AAD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>Voir aussi

Pour une implémentation détaillée de l’authentification par onglets AAD, voir :

* [Authentifier un utilisateur dans un onglet Teams de données](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-AAD.md)
