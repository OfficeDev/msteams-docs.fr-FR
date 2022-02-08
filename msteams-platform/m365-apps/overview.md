---
title: Étendre Teams applications à travers Microsoft 365 (prévisualisation)
description: Étendre vos expériences Teams d’application à d’autres domaines à forte Microsoft 365
ms.date: 11/15/2021
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: ef2aff7d7f23d45b16041404e7a530596e978fb5
ms.sourcegitcommit: 9bdd930523041377b52dadffbd8cd52a86a047d7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2022
ms.locfileid: "62443903"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Étendre Teams applications à travers Microsoft 365

> [!NOTE]
> Cette version préliminaire destinée aux développeurs est destinée à offrir aux développeurs Teams l’opportunité d’essayer les nouvelles fonctionnalités et de [](/microsoftteams/platform/feedback) fournir des commentaires sur cette extension de la plateforme de développement Teams dans d’autres domaines à forte utilisation de l’écosystème Microsoft 365.

Vous pouvez tester vos applications Teams en cours d’exécution dans Microsoft Office et Outlook en mettant à jour votre code pour utiliser le nouveau manifeste d’aperçu du [SDK client JavaScript v2](using-teams-client-sdk-preview.md) Microsoft Teams et Microsoft Teams [Développeur](../resources/schema/manifest-schema-dev-preview.md).

Avec cet aperçu, vous pouvez :

- Étendre les [onglets Teams des utilisateurs existants](/microsoftteams/platform/tabs/how-to/create-personal-tab) à Outlook pour les ordinateurs de bureau et sur le web, ainsi qu’Office sur le Web (office.com).
- Étendre les extensions Teams messagerie basées sur la recherche [existantes](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command) Outlook pour ordinateur de bureau et sur le web.

Pour obtenir des commentaires et des problèmes, continuez à utiliser les canaux Microsoft Teams [communauté des développeurs appropriés](/microsoftteams/platform/feedback).

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Teams onglets personnels dans Office et Outlook

Avec cet aperçu, vous pouvez étendre une application d’onglet personnel Teams pour qu’elle s’exécute à la fois dans Outlook sur Windows bureau et sur le web, ainsi que dans Office sur le Web.

Après le chargement de version Teams, votre onglet personnel apparaît comme l’une de vos applications installées dans Outlook et Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Onglet personnel en cours d’exécution outlook.com":::

## <a name="teams-messaging-extensions-in-outlook"></a>Teams extensions de messagerie dans Outlook

Avec cet aperçu, vous pouvez étendre vos extensions de messagerie Teams basées sur la recherche à Outlook sur le web et bureau Windows, ce qui permet aux clients de rechercher et de partager des résultats via la zone de composition de messages de Outlook, en plus des clients Microsoft Teams.

Après le chargement de version Teams, votre extension de messagerie apparaît comme l’une de vos applications installées dans la Outlook zone de message de composition.

:::image type="content" source="~/assets/images/git-issue-msging-extension.png" alt-text="extension de messagerie" lightbox="~/assets/images/git-issue-msging-extension.png" border="true":::

## <a name="next-step"></a>Étape suivante

Configurer votre environnement dev pour l’extension Teams applications à travers Microsoft 365 :

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)
