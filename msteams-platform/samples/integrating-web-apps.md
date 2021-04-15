---
author: heath-hamilton
description: Meilleures pratiques pour l'intégration d'applications web existantes à Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Intégrer une application web à Microsoft Teams
ms.openlocfilehash: 4671d2277d5eb7c035421c51b1714eccaac06a31
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696485"
---
# <a name="integrate-web-apps-with-teams"></a>Intégrer des applications web à Teams

Avez-vous une application web qui, selon vous, serait naturellement adaptée aux fonctionnalités sociales et collaboratives de Teams ? Ces instructions peuvent vous aider à comprendre comment intégrer les types d'applications suivants :

* **Applications autonomes**: il peut s'agit d'une application à page unique ou d'une application complexe de grande taille que vous souhaitez que les personnes utilisent certains aspects de Teams.
* **Applications de collaboration**: une application déjà conçue pour les fonctionnalités sociales et collaboratives inhérentes à Teams.
* **SharePoint**: page SharePoint que vous souhaitez faire surface dans Teams.

Pour chaque recommandation, vous pouvez voir si elle s'applique à votre scénario d'intégration.

## <a name="get-to-know-teams-platform-capabilities"></a>Faire connaître les fonctionnalités de la plateforme Teams

***Scénarios d'intégration**: applications autonomes, applications de collaboration, SharePoint*

Votre application Teams peut inclure des fonctionnalités que les utilisateurs souhaitent et peuvent attendre lors de la collaboration, mais vous ne connaissez peut-être pas la terminologie de développement Teams.

|Fonctionnalités d'application courantes   |Fonctionnalités de plateforme Teams   |
|----------|-----------|
|Page web incorporée, page d'accueil ou vue web  |[Onglets](../tabs/what-are-tabs.md)  |
|Partager des raccourcis et des extensions  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Raccourcis et extensions d'action  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[Bots](../bots/what-are-bots.md) |
|Notifications de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Connecteurs Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Services externes de message  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modals  |[Modules de tâche](../task-modules-and-cards/what-are-task-modules.md)  |
|Cartes riches en contenu  |[Cartes adaptatives](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Déterminer un sous-ensemble de fonctionnalités

***Scénarios d'intégration**: applications autonomes*

L'intégration de toutes les fonctionnalités d'une application existante dans Teams entraîne souvent une expérience utilisateur forcée ou contre nature, en particulier dans les applications plus volumineuses. Envisagez de commencer avec les fonctionnalités les plus importantes et celles qui s'intégreront plus naturellement avec Teams. N'oubliez pas que vous pouvez toujours autoriser les utilisateurs à lancer l'application principale et à accéder à son ensemble complet de fonctionnalités.

Avant de commencer un travail technique, planifiez votre application Teams :

1. [Maposez les cas d'utilisation de votre application sur les fonctionnalités de la plateforme Teams.](../concepts/design/map-use-cases.md)
1. [Déterminez les points d'entrée de votre application.](../concepts/extensibility-points.md) S'agit-il d'un usage personnel, d'une collaboration ou des deux ?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprendre les conditions requises et les options de SharePoint

***Scénarios d'intégration**: SharePoint*

Vous pouvez intégrer une [page SharePoint existante](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) en tant qu'onglet Teams. N'oubliez pas les choses suivantes :

* Il doit s'agit *d'une* page SharePoint Online moderne
* Seuls les onglets personnels sont pris en charge (vous ne pouvez pas intégrer votre page en tant qu'onglet de canal)

Vous pouvez également créer un onglet Teams à [l'aide de SharePoint Framework.](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)

## <a name="aim-towards-multi-tenancy"></a>Objectif de l'expérience d'une location multiple

***Scénarios d'intégration**: applications autonomes, applications de collaboration, SharePoint*

Si votre application est utilisée par plusieurs organisations, envisagez un hébergement multi-clients qui rendrait votre produit évolutif et simplifierait grandement la distribution.

## <a name="review-your-apis"></a>Passer en revue vos API

***Scénarios d'intégration**: applications autonomes, applications de collaboration*

Ne supposez pas que les API et structures de données existantes de votre application prennent entièrement en charge l'application lorsqu'elle est intégrée à Teams. Vous devrez [peut-être](../concepts/build-and-test/deep-links.md)augmenter ces [](../concepts/authentication/configure-identity-provider.md)informations avec des informations contextuelles sur Teams pour le mappage d'identité, la prise en charge des liens profonds et l'incorporation [de Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).

En savoir plus sur l'obtention de contexte pour votre [onglet](../tabs/how-to/access-teams-context.md) ou [bot](../bots/how-to/get-teams-context.md)Teams.

## <a name="understand-authentication-options"></a>Comprendre les options d'authentification

***Scénarios d'intégration**: applications autonomes, applications de collaboration, SharePoint*

Azure Active Directory (AD) est le fournisseur d'identité pour Teams. Si votre application utilise un autre fournisseur d'identité, vous devez soit faire un exercice de mappage d'identité, soit vous fédérer avec Azure AD.

Teams dispose de mécanismes d'authentification unique (SSO) avec Azure AD pour les applications tierces et des conseils pour les flux d'authentification vers d'autres fournisseurs d'identité à l'aide de normes telles que OAuth et Open ID Connect (OIDC).

Pour les pages SharePoint, vous ne pouvez utiliser l' sinceso SSO et vous ne pouvez pas ajouter un autre ID Azure AD si vous souhaitez qu'elle fonctionne pour une autre application (étant donné que l'ID est l'application SharePoint).

En savoir plus sur [l'authentification dans Teams.](../concepts/authentication/authentication.md)

## <a name="follow-teams-design-guidelines"></a>Suivre les instructions de conception teams

***Scénarios d'intégration**: applications autonomes, applications de collaboration*

En règle générale, votre application doit être naturelle dans Teams. Vous pensez peut-être que la migration de contenu d'application existant vers un onglet Teams est suffisante, mais nous vous recommandons vivement de suivre les instructions de conception [de Teams.](../concepts/design/understand-use-cases.md) Voir aussi : [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Optimiser la liaison profonde

***Scénarios d'intégration**: applications autonomes, applications de collaboration, SharePoint*

Presque tous les liens dans Teams peuvent être liés directement avec [un lien profond.](../concepts/build-and-test/deep-links.md) Votre application doit optimiser l'utilisation de ces éléments, y compris la liaison avec et à partir de messages spécifiques et du contenu d'onglet. Les liens profonds peuvent vraiment lier plusieurs éléments d'une application pour une expérience Teams plus native.

## <a name="be-smart-when-messaging-users"></a>Soyez intelligent lors de la messagerie des utilisateurs

***Scénarios d'intégration**: applications autonomes, applications de collaboration, SharePoint*

Prenez en compte les types de messages que votre application Teams peut envoyer maintenant et à long terme. Si vous pensez que votre application aura une conversation multi-thread, un [bot](../bots/what-are-bots.md) peut offrir plus de flexibilité qu'un [webhook.](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Les bots vous permettent également d'envoyer des *messages proactifs* à des utilisateurs individuels ou à des canaux. Il s'agit de messages non improvisés déclenchés par un événement externe et non d'un message envoyé à un bot. (Par exemple, votre bot peut envoyer un message de bienvenue lorsqu'il est installé ou qu'un nouvel utilisateur rejoint un canal.)

L'envoi de messages proactifs nécessite des identificateurs propres à Teams : vous pouvez capturer ces informations en extraire les données de liste ou de profil [utilisateur,](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)en vous abonnant à des [événements de conversation](../bots/how-to/conversations/subscribe-to-conversation-events.md)ou à l'aide de Microsoft [Graph.](https://docs.microsoft.com/graph/teams-proactive-messaging)

Ne faites pas attention aux utilisateurs de courrier indésirable avec un nombre excessif de messages. Si la fonctionnalité Teams la prend en charge, envisagez de laisser les utilisateurs configurer les paramètres de notification pour votre application (par exemple, « Ne m'envoyez pas de messages non improvisés »).

## <a name="use-sharepoint-for-file-and-data-storage"></a>Utiliser SharePoint pour le stockage de fichiers et de données

***Scénarios d'intégration :** Applications autonomes, applications de collaboration, pages SharePoint*

Lorsqu'une équipe est créée, une collection de sites [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) est également mise en service pour prendre en charge le stockage de fichiers et de données pour cette équipe. Votre application peut et doit tirer parti de cette fonctionnalité si elle interagit avec des fichiers. Vous pouvez également utiliser la collection de sites pour stocker des données brutes dans des listes SharePoint et Excel.
