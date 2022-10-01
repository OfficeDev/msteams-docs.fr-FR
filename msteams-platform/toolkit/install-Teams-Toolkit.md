---
title: Installer Teams Toolkit
author: zyxiaoyuer
description: Dans ce module, découvrez l’installation de Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 03d101df114d3f7564c78c433d01191172e180c9
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2022
ms.locfileid: "68295983"
---
# <a name="install-teams-toolkit"></a>Installer Teams Toolkit

Cet article explique comment installer l’extension Teams Toolkit.

## <a name="prerequisites"></a>Configuration requise

::: zone pivot="visual-studio-code"

Avant d’installer Teams Toolkit pour Visual Studio Code, vous devez [télécharger et installer Visual Studio Code](https://code.visualstudio.com/Download).

::: zone-end

::: zone pivot="visual-studio"

Avant d’installer Teams Toolkit pour Visual Studio, vous devez [télécharger et installer Visual Studio 2022](https://aka.ms/VSDownload) à l’aide de Visual Studio Installer.

::: zone-end

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Installer teams Toolkit pour Visual Studio Code

Vous pouvez installer Teams Toolkit à l’aide de la fenêtre Extensions dans Visual Studio Code ou l’installer à partir de Visual Studio Marketplace.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Lancez **Visual Studio Code**.
1. Ouvrez la fenêtre Extensions (**Ctrl+Maj+X** / **⌘⇧-X** ou **Afficher les extensions >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="Capture d’écran montrant comment installer.":::

1. Entrez **le Kit de ressources Teams** dans la zone de recherche.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Capture d’écran montrant le Kit de ressources.":::

1. Sélectionnez **Installer**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Capture d’écran montrant install toolkit 4.0.0.":::

   Une fois l’installation de Teams Toolkit réussie dans Visual Studio Code, une icône teams toolkit s’affiche dans la barre d’outils Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Capture d’écran montrant l’affichage après l’installation.":::

# <a name="marketplace"></a>[Marché](#tab/marketplace)

1. Accédez à [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) dans un navigateur web.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="Capture d’écran montrant l’installation de la Place de marché TTK.":::

1. Sélectionnez **Installer**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="Capture d’écran montrant comment installer le TTK.":::

1. Dans la fenêtre contextuelle, sélectionnez **Ouvrir** pour lancer Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Capture d’écran montrant la sélection de l’ouverture.":::

   La page d’extension du Kit de ressources Teams s’affiche dans Visual Studio Code :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Capture d’écran montrant comment sélectionner le TTK dans VSC.":::

1. Sélectionnez **Installer**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Capture d’écran montrant comment sélectionner Installer le TTK dans VSC.":::

   Une fois l’installation de Teams Toolkit réussie dans Visual Studio Code, une icône teams toolkit s’affiche dans la barre d’outils Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Capture d’écran montrant l’affichage après l’installation.":::

---

## <a name="installing-a-different-release-version"></a>Installation d’une version différente

Par défaut, Visual Studio Code maintient automatiquement le Kit de ressources Teams à jour. Si vous souhaitez installer une autre version, procédez comme suit :

* Sélectionnez l’icône Extensions (:::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG":::) dans la barre d’outils Visual Studio Code.
* Entrez **le Kit de ressources Teams**  dans la zone de recherche.
* Dans la page Du kit de ressources Teams, sélectionnez la flèche déroulante en regard du bouton **Désinstaller** .
* Sélectionnez **Installer une autre version...** dans le menu et choisissez la version à installer.

## <a name="installing-a-pre-release-version"></a>Installation d’une version préliminaire

L’extension Teams Toolkit pour Visual Studio Code est également disponible sur GitHub. Pour télécharger les préversion, accédez à la [page Mises en production sur GitHub](https://github.com/OfficeDev/TeamsFx/releases) et recherchez les téléchargements d’extension marqués comme étant en préversion.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Extension de kit de ressources Teams pour Visual Studio

   > [!IMPORTANT]
   > Nous vous recommandons d’utiliser Visual Studio 2022 version 17.3.3 ou ultérieure pour teams Toolkit, qui est la dernière version pour résoudre plusieurs problèmes connus dans les versions précédentes de Visual Studio.

1. [Téléchargez le programme d’installation de Visual Studio](https://aka.ms/VSDownload) ou ouvrez-le s’il est déjà installé.
2. Sélectionnez **Installer** ou **Modifier** si Visual Studio est déjà installé.
3. Sélectionnez l’onglet **Charges de** travail, puis sélectionnez l’ASP.NET et la charge de **travail de développement web** .
4. À droite, sélectionnez les **outils de développement Microsoft Teams** dans la section **Facultatif** du panneau **Détails de l’installation** .
5. Sélectionnez **Modifier** ou **Installer** pour terminer l’installation.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Capture d’écran montrant comment installer Visual Studio.":::

6. Une fois l’installation terminée, sélectionnez **Lancer** pour ouvrir Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Capture d’écran montrant comment lancer Visual Studio.":::

::: zone-end

## <a name="next-steps"></a>Prochaines étapes

Maintenant que Teams Toolkit est installé, [visitez Créer un projet Teams](create-new-project.md) pour commencer.

## <a name="see-also"></a>Voir aussi

* [Explorer le Kit de ressources Teams](explore-Teams-Toolkit.md)
* [Créer une application Teams à l’aide du kit de ressources Teams](create-new-project.md)
* [Préparer la création d’applications à l’aide de Microsoft Teams Toolkit](build-environments.md)
* [Provisionner des ressources cloud à l’aide du Kit de ressources Teams](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
