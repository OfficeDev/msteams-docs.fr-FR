---
title: Get started - Build your first Teams app with Blazor
author: adrianhall
description: Créez rapidement une Microsoft Teams qui affiche un « Hello, World! » à l’aide Microsoft Teams Shared Computer Toolkit et .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: 6a9c7e008e2fb6d77c3314286b09d006bd468c37
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667453"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="5a156-104">Créer et exécuter votre première application Microsoft Teams avec Blazor</span><span class="sxs-lookup"><span data-stu-id="5a156-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="5a156-105">Dans ce didacticiel, vous allez créer une application Microsoft Teams dans .NET/Blazor qui implémente une application personnelle simple pour tirer des informations du microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="5a156-105">In this tutorial, you will create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="5a156-106">(Une *application personnelle inclut* un ensemble d’onglets inclus pour une utilisation individuelle.)  Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment exécuter une application localement et comment déployer l’application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="5a156-106">(A *personal app* includes a set of tabs scoped for individual use.)  During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="5a156-107">L’application qui est conçue affiche les informations utilisateur de base pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="5a156-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="5a156-108">Lorsque l’autorisation est accordée, l’application se connecte à l’Graph Microsoft en tant qu’utilisateur actuel pour obtenir le profil complet.</span><span class="sxs-lookup"><span data-stu-id="5a156-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5a156-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="5a156-109">Before you begin</span></span>

<span data-ttu-id="5a156-110">Assurez-vous que votre environnement de développement est installé en installant les conditions [préalables](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="5a156-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a156-111">Installer les composants prérequis</span><span class="sxs-lookup"><span data-stu-id="5a156-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="5a156-112">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="5a156-112">Create your project</span></span>

<span data-ttu-id="5a156-113">Utilisez la Teams Shared Computer Toolkit pour créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="5a156-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="5a156-114">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="5a156-114">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="5a156-115">Ouvrez Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="5a156-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="5a156-116">Sélectionnez **Créer un projet.**</span><span class="sxs-lookup"><span data-stu-id="5a156-116">Select **Create a new project**.</span></span>

1. <span data-ttu-id="5a156-117">Sélectionnez **Microsoft Teams Application,** puis appuyez sur **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="5a156-117">Select **Microsoft Teams App**, then press **Next**.</span></span>  <span data-ttu-id="5a156-118">Pour vous aider à trouver le modèle, utilisez le type de **projet Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="5a156-118">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="5a156-119">Donnez un nom au projet et à la solution, puis appuyez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="5a156-119">Give the project and solution a good name, then press **Next**.</span></span>

1. <span data-ttu-id="5a156-120">Fournissez le nom de l’application et le nom de la société, puis appuyez sur **Créer.**</span><span class="sxs-lookup"><span data-stu-id="5a156-120">Provide the application name and company name, then press **Create**.</span></span>  <span data-ttu-id="5a156-121">Le nom de l’application et le nom de la société sont affichés pour vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="5a156-121">The application name and company name are displayed to your end users.</span></span>

1. <span data-ttu-id="5a156-122">Votre Teams sera créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="5a156-122">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="5a156-123">Une fois le projet créé, configurer l' sign-on unique avec M365 :</span><span class="sxs-lookup"><span data-stu-id="5a156-123">Once the project is created, set up single sign-on with M365:</span></span>

   - <span data-ttu-id="5a156-124">Sélectionnez **Project**  >  **TeamsFx**  >  **Configurer pour l' sso...**.</span><span class="sxs-lookup"><span data-stu-id="5a156-124">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   - <span data-ttu-id="5a156-125">Lorsque vous y invitez, connectez-vous à votre compte d’administrateur M365.</span><span class="sxs-lookup"><span data-stu-id="5a156-125">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="5a156-126">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="5a156-126">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="5a156-127">Ouvrez un Terminal et sélectionnez le répertoire dans lequel vous souhaitez créer le projet.</span><span class="sxs-lookup"><span data-stu-id="5a156-127">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="5a156-128">Exécutez `dotnet new -i` cette page pour installer le modèle à partir NuGet :</span><span class="sxs-lookup"><span data-stu-id="5a156-128">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="5a156-129">Vous ne devez le faire que la première fois ou lors de la mise à jour du modèle.</span><span class="sxs-lookup"><span data-stu-id="5a156-129">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="5a156-130">Vérifiez [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) la dernière version de ce package.</span><span class="sxs-lookup"><span data-stu-id="5a156-130">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="5a156-131">Créez un répertoire :</span><span class="sxs-lookup"><span data-stu-id="5a156-131">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="5a156-132">Exécutez `dotnet new` cette recherche pour créer un projet :</span><span class="sxs-lookup"><span data-stu-id="5a156-132">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="5a156-133">Une fois la construction échafaudée, configurez le projet pour Teams déploiement :</span><span class="sxs-lookup"><span data-stu-id="5a156-133">Once scaffolded, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

<span data-ttu-id="5a156-134">Vous pouvez maintenant ouvrir la solution dans Visual Studio débogage.</span><span class="sxs-lookup"><span data-stu-id="5a156-134">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="5a156-135">Faire une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="5a156-135">Take a tour of the source code</span></span>

<span data-ttu-id="5a156-136">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement.](#run-your-app-locally)</span><span class="sxs-lookup"><span data-stu-id="5a156-136">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="5a156-137">Une fois Teams Shared Computer Toolkit votre projet, vous avez les composants pour créer une application personnelle de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="5a156-137">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="5a156-138">Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de solutions Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="5a156-138">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour une application personnelle Visual Studio 2019.":::

- <span data-ttu-id="5a156-140">Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png` .</span><span class="sxs-lookup"><span data-stu-id="5a156-140">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="5a156-141">Le manifeste de l’application pour la publication via le portail de développement pour Teams est stocké dans `Properties/manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="5a156-141">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="5a156-142">Un contrôleur de serveur back-end est fourni pour `Controllers/BackendController.cs` faciliter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="5a156-142">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="5a156-143">Étant donné que vous avez créé une application d’onglet lors de l’installation, l’Teams Shared Computer Toolkit crée la modèle de tout le code nécessaire pour un onglet de base en tant que [serveur Blazor](/aspnet/core/blazor).</span><span class="sxs-lookup"><span data-stu-id="5a156-143">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="5a156-144">`Pages/Tab.razor` est le point d’entrée de l’application frontale.</span><span class="sxs-lookup"><span data-stu-id="5a156-144">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="5a156-145">`TeamsFx.cs`et `JS/src/index.js` est utilisé pour initialiser les communications avec l’Teams hôte.</span><span class="sxs-lookup"><span data-stu-id="5a156-145">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="5a156-146">Vous pouvez ajouter des fonctionnalités de back-end en ajoutant des contrôleurs ASP.NET Core supplémentaires à votre application.</span><span class="sxs-lookup"><span data-stu-id="5a156-146">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="5a156-147">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="5a156-147">Run your app locally</span></span>

<span data-ttu-id="5a156-148">Teams Shared Computer Toolkit vous permet d’exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="5a156-148">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="5a156-149">Il s’agit de plusieurs parties qui sont nécessaires pour fournir l’infrastructure Teams s’attend à :</span><span class="sxs-lookup"><span data-stu-id="5a156-149">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="5a156-150">Une application est inscrite auprès de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5a156-150">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="5a156-151">Cette application dispose d’autorisations associées à l’emplacement à partir de quel emplacement l’application est chargée et aux ressources back-end à partir des ressources à partir des quelles elle accède.</span><span class="sxs-lookup"><span data-stu-id="5a156-151">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="5a156-152">Une API web est hébergée (via IIS Express) pour faciliter les tâches d’authentification, agissant en tant que proxy entre l’application et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5a156-152">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="5a156-153">Un manifeste d’application est généré et existe dans le portail de développement pour Teams.</span><span class="sxs-lookup"><span data-stu-id="5a156-153">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="5a156-154">Teams utilise le manifeste de l’application pour indiquer aux clients connectés à partir de quel endroit charger l’application.</span><span class="sxs-lookup"><span data-stu-id="5a156-154">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="5a156-155">Une fois cette demande effectuée, l’application peut être chargée dans le client Teams client.</span><span class="sxs-lookup"><span data-stu-id="5a156-155">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="5a156-156">Nous utilisons le client web Teams pour voir le code HTML, CSS et JavaScript dans un environnement de développement web standard.</span><span class="sxs-lookup"><span data-stu-id="5a156-156">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="5a156-157">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="5a156-157">To build and run your app locally:</span></span>

1. <span data-ttu-id="5a156-158">À partir Visual Studio Code, **appuyez sur F5** pour exécuter votre application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="5a156-158">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

1. <span data-ttu-id="5a156-159">Si nécessaire, installez le certificat SSL auto-signé pour le débogage local.</span><span class="sxs-lookup"><span data-stu-id="5a156-159">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Screenshot showing how the prompt to install a SSL certificate to enable Teams to load your application from localhost.":::

1. <span data-ttu-id="5a156-161">Teams seront chargés dans un navigateur web et vous serez invité à vous y inscrire.</span><span class="sxs-lookup"><span data-stu-id="5a156-161">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="5a156-162">Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="5a156-162">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="5a156-163">Connectez-vous avec votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="5a156-163">Sign in with your M365 account.</span></span>
1. <span data-ttu-id="5a156-164">Lorsque vous avez été invité à installer l’application sur Teams, appuyez sur **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="5a156-164">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="5a156-165">Votre application s’affiche désormais :</span><span class="sxs-lookup"><span data-stu-id="5a156-165">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="Capture d’écran de l’application terminée":::

<span data-ttu-id="5a156-167">Vous pouvez faire des activités de débogage normales comme s’il s’avait été une autre application web (par exemple, la définition de points d’arrêt).</span><span class="sxs-lookup"><span data-stu-id="5a156-167">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="5a156-168">L’application prend en charge le rechargement à chaud.</span><span class="sxs-lookup"><span data-stu-id="5a156-168">The app supports hot reloading.</span></span>  <span data-ttu-id="5a156-169">Si vous modifiez un fichier dans le projet, la page est rechargée.</span><span class="sxs-lookup"><span data-stu-id="5a156-169">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="5a156-170">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogger.</span><span class="sxs-lookup"><span data-stu-id="5a156-170">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="5a156-171">Lorsque vous appuyez sur F5, le Teams Shared Computer Toolkit :</span><span class="sxs-lookup"><span data-stu-id="5a156-171">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="5a156-172">Vous avez inscrit votre application auprès Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5a156-172">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="5a156-173">Votre application a été inscrite pour le « chargement de version latéral » dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5a156-173">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="5a156-174">Le back-end de votre application a démarré en cours d’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="5a156-174">Started your application backend running locally.</span></span>
1. <span data-ttu-id="5a156-175">A démarré votre application frontale hébergée localement.</span><span class="sxs-lookup"><span data-stu-id="5a156-175">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="5a156-176">Démarré Microsoft Teams dans un navigateur web avec une commande pour demander Teams charger l’application de côté (l’URL est enregistrée dans le manifeste de l’application).</span><span class="sxs-lookup"><span data-stu-id="5a156-176">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="5a156-177">Découvrez comment résoudre les problèmes courants lors de l’exécution locale de votre application.</span><span class="sxs-lookup"><span data-stu-id="5a156-177">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="5a156-178">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement côté application.</span><span class="sxs-lookup"><span data-stu-id="5a156-178">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="5a156-179">Pour plus d’informations sur l’ouverture du compte, voir [Conditions préalables.](prerequisites.md#enable-sideloading)</span><span class="sxs-lookup"><span data-stu-id="5a156-179">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="5a156-180">Déployer votre application sur Azure</span><span class="sxs-lookup"><span data-stu-id="5a156-180">Deploy your app to Azure</span></span>

<span data-ttu-id="5a156-181">Le déploiement se compose de deux étapes.</span><span class="sxs-lookup"><span data-stu-id="5a156-181">Deployment consists of two steps.</span></span>  <span data-ttu-id="5a156-182">Tout d’abord, les ressources cloud nécessaires sont créées (également appelées approvisionnement), puis le code qui constitue votre application est copié dans les ressources cloud créées.</span><span class="sxs-lookup"><span data-stu-id="5a156-182">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

> <span data-ttu-id="5a156-183">**Aperçu**</span><span class="sxs-lookup"><span data-stu-id="5a156-183">**PREVIEW**</span></span>
>
> <span data-ttu-id="5a156-184">La prise en charge des applications Blazor est une nouveauté de Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="5a156-184">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="5a156-185">L’approvisionnement et le déploiement sont effectués avec une combinaison de Visual Studio 2019 et du portail de développement pour Teams.</span><span class="sxs-lookup"><span data-stu-id="5a156-185">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="5a156-186">Mettre en service et déployer votre application dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5a156-186">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="5a156-187">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nœud du projet et choisissez **Publier** (ou utilisez l’élément  >  **de** menu Publier la build).</span><span class="sxs-lookup"><span data-stu-id="5a156-187">In Solution Explorer, right-click the project node and choose **Publish** (or use the **Build** > **Publish** menu item).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="Sélectionner l’opération Publier sur le projet":::

1. <span data-ttu-id="5a156-189">Dans la **fenêtre** Publier, sélectionnez **Azure.**</span><span class="sxs-lookup"><span data-stu-id="5a156-189">In the **Publish** window, select **Azure**.</span></span>  <span data-ttu-id="5a156-190">Appuyez **sur Suivant**.</span><span class="sxs-lookup"><span data-stu-id="5a156-190">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="Sélectionner Azure comme cible de publication":::

1. <span data-ttu-id="5a156-192">Sélectionnez **Azure App Service (Windows).**</span><span class="sxs-lookup"><span data-stu-id="5a156-192">Select **Azure App Service (Windows)**.</span></span>  <span data-ttu-id="5a156-193">Appuyez **sur Suivant**.</span><span class="sxs-lookup"><span data-stu-id="5a156-193">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="Sélectionner Azure App Service comme cible de publication":::

1. <span data-ttu-id="5a156-195">Sélectionnez **+** pour créer une nouvelle instance du service d’application.</span><span class="sxs-lookup"><span data-stu-id="5a156-195">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="Créez une instance.":::

1. <span data-ttu-id="5a156-197">Dans la boîte de dialogue Créer un service d’application  **(Windows),** les champs d’entrée **Nom,** Nom de l’abonnement, Groupe de ressources et **Plan** d’hébergement sont remplies.</span><span class="sxs-lookup"><span data-stu-id="5a156-197">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="5a156-198">Si un service d’application est déjà en cours d’exécution, les paramètres existants sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="5a156-198">If you have already got an App Service running, existing settings will be selected.</span></span>  <span data-ttu-id="5a156-199">Vous pouvez choisir de créer un groupe de ressources et un plan d’hébergement (recommandé).</span><span class="sxs-lookup"><span data-stu-id="5a156-199">You can opt to create a new resource group and hosting plan (Recommended).</span></span>  <span data-ttu-id="5a156-200">Lorsque vous êtes prêt, sélectionnez **Créer.**</span><span class="sxs-lookup"><span data-stu-id="5a156-200">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="Sélectionner le plan d’hébergement et l’abonnement":::

1. <span data-ttu-id="5a156-202">Dans la **boîte de** dialogue Publier, l’instance nouvellement créée a été automatiquement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5a156-202">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="5a156-203">Lorsque vous êtes prêt, sélectionnez **Terminer.**</span><span class="sxs-lookup"><span data-stu-id="5a156-203">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="Sélectionnez la nouvelle instance.":::

1. <span data-ttu-id="5a156-205">Appuyez **sur l’icône** Modifier (crayon) en de côté du **mode** déploiement, puis sélectionnez **Autonome.**</span><span class="sxs-lookup"><span data-stu-id="5a156-205">Press the **Edit** (pencil) icon next to **Deployment Mode**, then select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="Sélectionnez le mode de déploiement autonome.":::

1. <span data-ttu-id="5a156-207">Sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="5a156-207">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="Publier votre application sur le service d’application":::

<span data-ttu-id="5a156-209">Visual Studio déploie l’application sur votre service d’application Azure et l’application web se charge dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="5a156-209">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="5a156-210">`/tab`Ajoutez-la à la fin de l’URL pour afficher votre page.</span><span class="sxs-lookup"><span data-stu-id="5a156-210">Add `/tab` to the end of the URL to see your page.</span></span>

<span data-ttu-id="5a156-211">Le volet **Publication** des propriétés du projet affiche l’URL du site et d’autres détails.</span><span class="sxs-lookup"><span data-stu-id="5a156-211">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="5a156-212">Notez l’URL du site.</span><span class="sxs-lookup"><span data-stu-id="5a156-212">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="5a156-213">Créer un environnement pour votre application</span><span class="sxs-lookup"><span data-stu-id="5a156-213">Create an environment for your app</span></span>

<span data-ttu-id="5a156-214">Le Portail des développeurs pour Teams l’endroit où les onglets de votre application sont chargés à partir d’un **environnement.**</span><span class="sxs-lookup"><span data-stu-id="5a156-214">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  <span data-ttu-id="5a156-215">Pour créer un environnement :</span><span class="sxs-lookup"><span data-stu-id="5a156-215">To create an environment:</span></span>

1. <span data-ttu-id="5a156-216">Ouvrez [le portail du développeur pour Teams](https://dev.teams.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5a156-216">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="5a156-217">Connectez-vous avec votre compte d’administration M365.</span><span class="sxs-lookup"><span data-stu-id="5a156-217">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="5a156-218">Dans la barre latérale, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="5a156-218">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="5a156-219">Si vous n’avez qu’une seule application, elle sera automatiquement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5a156-219">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="5a156-220">Si ce n’est pas le cas, sélectionnez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="5a156-220">If not, select your app from the list.</span></span>

1. <span data-ttu-id="5a156-221">Sélectionnez **Environnements**.</span><span class="sxs-lookup"><span data-stu-id="5a156-221">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="Sélectionner des environnements":::

1. <span data-ttu-id="5a156-223">Sélectionnez **Créer votre premier environnement.**</span><span class="sxs-lookup"><span data-stu-id="5a156-223">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="5a156-224">Entrez un nom pour votre environnement, puis appuyez sur **Ajouter**; par exemple _Production_.</span><span class="sxs-lookup"><span data-stu-id="5a156-224">Enter a name for your environment, then press **Add**; for example _Production_.</span></span>

1. <span data-ttu-id="5a156-225">Une fois l’environnement nouvellement créé sélectionné, **appuyez sur Créer votre première variable d’environnement.**</span><span class="sxs-lookup"><span data-stu-id="5a156-225">With the newly created environment selected, press **Create your first environment variable**.</span></span>

1. <span data-ttu-id="5a156-226">Entrez `azure_app_url` le **nom**.</span><span class="sxs-lookup"><span data-stu-id="5a156-226">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="5a156-227">Entrez l’URL de votre site Azure (sans `https://` la ) comme **valeur**.</span><span class="sxs-lookup"><span data-stu-id="5a156-227">Enter your Azure site URL (without the `https://`) as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="Créer une variable d’environnement":::

   <span data-ttu-id="5a156-229">Appuyez **sur Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="5a156-229">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="5a156-230">Mettre à jour le manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="5a156-230">Update the app manifest</span></span>

<span data-ttu-id="5a156-231">Le manifeste de l’application charge l’onglet à partir d’une `localhost` URL.</span><span class="sxs-lookup"><span data-stu-id="5a156-231">The app manifest is loading the tab from a `localhost` URL.</span></span>  <span data-ttu-id="5a156-232">Dans cette section, vous allez ajuster le manifeste de l’application pour charger l’onglet à partir de l’URL répertoriée dans l’environnement que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="5a156-232">In this section, you will adjust the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="5a156-233">Dans la barre latérale, sélectionnez **Informations de base.**</span><span class="sxs-lookup"><span data-stu-id="5a156-233">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="Sélectionner des informations de base":::

1. <span data-ttu-id="5a156-235">Il existe plusieurs endroits dans le manifeste qui résentent un élément `locahost:XXXXX` dans une URL.</span><span class="sxs-lookup"><span data-stu-id="5a156-235">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="5a156-236">Remplacez toutes les occurrences `{{azure_app_url}}` par (y compris les accolades).</span><span class="sxs-lookup"><span data-stu-id="5a156-236">Replace all occurrences with `{{azure_app_url}}` (including the curly braces).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="Ajuster les informations de base pour l’environnement":::

1. <span data-ttu-id="5a156-238">Lorsque vous terminez, appuyez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5a156-238">When complete, press **Save**.</span></span>

1. <span data-ttu-id="5a156-239">Dans la barre latérale, sélectionnez **Fonctionnalités.**</span><span class="sxs-lookup"><span data-stu-id="5a156-239">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="Sélectionner des fonctionnalités":::

1. <span data-ttu-id="5a156-241">Sélectionnez **Onglet personnel.**</span><span class="sxs-lookup"><span data-stu-id="5a156-241">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="5a156-242">En de côté de **l’onglet Personnel,** sélectionnez les trois points, puis sélectionnez **Modifier.**</span><span class="sxs-lookup"><span data-stu-id="5a156-242">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="Modifier les paramètres d’onglet personnel":::

1. <span data-ttu-id="5a156-244">Remplacez l’URL par la variable d’environnement dans les champs **Url de contenu** et Url du **site** web.</span><span class="sxs-lookup"><span data-stu-id="5a156-244">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="Modifier les URL d’onglet personnel":::

1. <span data-ttu-id="5a156-246">Appuyez sur **Mettre à jour.**</span><span class="sxs-lookup"><span data-stu-id="5a156-246">Press **Update**.</span></span>

1. <span data-ttu-id="5a156-247">Appuyez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5a156-247">Press **Save**.</span></span>

1. <span data-ttu-id="5a156-248">Dans la barre latérale, sélectionnez **Sign-On unique**.</span><span class="sxs-lookup"><span data-stu-id="5a156-248">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="5a156-249">Remplacez `localhost` **l’URI de l’ID d’application** par `{{azure_app_url}}` .</span><span class="sxs-lookup"><span data-stu-id="5a156-249">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="Modifier l’URI de l’ID d’application d' sign-on unique":::

1. <span data-ttu-id="5a156-251">Appuyez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5a156-251">Press **Save**.</span></span>

1. <span data-ttu-id="5a156-252">À partir de la barre latérale, appuyez **sur Domaines.**</span><span class="sxs-lookup"><span data-stu-id="5a156-252">From the sidebar, press **Domains**.</span></span>

1. <span data-ttu-id="5a156-253">Appuyez **sur Ajouter un domaine.**</span><span class="sxs-lookup"><span data-stu-id="5a156-253">Press **Add a domain**.</span></span>

1. <span data-ttu-id="5a156-254">Si ce domaine n’est pas répertorié comme un domaine valide, ajoutez-le en tant que `{{azure_app_url}}` domaine valide, puis appuyez sur **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="5a156-254">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then press **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="Ajouter un domaine":::

<span data-ttu-id="5a156-256">Vous pouvez désormais utiliser l’aperçu **dans Teams** en haut de la page pour lancer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="5a156-256">You can now use the **Preview in Teams** button at the top of the page to launch your app within Teams.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a156-257">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a156-257">Next steps</span></span>

<span data-ttu-id="5a156-258">Découvrez les autres méthodes de création d’Teams applications :</span><span class="sxs-lookup"><span data-stu-id="5a156-258">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="5a156-259">Créer une application Teams avec React</span><span class="sxs-lookup"><span data-stu-id="5a156-259">Create a Teams app with React</span></span>](first-app-react.md)
- <span data-ttu-id="5a156-260">[Créer une application Teams en tant que SharePoint Web Part](first-app-spfx.md) (Azure non requis)</span><span class="sxs-lookup"><span data-stu-id="5a156-260">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="5a156-261">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="5a156-261">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="5a156-262">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="5a156-262">Create a messaging extension</span></span>](first-message-extension.md)