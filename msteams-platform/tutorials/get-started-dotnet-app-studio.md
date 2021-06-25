---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C# ou .NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 58e11312e61124bf09fcb55d2bcd0fc475e75a49
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114610"
---
# <a name="build-your-first-teams-app-using-c"></a><span data-ttu-id="97309-104">Créer votre première application Teams en C #</span><span class="sxs-lookup"><span data-stu-id="97309-104">Build your first Teams app using C#</span></span>

<span data-ttu-id="97309-105">Dans ce didacticiel, vous allez apprendre à créer votre toute première application Microsoft Teams à l’aide de .NET ou C#.</span><span class="sxs-lookup"><span data-stu-id="97309-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using .NET or C#.</span></span> <span data-ttu-id="97309-106">Il vous permet également de suivre les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="97309-106">It also walks you through the steps to:</span></span>

1. [<span data-ttu-id="97309-107">Préparer votre environnement</span><span class="sxs-lookup"><span data-stu-id="97309-107">Prepare your environment</span></span>](#prepare-your-environment)
1. [<span data-ttu-id="97309-108">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="97309-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="97309-109">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="97309-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="97309-110">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="97309-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="97309-111">Héberger l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="97309-111">Host the sample app</span></span>](#hostsample)
1. [<span data-ttu-id="97309-112">Mettre à jour les informations d’identification de votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="97309-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="97309-113">Configurer l’onglet de l’application</span><span class="sxs-lookup"><span data-stu-id="97309-113">Configure the app tab</span></span>](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="97309-114">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="97309-114">Get prerequisites</span></span>

<span data-ttu-id="97309-115">Pour terminer ce didacticiel, vous devez installer les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="97309-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="97309-116">Installer Git</span><span class="sxs-lookup"><span data-stu-id="97309-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="97309-117">Installer Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97309-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="97309-118">Vous pouvez installer l’édition communautaire gratuite de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97309-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="97309-119">Lors de l’installation, s’il existe une option à `git` ajouter au chemin d’accès, sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="97309-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="97309-120">Dans une fenêtre terminal, exécutez la commande suivante pour vérifier votre `git` installation :</span><span class="sxs-lookup"><span data-stu-id="97309-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="97309-121">Utilisez une fenêtre terminal appropriée sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="97309-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="97309-122">Ces exemples utilisent Git Bash, mais peuvent être exécutés sur la plupart des plateformes.</span><span class="sxs-lookup"><span data-stu-id="97309-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="97309-123">Ouvrez la dernière version de Visual Studio et installez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="97309-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="97309-124">Vous pouvez utiliser la même fenêtre terminal pour exécuter les commandes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="97309-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="97309-125">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="97309-125">Download the sample</span></span>

<span data-ttu-id="97309-126">Vous pouvez commencer avec un simple [Hello World !](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="97309-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="97309-127">exemple dans C#.</span><span class="sxs-lookup"><span data-stu-id="97309-127">sample in C#.</span></span> <span data-ttu-id="97309-128">Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="97309-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="97309-129">Vous pouvez [bifurcation](https://help.github.com/articles/fork-a-repo/) [de ce repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) pour modifier et enregistrer vos modifications dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="97309-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="97309-130">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="97309-130">Build and run the sample</span></span>

<span data-ttu-id="97309-131">Vous pouvez créer et exécuter le smaple après son clonage.</span><span class="sxs-lookup"><span data-stu-id="97309-131">You can build and run the smaple after it is cloned.</span></span> 

<span data-ttu-id="97309-132">**Pour créer et exécuter l’exemple cloné**</span><span class="sxs-lookup"><span data-stu-id="97309-132">**To build and run the cloned sample**</span></span>

1. <span data-ttu-id="97309-133">Ouvrez le fichier de solution **Microsoft.Teams. Samples.HelloWorld.sln** à partir du répertoire **Microsoft-Teams-Samples/samples/app-hello-world/csharp** de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="97309-133">Open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span>
1. <span data-ttu-id="97309-134">Sélectionnez **Solution de** build dans **le** menu Build.</span><span class="sxs-lookup"><span data-stu-id="97309-134">Select **Build Solution** from the **Build** menu.</span></span>
1. <span data-ttu-id="97309-135">Sélectionnez **la touche F5** ou démarrez **le débogage** dans le menu **Débogage** pour exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="97309-135">Select the **F5** key, or select **Start Debugging** from the **Debug** menu to run the sample.</span></span>

<span data-ttu-id="97309-136">Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée.</span><span class="sxs-lookup"><span data-stu-id="97309-136">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="97309-137">Vous pouvez utiliser les URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :</span><span class="sxs-lookup"><span data-stu-id="97309-137">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

> [!Note]
> <span data-ttu-id="97309-138">Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande.</span><span class="sxs-lookup"><span data-stu-id="97309-138">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="97309-139">Pour plus d’informations, [consultez cette question sur Stack Overflow.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="97309-139">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

<a name="hostsample"></a>
## <a name="deploy-your-sample-app"></a><span data-ttu-id="97309-140">Déployer votre exemple d’application</span><span class="sxs-lookup"><span data-stu-id="97309-140">Deploy your sample app</span></span>

<span data-ttu-id="97309-141">Les applications Microsoft Teams sont des applications web qui fournissent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="97309-141">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="97309-142">Pour que la Teams charge votre application, votre application doit être disponible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="97309-142">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="97309-143">Pour ce faire, vous devez héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="97309-143">To do this, you need to host your app.</span></span> <span data-ttu-id="97309-144">Vous pouvez l’héberger dans Microsoft Azure gratuitement ou créer un tunnel vers le processus local sur votre ordinateur à l’aide `ngrok` de .</span><span class="sxs-lookup"><span data-stu-id="97309-144">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="97309-145">Après avoir héberger votre application, notez son URL racine, par exemple `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="97309-145">After you host your app, make a note of its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="97309-146">Tunnel à l’aide de ngrok</span><span class="sxs-lookup"><span data-stu-id="97309-146">Tunnel using ngrok</span></span>

<span data-ttu-id="97309-147">Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur et y créer un tunnel via un point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="97309-147">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="97309-148">[`ngrok`](https://ngrok.com) est un outil gratuit avec lequel vous pouvez obtenir une adresse web, telle que `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="97309-148">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="97309-149">Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok et l’ajouter à un emplacement dans votre `PATH` .</span><span class="sxs-lookup"><span data-stu-id="97309-149">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="97309-150">Après avoir `ngrok` installé, ouvrez une nouvelle fenêtre terminal et exécutez la commande suivante pour créer un tunnel :</span><span class="sxs-lookup"><span data-stu-id="97309-150">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="97309-151">`Ngrok` répond aux demandes provenant d’Internet et les approvisionnement vers votre application en cours d’exécution sur le port 44327.</span><span class="sxs-lookup"><span data-stu-id="97309-151">`Ngrok` responds to requests from the internet and routes them to your app running on port 44327.</span></span> 

<span data-ttu-id="97309-152">**Pour vérifier la réponse**</span><span class="sxs-lookup"><span data-stu-id="97309-152">**To verify the response**</span></span>

1. <span data-ttu-id="97309-153">Ouvrez votre navigateur, puis accédez à `https://d0ac14a5.ngrok.io/hello`.</span><span class="sxs-lookup"><span data-stu-id="97309-153">Open your browser and go to `https://d0ac14a5.ngrok.io/hello`.</span></span> <span data-ttu-id="97309-154">Cela charge la page Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="97309-154">This will load your app's Hello page.</span></span>
1. <span data-ttu-id="97309-155">Au lieu de l’URL mentionnée à l’étape 1, utilisez l’adresse de forwarding affichée `ngrok` dans votre session console.</span><span class="sxs-lookup"><span data-stu-id="97309-155">Instead of the URL mentioned in Step 1, use the forwarding address displayed by `ngrok` in your console session.</span></span>
    > [!NOTE]
    > <span data-ttu-id="97309-156">Si vous avez utilisé un autre port à l’étape [de](#build-and-run-the-sample) build et d’utilisation, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.</span><span class="sxs-lookup"><span data-stu-id="97309-156">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>
    > [!TIP]
    > <span data-ttu-id="97309-157">Il est bon de l’exécuter `ngrok` dans une autre fenêtre terminal.</span><span class="sxs-lookup"><span data-stu-id="97309-157">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="97309-158">Cela permet de ne pas `ngrok` s’exécute sans interférer avec l’application.</span><span class="sxs-lookup"><span data-stu-id="97309-158">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="97309-159">Vous devez arrêter, reconstruire et réexécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="97309-159">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="97309-160">La `ngrok` session fournit des informations de débogage utiles dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="97309-160">The `ngrok` session provides useful debugging information in this window.</span></span>

    <span data-ttu-id="97309-161">L’application est disponible uniquement pendant la session en cours sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="97309-161">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="97309-162">Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="97309-162">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="97309-163">N’oubliez pas que vous partagez l’application pour le test à d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="97309-163">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="97309-164">Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="97309-164">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="97309-165">La version payante `ngrok` de n’a pas cette limitation.</span><span class="sxs-lookup"><span data-stu-id="97309-165">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="97309-166">Hôte dans Azure</span><span class="sxs-lookup"><span data-stu-id="97309-166">Host in Azure</span></span>

<span data-ttu-id="97309-167">Microsoft Azure héberge votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée.</span><span class="sxs-lookup"><span data-stu-id="97309-167">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="97309-168">Cela suffit pour exécuter `Hello World` l’exemple.</span><span class="sxs-lookup"><span data-stu-id="97309-168">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="97309-169">Pour plus d’informations, [voir la création d’un compte Azure gratuit.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="97309-169">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="97309-170">Visual Studio la prise en charge intégrée du déploiement d’applications pour différents fournisseurs, notamment Azure :</span><span class="sxs-lookup"><span data-stu-id="97309-170">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

<span data-ttu-id="97309-171">**Mettre à jour le package d’application**</span><span class="sxs-lookup"><span data-stu-id="97309-171">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="97309-172">App Studio</span><span class="sxs-lookup"><span data-stu-id="97309-172">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="97309-173">Portail du développeur</span><span class="sxs-lookup"><span data-stu-id="97309-173">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="97309-174">**Pour installer le Portail du développeur (prévisualisation) dans Teams**</span><span class="sxs-lookup"><span data-stu-id="97309-174">**To install Developer Portal (preview) in Teams**</span></span>


1. <span data-ttu-id="97309-175">Sélectionnez **l’icône** Applications en bas de la barre de gauche, puis recherchez **Portail du développeur.**</span><span class="sxs-lookup"><span data-stu-id="97309-175">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="97309-176">Sélectionnez **Portail du développeur** et **Ouvrez.**</span><span class="sxs-lookup"><span data-stu-id="97309-176">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="97309-177">Sélectionnez l’onglet Applications et **sélectionnez Importer une application existante.**</span><span class="sxs-lookup"><span data-stu-id="97309-177">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="97309-178">Sélectionnez **Hello World** et **sélectionnez Importer.**</span><span class="sxs-lookup"><span data-stu-id="97309-178">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="97309-179">**L’application Hello World** est importée dans le Portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="97309-179">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="97309-180">Vous pouvez configurer votre application à l’aide du portail Teams développeur.</span><span class="sxs-lookup"><span data-stu-id="97309-180">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="97309-181">Le manifeste se trouve sous Distribuer.</span><span class="sxs-lookup"><span data-stu-id="97309-181">The Manifest is found under Distribute.</span></span> <span data-ttu-id="97309-182">Vous pouvez utiliser le manifeste pour configurer les fonctionnalités, les ressources requises et d’autres attributs importants pour votre application.</span><span class="sxs-lookup"><span data-stu-id="97309-182">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="97309-183">Pour plus d’informations sur la configuration de votre application à l’aide du Portail du développeur, voir [Teams Portail des développeurs.](../concepts/build-and-test/teams-developer-portal.md)</span><span class="sxs-lookup"><span data-stu-id="97309-183">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="97309-184">Mettre à jour les informations d’identification de votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="97309-184">Update the credentials for your hosted app</span></span>

<span data-ttu-id="97309-185">L’exemple d’application nécessite que les variables d’environnement soient définies sur les valeurs que vous avez enregistrées dans le fichier texte.</span><span class="sxs-lookup"><span data-stu-id="97309-185">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="97309-186">**Pour mettre à jour les informations d’identification de votre application hébergée**</span><span class="sxs-lookup"><span data-stu-id="97309-186">**To update the credentials for your hosted app**</span></span>

1. <span data-ttu-id="97309-187">Ouvrez le fichier `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="97309-187">Open the `appsettings.json` file.</span></span> 
1. <span data-ttu-id="97309-188">Mettez à **jour la valeur MicrosoftAppId** avec votre ID de bot que vous avez enregistré dans le fichier texte.</span><span class="sxs-lookup"><span data-stu-id="97309-188">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> 
1. <span data-ttu-id="97309-189">Mettez à jour **MicrosoftAppPassword avec** le mot de passe du bot que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="97309-189">Update the **MicrosoftAppPassword** with the bot password that you saved.</span></span>

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    <span data-ttu-id="97309-190">Une fois ces modifications apportées, resserez l’application.</span><span class="sxs-lookup"><span data-stu-id="97309-190">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="97309-191">Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez dans Azure, redéployer l’application.</span><span class="sxs-lookup"><span data-stu-id="97309-191">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a><span data-ttu-id="97309-192">Configurer l’onglet de l’application</span><span class="sxs-lookup"><span data-stu-id="97309-192">Configure the app tab</span></span>

<span data-ttu-id="97309-193">Après avoir installé l’application dans Teams, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="97309-193">After you have installed the app into teams, you must configure it to display the content.</span></span> 

<span data-ttu-id="97309-194">**Pour configurer l’onglet de l’application**</span><span class="sxs-lookup"><span data-stu-id="97309-194">**To configure the app tab**</span></span>

1. <span data-ttu-id="97309-195">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.</span><span class="sxs-lookup"><span data-stu-id="97309-195">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.</span></span>
1. <span data-ttu-id="97309-196">Sélectionnez **Hello World** dans la **liste Ajouter un** onglet.</span><span class="sxs-lookup"><span data-stu-id="97309-196">Select **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="97309-197">Une boîte de dialogue de configuration s’affiche pour vous permettre de sélectionner l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="97309-197">A configuration dialog box is displayed that enables you to select the tab to display in this channel.</span></span> 
1. <span data-ttu-id="97309-198">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="97309-198">Select **Save**.</span></span> <span data-ttu-id="97309-199">`Hello World`L’onglet est chargé avec l’onglet.</span><span class="sxs-lookup"><span data-stu-id="97309-199">The `Hello World` tab is loaded with the tab.</span></span>

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="97309-200">Testez votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="97309-200">Test your bot in Teams</span></span>

<span data-ttu-id="97309-201">Vous pouvez maintenant tester le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="97309-201">You can now test the bot in Teams.</span></span> 

<span data-ttu-id="97309-202">**Pour tester votre bot**</span><span class="sxs-lookup"><span data-stu-id="97309-202">**To test your bot**</span></span>

* <span data-ttu-id="97309-203">Sélectionnez un canal dans l’équipe où vous avez inscrit votre application et tapez `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="97309-203">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="97309-204">C’est ce qu’on appelle **\@ une mention.**</span><span class="sxs-lookup"><span data-stu-id="97309-204">This is called an **\@mention**.</span></span> <span data-ttu-id="97309-205">Le bot répond à tout message que vous envoyez.</span><span class="sxs-lookup"><span data-stu-id="97309-205">The bot replies to any message that you send.</span></span>

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="97309-206">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="97309-206">Test your messaging extension</span></span>

<span data-ttu-id="97309-207">Pour tester votre extension de messagerie, **sélectionnez...** sous la zone d’entrée dans l’affichage conversation.</span><span class="sxs-lookup"><span data-stu-id="97309-207">To test your messaging extension, select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="97309-208">Un menu avec **l’application « Hello World** » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="97309-208">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="97309-209">Lorsque vous le sélectionnez, un ensemble de textes aléatoires s’affiche.</span><span class="sxs-lookup"><span data-stu-id="97309-209">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="97309-210">Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="97309-210">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="97309-211">Sélectionnez l’un des textes aléatoires.</span><span class="sxs-lookup"><span data-stu-id="97309-211">Select one of the random text.</span></span> <span data-ttu-id="97309-212">Une carte mise en forme et prête à envoyer votre propre message s’affiche.</span><span class="sxs-lookup"><span data-stu-id="97309-212">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a><span data-ttu-id="97309-213">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="97309-213">See also</span></span>

* [<span data-ttu-id="97309-214">Présentation des didacticiels</span><span class="sxs-lookup"><span data-stu-id="97309-214">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="97309-215">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="97309-215">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)