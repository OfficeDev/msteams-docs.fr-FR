---
title: Créez des applications avec les Shared Computer Toolkit et Visual Studio Microsoft Teams
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide de Microsoft Teams Shared Computer Toolkit
keywords: boîte à outils visual studio teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875006"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="1b890-104">Créer des applications avec les Shared Computer Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b890-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="1b890-105">Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b890-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="1b890-106">Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="1b890-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b890-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="1b890-107">Prerequisites</span></span>

1. [<span data-ttu-id="1b890-108">Activer la prévisualisation pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="1b890-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="1b890-109">Assurez-vous que **<span>le</span>module ASP.NE T** et le module de développement web ont été ajoutés à votre instance Visual Studio web.</span><span class="sxs-lookup"><span data-stu-id="1b890-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="1b890-110">Vous pouvez vérifier en suivant les étapes de la Visual Studio en ajoutant ou en supprimant des charges de travail et de la documentation [sur les composants.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1b890-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="1b890-112">Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, iiS (Internet Information Services) doit être installé dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="1b890-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="1b890-113">Visual Studio n’inclut pas IIS et n’est pas inclus dans la configuration par défaut de Windows 10, Windows 8 ou Windows 7 ; Toutefois, vous pouvez télécharger la dernière version à partir du Centre [de téléchargement Microsoft.](https://www.microsoft.com/download/details.aspx?id=48264)</span><span class="sxs-lookup"><span data-stu-id="1b890-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Vue de page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="1b890-115">Installer la Shared Computer Toolkit Teams</span><span class="sxs-lookup"><span data-stu-id="1b890-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="1b890-116">Le Shared Computer Toolkit Microsoft Teams pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b890-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="1b890-117">Utilisation du kit de ressources</span><span class="sxs-lookup"><span data-stu-id="1b890-117">Using the toolkit</span></span>

- [<span data-ttu-id="1b890-118">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="1b890-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="1b890-119">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="1b890-120">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="1b890-121">Exécuter votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="1b890-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="1b890-122">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="1b890-123">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="1b890-124">Configurer un nouveau projet Teams</span><span class="sxs-lookup"><span data-stu-id="1b890-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="1b890-125">Sélectionnez **Créer un projet.**</span><span class="sxs-lookup"><span data-stu-id="1b890-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="1b890-126">Choisissez **l’application Microsoft Teams et** sélectionnez **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="1b890-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="1b890-127">Vous arrivez à **l’écran Configurer** votre nouveau projet où vous pouvez choisir le nom du **projet,** l’emplacement **et** le nom de **la solution.**</span><span class="sxs-lookup"><span data-stu-id="1b890-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="1b890-128">Cochez la case **« Placer la solution et le projet dans le même répertoire**».</span><span class="sxs-lookup"><span data-stu-id="1b890-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="1b890-129">Une fenêtre pop-up étiquetée **Ajouter des** fonctionnalités vous permettra de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="1b890-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="1b890-130">Sélectionnez **le bouton** Suivant pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="1b890-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="1b890-131">Une fenêtre pop-up étiquetée **Ajouter des** fonctionnalités vous permet de choisir les propriétés de chaque fonctionnalité sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="1b890-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="1b890-132">Sélectionnez **Terminer** et vous allez vous poser sur la page d’accueil **Shared Computer Toolkit Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="1b890-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="1b890-133">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-133">Configure your app</span></span>

<span data-ttu-id="1b890-134">Au cœur de l’application Teams, trois composants sont intégrés :</span><span class="sxs-lookup"><span data-stu-id="1b890-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="1b890-135">Client Microsoft Teams (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="1b890-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="1b890-136">Un serveur qui répond aux demandes de contenu qui sera affiché dans Teams, par exemple, du contenu d’onglet HTML ou une carte adaptative de bot .</span><span class="sxs-lookup"><span data-stu-id="1b890-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="1b890-137">Un [package d’application](/concepts/build-and-test/apps-package.md) Teams composé de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="1b890-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="1b890-138">Le manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="1b890-138">The manifest.json</span></span>
  > - <span data-ttu-id="1b890-139">Icône [de couleur à](../resources/schema/manifest-schema.md#icons) afficher dans le catalogue d’applications public ou d’organisation</span><span class="sxs-lookup"><span data-stu-id="1b890-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="1b890-140">Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre d’activité Teams.</span><span class="sxs-lookup"><span data-stu-id="1b890-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="1b890-141">Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="1b890-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="1b890-142">Si vous ne l’avez pas déjà fait, vous devrez vous connectez à votre compte ou à votre compte Microsoft 365 pour poursuivre le processus de développement.</span><span class="sxs-lookup"><span data-stu-id="1b890-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="1b890-143">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement au programme pour les développeurs [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="1b890-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="1b890-144">Il est *gratuit pendant* 90 jours et est continuellement renouvelé tant que vous l’utilisez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="1b890-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="1b890-145">Si vous avez un abonnement  Visual Studio *Entreprise* ou Professionnel, les deux programmes incluent un abonnement microsoft 365 [](https://aka.ms/MyVisualStudioBenefits)développeur gratuit, actif pendant toute la durée de vie de Visual Studio abonnement.</span><span class="sxs-lookup"><span data-stu-id="1b890-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="1b890-146">*Voir* [Configurer un abonnement Microsoft 365 Développeur.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="1b890-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="1b890-147">Étapes de configuration</span><span class="sxs-lookup"><span data-stu-id="1b890-147">Configuration steps</span></span>

1. <span data-ttu-id="1b890-148">Pour configurer votre application, sur la page d’accueil Shared Computer Toolkit **Microsoft Teams,** **sélectionnez Modifier le package d’application.**</span><span class="sxs-lookup"><span data-stu-id="1b890-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="1b890-149">Dans le menu **déroulant Mes environnements,** sélectionnez **Développement.**</span><span class="sxs-lookup"><span data-stu-id="1b890-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="1b890-150">Vous allez vous trouver sur la page **des détails de l’application** où vous pouvez modifier les champs de propriété de votre application.</span><span class="sxs-lookup"><span data-stu-id="1b890-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="1b890-151">La modification des champs dans la page détails de l’application met à jour le contenu du manifest.jssur le fichier qui sera finalement intégré au package de l’application.</span><span class="sxs-lookup"><span data-stu-id="1b890-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="1b890-152">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="1b890-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="1b890-153">Package de votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-153">Package your app</span></span>

<span data-ttu-id="1b890-154">La modification de la page de **détails** de l’application ou la mise à jour du manifeste **ou** des fichiers **.env** dans le dossier **.publish** de votre application génère automatiquement **votre fichierDevelopment.zip..**</span><span class="sxs-lookup"><span data-stu-id="1b890-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="1b890-155">Le Development.zip inclut trois fichiers obligatoires : **l'manifest.jset** [deux icônes.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="1b890-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="1b890-156">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="1b890-156">Install and run your app locally</span></span>

1. <span data-ttu-id="1b890-157">Dans le menu **déroulant Configurations** de la solution, sélectionnez **Déployer.**</span><span class="sxs-lookup"><span data-stu-id="1b890-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Menu Configurations de solution](../assets/images/solution-configurations.png)

2. <span data-ttu-id="1b890-159">Sélectionnez **le bouton IIS Express + Teams.**</span><span class="sxs-lookup"><span data-stu-id="1b890-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="1b890-160">Teams se lance et le dialogue d’installation de l’application doit apparaître dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="1b890-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="1b890-161">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="1b890-161">Validate your app</span></span>

<span data-ttu-id="1b890-162">La  page Valider vous permet de vérifier votre package d’application avant de la soumettre à AppSource.</span><span class="sxs-lookup"><span data-stu-id="1b890-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="1b890-163">Il vous suffit de charger le package de manifeste et l’outil de validation vérifie votre application par rapport à tous les cas de test liés au manifeste.</span><span class="sxs-lookup"><span data-stu-id="1b890-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="1b890-164">Pour chaque échec de test, la description fournit un lien de documentation pour vous aider à corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="1b890-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="1b890-165">Pour les tests qui sont difficiles  à automatiser, la liste de contrôle préliminaire détaille 7 des cas de test les plus courants qui ont échoué, ainsi qu’un lien vers une liste de vérification de soumission complète.</span><span class="sxs-lookup"><span data-stu-id="1b890-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="1b890-166">Publier votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="1b890-166">Publish your app to Teams</span></span>

<span data-ttu-id="1b890-167">✔ Sur la page d’accueil de votre projet, vous pouvez télécharger votre application vers une équipe, soumettre votre application au magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source d’application pour tous les utilisateurs de Teams.</span><span class="sxs-lookup"><span data-stu-id="1b890-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="1b890-168">✔ votre administrateur informatique examine ces soumissions.</span><span class="sxs-lookup"><span data-stu-id="1b890-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="1b890-169">✔ vous pouvez revenir à la **page** Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous allez soumettre des mises à jour à votre application ou annuler les soumissions actives.</span><span class="sxs-lookup"><span data-stu-id="1b890-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b890-170">Étape suivante : maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="1b890-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
