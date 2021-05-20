---
title: 'Tutoriel - Créez votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des Microsoft Teams applications avec C# ou .NET.
keywords: commencer .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566886"
---
# <a name="create-your-first-teams-app-using-c"></a><span data-ttu-id="684ac-104">Créez votre première application Teams en utilisant C #</span><span class="sxs-lookup"><span data-stu-id="684ac-104">Create your first Teams app using C#</span></span>

<span data-ttu-id="684ac-105">Ce tutoriel vous aide à créer une application Microsoft Teams en utilisant C#.</span><span class="sxs-lookup"><span data-stu-id="684ac-105">This tutorial helps you to create a Microsoft Teams app using C#.</span></span> <span data-ttu-id="684ac-106">Pour ce faire, vous devez :</span><span class="sxs-lookup"><span data-stu-id="684ac-106">To do this, you must:</span></span>

* <span data-ttu-id="684ac-107">Préparer votre environnement</span><span class="sxs-lookup"><span data-stu-id="684ac-107">Prepare your environment</span></span>
* <span data-ttu-id="684ac-108">Obtenez des conditions préalables</span><span class="sxs-lookup"><span data-stu-id="684ac-108">Get prerequisites</span></span>
* <span data-ttu-id="684ac-109">Télécharger l’échantillon</span><span class="sxs-lookup"><span data-stu-id="684ac-109">Download the sample</span></span>
* <span data-ttu-id="684ac-110">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="684ac-110">Build and run the sample</span></span>
* <span data-ttu-id="684ac-111">Hébergez l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="684ac-111">Host the sample app</span></span>
* <span data-ttu-id="684ac-112">Mettre à jour les informations d’identification de votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="684ac-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="684ac-113">Configurer l’onglet app</span><span class="sxs-lookup"><span data-stu-id="684ac-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="684ac-114">Obtenez des conditions préalables</span><span class="sxs-lookup"><span data-stu-id="684ac-114">Get prerequisites</span></span>

<span data-ttu-id="684ac-115">Pour compléter ce tutoriel, vous devez installer les outils suivants :</span><span class="sxs-lookup"><span data-stu-id="684ac-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="684ac-116">Installer Git</span><span class="sxs-lookup"><span data-stu-id="684ac-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="684ac-117">Installer Visual Studio</span><span class="sxs-lookup"><span data-stu-id="684ac-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="684ac-118">Vous pouvez installer l’édition communautaire gratuite de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="684ac-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="684ac-119">Lors de l’installation, s’il y a une option `git` à ajouter au chemin, sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="684ac-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="684ac-120">Dans une fenêtre terminale, exécutez la commande suivante pour vérifier votre `git` installation :</span><span class="sxs-lookup"><span data-stu-id="684ac-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="684ac-121">Utilisez une fenêtre terminale appropriée sur votre plate-forme.</span><span class="sxs-lookup"><span data-stu-id="684ac-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="684ac-122">Ces exemples utilisent Git Bash mais peuvent être exécutés sur la plupart des plates-formes.</span><span class="sxs-lookup"><span data-stu-id="684ac-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="684ac-123">Ouvrez la dernière version de Visual Studio installez toutes les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="684ac-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="684ac-124">Vous pouvez utiliser la même fenêtre terminale pour exécuter les commandes de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="684ac-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="684ac-125">Télécharger l’échantillon</span><span class="sxs-lookup"><span data-stu-id="684ac-125">Download the sample</span></span>

<span data-ttu-id="684ac-126">Vous pouvez commencer avec un simple [Bonjour, Monde!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="684ac-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="684ac-127">échantillon en C#.</span><span class="sxs-lookup"><span data-stu-id="684ac-127">sample in C#.</span></span> <span data-ttu-id="684ac-128">Dans une fenêtre terminale, exécutez la commande suivante pour cloner le référentiel d’échantillons sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="684ac-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="684ac-129">Vous pouvez [fourre-tout](https://help.github.com/articles/fork-a-repo/) [ce repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) pour modifier et enregistrer vos modifications à GitHub.</span><span class="sxs-lookup"><span data-stu-id="684ac-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="684ac-130">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="684ac-130">Build and run the sample</span></span>

<span data-ttu-id="684ac-131">Une fois le repo cloné, utilisez Visual Studio pour ouvrir le fichier de solution **Microsoft.Teams. Samples.HelloWorld.sln** de **l’annuaire Microsoft-Teams-Samples/samples/app-hello-world/csharp** de l’échantillon.</span><span class="sxs-lookup"><span data-stu-id="684ac-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="684ac-132">Sélectionnez ensuite **Build Solution** dans le menu **Build.**</span><span class="sxs-lookup"><span data-stu-id="684ac-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="684ac-133">Pour exécuter l’échantillon, **appuyez sur F5** ou **sélectionnez Démarrer le débogage** dans le menu **Debug.**</span><span class="sxs-lookup"><span data-stu-id="684ac-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="684ac-134">Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée.</span><span class="sxs-lookup"><span data-stu-id="684ac-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="684ac-135">Vous pouvez vous rendre aux URL suivantes pour vérifier que toutes les URL de l’application sont en train de charger :</span><span class="sxs-lookup"><span data-stu-id="684ac-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="684ac-136">Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le paquet avec la commande `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="684ac-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="684ac-137">Pour plus d’informations, [voir cette question sur Stack Overflow](https://stackoverflow.com/questions/32780315).</span><span class="sxs-lookup"><span data-stu-id="684ac-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="684ac-138">Hébergez l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="684ac-138">Host the sample app</span></span>

<span data-ttu-id="684ac-139">Les applications Microsoft Teams sont des applications Web qui fournissent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="684ac-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="684ac-140">Pour que Teams plate-forme pour charger votre application, votre application doit être disponible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="684ac-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="684ac-141">Pour ce faire, vous devez héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="684ac-141">To do this, you need to host your app.</span></span> <span data-ttu-id="684ac-142">Vous pouvez soit l’héberger Microsoft Azure gratuitement ou créer un tunnel vers le processus local sur votre ordinateur en utilisant `ngrok` .</span><span class="sxs-lookup"><span data-stu-id="684ac-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="684ac-143">Après avoir héberger votre application, notez son URL racine, telle `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .</span><span class="sxs-lookup"><span data-stu-id="684ac-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="684ac-144">Tunnel’utilisation de ngrok</span><span class="sxs-lookup"><span data-stu-id="684ac-144">Tunnel using ngrok</span></span>

<span data-ttu-id="684ac-145">Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur et créer un tunnel vers elle à travers un point d’évaluation web.</span><span class="sxs-lookup"><span data-stu-id="684ac-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="684ac-146">[`ngrok`](https://ngrok.com) est un outil gratuit avec lequel vous pouvez obtenir une adresse Web, comme `https://d0ac14a5.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="684ac-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="684ac-147">Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok et l’ajouter à un emplacement dans votre `PATH` .</span><span class="sxs-lookup"><span data-stu-id="684ac-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="684ac-148">Après votre `ngrok` installation, ouvrez une nouvelle fenêtre terminale et exécutez la commande suivante pour créer un tunnel :</span><span class="sxs-lookup"><span data-stu-id="684ac-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="684ac-149">`Ngrok` écoute les demandes d’Internet et les a adage vers votre application fonctionnant sur le port 44327.</span><span class="sxs-lookup"><span data-stu-id="684ac-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="684ac-150">Pour vérifier, ouvrez votre navigateur et allez `https://d0ac14a5.ngrok.io/hello` charger la page bonjour de votre application.</span><span class="sxs-lookup"><span data-stu-id="684ac-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="684ac-151">Au lieu de cette URL, utilisez l’adresse de forwarding affichée dans `ngrok` votre session console.</span><span class="sxs-lookup"><span data-stu-id="684ac-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="684ac-152">Si vous avez utilisé un port différent dans l’étape [de construction et d’exécuter,](#build-and-run-the-sample) assurez-vous d’utiliser le même numéro de port pour configurer `ngrok` le tunnel.</span><span class="sxs-lookup"><span data-stu-id="684ac-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="684ac-153">C’est une bonne idée de courir `ngrok` dans une fenêtre terminale différente.</span><span class="sxs-lookup"><span data-stu-id="684ac-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="684ac-154">Ceci est fait pour empêcher de `ngrok` courir sans interférer avec l’application.</span><span class="sxs-lookup"><span data-stu-id="684ac-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="684ac-155">Vous devez arrêter, reconstruire et réexécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="684ac-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="684ac-156">La `ngrok` session fournit des informations utiles de débogage dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="684ac-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="684ac-157">L’application n’est disponible que pendant la session en cours sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="684ac-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="684ac-158">Si la machine est arrêtée ou s’en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="684ac-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="684ac-159">Rappelez-vous cela lorsque vous partagez l’application pour les tests à d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="684ac-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="684ac-160">Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="684ac-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="684ac-161">La version payante de `ngrok` n’a pas cette limitation.</span><span class="sxs-lookup"><span data-stu-id="684ac-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="684ac-162">Hôte en Azure</span><span class="sxs-lookup"><span data-stu-id="684ac-162">Host in Azure</span></span>

<span data-ttu-id="684ac-163">Microsoft Azure votre application .NET sur un niveau gratuit en utilisant l’infrastructure partagée.</span><span class="sxs-lookup"><span data-stu-id="684ac-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="684ac-164">Cela suffit pour exécuter `Hello World` l’échantillon.</span><span class="sxs-lookup"><span data-stu-id="684ac-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="684ac-165">Pour plus d’informations, [voir création d’un nouveau compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="684ac-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="684ac-166">Visual Studio a intégré la prise en charge du déploiement d’applications à différents fournisseurs, y compris Azure :</span><span class="sxs-lookup"><span data-stu-id="684ac-166">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="684ac-167">Mettre à jour les informations d’identification de votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="684ac-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="684ac-168">L’exemple d’application nécessite que les variables de l’environnement soient définies en fonction des valeurs que vous avez enregistrées dans le fichier texte.</span><span class="sxs-lookup"><span data-stu-id="684ac-168">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="684ac-169">Ouvrez le fichier `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="684ac-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="684ac-170">Mettez à jour **la valeur MicrosoftAppId** avec votre identifiant bot que vous avez enregistré dans le fichier texte.</span><span class="sxs-lookup"><span data-stu-id="684ac-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="684ac-171">Mettez à jour **le MicrosoftAppPassword avec le** mot de passe bot que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="684ac-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="684ac-172">Une fois ces modifications apportées, reconstruisez l’application.</span><span class="sxs-lookup"><span data-stu-id="684ac-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="684ac-173">Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez azure, redéploiez l’application.</span><span class="sxs-lookup"><span data-stu-id="684ac-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="684ac-174">Configurer l’onglet app</span><span class="sxs-lookup"><span data-stu-id="684ac-174">Configure the app tab</span></span>

<span data-ttu-id="684ac-175">Une fois que vous installez l’application dans une équipe, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="684ac-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="684ac-176">Rendez-vous sur un canal de l’équipe où vous avez installé l’exemple **d’application et sélectionnez le bouton '+'** pour ajouter un nouvel onglet. Choisissez **Hello World dans** la liste Ajouter **un** onglet.</span><span class="sxs-lookup"><span data-stu-id="684ac-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="684ac-177">Une boîte de dialogue de configuration est affichée qui vous permet de choisir l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="684ac-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="684ac-178">Après avoir sélectionné l’onglet et sélectionné **Enregistrer l’onglet** `Hello World` est chargé avec l’onglet.</span><span class="sxs-lookup"><span data-stu-id="684ac-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="684ac-179">Testez votre bot en Teams</span><span class="sxs-lookup"><span data-stu-id="684ac-179">Test your bot in Teams</span></span>

<span data-ttu-id="684ac-180">Maintenant, vous pouvez tester le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="684ac-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="684ac-181">Sélectionnez un canal dans l’équipe où vous avez enregistré votre application et tapez `@your-bot-name` .</span><span class="sxs-lookup"><span data-stu-id="684ac-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="684ac-182">C’est ce qu’on **\@ appelle une mention**.</span><span class="sxs-lookup"><span data-stu-id="684ac-182">This is called an **\@mention**.</span></span> <span data-ttu-id="684ac-183">Le bot répond à tout message que vous envoyez.</span><span class="sxs-lookup"><span data-stu-id="684ac-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="684ac-184">Testez votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="684ac-184">Test your messaging extension</span></span>

<span data-ttu-id="684ac-185">Pour tester votre extension de messagerie, vous pouvez sélectionner ... en **dessous de** la boîte d’entrée dans votre vue de conversation.</span><span class="sxs-lookup"><span data-stu-id="684ac-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="684ac-186">Un menu avec **l’application 'Hello World'** est affiché.</span><span class="sxs-lookup"><span data-stu-id="684ac-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="684ac-187">Lorsque vous le sélectionnez, un ensemble de textes aléatoires s’affiche.</span><span class="sxs-lookup"><span data-stu-id="684ac-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="684ac-188">Vous pouvez sélectionner l’un des textes aléatoires et qui est inséré dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="684ac-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="684ac-189">Sélectionnez l’un des textes aléatoires.</span><span class="sxs-lookup"><span data-stu-id="684ac-189">Select one of the random text.</span></span> <span data-ttu-id="684ac-190">Une carte formatée et prête à envoyer avec votre propre message est affichée.</span><span class="sxs-lookup"><span data-stu-id="684ac-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
