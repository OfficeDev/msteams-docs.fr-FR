---
title: Prise en main-créer et exécuter votre première application
author: heath-hamilton
description: Créez rapidement une application Microsoft teams qui affiche un « Hello, World ! ». message à l’aide de Microsoft teams Toolkit.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: quickstart
ms.openlocfilehash: 20c9eee14649cda23e1d682940f489e78cba24b9
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452644"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="b73d0-104">Créer et exécuter votre première application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="b73d0-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="b73d0-105">Vous pouvez accéder directement au développement Microsoft teams en créant un onglet personnel qui affiche « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="b73d0-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="b73d0-106">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="b73d0-106">1. Create your app project</span></span>

<span data-ttu-id="b73d0-107">Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="b73d0-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="b73d0-110">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-110">Enter a name for your Teams app.</span></span> <span data-ttu-id="b73d0-111">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="b73d0-111">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="b73d0-112">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b73d0-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="b73d0-114">Activez l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="b73d0-114">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="b73d0-115">2. comprendre les composants importants du projet d’application</span><span class="sxs-lookup"><span data-stu-id="b73d0-115">2. Understand important app project components</span></span>

<span data-ttu-id="b73d0-116">Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="b73d0-117">Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="b73d0-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::

<span data-ttu-id="b73d0-119">Nous allons prendre quelques instants pour comprendre quelques-uns des principaux fichiers que les développeurs d’applications teams utilisent.</span><span class="sxs-lookup"><span data-stu-id="b73d0-119">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="b73d0-120">Manifeste de l’application ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="b73d0-120">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="b73d0-121">Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application.</span><span class="sxs-lookup"><span data-stu-id="b73d0-121">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="b73d0-122">Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="b73d0-122">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="b73d0-123">Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.</span><span class="sxs-lookup"><span data-stu-id="b73d0-123">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="b73d0-124">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="b73d0-124">App scaffolding</span></span>

<span data-ttu-id="b73d0-125">Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="b73d0-125">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="b73d0-126">Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="b73d0-126">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="b73d0-127">Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-127">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="b73d0-128">Package d’application ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="b73d0-128">App package (`Development.zip`)</span></span>

<span data-ttu-id="b73d0-129">Situé dans l' `.publish` annuaire, vous avez besoin du package d’application pour [chargement votre application](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-129">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="b73d0-130">Le package est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) ou [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="b73d0-130">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="b73d0-131">Voici quelques détails sur les fichiers de package d’application :</span><span class="sxs-lookup"><span data-stu-id="b73d0-131">Here are some details about the app package files:</span></span>

|<span data-ttu-id="b73d0-132">Nom</span><span class="sxs-lookup"><span data-stu-id="b73d0-132">Name</span></span>|<span data-ttu-id="b73d0-133">Type</span><span class="sxs-lookup"><span data-stu-id="b73d0-133">Type</span></span>|<span data-ttu-id="b73d0-134">Size</span><span class="sxs-lookup"><span data-stu-id="b73d0-134">Size</span></span>|<span data-ttu-id="b73d0-135">Emplacement du manifeste</span><span class="sxs-lookup"><span data-stu-id="b73d0-135">Manifest location</span></span>|<span data-ttu-id="b73d0-136">Nom de fichier du Toolkit</span><span class="sxs-lookup"><span data-stu-id="b73d0-136">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="b73d0-137">**Manifeste de l’application**</span><span class="sxs-lookup"><span data-stu-id="b73d0-137">**App manifest**</span></span>|`.json`| <span data-ttu-id="b73d0-138">—</span><span class="sxs-lookup"><span data-stu-id="b73d0-138">—</span></span> | <span data-ttu-id="b73d0-139">—</span><span class="sxs-lookup"><span data-stu-id="b73d0-139">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="b73d0-140">**Logo couleur**</span><span class="sxs-lookup"><span data-stu-id="b73d0-140">**Color logo**</span></span>|`.png`|<span data-ttu-id="b73d0-141">192 &times; 192 pixels</span><span class="sxs-lookup"><span data-stu-id="b73d0-141">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="b73d0-142">**Logo de plan**</span><span class="sxs-lookup"><span data-stu-id="b73d0-142">**Outline logo**</span></span>|`.png`|<span data-ttu-id="b73d0-143">32 &times; 32 pixels</span><span class="sxs-lookup"><span data-stu-id="b73d0-143">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a><span data-ttu-id="b73d0-144">3. exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="b73d0-144">3. Run your app</span></span>

<span data-ttu-id="b73d0-145">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="b73d0-145">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="b73d0-146">(Ces informations sont également disponibles dans la boîte à outils `README` .)</span><span class="sxs-lookup"><span data-stu-id="b73d0-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="b73d0-147">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="b73d0-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="b73d0-148">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="b73d0-148">Run `npm start`.</span></span> <span data-ttu-id="b73d0-149">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="b73d0-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="b73d0-150">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="b73d0-150">message in the terminal.</span></span>
1. <span data-ttu-id="b73d0-151">Ouvrez un navigateur et accédez à `https://localhost:3000` la page Web vierge intitulée **Microsoft teams**. (Ne vous inquiétez pas que vous ne pouvez pas voir le contenu sur la page.)</span><span class="sxs-lookup"><span data-stu-id="b73d0-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="b73d0-153">4. configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="b73d0-153">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="b73d0-154">Votre application est en cours d’exécution sur votre serveur Web local.</span><span class="sxs-lookup"><span data-stu-id="b73d0-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="b73d0-155">Pour exécuter votre application dans Teams, vous devez faire en sorte qu’elle soit `localhost` accessible via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b73d0-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="b73d0-156">Installez [ngrok](https://ngrok.com/download) si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="b73d0-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="b73d0-157">Lorsque vous exécutez cet outil, vous créez deux URL globalement disponibles qui pointent vers votre serveur Web local ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="b73d0-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="b73d0-158">Vous avez besoin de l’URL de transfert qui commence par `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="b73d0-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="b73d0-159">Ouvrez un nouveau terminal et exécutez `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="b73d0-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="b73d0-160">Copiez l’URL HTTPs que vous avez fournie (Voir l’exemple ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b73d0-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="b73d0-162">Dans votre `.publish` répertoire, ouvrez `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="b73d0-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="b73d0-163">Remplacez la `baseUrl0` valeur par l’URL copiée.</span><span class="sxs-lookup"><span data-stu-id="b73d0-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="b73d0-164">(Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ba5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="b73d0-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="b73d0-165">Le manifeste de votre application pointe maintenant vers l’emplacement où vous hébergez l’application.</span><span class="sxs-lookup"><span data-stu-id="b73d0-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="5-sideload-your-app-in-teams"></a><span data-ttu-id="b73d0-166">5. chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="b73d0-166">5. Sideload your app in Teams</span></span>

<span data-ttu-id="b73d0-167">Une fois que votre application est en cours d’exécution et accessible via HTTPs, vous êtes prêt à la télécharger vers Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="b73d0-168">Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation de la boîte à outils](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="b73d0-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="b73d0-169">Les erreurs doivent être résolues pour chargement l’application.</span><span class="sxs-lookup"><span data-stu-id="b73d0-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="b73d0-170">Connectez-vous au client teams avec votre compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="b73d0-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="b73d0-171">(Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="b73d0-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="b73d0-172">Sélectionnez **applications**, puis **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="b73d0-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="b73d0-173">Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="b73d0-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="b73d0-174">Une installation modale d’installation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b73d0-174">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="b73d0-176">Sélectionnez **Ajouter** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="b73d0-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::

<span data-ttu-id="b73d0-178">🎉 Félicitations !</span><span class="sxs-lookup"><span data-stu-id="b73d0-178">🎉 Congratulations!</span></span> <span data-ttu-id="b73d0-179">Votre application est en cours d’exécution dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="b73d0-180">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b73d0-180">Next step</span></span>

<span data-ttu-id="b73d0-181">Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="b73d0-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b73d0-182">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="b73d0-182">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="b73d0-183">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="b73d0-183">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="b73d0-184">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="b73d0-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)
