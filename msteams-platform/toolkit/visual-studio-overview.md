---
title: Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide Microsoft Teams Shared Computer Toolkit
keywords: boîte à outils visual studio teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949699"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio

Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio. Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="prerequisites"></a>Conditions requises

1. [Activer la prévisualisation pour les développeurs.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. Assurez-vous que **<span>le</span>module ASP.NE T** et le module de développement web ont été ajoutés à Visual Studio instance. Vous pouvez vérifier en suivant les étapes de la Visual Studio en ajoutant ou en supprimant des charges de travail et de la documentation [sur les composants.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)

![Module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, vous devez avoir installé Internet Information Services (IIS) dans votre environnement de développement. Visual Studio n’inclut pas IIS et n’est pas inclus dans la configuration Windows 10, Windows 8 ou Windows 7 par défaut ; Toutefois, vous pouvez télécharger la dernière version à partir du Centre [de téléchargement Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)

![Vue de page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Installer le Teams Shared Computer Toolkit

Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio. À partir Visual Studio Marketplace téléchargez également [Teams Shared Computer Toolkit pour Visual Studio 2019.](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)

## <a name="using-the-toolkit"></a>Utilisation du kit de ressources

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Package de votre application](#package-your-app)
- [Installer et exécuter votre application dans Teams](#install-and-run-your-app-locally)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams projet

![Teams kit de ressources installé](../assets/images/teamstoolkiticon.png)

1. Sélectionnez **Création d’un projet**.

    ![Création d’un projet](../assets/images/createnewproject.png)

1. Choisissez l’outil de démarrage rapide **pour Microsoft Teams app,** puis sélectionnez **Suivant.**
1. Dans la page **Configurer votre nouveau** projet, entrez le **Project,** l’emplacement et le **nom de la solution.** 
1. Sélectionnez la solution et le projet Place dans la même case **à cocher d’annuaire.**
1. Dans la **fenêtre pop-up Ajouter** des fonctionnalités, choisissez une ou plusieurs fonctionnalités pour la configuration de votre projet.
1. Sélectionnez **le bouton** Suivant pour terminer le processus de configuration.
1. Dans la **fenêtre pop-up Ajouter des** fonctionnalités, choisissez les propriétés de chaque fonctionnalité sélectionnée.
1. Sélectionnez **Terminer**. La **Microsoft Teams Shared Computer Toolkit** page d’accueil de l’événement s’affiche.

    ![Teams page d’accueil du kit de ressources](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a>Configurer votre application

L’application Teams principale englobe trois composants :

  1. Le client Microsoft Teams web, de bureau ou mobile, où les utilisateurs interagissent avec votre application.
  1. Un serveur qui répond aux demandes de contenu qui s’affiche dans Teams, par exemple, du contenu d’onglet HTML ou une carte adaptative de bot.
  1. Un package Teams’application se compose de trois fichiers :

      - Le manifest.jssur
      - Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou de l’organisation.
      - Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.

Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.

> [!NOTE]
>Si ce n’est pas déjà fait, vous devez vous Microsoft 365 votre compte d’utilisateur pour poursuivre le processus de développement.
>
> Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement [Microsoft 365 programme pour les développeurs.](https://developer.microsoft.com/microsoft-365/dev-program) Il est gratuit pendant 90 jours et renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 développeur [gratuit,](https://aka.ms/MyVisualStudioBenefits)actif pendant toute la durée de Visual Studio abonnement. Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)

### <a name="configuration-steps"></a>Étapes de configuration

1. Pour configurer votre application,  sur la page Microsoft Teams Shared Computer Toolkit’accueil, sélectionnez **Modifier le package d’application.**
1. Dans le menu **déroulant Mes environnements,** sélectionnez **Développement.**
1. Dans la page **Détails de l’application,** modifiez les champs de propriété de votre application.
    
    La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera intégré au package d’application. Pour plus d’informations, [voir Teams Shared Computer Toolkit manifeste.](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Package de votre application

La modification de la page de **détails** de l’application ou la mise à jour du manifeste **ou** des fichiers **.env** dans le dossier **.publish** de votre application génère automatiquement **votre fichierDevelopment.zip..** Le Development.zip inclut trois fichiers requis, **l'manifest.jset** [deux icônes.](../concepts/build-and-test/apps-package.md#app-icons)

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

1. Dans le menu **déroulant Configurations** de la solution, **sélectionnez Déployer** comme illustré dans l’image suivante :

    ![Menu Configurations de la solution](../assets/images/solution-configurations.png)

1. Sélectionnez **le IIS Express + Teams** bouton.

    La boîte de dialogue d’installation de l’application s’affiche dans Teams client.

## <a name="validate-your-app"></a>Valider votre application

La  page Valider vous permet de vérifier votre package d’application avant de la soumettre à AppSource. Il vous suffit de charger le package de manifeste et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste. Pour chaque échec de test, la description fournit un lien de documentation pour vous aider à corriger l’erreur. Pour les tests difficiles à automatiser, la liste de contrôle préliminaire détaille 7 des cas de test les plus courants qui ont échoué, ainsi qu’un lien vers une liste de vérification de soumission complète. 

## <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

* Sur la page d’accueil de votre projet, vous pouvez télécharger votre application dans une équipe, l’envoyer sur le magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs Teams.

* Votre administrateur informatique examine ces envois.

* Vous pouvez revenir à **la** page Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous pouvez soumettre des mises à jour à votre application ou annuler les soumissions actives.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
