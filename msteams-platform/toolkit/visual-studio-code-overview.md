---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio code
description: Commencer à créer des applications personnalisées directement dans Visual Studio code avec Microsoft teams Toolkit
keywords: Kit de développement Visual Studio Visual Studio teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 41b0eeaeef1c7094fc9c8cbdc05c2db899245fc6
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476929"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Créer des applications avec Team Toolkit et Visual Studio code

Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code. Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="installing-the-teams-toolkit"></a>Installation du kit de développement teams

Microsoft teams Toolkit for Visual Studio code peut être téléchargé à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu’extension dans Visual Studio code.

> [!TIP]
> Après l’installation, vous devriez voir la boîte à outils teams dans la barre d’activité code Visual Studio. Si ce n’est pas le cas, cliquez avec le bouton droit de la barre d’activité et sélectionnez **Microsoft teams** pour épingler la boîte à outils pour un accès facile.

## <a name="using-the-toolkit"></a>Utilisation de la boîte à outils

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Importer un projet existant](#import-an-existing-teams-app-project)
- [Configurer votre application](#configure-your-app)
- [Empaquetage de votre application](#package-your-app)
- [Exécuter votre application localement ou dans teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet teams

1. Créez un dossier/espace de travail pour votre projet dans votre environnement local.
1. Dans Visual Studio code, sélectionnez l’icône teams ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **ouvrir la boîte à outils Microsoft teams** dans le menu de commandes.
1. Sélectionnez **créer une nouvelle application teams** dans le menu de commandes.
1. Lorsque vous y êtes invité, entrez le nom de l’espace de travail. Il sera utilisé à la fois comme nom du dossier dans lequel votre projet réside et comme nom par défaut de votre application.
1. Appuyez sur **entrée** pour accéder à l’écran **Add Capabilities** et configurer les propriétés de votre nouvelle application.
1. Cliquez sur le bouton **Terminer** pour terminer le processus de configuration.

## <a name="import-an-existing-teams-app-project"></a>Importer un projet d’application teams existant

1. Dans Visual Studio code, sélectionnez l’icône teams ![Icône Teams](../assets/icons/favicon-16x16.png) à partir de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Importer un package d’application** dans le menu de commandes.
1. Choisissez votre fichier zip de [package d’application teams](../concepts/build-and-test/apps-package.md) existant.
1. Cliquez sur le bouton **Sélectionner un package de publication** . L’onglet Configuration de la boîte à outils doit maintenant être renseigné avec les détails de votre application.
1. Dans Visual Studio code, sélectionnez **fichier**  ->  **Ajouter un dossier à l’espace de travail** pour ajouter le répertoire de votre code source à l’espace de travail de code Visual Studio.

## <a name="configure-your-app"></a>Configurer votre application

À son niveau principal, l’application teams adopte trois composants :

  1. Le client Microsoft Teams (Web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Serveur qui répond aux demandes de contenu qui s’affichent dans Teams, par exemple, le contenu de l’onglet HTML ou une carte de robot.
  1. Package d' [application](/concepts/build-and-test/apps-package.md) teams comprenant trois fichiers :

  > [!div class="checklist"]
  >
  > - La manifest.jssur 
  > - Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour l’affichage de votre application dans le catalogue d’applications public ou d’organisation
 > - [Icône de plan](../resources/schema/manifest-schema.md#icons) pour l’affichage dans la barre d’activité de teams.

Lorsqu’une application est installée, le client teams analyse le fichier manifeste pour déterminer les informations nécessaires telles que le nom de votre application et l’URL où se trouvent les services.

1. Pour configurer votre application, accédez à l’onglet **Microsoft teams Toolkit** dans Visual Studio code.
1. Sélectionnez **modifier le package d’application** pour afficher la page des détails de l' **application** .
1. La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application. *Voir* [éditeur de manifeste de l’application Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Empaquetage de votre application

La modification de la page de détails de l' **application** ou la mise à jour du **manifeste**, ou des fichiers **. env** dans le dossier  **. Publish** de votre application, génère automatiquement votre fichier **Development.zip** . Vous devez inclure [deux icônes](../concepts/build-and-test/apps-package.md#icons) dans ce même dossier.

## <a name="run-your-app"></a>Exécuter votre application

### <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Pour obtenir des instructions détaillées sur la façon d’empaqueter et de tester votre application, reportez-vous à la page **générer et exécuter* du contenu dans votre page d’accueil Project. En général, vous devez installer le serveur de votre application, le faire fonctionner, puis configurer une solution de tunneling afin que les équipes puissent accéder au contenu exécuté à partir de localhost.

### <a name="enable-development-from-localhost"></a>Activer le développement à partir de localhost

Si vous souhaitez déboguer votre application basée sur les onglets sur localhost à l’aide du protocole HTTPs, vous devez indiquer à votre navigateur d’approuver l’application en provenance de <https://localhost> . Accédez à la page <https://localhost:3000/tab>. Si vous voyez un avertissement indiquant que le site n’est pas approuvé, sélectionnez l’option continuer quand même. Votre application doit maintenant être accessible depuis le client Teams.

### <a name="run-your-app-in-teams"></a>Exécuter votre application dans teams

Conditions préalables : [activer le mode aperçu développeur teams](https://aka.ms/teams-toolkit-enable-devpreview)

1. Accédez à la barre d’activité sur le côté gauche de la fenêtre de code Visual Studio.
1. Sélectionnez l’icône **exécuter** pour afficher l’affichage **exécuter et déboguer** .
1. Vous pouvez également utiliser le raccourci clavier `Ctrl+Shift+D` .

> [!div class="nextstepaction"]
> [Étape suivante : maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
