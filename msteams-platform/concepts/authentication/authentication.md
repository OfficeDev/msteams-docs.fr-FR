---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification dans Teams et son utilisation dans vos applications
ms.topic: conceptual
keywords: Authentification teams OAuth SSO AAD
ms.openlocfilehash: 6ddcd8a9e847d9216b7e2dcc12733a6cd413b48e
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014291"
---
# <a name="authenticating-users-in-microsoft-teams"></a>Authentification des utilisateurs dans Microsoft Teams

> [!Note]
> L’authentification web sur les clients mobiles nécessite la version 1.4.1 ou ultérieure du SDK JavaScript teams.

Pour que votre application accède aux informations utilisateur protégées par Azure Active Directory, ainsi qu’aux données d’autres services tels que Facebook et Twitter, votre application devra établir une connexion fiable avec ces fournisseurs. Si votre application doit utiliser les API Microsoft Graph dans l’étendue utilisateur, vous devez également authentifier l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Microsoft Teams, il existe deux flux d’authentification différents dont votre application peut tirer parti. Vous pouvez effectuer un flux d’authentification basé sur le web traditionnel dans une [page](~/tabs/how-to/create-tab-pages/content-page.md) de contenu incorporée dans un onglet, une page de configuration ou un module de tâche. Si votre application contient un bot de conversation, vous pouvez utiliser le flux OAuthPrompt (et éventuellement le service d’authentification d’Azure Bot Framework) pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification web

Vous devez utiliser le flux d’authentification web pour les [onglets](~/tabs/what-are-tabs.md)et choisir de l’utiliser avec des [bots](~/bots/what-are-bots.md) de conversation ou des [extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md) Vous allez utiliser le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) dans une page de contenu web pour activer l’authentification, puis incorporer cette page de contenu dans un onglet, une page de configuration ou un module de tâche. Si vous souhaitez utiliser le flux d’authentification web avec un bot de conversation, vous devez utiliser un module de tâche [avec un bot.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

* [Le flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglets dans Teams. Il s’agit d’un flux d’authentification web classique utilisé pour les onglets.
* [L’authentification Azure AD](~/tabs/how-to/authentication/auth-tab-AAD.md) dans les onglets décrit comment se connecter à Azure Active Directory à partir d’un onglet dans votre application dans Teams.
* [L’authentification en mode silencieux (Azure AD)](~/tabs/how-to/authentication/auth-silent-AAD.md) décrit comment réduire les invites de signature/consentement dans votre application à l’aide d’Azure Active Directory.
* Authentification web en [dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) ou [JavaScript/Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Flux OAuthPrompt pour les bots de conversation

OAuthPrompt d’Azure Bot Framework facilite l’authentification pour les applications utilisant des bots de conversation. Vous pouvez également tirer parti du service de jeton d’Azure Bot Framework pour faciliter la mise en cache des jetons.

Pour plus d’informations sur l’utilisation d’OAuthPrompt, voir :

* [La vue d’ensemble du flux](~/bots/how-to/authentication/auth-flow-bot.md) d’authentification de bot décrit le fonctionnement de l’authentification au sein d’un bot dans votre application dans Teams. Cela illustre un flux d’authentification non web utilisé pour les bots sur toutes les versions de Teams (web, application de bureau et applications mobiles)
* [Authentification bot](~/bots/how-to/authentication/add-authentication.md)
* Exemple d’authentification de bot (V3 SDK) dans [dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) ou [JavaScript/Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)

## <a name="configure-your-identity-provider"></a>Configurer votre fournisseur d’identité

Quel que soit le flux d’authentification utilisé par votre application (vous utilisez peut-être les deux), vous devez configurer votre fournisseur d’identité pour communiquer avec votre application Teams. La plupart des exemples et des pas à pas que vous trouverez ici porteront principalement sur l’utilisation d’Azure Active Directory comme fournisseur d’identité. Les concepts s’appliquent toutefois, quel que soit le fournisseur d’identité que vous utiliserez.

Pour plus d’informations, [voir configuration d’un fournisseur d’identité](~/concepts/authentication/configure-identity-provider.md)
