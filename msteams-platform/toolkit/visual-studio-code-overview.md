---
title: Créez des applications avec la boîte à outils Microsoft Teams et Visual Studio Code
description: Démarrage créer d’excellentes applications personnalisées directement dans Visual Studio Code avec le kit de ressources Microsoft Teams.
keywords: Teams Visual Studio Code Toolkit
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 4672c6be9629d70c50885ecd0d9d034c943a337a
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123075"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Créer des applications avec le kit de ressources Teams et le code Visual Studio

Le kit de ressources Teams pour Visual Studio Code aide les développeurs à créer et déployer des applications Teams avec une identité intégrée, un accès au stockage cloud, des données de Microsoft Graph et d’autres services dans Azure et Microsoft 365 avec une approche « zéro configuration » de l’expérience développeur.

Vous pouvez également utiliser le kit de ressources avec Visual Studio ou en tant qu’interface CLI (appelée `teamsfx`).

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Installer le kit de ressources Teams pour Visual Studio Code

1. Ouvrez Visual Studio Code.
1. Sélectionnez la vue Extensions (**Ctrl+Maj+X** / **⌘⇧-X** ou **Afficher les extensions >**).
1. Dans la zone de recherche, entrez _Teams Toolkit_.
1. Sélectionnez le bouton d’installation vert en regard du kit de ressources Teams.

Vous trouverez également le kit de ressources Teams sur la [Place de marché du code Visual Studio](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

Les outils suivants sont installés par l’extension Visual Studio Code quand ils sont nécessaires. Si elle est déjà installée, la version installée est utilisée à la place. Si vous utilisez Linux (y compris WSL), vous devez installer ces outils avant d’utiliser :

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools est utilisé pour exécuter tous les composants principaux localement lors d’une exécution de débogage locale, y compris les assistances d’authentification requises lors de l’exécution de vos services dans Azure. Il est installé dans le répertoire du projet à l’aide de la npm`devDependencies`.

- [Kit de développement logiciel .NET](/dotnet/core/install/)

    Le Kit de développement logiciel (SDK) .NET est utilisé pour installer des liaisons personnalisées pour le débogage local et les déploiements d’applications Azure Functions. Si vous n’avez pas installé le Kit de développement logiciel (SDK) .NET 3.1 ou version ultérieure globalement, la version portable est installée.

- [ngrok](https://ngrok.com/download)

    Certaines fonctionnalités d’application Teams (bots conversationnels, extensions de messagerie et webhooks entrants) nécessitent des connexions entrantes.  Vous devez exposer votre système de développement à Teams par le biais d’un tunnel. Un tunnel n’est pas nécessaire pour les applications qui incluent uniquement des onglets.  Ce package est installé dans le répertoire du projet (à l’aide de npm`devDependencies`).

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Utiliser le kit de ressources Teams pour Visual Studio Code

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Exécuter votre application localement](#install-and-run-your-app-locally)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams

Le kit de ressources Teams peut créer React applications hébergées dans Azure ou SPFx composants WebPart hébergés sur votre environnement Microsoft 365 SharePoint. Pour créer une application React à héberger sur Azure :

1. Ouvrez Visual Studio Code.
1. Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. Sélectionnez **Création d’un projet**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. Sélectionnez **Créer une application Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. À l’étape **Sélectionner des fonctionnalités** , la fonctionnalité **Tab** est déjà sélectionnée. Vous pouvez également sélectionner **éventuellement bot** et **extension de messagerie**.  Appuyez sur **OK**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. À l’étape **Type d’hébergement frontal**, sélectionnez **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. Si vous le souhaitez, dans l’étape **Ressources cloud** , sélectionnez les ressources cloud utilisées par votre application. Vous pouvez sélectionner l’accès CRUD (créer, lire, mettre à jour et supprimer) à une table SQL ou à une API :

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Capture d’écran présentant comment ajouter des ressources cloud à votre nouvelle application.":::

1. À l’étape **Langage de programmation** , vous pouvez choisir **JavaScript** ou **TypeScript** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. Sélectionnez un dossier d’espace de travail. Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.

1. Entrez un nom approprié pour votre application, tel que `helloworld`. Le nom de l’application doit contenir des caractères alphanumériques uniquement. Appuyez sur **Entrer** pour continuer.

Votre application Teams est créée en quelques secondes. L’application échafaudée contient du code pour gérer l’authentification unique avec Azure Active Directory et l’accès à Microsoft Graph. Si vous avez sélectionné des ressources Azure, le code de ces ressources est également disponible.

Pour obtenir un aperçu du processus de création et de publication SPFx, consultez le [didacticiel SPFx](../get-started/first-app-spfx.md).

## <a name="configure-your-app"></a>Configurer votre application

À la base, l’application Teams englobe trois composants :

  1. Client Microsoft Teams (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
  1. Serveur qui répond aux demandes de contenu affichées dans Teams. Par exemple, le contenu de l’onglet HTML ou une carte adaptative de bot.
  1. Un package d’application Teams se compose de trois fichiers :

      > [!div class="checklist"]
      >
      > - Manifest.json.
      > - [Icône de couleur](../resources/schema/manifest-schema.md#icons) que votre application doit afficher dans le catalogue d’applications publique ou d’organisation.
      > - Icône [de plan](../resources/schema/manifest-schema.md#icons) à afficher dans la barre d’activité Teams.

Le manifeste et les icônes sont stockés dans le `.fx` dossier de votre projet avant d’être chargés dans Teams. Lorsqu’une application est installée, le client Teams analyse le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.

1. Pour configurer votre application, accédez à l’onglet **Teams Toolkit** dans Visual Studio Code.
1. Sélectionnez **l’Éditeur de manifeste** dans la section **Project**.

La modification des champs dans la page détails de l’application met à jour le contenu du fichier manifest.json qui est finalement fourni dans le cadre du package d’application.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Pour créer et exécuter votre application localement :

1. À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.

   > Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.  Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée. Cette finalisation peut prendre entre 3 et 5 minutes.

   Le kit de ressources vous invite à installer un certificat local si nécessaire. Ce certificat permet à Teams de charger votre application à partir de `https://localhost`. Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. Votre navigateur web est lancé votre exécuter l’application. Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur. Vous pouvez également être invité à basculer vers l’application Teams à d’autres moments. Sélectionnez l’application web lorsque cela se produit.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. Vous serez peut-être invité à vous connecter. Si c’est le cas, connectez-vous avec votre compte Microsoft 365.
1. Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.

Le back-end et le front-end sont connectés au débogueur Visual Studio Code. Cela vous permet de définir des points d’arrêt n’importe où dans votre code et d’inspecter l’état.  Vous pouvez également utiliser tous les outils de débogage front-end (tels que les outils de développement React) dans le navigateur.  Pour plus d’informations sur le débogage dans Visual Studio Code, consultez [la documentation](https://code.visualstudio.com/Docs/editor/debugging).

## <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

Avant de pouvoir être utilisée par d’autres personnes, vous devez publier votre application sur le portail des développeurs pour Teams.

1. Pour publier votre application, accédez à l’onglet **Teams Toolkit** dans Visual Studio Code.
1. Sélectionnez **Publier sur Teams** dans la section **Project**.

Si vous utilisez l’hébergement Azure, vous devez avoir configuré et déployé sur le cloud. Pour obtenir un aperçu du processus de publication SPFx, consultez le [didacticiel SPFx](../get-started/first-app-spfx.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenance et prise en charge de votre application publiée](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>Voir aussi

- [Créer des applications avec le Teams Toolkit et Visual Studio](~/toolkit/visual-studio-overview.md)
- [Créer des onglets et d’autres expériences hébergées avec le SDK client JavaScript Microsoft Teams](~/tabs/how-to/using-teams-client-sdk.md)
