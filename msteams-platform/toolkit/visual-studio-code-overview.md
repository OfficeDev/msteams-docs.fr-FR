---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio code
description: Commencer à créer des applications personnalisées directement dans Visual Studio code avec Microsoft teams Toolkit
keywords: Kit de développement Visual Studio Visual Studio teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 41b0eeaeef1c7094fc9c8cbdc05c2db899245fc6
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476929"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="a3212-104">Créer des applications avec Team Toolkit et Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="a3212-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="a3212-105">Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a3212-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="a3212-106">Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="a3212-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="a3212-107">Installation du kit de développement teams</span><span class="sxs-lookup"><span data-stu-id="a3212-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="a3212-108">Microsoft teams Toolkit for Visual Studio code peut être téléchargé à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu’extension dans Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="a3212-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="a3212-109">Après l’installation, vous devriez voir la boîte à outils teams dans la barre d’activité code Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3212-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="a3212-110">Si ce n’est pas le cas, cliquez avec le bouton droit de la barre d’activité et sélectionnez **Microsoft teams** pour épingler la boîte à outils pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="a3212-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="a3212-111">Utilisation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="a3212-111">Using the toolkit</span></span>

- [<span data-ttu-id="a3212-112">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="a3212-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="a3212-113">Importer un projet existant</span><span class="sxs-lookup"><span data-stu-id="a3212-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="a3212-114">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="a3212-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="a3212-115">Empaquetage de votre application</span><span class="sxs-lookup"><span data-stu-id="a3212-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="a3212-116">Exécuter votre application localement ou dans teams</span><span class="sxs-lookup"><span data-stu-id="a3212-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="a3212-117">Configurer un nouveau projet teams</span><span class="sxs-lookup"><span data-stu-id="a3212-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="a3212-118">Créez un dossier/espace de travail pour votre projet dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="a3212-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="a3212-119">Dans Visual Studio code, sélectionnez l’icône teams</span><span class="sxs-lookup"><span data-stu-id="a3212-119">In Visual Studio Code, select the Teams icon</span></span> ![Icône Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="a3212-121">à partir de la barre d’activité sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a3212-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="a3212-122">Sélectionnez **ouvrir la boîte à outils Microsoft teams** dans le menu de commandes.</span><span class="sxs-lookup"><span data-stu-id="a3212-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="a3212-123">Sélectionnez **créer une nouvelle application teams** dans le menu de commandes.</span><span class="sxs-lookup"><span data-stu-id="a3212-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="a3212-124">Lorsque vous y êtes invité, entrez le nom de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="a3212-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="a3212-125">Il sera utilisé à la fois comme nom du dossier dans lequel votre projet réside et comme nom par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="a3212-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="a3212-126">Appuyez sur **entrée** pour accéder à l’écran **Add Capabilities** et configurer les propriétés de votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="a3212-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="a3212-127">Cliquez sur le bouton **Terminer** pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="a3212-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="a3212-128">Importer un projet d’application teams existant</span><span class="sxs-lookup"><span data-stu-id="a3212-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="a3212-129">Dans Visual Studio code, sélectionnez l’icône teams</span><span class="sxs-lookup"><span data-stu-id="a3212-129">In Visual Studio Code, select the Teams icon</span></span> ![Icône Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="a3212-131">à partir de la barre d’activité sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a3212-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="a3212-132">Sélectionnez **Importer un package d’application** dans le menu de commandes.</span><span class="sxs-lookup"><span data-stu-id="a3212-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="a3212-133">Choisissez votre fichier zip de [package d’application teams](../concepts/build-and-test/apps-package.md) existant.</span><span class="sxs-lookup"><span data-stu-id="a3212-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="a3212-134">Cliquez sur le bouton **Sélectionner un package de publication** .</span><span class="sxs-lookup"><span data-stu-id="a3212-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="a3212-135">L’onglet Configuration de la boîte à outils doit maintenant être renseigné avec les détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="a3212-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="a3212-136">Dans Visual Studio code, sélectionnez **fichier**  ->  **Ajouter un dossier à l’espace de travail** pour ajouter le répertoire de votre code source à l’espace de travail de code Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3212-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="a3212-137">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="a3212-137">Configure your app</span></span>

<span data-ttu-id="a3212-138">À son niveau principal, l’application teams adopte trois composants :</span><span class="sxs-lookup"><span data-stu-id="a3212-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="a3212-139">Le client Microsoft Teams (Web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="a3212-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="a3212-140">Serveur qui répond aux demandes de contenu qui s’affichent dans Teams, par exemple, le contenu de l’onglet HTML ou une carte de robot.</span><span class="sxs-lookup"><span data-stu-id="a3212-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="a3212-141">Package d' [application](/concepts/build-and-test/apps-package.md) teams comprenant trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="a3212-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="a3212-142">La manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="a3212-142">The manifest.json</span></span> 
  > - <span data-ttu-id="a3212-143">Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour l’affichage de votre application dans le catalogue d’applications public ou d’organisation</span><span class="sxs-lookup"><span data-stu-id="a3212-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="a3212-144">[Icône de plan](../resources/schema/manifest-schema.md#icons) pour l’affichage dans la barre d’activité de teams.</span><span class="sxs-lookup"><span data-stu-id="a3212-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="a3212-145">Lorsqu’une application est installée, le client teams analyse le fichier manifeste pour déterminer les informations nécessaires telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="a3212-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="a3212-146">Pour configurer votre application, accédez à l’onglet **Microsoft teams Toolkit** dans Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="a3212-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="a3212-147">Sélectionnez **modifier le package d’application** pour afficher la page des détails de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="a3212-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="a3212-148">La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application.</span><span class="sxs-lookup"><span data-stu-id="a3212-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="a3212-149">*Voir* [éditeur de manifeste de l’application Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="a3212-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="a3212-150">Empaquetage de votre application</span><span class="sxs-lookup"><span data-stu-id="a3212-150">Package your app</span></span>

<span data-ttu-id="a3212-151">La modification de la page de détails de l' **application** ou la mise à jour du **manifeste**, ou des fichiers **. env** dans le dossier  **. Publish** de votre application, génère automatiquement votre fichier **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="a3212-151">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="a3212-152">Vous devez inclure [deux icônes](../concepts/build-and-test/apps-package.md#icons) dans ce même dossier.</span><span class="sxs-lookup"><span data-stu-id="a3212-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="a3212-153">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="a3212-153">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="a3212-154">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="a3212-154">Install and run your app locally</span></span>

<span data-ttu-id="a3212-155">Pour obtenir des instructions détaillées sur la façon d’empaqueter et de tester votre application, reportez-vous à la page \**générer et exécuter* du contenu dans votre page d’accueil Project.</span><span class="sxs-lookup"><span data-stu-id="a3212-155">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="a3212-156">En général, vous devez installer le serveur de votre application, le faire fonctionner, puis configurer une solution de tunneling afin que les équipes puissent accéder au contenu exécuté à partir de localhost.</span><span class="sxs-lookup"><span data-stu-id="a3212-156">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="a3212-157">Activer le développement à partir de localhost</span><span class="sxs-lookup"><span data-stu-id="a3212-157">Enable development from localhost</span></span>

<span data-ttu-id="a3212-158">Si vous souhaitez déboguer votre application basée sur les onglets sur localhost à l’aide du protocole HTTPs, vous devez indiquer à votre navigateur d’approuver l’application en provenance de <https://localhost> .</span><span class="sxs-lookup"><span data-stu-id="a3212-158">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="a3212-159">Accédez à la page <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="a3212-159">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="a3212-160">Si vous voyez un avertissement indiquant que le site n’est pas approuvé, sélectionnez l’option continuer quand même.</span><span class="sxs-lookup"><span data-stu-id="a3212-160">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="a3212-161">Votre application doit maintenant être accessible depuis le client Teams.</span><span class="sxs-lookup"><span data-stu-id="a3212-161">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="a3212-162">Exécuter votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="a3212-162">Run your app in Teams</span></span>

<span data-ttu-id="a3212-163">Conditions préalables : [activer le mode aperçu développeur teams](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="a3212-163">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="a3212-164">Accédez à la barre d’activité sur le côté gauche de la fenêtre de code Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3212-164">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="a3212-165">Sélectionnez l’icône **exécuter** pour afficher l’affichage **exécuter et déboguer** .</span><span class="sxs-lookup"><span data-stu-id="a3212-165">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="a3212-166">Vous pouvez également utiliser le raccourci clavier `Ctrl+Shift+D` .</span><span class="sxs-lookup"><span data-stu-id="a3212-166">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3212-167">Étape suivante : maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="a3212-167">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
