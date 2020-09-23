---
author: heath-hamilton
description: Meilleures pratiques pour l’intégration d’applications Web existantes à Microsoft teams
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Intégration d’une application Web à Microsoft teams
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210272"
---
# <a name="integrate-web-apps-with-teams"></a>Intégration des applications Web à teams

Disposez-vous d’une application Web dont vous pensez qu’elle s’ajuste naturellement aux fonctionnalités sociales et collaboratives de teams ? Ces instructions peuvent vous aider à comprendre comment intégrer les types d’applications suivants :

* **Applications autonomes**: il peut s’agir d’une application à page unique ou d’une application complexe de grande taille sur laquelle vous souhaitez que les utilisateurs puissent utiliser certains aspects de dans Teams.
* **Applications de collaboration**: application déjà conçue pour les fonctionnalités sociales et de collaboration inhérentes à Teams.
* **SharePoint**: page SharePoint que vous souhaitez placer dans Teams.

Pour chaque instruction, vous pouvez voir si elle s’applique à votre scénario d’intégration.

## <a name="get-to-know-teams-platform-capabilities"></a>Découverte des fonctionnalités de la plateforme teams

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint *

Votre application de teams peut inclure des fonctionnalités que les utilisateurs veulent et peuvent attendre lors de la collaboration, mais vous n’êtes peut-être pas familiarisé avec la terminologie de développement de teams.

|Fonctionnalités d’application communes   |Fonctionnalités de la plateforme teams   |
|----------|-----------|
|Page Web, page d’accueil ou WebView incorporée  |[Onglets](../tabs/what-are-tabs.md)  |
|Partager des raccourcis et des extensions  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Raccourcis et extensions d’action  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[Bots](../bots/what-are-bots.md) |
|Notifications de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Connecteurs Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Services externes de message  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modaux  |[Modules de tâche](../task-modules-and-cards/what-are-task-modules.md)  |
|Cartes riches en contenu  |[Cartes adaptatives](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Déterminer un sous-ensemble de fonctionnalités

***Scénarios d’intégration**: applications autonomes *

L’intégration de toutes les fonctionnalités d’une application existante dans teams conduit souvent à une expérience utilisateur forcée ou non naturelle, en particulier dans les applications plus volumineuses. Envisagez de commencer avec les fonctionnalités les plus percutantes et celles qui s’intégreront plus naturellement à Teams. N’oubliez pas que vous pouvez toujours autoriser les utilisateurs à lancer l’application principale et à accéder à son ensemble complet de fonctionnalités.

Avant de commencer toute tâche technique, effectuez une planification pour votre application teams :

1. [Mappez les cas d’utilisation de votre application aux fonctionnalités de la plateforme teams](../concepts/design/map-use-cases.md).
1. [Déterminez les points d’entrée de votre application](../concepts/extensibility-points.md). S’agit-il d’une utilisation personnelle, d’une collaboration ou des deux ?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprendre les options et les conditions requises pour SharePoint

***Scénarios d’intégration**: SharePoint *

Vous pouvez intégrer une [page SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) existante en tant qu’onglet Teams. Souvenez-vous des éléments suivants :

* Il doit s’agir d’une page SharePoint Online *moderne*
* Seuls les onglets personnels sont pris en charge (vous ne pouvez pas intégrer votre page en tant qu’onglet de canal)

Vous pouvez également créer un onglet teams [à l’aide de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Objectif de l’architecture mutualisée

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint *

Si votre application est utilisée par plusieurs organisations, envisagez l’hébergement sur plusieurs clients qui permettrait à votre produit d’être évolutif et simplifiant grandement la distribution.

## <a name="review-your-apis"></a>Vérifier vos API

***Scénarios d’intégration**: applications autonomes, applications de collaboration *

Ne partez pas du principe que les API et structures de données existantes de votre application prennent entièrement en charge l’application lorsqu’elle est intégrée à Teams. Vous devrez peut-être les enrichir avec des informations contextuelles sur teams pour le [mappage des identités](../concepts/authentication/configure-identity-provider.md), la [prise en charge des liens détaillés](../concepts/build-and-test/deep-links.md)et l' [incorporation de Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).

En savoir plus sur l’obtention de contexte pour l' [onglet](../tabs/how-to/access-teams-context.md) ou le [bot](../bots/how-to/get-teams-context.md)de votre équipe.

## <a name="understand-authentication-options"></a>Comprendre les options d’authentification

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint *

Azure Active Directory (AD) est le fournisseur d’identité pour Teams. Si votre application utilise un fournisseur d’identité différent, vous devez effectuer un exercice de mappage des identités ou fédérer avec Azure AD.

Teams possède des mécanismes d’authentification unique (SSO) avec Azure AD pour les applications tierces et des conseils pour les flux d’authentification vers d’autres fournisseurs d’identité à l’aide de normes telles que OAuth et Open ID Connect (OIDC).

Pour les pages SharePoint, vous pouvez utiliser uniquement l’authentification unique et ne peut pas ajouter un autre ID Azure AD si vous souhaitez que l’authentification unique fonctionne pour une autre application (étant donné que l’ID est l’application SharePoint).

En savoir plus sur [l’authentification dans teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Suivre les instructions de conception de teams

***Scénarios d’intégration**: applications autonomes, applications de collaboration *

En règle générale, votre application doit sembler naturelle dans Teams. Vous pouvez envisager de migrer le contenu d’une application existant vers un onglet Teams, mais nous vous recommandons vivement d’utiliser les [instructions de conception de teams](../concepts/design/understand-use-cases.md). Voir aussi : [système de conception Fluent](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Optimiser la liaison profonde

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint *

Tout le long de teams peut être lié directement à un [lien profond](../concepts/build-and-test/deep-links.md). Votre application doit optimiser l’utilisation de ces éléments, notamment les liens vers et à partir de messages et de contenu de tabulation spécifiques. Les liens détaillés peuvent véritablement relier plusieurs parties d’une application pour une expérience plus native de teams.

## <a name="be-smart-when-messaging-users"></a>Soyez intelligent lorsque les utilisateurs de messagerie

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint *

Examinez les types de messages que votre application de teams peut envoyer maintenant et à long terme. Si vous pensez que votre application aura toujours une conversation multithread, un [bot](../bots/what-are-bots.md) peut offrir davantage de flexibilité qu’un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Les robots vous permettent également d’envoyer des *messages proactifs* à des utilisateurs ou à des canaux individuels. Il s’agit des messages non invités déclenchés par un événement extérieur et non d’un message envoyé à un bot. (Par exemple, votre robot peut envoyer un message de bienvenue lorsqu’il est installé ou un nouvel utilisateur rejoint un canal.) 

L’envoi de messages proactifs nécessite des identificateurs spécifiques à teams : vous pouvez capturer ces informations en [extrayant des données de liste ou de profil utilisateur](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile), en vous [abonnant à des événements de conversation](../bots/how-to/conversations/subscribe-to-conversation-events.md)ou à l’aide de [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).

N’oubliez pas que les utilisateurs de courrier indésirable possèdent trop de messages. Si la fonctionnalité teams le prend en charge, pensez à autoriser les utilisateurs à configurer les paramètres de notification de votre application (par exemple, « ne pas m’envoyer de messages non sollicités ».).

## <a name="use-sharepoint-for-file-and-data-storage"></a>Utiliser SharePoint pour le stockage de fichiers et de données

***Scénarios d’intégration :** Applications autonomes, applications de collaboration, pages SharePoint*

Lorsqu’une équipe est créée, une [collection de sites SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) est également configurée pour prendre en charge le stockage de fichiers et de données pour cette équipe. Votre application peut et doit utiliser cette fonctionnalité si elle interagit avec des fichiers. Vous pouvez également utiliser la collection de sites pour stocker des données brutes dans des listes SharePoint et Excel.
