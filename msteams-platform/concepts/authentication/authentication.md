---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification dans Teams et comment l’utiliser dans les applications
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams authentication OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 811b8917297ad8fe1420f4887983b93f43cd73b3
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103957"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Authentifier les utilisateurs dans Microsoft Teams

> [!Note]
> L’authentification web sur les clients mobiles nécessite la version 1.4.1 ou ultérieure du SDK client JavaScript Teams.

Pour accéder aux informations utilisateur protégées par Azure AD et aux données de services tels que Facebook et Twitter, l’application établit une connexion approuvée avec ces fournisseurs. Si l’application utilise des API Microsoft Graph dans l’étendue de l’utilisateur, authentifiez l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Teams, il existe deux flux d’authentification différents pour l’application. Effectuez un flux d’authentification web traditionnel dans une [page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) incorporée dans un onglet, une page de configuration ou un module de tâche. Si l’application contient un robot de conversation, utilisez le flux OAuthPrompt et éventuellement le service du jeton d’Azure Bot Framework pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification web

Utilisez le flux d’authentification web pour [les onglets](~/tabs/what-are-tabs.md) et choisissez de l’utiliser avec [des bots conversationnels](~/bots/what-are-bots.md) ou [des extensions de message](~/messaging-extensions/what-are-messaging-extensions.md). Utilisez le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) dans une page de contenu web pour activer l’authentification. Après avoir activé l’authentification, incorporez la page de contenu dans un onglet, une page de configuration, ou un module de tâche. Pour plus d’informations sur le flux d’authentification basé sur le web, consultez :

* [L’ajout de l’authentification au bot Teams](~/bots/how-to/authentication/add-authentication.md) décrit comment utiliser le flux d’authentification web avec un bot conversationnel.
* [Le flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglet dans Teams. Cela montre un flux d’authentification web classique utilisé pour les onglets.
* [Azure AD l’authentification dans les onglets](~/tabs/how-to/authentication/auth-tab-AAD.md) décrit comment se connecter à Azure AD à partir d’un onglet de l’application dans Teams.
* [L’Azure AD d’authentification silencieuse](~/tabs/how-to/authentication/auth-silent-AAD.md) décrit comment réduire les invites de connexion ou de consentement dans l’application à l’aide de Azure AD.
* [.Net ou C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) ou [JavaScript ou Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) fournit des exemples d’authentification basée sur le web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flux OAuthPrompt pour les bots conversationnels

L’OAuthPrompt d’Azure Bot Framework facilite l’authentification pour les applications à l’aide de robots de conversation. Utilisez le service de jeton d’Azure Bot Framework pour vous aider avec la mise en cache de jetons.

Pour plus d’informations sur l’utilisation d’OAuthPrompt, consultez :

* [Vue d’ensemble du flux d’authentification](~/bots/how-to/authentication/auth-flow-bot.md) de bot décrit le fonctionnement de l’authentification au sein d’un bot dans l’application dans Teams. Cela montre un flux d’authentification non web utilisé pour les bots sur Teams applications web, de bureau et mobiles.
* [L’authentification](~/bots/how-to/authentication/add-authentication.md) de bot décrit comment ajouter l’authentification OAuth au bot Teams.

## <a name="code-sample"></a>Exemple de code

fournit un exemple de Kit de développement logiciel (SDK) d’authentification de bot v3.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Authentification de bot | Cet exemple montre comment commencer à utiliser l’authentification dans un bot pour Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Authentification unique Tab, Bot and Message Extension (ME) | Cet exemple montre l’authentification unique pour Tab, Bot et ME - search, action, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Non disponible |

## <a name="configure-the-identity-provider"></a>Configuration du fournisseur d’identité

Quel que soit le flux d’authentification de l’application, configurez le fournisseur d’identité pour communiquer avec l’application Teams. La plupart des exemples et des procédures pas à pas traitent principalement de l’utilisation de Azure AD en tant que fournisseur d’identité. Toutefois, les concepts s’appliquent indépendamment du fournisseur d’identité.

Pour plus d’informations, consultez [la configuration d’un fournisseur d’identité](~/concepts/authentication/configure-identity-provider.md).

## <a name="third-party-cookies-on-ios"></a>Cookies tiers sur iOS

Après la mise à jour d’iOS 14, Apple a bloqué par défaut l’accès tiers aux [cookies](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) pour toutes les applications. Par conséquent, les applications qui tirent parti des cookies tiers pour l’authentification dans leurs onglets Canal ou Conversation et applications personnelles ne pourront pas terminer leurs workflows d’authentification sur Teams clients iOS. Pour vous conformer aux exigences de confidentialité et de sécurité, vous devez passer à un système basé sur des jetons ou utiliser des cookies internes pour les flux de travail d’authentification utilisateur.

## <a name="see-also"></a>Voir aussi

* [Flux d’authentification Microsoft Teams pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Support de l'identification unique pour les robots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Ajouter l’authentification à votre extension de message](~/messaging-extensions/how-to/add-authentication.md)
