---
title: Créer et exécuter un « Hello, World ! » Application Teams
author: heath-hamilton
description: Créez et exécutez votre première application Microsoft Teams, un onglet personnel qui affiche « Hello, World ! ».
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 5be2e8f2932a91ed11137f3a7be544e12bd65559
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210150"
---
# <a name="build-a-hello-world-teams-app"></a><span data-ttu-id="eb522-104">Créer un « Hello, World ! »</span><span class="sxs-lookup"><span data-stu-id="eb522-104">Build a "Hello, World!"</span></span> <span data-ttu-id="eb522-105">Application Teams</span><span class="sxs-lookup"><span data-stu-id="eb522-105">Teams app</span></span>

<span data-ttu-id="eb522-106">Vous pouvez accéder directement au développement de la plateforme Microsoft teams en créant un onglet personnel qui affiche « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="eb522-106">You can jump right into Microsoft Teams platform development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="eb522-107">Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="eb522-107">Create your app project</span></span>

<span data-ttu-id="eb522-108">Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="eb522-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Capture d’écran montrant comment créer une nouvelle application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="eb522-111">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-111">Enter a name for your Teams app.</span></span> <span data-ttu-id="eb522-112">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="eb522-112">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="eb522-113">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb522-113">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Capture d’écran indiquant comment configurer votre projet d’application avec Visual Studio code teams Toolkit.":::
1. <span data-ttu-id="eb522-115">Activez l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="eb522-115">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="eb522-116">Comprendre les composants importants du projet d’application</span><span class="sxs-lookup"><span data-stu-id="eb522-116">Understand important app project components</span></span>

<span data-ttu-id="eb522-117">Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-117">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="eb522-118">Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="eb522-118">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Capture d’écran illustrant les fichiers de projet d’application pour un onglet personnel dans Visual Studio code.":::

<span data-ttu-id="eb522-120">Nous allons prendre quelques instants pour comprendre quelques-uns des principaux fichiers que les développeurs d’applications teams utilisent.</span><span class="sxs-lookup"><span data-stu-id="eb522-120">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="eb522-121">Manifeste de l’application ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="eb522-121">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="eb522-122">Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application.</span><span class="sxs-lookup"><span data-stu-id="eb522-122">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="eb522-123">Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="eb522-123">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="eb522-124">Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.</span><span class="sxs-lookup"><span data-stu-id="eb522-124">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="eb522-125">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="eb522-125">App scaffolding</span></span>

<span data-ttu-id="eb522-126">Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="eb522-126">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="eb522-127">Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="eb522-127">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="eb522-128">Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-128">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="eb522-129">Package d’application ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="eb522-129">App package (`Development.zip`)</span></span>

<span data-ttu-id="eb522-130">Situé dans l' `.publish` annuaire, vous avez besoin du package d’application pour [chargement votre application](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) dans Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-130">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="eb522-131">Le package est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) ou [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="eb522-131">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="eb522-132">Voici quelques détails sur les fichiers de package d’application :</span><span class="sxs-lookup"><span data-stu-id="eb522-132">Here are some details about the app package files:</span></span>

|<span data-ttu-id="eb522-133">Nom</span><span class="sxs-lookup"><span data-stu-id="eb522-133">Name</span></span>|<span data-ttu-id="eb522-134">Type</span><span class="sxs-lookup"><span data-stu-id="eb522-134">Type</span></span>|<span data-ttu-id="eb522-135">Size</span><span class="sxs-lookup"><span data-stu-id="eb522-135">Size</span></span>|<span data-ttu-id="eb522-136">Emplacement du manifeste</span><span class="sxs-lookup"><span data-stu-id="eb522-136">Manifest location</span></span>|<span data-ttu-id="eb522-137">Nom de fichier du Toolkit</span><span class="sxs-lookup"><span data-stu-id="eb522-137">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="eb522-138">**Manifeste de l’application**</span><span class="sxs-lookup"><span data-stu-id="eb522-138">**App manifest**</span></span>|`.json`| <span data-ttu-id="eb522-139">—</span><span class="sxs-lookup"><span data-stu-id="eb522-139">—</span></span> | <span data-ttu-id="eb522-140">—</span><span class="sxs-lookup"><span data-stu-id="eb522-140">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="eb522-141">**Logo couleur**</span><span class="sxs-lookup"><span data-stu-id="eb522-141">**Color logo**</span></span>|`.png`|<span data-ttu-id="eb522-142">192 &times; 192 pixels</span><span class="sxs-lookup"><span data-stu-id="eb522-142">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="eb522-143">**Logo de plan**</span><span class="sxs-lookup"><span data-stu-id="eb522-143">**Outline logo**</span></span>|`.png`|<span data-ttu-id="eb522-144">32 &times; 32 pixels</span><span class="sxs-lookup"><span data-stu-id="eb522-144">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="eb522-145">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="eb522-145">Run your app</span></span>

<span data-ttu-id="eb522-146">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="eb522-146">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="eb522-147">(Ces informations sont également disponibles dans la boîte à outils `README` .)</span><span class="sxs-lookup"><span data-stu-id="eb522-147">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="eb522-148">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="eb522-148">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="eb522-149">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="eb522-149">Run `npm start`.</span></span> <span data-ttu-id="eb522-150">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="eb522-150">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="eb522-151">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="eb522-151">message in the terminal.</span></span>
1. <span data-ttu-id="eb522-152">Ouvrez un navigateur et accédez à `https://localhost:3000` la page Web vierge intitulée **Microsoft teams**. (Ne vous inquiétez pas que vous ne pouvez pas voir le contenu sur la page.)</span><span class="sxs-lookup"><span data-stu-id="eb522-152">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Capture d’écran illustrant l’apparence de votre application en cours d’exécution dans un navigateur.":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="eb522-154">Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="eb522-154">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="eb522-155">Votre application est en cours d’exécution sur votre serveur Web local.</span><span class="sxs-lookup"><span data-stu-id="eb522-155">Your app is up and running on your local web server.</span></span> <span data-ttu-id="eb522-156">Pour exécuter votre application dans Teams, vous devez faire en sorte qu’elle soit `localhost` accessible via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb522-156">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="eb522-157">Installez [ngrok](https://ngrok.com/download) si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="eb522-157">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="eb522-158">Lorsque vous exécutez cet outil, vous créez deux URL globalement disponibles qui pointent vers votre serveur Web local ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="eb522-158">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="eb522-159">Vous avez besoin de l’URL de transfert qui commence par `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="eb522-159">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="eb522-160">Ouvrez un nouveau terminal et exécutez `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="eb522-160">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="eb522-161">Copiez l’URL HTTPs que vous avez fournie (Voir l’exemple ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="eb522-161">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Capture d’écran illustrant un terminal avec ngrok en cours d’exécution.":::
1. <span data-ttu-id="eb522-163">Dans votre `.publish` répertoire, ouvrez `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="eb522-163">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="eb522-164">Remplacez la `baseUrl0` valeur par l’URL copiée.</span><span class="sxs-lookup"><span data-stu-id="eb522-164">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="eb522-165">(Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ba5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="eb522-165">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="eb522-166">Le manifeste de votre application pointe maintenant vers l’emplacement où vous hébergez l’application.</span><span class="sxs-lookup"><span data-stu-id="eb522-166">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="eb522-167">Chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="eb522-167">Sideload your app in Teams</span></span>

<span data-ttu-id="eb522-168">Une fois que votre application est en cours d’exécution et accessible via HTTPs, vous êtes prêt à la télécharger vers Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-168">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="eb522-169">Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation de la boîte à outils](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="eb522-169">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="eb522-170">Les erreurs doivent être résolues pour chargement l’application.</span><span class="sxs-lookup"><span data-stu-id="eb522-170">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="eb522-171">Connectez-vous au client teams avec votre compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="eb522-171">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="eb522-172">(Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="eb522-172">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="eb522-173">Sélectionnez **applications**, puis **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="eb522-173">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="eb522-174">Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="eb522-174">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="eb522-175">Une installation modale d’installation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="eb522-175">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Capture d’écran illustrant un exemple d’installation de l’application teams modale.":::
1. <span data-ttu-id="eb522-177">Sélectionnez **Ajouter** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="eb522-177">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Capture d’écran illustrant un exemple d’application d’onglet personnelle « Hello, World ! » en cours d’exécution dans Teams.":::

<span data-ttu-id="eb522-179">🎉 Félicitations !</span><span class="sxs-lookup"><span data-stu-id="eb522-179">🎉 Congratulations!</span></span> <span data-ttu-id="eb522-180">Votre application est en cours d’exécution dans Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-180">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="eb522-181">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="eb522-181">Next step</span></span>

<span data-ttu-id="eb522-182">Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="eb522-182">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb522-183">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="eb522-183">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="eb522-184">Onglet créer un canal</span><span class="sxs-lookup"><span data-stu-id="eb522-184">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="eb522-185">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="eb522-185">Build a bot</span></span>](../build-your-first-app/build-bot.md)
