---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification Teams et comment l’utiliser dans les applications
ms.topic: conceptual
localization_priority: Normal
keywords: Authentification teams OAuth SSO AAD
ms.openlocfilehash: ed169e3cc5f9190571890cb891665a493bd052d1
ms.sourcegitcommit: ec79bbbc3a8daa1ad96de809fc6d17367e8f0c6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/04/2021
ms.locfileid: "53726942"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Authentifier les utilisateurs dans Microsoft Teams

> [!Note]
> L’authentification web sur les clients mobiles nécessite la version 1.4.1 ou ultérieure du SDK client JavaScript Teams version ultérieure.

Pour accéder aux informations utilisateur protégées par Azure Active Directory (AAD) et accéder aux données à partir de services tels que Facebook et Twitter, l’application établit une connexion fiable avec ces fournisseurs. Si l’application utilise les API microsoft Graph dans l’étendue utilisateur, authentifier l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Teams, il existe deux flux d’authentification différents pour l’application. Effectuez un flux d’authentification basé sur le web traditionnel dans une [page](~/tabs/how-to/create-tab-pages/content-page.md) de contenu incorporée dans un onglet, une page de configuration ou un module de tâche. Si l’application contient un robot de conversation, utilisez le flux OAuthPrompt et éventuellement le service du jeton d’Azure Bot Framework pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification web

Utilisez le flux d’authentification web pour les [onglets](~/tabs/what-are-tabs.md) et choisissez de l’utiliser avec des [bots](~/bots/what-are-bots.md) de conversation ou [des extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md) Utilisez le [SDK Microsoft Teams client JavaScript dans](/javascript/api/overview/msteams-client) une page de contenu web pour activer l’authentification. Après avoir activé l’authentification, incorporez la page de contenu dans un onglet, une page de configuration, ou un module de tâche. Pour plus d’informations sur le flux d’authentification web, voir :

* [Ajouter l’authentification au bot Teams décrit](~/bots/how-to/authentication/add-authentication.md) comment utiliser le flux d’authentification web avec un bot de conversation.
* [Le flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglets Teams. Il s’agit d’un flux d’authentification web classique utilisé pour les onglets.
* [L’authentification AAD](~/tabs/how-to/authentication/auth-tab-AAD.md) dans les onglets décrit comment se connecter à AAD à partir d’un onglet dans l’application Teams.
* [L’authentification en mode silencieux AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) décrit comment réduire les invites de signature ou de consentement dans l’application à l’aide d’AAD.
* [.Net ou C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [ou JavaScript ou Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) fournit des exemples pour l’authentification basée sur le web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flux OAuthPrompt pour les bots de conversation

L’OAuthPrompt d’Azure Bot Framework facilite l’authentification pour les applications à l’aide de robots de conversation. Utilisez le service de jeton d’Azure Bot Framework pour vous aider avec la mise en cache de jetons.

Pour plus d’informations sur l’utilisation d’OAuthPrompt, voir :

* [La vue d’ensemble du flux](~/bots/how-to/authentication/auth-flow-bot.md) d’authentification de bot décrit le fonctionnement de l’authentification au sein d’un bot dans l’application Teams. Cela illustre un flux d’authentification non basé sur le web utilisé pour les bots sur Teams web, d’application de bureau et d’applications mobiles.
* [L’authentification](~/bots/how-to/authentication/add-authentication.md) de bot décrit comment ajouter l’authentification OAuth au bot Teams bot.

## <a name="code-sample"></a>Exemple de code

fournit un exemple de SDK d’authentification du bot v3.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Authentification bot | Cet exemple montre comment démarrer avec l’authentification dans un bot pour Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Tab, Bot and Messaging Extension (ME) SSO | Cet exemple montre l' sso pour l’onglet, le bot et l’me - recherche, action, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Non disponible |


## <a name="configure-the-identity-provider"></a>Configuration du fournisseur d’identité

Quel que soit le flux d’authentification de l’application, configurez le fournisseur d’identité pour qu’il communique Teams’application. La plupart des exemples et des pas à pas concernent principalement l’utilisation d’AAD comme fournisseur d’identité. Les concepts s’appliquent toutefois, quel que soit le fournisseur d’identité.

Pour plus d’informations, [voir configuration d’un fournisseur d’identité.](~/concepts/authentication/configure-identity-provider.md)
