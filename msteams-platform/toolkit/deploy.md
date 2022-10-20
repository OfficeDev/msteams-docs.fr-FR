---
title: Déployer à partir du cloud
author: MuyangAmigo
description: Dans ce module, découvrez comment déployer une application dans le cloud, Azure ou SharePoint et déployer des applications Teams à l’aide du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 4f5afe23e9d8deefdf2b1b182fa51cfe034e5c4d
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615141"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Déployer l’application Teams dans le cloud

Teams Toolkit vous aide à déployer ou à charger le code frontal et back-end dans votre application sur vos ressources cloud provisionnées dans Azure.

::: zone pivot="visual-studio-code"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio-code"></a>Déployer une application Teams dans le cloud à l’aide de Visual Studio Code

Vous pouvez déployer les éléments suivants dans le cloud :

* L’onglet, tel que les applications frontales, est déployé sur Stockage Azure et configuré pour l’hébergement web statique ou un site SharePoint.
* Les API back-end sont déployées sur Azure Functions.
* Le bot ou l’extension de message est déployé sur Azure App Service.

  > [!NOTE]
  > Avant de déployer du code d’application dans le cloud Azure, vous devez terminer avec succès [l’approvisionnement des ressources cloud](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Déployer des applications Teams à l’aide du Kit de ressources Teams

Les guides de prise en main vous aident à déployer à l’aide du Kit de ressources Teams. Vous pouvez utiliser les éléments suivants pour déployer votre application Teams :

* [Déployer votre application vers Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Déployer votre extension vers SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Détails sur la charge de travail de l’application Teams

| Charge de travail de l’application Teams | Code source | Artefact de build| Ressource cible |
|-------------|----------|---------------|---------------|
|Onglets avec React </br> Charge de travail frontale| `yourProjectFolder/tabs`| `tabs/build` |Stockage Azure |
|Onglets avec SharePoint </br> Charge de travail frontale | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |Catalogue des applications SharePoint |
|API sur Azure Functions </br> Charge de travail principale | `yourProjectFolder/api`| Non applicable |Azure Functions |
|Bots et extensions de message </br> Charge de travail principale | `yourProjectFolder/bot` | Non applicable | Azure App Service |

> [!NOTE]
> Lorsque vous incluez une ressource de gestion des API Azure dans votre projet et que vous déclenchez le déploiement, vous pouvez publier vos API dans Azure Functions sur le service de gestion des API Azure.

::: zone-end

::: zone pivot="visual-studio"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Déployer une application Teams dans le cloud à l’aide de Visual Studio

Les applications suivantes peuvent être déployées dans Visual Studio :

* L’application onglet, telle que les applications frontales, est déployée dans stockage Azure, configurée pour l’hébergement web statique.
* L’application de bot de notification avec des déclencheurs Azure Functions peut être déployée sur Azure Functions.
* L’application bot ou l’extension de message peut être déployée sur Azure App Services.

Après le déploiement, vous pouvez afficher un aperçu de l’application dans le client Teams ou le navigateur web avant de commencer à l’utiliser.

## <a name="deploy-teams-app-using-teams-toolkit"></a>Déployer une application Teams à l’aide du Kit de ressources Teams

1. Ouvrez Visual Studio.
1. Sélectionnez **Créer un projet** ou ouvrez un projet existant dans la liste.
1. Cliquez avec le bouton droit sur votre projet **MyTeamsApp1** > **Teams Toolkit** > **Deploy sur le cloud**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="déployer dans le cloud":::

   > [!NOTE]
   > Dans ce scénario, le nom du projet est MyTeamsApp1.

1. Sélectionnez **Déployer** dans la boîte de dialogue de confirmation.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="Boîte de dialogue de confirmation de déploiement vers le cloud":::

   Une fois le processus de déploiement terminé, vous pouvez voir une fenêtre contextuelle avec la confirmation qu’il a été correctement déployé. Vous pouvez également vérifier l’état dans la fenêtre de sortie.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="déployer dans la fenêtre contextuelle cloud":::

### <a name="preview-your-app"></a>Afficher un aperçu de votre application

Pour afficher un aperçu de votre application, vous devez d’abord créer un package d’application Zip et charger une version test dans le client Teams.

1. Sélectionnez package **d’application zip** du **Kit de ressources** >  **Project** >  Teams.
1. Sélectionnez l’option **Pour local** ou **Pour Azure** pour générer le package d’application Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package1.png" alt-text="Générer un package d’application Teams":::

**Pour afficher un aperçu de votre application dans le client Teams**

1. Sélectionnez **Project** > **Teams Toolkit** > **Preview dans Teams**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams2.png" alt-text="Aperçu de l’application Teams dans le client Teams":::

   Votre application est maintenant chargée de manière indépendante dans Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Charger une version test de l’application Teams dans le client Teams":::

L’autre façon d’afficher un aperçu de votre application :

1. Cliquez avec le bouton droit sur votre projet **MyTeamsApp1** sous **Explorateur de solutions**.
1. Sélectionnez La **préversion du** **Kit de ressources** >  Teams dans Teams pour lancer l’application Teams dans le navigateur web.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Aperçu de l’application Teams dans le navigateur web":::

   > [!NOTE]
   > Les mêmes options de menu sont disponibles dans le menu Projet.

   Votre application est maintenant chargée de manière indépendante dans Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Charger une version test de l’application Teams dans le client Teams":::

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Créer et déployer un service cloud Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Créer des applications Teams multi-fonctionnalités](add-capability.md)
* [Ajouter des ressources cloud à l’application Microsoft Teams](add-resource.md)
* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Déboguer votre application Teams localement à l’aide de Visual Studio](debug-teams-app-visual-studio.md)
