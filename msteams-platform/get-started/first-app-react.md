---
title: Prise en main :cCréez votre première application Teams avec React
author: adrianhall
description: Créez rapidement une application Microsoft Teams qui affiche un message « Hello, World ! » message à l’aide du Kit de ressources Microsoft Teams et de React.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: c257bcd805a6b7b38ab657cb31cad961df1c4704
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254320"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="e88b4-104">Créer et exécuter votre première application Microsoft Teams avec React</span><span class="sxs-lookup"><span data-stu-id="e88b4-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="e88b4-105">Dans ce didacticiel, vous allez apprendre à créer une application Microsoft Teams dans React qui implémente une application personnelle simple pour tirer des informations du microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e88b4-105">In this tutorial, you will learn how to create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="e88b4-106">Par exemple, une *application personnelle inclut* un ensemble d’onglets pour une utilisation individuelle.</span><span class="sxs-lookup"><span data-stu-id="e88b4-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="e88b4-107">Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment exécuter une application localement et comment déployer l’application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e88b4-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="e88b4-108">L'application créée affiche des informations de base sur l'utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="e88b4-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="e88b4-109">Lorsque l'autorisation est accordée, l'application se connecte au Microsoft Graph en tant qu'utilisateur actuel pour obtenir le profil complet.</span><span class="sxs-lookup"><span data-stu-id="e88b4-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e88b4-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e88b4-110">Before you begin</span></span>

<span data-ttu-id="e88b4-111">Assurez-vous que votre environnement de développement est installé en installant les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="e88b4-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e88b4-112">Installer les composants prérequis</span><span class="sxs-lookup"><span data-stu-id="e88b4-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="e88b4-113">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="e88b4-113">Create your project</span></span>

<span data-ttu-id="e88b4-114">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="e88b4-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e88b4-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e88b4-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e88b4-116">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e88b4-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="e88b4-117">Ouvrez le Teams Shared Computer Toolkit et sélectionnez l’icône Teams dans la barre latérale :</span><span class="sxs-lookup"><span data-stu-id="e88b4-117">Open the Teams Toolkit and select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="e88b4-119">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="e88b4-121">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="e88b4-123">Dans la section **Sélectionner des fonctionnalités,** sélectionnez **l’onglet** sélectionné, puis sélectionnez **OK.**</span><span class="sxs-lookup"><span data-stu-id="e88b4-123">In the **Select capabilities** section, varify that **Tab** is selected and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="e88b4-125">Dans la section **Type d’hébergement frontal,** sélectionnez **Azure.**</span><span class="sxs-lookup"><span data-stu-id="e88b4-125">In the **Frontend hosting type** section, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. <span data-ttu-id="e88b4-127">Dans la section **Ressources cloud,** sélectionnez **OK.**</span><span class="sxs-lookup"><span data-stu-id="e88b4-127">In the **Cloud resources** section, select **OK**.</span></span>  <span data-ttu-id="e88b4-128">Nous n’avons pas besoin de ressources cloud supplémentaires pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e88b4-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Capture d’écran présentant comment ajouter des ressources cloud à votre nouvelle application.":::

1. <span data-ttu-id="e88b4-130">Dans la section **Langage de** programmation, **sélectionnez JavaScript.**</span><span class="sxs-lookup"><span data-stu-id="e88b4-130">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. <span data-ttu-id="e88b4-132">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="e88b4-132">Select a workspace folder.</span></span> <span data-ttu-id="e88b4-133">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="e88b4-133">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="e88b4-134">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-134">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="e88b4-135">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="e88b4-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="e88b4-136">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="e88b4-136">Press **Enter** to continue.</span></span>

   <span data-ttu-id="e88b4-137">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="e88b4-137">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="e88b4-138">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e88b4-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="e88b4-139">Utilisez le CLI `teamsfx` pou créer votre premier projet.</span><span class="sxs-lookup"><span data-stu-id="e88b4-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="e88b4-140">Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="e88b4-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="e88b4-141">Le CLI parcourt quelques questions pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="e88b4-141">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="e88b4-142">Chaque question vous indique comment y répondre, par exemple, utilisez des touches de direction pour sélectionner une option.</span><span class="sxs-lookup"><span data-stu-id="e88b4-142">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="e88b4-143">Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="e88b4-144">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="e88b4-145">Sélectionnez la **fonctionnalité Onglet.**</span><span class="sxs-lookup"><span data-stu-id="e88b4-145">Select the **Tab** capability.</span></span>
1. <span data-ttu-id="e88b4-146">Sélectionnez l'hébergement frontal **Azure**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-146">Select **Azure** frontend hosting.</span></span> <span data-ttu-id="e88b4-147">Ne sélectionnez aucune ressource cloud.</span><span class="sxs-lookup"><span data-stu-id="e88b4-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="e88b4-148">Sélectionnez **JavaScript** comme langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="e88b4-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="e88b4-149">Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.</span><span class="sxs-lookup"><span data-stu-id="e88b4-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="e88b4-150">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="e88b4-151">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="e88b4-151">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="e88b4-152">Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.</span><span class="sxs-lookup"><span data-stu-id="e88b4-152">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="e88b4-153">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="e88b4-153">Take a tour of the source code</span></span>

<span data-ttu-id="e88b4-154">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="e88b4-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="e88b4-155">Une fois Teams Shared Computer Toolkit votre projet, vous avez les composants pour créer une application personnelle de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="e88b4-155">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="e88b4-156">Les répertoires et les fichiers du projet s'affichent dans la zone Explorateur de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e88b4-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Capture d’écran présentant les fichiers projet d’application pour une application personnelle dans Visual Studio Code.":::

<span data-ttu-id="e88b4-158">Le Kit de ressources crée automatiquement une structure pour vous dans le répertoire du projet en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="e88b4-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="e88b4-159">Le Kit de ressources Teams conserve son état pour votre application dans le répertoire `.fx`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="e88b4-160">Parmi les autres éléments de ce répertoire :</span><span class="sxs-lookup"><span data-stu-id="e88b4-160">Among other items in this directory:</span></span>

- <span data-ttu-id="e88b4-161">Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="e88b4-162">Le manifeste de l'application pour la publication sur le portail des développeurs pour Teams est stocké dans `manifest.source.json`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="e88b4-163">Les paramètres que vous avez choisis lors de la création du projet sont stockés dans `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="e88b4-164">Comme vous avez sélectionné la fonctionnalité d’onglet lors de l’installation, le Kit de ressources Teams génère automatiquement tout le code nécessaire pour un onglet de base dans le répertoire `tabs`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="e88b4-165">Ce répertoire contient plusieurs fichiers importants :</span><span class="sxs-lookup"><span data-stu-id="e88b4-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="e88b4-166">`tabs/src/index.jsx` est le point d’entrée de l’application frontale, où le composant principal `App` est rendu avec `ReactDOM.render()`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="e88b4-167">`tabs/src/components/App.jsx` gère le routage d’URL dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="e88b4-168">Il appelle le [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir une communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="e88b4-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="e88b4-169">`tabs/src/components/Tab.jsx` contient le code pour implémenter l’interface utilisateur de votre application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="e88b4-170">`tabs/src/components/TabConfig.jsx` contient le code pour implémenter l’interface utilisateur qui configure votre application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="e88b4-171">Plusieurs onglets sont requis par le runtime Teams, notamment l’avis de confidentialité, les conditions d’utilisation et les onglets de configuration.</span><span class="sxs-lookup"><span data-stu-id="e88b4-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="e88b4-172">Le code de l’avis de confidentialité et des conditions d’utilisation se trouve dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="e88b4-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="e88b4-173">Lorsque vous ajoutez des fonctionnalités cloud, des répertoires supplémentaires sont ajoutés au projet.</span><span class="sxs-lookup"><span data-stu-id="e88b4-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="e88b4-174">Plus particulièrement, le répertoire `api` contient le code de tout Azure Functions que vous écrivez.</span><span class="sxs-lookup"><span data-stu-id="e88b4-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="e88b4-175">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="e88b4-175">Run your app locally</span></span>

<span data-ttu-id="e88b4-176">Le Kit de ressources Teams vous permet d’exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="e88b4-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="e88b4-177">Il s’agit de plusieurs parties nécessaires pour fournir l’infrastructure correcte attendue par Teams :</span><span class="sxs-lookup"><span data-stu-id="e88b4-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="e88b4-178">Une application est inscrite auprès de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e88b4-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="e88b4-179">Cette application dispose d’autorisations associées à l’emplacement à partir duquel l’application est chargée et aux ressources principales auxquelles elle accède.</span><span class="sxs-lookup"><span data-stu-id="e88b4-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="e88b4-180">Une API web est hébergée pour faciliter les tâches d’authentification, en agissant comme un proxy entre l’application et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e88b4-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="e88b4-181">Cette opération est exécutée par Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="e88b4-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="e88b4-182">Il est accessible à l’URL `https://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="e88b4-183">Les ressources HTML, CSS et JavaScript qui composent le serveur frontal de l’application sont hébergées sur un service local.</span><span class="sxs-lookup"><span data-stu-id="e88b4-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="e88b4-184">Il est accessible à `https://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="e88b4-185">Un manifeste d'application est généré et existe dans le portail des développeurs pour Teams.</span><span class="sxs-lookup"><span data-stu-id="e88b4-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="e88b4-186">Teams utilise le manifeste de l’application pour indiquer aux clients connectés où charger l’application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="e88b4-187">Une fois cette demande effectuée, l’application peut être chargée dans le client Teams client.</span><span class="sxs-lookup"><span data-stu-id="e88b4-187">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="e88b4-188">Nous utilisons le client web Teams pour voir le code HTML, CSS et JavaScript dans un environnement de développement web standard.</span><span class="sxs-lookup"><span data-stu-id="e88b4-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="e88b4-189">Générez et exécutez votre application localement dans Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e88b4-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="e88b4-190">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="e88b4-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="e88b4-191">À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.</span><span class="sxs-lookup"><span data-stu-id="e88b4-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="e88b4-192">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="e88b4-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="e88b4-193">Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="e88b4-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="e88b4-194">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="e88b4-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="e88b4-195">Le Shared Computer Toolkit vous invite à installer un certificat local si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e88b4-195">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="e88b4-196">Ce certificat permet à Teams de charger votre application à partir de `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e88b4-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="e88b4-197">Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="e88b4-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. <span data-ttu-id="e88b4-199">Votre navigateur web commence à exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-199">Your web browser starts to run the app.</span></span> <span data-ttu-id="e88b4-200">Si vous êtes invité à ouvrir Teams bureau, sélectionnez **Annuler** pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="e88b4-200">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="e88b4-201">Vous pouvez également être invité à basculer vers Teams bureau à d’autres moments ; sélectionnez l Teams’application web lorsque cela se produit.</span><span class="sxs-lookup"><span data-stu-id="e88b4-201">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. <span data-ttu-id="e88b4-203">Connectez-vous à l’invite avec votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="e88b4-203">Sign in with your M365 account when prompted.</span></span>
1. <span data-ttu-id="e88b4-204">Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-204">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="e88b4-205">Votre application s’affiche désormais :</span><span class="sxs-lookup"><span data-stu-id="e88b4-205">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Capture d’écran de l’application terminée":::

<span data-ttu-id="e88b4-207">Vous pouvez faire des activités de débogage normales comme s’il s’avait été une autre application web, telle que la définition de points d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="e88b4-207">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="e88b4-208">L’application prend en charge le rechargement à chaud.</span><span class="sxs-lookup"><span data-stu-id="e88b4-208">The app supports hot reloading.</span></span> <span data-ttu-id="e88b4-209">Si vous modifiez un fichier dans le projet, la page est rechargée.</span><span class="sxs-lookup"><span data-stu-id="e88b4-209">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="e88b4-210">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="e88b4-210">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="e88b4-211">Lorsque vous appuyez sur **la touche F5,** le Teams Shared Computer Toolkit :</span><span class="sxs-lookup"><span data-stu-id="e88b4-211">When you press the **F5** key, the Teams Toolkit:</span></span>

* <span data-ttu-id="e88b4-212">Inscrit votre application avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e88b4-212">Registers your application with Azure Active Directory.</span></span>
* <span data-ttu-id="e88b4-213">*Charge une version de version* Teams.</span><span class="sxs-lookup"><span data-stu-id="e88b4-213">*Sideloads* your app in Teams.</span></span>
* <span data-ttu-id="e88b4-214">Démarre le système principal de votre application en cours d’exécution localement à [l’aide des outils Azure Function Core](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="e88b4-214">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
* <span data-ttu-id="e88b4-215">Démarre votre application frontale hébergée localement.</span><span class="sxs-lookup"><span data-stu-id="e88b4-215">Starts your application front-end hosted locally.</span></span>
* <span data-ttu-id="e88b4-216">Démarre Microsoft Teams dans un navigateur web avec une commande pour indiquer Teams charger l’application de côté à partir `https://localhost:3000/tab` de .</span><span class="sxs-lookup"><span data-stu-id="e88b4-216">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="e88b4-217">Il s’agit de l’URL inscrite dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-217">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="e88b4-218">Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="e88b4-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="e88b4-219">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte Teams qui permet le chargement de version test d’une application.</span><span class="sxs-lookup"><span data-stu-id="e88b4-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="e88b4-220">Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="e88b4-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="e88b4-221">Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</span><span class="sxs-lookup"><span data-stu-id="e88b4-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="e88b4-222">Avant le déploiement, l’application s’est exécutée localement :</span><span class="sxs-lookup"><span data-stu-id="e88b4-222">Before deployment, the application has been running locally:</span></span>

* <span data-ttu-id="e88b4-223">Le serveur principal s’exécute en utilisant **Azure Functions Core Tools**.</span><span class="sxs-lookup"><span data-stu-id="e88b4-223">The backend runs using **Azure Functions Core Tools**.</span></span>
* <span data-ttu-id="e88b4-224">Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.</span><span class="sxs-lookup"><span data-stu-id="e88b4-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="e88b4-225">Le déploiement implique l’approvisionnement de ressources sur un abonnement Azure actif et le déploiement ou le chargement du code frontal et frontal de l’application vers Azure.</span><span class="sxs-lookup"><span data-stu-id="e88b4-225">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

* <span data-ttu-id="e88b4-226">Le système back-end, s’il est configuré, utilise divers services Azure, notamment Azure App Service et stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e88b4-226">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
* <span data-ttu-id="e88b4-227">L’application frontale sera déployée sur un compte de stockage Azure configuré pour l’hébergement web statique.</span><span class="sxs-lookup"><span data-stu-id="e88b4-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="e88b4-228">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e88b4-228">See also</span></span>

* [<span data-ttu-id="e88b4-229">Présentation des didacticiels</span><span class="sxs-lookup"><span data-stu-id="e88b4-229">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="e88b4-230">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="e88b4-230">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="e88b4-231">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="e88b4-231">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="e88b4-232">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="e88b4-232">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
