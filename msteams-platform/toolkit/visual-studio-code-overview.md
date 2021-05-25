---
title: Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio Code l’aide Microsoft Teams Shared Computer Toolkit
keywords: kit de ressources teams Visual Studio Code
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d51ccf3ed62e22fb417eec72d1f409b1b77b9da6
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629836"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio Code

Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code. Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="installing-the-teams-toolkit"></a>Installation du Teams Shared Computer Toolkit

Le Microsoft Teams Shared Computer Toolkit pour Visual Studio Code est disponible en téléchargement à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu’extension dans Visual Studio Code.

> [!TIP]
> Après l’installation, vous devez voir le Teams Shared Computer Toolkit dans la barre d Visual Studio Code’activité. Si ce n’est pas le cas, cliquez avec le bouton droit dans la barre **d’activité** et sélectionnez Microsoft Teams pour épingler le kit de ressources pour faciliter l’accès.

## <a name="using-the-toolkit"></a>Utilisation du kit de ressources

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Importer un projet existant](#import-an-existing-teams-app-project)
- [Configurer votre application](#configure-your-app)
- [Package de votre application](#package-your-app)
- [Exécuter votre application localement ou dans Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams projet

1. Créez un espace de travail ou un dossier pour votre projet dans votre environnement local.
1. Dans Visual Studio Code, sélectionnez l’icône Teams de l’icône ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Ouvrir le Microsoft Teams Shared Computer Toolkit** dans le menu de commande.
1. Sélectionnez **Créer une application Teams dans** le menu de commande.
1. Lorsque vous y invitez, entrez le nom de l’espace de travail. Il sera utilisé à la fois comme nom du dossier où résidera votre projet et comme nom par défaut de votre application.
1. Appuyez **sur Entrée** et vous arriverez à l’écran Ajouter **des** fonctionnalités pour configurer les propriétés de votre nouvelle application.
1. Sélectionnez le **bouton** Terminer pour terminer le processus de configuration.

## <a name="import-an-existing-teams-app-project"></a>Importer un projet d’Teams existant

1. Dans Visual Studio Code, sélectionnez l’icône Teams de l’icône ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Importer un package d’application** dans le menu de commande.
1. Choisissez votre fichier zip Teams [package d’application](/microsoftteams/platform/concepts/build-and-test/apps-package?view=msteams-client-js-latest&preserve-view=true) existant.
1. Sélectionnez le bouton Sélectionner **un package de** publication. L’onglet configuration du kit de ressources doit maintenant être rempli avec les détails de votre application.
1. Dans Visual Studio Code, sélectionnez Ajouter un dossier à l’espace de travail pour ajouter votre répertoire de code source à l Visual Studio Code  ->   de travail.

## <a name="configure-your-app"></a>Configurer votre application

L’application Teams principale englobe trois composants :

  1. Le Microsoft Teams client (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Serveur qui répond aux demandes de contenu qui s’afficheront dans Teams. Par exemple, le contenu d’onglet HTML ou une carte adaptative de bot.
  1. Un package Teams’application se compose de trois fichiers :

      > [!div class="checklist"]
      >
      > - Le manifest.jsest alors en cours. 
      > - Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou d’organisation.
      > - Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.

Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.

1. Pour configurer votre application, accédez à **l’onglet Microsoft Teams Shared Computer Toolkit** dans Visual Studio Code.
1. Sélectionnez **Modifier le package d’application** pour afficher la page **Détails de l’application.**
1. La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l’application. Pour plus d’informations, voir [l’éditeur de manifeste App Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Package de votre application

La modification de la page de **détails** **de** l’application, du manifeste ou des fichiers **.env** dans le dossier  **.publish** de votre application génère automatiquement **Development.zip** fichier. Vous devez inclure deux [icônes](../concepts/build-and-test/apps-package.md#app-icons) dans ce même dossier.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

## <a name="run-your-app"></a>Exécuter votre application

### <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Reportez-vous **au contenu Créer** et exécuter dans la page d’accueil de votre projet pour obtenir des instructions détaillées sur la façon de créer un package et de tester votre application. En règle générale, vous devez installer le serveur de votre application, le faire fonctionner, puis configurer une solution de tunnel afin que Teams puisse accéder au contenu s’exécutant à partir de l’host local.

### <a name="enable-development-from-localhost"></a>Activer le développement à partir de l’host local

Si vous souhaitez déboguer votre application basée sur l’onglet sur localhost à l’aide du protocole HTTPS, vous devrez indiquer à votre navigateur d’faire confiance à l’application à partir de . `<https://localhost>` Accédez à la page `<https://localhost:3000/tab>`. Si vous voyez un avertissement indiquant que le site n’est pas approuvé, choisissez l’option pour continuer malgré tout. Votre application doit maintenant être accessible à partir du client Teams client.

### <a name="run-your-app-in-teams"></a>Exécuter votre application dans Teams

Conditions préalables : activer [Teams mode d’aperçu pour les développeurs](https://aka.ms/teams-toolkit-enable-devpreview)

1. Accédez à la barre d’activité sur le côté gauche de Visual Studio Code fenêtre.
1. Sélectionnez **l’icône** Exécuter pour afficher **l’affichage Exécuter et déboguer.**
1. Vous pouvez également utiliser le raccourci `Ctrl+Shift+D` clavier.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
