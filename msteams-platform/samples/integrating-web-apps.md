---
author: heath-hamilton
description: Meilleures pratiques pour intégrer les applications Web existantes avec Microsoft Teams
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

Vous pouvez rendre les applications Web adaptées aux fonctionnalités sociales et collaboratives de Teams, en les intégrant correctement aux Teams.
  
Les différents types d’applications que vous pouvez intégrer à Teams sont les suivants :
* **Applications autonomes : Une** application autonome est une application d’une page ou d’une grande, complexe. L’utilisateur peut utiliser certains aspects de celui-ci dans Teams.
* **Applications de collaboration**: Application déjà conçue pour les fonctionnalités sociales et collaboratives inhérentes à Teams.
* **SharePoint**: Une page SharePoint que vous souhaitez faire surface dans Teams.

Vous pouvez cartographier et suivre les lignes directrices appropriées applicables à votre scénario d’intégration.
Ce document donne un aperçu des capacités de Teams, des exigences de points de partage pour le stockage de fichiers et de données, des exigences de l’API, de l’authentification et de la liaison profonde de votre application avec Teams.
 
## <a name="get-to-know-teams-platform-capabilities"></a>Faites la Teams de la plateforme

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Votre application Teams doit inclure les fonctionnalités collaboratives requises et attendues. Pour travailler avec l’intégration d’applications, il est important de se familiariser avec Teams terminologie de développement.

|Fonctionnalités d’application courantes   |Teams de plate-forme   |
|----------|-----------|
|Page Web intégrée, page d’accueil ou webview  |[Onglets](../tabs/what-are-tabs.md)  |
|Partager des raccourcis et des extensions  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Raccourcis d’action et extensions  |[Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots (Chatbots)  |[Bots](../bots/what-are-bots.md) |
|Notifications de canal  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks entrants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Connecteurs Office 365](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Messages services externes  |[Bots](../bots/what-are-bots.md)<br/>[Webhooks sortants](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modalités  |[Modules de tâche](../task-modules-and-cards/what-are-task-modules.md)  |
|Cartes riches en contenu  |[Cartes adaptatives](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>Déterminer un sous-ensemble de fonctionnalités

***Scénarios d’intégration**: Applications autonomes*

L’intégration de toutes les fonctionnalités d’une application existante dans Teams conduit souvent à une expérience utilisateur forcée ou contre nature, en particulier dans les applications plus grandes. Commencez par les fonctionnalités les plus perspicaces et celles qui s’intègrent plus naturellement Teams. Vous pouvez permettre aux utilisateurs de lancer l’application principale et d’accéder à son ensemble complet de fonctionnalités.

**Conditions préalables pour intégrer votre application à Teams** Voici les conditions préalables pour intégrer votre application à Teams. 

1. [Cartographiez les cas d’utilisation de votre application pour Teams capacités de la plate-forme](../concepts/design/map-use-cases.md).
1. [Déterminez les points d’entrée de votre application](../concepts/extensibility-points.md). Est-ce pour un usage personnel, la collaboration, ou les deux?

## <a name="understand-sharepoint-requirements-and-options"></a>Comprendre SharePoint exigences et les options

***Scénarios d’intégration**: SharePoint*

Pour intégrer une [page SharePoint existante comme](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) onglet Teams, vous devez tenir compte des éléments suivants :

* Il doit s’agir *d’une* page SharePoint en ligne moderne.
* Seuls les onglets personnels sont pris en charge. Vous ne pouvez pas intégrer votre page comme onglet canal.

Alternativement, vous pouvez construire un onglet Teams en [utilisant le SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).

## <a name="aim-towards-multi-tenancy"></a>Viser la multi-location

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Si votre application est utilisée par plusieurs organisations, envisagez l’hébergement multi-locataires qui rend votre produit évolutif et simplifie considérablement la distribution.

## <a name="review-your-apis"></a>Passez en revue vos API

***Scénarios d’intégration**: applications autonomes, applications de collaboration*

Vous devez faire en sorte que les API et structures de données existantes de votre application soutiennent l’application lors de l’intégration Teams. Pour étendre le support, vous devez augmenter les API et les structures de données avec des informations contextuelles sur les Teams pour la [cartographie d’identité,](../concepts/authentication/configure-identity-provider.md) [le support de lien](../concepts/build-and-test/deep-links.md)profond, et [l’intégration de Microsoft Graph](/graph/teams-concept-overview).

En savoir plus sur l’obtention de contexte pour Teams [onglet ou](../tabs/how-to/access-teams-context.md) [bot](../bots/how-to/get-teams-context.md).

## <a name="understand-authentication-options"></a>Comprendre les options d’authentification

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Azure Active Directory (AD) est le fournisseur d’identité pour Teams. Si votre application utilise un autre fournisseur d’identité, vous devez soit faire un exercice de cartographie d’identité, soit combiner avec Azure AD.

Teams dispose de mécanismes de connect-on unique (SSO) avec Azure AD pour les applications tierces. Il fournit également des conseils pour les flux d’authentification à d’autres fournisseurs d’identité en utilisant des normes telles que OAuth et Open ID Connecter, connu sous le nom OIDC.

Pour SharePoint pages, vous ne pouvez utiliser SSO et ne pouvez pas ajouter un autre identifiant D’ANNONCE Azure si vous souhaitez que SSO fonctionne pour une autre application car l’ID est l’application SharePoint.

En savoir plus sur [l’authentification Teams](../concepts/authentication/authentication.md).

## <a name="follow-teams-design-guidelines"></a>Suivez les Teams de conception

***Scénarios d’intégration**: applications autonomes, applications de collaboration*

Assurez-vous de [suivre Teams de conception](../concepts/design/understand-use-cases.md) pour rendre votre application native à Teams. Vous ne pouvez pas migrer un contenu d’application existant vers Teams onglet. Pour plus d’informations sur la conception d’applications, [voir Fluent Design System](https://fluentsite.z22.web.core.windows.net/).

## <a name="maximize-deep-linking"></a>Maximiser les liens profonds

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Vous pouvez créer des liens vers des informations et des fonctionnalités dans Teams. Utilisez [des liens profonds](../concepts/build-and-test/deep-links.md) pour lier votre application avec Teams car ils relient plusieurs pièces d’une application pour une expérience plus Teams native.

## <a name="be-smart-when-messaging-users"></a>Soyez intelligent lorsque les utilisateurs de messagerie

***Scénarios d’intégration**: applications autonomes, applications de collaboration, SharePoint*

Utilisez un [bot](../bots/what-are-bots.md) dans votre application Teams pour une conversation multi-threaded, car il offre plus de flexibilité qu’un [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).

Bots vous permet également d’envoyer des **messages proactifs** aux utilisateurs individuels ou aux canaux. Les messages proactifs sont des messages non sollicités déclenchés par un événement extérieur et non un message envoyé à un bot. Par exemple, votre bot envoie un message de bienvenue lorsqu’il est installé ou qu’un nouvel utilisateur rejoint un canal. 

L’envoi de messages proactifs nécessite Teams identificateurs spécifiques à chaque entreprise. Vous pouvez capturer les informations en [récupérant des données de liste ou de profil d’utilisateur,](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile) [en vous abonnant](../bots/how-to/conversations/subscribe-to-conversation-events.md)à des événements de conversation ou [en utilisant Microsoft Graph](/graph/teams-proactive-messaging).

Ne spammez pas les utilisateurs avec des messages excessifs. Si la Teams supporte, les utilisateurs peuvent configurer les paramètres de notification de votre application.   
Voici un exemple de message de notification : **ne m’envoyez pas de messages non sollicités.**

## <a name="use-sharepoint-for-file-and-data-storage"></a>Utilisez des SharePoint pour le stockage de fichiers et de données

***Scénarios d’intégration :** Applications autonomes, applications de collaboration, SharePoint pages*

Lorsqu’une équipe est créée, une [SharePoint de site](/microsoftteams/sharepoint-onedrive-interact) est également mise à disposition pour prendre en charge le stockage des fichiers et des données pour cette équipe. Votre application doit tirer parti de cette fonctionnalité si elle interagit avec les fichiers. Utilisez la collection du site pour stocker des données brutes dans SharePoint listes et Excel.

## <a name="see-also"></a>Voir aussi

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
