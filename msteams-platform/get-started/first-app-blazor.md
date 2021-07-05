---
title: Get started - Build your first Teams app with Blazor
author: adrianhall
description: Créez rapidement une application Microsoft Teams qui affiche un message « Hello, World ! » à l’aide Microsoft Teams Shared Computer Toolkit et .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254306"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="84ec5-104">Créer et exécuter votre première application Microsoft Teams avec Blazor</span><span class="sxs-lookup"><span data-stu-id="84ec5-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="84ec5-105">Dans ce didacticiel, vous allez apprendre à créer une application Microsoft Teams dans .NET/Blazor qui implémente une application personnelle simple pour tirer des informations du microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="84ec5-105">In this tutorial, you will learn how to create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="84ec5-106">Par exemple, une *application personnelle inclut* un ensemble d’onglets pour une utilisation individuelle.</span><span class="sxs-lookup"><span data-stu-id="84ec5-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="84ec5-107">Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment exécuter une application localement et comment déployer l’application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="84ec5-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="84ec5-108">L'application créée affiche des informations de base sur l'utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="84ec5-108">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="84ec5-109">Lorsque l'autorisation est accordée, l'application se connecte au Microsoft Graph en tant qu'utilisateur actuel pour obtenir le profil complet.</span><span class="sxs-lookup"><span data-stu-id="84ec5-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="84ec5-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="84ec5-110">Before you begin</span></span>

<span data-ttu-id="84ec5-111">Assurez-vous que votre environnement de développement est installé en installant les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="84ec5-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="84ec5-112">Installer les composants prérequis</span><span class="sxs-lookup"><span data-stu-id="84ec5-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="84ec5-113">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="84ec5-113">Create your project</span></span>

<span data-ttu-id="84ec5-114">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="84ec5-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="84ec5-115">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="84ec5-115">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="84ec5-116">Ouvrez Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="84ec5-116">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="84ec5-117">Sélectionnez **Créer un projet.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-117">Select **Create a new project**.</span></span>

1. <span data-ttu-id="84ec5-118">Sélectionnez **Microsoft Teams application,** puis sélectionnez **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-118">Select **Microsoft Teams App**, then select **Next**.</span></span>  <span data-ttu-id="84ec5-119">Pour vous aider à trouver le modèle, utilisez le type de **projet Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-119">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="84ec5-120">Entrez un nom et sélectionnez **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-120">Enter a name and select **Next**.</span></span>

1. <span data-ttu-id="84ec5-121">Entrez le nom de l’application et le nom de la société.</span><span class="sxs-lookup"><span data-stu-id="84ec5-121">Enter the application name and company name.</span></span>

1. <span data-ttu-id="84ec5-122">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-122">Select **Create**.</span></span>  <span data-ttu-id="84ec5-123">Le nom de l’application et le nom de la société sont affichés pour vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="84ec5-123">The application name and company name are displayed to your end users.</span></span> <span data-ttu-id="84ec5-124">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="84ec5-124">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="84ec5-125">Une fois le projet créé, configurer l' sign-on unique avec M365 :</span><span class="sxs-lookup"><span data-stu-id="84ec5-125">After the project is created, set up single sign-on with M365:</span></span>

   1. <span data-ttu-id="84ec5-126">Sélectionnez **Project**  >  **TeamsFx**  >  **Configurer pour l' sso...**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-126">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   1. <span data-ttu-id="84ec5-127">Lorsque vous y invitez, connectez-vous à votre compte d’administrateur M365.</span><span class="sxs-lookup"><span data-stu-id="84ec5-127">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="84ec5-128">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="84ec5-128">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="84ec5-129">Ouvrez un Terminal et sélectionnez le répertoire dans lequel vous souhaitez créer le projet.</span><span class="sxs-lookup"><span data-stu-id="84ec5-129">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="84ec5-130">Exécutez `dotnet new -i` cette page pour installer le modèle à partir NuGet :</span><span class="sxs-lookup"><span data-stu-id="84ec5-130">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="84ec5-131">Vous ne devez le faire que la première fois ou lors de la mise à jour du modèle.</span><span class="sxs-lookup"><span data-stu-id="84ec5-131">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="84ec5-132">Vérifiez [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) la dernière version de ce package.</span><span class="sxs-lookup"><span data-stu-id="84ec5-132">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="84ec5-133">Créez un répertoire :</span><span class="sxs-lookup"><span data-stu-id="84ec5-133">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="84ec5-134">Exécutez `dotnet new` cette recherche pour créer un projet :</span><span class="sxs-lookup"><span data-stu-id="84ec5-134">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="84ec5-135">Après la mise en place de la échafaudage, configurez le projet pour Teams déploiement :</span><span class="sxs-lookup"><span data-stu-id="84ec5-135">After scaffolding, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

   <span data-ttu-id="84ec5-136">Vous pouvez maintenant ouvrir la solution dans Visual Studio débogage.</span><span class="sxs-lookup"><span data-stu-id="84ec5-136">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="84ec5-137">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="84ec5-137">Take a tour of the source code</span></span>

<span data-ttu-id="84ec5-138">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="84ec5-138">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="84ec5-139">Une fois Teams Shared Computer Toolkit votre projet, vous avez les composants pour créer une application personnelle de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="84ec5-139">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="84ec5-140">Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de solutions Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="84ec5-140">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour une application personnelle Visual Studio 2019.":::

- <span data-ttu-id="84ec5-142">Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png`.</span><span class="sxs-lookup"><span data-stu-id="84ec5-142">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="84ec5-143">Le manifeste de l’application pour la publication via le portail de développement pour Teams est stocké dans `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="84ec5-143">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="84ec5-144">Un contrôleur de serveur back-end est fourni pour `Controllers/BackendController.cs` faciliter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="84ec5-144">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="84ec5-145">Étant donné que vous avez créé une application d’onglet lors de l’installation, l’Teams Shared Computer Toolkit crée la modèle de tout le code nécessaire pour un onglet de base en tant que [serveur Blazor](/aspnet/core/blazor).</span><span class="sxs-lookup"><span data-stu-id="84ec5-145">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="84ec5-146">`Pages/Tab.razor` est le point d’entrée de l’application frontale.</span><span class="sxs-lookup"><span data-stu-id="84ec5-146">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="84ec5-147">`TeamsFx.cs`et `JS/src/index.js` sert à initialiser les communications avec l’Teams hôte.</span><span class="sxs-lookup"><span data-stu-id="84ec5-147">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="84ec5-148">Vous pouvez ajouter des fonctionnalités de back-end en ajoutant des contrôleurs ASP.NET Core supplémentaires à votre application.</span><span class="sxs-lookup"><span data-stu-id="84ec5-148">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="84ec5-149">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="84ec5-149">Run your app locally</span></span>

<span data-ttu-id="84ec5-150">Le Kit de ressources Teams vous permet d’exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="84ec5-150">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="84ec5-151">Il s’agit de plusieurs parties nécessaires pour fournir l’infrastructure correcte attendue par Teams :</span><span class="sxs-lookup"><span data-stu-id="84ec5-151">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="84ec5-152">Une application est inscrite auprès de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84ec5-152">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="84ec5-153">Cette application dispose d’autorisations associées à l’emplacement à partir duquel l’application est chargée et aux ressources principales auxquelles elle accède.</span><span class="sxs-lookup"><span data-stu-id="84ec5-153">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="84ec5-154">Une API web est hébergée (via IIS Express) pour faciliter les tâches d’authentification, agissant en tant que proxy entre l’application et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84ec5-154">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="84ec5-155">Un manifeste d'application est généré et existe dans le portail des développeurs pour Teams.</span><span class="sxs-lookup"><span data-stu-id="84ec5-155">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="84ec5-156">Teams utilise le manifeste de l’application pour indiquer aux clients connectés où charger l’application.</span><span class="sxs-lookup"><span data-stu-id="84ec5-156">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="84ec5-157">Une fois cette demande effectuée, l’application peut être chargée dans le client Teams client.</span><span class="sxs-lookup"><span data-stu-id="84ec5-157">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="84ec5-158">Nous utilisons le client web Teams pour voir le code HTML, CSS et JavaScript dans un environnement de développement web standard.</span><span class="sxs-lookup"><span data-stu-id="84ec5-158">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="84ec5-159">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="84ec5-159">To build and run your app locally:</span></span>


1. <span data-ttu-id="84ec5-160">À Visual Studio Code, appuyez sur la **touche F5** pour exécuter votre application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="84ec5-160">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>


1. <span data-ttu-id="84ec5-161">Si nécessaire, installez le certificat SSL auto-signé pour le débogage local.</span><span class="sxs-lookup"><span data-stu-id="84ec5-161">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. <span data-ttu-id="84ec5-163">Teams sera chargée dans un navigateur web et vous serez invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="84ec5-163">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="84ec5-164">Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="84ec5-164">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="84ec5-165">Connectez-vous à votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="84ec5-165">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="84ec5-166">Lorsque vous y invitez l’application sur Teams, sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-166">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="84ec5-167">Votre application s’affiche désormais :</span><span class="sxs-lookup"><span data-stu-id="84ec5-167">Your app will now be displayed:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Capture d’écran de l’application terminée":::

   <span data-ttu-id="84ec5-169">Vous pouvez effectuer les activités de débogage comme s’il s’était produit une autre application web telle que la définition de points d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="84ec5-169">You can perform the debugging activities as if this were any other web application like setting breakpoints.</span></span> <span data-ttu-id="84ec5-170">L’application prend en charge le rechargement à chaud.</span><span class="sxs-lookup"><span data-stu-id="84ec5-170">The app supports hot reloading.</span></span>  <span data-ttu-id="84ec5-171">Si vous modifiez un fichier dans le projet, la page est rechargée.</span><span class="sxs-lookup"><span data-stu-id="84ec5-171">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="84ec5-172">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="84ec5-172">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="84ec5-173">Lorsque vous appuyez sur **la touche F5,** le Teams Shared Computer Toolkit :</span><span class="sxs-lookup"><span data-stu-id="84ec5-173">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="84ec5-174">Inscrit votre application avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84ec5-174">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="84ec5-175">Inscrit votre application pour le « chargement de version latéral » dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="84ec5-175">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="84ec5-176">Démarre le back-end de votre application en cours d’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="84ec5-176">Starts your application backend running locally.</span></span>
1. <span data-ttu-id="84ec5-177">Démarre votre application frontale hébergée localement.</span><span class="sxs-lookup"><span data-stu-id="84ec5-177">Starts your application front-end hosted locally.</span></span>
1. <span data-ttu-id="84ec5-178">Démarre Microsoft Teams dans un navigateur web avec une commande pour demander Teams charger l’application de côté (l’URL est enregistrée dans le manifeste de l’application).</span><span class="sxs-lookup"><span data-stu-id="84ec5-178">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="84ec5-179">Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="84ec5-179">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="84ec5-180">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement côté application.</span><span class="sxs-lookup"><span data-stu-id="84ec5-180">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="84ec5-181">Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="84ec5-181">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="84ec5-182">Déployer votre application sur Azure</span><span class="sxs-lookup"><span data-stu-id="84ec5-182">Deploy your app to Azure</span></span>

<span data-ttu-id="84ec5-183">Le déploiement se compose de deux étapes :</span><span class="sxs-lookup"><span data-stu-id="84ec5-183">Deployment consists of two steps:</span></span> 

1. <span data-ttu-id="84ec5-184">Les ressources cloud nécessaires sont créées.</span><span class="sxs-lookup"><span data-stu-id="84ec5-184">Necessary cloud resources are created.</span></span> <span data-ttu-id="84ec5-185">C’est également ce qu’on appelle la mise en service.</span><span class="sxs-lookup"><span data-stu-id="84ec5-185">This is also known as provisioning.</span></span>
1. <span data-ttu-id="84ec5-186">Commencez à coder et copiez votre application dans les ressources cloud créées.</span><span class="sxs-lookup"><span data-stu-id="84ec5-186">Start coding and copy your app into the created cloud resources.</span></span>

> <span data-ttu-id="84ec5-187">**Aperçu**</span><span class="sxs-lookup"><span data-stu-id="84ec5-187">**PREVIEW**</span></span>
>
> <span data-ttu-id="84ec5-188">La prise en charge des applications Blazor est une nouveauté de Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="84ec5-188">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="84ec5-189">L’approvisionnement et le déploiement sont effectués avec une combinaison de Visual Studio 2019 et du portail de développement pour Teams.</span><span class="sxs-lookup"><span data-stu-id="84ec5-189">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="84ec5-190">Mettre en service et déployer votre application dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="84ec5-190">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="84ec5-191">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nœud de projet et sélectionnez **Publier.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-191">In Solution Explorer, right-click the project node and select **Publish**.</span></span> <span data-ttu-id="84ec5-192">Vous pouvez également utiliser **l’élément**  >  **de** menu Publier la build.</span><span class="sxs-lookup"><span data-stu-id="84ec5-192">You can also use the **Build** > **Publish** menu item.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Sélectionner l’opération Publier sur le projet":::

1. <span data-ttu-id="84ec5-194">Dans la **fenêtre** Publier, sélectionnez **Azure** et **selct Next**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-194">In the **Publish** window, select **Azure** and selct **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Sélectionner Azure comme cible de publication":::

1. <span data-ttu-id="84ec5-196">Sélectionnez **Azure App Service (Windows)** et **sélectionnez Suivant**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-196">Select **Azure App Service (Windows)** and select **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Sélectionner Azure App Service comme cible de publication":::

1. <span data-ttu-id="84ec5-198">Sélectionnez **+** pour créer une nouvelle instance du service d’application.</span><span class="sxs-lookup"><span data-stu-id="84ec5-198">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Créez une instance.":::

1. <span data-ttu-id="84ec5-200">Dans la boîte de dialogue Créer un service d’application  **(Windows),** les champs d’entrée **Nom,** Nom de l’abonnement, Groupe de ressources et **Plan** d’hébergement sont remplies.</span><span class="sxs-lookup"><span data-stu-id="84ec5-200">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="84ec5-201">Si un service d’application est déjà en cours d’exécution, les paramètres existants sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="84ec5-201">If you have already got an App Service running, existing settings are selected.</span></span>  <span data-ttu-id="84ec5-202">Vous pouvez choisir de créer un groupe de ressources et un plan d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="84ec5-202">You can opt to create a new resource group and hosting plan.</span></span>  <span data-ttu-id="84ec5-203">Lorsque vous êtes prêt, sélectionnez **Créer.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-203">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Sélectionner le plan d’hébergement et l’abonnement":::

1. <span data-ttu-id="84ec5-205">Dans la **boîte de** dialogue Publier, l’instance nouvellement créée a été automatiquement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="84ec5-205">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="84ec5-206">Lorsque vous êtes prêt, sélectionnez **Terminer.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-206">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Sélectionnez la nouvelle instance.":::

1. <span data-ttu-id="84ec5-208">Sélectionnez **l’icône** Modifier (crayon) en de côté du **mode** déploiement, puis sélectionnez **Autonome.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-208">Select the **Edit** (pencil) icon next to **Deployment Mode**, and select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Sélectionnez le mode de déploiement autonome.":::

1. <span data-ttu-id="84ec5-210">Sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-210">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Publier votre application sur le service d’application":::

   <span data-ttu-id="84ec5-212">Visual Studio déploie l’application sur votre service d’application Azure et l’application web se charge dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="84ec5-212">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="84ec5-213">`/tab`Ajoutez-la à la fin de l’URL pour afficher votre page.</span><span class="sxs-lookup"><span data-stu-id="84ec5-213">Add `/tab` to the end of the URL to see your page.</span></span>

   <span data-ttu-id="84ec5-214">Le volet **Publication** des propriétés du projet affiche l’URL du site et d’autres détails.</span><span class="sxs-lookup"><span data-stu-id="84ec5-214">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="84ec5-215">Notez l’URL du site.</span><span class="sxs-lookup"><span data-stu-id="84ec5-215">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="84ec5-216">Créer un environnement pour votre application</span><span class="sxs-lookup"><span data-stu-id="84ec5-216">Create an environment for your app</span></span>

<span data-ttu-id="84ec5-217">Le Portail des développeurs pour Teams l’endroit où les onglets de votre application sont chargés à partir d’un **environnement.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-217">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  

<span data-ttu-id="84ec5-218">**Pour créer un environnement :**</span><span class="sxs-lookup"><span data-stu-id="84ec5-218">**To create an environment:**</span></span>

1. <span data-ttu-id="84ec5-219">Ouvrez [le portail du développeur pour Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="84ec5-219">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="84ec5-220">Connectez-vous avec votre compte d’administration M365.</span><span class="sxs-lookup"><span data-stu-id="84ec5-220">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="84ec5-221">Dans la barre latérale, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-221">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="84ec5-222">Si vous n’avez qu’une seule application, elle sera automatiquement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="84ec5-222">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="84ec5-223">Si ce n’est pas le cas, sélectionnez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="84ec5-223">If not, select your app from the list.</span></span>

1. <span data-ttu-id="84ec5-224">Sélectionnez **Environnements**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-224">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Sélectionner des environnements":::

1. <span data-ttu-id="84ec5-226">Sélectionnez **Créer votre premier environnement.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-226">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="84ec5-227">Entrez un nom pour votre environnement, puis sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-227">Enter a name for your environment and select **Add**.</span></span> <span data-ttu-id="84ec5-228">Par exemple, `_Production_`.</span><span class="sxs-lookup"><span data-stu-id="84ec5-228">For example, `_Production_`.</span></span>

1. <span data-ttu-id="84ec5-229">Sélectionnez **Créer votre première variable d’environnement.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-229">Select **Create your first environment variable**.</span></span>

1. <span data-ttu-id="84ec5-230">Entrez `azure_app_url` le **nom**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-230">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="84ec5-231">Entrez l’URL de votre site Azure sans `https://` la valeur . </span><span class="sxs-lookup"><span data-stu-id="84ec5-231">Enter your Azure site URL without the `https://` as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Créer une variable d’environnement":::

   <span data-ttu-id="84ec5-233">Appuyez **sur Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-233">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="84ec5-234">Mettre à jour le manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="84ec5-234">Update the app manifest</span></span>

<span data-ttu-id="84ec5-235">Le manifeste de l’application charge l’onglet à partir d’une `localhost` URL.</span><span class="sxs-lookup"><span data-stu-id="84ec5-235">The app manifest loads the tab from a `localhost` URL.</span></span>  <span data-ttu-id="84ec5-236">Dans cette section, vous allez configurer le manifeste de l’application pour charger l’onglet à partir de l’URL répertoriée dans l’environnement que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="84ec5-236">In this section, you will configure the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="84ec5-237">Dans la barre latérale, sélectionnez **Informations de base.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-237">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Sélectionner des informations de base":::

1. <span data-ttu-id="84ec5-239">Il existe plusieurs endroits dans le manifeste qui résentent un élément `locahost:XXXXX` dans une URL.</span><span class="sxs-lookup"><span data-stu-id="84ec5-239">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="84ec5-240">Remplacez toutes les occurrences `{{azure_app_url}}` par , y compris les accolades.</span><span class="sxs-lookup"><span data-stu-id="84ec5-240">Replace all occurrences with `{{azure_app_url}}`, including the curly braces.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Ajuster les informations de base pour l’environnement":::

1. <span data-ttu-id="84ec5-242">Lorsque vous avez terminé, sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-242">When complete, select **Save**.</span></span>

1. <span data-ttu-id="84ec5-243">Dans la barre latérale, sélectionnez **Fonctionnalités.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-243">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Sélectionner des fonctionnalités":::

1. <span data-ttu-id="84ec5-245">Sélectionnez **Onglet personnel.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-245">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="84ec5-246">En de côté de **l’onglet Personnel,** sélectionnez les trois points, puis sélectionnez **Modifier.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-246">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Modifier les paramètres d’onglet personnel":::

1. <span data-ttu-id="84ec5-248">Remplacez l’URL par la variable d’environnement dans les champs **URL de contenu** et URL du **site** web.</span><span class="sxs-lookup"><span data-stu-id="84ec5-248">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Modifier les URL d’onglet personnel":::

1. <span data-ttu-id="84ec5-250">Sélectionnez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-250">Select **Update**.</span></span>

1. <span data-ttu-id="84ec5-251">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-251">Select **Save**.</span></span>

1. <span data-ttu-id="84ec5-252">Dans la barre latérale, sélectionnez **Sign-On unique**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-252">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="84ec5-253">Remplacez `localhost` **l’URI de l’ID d’application** par `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="84ec5-253">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Modifier l’URI de l’ID d’application d' sign-on unique":::

1. <span data-ttu-id="84ec5-255">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-255">Select **Save**.</span></span>

1. <span data-ttu-id="84ec5-256">Dans la barre latérale, sélectionnez **Domaines.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-256">From the sidebar, select **Domains**.</span></span>

1. <span data-ttu-id="84ec5-257">Sélectionnez **Ajouter un domaine**.</span><span class="sxs-lookup"><span data-stu-id="84ec5-257">Select **Add a domain**.</span></span>

1. <span data-ttu-id="84ec5-258">Si ce domaine n’est pas répertorié comme un domaine valide, ajoutez-le en tant que `{{azure_app_url}}` domaine valide, puis sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="84ec5-258">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then select **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Ajouter un domaine":::

   <span data-ttu-id="84ec5-260">Vous pouvez désormais utiliser l’option Aperçu **Teams** en haut de la page pour lancer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="84ec5-260">You can now use the **Preview in Teams** option at the top of the page to launch your app within Teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="84ec5-261">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="84ec5-261">See also</span></span>

* [<span data-ttu-id="84ec5-262">Présentation des didacticiels</span><span class="sxs-lookup"><span data-stu-id="84ec5-262">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="84ec5-263">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="84ec5-263">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="84ec5-264">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="84ec5-264">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="84ec5-265">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="84ec5-265">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
