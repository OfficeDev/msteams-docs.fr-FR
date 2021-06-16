---
title: Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide Microsoft Teams Shared Computer Toolkit
keywords: boîte à outils visual studio teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949699"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="37b43-104">Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37b43-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="37b43-105">Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37b43-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="37b43-106">Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="37b43-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37b43-107">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="37b43-107">Prerequisites</span></span>

1. <span data-ttu-id="37b43-108">[Activer la prévisualisation pour les développeurs.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)</span><span class="sxs-lookup"><span data-stu-id="37b43-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="37b43-109">Assurez-vous que **<span>le</span>module ASP.NE T** et le module de développement web ont été ajoutés à Visual Studio instance.</span><span class="sxs-lookup"><span data-stu-id="37b43-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="37b43-110">Vous pouvez vérifier en suivant les étapes de la Visual Studio en ajoutant ou en supprimant des charges de travail et de la documentation [sur les composants.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="37b43-110">You can check by following the steps in the [modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="37b43-112">Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, vous devez avoir installé Internet Information Services (IIS) dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="37b43-112">If you want to test your app by deploying it from Visual Studio, you must have Internet Information Services (IIS)) installed in your development environment.</span></span> <span data-ttu-id="37b43-113">Visual Studio n’inclut pas IIS et n’est pas inclus dans la configuration Windows 10, Windows 8 ou Windows 7 par défaut ; Toutefois, vous pouvez télécharger la dernière version à partir du Centre [de téléchargement Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="37b43-113">Visual Studio does not include IIS and it is not included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Vue de page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="37b43-115">Installer le Teams Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="37b43-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="37b43-116">Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37b43-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span> <span data-ttu-id="37b43-117">À partir Visual Studio Marketplace téléchargez également [Teams Shared Computer Toolkit pour Visual Studio 2019.](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)</span><span class="sxs-lookup"><span data-stu-id="37b43-117">From the Visual Studio Marketplace also download [Teams Toolkit for Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="37b43-118">Utilisation du kit de ressources</span><span class="sxs-lookup"><span data-stu-id="37b43-118">Using the toolkit</span></span>

- [<span data-ttu-id="37b43-119">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="37b43-119">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="37b43-120">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-120">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="37b43-121">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-121">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="37b43-122">Installer et exécuter votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="37b43-122">Install and run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="37b43-123">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-123">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="37b43-124">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-124">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="37b43-125">Configurer un nouveau projet Teams projet</span><span class="sxs-lookup"><span data-stu-id="37b43-125">Set up a new Teams project</span></span>

![Teams kit de ressources installé](../assets/images/teamstoolkiticon.png)

1. <span data-ttu-id="37b43-127">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="37b43-127">Select **Create New Project**.</span></span>

    ![Création d’un projet](../assets/images/createnewproject.png)

1. <span data-ttu-id="37b43-129">Choisissez l’outil de démarrage rapide **pour Microsoft Teams app,** puis sélectionnez **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="37b43-129">Choose the quickstart tool for **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="37b43-130">Dans la page **Configurer votre nouveau** projet, entrez le **Project,** l’emplacement et le **nom de la solution.** </span><span class="sxs-lookup"><span data-stu-id="37b43-130">In the **Configure your new project** page, enter the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="37b43-131">Sélectionnez la solution et le projet Place dans la même case **à cocher d’annuaire.**</span><span class="sxs-lookup"><span data-stu-id="37b43-131">Select the **Place solution and project in the same directory** checkbox.</span></span>
1. <span data-ttu-id="37b43-132">Dans la **fenêtre pop-up Ajouter** des fonctionnalités, choisissez une ou plusieurs fonctionnalités pour la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="37b43-132">In the **Add Capabilities** pop-up window, choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="37b43-133">Sélectionnez **le bouton** Suivant pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="37b43-133">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="37b43-134">Dans la **fenêtre pop-up Ajouter des** fonctionnalités, choisissez les propriétés de chaque fonctionnalité sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="37b43-134">In the **Add Capabilities** pop-up window, choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="37b43-135">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="37b43-135">Select **Finish**.</span></span> <span data-ttu-id="37b43-136">La **Microsoft Teams Shared Computer Toolkit** page d’accueil de l’événement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="37b43-136">The **Microsoft Teams Toolkit** landing page is shown.</span></span>

    ![Teams page d’accueil du kit de ressources](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a><span data-ttu-id="37b43-138">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-138">Configure your app</span></span>

<span data-ttu-id="37b43-139">L’application Teams principale englobe trois composants :</span><span class="sxs-lookup"><span data-stu-id="37b43-139">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="37b43-140">Le client Microsoft Teams web, de bureau ou mobile, où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="37b43-140">The Microsoft Teams client including web, desktop, or mobile, where users interact with your app.</span></span>
  1. <span data-ttu-id="37b43-141">Un serveur qui répond aux demandes de contenu qui s’affiche dans Teams, par exemple, du contenu d’onglet HTML ou une carte adaptative de bot.</span><span class="sxs-lookup"><span data-stu-id="37b43-141">A server that responds to requests for content that is displayed in Teams, for example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="37b43-142">Un package Teams’application se compose de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="37b43-142">A Teams app package consists of three files:</span></span>

      - <span data-ttu-id="37b43-143">Le manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="37b43-143">The manifest.json</span></span>
      - <span data-ttu-id="37b43-144">Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="37b43-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      - <span data-ttu-id="37b43-145">Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.</span><span class="sxs-lookup"><span data-stu-id="37b43-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="37b43-146">Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="37b43-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="37b43-147">Si ce n’est pas déjà fait, vous devez vous Microsoft 365 votre compte d’utilisateur pour poursuivre le processus de développement.</span><span class="sxs-lookup"><span data-stu-id="37b43-147">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="37b43-148">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement [Microsoft 365 programme pour les développeurs.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="37b43-148">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="37b43-149">Il est gratuit pendant 90 jours et renouvelé tant que vous l’utilisez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="37b43-149">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="37b43-150">Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 développeur [gratuit,](https://aka.ms/MyVisualStudioBenefits)actif pendant toute la durée de Visual Studio abonnement.</span><span class="sxs-lookup"><span data-stu-id="37b43-150">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="37b43-151">Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="37b43-151">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="37b43-152">Étapes de configuration</span><span class="sxs-lookup"><span data-stu-id="37b43-152">Configuration steps</span></span>

1. <span data-ttu-id="37b43-153">Pour configurer votre application,  sur la page Microsoft Teams Shared Computer Toolkit’accueil, sélectionnez **Modifier le package d’application.**</span><span class="sxs-lookup"><span data-stu-id="37b43-153">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="37b43-154">Dans le menu **déroulant Mes environnements,** sélectionnez **Développement.**</span><span class="sxs-lookup"><span data-stu-id="37b43-154">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="37b43-155">Dans la page **Détails de l’application,** modifiez les champs de propriété de votre application.</span><span class="sxs-lookup"><span data-stu-id="37b43-155">In the **App details** page, edit your app's property fields.</span></span>
    
    <span data-ttu-id="37b43-156">La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera intégré au package d’application.</span><span class="sxs-lookup"><span data-stu-id="37b43-156">Editing the fields in the App details page updates the contents of the manifest.json file that will ship as part of the app package.</span></span> <span data-ttu-id="37b43-157">Pour plus d’informations, [voir Teams Shared Computer Toolkit manifeste.](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="37b43-157">For more information, see [Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).</span></span>

## <a name="package-your-app"></a><span data-ttu-id="37b43-158">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-158">Package your app</span></span>

<span data-ttu-id="37b43-159">La modification de la page de **détails** de l’application ou la mise à jour du manifeste **ou** des fichiers **.env** dans le dossier **.publish** de votre application génère automatiquement **votre fichierDevelopment.zip..**</span><span class="sxs-lookup"><span data-stu-id="37b43-159">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="37b43-160">Le Development.zip inclut trois fichiers requis, **l'manifest.jset** [deux icônes.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="37b43-160">The Development.zip file includes three required files, the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="37b43-161">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="37b43-161">Install and run your app locally</span></span>

1. <span data-ttu-id="37b43-162">Dans le menu **déroulant Configurations** de la solution, **sélectionnez Déployer** comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="37b43-162">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Menu Configurations de la solution](../assets/images/solution-configurations.png)

1. <span data-ttu-id="37b43-164">Sélectionnez **le IIS Express + Teams** bouton.</span><span class="sxs-lookup"><span data-stu-id="37b43-164">Select the **IIS Express + Teams** button.</span></span>

    <span data-ttu-id="37b43-165">La boîte de dialogue d’installation de l’application s’affiche dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="37b43-165">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="37b43-166">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="37b43-166">Validate your app</span></span>

<span data-ttu-id="37b43-167">La  page Valider vous permet de vérifier votre package d’application avant de la soumettre à AppSource.</span><span class="sxs-lookup"><span data-stu-id="37b43-167">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="37b43-168">Il vous suffit de charger le package de manifeste et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste.</span><span class="sxs-lookup"><span data-stu-id="37b43-168">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="37b43-169">Pour chaque échec de test, la description fournit un lien de documentation pour vous aider à corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="37b43-169">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="37b43-170">Pour les tests difficiles à automatiser, la liste de contrôle préliminaire détaille 7 des cas de test les plus courants qui ont échoué, ainsi qu’un lien vers une liste de vérification de soumission complète. </span><span class="sxs-lookup"><span data-stu-id="37b43-170">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="37b43-171">Publier votre application sur Teams</span><span class="sxs-lookup"><span data-stu-id="37b43-171">Publish your app to Teams</span></span>

* <span data-ttu-id="37b43-172">Sur la page d’accueil de votre projet, vous pouvez télécharger votre application dans une équipe, l’envoyer sur le magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs Teams.</span><span class="sxs-lookup"><span data-stu-id="37b43-172">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

* <span data-ttu-id="37b43-173">Votre administrateur informatique examine ces envois.</span><span class="sxs-lookup"><span data-stu-id="37b43-173">Your IT admin will review these submissions.</span></span>

* <span data-ttu-id="37b43-174">Vous pouvez revenir à **la** page Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous pouvez soumettre des mises à jour à votre application ou annuler les soumissions actives.</span><span class="sxs-lookup"><span data-stu-id="37b43-174">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="37b43-175">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="37b43-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37b43-176">Maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="37b43-176">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
