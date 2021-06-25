---
title: Didacticiel - Créer votre première application à l’aide du générateur Yeoman
description: Découvrez comment commencer à créer des applications Microsoft Teams avec le générateur Yeoman.
keywords: mise en node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: ed9e9c15c1287bb6d26778161302e45833205a75
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114387"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="424ca-104">Créer votre première application Microsoft Teams à l’aide du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="424ca-104">Build your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="424ca-105">Ce didacticiel provient du [générateur Yeoman pour Teams wiki.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="424ca-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="424ca-106">Dans ce didacticiel, vous allez apprendre à créer votre toute première application Microsoft Teams à l’aide Microsoft Teams générateur Yeoman.</span><span class="sxs-lookup"><span data-stu-id="424ca-106">In this tutorial, you will learn how to build your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="424ca-107">Il vous permet également de passer par le processus de mise à niveau de votre Teams à l’aide du générateur Yeoman.</span><span class="sxs-lookup"><span data-stu-id="424ca-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="424ca-108">Avant de commencer, vous devez avoir un compte Teams qui autorise le chargement de version de version [d’application.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="424ca-108">Before you begin, you must have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![Git du générateur yeoman](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="424ca-110">Obtenir les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="424ca-110">Get Prerequisites</span></span>

<span data-ttu-id="424ca-111">Vous devez installer les logiciels suivants sur votre ordinateur avant de commencer à utiliser le générateur Yeoman :</span><span class="sxs-lookup"><span data-stu-id="424ca-111">You need to install the following on your machine before starting to use the Yeoman generator:</span></span>

* <span data-ttu-id="424ca-112">Node.js</span><span class="sxs-lookup"><span data-stu-id="424ca-112">Node.js</span></span>

   <span data-ttu-id="424ca-113">Vous devez avoir installé Node.js sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="424ca-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="424ca-114">Vous devez utiliser la dernière [version de LTS.](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="424ca-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

* <span data-ttu-id="424ca-115">Un éditeur de code</span><span class="sxs-lookup"><span data-stu-id="424ca-115">A code editor</span></span>

   <span data-ttu-id="424ca-116">Vous avez besoin d’un éditeur de code.</span><span class="sxs-lookup"><span data-stu-id="424ca-116">You need a code editor.</span></span> <span data-ttu-id="424ca-117">La plupart de cette documentation et des images font référence à l’utilisation [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="424ca-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="424ca-118">Toutefois, n’hésitez pas à utiliser l’éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="424ca-118">However, feel free to use whatever text editor you prefer.</span></span>

* <span data-ttu-id="424ca-119">Yeoman et Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="424ca-119">Yeoman and Gulp CLI</span></span>

   <span data-ttu-id="424ca-120">Pour échafauder des projets à l’aide du générateur, vous devez installer l’outil Yeoman et le gestionnaire des tâches gulp CLI.</span><span class="sxs-lookup"><span data-stu-id="424ca-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

   <span data-ttu-id="424ca-121">Ouvrez une invite de commandes et tapez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="424ca-121">Open up a command prompt and type the following:</span></span>

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a><span data-ttu-id="424ca-122">Installer le générateur</span><span class="sxs-lookup"><span data-stu-id="424ca-122">Install the generator</span></span>

<span data-ttu-id="424ca-123">Installez le Teams générateur Yeoman avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="424ca-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm init yo teams
```

<span data-ttu-id="424ca-124">Installez la version d’aperçu du générateur avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="424ca-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a><span data-ttu-id="424ca-125">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="424ca-125">Generate your project</span></span>

<span data-ttu-id="424ca-126">Cette section vous présente les étapes à suivre pour générer votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-126">This section walks you through the steps to generate your project.</span></span>

<span data-ttu-id="424ca-127">**Pour générer votre projet**</span><span class="sxs-lookup"><span data-stu-id="424ca-127">**To generate your project**</span></span>

1. <span data-ttu-id="424ca-128">Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-128">Open a command prompt and create a new directory where you want to create your project.</span></span>
1. <span data-ttu-id="424ca-129">Go to the directory, and run the command `yo teams` .</span><span class="sxs-lookup"><span data-stu-id="424ca-129">Go to the directory, and run the command `yo teams`.</span></span> <span data-ttu-id="424ca-130">Le générateur démarre.</span><span class="sxs-lookup"><span data-stu-id="424ca-130">The generator starts.</span></span>
1. <span data-ttu-id="424ca-131">Répondez aux questions posées par le générateur :</span><span class="sxs-lookup"><span data-stu-id="424ca-131">Respond to the set of questions prompted by the generator:</span></span>

   ![équipes yo](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="424ca-133">Entrez un nom pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-133">Enter a name for your project.</span></span> <span data-ttu-id="424ca-134">Vous pouvez la laisser telle qu’elle est en appuyant sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="424ca-134">You can leave it as is by pressing Enter.</span></span>
   1. <span data-ttu-id="424ca-135">Entrez un chemin d’accès pour le nouveau répertoire si vous souhaitez créer un répertoire.</span><span class="sxs-lookup"><span data-stu-id="424ca-135">Enter a path for the new directory if you want to create a new directory.</span></span> <span data-ttu-id="424ca-136">Comme vous êtes déjà dans le répertoire de votre recherche, appuyez simplement sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="424ca-136">As you are already in the directory you want, just press Enter.</span></span>
   1. <span data-ttu-id="424ca-137">Entrez le titre de votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-137">Enter the title of your project.</span></span> <span data-ttu-id="424ca-138">Ce titre sera utilisé dans le manifeste et la description de votre application.</span><span class="sxs-lookup"><span data-stu-id="424ca-138">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="424ca-139">Entrez un nom de société qui sera également utilisé dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="424ca-139">Enter a company name which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="424ca-140">Entrez la version du manifeste que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="424ca-140">Enter the version of the manifest you want to use.</span></span> <span data-ttu-id="424ca-141">Pour ce didacticiel, `v1.5` sélectionnez, qui est le schéma général disponible actuel.</span><span class="sxs-lookup"><span data-stu-id="424ca-141">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="424ca-142">Sélectionnez les éléments que vous souhaitez ajouter à votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-142">Select the items you want to add to your project.</span></span> <span data-ttu-id="424ca-143">Vous pouvez sélectionner un seul ou n’importe quelle combinaison d’éléments.</span><span class="sxs-lookup"><span data-stu-id="424ca-143">You can select a single one or any combination of items.</span></span> <span data-ttu-id="424ca-144">Pour ce didacticiel, sélectionnez *simplement un onglet*:</span><span class="sxs-lookup"><span data-stu-id="424ca-144">For this tutorials, just select *a Tab*:</span></span>

    ![sélection d’élément](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="424ca-146">Répondez à l’ensemble suivant de questions de suivi qui s’affichent en fonction des éléments que vous avez sélectionnés à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="424ca-146">Respond to the next set of follow-up questions that appear based on the items you selected in Step 2.</span></span>
1. <span data-ttu-id="424ca-147">Entrez une URL pour l’emplacement où vous hébergez votre solution.</span><span class="sxs-lookup"><span data-stu-id="424ca-147">Enter a URL for the location where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="424ca-148">L’URL peut être n’importe quelle URL, mais par défaut, le générateur suggère une URL de site web Azure.</span><span class="sxs-lookup"><span data-stu-id="424ca-148">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="424ca-149">Confirmez si vous souhaitez inclure des tests unitaires pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="424ca-149">Confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="424ca-150">La réponse par défaut est **Oui**.</span><span class="sxs-lookup"><span data-stu-id="424ca-150">The default response is **Yes**.</span></span> <span data-ttu-id="424ca-151">Si vous choisissez d’inclure le test unitaire, le projet généré aura une infrastructure de test unitaire et des tests unitaires par défaut pour les différents éléments en cours de structure.</span><span class="sxs-lookup"><span data-stu-id="424ca-151">If you opt to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="424ca-152">Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.</span><span class="sxs-lookup"><span data-stu-id="424ca-152">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="424ca-153">Le générateur comporte un grand nombre de fonctionnalités avancées intégrées que vous pouvez choisir d’utiliser ou de refuser.</span><span class="sxs-lookup"><span data-stu-id="424ca-153">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="424ca-154">Pour faciliter la signature, vous serez également invité à utiliser Azure Application Informations pour la signature.</span><span class="sxs-lookup"><span data-stu-id="424ca-154">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="424ca-155">Si vous **sélectionnez Oui,** vous devez fournir une clé d’Informations application Azure.</span><span class="sxs-lookup"><span data-stu-id="424ca-155">If you select **Yes**, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="424ca-156">Pour ce didacticiel, désinsévez l’utilisation d’Application Informations.</span><span class="sxs-lookup"><span data-stu-id="424ca-156">For this tutorial opt-out of using Application Insights.</span></span>

   <span data-ttu-id="424ca-157">L’ensemble de questions suivant sera basé sur les éléments précédemment sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="424ca-157">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="424ca-158">Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez être en mesure d’utiliser cette application en tant que SharePoint Web Part Online.</span><span class="sxs-lookup"><span data-stu-id="424ca-158">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="424ca-159">Une fois que vous avez fourni le nom, le générateur génère le projet et installe toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="424ca-159">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="424ca-160">Cela prendra une minute ou deux.</span><span class="sxs-lookup"><span data-stu-id="424ca-160">This will take a minute or two.</span></span>

## <a name="add-code-to-your-tab"></a><span data-ttu-id="424ca-161">Ajouter du code à votre onglet</span><span class="sxs-lookup"><span data-stu-id="424ca-161">Add code to your tab</span></span>

<span data-ttu-id="424ca-162">Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code favori.</span><span class="sxs-lookup"><span data-stu-id="424ca-162">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="424ca-163">Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé.</span><span class="sxs-lookup"><span data-stu-id="424ca-163">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="424ca-164">Pour plus d’informations, [voir Project structure.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)</span><span class="sxs-lookup"><span data-stu-id="424ca-164">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="424ca-165">Votre onglet se trouve dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier.</span><span class="sxs-lookup"><span data-stu-id="424ca-165">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="424ca-166">Il s’agit de la classe React TypeScript pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="424ca-166">This is the TypeScript React-based class for your tab.</span></span> 

1. <span data-ttu-id="424ca-167">Recherchez la méthode et ajoutez une ligne de code à l’intérieur du contrôle afin `render()` `<PanelBody>` qu’elle ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="424ca-167">Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. <span data-ttu-id="424ca-168">Enregistrez le fichier et revenir à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="424ca-168">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="424ca-169">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="424ca-169">Build your app</span></span>

<span data-ttu-id="424ca-170">Vous pouvez maintenant créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-170">You can now build your project.</span></span> <span data-ttu-id="424ca-171">Cette procédure s’est effectuée en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="424ca-171">This is done in two steps.</span></span>

1. <span data-ttu-id="424ca-172">Créez le Teams manifeste de l’application pour l’application que vous avez téléchargée dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="424ca-172">Create the Teams App manifest file for the app that you uploaded into Microsoft Teams.</span></span> <span data-ttu-id="424ca-173">Cette tâche est effectuée par la tâche Gulp `gulp manifest` .</span><span class="sxs-lookup"><span data-stu-id="424ca-173">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="424ca-174">Cela valide le manifeste et crée un fichier zip dans `./package` le répertoire.</span><span class="sxs-lookup"><span data-stu-id="424ca-174">This will validate the manifest and create a zip file in the `./package` directory.</span></span>
1. <span data-ttu-id="424ca-175">Exécutez `gulp build` la commande pour créer la solution.</span><span class="sxs-lookup"><span data-stu-id="424ca-175">Run the `gulp build` command to build the solution.</span></span> <span data-ttu-id="424ca-176">Cela transpile votre solution dans le `./dist` dossier.</span><span class="sxs-lookup"><span data-stu-id="424ca-176">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="424ca-177">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="424ca-177">Run your app</span></span>

<span data-ttu-id="424ca-178">Pour exécuter votre application, utilisez la `gulp serve` commande.</span><span class="sxs-lookup"><span data-stu-id="424ca-178">To run your app, use the `gulp serve` command.</span></span> <span data-ttu-id="424ca-179">Cela permet de créer et de démarrer un serveur web local pour tester votre application.</span><span class="sxs-lookup"><span data-stu-id="424ca-179">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="424ca-180">La commande reconstruira également l’application chaque fois que vous enregistrez un fichier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="424ca-180">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="424ca-181">Vous devez maintenant vous assurer que votre `http://localhost:3007/myFirstAppTab/` onglet est rendu.</span><span class="sxs-lookup"><span data-stu-id="424ca-181">You should now be go to `http://localhost:3007/myFirstAppTab/` and ensure that your tab is rendering.</span></span> <span data-ttu-id="424ca-182">Toutefois, il n’est pas Microsoft Teams pour le moment.</span><span class="sxs-lookup"><span data-stu-id="424ca-182">However, it is not in Microsoft Teams yet.</span></span> 

<span data-ttu-id="424ca-183">**Pour restituer votre onglet dans Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="424ca-183">**To render your tab in Microsoft Teams**</span></span>

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="424ca-185">Exécuter votre application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="424ca-185">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="424ca-186">Microsoft Teams ne vous permet pas d’héberger votre application sur localhost, vous devez donc la publier sur une URL publique ou utiliser un proxy tel que ngrok.</span><span class="sxs-lookup"><span data-stu-id="424ca-186">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span> <span data-ttu-id="424ca-187">La bonne nouvelle est que le projet échafaudé dispose de ce pré-projet intégré.</span><span class="sxs-lookup"><span data-stu-id="424ca-187">Good news is that the scaffolded project has this built-in.</span></span> 

<span data-ttu-id="424ca-188">**Pour exécuter votre application dans Teams**</span><span class="sxs-lookup"><span data-stu-id="424ca-188">**To run your app in Teams**</span></span>

1. <span data-ttu-id="424ca-189">`gulp ngrok-serve`S’exécute dans Terminal.</span><span class="sxs-lookup"><span data-stu-id="424ca-189">Run `gulp ngrok-serve` in Terminal.</span></span> <span data-ttu-id="424ca-190">Lorsque vous exécutez le service ngrok, il est démarré en arrière-plan, avec une entrée DNS unique et publique, et il inséra également le manifeste avec cette URL unique, puis il fera exactement la même chose que `gulp ngrok-serve` `gulp serve` .</span><span class="sxs-lookup"><span data-stu-id="424ca-190">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>
1. <span data-ttu-id="424ca-191">Créez une équipe Microsoft Teams de recherche.</span><span class="sxs-lookup"><span data-stu-id="424ca-191">Create a new Microsoft Teams team.</span></span>
1. <span data-ttu-id="424ca-192">Sélectionnez le nom de l’équipe > Teams Paramètres > applications.</span><span class="sxs-lookup"><span data-stu-id="424ca-192">Select the Team name > Teams Settings > Apps.</span></span>
1. <span data-ttu-id="424ca-193">Dans le coin inférieur droit, **sélectionnez Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="424ca-193">From the lower right corner, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="424ca-194">Go to the `package` folder under your project folder.</span><span class="sxs-lookup"><span data-stu-id="424ca-194">Go to the `package` folder under your project folder.</span></span> 
1. <span data-ttu-id="424ca-195">Sélectionnez le fichier zip dans ce dossier et sélectionnez Ouvrir.</span><span class="sxs-lookup"><span data-stu-id="424ca-195">Select the zip file in that folder and select open.</span></span> 
   <span data-ttu-id="424ca-196">Votre application est désormais rechargée de Microsoft Teams :</span><span class="sxs-lookup"><span data-stu-id="424ca-196">Your App is now sideloaded into Microsoft Teams:</span></span>

   ![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)
1. <span data-ttu-id="424ca-198">Revenir au canal **Général** et choisir **+** d’ajouter un nouvel onglet. Vous devez voir votre onglet dans la liste des onglets : ![ configurer l’onglet](~/assets/yeoman-images/teams-first-app-5.png)</span><span class="sxs-lookup"><span data-stu-id="424ca-198">Go back to the **General** channel and select **+** to add a new Tab. You should see your tab in the list of tabs: ![configure tab](~/assets/yeoman-images/teams-first-app-5.png)</span></span>
1. <span data-ttu-id="424ca-199">Sélectionnez votre onglet et suivez les instructions pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="424ca-199">Select your tab and follow the instructions to add it.</span></span> <span data-ttu-id="424ca-200">Notez que vous avez une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source.</span><span class="sxs-lookup"><span data-stu-id="424ca-200">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="424ca-201">Sélectionnez *Enregistrer* pour ajouter votre onglet au canal.</span><span class="sxs-lookup"><span data-stu-id="424ca-201">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="424ca-202">Votre onglet est maintenant chargé à l’intérieur Microsoft Teams !</span><span class="sxs-lookup"><span data-stu-id="424ca-202">Your tab is now loaded inside Microsoft Teams!</span></span>

   ![exécution de l’onglet dans teams](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a><span data-ttu-id="424ca-204">Mise à niveau Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="424ca-204">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="424ca-205">Vous pouvez également mettre à niveau votre version Microsoft Teams actuelle vers la dernière version à l’aide Microsoft Teams générateur Yeoman.</span><span class="sxs-lookup"><span data-stu-id="424ca-205">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="424ca-206">**Pour mettre à niveau Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="424ca-206">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="424ca-207">Obtenez la version actuelle de Teams avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="424ca-207">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="424ca-208">Utilisez la commande suivante pour sélectionner et mettre à jour votre générateur :</span><span class="sxs-lookup"><span data-stu-id="424ca-208">Use the following command to select and update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="424ca-209">Utilisez les touches de direction pour sélectionner **Mettre à jour vos générateurs**:</span><span class="sxs-lookup"><span data-stu-id="424ca-209">Use the  arrow keys to select **Update your Generators**:</span></span>

   ![image de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="424ca-211">Sélectionnez le générateur de votre choix dans la liste des générateurs :</span><span class="sxs-lookup"><span data-stu-id="424ca-211">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="424ca-212">Utilisez la barre d’espace pour sélectionner ou effacer une version Teams sélectionnée dans les options disponibles.</span><span class="sxs-lookup"><span data-stu-id="424ca-212">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![image de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="424ca-214">L’installation de la Teams prend quelques secondes à quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="424ca-214">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="424ca-215">Une fois l’installation terminée, utilisez la commande suivante pour vérifier la version installée :</span><span class="sxs-lookup"><span data-stu-id="424ca-215">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
 <span data-ttu-id="424ca-216">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="424ca-216">Congrats!</span></span> <span data-ttu-id="424ca-217">Vous avez créé et déployé votre première Microsoft Teams application.</span><span class="sxs-lookup"><span data-stu-id="424ca-217">You built and deployed your first Microsoft Teams app.</span></span> <span data-ttu-id="424ca-218">Vous avez également mis à niveau Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="424ca-218">You also upgraded Microsoft Teams.</span></span>

 ## <a name="see-also"></a><span data-ttu-id="424ca-219">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="424ca-219">See also</span></span>

* [<span data-ttu-id="424ca-220">Présentation des didacticiels</span><span class="sxs-lookup"><span data-stu-id="424ca-220">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="424ca-221">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="424ca-221">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)