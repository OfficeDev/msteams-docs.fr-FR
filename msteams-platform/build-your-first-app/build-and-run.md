---
title: Prise en main-créer et exécuter votre première application
author: heath-hamilton
description: Créez rapidement une application Microsoft teams qui affiche un « Hello, World ! ». message à l’aide de Microsoft teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 2d357ef71bfc4c498b54d94f9d0717cf886df17d
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552478"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="45caa-104">Créer et exécuter votre première application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="45caa-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="45caa-105">Vous pouvez accéder directement au développement Microsoft teams en créant un onglet personnel qui affiche « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="45caa-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="45caa-106">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="45caa-106">1. Create your app project</span></span>

<span data-ttu-id="45caa-107">Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="45caa-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="45caa-109">Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="45caa-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="45caa-110">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="45caa-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran indiquant comment configurer votre projet d’application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="45caa-112">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="45caa-113">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="45caa-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="45caa-114">Activez uniquement l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="45caa-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

> [!NOTE]

> <span data-ttu-id="45caa-115">Pour installer votre package d’application après avoir créé un nouveau projet dans la boîte à outils, appuyez sur F5/exécuter.</span><span class="sxs-lookup"><span data-stu-id="45caa-115">To install your app package after creating a new project in the toolkit, press F5/run.</span></span> <span data-ttu-id="45caa-116">Il lancera chrome et installera votre package.</span><span class="sxs-lookup"><span data-stu-id="45caa-116">It will launch Chrome and install your package.</span></span> <span data-ttu-id="45caa-117">Le package est stocké dans App Studio et installé à l’aide du `appId` .</span><span class="sxs-lookup"><span data-stu-id="45caa-117">The package is stored in App Studio and installed using the `appId`.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="45caa-118">2. comprendre les composants importants du projet d’application</span><span class="sxs-lookup"><span data-stu-id="45caa-118">2. Understand important app project components</span></span>

<span data-ttu-id="45caa-119">Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-119">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="45caa-120">Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="45caa-120">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran illustrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="45caa-122">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="45caa-122">App scaffolding</span></span>

<span data-ttu-id="45caa-123">Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="45caa-123">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="45caa-124">Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="45caa-124">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="45caa-125">Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-125">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="45caa-126">ID de l’application</span><span class="sxs-lookup"><span data-stu-id="45caa-126">App ID</span></span>

<span data-ttu-id="45caa-127">L’ID d’application de teams est nécessaire pour configurer votre application avec App Studio.</span><span class="sxs-lookup"><span data-stu-id="45caa-127">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="45caa-128">Vous pouvez trouver l’ID dans l' `teamsAppId` objet, qui se trouve dans le fichier de votre projet `package.json` .</span><span class="sxs-lookup"><span data-stu-id="45caa-128">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="45caa-129">3. générez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="45caa-129">3. Build and run your app</span></span>

<span data-ttu-id="45caa-130">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="45caa-130">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="45caa-131">(Ces informations sont également disponibles dans la boîte à outils `README` .)</span><span class="sxs-lookup"><span data-stu-id="45caa-131">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="45caa-132">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="45caa-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="45caa-133">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="45caa-133">Run `npm start`.</span></span>

<span data-ttu-id="45caa-134">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="45caa-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="45caa-135">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="45caa-135">message in the terminal.</span></span> <span data-ttu-id="45caa-136">Votre application est en cours d’exécution sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="45caa-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="45caa-137">4. chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="45caa-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="45caa-138">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="45caa-139">Pour ce faire, vous devez disposer d’un compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="45caa-139">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="45caa-140">(Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="45caa-140">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="45caa-141">Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation dans App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), qui est incluse dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="45caa-141">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="45caa-142">Les erreurs doivent être résolues pour chargement l’application.</span><span class="sxs-lookup"><span data-stu-id="45caa-142">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="45caa-143">Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-143">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="45caa-144">Pour afficher le contenu de votre application dans Teams, spécifiez le lieu de fiabilité de votre application ( `localhost` ).</span><span class="sxs-lookup"><span data-stu-id="45caa-144">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="45caa-145">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyé sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="45caa-145">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="45caa-146">Accédez à `https://localhost:3000/tab` la page et passez à la page.</span><span class="sxs-lookup"><span data-stu-id="45caa-146">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="45caa-147">Revenir à Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-147">Go back to Teams.</span></span> <span data-ttu-id="45caa-148">Dans la boîte de dialogue, sélectionnez **Ajouter pour moi** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="45caa-148">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran illustrant un exemple d’application d’onglet personnelle « Hello, World ! » en cours d’exécution dans Teams.":::

<span data-ttu-id="45caa-150">🎉 Félicitations !</span><span class="sxs-lookup"><span data-stu-id="45caa-150">🎉 Congratulations!</span></span> <span data-ttu-id="45caa-151">Votre application est en cours d’exécution dans Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-151">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="45caa-152">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="45caa-152">Next step</span></span>

<span data-ttu-id="45caa-153">Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="45caa-153">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="45caa-154">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="45caa-154">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="45caa-155">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="45caa-155">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="45caa-156">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="45caa-156">Build a bot</span></span>](../build-your-first-app/build-bot.md)
