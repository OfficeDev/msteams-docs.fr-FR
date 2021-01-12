---
title: 'Commencer : créer et exécuter votre première application'
author: heath-hamilton
description: Créez rapidement une application Microsoft Teams qui affiche un « Hello, World! » à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: bc5d18dd887cbdbf56b8d6d013f53c21d1540370
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795467"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="9a91d-104">Créer et exécuter votre première application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9a91d-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="9a91d-105">Vous pouvez vous lancer directement dans le développement Microsoft Teams en construisant un onglet personnel qui affiche « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="9a91d-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="9a91d-106">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="9a91d-106">1. Create your app project</span></span>

<span data-ttu-id="9a91d-107">Utilisez la Shared Computer Toolkit Microsoft Teams Visual Studio code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="9a91d-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="9a91d-109">Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="9a91d-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="9a91d-110">Dans **l’écran Ajouter des fonctionnalités,** sélectionnez **Onglet,** puis **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9a91d-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran montrant comment configurer votre projet d’application avec la Visual Studio Code Teams Shared Computer Toolkit.":::
1. <span data-ttu-id="9a91d-112">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="9a91d-113">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="9a91d-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="9a91d-114">Cochez uniquement **l’option Onglet** Personnel et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="9a91d-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="9a91d-115">2. Comprendre les composants importants d’un projet d’application</span><span class="sxs-lookup"><span data-stu-id="9a91d-115">2. Understand important app project components</span></span>

<span data-ttu-id="9a91d-116">Une fois que le kit de ressources a configuré votre projet, vous avez les composants pour créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="9a91d-117">Les répertoires et fichiers du projet s’affichent dans la zone Explorateur de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9a91d-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran montrant les fichiers de projet d’application pour un onglet personnel Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="9a91d-119">Échafaudage d’application</span><span class="sxs-lookup"><span data-stu-id="9a91d-119">App scaffolding</span></span>

<span data-ttu-id="9a91d-120">Le kit de ressources crée automatiquement la création de la forme dans le répertoire en fonction des fonctionnalités que vous avez ajoutées lors de `src` l’installation.</span><span class="sxs-lookup"><span data-stu-id="9a91d-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="9a91d-121">Si vous créez un onglet lors de l’installation, par exemple, le fichier dans le répertoire est important car il gère l’initialisation et le `App.js` `src/components` routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="9a91d-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="9a91d-122">Il appelle le [SDK client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-122">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="9a91d-123">ID de l’application</span><span class="sxs-lookup"><span data-stu-id="9a91d-123">App ID</span></span>

<span data-ttu-id="9a91d-124">Votre ID d’application Teams est nécessaire pour configurer votre application avec App Studio.</span><span class="sxs-lookup"><span data-stu-id="9a91d-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="9a91d-125">Vous pouvez trouver l’ID dans `teamsAppId` l’objet, qui se trouve dans le fichier de votre `package.json` projet.</span><span class="sxs-lookup"><span data-stu-id="9a91d-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="9a91d-126">3. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="9a91d-126">3. Build and run your app</span></span>

<span data-ttu-id="9a91d-127">Dans l’intérêt du temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="9a91d-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="9a91d-128">(Ces informations sont également disponibles dans le kit de `README` ressources.)</span><span class="sxs-lookup"><span data-stu-id="9a91d-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="9a91d-129">Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="9a91d-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="9a91d-130">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="9a91d-130">Run `npm start`.</span></span>

<span data-ttu-id="9a91d-131">Une fois terminé, une compilation a **réussi !**</span><span class="sxs-lookup"><span data-stu-id="9a91d-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="9a91d-132">dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="9a91d-132">message in the terminal.</span></span> <span data-ttu-id="9a91d-133">Votre application est en cours d’exécution sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="9a91d-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="9a91d-134">4. Chargement de version secondaire de votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="9a91d-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="9a91d-135">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="9a91d-136">Pour ce faire, vous devez avoir un compte qui autorise le chargement de version de version d’application.</span><span class="sxs-lookup"><span data-stu-id="9a91d-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="9a91d-137">(Si vous n’êtes pas sûr de l’avoir, découvrez comment obtenir un compte [de développement Teams.)](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="9a91d-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="9a91d-138">Avant de recharger une version indépendante de votre application, recherchez les problèmes à l’aide de la fonctionnalité de validation dans [App Studio,](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)qui est incluse dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="9a91d-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="9a91d-139">Les erreurs doivent être corrigées pour que le chargement de version de l’application réussisse.</span><span class="sxs-lookup"><span data-stu-id="9a91d-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="9a91d-140">Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="9a91d-141">Pour afficher le contenu de votre application dans Teams, spécifiez que l’endroit où votre application est en cours d’exécution ( `localhost` ) est digne de confiance :</span><span class="sxs-lookup"><span data-stu-id="9a91d-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="9a91d-142">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="9a91d-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="9a91d-143">Go to `https://localhost:3000/tab` and proceed to the page.</span><span class="sxs-lookup"><span data-stu-id="9a91d-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="9a91d-144">Revenir à Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-144">Go back to Teams.</span></span> <span data-ttu-id="9a91d-145">Dans la boîte de dialogue, **sélectionnez Ajouter pour moi** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="9a91d-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran montrant un exemple d’application d’onglet personnel « Hello, World! » en cours d’exécution dans Teams.":::

<span data-ttu-id="9a91d-147">🎉 félicitations !</span><span class="sxs-lookup"><span data-stu-id="9a91d-147">🎉 Congratulations!</span></span> <span data-ttu-id="9a91d-148">Votre application s’exécute dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="9a91d-149">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="9a91d-149">Next step</span></span>

<span data-ttu-id="9a91d-150">Développez l’onglet personnel que vous avez créé ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="9a91d-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a91d-151">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="9a91d-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="9a91d-152">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="9a91d-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="9a91d-153">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="9a91d-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
