---
title: Get started - Build your first Teams app with SPFx
author: zhenyasav
description: Découvrez comment créer un onglet personnalisé à l’SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 54886b47bbe70fed5dd1f010517e6c91d8d5a50d
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646670"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>Créer et exécuter votre première application Microsoft Teams avec SharePoint Framework (SPFx)

Dans ce didacticiel, vous allez créer une application Microsoft Teams dans SharePoint Framework (SPFx) qui implémente une application personnelle simple. (Une *application personnelle inclut* un ensemble d’onglets inclus pour une utilisation individuelle.) Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment l’exécuter localement et comment déployer l’application sur SharePoint.

## <a name="before-you-begin"></a>Avant de commencer

Assurez-vous que votre environnement de développement est bien installé en installant les conditions [préalables](prerequisites.md)

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="get-organized"></a>Organisez-vous

Outre les conditions préalables, vous devez également être administrateur d’une collection SharePoint sites.  C’est ici que vous allez déployer votre application pour l’hébergement.  Si vous utilisez un client de programme pour les développeurs M365, utilisez le compte d’administrateur que vous avez créé lorsque vous vous êtes inscrit au programme.  

## <a name="create-your-project"></a>Créer votre projet

Utilisez la Teams Shared Computer Toolkit pour créer votre premier projet :

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio code.
1. Ouvrez le Teams Shared Computer Toolkit en sélectionnant l’icône Teams dans la barre latérale :

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre Visual Studio Code côté.":::

1. Sélectionnez **Créer un Project**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Créer un Project dans la barre Teams Shared Computer Toolkit côté.":::

1. Sélectionnez **Créer une application Teams.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour créer une Project":::

1. À **l’étape Sélectionner les fonctionnalités,** la fonctionnalité **Onglet** est déjà sélectionnée.  Appuyez sur **OK**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran montrant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. Dans **l’étape du type d’hébergement** frontal, **sélectionnez SharePoint Framework (SPFx).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran montrant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. À **l’étape Framework,** **sélectionnez React**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Select Framework":::

1. Lorsque vous avez demandé un **nom de partie Webpart,** **appuyez sur Entrée** pour accepter la valeur par défaut.

1. Lorsque vous avez demandé la **description du site WebPart,** **appuyez sur Entrée** pour accepter la valeur par défaut.

1. Lorsque vous avez demandé le **langage de programmation,** **appuyez sur Entrée** pour accepter la valeur par défaut.

1. Sélectionnez un dossier d’espace de travail.  Un dossier sera créé dans votre dossier d’espace de travail pour le projet que vous créez.

1. Entrez un nom approprié pour votre application, par `helloworld` exemple.  Le nom de l’application doit uniquement être constitué de caractères alphanumériques.  Appuyez **sur Entrée** pour continuer.

Votre Teams sera créée en quelques secondes.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Utilisez `teamsfx` l’CLI pour créer votre premier projet.  Commencez à partir du dossier dans lequel vous souhaitez créer le dossier de projet.

``` bash
teamsfx new
```

L’CLI vous pose quelques questions pour créer le projet.  Chaque question vous indique comment y répondre (par exemple, pour utiliser des touches de direction pour sélectionner une option).  Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.

1. Sélectionnez **Créer une application Teams.**
1. Choisissez la fonctionnalité **Onglet.**
1. Sélectionnez **SharePoint Framework (SPFx)** frontal.
1. Sélectionnez **React** framework.
1. Appuyez **sur Entrée** pour le nom **du webpart.**
1. Appuyez **sur Entrée** pour obtenir **la description du site WebPart.**
1. Appuyez **sur Entrée** pour le langage **de programmation.**
1. Appuyez **sur Entrée** pour sélectionner le dossier d’espace de travail par défaut.
1. Entrez un nom approprié pour votre application, par `helloworld` exemple.  Le nom de l’application doit uniquement être constitué de caractères alphanumériques.

Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.

---

- [En savoir plus sur le développement pour SharePoint Framework](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>Faire une visite guidée du code source

Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement.](#run-your-app-locally)

Une fois Teams Shared Computer Toolkit votre projet, vous avez les composants pour créer une application personnelle de base pour Teams hébergée dans le SharePoint Framework.  Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour une application personnelle Visual Studio Code.":::

Le Shared Computer Toolkit crée automatiquement la création de la création de la construction automatique dans le répertoire du projet en fonction des fonctionnalités que vous avez ajoutées lors de l’installation. Le Teams Shared Computer Toolkit maintient son état pour votre application dans `.fx` l’annuaire.  Parmi les autres éléments de ce répertoire :

- Les icônes d’application sont stockées en tant que fichiers PNG dans `color.png` et `outline.png` .
- Le manifeste de l’application pour la publication sur le Portail Teams est stocké dans `manifest.source.json` .
- Les paramètres que vous avez choisis lors de la création du projet sont stockés dans `settings.json` .

Étant donné que vous avez sélectionné un SPFx webpart, les fichiers suivants sont pertinents pour votre interface utilisateur :

- Le dossier `SPFx/src/webparts/{webpart}` contient votre SPFx webpart.
- Le fichier `.vscode/launch.json` décrit les configurations de débogage disponibles dans la palette de débogage.

Pour plus d’informations sur SharePoint webparts pour Teams, reportez-vous [à la documentation SharePoint.](/sharepoint/dev/spfx/build-for-teams-overview)

## <a name="run-your-app-locally"></a>Exécuter votre application localement

Teams Shared Computer Toolkit vous permet d’héberger votre application localement et de l’exécuter via [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Créer et exécuter votre application localement dans Visual Studio Code

Pour créer et exécuter votre application localement :

1. À partir Visual Studio Code, appuyez **sur F5**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Capture d’écran montrant comment démarrer une application SPFx dans un workbench local.":::

   > [!NOTE]
   > Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est conçue.  Une fenêtre de navigateur s’ouvre et charge automatiquement SharePoint Workbench une fois la build terminée.  Cela peut prendre entre 3 et 5 minutes.

   Une fois que SharePoint Workbench est chargé.

   >[!NOTE]
   > Le Shared Computer Toolkit vous invite à installer un certificat local si nécessaire. Ce certificat permet Teams charger votre application à partir `https://localhost` de . Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Screenshot showing how the prompt to install a SSL certificate to enable Teams to load your application from localhost.":::

1. Appuyez sur **l’une des** icônes Ajouter un webpart (+) pour ajouter votre webpart.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart showing.":::

1. Choisissez votre webpart dans le menu.

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart selection.":::

Votre application doit maintenant être en cours d’exécution.  Vous pouvez faire des activités de débogage normales comme s’il s’SPFx un autre SPFx webpart (par exemple, la définition de points d’arrêt).

> [!TIP]
> Essayez de placer des points d’arrêt dans la méthode de rendu et de `SPFx/src/webparts/{webpart}/{webpart}.ts` recharger la fenêtre du navigateur. VS Code s’arrête sur les points d’arrêt dans votre code.

## <a name="deploy-your-app-to-sharepoint"></a>Déployer votre application sur SharePoint

Assurez-vous qu SharePoint catalogue d’applications existant dans votre déploiement.  S’il n’en existe pas, [créez-en un.](/sharepoint/use-app-catalog)  La création complète du catalogue d’applications peut prendre jusqu’à 15 minutes.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code.
1. Sélectionnez le Teams Shared Computer Toolkit la barre latérale en sélectionnant l’icône Teams côté.
1. Sélectionnez **Provision dans le cloud**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Capture d’écran montrant les commandes d’approvisionnement":::

1. Vous pouvez surveiller la progression en regardant les boîtes de dialogue dans le coin inférieur droit.  Après quelques secondes, vous verrez l’avis suivant :

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Capture d’écran montrant la boîte de dialogue de mise en service terminée.":::

1. Une fois l’approvisionnement terminé, **sélectionnez Déployer sur le cloud.**

1. Actuellement, le déploiement automatisé n’est pas disponible.  Une boîte de dialogue s’invite à créer et déployer manuellement. Appuyez **sur Build SharePoint Package**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Capture d’écran de la boîte de dialogue Créer un package Sharepoint":::

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Dans la fenêtre de votre terminal :

1. Exécutez `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Vous pouvez être invité à vous connecter à votre abonnement Azure.  Si nécessaire, vous serez invité à sélectionner un abonnement Azure à utiliser pour les ressources Azure.

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

1. Exécutez `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

1. Lorsque vous y sont invités, **sélectionnez Créer SharePoint package.**

---

Le package SharePoint est situé dans `SPFx/sharepoint/solution` votre projet.  Télécharger package à SharePoint :

1. Connectez-vous à la console d’administration M365, puis accédez au SharePoint d’application.

   - Ouvrez `https://admin.microsoft.com/AdminPortal/Home` .
   - Sous **Centres d’administration,** sélectionnez **SharePoint’administration** centrale.
   - Sélectionnez **d’autres** fonctionnalités dans le menu de la barre latérale.
   - Appuyez **sur Ouvrir** sous **Applications.**
   - Sélectionnez **catalogue d’applications.**

1. Sélectionnez **Distribuer des applications pour SharePoint**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Distribuer des applications pour SharePoint.":::

1. Sélectionnez **Télécharger**.

1. Appuyez **sur Choisir un fichier**.

1. Recherchez `{project}.sppkg` votre fichier, situé dans le `SPFx/sharepoint/solution` dossier de votre projet.  Appuyez **sur Ouvrir**.

1. Appuyez sur **OK**.

1. Le SharePoint de déploiement démarre automatiquement.  **Assurez-vous que la vérification de la mise** à disposition de cette solution pour tous les sites de l’organisation est vérifiée, puis appuyez sur **Déployer.**

1. Sélectionnez **l’onglet** FICHIERS.

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Sélectionnez l’onglet Fichiers dans SharePoint catalogue d’applications.":::

1. sélectionnez le package que vous avez déployé, puis appuyez sur **Synchroniser Teams** dans le ruban.

    > [!Note]
    > La synchronisation avec Teams processus peut prendre quelques minutes.  Un message s’affiche sur le côté droit du navigateur indiquant que l’application s’est correctement synchronisée avec Teams.

Ouvrez l Teams application (ou connectez-vous sur `https://teams.microsoft.com` ).  Appuyez sur le point triple sur la barre latérale, puis sélectionnez **Toutes les applications.**  L’application sera placée dans la catégorie **Applications conçues pour votre** organisation.  Vous pouvez ajouter l’application à partir de là.

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Capture d’écran montrant l’application dans Teams":::

## <a name="next-steps"></a>Étapes suivantes

Découvrez les autres méthodes de création d’Teams applications :

- [Créer une application Teams avec React](first-app-react.md)
- [Créer une application Teams avec Blazor](first-app-blazor.md)
- [Créer une application de bot de conversation](first-app-bot.md)
- [Créer une extension de messagerie](first-message-extension.md)
