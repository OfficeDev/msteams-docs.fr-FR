---
title: Installer Teams Toolkit
author: zyxiaoyuer
description: Dans ce module, découvrez l’installation du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: c784e5d2242381a919500b16ab922a397bfc5d9e
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780683"
---
# <a name="install-teams-toolkit"></a>Installer Teams Toolkit

Teams Toolkit est une extension dans Visual Studio et Visual Studio Code. Dans ce document, vous pouvez apprendre à installer Teams Toolkit.

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Installer teams Toolkit pour Visual Studio Code

Avant de commencer l’installation, visual Studio Code et le client Teams doivent être installés.

## <a name="steps-to-install-teams-toolkit"></a>Étapes d’installation de Teams Toolkit

Vous pouvez installer Teams Toolkit à partir d’une extension dans Visual Studio Code et à partir de Visual Studio Code Marketplace. Les étapes suivantes vous aident à installer Teams Toolkit :

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez **Visual Studio Code**.
1. Sélectionnez la vue Extensions (**Ctrl+Maj+X** / **⌘⇧-X** ou **Afficher les extensions >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="installer":::

1. Entrez **le Kit de ressources Teams** dans la zone de recherche.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Kit de ressources":::

1. Sélectionnez **Installer**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="install toolkit 4.0.0":::

   Une fois l’installation de Teams Toolkit réussie dans Visual Studio Code, l’icône du Kit de ressources Teams s’affiche dans la barre d’outils Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Après l’installation":::

# <a name="marketplace"></a>[Marché](#tab/marketplace)

1. Ouvrez [la Place de marché Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

   La page suivante s’affiche.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="installer la Place de marché TTK":::

1. Sélectionnez **Installer**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="installer le TTK":::

1. Dans la fenêtre contextuelle, sélectionnez **Ouvrir**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Sélectionnez l’ouverture":::

   La page Visual Studio Code suivante s’affiche.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Sélectionner le TTK dans VSC":::

1. Sélectionnez **Installer**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Sélectionner Installer le TTK dans VSC":::

   Une fois l’installation de Teams Toolkit réussie dans Visual Studio Code, l’icône du Kit de ressources Teams s’affiche dans la barre d’outils Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Après l’installation":::

---

#### <a name="upgrade-teams-toolkit"></a>Mettre à niveau teams Toolkit

Teams Toolkit est mis à niveau vers la dernière version par défaut. Les étapes suivantes vous aident à installer différentes versions :

* Sélectionnez l’icône Extensions :::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG"::: .
* Entrez **le Kit de ressources Teams**  dans la zone de recherche.
* Dans l’extension Teams Toolkit, sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/setting icon.PNG"::: .
* Sélectionnez **Installer une autre version** pour la mise à niveau vers la dernière version du Kit de ressources Teams.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Extension de kit de ressources Teams pour Visual Studio

Avant de commencer l’installation, vous devez installer Visual Studio Installer.

Vous pouvez télécharger la dernière Visual Studio Installer à partir de la page de [téléchargement de Visual Studio](https://visualstudio.microsoft.com/vs/preview/).

## <a name="steps-to-install-teams-toolkit"></a>Étapes d’installation de Teams Toolkit

Après avoir ouvert le Visual Studio Installer, dans la fenêtre charges de travail contextuelles :

1. Sélectionnez l’ASP.NET et la charge de **travail de développement web**.
1. Sélectionnez les **outils de développement Microsoft Teams** dans le panneau **Détails de l’installation** .
1. Sélectionnez **Installer**.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Installation de Visual Studio":::

1. Sélectionnez **Lancer** pour ouvrir Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Lancer Visual Studio":::

   > [!IMPORTANT]
   > Il est recommandé de télécharger Visual Studio 2022 version 17.3.3, car Teams Toolkit pour Visual Studio est en disponibilité générale dans cette version. Cet article est écrit pour Visual Studio 2022 version 17.3.3. Teams Toolkit version 17.3.* ou ultérieure.

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Explorer le Kit de ressources Teams](explore-Teams-Toolkit.md)
* [Créer une application Teams à l’aide du kit de ressources Teams](create-new-project.md)
* [Préparer la création d’applications à l’aide de Microsoft Teams Toolkit](build-environments.md)
* [Provisionner des ressources cloud à l’aide du Kit de ressources Teams](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
