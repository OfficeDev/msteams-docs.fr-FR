---
title: Flux d’authentification pour les onglets
description: Décrit le flux d’authentification dans les onglets
keywords: onglets de flux d’authentification des équipes
ms.openlocfilehash: de5e0312e4523c3adef211dc03b0349c205f92cb
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346678"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Flux d’authentification Microsoft teams pour les onglets

> [!Note]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins la version 1.4.1 du kit de développement logiciel (SDK) JavaScript Teams.
> Le kit de développement logiciel teams lance une fenêtre distincte pour le flux d’authentification et, par conséquent, l’attribut samesite peut être défini sur « Lax ». Actuellement, SameSite = None n’est pas pris en charge par le client de bureau teams ni par les versions antérieures de chrome ou Safari.

OAuth 2,0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure AD et de nombreux autres fournisseurs d’identité. Une compréhension de base de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans teams ; [Voici une bonne présentation](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que les [spécifications formelles](https://oauth.net/2/). Le flux d’authentification pour les onglets et les robots est un peu différent, car les onglets sont très similaires aux sites Web afin qu’ils puissent utiliser OAuth 2,0 directement ; les robots ne sont pas et doivent effectuer quelques opérations différemment, mais les concepts de base sont identiques.

pour obtenir un exemple illustrant le flux d’authentification des onglets et des bots à l’aide du nœud utilisant le [type d’autorisation implicite OAuth 2,0](https://oauth.net/2/grant-types/implicit/).

![Diagramme de séquence d’authentification d’onglet](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. L’utilisateur interagit avec le contenu de la page de configuration ou de contenu de l’onglet, généralement un bouton intitulé « se connecter » ou « se connecter ».
2. L’onglet construit l’URL pour sa page de démarrage d’authentification, en utilisant éventuellement les informations des espaces réservés d’URL ou en appelant `microsoftTeams.getContext()` teams Client SDK Method afin de rationaliser l’expérience d’authentification pour l’utilisateur. Par exemple, lors de l’authentification auprès d’Azure AD, si le `login_hint` paramètre est défini sur l’adresse e-mail de l’utilisateur, il est possible que l’utilisateur ne doive pas se connecter si cela a été fait récemment, car Azure ad utilise les informations d’identification mises en cache de l’utilisateur si cela est possible : le menu contextuel clignote brièvement, puis disparaît.
3. L’onglet appelle ensuite la méthode `microsoftTeams.authentication.authenticate()` et inscrit les fonctions `successCallback` et `failureCallback`.
4. Teams ouvre la page de démarrage dans un IFRAME dans une fenêtre contextuelle. La page de démarrage génère `state` des données aléatoires, les enregistre pour une validation ultérieure et les redirige vers le point de terminaison du fournisseur d’identité, par `/authorize` exemple `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` pour Azure ad. Remplacez `<tenant id>` par votre propre ID de client (Context. TID).
    * Comme les autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver sur un domaine de sa `validDomains` liste et sur le même domaine que la page de redirection post-connexion.
    * **Important**: les appels de flux d’octroi implicite OAuth 2,0 pour un `state` paramètre dans la demande d’authentification qui contient des données de session uniques pour empêcher une [attaque de contrefaçon de demande intersite](https://en.wikipedia.org/wiki/Cross-site_request_forgery). Les exemples ci-dessous utilisent un GUID généré de manière aléatoire pour les `state` données.
5. Sur le site du fournisseur, l’utilisateur se connecte et autorise l’accès à l’onglet.
6. Le fournisseur dirige l’utilisateur vers la page de redirection OAuth 2,0 de l’onglet avec un jeton d’accès.
7. L’onglet vérifie que la valeur renvoyée `state` correspond à ce qui a été enregistré précédemment, et appelle `microsoftTeams.authentication.notifySuccess()` , qui appelle à son tour la `successCallback` fonction inscrite à l’étape 3.
8. Teams ferme la fenêtre contextuelle.
9. L’onglet affiche l’interface utilisateur de configuration ou actualise ou recharge le contenu des onglets, selon l’emplacement à partir duquel l’utilisateur a démarré.

## <a name="treat-tab-context-as-hints"></a>Considérer le contexte de l’onglet comme des conseils

Bien que le contexte d’onglet fournit des informations utiles sur l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur, que vous l’obteniez comme paramètres d’URL de votre URL de contenu de tabulation ou en appelant la `microsoftTeams.getContext()` fonction dans le kit de développement logiciel (SDK) du client Microsoft Teams. Un acteur malveillant peut appeler votre URL de contenu de tabulation avec ses propres paramètres, et une page Web qui emprunte l’identité de Microsoft teams pourrait charger votre URL de contenu d’onglet dans un IFRAME et renvoyer ses propres données à la `getContext()` fonction. Vous devez traiter les informations relatives à l’identité dans le contexte de l’onglet simplement comme des conseils et les valider avant de les utiliser.

## <a name="samples"></a>Exemples

Pour obtenir un exemple de code illustrant le processus d’authentification par onglet, voir :

* [Exemple d’authentification de l’onglet Microsoft Teams (nœud)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Exemple d’authentification de l’onglet Microsoft Teams (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>Plus de détails

Pour obtenir une description détaillée de l’implémentation de l’authentification d’onglet pour Azure Active Directory, voir :

* [Authentifier un utilisateur sous un onglet Microsoft teams](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-AAD.md)
