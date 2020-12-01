---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio
description: Commencer à créer des applications personnalisées directement dans Visual Studio à l’aide du kit de développement Microsoft teams
keywords: Kit de développement Visual Studio teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 5ba3cd8b5714876a96595aec295ff6d0066e115f
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476985"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="5672b-104">Créer des applications avec Team Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5672b-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="5672b-105">Le Kit de ressources Microsoft teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5672b-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="5672b-106">Le kit de ressources Microsoft Teams vous guide dans le processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application d’équipe.</span><span class="sxs-lookup"><span data-stu-id="5672b-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5672b-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="5672b-107">Prerequisites</span></span>

1. [<span data-ttu-id="5672b-108">Activer l’Aperçu pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="5672b-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="5672b-109">Assurez-vous que le **<span>ASP.ne</span>T et le module de développement Web** a été ajouté à votre instance Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5672b-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="5672b-110">Vous pouvez vérifier en suivant les étapes de la procédure [modifier Visual Studio en ajoutant ou en supprimant les charges de travail et](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) la documentation des composants.</span><span class="sxs-lookup"><span data-stu-id="5672b-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![module asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="5672b-112">Si vous souhaitez tester votre application en la déployant à partir de Visual Studio, IIS (Internet Information Services) doit être installé dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="5672b-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="5672b-113">Visual Studio n’inclut pas les services Internet (IIS) et il n’est pas inclus dans la configuration par défaut de Windows 10, Windows 8 ou Windows 7 ; Toutefois, vous pouvez télécharger la dernière version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=48264).</span><span class="sxs-lookup"><span data-stu-id="5672b-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![Affichage de la page de téléchargement IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="5672b-115">Installer la boîte à outils teams</span><span class="sxs-lookup"><span data-stu-id="5672b-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="5672b-116">Microsoft teams Toolkit pour Visual Studio peut être téléchargé à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) ou directement à partir du menu **Extensions** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5672b-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="5672b-117">Utilisation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="5672b-117">Using the toolkit</span></span>

- [<span data-ttu-id="5672b-118">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="5672b-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="5672b-119">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="5672b-120">Empaquetage de votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="5672b-121">Exécuter votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="5672b-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="5672b-122">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="5672b-123">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="5672b-124">Configurer un nouveau projet teams</span><span class="sxs-lookup"><span data-stu-id="5672b-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="5672b-125">Sélectionnez **créer un nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="5672b-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="5672b-126">Choisissez **application Microsoft teams** , puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="5672b-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="5672b-127">Vous arrivez à l’écran **configurer votre nouveau projet** , qui vous permet de choisir le **nom du projet**, son **emplacement** et le nom de la **solution**.</span><span class="sxs-lookup"><span data-stu-id="5672b-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="5672b-128">Activez la case à cocher **Placer la solution et le projet dans le même répertoire**.</span><span class="sxs-lookup"><span data-stu-id="5672b-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="5672b-129">Une fenêtre contextuelle intitulée ajouter des **fonctionnalités** vous permet de choisir une ou plusieurs fonctionnalités pour la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="5672b-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="5672b-130">Cliquez sur le bouton **suivant** pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="5672b-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="5672b-131">Une fenêtre contextuelle intitulée ajouter des **fonctionnalités** vous permet de choisir les propriétés de chaque fonctionnalité sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5672b-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="5672b-132">Sélectionnez **Terminer** et vous serez sur la page d’accueil du **Kit Microsoft teams** .</span><span class="sxs-lookup"><span data-stu-id="5672b-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="5672b-133">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-133">Configure your app</span></span>

<span data-ttu-id="5672b-134">À son niveau principal, l’application teams adopte trois composants :</span><span class="sxs-lookup"><span data-stu-id="5672b-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="5672b-135">Le client Microsoft Teams (Web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="5672b-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="5672b-136">Serveur qui répond aux demandes de contenu qui s’affichent dans Teams, par exemple, le contenu de l’onglet HTML ou une carte de robot.</span><span class="sxs-lookup"><span data-stu-id="5672b-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="5672b-137">Package d' [application](/concepts/build-and-test/apps-package.md) teams comprenant trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="5672b-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="5672b-138">La manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="5672b-138">The manifest.json</span></span>
  > - <span data-ttu-id="5672b-139">Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour l’affichage de votre application dans le catalogue d’applications public ou d’organisation</span><span class="sxs-lookup"><span data-stu-id="5672b-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="5672b-140">[Icône de plan](../resources/schema/manifest-schema.md#icons) pour l’affichage dans la barre d’activité de teams.</span><span class="sxs-lookup"><span data-stu-id="5672b-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="5672b-141">Lorsqu’une application est installée, le client teams analyse le fichier manifeste pour déterminer les informations nécessaires telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="5672b-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="5672b-142">Si vous ne l’avez pas déjà fait, vous devez vous connecter à votre compte Microsoft 365 ou pour poursuivre le processus de développement.</span><span class="sxs-lookup"><span data-stu-id="5672b-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="5672b-143">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire pour obtenir un abonnement au [programme de développement microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="5672b-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="5672b-144">Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="5672b-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="5672b-145">Si vous disposez d’un abonnement Visual Studio *entreprise* ou *professionnel* , les deux programmes incluent un [abonnement de développeur](https://aka.ms/MyVisualStudioBenefits)gratuit Microsoft 365, actif pendant la durée de vie de votre abonnement Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5672b-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="5672b-146">*Consultez la rubrique* [configurer un abonnement développeur Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="5672b-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="5672b-147">Étapes de configuration</span><span class="sxs-lookup"><span data-stu-id="5672b-147">Configuration steps</span></span>

1. <span data-ttu-id="5672b-148">Pour configurer votre application, dans la page d’accueil du kit de développement **Microsoft teams** , sélectionnez **modifier le package d’application** .</span><span class="sxs-lookup"><span data-stu-id="5672b-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="5672b-149">Dans le menu déroulant **My environnements** , sélectionnez **Development**.</span><span class="sxs-lookup"><span data-stu-id="5672b-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="5672b-150">Sur la page Détails de l' **application** , vous allez pouvoir modifier les champs de propriétés de votre application.</span><span class="sxs-lookup"><span data-stu-id="5672b-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="5672b-151">La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application.</span><span class="sxs-lookup"><span data-stu-id="5672b-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="5672b-152">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="5672b-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="5672b-153">Empaquetage de votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-153">Package your app</span></span>

<span data-ttu-id="5672b-154">La modification de la page de détails de l' **application** ou la mise à jour du **manifeste**, ou des fichiers **. env** dans le dossier  **. Publish** de votre application, génère automatiquement votre fichier **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="5672b-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="5672b-155">Le fichier Development.zip inclut trois fichiers requis : les **manifest.jssur** et [deux fichiers d’icônes](../concepts/build-and-test/apps-package.md#icons).</span><span class="sxs-lookup"><span data-stu-id="5672b-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="5672b-156">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="5672b-156">Install and run your app locally</span></span>

1. <span data-ttu-id="5672b-157">Dans le menu déroulant **configurations de solutions** , sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="5672b-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Menu configurations de solutions](../assets/images/solution-configurations.png)

2. <span data-ttu-id="5672b-159">Sélectionnez le bouton **ISS Express + teams** .</span><span class="sxs-lookup"><span data-stu-id="5672b-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="5672b-160">Teams se lance et la boîte de dialogue d’installation de l’application doit apparaître dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="5672b-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="5672b-161">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="5672b-161">Validate your app</span></span>

<span data-ttu-id="5672b-162">La page **Validate** vous permet de vérifier votre package d’application avant d’envoyer votre application à AppSource.</span><span class="sxs-lookup"><span data-stu-id="5672b-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="5672b-163">Téléchargez simplement le package de manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés au manifeste.</span><span class="sxs-lookup"><span data-stu-id="5672b-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="5672b-164">Pour chaque test ayant échoué, la description fournit un lien vers la documentation pour vous aider à résoudre l’erreur.</span><span class="sxs-lookup"><span data-stu-id="5672b-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="5672b-165">Pour les tests difficiles à automatiser, la liste de **vérification préliminaire** décrit les 7 des cas de test ayant échoué les plus fréquents, ainsi que le lien vers une liste de contrôle d’envoi complète.</span><span class="sxs-lookup"><span data-stu-id="5672b-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="5672b-166">Publier votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="5672b-166">Publish your app to Teams</span></span>

<span data-ttu-id="5672b-167">✔ Sur la page d’accueil de votre projet, vous pouvez charger votre application dans une équipe, envoyer votre application à votre magasin d’applications personnalisé d’entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs de teams.</span><span class="sxs-lookup"><span data-stu-id="5672b-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="5672b-168">✔ Votre administrateur informatique examinera ces envois.</span><span class="sxs-lookup"><span data-stu-id="5672b-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="5672b-169">✔ Vous pouvez revenir à la page **publier** pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. Il s’agit également de l’endroit où vous allez envoyer des mises à jour à votre application ou d’annuler les envois actuellement actifs.</span><span class="sxs-lookup"><span data-stu-id="5672b-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5672b-170">Étape suivante : maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="5672b-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
