---
title: 'Didacticiel : créer votre première application à l’aide du générateur Yeoman'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec le générateur Yeoman.
keywords: mise en node.js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037003"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="ca33e-104">Créer votre première application Microsoft Teams à l’aide du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="ca33e-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

>[!Note]
><span data-ttu-id="ca33e-105">Ce didacticiel provient du [générateur Yeoman pour le wiki Teams.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="ca33e-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="ca33e-106">Dans ce didacticiel, nous allons passer en premier lieu à la création de votre toute première application Microsoft Teams à l’aide du générateur Yeoman Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ca33e-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="ca33e-107">Il part du principe que vous avez un compte Teams qui permet le chargement de version de [l’application.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="ca33e-107">It assumes that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![Git du générateur yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="ca33e-109">Installer et préparer votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="ca33e-109">Setup and prepare your machine</span></span>

<span data-ttu-id="ca33e-110">Vous devez installer ce qui suit sur votre ordinateur avant de commencer à utiliser le générateur Yeoman.</span><span class="sxs-lookup"><span data-stu-id="ca33e-110">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="ca33e-111">Installer Node.js.</span><span class="sxs-lookup"><span data-stu-id="ca33e-111">Install Node.js</span></span>

<span data-ttu-id="ca33e-112">Vous devez avoir installé Node.js sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ca33e-112">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="ca33e-113">Vous devez utiliser la dernière [version de LTS.](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="ca33e-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="ca33e-114">Installer un éditeur de code</span><span class="sxs-lookup"><span data-stu-id="ca33e-114">Install a code editor</span></span>

<span data-ttu-id="ca33e-115">Vous avez également besoin d’un éditeur de code, n’hésitez pas à utiliser l’éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ca33e-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="ca33e-116">Toutefois, la plupart de cette documentation et captures d’écran font référence à [l’utilisation Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ca33e-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="ca33e-117">Installer Yeoman et Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="ca33e-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="ca33e-118">Pour pouvoir échafauder des projets à l’aide du générateur Teams, vous devez installer l’outil Yeoman ainsi que le gestionnaire des tâches gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="ca33e-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="ca33e-119">Ouvrez une invite de commandes et tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ca33e-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="ca33e-120">Installer le générateur</span><span class="sxs-lookup"><span data-stu-id="ca33e-120">Install the generator</span></span>

<span data-ttu-id="ca33e-121">Installez le générateur Yeoman teams avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ca33e-121">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="ca33e-122">Pour installer les versions d’aperçu du générateur, exécutez la commande ci-après :</span><span class="sxs-lookup"><span data-stu-id="ca33e-122">To install preview versions of the generator, run this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="ca33e-123">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="ca33e-123">Generate your project</span></span>

<span data-ttu-id="ca33e-124">Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet et dans ce répertoire exécutez la `yo teams` commande.</span><span class="sxs-lookup"><span data-stu-id="ca33e-124">Open up a command prompt and create a new directory where you want to create your project and in that directory run the command `yo teams`.</span></span>

<span data-ttu-id="ca33e-125">Cela démarre le générateur, qui vous invite à répondre à un ensemble de questions.</span><span class="sxs-lookup"><span data-stu-id="ca33e-125">This starts the generator, which prompts you with a set of questions.</span></span>

![équipes yo](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="ca33e-127">La première question porte sur le nom de votre projet, vous pouvez le laisser tel qu’il est en appuyant sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="ca33e-127">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="ca33e-128">La question suivante vous demande si vous souhaitez créer un répertoire ou utiliser le répertoire actuel.</span><span class="sxs-lookup"><span data-stu-id="ca33e-128">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="ca33e-129">Comme nous sommes déjà dans le répertoire que nous voulons, nous appuyons simplement sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="ca33e-129">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="ca33e-130">L’étape suivante demande un titre de votre projet, ce titre sera utilisé dans le manifeste et la description de votre application.</span><span class="sxs-lookup"><span data-stu-id="ca33e-130">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="ca33e-131">Vous serez ensuite invité à obtenir un nom de société, qui sera également utilisé dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="ca33e-131">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="ca33e-132">La cinquième question vous demande quelle version du manifeste vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="ca33e-132">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="ca33e-133">Pour ce didacticiel, `v1.5` sélectionnez, qui est le schéma général disponible actuel.</span><span class="sxs-lookup"><span data-stu-id="ca33e-133">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="ca33e-134">Après cela, le générateur vous demandera quels éléments vous souhaitez ajouter à votre projet.</span><span class="sxs-lookup"><span data-stu-id="ca33e-134">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="ca33e-135">Vous pouvez sélectionner un seul ou n’importe quelle combinaison d’éléments.</span><span class="sxs-lookup"><span data-stu-id="ca33e-135">You can select a single one or any combination of items.</span></span> <span data-ttu-id="ca33e-136">Pour l’instant, sélectionnez *simplement un onglet.*</span><span class="sxs-lookup"><span data-stu-id="ca33e-136">For now, just select *a Tab*.</span></span>

![sélection d’élément](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="ca33e-138">En fonction des éléments que vous sélectionnez, vous serez invité à répondre à un ensemble de questions de suivi.</span><span class="sxs-lookup"><span data-stu-id="ca33e-138">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="ca33e-139">Vous devez maintenant entrer une URL de l’endroit où vous hébergez votre solution.</span><span class="sxs-lookup"><span data-stu-id="ca33e-139">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="ca33e-140">Il peut s’agit de n’importe quelle URL, mais par défaut, le générateur suggère une URL de sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="ca33e-140">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="ca33e-141">Le générateur comporte un grand nombre de fonctionnalités avancées intégrées que vous pouvez choisir d’utiliser ou de refuser.</span><span class="sxs-lookup"><span data-stu-id="ca33e-141">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="ca33e-142">À la suite de la question d’URL qui vous sera posée si vous souhaitez inclure un test unitaire pour votre solution, la valeur par défaut est oui.</span><span class="sxs-lookup"><span data-stu-id="ca33e-142">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="ca33e-143">Si vous choisissez cette option, le projet généré aura une infrastructure de test unitaire et certains tests unitaires par défaut pour les différents éléments en cours de structure.</span><span class="sxs-lookup"><span data-stu-id="ca33e-143">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="ca33e-144">Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.</span><span class="sxs-lookup"><span data-stu-id="ca33e-144">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="ca33e-145">Pour faciliter la journalisation, vous serez également invité à utiliser Azure Application Insights pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="ca33e-145">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="ca33e-146">Si vous choisissez Oui, vous devez fournir une clé Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ca33e-146">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="ca33e-147">Pour ce didacticiel, dés optez pour l’utilisation d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ca33e-147">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="ca33e-148">L’ensemble de questions suivant sera basé sur votre sélection d’éléments précédemment.</span><span class="sxs-lookup"><span data-stu-id="ca33e-148">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="ca33e-149">Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez être en mesure d’utiliser cette application en tant que partie Web SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="ca33e-149">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="ca33e-150">Une fois que vous avez fourni ce nom, le générateur génère le projet et installe toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="ca33e-150">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="ca33e-151">Cela prendra une minute ou deux.</span><span class="sxs-lookup"><span data-stu-id="ca33e-151">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="ca33e-152">Ajouter du code à votre onglet</span><span class="sxs-lookup"><span data-stu-id="ca33e-152">Add some code to your tab</span></span>

<span data-ttu-id="ca33e-153">Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code favori.</span><span class="sxs-lookup"><span data-stu-id="ca33e-153">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="ca33e-154">Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé . Vous pouvez en savoir plus à ce sujet dans la documentation [de structure de](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) projet.</span><span class="sxs-lookup"><span data-stu-id="ca33e-154">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="ca33e-155">Votre onglet se trouve dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier.</span><span class="sxs-lookup"><span data-stu-id="ca33e-155">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="ca33e-156">Il s’agit de la classe React TypeScript pour votre onglet. Recherchez la méthode et ajoutez une ligne de code à l’intérieur du contrôle afin qu’elle `render()` `<PanelBody>` ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="ca33e-156">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="ca33e-157">Enregistrez le fichier et revenir à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="ca33e-157">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="ca33e-158">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="ca33e-158">Build your app</span></span>

<span data-ttu-id="ca33e-159">Vous pouvez maintenant créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="ca33e-159">You can now build your project.</span></span> <span data-ttu-id="ca33e-160">Cette étape est effectuée en deux étapes (ou une étape, voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="ca33e-160">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="ca33e-161">Tout d’abord, vous devez créer le fichier manifeste de l’application Teams, que vous téléchargez/chargez de nouveau dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ca33e-161">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="ca33e-162">Cette tâche est effectuée par la tâche Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="ca33e-162">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="ca33e-163">Cela valide le manifeste et crée un fichier zip dans `./package` le répertoire.</span><span class="sxs-lookup"><span data-stu-id="ca33e-163">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="ca33e-164">Pour créer votre solution, utilisez la `gulp build` commande.</span><span class="sxs-lookup"><span data-stu-id="ca33e-164">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="ca33e-165">Cela transpile votre solution dans le `./dist` dossier.</span><span class="sxs-lookup"><span data-stu-id="ca33e-165">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="ca33e-166">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ca33e-166">Run your app</span></span>

<span data-ttu-id="ca33e-167">Pour exécuter votre application, utilisez la `gulp serve` commande.</span><span class="sxs-lookup"><span data-stu-id="ca33e-167">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="ca33e-168">Cela permet de créer et de démarrer un serveur web local pour tester votre application.</span><span class="sxs-lookup"><span data-stu-id="ca33e-168">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="ca33e-169">La commande reconstruira également l’application chaque fois que vous enregistrez un fichier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ca33e-169">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="ca33e-170">Vous devez maintenant être en mesure de parcourir pour `http://localhost:3007/myFirstAppTab/` vous assurer que votre onglet est rendu.</span><span class="sxs-lookup"><span data-stu-id="ca33e-170">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="ca33e-171">Toutefois, pas encore dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ca33e-171">However, not in Microsoft Teams yet.</span></span>

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="ca33e-173">Exécuter votre application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ca33e-173">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="ca33e-174">Microsoft Teams ne vous permet pas d’héberger votre application sur localhost. Vous devez donc la publier sur une URL publique ou utiliser un proxy tel que ngrok.</span><span class="sxs-lookup"><span data-stu-id="ca33e-174">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="ca33e-175">La bonne nouvelle est que le projet échafaudé dispose de ce projet intégré.</span><span class="sxs-lookup"><span data-stu-id="ca33e-175">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="ca33e-176">Lorsque vous exécutez le service ngrok, il est démarré en arrière-plan, avec une entrée DNS unique et publique, et il inséra également le manifeste avec cette URL unique, puis il fera exactement la même chose que `gulp ngrok-serve` `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="ca33e-176">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="ca33e-177">Après l’exécution, créez une équipe Microsoft Teams et, lorsqu’elle est créée, cliquez sur le nom de l’équipe, pour aller aux paramètres d’équipe, puis `gulp ngrok-serve` sélectionnez *Applications.*</span><span class="sxs-lookup"><span data-stu-id="ca33e-177">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="ca33e-178">Dans le coin inférieur droit, vous devez voir un lien Télécharger une application *personnalisée,* sélectionnez-la, puis accédez au dossier de votre projet et au sous-dossier `package` appelé.</span><span class="sxs-lookup"><span data-stu-id="ca33e-178">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="ca33e-179">Sélectionnez le fichier zip dans ce dossier, puis ouvrez.</span><span class="sxs-lookup"><span data-stu-id="ca33e-179">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="ca33e-180">Votre application est désormais rechargée de nouveau dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ca33e-180">Your App is now sideloaded into Microsoft Teams.</span></span>

![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="ca33e-182">Revenir au canal *Général* et choisir *+* d’ajouter un nouvel onglet. Votre onglet doit s’y voir dans la liste des onglets.</span><span class="sxs-lookup"><span data-stu-id="ca33e-182">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![configurer l’onglet](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="ca33e-184">Choisissez votre onglet et suivez les instructions pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="ca33e-184">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="ca33e-185">Notez que vous avez une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source.</span><span class="sxs-lookup"><span data-stu-id="ca33e-185">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="ca33e-186">Sélectionnez *Enregistrer* pour ajouter votre onglet au canal.</span><span class="sxs-lookup"><span data-stu-id="ca33e-186">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="ca33e-187">Une fois que vous avez terminé, votre onglet doit être chargé dans Microsoft Teams !</span><span class="sxs-lookup"><span data-stu-id="ca33e-187">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![exécution de l’onglet dans teams](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="ca33e-189">**Félicitations ! Vous avez créé et déployé votre première application Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="ca33e-189">**Congrats! You built and deployed your first Microsoft Teams app**</span></span>
