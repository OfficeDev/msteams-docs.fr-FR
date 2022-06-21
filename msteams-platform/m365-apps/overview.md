---
title: Étendre les applications Teams à travers Microsoft 365 (version préliminaire)
description: Découvrez comment créer et mettre à jour vos expériences d’application Teams vers d’autres zones de Microsoft 365 à forte utilisation.
ms.date: 05/24/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: a595626fab5a8e3d98e45066392cfad8d7604a22
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189883"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Étendre Teams applications à travers Microsoft 365

Avec les dernières versions de Microsoft Teams Kit de développement logiciel ([SDK) client JavaScript](../tabs/how-to/using-teams-client-sdk.md) (version 2.0.0), [Teams manifeste d’application](../resources/schema/manifest-schema.md) (version 1.13) et [Teams Toolkit](../toolkit/visual-studio-code-overview.md), vous pouvez créer et mettre à jour Teams applications pour qu’elles s’exécutent dans d’autres produits Microsoft 365 à utilisation élevée et les publient sur la Place de marché commerciale Microsoft ([ Microsoft AppSource](https://appsource.microsoft.com/)).

L’extension de votre application Teams sur Microsoft 365 offre un moyen simplifié de fournir des applications multiplateformes à un public d’utilisateurs étendu : à partir d’une base de code unique, vous pouvez créer des expériences d’application adaptées aux environnements Teams, Outlook et Office. Les utilisateurs finaux n’auront pas à quitter le contexte de leur travail pour utiliser votre application, et les administrateurs bénéficient d’un workflow de gestion et de déploiement consolidé.

La plateforme d’applications Teams continue d’évoluer et de s’étendre de manière holistique à l’écosystème Microsoft 365. Voici la prise en charge actuelle des éléments de plateforme d’application Teams dans Microsoft 365 (Teams, Outlook et Office en tant qu’hôtes d’applications) :

|          | Élément de manifeste d’application | prise en charge Teams |prise en charge de Outlook* | prise en charge de Office* | Remarques |
|--|--|--|--|--|--|
| [**Onglets**](../tabs/what-are-tabs.md) (étendue personnelle)    |`staticTabs`  | Web, Bureau, Mobile | Web (version ciblée), Bureau (canal bêta) | Web (version ciblée)| Étendue de canal et de groupe non encore prise en charge pour Microsoft 365. Consultez [les notes](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Extensions de message**](../messaging-extensions/what-are-messaging-extensions.md) (basées sur la recherche)| `composeExtensions` | Web, Bureau, Mobile| Web (version ciblée), Bureau (canal bêta)| - |L’action n’est pas encore prise en charge pour Microsoft 365. Consultez [les notes](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook). |
| [**connecteurs Graph**](/graph/connecting-external-content-connectors-overview)| `graphConnector` | Web, Bureau, Mobile| Web, Bureau | Web| Voir [les notes](#graph-connectors)
| [**compléments Office**](/office/dev/add-ins/develop/json-manifest-overview) (préversion) | `extensions` | - | Web, Bureau | - | Disponible uniquement dans la version [du manifeste devPreview](../resources/schema/manifest-schema-dev-preview.md) . Consultez [les notes](#office-add-ins-preview).|

\*[L’option de publication ciblée Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) et [l’inscription de canal de mise à jour Microsoft 365 Apps](/deployoffice/change-update-channels) nécessitent l’adhésion de l’administrateur pour l’ensemble de l’organisation ou des utilisateurs sélectionnés. Les canaux de mise à jour sont spécifiques à l’appareil et s’appliquent uniquement aux installations de Office en cours d’exécution sur Windows.

Pour obtenir des conseils sur le manifeste d’application Teams et le guide de gestion des versions du Kit de développement logiciel (SDK), ainsi que d’autres informations sur la prise en charge actuelle des fonctionnalités de plateforme Teams dans Microsoft 365, consultez la [vue d’ensemble du kit de développement logiciel (SDK) client JavaScript Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Nous accueillons vos commentaires et vos rapports de problèmes à mesure que vous développez Teams applications pour qu’elles s’exécutent dans l’écosystème Microsoft 365! Utilisez les canaux de [communauté de développeurs Microsoft Teams](/microsoftteams/platform/feedback) standard pour envoyer des commentaires.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Onglets personnels et extensions de messagerie dans Outlook et Office

Atteignez vos utilisateurs là où ils se trouvent, dans le contexte de leur travail, en étendant votre application web en tant qu’application d’onglet personnel Teams qui s’exécute également dans Outlook et Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Les onglets personnels s’exécutant dans Outlook, Office et Teams":::

Vous pouvez également étendre vos extensions de message de Teams basées sur la recherche à Outlook sur le web et Windows bureau, ce qui permet à vos clients de rechercher et de partager des résultats via la zone de rédaction de messages de Outlook, en plus de Microsoft Teams clients.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extension de message en cours d’exécution dans Outlook et Teams":::

La création de votre application avec le [dernier manifeste d’application Teams](../resources/schema/manifest-schema.md) et [Teams SDK client JavaScript](../tabs/how-to/using-teams-client-sdk.md) vous offre un processus de développement consolidé. En vous permettant d’offrir à vos clients une expérience rationalisée de déploiement, d’installation et d’administration, vous pouvez étendre la portée et l’utilisation potentielles de votre application.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Utiliser Teams manifeste d’application dans Microsoft 365

Dans le but de simplifier et de simplifier l’écosystème des développeurs Microsoft 365, nous continuons à étendre le manifeste de l’application Teams à d’autres domaines de Microsoft 365 avec les éléments suivants.

### <a name="graph-connectors"></a>connecteurs Graph

Avec les connecteurs Microsoft Graph, votre organisation peut indexer des données tierces afin qu’elles apparaissent sous forme de résultats Recherche Microsoft, en développant les types de sources de contenu pouvant faire l’objet d’une recherche dans vos applications Teams.
Pour plus d’informations, consultez [la vue d’ensemble des connecteurs Microsoft Graph pour Recherche Microsoft](/microsoftsearch/connectors-overview).

Pour commencer à utiliser les connecteurs de graphe dans Teams applications, consultez [l’exemple de connecteurs Graph Teams Toolkit](https://aka.ms/teamsfx-graph-connector-sample) et Microsoft Teams référence de [schéma de manifeste en préversion du développeur](../resources/schema/manifest-schema-dev-preview.md).

### <a name="office-add-ins-preview"></a>compléments Office (préversion)

Vous pouvez maintenant définir et déployer des compléments Office dans la [préversion développeur](../resources/schema/manifest-schema-dev-preview.md) du manifeste d’application Microsoft Teams. Actuellement, cette préversion est limitée à Outlook compléments exécutés sur des Office d’abonnement pour Windows.

Pour plus d’informations, consultez [Manifeste Teams pour les compléments Office (préversion).](/office/dev/add-ins/develop/json-manifest-overview)

## <a name="microsoft-appsource-submission"></a>Soumission Microsoft AppSource

Rejoignez le nombre croissant d’applications de production Teams dans le Magasin [Microsoft AppSource](https://appsource.microsoft.com/) avec une prise en charge étendue des audiences Outlook et Office (version ciblée). Le processus de soumission d’applications [pour Teams applications activées pour Outlook et Office](../concepts/deploy-and-publish/appsource/publish.md) est le même que pour les applications Teams traditionnelles. La seule différence est que vous allez utiliser Teams manifeste d’application [version 1.13](../tabs/how-to/using-teams-client-sdk.md) dans votre package d’application, ce qui introduit la prise en charge des applications Teams qui s’exécutent sur Microsoft 365.

Une fois publiée en tant qu’application Teams compatible Microsoft 365, votre application est détectable en tant qu’application installable à partir des magasins Outlook et application Office, en plus du magasin Teams. Lors de l’exécution dans Outlook et Office, votre application utilise les mêmes autorisations accordées dans Teams. Teams administrateurs peuvent [gérer l’accès aux applications Teams dans Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) pour les utilisateurs de leur organisation.

Pour plus d’informations, consultez [Publier des applications Teams pour Microsoft 365](publish.md).

## <a name="next-step"></a>Étape suivante

Configurez votre environnement de développement pour créer des applications Teams pour Microsoft 365 :

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)
