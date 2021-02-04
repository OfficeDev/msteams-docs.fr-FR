---
title: 'Commencer : créer et exécuter votre première application'
author: heath-hamilton
description: Créez rapidement une application Microsoft Teams qui affiche un « Hello, World! » à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093949"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="e0ef4-104">Créer et exécuter votre première application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e0ef4-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="e0ef4-105">Démarrez le développement de Microsoft Teams en construisant un onglet personnel qui affiche « Hello, World! ».</span><span class="sxs-lookup"><span data-stu-id="e0ef4-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="e0ef4-106">Créez et exécutez votre première application Teams en suivant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0ef4-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="e0ef4-107">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="e0ef4-107">1. Create your app project</span></span>

<span data-ttu-id="e0ef4-108">Utilisez la Shared Computer Toolkit Microsoft Teams Visual Studio Code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="e0ef4-109">Créez votre projet d’application en suivant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0ef4-109">Create your app project using the following steps:</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="e0ef4-111">Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="e0ef4-112">Dans **l’écran Ajouter des fonctionnalités,** **sélectionnez Onglet,** puis **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran montrant comment configurer votre projet d’application avec la Visual Studio Code Teams Shared Computer Toolkit.":::
1. <span data-ttu-id="e0ef4-114">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="e0ef4-115">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="e0ef4-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="e0ef4-116">Cochez uniquement **l’option Onglet** Personnel et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="e0ef4-117">2. Comprendre les composants importants d’un projet d’application</span><span class="sxs-lookup"><span data-stu-id="e0ef4-117">2. Understand important app project components</span></span>

<span data-ttu-id="e0ef4-118">Une fois que le kit de ressources a configuré votre projet, vous avez les composants pour créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="e0ef4-119">Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="e0ef4-121">Échafaudage d’application</span><span class="sxs-lookup"><span data-stu-id="e0ef4-121">App scaffolding</span></span>

<span data-ttu-id="e0ef4-122">Le kit de ressources crée automatiquement la création de la forme dans le répertoire en fonction des fonctionnalités que vous avez ajoutées lors de `src` l’installation.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="e0ef4-123">Si vous créez un onglet lors de l’installation, par exemple, le fichier dans le répertoire est important car il gère l’initialisation et le `App.js` `src/components` routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="e0ef4-124">Il appelle le [SDK client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="e0ef4-125">ID de l’application</span><span class="sxs-lookup"><span data-stu-id="e0ef4-125">App ID</span></span>

<span data-ttu-id="e0ef4-126">Configurez votre application avec App Studio à l’aide de l’ID d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="e0ef4-127">Recherchez l’ID dans `teamsAppId` l’objet, qui se trouve dans le fichier de votre `package.json` projet.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="e0ef4-128">3. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="e0ef4-128">3. Build and run your app</span></span>

<span data-ttu-id="e0ef4-129">Créez et exécutez votre application localement pour gagner du temps.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="e0ef4-130">Ces informations sont également disponibles dans le kit de `README` ressources.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="e0ef4-131">Créez et exécutez votre application en suivant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0ef4-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="e0ef4-132">Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="e0ef4-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="e0ef4-133">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="e0ef4-133">Run `npm start`.</span></span>

<span data-ttu-id="e0ef4-134">Une fois terminé, une compilation a **réussi !**</span><span class="sxs-lookup"><span data-stu-id="e0ef4-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="e0ef4-135">dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-135">message in the terminal.</span></span> <span data-ttu-id="e0ef4-136">Votre application est en cours d’exécution sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="e0ef4-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="e0ef4-137">4. Chargement de version secondaire de votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="e0ef4-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="e0ef4-138">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="e0ef4-139">Pour ce faire, vous devez avoir un compte de développement Microsoft 365 qui autorise le chargement de version de version d’application.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="e0ef4-140">Pour plus d’informations sur l’ouverture de compte, voir [le compte de développement Teams.](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="e0ef4-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="e0ef4-141">Recherchez les problèmes avant de recharger une version indépendante de votre application, à l’aide de la fonctionnalité de validation dans [App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)qui est incluse dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="e0ef4-142">Corrigez les erreurs de chargement de version de l’application.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="e0ef4-143">Chargez une version de votre application dans Teams en suivant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0ef4-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="e0ef4-144">Pour activer le chargement de version sideloading avant de charger une version de version de votre application dans Teams, suivez les étapes de l’étape Activer le chargement de version [de l’application.](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)</span><span class="sxs-lookup"><span data-stu-id="e0ef4-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="e0ef4-145">Sélectionnez **la touche F5** pour lancer un client web Teams dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="e0ef4-146">Pour afficher le contenu de votre application dans Teams, spécifiez que l’endroit où votre application est en cours d’exécution ( `localhost` ) est digne de confiance :</span><span class="sxs-lookup"><span data-stu-id="e0ef4-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="e0ef4-147">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="e0ef4-148">Go to `https://localhost:3000/tab` and proceed to the page.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="e0ef4-149">Revenir à Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-149">Go back to Teams.</span></span> <span data-ttu-id="e0ef4-150">Dans la boîte de dialogue, **sélectionnez Ajouter pour moi** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran montrant un exemple d’application d’onglet personnel « Hello, World! » en cours d’exécution dans Teams.":::

<span data-ttu-id="e0ef4-152">🎉 félicitations !</span><span class="sxs-lookup"><span data-stu-id="e0ef4-152">🎉 Congratulations!</span></span> <span data-ttu-id="e0ef4-153">Votre application s’exécute dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="e0ef4-154">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e0ef4-154">Next step</span></span>

<span data-ttu-id="e0ef4-155">Développez l’onglet personnel que vous avez créé ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="e0ef4-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e0ef4-156">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="e0ef4-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e0ef4-157">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="e0ef4-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e0ef4-158">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="e0ef4-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)
