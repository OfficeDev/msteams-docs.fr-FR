---
title: Prise en main :cCréez votre première application Teams avec React
author: adrianhall
description: Créez rapidement une application Microsoft Teams qui affiche un message « Hello, World ! » message à l’aide du Kit de ressources Microsoft Teams et de React.
ms.author: adhal
ms.date: 05/18/2021
ms.topic: quickstart
ms.openlocfilehash: 4560e332834fec7b681a6b2babf3e881b5e472f7
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698140"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="476be-104">Créer et exécuter votre première application Microsoft Teams avec React</span><span class="sxs-lookup"><span data-stu-id="476be-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="476be-105">Dans ce didacticiel, vous allez créer une application Microsoft Teams dans React qui implémente une application personnelle simple pour extraire des informations du Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="476be-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="476be-106">(Une *application personnelle* inclut un ensemble d’onglets délimités pour une utilisation individuelle.) Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment exécuter une application localement et comment déployer l’application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="476be-106">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="476be-107">L'application créée affiche des informations de base sur l'utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="476be-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="476be-108">Lorsque l'autorisation est accordée, l'application se connecte au Microsoft Graph en tant qu'utilisateur actuel pour obtenir le profil complet.</span><span class="sxs-lookup"><span data-stu-id="476be-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="476be-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="476be-109">Before you begin</span></span>

<span data-ttu-id="476be-110">Vérifiez que votre environnement de développement est configuré en installant les [Conditions préalables](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="476be-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="476be-111">Installer les composants prérequis</span><span class="sxs-lookup"><span data-stu-id="476be-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="476be-112">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="476be-112">Create your project</span></span>

<span data-ttu-id="476be-113">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="476be-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="476be-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="476be-114">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="476be-115">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="476be-115">Open Visual Studio code.</span></span>
1. <span data-ttu-id="476be-116">Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :</span><span class="sxs-lookup"><span data-stu-id="476be-116">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="476be-118">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="476be-118">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="476be-120">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="476be-120">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="476be-122">À l’étape **Sélectionner les fonctionnalités**, la fonctionnalité **Onglet** est déjà sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="476be-122">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="476be-123">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="476be-123">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="476be-125">À l’étape **Type d’hébergement frontal**, sélectionnez **Azure**.</span><span class="sxs-lookup"><span data-stu-id="476be-125">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. <span data-ttu-id="476be-127">À l’étape **Ressources cloud**, appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="476be-127">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="476be-128">Nous n’avons pas besoin de ressources cloud supplémentaires pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="476be-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Capture d’écran présentant comment ajouter des ressources cloud à votre nouvelle application.":::

1. <span data-ttu-id="476be-130">À l’étape **Langage de programmation**, sélectionnez **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="476be-130">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. <span data-ttu-id="476be-132">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="476be-132">Select a workspace folder.</span></span>  <span data-ttu-id="476be-133">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="476be-133">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="476be-134">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="476be-134">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="476be-135">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="476be-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="476be-136">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="476be-136">Press **Enter** to continue.</span></span>

<span data-ttu-id="476be-137">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="476be-137">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="476be-138">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="476be-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="476be-139">Utilisez le CLI `teamsfx` pou créer votre premier projet.</span><span class="sxs-lookup"><span data-stu-id="476be-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="476be-140">Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="476be-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="476be-141">Le CLI parcourt quelques questions pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="476be-141">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="476be-142">Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).</span><span class="sxs-lookup"><span data-stu-id="476be-142">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="476be-143">Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="476be-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="476be-144">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="476be-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="476be-145">Choisissez la fonctionnalité **Onglet**.</span><span class="sxs-lookup"><span data-stu-id="476be-145">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="476be-146">Sélectionnez l'hébergement frontal **Azure**.</span><span class="sxs-lookup"><span data-stu-id="476be-146">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="476be-147">Ne sélectionnez aucune ressource cloud.</span><span class="sxs-lookup"><span data-stu-id="476be-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="476be-148">Sélectionnez **JavaScript** comme langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="476be-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="476be-149">Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.</span><span class="sxs-lookup"><span data-stu-id="476be-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="476be-150">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="476be-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="476be-151">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="476be-151">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="476be-152">Une fois toutes les questions répondues, votre projet est créé.</span><span class="sxs-lookup"><span data-stu-id="476be-152">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="476be-153">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="476be-153">Take a tour of the source code</span></span>

<span data-ttu-id="476be-154">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="476be-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="476be-155">Une fois que le Kit de ressources Teams a configuré votre projet, vous disposez des composants pour créer une application personnelle de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="476be-155">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="476be-156">Les répertoires et les fichiers du projet s'affichent dans la zone Explorateur de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="476be-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Capture d’écran présentant les fichiers projet d’application pour une application personnelle dans Visual Studio Code.":::

<span data-ttu-id="476be-158">Le Kit de ressources crée automatiquement une structure pour vous dans le répertoire du projet en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="476be-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="476be-159">Le Kit de ressources Teams conserve son état pour votre application dans le répertoire `.fx`.</span><span class="sxs-lookup"><span data-stu-id="476be-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="476be-160">Parmi les autres éléments de ce répertoire :</span><span class="sxs-lookup"><span data-stu-id="476be-160">Among other items in this directory:</span></span>

- <span data-ttu-id="476be-161">Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="476be-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="476be-162">Le manifeste de l'application pour la publication sur le portail des développeurs pour Teams est stocké dans `manifest.source.json`.</span><span class="sxs-lookup"><span data-stu-id="476be-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="476be-163">Les paramètres que vous avez choisis lors de la création du projet sont stockés dans `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="476be-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="476be-164">Comme vous avez sélectionné la fonctionnalité d’onglet lors de l’installation, le Kit de ressources Teams génère automatiquement tout le code nécessaire pour un onglet de base dans le répertoire `tabs`.</span><span class="sxs-lookup"><span data-stu-id="476be-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="476be-165">Ce répertoire contient plusieurs fichiers importants :</span><span class="sxs-lookup"><span data-stu-id="476be-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="476be-166">`tabs/src/index.jsx` est le point d’entrée de l’application frontale, où le composant principal `App` est rendu avec `ReactDOM.render()`.</span><span class="sxs-lookup"><span data-stu-id="476be-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="476be-167">`tabs/src/components/App.jsx` gère le routage d’URL dans votre application.</span><span class="sxs-lookup"><span data-stu-id="476be-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="476be-168">Il appelle le [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir une communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="476be-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="476be-169">`tabs/src/components/Tab.jsx` contient le code pour implémenter l’interface utilisateur de votre application.</span><span class="sxs-lookup"><span data-stu-id="476be-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="476be-170">`tabs/src/components/TabConfig.jsx` contient le code pour implémenter l’interface utilisateur qui configure votre application.</span><span class="sxs-lookup"><span data-stu-id="476be-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="476be-171">Plusieurs onglets sont requis par le runtime Teams, notamment l’avis de confidentialité, les conditions d’utilisation et les onglets de configuration.</span><span class="sxs-lookup"><span data-stu-id="476be-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="476be-172">Le code de l’avis de confidentialité et des conditions d’utilisation se trouve dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="476be-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="476be-173">Lorsque vous ajoutez des fonctionnalités cloud, des répertoires supplémentaires sont ajoutés au projet.</span><span class="sxs-lookup"><span data-stu-id="476be-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="476be-174">Plus particulièrement, le répertoire `api` contient le code de tout Azure Functions que vous écrivez.</span><span class="sxs-lookup"><span data-stu-id="476be-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="476be-175">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="476be-175">Run your app locally</span></span>

<span data-ttu-id="476be-176">Le Kit de ressources Teams vous permet d’exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="476be-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="476be-177">Il s’agit de plusieurs parties nécessaires pour fournir l’infrastructure correcte attendue par Teams :</span><span class="sxs-lookup"><span data-stu-id="476be-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="476be-178">Une application est inscrite auprès de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="476be-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="476be-179">Cette application dispose d’autorisations associées à l’emplacement à partir duquel l’application est chargée et aux ressources principales auxquelles elle accède.</span><span class="sxs-lookup"><span data-stu-id="476be-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="476be-180">Une API web est hébergée pour faciliter les tâches d’authentification, en agissant comme un proxy entre l’application et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="476be-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="476be-181">Cette opération est exécutée par Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="476be-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="476be-182">Il est accessible à l’URL `https://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="476be-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="476be-183">Les ressources HTML, CSS et JavaScript qui composent le serveur frontal de l’application sont hébergées sur un service local.</span><span class="sxs-lookup"><span data-stu-id="476be-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="476be-184">Il est accessible à `https://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="476be-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="476be-185">Un manifeste d'application est généré et existe dans le portail des développeurs pour Teams.</span><span class="sxs-lookup"><span data-stu-id="476be-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="476be-186">Teams utilise le manifeste de l’application pour indiquer aux clients connectés où charger l’application.</span><span class="sxs-lookup"><span data-stu-id="476be-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="476be-187">Une fois cette opération effectuée, l’application peut être chargée dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="476be-187">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="476be-188">Nous utilisons le client web Teams pour voir le code HTML, CSS et JavaScript dans un environnement de développement web standard.</span><span class="sxs-lookup"><span data-stu-id="476be-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

[!INCLUDE [Adjust your browser launch settings](~/includes/get-started/browser-private-launch.md)]

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="476be-189">Générez et exécutez votre application localement dans Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="476be-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="476be-190">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="476be-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="476be-191">À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.</span><span class="sxs-lookup"><span data-stu-id="476be-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="476be-192">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="476be-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="476be-193">Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="476be-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="476be-194">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="476be-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="476be-195">Le Kit de ressources vous invite à installer un certificat local si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="476be-195">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="476be-196">Ce certificat permet à Teams de charger votre application à partir de `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="476be-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="476be-197">Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="476be-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. <span data-ttu-id="476be-199">Votre navigateur web est lancé votre exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="476be-199">Your web browser is started to run the application.</span></span> <span data-ttu-id="476be-200">Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="476be-200">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="476be-201">Lorsque vous y êtes invité, sélectionnez **Utiliser l’application web à la place**.</span><span class="sxs-lookup"><span data-stu-id="476be-201">When prompted, select **Use the web app instead**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. <span data-ttu-id="476be-203">Vous serez peut-être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="476be-203">You may be prompted to sign in.</span></span>  <span data-ttu-id="476be-204">Dans ce cas, connectez-vous à l'aide de votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="476be-204">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="476be-205">Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="476be-205">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="476be-206">Votre application s’affiche désormais :</span><span class="sxs-lookup"><span data-stu-id="476be-206">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Capture d’écran de l’application terminée":::

<span data-ttu-id="476be-208">Vous pouvez effectuer des activités de débogage normales comme s’il s’agissait d’une autre application web (par exemple, définir des points d’arrêt).</span><span class="sxs-lookup"><span data-stu-id="476be-208">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="476be-209">L’application prend en charge le rechargement à chaud.</span><span class="sxs-lookup"><span data-stu-id="476be-209">The app supports hot reloading.</span></span>  <span data-ttu-id="476be-210">Si vous modifiez un fichier dans le projet, la page est rechargée.</span><span class="sxs-lookup"><span data-stu-id="476be-210">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="476be-211">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="476be-211">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="476be-212">Lorsque vous appuyez sur F5, le Kit de ressources Teams :</span><span class="sxs-lookup"><span data-stu-id="476be-212">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="476be-213">Votre application a été inscrite dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="476be-213">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="476be-214">*A chargés indépendamment* votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="476be-214">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="476be-215">A démarré votre serveur principal d’application s’exécutant localement en utilisant [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="476be-215">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="476be-216">Démarrage de votre application frontale hébergée localement.</span><span class="sxs-lookup"><span data-stu-id="476be-216">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="476be-217">Démarrage de Microsoft Teams dans un navigateur web avec une commande pour demander à Teams de charger l’application à partir de `https://localhost:3000/tab` (l’URL est inscrite dans le manifeste de l’application).</span><span class="sxs-lookup"><span data-stu-id="476be-217">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab` (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="476be-218">Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="476be-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="476be-219">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte Teams qui permet le chargement de version test d’une application.</span><span class="sxs-lookup"><span data-stu-id="476be-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="476be-220">Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="476be-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="476be-221">Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</span><span class="sxs-lookup"><span data-stu-id="476be-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="476be-222">Avant le déploiement, l’application s’est exécutée localement :</span><span class="sxs-lookup"><span data-stu-id="476be-222">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="476be-223">Le serveur principal s’exécute en utilisant _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="476be-223">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="476be-224">Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.</span><span class="sxs-lookup"><span data-stu-id="476be-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="476be-225">Le déploiement implique la mise en service de ressources sur un abonnement Azure actif et le déploiement (chargement) du code du serveur principal et du serveur frontal pour l’application vers Azure.</span><span class="sxs-lookup"><span data-stu-id="476be-225">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="476be-226">Le serveur principal (s'il est configuré) utilise une variété de services Azure, notamment Azure App Service et stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="476be-226">The backend (if configured) uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="476be-227">L’application frontale sera déployée sur un compte de stockage Azure configuré pour l’hébergement web statique.</span><span class="sxs-lookup"><span data-stu-id="476be-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="476be-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="476be-228">Next steps</span></span>

<span data-ttu-id="476be-229">Découvrez d’autres méthodes pour la création d’applications Teams :</span><span class="sxs-lookup"><span data-stu-id="476be-229">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="476be-230">Créer une application Teams à l’aide de Blazor</span><span class="sxs-lookup"><span data-stu-id="476be-230">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="476be-231">[Créer une application Teams en tant que composant WebPart SharePoint](first-app-spfx.md) (Azure non requis)</span><span class="sxs-lookup"><span data-stu-id="476be-231">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="476be-232">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="476be-232">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="476be-233">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="476be-233">Create a messaging extension</span></span>](first-message-extension.md)
