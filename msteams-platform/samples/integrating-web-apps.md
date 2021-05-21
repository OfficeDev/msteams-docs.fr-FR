---
author: heath-hamilton
description: Meilleures pratiques pour l’intégration d’applications web existantes à Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Applications web
ms.openlocfilehash: 6783a05079f876cf3c2475a0ad5ca0e1f6687fc4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566221"
---
# <a name="web-apps"></a>Applications web 

Vous pouvez rendre les applications web adaptées Teams fonctionnalités sociales et collaboratives de votre Teams.
  
Les différents types d’applications que vous pouvez intégrer à Teams sont les suivants :
* **Applications autonomes**: une application autonome est une application à page unique ou grande, et complexe. L’utilisateur peut en utiliser certains aspects dans Teams.
* **Applications de collaboration**: une application déjà conçue pour les fonctionnalités sociales et collaboratives inhérentes à Teams.
* **SharePoint**: page SharePoint que vous souhaitez faire surface dans Teams.

Vous pouvez maîtr et suivre les recommandations appropriées applicables à votre scénario d’intégration.
Ce document offre une vue d’ensemble des fonctionnalités de Teams, des exigences de point de partage pour le stockage de fichiers et de données, des exigences d’API, de l’authentification et de la liaison approfondie de votre application avec Teams.
 
## <a name="get-to-know-teams-platform-capabilities"></a>Faire connaître les fonctionnalités Teams plateforme

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Votre application Teams doit inclure les fonctionnalités de collaboration requises et attendues. Pour travailler avec l’intégration des applications, il est important de se familiariser avec la terminologie Teams développement.

|Fonctionnalités d’application courantes   |Teams plateforme   |
|----------|-----------|
|Page web incorporée, page d’accueil ou vue web  |[Onglets](../tabs/what-are-tabs.md)  |
|Partager des raccourcis et des extensions  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Raccourcis et extensions d’action  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[Bots](../bots/what-are-bots.md) |
|Notifications de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Connecteurs Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Services externes de message  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modals  |[Modules de tâche](../task-modules-and-cards/what-are-task-modules.md)  |
|Cartes riches en contenu  |[Cartes adaptatives](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Déterminer un sous-ensemble de fonctionnalités

***Scénarios d’intégration**: applications autonomes*

L’intégration de toutes les fonctionnalités d’une application existante dans Teams entraîne souvent une expérience utilisateur forcée ou contre nature, en particulier dans les applications plus volumineuses. Commencez avec les fonctionnalités les plus importantes et celles qui s’intègrent plus naturellement à Teams. Vous pouvez permettre aux utilisateurs de lancer l’application principale et d’accéder à son ensemble complet de fonctionnalités.

**Conditions préalables à l’intégration de votre application à Teams** Voici les conditions préalables à l’intégration de votre application avec Teams. 

1. [Maposez les cas d’utilisation de votre application Teams fonctionnalités de la plateforme.](../concepts/design/map-use-cases.md)
1. [Déterminez les points d’entrée de votre application.](../concepts/extensibility-points.md) S’agit-il d’un usage personnel, d’une collaboration ou des deux ?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprendre les SharePoint et les options

***Scénarios d’intégration**: SharePoint*

Pour intégrer une page SharePoint [sous](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) la Teams, vous devez prendre en compte les considérations suivantes :

* Il doit s’agit *d’une* page SharePoint en ligne moderne.
* Seuls les onglets personnels sont pris en charge. Vous ne pouvez pas intégrer votre page en tant qu’onglet de canal.

Vous pouvez également créer un onglet Teams à [l’aide de la SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Objectif de l’expérience d’une location multiple

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Si votre application est utilisée par plusieurs organisations, envisagez l’hébergement à plusieurs clients qui rend votre produit évolutif et simplifie grandement la distribution.

## <a name="review-your-apis"></a>Passer en revue vos API

***Scénarios d’intégration**: applications autonomes, applications de collaboration*

Vous devez faire en sorte que les API et structures de données existantes de votre application la prise en charge lors de l’intégration à Teams. Pour étendre la prise en charge, vous devez enrichir les API et [](../concepts/build-and-test/deep-links.md)les structures de données avec des informations contextuelles sur les Teams pour le mappage d’identité, [](../concepts/authentication/configure-identity-provider.md)la prise en charge des liens profonds et l’incorporation de Microsoft [Graph](/graph/teams-concept-overview).

En savoir plus sur l’obtention de contexte pour Teams [onglet ou](../tabs/how-to/access-teams-context.md) [bot.](../bots/how-to/get-teams-context.md)

## <a name="understand-authentication-options"></a>Comprendre les options d’authentification

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Azure Active Directory (AD) est le fournisseur d’identité pour Teams. Si votre application utilise un autre fournisseur d’identité, vous devez soit faire un exercice de mappage d’identité, soit combiner avec Azure AD.

Teams des mécanismes d' sign-on (SSO) avec Azure AD pour les applications tierces. Il fournit également des conseils pour les flux d’authentification à d’autres fournisseurs d’identité à l’aide de normes telles que OAuth et Open ID Connecter, appelés OIDC.

Pour SharePoint pages, vous pouvez uniquement utiliser l’oD unique et vous ne pouvez pas ajouter un autre ID Azure AD si vous souhaitez que l’oD unique fonctionne pour une autre application, car l’ID est l’SharePoint application.

En savoir plus sur [l’authentification dans Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Suivre les instructions Teams conception

***Scénarios d’intégration**: applications autonomes, applications de collaboration*

Veillez à suivre [Teams de conception](../concepts/design/understand-use-cases.md) pour que votre application soit native à Teams. Vous ne pouvez pas migrer le contenu d’une application existante vers Teams onglet. Pour plus d’informations sur la conception d’application, voir [Fluent Design System.](https://fluentsite.z22.web.core.windows.net/)

## <a name="maximize-deep-linking"></a>Optimiser la liaison profonde

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Utilisez [des liens profonds](../concepts/build-and-test/deep-links.md) pour lier votre application à Teams car ils relient plusieurs parties d’une application pour une expérience Teams native.

## <a name="be-smart-when-messaging-users"></a>Soyez intelligent lors de la messagerie des utilisateurs

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Utilisez un [bot dans](../bots/what-are-bots.md) votre application Teams pour les conversations multi-threads, car il offre plus de flexibilité qu’un [webhook.](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

Les bots vous permettent également d’envoyer des **messages proactifs** à des utilisateurs individuels ou à des canaux. Les messages proactifs sont des messages non improvisés déclenchés par un événement externe et non un message envoyé à un bot. Par exemple, votre bot envoie un message de bienvenue lorsqu’il est installé ou qu’un nouvel utilisateur rejoint un canal. 

L’envoi de messages proactifs Teams identificateurs spécifiques. Vous pouvez capturer les informations en extraire des données de liste ou de profil [utilisateur,](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)en vous abonnant à des [événements de conversation](../bots/how-to/conversations/subscribe-to-conversation-events.md)ou en utilisant Microsoft [Graph](/graph/teams-proactive-messaging).

Ne pas envoyer de courrier indésirable aux utilisateurs avec des messages excessifs. Si la fonctionnalité Teams la prend en charge, les utilisateurs peuvent configurer les paramètres de notification pour votre application.   
Voici un exemple de message de notification : **Ne m’envoyez pas de messages non sollicités.**

## <a name="use-sharepoint-for-file-and-data-storage"></a>Utiliser les SharePoint pour le stockage de fichiers et de données

***Scénarios d’intégration :** Applications autonomes, applications de collaboration, SharePoint pages*

Lorsqu’une équipe est créée, une [collection SharePoint de sites](/microsoftteams/sharepoint-onedrive-interact) est également mise en service pour prendre en charge le stockage de fichiers et de données pour cette équipe. Votre application doit tirer parti de cette fonctionnalité si elle interagit avec des fichiers. Utilisez la collection de sites pour stocker des données brutes dans SharePoint listes et Excel.

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
