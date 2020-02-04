---
title: Prise en main d’App Studio et node. js
description: Commencer à créer des applications intéressantes dans Microsoft teams à l’aide de node. js et d’App Studio
keywords: nœud de mise en route. js NodeJS App Studio
ms.date: 11/09/2018
ms.openlocfilehash: 36da6d7445ad7780f6bbbf52ccce3e558c76be72
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673970"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a><span data-ttu-id="9f99a-104">Prise en main de la plateforme Microsoft teams avec node. js et App Studio</span><span class="sxs-lookup"><span data-stu-id="9f99a-104">Get started on the Microsoft Teams platform with Node.js and App Studio</span></span>

<span data-ttu-id="9f99a-105">La plateforme de développement [Microsoft teams](/microsoftteams/) vous permet d’étendre facilement teams et d’intégrer vos propres applications et services de façon transparente dans l’espace de travail de teams.</span><span class="sxs-lookup"><span data-stu-id="9f99a-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="9f99a-106">Ces applications peuvent ensuite être distribuées à votre entreprise ou pour teams dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="9f99a-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="9f99a-107">Pour étendre Microsoft Teams, vous devez créer une application Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9f99a-107">To extend Microsoft Teams, you need to create a Microsoft Teams app.</span></span> <span data-ttu-id="9f99a-108">Une application Microsoft teams est une application Web que vous hébergez.</span><span class="sxs-lookup"><span data-stu-id="9f99a-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="9f99a-109">Cette application peut ensuite être intégrée dans l’espace de travail de l’utilisateur dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9f99a-109">This app can then be integrated into the user's workspace in Teams.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="9f99a-110">Télécharger et héberger votre application</span><span class="sxs-lookup"><span data-stu-id="9f99a-110">Download and host your app</span></span>

<span data-ttu-id="9f99a-111">Procédez comme suit pour télécharger et héberger une application « Hello World » simple dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9f99a-111">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="9f99a-112">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="9f99a-112">Get prerequisites</span></span>

<span data-ttu-id="9f99a-113">Pour effectuer ce didacticiel, vous avez besoin des outils suivants.</span><span class="sxs-lookup"><span data-stu-id="9f99a-113">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="9f99a-114">Si vous ne les avez pas encore installés, vous pouvez les installer à partir de ces liens.</span><span class="sxs-lookup"><span data-stu-id="9f99a-114">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="9f99a-115">Git</span><span class="sxs-lookup"><span data-stu-id="9f99a-115">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="9f99a-116">Node. js et NPM</span><span class="sxs-lookup"><span data-stu-id="9f99a-116">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="9f99a-117">Obtenir un éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="9f99a-117">Get any text editor or IDE.</span></span> <span data-ttu-id="9f99a-118">Vous pouvez installer et utiliser [Visual Studio code](https://code.visualstudio.com/download) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="9f99a-118">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="9f99a-119">Si vous voyez des options permettant `git`d' `node`ajouter `npm`,, `code` , et le chemin d’accès pendant l’installation, choisissez de le faire.</span><span class="sxs-lookup"><span data-stu-id="9f99a-119">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="9f99a-120">Il sera pratique.</span><span class="sxs-lookup"><span data-stu-id="9f99a-120">It will be handy.</span></span>

<span data-ttu-id="9f99a-121">Vérifiez que les outils sont disponibles en exécutant ce qui suit dans une fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="9f99a-121">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="9f99a-122">Utilisez la fenêtre de terminal qui vous convient le mieux sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="9f99a-122">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="9f99a-123">Ces exemples utilisent bash (inclus dans Git), mais ces scripts s’exécuteront sur la plupart des plateformes.</span><span class="sxs-lookup"><span data-stu-id="9f99a-123">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 4.0.2
```

<span data-ttu-id="9f99a-124">Vous disposez peut-être d’une autre version de ces applications.</span><span class="sxs-lookup"><span data-stu-id="9f99a-124">You may have a different version of these applications.</span></span> <span data-ttu-id="9f99a-125">Cela ne doit pas être un problème, à l’exception de Gulp.</span><span class="sxs-lookup"><span data-stu-id="9f99a-125">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="9f99a-126">Pour Gulp, vous devez utiliser la version 4.0.0 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9f99a-126">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="9f99a-127">Si Gulp n’est pas installé (ou si vous n’avez pas installé la version incorrecte) `npm install gulp` , faites-le maintenant en exécutant la fenêtre de votre terminal.</span><span class="sxs-lookup"><span data-stu-id="9f99a-127">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="9f99a-128">Si vous avez installé Visual Studio code, vous pouvez vérifier l’installation en exécutant :</span><span class="sxs-lookup"><span data-stu-id="9f99a-128">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="9f99a-129">Vous pouvez continuer à utiliser cette fenêtre de terminal pour exécuter les commandes qui suivent dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9f99a-129">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="9f99a-130">Télécharger l’exemple</span><span class="sxs-lookup"><span data-stu-id="9f99a-130">Download the sample</span></span>

<span data-ttu-id="9f99a-131">Nous avons fourni un simple [Hello, World !](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="9f99a-131">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="9f99a-132">exemple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="9f99a-132">sample to get you started.</span></span> <span data-ttu-id="9f99a-133">Dans une fenêtre de terminal, exécutez la commande suivante pour cloner le référentiel de l’exemple sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="9f99a-133">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="9f99a-134">Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) sur cette [référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) si vous voulez modifier et archiver les modifications apportées à votre référentiel GitHub à des fins de référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9f99a-134">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="9f99a-135">Création et exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="9f99a-135">Build and run the sample</span></span>

<span data-ttu-id="9f99a-136">Une fois le référentiel cloné, accédez au répertoire qui contient l’exemple :</span><span class="sxs-lookup"><span data-stu-id="9f99a-136">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="9f99a-137">Pour générer l’exemple, vous devez installer toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="9f99a-137">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="9f99a-138">Pour ce faire, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9f99a-138">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="9f99a-139">Vous devriez voir une série de dépendances installées.</span><span class="sxs-lookup"><span data-stu-id="9f99a-139">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="9f99a-140">Une fois ces opérations terminées, vous pouvez exécuter l’application :</span><span class="sxs-lookup"><span data-stu-id="9f99a-140">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="9f99a-141">Lors du démarrage de l’application Hello-World, `App started listening on port 3333` celle-ci s’affiche dans la fenêtre du terminal.</span><span class="sxs-lookup"><span data-stu-id="9f99a-141">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="9f99a-142">Si vous voyez un numéro de port différent affiché dans le message ci-dessus, c’est qu’une variable d’environnement de PORT est définie.</span><span class="sxs-lookup"><span data-stu-id="9f99a-142">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="9f99a-143">Vous pouvez continuer à utiliser ce port ou modifier votre variable d’environnement sur 3333.</span><span class="sxs-lookup"><span data-stu-id="9f99a-143">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="9f99a-144">À ce stade, vous pouvez ouvrir une fenêtre de navigateur et accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :</span><span class="sxs-lookup"><span data-stu-id="9f99a-144">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="9f99a-145">Héberger l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="9f99a-145">Host the sample app</span></span>

<span data-ttu-id="9f99a-146">N’oubliez pas que les applications dans Microsoft teams sont des applications Web qui exposent une ou plusieurs fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9f99a-146">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="9f99a-147">Pour que la plateforme teams charge votre application, votre application doit être accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="9f99a-147">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="9f99a-148">Pour permettre à votre application d’être accessible à partir d’Internet, vous devez *héberger* votre application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-148">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="9f99a-149">Pour les tests locaux, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel à l’aide d’un point de terminaison Web.</span><span class="sxs-lookup"><span data-stu-id="9f99a-149">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="9f99a-150">[ngrok](https://ngrok.com) est un outil gratuit qui vous permet d’effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="9f99a-150">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="9f99a-151">Avec *ngrok* , vous pouvez obtenir une adresse Web telle `https://d0ac14a5.ngrok.io` que (cette URL n’est qu’un exemple).</span><span class="sxs-lookup"><span data-stu-id="9f99a-151">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="9f99a-152">Vous pouvez [Télécharger et installer](https://ngrok.com/download) *ngrok* pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="9f99a-152">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="9f99a-153">Veillez à l’ajouter à un emplacement dans votre `PATH`.</span><span class="sxs-lookup"><span data-stu-id="9f99a-153">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="9f99a-154">Une fois que vous l’avez installé, vous pouvez ouvrir une nouvelle fenêtre de terminal et exécuter la commande suivante pour créer un tunnel.</span><span class="sxs-lookup"><span data-stu-id="9f99a-154">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="9f99a-155">L’exemple utilise le port 3333, veillez donc à le spécifier ici.</span><span class="sxs-lookup"><span data-stu-id="9f99a-155">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="9f99a-156">*Ngrok* écoutera les demandes en provenance d’Internet et les acheminera vers votre application en cours d’exécution sur le port 3333.</span><span class="sxs-lookup"><span data-stu-id="9f99a-156">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="9f99a-157">Vous pouvez vérifier en ouvrant votre navigateur et en accédant à `https://d0ac14a5.ngrok.io/hello` pour charger la page Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-157">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="9f99a-158">Veillez à utiliser l’adresse de transfert affichée par *ngrok* dans votre session de console au lieu de cette URL.</span><span class="sxs-lookup"><span data-stu-id="9f99a-158">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="9f99a-159">Si vous avez utilisé un port différent dans l’étape de [création et d’exécution](#build-and-run-the-sample) ci-dessus, assurez-vous d’utiliser le même numéro de port pour configurer le tunnel *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="9f99a-159">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="9f99a-160">Il est judicieux d’exécuter *ngrok* dans une autre fenêtre de terminal pour continuer à fonctionner sans interférer avec l’application de nœud que vous devrez peut-être arrêter, reconstruire et réexécuter.</span><span class="sxs-lookup"><span data-stu-id="9f99a-160">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="9f99a-161">La session *ngrok* renverra des informations utiles sur le débogage dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9f99a-161">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="9f99a-162">Il existe une version payante d' *ngrok* qui autorise les noms persistants.</span><span class="sxs-lookup"><span data-stu-id="9f99a-162">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="9f99a-163">Si vous utilisez la version gratuite, votre application ne sera disponible que pendant la session en cours sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="9f99a-163">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="9f99a-164">Si l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="9f99a-164">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="9f99a-165">Souvenez-vous de ceci lors du partage de l’application pour le test par d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9f99a-165">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="9f99a-166">Si vous devez redémarrer le service, il renverra une nouvelle adresse et vous devrez mettre à jour chaque emplacement qui utilise cette adresse.</span><span class="sxs-lookup"><span data-stu-id="9f99a-166">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="9f99a-167">N’oubliez pas d’indiquer l’URL de votre application, car vous en aurez besoin plus tard lors de l’inscription de l’application auprès de teams à l’aide d’App Studio.</span><span class="sxs-lookup"><span data-stu-id="9f99a-167">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="9f99a-168">Le bloc-notes fonctionne à cet effet.</span><span class="sxs-lookup"><span data-stu-id="9f99a-168">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="9f99a-169">Déployer votre application dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="9f99a-169">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="9f99a-170">À ce stade, vous disposez d’une application hébergée sur Internet, mais vous n’avez aucun moyen d’indiquer à teams où le Rechercher, ni même ce que votre application est appelée.</span><span class="sxs-lookup"><span data-stu-id="9f99a-170">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="9f99a-171">Pour ce faire, vous devez maintenant créer un package d’application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-171">To do this you now have to create an app package.</span></span> <span data-ttu-id="9f99a-172">Il ne s’agit que d’un fichier texte qui contient le manifeste de l’application et de certaines icônes que le client teams utilisera pour afficher et personnaliser correctement votre application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-172">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="9f99a-173">Vous pouvez créer manuellement ce package d’application, ou vous pouvez utiliser app Studio, un outil qui s’exécute dans teams pour simplifier le processus d’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-173">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="9f99a-174">Il est recommandé d’App Studio pour créer et mettre à jour le package d’application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-174">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="9f99a-175">Pour les deux méthodes, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9f99a-175">For either method you will need the following:</span></span>

- <span data-ttu-id="9f99a-176">URL où votre application peut être trouvée sur Internet.</span><span class="sxs-lookup"><span data-stu-id="9f99a-176">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="9f99a-177">Icônes que teams utilisera pour personnaliser votre application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-177">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="9f99a-178">L’exemple est fourni avec des icônes d’espace réservé situées dans «src\static\images.</span><span class="sxs-lookup"><span data-stu-id="9f99a-178">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="9f99a-179">App Studio fournira également les icônes par défaut si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9f99a-179">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="9f99a-180">Mettre à jour votre application hébergée</span><span class="sxs-lookup"><span data-stu-id="9f99a-180">Update your hosted app</span></span>

<span data-ttu-id="9f99a-181">L’exemple d’application requiert que les variables d’environnement suivantes soient définies sur les valeurs que vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="9f99a-181">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="9f99a-182">La manière dont vous effectuez cette opération diffère selon la manière dont vous avez hébergé votre application.</span><span class="sxs-lookup"><span data-stu-id="9f99a-182">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="9f99a-183">L’utilisation de variables d’environnement est importante dans la mesure où ces valeurs font partie de votre environnement : elles sont accessibles par le code de votre application, mais elles ne sont pas exposées à des tiers qui peuvent examiner les fichiers qui composent votre site.</span><span class="sxs-lookup"><span data-stu-id="9f99a-183">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="9f99a-184">Si vous exécutez l’application à l’aide de ngrok, vous devez configurer certaines variables d’environnement locales.</span><span class="sxs-lookup"><span data-stu-id="9f99a-184">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="9f99a-185">Il existe de nombreuses façons de le faire, mais le plus simple, si vous utilisez Visual Studio code, est d’ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span><span class="sxs-lookup"><span data-stu-id="9f99a-185">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="9f99a-186">Où :</span><span class="sxs-lookup"><span data-stu-id="9f99a-186">Where:</span></span>

<span data-ttu-id="9f99a-187">MICROSOFT_APP_ID et MICROSOFT_APP_PASSWORD sont respectivement l’ID et le mot de passe de votre robot.</span><span class="sxs-lookup"><span data-stu-id="9f99a-187">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="9f99a-188">NODE_DEBUG vous montrera ce qui se passe dans votre bot dans la console de débogage de code Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9f99a-188">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="9f99a-189">NODE_CONFIG_DIR pointe vers le répertoire situé à la racine du référentiel (par défaut, lorsque l’application est exécutée localement, elle la recherche dans le dossier src).</span><span class="sxs-lookup"><span data-stu-id="9f99a-189">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="9f99a-190">Si vous n’avez pas arrêté NPM de la version antérieure dans le didacticiel, vous devrez `npm stop` exécuter pour que Visual Studio code collecte correctement vos variables de configuration de lancement.</span><span class="sxs-lookup"><span data-stu-id="9f99a-190">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="9f99a-191">Configurer l’onglet application</span><span class="sxs-lookup"><span data-stu-id="9f99a-191">Configure the app tab</span></span>

<span data-ttu-id="9f99a-192">Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="9f99a-192">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="9f99a-193">Accédez à un canal de l’équipe et cliquez sur le bouton **« + »** pour ajouter un nouvel onglet. Vous pouvez ensuite choisir `Hello World` dans la liste **Ajouter un onglet** .</span><span class="sxs-lookup"><span data-stu-id="9f99a-193">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="9f99a-194">Une boîte de dialogue de configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9f99a-194">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="9f99a-195">Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal.</span><span class="sxs-lookup"><span data-stu-id="9f99a-195">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="9f99a-196">Une fois que vous avez sélectionné l’onglet `Save` , puis cliqué sur `Hello World` , vous pouvez voir l’onglet chargé avec l’onglet que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="9f99a-196">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Capture d’écran de la configuration" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="9f99a-198">Tester votre robot dans teams</span><span class="sxs-lookup"><span data-stu-id="9f99a-198">Test your bot in Teams</span></span>

<span data-ttu-id="9f99a-199">Vous pouvez désormais interagir avec le bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9f99a-199">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="9f99a-200">Sélectionnez un canal dans l’équipe où vous avez enregistré votre application, puis `@your-bot-name`tapez, suivi de votre message.</span><span class="sxs-lookup"><span data-stu-id="9f99a-200">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="9f99a-201">Il s’agit d’une \*\* \@mention\*\*.</span><span class="sxs-lookup"><span data-stu-id="9f99a-201">This is called an **\@mention**.</span></span> <span data-ttu-id="9f99a-202">Tout message que vous envoyez au bot vous sera renvoyé en tant que réponse.</span><span class="sxs-lookup"><span data-stu-id="9f99a-202">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="Réponses de robot" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="9f99a-204">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9f99a-204">Test your messaging extension</span></span>

<span data-ttu-id="9f99a-205">Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée de votre affichage conversation.</span><span class="sxs-lookup"><span data-stu-id="9f99a-205">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="9f99a-206">Un menu s’affiche avec l’application **« Hello World »** .</span><span class="sxs-lookup"><span data-stu-id="9f99a-206">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="9f99a-207">Lorsque vous cliquez dessus, vous verrez un certain nombre de textes aléatoires.</span><span class="sxs-lookup"><span data-stu-id="9f99a-207">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="9f99a-208">Vous pouvez choisir l’un d’entre eux et l’insérer dans votre conversation.</span><span class="sxs-lookup"><span data-stu-id="9f99a-208">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" title="Menu extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" title="Résultat de l’extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="9f99a-211">Choisissez l’un des textes aléatoires, et vous verrez une carte formatée et prête à envoyer avec votre propre message en bas.</span><span class="sxs-lookup"><span data-stu-id="9f99a-211">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" title="Envoi d’extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
