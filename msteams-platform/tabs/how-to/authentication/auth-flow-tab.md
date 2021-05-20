---
title: Flux d’authentification pour onglets
description: Décrit le flux d’authentification dans les onglets
ms.topic: conceptual
localization_priority: Normal
keywords: onglets de flux d’authentification des équipes
ms.openlocfilehash: 1282c149beba0ff5b424585f566a703f48234fa2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566690"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teams d’authentification pour les onglets

> [!NOTE]
> Pour que l’authentification fonctionne pour votre onglet sur les clients mobiles, vous devez vous assurer que vous utilisez au moins 1.4.1 version de la Microsoft Teams JavaScript SDK.
> Teams SDK lance une fenêtre séparée pour le flux d’authentification. Définissez `SameSite` l’attribut **de Lax**. Teams client de bureau ou les anciennes versions de Chrome ou Safari ne supportent `SameSite` pas =None.

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure Active Directory (AAD) et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable pour travailler avec l’authentification Teams. Pour plus d’informations, [voir OAuth 2 simplifié](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que [la spécification formelle](https://oauth.net/2/). Le flux d’authentification pour les onglets et les bots est différent parce que les onglets sont similaires aux sites Web afin qu’ils puissent utiliser OAuth 2.0 directement. Les bots font quelques choses différemment, mais les concepts de base sont identiques.

Pour un exemple de flux d’authentification pour les onglets et les bots utilisant nœud et le type de subvention implicite [OAuth 2.0](https://oauth.net/2/grant-types/implicit/), voir [lancer le flux d’authentification pour les onglets](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow).

> [!NOTE]
> Avant **d’afficher un bouton de** connexion à l’utilisateur et `microsoftTeams.authentication.authenticate` d’appeler l’API en réponse à la sélection du bouton, vous devez attendre la paracénalisation SDK pour terminer. Vous pouvez transmettre un rappel à `microsoftTeams.initialize` l’API qui est appelé lorsque l’initialisation se termine.

![Diagramme de séquence d’authentification d’onglet](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. L’utilisateur interagit avec le contenu de la configuration de l’onglet ou de la page de contenu, généralement **un bouton Connexion** ou **Connexion.**
2. L’onglet construit l’URL de sa page de démarrage auth. En option, il utilise les informations des espaces réservés url ou `microsoftTeams.getContext()` des appels Teams client SDK méthode pour rationaliser l’expérience d’authentification pour l’utilisateur. Par exemple, lors de l’authentification avec AAD, si `login_hint` le paramètre est défini sur l’adresse e-mail de l’utilisateur, l’utilisateur n’a pas à se connecter s’il l’a fait récemment. C’est parce qu’AAD utilise les informations d’identification mises en cache de l’utilisateur. La fenêtre contextée est affichée brièvement, puis disparaît.
3. L’onglet appelle ensuite la méthode `microsoftTeams.authentication.authenticate()` et inscrit les fonctions `successCallback` et `failureCallback`.
4. Teams ouvre la page de démarrage dans un iframe dans une fenêtre contextée. La page de démarrage génère des `state` données aléatoires, les enregistre pour validation future et redirige vers le point de `/authorize` terminaison du fournisseur `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` d’identité, comme pour Azure AD. Remplacez `<tenant id>` par votre propre id locataire qui est context.tid.
Comme pour les autres flux d’auth d’application en Teams, la page de démarrage doit être sur un domaine qui est dans `validDomains` sa liste, et sur le même domaine que le signe de poste dans la page de redirection.

    > [!NOTE]
    > Le flux implicite de subvention oAuth 2.0 nécessite un `state` paramètre dans la demande d’authentification, qui contient des données de session uniques pour empêcher [une attaque de contrefaçon de demande inter-sites.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) Les exemples utilisent un GUID généré au hasard pour les `state` données.

5. Sur le site du fournisseur, l’utilisateur se s’insurde et donne accès à l’onglet.
6. Le fournisseur emmène l’utilisateur à la page de redirection OAuth 2.0 de l’onglet avec un jeton d’accès.
7. L’onglet vérifie que la valeur retournée `state` correspond à ce qui a été enregistré précédemment, et les appels , qui à son tour appelle la fonction enregistrée à `microsoftTeams.authentication.notifySuccess()` `successCallback` l’étape 3.
8. Teams ferme la fenêtre pop-up.
9. L’onglet affiche l’interface utilisateur de configuration, actualise ou recharge le contenu des onglets, selon l’endroit d’où l’utilisateur a commencé.

## <a name="treat-tab-context-as-hints"></a>Traiter le contexte de l’onglet comme des indices

Bien que le contexte de l’onglet fournit des informations utiles concernant l’utilisateur, n’utilisez pas ces informations pour authentifier l’utilisateur. Authentifiez l’utilisateur même si vous obtenez les informations en tant que paramètres URL de votre URL de contenu d’onglet ou `microsoftTeams.getContext()` en appelant la fonction dans Microsoft Teams client SDK. Un acteur malveillant peut invoquer votre URL de contenu d’onglet avec ses propres paramètres. L’acteur peut également invoquer une page Web se faisant passer pour Microsoft Teams pour charger votre URL de contenu d’onglet dans un iframe et retourner ses propres données à la `getContext()` fonction. Vous devez traiter les informations liées à l’identité dans le contexte de l’onglet simplement comme des indices et les valider avant utilisation. Référez-vous aux notes dans [naviguer vers la page d’autorisation de votre page pop-up](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page).

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification de l’onglet :

| **Nom de l’échantillon** | **Description** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teams’authentification de l’onglet | Processus d’authentification pour les onglets utilisant AAD. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="more-details"></a>Plus de détails

Pour une implémentation détaillée pour l’authentification des onglets à l’aide d’AAD, voir :

* [Authentifier un utilisateur dans un onglet Teams’utilisateur](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Authentification en mode silencieux](~/tabs/how-to/authentication/auth-silent-AAD.md)
