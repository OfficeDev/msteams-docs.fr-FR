---
title: Prise en main-créer et exécuter votre première application
author: heath-hamilton
description: Créez rapidement une application Microsoft teams qui affiche un « Hello, World ! ». message à l’aide de Microsoft teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931775"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="1d8d5-104">Créer et exécuter votre première application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="1d8d5-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="1d8d5-105">Vous pouvez accéder directement au développement Microsoft teams en créant un onglet personnel qui affiche « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="1d8d5-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="1d8d5-106">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="1d8d5-106">1. Create your app project</span></span>

<span data-ttu-id="1d8d5-107">Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="1d8d5-109">Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="1d8d5-110">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran indiquant comment configurer votre projet d’application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="1d8d5-112">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="1d8d5-113">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="1d8d5-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="1d8d5-114">Activez uniquement l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="1d8d5-115">2. comprendre les composants importants du projet d’application</span><span class="sxs-lookup"><span data-stu-id="1d8d5-115">2. Understand important app project components</span></span>

<span data-ttu-id="1d8d5-116">Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="1d8d5-117">Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran illustrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="1d8d5-119">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="1d8d5-119">App scaffolding</span></span>

<span data-ttu-id="1d8d5-120">Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="1d8d5-121">Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="1d8d5-122">Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-122">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="1d8d5-123">ID de l’application</span><span class="sxs-lookup"><span data-stu-id="1d8d5-123">App ID</span></span>

<span data-ttu-id="1d8d5-124">L’ID d’application de teams est nécessaire pour configurer votre application avec App Studio.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="1d8d5-125">Vous pouvez trouver l’ID dans l' `teamsAppId` objet, qui se trouve dans le fichier de votre projet `package.json` .</span><span class="sxs-lookup"><span data-stu-id="1d8d5-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="1d8d5-126">3. générez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="1d8d5-126">3. Build and run your app</span></span>

<span data-ttu-id="1d8d5-127">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="1d8d5-128">(Ces informations sont également disponibles dans la boîte à outils `README` .)</span><span class="sxs-lookup"><span data-stu-id="1d8d5-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="1d8d5-129">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="1d8d5-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="1d8d5-130">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="1d8d5-130">Run `npm start`.</span></span>

<span data-ttu-id="1d8d5-131">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="1d8d5-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="1d8d5-132">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-132">message in the terminal.</span></span> <span data-ttu-id="1d8d5-133">Votre application est en cours d’exécution sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="1d8d5-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="1d8d5-134">4. chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="1d8d5-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="1d8d5-135">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="1d8d5-136">Pour ce faire, vous devez disposer d’un compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="1d8d5-137">(Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="1d8d5-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="1d8d5-138">Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation dans App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), qui est incluse dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="1d8d5-139">Les erreurs doivent être résolues pour chargement l’application.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="1d8d5-140">Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="1d8d5-141">Pour afficher le contenu de votre application dans Teams, spécifiez le lieu de fiabilité de votre application ( `localhost` ).</span><span class="sxs-lookup"><span data-stu-id="1d8d5-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="1d8d5-142">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyé sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="1d8d5-143">Accédez à `https://localhost:3000/tab` la page et passez à la page.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="1d8d5-144">Revenir à Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-144">Go back to Teams.</span></span> <span data-ttu-id="1d8d5-145">Dans la boîte de dialogue, sélectionnez **Ajouter pour moi** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran illustrant un exemple d’application d’onglet personnelle « Hello, World ! » en cours d’exécution dans Teams.":::

<span data-ttu-id="1d8d5-147">🎉 Félicitations !</span><span class="sxs-lookup"><span data-stu-id="1d8d5-147">🎉 Congratulations!</span></span> <span data-ttu-id="1d8d5-148">Votre application est en cours d’exécution dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="1d8d5-149">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1d8d5-149">Next step</span></span>

<span data-ttu-id="1d8d5-150">Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="1d8d5-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d8d5-151">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="1d8d5-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1d8d5-152">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="1d8d5-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1d8d5-153">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="1d8d5-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
