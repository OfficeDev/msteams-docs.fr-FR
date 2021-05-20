---
title: Créez des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio
description: Obtenez commencé à construire d’excellentes applications personnalisées directement Visual Studio avec le Microsoft Teams Shared Computer Toolkit
keywords: équipes kit d’outils studio visuel
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
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="422e4-104">Créez des applications avec les Teams Shared Computer Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="422e4-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="422e4-105">Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="422e4-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="422e4-106">Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="422e4-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="422e4-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="422e4-107">Prerequisites</span></span>

1. <span data-ttu-id="422e4-108">[Activer l’aperçu des développeurs](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="422e4-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="422e4-109">Assurez-vous que **<span>le module ASP.NE</span>T et web a** été ajouté à votre instance Visual Studio web.</span><span class="sxs-lookup"><span data-stu-id="422e4-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="422e4-110">Vous pouvez vérifier en suivant les étapes de la modification de la [Visual Studio en ajoutant ou en supprimant les charges de travail et la](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation des composants.</span><span class="sxs-lookup"><span data-stu-id="422e4-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![module visuel de asp.net studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="422e4-112">Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, vous devrez faire installer IIS (Internet Information Services) dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="422e4-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="422e4-113">Visual Studio n’inclut pas IIS et il n’est pas inclus dans la configuration Windows 10, Windows 8 ou Windows 7; toutefois, vous pouvez télécharger la dernière version à partir du centre [de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).</span><span class="sxs-lookup"><span data-stu-id="422e4-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Vue de la page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="422e4-115">Installez le Teams Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="422e4-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="422e4-116">Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement sur [le Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="422e4-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="422e4-117">Utilisation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="422e4-117">Using the toolkit</span></span>

- [<span data-ttu-id="422e4-118">Mettre en place un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="422e4-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="422e4-119">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="422e4-120">Emballez votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="422e4-121">Exécutez votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="422e4-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="422e4-122">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="422e4-123">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="422e4-124">Mettre en place un nouveau projet Teams projet</span><span class="sxs-lookup"><span data-stu-id="422e4-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="422e4-125">Sélectionnez **Créer un nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="422e4-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="422e4-126">Choisissez **Microsoft Teams appe et** sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="422e4-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="422e4-127">Vous arriverez à **l’écran Configurer votre nouveau** projet où vous pouvez choisir le nom **Project,** **emplacement,** et le nom **de la solution**.</span><span class="sxs-lookup"><span data-stu-id="422e4-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="422e4-128">Cochez la case **labeled Place solution et projet dans le même répertoire**.</span><span class="sxs-lookup"><span data-stu-id="422e4-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="422e4-129">Une fenêtre contexturée étiquetée **Add Capabilities vous** permettra de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="422e4-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="422e4-130">Sélectionnez **le bouton** Suivant pour compléter le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="422e4-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="422e4-131">Une fenêtre contexturée étiquetée **Add Capabilities** vous permettra de choisir les propriétés pour chaque capacité sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="422e4-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="422e4-132">Sélectionnez **Finition** et vous atterrirez sur la page **Microsoft Teams Shared Computer Toolkit** de destination.</span><span class="sxs-lookup"><span data-stu-id="422e4-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="422e4-133">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-133">Configure your app</span></span>

<span data-ttu-id="422e4-134">À la base, l Teams apprateur de messagerie embrasse trois composantes :</span><span class="sxs-lookup"><span data-stu-id="422e4-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="422e4-135">Le Microsoft Teams client (web, bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="422e4-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="422e4-136">Un serveur qui répond aux demandes de contenu qui seront affichées en Teams, par exemple, le contenu de l’onglet HTML ou une carte adaptative bot .</span><span class="sxs-lookup"><span data-stu-id="422e4-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="422e4-137">Un paquet Teams’application se compose de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="422e4-137">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="422e4-138">Le manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="422e4-138">The manifest.json</span></span>
      > - <span data-ttu-id="422e4-139">Une [icône couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications publiques ou organisation</span><span class="sxs-lookup"><span data-stu-id="422e4-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
      > - <span data-ttu-id="422e4-140">Une [icône de contour](../resources/schema/manifest-schema.md#icons) pour l’affichage sur la barre d Teams’activité.</span><span class="sxs-lookup"><span data-stu-id="422e4-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="422e4-141">Lorsqu’une application est installée, le client Teams parse le fichier manifeste pour déterminer les informations nécessaires comme le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="422e4-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="422e4-142">Si vous ne l’avez pas déjà fait, vous devrez vous connecter à votre Microsoft 365 ou compte pour poursuivre le processus de développement.</span><span class="sxs-lookup"><span data-stu-id="422e4-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="422e4-143">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un [abonnement Microsoft 365 programme de développement.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="422e4-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="422e4-144">Il est gratuit *pendant* 90 jours et sera continuellement renouvelé tant que vous l’utilisez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="422e4-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="422e4-145">Si vous avez un abonnement Visual Studio *Enterprise* *ou Professional,* les deux programmes incluent un abonnement gratuit de développeur [Microsoft 365,](https://aka.ms/MyVisualStudioBenefits)actif pour la durée de vie de votre abonnement Visual Studio abonnement.</span><span class="sxs-lookup"><span data-stu-id="422e4-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="422e4-146">Pour plus d’informations, [voir Configurer un abonnement Microsoft 365 développeur .](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="422e4-146">For more information, See [Set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="422e4-147">Étapes de configuration</span><span class="sxs-lookup"><span data-stu-id="422e4-147">Configuration steps</span></span>

1. <span data-ttu-id="422e4-148">Pour configurer votre application, sur la page **de Microsoft Teams Shared Computer Toolkit,** sélectionnez **Modifier le package de l’application**.</span><span class="sxs-lookup"><span data-stu-id="422e4-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="422e4-149">À partir du menu de drop-down **My Environments,** sélectionnez **développement**.</span><span class="sxs-lookup"><span data-stu-id="422e4-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="422e4-150">Vous atterrirez sur la page **de détails de** l’application où vous pourrez modifier les champs de propriété de votre application.</span><span class="sxs-lookup"><span data-stu-id="422e4-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="422e4-151">L’édition des champs dans la page détails de l’application met à jour le contenu des manifest.jsdans le fichier qui sera finalement expédié dans le cadre du paquet d’application.</span><span class="sxs-lookup"><span data-stu-id="422e4-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="422e4-152">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="422e4-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="422e4-153">Emballez votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-153">Package your app</span></span>

<span data-ttu-id="422e4-154">La modification de la page **des détails** de l’application ou la **mise à** jour du manifeste, ou les fichiers **.env dans** le dossier  **.publish de** votre application **généreront automatiquementDevelopment.zip** fichier.</span><span class="sxs-lookup"><span data-stu-id="422e4-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="422e4-155">Le Development.zip inclut trois fichiers requis : le **manifest.jset** [deux icônes](../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="422e4-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="422e4-156">Installez et exécutez votre application localement</span><span class="sxs-lookup"><span data-stu-id="422e4-156">Install and run your app locally</span></span>

1. <span data-ttu-id="422e4-157">À partir du menu **de dropdown configurations** de solution, **sélectionnez Déployer** comme indiqué dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="422e4-157">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![Menu configurations de solutions](../assets/images/solution-configurations.png)

2. <span data-ttu-id="422e4-159">Sélectionnez **le bouton IIS Express + Teams** + .</span><span class="sxs-lookup"><span data-stu-id="422e4-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="422e4-160">Teams lancera et le dialogue d’installation de l’application doit apparaître dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="422e4-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="422e4-161">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="422e4-161">Validate your app</span></span>

<span data-ttu-id="422e4-162">La page **Validate** vous permet de vérifier le package de votre application avant de soumettre votre application à AppSource.</span><span class="sxs-lookup"><span data-stu-id="422e4-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="422e4-163">Il suffit de télécharger le paquet manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés manifestes.</span><span class="sxs-lookup"><span data-stu-id="422e4-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="422e4-164">Pour chaque test échoué, la description fournit un lien de documentation pour vous aider à corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="422e4-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="422e4-165">Pour les tests difficiles à automatiser, la liste de vérification préliminaire détaille 7 des cas de test échoués les plus courants ainsi qu’un lien vers une liste de vérification complète de la soumission. </span><span class="sxs-lookup"><span data-stu-id="422e4-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="422e4-166">Publier votre application sur Teams</span><span class="sxs-lookup"><span data-stu-id="422e4-166">Publish your app to Teams</span></span>

<span data-ttu-id="422e4-167">✔ Sur votre page d’accueil du projet, vous pouvez télécharger votre application à une équipe, soumettre votre application à votre app store personnalisé pour les utilisateurs de votre organisation, ou soumettre votre application à App Source pour tous les utilisateurs de Teams.</span><span class="sxs-lookup"><span data-stu-id="422e4-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="422e4-168">✔ votre administrateur informatique examinera ces soumissions.</span><span class="sxs-lookup"><span data-stu-id="422e4-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="422e4-169">✔ Vous pouvez revenir à la page **Publier** pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous viendront soumettre des mises à jour à votre application ou annuler toutes les soumissions actuellement actives.</span><span class="sxs-lookup"><span data-stu-id="422e4-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="422e4-170">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="422e4-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="422e4-171">Maintenir et soutenir votre application publiée</span><span class="sxs-lookup"><span data-stu-id="422e4-171">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
