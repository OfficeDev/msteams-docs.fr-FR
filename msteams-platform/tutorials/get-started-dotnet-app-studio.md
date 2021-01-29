---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C#/.NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037038"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a><span data-ttu-id="f9af7-104">Créer votre première application Microsoft Teams à l’aide de C #</span><span class="sxs-lookup"><span data-stu-id="f9af7-104">Create your first Microsoft Teams app using C#</span></span>

<span data-ttu-id="f9af7-105">Ce didacticiel vous aide à commencer à créer une application Microsoft Teams en C# sur .NET.</span><span class="sxs-lookup"><span data-stu-id="f9af7-105">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="f9af7-106">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="f9af7-106">Get prerequisites</span></span>

<span data-ttu-id="f9af7-107">Pour effectuer ce didacticiel, vous devez obtenir les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="f9af7-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="f9af7-108">Installer Git</span><span class="sxs-lookup"><span data-stu-id="f9af7-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="f9af7-109">[Installez Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f9af7-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="f9af7-110">Vous pouvez installer l’édition communautaire gratuite.</span><span class="sxs-lookup"><span data-stu-id="f9af7-110">You can install the free community edition.</span></span>

<span data-ttu-id="f9af7-111">Si vous voyez une option à ajouter au chemin d’accès lors `git` de l’installation, choisissez de le faire.</span><span class="sxs-lookup"><span data-stu-id="f9af7-111">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="f9af7-112">Ce sera pratique.</span><span class="sxs-lookup"><span data-stu-id="f9af7-112">It will be handy.</span></span>

<span data-ttu-id="f9af7-113">Vérifiez votre `git` installation en exécutant ce qui suit dans une fenêtre terminal :</span><span class="sxs-lookup"><span data-stu-id="f9af7-113">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="f9af7-114">Utilisez la fenêtre terminal la plus à l’aise sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="f9af7-114">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="f9af7-115">Ces exemples utilisent Bash, mais s’exécutent sur la plupart des plateformes.</span><span class="sxs-lookup"><span data-stu-id="f9af7-115">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="f9af7-116">Assurez-vous de lancer la dernière version de Visual Studio et d’installer les mises à jour si elles sont affichées.</span><span class="sxs-lookup"><span data-stu-id="f9af7-116">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="f9af7-117">Vous pouvez continuer à utiliser cette fenêtre terminal pour exécuter les commandes qui suivent dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f9af7-117">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="f9af7-118">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="f9af7-118">Download the sample</span></span>

<span data-ttu-id="f9af7-119">Nous avons fourni un simple [Hello World !](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="f9af7-119">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="f9af7-120">exemple en C# pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="f9af7-120">sample in C# to get you started.</span></span> <span data-ttu-id="f9af7-121">Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="f9af7-121">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="f9af7-122">Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) [ce référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) si vous souhaitez modifier et vérifier vos modifications dans GitHub pour référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f9af7-122">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="f9af7-123">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="f9af7-123">Build and run the sample</span></span>

<span data-ttu-id="f9af7-124">Une fois le dépôt cloné, utilisez Visual Studio pour ouvrir le fichier de solution à partir du répertoire racine de l’exemple, puis cliquez dans `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` le `Build` menu.</span><span class="sxs-lookup"><span data-stu-id="f9af7-124">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="f9af7-125">Vous pouvez exécuter l’exemple en appuyant `F5` ou en choisissant `Start Debugging` dans le `Debug` menu.</span><span class="sxs-lookup"><span data-stu-id="f9af7-125">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="f9af7-126">Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée.</span><span class="sxs-lookup"><span data-stu-id="f9af7-126">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="f9af7-127">Vous pouvez accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :</span><span class="sxs-lookup"><span data-stu-id="f9af7-127">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="f9af7-128">Si vous recevez une erreur telle `Could not find a part of the path … bin\roslyn\csc.exe` que , essayez de mettre à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande.</span><span class="sxs-lookup"><span data-stu-id="f9af7-128">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="f9af7-129">Consultez [cette question sur StackOverflow pour](https://stackoverflow.com/questions/32780315) plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f9af7-129">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="f9af7-130">Héberger l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="f9af7-130">Host the sample app</span></span>

<span data-ttu-id="f9af7-131">N’oubliez pas que les applications dans Microsoft Teams sont des applications web qui exposent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f9af7-131">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="f9af7-132">Pour que la plateforme Teams charge votre application, votre application doit être accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="f9af7-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="f9af7-133">Pour rendre votre application accessible à partir d’Internet, vous devez l’héberger.</span><span class="sxs-lookup"><span data-stu-id="f9af7-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="f9af7-134">Vous pouvez l’héberger gratuitement dans Microsoft Azure ou créer un tunnel vers le processus local sur votre ordinateur de développement à l’aide `ngrok` de .</span><span class="sxs-lookup"><span data-stu-id="f9af7-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="f9af7-135">Lorsque vous avez terminé l’hébergement de votre application, notez son URL racine.</span><span class="sxs-lookup"><span data-stu-id="f9af7-135">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="f9af7-136">Il ressemblera à : `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="f9af7-136">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="f9af7-137">Tunnel utilisant ngrok</span><span class="sxs-lookup"><span data-stu-id="f9af7-137">Tunnel using ngrok</span></span>

<span data-ttu-id="f9af7-138">Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel via un point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="f9af7-138">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="f9af7-139">[ngrok est](https://ngrok.com) un outil gratuit qui vous permet de le faire.</span><span class="sxs-lookup"><span data-stu-id="f9af7-139">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="f9af7-140">Avec ngrok, vous pouvez obtenir une adresse web telle que `https://d0ac14a5.ngrok.io` (cette URL n’est qu’un exemple).</span><span class="sxs-lookup"><span data-stu-id="f9af7-140">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="f9af7-141">Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f9af7-141">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="f9af7-142">Veillez à l’ajouter à un emplacement dans votre `PATH` .</span><span class="sxs-lookup"><span data-stu-id="f9af7-142">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="f9af7-143">Une fois l’installation installée, vous pouvez ouvrir une nouvelle fenêtre terminal et exécuter la commande suivante pour créer un tunnel.</span><span class="sxs-lookup"><span data-stu-id="f9af7-143">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="f9af7-144">L’exemple utilise le port 3333, donc n’oubliez pas de le spécifier ici.</span><span class="sxs-lookup"><span data-stu-id="f9af7-144">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="f9af7-145">Ngrok écoutera les demandes provenant d’Internet et les routera vers votre application en cours d’exécution sur le port 3333.</span><span class="sxs-lookup"><span data-stu-id="f9af7-145">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="f9af7-146">Vous pouvez vérifier en ouvrant votre navigateur et en allant `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="f9af7-146">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="f9af7-147">Assurez-vous d’utiliser l’adresse de forwarding affichée par ngrok dans votre session console au lieu de cette URL.</span><span class="sxs-lookup"><span data-stu-id="f9af7-147">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f9af7-148">Si vous avez utilisé un [](#build-and-run-the-sample) autre port dans la build et l’étape d’utilisation ci-dessus, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.</span><span class="sxs-lookup"><span data-stu-id="f9af7-148">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="f9af7-149">Il est bon de l’exécuter dans une autre fenêtre terminal pour la maintenir en cours d’exécution sans interférer avec l’application que vous de devez peut-être arrêter, reconstruire et `ngrok` réexécuter par la suite.</span><span class="sxs-lookup"><span data-stu-id="f9af7-149">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="f9af7-150">La `ngrok` session retourne des informations de débogage utiles dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f9af7-150">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="f9af7-151">L’application sera disponible uniquement pendant la session en cours sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="f9af7-151">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="f9af7-152">Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="f9af7-152">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="f9af7-153">N’oubliez pas cela lors du partage de l’application pour les tests effectués par d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f9af7-153">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="f9af7-154">Si vous devez redémarrer le service, il retourne une nouvelle adresse et vous devez mettre à jour chaque endroit qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="f9af7-154">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="f9af7-155">La version payante de Ngrok n’a pas cette limitation.</span><span class="sxs-lookup"><span data-stu-id="f9af7-155">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="f9af7-156">Hôte dans Azure</span><span class="sxs-lookup"><span data-stu-id="f9af7-156">Host in Azure</span></span>

<span data-ttu-id="f9af7-157">Microsoft Azure vous permet d’héberger votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée.</span><span class="sxs-lookup"><span data-stu-id="f9af7-157">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="f9af7-158">Cela sera suffisant pour exécuter cet `Hello World` exemple.</span><span class="sxs-lookup"><span data-stu-id="f9af7-158">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="f9af7-159">Pour plus [d’informations, voir](https://azure.microsoft.com/free/) la création d’un compte gratuit.</span><span class="sxs-lookup"><span data-stu-id="f9af7-159">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="f9af7-160">Visual Studio la prise en charge intégrée du déploiement d’applications pour différents fournisseurs, y compris Azure.</span><span class="sxs-lookup"><span data-stu-id="f9af7-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="f9af7-161">Mettre à jour les informations d’identification de votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="f9af7-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="f9af7-162">L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez not es précédemment.</span><span class="sxs-lookup"><span data-stu-id="f9af7-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="f9af7-163">Ouvrez le fichier appsettings.jssur.</span><span class="sxs-lookup"><span data-stu-id="f9af7-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="f9af7-164">Mettez à *jour la valeur MicrosoftAppId* avec votre ID de bot que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="f9af7-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="f9af7-165">Mettez à jour *MicrosoftAppPassword avec* le mot de passe bot que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="f9af7-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="f9af7-166">Une fois ces modifications apportées, resserez l’application.</span><span class="sxs-lookup"><span data-stu-id="f9af7-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="f9af7-167">Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez dans Azure redéployer l’application.</span><span class="sxs-lookup"><span data-stu-id="f9af7-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="f9af7-168">Configurer l’onglet de l’application</span><span class="sxs-lookup"><span data-stu-id="f9af7-168">Configure the app tab</span></span>

<span data-ttu-id="f9af7-169">Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="f9af7-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="f9af7-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. Vous pouvez ensuite choisir `Hello World` dans la liste Ajouter un **onglet.**</span><span class="sxs-lookup"><span data-stu-id="f9af7-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="f9af7-171">Une boîte de dialogue de configuration s’est ensuite présentée.</span><span class="sxs-lookup"><span data-stu-id="f9af7-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="f9af7-172">Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="f9af7-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="f9af7-173">Une fois que vous avez sélectionné l’onglet et cliqué dessus, vous pouvez voir l’onglet chargé `Save` `Hello World` avec l’onglet que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="f9af7-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="f9af7-174">Tester votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="f9af7-174">Test your bot in Teams</span></span>

<span data-ttu-id="f9af7-175">Vous pouvez désormais interagir avec le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="f9af7-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="f9af7-176">Choisissez un canal dans l’équipe où vous avez inscrit votre application, puis tapez `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="f9af7-176">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="f9af7-177">C’est ce qu’on appelle **\@ une mention.**</span><span class="sxs-lookup"><span data-stu-id="f9af7-177">This is called an **\@mention**.</span></span> <span data-ttu-id="f9af7-178">Le message que vous envoyez au bot vous sera renvoyé en tant que réponse.</span><span class="sxs-lookup"><span data-stu-id="f9af7-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="f9af7-179">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="f9af7-179">Test your messaging extension</span></span>

<span data-ttu-id="f9af7-180">Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée dans l’affichage conversation.</span><span class="sxs-lookup"><span data-stu-id="f9af7-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="f9af7-181">Un menu apparaît avec **l’application « Hello World** » dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f9af7-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="f9af7-182">Lorsque vous cliquez dessus, un grand nombre de textes aléatoires s’affichent.</span><span class="sxs-lookup"><span data-stu-id="f9af7-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="f9af7-183">Vous pouvez choisir l’un d’eux et celui-ci sera inséré dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="f9af7-183">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="f9af7-184">Choisissez l’un des textes aléatoires et vous verrez une carte mise en forme et prête à être envoyé avec votre propre message en bas.</span><span class="sxs-lookup"><span data-stu-id="f9af7-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
