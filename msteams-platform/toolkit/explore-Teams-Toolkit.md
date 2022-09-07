---
title: Explorer le Kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment explorer Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 0ef95064a1715a64d8f719c54aced7cdc74ecb23
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617246"
---
# <a name="explore-teams-toolkit"></a>Explorer le Kit de ressources Teams

Dans ce document, vous pouvez comprendre différents éléments d’interface utilisateur, ainsi que la description et l’utilisation de base dans le Kit de ressources Teams.

## <a name="teams-toolkit-basic-ui-elements"></a>Éléments d’interface utilisateur de base du Kit de ressources Teams

Après l’installation du Kit de ressources Teams, vous verrez l’interface utilisateur du Kit de ressources Teams, comme illustré dans l’image suivante :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1.png" alt-text="Vue d’ensemble de Teams Toolkit":::

| Numéro de série | Éléments d’interface utilisateur | Définition |
| --- | --- |
| 1 | **Prise en main** | Explorez le Kit de ressources Teams. |
| &nbsp; | **Tutoriels** | Accéder à différents didacticiels. |
| &nbsp; | **Documentation** | Accédez à la documentation du développeur Microsoft Teams. |
| 2 | **Créer une application Teams** | Créez une application Teams en fonction de vos besoins. |
| 3 | **Afficher les exemples** | Créez différents types d’application en fonction d’exemples existants. |
| 4 | **Ouvrir le dossier** | Ouvrez l’application Teams existante. |
| 5 | **Nouveau fichier** | Créez un fichier. |
| &nbsp; | **Ouvrir le fichier** | Ouvrez le fichier existant. |
| &nbsp; | **Ouvrir le dossier** | Ouvrez le dossier existant. |
| 6 | **Récente** | Affichez les fichiers récents. |

### <a name="exploring-the-teams-toolkit-task-pane"></a>Exploration du volet Office du Kit de ressources Teams

Vous pouvez explorer d’autres éléments d’interface utilisateur à partir du volet Office dans le Kit de ressources Teams. Le volet Office est visible uniquement après la création d’une application à l’aide du Kit de ressources Teams. La vidéo suivante vous aide à connaître le processus de création d’une application Teams et, après ce processus, vous pouvez afficher le volet Office dans le Kit de ressources Teams.

   ![Créer une application Teams](~/assets/videos/javascript-tab-app1.gif)

Après avoir créé une application Teams, vous pouvez voir la structure de répertoire de l’application dans le volet gauche et le fichier lisez-moi dans le volet droit.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page.png" alt-text="Première page du Kit de ressources Teams":::

Faisons une visite guidée de l’interface utilisateur du Kit de ressources Teams.

 Dans la barre d’outils Visual Studio Code, les icônes suivantes sont pertinentes pour le Kit de ressources Teams :

| Icône | Description |
| --- | --- |
| **Explorer** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | Pour afficher la structure de répertoire de l’application. |
| **Exécuter et déboguer** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | Pour démarrer le processus de débogage local ou distant. |
| **Toolkit Teams** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | Pour afficher le volet Office dans le Kit de ressources Teams. |

Dans le volet Office, vous pouvez voir les sections suivantes :

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1.png" alt-text="section comptes":::
   :::column-end:::
   :::column span="":::

        Pour développer une application Teams, vous avez besoin des comptes suivants :
        
        * **Connectez-vous à M365** : utilisez votre compte Microsoft 365 avec un abonnement E5 valide pour créer votre application.

        * **Connectez-vous à Azure** : utilisez votre compte Azure pour déployer l’application sur Azure. Vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/free/) avant de commencer.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="Section Environnement":::
   :::column-end:::
   :::column span="":::

        Pour déployer votre application Teams, vous avez besoin des environnements suivants :
        
       * **local** : déployez votre application dans l’environnement local par défaut avec des configurations d’environnement de machine locale.

        * **dev** : déployez votre application dans l’environnement de développement par défaut avec des configurations d’environnement distant ou cloud. Vous pouvez créer d’autres environnements, selon vos besoins.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development.png" alt-text="Section Développement":::
   :::column-end:::
   :::column span="":::

        Pour créer et personnaliser votre application Teams, vous avez besoin des fonctionnalités suivantes :
        
       * **Créer une application Teams** : utilisez l’Assistant Kit de ressources pour préparer la génération de modèles automatiques de projet pour le développement d’applications.

        * **Afficher les exemples** : sélectionnez l’une des exemples d’applications du Kit de ressources Teams. Le kit de ressources télécharge le code de l’application à partir de GitHub et vous pouvez générer l’exemple d’application.
        
        * **Ajouter des fonctionnalités** : ajoutez d’autres fonctionnalités Teams requises à l’application Teams pendant le processus de développement et ajoutez des ressources cloud facultatives adaptées à votre application.
       
        * **Modifier le fichier manifeste** : modifier l’intégration de l’application Teams au client Teams.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="Section Déploiement":::
   :::column-end:::
   :::column span="":::

        Pour provisionner, déployer et publier votre application Teams, vous avez besoin des fonctionnalités suivantes :
        
        * **Provisionner dans le cloud** : allouer des ressources Azure pour votre application. Teams Toolkit est intégré à Azure Resource Manager.

        * **Package de métadonnées Zip Teams** : créez le package d’application qui peut être chargé dans Teams ou le portail des développeurs. Il contient le manifeste de l’application et les icônes d’application.
        
        * **Déployer sur le cloud** : déployez le code source sur Azure.
       
        * **Publier dans Teams** : publiez votre application développée et distribuez-la dans des étendues telles que personnelle, d’équipe, de canal ou d’organisation.
        
        * **Portail des développeurs pour Teams** : utilisez le portail des développeurs pour configurer et gérer votre application Teams. 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="Section Aide et commentaires":::
   :::column-end:::
   :::column span="":::

        Pour accéder à plus d’informations sur teams Toolkit. vous avez besoin de la documentation et des ressources suivantes.
        
        * **Prise en main** : consultez l’aide prise en main du Kit de ressources Teams dans Visual Studio Code.

        * **Didacticiels** : Sélectionnez cette option pour accéder à différents didacticiels.
        
        * **Documentation** : Sélectionnez cette option pour accéder à la documentation du développeur Microsoft Teams.
       
        * **Signaler des problèmes sur GitHub** : sélectionnez pour accéder à la page GitHub et soulever des problèmes.
   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Voir aussi

* [Installer Teams Toolkit](install-Teams-Toolkit.md)
* [Créer une application Teams à l’aide du kit de ressources Teams](create-new-project.md)
* [Préparer la création d’applications à l’aide de Microsoft Teams Toolkit](build-environments.md)
* [Provisionner des ressources cloud à l’aide du Kit de ressources Teams](provision.md)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="UI Elements":::

|Section|Features|Details
|---------|---------|--------|
| **1. ACCOUNTS** | &nbsp; | &nbsp; |
| &nbsp; |Microsoft 365 account|  Use your Microsoft 365 account with a valid E5 subscription for building your app.|
| &nbsp; | Azure Account |  Use your Azure account for deploying app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.|
|**2.ENVIRONMENT** |  &nbsp; | &nbsp;|
| &nbsp; |Local |Deploy your app in the default local environment with local machine environment configurations.|
| &nbsp; | Dev |Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need.|
| **3.DEVELOPMENT** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Teams Toolkit helps you to create and customize your Teams app project that makes the Teams app development work simpler. Create a new Teams app helps you to start with Teams app development by creating new Teams project using Teams Toolkit either by using **Create new project**|
| &nbsp; | View Samples | Select any of Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app.|
| &nbsp; | Add Features | It helps you to add additional Teams capabilities such as **Tab** or **Bot** or **Message extension** or **Command bot** or **Notification bot**, or **SSO enabled tab** optionally add Azure resources such as **Azure SQL Database** or **Azure Key Vault**, or **Azure function** or **Azure API Management** which fits your development needs to your current Teams app. You can also add **API connection** or **Single Sign-on** or **CI/CD workflows** for your Teams app.
| &nbsp; | Edit Manifest file | It helps you customize manifest file based on the app requirements |
| **4.DEPLOYMENT** | &nbsp; | &nbsp; |
| &nbsp;| Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager.|
| &nbsp; | Zip Teams metadata package| Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons. |
| &nbsp; | Deploy to the cloud| Deploy the source code to Azure.|
| &nbsp; | Publish to Teams| Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.|
| &nbsp; | Developer Portal for Teams| It is the primary tool for configuring, distributing, and managing your Microsoft Teams apps. You can collaborate with colleagues on your app, set up runtime environments, and much more. |
| **5.HELP AND FEEDBACK** | &nbsp; | &nbsp; |
| &nbsp; | Get Started |  View the Teams Toolkit Get started help within Visual Studio Code.|
| &nbsp; | Tutorials| Select to access different tutorials.|
| &nbsp; | Documentation| Select to access the Microsoft Teams Developer Documentation.|
| &nbsp; | Report issues on GitHub| It helps to get **Quick support** from product expert. Browse the existing issues before you create a new one, or visit [StackOverflow tag `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) to submit feedback.|
| **6.Explorer** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | It helps to view the directory structure of your app.|
| **7.Run and Debug** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | To start the local or remote debug process.|
-->
