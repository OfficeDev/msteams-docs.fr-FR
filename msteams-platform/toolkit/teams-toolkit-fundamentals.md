---
title: Vue d’ensemble du kit de ressources Teams
author: zyxiaoyuer
description: Vue d’ensemble du Kit de ressources Teams, installation de Teams Toolkit et visite guidée des fonctionnalités du Kit de ressources
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/17/2022
ms.openlocfilehash: 36436b5cc2cf7edec784ab653b12d8cf44172b8b
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65654617"
---
# <a name="teams-toolkit-overview"></a>Vue d’ensemble du kit de ressources Teams


Teams Toolkit for Microsoft Visual Studio Code vous aide à créer et déployer des applications Teams avec une identité intégrée, un accès au stockage cloud, des données de Microsoft Graph et d’autres services dans Azure et Microsoft 365 avec une approche de configuration zéro. Pour le développement d’applications Teams, similaire au Kit de ressources Teams pour Visual Studio, vous pouvez utiliser l’[outil CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), qui se compose de toolkit `teamsfx`.
Teams Toolkit vous permet de créer, déboguer et déployer votre application Teams directement à partir de Visual Studio Code. Le développement d’applications avec le kit de ressources présente les avantages suivants :

* Identité intégrée
* Accès au stockage cloud
* Données de Microsoft Graph
* Services Azure et Microsoft 365 avec une approche de configuration zéro

Teams Toolkit propose tous les outils nécessaires à la création d’une application Teams au même endroit.

## <a name="user-journey-of-teams-toolkit"></a>Parcours utilisateur du Kit de ressources Teams

Teams Toolkit automatise le travail manuel et offre une excellente intégration des ressources Teams et Azure. L’image suivante montre le parcours utilisateur du Kit de ressources Teams :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Utilisateur du kit de ressources Teams" border="true":::

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

1. Entrez **Teams Toolkit** dans la zone de recherche.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Kit de ressources":::

1. Sélectionnez **Installer**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="install toolkit 4.0.0":::

> [!TIP]
> Vous pouvez installer teams Toolkit à partir de [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Visite guidée du Kit de ressources Teams

Après l’installation du Kit de ressources, l’interface utilisateur du Kit de ressources Teams s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="mini-fonctions":::

Vous pouvez sélectionner **Prise en main** pour explorer le kit de ressources Teams, ou sélectionner **Créer une application Teams** pour créer un projet Teams. Si vous avez un projet Teams créé par Teams Toolkit ouvert dans Visual Studio Code, vous verrez Teams’interface utilisateur du Kit de ressources avec toutes les fonctionnalités, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="Capture d’écran du kit de ressourcesteams":::

Examinons les sujets abordés dans ce document.

## <a name="accounts"></a>Comptes

Pour développer une application Teams, vous avez besoin d’au moins un compte Microsoft 365 avec un abonnement valide. Si vous souhaitez héberger vos ressources principales sur Azure, un compte Azure est également nécessaire. Teams Toolkit prend en charge l’expérience intégrée pour se connecter, approvisionner et déployer des ressources Azure. Vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="environment"></a>Environnement

Teams Toolkit vous permet de créer et de gérer plusieurs environnements, d’approvisionner et de déployer des artefacts dans l’environnement cible pour l’application Teams.

### <a name="teamsfx-collaboration"></a>TeamsFx Collaboration

Il permet aux développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx pour déboguer, approvisionner et déployer le même projet TeamsFx.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Projet Teamsfx":::

## <a name="development"></a>Développement

Teams Toolkit vous aide à créer et personnaliser votre projet d’application Teams, ce qui simplifie le développement d’applications Teams.

### <a name="create-a-new-teams-app"></a>Créer une application Teams.

Il vous aide à commencer par Teams développement d’applications en créant un projet Teams à l’aide de Teams Toolkit à l’aide de **Créer un projet** ou **de Démarrer à partir d’un exemple**.

### <a name="add-features"></a>Ajouter des fonctionnalités

Il vous permet d’ajouter incrémentiellement des fonctionnalités de Teams supplémentaires telles que **Tab** ou **Bot**, ou d’ajouter éventuellement des ressources Azure telles que **Azure SQL Database** ou **Azure Key Vault**, qui correspond à vos besoins de développement à votre application Teams actuelle. Vous pouvez également ajouter **des flux de travail d’authentification unique** ou **CI/CD** pour votre application Teams. 

### <a name="edit-manifest-file"></a>Modifier le fichier manifeste

Il vous aide à modifier l’intégration de l’application Teams avec le client Teams.

## <a name="deployment"></a>Déploiement

Pendant ou après le développement, veillez à provisionner, déployer et publier l’application Teams avant qu’elle ne soit accessible aux utilisateurs.

### <a name="provision-in-the-cloud"></a>Provisionner dans le cloud

Il s’intègre à Azure Resource Manager qui vous permet de provisionner des ressources Azure dont votre application a besoin pour l’approche du code.

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

Nous allons explorer les fonctionnalités du Kit de ressources Teams.

| Fonctionnalités du kit de ressources Teams | Comprend... | Ce que vous pouvez faire |
| --- | --- | --- |
| **Comptes** | &nbsp; | &nbsp; |
| &nbsp; | Compte Microsoft 365 | Utilisez votre compte Microsoft 365 avec un abonnement E5 valide pour créer votre application. |
| &nbsp; | Compte Azure | Utilisez votre compte Azure pour déployer une application sur Azure. |
| **Environnement** | &nbsp; | &nbsp; |
| &nbsp; | local | Déployez votre application dans l’environnement local par défaut avec des configurations d’environnement d’ordinateur local. |
| &nbsp; | dev | Déployez votre application dans l’environnement de développement par défaut avec des configurations d’environnement distant ou cloud. Vous pouvez créer d’autres environnements, selon vos besoins. |
| **Développement** | &nbsp; | &nbsp; |
| &nbsp; | Créer une application Teams. | Utilisez l’Assistant Kit de ressources pour préparer la génération de modèles automatiques de projet pour le développement d’applications. |
| &nbsp; | Afficher des exemples | Sélectionnez l’un des 12 exemples d’applications du Kit de ressources Teams. Le kit de ressources télécharge le code de l’application à partir de GitHub et vous pouvez générer l’exemple d’application. |
| &nbsp; | Ajouter des fonctionnalités | - Ajoutez d’autres fonctionnalités de Teams requises pour Teams application pendant le processus de développement. </br> - Ajoutez des ressources cloud facultatives adaptées à votre application. |
| &nbsp; | Modifier le fichier manifeste | Modifiez l’intégration de l’application Teams au client Teams. |
| **Déploiement** | &nbsp; | &nbsp; |
| &nbsp; | Provisionner dans le cloud | Allouez des ressources Azure pour votre application. Teams Toolkit est intégré à Azure Resource Manager. |
| &nbsp; | Package de métadonnées Zip Teams | Créez le package d’application qui peut être chargé dans Teams ou Developer Portal. Il contient le manifeste de l’application et les icônes d’application.  |
| &nbsp; | Déployer à partir du cloud | Déployez le code source sur Azure. |
| &nbsp; | Publier dans Teams | Publiez votre application développée et distribuez-la à des étendues telles que personnelles, d’équipe, de canal ou d’organisation. |
| &nbsp; | Documentation pour les développeurs | Utilisez Developer Portal pour configurer et gérer votre application Teams. |
| **Aide et de commentaires** | &nbsp; | &nbsp; |
| &nbsp; | Démarrage rapide | Consultez l’aide de démarrage rapide du kit de ressources Teams dans Visual Studio Code.  |
| &nbsp; | Didacticiel | Sélectionnez cette option pour accéder à différents didacticiels. |
| &nbsp; | Documentation | Sélectionnez cette option pour accéder à la documentation du développeur Microsoft Teams. |
| &nbsp; | Signaler des problèmes sur GitHub | Sélectionnez cette option pour accéder à la page GitHub et signaler tout problème. |


> [!TIP]
> Parcourez les problèmes existants avant d’en créer un, ou visitez [balise StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) pour soumettre des commentaires.

## <a name="see-also"></a>Voir aussi

* [Créer un projet à l’aide du kit de ressources Teams](create-new-project.md)
* [Préparer des comptes pour créer des applications Teams](accounts.md)
* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer à partir du cloud](deploy.md)
