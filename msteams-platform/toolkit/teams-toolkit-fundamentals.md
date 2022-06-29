---
title: Vue d’ensemble du kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez le Kit de ressources Teams, l’installation de Teams Toolkit et le parcours utilisateur du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: 49bf74276053f927f0337882d6f278ca64494128
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484604"
---
# <a name="teams-toolkit-overview"></a>Vue d’ensemble du kit de ressources Teams

Teams Toolkit for Microsoft Visual Studio Code vous aide à créer et déployer des applications Teams avec une identité intégrée, un accès au stockage cloud, des données de Microsoft Graph et d’autres services dans Azure et Microsoft 365 avec une approche de configuration zéro. Pour le développement d’applications Teams, similaire au Kit de ressources Teams pour Visual Studio, vous pouvez utiliser l’[outil CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), qui se compose de toolkit `teamsfx`.
Teams Toolkit vous permet de créer, déboguer et déployer votre application Teams directement à partir de Visual Studio Code. Le développement d’applications avec le kit de ressources présente les avantages suivants :

* Identité intégrée
* Accès au stockage cloud
* Données de Microsoft Graph
* Services Azure et Microsoft 365 avec une approche de configuration zéro.

Teams Toolkit propose tous les outils nécessaires à la création d’une application Teams au même endroit.

## <a name="user-journey-of-teams-toolkit"></a>Parcours utilisateur du Kit de ressources Teams

Teams Toolkit automatise le travail manuel et offre une excellente intégration des ressources Teams et Azure. L’image suivante montre le parcours utilisateur du Kit de ressources Teams :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey1.png" alt-text="Parcours utilisateur du Kit de ressources Teams" border="true" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

Les principaux jalons de ce parcours sont les suivants :

1. Commencez par créer un projet ou essayer un exemple d’application Teams.
1. Ajoutez des fonctionnalités ou modifiez le fichier manifeste si nécessaire.
1. Utilisez Microsoft 365 compte pour générer et déboguer votre application Teams.
1. Utilisez un compte Azure pour provisionner et déployer votre application dans le cloud.
1. Publiez votre application dans Teams.

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Installer teams Toolkit pour Visual Studio Code

1. Ouvrez **Visual Studio Code.**
1. Sélectionnez la vue Extensions (**Ctrl+Maj+X** / **⌘⇧-X** ou **Afficher les extensions >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="installer":::

1. Entrez **le Kit de ressources Teams** dans la zone de recherche.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Kit de ressources":::

1. Sélectionnez **Installer**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="install toolkit 4.0.0":::

> [!TIP]
> Vous pouvez installer teams Toolkit à partir de [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Visite guidée du Kit de ressources Teams

Après l’installation du Kit de ressources, l’interface utilisateur du Kit de ressources Teams s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="mini-fonctions":::

Vous pouvez sélectionner **Prise en main** pour explorer le Kit de ressources Teams, ou sélectionner **Créer une application Teams** pour créer un projet Teams. Si vous avez un projet Teams créé par Teams Toolkit ouvert dans Visual Studio Code, vous verrez l’interface utilisateur du Kit de ressources Teams avec toutes les fonctionnalités, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="Capture d’écran du kit de ressourcesteams":::

Examinons les sujets abordés dans ce document.

## <a name="accounts"></a>Comptes

Pour développer une application Teams, vous avez besoin d’au moins un compte Microsoft 365 avec un abonnement valide. Si vous souhaitez héberger vos ressources principales sur Azure, un compte Azure est également nécessaire. Teams Toolkit prend en charge l’expérience intégrée de connexion, de provisionnement et de déploiement pour les ressources Azure. Vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="environment"></a>Environnement

Teams Toolkit vous permet de créer et de gérer plusieurs environnements, d’approvisionner et de déployer des artefacts dans l’environnement cible pour l’application Teams.

### <a name="teamsfx-collaboration"></a>TeamsFx Collaboration

Il permet aux développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx pour déboguer, approvisionner et déployer le même projet TeamsFx.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Projet Teamsfx":::

## <a name="development"></a>Développement

Teams Toolkit vous aide à créer et personnaliser votre projet d’application Teams, ce qui simplifie le développement d’applications Teams.

### <a name="create-a-new-teams-app"></a>Créer une application Teams.

Il vous aide à démarrer avec le développement d’applications Teams en créant un projet Teams à l’aide du Kit de ressources Teams à l’aide de **Créer un projet** ou **de Démarrer à partir d’un exemple**.

### <a name="add-features"></a>Ajouter des fonctionnalités

Il vous permet d’ajouter incrémentiellement des fonctionnalités Teams supplémentaires telles que **Tab** ou **Bot**, ou éventuellement d’ajouter des ressources Azure telles que **Azure SQL Database** ou **Azure Key Vault**, qui correspond à vos besoins de développement à votre application Teams actuelle. Vous pouvez également ajouter **des flux de travail d’authentification unique** ou **CI/CD** pour votre application Teams.

### <a name="edit-manifest-file"></a>Modifier le fichier manifeste

Il vous aide à modifier l’intégration de l’application Teams avec le client Teams.

## <a name="deployment"></a>Déploiement

Pendant ou après le développement, veillez à provisionner, déployer et publier l’application Teams avant qu’elle ne soit accessible aux utilisateurs.

### <a name="provision-in-the-cloud"></a>Provisionner dans le cloud

Il s’intègre à Azure Resource Manager qui vous permet de provisionner des ressources Azure, dont votre application a besoin pour l’approche du code.

### <a name="deploy-to-the-cloud"></a>Déployer à partir du cloud

 Il vous aide à déployer le code source sur Azure.

### <a name="publish-to-teams"></a>Publier dans Teams

Après avoir créé l’application, vous pouvez distribuer votre application à différentes étendues, telles qu’une personne, une équipe, une organisation ou n’importe qui. Publier dans Teams vous aide à publier votre application développée.

#### <a name="teamsfx-cli"></a>TeamsFx CLI

Il s’agit d’une interface de ligne de commande textuelle qui accélère le développement d’applications Teams et active également le scénario CI/CD dans lequel vous pouvez intégrer l’interface CLI dans des scripts pour l’automatisation.

#### <a name="teamsfx-sdk"></a>Kit de développement logiciel (SDK) TeamsFx

Il vous aide à réduire les tâches d’implémentation de l’identité et d’accès aux ressources cloud aux instructions monolignes sans configuration.

## <a name="help-and-feedback"></a>Aide et commentaires

Dans cette section, vous trouverez la documentation et les ressources dont vous avez besoin. Vous pouvez sélectionner **Signaler les problèmes sur GitHub** dans le Kit de ressources Teams pour obtenir un **Support rapide** de l’expert produit. Parcourez le problème avant d’en créer un nouveau, ou visitez [balise StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) pour soumettre des commentaires.
<!--  
Let's explore Teams Toolkit features.

| Teams Toolkit Features | Includes | What you can do |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 account | Use your Microsoft 365 account with a valid E5 subscription for building your app. |
| &nbsp; | Azure account | Use your Azure account for deploying app on Azure. |
| **Environment** | &nbsp; | &nbsp; |
| &nbsp; | local | Deploy your app in the default local environment with local machine environment configurations. |
| &nbsp; | dev | Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need. |
| **Development** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Use the toolkit wizard to prepare project scaffolding for app development. |
| &nbsp; | View samples | Select any of Teams Toolkit's 12 sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app. |
| &nbsp; | Add Features | - Add other required Teams capabilities to Teams app during development process. </br> - Add optional cloud resources suitable for your app. |
| &nbsp; | Edit manifest file | Edit the Teams app integration with Teams client. |
| **Deployment** | &nbsp; | &nbsp; |
| &nbsp; | Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager. |
| &nbsp; | Zip Teams metadata package | Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.  |
| &nbsp; | Deploy to the cloud | Deploy the source code to Azure. |
| &nbsp; | Publish to Teams | Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization. |
| &nbsp; | Developer Portal for Teams | Use Developer Portal to configure and manage your Teams app. |
| **Help and Feedback** | &nbsp; | &nbsp; |
| &nbsp; | Quick start | View the Teams Toolkit Quick start help within Visual Studio Code.  |
| &nbsp; | Tutorial | Select to access different tutorials. |
| &nbsp; | Documentation | Select to access the Microsoft Teams Developer Documentation. |
| &nbsp; | Report issues on GitHub | Select to access GitHub page and raise any issues. |

-->
> [!TIP]
> Parcourez les problèmes existants avant d’en créer un, ou visitez [balise StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) pour soumettre des commentaires.

## <a name="see-also"></a>Voir aussi

* [Créer un projet à l’aide du kit de ressources Teams](create-new-project.md)
* [Préparer des comptes pour créer des applications Teams](accounts.md)
* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer à partir du cloud](deploy.md)
