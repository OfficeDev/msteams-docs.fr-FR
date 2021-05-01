---
title: 'Commencer : créer et exécuter votre première application'
author: girliemac
description: Créez rapidement une Microsoft Teams qui affiche un « Hello, World! » à l'aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: 6c3d215a3f2c1aa89a9a2bf28aad081d98c6dc33
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101722"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="d48c7-104">Créer votre première application Microsoft Teams de messagerie</span><span class="sxs-lookup"><span data-stu-id="d48c7-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="d48c7-105">Ce démarrage rapide vous apprend à créer et exécuter une Microsoft Teams qui affiche « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="d48c7-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d48c7-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d48c7-106">Prerequisites</span></span>

<span data-ttu-id="d48c7-107">Avant de commencer, vous devez configurer votre client [de développement Teams et](#set-up-your-teams-development-tenant) installer vos outils Teams [développement.](#install-your-development-tools)</span><span class="sxs-lookup"><span data-stu-id="d48c7-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="d48c7-108">Configurer votre client Teams développement</span><span class="sxs-lookup"><span data-stu-id="d48c7-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="d48c7-109">Un **client** est comme un conteneur pour une organisation.</span><span class="sxs-lookup"><span data-stu-id="d48c7-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="d48c7-110">Dans Teams termes, un client est l'endroit où les personnes de cette organisation discutent, partagent des fichiers et exécutent des réunions.</span><span class="sxs-lookup"><span data-stu-id="d48c7-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="d48c7-111">En tant que développeur, vous avez besoin d'un client pour le chargement indépendant et le test Teams applications que vous construisez.</span><span class="sxs-lookup"><span data-stu-id="d48c7-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="d48c7-112">N'avez pas de client</span><span class="sxs-lookup"><span data-stu-id="d48c7-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="d48c7-113">Vous pouvez obtenir un compte Teams test gratuit, qui inclut un client qui autorise le chargement indépendant d'une application, en rejoignant le programme Microsoft 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="d48c7-114">Le processus d'inscription prend environ deux minutes.</span><span class="sxs-lookup"><span data-stu-id="d48c7-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="d48c7-115">**Pour obtenir un client**</span><span class="sxs-lookup"><span data-stu-id="d48c7-115">**To get a tenant**</span></span>

1. <span data-ttu-id="d48c7-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="d48c7-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="d48c7-117">Sélectionnez **Rejoindre maintenant** et suivez les instructions à l'écran.</span><span class="sxs-lookup"><span data-stu-id="d48c7-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="d48c7-118">Dans l'écran d'accueil, **sélectionnez Configurer l'abonnement E5.**</span><span class="sxs-lookup"><span data-stu-id="d48c7-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="d48c7-119">Configurer votre compte Microsoft 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="d48c7-120">Une fois que vous avez terminé, l'écran suivant s'affiche :</span><span class="sxs-lookup"><span data-stu-id="d48c7-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme Microsoft 365 développeur.":::

1. <span data-ttu-id="d48c7-122">Connectez-vous Teams avec votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="d48c7-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="d48c7-123">Dans le Teams client, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="d48c7-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="d48c7-124">Vérifiez que vous pouvez voir l'Télécharger une option **d'application** personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d48c7-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="d48c7-125">Si vous le faites, cela signifie que vous pouvez télécharger une version de version de chargement de version de version d'application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="d48c7-127">Avoir un client</span><span class="sxs-lookup"><span data-stu-id="d48c7-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="d48c7-128">Si vous avez déjà un client, vérifiez si vous pouvez télécharger une version de version de chargement de version Teams.</span><span class="sxs-lookup"><span data-stu-id="d48c7-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="d48c7-129">**Vérifier que vous pouvez télécharger une version de version de chargement de version de vos applications**</span><span class="sxs-lookup"><span data-stu-id="d48c7-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="d48c7-130">Dans le Teams client, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="d48c7-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="d48c7-131">Vérifiez que vous pouvez voir l'Télécharger une option **d'application** personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d48c7-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="d48c7-132">Si vous le faites, cela signifie que vous pouvez télécharger une version de version de chargement de version de version d'application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="d48c7-134">Installer vos outils de développement</span><span class="sxs-lookup"><span data-stu-id="d48c7-134">Install your development tools</span></span>

<span data-ttu-id="d48c7-135">Pour créer cette application, vous utiliserez la Teams Shared Computer Toolkit pour Visual Studio Code démarrer rapidement.</span><span class="sxs-lookup"><span data-stu-id="d48c7-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="d48c7-136">Vous pouvez également créer des Teams à l'aide de l'un de vos outils pré-utilisés.</span><span class="sxs-lookup"><span data-stu-id="d48c7-136">You can also build Teams apps with any of your preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="d48c7-137">Teams affiche le contenu de l'application uniquement par le biais de connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d48c7-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="d48c7-138">Pour déboguer certains types d'applications localement, comme un bot, vous allez apprendre à utiliser ngrok pour configurer un tunnel sécurisé entre Teams et votre application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="d48c7-139">Les applications Teams production sont hébergées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="d48c7-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="d48c7-140">**Pour installer les outils Microsoft Teams de gestion**</span><span class="sxs-lookup"><span data-stu-id="d48c7-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="d48c7-141">Installez [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="d48c7-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="d48c7-142">Si vous prévoyez de créer un bot ou une extension de messagerie, installez [ngrok](https://ngrok.com/download) et exposez votre localhost sur Internet à l'aide [de ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span><span class="sxs-lookup"><span data-stu-id="d48c7-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="d48c7-143">Installez la dernière version de [Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="d48c7-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d48c7-144">Le kit de ressources ne prend pas en charge les versions antérieures de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d48c7-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. Dans la barre d'activité de gauche, sélectionnez **Extensions.** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. <span data-ttu-id="d48c7-146">Dans **Microsoft Teams Shared Computer Toolkit,** sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="d48c7-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Illustration montrant où dans Visual Studio Code vous pouvez installer l'extension Microsoft Teams Shared Computer Toolkit.":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="d48c7-148">1. Créer votre projet d'application</span><span class="sxs-lookup"><span data-stu-id="d48c7-148">1. Create your app project</span></span>

1. <span data-ttu-id="d48c7-149">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d48c7-149">Open Visual Studio Code.</span></span>
1. Sélectionnez **Microsoft Teams Shared Computer Toolkit** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **créer une application Teams.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Capture d'écran montrant comment créer votre projet d'application avec le Visual Studio Code Teams Shared Computer Toolkit.":::
   
1. <span data-ttu-id="d48c7-152">Connectez-vous avec votre Microsoft 365 de développement.</span><span class="sxs-lookup"><span data-stu-id="d48c7-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="d48c7-153">Soit celui que vous avez créé, soit le compte que vous avez déjà qui autorise le chargement d'une version de l'application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="d48c7-154">Dans **l'écran Sélectionner un** projet, sélectionnez **Application** personnelle et **sélectionnez JS** (JavaScript) > **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d48c7-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Capture d'écran montrant comment configurer votre projet d'application avec le Visual Studio Code Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="d48c7-156">Entrez un nom pour votre application Teams de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d48c7-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Capture d'écran montrant comment ajouter un nom à votre projet d'application avec le Visual Studio Code Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="d48c7-158">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d48c7-158">Select **Finish**.</span></span> 
   <span data-ttu-id="d48c7-159">Votre projet est maintenant configuré.</span><span class="sxs-lookup"><span data-stu-id="d48c7-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="d48c7-160">2. Comprendre les composants de votre projet d'application</span><span class="sxs-lookup"><span data-stu-id="d48c7-160">2. Understand your app project components</span></span>

<span data-ttu-id="d48c7-161">Une fois que le kit de ressources a configuré votre projet d'application, vous avez les composants pour créer votre « Hello World! »</span><span class="sxs-lookup"><span data-stu-id="d48c7-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="d48c7-162">Teams application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-162">Teams app.</span></span> <span data-ttu-id="d48c7-163">Les répertoires et fichiers du projet se trouvent dans l'Explorateur Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d48c7-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Screenshot showing the scaffolding in your app project with the Visual Studio Code Teams Shared Computer Toolkit.":::

<span data-ttu-id="d48c7-165">Le kit de ressources crée automatiquement la création de la création de lacafé d'application dans le répertoire en fonction des fonctionnalités que vous avez ajoutées `src` lors de l'installation.</span><span class="sxs-lookup"><span data-stu-id="d48c7-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="d48c7-166">Étant donné que vous avez créé un onglet lors de l'installation, le fichier dans le répertoire gère l'initialisation et le `App.js` `src/components` routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="d48c7-167">Le fichier appelle également le SDK Microsoft Teams client JavaScript pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="d48c7-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="d48c7-168">3. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="d48c7-168">3. Build and run your app</span></span>

<span data-ttu-id="d48c7-169">Créez et exécutez votre application localement pour gagner du temps.</span><span class="sxs-lookup"><span data-stu-id="d48c7-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="d48c7-170">**Pour créer et exécuter votre application**</span><span class="sxs-lookup"><span data-stu-id="d48c7-170">**To build and run your app**</span></span>

1. <span data-ttu-id="d48c7-171">Dans Visual Studio Code, sélectionnez **Afficher le**  >  **terminal.**</span><span class="sxs-lookup"><span data-stu-id="d48c7-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="d48c7-172">Exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="d48c7-172">Run `npm install`.</span></span>
1. <span data-ttu-id="d48c7-173">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="d48c7-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="d48c7-174">Une **compilation réussie !**</span><span class="sxs-lookup"><span data-stu-id="d48c7-174">A **Compiled successfully!**</span></span> <span data-ttu-id="d48c7-175">s'affiche dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="d48c7-175">message appears in the terminal.</span></span> <span data-ttu-id="d48c7-176">Votre application est désormais en cours d'exécution sur votre localhost sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="d48c7-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="d48c7-177">4. Chargement d'une version de version Teams</span><span class="sxs-lookup"><span data-stu-id="d48c7-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="d48c7-178">Le chargement de version d'évaluation est le processus d'installation d'une application dans Teams qui n'a pas été approuvée par votre administrateur ou Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d48c7-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="d48c7-179">Le chargement de version test est courant lors du test et du débogage Teams applications.</span><span class="sxs-lookup"><span data-stu-id="d48c7-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="d48c7-180">Par défaut, Teams n'autorise pas le chargement de version de l'application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="d48c7-181">Vous pouvez modifier ce paramètre dans le centre d Teams'administration.</span><span class="sxs-lookup"><span data-stu-id="d48c7-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="d48c7-182">**Pour activer le chargement de version de l'application dans Teams**</span><span class="sxs-lookup"><span data-stu-id="d48c7-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="d48c7-183">Connectez-vous au [centre Microsoft 365'administration avec](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) vos informations d'identification d'administrateur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="d48c7-184">Sélectionnez **Afficher**  >  **tous les Teams**.</span><span class="sxs-lookup"><span data-stu-id="d48c7-184">Select **Show All** > **Teams**.</span></span> 

   ![image du menu centre d'administration](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="d48c7-186">L'option d'Teams peut prendre  jusqu'à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="d48c7-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="d48c7-187">Go to **Teams apps**  >  **Setup policies**  >  **Global** (Org-wide default).</span><span class="sxs-lookup"><span data-stu-id="d48c7-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![activer l'affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="d48c7-189">Activer le **basculement d'applications personnalisées** de chargement.</span><span class="sxs-lookup"><span data-stu-id="d48c7-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="d48c7-190">Sélectionnez **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="d48c7-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="d48c7-191">Votre client test autorise désormais le chargement de version test de l'application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d48c7-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="d48c7-192">Vérifiez les problèmes avant de décharger votre application à l'aide de la fonctionnalité de validation dans App Studio, qui est incluse dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="d48c7-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="d48c7-193">Corrigez les erreurs de chargement de version de l'application.</span><span class="sxs-lookup"><span data-stu-id="d48c7-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="d48c7-194">Chargement de version secondaire de votre application</span><span class="sxs-lookup"><span data-stu-id="d48c7-194">Sideload your app</span></span>

1. <span data-ttu-id="d48c7-195">Dans Visual Studio Code, ouvrez le Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d48c7-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="d48c7-196">Go to **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="d48c7-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="d48c7-197">Sélectionnez **Tester et distribuer l'installation.**  >  </span><span class="sxs-lookup"><span data-stu-id="d48c7-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Screenshot showing how to sideload your app to Teams client with the Visual Studio Code Teams Shared Computer Toolkit.":::

<span data-ttu-id="d48c7-199">**Alternativement**</span><span class="sxs-lookup"><span data-stu-id="d48c7-199">**Alternatively**</span></span>

1. <span data-ttu-id="d48c7-200">Sélectionnez la **touche F5** pour ouvrir la fenêtre du navigateur à installer.</span><span class="sxs-lookup"><span data-stu-id="d48c7-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="d48c7-201">Cela permet d'ignorer le processus d'installation dans **App Studio** et de Teams dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="d48c7-202">Dans la boîte de dialogue d'installation, **sélectionnez Ajouter** pour installer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="d48c7-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Screenshot showing how to sideload your app to Teams client.":::

   > [!Note]
   > <span data-ttu-id="d48c7-204">App Studio est également disponible en tant qu'application autonome pour Teams client.</span><span class="sxs-lookup"><span data-stu-id="d48c7-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="d48c7-205">Résoudre les problèmes de chargement de version secondaire</span><span class="sxs-lookup"><span data-stu-id="d48c7-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="d48c7-206">**Échec de l'installation**</span><span class="sxs-lookup"><span data-stu-id="d48c7-206">**Installation failed**</span></span>

<span data-ttu-id="d48c7-207">Si le message d'erreur s'affiche lors de l'installation de votre application, vérifiez que les informations de `Manifest parsing has failed` l'application sont entrées correctement.</span><span class="sxs-lookup"><span data-stu-id="d48c7-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="d48c7-208">**Pour vérifier les informations de l'application**</span><span class="sxs-lookup"><span data-stu-id="d48c7-208">**To verify the app information**</span></span>

* <span data-ttu-id="d48c7-209">Dans la Teams Shared Computer Toolkit, allez aux détails de **l'application App Studio** et vérifiez que toutes les informations requises  >   sont entrées correctement.</span><span class="sxs-lookup"><span data-stu-id="d48c7-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="d48c7-210">Si vous avez modifié manuellement le fichier, vérifiez que le JSON est bien défini dans l'outil manifeste de `manifest.json` l'application dans App Studio. </span><span class="sxs-lookup"><span data-stu-id="d48c7-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="d48c7-211">**Contenu de l'onglet non affiché**</span><span class="sxs-lookup"><span data-stu-id="d48c7-211">**Tab content not displayed**</span></span>

<span data-ttu-id="d48c7-212">Vérifiez que votre application est en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="d48c7-212">Verify that your app is running.</span></span> <span data-ttu-id="d48c7-213">Si ce n'est pas le cas, allez sur le terminal et exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="d48c7-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="d48c7-214">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d48c7-214">See also</span></span>

* [<span data-ttu-id="d48c7-215">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="d48c7-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="d48c7-216">Choix d'une configuration pour tester et déboguer votre Microsoft Teams application</span><span class="sxs-lookup"><span data-stu-id="d48c7-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="d48c7-217">Création d'onglets et d'autres expériences hébergées avec Microsoft Teams SDK client JavaScript</span><span class="sxs-lookup"><span data-stu-id="d48c7-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="d48c7-218">Préparer la soumission d'AppSource</span><span class="sxs-lookup"><span data-stu-id="d48c7-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="d48c7-219">Développez rapidement des applications avec App Studio pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d48c7-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="d48c7-220">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="d48c7-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="d48c7-221">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="d48c7-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d48c7-222">Créer un onglet personnel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d48c7-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
