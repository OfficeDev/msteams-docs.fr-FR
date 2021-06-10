---
title: Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio Code l’aide Microsoft Teams Shared Computer Toolkit
keywords: kit de ressources teams Visual Studio Code
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bc97a78df5618c87dfc66fae179145acd749ad1f
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721821"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="1b479-104">Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1b479-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="1b479-105">La Teams Shared Computer Toolkit pour Visual Studio Code permet aux développeurs de créer et de déployer des applications Teams avec une identité intégrée, l’accès au stockage cloud, les données de Microsoft Graph et d’autres services dans Azure et M365 avec une approche « de configuration zéro » de l’expérience développeur.</span><span class="sxs-lookup"><span data-stu-id="1b479-105">The Teams Toolkit for Visual Studio Code helps developers create and deploy Teams apps with integrated identity, access to cloud storage, data from Microsoft Graph, and other services in Azure and M365 with a “zero-configuration” approach to the developer experience.</span></span>  

<span data-ttu-id="1b479-106">Vous pouvez également utiliser le kit de ressources avec Visual Studio ou en tant qu’CLI (appelé `teamsfx` ).</span><span class="sxs-lookup"><span data-stu-id="1b479-106">You also can use the toolkit with Visual Studio or as a CLI (called `teamsfx`).</span></span>

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="1b479-107">Installer le Teams Shared Computer Toolkit pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1b479-107">Install the Teams Toolkit for Visual Studio Code</span></span>

1. <span data-ttu-id="1b479-108">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1b479-108">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="1b479-109">Sélectionnez l’affichage Extensions (**Ctrl+Shift+X**  /  **⌘⇧-X** ou Afficher **> extensions**).</span><span class="sxs-lookup"><span data-stu-id="1b479-109">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="1b479-110">Dans la zone de recherche, entrez _Teams Shared Computer Toolkit_.</span><span class="sxs-lookup"><span data-stu-id="1b479-110">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="1b479-111">Sélectionnez le bouton d’installation vert en Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="1b479-111">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="1b479-112">Vous pouvez également trouver le Teams Shared Computer Toolkit sur le [Visual Studio Code Marketplace.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)</span><span class="sxs-lookup"><span data-stu-id="1b479-112">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="1b479-113">Les outils suivants sont installés par l’extension Visual Studio Code si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1b479-113">The following tools will be installed by the Visual Studio Code extension when they are needed.</span></span>  <span data-ttu-id="1b479-114">S’il est déjà installé, la version installée sera utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="1b479-114">If already installed, the installed version will be used instead.</span></span>  <span data-ttu-id="1b479-115">Si vous utilisez Linux (y compris WSL), vous devez installer ces outils avant d’utiliser :</span><span class="sxs-lookup"><span data-stu-id="1b479-115">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="1b479-116">Outils azure Functions Core</span><span class="sxs-lookup"><span data-stu-id="1b479-116">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="1b479-117">Azure Functions Core Tools permet d’exécuter localement tous les composants principaux lors d’une exécution de débogage locale, y compris les outils d’aide à l’authentification requis lors de l’exécution de vos services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1b479-117">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span>  <span data-ttu-id="1b479-118">Il est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="1b479-118">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="1b479-119">Kit de développement logiciel .NET</span><span class="sxs-lookup"><span data-stu-id="1b479-119">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="1b479-120">Le SDK .NET permet d’installer des liaisons personnalisées pour le débogage local et les déploiements d’applications Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1b479-120">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span>  <span data-ttu-id="1b479-121">Si vous n’avez pas installé le SDK .NET 3.1 (ou version ultérieure) globalement, la version portable sera installée.</span><span class="sxs-lookup"><span data-stu-id="1b479-121">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.</span></span>

- [<span data-ttu-id="1b479-122">ngrok</span><span class="sxs-lookup"><span data-stu-id="1b479-122">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="1b479-123">Certaines Teams d’application (bots de conversation, extensions de messagerie et webhooks entrants) nécessitent des connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="1b479-123">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="1b479-124">Vous devez exposer votre système de développement à la Teams via un tunnel.</span><span class="sxs-lookup"><span data-stu-id="1b479-124">You need to expose your development system to Teams through a tunnel.</span></span>  <span data-ttu-id="1b479-125">Un tunnel n’est pas requis pour les applications qui incluent uniquement des onglets.</span><span class="sxs-lookup"><span data-stu-id="1b479-125">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="1b479-126">Ce package est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="1b479-126">This package is installed within the project directory (using npm `devDependencies`).</span></span>

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="1b479-127">Utilisez la Teams Shared Computer Toolkit pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1b479-127">Use the Teams Toolkit for Visual Studio Code</span></span>

- [<span data-ttu-id="1b479-128">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="1b479-128">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="1b479-129">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="1b479-129">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="1b479-130">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="1b479-130">Run your app locally</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="1b479-131">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="1b479-131">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="1b479-132">Configurer un nouveau projet Teams projet</span><span class="sxs-lookup"><span data-stu-id="1b479-132">Set up a new Teams project</span></span>

<span data-ttu-id="1b479-133">Le Teams Shared Computer Toolkit peut créer des applications React qui seront hébergées dans Azure ou des composants Web SPFx qui seront hébergés sur votre environnement SharePoint M365.</span><span class="sxs-lookup"><span data-stu-id="1b479-133">The Teams Toolkit can create React apps that will be hosted in Azure or SPFx web parts that will be hosted on your M365 SharePoint environment.</span></span>  <span data-ttu-id="1b479-134">Pour créer une application React à héberger sur Azure :</span><span class="sxs-lookup"><span data-stu-id="1b479-134">To create a new React app to be hosted on Azure:</span></span>

1. <span data-ttu-id="1b479-135">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1b479-135">Open Visual Studio code.</span></span>
1. <span data-ttu-id="1b479-136">Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :</span><span class="sxs-lookup"><span data-stu-id="1b479-136">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="1b479-138">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="1b479-138">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="1b479-140">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="1b479-140">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="1b479-142">À l’étape **Sélectionner les fonctionnalités**, la fonctionnalité **Onglet** est déjà sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="1b479-142">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="1b479-143">Vous pouvez également  sélectionner bot et **extension de messagerie.**</span><span class="sxs-lookup"><span data-stu-id="1b479-143">You can also optionally select **Bot** and **Messaging Extension**.</span></span>  <span data-ttu-id="1b479-144">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b479-144">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="1b479-146">À l’étape **Type d’hébergement frontal**, sélectionnez **Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b479-146">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. <span data-ttu-id="1b479-148">(Facultatif) À **l’étape Ressources cloud,** sélectionnez les ressources cloud que votre application utilisera.</span><span class="sxs-lookup"><span data-stu-id="1b479-148">(Optional) On the **Cloud resources** step, select cloud resources that your application will use.</span></span>  <span data-ttu-id="1b479-149">Vous pouvez sélectionner l’accès CRUD (créer, lire, mettre à jour, supprimer) à une table SQL une API :</span><span class="sxs-lookup"><span data-stu-id="1b479-149">You can select CRUD (create, read, update, delete) access to a SQL table or an API:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Capture d’écran présentant comment ajouter des ressources cloud à votre nouvelle application.":::

1. <span data-ttu-id="1b479-151">À **l’étape Du langage de** programmation, vous pouvez choisir **JavaScript** ou **TypeScript**:</span><span class="sxs-lookup"><span data-stu-id="1b479-151">On the **Programming Language** step, you can choose **JavaScript** or **TypeScript**:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. <span data-ttu-id="1b479-153">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="1b479-153">Select a workspace folder.</span></span>  <span data-ttu-id="1b479-154">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="1b479-154">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="1b479-155">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="1b479-155">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="1b479-156">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="1b479-156">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="1b479-157">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="1b479-157">Press **Enter** to continue.</span></span>

<span data-ttu-id="1b479-158">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="1b479-158">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="1b479-159">L’application échafaudée contient du code pour gérer l' sign-on unique Azure Active Directory et l’accès au microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1b479-159">The scaffolded app contains code to handle single sign-on with Azure Active Directory and access to the Microsoft Graph.</span></span>  <span data-ttu-id="1b479-160">Si vous avez sélectionné des ressources Azure, le code de ces ressources sera également disponible.</span><span class="sxs-lookup"><span data-stu-id="1b479-160">If you selected Azure resources, then the code for those resources will also be available.</span></span>

<span data-ttu-id="1b479-161">Pour une procédure pas à pas du processus SPFx création et de publication, voir [le didacticiel SPFx de publication.](../get-started/first-app-spfx.md)</span><span class="sxs-lookup"><span data-stu-id="1b479-161">For a walk-through of the SPFx creation and publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="1b479-162">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="1b479-162">Configure your app</span></span>

<span data-ttu-id="1b479-163">L’application Teams principale englobe trois composants :</span><span class="sxs-lookup"><span data-stu-id="1b479-163">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="1b479-164">Le Microsoft Teams client (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="1b479-164">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="1b479-165">Serveur qui répond aux demandes de contenu qui s’afficheront dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1b479-165">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="1b479-166">Par exemple, le contenu d’onglet HTML ou une carte adaptative de bot.</span><span class="sxs-lookup"><span data-stu-id="1b479-166">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="1b479-167">Un package Teams’application se compose de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="1b479-167">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="1b479-168">Le manifest.jsest alors en cours.</span><span class="sxs-lookup"><span data-stu-id="1b479-168">The manifest.json.</span></span>
      > - <span data-ttu-id="1b479-169">Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="1b479-169">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="1b479-170">Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.</span><span class="sxs-lookup"><span data-stu-id="1b479-170">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="1b479-171">Le manifeste et les icônes sont stockés dans le dossier de votre projet avant d’être chargés `.fx` vers Teams.</span><span class="sxs-lookup"><span data-stu-id="1b479-171">The manifest and icons are stored in the `.fx` folder of your project prior to being uploaded to Teams.</span></span> <span data-ttu-id="1b479-172">Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="1b479-172">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="1b479-173">Pour configurer votre application, accédez à **l’onglet Teams Shared Computer Toolkit** dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1b479-173">To configure your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="1b479-174">Sélectionnez **l’Éditeur** de **manifeste dans Project** section.</span><span class="sxs-lookup"><span data-stu-id="1b479-174">Select **Manifest Editor** in the **Project** section.</span></span>

<span data-ttu-id="1b479-175">La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l’application.</span><span class="sxs-lookup"><span data-stu-id="1b479-175">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="1b479-176">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="1b479-176">Install and run your app locally</span></span>

<span data-ttu-id="1b479-177">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="1b479-177">To build and run your app locally:</span></span>

1. <span data-ttu-id="1b479-178">À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.</span><span class="sxs-lookup"><span data-stu-id="1b479-178">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="1b479-179">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="1b479-179">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="1b479-180">Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="1b479-180">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="1b479-181">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="1b479-181">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="1b479-182">Le kit de ressources vous invite à installer un certificat local si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1b479-182">The toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="1b479-183">Ce certificat permet à Teams de charger votre application à partir de `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="1b479-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="1b479-184">Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="1b479-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. <span data-ttu-id="1b479-186">Votre navigateur web est lancé votre exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="1b479-186">Your web browser is started to run the application.</span></span> <span data-ttu-id="1b479-187">Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="1b479-187">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="1b479-188">Vous pouvez également être invité à basculer vers l’application Teams à d’autres moments.</span><span class="sxs-lookup"><span data-stu-id="1b479-188">You may also be prompted to switch to the Teams application at other times.</span></span> <span data-ttu-id="1b479-189">Sélectionnez l’application web lorsque cela se produit.</span><span class="sxs-lookup"><span data-stu-id="1b479-189">Select the web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. <span data-ttu-id="1b479-191">Vous serez peut-être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="1b479-191">You may be prompted to sign in.</span></span>  <span data-ttu-id="1b479-192">Dans ce cas, connectez-vous à l'aide de votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="1b479-192">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="1b479-193">Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1b479-193">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="1b479-194">Le back-end et le frontend sont raccordés au débo Visual Studio Code débogger.</span><span class="sxs-lookup"><span data-stu-id="1b479-194">Both the backend and frontend are hooked into the Visual Studio Code debugger.</span></span>  <span data-ttu-id="1b479-195">Cela vous permet de définir des points d’arrêt n’importe où dans votre code et d’inspecter l’état.</span><span class="sxs-lookup"><span data-stu-id="1b479-195">This allows you to set breakpoints anywhere in your code and inspect state.</span></span>  <span data-ttu-id="1b479-196">Vous pouvez également utiliser n’importe quel outil de débogage frontal (tel que les outils React développeur) dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="1b479-196">You can also use any frontend debugging tools (such as the React Developer Tools) within the browser.</span></span>  <span data-ttu-id="1b479-197">Pour plus d’informations sur le débogage dans Visual Studio Code, [examinez la documentation.](https://code.visualstudio.com/Docs/editor/debugging)</span><span class="sxs-lookup"><span data-stu-id="1b479-197">For more information about debugging in Visual Studio Code, review [the documentation](https://code.visualstudio.com/Docs/editor/debugging).</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="1b479-198">Publier votre application sur Teams</span><span class="sxs-lookup"><span data-stu-id="1b479-198">Publish your app to Teams</span></span>

<span data-ttu-id="1b479-199">Avant de pouvoir être utilisé par d’autres personnes, vous devez publier votre application sur le portail de développement pour Teams.</span><span class="sxs-lookup"><span data-stu-id="1b479-199">Before it can be used by other people, you must publish your app to the Developer Portal for Teams.</span></span>

1. <span data-ttu-id="1b479-200">Pour publier votre application, accédez à **l’onglet Teams Shared Computer Toolkit** dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1b479-200">To publish your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="1b479-201">Sélectionnez **Publier à Teams** dans la section **Project** de publication.</span><span class="sxs-lookup"><span data-stu-id="1b479-201">Select **Publish to Teams** in the **Project** section.</span></span>

<span data-ttu-id="1b479-202">Si vous utilisez l’hébergement Azure, vous devez avoir mis en service et déployé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="1b479-202">If using Azure hosting, you must have provisioned and deployed to the cloud.</span></span> <span data-ttu-id="1b479-203">Pour une procédure pas à pas du processus SPFx publication, voir le [didacticiel SPFx de publication.](../get-started/first-app-spfx.md)</span><span class="sxs-lookup"><span data-stu-id="1b479-203">For a walk-through of the SPFx publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="1b479-204">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1b479-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b479-205">Maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="1b479-205">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
