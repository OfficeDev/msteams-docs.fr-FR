---
title: Créer des applications avec le code de Shared Computer Toolkit et Visual Studio Microsoft Teams
description: Commencer à créer d'excellentes applications personnalisées directement dans Visual Studio Code avec microsoft Teams Shared Computer Toolkit
keywords: kit de ressources teams Visual Studio Code
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020260"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Créer des applications avec le code Shared Computer Toolkit et Visual Studio Teams

Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code. Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="installing-the-teams-toolkit"></a>Installation de l'Shared Computer Toolkit

Microsoft Teams Shared Computer Toolkit for Visual Studio Code est disponible en téléchargement à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu'extension dans Visual Studio Code.

> [!TIP]
> Après l'installation, les équipes doivent s'Shared Computer Toolkit dans la barre Visual Studio'activité code. Si ce n'est pas le cas, cliquez avec le bouton droit dans la barre d'activité et sélectionnez **Microsoft Teams** pour épingler le kit de ressources pour un accès facile.

## <a name="using-the-toolkit"></a>Utilisation du kit de ressources

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Importer un projet existant](#import-an-existing-teams-app-project)
- [Configurer votre application](#configure-your-app)
- [Package de votre application](#package-your-app)
- [Exécuter votre application localement ou dans Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams

1. Créez un espace de travail/dossier pour votre projet dans votre environnement local.
1. Dans Visual Studio code, sélectionnez l'icône Teams ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d'activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Ouvrir l'Shared Computer Toolkit Microsoft Teams** dans le menu de commande.
1. Sélectionnez **Créer une application Teams dans** le menu de commande.
1. Lorsque vous y invitez, entrez le nom de l'espace de travail. Il sera utilisé à la fois comme nom du dossier où résidera votre projet et comme nom par défaut de votre application.
1. Appuyez **sur Entrée** pour accéder à l'écran Ajouter des **fonctionnalités** et configurer les propriétés de votre nouvelle application.
1. Sélectionnez le **bouton** Terminer pour terminer le processus de configuration.

## <a name="import-an-existing-teams-app-project"></a>Importer un projet d'application Teams existant

1. Dans Visual Studio code, sélectionnez l'icône Teams ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d'activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Importer un package d'application** dans le menu de commande.
1. Choisissez votre fichier zip de [package d'application Teams](../concepts/build-and-test/apps-package.md) existant.
1. Sélectionnez **le bouton Sélectionner un package de** publication. L'onglet configuration du kit de ressources doit maintenant être rempli avec les détails de votre application.
1. Dans Visual Studio code, sélectionnez Fichier Ajouter un dossier à l'espace de travail pour ajouter votre répertoire de code source à l'espace   ->   Visual Studio code.

## <a name="configure-your-app"></a>Configurer votre application

Au cœur de l'application Teams, trois composants sont intégrés :

  1. Client Microsoft Teams (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Un serveur qui répond aux demandes de contenu qui sera affiché dans Teams, par exemple, du contenu d'onglet HTML ou une carte adaptative de bot .
  1. Un [package d'application](/concepts/build-and-test/apps-package.md) Teams composé de trois fichiers :

  > [!div class="checklist"]
  >
  > - Le manifest.jssur 
  > - Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour votre application à afficher dans le catalogue d'applications public ou de l'organisation
 > - Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre d'activité Teams.

Lorsqu'une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l'URL où se trouvent les services.

1. Pour configurer votre application, accédez à l'onglet **Shared Computer Toolkit Microsoft Teams** dans Visual Studio Code.
1. Sélectionnez **Modifier le package d'application** pour afficher la page **Détails de l'application.**
1. La modification des champs dans la page détails de l'application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l'application. *Voir* [l'éditeur de manifeste App Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Package de votre application

La modification de la page de **détails** **de** l'application, du manifeste ou des fichiers **.env** dans le dossier  **.publish** de votre application génère automatiquement **Development.zip** fichier. Vous devez inclure deux [icônes](../concepts/build-and-test/apps-package.md#app-icons) dans ce même dossier.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

## <a name="run-your-app"></a>Exécuter votre application

### <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Reportez-vous à * Créer et exécuter *du* contenu dans la page d'accueil de votre projet pour obtenir des instructions détaillées sur la façon de créer un package et de tester votre application. En règle générale, vous devez installer le serveur de votre application, le faire fonctionner, puis configurer une solution de tunnel afin que Teams puisse accéder au contenu s'exécutant à partir de l'host local.

### <a name="enable-development-from-localhost"></a>Activer le développement à partir de l'host local

Si vous souhaitez déboguer votre application basée sur l'onglet sur localhost à l'aide du protocole HTTPS, vous devrez indiquer à votre navigateur d'faire confiance à l'application à partir de . <https://localhost> Accédez à la page <https://localhost:3000/tab>. Si vous voyez un avertissement indiquant que le site n'est pas approuvé, choisissez l'option pour continuer malgré tout. Votre application doit maintenant être accessible à partir du client Teams.

### <a name="run-your-app-in-teams"></a>Exécuter votre application dans Teams

Conditions préalables : activer [le mode d'aperçu pour les développeurs Teams](https://aka.ms/teams-toolkit-enable-devpreview)

1. Accédez à la barre d'activité sur le côté gauche de la Visual Studio Code.
1. Sélectionnez **l'icône** Exécuter pour afficher **l'affichage Exécuter et déboguer.**
1. Vous pouvez également utiliser le raccourci `Ctrl+Shift+D` clavier.

> [!div class="nextstepaction"]
> [Étape suivante : maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
