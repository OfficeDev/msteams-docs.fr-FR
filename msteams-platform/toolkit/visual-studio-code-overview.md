---
title: Créez des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code
description: Obtenez commencé à construire d’excellentes applications personnalisées directement Visual Studio Code avec le Microsoft Teams Shared Computer Toolkit
keywords: équipes kit d’outils de code studio visuel
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566557"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="dc1f4-104">Créez des applications avec les Teams Shared Computer Toolkit et Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dc1f4-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="dc1f4-105">Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement deVisual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="dc1f4-106">Le kit de ressources vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="dc1f4-107">Installation de la Teams Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="dc1f4-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="dc1f4-108">Le Microsoft Teams Shared Computer Toolkit pour Visual Studio Code est disponible en téléchargement sur [le Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement sous forme d’extension dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="dc1f4-109">Après l’installation, vous devriez voir les Teams Shared Computer Toolkit la barre d Visual Studio Code’activité.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="dc1f4-110">Si ce n’est pas le cas, cliquez à droite dans la barre **d’activité et sélectionnez Microsoft Teams** épingler la boîte à outils pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="dc1f4-111">Utilisation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="dc1f4-111">Using the toolkit</span></span>

- [<span data-ttu-id="dc1f4-112">Mettre en place un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="dc1f4-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="dc1f4-113">Importer un projet existant</span><span class="sxs-lookup"><span data-stu-id="dc1f4-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="dc1f4-114">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="dc1f4-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="dc1f4-115">Emballez votre application</span><span class="sxs-lookup"><span data-stu-id="dc1f4-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="dc1f4-116">Exécutez votre application localement ou en Teams</span><span class="sxs-lookup"><span data-stu-id="dc1f4-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="dc1f4-117">Mettre en place un nouveau projet Teams projet</span><span class="sxs-lookup"><span data-stu-id="dc1f4-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="dc1f4-118">Créez un espace de travail ou un dossier pour votre projet dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-118">Create a workspace or folder for your project in your local environment.</span></span>
1. <span data-ttu-id="dc1f4-119">Dans Visual Studio Code, sélectionnez l’icône Teams’actualité</span><span class="sxs-lookup"><span data-stu-id="dc1f4-119">In Visual Studio Code, select the Teams icon</span></span> ![Icône Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="dc1f4-121">de la barre d’activité sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="dc1f4-122">Sélectionnez **Ouvrez Microsoft Teams Shared Computer Toolkit du** menu de commande.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="dc1f4-123">Sélectionnez **Créer une nouvelle application Teams à partir** du menu de commande.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="dc1f4-124">Lorsque vous êtes invité, entrez le nom de l’espace de travail .</span><span class="sxs-lookup"><span data-stu-id="dc1f4-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="dc1f4-125">Cela sera utilisé à la fois comme nom du dossier où votre projet résidera, et le nom par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="dc1f4-126">Appuyez **sur** Entrez et vous arriverez à **l’écran des fonctionnalités Ajouter** configurer les propriétés de votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="dc1f4-127">Sélectionnez **le bouton** Finition pour compléter le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="dc1f4-128">Importer un projet d’application Teams’environnement existant</span><span class="sxs-lookup"><span data-stu-id="dc1f4-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="dc1f4-129">Dans Visual Studio Code, sélectionnez l’icône Teams’actualité</span><span class="sxs-lookup"><span data-stu-id="dc1f4-129">In Visual Studio Code, select the Teams icon</span></span> ![Icône Teams](../assets/icons/favicon-16x16.png) <span data-ttu-id="dc1f4-131">de la barre d’activité sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="dc1f4-132">Sélectionnez **Le package d’application** Import dans le menu de commande.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="dc1f4-133">Choisissez votre fichier [zip Teams’application](../concepts/build-and-test/apps-package.md) existante.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="dc1f4-134">Choisissez le bouton **Sélectionner le paquet de** publication.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="dc1f4-135">L’onglet configuration de la boîte à outils doit maintenant être rempli des détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="dc1f4-136">Dans Visual Studio Code, sélectionnez **Fichier**  ->  **Ajouter dossier à Workspace pour** ajouter votre répertoire de code source à l’espace de travail Visual Studio Code source.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="dc1f4-137">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="dc1f4-137">Configure your app</span></span>

<span data-ttu-id="dc1f4-138">À la base, l Teams apprateur de messagerie embrasse trois composantes :</span><span class="sxs-lookup"><span data-stu-id="dc1f4-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="dc1f4-139">Le Microsoft Teams client (web, bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="dc1f4-140">Un serveur qui répond aux demandes de contenu qui seront affichées dans Teams.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-140">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="dc1f4-141">Par exemple, le contenu de l’onglet HTML ou une carte adaptative bot.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-141">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="dc1f4-142">Un [Teams’application comprenant](/concepts/build-and-test/apps-package.md) trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="dc1f4-142">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="dc1f4-143">Le manifest.jssur.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-143">The manifest.json.</span></span> 
      > - <span data-ttu-id="dc1f4-144">Une [icône couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications publiques ou organisation.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="dc1f4-145">Une [icône de contour](../resources/schema/manifest-schema.md#icons) pour l’affichage sur la barre d Teams’activité.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="dc1f4-146">Lorsqu’une application est installée, le client Teams parse le fichier manifeste pour déterminer les informations nécessaires comme le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="dc1f4-147">Pour configurer votre application, accédez **à l’onglet** Microsoft Teams Shared Computer Toolkit’Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-147">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="dc1f4-148">Sélectionnez **Modifier le paquet d’applications** pour afficher la page **détails de** l’application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-148">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="dc1f4-149">L’édition des champs dans la page détails de l’application met à jour le contenu des manifest.jsdans le fichier qui sera finalement expédié dans le cadre du paquet d’application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-149">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="dc1f4-150">Pour plus d’informations, voir [l’éditeur manifeste d’App Studio](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="dc1f4-150">For more information, See [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="dc1f4-151">Emballez votre application</span><span class="sxs-lookup"><span data-stu-id="dc1f4-151">Package your app</span></span>

<span data-ttu-id="dc1f4-152">La modification de la page **de détails** de **l’application,** manifeste, **ou .env** fichiers dans le  **dossier de votre application .publish** générera **automatiquement votreDevelopment.zip** fichier.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-152">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="dc1f4-153">Vous devrez inclure deux [icônes dans](../concepts/build-and-test/apps-package.md#app-icons) ce même dossier.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-153">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="dc1f4-154">Installez et exécutez votre application localement</span><span class="sxs-lookup"><span data-stu-id="dc1f4-154">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="dc1f4-155">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="dc1f4-155">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="dc1f4-156">Installez et exécutez votre application localement</span><span class="sxs-lookup"><span data-stu-id="dc1f4-156">Install and run your app locally</span></span>

<span data-ttu-id="dc1f4-157">Reportez-vous au **contenu Build and Run** de votre page d’accueil du projet pour obtenir des instructions détaillées sur la façon d’emballer et de tester votre application.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-157">Refer to the **Build and Run** content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="dc1f4-158">En général, vous devez installer le serveur de votre application, l’exécuter, puis configurer une solution de tunneling afin que Teams puisse accéder au contenu en cours d’exécution à partir de localhost.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-158">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="dc1f4-159">Permettre le développement à partir de localhost</span><span class="sxs-lookup"><span data-stu-id="dc1f4-159">Enable development from localhost</span></span>

<span data-ttu-id="dc1f4-160">Si vous souhaitez débobug votre application basée sur l’onglet sur localhost en utilisant HTTPS, vous devrez dire à votre navigateur de faire confiance à l’application en cours de service à partir <https://localhost> de .</span><span class="sxs-lookup"><span data-stu-id="dc1f4-160">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="dc1f4-161">Accédez à la page <https://localhost:3000/tab>.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-161">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="dc1f4-162">Si vous voyez un avertissement indiquant que le site n’est pas fiable, choisissez l’option de procéder de toute façon.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-162">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="dc1f4-163">Votre application doit désormais être accessible à partir du Teams client.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-163">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="dc1f4-164">Exécutez votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="dc1f4-164">Run your app in Teams</span></span>

<span data-ttu-id="dc1f4-165">Conditions préalables : [Activer le mode Teams aperçu des développeurs](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="dc1f4-165">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="dc1f4-166">Accédez à la barre d’activité sur le côté gauche de la Visual Studio Code fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dc1f4-166">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="dc1f4-167">Sélectionnez **l’icône** Exécuter pour afficher **la vue Exécuter et Debug.**</span><span class="sxs-lookup"><span data-stu-id="dc1f4-167">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="dc1f4-168">Vous pouvez également utiliser le raccourci clavier `Ctrl+Shift+D` .</span><span class="sxs-lookup"><span data-stu-id="dc1f4-168">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="next-step"></a><span data-ttu-id="dc1f4-169">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="dc1f4-169">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc1f4-170">Maintenir et soutenir votre application publiée</span><span class="sxs-lookup"><span data-stu-id="dc1f4-170">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
