---
author: heath-hamilton
description: Meilleures pratiques ou considérations relatives à l’intégration d’applications web existantes à Microsoft Teams
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: Considérations relatives à l’intégration de Teams
ms.openlocfilehash: eb278d078c7b195ff5d2d2a2f980ffc9db74f748
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685596"
---
# <a name="considerations-for-teams-integration"></a>Considérations relatives à l’intégration de Teams

Vous pouvez rendre les applications web adaptées aux fonctionnalités sociales et collaboratives de Teams en les intégrant correctement à Teams.
  
Les différents types d’applications que vous pouvez intégrer à Teams sont les suivants :

* **Applications autonomes** : une application autonome est une application monopage ou volumineuse et complexe. L’utilisateur peut utiliser certains aspects de celui-ci dans Teams.
* **Applications de collaboration** : une application déjà conçue pour les fonctionnalités sociales et collaboratives inhérentes à Teams.
* **SharePoint** : page SharePoint que vous souhaitez afficher dans Teams.

Vous pouvez mapper et suivre les instructions appropriées applicables à votre scénario d’intégration.
Ce document donne une vue d’ensemble des fonctionnalités de Teams, des exigences de point de partage pour le stockage de fichiers et de données, des exigences d’API, de l’authentification et de la liaison approfondie de votre application avec Teams.

## <a name="get-to-know-teams-platform-capabilities"></a>Découvrir Teams fonctionnalités de la plateforme

***Scénarios d’intégration** : applications autonomes, applications de collaboration, SharePoint*

Votre application Teams doit inclure les fonctionnalités collaboratives requises et attendues. Pour utiliser l’intégration d’applications, il est important de se familiariser avec Teams terminologie de développement.

|Fonctionnalités courantes de l’application   |fonctionnalités de plateforme Teams   |
|----------|-----------|
|Page web incorporée, page d’accueil ou vue web  |[Onglets](../tabs/what-are-tabs.md)  |
|Partager des raccourcis et des extensions  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Raccourcis et extensions d’action  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots |[Bots](../bots/what-are-bots.md) |
|Notifications de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Connecteurs Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Services externes de message  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modales  |[Modules de tâche](../task-modules-and-cards/what-are-task-modules.md)  |
|Cartes riches en contenu  |[Cartes adaptatives](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Déterminer un sous-ensemble de fonctionnalités

***Scénarios d’intégration** : applications autonomes*

L’intégration de toutes les fonctionnalités d’une application existante dans Teams entraîne souvent une expérience utilisateur forcée ou non naturelle, en particulier dans les applications plus volumineuses. Commencez par les fonctionnalités les plus percutantes et celles qui s’intègrent plus naturellement à Teams. Vous pouvez autoriser les utilisateurs à lancer l’application principale et à accéder à son ensemble complet de fonctionnalités.

Voici les conditions préalables à l’intégration de votre application à Teams.

1. [Mappez les cas d’utilisation de votre application aux fonctionnalités de la plateforme Teams](../concepts/design/map-use-cases.md).
1. [Déterminez les points d’entrée de votre application](../concepts/extensibility-points.md). Est-ce à des fins personnelles, pour la collaboration ou pour les deux ?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprendre SharePoint exigences et options

***Scénarios d’intégration** : SharePoint*

Pour intégrer une [page SharePoint](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model) existante sous la forme d’un onglet Teams, vous devez prendre en compte les éléments suivants :

* Il doit s’agir d’une page *en ligne SharePoint moderne*.
* Seuls les onglets personnels sont pris en charge. Vous ne pouvez pas intégrer votre page sous forme d’onglet de canal.

Vous pouvez également créer un onglet Teams [à l’aide de la SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multitenancy"></a>Viser l’architecture mutualisée

***Scénarios d’intégration** : applications autonomes, applications de collaboration, SharePoint*

Si votre application est utilisée par plusieurs organisations, envisagez l’hébergement multilocataire. Il rend votre produit évolutif et simplifie la distribution.

## <a name="review-your-apis"></a>Passer en revue vos API

***Scénarios d’intégration** : applications autonomes, applications de collaboration*

Les API et les structures de données de votre application doivent la prise en charge lors de l’intégration à Teams. Pour étendre la prise en charge, vous devez augmenter les API et les structures de données avec des informations contextuelles sur Teams pour le [mappage d’identités](../concepts/authentication/configure-identity-provider.md), la [prise en charge des liens profonds](../concepts/build-and-test/deep-links.md) et l’incorporation [de Microsoft Graph](/graph/teams-concept-overview).

Découvrez comment obtenir le contexte de votre [onglet](../tabs/how-to/access-teams-context.md) ou [bot](../bots/how-to/get-teams-context.md) Teams.

## <a name="understand-authentication-options"></a>Comprendre les options d’authentification

***Scénarios d’intégration** : applications autonomes, applications de collaboration, SharePoint*

Azure Active Directory est le fournisseur d’identité pour Teams. Si votre application utilise un autre fournisseur d’identité, vous devez effectuer un exercice de mappage d’identité ou combiner avec Microsoft Azure Active Directory (Azure AD).

Teams dispose de mécanismes d’authentification unique avec Azure AD pour les applications tierces. Il fournit également des conseils pour les flux d’authentification vers d’autres fournisseurs d’identité à l’aide de normes telles que OAuth et Open ID Connecter, appelées OIDC.

> [!IMPORTANT]
> Actuellement, les applications tierces sont disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais ne sont pas disponibles pour GCC-High et le ministère de la Défense (DOD). Les applications tierces sont désactivées par défaut pour Cloud de la communauté du secteur public. Pour activer des applications tierces pour Cloud de la communauté du secteur public, consultez [gérer les stratégies d’autorisation d’application](/microsoftteams/teams-app-permission-policies) et [gérer les applications](/microsoftteams/manage-apps).

Pour SharePoint pages, vous pouvez uniquement utiliser l’authentification unique et ne pouvez pas ajouter un autre ID Azure AD si vous souhaitez que l’authentification unique fonctionne pour une autre application, car l’ID est l’application SharePoint.

En savoir plus sur [l’authentification dans Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Suivre Teams instructions de conception

***Scénarios d’intégration** : applications autonomes, applications de collaboration*

Veillez à suivre [Teams instructions de conception](../concepts/design/understand-use-cases.md) pour rendre votre application native à Teams. Vous ne pouvez pas migrer un contenu d’application existant vers un onglet Teams. Pour plus d’informations sur la conception d’applications, consultez [Système Fluent Design](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Optimiser la liaison profonde

***Scénarios d’intégration** : applications autonomes, applications de collaboration, SharePoint*

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Utilisez [des liens profonds](../concepts/build-and-test/deep-links.md) pour lier votre application à Teams, car elles relient plusieurs éléments d’une application pour une expérience de Teams plus native.

## <a name="be-smart-when-messaging-users"></a>Soyez intelligent lors de la messagerie des utilisateurs

***Scénarios d’intégration** : applications autonomes, applications de collaboration, SharePoint*

Utilisez un [bot](../bots/what-are-bots.md) dans votre application Teams pour une conversation multithread, car il offre plus de flexibilité qu’un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Les bots vous permettent également d’envoyer des **messages proactifs** à des utilisateurs ou canaux individuels. Les messages proactifs sont des messages non promptés déclenchés par un événement externe et non un message envoyé à un bot. Par exemple, votre bot envoie un message de bienvenue lorsqu’il est installé ou qu’un nouvel utilisateur rejoint un canal.

L’envoi de messages proactifs nécessite des identificateurs spécifiques à Teams. Vous pouvez capturer les informations [en extrayant des données de liste ou de profil utilisateur](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [en vous abonnant à des événements de conversation](../bots/how-to/conversations/subscribe-to-conversation-events.md) ou en utilisant [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams).

Ne pas envoyer de courrier indésirable aux utilisateurs avec des messages excessifs. Si la fonctionnalité Teams la prend en charge, les utilisateurs peuvent configurer les paramètres de notification pour votre application.
Voici un exemple de message de notification : **ne m’envoyez pas de messages non dépossés**.

## <a name="use-sharepoint-for-file-and-data-storage"></a>Utiliser SharePoint pour le stockage de fichiers et de données

***Scénarios d’intégration :** Applications autonomes, applications de collaboration, pages SharePoint*

Lorsqu’une équipe est créée, une [collection de sites SharePoint](/microsoftteams/sharepoint-onedrive-interact) est également configurée pour prendre en charge le stockage de fichiers et de données pour cette équipe. Votre application doit tirer parti de cette fonctionnalité si elle interagit avec des fichiers. Utilisez la collection de sites pour stocker des données brutes dans SharePoint Listes et Microsoft Excel.

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Solutions à faible code et sans code pour Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Partager vers Teams à partir d’applications web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Attributs de cookie SameSite](~/resources/samesite-cookie-update.md)
* [Intégrer Power Virtual Agents chatbot](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
