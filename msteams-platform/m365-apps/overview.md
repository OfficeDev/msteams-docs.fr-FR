---
title: Étendre les applications Teams à travers Microsoft 365 (version préliminaire)
description: Étendez vos expériences d’application Teams à d’autres domaines à utilisation élevée de Microsoft 365
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 66ba17a638fc57b47febef34bea769e39cdea7e3
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111947"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Étendre Teams applications à travers Microsoft 365

> [!NOTE]
> Cette préversion pour les développeurs précoces a pour but de permettre aux développeurs Teams d’essayer les nouvelles fonctionnalités et de [fournir des commentaires](/microsoftteams/platform/feedback) sur cette extension de la plateforme de développement Teams dans d’autres zones à utilisation élevée de l’écosystème Microsoft 365.

Vous pouvez tester vos applications Teams qui s’exécutant dans Microsoft Office et Outlook, en mettant à jour votre code pour utiliser la nouvelle [version préliminaire du kit de développement logiciel (SDK) client JavaScript Microsoft Teams v2](using-teams-client-sdk-preview.md) et Microsoft Teams [manifeste d’aperçu pour les développeurs](../resources/schema/manifest-schema-dev-preview.md).

Avec cette préversion, vous pouvez :

- Étendez les [onglets personnels](/microsoftteams/platform/tabs/how-to/create-personal-tab)existants Teams à Outlook pour bureau et sur le web, ainsi qu’à Office sur le web (office.com).
- Étendez les extensions de messages [basées sur la recherche Teams existantes](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command) à Outlook pour ordinateur de bureau et sur le web.

Pour les commentaires et les problèmes, continuez à utiliser les [canaux de la communauté Microsoft Teams](/microsoftteams/platform/feedback).

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Onglets personnels Teams dans Office et Outlook

Avec cette préversion, vous pouvez étendre une application d’onglet personnel Teams pour qu’elle s’exécute à la fois dans Outlook sur le Bureau Windows et sur le web, ainsi que dans Office sur le web.

Après le chargement indépendant vers Teams, votre onglet personnel apparaît comme l’une de vos applications installées dans Outlook et Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Les onglets personnels s’exécutant dans Outlook, Office et Teams":::

## <a name="teams-message-extensions-in-outlook"></a>Extensions de message Teams dans Outlook

Avec cette préversion, vous pouvez étendre vos extensions de message Teams basées sur la recherche à Outlook sur le web et au Bureau Windows, ce qui permet aux clients de rechercher et de partager des résultats via la zone de rédaction des messages Outlook, en plus des clients Microsoft Teams.

Après le chargement de version test dans Teams, votre extension de message s’affiche comme l’une de vos applications installées dans la zone de rédaction de message Outlook.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extension de message en cours d’exécution dans Outlook et Teams":::

## <a name="next-steps"></a>Étapes suivantes

Configurez votre environnement de développement pour étendre les applications Teams sur Microsoft 365 :

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)
