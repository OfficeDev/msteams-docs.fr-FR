---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification Teams et comment l’utiliser dans les applications
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Authentification OAuth oAuth Azure AD
ms.openlocfilehash: 0e98887b309e6d3752d27ee120326e02aeb54922
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212341"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Authentifier les utilisateurs dans Microsoft Teams

> [!Note]
> L’authentification web sur les clients mobiles nécessite la version 1.4.1 ou ultérieure du SDK client JavaScript Teams version ultérieure.

Pour accéder aux informations utilisateur protégées par Azure Active Directory et accéder aux données à partir de services tels que Facebook et Twitter, l’application établit une connexion fiable avec ces fournisseurs. Si l’application utilise les API Graph Microsoft dans l’étendue utilisateur, authentifier l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Teams, il existe deux flux d’authentification différents pour l’application. Effectuez un flux d’authentification basé sur le web traditionnel dans une [page](~/tabs/how-to/create-tab-pages/content-page.md) de contenu incorporée dans un onglet, une page de configuration ou un module de tâche. Si l’application contient un robot de conversation, utilisez le flux OAuthPrompt et éventuellement le service du jeton d’Azure Bot Framework pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification web

Utilisez le flux d’authentification web pour les [onglets](~/tabs/what-are-tabs.md) et choisissez de l’utiliser avec des [bots](~/bots/what-are-bots.md) de conversation ou des [extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md) Utilisez le [SDK Microsoft Teams client JavaScript dans](/javascript/api/overview/msteams-client) une page de contenu web pour activer l’authentification. Après avoir activé l’authentification, incorporez la page de contenu dans un onglet, une page de configuration, ou un module de tâche. Pour plus d’informations sur le flux d’authentification web, voir :

* [Ajouter l’authentification au bot Teams décrit](~/bots/how-to/authentication/add-authentication.md) comment utiliser le flux d’authentification web avec un bot de conversation.
* [Le flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglets Teams. Il s’agit d’un flux d’authentification web classique utilisé pour les onglets.
* [Azure AD’authentification dans](~/tabs/how-to/authentication/auth-tab-AAD.md) les onglets décrit comment se connecter à Azure AD à partir d’un onglet dans l’application dans Teams.
* [L’authentification Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) explique comment réduire les invites de signature ou de consentement dans l’application à l’aide Azure AD.
* [.Net ou C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [ou JavaScript ou Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) fournit des exemples pour l’authentification basée sur le web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flux OAuthPrompt pour les bots de conversation

L’OAuthPrompt d’Azure Bot Framework facilite l’authentification pour les applications à l’aide de robots de conversation. Utilisez le service de jeton d’Azure Bot Framework pour vous aider avec la mise en cache de jetons.

Pour plus d’informations sur l’utilisation d’OAuthPrompt, voir :

* [La vue d’ensemble du flux](~/bots/how-to/authentication/auth-flow-bot.md) d’authentification de bot décrit le fonctionnement de l’authentification au sein d’un bot dans l’application Teams. Cela illustre un flux d’authentification non basé sur le web utilisé pour les bots sur Teams web, application de bureau et applications mobiles.
* [L’authentification](~/bots/how-to/authentication/add-authentication.md) bot décrit comment ajouter l’authentification OAuth au bot Teams bot.

## <a name="code-sample"></a>Exemple de code

fournit un exemple de SDK d’authentification du bot v3.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Authentification bot | Cet exemple montre comment démarrer avec l’authentification dans un bot pour Microsoft Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Tab, Bot and Messaging Extension (ME) SSO | Cet exemple montre s’il s’agit d’une 3D pour l’onglet, le bot et l’me - recherche, action, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Non disponible |


## <a name="configure-the-identity-provider"></a>Configuration du fournisseur d’identité

Quel que soit le flux d’authentification de l’application, configurez le fournisseur d’identité pour qu’il communique avec Teams’application. La plupart des exemples et des walkthroughs traitent principalement de l’utilisation Azure AD comme fournisseur d’identité. Les concepts s’appliquent toutefois, quel que soit le fournisseur d’identité. 

Pour plus d’informations, [voir configuration d’un fournisseur d’identité.](~/concepts/authentication/configure-identity-provider.md)

## <a name="third-party-cookies-on-ios"></a>Cookies tiers sur iOS

Après la mise à jour d’iOS 14, Apple a bloqué l’accès par défaut aux [cookies](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) tiers pour toutes les applications. Par conséquent, les applications qui utilisent des cookies tiers pour l’authentification dans leurs onglets Canal ou Conversation et applications personnelles ne pourront pas terminer leurs flux de travail d’authentification sur Teams clients iOS. Pour respecter les exigences de confidentialité et de sécurité, vous devez passer à un système basé sur les jetons ou utiliser des cookies de première partie pour les flux de travail d’authentification utilisateur.

## <a name="see-also"></a>Voir aussi

* [Microsoft Teams’authentification pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md)
* [Support de l'identification unique pour les robots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [Ajouter une authentification à votre extension de messagerie](~/messaging-extensions/how-to/add-authentication.md)