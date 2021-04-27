---
title: Didacticiel - Créer votre première application à l'aide du générateur Yeoman
description: Découvrez comment commencer à créer des applications Microsoft Teams avec le générateur Yeoman.
keywords: mise en node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 9efbe6f6e6502120f1afdadb9b538182f1406c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018431"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="58a6d-104">Créer votre première application Microsoft Teams à l'aide du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="58a6d-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="58a6d-105">Ce didacticiel provient du [générateur Yeoman pour le wiki Teams.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="58a6d-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="58a6d-106">Dans ce didacticiel, nous allons passer en premier lieu à la création de votre toute première application Microsoft Teams à l'aide du générateur Yeoman Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="58a6d-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="58a6d-107">Il vous dirige également tout au long du processus de mise à niveau de teams à l'aide du générateur Yeoman.</span><span class="sxs-lookup"><span data-stu-id="58a6d-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="58a6d-108">La condition préalable pour commencer avec ce didacticiel est que vous avez un compte Teams qui permet le chargement de version de version [d'application.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="58a6d-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![Git du générateur yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="58a6d-110">Installer et préparer votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="58a6d-110">Setup and prepare your machine</span></span>

<span data-ttu-id="58a6d-111">Vous devez installer ce qui suit sur votre ordinateur avant de commencer à utiliser le générateur Yeoman.</span><span class="sxs-lookup"><span data-stu-id="58a6d-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="58a6d-112">Installer Node.js.</span><span class="sxs-lookup"><span data-stu-id="58a6d-112">Install Node.js</span></span>

<span data-ttu-id="58a6d-113">Vous devez avoir installé Node.js sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="58a6d-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="58a6d-114">Vous devez utiliser la dernière [version de LTS.](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="58a6d-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="58a6d-115">Installer un éditeur de code</span><span class="sxs-lookup"><span data-stu-id="58a6d-115">Install a code editor</span></span>

<span data-ttu-id="58a6d-116">Vous avez besoin d'un éditeur de code.</span><span class="sxs-lookup"><span data-stu-id="58a6d-116">You need a code editor.</span></span> <span data-ttu-id="58a6d-117">La plupart de cette documentation et images font référence à l'utilisation [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="58a6d-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="58a6d-118">Toutefois, n'hésitez pas à utiliser l'éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="58a6d-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="58a6d-119">Installer Yeoman et Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="58a6d-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="58a6d-120">Pour échafauder des projets à l'aide du générateur, vous devez installer l'outil Yeoman et le gestionnaire des tâches gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="58a6d-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="58a6d-121">Ouvrez une invite de commandes et tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="58a6d-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="58a6d-122">Installer le générateur</span><span class="sxs-lookup"><span data-stu-id="58a6d-122">Install the generator</span></span>

<span data-ttu-id="58a6d-123">Installez le générateur Yeoman teams avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="58a6d-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="58a6d-124">Installez la version d'aperçu du générateur avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="58a6d-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="58a6d-125">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="58a6d-125">Generate your project</span></span>

<span data-ttu-id="58a6d-126">Cette section vous présente les étapes de génération de votre projet.</span><span class="sxs-lookup"><span data-stu-id="58a6d-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="58a6d-127">**Pour générer votre projet**</span><span class="sxs-lookup"><span data-stu-id="58a6d-127">**To generate your project**</span></span>

1. <span data-ttu-id="58a6d-128">Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet, puis exécutez la commande dans ce `yo teams` répertoire.</span><span class="sxs-lookup"><span data-stu-id="58a6d-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="58a6d-129">Le générateur démarre.</span><span class="sxs-lookup"><span data-stu-id="58a6d-129">The generator starts.</span></span>
1. <span data-ttu-id="58a6d-130">Répondez à l'ensemble des questions posées par le générateur.</span><span class="sxs-lookup"><span data-stu-id="58a6d-130">Respond to the set of questions prompted by the generator.</span></span>

   ![équipes yo](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="58a6d-132">La première question porte sur le nom de votre projet, vous pouvez le laisser tel qu'il est en appuyant sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="58a6d-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="58a6d-133">La question suivante vous demande si vous souhaitez créer un répertoire ou utiliser le répertoire actuel.</span><span class="sxs-lookup"><span data-stu-id="58a6d-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="58a6d-134">Comme vous êtes déjà dans le répertoire que vous souhaitez, appuyez simplement sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="58a6d-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="58a6d-135">Dans la question suivante, tapez le titre de votre projet.</span><span class="sxs-lookup"><span data-stu-id="58a6d-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="58a6d-136">Ce titre sera utilisé dans le manifeste et la description de votre application.</span><span class="sxs-lookup"><span data-stu-id="58a6d-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="58a6d-137">Ensuite, un nom de société vous sera demandé, qui sera également utilisé dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="58a6d-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="58a6d-138">La cinquième question vous demande quelle version du manifeste vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="58a6d-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="58a6d-139">Pour ce didacticiel, `v1.5` sélectionnez, qui est le schéma général disponible actuel.</span><span class="sxs-lookup"><span data-stu-id="58a6d-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="58a6d-140">Ensuite, le générateur vous demandera quels éléments vous souhaitez ajouter à votre projet.</span><span class="sxs-lookup"><span data-stu-id="58a6d-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="58a6d-141">Vous pouvez sélectionner un seul ou n'importe quelle combinaison d'éléments.</span><span class="sxs-lookup"><span data-stu-id="58a6d-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="58a6d-142">Pour ce didacticiel, sélectionnez *simplement un onglet.*</span><span class="sxs-lookup"><span data-stu-id="58a6d-142">For this tutorials, just select *a Tab*.</span></span>

    ![sélection d'élément](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="58a6d-144">Répondez à l'ensemble suivant de questions de suivi qui s'affichent en fonction des éléments que vous avez sélectionnés à l'étape 2.</span><span class="sxs-lookup"><span data-stu-id="58a6d-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="58a6d-145">Entrez une URL de l'endroit où vous hébergez votre solution.</span><span class="sxs-lookup"><span data-stu-id="58a6d-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="58a6d-146">L'URL peut être n'importe quelle URL, mais par défaut, le générateur suggère une URL de site web Azure.</span><span class="sxs-lookup"><span data-stu-id="58a6d-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="58a6d-147">Dans la question suivante, confirmez si vous souhaitez inclure des tests unitaires pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="58a6d-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="58a6d-148">La réponse par défaut est *oui*.</span><span class="sxs-lookup"><span data-stu-id="58a6d-148">The default response is *yes*.</span></span> <span data-ttu-id="58a6d-149">Si vous choisissez d'inclure le test unitaire, le projet généré aura une infrastructure de test unitaire et des tests unitaires par défaut pour les différents éléments en cours de structure.</span><span class="sxs-lookup"><span data-stu-id="58a6d-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="58a6d-150">Pour ce didacticiel, choisissez de ne pas inclure d'infrastructure de test.</span><span class="sxs-lookup"><span data-stu-id="58a6d-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="58a6d-151">Le générateur comporte un grand nombre de fonctionnalités avancées intégrées que vous pouvez choisir d'utiliser ou de refuser.</span><span class="sxs-lookup"><span data-stu-id="58a6d-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="58a6d-152">Pour faciliter la signature, vous serez également invité à utiliser Azure Application Insights pour la signature.</span><span class="sxs-lookup"><span data-stu-id="58a6d-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="58a6d-153">Si vous choisissez *Oui,* vous devez fournir une clé Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58a6d-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="58a6d-154">Pour ce didacticiel, dés optez pour l'utilisation d'Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58a6d-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="58a6d-155">L'ensemble de questions suivant sera basé sur les éléments précédemment sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="58a6d-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="58a6d-156">Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez être en mesure d'utiliser cette application en tant que partie Web SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="58a6d-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="58a6d-157">Une fois que vous avez fourni le nom, le générateur génère le projet et installe toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="58a6d-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="58a6d-158">Cela prendra une minute ou deux.</span><span class="sxs-lookup"><span data-stu-id="58a6d-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="58a6d-159">Ajouter du code à votre onglet</span><span class="sxs-lookup"><span data-stu-id="58a6d-159">Add some code to your tab</span></span>

<span data-ttu-id="58a6d-160">Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code favori.</span><span class="sxs-lookup"><span data-stu-id="58a6d-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="58a6d-161">Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé.</span><span class="sxs-lookup"><span data-stu-id="58a6d-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="58a6d-162">Pour plus d'informations, voir la documentation [relative à la structure du](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) projet.</span><span class="sxs-lookup"><span data-stu-id="58a6d-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="58a6d-163">Votre onglet se trouve dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier.</span><span class="sxs-lookup"><span data-stu-id="58a6d-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="58a6d-164">Il s'agit de la classe React TypeScript pour votre onglet. Recherchez la méthode et ajoutez une ligne de code à l'intérieur du contrôle afin `render()` `<PanelBody>` qu'elle ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="58a6d-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="58a6d-165">Enregistrez le fichier et revenir à l'invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="58a6d-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="58a6d-166">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="58a6d-166">Build your app</span></span>

<span data-ttu-id="58a6d-167">Vous pouvez maintenant créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="58a6d-167">You can now build your project.</span></span> <span data-ttu-id="58a6d-168">Cette étape est effectuée en deux étapes (ou une étape, voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="58a6d-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="58a6d-169">Tout d'abord, vous devez créer le fichier manifeste de l'application Teams, que vous téléchargez/chargez de nouveau dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="58a6d-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="58a6d-170">Cette tâche est effectuée par la tâche Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="58a6d-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="58a6d-171">Cela valide le manifeste et crée un fichier zip dans `./package` le répertoire.</span><span class="sxs-lookup"><span data-stu-id="58a6d-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="58a6d-172">Pour créer votre solution, utilisez la `gulp build` commande.</span><span class="sxs-lookup"><span data-stu-id="58a6d-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="58a6d-173">Cela transpile votre solution dans le `./dist` dossier.</span><span class="sxs-lookup"><span data-stu-id="58a6d-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="58a6d-174">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="58a6d-174">Run your app</span></span>

<span data-ttu-id="58a6d-175">Pour exécuter votre application, utilisez la `gulp serve` commande.</span><span class="sxs-lookup"><span data-stu-id="58a6d-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="58a6d-176">Cela permet de créer et de démarrer un serveur web local pour tester votre application.</span><span class="sxs-lookup"><span data-stu-id="58a6d-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="58a6d-177">La commande reconstruira également l'application chaque fois que vous enregistrez un fichier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="58a6d-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="58a6d-178">Vous devez maintenant être en mesure de parcourir pour `http://localhost:3007/myFirstAppTab/` vous assurer que votre onglet est rendu.</span><span class="sxs-lookup"><span data-stu-id="58a6d-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="58a6d-179">Toutefois, pas encore dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="58a6d-179">However, not in Microsoft Teams yet.</span></span>

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="58a6d-181">Exécuter votre application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="58a6d-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="58a6d-182">Microsoft Teams ne vous permet pas d'héberger votre application sur localhost. Vous devez donc la publier sur une URL publique ou utiliser un proxy tel que ngrok.</span><span class="sxs-lookup"><span data-stu-id="58a6d-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="58a6d-183">La bonne nouvelle est que le projet échafaudé dispose de ce projet intégré.</span><span class="sxs-lookup"><span data-stu-id="58a6d-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="58a6d-184">Lorsque vous exécutez le service ngrok, il est démarré en arrière-plan, avec une entrée DNS unique et publique, et il inséra également le manifeste avec cette URL unique, puis il fera exactement la même chose que `gulp ngrok-serve` `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="58a6d-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="58a6d-185">Après l'exécution, créez une équipe Microsoft Teams et, lorsqu'elle est créée, cliquez sur le nom de l'équipe, pour aller aux paramètres d'équipe, puis `gulp ngrok-serve` sélectionnez *Applications.*</span><span class="sxs-lookup"><span data-stu-id="58a6d-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="58a6d-186">Dans le coin inférieur droit, vous devez voir un lien Télécharger une application *personnalisée,* sélectionnez-la, puis accédez au dossier de votre projet et au sous-dossier `package` appelé.</span><span class="sxs-lookup"><span data-stu-id="58a6d-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="58a6d-187">Sélectionnez le fichier zip dans ce dossier, puis ouvrez.</span><span class="sxs-lookup"><span data-stu-id="58a6d-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="58a6d-188">Votre application est désormais rechargée de nouveau dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="58a6d-188">Your App is now sideloaded into Microsoft Teams.</span></span>

![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="58a6d-190">Revenir au canal *Général* et choisir *+* d'ajouter un nouvel onglet. Votre onglet doit s'y voir dans la liste des onglets.</span><span class="sxs-lookup"><span data-stu-id="58a6d-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![configurer l'onglet](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="58a6d-192">Choisissez votre onglet et suivez les instructions pour l'ajouter.</span><span class="sxs-lookup"><span data-stu-id="58a6d-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="58a6d-193">Notez que vous avez une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source.</span><span class="sxs-lookup"><span data-stu-id="58a6d-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="58a6d-194">Sélectionnez *Enregistrer* pour ajouter votre onglet au canal.</span><span class="sxs-lookup"><span data-stu-id="58a6d-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="58a6d-195">Une fois que vous avez terminé, votre onglet doit être chargé dans Microsoft Teams !</span><span class="sxs-lookup"><span data-stu-id="58a6d-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![exécution de l'onglet dans teams](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="58a6d-197">Mettre à niveau Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="58a6d-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="58a6d-198">Vous pouvez également mettre à niveau votre version actuelle de Microsoft Teams vers la dernière version à l'aide du générateur Yeoman Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="58a6d-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="58a6d-199">**Pour mettre à niveau Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="58a6d-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="58a6d-200">Obtenez la version actuelle de Teams avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="58a6d-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="58a6d-201">Utilisez la commande suivante pour sélectionner mettre à jour votre générateur :</span><span class="sxs-lookup"><span data-stu-id="58a6d-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="58a6d-202">Utilisez les touches de direction pour choisir **Mettre à jour vos générateurs.**</span><span class="sxs-lookup"><span data-stu-id="58a6d-202">Use the  arrow keys to choose **Update your Generators**.</span></span>

   ![image de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="58a6d-204">Sélectionnez le générateur de votre choix dans la liste des générateurs.</span><span class="sxs-lookup"><span data-stu-id="58a6d-204">Select the generator you want from the list of generators.</span></span>
   > [!NOTE]
   > <span data-ttu-id="58a6d-205">Utilisez la barre d'espace pour sélectionner ou effacer une version sélectionnée de Teams parmi les options disponibles.</span><span class="sxs-lookup"><span data-stu-id="58a6d-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![image de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="58a6d-207">L'installation de Teams prend quelques secondes à quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="58a6d-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="58a6d-208">Une fois l'installation terminée, utilisez la commande suivante pour vérifier la version installée :</span><span class="sxs-lookup"><span data-stu-id="58a6d-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="58a6d-209">**Félicitations ! Vous avez créé et déployé votre première application Microsoft Teams. Vous avez également mis à niveau Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="58a6d-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
