---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C# ou .NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231522"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="ba8bc-104">Créer votre première application Teams en C# ou .NET</span><span class="sxs-lookup"><span data-stu-id="ba8bc-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="ba8bc-105">Ce didacticiel vous aide à créer une application Microsoft Teams en C# ou .NET.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="ba8bc-106">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ba8bc-106">Get prerequisites</span></span>

<span data-ttu-id="ba8bc-107">Pour effectuer ce didacticiel, vous devez obtenir les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="ba8bc-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="ba8bc-108">Installer Git</span><span class="sxs-lookup"><span data-stu-id="ba8bc-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="ba8bc-109">[Installez Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ba8bc-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="ba8bc-110">Vous pouvez installer l’édition communautaire gratuite.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-110">You can install the free community edition.</span></span>

<span data-ttu-id="ba8bc-111">Lors de l’installation, s’il existe une option d’ajout au chemin d’accès, `git` sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-111">During installation, if there is an option to add `git` to the PATH, choose it.</span></span>

<span data-ttu-id="ba8bc-112">Dans une fenêtre terminal, exécutez la commande suivante pour vérifier votre `git` installation :</span><span class="sxs-lookup"><span data-stu-id="ba8bc-112">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="ba8bc-113">Utilisez une fenêtre terminal appropriée sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-113">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="ba8bc-114">Ces exemples utilisent Bash, mais s’exécutent sur la plupart des plateformes.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-114">These examples use Bash but run on most platforms.</span></span>

<span data-ttu-id="ba8bc-115">Veillez à lancer la dernière version de Visual Studio et à installer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-115">Make sure to launch the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="ba8bc-116">Vous pouvez utiliser la même fenêtre terminal pour exécuter les commandes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-116">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="ba8bc-117">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="ba8bc-117">Download the sample</span></span>

<span data-ttu-id="ba8bc-118">Vous pouvez commencer avec un simple [Hello World !](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="ba8bc-118">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="ba8bc-119">exemple en C#.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-119">sample in C#.</span></span> <span data-ttu-id="ba8bc-120">Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="ba8bc-120">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="ba8bc-121">Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) [ce référentiel pour](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) modifier et enregistrer vos modifications dans GitHub pour référence.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-121">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) to modify and save your changes to GitHub for reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="ba8bc-122">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="ba8bc-122">Build and run the sample</span></span>

<span data-ttu-id="ba8bc-123">Une fois le dépôt cloné, utilisez Visual Studio pour ouvrir le fichier de solution à partir du répertoire racine de l’exemple et sélectionnez-le `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` dans le `Build` menu.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-123">After the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and select `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="ba8bc-124">Pour exécuter l’exemple, `F5` appuyez ou choisissez `Start Debugging` dans le `Debug` menu.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-124">To run the sample press `F5` or choose `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="ba8bc-125">Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-125">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="ba8bc-126">Vous pouvez accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :</span><span class="sxs-lookup"><span data-stu-id="ba8bc-126">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="ba8bc-127">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="ba8bc-127">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="ba8bc-128">Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="ba8bc-129">Pour plus d’informations, [consultez cette question sur StackOverflow.](https://stackoverflow.com/questions/32780315)</span><span class="sxs-lookup"><span data-stu-id="ba8bc-129">For more information, see [this question on StackOverflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="ba8bc-130">Héberger l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="ba8bc-130">Host the sample app</span></span>

<span data-ttu-id="ba8bc-131">Les applications dans Microsoft Teams sont des applications web qui fournissent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-131">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="ba8bc-132">Pour que la plateforme Teams charge votre application, votre application doit être accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="ba8bc-133">Pour rendre votre application accessible à partir d’Internet, vous devez l’héberger.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="ba8bc-134">Vous pouvez l’héberger gratuitement dans Microsoft Azure ou créer un tunnel vers le processus local sur votre ordinateur de développement à l’aide `ngrok` de .</span><span class="sxs-lookup"><span data-stu-id="ba8bc-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="ba8bc-135">Lorsque vous avez terminé l’hébergement de votre application, notez son URL racine.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-135">When you finish hosting your app, note its root URL.</span></span> <span data-ttu-id="ba8bc-136">Par exemple, `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="ba8bc-136">For example, `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="ba8bc-137">Tunnel utilisant ngrok</span><span class="sxs-lookup"><span data-stu-id="ba8bc-137">Tunnel using ngrok</span></span>

<span data-ttu-id="ba8bc-138">Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel via un point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-138">For quick testing, you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="ba8bc-139">[ngrok est](https://ngrok.com) un outil gratuit avec lequel vous pouvez obtenir une adresse web telle que `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="ba8bc-139">[ngrok](https://ngrok.com) is a free tool with which you can get a web address such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="ba8bc-140">Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-140">You can [download and install](https://ngrok.com/download) ngrok.</span></span> <span data-ttu-id="ba8bc-141">Veillez à l’ajouter à un emplacement dans votre `PATH` .</span><span class="sxs-lookup"><span data-stu-id="ba8bc-141">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="ba8bc-142">Après avoir installé ngrok, ouvrez une nouvelle fenêtre terminal et exécutez la commande suivante pour créer un tunnel :</span><span class="sxs-lookup"><span data-stu-id="ba8bc-142">After you install ngrok, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="ba8bc-143">L’exemple utilise le port 44327 et assurez-vous de le spécifier.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-143">The sample uses port 44327 be sure to specify it.</span></span>

<span data-ttu-id="ba8bc-144">Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application en cours d’exécution sur le port 44327.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-144">Ngrok listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="ba8bc-145">Pour vérifier, ouvrez votre navigateur et allez `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-145">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="ba8bc-146">Au lieu de cette URL, utilisez l’adresse de forwarding affichée par ngrok dans votre session console.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-146">Instead of this URL, use the forwarding address displayed by ngrok in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8bc-147">Si vous avez utilisé un [](#build-and-run-the-sample) autre port lors de l’étape de build et d’utilisation, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-147">If you have used a different port in the [build and run](#build-and-run-the-sample) step, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="ba8bc-148">Il est bon de l’exécuter `ngrok` dans une autre fenêtre terminal.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-148">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="ba8bc-149">Cette étape est effectuée pour empêcher ngrok de s’exécute sans interférer avec l’application, que vous devez arrêter, reconstruire et réexécuter.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-149">This is done to keep ngrok from running without interfering with the app, which you have to stop, rebuild, and rerun.</span></span> <span data-ttu-id="ba8bc-150">La `ngrok` session fournit des informations de débogage utiles dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-150">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="ba8bc-151">L’application est disponible uniquement pendant la session en cours sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-151">The app is only available during the current session on your development machine.</span></span> <span data-ttu-id="ba8bc-152">Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-152">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="ba8bc-153">N’oubliez pas que vous partagez l’application pour le test à d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-153">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="ba8bc-154">Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-154">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="ba8bc-155">La version payante de ngrok n’a pas cette limitation.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-155">The paid version of ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="ba8bc-156">Hôte dans Azure</span><span class="sxs-lookup"><span data-stu-id="ba8bc-156">Host in Azure</span></span>

<span data-ttu-id="ba8bc-157">Microsoft Azure héberge votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-157">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="ba8bc-158">Cela suffit pour exécuter `Hello World` l’exemple.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-158">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="ba8bc-159">Pour plus d’informations, [voir la création d’un compte gratuit.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="ba8bc-159">For more information, see [creating a new free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="ba8bc-160">Visual Studio la prise en charge intégrée du déploiement d’applications pour différents fournisseurs, y compris Azure.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="ba8bc-161">Mettre à jour les informations d’identification de votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="ba8bc-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="ba8bc-162">L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez not es précédemment.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="ba8bc-163">Ouvrez le fichier appsettings.jssur.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="ba8bc-164">Mettez à *jour la valeur MicrosoftAppId* avec votre ID de bot que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="ba8bc-165">Mettez à jour *MicrosoftAppPassword avec* le mot de passe bot que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="ba8bc-166">Une fois ces modifications apportées, resserez l’application.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="ba8bc-167">Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez dans Azure redéployer l’application.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="ba8bc-168">Configurer l’onglet de l’application</span><span class="sxs-lookup"><span data-stu-id="ba8bc-168">Configure the app tab</span></span>

<span data-ttu-id="ba8bc-169">Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="ba8bc-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. Vous pouvez ensuite choisir `Hello World` dans la liste Ajouter un **onglet.**</span><span class="sxs-lookup"><span data-stu-id="ba8bc-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="ba8bc-171">Une boîte de dialogue de configuration s’est ensuite présentée.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="ba8bc-172">Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="ba8bc-173">Une fois que vous avez sélectionné l’onglet et cliqué dessus, vous pouvez voir l’onglet chargé `Save` `Hello World` avec l’onglet que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="ba8bc-174">Tester votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="ba8bc-174">Test your bot in Teams</span></span>

<span data-ttu-id="ba8bc-175">Vous pouvez désormais interagir avec le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="ba8bc-176">Choisissez un canal dans l’équipe où vous avez inscrit votre application et tapez `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="ba8bc-176">Choose a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="ba8bc-177">C’est ce qu’on appelle **\@ une mention.**</span><span class="sxs-lookup"><span data-stu-id="ba8bc-177">This is called an **\@mention**.</span></span> <span data-ttu-id="ba8bc-178">Le message que vous envoyez au bot vous sera renvoyé en tant que réponse.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="ba8bc-179">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ba8bc-179">Test your messaging extension</span></span>

<span data-ttu-id="ba8bc-180">Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée dans l’affichage conversation.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="ba8bc-181">Un menu apparaît avec **l’application « Hello World** » dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="ba8bc-182">Lorsque vous cliquez dessus, un grand nombre de textes aléatoires s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="ba8bc-183">Vous pouvez choisir l’un d’eux et celui-ci est inséré dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-183">You can choose any one of them and it is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="ba8bc-184">Choisissez l’un des textes aléatoires et vous verrez une carte mise en forme et prête à être envoyé avec votre propre message en bas.</span><span class="sxs-lookup"><span data-stu-id="ba8bc-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
