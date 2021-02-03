---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification dans Teams et comment l’utiliser dans les applications
ms.topic: conceptual
keywords: Authentification teams OAuth SSO AAD
ms.openlocfilehash: 88b2098b7d45444cf47bebdfccc22fae772b7c22
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073102"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Authentifier les utilisateurs dans Microsoft Teams

> [!NOTE]
> L’authentification web sur les clients mobiles requiert la version 1.4.1 ou ultérieure du SDK JavaScript Microsoft Teams.

Pour accéder aux informations utilisateur protégées par Azure Active Directory (AAD) et accéder aux données à partir de services tels que Facebook et Twitter, l’application établit une connexion fiable avec ces fournisseurs. Si l’application utilise les API Microsoft Graph dans l’étendue utilisateur, authentifier l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Teams, il existe deux flux d’authentification différents pour l’application. Effectuez un flux d’authentification basé sur le web traditionnel dans une [page](~/tabs/how-to/create-tab-pages/content-page.md) de contenu incorporée dans un onglet, une page de configuration ou un module de tâche. Si l’application contient un bot de conversation, utilisez le flux OAuthPrompt et éventuellement le service d’authentification par jeton d’Azure Bot Framework pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification web

Utilisez le flux d’authentification web pour les [onglets](~/tabs/what-are-tabs.md) et choisissez de l’utiliser avec des [bots](~/bots/what-are-bots.md) de conversation ou [des extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md) Utilisez le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) dans une page de contenu web pour activer l’authentification. Après avoir authentification, incorporez la page de contenu dans un onglet, une page de configuration ou un module de tâche. Pour plus d’informations sur le flux d’authentification web, voir :

* [L’ajout d’authentification](~/bots/how-to/authentication/add-authentication.md) au bot Teams décrit comment utiliser le flux d’authentification web avec un bot de conversation.
* [Le flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglets dans Teams. Il s’agit d’un flux d’authentification web classique utilisé pour les onglets.
* [L’authentification AAD dans les onglets](~/tabs/how-to/authentication/auth-tab-AAD.md) décrit comment se connecter à AAD à partir d’un onglet dans l’application dans Teams.
* [L’authentification en mode silencieux AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) décrit comment réduire les invites de signature ou de consentement dans l’application à l’aide d’AAD.
* [.Net ou C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) ou [JavaScript ou Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) fournit des exemples pour l’authentification basée sur le web.

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flux OAuthPrompt pour les bots de conversation

OAuthPrompt d’Azure Bot Framework facilite l’authentification pour les applications utilisant des bots de conversation. Utilisez le service de jeton d’Azure Bot Framework pour faciliter la mise en cache des jetons.

Pour plus d’informations sur l’utilisation d’OAuthPrompt, voir :

* [La vue d’ensemble du flux](~/bots/how-to/authentication/auth-flow-bot.md) d’authentification de bot décrit le fonctionnement de l’authentification au sein d’un bot dans l’application dans Teams. Cela illustre un flux d’authentification non web utilisé pour les bots sur le web Teams, les applications de bureau et les applications mobiles.
* [L’authentification](~/bots/how-to/authentication/add-authentication.md) de bot décrit comment ajouter l’authentification OAuth au bot Teams.
* [.Net ou C# ou](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) [JavaScript ou Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) fournit un exemple de SDK d’authentification de bot v3.

## <a name="configure-the-identity-provider"></a>Configurer le fournisseur d’identité

Quel que soit le flux d’authentification de l’application, configurez le fournisseur d’identité pour communiquer avec l’application Teams. La plupart des exemples et des pas à pas concernent principalement l’utilisation d’AAD comme fournisseur d’identité. Les concepts, toutefois, s’appliquent quel que soit le fournisseur d’identité.

Pour plus d’informations, [voir configuration d’un fournisseur d’identité.](~/concepts/authentication/configure-identity-provider.md)
