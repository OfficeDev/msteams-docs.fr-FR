---
title: Prise en main du générateur Yeoman pour Microsoft teams
description: Commencer à créer des applications intéressantes avec le générateur Yeoman pour Microsoft teams
keywords: mise en route node.js NodeJS Yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f9b3f165d3b5387f8e7d30563134ed4889920ca5
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237992"
---
# <a name="build-your-first-microsoft-teams-app"></a><span data-ttu-id="7ce29-104">Créer votre première application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="7ce29-104">Build your First Microsoft Teams App</span></span>

>[!Note]
><span data-ttu-id="7ce29-105">Ce didacticiel provient du [Générateur Yeoman pour le wiki teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="7ce29-105">This tutorial comes from the [yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span></span>

<span data-ttu-id="7ce29-106">Dans ce didacticiel, nous allons passer par la création de votre première application Microsoft teams à l’aide du générateur Yeoman de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7ce29-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="7ce29-107">Il part du principe que vous avez [activé le chargement latéral des applications Microsoft teams](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7ce29-107">It assumes that you have [enabled side-loading of Microsoft Teams apps](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![git du générateur Yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="7ce29-109">Configurer et préparer votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="7ce29-109">Setup and prepare your machine</span></span>

<span data-ttu-id="7ce29-110">Vous devez installer les éléments suivants sur votre ordinateur avant de commencer à utiliser le générateur teams.</span><span class="sxs-lookup"><span data-stu-id="7ce29-110">You need to install the following on your machine before starting to use the Teams Generator.</span></span>

### <a name="install-node"></a><span data-ttu-id="7ce29-111">Nœud Installer</span><span class="sxs-lookup"><span data-stu-id="7ce29-111">Install Node</span></span>

<span data-ttu-id="7ce29-112">NodeJS doit être installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ce29-112">You need to have NodeJS installed on your machine.</span></span> <span data-ttu-id="7ce29-113">Vous devez utiliser la dernière [version d’LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="7ce29-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="7ce29-114">Installer un éditeur de code</span><span class="sxs-lookup"><span data-stu-id="7ce29-114">Install a code editor</span></span>

<span data-ttu-id="7ce29-115">Vous avez également besoin d’un éditeur de code, n’hésitez pas à utiliser l’éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="7ce29-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="7ce29-116">Toutefois, la plupart de ces documents et captures d’écran font référence à l’utilisation de [Visual Studio code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="7ce29-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="7ce29-117">Installer Yeoman et Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="7ce29-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="7ce29-118">Pour être en mesure de structurer des projets à l’aide du générateur Teams, vous devez installer l’outil Yeoman ainsi que le gestionnaire des tâches CLI de Gulp.</span><span class="sxs-lookup"><span data-stu-id="7ce29-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="7ce29-119">Ouvrez une invite de commandes et tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7ce29-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a><span data-ttu-id="7ce29-120">Installer le générateur d’applications Microsoft teams-Yo teams</span><span class="sxs-lookup"><span data-stu-id="7ce29-120">Install the Microsoft Teams Apps generator - Yo Teams</span></span>

<span data-ttu-id="7ce29-121">Le générateur Yeoman pour les applications Microsoft teams est installé avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7ce29-121">The Yeoman generator for Microsoft Teams apps are installed with the following command:</span></span>

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a><span data-ttu-id="7ce29-122">Installer les versions d’évaluation</span><span class="sxs-lookup"><span data-stu-id="7ce29-122">Install preview versions</span></span>

<span data-ttu-id="7ce29-123">Si vous souhaitez installer des versions d’évaluation du générateur teams à l’aide de cette commande, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ce29-123">If you want to install preview versions of the Teams generator with this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="7ce29-124">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="7ce29-124">Generate your project</span></span>

<span data-ttu-id="7ce29-125">Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet, puis tapez la commande dans ce répertoire `yo teams` .</span><span class="sxs-lookup"><span data-stu-id="7ce29-125">Open up a command prompt and create a new directory where you want to create your project and in that directory type the command `yo teams`.</span></span> <span data-ttu-id="7ce29-126">Cette opération démarre le générateur d’applications teams et vous demande un ensemble de questions.</span><span class="sxs-lookup"><span data-stu-id="7ce29-126">This will start the Teams Apps generator and you will be asked a set of questions.</span></span>

![Yo teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="7ce29-128">La première question concerne le nom de votre projet, vous pouvez la laisser telle quelle en appuyant sur entrée.</span><span class="sxs-lookup"><span data-stu-id="7ce29-128">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="7ce29-129">La question suivante vous demande si vous souhaitez créer un nouveau répertoire ou utiliser le répertoire actuel.</span><span class="sxs-lookup"><span data-stu-id="7ce29-129">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="7ce29-130">Comme nous l’avons déjà fait dans le répertoire que nous souhaitons, nous appuyons simplement sur entrée.</span><span class="sxs-lookup"><span data-stu-id="7ce29-130">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="7ce29-131">L’étape suivante demande un titre de votre projet, ce titre sera utilisé dans le manifeste et la description de votre application.</span><span class="sxs-lookup"><span data-stu-id="7ce29-131">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="7ce29-132">Puis vous serez invité à indiquer un nom d’entreprise, qui sera également utilisé dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="7ce29-132">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="7ce29-133">La cinquième question vous demande quelle version du manifeste vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="7ce29-133">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="7ce29-134">Pour ce didacticiel `v1.5` , sélectionnez, qui est le schéma actuellement disponible général.</span><span class="sxs-lookup"><span data-stu-id="7ce29-134">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="7ce29-135">Une fois que ce générateur vous demandera quels éléments vous souhaitez ajouter à votre projet.</span><span class="sxs-lookup"><span data-stu-id="7ce29-135">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="7ce29-136">Vous pouvez sélectionner une seule combinaison ou une combinaison d’éléments.</span><span class="sxs-lookup"><span data-stu-id="7ce29-136">You can select a single one or any combination of items.</span></span> <span data-ttu-id="7ce29-137">Pour le moment, il vous suffit de sélectionner *un onglet*.</span><span class="sxs-lookup"><span data-stu-id="7ce29-137">For now, just select *a Tab*.</span></span>

![sélection de l’élément](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="7ce29-139">En fonction des éléments que vous sélectionnez, vous serez invité à un ensemble de questions de suivi.</span><span class="sxs-lookup"><span data-stu-id="7ce29-139">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="7ce29-140">À présent, vous devez entrer une URL où vous allez héberger votre solution.</span><span class="sxs-lookup"><span data-stu-id="7ce29-140">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="7ce29-141">Il peut s’agir de n’importe quelle URL, mais par défaut, le générateur suggère une URL de sites Web Azure.</span><span class="sxs-lookup"><span data-stu-id="7ce29-141">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="7ce29-142">Le générateur dispose d’un grand nombre de fonctionnalités avancées intégrées que vous pouvez accepter ou refuser.</span><span class="sxs-lookup"><span data-stu-id="7ce29-142">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="7ce29-143">À la suite de la question URL, vous serez invité à indiquer si vous souhaitez inclure des tests unitaires pour votre solution, la valeur par défaut est oui.</span><span class="sxs-lookup"><span data-stu-id="7ce29-143">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="7ce29-144">Si vous choisissez cette option, le projet généré disposera d’une infrastructure de test d’unité et de tests d’unité par défaut pour les différents éléments en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="7ce29-144">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="7ce29-145">Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.</span><span class="sxs-lookup"><span data-stu-id="7ce29-145">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="7ce29-146">Pour faciliter la journalisation, vous serez également invité à indiquer si vous souhaitez utiliser Azure application Insights pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="7ce29-146">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="7ce29-147">Si vous choisissez Oui, vous devrez fournir une clé Insights d’application Azure.</span><span class="sxs-lookup"><span data-stu-id="7ce29-147">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="7ce29-148">Pour ce didacticiel, n’utilisez pas les informations d’application.</span><span class="sxs-lookup"><span data-stu-id="7ce29-148">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="7ce29-149">Le prochain ensemble de questions sera basé sur votre sélection d’éléments précédemment.</span><span class="sxs-lookup"><span data-stu-id="7ce29-149">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="7ce29-150">Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez pouvoir utiliser cette application en tant que composant WebPart SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="7ce29-150">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="7ce29-151">Une fois que vous avez fourni ce nom, le générateur génère le projet et installe toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="7ce29-151">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="7ce29-152">Cette opération prend une ou deux minutes.</span><span class="sxs-lookup"><span data-stu-id="7ce29-152">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="7ce29-153">Ajouter du code à votre onglet</span><span class="sxs-lookup"><span data-stu-id="7ce29-153">Add some code to your tab</span></span>

<span data-ttu-id="7ce29-154">Une fois le générateur exécuté, vous pouvez ouvrir la solution dans votre éditeur de code favori.</span><span class="sxs-lookup"><span data-stu-id="7ce29-154">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="7ce29-155">Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé, vous pouvez en savoir plus à ce sujet dans la documentation sur la [structure du projet](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) .</span><span class="sxs-lookup"><span data-stu-id="7ce29-155">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="7ce29-156">Votre onglet sera situé dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier.</span><span class="sxs-lookup"><span data-stu-id="7ce29-156">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="7ce29-157">Il s’agit de la classe basée sur les réplications de type dactylographié pour votre onglet. Recherchez la `render()` méthode et ajoutez une ligne de code à l’intérieur du `<PanelBody>` contrôle afin qu’elle se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ce29-157">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="7ce29-158">Enregistrez le fichier et revenez à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="7ce29-158">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="7ce29-159">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="7ce29-159">Build your app</span></span>

<span data-ttu-id="7ce29-160">Vous pouvez maintenant générer votre projet.</span><span class="sxs-lookup"><span data-stu-id="7ce29-160">You can now build your project.</span></span> <span data-ttu-id="7ce29-161">Cette opération est réalisée en deux étapes (ou une seule étape, voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="7ce29-161">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="7ce29-162">Tout d’abord, vous devez créer le fichier manifeste de l’application teams que vous téléchargez/chargement dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7ce29-162">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="7ce29-163">Cette opération est exécutée par la tâche Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="7ce29-163">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="7ce29-164">Cela permet de valider le manifeste et de créer un fichier zip dans le `./package` répertoire.</span><span class="sxs-lookup"><span data-stu-id="7ce29-164">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="7ce29-165">Pour créer votre solution, utilisez la `gulp build` commande.</span><span class="sxs-lookup"><span data-stu-id="7ce29-165">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="7ce29-166">Cela permet de transpiler votre solution dans le `./dist` dossier.</span><span class="sxs-lookup"><span data-stu-id="7ce29-166">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="7ce29-167">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="7ce29-167">Run your app</span></span>

<span data-ttu-id="7ce29-168">Pour exécuter votre application, vous utilisez la `gulp serve` commande.</span><span class="sxs-lookup"><span data-stu-id="7ce29-168">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="7ce29-169">Cela permet de créer et de démarrer un serveur Web local pour tester votre application.</span><span class="sxs-lookup"><span data-stu-id="7ce29-169">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="7ce29-170">La commande reconstruira également l’application chaque fois que vous enregistrerez un fichier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="7ce29-170">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="7ce29-171">Vous devez maintenant être en mesure d’accéder à pour `http://localhost:3007/myFirstAppTab/` vérifier que votre onglet est rendu.</span><span class="sxs-lookup"><span data-stu-id="7ce29-171">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="7ce29-172">Toutefois, vous ne disposez pas encore de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7ce29-172">However, not in Microsoft Teams yet.</span></span>

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="7ce29-174">Exécuter votre application dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="7ce29-174">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="7ce29-175">Microsoft Teams ne vous permet pas d’héberger votre application sur localhost, c’est pourquoi vous devez la publier sur une URL publique ou utiliser un proxy tel que ngrok.</span><span class="sxs-lookup"><span data-stu-id="7ce29-175">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="7ce29-176">La bonne nouvelle est que le projet de génération de modèles automatique dispose de cette configuration intégrée.</span><span class="sxs-lookup"><span data-stu-id="7ce29-176">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="7ce29-177">Lorsque vous exécutez `gulp ngrok-serve` le service ngrok est démarré en arrière-plan, avec une entrée DNS unique et publique, et il compresse également le manifeste avec cette URL unique, puis effectue exactement la même chose que `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="7ce29-177">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="7ce29-178">Après avoir exécuté `gulp ngrok-serve` , créez une nouvelle équipe Microsoft teams et, lorsqu’elle est créée, cliquez sur le nom de l’équipe, pour accéder aux paramètres Teams, puis sélectionnez *applications*.</span><span class="sxs-lookup"><span data-stu-id="7ce29-178">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="7ce29-179">Dans le coin inférieur droit, vous devriez voir un lien *charger une application personnalisée*, sélectionnez-le, puis accédez à votre dossier de projet et le sous-dossier appelé `package` .</span><span class="sxs-lookup"><span data-stu-id="7ce29-179">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="7ce29-180">Sélectionnez le fichier zip dans ce dossier, puis cliquez sur Ouvrir.</span><span class="sxs-lookup"><span data-stu-id="7ce29-180">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="7ce29-181">Votre application est désormais versions test chargées dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="7ce29-181">Your App is now sideloaded into Microsoft Teams.</span></span>

![application versions test chargées](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="7ce29-183">Revenez à la chaîne *général* et sélectionnez *+* pour ajouter un nouvel onglet. Votre onglet doit apparaître dans la liste des onglets.</span><span class="sxs-lookup"><span data-stu-id="7ce29-183">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![onglet configurer](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="7ce29-185">Choisissez votre onglet et suivez les instructions pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="7ce29-185">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="7ce29-186">Notez que vous disposez d’une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source.</span><span class="sxs-lookup"><span data-stu-id="7ce29-186">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="7ce29-187">Sélectionnez *Enregistrer* pour ajouter votre onglet au canal.</span><span class="sxs-lookup"><span data-stu-id="7ce29-187">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="7ce29-188">Une fois que vous avez fini de charger votre onglet dans Microsoft teams !</span><span class="sxs-lookup"><span data-stu-id="7ce29-188">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![onglet en cours d’exécution dans teams](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="7ce29-190">**Félicitations ! Vous avez créé et déployé votre première application Microsoft teams**</span><span class="sxs-lookup"><span data-stu-id="7ce29-190">**Congrats! You built and deployed your first Microsoft Teams App**</span></span>
