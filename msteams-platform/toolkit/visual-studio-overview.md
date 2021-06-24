---
title: Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio
description: Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide Microsoft Teams Shared Computer Toolkit
keywords: boîte à outils visual studio teams
localization_priority: Normal
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 6a0f466ba0d95312695be8b5460fc949e3f70811
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095513"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="99fea-104">Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99fea-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="99fea-105">Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99fea-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="99fea-106">Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="99fea-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99fea-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="99fea-107">Prerequisites</span></span>

1. <span data-ttu-id="99fea-108">[Activer la prévisualisation pour les développeurs.](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)</span><span class="sxs-lookup"><span data-stu-id="99fea-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

2. <span data-ttu-id="99fea-109">Assurez-vous que **<span>le</span> module ASP.NET** de développement web a été ajouté à votre instance Visual Studio web.</span><span class="sxs-lookup"><span data-stu-id="99fea-109">Make sure that the **<span>ASP.NET</span> and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="99fea-110">Pour plus d’informations, voir Modifier Visual Studio en ajoutant ou en supprimant des charges de travail [et des composants.](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="99fea-110">For more information, see [Modify Visual Studio by adding or removing workloads and components](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).</span></span>

![Module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="99fea-112">Installer le Teams Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="99fea-112">Install the Teams Toolkit</span></span>

<span data-ttu-id="99fea-113">Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) ou directement à partir du menu **Extensions** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99fea-113">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="use-the-toolkit"></a><span data-ttu-id="99fea-114">Utiliser le kit de ressources</span><span class="sxs-lookup"><span data-stu-id="99fea-114">Use the toolkit</span></span>

- [<span data-ttu-id="99fea-115">Configurer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="99fea-115">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="99fea-116">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="99fea-116">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="99fea-117">Exécuter votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="99fea-117">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="99fea-118">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="99fea-118">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="99fea-119">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="99fea-119">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="99fea-120">Configurer un nouveau projet Teams projet</span><span class="sxs-lookup"><span data-stu-id="99fea-120">Set up a new Teams project</span></span>

1. <span data-ttu-id="99fea-121">Lancez Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="99fea-121">Launch Visual Studio 2019.</span></span>
2. <span data-ttu-id="99fea-122">Sélectionnez **Créer un projet.**</span><span class="sxs-lookup"><span data-stu-id="99fea-122">Select **Create a new project**.</span></span>
3. <span data-ttu-id="99fea-123">Recherchez **Microsoft Teams app et** sélectionnez **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="99fea-123">Search for **Microsoft Teams App** and select **Next**.</span></span>
4. <span data-ttu-id="99fea-124">Dans la **zone Configurer votre nouveau projet,** entrez le **Project,** **l’emplacement** et le **nom de la solution.**</span><span class="sxs-lookup"><span data-stu-id="99fea-124">In the **Configure your new project**, enter the **Project name**, **Location**, and **Solution name**.</span></span>
5. <span data-ttu-id="99fea-125">Sélectionnez **Suivant** pour entrer un nom pour l’application.</span><span class="sxs-lookup"><span data-stu-id="99fea-125">Select **Next** to enter a name for the app.</span></span>
6. <span data-ttu-id="99fea-126">Dans l’écran Informations supplémentaires,  entrez un nom **d’application** et un nom de développeur ou de société pour Teams application.</span><span class="sxs-lookup"><span data-stu-id="99fea-126">In the Additional Information screen, enter an **Application Name** and **Developer or Company name** for your Teams app.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="99fea-127">Configurer votre application</span><span class="sxs-lookup"><span data-stu-id="99fea-127">Configure your app</span></span>

<span data-ttu-id="99fea-128">L’application Teams principale englobe trois composants :</span><span class="sxs-lookup"><span data-stu-id="99fea-128">At its core, the Teams app embraces three components:</span></span>

- <span data-ttu-id="99fea-129">Le Microsoft Teams client (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="99fea-129">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
- <span data-ttu-id="99fea-130">Serveur qui répond aux demandes de contenu affichées dans Teams.</span><span class="sxs-lookup"><span data-stu-id="99fea-130">A server that responds to requests for content displayed in Teams.</span></span> <span data-ttu-id="99fea-131">Par exemple, le contenu d’onglet HTML ou une carte adaptative de bot.</span><span class="sxs-lookup"><span data-stu-id="99fea-131">For example, HTML tab content or a bot adaptive card.</span></span>
- <span data-ttu-id="99fea-132">Un package Teams’application se compose de trois fichiers :</span><span class="sxs-lookup"><span data-stu-id="99fea-132">A Teams app package consists of three files:</span></span>

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="99fea-133">Le manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="99fea-133">The manifest.json</span></span>
    > - <span data-ttu-id="99fea-134">Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="99fea-134">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
    > - <span data-ttu-id="99fea-135">Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.</span><span class="sxs-lookup"><span data-stu-id="99fea-135">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="99fea-136">Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.</span><span class="sxs-lookup"><span data-stu-id="99fea-136">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="99fea-137">Si ce n’est pas déjà fait, vous devez vous Microsoft 365 votre compte d’utilisateur pour poursuivre le processus de développement.</span><span class="sxs-lookup"><span data-stu-id="99fea-137">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="99fea-138">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement [Microsoft 365 programme pour les développeurs.](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="99fea-138">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="99fea-139">Il est gratuit pendant 90 jours et renouvelé tant que vous l’utilisez pour l’activité de développement.</span><span class="sxs-lookup"><span data-stu-id="99fea-139">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="99fea-140">Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 développeur [gratuit,](https://aka.ms/MyVisualStudioBenefits)actif pendant toute la durée de Visual Studio abonnement.</span><span class="sxs-lookup"><span data-stu-id="99fea-140">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="99fea-141">Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="99fea-141">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="99fea-142">Étapes de configuration</span><span class="sxs-lookup"><span data-stu-id="99fea-142">Configuration steps</span></span>

1. <span data-ttu-id="99fea-143">Pour configurer votre application, sélectionnez le menu Project > TeamsFx > configurer pour l’électrable **SSO....**</span><span class="sxs-lookup"><span data-stu-id="99fea-143">To configure your app, select the **Project > TeamsFx > Configure for SSO...** menu.</span></span>

<span data-ttu-id="99fea-144">Lorsque vous y invitez, connectez-vous à votre compte Microsoft qui possède un client M365.</span><span class="sxs-lookup"><span data-stu-id="99fea-144">When prompted, sign in to your Microsoft account that has an M365 tenant.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="99fea-145">Installer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="99fea-145">Install and run your app locally</span></span>

<span data-ttu-id="99fea-146">Appuyez sur F5 pour démarrer le débogage.</span><span class="sxs-lookup"><span data-stu-id="99fea-146">Press F5 to start debugging.</span></span> <span data-ttu-id="99fea-147">La boîte de dialogue d’installation de l’application s’affiche dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="99fea-147">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="99fea-148">Valider votre application</span><span class="sxs-lookup"><span data-stu-id="99fea-148">Validate your app</span></span>

<span data-ttu-id="99fea-149">Le menu **Project > validation teamsFx** > Teams manifeste vous permet de vérifier que votre package d’application est valide.</span><span class="sxs-lookup"><span data-stu-id="99fea-149">The **Project > TeamsFx Validate > Teams Manifest** menu allows you to check that your app package is valid.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="99fea-150">Publier votre application sur Teams</span><span class="sxs-lookup"><span data-stu-id="99fea-150">Publish your app to Teams</span></span>

<span data-ttu-id="99fea-151">Dans le portail du développeur [Teams,](https://dev.teams.microsoft.com/home)vous pouvez télécharger votre application vers une équipe, soumettre votre application au magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source d’application pour tous les utilisateurs Teams.</span><span class="sxs-lookup"><span data-stu-id="99fea-151">In the [Teams Developer Portal](https://dev.teams.microsoft.com/home), you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

- <span data-ttu-id="99fea-152">Votre administrateur informatique examine ces envois.</span><span class="sxs-lookup"><span data-stu-id="99fea-152">Your IT admin will review these submissions.</span></span>
- <span data-ttu-id="99fea-153">Vous pouvez revenir à **la** page Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous pouvez soumettre des mises à jour à votre application ou annuler les soumissions actives.</span><span class="sxs-lookup"><span data-stu-id="99fea-153">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="99fea-154">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="99fea-154">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99fea-155">Créer et exécuter votre première application Microsoft Teams avec Blazor</span><span class="sxs-lookup"><span data-stu-id="99fea-155">Build and run your first Microsoft Teams app with Blazor</span></span>](../get-started/first-app-blazor.md)
