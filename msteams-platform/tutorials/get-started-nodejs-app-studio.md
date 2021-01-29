---
title: 'Didacticiel : créer votre première application à l’aide Node.js'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec Node.js.
keywords: mise en node.js nodejs App Studio
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 03dcf79a46266321e54c7e99bf01cdd2a87075fa
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037045"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="aeb67-104">Créer votre première application Microsoft Teams à l’aide Node.js</span><span class="sxs-lookup"><span data-stu-id="aeb67-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="aeb67-105">Ce didacticiel vous aide à commencer à créer une application Microsoft Teams à l’aide Node.js.</span><span class="sxs-lookup"><span data-stu-id="aeb67-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="aeb67-106">Télécharger et héberger votre application</span><span class="sxs-lookup"><span data-stu-id="aeb67-106">Download and host your app</span></span>

<span data-ttu-id="aeb67-107">Suivez ces étapes pour télécharger et héberger une application « hello world » simple dans Teams.</span><span class="sxs-lookup"><span data-stu-id="aeb67-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="aeb67-108">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="aeb67-108">Get prerequisites</span></span>

<span data-ttu-id="aeb67-109">Pour effectuer ce didacticiel, vous avez besoin des outils suivants.</span><span class="sxs-lookup"><span data-stu-id="aeb67-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="aeb67-110">Si vous ne les avez pas encore, vous pouvez les installer à partir de ces liens.</span><span class="sxs-lookup"><span data-stu-id="aeb67-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="aeb67-111">Git</span><span class="sxs-lookup"><span data-stu-id="aeb67-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="aeb67-112">Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="aeb67-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="aeb67-113">Obtenez n’importe quel éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="aeb67-113">Get any text editor or IDE.</span></span> <span data-ttu-id="aeb67-114">Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuit.</span><span class="sxs-lookup"><span data-stu-id="aeb67-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="aeb67-115">Si des options s’offrent à vous pour ajouter , et pour path lors de `git` `node` `npm` `code` l’installation, choisissez de le faire.</span><span class="sxs-lookup"><span data-stu-id="aeb67-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="aeb67-116">Ce sera pratique.</span><span class="sxs-lookup"><span data-stu-id="aeb67-116">It will be handy.</span></span>

<span data-ttu-id="aeb67-117">Vérifiez que les outils sont disponibles en exécutant ce qui suit dans une fenêtre terminal :</span><span class="sxs-lookup"><span data-stu-id="aeb67-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="aeb67-118">Utilisez la fenêtre terminal la plus à l’aise sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="aeb67-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="aeb67-119">Ces exemples utilisent Bash (qui est inclus dans Git), mais ces scripts s’exécuteront sur la plupart des plateformes.</span><span class="sxs-lookup"><span data-stu-id="aeb67-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

<span data-ttu-id="aeb67-120">Vous pouvez avoir une version différente de ces applications.</span><span class="sxs-lookup"><span data-stu-id="aeb67-120">You may have a different version of these applications.</span></span> <span data-ttu-id="aeb67-121">Cela ne doit pas être un problème, à l’exception de Gulp.</span><span class="sxs-lookup"><span data-stu-id="aeb67-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="aeb67-122">Pour gulp, vous devez utiliser la version 4.0.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="aeb67-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="aeb67-123">Si gulp n’est pas installé (ou si la version est mal installée), exécutez-le maintenant dans la `npm install gulp` fenêtre de votre terminal.</span><span class="sxs-lookup"><span data-stu-id="aeb67-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="aeb67-124">Si vous avez installé Visual Studio Code, vous pouvez vérifier l’installation en exécutant :</span><span class="sxs-lookup"><span data-stu-id="aeb67-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="aeb67-125">Vous pouvez continuer à utiliser cette fenêtre terminal pour exécuter les commandes qui suivent dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="aeb67-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="aeb67-126">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="aeb67-126">Download the sample</span></span>

<span data-ttu-id="aeb67-127">Nous avons fourni un simple [Hello World !](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="aeb67-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="aeb67-128">pour commencer.</span><span class="sxs-lookup"><span data-stu-id="aeb67-128">sample to get you started.</span></span> <span data-ttu-id="aeb67-129">Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="aeb67-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="aeb67-130">Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) [ce référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) si vous souhaitez modifier et vérifier vos modifications apportées à votre référentiel GitHub pour référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="aeb67-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="aeb67-131">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="aeb67-131">Build and run the sample</span></span>

<span data-ttu-id="aeb67-132">Une fois le repo cloné, modifiez le répertoire qui contient l’exemple :</span><span class="sxs-lookup"><span data-stu-id="aeb67-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="aeb67-133">Pour créer l’exemple, vous devez installer toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="aeb67-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="aeb67-134">Pour ce faire, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aeb67-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="aeb67-135">Vous devriez voir un grand nombre de dépendances installées.</span><span class="sxs-lookup"><span data-stu-id="aeb67-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="aeb67-136">Une fois qu’elles sont terminées, vous pouvez exécuter l’application :</span><span class="sxs-lookup"><span data-stu-id="aeb67-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="aeb67-137">Lorsque l’application Hello World démarre, elle s’affiche `App started listening on port 3333` dans la fenêtre du terminal.</span><span class="sxs-lookup"><span data-stu-id="aeb67-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="aeb67-138">Si vous voyez un autre numéro de port affiché dans le message ci-dessus, c’est parce que vous avez un ensemble de variables d’environnement PORT.</span><span class="sxs-lookup"><span data-stu-id="aeb67-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="aeb67-139">Vous pouvez continuer à utiliser ce port ou modifier votre variable d’environnement en 3333.</span><span class="sxs-lookup"><span data-stu-id="aeb67-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="aeb67-140">À ce stade, vous pouvez ouvrir une fenêtre de navigateur et accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :</span><span class="sxs-lookup"><span data-stu-id="aeb67-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="aeb67-141">Héberger l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="aeb67-141">Host the sample app</span></span>

<span data-ttu-id="aeb67-142">N’oubliez pas que les applications dans Microsoft Teams sont des applications web qui exposent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="aeb67-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="aeb67-143">Pour que la plateforme Teams charge votre application, votre application doit être accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="aeb67-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="aeb67-144">Pour rendre votre application accessible à partir d’Internet, vous devez *l’héberger.*</span><span class="sxs-lookup"><span data-stu-id="aeb67-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="aeb67-145">Pour les tests locaux, vous pouvez exécuter l’application sur votre ordinateur local et créer un tunnel vers celui-ci avec un point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="aeb67-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="aeb67-146">[ngrok est](https://ngrok.com) un outil gratuit qui vous permet de le faire.</span><span class="sxs-lookup"><span data-stu-id="aeb67-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="aeb67-147">Avec *ngrok,* vous pouvez obtenir une adresse web telle que `https://d0ac14a5.ngrok.io` (cette URL n’est qu’un exemple).</span><span class="sxs-lookup"><span data-stu-id="aeb67-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="aeb67-148">Vous pouvez [télécharger et installer](https://ngrok.com/download) *ngrok* pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="aeb67-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="aeb67-149">Veillez à l’ajouter à un emplacement dans votre `PATH` .</span><span class="sxs-lookup"><span data-stu-id="aeb67-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="aeb67-150">Une fois l’installation installée, vous pouvez ouvrir une nouvelle fenêtre terminal et exécuter la commande suivante pour créer un tunnel.</span><span class="sxs-lookup"><span data-stu-id="aeb67-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="aeb67-151">L’exemple utilise le port 3333, donc n’oubliez pas de le spécifier ici.</span><span class="sxs-lookup"><span data-stu-id="aeb67-151">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="aeb67-152">*Ngrok écoutera* les demandes provenant d’Internet et les routera vers votre application en cours d’exécution sur le port 3333.</span><span class="sxs-lookup"><span data-stu-id="aeb67-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="aeb67-153">Vous pouvez vérifier en ouvrant votre navigateur et en allant `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="aeb67-154">Assurez-vous d’utiliser l’adresse de forwarding affichée par *ngrok dans* votre session console au lieu de cette URL.</span><span class="sxs-lookup"><span data-stu-id="aeb67-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="aeb67-155">Si vous avez utilisé un [](#build-and-run-the-sample) autre port dans la build et l’étape d’utilisation ci-dessus, veillez à utiliser le même numéro de port pour configurer le tunnel *ngrok.*</span><span class="sxs-lookup"><span data-stu-id="aeb67-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="aeb67-156">Il est bon d’exécuter *ngrok* dans une autre fenêtre terminal pour la maintenir en cours d’exécution sans interférer avec l’application de nœud que vous de devez peut-être arrêter, reconstruire et réexécuter par la suite.</span><span class="sxs-lookup"><span data-stu-id="aeb67-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="aeb67-157">La session *ngrok* retourne des informations de débogage utiles dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="aeb67-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="aeb67-158">Il existe une version payante de *ngrok* qui autorise les noms persistants.</span><span class="sxs-lookup"><span data-stu-id="aeb67-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="aeb67-159">Si vous utilisez la version gratuite, votre application sera disponible uniquement pendant la session en cours sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="aeb67-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="aeb67-160">Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="aeb67-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="aeb67-161">N’oubliez pas cela lors du partage de l’application pour les tests effectués par d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="aeb67-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="aeb67-162">Si vous devez redémarrer le service, il retourne une nouvelle adresse et vous devez mettre à jour chaque endroit qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="aeb67-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="aeb67-163">N’oubliez pas de noter l’URL de votre application, car vous en aurez besoin ultérieurement lorsque vous enregistrerez l’application auprès de Teams à l’aide d’App studio.</span><span class="sxs-lookup"><span data-stu-id="aeb67-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="aeb67-164">Le Bloc-notes fonctionne parfaitement à cet effet.</span><span class="sxs-lookup"><span data-stu-id="aeb67-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="aeb67-165">Déployer votre application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="aeb67-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="aeb67-166">À ce stade, vous avez une application hébergée sur Internet, mais vous n’avez aucun moyen de dire à Teams où la rechercher, ni même ce que votre application appelle.</span><span class="sxs-lookup"><span data-stu-id="aeb67-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="aeb67-167">Pour ce faire, vous devez maintenant créer un package d’application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="aeb67-168">Il s’agit d’un peu plus qu’un fichier texte qui contient le manifeste de l’application et certaines icônes que le client Teams utilisera pour afficher et marque correctement votre application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="aeb67-169">Vous pouvez créer manuellement ce package d’application ou utiliser App Studio, un outil qui s’exécute dans Teams pour simplifier le processus d’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="aeb67-170">App Studio est la façon recommandée de créer et de mettre à jour le package d’application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="aeb67-171">Pour l’une ou l’autre des méthodes, vous aurez besoin des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="aeb67-171">For either method you will need the following:</span></span>

- <span data-ttu-id="aeb67-172">URL dans laquelle votre application est disponible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="aeb67-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="aeb67-173">Icônes que Teams utilisera pour brander votre application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="aeb67-174">L’exemple est livré avec des icônes d’espace réservé situées dans « src\static\images ».</span><span class="sxs-lookup"><span data-stu-id="aeb67-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="aeb67-175">App Studio fournit également des icônes par défaut si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="aeb67-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="aeb67-176">Mettre à jour votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="aeb67-176">Update your hosted app</span></span>

<span data-ttu-id="aeb67-177">L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez not es précédemment.</span><span class="sxs-lookup"><span data-stu-id="aeb67-177">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="aeb67-178">La façon dont vous faites cela diffère en fonction de la façon dont vous avez hébergé votre application.</span><span class="sxs-lookup"><span data-stu-id="aeb67-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="aeb67-179">L’élément important de l’utilisation des variables d’environnement est que ces valeurs font partie de votre environnement : elles sont accessibles par le code de votre application, mais elles ne sont pas exposées à des tiers qui peuvent examiner les fichiers qui constitueront votre site.</span><span class="sxs-lookup"><span data-stu-id="aeb67-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="aeb67-180">Si vous exécutez l’application à l’aide de ngrok, vous devez configurer certaines variables d’environnement local.</span><span class="sxs-lookup"><span data-stu-id="aeb67-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="aeb67-181">Il existe plusieurs façons de le faire, mais le plus simple, si vous utilisez Visual Studio Code, consiste à ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span><span class="sxs-lookup"><span data-stu-id="aeb67-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

<span data-ttu-id="aeb67-182">Où :</span><span class="sxs-lookup"><span data-stu-id="aeb67-182">Where:</span></span>

<span data-ttu-id="aeb67-183">MICROSOFT_APP_ID et MICROSOFT_APP_PASSWORD est l’ID et le mot de passe, respectivement, pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="aeb67-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="aeb67-184">NODE_DEBUG vous montre ce qui se passe dans votre bot dans la console de débogage Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="aeb67-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="aeb67-185">NODE_CONFIG_DIR pointe vers le répertoire à la racine du référentiel (par défaut, lorsque l’application est exécuté localement, elle le recherche dans le dossier src).</span><span class="sxs-lookup"><span data-stu-id="aeb67-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="aeb67-186">Si vous n’avez pas arrêté npm plus tôt dans le didacticiel, vous devrez l’exécuter pour que Visual Studio Code collecte correctement vos variables de `npm stop` configuration de lancement.</span><span class="sxs-lookup"><span data-stu-id="aeb67-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="aeb67-187">Configurer l’onglet de l’application</span><span class="sxs-lookup"><span data-stu-id="aeb67-187">Configure the app tab</span></span>

<span data-ttu-id="aeb67-188">Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="aeb67-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="aeb67-189">Go to a channel in the team and click on the **'+'** button to add a new tab. Vous pouvez ensuite choisir `Hello World` dans la liste Ajouter un **onglet.**</span><span class="sxs-lookup"><span data-stu-id="aeb67-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="aeb67-190">Une boîte de dialogue de configuration s’est ensuite présentée.</span><span class="sxs-lookup"><span data-stu-id="aeb67-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="aeb67-191">Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="aeb67-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="aeb67-192">Une fois que vous avez sélectionné l’onglet et cliqué dessus, vous pouvez voir `Save` l’onglet chargé `Hello World` avec l’onglet que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="aeb67-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="aeb67-193">Tester votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="aeb67-193">Test your bot in Teams</span></span>

<span data-ttu-id="aeb67-194">Vous pouvez désormais interagir avec le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="aeb67-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="aeb67-195">Choisissez un canal dans l’équipe où vous avez inscrit votre application, puis tapez `@your-bot-name` , suivi de votre message.</span><span class="sxs-lookup"><span data-stu-id="aeb67-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="aeb67-196">C’est ce qu’on appelle **\@ une mention.**</span><span class="sxs-lookup"><span data-stu-id="aeb67-196">This is called an **\@mention**.</span></span> <span data-ttu-id="aeb67-197">Le message que vous envoyez au bot vous sera renvoyé en tant que réponse.</span><span class="sxs-lookup"><span data-stu-id="aeb67-197">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="aeb67-198">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="aeb67-198">Test your messaging extension</span></span>

<span data-ttu-id="aeb67-199">Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée dans l’affichage conversation.</span><span class="sxs-lookup"><span data-stu-id="aeb67-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="aeb67-200">Un menu apparaît avec **l’application « Hello World** » dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="aeb67-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="aeb67-201">Lorsque vous cliquez dessus, vous voyez un certain nombre de textes aléatoires.</span><span class="sxs-lookup"><span data-stu-id="aeb67-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="aeb67-202">Vous pouvez choisir l’un d’eux et celui-ci sera inséré dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="aeb67-202">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="aeb67-203">Choisissez l’un des textes aléatoires et vous verrez une carte mise en forme et prête à être envoyé avec votre propre message en bas.</span><span class="sxs-lookup"><span data-stu-id="aeb67-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
