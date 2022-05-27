---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification dans Teams et comment l’utiliser dans les applications
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Microsoft Azure Active Directory DSO OAuth d’authentification teams (Azure AD)
ms.openlocfilehash: 53f258769140a2b40bb59a1232250f74ec693bee
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757156"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Authentifier les utilisateurs dans Microsoft Teams

> [!Note]
> L’authentification web sur les clients mobiles nécessite la version 1.4.1 ou ultérieure du Kit de développement logiciel (SDK) du client JavaScript Teams.

Pour accéder aux informations utilisateur protégées par Azure AD et accéder aux données de services tels que Facebook et Twitter, l’application établit une connexion approuvée avec ces fournisseurs. Si l’application utilise Microsoft Graph API dans l’étendue utilisateur, authentifiez l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Teams, il existe deux flux d’authentification différents pour l’application. Effectuer un flux d’authentification web traditionnel sur une [page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) incorporée dans un onglet, une page de configuration, ou un module de tâche. Si l’application contient un robot de conversation, utilisez le flux OAuthPrompt et éventuellement le service du jeton d’Azure Bot Framework pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification web

Utilisez le flux d’authentification web pour les [onglets](~/tabs/what-are-tabs.md) et choisissez de l’utiliser avec [des robots de conversation](~/bots/what-are-bots.md) ou [des extensions de message](~/messaging-extensions/what-are-messaging-extensions.md). Utilisez le [Kit de développement logiciel (SDK)](/javascript/api/overview/msteams-client) du client JavaScript Microsoft Teams sur une page de contenu web pour activer l’authentification. Après avoir activé l’authentification, incorporez la page de contenu dans un onglet, une page de configuration, ou un module de tâche. Pour plus d’informations sur le flux d’authentification web, consultez :

* [Ajouter l’authentification au bot Teams](~/bots/how-to/authentication/add-authentication.md) décrit comment utiliser le flux d’authentification web avec un bot conversationnel.
* [Le flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglets dans Teams, qui montre un flux d’authentification web classique utilisé pour les onglets.
* [Authentification Azure AD dans les onglets](~/tabs/how-to/authentication/auth-tab-AAD.md) décrit comment se connecter à Azure AD à partir d’un onglet de l’application dans Teams.
* [Authentification silencieuse Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) décrit comment réduire les invites de connexion ou de consentement dans l’application à l’aide de Azure AD.
* [.Net ou C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) ou [JavaScript ou Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) fournit des exemples pour l’authentification basée sur le web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Le Flux OAuthPrompt pour les robots de conversation

L’OAuthPrompt d’Azure Bot Framework facilite l’authentification pour les applications à l’aide de robots de conversation. Utilisez le service de jeton d’Azure Bot Framework pour vous aider avec la mise en cache de jetons.

Pour plus d’informations sur l’utilisation d’OAuthPrompt, consultez :

* [La vue d’ensemble du flux d’authentification](~/bots/how-to/authentication/auth-flow-bot.md) de bot décrit le fonctionnement de l’authentification au sein d’un bot dans l’application dans Teams, qui montre un flux d’authentification non web utilisé pour les bots sur Teams web, l’application de bureau et les applications mobiles.
* [Authentification de bot](~/bots/how-to/authentication/add-authentication.md) décrit comment ajouter l’authentification OAuth au bot Teams.

## <a name="code-sample"></a>Exemple de code

fournit un exemple de Kit de développement logiciel (SDK) Bot Authentication v3.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Authentification du bot | Cet exemple montre comment prendre en main l’authentification dans un bot pour Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Authentification unique Tab, Bot and Message Extension (ME) | Cet exemple montre l’authentification unique pour Tab, Bot et ME : recherche, action, déploiement de liens. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Non disponible |

## <a name="configure-the-identity-provider"></a>Configuration du fournisseur d’identité

Quel que soit le flux d’authentification de l’application, configurez le fournisseur d’identité pour communiquer avec l’application Teams. La plupart des exemples et des procédures pas à pas traitent principalement de l’utilisation de Azure AD en tant que fournisseur d’identité. Toutefois, les concepts s’appliquent quel que soit le fournisseur d’identité.

Pour plus d’informations, consultez [configuration d’un fournisseur d’identité](~/concepts/authentication/configure-identity-provider.md).

## <a name="third-party-cookies-on-ios"></a>Cookies tiers sur iOS

Après la mise à jour d’iOS 14, Apple a bloqué l’accès [cookie tiers](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) pour toutes les applications par défaut. Par conséquent, les applications qui tirent parti des cookies tiers pour l’authentification dans leurs onglets Canal ou Conversation et applications personnelles ne pourront pas terminer leurs flux de travail d’authentification sur Teams iOS clients. Pour vous conformer aux exigences de confidentialité et de sécurité, vous devez passer à un système basé sur des jetons ou utiliser des cookies internes pour les flux de travail d’authentification utilisateur.

## <a name="see-also"></a>Voir aussi

* [Flux d’authentification Microsoft Teams pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Support de l'identification unique pour les robots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Ajouter une authentification à votre extension de messagerie](~/messaging-extensions/how-to/add-authentication.md)
