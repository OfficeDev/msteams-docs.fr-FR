---
title: Flux d’authentification pour les onglets
description: Décrit le flux d’authentification dans les onglets
ms.topic: conceptual
keywords: Onglets de flux d’authentification Teams
ms.openlocfilehash: 9505419a6594529bcf8d19a90d029705e573c67b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014585"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Flux d’authentification Microsoft Teams pour les onglets

> [!Note]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du SDK JavaScript teams.
> Le SDK Teams lance une fenêtre distincte pour le flux d’authentification et par conséquent, l’attribut samesite peut être définie sur « Lax ». Actuellement, SameSite=None n’est pas pris en charge par le client de bureau Teams ou les versions antérieures de Chrome ou Safari.

OAuth 2.0 est une norme ouverte d’authentification et d’autorisation utilisée par Azure AD et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams . [Voici une bonne vue d’ensemble](https://aaronparecki.com/oauth-2-simplified/) plus facile à suivre que la [spécification formelle.](https://oauth.net/2/) Le flux d’authentification pour les onglets et les bots est légèrement différent, car les onglets sont très similaires aux sites web afin qu’ils peuvent utiliser OAuth 2.0 directement ; Les bots ne sont pas et doivent faire certaines choses différemment, mais les concepts de base sont identiques.

*Voir*, Lancer le flux d’authentification pour les [onglets](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow) pour un exemple de flux d’authentification pour les onglets et les bots à l’aide de Node et du type d’octroi implicite [OAuth 2.0.](https://oauth.net/2/grant-types/implicit/)

![Diagramme de séquence d’authentification par onglet](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. L’utilisateur interagit avec le contenu de la page de configuration ou de contenu de l’onglet, généralement un bouton étiqueté « Se connecter » ou « Se connecter ».
2. L’onglet construit l’URL de sa page de démarrage d’authentification, en utilisant éventuellement les informations des espaces réservé d’URL ou en appelant la méthode du SDK client Teams pour simplifier l’expérience d’authentification de `microsoftTeams.getContext()` l’utilisateur. Par exemple, lors de l’authentification avec Azure AD, si le paramètre est définie sur l’adresse e-mail de l’utilisateur, il se peut que l’utilisateur n’a même pas besoin de se connecter s’il l’a fait récemment, car Azure AD utilisera les informations d’identification mises en cache de l’utilisateur si possible : la fenêtre popup clignote brièvement, puis `login_hint` disparaît.
3. L’onglet appelle ensuite la méthode `microsoftTeams.authentication.authenticate()` et inscrit les fonctions `successCallback` et `failureCallback`.
4. Teams ouvre la page de démarrage dans un iframe dans une fenêtre. La page de démarrage génère des données aléatoires, les enregistre pour une validation future et les redirige vers le point de terminaison du fournisseur d’identité, par exemple `state` `/authorize` pour Azure `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` AD. Remplacez `<tenant id>` par votre propre ID de client (context.tid).
    * Comme les autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver sur un domaine qui figure dans sa liste et sur le même domaine que la page de `validDomains` redirection post-connexion.
    * **IMPORTANT**: le flux d’octroi implicite OAuth 2.0 appelle un paramètre dans la demande d’authentification qui contient des données de session uniques pour empêcher une attaque par falsification de demande entre `state` [sites.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) Les exemples ci-dessous utilisent un GUID généré de manière aléatoire pour les `state` données.
5. Sur le site du fournisseur, l’utilisateur se signe et accorde l’accès à l’onglet.
6. Le fournisseur redirige l’utilisateur vers la page de redirection OAuth 2.0 de l’onglet avec un jeton d’accès.
7. L’onglet vérifie que la valeur renvoyée correspond à ce qui a été enregistré précédemment et appelle, ce qui appelle à son tour la fonction inscrite à `state` `microsoftTeams.authentication.notifySuccess()` l’étape `successCallback` 3.
8. Teams ferme la fenêtre pop-up.
9. L’onglet affiche l’interface utilisateur de configuration ou actualise ou recharge le contenu des onglets, en fonction de l’origine de l’utilisateur.

## <a name="treat-tab-context-as-hints"></a>Traiter le contexte de l’onglet comme des conseils

Bien que le contexte de l’onglet fournit des informations utiles concernant l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur, que vous l’obtenez en tant que paramètres d’URL de l’URL de contenu de votre onglet ou en appelant la fonction dans le `microsoftTeams.getContext()` SDK client Microsoft Teams. Un acteur malveillant peut appeler l’URL de contenu de votre onglet avec ses propres paramètres, et une page web usurpant l’identité de Microsoft Teams peut charger l’URL du contenu de votre onglet dans un iframe et renvoyer ses propres données à la `getContext()` fonction. Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet simplement comme des conseils et les valider avant de les utiliser. Reportez-vous aux notes de [la page d’autorisation à partir de votre page popup.](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)

## <a name="samples"></a>Exemples

Pour obtenir un exemple de code montrant le processus d’authentification par onglet, voir :

* [Exemple d’authentification d’onglet Microsoft Teams (nœud)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Exemple d’authentification d’onglet Microsoft Teams (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>Plus de détails

Pour obtenir une procédure pas à pas d’implémentation détaillée de l’authentification par onglet ciblant Azure Active Directory, voir :

* [Authentifier un utilisateur dans un onglet Microsoft Teams](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-AAD.md)
