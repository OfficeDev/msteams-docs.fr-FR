---
title: 'Commencer : créer et exécuter votre première application'
author: girliemac
description: Créez rapidement une application Microsoft Teams qui affiche un « Hello, World! » à l'aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068781"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="dcd12-104">Créer votre première application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="dcd12-105">Ce démarrage rapide vous apprend à créer et exécuter l'application Microsoft Teams qui affiche « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="dcd12-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcd12-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dcd12-106">Prerequisites</span></span>

<span data-ttu-id="dcd12-107">Avant de commencer, vous devez configurer [votre client](#set-up-your-teams-development-tenant) de développement Teams et installer [vos outils de développement Teams.](#install-your-development-tools)</span><span class="sxs-lookup"><span data-stu-id="dcd12-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="dcd12-108">Configurer votre client de développement Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="dcd12-109">Un **client** est comme un conteneur pour une organisation.</span><span class="sxs-lookup"><span data-stu-id="dcd12-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="dcd12-110">En termes teams, un client est l'endroit où les personnes de cette organisation discutent, partagent des fichiers et exécutent des réunions.</span><span class="sxs-lookup"><span data-stu-id="dcd12-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="dcd12-111">En tant que développeur, vous avez besoin d'un client pour le chargement indépendant et le test des applications Teams que vous construisez.</span><span class="sxs-lookup"><span data-stu-id="dcd12-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="dcd12-112">N'avez pas de client</span><span class="sxs-lookup"><span data-stu-id="dcd12-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="dcd12-113">Vous pouvez obtenir un compte de test Teams gratuit, qui inclut un client qui autorise le chargement de version test d'application, en rejoignant le programme pour les développeurs Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="dcd12-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="dcd12-114">Le processus d'inscription prend environ deux minutes.</span><span class="sxs-lookup"><span data-stu-id="dcd12-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="dcd12-115">**Pour obtenir un client**</span><span class="sxs-lookup"><span data-stu-id="dcd12-115">**To get a tenant**</span></span>

1. <span data-ttu-id="dcd12-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="dcd12-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="dcd12-117">Sélectionnez **Rejoindre maintenant** et suivez les instructions à l'écran.</span><span class="sxs-lookup"><span data-stu-id="dcd12-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="dcd12-118">Dans l'écran d'accueil, **sélectionnez Configurer l'abonnement E5.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="dcd12-119">Configurer votre compte de développeur Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="dcd12-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="dcd12-120">Une fois que vous avez terminé, l'écran suivant s'affiche :</span><span class="sxs-lookup"><span data-stu-id="dcd12-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme pour les développeurs Microsoft 365.":::

1. <span data-ttu-id="dcd12-122">Connectez-vous à Teams avec votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="dcd12-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="dcd12-123">Dans le client Teams, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="dcd12-124">Vérifiez que vous pouvez voir l'option **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="dcd12-125">Si c'est le cas, cela signifie que vous pouvez télécharger une version de version de chargement de version d'application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="dcd12-127">Avoir un client</span><span class="sxs-lookup"><span data-stu-id="dcd12-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="dcd12-128">Si vous avez déjà un client, vérifiez si vous pouvez télécharger une version de version de chargement de version d'application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="dcd12-129">**Vérifier que vous pouvez télécharger une version de version de chargement de version de vos applications**</span><span class="sxs-lookup"><span data-stu-id="dcd12-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="dcd12-130">Dans le client Teams, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="dcd12-131">Vérifiez que vous pouvez voir l'option **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="dcd12-132">Si vous le faites, cela signifie que vous pouvez télécharger une version de version de chargement de version de version d'application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="dcd12-134">Installer vos outils de développement</span><span class="sxs-lookup"><span data-stu-id="dcd12-134">Install your development tools</span></span>

<span data-ttu-id="dcd12-135">Pour créer cette application, vous allez utiliser le Shared Computer Toolkit Teams pour Visual Studio code pour démarrer rapidement.</span><span class="sxs-lookup"><span data-stu-id="dcd12-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="dcd12-136">Vous pouvez également créer des applications Teams avec n'importe quel de vos outils pré-utilisés.</span><span class="sxs-lookup"><span data-stu-id="dcd12-136">You can also build Teams apps with any ofyour preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="dcd12-137">Teams affiche le contenu de l'application uniquement par le biais de connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dcd12-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="dcd12-138">Pour déboguer certains types d'applications localement, comme un bot, vous allez apprendre à utiliser ngrok pour configurer un tunnel sécurisé entre Teams et votre application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="dcd12-139">Les applications De Production Teams sont hébergées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd12-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="dcd12-140">**Pour installer les outils Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="dcd12-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="dcd12-141">Installez [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="dcd12-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="dcd12-142">Si vous prévoyez de créer un bot ou une extension de messagerie, installez [ngrok](https://ngrok.com/download) et exposez votre [localhost sur Internet](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)à l'aide de ngrok .</span><span class="sxs-lookup"><span data-stu-id="dcd12-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="dcd12-143">Installez la dernière version de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="dcd12-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="dcd12-144">Le kit de ressources ne prend pas en charge les versions antérieures Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dcd12-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. Dans la barre d'activité de gauche, sélectionnez **Extensions.** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. <span data-ttu-id="dcd12-146">Dans **Microsoft Teams Shared Computer Toolkit,** sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où, dans Visual Studio Code, vous pouvez installer l'extension Shared Computer Toolkit Microsoft Teams.":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="dcd12-148">1. Créer votre projet d'application</span><span class="sxs-lookup"><span data-stu-id="dcd12-148">1. Create your app project</span></span>

1. <span data-ttu-id="dcd12-149">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dcd12-149">Open Visual Studio Code.</span></span>
1. Sélectionnez **Microsoft Teams Shared Computer Toolkit** créer une application :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Capture d'écran montrant comment créer votre projet d'application avec la Visual Studio Code Teams Shared Computer Toolkit.":::
   
1. <span data-ttu-id="dcd12-152">Connectez-vous avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="dcd12-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="dcd12-153">Soit celui que vous avez créé, soit le compte que vous avez déjà qui autorise le chargement d'une version de l'application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="dcd12-154">Dans **l'écran Sélectionner un** projet, sélectionnez **Application** personnelle et **sélectionnez JS** (JavaScript) > **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dcd12-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Capture d'écran montrant comment configurer votre projet d'application avec la Visual Studio Code Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="dcd12-156">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Screenshot showing how to add a name to your app project with the Visual Studio Code Teams Toolkit.":::

1. <span data-ttu-id="dcd12-158">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="dcd12-158">Select **Finish**.</span></span> 
   <span data-ttu-id="dcd12-159">Votre projet est maintenant configuré.</span><span class="sxs-lookup"><span data-stu-id="dcd12-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="dcd12-160">2. Comprendre les composants de votre projet d'application</span><span class="sxs-lookup"><span data-stu-id="dcd12-160">2. Understand your app project components</span></span>

<span data-ttu-id="dcd12-161">Une fois que le kit de ressources a configuré votre projet d'application, vous avez les composants pour créer votre « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="dcd12-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="dcd12-162">Application Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-162">Teams app.</span></span> <span data-ttu-id="dcd12-163">Les répertoires et fichiers du projet se trouvent dans l'Explorateur Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="dcd12-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Screenshot showing the scaffolding in your app project with the Visual Studio Code Teams Toolkit.":::

<span data-ttu-id="dcd12-165">Le kit de ressources crée automatiquement la création de la création de lacafé d'application dans le répertoire en fonction des fonctionnalités que vous avez ajoutées `src` lors de l'installation.</span><span class="sxs-lookup"><span data-stu-id="dcd12-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="dcd12-166">Étant donné que vous avez créé un onglet lors de l'installation, le fichier dans le répertoire gère l'initialisation et le `App.js` `src/components` routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="dcd12-167">Le fichier appelle également le SDK client JavaScript Microsoft Teams pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="dcd12-168">3. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="dcd12-168">3. Build and run your app</span></span>

<span data-ttu-id="dcd12-169">Créez et exécutez votre application localement pour gagner du temps.</span><span class="sxs-lookup"><span data-stu-id="dcd12-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="dcd12-170">**Pour créer et exécuter votre application**</span><span class="sxs-lookup"><span data-stu-id="dcd12-170">**To build and run your app**</span></span>

1. <span data-ttu-id="dcd12-171">Dans Visual Studio code, sélectionnez **Afficher le**  >  **terminal.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="dcd12-172">Exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="dcd12-172">Run `npm install`.</span></span>
1. <span data-ttu-id="dcd12-173">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="dcd12-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="dcd12-174">Une **compilation réussie !**</span><span class="sxs-lookup"><span data-stu-id="dcd12-174">A **Compiled successfully!**</span></span> <span data-ttu-id="dcd12-175">s'affiche dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="dcd12-175">message appears in the terminal.</span></span> <span data-ttu-id="dcd12-176">Votre application est désormais en cours d'exécution sur votre localhost sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="dcd12-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="dcd12-177">4. Chargement de version secondaire de votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="dcd12-178">Le chargement de version d'évaluation est le processus d'installation d'une application dans Teams qui n'a pas été approuvée par votre administrateur ou Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcd12-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="dcd12-179">Le chargement de version test est courant lors du test et du débogage des applications Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="dcd12-180">Par défaut, Teams n'autorise pas le chargement de version de l'application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="dcd12-181">Vous pouvez modifier ce paramètre dans le Centre d'administration Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="dcd12-182">**Pour activer le chargement de version d'application dans Teams**</span><span class="sxs-lookup"><span data-stu-id="dcd12-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="dcd12-183">Connectez-vous au [Centre d'administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d'identification d'administrateur.</span><span class="sxs-lookup"><span data-stu-id="dcd12-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="dcd12-184">Sélectionnez **Afficher toutes les**  >  **équipes.**</span><span class="sxs-lookup"><span data-stu-id="dcd12-184">Select **Show All** > **Teams**.</span></span> 

   ![image du menu centre d'administration](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="dcd12-186">L'apparition de l'option **Teams** peut prendre jusqu'à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="dcd12-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="dcd12-187">Go to **Teams apps**  >  **Setup policies**  >  **Global** (Org-wide default).</span><span class="sxs-lookup"><span data-stu-id="dcd12-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![activer l'affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="dcd12-189">Activer le **basculement d'applications personnalisées** de chargement.</span><span class="sxs-lookup"><span data-stu-id="dcd12-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="dcd12-190">Sélectionnez **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="dcd12-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="dcd12-191">Votre client test autorise désormais le chargement de version test de l'application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="dcd12-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="dcd12-192">Vérifiez les problèmes avant de décharger votre application à l'aide de la fonctionnalité de validation dans App Studio, qui est incluse dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="dcd12-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="dcd12-193">Corrigez les erreurs de chargement de version de l'application.</span><span class="sxs-lookup"><span data-stu-id="dcd12-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="dcd12-194">Chargement de version secondaire de votre application</span><span class="sxs-lookup"><span data-stu-id="dcd12-194">Sideload your app</span></span>

1. <span data-ttu-id="dcd12-195">Dans Visual Studio Code, ouvrez le Shared Computer Toolkit Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="dcd12-196">Go to **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="dcd12-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="dcd12-197">Sélectionnez **Tester et distribuer l'installation.**  >  </span><span class="sxs-lookup"><span data-stu-id="dcd12-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Screenshot showing how to sideload your app to Teams client with the Visual Studio Code Teams Toolkit.":::

<span data-ttu-id="dcd12-199">**Alternativement**</span><span class="sxs-lookup"><span data-stu-id="dcd12-199">**Alternatively**</span></span>

1. <span data-ttu-id="dcd12-200">Sélectionnez la **touche F5** pour ouvrir la fenêtre du navigateur à installer.</span><span class="sxs-lookup"><span data-stu-id="dcd12-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="dcd12-201">Cela permet d'ignorer le processus d'installation dans **App Studio** et d'installer Teams dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="dcd12-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="dcd12-202">Dans la boîte de dialogue d'installation, **sélectionnez Ajouter** pour installer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Screenshot showing how to sideload your app to Teams client.":::

   > [!Note]
   > <span data-ttu-id="dcd12-204">App Studio est également disponible en tant qu'application autonome pour le client Teams.</span><span class="sxs-lookup"><span data-stu-id="dcd12-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="dcd12-205">Résoudre les problèmes de chargement de version secondaire</span><span class="sxs-lookup"><span data-stu-id="dcd12-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="dcd12-206">**Échec de l'installation**</span><span class="sxs-lookup"><span data-stu-id="dcd12-206">**Installation failed**</span></span>

<span data-ttu-id="dcd12-207">Si le message d'erreur s'affiche lors de l'installation de votre application, vérifiez que les informations de `Manifest parsing has failed` l'application sont entrées correctement.</span><span class="sxs-lookup"><span data-stu-id="dcd12-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="dcd12-208">**Pour vérifier les informations de l'application**</span><span class="sxs-lookup"><span data-stu-id="dcd12-208">**To verify the app information**</span></span>

* <span data-ttu-id="dcd12-209">Dans la Shared Computer Toolkit Teams, allez aux détails de **l'application App Studio** et vérifiez que toutes les informations requises sont  >   entrées correctement.</span><span class="sxs-lookup"><span data-stu-id="dcd12-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="dcd12-210">Si vous avez modifié manuellement le fichier, vérifiez que le JSON est bien défini dans l'outil manifeste de `manifest.json` l'application dans  App Studio.</span><span class="sxs-lookup"><span data-stu-id="dcd12-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="dcd12-211">**Contenu de l'onglet non affiché**</span><span class="sxs-lookup"><span data-stu-id="dcd12-211">**Tab content not displayed**</span></span>

<span data-ttu-id="dcd12-212">Vérifiez que votre application est en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="dcd12-212">Verify that your app is running.</span></span> <span data-ttu-id="dcd12-213">Si ce n'est pas le cas, allez sur le terminal et exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="dcd12-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="dcd12-214">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dcd12-214">See also</span></span>

* [<span data-ttu-id="dcd12-215">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="dcd12-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="dcd12-216">Choix d'une configuration pour tester et déboguer votre application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="dcd12-217">Création d'onglets et d'autres expériences hébergées avec le SDK client JavaScript Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="dcd12-218">Préparer la soumission d'AppSource</span><span class="sxs-lookup"><span data-stu-id="dcd12-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="dcd12-219">Développez rapidement des applications avec App Studio pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="dcd12-220">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="dcd12-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="dcd12-221">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="dcd12-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dcd12-222">Créer un onglet personnel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dcd12-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
