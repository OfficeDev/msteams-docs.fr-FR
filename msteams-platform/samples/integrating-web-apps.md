---
author: heath-hamilton
description: Meilleures pratiques ou considérations relatives à l’intégration d’applications web existantes à Microsoft Teams
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: Considérations relatives à l’intégration de Teams
ms.openlocfilehash: e963019783699ebe0ed20b8e45632d03d6631e71
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757639"
---
# <a name="considerations-for-teams-integration"></a>Considérations relatives à l’intégration de Teams

Vous pouvez rendre les applications web adaptées aux fonctionnalités sociales et collaboratives de Teams, en les intégrant correctement à Teams.
  
Les différents types d’applications que vous pouvez intégrer à Teams sont les suivants :

* **applications autonomes**: une application autonome est une application à page unique ou volumineuse et complexe. L’utilisateur peut utiliser certains aspects de celui-ci dans Teams.
* **Applications de collaboration**: une application déjà conçue pour les fonctionnalités sociales et collaboratives inhérentes à Teams.
* **SharePoint** : page SharePoint que vous souhaitez afficher dans Teams.

Vous pouvez mapper et suivre les instructions appropriées applicables à votre scénario d’intégration.
Ce document donne une vue d’ensemble des fonctionnalités teams, des exigences de point de partage pour le stockage de fichiers et de données, des exigences d’API, de l’authentification et de la liaison approfondie de votre application avec Teams.

## <a name="get-to-know-teams-platform-capabilities"></a>Découvrir les fonctionnalités de la plateforme Teams

***scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Votre application Teams doit inclure les fonctionnalités de collaboration requises et attendues. Pour utiliser l’intégration d’applications, il est important de se familiariser avec Teams terminologie de développement.

|Fonctionnalités d’application courantes   |Fonctionnalités de la plateforme Teams   |
|----------|-----------|
|Page web incorporée, page d’accueil ou affichage web  |[Onglets](../tabs/what-are-tabs.md)  |
|Partager des raccourcis et des extensions  |[Extensions de messages](../messaging-extensions/what-are-messaging-extensions.md)  |
|Raccourcis et extensions d’action  |[Extensions de messages](../messaging-extensions/what-are-messaging-extensions.md)  |
|Bots conversationnels |[Bots](../bots/what-are-bots.md) |
|Notifications du canal  |[Bots](../bots/what-are-bots.md)<br/>[webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Connecteurs Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Envoyer un message aux services externes  |[Bots](../bots/what-are-bots.md)<br/>[webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modales  |[Modules de tâche](../task-modules-and-cards/what-are-task-modules.md)  |
|Cartes riches en contenu  |[Cartes adaptatives](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Déterminer un sous-ensemble de fonctionnalités

***scénarios d’intégration**: applications autonomes*

Intégrer toutes les fonctionnalités d'une application existante dans Teams conduit souvent à une expérience utilisateur forcée ou non naturelle, en particulier pour les applications de grande taille. Commencez par les fonctionnalités les plus percutantes et celles qui s’intègrent plus naturellement à Teams. Vous pouvez autoriser les utilisateurs à lancer l’application principale et à accéder à son ensemble complet de fonctionnalités.

Voici les conditions préalables à l’intégration de votre application à Teams.

1. [mappez les cas d’usage de votre application aux fonctionnalités de la plateforme Teams](../concepts/design/map-use-cases.md).
1. [Déterminer les points d’entrée de votre application](../concepts/extensibility-points.md). Est-ce à des fins personnelles, de collaboration ou pour les deux ?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprendre les exigences et les options de SharePoint

***scénarios d’intégration**: SharePoint*

Pour intégrer une page SharePoint [existante](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model) sous la forme d’un onglet Teams, vous devez prendre en compte les éléments suivants :

* Il doit s’agir d’une page *moderne* SharePoint Online.
* Seuls les onglets personnels sont pris en charge. Vous ne pouvez pas intégrer votre page en tant qu’onglet de canal.

Vous pouvez également créer un onglet Teams [à l’aide de l’infrastructure SharePoint](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multitenancy"></a>Visez l’architecture mutualisée

***scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Si votre application est utilisée par plusieurs organisations, envisagez l’hébergement multilocataire. Cela rend votre produit évolutif et simplifie la distribution.

## <a name="review-your-apis"></a>Passer en revue vos API

***scénarios d’intégration**: applications autonomes, applications de collaboration*

Les API et les structures de données de votre application doivent prendre en charge l’application lors de l’intégration à Teams. Pour étendre la prise en charge, vous devez augmenter les API et les structures de données avec des informations contextuelles sur Teams pour de [mappage d’identité](../concepts/authentication/configure-identity-provider.md), [prise en charge des liens profonds](../concepts/build-and-test/deep-links.md)et [incorporer Microsoft Graph](/graph/teams-concept-overview).

Découvrez comment obtenir le contexte de votre [d’onglet Teams](../tabs/how-to/access-teams-context.md) ou [bot](../bots/how-to/get-teams-context.md).

## <a name="understand-authentication-options"></a>Comprendre les options d’authentification

***scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Azure Active Directory est le fournisseur d’identité pour Teams. Si votre application utilise un autre fournisseur d’identité, vous devez effectuer un exercice de mappage d’identité ou combiner avec Microsoft Azure Active Directory (Azure AD).

Teams dispose de mécanismes d’authentification unique (SSO) avec Azure AD pour les applications tierces. Il fournit également des conseils pour les flux d’authentification à d’autres fournisseurs d’identité à l’aide de normes telles que OAuth et Open ID Connect, appelées OIDC.

> [!IMPORTANT]
> Actuellement, les applications tierces sont disponibles dans Cloud de la communauté du secteur public (GCC), mais ne sont pas disponibles pour GCC-High et le Ministère de la défense (DOD). Les applications tierces sont désactivées par défaut pour GCC. Pour activer des applications tierces pour GCC, consultez [gérer les stratégies d’autorisation d’application](/microsoftteams/teams-app-permission-policies) et [gérer les applications](/microsoftteams/manage-apps).

Pour SharePoint pages, vous pouvez uniquement utiliser l’authentification unique et ne pouvez pas ajouter un autre ID Azure AD si vous souhaitez que l’authentification unique fonctionne pour une autre application, car l’ID est l’application SharePoint.

En savoir plus sur [l’authentification dans Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Suivez les instructions de conception teams

***scénarios d’intégration**: applications autonomes, applications de collaboration*

Veillez à suivre les instructions de conception [Teams](../concepts/design/understand-use-cases.md) pour rendre votre application native dans Teams. Vous ne pouvez pas migrer un contenu d’application existant vers un onglet Teams. Pour plus d’informations sur la conception d’applications, consultez [Système Fluent Design](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Optimiser la liaison approfondie

***scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Utilisez [liens profonds](../concepts/build-and-test/deep-links.md) pour lier votre application à Teams, car ils relient plusieurs éléments d’une application pour une expérience Teams plus native.

## <a name="be-smart-when-messaging-users"></a>Soyez intelligent lors de la messagerie des utilisateurs

***scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Utilisez un [bot](../bots/what-are-bots.md) dans votre application Teams pour une conversation multithread, car il offre plus de flexibilité qu’un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Les bots vous permettent également d’envoyer **messages proactifs** à des utilisateurs ou canaux individuels. Les messages proactifs sont des messages non traités déclenchés par un événement externe et non envoyés à un bot. Par exemple, votre bot envoie un message de bienvenue lorsqu’il est installé ou qu’un nouvel utilisateur rejoint un canal.

L’envoi de messages proactifs nécessite des identificateurs spécifiques à Teams. Vous pouvez capturer les informations en [extrayant la liste ou les données de profil utilisateur](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [en vous abonnant aux événements de conversation](../bots/how-to/conversations/subscribe-to-conversation-events.md)ou en utilisant [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams).

Ne pas envoyer de courrier indésirable aux utilisateurs avec des messages excessifs. Si la fonctionnalité Teams la prend en charge, les utilisateurs peuvent configurer les paramètres de notification pour votre application.
Voici un exemple de message de notification : **ne m’envoyez pas de messages non traités**.

## <a name="use-sharepoint-for-file-and-data-storage"></a>Utiliser SharePoint pour le stockage de fichiers et de données

scénarios d’intégration ***: applications autonomes**, applications de collaboration, pages SharePoint*

Lorsqu’une équipe est créée, une de [collection de sites SharePoint](/microsoftteams/sharepoint-onedrive-interact) est également configurée pour prendre en charge le stockage de fichiers et de données pour cette équipe. Votre application doit tirer parti de cette fonctionnalité si elle interagit avec des fichiers. Utilisez la collection de sites pour stocker des données brutes dans les listes SharePoint et Microsoft Excel.

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [solutions à code faible et sans code pour Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Partager vers Teams à partir d’applications web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [attributs de cookie SameSite](~/resources/samesite-cookie-update.md)
* [intégrer chatbot Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
