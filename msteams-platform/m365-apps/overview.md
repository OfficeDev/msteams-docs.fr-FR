---
title: Étendre les applications Teams à travers Microsoft 365 (version préliminaire)
description: Découvrez comment étendre les applications Teams à Microsoft 365 (en cours d’exécution dans Teams, Outlook et Office en tant qu’hôtes d’applications).
ms.date: 10/10/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 4c05fbe0c763d9b650573e33edfa5e332aaba90d
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537537"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Étendre Teams applications à travers Microsoft 365

Avec les dernières versions du Kit de développement logiciel ( [SDK) client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) (version 2.0.0 et ultérieure), du [manifeste d’application Teams](../resources/schema/manifest-schema.md) (version 1.13 et ultérieure) et du Kit de ressources [Teams](../toolkit/visual-studio-code-overview.md), vous pouvez créer et mettre à jour des applications Teams pour qu’elles s’exécutent dans d’autres produits Microsoft 365 à utilisation élevée et les publient sur la Place de marché commerciale Microsoft ([Microsoft AppSource](https://appsource.microsoft.com/)) ou le magasin d’applications privé de votre organisation.

L’extension de votre application Teams dans Microsoft 365 offre un moyen simplifié de fournir des applications multiplateformes à un public d’utilisateurs étendu : à partir d’une base de code unique, vous pouvez créer des expériences d’application adaptées aux environnements Teams, Outlook et Office. Les utilisateurs finaux n’auront pas à quitter le contexte de leur travail pour utiliser votre application, et les administrateurs bénéficient d’un workflow de gestion et de déploiement consolidé.

La plateforme d’applications Teams continue d’évoluer et de se développer de manière holistique dans l’écosystème Microsoft 365. Voici la prise en charge actuelle des éléments de plateforme d’application Teams dans Microsoft 365 (Teams, Outlook et Office en tant qu’hôtes d’applications) :

| Fonctionnalités de l’application Teams| Élément de manifeste d’application | Prise en charge de Teams |Prise en charge d’Outlook* | Prise en charge d’Office* | Remarques |
|--|--|--|--|--|--|
| [**Étendue personnelle des onglets**](../tabs/what-are-tabs.md)    |`staticTabs`  | Web, Bureau, Mobile | Web (version ciblée), Bureau (canal bêta) | Web (version ciblée), Bureau (canal bêta), Mobile (Android)| Étendue de canal et de groupe non encore prise en charge pour Microsoft 365. Consultez [les notes](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Extensions de message basées**](../messaging-extensions/what-are-messaging-extensions.md) sur la recherche| `composeExtensions` | Web, Bureau, Mobile| Web (version ciblée), Bureau (canal bêta)| - |Basée sur des actions non encore prises en charge pour Microsoft 365. Consultez [les notes](extend-m365-teams-message-extension.md#troubleshooting). |
| Déploiement de lien | `composeExtensions.messageHandlers` | Web, Bureau | Web (version ciblée), Bureau (canal bêta) | - | Voir [les notes](extend-m365-teams-message-extension.md#link-unfurling) |
| [**Compléments Office**](/office/dev/add-ins/develop/json-manifest-overview) (préversion) | `extensions` | - | Web, Bureau | - | Disponible uniquement dans la version [du manifeste devPreview](../resources/schema/manifest-schema-dev-preview.md) . Consultez [les notes](#office-add-ins-preview).|

\*L’option [de publication ciblée Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) et [l’inscription de canal de mise à jour Microsoft 365 Apps](/deployoffice/change-update-channels) nécessitent l’adhésion de l’administrateur pour l’ensemble de l’organisation ou des utilisateurs sélectionnés. Les canaux de mise à jour sont spécifiques à l’appareil et s’appliquent uniquement aux installations d’Office s’exécutant sur Windows.

Pour obtenir des conseils sur le manifeste de l’application Teams et le guide de gestion des versions du Kit de développement logiciel (SDK) Teams, et pour plus d’informations sur la prise en charge actuelle des fonctionnalités de plateforme Teams dans Microsoft 365, consultez la [vue d’ensemble du Kit de développement logiciel (SDK) client JavaScript Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Nous accueillons vos commentaires et vos rapports de problèmes à mesure que vous développez des applications Teams pour qu’elles s’exécutent dans l’écosystème Microsoft 365 ! Utilisez les [canaux réguliers de la communauté des développeurs Microsoft Teams](/microsoftteams/platform/feedback) pour envoyer des commentaires.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Onglets personnels et extensions de messagerie dans Outlook et Office

Atteignez vos utilisateurs là où ils se trouvent, dans le contexte de leur travail, en étendant votre application web en tant qu’application [d’onglet personnel Teams](extend-m365-teams-personal-tab.md) qui s’exécute également dans Outlook et Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="La capture d’écran est un exemple montrant l’onglet Personnel en cours d’exécution dans Outlook, Office et Teams.":::

Sur mobile, vous pouvez tester et déboguer votre onglet personnel Teams [s’exécutant sur l’application Office pour Android](extend-m365-teams-personal-tab.md#office-app-for-android).

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="La capture d’écran est un exemple montrant l’onglet personnel en cours d’exécution dans Office.":::

Vous pouvez également étendre vos [extensions de message Teams basées](extend-m365-teams-message-extension.md) sur la recherche à Outlook sur le web et au bureau Windows, ce qui permet à vos clients de rechercher et de partager des résultats via la zone de composition des messages d’Outlook, en plus des clients Microsoft Teams.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="La capture d’écran est un exemple montrant l’extension Message en cours d’exécution dans Outlook et Teams.":::

[Le déploiement de liens](extend-m365-teams-message-extension.md#link-unfurling)  fonctionne dans les environnements Web et Windows Outlook de la même façon que dans Microsoft Teams sans autre travail que l’utilisation du manifeste d’application Teams version 1.13 ou ultérieure.

:::image type="content" source="images/outlook-teams-link-unfurling.png" alt-text="La capture d’écran est un exemple montrant le déploiement de Liens en cours d’exécution dans Outlook et Teams.":::

Générez votre application avec le [dernier manifeste d’application Teams](../resources/schema/manifest-schema.md) et le kit de développement logiciel ( [SDK) client JavaScript Teams](../tabs/how-to/using-teams-client-sdk.md) pour bénéficier du dernier processus de développement d’applications Microsoft 365 consolidé. Ensuite, offrez à vos clients une expérience rationalisée de déploiement, d’installation et d’administration qui étend la portée et l’utilisation de votre application.

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
