---
title: Authentifier un utilisateur dans teams
description: Décrit l’authentification dans teams et son utilisation dans vos applications
keywords: authentification des équipes AAD SSO OAuth
ms.openlocfilehash: d3ae57d9937c6794fb743b44ca8210a5afd181bf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673657"
---
# <a name="authentication-in-teams"></a>Authentification dans teams

> [!Note]
> L’authentification Web sur les clients mobiles nécessite la version 1.4.1 ou une version ultérieure du kit de développement logiciel (SDK) JavaScript Teams.

Pour que votre application puisse accéder aux informations utilisateur protégées par Azure Active Directory, ainsi que pour accéder aux données d’autres services comme Facebook et Twitter, votre application doit établir une connexion approuvée avec ces fournisseurs. Si votre application doit utiliser les API Microsoft Graph dans la portée de l’utilisateur, vous devrez également authentifier l’utilisateur pour récupérer les jetons d’authentification appropriés.

Dans Microsoft Teams, il existe deux flux d’authentification différents pour que votre application tire parti. Vous pouvez effectuer un flux d’authentification Web classique dans une [page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) incorporée dans un onglet, une page de configuration ou un module de tâches. Si votre application contient un bot conversationnel, vous pouvez utiliser le flux OAuthPrompt (et éventuellement le service de jeton de l’infrastructure Azure bot) pour authentifier un utilisateur dans le cadre d’une conversation.

## <a name="web-based-authentication-flow"></a>Flux d’authentification Web

Vous devrez utiliser le flux d’authentification Web pour les [onglets](~/tabs/what-are-tabs.md)et pouvez choisir de l’utiliser avec des [robots de conversation](~/bots/what-are-bots.md) ou des [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md). Vous utiliserez le [Kit de développement logiciel (SDK) du client JavaScript Microsoft teams](/javascript/api/overview/msteams-client) dans une page de contenu Web pour activer l’authentification, puis incorporez cette page de contenu dans un onglet, une page de configuration ou un module de tâches. Si vous souhaitez utiliser le flux d’authentification Web avec un bot de conversation, vous devez [utiliser un module de tâches avec un bot](~/task-modules-and-cards/task-modules/task-modules-bots.md).

* Le [flux d’authentification dans les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) décrit le fonctionnement de l’authentification par onglet dans Teams. Cela montre un flux d’authentification Web standard utilisé pour les onglets.
* [Authentification Azure ad dans les onglets](~/tabs/how-to/authentication/auth-tab-AAD.md) décrit comment se connecter à Azure Active Directory à partir d’un onglet de votre application dans Teams.
* [Authentification sans assistance (Azure AD)](~/tabs/how-to/authentication/auth-silent-AAD.md) décrit comment réduire les invites de connexion/de consentement dans votre application à l’aide d’Azure Active Directory.
* Authentification Web dans [dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) ou [JavaScript/node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>Le flux OAuthPrompt pour les bots de conversation

La OAuthPrompt de l’infrastructure Azure bot facilite l’authentification pour les applications utilisant des bots conversation. Vous pouvez également tirer parti du service de jeton de l’infrastructure de robots Azure pour faciliter la mise en cache des jetons.

Pour plus d’informations sur l’utilisation de l’OAuthPrompt, consultez la rubrique suivante :

* [Présentation du flux d’authentification des robots](~/bots/how-to/authentication/auth-flow-bot.md) décrit le fonctionnement de l’authentification dans un bot de votre application dans Teams. Cela montre un flux d’authentification non Web utilisé pour les robots sur toutes les versions de Teams (Web, application de bureau et applications mobiles)
* [Authentification de robot](~/bots/how-to/authentication/add-authentication.md)
* Exemple d’authentification bot (kit de développement logiciel V3) dans [dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) ou [JavaScript/node. js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)

## <a name="configure-your-identity-provider"></a>Configurer votre fournisseur d’identité

Quel que soit le flux d’authentification utilisé par votre application (vous pouvez même utiliser les deux), vous devrez configurer votre fournisseur d’identité pour qu’il communique avec votre application Teams. La majorité des exemples et des procédures pas à pas que vous trouverez ici traite principalement de l’utilisation d’Azure Active Directory en tant que fournisseur d’identité. Les concepts s’appliquent néanmoins, quel que soit le fournisseur d’identité que vous utiliserez.

Pour plus d’informations, consultez la rubrique [configuration d’un fournisseur d’identité](~/concepts/authentication/configure-identity-provider.md)
