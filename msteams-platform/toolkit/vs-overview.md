---
title: Créer des applications avec Microsoft teams Toolkit et Visual Studio
description: Commencer à créer des applications personnalisées directement dans Visual Studio à l’aide du kit de développement Microsoft teams
keywords: Kit de développement Visual Studio teams
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: Auto
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051710"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="3c7e2-104">Créer des applications avec Microsoft teams Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c7e2-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="3c7e2-105">Le kit de développement Microsoft teams vous permet de créer des applications teams personnalisées directement dans l’environnement Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio environment.</span></span> <span data-ttu-id="3c7e2-106">Le kit de développement vous guide tout au long du processus et vous fournit tout ce dont vous avez besoin pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="3c7e2-107">Installation du kit de développement teams</span><span class="sxs-lookup"><span data-stu-id="3c7e2-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="3c7e2-108">Microsoft teams Toolkit pour Visual Studio peut être téléchargé à partir de [Visual Studio Marketplace](https://aka.ms/teams-toolkit) ou directement en tant qu’extension dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-108">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="3c7e2-109">Utilisation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="3c7e2-109">Using the toolkit</span></span>

- [<span data-ttu-id="3c7e2-110">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="3c7e2-110">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="3c7e2-111">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-111">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="3c7e2-112">Empaquetage de votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-112">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="3c7e2-113">Exécuter votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="3c7e2-113">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="3c7e2-114">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-114">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="3c7e2-115">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-115">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="3c7e2-116">Configurer un nouveau projet teams</span><span class="sxs-lookup"><span data-stu-id="3c7e2-116">Set up a new Teams project</span></span>

1. <span data-ttu-id="3c7e2-117">Créez un projet et sélectionnez le modèle Microsoft Terams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-117">Create a new project and select the Microsoft Terams Toolkit template.</span></span>
1. <span data-ttu-id="3c7e2-118">Vous arrivez à l’écran **Add Capabilities** pour configurer les propriétés de votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-118">You will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="3c7e2-119">Cliquez sur le bouton **Terminer** pour terminer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-119">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="3c7e2-120">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-120">Configure your app</span></span>

<span data-ttu-id="3c7e2-121">À son niveau principal, l’application teams adopte trois composants :</span><span class="sxs-lookup"><span data-stu-id="3c7e2-121">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="3c7e2-122">Le client Microsoft Teams (Web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-122">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="3c7e2-123">Serveur qui répond aux demandes de contenu qui s’affichent dans Teams, par exemple, le contenu de l’onglet HTML ou une carte de robot.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-123">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="3c7e2-124">Package d' [application](/concepts/build-and-test/apps-package.md) teams comprenant trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="3c7e2-124">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="3c7e2-125">La manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="3c7e2-125">The manifest.json</span></span> 
  > - <span data-ttu-id="3c7e2-126">Une [icône de couleur](../resources/schema/manifest-schema.md#icons) pour l’affichage de votre application dans le catalogue d’applications public ou d’organisation</span><span class="sxs-lookup"><span data-stu-id="3c7e2-126">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="3c7e2-127">[Icône de plan](../resources/schema/manifest-schema.md#icons) pour l’affichage dans la barre d’activité de teams.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-127">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="3c7e2-128">Lorsqu’une application est installée, le client teams analyse le fichier manifeste pour déterminer les informations nécessaires telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-128">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="3c7e2-129">Pour configurer votre application, accédez à la fenêtre d’extension de **Microsoft teams Toolkit** .</span><span class="sxs-lookup"><span data-stu-id="3c7e2-129">To configure your app, navigate to the **Microsoft Teams Toolkit** extension window.</span></span>
1. <span data-ttu-id="3c7e2-130">Sélectionnez **modifier le package d’application** pour afficher la page des détails de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="3c7e2-130">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="3c7e2-131">La modification des champs de la page des détails de l’application met à jour le contenu de la manifest.jssur un fichier qui sera finalement envoyé dans le cadre du package d’application.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-131">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="3c7e2-132">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="3c7e2-132">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="3c7e2-133">Empaquetage de votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-133">Package your app</span></span>

<span data-ttu-id="3c7e2-134">Modification vous êtes la page de détails de l' **application** ou vous mettez à jour le **manifeste**, ou les fichiers **. env** dans le dossier **. Publish** de votre application généreront automatiquement votre fichier **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="3c7e2-134">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="3c7e2-135">Vous devez inclure [deux icônes](../concepts/build-and-test/apps-package.md#icons) dans ce même dossier.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-135">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="3c7e2-136">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="3c7e2-136">Install and run your app locally</span></span>

<span data-ttu-id="3c7e2-137">Dans le menu déroulant *configurations de solutions* , sélectionnez *déployer*.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-137">From the *Solutions Configurations* dropdown menu, select *Deploy*.</span></span> <span data-ttu-id="3c7e2-138">Appuyez sur le bouton *ISS Express + teams* .</span><span class="sxs-lookup"><span data-stu-id="3c7e2-138">Press the *ISS Express + Teams* button.</span></span> <span data-ttu-id="3c7e2-139">Teams se lance et la boîte de dialogue d’installation de l’application doit apparaître dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-139">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="3c7e2-140">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="3c7e2-140">Validate your app</span></span>

<span data-ttu-id="3c7e2-141">La page **Validate** vous permet de vérifier votre package d’application avant d’envoyer votre application à AppSource.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-141">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="3c7e2-142">Téléchargez simplement le package de manifeste et l’outil de validation vérifiera votre application par rapport à tous les cas de test liés au manifeste.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-142">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="3c7e2-143">Pour chaque test ayant échoué, la description fournit un lien vers la documentation pour vous aider à résoudre l’erreur.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-143">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="3c7e2-144">Pour les tests difficiles à automatiser, la liste de **vérification préliminaire** décrit les 7 des cas de test ayant échoué les plus fréquents, ainsi que le lien vers une liste de contrôle d’envoi complète.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-144">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="3c7e2-145">Publier votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="3c7e2-145">Publish your app to Teams</span></span>

<span data-ttu-id="3c7e2-146">Sur la page d’accueil de votre projet, vous pouvez charger votre application dans une équipe, envoyer votre application à votre magasin d’applications personnalisé d’entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source de l’application pour tous les utilisateurs de teams.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-146">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="3c7e2-147">Votre administrateur informatique examinera ces envois.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-147">Your IT admin will review these submissions.</span></span> <span data-ttu-id="3c7e2-148">Vous pouvez revenir à la page *publier* pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. Il s’agit également de l’endroit où vous allez envoyer des mises à jour à votre application ou d’annuler les envois actuellement actifs.</span><span class="sxs-lookup"><span data-stu-id="3c7e2-148">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c7e2-149">Étape suivante : maintenance et prise en charge de votre application publiée</span><span class="sxs-lookup"><span data-stu-id="3c7e2-149">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
