---
title: Étendre les applications Teams à travers Microsoft 365 (version préliminaire)
description: Découvrez comment créer, mettre à jour et étendre votre application Teams sur Microsoft M365 (Teams, Outlook et Office en tant qu’hôtes d’applications). Soumission Microsoft AppSource.
ms.date: 05/24/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 835af580a23a5fa4bcf99bf5fd2f091d076df489
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100617"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Étendre Teams applications à travers Microsoft 365

Avec les dernières versions du Kit de développement logiciel ( [SDK) client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) (version 2.0.0 et ultérieure), du [manifeste d’application Teams](../resources/schema/manifest-schema.md) (version 1.13 et ultérieure) et du [Kit](../toolkit/visual-studio-code-overview.md) de ressources Teams, vous pouvez créer et mettre à jour des applications Teams pour qu’elles s’exécutent dans d’autres produits Microsoft 365 à utilisation élevée et les publient sur la Place de marché commerciale Microsoft ([place de marché commerciale Microsoft](https://appsource.microsoft.com/)).

L’extension de votre application Teams dans Microsoft 365 offre un moyen simplifié de fournir des applications multiplateformes à un public d’utilisateurs étendu : à partir d’une base de code unique, vous pouvez créer des expériences d’application adaptées aux environnements Teams, Outlook et Office. Les utilisateurs finaux n’auront pas à quitter le contexte de leur travail pour utiliser votre application, et les administrateurs bénéficient d’un workflow de gestion et de déploiement consolidé.

La plateforme d’applications Teams continue d’évoluer et de se développer de manière holistique dans l’écosystème Microsoft 365. Voici la prise en charge actuelle des éléments de plateforme d’application Teams dans Microsoft 365 (Teams, Outlook et Office en tant qu’hôtes d’applications) :

|          | Élément de manifeste d’application | Prise en charge de Teams |Prise en charge d’Outlook* | Prise en charge d’Office* | Remarques |
|--|--|--|--|--|--|
| [**Onglets**](../tabs/what-are-tabs.md) (étendue personnelle)    |`staticTabs`  | Web, Bureau, Mobile | Web (version ciblée), Bureau (canal bêta) | Web (version ciblée), Bureau (canal bêta), Mobile (Android)| Étendue de canal et de groupe non encore prise en charge pour Microsoft 365. Consultez [les notes](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Extensions de message**](../messaging-extensions/what-are-messaging-extensions.md) (basées sur la recherche)| `composeExtensions` | Web, Bureau, Mobile| Web (version ciblée), Bureau (canal bêta)| - |Basée sur des actions non encore prises en charge pour Microsoft 365. Consultez [les notes](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook). |
| [**Compléments Office**](/office/dev/add-ins/develop/json-manifest-overview) (préversion) | `extensions` | - | Web, Bureau | - | Disponible uniquement dans la version [du manifeste devPreview](../resources/schema/manifest-schema-dev-preview.md) . Consultez [les notes](#office-add-ins-preview).|

\*L’option [de publication ciblée Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) et [l’inscription de canal de mise à jour Microsoft 365 Apps](/deployoffice/change-update-channels) nécessitent l’adhésion de l’administrateur pour l’ensemble de l’organisation ou des utilisateurs sélectionnés. Les canaux de mise à jour sont spécifiques à l’appareil et s’appliquent uniquement aux installations d’Office s’exécutant sur Windows.

Pour obtenir des conseils sur le manifeste de l’application Teams et le guide de gestion des versions du Kit de développement logiciel (SDK) Teams, et pour plus d’informations sur la prise en charge actuelle des fonctionnalités de plateforme Teams dans Microsoft 365, consultez la [vue d’ensemble du Kit de développement logiciel (SDK) client JavaScript Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Nous accueillons vos commentaires et vos rapports de problèmes à mesure que vous développez des applications Teams pour qu’elles s’exécutent dans l’écosystème Microsoft 365 ! Utilisez les [canaux réguliers de la communauté des développeurs Microsoft Teams](/microsoftteams/platform/feedback) pour envoyer des commentaires.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Onglets personnels et extensions de messagerie dans Outlook et Office

Atteignez vos utilisateurs là où ils se trouvent, dans le contexte de leur travail, en étendant votre application web en tant qu’application d’onglet personnel Teams qui s’exécute également dans Outlook et Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="La capture d’écran est un exemple montrant l’onglet Personnel en cours d’exécution dans Outlook, Office et Teams.":::

Sur mobile, vous pouvez tester et déboguer votre onglet personnel Teams s’exécutant sur l’application Office pour Android.

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="La capture d’écran est un exemple montrant l’onglet personnel en cours d’exécution dans Office.":::

Vous pouvez également étendre vos extensions de message Teams basées sur la recherche à Outlook sur le web et au bureau Windows, ce qui permet à vos clients de rechercher et de partager des résultats via la zone de composition des messages d’Outlook, en plus des clients Microsoft Teams.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="La capture d’écran est un exemple montrant l’extension Message en cours d’exécution dans Outlook et Teams.":::

La création de votre application avec le [dernier manifeste d’application Teams](../resources/schema/manifest-schema.md) et le [kit de développement logiciel (SDK) client JavaScript Teams](../tabs/how-to/using-teams-client-sdk.md) vous offre un processus de développement consolidé. En vous permettant d’offrir à vos clients une expérience rationalisée de déploiement, d’installation et d’administration, vous pouvez étendre la portée et l’utilisation potentielles de votre application.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Utiliser le manifeste d’application Teams dans Microsoft 365

Dans le but de simplifier et de simplifier l’écosystème des développeurs Microsoft 365, nous continuons à étendre le manifeste de l’application Teams à d’autres domaines de Microsoft 365, en procédant comme suit.

### <a name="office-add-ins-preview"></a>Compléments Office (préversion)

Vous pouvez maintenant définir et déployer des compléments Office dans la [préversion développeur](../resources/schema/manifest-schema-dev-preview.md) du manifeste de l’application Microsoft Teams. Actuellement, cette préversion est limitée aux compléments Outlook exécutés sur l’abonnement Office pour Windows.

Pour plus d’informations, consultez [Manifeste Teams pour les compléments Office (préversion).](/office/dev/add-ins/develop/json-manifest-overview)

## <a name="microsoft-commercial-marketplace-submission"></a>Soumission de la Place de marché commerciale Microsoft

Rejoignez le nombre croissant d’applications Teams de production dans le magasin Microsoft [Commercial Marketplace](https://appsource.microsoft.com/) (Microsoft AppSource) avec une prise en charge étendue pour les audiences Outlook et Office en préversion (version ciblée). Le [processus de soumission d’applications pour les applications Teams activées pour Outlook et Office](../concepts/deploy-and-publish/appsource/publish.md) est le même que pour les applications Teams traditionnelles. La seule différence est que vous allez utiliser le manifeste d’application Teams [version 1.13](../tabs/how-to/using-teams-client-sdk.md) dans votre package d’application, ce qui introduit la prise en charge des applications Teams qui s’exécutent sur Microsoft 365.

Une fois publiée en tant qu’application Teams compatible Avec Microsoft 365, votre application sera détectable en tant qu’application installable à partir des magasins d’applications Outlook et Office, en plus du Magasin Teams. Lors de l’exécution dans Outlook et Office, votre application utilise les mêmes autorisations accordées dans Teams. Les administrateurs Teams peuvent [gérer l’accès aux applications Teams dans Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) pour les utilisateurs de leur organisation.

Pour plus d’informations, consultez [Publier des applications Teams pour Microsoft 365](publish.md).

## <a name="next-step"></a>Étape suivante

Configurez votre environnement de développement pour créer des applications Teams pour Microsoft 365 :

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)