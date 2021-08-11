---
title: Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio Code l’aide Microsoft Teams Shared Computer Toolkit
keywords: kit de ressources teams Visual Studio Code
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 76e31270f19b5062869dda83766d189ef178612a76ca5eae80e734ffbb072e21
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709343"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio Code

La Teams Shared Computer Toolkit pour Visual Studio Code permet aux développeurs de créer et de déployer des applications Teams avec une identité intégrée, l’accès au stockage cloud, les données de Microsoft Graph et d’autres services dans Azure et M365 avec une approche « de configuration zéro » de l’expérience développeur.  

Vous pouvez également utiliser le kit de ressources avec Visual Studio ou en tant qu’CLI (appelé `teamsfx` ).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Installer le Teams Shared Computer Toolkit pour Visual Studio Code

1. Ouvrez Visual Studio Code.
1. Sélectionnez l’affichage Extensions (**Ctrl+Shift+X**  /  **⌘⇧-X** ou Afficher **> extensions**).
1. Dans la zone de recherche, entrez _Teams Shared Computer Toolkit_.
1. Sélectionnez le bouton d’installation vert en Teams Shared Computer Toolkit.

Vous pouvez également trouver le Teams Shared Computer Toolkit sur le [Visual Studio Code Marketplace.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

Les outils suivants sont installés par l’extension Visual Studio Code si nécessaire. S’il est déjà installé, la version installée est utilisée à la place. Si vous utilisez Linux (y compris WSL), vous devez installer ces outils avant d’utiliser :

- [Outils azure Functions Core](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools permet d’exécuter localement tous les composants principaux lors d’une exécution de débogage locale, y compris les outils d’aide à l’authentification requis lors de l’exécution de vos services dans Azure. Il est installé dans le répertoire du projet à l’aide de npm `devDependencies` .

- [Kit de développement logiciel .NET](/dotnet/core/install/)

    Le SDK .NET permet d’installer des liaisons personnalisées pour le débogage local et les déploiements d’applications Azure Functions. Si vous n’avez pas installé le SDK .NET 3.1 ou version ultérieure globalement, la version portable est installée.

- [ngrok](https://ngrok.com/download)

    Certaines Teams d’application (bots de conversation, extensions de messagerie et webhooks entrants) nécessitent des connexions entrantes.  Vous devez exposer votre système de développement à la Teams via un tunnel. Un tunnel n’est pas requis pour les applications qui incluent uniquement des onglets.  Ce package est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Utilisez la Teams Shared Computer Toolkit pour Visual Studio Code

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Exécuter votre application localement](#install-and-run-your-app-locally)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams projet

Le Teams Shared Computer Toolkit peut créer des applications React hébergées dans Azure ou des composants Web SPFx hébergés sur votre environnement de SharePoint M365. Pour créer une application React à héberger sur Azure :

1. Ouvrez Visual Studio Code.
1. Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. Sélectionnez **Création d’un projet**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. Sélectionnez **Créer une application Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. À **l’étape Sélectionner les fonctionnalités,** la fonctionnalité **Onglet** est déjà sélectionnée. Vous pouvez également  sélectionner bot et **extension de messagerie.**  Appuyez sur **OK**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. À l’étape **Type d’hébergement frontal**, sélectionnez **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. Éventuellement, à l’étape Des ressources **cloud,** sélectionnez les ressources cloud que votre application utilise. Vous pouvez sélectionner l’accès CRUD (créer, lire, mettre à jour et supprimer) à une table SQL une API :

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Capture d’écran présentant comment ajouter des ressources cloud à votre nouvelle application.":::

1. À **l’étape Du langage de** programmation, vous pouvez choisir **JavaScript** ou **TypeScript**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. Sélectionnez un dossier d’espace de travail. Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.

1. Entrez un nom approprié pour votre application, tel que `helloworld`. Le nom de l’application doit contenir des caractères alphanumériques uniquement.  Appuyez sur **Entrer** pour continuer.

Votre application Teams est créée en quelques secondes. L’application échafaudée contient du code pour gérer l' sign-on unique Azure Active Directory et l’accès au microsoft Graph.  Si vous avez sélectionné des ressources Azure, le code de ces ressources est également disponible.

Pour une procédure pas à pas du processus SPFx création et de publication, voir [le didacticiel SPFx de publication.](../get-started/first-app-spfx.md)

## <a name="configure-your-app"></a>Configurer votre application

L’application Teams principale englobe trois composants :

  1. Le Microsoft Teams client (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Serveur qui répond aux demandes de contenu affichées dans Teams. Par exemple, le contenu d’onglet HTML ou une carte adaptative de bot.
  1. Un package Teams’application se compose de trois fichiers :

      > [!div class="checklist"]
      >
      > - Le manifest.jsest alors en cours.
      > - Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou de l’organisation.
      > - Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.

Le manifeste et les icônes sont stockés dans le dossier de votre projet avant d’être chargés `.fx` vers Teams. Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.

1. Pour configurer votre application, accédez à **l’onglet Teams Shared Computer Toolkit** dans Visual Studio Code.
1. Sélectionnez **l’Éditeur** de **manifeste dans Project** section.

La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui est finalement livré dans le cadre du package d’application.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Pour créer et exécuter votre application localement :

1. À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.

   > Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.  Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.  Cette finalisation peut prendre entre 3 et 5 minutes.

   Le kit de ressources vous invite à installer un certificat local si nécessaire. Ce certificat permet à Teams de charger votre application à partir de `https://localhost`. Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. Votre navigateur web est lancé votre exécuter l’application. Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur. Vous pouvez également être invité à basculer vers l’application Teams à d’autres moments. Sélectionnez l’application web lorsque cela se produit.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. Vous serez peut-être invité à vous connecter. Dans ce cas, connectez-vous à l'aide de votre compte M365.
1. Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.

Le back-end et le frontend sont raccordés au débo Visual Studio Code débogger.  Cela vous permet de définir des points d’arrêt n’importe où dans votre code et d’inspecter l’état.  Vous pouvez également utiliser n’importe quel outil de débogage frontal (par exemple, React Outils de développement) dans le navigateur.  Pour plus d’informations sur le débogage dans Visual Studio Code, [examinez la documentation.](https://code.visualstudio.com/Docs/editor/debugging)

## <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

Avant de pouvoir être utilisé par d’autres personnes, vous devez publier votre application sur le portail de développement pour Teams.

1. Pour publier votre application, accédez à **l’onglet Teams Shared Computer Toolkit** dans Visual Studio Code.
1. Sélectionnez **Publier à Teams** dans la section **Project** de publication.

Si vous utilisez l’hébergement Azure, vous devez avoir mis en service et déployé sur le cloud. Pour une procédure pas à pas du processus SPFx de publication, voir [le didacticiel SPFx de publication.](../get-started/first-app-spfx.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
