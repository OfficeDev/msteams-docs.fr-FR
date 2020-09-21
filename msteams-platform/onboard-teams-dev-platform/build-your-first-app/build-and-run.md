---
title: Créer et exécuter une application de première équipe
author: heath-hamilton
ms.author: lajanuar
description: Exécutez votre première application Microsoft Teams.
ms.date: 08/31/2020
ms.topic: quickstart
ms.openlocfilehash: 441b70480d9c177e9c6140342df8c9ea29494a29
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964655"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="93287-103">Créer et exécuter votre première application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="93287-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="93287-104">Vous pouvez accéder directement au développement sur la plateforme Microsoft teams en créant et en exécutant rapidement un onglet personnel de base.</span><span class="sxs-lookup"><span data-stu-id="93287-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic personal tab.</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="93287-105">Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="93287-105">Create your app project</span></span>

<span data-ttu-id="93287-106">Utilisez la boîte à outils Microsoft teams dans Visual Studio code pour configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="93287-106">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
:::image type="content" source="../doc-links/images/create-teams-app.png" alt-text="image de l’application de création de teams":::
1. <span data-ttu-id="93287-109">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-109">Enter a name for your Teams app.</span></span> <span data-ttu-id="93287-110">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="93287-110">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="93287-111">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="93287-111">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../doc-links/images/choose-tab.png" alt-text="vue de l’image de l’application de création de teams":::
1. <span data-ttu-id="93287-113">Activez l’option **onglet personnel** et sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="93287-113">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="93287-114">Comprendre les composants importants du projet d’application</span><span class="sxs-lookup"><span data-stu-id="93287-114">Understand important app project components</span></span>

<span data-ttu-id="93287-115">Une fois que le kit d’outils configure votre projet, vous disposez des composants permettant de créer un onglet personnel de base pour Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-115">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="93287-116">Les répertoires et les fichiers du projet sont affichés dans la zone Explorateur de Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="93287-116">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../doc-links/images/app-project-files.png" alt-text="Fichiers de projet d’application dans Visual Studio code.":::

<span data-ttu-id="93287-118">Nous allons prendre le temps de comprendre certains des principaux fichiers que les développeurs d’applications teams utilisent.</span><span class="sxs-lookup"><span data-stu-id="93287-118">Let's take time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="93287-119">Manifeste de l’application ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="93287-119">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="93287-120">Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application.</span><span class="sxs-lookup"><span data-stu-id="93287-120">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="93287-121">Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="93287-121">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="93287-122">Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.</span><span class="sxs-lookup"><span data-stu-id="93287-122">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="93287-123">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="93287-123">App scaffolding</span></span>

<span data-ttu-id="93287-124">Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="93287-124">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="93287-125">Si vous créez un onglet pendant l’installation, par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="93287-125">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="93287-126">Il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../../tabs/how-to/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-126">It calls the [Microsoft Teams SDK](../../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="93287-127">Package d’application ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="93287-127">App package (`Development.zip`)</span></span>

<span data-ttu-id="93287-128">Situé dans l' `.publish` annuaire, vous avez besoin du package d’application pour [chargement votre application](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) dans Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-128">Located in the `.publish` directory, you need the app package to [sideload your app](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="93287-129">Le package est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) ou [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="93287-129">The package is also used when [publishing to your organization's app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="93287-130">Voici quelques détails sur les fichiers de package d’application :</span><span class="sxs-lookup"><span data-stu-id="93287-130">Here are some details about the app package files:</span></span>

|<span data-ttu-id="93287-131">Nom</span><span class="sxs-lookup"><span data-stu-id="93287-131">Name</span></span>|<span data-ttu-id="93287-132">Type</span><span class="sxs-lookup"><span data-stu-id="93287-132">Type</span></span>|<span data-ttu-id="93287-133">Size</span><span class="sxs-lookup"><span data-stu-id="93287-133">Size</span></span>|<span data-ttu-id="93287-134">Emplacement du manifeste</span><span class="sxs-lookup"><span data-stu-id="93287-134">Manifest location</span></span>|<span data-ttu-id="93287-135">Nom de fichier du Toolkit</span><span class="sxs-lookup"><span data-stu-id="93287-135">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="93287-136">**Manifeste de l’application**</span><span class="sxs-lookup"><span data-stu-id="93287-136">**App manifest**</span></span>|`.json`| <span data-ttu-id="93287-137">—</span><span class="sxs-lookup"><span data-stu-id="93287-137">—</span></span> | <span data-ttu-id="93287-138">—</span><span class="sxs-lookup"><span data-stu-id="93287-138">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="93287-139">**Logo couleur**</span><span class="sxs-lookup"><span data-stu-id="93287-139">**Color logo**</span></span>|`.png`|<span data-ttu-id="93287-140">192 &times; 192 pixels</span><span class="sxs-lookup"><span data-stu-id="93287-140">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="93287-141">**Logo de plan**</span><span class="sxs-lookup"><span data-stu-id="93287-141">**Outline logo**</span></span>|`.png`|<span data-ttu-id="93287-142">32 &times; 32 pixels</span><span class="sxs-lookup"><span data-stu-id="93287-142">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="93287-143">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="93287-143">Run your app</span></span>

<span data-ttu-id="93287-144">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="93287-144">In the interest of time, you'll build and run your app locally.</span></span> <span data-ttu-id="93287-145">Les applications teams de teams sont hébergées dans le Cloud.</span><span class="sxs-lookup"><span data-stu-id="93287-145">Production-level Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="93287-146">(Ces informations sont également disponibles dans la boîte à outils `README` .)</span><span class="sxs-lookup"><span data-stu-id="93287-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="93287-147">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="93287-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="93287-148">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="93287-148">Run `npm start`.</span></span> <span data-ttu-id="93287-149">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="93287-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="93287-150">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="93287-150">message in the terminal.</span></span>
1. <span data-ttu-id="93287-151">Ouvrez un navigateur et accédez à `https://localhost:3000` la page Web vierge intitulée **Microsoft teams**. (Ne vous inquiétez pas que vous ne pouvez pas voir le contenu sur la page.)</span><span class="sxs-lookup"><span data-stu-id="93287-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../doc-links/images/local-host-tab.png" alt-text="Affichage de l’application dans un navigateur.":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="93287-153">Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="93287-153">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="93287-154">Votre application est en cours d’exécution sur votre serveur Web local.</span><span class="sxs-lookup"><span data-stu-id="93287-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="93287-155">Pour exécuter votre application dans Teams, vous devez faire en sorte qu’elle soit `localhost` accessible via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="93287-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="93287-156">Installez [ngrok](https://ngrok.com/download) si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="93287-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="93287-157">Lorsque vous exécutez cet outil, vous créez deux URL globalement disponibles qui pointent vers votre serveur Web local ( `http://localhost:3000` ).</span><span class="sxs-lookup"><span data-stu-id="93287-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="93287-158">Vous avez besoin de l’URL de transfert qui commence par `HTTPS` .</span><span class="sxs-lookup"><span data-stu-id="93287-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="93287-159">Ouvrez un nouveau terminal et exécutez `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="93287-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="93287-160">Copiez l’URL HTTPs que vous avez fournie (Voir l’exemple ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="93287-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../doc-links/images/ngrok-running.png" alt-text="image en cours d’exécution ngrok":::
1. <span data-ttu-id="93287-162">Dans votre `.publish` répertoire, ouvrez `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="93287-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="93287-163">Remplacez la `baseUrl0` valeur par l’URL copiée.</span><span class="sxs-lookup"><span data-stu-id="93287-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="93287-164">(Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ba5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="93287-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="93287-165">Le manifeste de votre application pointe maintenant vers l’emplacement où vous hébergez l’application.</span><span class="sxs-lookup"><span data-stu-id="93287-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="93287-166">Chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="93287-166">Sideload your app in Teams</span></span>

<span data-ttu-id="93287-167">Une fois que votre application est en cours d’exécution et accessible via HTTPs, vous êtes prêt à la télécharger vers Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="93287-168">Avant de chargement votre application, vérifiez les problèmes à l’aide de la [fonctionnalité de validation de la boîte à outils](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span><span class="sxs-lookup"><span data-stu-id="93287-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="93287-169">Les erreurs doivent être résolues pour chargement l’application.</span><span class="sxs-lookup"><span data-stu-id="93287-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="93287-170">Connectez-vous au client teams avec votre compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="93287-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="93287-171">(Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="93287-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="93287-172">Sélectionnez **applications**, puis **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="93287-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="93287-173">Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="93287-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="93287-174">Affichage modal d’installation.</span><span class="sxs-lookup"><span data-stu-id="93287-174">An install modal displays.</span></span>
:::image type="content" source="../doc-links/images/add-teams-app.png" alt-text="Ajouter une application teams":::
1. <span data-ttu-id="93287-176">Sélectionnez **Ajouter** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="93287-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../doc-links/images/tab-running.png" alt-text="Capture d’écran illustrant un exemple Hello, World ! application dans Teams.":::

<span data-ttu-id="93287-178">🎉 Félicitations !</span><span class="sxs-lookup"><span data-stu-id="93287-178">🎉 Congratulations!</span></span> <span data-ttu-id="93287-179">Votre application est en cours d’exécution dans Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="93287-180">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="93287-180">Next step</span></span>

<span data-ttu-id="93287-181">Développez l’onglet personnel que vous venez de créer ou créez un autre type d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="93287-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="93287-182">Ajouter à votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="93287-182">Add to your personal tab</span></span>](../build-your-first-app/add-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="93287-183">Onglet créer un canal</span><span class="sxs-lookup"><span data-stu-id="93287-183">Build a channel tab</span></span>](../build-your-first-app/add-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="93287-184">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="93287-184">Build a bot</span></span>](../build-your-first-app/add-bot.md)
