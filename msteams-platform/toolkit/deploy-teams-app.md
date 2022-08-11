---
title: Déployer une application Teams dans le cloud à l’aide de Visual Studio
author: surbhigupta
description: Dans ce module, découvrez comment déployer une application dans le cloud, Azure ou SharePoint et déployer des applications Teams à l’aide du Kit de ressources Teams dans Visual Studio
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: be4eeb10e16b0dda4d789e4607ac8ffbc302b0e1
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302443"
---
# <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Déployer une application Teams dans le cloud à l’aide de Visual Studio

Teams Toolkit vous aide à déployer ou à charger le code frontal et back-end de votre application sur les ressources cloud approvisionnées dans votre abonnement Azure. Après le déploiement, vous pouvez afficher un aperçu de l’application dans le client Teams ou le navigateur web avant de commencer à l’utiliser. Les applications suivantes peuvent être déployées dans Visual Studio :

* L’application onglet, telle que les applications frontales, est déployée dans le stockage Azure, configurée pour l’hébergement web statique.
* L’application de bot de notification avec des déclencheurs de fonction Azure peut être déployée sur des fonctions Azure.
* L’application bot ou l’extension de message peut être déployée sur les services d’application Azure.

## <a name="prerequisite"></a>Conditions préalables

Voici la liste des outils dont vous avez besoin pour créer et déployer vos applications.

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| &nbsp; | **Obligatoire** | &nbsp; |
| &nbsp; | Visual Studio 2022 version 17.3 | Vous pouvez installer l’édition Entreprise de Visual Studio et installer la charge de travail « ASP.NET » et les outils de développement Microsoft Teams. |
| &nbsp; | Toolkit Teams | Extension Visual Studio qui crée une structure de projet pour votre application. Utilisez la dernière version. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
| &nbsp; | Azure Tools et [Microsoft Azure CLI](/cli/azure/install-azure-cli) | Outils Azure pour accéder aux données stockées ou déployer un backend cloud pour votre application Teams dans Azure. |

  > [!NOTE]
  > Avant de déployer du code de projet dans le cloud, [provisionnez des ressources cloud pour TTK Visual Studio](provision VS.md).

## <a name="deploy-teams-app-using-teams-toolkit"></a>Déployer une application Teams à l’aide du Kit de ressources Teams

1. Lancez Visual Studio.
1. Sélectionnez **Créer un projet** ou ouvrez un projet existant dans la liste.
1. Cliquez avec le bouton droit sur votre projet **MyTeamsApp1**.
1. Sélectionnez **Teams Toolkit**.
1. Sélectionnez **Déployer dans le cloud...**

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="déployer dans le cloud":::

   > [!NOTE]
   > Dans ce scénario, le nom du projet est MyTeamsApp1.

1. Sélectionnez **Déployer** dans la boîte de dialogue de confirmation.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="Boîte de dialogue de confirmation de déploiement vers le cloud":::

1. Une fois le processus de déploiement déclenché et terminé, vous pouvez voir une fenêtre contextuelle avec la confirmation qu’il a été correctement déployé. Vous pouvez également vérifier l’état dans la fenêtre de sortie.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="déployer dans la fenêtre contextuelle cloud":::

Une fois votre projet déployé sur Azure, il existe différentes façons d’afficher un aperçu de votre application dans le Kit de ressources Teams :

1. Sélectionnez **Project** > **Teams Toolkit** > **Zip App Package** pour générer le package d’application Teams.
1. Sélectionnez l’option **Pour local** ou **Pour Azure** et chargez-le sur le client Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package.png" alt-text="Générer un package d’application Teams":::

  **Pour afficher un aperçu de votre application dans le client Teams**

3. Sélectionnez **Projet**.
4. Sélectionnez **Teams Toolkit**.
5. Sélectionnez **Aperçu dans Teams**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams1.png" alt-text="Aperçu de l’application Teams dans le client Teams":::

L’autre façon d’afficher un aperçu de votre application :

1. Cliquez avec le bouton droit sur votre projet **MyTeamsApp1** sous le panneau Explorateur de solutions.
1. Sélectionnez **Teams Toolkit**.
1. Sélectionnez **Aperçu dans Teams** pour lancer l’application Teams dans le navigateur web.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Aperçu de l’application Teams dans le navigateur web":::

   > [!NOTE]
   > Les mêmes options de menu sont disponibles dans le menu Projet.

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Déboguer votre application Teams localement à l’aide de Visual Studio](debug-teams-app-visual-studio.md)
