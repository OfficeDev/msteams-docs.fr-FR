---
title: Get started - Build your first Teams app with SPFx
author: zhenyasav
description: Découvrez comment créer un onglet personnalisé à l’SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 7bbbf7ae1d74a9094af5bc6ca4b3ac797ba05d5d
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037662"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="552a5-103">Créer et exécuter votre première application Microsoft Teams avec SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="552a5-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="552a5-104">Dans ce didacticiel, vous allez créer une application Microsoft Teams dans SharePoint Framework (SPFx) qui implémente une application personnelle simple.</span><span class="sxs-lookup"><span data-stu-id="552a5-104">In this tutorial, you will create a new Microsoft Teams app in SharePoint Framework (SPFx) that implements a simple personal app.</span></span> <span data-ttu-id="552a5-105">(Une *application personnelle inclut* un ensemble d’onglets inclus pour une utilisation individuelle.) Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment l’exécuter localement et comment déployer l’application sur SharePoint.</span><span class="sxs-lookup"><span data-stu-id="552a5-105">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run the app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="552a5-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="552a5-106">Before you begin</span></span>

<span data-ttu-id="552a5-107">Vérifiez que votre environnement de développement est configuré en installant les [Conditions préalables](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="552a5-107">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="552a5-108">Installer les composants prérequis</span><span class="sxs-lookup"><span data-stu-id="552a5-108">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="552a5-109">Organisez-vous</span><span class="sxs-lookup"><span data-stu-id="552a5-109">Get organized</span></span>

<span data-ttu-id="552a5-110">Outre les conditions préalables, vous devez également être administrateur d’une collection SharePoint sites.</span><span class="sxs-lookup"><span data-stu-id="552a5-110">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="552a5-111">C’est ici que vous allez déployer votre application pour l’hébergement.</span><span class="sxs-lookup"><span data-stu-id="552a5-111">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="552a5-112">Si vous utilisez un client de programme pour les développeurs M365, utilisez le compte d’administrateur que vous avez créé lorsque vous vous êtes inscrit au programme.</span><span class="sxs-lookup"><span data-stu-id="552a5-112">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="552a5-113">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="552a5-113">Create your project</span></span>

<span data-ttu-id="552a5-114">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="552a5-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="552a5-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="552a5-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="552a5-116">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="552a5-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="552a5-117">Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :</span><span class="sxs-lookup"><span data-stu-id="552a5-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="552a5-119">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="552a5-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="552a5-121">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="552a5-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="552a5-123">À l’étape **Sélectionner les fonctionnalités**, la fonctionnalité **Onglet** est déjà sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="552a5-123">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="552a5-124">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="552a5-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="552a5-126">Dans **l’étape du type d’hébergement** frontal, **sélectionnez SharePoint Framework (SPFx).**</span><span class="sxs-lookup"><span data-stu-id="552a5-126">On the **Frontend hosting type** step, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. <span data-ttu-id="552a5-128">Dans **l’étape Framework,** **sélectionnez React**.</span><span class="sxs-lookup"><span data-stu-id="552a5-128">On the **Framework** step, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Select Framework":::

1. <span data-ttu-id="552a5-130">Lorsque vous avez demandé un **nom de partie Webpart,** **appuyez sur Entrée** pour accepter la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="552a5-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="552a5-131">Lorsque vous avez demandé la **description du site WebPart,** **appuyez sur Entrée** pour accepter la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="552a5-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="552a5-132">Lorsque vous avez demandé le **langage de programmation,** **appuyez sur Entrée** pour accepter la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="552a5-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="552a5-133">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="552a5-133">Select a workspace folder.</span></span>  <span data-ttu-id="552a5-134">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="552a5-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="552a5-135">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="552a5-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="552a5-136">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="552a5-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="552a5-137">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="552a5-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="552a5-138">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="552a5-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="552a5-139">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="552a5-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="552a5-140">Utilisez le CLI `teamsfx` pou créer votre premier projet.</span><span class="sxs-lookup"><span data-stu-id="552a5-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="552a5-141">Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="552a5-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="552a5-142">Le CLI parcourt quelques questions pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="552a5-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="552a5-143">Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).</span><span class="sxs-lookup"><span data-stu-id="552a5-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="552a5-144">Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="552a5-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="552a5-145">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="552a5-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="552a5-146">Choisissez la fonctionnalité **Onglet**.</span><span class="sxs-lookup"><span data-stu-id="552a5-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="552a5-147">Sélectionnez **SharePoint Framework (SPFx)** frontal.</span><span class="sxs-lookup"><span data-stu-id="552a5-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="552a5-148">Sélectionnez **React** framework.</span><span class="sxs-lookup"><span data-stu-id="552a5-148">Select **React** framework.</span></span>
1. <span data-ttu-id="552a5-149">Appuyez **sur Entrée** pour le nom **du webpart.**</span><span class="sxs-lookup"><span data-stu-id="552a5-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="552a5-150">Appuyez **sur Entrée** pour obtenir **la description du site WebPart.**</span><span class="sxs-lookup"><span data-stu-id="552a5-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="552a5-151">Appuyez **sur Entrée** pour le langage **de programmation.**</span><span class="sxs-lookup"><span data-stu-id="552a5-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="552a5-152">Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.</span><span class="sxs-lookup"><span data-stu-id="552a5-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="552a5-153">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="552a5-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="552a5-154">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="552a5-154">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="552a5-155">Une fois toutes les questions répondues, votre projet est créé.</span><span class="sxs-lookup"><span data-stu-id="552a5-155">Once all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="552a5-156">En savoir plus sur le développement pour SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="552a5-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="552a5-157">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="552a5-157">Take a tour of the source code</span></span>

<span data-ttu-id="552a5-158">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="552a5-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="552a5-159">Une fois Teams Shared Computer Toolkit votre projet, vous avez les composants pour créer une application personnelle de base pour Teams hébergée dans le SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="552a5-159">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="552a5-160">Les répertoires et les fichiers du projet s'affichent dans la zone Explorateur de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="552a5-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Capture d’écran présentant les fichiers projet d’application pour une application personnelle dans Visual Studio Code.":::

<span data-ttu-id="552a5-162">Le Kit de ressources crée automatiquement une structure pour vous dans le répertoire du projet en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="552a5-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="552a5-163">Le Kit de ressources Teams conserve son état pour votre application dans le répertoire `.fx`.</span><span class="sxs-lookup"><span data-stu-id="552a5-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="552a5-164">Parmi les autres éléments de ce répertoire :</span><span class="sxs-lookup"><span data-stu-id="552a5-164">Among other items in this directory:</span></span>

- <span data-ttu-id="552a5-165">Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="552a5-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="552a5-166">Le manifeste de l’application pour la publication sur le Portail Teams est stocké dans `manifest.source.json` .</span><span class="sxs-lookup"><span data-stu-id="552a5-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="552a5-167">Les paramètres que vous avez choisis lors de la création du projet sont stockés dans `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="552a5-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="552a5-168">Étant donné que vous avez sélectionné un SPFx webpart, les fichiers suivants sont pertinents pour votre interface utilisateur :</span><span class="sxs-lookup"><span data-stu-id="552a5-168">Since you selected a SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="552a5-169">Le dossier `SPFx/src/webparts/{webpart}` contient votre SPFx webpart.</span><span class="sxs-lookup"><span data-stu-id="552a5-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="552a5-170">Le fichier `.vscode/launch.json` décrit les configurations de débogage disponibles dans la palette de débogage.</span><span class="sxs-lookup"><span data-stu-id="552a5-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="552a5-171">Pour plus d’informations SharePoint webparts pour Teams, reportez-vous [à la documentation SharePoint.](/sharepoint/dev/spfx/build-for-teams-overview)</span><span class="sxs-lookup"><span data-stu-id="552a5-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="552a5-172">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="552a5-172">Run your app locally</span></span>

<span data-ttu-id="552a5-173">Teams Shared Computer Toolkit vous permet d’héberger votre application localement et de l’exécuter via [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span><span class="sxs-lookup"><span data-stu-id="552a5-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="552a5-174">Générez et exécutez votre application localement dans Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="552a5-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="552a5-175">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="552a5-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="552a5-176">À partir Visual Studio Code, appuyez **sur F5**.</span><span class="sxs-lookup"><span data-stu-id="552a5-176">From Visual Studio Code, press **F5**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="Capture d’écran montrant comment démarrer une application SPFx dans un workbench local.":::

   > [!NOTE]
   > <span data-ttu-id="552a5-178">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="552a5-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="552a5-179">Une fenêtre de navigateur s’ouvre et charge automatiquement SharePoint Workbench une fois la build terminée.</span><span class="sxs-lookup"><span data-stu-id="552a5-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="552a5-180">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="552a5-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="552a5-181">Une fois que SharePoint Workbench est chargé.</span><span class="sxs-lookup"><span data-stu-id="552a5-181">Once the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="552a5-182">Le Kit de ressources vous invite à installer un certificat local si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="552a5-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="552a5-183">Ce certificat permet à Teams de charger votre application à partir de `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="552a5-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="552a5-184">Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="552a5-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. <span data-ttu-id="552a5-186">Appuyez sur **l’une des** icônes Ajouter un webpart (+) pour ajouter votre webpart.</span><span class="sxs-lookup"><span data-stu-id="552a5-186">Press one of the **Add Webpart** (+) icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart showing.":::

1. <span data-ttu-id="552a5-188">Choisissez votre webpart dans le menu.</span><span class="sxs-lookup"><span data-stu-id="552a5-188">Choose your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart selection.":::

<span data-ttu-id="552a5-190">Votre application doit maintenant être en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="552a5-190">Your app should now be running.</span></span>  <span data-ttu-id="552a5-191">Vous pouvez faire des activités de débogage normales comme s’il s’SPFx un autre SPFx webpart (par exemple, la définition de points d’arrêt).</span><span class="sxs-lookup"><span data-stu-id="552a5-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

> [!TIP]
> <span data-ttu-id="552a5-192">Essayez de placer des points d’arrêt dans la méthode de rendu et de `SPFx/src/webparts/{webpart}/{webpart}.ts` recharger la fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="552a5-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="552a5-193">VS Code s’arrête sur les points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="552a5-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="552a5-194">Déployer votre application sur SharePoint</span><span class="sxs-lookup"><span data-stu-id="552a5-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="552a5-195">Assurez-vous qu SharePoint catalogue d’applications existant dans votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="552a5-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="552a5-196">S’il n’en existe pas, [créez-en un.](/sharepoint/use-app-catalog)</span><span class="sxs-lookup"><span data-stu-id="552a5-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="552a5-197">La création complète du catalogue d’applications peut prendre jusqu’à 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="552a5-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="552a5-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="552a5-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="552a5-199">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="552a5-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="552a5-200">Sélectionnez le Teams Shared Computer Toolkit la barre latérale en sélectionnant l’icône Teams côté.</span><span class="sxs-lookup"><span data-stu-id="552a5-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="552a5-201">Sélectionnez **Provision dans le cloud**.</span><span class="sxs-lookup"><span data-stu-id="552a5-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Capture d’écran montrant les commandes d’approvisionnement":::

1. <span data-ttu-id="552a5-203">Vous pouvez surveiller la progression en regardant les boîtes de dialogue dans le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="552a5-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="552a5-204">Après quelques secondes, vous verrez l’avis suivant :</span><span class="sxs-lookup"><span data-stu-id="552a5-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Capture d’écran montrant la boîte de dialogue de mise en service terminée.":::

1. <span data-ttu-id="552a5-206">Une fois l’approvisionnement terminé, **sélectionnez Déployer sur le cloud.**</span><span class="sxs-lookup"><span data-stu-id="552a5-206">Once provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="552a5-207">Actuellement, le déploiement automatisé n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="552a5-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="552a5-208">Une boîte de dialogue s’invite à créer et déployer manuellement.</span><span class="sxs-lookup"><span data-stu-id="552a5-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="552a5-209">Appuyez **sur Build SharePoint Package**.</span><span class="sxs-lookup"><span data-stu-id="552a5-209">Press **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="Capture d’écran de la boîte de dialogue Créer un package Sharepoint":::

# <a name="command-line"></a>[<span data-ttu-id="552a5-211">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="552a5-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="552a5-212">Dans la fenêtre de votre terminal :</span><span class="sxs-lookup"><span data-stu-id="552a5-212">In your terminal window:</span></span>

1. <span data-ttu-id="552a5-213">Exécutez `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="552a5-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="552a5-214">Vous pouvez être invité à vous connecter à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="552a5-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="552a5-215">Si nécessaire, vous serez invité à sélectionner un abonnement Azure à utiliser pour les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="552a5-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="552a5-216">Certaines ressources Azure sont toujours utilisées pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="552a5-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="552a5-217">Exécutez `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="552a5-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="552a5-218">Lorsque vous y sont invités, **sélectionnez Créer SharePoint package.**</span><span class="sxs-lookup"><span data-stu-id="552a5-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="552a5-219">Le package SharePoint est situé dans `SPFx/sharepoint/solution` votre projet.</span><span class="sxs-lookup"><span data-stu-id="552a5-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="552a5-220">Télécharger package à SharePoint :</span><span class="sxs-lookup"><span data-stu-id="552a5-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="552a5-221">Connectez-vous à la console d’administration M365, puis accédez au SharePoint d’application.</span><span class="sxs-lookup"><span data-stu-id="552a5-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   - <span data-ttu-id="552a5-222">Ouvrez `https://admin.microsoft.com/AdminPortal/Home` .</span><span class="sxs-lookup"><span data-stu-id="552a5-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   - <span data-ttu-id="552a5-223">Sous **Centres d’administration,** sélectionnez **SharePoint** centre d’administration.</span><span class="sxs-lookup"><span data-stu-id="552a5-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   - <span data-ttu-id="552a5-224">Sélectionnez **d’autres** fonctionnalités dans le menu de la barre latérale.</span><span class="sxs-lookup"><span data-stu-id="552a5-224">Select **More features** from the sidebar menu.</span></span>
   - <span data-ttu-id="552a5-225">Appuyez **sur Ouvrir** sous **Applications.**</span><span class="sxs-lookup"><span data-stu-id="552a5-225">Press **Open** under **Apps**.</span></span>
   - <span data-ttu-id="552a5-226">Sélectionnez **catalogue d’applications.**</span><span class="sxs-lookup"><span data-stu-id="552a5-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="552a5-227">Sélectionnez **Distribuer des applications pour SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="552a5-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="Distribuer des applications pour SharePoint.":::

1. <span data-ttu-id="552a5-229">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="552a5-229">Select **Upload**.</span></span>

1. <span data-ttu-id="552a5-230">Appuyez **sur Choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="552a5-230">Press **Choose File**.</span></span>

1. <span data-ttu-id="552a5-231">Recherchez `{project}.sppkg` votre fichier, situé dans le `SPFx/sharepoint/solution` dossier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="552a5-231">Locate your `{project}.sppkg` file, located in the `SPFx/sharepoint/solution` folder within your project.</span></span>  <span data-ttu-id="552a5-232">Appuyez **sur Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="552a5-232">Press **Open**.</span></span>

1. <span data-ttu-id="552a5-233">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="552a5-233">Press **OK**.</span></span>

1. <span data-ttu-id="552a5-234">Le SharePoint de déploiement démarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="552a5-234">The SharePoint deployment process will automatically start.</span></span>  <span data-ttu-id="552a5-235">**Assurez-vous que la vérification de la mise** à disposition de cette solution pour tous les sites de l’organisation est vérifiée, puis appuyez sur **Déployer.**</span><span class="sxs-lookup"><span data-stu-id="552a5-235">Ensure **Make this solution available to all sites in the organization** is checked, then press **Deploy**.</span></span>

1. <span data-ttu-id="552a5-236">Sélectionnez **l’onglet** FICHIERS.</span><span class="sxs-lookup"><span data-stu-id="552a5-236">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="Sélectionnez l’onglet Fichiers dans SharePoint catalogue d’applications.":::

1. <span data-ttu-id="552a5-238">sélectionnez le package que vous avez déployé, puis appuyez sur **Synchroniser Teams** dans le ruban.</span><span class="sxs-lookup"><span data-stu-id="552a5-238">select the package you deployed, then press **Sync to Teams** in the ribbon.</span></span>

    > [!Note]
    > <span data-ttu-id="552a5-239">La synchronisation avec Teams processus peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="552a5-239">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="552a5-240">Un message s’affiche sur le côté droit du navigateur indiquant que l’application a été correctement synchronisée avec Teams.</span><span class="sxs-lookup"><span data-stu-id="552a5-240">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

<span data-ttu-id="552a5-241">Ouvrez l Teams application (ou connectez-vous sur `https://teams.microsoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="552a5-241">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="552a5-242">Appuyez sur le point triple sur la barre latérale, puis sélectionnez **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="552a5-242">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="552a5-243">L’application sera placée dans la catégorie **Applications conçues pour votre** organisation.</span><span class="sxs-lookup"><span data-stu-id="552a5-243">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="552a5-244">Vous pouvez ajouter l’application à partir de là.</span><span class="sxs-lookup"><span data-stu-id="552a5-244">You can add the app from there.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="Capture d’écran montrant l’application dans Teams":::

## <a name="see-also"></a><span data-ttu-id="552a5-246">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="552a5-246">See also</span></span>

- [<span data-ttu-id="552a5-247">Créer une application Teams à l’aide de React</span><span class="sxs-lookup"><span data-stu-id="552a5-247">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="552a5-248">Créer une application Teams à l’aide de Blazor</span><span class="sxs-lookup"><span data-stu-id="552a5-248">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="552a5-249">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="552a5-249">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="552a5-250">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="552a5-250">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="552a5-251">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="552a5-251">Create a conversational bot app</span></span>](first-app-bot.md)
