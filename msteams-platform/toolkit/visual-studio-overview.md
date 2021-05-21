---
title: Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide Microsoft Teams Shared Computer Toolkit
keywords: boîte à outils visual studio teams
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566550"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="7d140-104">Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d140-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="7d140-105">Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d140-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="7d140-106">Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="7d140-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d140-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7d140-107">Prerequisites</span></span>

1. <span data-ttu-id="7d140-108">[Activer la prévisualisation pour les développeurs.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)</span><span class="sxs-lookup"><span data-stu-id="7d140-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="7d140-109">Assurez-vous que **<span>le</span>module ASP.NE T** et le module de développement web ont été ajoutés à Visual Studio instance.</span><span class="sxs-lookup"><span data-stu-id="7d140-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="7d140-110">Vous pouvez vérifier en suivant les étapes de la Visual Studio en ajoutant ou en supprimant des charges de travail et de la documentation [sur les composants.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7d140-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="7d140-112">Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, iiS (Internet Information Services) doit être installé dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="7d140-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="7d140-113">Visual Studio n’inclut pas IIS et n’est pas inclus dans la configuration Windows 10, Windows 8 ou Windows 7 par défaut ; Toutefois, vous pouvez télécharger la dernière version à partir du Centre [de téléchargement Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="7d140-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Vue de page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="7d140-115">Installer le Teams Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="7d140-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="7d140-116">Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d140-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="7d140-117">Utilisation du kit de ressources</span><span class="sxs-lookup"><span data-stu-id="7d140-117">Using the toolkit</span></span>

- [<span data-ttu-id="7d140-118">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="7d140-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="7d140-119">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="7d140-120">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="7d140-121">Exécuter votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="7d140-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="7d140-122">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="7d140-123">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="7d140-124">Configurer un nouveau projet Teams projet</span><span class="sxs-lookup"><span data-stu-id="7d140-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="7d140-125">Sélectionnez **Créer un projet.**</span><span class="sxs-lookup"><span data-stu-id="7d140-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="7d140-126">Choose **Microsoft Teams App** and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="7d140-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="7d140-127">Vous arrivez à **l’écran** Configurer votre nouveau projet où vous pouvez choisir le nom **Project,** l’emplacement **et** le nom de **la solution.**</span><span class="sxs-lookup"><span data-stu-id="7d140-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="7d140-128">Cochez la case **« Placer la solution et le projet dans le même répertoire**».</span><span class="sxs-lookup"><span data-stu-id="7d140-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="7d140-129">Une fenêtre pop-up étiquetée **Ajouter** des fonctionnalités vous permet de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="7d140-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="7d140-130">Sélectionnez **le bouton** Suivant pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="7d140-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="7d140-131">Une fenêtre pop-up étiquetée **Ajouter des** fonctionnalités vous permet de choisir les propriétés de chaque fonctionnalité sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="7d140-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="7d140-132">Sélectionnez **Terminer** et vous allez vous poser sur **Microsoft Teams Shared Computer Toolkit** page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="7d140-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="7d140-133">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-133">Configure your app</span></span>

<span data-ttu-id="7d140-134">L’application Teams principale englobe trois composants :</span><span class="sxs-lookup"><span data-stu-id="7d140-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="7d140-135">Le Microsoft Teams client (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="7d140-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="7d140-136">Un serveur qui répond aux demandes de contenu qui s’afficheront dans Teams, par exemple, du contenu d’onglet HTML ou une carte adaptative de bot .</span><span class="sxs-lookup"><span data-stu-id="7d140-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="7d140-137">Un package Teams’application se compose de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="7d140-137">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="7d140-138">Le manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="7d140-138">The manifest.json</span></span>
      > - <span data-ttu-id="7d140-139">Icône [de couleur à](../resources/schema/manifest-schema.md#icons) afficher dans le catalogue d’applications public ou d’organisation</span><span class="sxs-lookup"><span data-stu-id="7d140-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
      > - <span data-ttu-id="7d140-140">Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.</span><span class="sxs-lookup"><span data-stu-id="7d140-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="7d140-141">Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="7d140-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="7d140-142">Si ce n’est pas déjà fait, vous devrez vous Microsoft 365 votre compte ou compte pour poursuivre le processus de développement.</span><span class="sxs-lookup"><span data-stu-id="7d140-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="7d140-143">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement au Microsoft 365 [développeur.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="7d140-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="7d140-144">Il est *gratuit pendant* 90 jours et est continuellement renouvelé tant que vous l’utilisez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="7d140-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="7d140-145">Si vous avez un abonnement Visual Studio *Enterprise* ou *Professional,* les deux programmes incluent un abonnement Microsoft 365 développeur [gratuit,](https://aka.ms/MyVisualStudioBenefits)actif pendant toute la durée de vie de Visual Studio abonnement.</span><span class="sxs-lookup"><span data-stu-id="7d140-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="7d140-146">Pour plus d’informations, voir [Configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="7d140-146">For more information, See [Set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="7d140-147">Étapes de configuration</span><span class="sxs-lookup"><span data-stu-id="7d140-147">Configuration steps</span></span>

1. <span data-ttu-id="7d140-148">Pour configurer votre application,  sur la page Microsoft Teams Shared Computer Toolkit’accueil, sélectionnez **Modifier le package d’application.**</span><span class="sxs-lookup"><span data-stu-id="7d140-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="7d140-149">Dans le menu **déroulant Mes environnements,** sélectionnez **Développement.**</span><span class="sxs-lookup"><span data-stu-id="7d140-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="7d140-150">Vous allez vous trouver sur la page **des détails de l’application** où vous pouvez modifier les champs de propriété de votre application.</span><span class="sxs-lookup"><span data-stu-id="7d140-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="7d140-151">La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l’application.</span><span class="sxs-lookup"><span data-stu-id="7d140-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="7d140-152">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="7d140-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="7d140-153">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-153">Package your app</span></span>

<span data-ttu-id="7d140-154">La modification de la page de **détails** de l’application ou la mise à jour du manifeste **ou** des fichiers **.env** dans le dossier **.publish** de votre application génère automatiquement **votre fichierDevelopment.zip..**</span><span class="sxs-lookup"><span data-stu-id="7d140-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="7d140-155">Le Development.zip inclut trois fichiers obligatoires : **l'manifest.jset** [deux icônes.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="7d140-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="7d140-156">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="7d140-156">Install and run your app locally</span></span>

1. <span data-ttu-id="7d140-157">Dans le menu **déroulant Configurations** de la solution, **sélectionnez Déployer** comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="7d140-157">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Menu Configurations de la solution](../assets/images/solution-configurations.png)

2. <span data-ttu-id="7d140-159">Sélectionnez **le IIS Express + Teams** bouton.</span><span class="sxs-lookup"><span data-stu-id="7d140-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="7d140-160">Teams s’affiche et le dialogue d’installation de l’application doit s’Teams client.</span><span class="sxs-lookup"><span data-stu-id="7d140-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="7d140-161">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="7d140-161">Validate your app</span></span>

<span data-ttu-id="7d140-162">La  page Valider vous permet de vérifier votre package d’application avant de la soumettre à AppSource.</span><span class="sxs-lookup"><span data-stu-id="7d140-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="7d140-163">Il vous suffit de charger le package de manifeste et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste.</span><span class="sxs-lookup"><span data-stu-id="7d140-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="7d140-164">Pour chaque échec de test, la description fournit un lien de documentation pour vous aider à corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="7d140-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="7d140-165">Pour les tests qui sont difficiles  à automatiser, la liste de contrôle préliminaire détaille 7 des cas de test les plus courants qui ont échoué, ainsi qu’un lien vers une liste de vérification de soumission complète.</span><span class="sxs-lookup"><span data-stu-id="7d140-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="7d140-166">Publier votre application sur Teams</span><span class="sxs-lookup"><span data-stu-id="7d140-166">Publish your app to Teams</span></span>

<span data-ttu-id="7d140-167">✔ Sur la page d’accueil de votre projet, vous pouvez charger votre application vers une équipe, soumettre votre application au magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source d’application pour tous les utilisateurs Teams.</span><span class="sxs-lookup"><span data-stu-id="7d140-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="7d140-168">✔ votre administrateur informatique examine ces soumissions.</span><span class="sxs-lookup"><span data-stu-id="7d140-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="7d140-169">✔ vous pouvez revenir à la **page** Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous allez envoyer des mises à jour à votre application ou annuler les soumissions actives.</span><span class="sxs-lookup"><span data-stu-id="7d140-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="7d140-170">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="7d140-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d140-171">Maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="7d140-171">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
