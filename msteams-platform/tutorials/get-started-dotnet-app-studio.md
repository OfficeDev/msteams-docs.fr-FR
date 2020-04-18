---
title: Prise en main de C#/.NET
description: Commencer à créer des applications intéressantes dans Microsoft teams à l’aide de C#/.NET
keywords: mise en route .net c# CSharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 61237cd3178fcb41357230536827f732faf65ee4
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550958"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a><span data-ttu-id="11cea-104">Prise en main de la plateforme Microsoft teams avec C#/.NET et App Studio</span><span class="sxs-lookup"><span data-stu-id="11cea-104">Get started on the Microsoft Teams platform with C#/.NET and App Studio</span></span>

<span data-ttu-id="11cea-105">La plateforme de développement [Microsoft teams](/microsoftteams/) vous permet d’étendre facilement teams et d’intégrer vos propres applications et services de façon transparente dans l’espace de travail de teams.</span><span class="sxs-lookup"><span data-stu-id="11cea-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="11cea-106">Ces applications peuvent ensuite être distribuées à votre entreprise ou pour teams dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="11cea-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="11cea-107">Pour étendre Microsoft Teams, vous devez créer une application Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="11cea-107">To extend Microsoft Teams, you will need to create a Microsoft Teams app.</span></span> <span data-ttu-id="11cea-108">Une application Microsoft teams est une application Web que vous hébergez.</span><span class="sxs-lookup"><span data-stu-id="11cea-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="11cea-109">Cette application peut ensuite être intégrée dans l’espace de travail de l’utilisateur dans Teams.</span><span class="sxs-lookup"><span data-stu-id="11cea-109">This app can then be integrated into the user's workspace in Teams.</span></span>

<span data-ttu-id="11cea-110">Ce didacticiel vous permet de commencer à créer une application Microsoft teams à l’aide de C# sur .NET.</span><span class="sxs-lookup"><span data-stu-id="11cea-110">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span> <span data-ttu-id="11cea-111">Vous pouvez tester l’application en la chargeant dans une équipe pour laquelle vous disposez d’autorisations, ou dans un client test créé à l’aide du programme de développement Office.</span><span class="sxs-lookup"><span data-stu-id="11cea-111">You can test the app by loading it into a Team that you have permissions for, or into a test tenant created using the Office Developer Program.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="11cea-112">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="11cea-112">Get prerequisites</span></span>

<span data-ttu-id="11cea-113">Pour effectuer ce didacticiel, vous devez obtenir les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="11cea-113">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="11cea-114">Installer Git</span><span class="sxs-lookup"><span data-stu-id="11cea-114">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="11cea-115">[Installez Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="11cea-115">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="11cea-116">Vous pouvez installer la version gratuite de la communauté.</span><span class="sxs-lookup"><span data-stu-id="11cea-116">You can install the free community edition.</span></span>

<span data-ttu-id="11cea-117">Si vous voyez une option à ajouter `git` au chemin d’accès pendant l’installation, choisissez de le faire.</span><span class="sxs-lookup"><span data-stu-id="11cea-117">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="11cea-118">Il sera pratique.</span><span class="sxs-lookup"><span data-stu-id="11cea-118">It will be handy.</span></span>

<span data-ttu-id="11cea-119">Vérifiez votre `git` installation en exécutant la commande suivante dans une fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="11cea-119">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="11cea-120">Utilisez la fenêtre de terminal qui vous convient le mieux sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="11cea-120">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="11cea-121">Ces exemples utilisent bash, mais s’exécuteront sur la plupart des plateformes.</span><span class="sxs-lookup"><span data-stu-id="11cea-121">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="11cea-122">Veillez à lancer la dernière version de Visual Studio et à installer toutes les mises à jour, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="11cea-122">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="11cea-123">Vous pouvez continuer à utiliser cette fenêtre de terminal pour exécuter les commandes qui suivent dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="11cea-123">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="11cea-124">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="11cea-124">Download the sample</span></span>

<span data-ttu-id="11cea-125">Nous avons fourni un simple [Hello, World !](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="11cea-125">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="11cea-126">exemple en C# pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="11cea-126">sample in C# to get you started.</span></span> <span data-ttu-id="11cea-127">Dans une fenêtre de terminal, exécutez la commande suivante pour cloner le référentiel de l’exemple sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="11cea-127">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="11cea-128">Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) sur cette [référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) si vous voulez modifier et archiver les modifications apportées à GitHub à des fins de référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="11cea-128">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="11cea-129">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="11cea-129">Build and run the sample</span></span>

<span data-ttu-id="11cea-130">Une fois le référentiel cloné, utilisez Visual Studio pour ouvrir le fichier `Microsoft.Teams.Samples.HelloWorld.sln` de solution à partir du répertoire racine de l’exemple, `Build Solution` puis cliquez `Build` sur dans le menu.</span><span class="sxs-lookup"><span data-stu-id="11cea-130">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="11cea-131">Vous pouvez exécuter l’exemple en appuyant `F5` sur `Start Debugging` ou en `Debug` sélectionnant dans le menu.</span><span class="sxs-lookup"><span data-stu-id="11cea-131">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="11cea-132">Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée.</span><span class="sxs-lookup"><span data-stu-id="11cea-132">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="11cea-133">Vous pouvez accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :</span><span class="sxs-lookup"><span data-stu-id="11cea-133">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="11cea-134">Si vous recevez une erreur telle `Could not find a part of the path … bin\roslyn\csc.exe`que, essayez de mettre à jour le package `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`à l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="11cea-134">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="11cea-135">Pour plus d’informations, consultez [cette question sur StackOverflow](https://stackoverflow.com/questions/32780315) .</span><span class="sxs-lookup"><span data-stu-id="11cea-135">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="11cea-136">Héberger l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="11cea-136">Host the sample app</span></span>

<span data-ttu-id="11cea-137">N’oubliez pas que les applications dans Microsoft teams sont des applications Web qui exposent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="11cea-137">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="11cea-138">Pour que la plateforme teams charge votre application, votre application doit être accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="11cea-138">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="11cea-139">Pour permettre à votre application d’être accessible à partir d’Internet, vous devez héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="11cea-139">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="11cea-140">Vous pouvez l’héberger dans Microsoft Azure gratuitement ou créer un tunnel vers le processus local sur votre ordinateur de développement à `ngrok`l’aide de.</span><span class="sxs-lookup"><span data-stu-id="11cea-140">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="11cea-141">Une fois que vous avez terminé d’héberger votre application, prenez note de son URL racine.</span><span class="sxs-lookup"><span data-stu-id="11cea-141">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="11cea-142">Il ressemblera à ceci `https://yourteamsapp.ngrok.io` : `https://yourteamsapp.azurewebsites.net`ou.</span><span class="sxs-lookup"><span data-stu-id="11cea-142">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="11cea-143">Tunnel à l’aide de ngrok</span><span class="sxs-lookup"><span data-stu-id="11cea-143">Tunnel using ngrok</span></span>

<span data-ttu-id="11cea-144">Pour un test rapide, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel via un point de terminaison Web.</span><span class="sxs-lookup"><span data-stu-id="11cea-144">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="11cea-145">[ngrok](https://ngrok.com) est un outil gratuit qui vous permet d’effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="11cea-145">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="11cea-146">Avec ngrok, vous pouvez obtenir une adresse Web telle `https://d0ac14a5.ngrok.io` que (cette URL n’est qu’un exemple).</span><span class="sxs-lookup"><span data-stu-id="11cea-146">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="11cea-147">Vous pouvez [Télécharger et installer](https://ngrok.com/download) ngrok pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="11cea-147">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="11cea-148">Veillez à l’ajouter à un emplacement dans votre `PATH`.</span><span class="sxs-lookup"><span data-stu-id="11cea-148">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="11cea-149">Une fois que vous l’avez installé, vous pouvez ouvrir une nouvelle fenêtre de terminal et exécuter la commande suivante pour créer un tunnel.</span><span class="sxs-lookup"><span data-stu-id="11cea-149">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="11cea-150">L’exemple utilise le port 3333, veillez donc à le spécifier ici.</span><span class="sxs-lookup"><span data-stu-id="11cea-150">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="11cea-151">Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application en cours d’exécution sur le port 3333.</span><span class="sxs-lookup"><span data-stu-id="11cea-151">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="11cea-152">Vous pouvez vérifier en ouvrant votre navigateur et en accédant à `https://d0ac14a5.ngrok.io/hello` pour charger la page Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="11cea-152">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="11cea-153">Veillez à utiliser l’adresse de transfert affichée par ngrok dans votre session de console au lieu de cette URL.</span><span class="sxs-lookup"><span data-stu-id="11cea-153">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="11cea-154">Si vous avez utilisé un autre port dans l’étape de [création et d’exécution](#build-and-run-the-sample) ci-dessus, vérifiez que vous utilisez le même numéro `ngrok` de port pour configurer le tunnel.</span><span class="sxs-lookup"><span data-stu-id="11cea-154">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="11cea-155">Il est judicieux de s’exécuter `ngrok` dans une autre fenêtre de terminal pour qu’elle continue de s’exécuter sans interférer avec l’application que vous devrez peut-être arrêter, reconstruire et réexécuter.</span><span class="sxs-lookup"><span data-stu-id="11cea-155">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="11cea-156">La `ngrok` session renverra des informations utiles sur le débogage dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="11cea-156">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="11cea-157">L’application sera disponible uniquement pendant la session en cours sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="11cea-157">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="11cea-158">Si l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="11cea-158">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="11cea-159">Souvenez-vous de ceci lors du partage de l’application pour le test par d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="11cea-159">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="11cea-160">Si vous devez redémarrer le service, il renverra une nouvelle adresse et vous devrez mettre à jour chaque emplacement qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="11cea-160">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="11cea-161">La version payante de Ngrok n’a pas cette limitation.</span><span class="sxs-lookup"><span data-stu-id="11cea-161">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="11cea-162">Hôte dans Azure</span><span class="sxs-lookup"><span data-stu-id="11cea-162">Host in Azure</span></span>

<span data-ttu-id="11cea-163">Microsoft Azure vous permet d’héberger votre application .NET sur une couche libre à l’aide de l’infrastructure partagée.</span><span class="sxs-lookup"><span data-stu-id="11cea-163">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="11cea-164">Cela sera suffisant pour exécuter cet `Hello World` exemple.</span><span class="sxs-lookup"><span data-stu-id="11cea-164">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="11cea-165">Pour plus d’informations, consultez [la rubrique Création d’un compte gratuit](https://azure.microsoft.com/free/) .</span><span class="sxs-lookup"><span data-stu-id="11cea-165">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="11cea-166">Visual Studio prend en charge le déploiement d’applications sur différents fournisseurs, dont Azure.</span><span class="sxs-lookup"><span data-stu-id="11cea-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="11cea-168">Mettre à jour les informations d’identification pour votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="11cea-168">Update the credentials for your hosted app</span></span>

<span data-ttu-id="11cea-169">L’exemple d’application requiert que les variables d’environnement suivantes soient définies sur les valeurs que vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="11cea-169">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="11cea-170">Ouvrez le fichier Web. config et recherchez la section *appSettings* .</span><span class="sxs-lookup"><span data-stu-id="11cea-170">Open up the web.config file and find the *appSettings* section.</span></span> <span data-ttu-id="11cea-171">Mettez à jour la valeur *MicrosoftAppId* avec votre ID bot que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="11cea-171">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="11cea-172">Mettez à jour le *MicrosoftAppPassword* avec le mot de passe du bot que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="11cea-172">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="définition des clés"/>

<span data-ttu-id="11cea-174">Une fois ces modifications effectuées, régénérez l’application.</span><span class="sxs-lookup"><span data-stu-id="11cea-174">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="11cea-175">Si vous utilisez ngrok, exécutez l’application localement et, si vous hébergez dans Azure, redéployez l’application.</span><span class="sxs-lookup"><span data-stu-id="11cea-175">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="11cea-176">Configurer l’onglet application</span><span class="sxs-lookup"><span data-stu-id="11cea-176">Configure the app tab</span></span>

<span data-ttu-id="11cea-177">Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="11cea-177">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="11cea-178">Accédez à un canal de l’équipe où vous avez installé l’exemple d’application, puis cliquez sur le bouton **« + »** pour ajouter un nouvel onglet. Vous pouvez ensuite choisir `Hello World` dans la liste **Ajouter un onglet** .</span><span class="sxs-lookup"><span data-stu-id="11cea-178">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="11cea-179">Une boîte de dialogue de configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="11cea-179">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="11cea-180">Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="11cea-180">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="11cea-181">Une fois que vous avez sélectionné l’onglet `Save` , puis cliqué sur, `Hello World` vous pouvez voir l’onglet chargé avec l’onglet que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="11cea-181">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Capture d’écran de la configuration" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="11cea-183">Tester votre robot dans teams</span><span class="sxs-lookup"><span data-stu-id="11cea-183">Test your bot in Teams</span></span>

<span data-ttu-id="11cea-184">Vous pouvez désormais interagir avec le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="11cea-184">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="11cea-185">Sélectionnez un canal dans l’équipe où vous avez enregistré votre application, puis `@your-bot-name`tapez.</span><span class="sxs-lookup"><span data-stu-id="11cea-185">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="11cea-186">Il s’agit d’une \*\* \@mention\*\*.</span><span class="sxs-lookup"><span data-stu-id="11cea-186">This is called an **\@mention**.</span></span> <span data-ttu-id="11cea-187">Tout message que vous envoyez au bot vous sera renvoyé en tant que réponse.</span><span class="sxs-lookup"><span data-stu-id="11cea-187">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="Réponses de robot" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="11cea-189">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="11cea-189">Test your messaging extension</span></span>

<span data-ttu-id="11cea-190">Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée de votre affichage conversation.</span><span class="sxs-lookup"><span data-stu-id="11cea-190">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="11cea-191">Un menu s’affiche avec l’application **« Hello World »** .</span><span class="sxs-lookup"><span data-stu-id="11cea-191">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="11cea-192">Lorsque vous cliquez dessus, un ensemble de textes aléatoires s’affichent.</span><span class="sxs-lookup"><span data-stu-id="11cea-192">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="11cea-193">Vous pouvez choisir l’un d’entre eux et l’insérer dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="11cea-193">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" title="Menu extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="Résultat de l’extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="11cea-196">Choisissez l’un des textes aléatoires, et vous verrez une carte formatée et prête à envoyer avec votre propre message en bas.</span><span class="sxs-lookup"><span data-stu-id="11cea-196">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" title="Envoi d’extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
