---
title: Créer et exécuter votre première application teams
author: heath-hamilton
description: Exécutez votre première application Microsoft Teams.
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651984"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="611ed-103">Créer et exécuter votre première application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="611ed-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="611ed-104">Vous pouvez accéder directement au développement sur la plateforme Microsoft teams en générant et en exécutant rapidement une application de base.</span><span class="sxs-lookup"><span data-stu-id="611ed-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic app.</span></span>

> [!NOTE]
> <span data-ttu-id="611ed-105">Il est utile de posséder des connaissances pratiques sur JavaScript (en particulier REACT) lorsque vous suivez ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="611ed-105">It's helpful to have working knowledge of JavaScript (specifically React) when following these tutorials.</span></span>

## <a name="set-up-your-development-account"></a><span data-ttu-id="611ed-106">Configurer votre compte de développement</span><span class="sxs-lookup"><span data-stu-id="611ed-106">Set up your development account</span></span>

<span data-ttu-id="611ed-107">Pour créer des applications pour Teams, vous avez besoin d’un compte teams qui autorise chargement (votre compte peut déjà fournir cette opération).</span><span class="sxs-lookup"><span data-stu-id="611ed-107">To build apps for Teams, you need a Teams account that allows sideloading (your account may already provide this).</span></span> <span data-ttu-id="611ed-108">Si ce n’est pas le cas, inscrivez-vous pour un abonnement développeur Microsoft 365 afin de pouvoir obtenir un client test.</span><span class="sxs-lookup"><span data-stu-id="611ed-108">If it doesn't, register for a Microsoft 365 developer subscription so you can get a test tenant.</span></span>

1. <span data-ttu-id="611ed-109">Vérifiez si vous pouvez chargement des applications dans teams :</span><span class="sxs-lookup"><span data-stu-id="611ed-109">Verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="611ed-110">Dans le client Teams, sélectionnez **applications**.</span><span class="sxs-lookup"><span data-stu-id="611ed-110">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="611ed-111">Recherchez une option permettant de **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="611ed-111">Look for an option to **Upload a custom app**.</span></span>
1. <span data-ttu-id="611ed-112">Si vous avez cette option, vous pouvez commencer à créer.</span><span class="sxs-lookup"><span data-stu-id="611ed-112">If you have this option, you can start building.</span></span> <span data-ttu-id="611ed-113">Si ce n’est pas le cas, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="611ed-113">If not, do the following:</span></span>
    1. <span data-ttu-id="611ed-114">Inscrivez-vous pour un [abonnement développeur Microsoft 365](../doc-links/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="611ed-114">Register for a [Microsoft 365 developer subscription](../doc-links/prepare-your-o365-tenant.md).</span></span>
    1. <span data-ttu-id="611ed-115">[Activez l’application personnalisée chargement](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) pour votre compte de test.</span><span class="sxs-lookup"><span data-stu-id="611ed-115">[Enable custom app sideloading](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for your test account.</span></span>

## <a name="get-your-development-tools"></a><span data-ttu-id="611ed-116">Obtenir vos outils de développement</span><span class="sxs-lookup"><span data-stu-id="611ed-116">Get your development tools</span></span>

<span data-ttu-id="611ed-117">Vous pouvez créer des applications teams avec vos outils préférés, mais voici ce dont vous avez besoin pour commencer rapidement avec Visual Studio code et Microsoft teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="611ed-117">You can build Teams apps with your preferred tools, but here's what you need to get started quickly with Visual Studio Code and the Microsoft Teams Toolkit.</span></span>

1. <span data-ttu-id="611ed-118">Installez la dernière version de [Visual Studio code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="611ed-118">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span>
1. <span data-ttu-id="611ed-119">Dans Visual Studio code, sélectionnez **Extensions** ![ Visual Studio Toolkit View ](../doc-links/images/vs-code-extensions.png) sur la barre d’activité de gauche et Install the **Microsoft teams Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="611ed-119">In Visual Studio Code, select **Extensions** ![visual studio toolkit view](../doc-links/images/vs-code-extensions.png) on the left Activity Bar and install the **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="611ed-120">Installez [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="611ed-120">Install [Node.js](https://nodejs.org/en/).</span></span>

## <a name="create-an-app-project"></a><span data-ttu-id="611ed-121">Créer un projet d’application</span><span class="sxs-lookup"><span data-stu-id="611ed-121">Create an app project</span></span>

<span data-ttu-id="611ed-122">La boîte à outils Microsoft teams peut vous aider à configurer votre premier projet d’application.</span><span class="sxs-lookup"><span data-stu-id="611ed-122">The Microsoft Teams Toolkit can help you set up your first app project.</span></span>

1. <span data-ttu-id="611ed-123">Dans Visual Studio code, ouvrez la boîte à outils en sélectionnant l’icône Teams.</span><span class="sxs-lookup"><span data-stu-id="611ed-123">In Visual Studio Code, open the toolkit by selecting the Teams icon</span></span> ![icône teams](../doc-links/images/favicon-16x16.png) <span data-ttu-id="611ed-125">dans la barre d’activité de gauche.</span><span class="sxs-lookup"><span data-stu-id="611ed-125">on the left Activity Bar.</span></span>
1. <span data-ttu-id="611ed-126">Sélectionnez **créer une nouvelle application teams**.</span><span class="sxs-lookup"><span data-stu-id="611ed-126">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="611ed-127">Lorsque vous y êtes invité, entrez un nom pour votre application.</span><span class="sxs-lookup"><span data-stu-id="611ed-127">When prompted, enter a name for your app.</span></span> <span data-ttu-id="611ed-128">Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="611ed-128">This is the default name for your app and also the name of the project directory on your local machine.</span></span>
1. <span data-ttu-id="611ed-129">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="611ed-129">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="611ed-130">Activez l’option **onglet personnel** , puis sélectionnez **Terminer** pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="611ed-130">Check the **Personal tab** option and select **Finish** to configure your project.</span></span>

![vue ajouter des onglets de la boîte à outils](../doc-links/images/toolkit-add-tabs.PNG)

<span data-ttu-id="611ed-132">Une fois terminé, vous disposez des composants d’échafaudage de l’application pour la création d’un onglet personnel.</span><span class="sxs-lookup"><span data-stu-id="611ed-132">Once complete, you have the app scaffolding components for building a personal tab.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="611ed-133">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="611ed-133">Run your app</span></span>

<span data-ttu-id="611ed-134">Suivez le `README.md` dans votre projet pour générer, exécuter et déployer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="611ed-134">Follow the `README.md` in your project to build, run, and deploy your app to Teams.</span></span> <span data-ttu-id="611ed-135">En règle générale, ces instructions vous aident à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="611ed-135">In general, these instructions help you do the following:</span></span>

* <span data-ttu-id="611ed-136">Héberger votre application sur `localhost` .</span><span class="sxs-lookup"><span data-stu-id="611ed-136">Host your app on `localhost`.</span></span>
* <span data-ttu-id="611ed-137">[Configurez un tunnel sécurisé avec ngrok](../doc-links/debug.md#locally-hosted) afin que les équipes puissent accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="611ed-137">[Set up a secure tunnel with ngrok](../doc-links/debug.md#locally-hosted) so that Teams can access your app.</span></span> <span data-ttu-id="611ed-138">(Installer [ngrok](https://ngrok.com/download).)</span><span class="sxs-lookup"><span data-stu-id="611ed-138">(Install [ngrok](https://ngrok.com/download).)</span></span>
* <span data-ttu-id="611ed-139">[Chargement votre application](../doc-links/apps-upload.md) dans le client teams à l’aide du `Development.zip` dans le `.publish` dossier.</span><span class="sxs-lookup"><span data-stu-id="611ed-139">[Sideload your app](../doc-links/apps-upload.md) in the Teams client using the `Development.zip` in the `.publish` folder.</span></span>

<span data-ttu-id="611ed-140">Une fois que vous avez chargement votre application, elle doit ressembler à ce qui suit dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="611ed-140">Once you sideload your app, it should look like this in the Teams client.</span></span>

![Onglet exemple Hello World](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a><span data-ttu-id="611ed-142">Fichiers de projet d’application importants</span><span class="sxs-lookup"><span data-stu-id="611ed-142">Important app project files</span></span>

<span data-ttu-id="611ed-143">Avec votre projet d’application et la configuration de la génération de modèles automatique, prenez le temps de comprendre certains des principaux fichiers que les développeurs d’applications teams utilisent.</span><span class="sxs-lookup"><span data-stu-id="611ed-143">With your app project and scaffolding set up, take some time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="611ed-144">Manifeste de l’application ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="611ed-144">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="611ed-145">Situé dans l' `.publish` annuaire, le manifeste de l’application est le point de départ de tout projet d’application.</span><span class="sxs-lookup"><span data-stu-id="611ed-145">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="611ed-146">Le manifeste définit les attributs fondamentaux de votre application et pointe vers les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="611ed-146">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="611ed-147">Lorsque vous installez une application, teams analyse le manifeste pour comprendre comment afficher votre application dans le client.</span><span class="sxs-lookup"><span data-stu-id="611ed-147">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

<span data-ttu-id="611ed-148">Dans les didacticiels suivants, vous allez vous concentrer sur les sections du manifeste de l’application pour la création d’onglets de canaux et personnels.</span><span class="sxs-lookup"><span data-stu-id="611ed-148">In the following tutorials, you'll focus on the sections of the app manifest for building personal and channel tabs.</span></span>

### <a name="package-developmentzip"></a><span data-ttu-id="611ed-149">Package ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="611ed-149">Package (`Development.zip`)</span></span>

<span data-ttu-id="611ed-150">Dans l' `.publish` annuaire, vous avez également besoin du package d’application pour [chargement votre application](../../overview.md#how-can-you-share-your-teams-app) dans Teams.</span><span class="sxs-lookup"><span data-stu-id="611ed-150">Also located in the `.publish` directory, you need the app package to [sideload your app](../../overview.md#how-can-you-share-your-teams-app) in Teams.</span></span> <span data-ttu-id="611ed-151">Il est également utilisé lors [de la publication dans le catalogue d’applications de votre organisation](../../overview.md#how-can-you-share-your-teams-app) ou [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span><span class="sxs-lookup"><span data-stu-id="611ed-151">It's also used when [publishing to your organization's app catalog](../../overview.md#how-can-you-share-your-teams-app) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="611ed-152">Voici quelques détails sur les fichiers de package d’application :</span><span class="sxs-lookup"><span data-stu-id="611ed-152">Here are some details about the app package files:</span></span>

|<span data-ttu-id="611ed-153">Nom</span><span class="sxs-lookup"><span data-stu-id="611ed-153">Name</span></span>|<span data-ttu-id="611ed-154">Type</span><span class="sxs-lookup"><span data-stu-id="611ed-154">Type</span></span>|<span data-ttu-id="611ed-155">Size</span><span class="sxs-lookup"><span data-stu-id="611ed-155">Size</span></span>|<span data-ttu-id="611ed-156">Emplacement du manifeste</span><span class="sxs-lookup"><span data-stu-id="611ed-156">Manifest location</span></span>|<span data-ttu-id="611ed-157">Nom de fichier du Toolkit</span><span class="sxs-lookup"><span data-stu-id="611ed-157">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="611ed-158">**Manifeste de l’application**</span><span class="sxs-lookup"><span data-stu-id="611ed-158">**App manifest**</span></span>|`.json`| <span data-ttu-id="611ed-159">—</span><span class="sxs-lookup"><span data-stu-id="611ed-159">—</span></span> | <span data-ttu-id="611ed-160">—</span><span class="sxs-lookup"><span data-stu-id="611ed-160">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="611ed-161">**Logo couleur**</span><span class="sxs-lookup"><span data-stu-id="611ed-161">**Color logo**</span></span>|`.png`|<span data-ttu-id="611ed-162">192 &times; 192 pixels</span><span class="sxs-lookup"><span data-stu-id="611ed-162">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="611ed-163">**Logo de plan**</span><span class="sxs-lookup"><span data-stu-id="611ed-163">**Outline logo**</span></span>|`.png`|<span data-ttu-id="611ed-164">32 &times; 32 pixels</span><span class="sxs-lookup"><span data-stu-id="611ed-164">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a><span data-ttu-id="611ed-165">Génération de modèles ( `src` )</span><span class="sxs-lookup"><span data-stu-id="611ed-165">Scaffolding (`src`)</span></span>

<span data-ttu-id="611ed-166">Le kit de fonctions crée automatiquement une structure pour vous dans le `src` répertoire en fonction des fonctionnalités que vous avez ajoutées lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="611ed-166">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="611ed-167">Certains fichiers sont créés, quel que soit le type d’application dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="611ed-167">Some files are created no matter what kind of app you have, though.</span></span> <span data-ttu-id="611ed-168">Par exemple, le `App.js` fichier dans le `src/components` répertoire est important, car il gère l’initialisation et le routage de votre application.</span><span class="sxs-lookup"><span data-stu-id="611ed-168">For example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="611ed-169">Plus important encore, il appelle le [Kit de développement logiciel (SDK) Microsoft teams](../doc-links/using-teams-client-sdk.md) pour établir la communication entre votre application et Teams.</span><span class="sxs-lookup"><span data-stu-id="611ed-169">Most importantly, it calls the [Microsoft Teams SDK](../doc-links/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

<span data-ttu-id="611ed-170">Pour plus d’informations sur la génération de modèles automatique dans les didacticiels, consultez la rubrique Création d’onglets personnels et de chaînes.</span><span class="sxs-lookup"><span data-stu-id="611ed-170">You can learn more about scaffolding in the tutorials for creating personal and channel tabs.</span></span>

## <a name="next-step"></a><span data-ttu-id="611ed-171">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="611ed-171">Next step</span></span>

<span data-ttu-id="611ed-172">🎉 Félicitations !</span><span class="sxs-lookup"><span data-stu-id="611ed-172">🎉 Congratulations!</span></span> <span data-ttu-id="611ed-173">Vous avez une application teams en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="611ed-173">You have a running Teams app.</span></span> <span data-ttu-id="611ed-174">Cliquez sur le bouton suivant pour découvrir comment ajouter une fonctionnalité de monde réel.</span><span class="sxs-lookup"><span data-stu-id="611ed-174">Select the following button to learn how to add a real-world feature to it.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="611ed-175">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="611ed-175">Build a personal tab</span></span>](add-personal-tab.md)
