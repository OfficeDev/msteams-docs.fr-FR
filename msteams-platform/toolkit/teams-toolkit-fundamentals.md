---
title: Teams Shared Computer Toolkit vue d’ensemble
author: zyxiaoyuer
description: 'Vue d’Teams Shared Computer Toolkit, installation de Teams Shared Computer Toolkit et présentation des fonctionnalités Shared Computer Toolkit d’installation'
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="teams-toolkit-overview"></a>Teams Shared Computer Toolkit vue d’ensemble

> [!NOTE]
> Actuellement, cette fonctionnalité est disponible en prévisualisation **pour les développeurs publics** uniquement.

Teams Shared Computer Toolkit vous permet de créer, déboguer et déployer votre application Teams directement à partir de Visual Studio Code. Le développement d’applications avec le kit de ressources présente les avantages de :

- Identité intégrée
- Accès au stockage cloud
- Données de Microsoft Graph
- Azure et les services Microsoft 365 avec une approche de configuration zéro

Teams Shared Computer Toolkit tous les outils nécessaires pour créer une application Teams au même endroit.

Pour Teams développement d’applications, similaire à Teams Shared Computer Toolkit pour Visual Studio Code, vous pouvez utiliser l’outil [CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), qui `teamsfx`se compose de Shared Computer Toolkit .

## <a name="user-journey-of-teams-toolkit"></a>Parcours de l’Teams Shared Computer Toolkit

Teams Shared Computer Toolkit automatise le travail manuel et offre une intégration Teams ressources Azure. L’image suivante illustre Teams Shared Computer Toolkit parcours de l’utilisateur :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams Shared Computer Toolkit parcours de l’utilisateur" border="true":::

Les principaux jalons de ce parcours sont les :

1. Commencez par créer un projet ou essayez un exemple d’Teams application.
1. Ajoutez des fonctionnalités ou modifiez le fichier manifeste selon vos besoins.
1. Utilisez Microsoft 365 pour créer et déboguer votre application Teams client.
1. Utilisez un compte Azure pour mettre en service et déployer votre application dans le cloud.
1. Publiez votre application sur Teams.

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Installer Teams Shared Computer Toolkit pour Visual Studio Code

1. **Ouvrez Visual Studio Code.**
1. Sélectionnez l’affichage Extensions (**Ctrl+Shift+X** / **⌘⇧-X** ou Afficher **> extensions)** :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="install":::

1. Entrez **Teams Shared Computer Toolkit** dans la zone de recherche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-2.png" alt-text="Kit de ressources":::

1. Sélectionnez **Installer** :
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install.png" alt-text="kit de ressources d’installation":::

> [!TIP]
> Vous pouvez installer des Teams Shared Computer Toolkit à partir [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Faites une visite guidée de Teams Shared Computer Toolkit

Après Shared Computer Toolkit’installation, l’interface Teams Shared Computer Toolkit’utilisateur s’affiche, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teams toolkit.png" alt-text="mini fonctions":::

Vous pouvez sélectionner **Démarrage** rapide pour explorer le Teams Shared Computer Toolkit ou sélectionner Créer une application Teams **pour** créer un projet Teams projet. Vous pouvez afficher la liste de toutes les fonctionnalités Shared Computer Toolkit lorsque vous créez ou ouvrez un projet existant dans Visual Studio Code barre latérale.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/toolkit functions.png" alt-text="Fonctions":::

Examinons les sujets abordés dans ce document :

## <a name="accounts"></a>Comptes

Pour développer une application Teams, vous avez besoin d’au moins un compte Microsoft 365 avec un abonnement valide. Si vous souhaitez héberger vos ressources back-end sur Azure, un compte Azure est également nécessaire. Teams Shared Computer Toolkit prend en charge l’expérience intégrée pour se connecter, mettre en service et déployer des ressources Azure. Vous pouvez [créer un compte Azure gratuit avant](https://azure.microsoft.com/free/) de commencer.

## <a name="environment"></a>Environnement

Teams Shared Computer Toolkit vous permet de créer et de gérer plusieurs environnements, de mettre en service et de déployer des artefacts dans l’environnement cible pour Teams App.

### <a name="teamsfx-collaboration"></a>TeamsFx Collaboration

Il permet aux développeurs et au propriétaire du projet d’inviter d’autres collaborateurs au projet TeamsFx pour déboguer, mettre en service et déployer le même projet TeamsFx.

## <a name="development"></a>Développement

Teams Shared Computer Toolkit vous permet de créer et de personnaliser Teams projet d’application qui facilite le Teams de développement d’applications.

### <a name="create-a-new-teams-app"></a>Créer une application Teams de messagerie

Il vous permet de commencer avec Teams développement d’applications en créant un projet Teams à l’aide de Teams Shared Computer Toolkit à l’aide de Créer  un nouveau projet ou créer à partir **d’exemples**.

### <a name="add-capabilities"></a>Ajouter des fonctionnalités

Il permet d’ajouter d’autres fonctionnalités de Teams requises à Teams’application au cours du processus de développement.

### <a name="add-cloud-resources"></a>Ajouter des ressources cloud

Il vous permet d’ajouter, si vous le souhaitez, des ressources cloud adaptées à vos besoins de développement.

### <a name="edit-manifest-file"></a>Modifier le fichier manifeste 

Il vous permet de modifier l’intégration Teams’application avec Teams client.

## <a name="deployment"></a>Déploiement

Pendant ou après le développement, veillez à mettre en service, déployer et publier Teams application avant qu’elle ne soit accessible aux utilisateurs.

### <a name="provision-in-the-cloud"></a>Mise en service dans le cloud

Il s’intègre au Gestionnaire de ressources Azure qui vous permet de mettre en service des ressources Azure, dont votre application a besoin pour l’approche du code.

### <a name="deploy-to-the-cloud"></a>Déployer dans le cloud

 Il vous permet de déployer le code source dans Azure.

### <a name="publish-to-teams"></a>Publier sur Teams

Après avoir créé l’application, vous pouvez distribuer votre application à différentes étendues, telles qu’une personne, une équipe, une organisation ou toute autre personne. Publier sur Teams vous permet de publier votre application développée.

### <a name="cicd-guide"></a>Guide CI/CD

Il permet d’automatiser votre flux de travail de développement lors de la création Teams application. Le guide CI/CD vous fournit des outils et des modèles pour vous aider à démarrer lors de la configuration des pipelines CI ou CD.

#### <a name="teamsfx-cli"></a>TeamsFx CLI

Il s’agit d’une interface de ligne de commande textuelle qui accélère le développement d’applications Teams et permet également un scénario CI/CD dans lequel vous pouvez intégrer l’interface de ligne de commande dans des scripts pour l’automatisation.

#### <a name="teamsfx-sdk"></a>Kit de développement logiciel (SDK) TeamsFx

Il vous aide à réduire les tâches d’implémentation de l’identité et l’accès aux ressources cloud aux instructions à ligne unique avec une configuration nulle.

## <a name="help-and-feedback"></a>Aide et commentaires

Dans cette section, vous trouverez la documentation et les ressources dont vous avez besoin. Vous pouvez sélectionner **Signaler les problèmes sur GitHub** la Teams Shared Computer Toolkit pour obtenir un **support rapide** de la part d’un expert produit. Parcourez le problème avant d’en créer un, ou visitez la balise [StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) pour envoyer des commentaires.

Explorons les fonctionnalités Teams Shared Computer Toolkit de recherche.

| Teams Shared Computer Toolkit fonctionnalités | Inclut... | Ce que vous pouvez faire |
| --- | --- | --- |
| **Comptes** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 compte | Utilisez votre compte Microsoft 365 avec un abonnement E5 valide pour créer votre application. |
| &nbsp; | Compte Azure | Utilisez votre compte Azure pour déployer l’application sur Azure. |
| **Environnement** | &nbsp; | &nbsp; |
| &nbsp; | local | Déployez votre application dans l’environnement local par défaut avec des configurations d’environnement d’ordinateur local. |
| &nbsp; | dev | Déployez votre application dans l’environnement dev par défaut avec des configurations d’environnement distant ou cloud. Vous pouvez créer d’autres environnements, selon vos besoins. |
| **Développement** | &nbsp; | &nbsp; |
| &nbsp; | Créer une application Teams de messagerie | Utilisez l’Assistant Kit de ressources pour préparer la création de lacafé de projet pour le développement d’applications. |
| &nbsp; | Afficher des exemples | Sélectionnez l’Teams Shared Computer Toolkit parmi les 12 exemples d’applications. Le kit de ressources télécharge le code de l’application GitHub, et vous pouvez créer l’exemple d’application. |
| &nbsp; | Ajouter des fonctionnalités | Ajoutez d’autres fonctionnalités Teams requises pour Teams’application au cours du processus de développement. |
| &nbsp; | Ajouter des ressources cloud | Ajoutez des ressources cloud facultatives adaptées à votre application. |
| &nbsp; | Modifier le fichier manifeste | Modifiez l Teams’intégration de l’application Teams client. |
| **Déploiement** | &nbsp; | &nbsp; |
| &nbsp; | Mise en service dans le cloud | Allouez des ressources Azure à votre application. Teams Shared Computer Toolkit est intégré à Azure Resource Manager. |
| &nbsp; | Package de métadonnées Teams zip | Créez le package d’application qui peut être téléchargé vers Teams ou le portail du développeur. Il contient le manifeste de l’application et les icônes de l’application.  |
| &nbsp; | Déployer dans le cloud | Déployez le code source dans Azure. |
| &nbsp; | Publier sur Teams | Publiez votre application développée et distribuez-la à des étendues telles que personnelle, d’équipe, de canal ou d’organisation. |
| &nbsp; | Documentation pour les développeurs | Utilisez le portail du développeur pour configurer et gérer votre application Teams client. |
| &nbsp; | Guide CI/CD | Automatisez votre flux de travail de développement lors de la création Teams application. |
| **Aide et commentaires** | &nbsp; | &nbsp; |
| &nbsp; | Démarrage rapide | Affichez l Teams Shared Computer Toolkit de démarrage rapide dans Visual Studio Code.  |
| &nbsp; | Documentation | Sélectionnez cette sélection pour accéder à Microsoft Teams documentation du développeur. |
| &nbsp; | Signaler les problèmes sur GitHub | Choisissez d’accéder GitHub page et de lever des problèmes. |
|

> [!TIP]
> Parcourez les problèmes existants avant d’en créer un nouveau ou visitez la balise [StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) pour envoyer des commentaires.

## <a name="see-also"></a>Voir aussi

* [Créer un projet à l’aide Teams Shared Computer Toolkit](create-new-project.md)
* [Préparer les comptes à créer des applications Teams client](accounts.md)
* [Publier des applications Teams à l’aide du Kit de ressources Teams](publish.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer dans le cloud](deploy.md)
