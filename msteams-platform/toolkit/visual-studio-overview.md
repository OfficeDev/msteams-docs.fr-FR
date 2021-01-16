---
title: Créez des applications avec les Shared Computer Toolkit et Visual Studio Microsoft Teams
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide de Microsoft Teams Shared Computer Toolkit
keywords: boîte à outils visual studio teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875006"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Créer des applications avec les Shared Computer Toolkit et Visual Studio

Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio. Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="prerequisites"></a>Conditions préalables

1. [Activer la prévisualisation pour les développeurs](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. Assurez-vous que **<span>le</span>module ASP.NE T** et le module de développement web ont été ajoutés à votre instance Visual Studio web. Vous pouvez vérifier en suivant les étapes de la Visual Studio en ajoutant ou en supprimant des charges de travail et de la documentation [sur les composants.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)

![module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, iiS (Internet Information Services) doit être installé dans votre environnement de développement. Visual Studio n’inclut pas IIS et n’est pas inclus dans la configuration par défaut de Windows 10, Windows 8 ou Windows 7 ; Toutefois, vous pouvez télécharger la dernière version à partir du Centre [de téléchargement Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)

![Vue de page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Installer la Shared Computer Toolkit Teams

Le Shared Computer Toolkit Microsoft Teams pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.

## <a name="using-the-toolkit"></a>Utilisation du kit de ressources

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Package de votre application](#package-your-app)
- [Exécuter votre application dans Teams](#install-and-run-your-app-locally)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams

1. Sélectionnez **Créer un projet.**
1. Choisissez **l’application Microsoft Teams et** sélectionnez **Suivant.**
1. Vous arrivez à **l’écran Configurer** votre nouveau projet où vous pouvez choisir le nom du **projet,** l’emplacement **et** le nom de **la solution.**
1. Cochez la case **« Placer la solution et le projet dans le même répertoire**».
1. Une fenêtre pop-up étiquetée **Ajouter des** fonctionnalités vous permettra de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.
1. Sélectionnez **le bouton** Suivant pour terminer le processus de configuration.
1. Une fenêtre pop-up étiquetée **Ajouter des** fonctionnalités vous permet de choisir les propriétés de chaque fonctionnalité sélectionnée.
1. Sélectionnez **Terminer** et vous allez vous poser sur la page d’accueil **Shared Computer Toolkit Microsoft Teams.**

## <a name="configure-your-app"></a>Configurer votre application

Au cœur de l’application Teams, trois composants sont intégrés :

  1. Client Microsoft Teams (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Un serveur qui répond aux demandes de contenu qui sera affiché dans Teams, par exemple, du contenu d’onglet HTML ou une carte adaptative de bot .
  1. Un [package d’application](/concepts/build-and-test/apps-package.md) Teams composé de trois fichiers :

  > [!div class="checklist"]
  >
  > - Le manifest.jssur
  > - Icône [de couleur à](../resources/schema/manifest-schema.md#icons) afficher dans le catalogue d’applications public ou d’organisation
 > - Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre d’activité Teams.

Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.

> [!NOTE]
>Si vous ne l’avez pas déjà fait, vous devrez vous connectez à votre compte ou à votre compte Microsoft 365 pour poursuivre le processus de développement.
>
> Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement au programme pour les développeurs [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) Il est *gratuit pendant* 90 jours et est continuellement renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement  Visual Studio *Entreprise* ou Professionnel, les deux programmes incluent un abonnement microsoft 365 [](https://aka.ms/MyVisualStudioBenefits)développeur gratuit, actif pendant toute la durée de vie de Visual Studio abonnement. *Voir* [Configurer un abonnement Microsoft 365 Développeur.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)
>

### <a name="configuration-steps"></a>Étapes de configuration

1. Pour configurer votre application, sur la page d’accueil Shared Computer Toolkit **Microsoft Teams,** **sélectionnez Modifier le package d’application.**
1. Dans le menu **déroulant Mes environnements,** sélectionnez **Développement.**
1. Vous allez vous trouver sur la page **des détails de l’application** où vous pouvez modifier les champs de propriété de votre application.
1. La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l’application. [En savoir plus](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Package de votre application

La modification de la page de **détails** de l’application ou la mise à jour du manifeste **ou** des fichiers **.env** dans le dossier **.publish** de votre application génère automatiquement **votre fichierDevelopment.zip..** Le Development.zip inclut trois fichiers obligatoires : **l'manifest.jset** [deux icônes.](../concepts/build-and-test/apps-package.md#app-icons)

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

1. Dans le menu **déroulant Configurations** de la solution, sélectionnez **Déployer.**

![Menu Configurations de solution](../assets/images/solution-configurations.png)

2. Sélectionnez **le bouton IIS Express + Teams.**

1. Teams se lance et le dialogue d’installation de l’application doit apparaître dans le client Teams.

## <a name="validate-your-app"></a>Valider votre application

La  page Valider vous permet de vérifier votre package d’application avant de la soumettre à AppSource. Il vous suffit de charger le package de manifeste et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste. Pour chaque échec de test, la description fournit un lien de documentation pour vous aider à corriger l’erreur. Pour les tests qui sont difficiles  à automatiser, la liste de contrôle préliminaire détaille 7 des cas de test les plus courants qui ont échoué, ainsi qu’un lien vers une liste de vérification de soumission complète.

## <a name="publish-your-app-to-teams"></a>Publier votre application dans Teams

✔ Sur la page d’accueil de votre projet, vous pouvez télécharger votre application vers une équipe, soumettre votre application au magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source d’application pour tous les utilisateurs de Teams.

✔ votre administrateur informatique examine ces soumissions.

✔ vous pouvez revenir à la **page** Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous allez soumettre des mises à jour à votre application ou annuler les soumissions actives.

> [!div class="nextstepaction"]
> [Étape suivante : maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
