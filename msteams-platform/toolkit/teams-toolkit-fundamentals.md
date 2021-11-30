---
title: Teams Shared Computer Toolkit de base
author: zyxiaoyuer
description: Décrit les principes de base de Teams Shared Computer Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 121f376f3958ad2c78eabf446efb14d11f733e68
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227932"
---
# <a name="teams-toolkit"></a>Teams Shared Computer Toolkit

> [!NOTE]
> Actuellement, cette fonctionnalité est disponible en prévisualisation **pour les** développeurs publics uniquement.

Teams Shared Computer Toolkit for Visual Studio Code permet aux développeurs de créer et de déployer des applications Teams avec une identité intégrée, l’accès au stockage cloud, les données de Microsoft Graph et d’autres services dans Azure et Microsoft 365  avec une approche de configuration zéro pour l’expérience du développeur.  

Il existe une Teams Shared Computer Toolkit pour Visual Studio et un outil [CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) pour Teams développement d’applications (appelé `teamsfx` ).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Installer le Teams Shared Computer Toolkit pour Visual Studio Code

1. Ouvrez **Visual Studio Code.**

1. Sélectionnez l’affichage Extensions (**Ctrl+Shift+X**  /  **⌘⇧-X** ou **Afficher > extensions**).

1. Dans la zone de recherche, entrez **Teams Shared Computer Toolkit**.

1. Sélectionnez **le** bouton Installer en Teams Shared Computer Toolkit.

Vous pouvez également trouver le Teams Shared Computer Toolkit sur [le Visual Studio Code Marketplace.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

## <a name="support-teams-apps-capabilities"></a>Prise en charge Teams applications

[Microsoft Teams fonctionnalités d’application](../concepts/capabilities-overview.md) sont Teams points d’extensibilité.Teams Shared Computer Toolkit for Visual Studio Code permet aux développeurs de travailler sur un projet avec les fonctionnalités d’Teams suivantes :

* [Onglets](../tabs/what-are-tabs.md#microsoft-teams-tabs)

* [Bots](../bots/what-are-bots.md#bots-in-microsoft-teams)

* [Extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md#messaging-extensions) 

Votre Teams projet peut contenir l’une des fonctionnalités ou les trois fonctionnalités ci-dessus. Vous pouvez sélectionner n’importe quelle fonctionnalité lorsque vous créez le Teams Project.

![Sélectionner des fonctionnalités pour créer des Project](./images/create-project-capabilities.png)

Teams Shared Computer Toolkit offre la flexibilité nécessaire pour ajouter d’autres fonctionnalités dans le processus de développement Teams d’application.

![ajouter des fonctionnalités](./images/add-capabilities.png)

## <a name="user-journey-of-teams-toolkit"></a>Parcours de l’Teams Shared Computer Toolkit

Teams Shared Computer Toolkit fournit des fonctionnalités de Teams développement d’applications pour faciliter le débogage, le déploiement et la publication. Teams Shared Computer Toolkit automatise le travail manuel et offre une intégration Teams ressources Azure. L’image suivante illustre Teams Shared Computer Toolkit parcours de l’utilisateur :

![Teams Shared Computer Toolkit parcours de l’utilisateur](./images/teams-toolkit-user-journey.png)

## <a name="take-a-tour-of-teams-toolkit-for-visual-studio-code"></a>Faites une visite guidée de Teams Shared Computer Toolkit’Visual Studio Code

Si vous n’ouvrez aucun projet Teams dans VS Code ou si vous ouvrez un projet qui n’est pas créé à l’aide de Teams Shared Computer Toolkit v2.+, vous verrez l’interface utilisateur Teams Shared Computer Toolkit avec des fonctionnalités limitées, comme illustré dans l’image suivante :

:::image type="content" source="./images/teams-toolkit-beforestart.png" alt-text="Avant le début Teams Shared Computer Toolkit":::

Vous pouvez sélectionner **Démarrage** rapide pour explorer le Teams Shared Computer Toolkit ou sélectionner Créer une application Teams **pour** créer un projet Teams projet. Si un Teams Project créé par Teams Shared Computer Toolkit v2.+ est ouvert dans VS Code, vous verrez une interface utilisateur Teams Shared Computer Toolkit avec davantage de fonctionnalités, comme illustré dans l’image suivante :

:::image type="content" source="./images/teams-toolkit-overview.png" alt-text="Faites une visite guidée de Teams Shared Computer Toolkit":::

Examinons les fonctionnalités disponibles dans Teams Shared Computer Toolkit :

* [Comptes](#accounts)

* [Environnement](#environment)

* [Développement](#development)

* [Déploiement](#deployment)

* [Aide et commentaires](#help-and-feedback)

### <a name="accounts"></a>Comptes

Les développeurs doivent avoir un compte Microsoft 365 pour créer Teams application. Si vous n’en avez pas, vous pouvez obtenir un compte Teams développeur gratuit en rejoignant le programme [Microsoft 365 développeur :](https://developer.microsoft.com/microsoft-365/dev-program)

![Teams Shared Computer Toolkit une visite guidée - Comptes](./images/teams-toolkit-accounts.png)

Le compte Azure est couramment utilisé dans Teams développement d’applications. Si vous souhaitez héberger votre application Teams ou accéder aux ressources sur Azure, vous devez avoir un compte Azure. Teams Shared Computer Toolkit prise en charge de l’expérience intégrée pour se connecter, mettre en service et déployer des ressources Azure. Vous pouvez [créer un compte Azure gratuit avant](https://azure.microsoft.com/free/) de commencer.

 Pour plus d’informations, voir [préparer les comptes à la Teams app.](accounts.md)

### <a name="environment"></a>Environnement

Teams Shared Computer Toolkit vous permet de gérer plusieurs environnements. Vous pouvez ajouter, configurer et personnaliser des environnements. Vous pouvez choisir d’ajouter des collaborateurs pour chaque environnement :

![Teams Shared Computer Toolkit une visite guidée - Environnement](./images/teams-toolkit-env.png)

 Pour plus d’informations, [voir gérer plusieurs environnements](TeamsFx-multi-env.md) et collaborer avec d’autres développeurs [sur Teams projet.](TeamsFx-collaboration.md)

### <a name="development"></a>Développement

Teams Shared Computer Toolkit vous permet de créer et de personnaliser votre projet d’application Teams qui permet au Teams de développement d’applications de fonctionner facilement et rapidement : 

![Teams Shared Computer Toolkit une visite guidée - Développement](./images/teams-toolkit-development.png)

1. **Créer une application Teams**, permet de démarrer Teams développement d’applications avec un projet de modèle « Hello World » ou un exemple de projet. Pour plus d’informations, [voir créer Teams projet](create-new-project.md)
1. **Afficher des exemples**, présente un ensemble de Teams d’exemples d’applications que vous pouvez explorer, référencer et développer.
1. **Ajouter des fonctionnalités**, permet d’ajouter Teams fonctionnalités à Teams’application à tout moment pendant le processus de développement. Pour plus d’informations, voir [ajouter des fonctionnalités à votre Teams application](add-capability.md)
1. **L’ajout de ressources** cloud vous permet d’ajouter des ressources cloud supplémentaires en fonction de la modification des conditions requises. Pour plus d’informations, voir [ajouter des ressources cloud pour Teams application](add-resource.md)
1. **Modifier le fichier manifeste** vous permet de modifier facilement la façon dont Teams’application s’intègre Teams client. Pour plus d’informations, [voir Teams fichier manifeste et](TeamsFx-manifest-preview.md) modifier Teams fichier [manifeste.](TeamsFx-manifest-customization.md)

### <a name="deployment"></a>Déploiement

Pendant ou après le développement, vous devez suivre le processus de mise en service, de déploiement et de publication de l’application Teams avant qu’elle ne soit accessible à vos utilisateurs :

![Teams Shared Computer Toolkit une visite guidée - Déploiement](./images/teams-toolkit-deployment.png)

1. Si vous souhaitez héberger votre application Teams sur Azure ou utiliser des ressources Azure, la mise en service dans le **cloud** vous permet d’automatiser le processus de création de ressources Azure. Pour l’utiliser, vous devez avoir un abonnement Azure. Pour plus d’informations, voir [la mise en service des ressources cloud.](provision.md)

1. Avant de publier votre application ou de partager votre application, vous pouvez créer votre application Teams en packages en **sélectionnant Zip Teams package de métadonnées**.

1. **Déployer dans le cloud vous** permet de déployer leur code source dans Azure. La configuration requise pour exécuter le déploiement consiste à avoir mis en service des ressources en exécutant provision dans le **cloud** ou vous devez créer les ressources Azure manuellement et spécifier le paramètre de ressource dans les paramètres de votre environnement de projet. Pour plus d’informations, [voir déployer Teams’application dans le cloud.](deploy.md)

1. Au lieu de publier manuellement votre application Teams personnalisée, vous pouvez utiliser la fonction Publier sur **Teams** pour appeler Teams api pour publier Teams application. Vous avez besoin de l’autorisation de télécharger Teams’application. Pour plus d’informations, [voir publier votre application sur Teams](publish.md).

1. Le Portail des développeurs Teams est l’endroit où vous pouvez gérer et distribuer Teams application. Pour plus d’informations, voir [le portail des développeurs](/microsoftteams/platform/concepts/build-and-test/teams-developer-portal)

1. Teams Shared Computer Toolkit fournit également un modèle CI/CD pour les outils CI/CD tels que GitHub flux de travail, Azure Devops et Jenkins. Pour plus d’informations, [voir build CI/CD pipelines for Teams application](use-CICD-template.md)

### <a name="help-and-feedback"></a>Aide et commentaires

Dans cette section, vous trouverez facilement la documentation et les ressources dont vous avez besoin. Vous pouvez sélectionner **Signaler les problèmes sur GitHub** la Teams Shared Computer Toolkit pour obtenir un support **rapide** de la part d’un expert produit. Parcourez le problème avant d’en créer un, ou visitez la balise [StackOverflow `teams-toolkit` ](https://stackoverflow.com/questions/tagged/teams-toolkit) pour parcourir et poser des questions :

![Teams Shared Computer Toolkit une visite guidée - Aide](./images/teams-toolkit-help.png)

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Créer une nouvelle utilisation de projet Teams Shared Computer Toolkit](create-new-project.md)

> [!div class="nextstepaction"]
>[Préparer les comptes à créer des applications Teams client](accounts.md)
