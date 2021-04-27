---
title: Créer des applications avec le code de Shared Computer Toolkit et Visual Studio Microsoft Teams
description: Commencer à créer d'excellentes applications personnalisées directement dans Visual Studio Code avec microsoft Teams Shared Computer Toolkit
keywords: kit de ressources teams Visual Studio Code
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020260"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="48014-104">Créer des applications avec le code Shared Computer Toolkit et Visual Studio Teams</span><span class="sxs-lookup"><span data-stu-id="48014-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="48014-105">Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="48014-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="48014-106">Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="48014-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="48014-107">Installation de l'Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="48014-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="48014-108">Microsoft Teams Shared Computer Toolkit for Visual Studio Code est disponible en téléchargement à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu'extension dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="48014-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="48014-109">Après l'installation, les équipes doivent s'Shared Computer Toolkit dans la barre Visual Studio'activité code.</span><span class="sxs-lookup"><span data-stu-id="48014-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="48014-110">Si ce n'est pas le cas, cliquez avec le bouton droit dans la barre d'activité et sélectionnez **Microsoft Teams** pour épingler le kit de ressources pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="48014-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="48014-111">Utilisation du kit de ressources</span><span class="sxs-lookup"><span data-stu-id="48014-111">Using the toolkit</span></span>

- [<span data-ttu-id="48014-112">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="48014-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="48014-113">Importer un projet existant</span><span class="sxs-lookup"><span data-stu-id="48014-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="48014-114">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="48014-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="48014-115">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="48014-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="48014-116">Exécuter votre application localement ou dans Teams</span><span class="sxs-lookup"><span data-stu-id="48014-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="48014-117">Configurer un nouveau projet Teams</span><span class="sxs-lookup"><span data-stu-id="48014-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="48014-118">Créez un espace de travail/dossier pour votre projet dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="48014-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="48014-119">Dans Visual Studio code, sélectionnez l'icône Teams</span><span class="sxs-lookup"><span data-stu-id="48014-119">In Visual Studio Code, select the Teams icon</span></span> ![Icône Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="48014-121">à partir de la barre d'activité sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="48014-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="48014-122">Sélectionnez **Ouvrir l'Shared Computer Toolkit Microsoft Teams** dans le menu de commande.</span><span class="sxs-lookup"><span data-stu-id="48014-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="48014-123">Sélectionnez **Créer une application Teams dans** le menu de commande.</span><span class="sxs-lookup"><span data-stu-id="48014-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="48014-124">Lorsque vous y invitez, entrez le nom de l'espace de travail.</span><span class="sxs-lookup"><span data-stu-id="48014-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="48014-125">Il sera utilisé à la fois comme nom du dossier où résidera votre projet et comme nom par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="48014-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="48014-126">Appuyez **sur Entrée** pour accéder à l'écran Ajouter des **fonctionnalités** et configurer les propriétés de votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="48014-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="48014-127">Sélectionnez le **bouton** Terminer pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="48014-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="48014-128">Importer un projet d'application Teams existant</span><span class="sxs-lookup"><span data-stu-id="48014-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="48014-129">Dans Visual Studio code, sélectionnez l'icône Teams</span><span class="sxs-lookup"><span data-stu-id="48014-129">In Visual Studio Code, select the Teams icon</span></span> ![Icône Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="48014-131">à partir de la barre d'activité sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="48014-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="48014-132">Sélectionnez **Importer un package d'application** dans le menu de commande.</span><span class="sxs-lookup"><span data-stu-id="48014-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="48014-133">Choisissez votre fichier zip de [package d'application Teams](../concepts/build-and-test/apps-package.md) existant.</span><span class="sxs-lookup"><span data-stu-id="48014-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="48014-134">Sélectionnez **le bouton Sélectionner un package de** publication.</span><span class="sxs-lookup"><span data-stu-id="48014-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="48014-135">L'onglet configuration du kit de ressources doit maintenant être rempli avec les détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="48014-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="48014-136">Dans Visual Studio code, sélectionnez Fichier Ajouter un dossier à l'espace de travail pour ajouter votre répertoire de code source à l'espace   ->   Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="48014-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="48014-137">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="48014-137">Configure your app</span></span>

<span data-ttu-id="48014-138">Au cœur de l'application Teams, trois composants sont intégrés :</span><span class="sxs-lookup"><span data-stu-id="48014-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="48014-139">Client Microsoft Teams (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="48014-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="48014-140">Un serveur qui répond aux demandes de contenu qui sera affiché dans Teams, par exemple, du contenu d'onglet HTML ou une carte adaptative de bot .</span><span class="sxs-lookup"><span data-stu-id="48014-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="48014-141">Un [package d'application](/concepts/build-and-test/apps-package.md) Teams composé de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="48014-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="48014-142">Le manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="48014-142">The manifest.json</span></span> 
  > - <span data-ttu-id="48014-143">Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour votre application à afficher dans le catalogue d'applications public ou de l'organisation</span><span class="sxs-lookup"><span data-stu-id="48014-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="48014-144">Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre d'activité Teams.</span><span class="sxs-lookup"><span data-stu-id="48014-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="48014-145">Lorsqu'une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l'URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="48014-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="48014-146">Pour configurer votre application, accédez à l'onglet **Shared Computer Toolkit Microsoft Teams** dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="48014-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="48014-147">Sélectionnez **Modifier le package d'application** pour afficher la page **Détails de l'application.**</span><span class="sxs-lookup"><span data-stu-id="48014-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="48014-148">La modification des champs dans la page détails de l'application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l'application.</span><span class="sxs-lookup"><span data-stu-id="48014-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="48014-149">*Voir* [l'éditeur de manifeste App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="48014-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="48014-150">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="48014-150">Package your app</span></span>

<span data-ttu-id="48014-151">La modification de la page de **détails** **de** l'application, du manifeste ou des fichiers **.env** dans le dossier  **.publish** de votre application génère automatiquement **Development.zip** fichier.</span><span class="sxs-lookup"><span data-stu-id="48014-151">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="48014-152">Vous devez inclure deux [icônes](../concepts/build-and-test/apps-package.md#app-icons) dans ce même dossier.</span><span class="sxs-lookup"><span data-stu-id="48014-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="48014-153">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="48014-153">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="48014-154">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="48014-154">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="48014-155">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="48014-155">Install and run your app locally</span></span>

<span data-ttu-id="48014-156">Reportez-vous à \* Créer et exécuter *du* contenu dans la page d'accueil de votre projet pour obtenir des instructions détaillées sur la façon de créer un package et de tester votre application.</span><span class="sxs-lookup"><span data-stu-id="48014-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="48014-157">En règle générale, vous devez installer le serveur de votre application, le faire fonctionner, puis configurer une solution de tunnel afin que Teams puisse accéder au contenu s'exécutant à partir de l'host local.</span><span class="sxs-lookup"><span data-stu-id="48014-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="48014-158">Activer le développement à partir de l'host local</span><span class="sxs-lookup"><span data-stu-id="48014-158">Enable development from localhost</span></span>

<span data-ttu-id="48014-159">Si vous souhaitez déboguer votre application basée sur l'onglet sur localhost à l'aide du protocole HTTPS, vous devrez indiquer à votre navigateur d'faire confiance à l'application à partir de . <https://localhost></span><span class="sxs-lookup"><span data-stu-id="48014-159">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="48014-160">Accédez à la page <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="48014-160">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="48014-161">Si vous voyez un avertissement indiquant que le site n'est pas approuvé, choisissez l'option pour continuer malgré tout.</span><span class="sxs-lookup"><span data-stu-id="48014-161">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="48014-162">Votre application doit maintenant être accessible à partir du client Teams.</span><span class="sxs-lookup"><span data-stu-id="48014-162">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="48014-163">Exécuter votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="48014-163">Run your app in Teams</span></span>

<span data-ttu-id="48014-164">Conditions préalables : activer [le mode d'aperçu pour les développeurs Teams](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="48014-164">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="48014-165">Accédez à la barre d'activité sur le côté gauche de la Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="48014-165">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="48014-166">Sélectionnez **l'icône** Exécuter pour afficher **l'affichage Exécuter et déboguer.**</span><span class="sxs-lookup"><span data-stu-id="48014-166">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="48014-167">Vous pouvez également utiliser le raccourci `Ctrl+Shift+D` clavier.</span><span class="sxs-lookup"><span data-stu-id="48014-167">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48014-168">Étape suivante : maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="48014-168">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
