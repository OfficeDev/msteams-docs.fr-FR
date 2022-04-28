---
title: Étendre Teams applications sur Microsoft 365 (préversion)
description: Étendre vos expériences d’application Teams à d’autres zones à forte utilisation de Microsoft 365
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 013bb773897965d51daaa485459eec78478292b3
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104342"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Étendre Teams applications à travers Microsoft 365

> [!NOTE]
> Cette préversion précoce pour les développeurs est destinée à offrir aux développeurs Teams des applications existantes la possibilité d’essayer les nouvelles fonctionnalités et [de fournir des commentaires](/microsoftteams/platform/feedback) sur cette expansion de la plateforme de développement Teams dans d’autres zones à forte utilisation de l’écosystème Microsoft 365.

Vous pouvez tester vos applications Teams s’exécutant dans Microsoft Office et Outlook en mettant à jour votre code pour utiliser le nouveau [Microsoft Teams kit de développement logiciel (SDK) client JavaScript v2 (préversion](using-teams-client-sdk-preview.md)) et Microsoft Teams [manifeste en préversion du développeur](../resources/schema/manifest-schema-dev-preview.md).

Avec cette préversion, vous pouvez :

- Étendez les [onglets personnels Teams existants](/microsoftteams/platform/tabs/how-to/create-personal-tab) à Outlook pour le bureau et sur le web, ainsi que Office sur le Web (office.com).
- Étendez les [extensions de message basées sur la recherche](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command) Teams existantes à Outlook pour le bureau et sur le web.

Pour obtenir des commentaires et des problèmes, continuez à utiliser les [canaux de communauté de développeurs Microsoft Teams appropriés](/microsoftteams/platform/feedback).

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Teams onglets personnels dans Office et Outlook

Avec cette préversion, vous pouvez étendre une application d’onglet Teams personnelle à exécuter à la fois dans Outlook sur Windows bureau et sur le web, ainsi que Office sur le Web.

Après le chargement indépendant vers Teams, votre onglet personnel apparaît comme l’une de vos applications installées dans Outlook et Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Onglet personnel s’exécutant dans Outlook, Office et Teams":::

## <a name="teams-message-extensions-in-outlook"></a>Teams extensions de message dans Outlook

Avec cette préversion, vous pouvez étendre vos extensions de message de Teams basées sur la recherche à Outlook sur le web et Windows bureau, ce qui permet aux clients de rechercher et de partager des résultats via la zone de composition de messages de Outlook, en plus de Microsoft Teams clients.

Après le chargement indépendant vers Teams, votre extension de message apparaît comme l’une de vos applications installées dans la zone de message de composition Outlook.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extension de message en cours d’exécution dans Outlook et Teams":::

## <a name="next-steps"></a>Étapes suivantes

Configurez votre environnement de développement pour étendre Teams applications sur Microsoft 365 :

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)
