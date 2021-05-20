---
title: Créez des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code
description: Obtenez commencé à construire d’excellentes applications personnalisées directement Visual Studio Code avec le Microsoft Teams Shared Computer Toolkit
keywords: équipes kit d’outils de code studio visuel
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566557"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Créez des applications avec les Teams Shared Computer Toolkit et Visual Studio Code

Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code. Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="installing-the-teams-toolkit"></a>Installation de la Teams Shared Computer Toolkit

Le Microsoft Teams Shared Computer Toolkit pour Visual Studio Code est disponible en téléchargement sur [le Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement sous forme d’extension dans Visual Studio Code.

> [!TIP]
> Après l’installation, vous devriez voir les Teams Shared Computer Toolkit la barre d Visual Studio Code’activité. Si ce n’est pas le cas, cliquez à droite dans la barre **d’activité et sélectionnez Microsoft Teams** épingler la boîte à outils pour un accès facile.

## <a name="using-the-toolkit"></a>Utilisation de la boîte à outils

- [Mettre en place un nouveau projet](#set-up-a-new-teams-project)
- [Importer un projet existant](#import-an-existing-teams-app-project)
- [Configurer votre application](#configure-your-app)
- [Emballez votre application](#package-your-app)
- [Exécutez votre application localement ou en Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>Mettre en place un nouveau projet Teams projet

1. Créez un espace de travail ou un dossier pour votre projet dans votre environnement local.
1. Dans Visual Studio Code, sélectionnez l’icône Teams’actualité ![Icône Teams](../assets/icons/favicon-16x16.png) de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Ouvrez Microsoft Teams Shared Computer Toolkit du** menu de commande.
1. Sélectionnez **Créer une nouvelle application Teams à partir** du menu de commande.
1. Lorsque vous êtes invité, entrez le nom de l’espace de travail . Cela sera utilisé à la fois comme nom du dossier où votre projet résidera, et le nom par défaut de votre application.
1. Appuyez **sur** Entrez et vous arriverez à **l’écran des fonctionnalités Ajouter** configurer les propriétés de votre nouvelle application.
1. Sélectionnez **le bouton** Finition pour compléter le processus de configuration.

## <a name="import-an-existing-teams-app-project"></a>Importer un projet d’application Teams’environnement existant

1. Dans Visual Studio Code, sélectionnez l’icône Teams’actualité ![Icône Teams](../assets/icons/favicon-16x16.png) de la barre d’activité sur le côté gauche de la fenêtre.
1. Sélectionnez **Le package d’application** Import dans le menu de commande.
1. Choisissez votre fichier [zip Teams’application](../concepts/build-and-test/apps-package.md) existante.
1. Choisissez le bouton **Sélectionner le paquet de** publication. L’onglet configuration de la boîte à outils doit maintenant être rempli des détails de votre application.
1. Dans Visual Studio Code, sélectionnez **Fichier**  ->  **Ajouter dossier à Workspace pour** ajouter votre répertoire de code source à l’espace de travail Visual Studio Code source.

## <a name="configure-your-app"></a>Configurer votre application

À la base, l Teams apprateur de messagerie embrasse trois composantes :

  1. Le Microsoft Teams client (web, bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Un serveur qui répond aux demandes de contenu qui seront affichées dans Teams. Par exemple, le contenu de l’onglet HTML ou une carte adaptative bot.
  1. Un [Teams’application comprenant](/concepts/build-and-test/apps-package.md) trois fichiers :

      > [!div class="checklist"]
      >
      > - Le manifest.jssur. 
      > - Une [icône couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications publiques ou organisation.
      > - Une [icône de contour](../resources/schema/manifest-schema.md#icons) pour l’affichage sur la barre d Teams’activité.

Lorsqu’une application est installée, le client Teams parse le fichier manifeste pour déterminer les informations nécessaires comme le nom de votre application et l’URL où se trouvent les services.

1. Pour configurer votre application, accédez **à l’onglet** Microsoft Teams Shared Computer Toolkit’Visual Studio Code.
1. Sélectionnez **Modifier le paquet d’applications** pour afficher la page **détails de** l’application.
1. L’édition des champs dans la page détails de l’application met à jour le contenu des manifest.jsdans le fichier qui sera finalement expédié dans le cadre du paquet d’application. Pour plus d’informations, voir [l’éditeur manifeste d’App Studio](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>Emballez votre application

La modification de la page **de détails** de **l’application,** manifeste, **ou .env** fichiers dans le  **dossier de votre application .publish** générera **automatiquement votreDevelopment.zip** fichier. Vous devrez inclure deux [icônes dans](../concepts/build-and-test/apps-package.md#app-icons) ce même dossier.

## <a name="install-and-run-your-app-locally"></a>Installez et exécutez votre application localement

## <a name="run-your-app"></a>Exécuter votre application

### <a name="install-and-run-your-app-locally"></a>Installez et exécutez votre application localement

Reportez-vous au **contenu Build and Run** de votre page d’accueil du projet pour obtenir des instructions détaillées sur la façon d’emballer et de tester votre application. En général, vous devez installer le serveur de votre application, l’exécuter, puis configurer une solution de tunneling afin que Teams puisse accéder au contenu en cours d’exécution à partir de localhost.

### <a name="enable-development-from-localhost"></a>Permettre le développement à partir de localhost

Si vous souhaitez débobug votre application basée sur l’onglet sur localhost en utilisant HTTPS, vous devrez dire à votre navigateur de faire confiance à l’application en cours de service à partir <https://localhost> de . Accédez à la page <https://localhost:3000/tab>. Si vous voyez un avertissement indiquant que le site n’est pas fiable, choisissez l’option de procéder de toute façon. Votre application doit désormais être accessible à partir du Teams client.

### <a name="run-your-app-in-teams"></a>Exécutez votre application dans Teams

Conditions préalables : [Activer le mode Teams aperçu des développeurs](https://aka.ms/teams-toolkit-enable-devpreview)

1. Accédez à la barre d’activité sur le côté gauche de la Visual Studio Code fenêtre.
1. Sélectionnez **l’icône** Exécuter pour afficher **la vue Exécuter et Debug.**
1. Vous pouvez également utiliser le raccourci clavier `Ctrl+Shift+D` .

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenir et soutenir votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
