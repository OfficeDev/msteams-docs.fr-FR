---
title: Vue d’ensemble du kit de ressources Teams
author: zyxiaoyuer
description: Vue d’ensemble du Kit de ressources Teams, installation de Teams Toolkit et visite guidée des fonctionnalités du Kit de ressources
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: de249f060581c2d8e1f90408c8431fe451125ef2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111422"
---
# <a name="teams-toolkit-overview"></a>Vue d’ensemble du kit de ressources Teams

> [!NOTE]
> Actuellement, cette fonctionnalité est disponible dans **préversion publique des développeurs** uniquement.

Teams Toolkit for Microsoft Visual Studio Code vous aide à créer et déployer des applications Teams avec une identité intégrée, un accès au stockage cloud, des données de Microsoft Graph et d’autres services dans Azure et Microsoft 365 avec une approche de configuration zéro. Pour le développement d’applications Teams, similaire au Kit de ressources Teams pour Visual Studio, vous pouvez utiliser l’[outil CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), qui se compose de toolkit `teamsfx`.
Teams Toolkit vous permet de créer, déboguer et déployer votre application Teams directement à partir de Visual Studio Code. Le développement d’applications avec le kit de ressources présente les avantages suivants :

* Identité intégrée
* Accès au stockage cloud
* Données de Microsoft Graph
* Services Azure et Microsoft 365 avec une approche de configuration zéro

Teams Toolkit propose tous les outils nécessaires à la création d’une application Teams au même endroit.

Pour le développement d’applications Teams, similaire au Kit de ressources Teams pour Visual Studio Code, vous pouvez utiliser l’['outil CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), qui se compose de `teamsfx` kit de ressources.

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
1. Sélectionnez la vue Extensions (**Ctrl+Maj+X** / **⌘⇧-X** ou **Afficher > extensions**) :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="installer":::

1. Entrez du **Kit de ressources Teams** dans la zone de recherche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-2.png" alt-text="Kit de ressources":::

1. Sélectionnez **installer**:
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install.png" alt-text="installer le kit de ressources":::

> [!TIP]
> Vous pouvez installer teams Toolkit à partir de [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Visite guidée du Kit de ressources Teams

Après l’installation du Kit de ressources, l’interface utilisateur du Kit de ressources Teams s’affiche comme indiqué dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teams toolkit.png" alt-text="mini-fonctions":::

Vous pouvez sélectionner **Démarrage rapide** pour explorer le Kit de ressources Teams ou sélectionner **Créer une application Teams** pour créer un projet Teams. Si vous avez un projet Teams créé par Teams Toolkit v2.+ ouvert dans Visual Studio Code, vous verrez l’interface utilisateur du Kit de ressources Teams avec toutes les fonctionnalités, comme illustré dans l’image suivante : vous pouvez sélectionner **Démarrage rapide** pour explorer le Kit de ressources Teams, ou sélectionner **Créer une application Teams** pour créer un projet Teams. Vous pouvez afficher la liste de toutes les fonctionnalités du Kit de ressources lorsque vous créez ou ouvrez un projet existant dans Visual Studio Code barre latérale.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/toolkit functions.png" alt-text="Fonctions":::

Passons en revue les sujets abordés dans ce document :

## <a name="accounts"></a>Comptes

Pour développer une application Teams, vous avez besoin d’au moins un compte Microsoft 365 avec un abonnement valide. Si vous souhaitez héberger vos ressources principales sur Azure, un compte Azure est également nécessaire. Teams Toolkit prend en charge l’expérience intégrée pour se connecter, approvisionner et déployer des ressources Azure. Vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="environment"></a>Environnement

Teams Toolkit vous permet de créer et de gérer plusieurs environnements, d’approvisionner et de déployer des artefacts dans l’environnement cible pour l’application Teams.

### <a name="teamsfx-collaboration"></a>TeamsFx Collaboration

Il permet aux développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx pour déboguer, approvisionner et déployer le même projet TeamsFx.

## <a name="development"></a>Développement

Teams Toolkit vous aide à créer et personnaliser votre projet d’application Teams, ce qui simplifie le développement d’applications Teams.

### <a name="create-a-new-teams-app"></a>Créer une application Teams.

Il vous aide à démarrer avec le développement d’applications Teams en créant un projet Teams à l’aide du Kit de ressources Teams à l’aide de **Créer un projet** ou **Créer à partir d’exemples**.

### <a name="add-capabilities"></a>Ajouter des fonctionnalités

Il permet d’ajouter d’autres fonctionnalités Teams requises à l’application Teams pendant le processus de développement.

### <a name="add-cloud-resources"></a>Ajouter des ressources cloud

Il vous permet d’ajouter éventuellement des ressources cloud adaptées à vos besoins de développement.

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

### <a name="cicd-guide"></a>Guide CI/CD

Il permet d’automatiser votre flux de travail de développement lors de la création d’une application Teams. Le guide CI/CD fournit des outils et des modèles pour vous permettre de commencer à configurer des pipelines CI ou CD.

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
| &nbsp; | Ajouter des fonctionnalités | Ajoutez d’autres fonctionnalités Teams requises à l’application Teams pendant le processus de développement. |
| &nbsp; | Ajouter des ressources cloud | Ajoutez des ressources cloud facultatives adaptées à votre application. |
| &nbsp; | Modifier le fichier manifeste | Modifiez l’intégration de l’application Teams au client Teams. |
| **Déploiement** | &nbsp; | &nbsp; |
| &nbsp; | Provisionner dans le cloud | Allouez des ressources Azure pour votre application. Teams Toolkit est intégré à Azure Resource Manager. |
| &nbsp; | Package de métadonnées Zip Teams | Créez le package d’application qui peut être chargé dans Teams ou Developer Portal. Il contient le manifeste de l’application et les icônes d’application.  |
| &nbsp; | Déployer à partir du cloud | Déployez le code source sur Azure. |
| &nbsp; | Publier dans Teams | Publiez votre application développée et distribuez-la à des étendues telles que personnelles, d’équipe, de canal ou d’organisation. |
| &nbsp; | Documentation pour les développeurs | Utilisez Developer Portal pour configurer et gérer votre application Teams. |
| &nbsp; | Guide CI/CD | Automatiser votre flux de travail de développement lors de la création d’une application Teams. |
| **Aide et de commentaires** | &nbsp; | &nbsp; |
| &nbsp; | Démarrage rapide | Affichez l’aide du kit de ressources Teams Démarrage rapide dans Visual Studio Code.  |
| &nbsp; | Documentation | Sélectionnez cette option pour accéder à la documentation du développeur Microsoft Teams. |
| &nbsp; | Signaler des problèmes sur GitHub | Sélectionnez cette option pour accéder à la page GitHub et signaler tout problème. |
|

> [!TIP]
> Parcourez les problèmes existants avant d’en créer un, ou visitez [balise StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) pour soumettre des commentaires.

## <a name="see-also"></a>Voir aussi

* [Créer un projet à l’aide du kit de ressources Teams](create-new-project.md)
* [Préparer des comptes pour créer des applications Teams](accounts.md)
* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer à partir du cloud](deploy.md)
