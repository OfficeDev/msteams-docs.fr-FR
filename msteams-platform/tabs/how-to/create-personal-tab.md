---
title: Créer un onglet personnel
author: laujan
description: Guide de démarrage rapide sur la création d’un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 47ed3027f936366964871733e78c7a43851ffb99
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179845"
---
# <a name="create-a-personal-tab"></a><span data-ttu-id="ede60-103">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="ede60-103">Create a personal tab</span></span>

## <a name="create-a-custom-personal-tab"></a><span data-ttu-id="ede60-104">Créer un onglet personnel personnalisé</span><span class="sxs-lookup"><span data-stu-id="ede60-104">Create a custom personal tab</span></span>

<span data-ttu-id="ede60-105">Vous pouvez créer un onglet personnel à l'Node.js Yeoman Generator, ASP.NET Core ou ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="ede60-105">You can create a personal tab using Node.js and the Yeoman Generator, ASP.NET Core, or ASP.NET Core MVC.</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="ede60-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ede60-106">Node.js</span></span>](#tab/nodejs)

### <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator"></a><span data-ttu-id="ede60-107">Créer un onglet personnel personnalisé à l’aide Node.js et du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="ede60-107">Create a custom personal tab using Node.js and the Yeoman Generator</span></span>

> [!NOTE]
> <span data-ttu-id="ede60-108">Cet article suit les étapes décrites dans la build de votre premier Wiki [Microsoft Teams’application,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) qui se trouve dans le référentiel GitHub Microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="ede60-108">This article follows the steps outlined in the [build your first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="ede60-109">Vous pouvez créer un onglet personnel personnalisé à [l’aide Teams générateur Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="ede60-109">You can create a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="ede60-110">L’application est également téléchargée vers Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-110">The application is also uploaded to Teams.</span></span>

### <a name="prerequisites-for-teams-apps"></a><span data-ttu-id="ede60-111">Conditions préalables pour Teams applications</span><span class="sxs-lookup"><span data-stu-id="ede60-111">Prerequisites for Teams apps</span></span>

<span data-ttu-id="ede60-112">Vous devez connaître les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="ede60-112">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="ede60-113">Vous devez avoir un client Office 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="ede60-113">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="ede60-114">Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="ede60-114">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ede60-115">Si vous n’avez pas de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme Office 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="ede60-115">If you do not have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="ede60-116">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="ede60-116">The subscription remains active as long as you are using it for ongoing development.</span></span> <span data-ttu-id="ede60-117">Bienvenue [dans le programme Office 365 développeur.](/office/developer-program/microsoft-365-developer-program)</span><span class="sxs-lookup"><span data-stu-id="ede60-117">See [welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="ede60-118">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="ede60-118">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ede60-119">N’importe quel éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="ede60-119">Any text editor or IDE.</span></span> <span data-ttu-id="ede60-120">Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="ede60-120">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="ede60-121">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ede60-121">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="ede60-122">Utilisez la dernière version de LTS.</span><span class="sxs-lookup"><span data-stu-id="ede60-122">Use the latest LTS version.</span></span> <span data-ttu-id="ede60-123">Le nœud Gestionnaire de package (npm) est installé dans votre système avec l’installation de Node.js.</span><span class="sxs-lookup"><span data-stu-id="ede60-123">The Node Package Manager (npm) is installed in your system with the installation of Node.js.</span></span>

- <span data-ttu-id="ede60-124">Une fois que vous avez installé Node.js, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant les commandes suivantes dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="ede60-124">After you have successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by entering the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="ede60-125">Installez le générateur Microsoft Teams Apps en entrant les commandes suivantes dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="ede60-125">Install the Microsoft Teams Apps generator by entering the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a><span data-ttu-id="ede60-126">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="ede60-126">Generate your project</span></span>

<span data-ttu-id="ede60-127">**Pour générer votre projet**</span><span class="sxs-lookup"><span data-stu-id="ede60-127">**To generate your project**</span></span>

1. <span data-ttu-id="ede60-128">À l’invite de commandes, créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-128">At a command prompt, create a new directory for your tab project.</span></span>

1. <span data-ttu-id="ede60-129">Pour démarrer le générateur, allez dans votre nouveau répertoire et entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-129">To start the generator, go to your new directory and enter the following command:</span></span>

    ```bash
    yo teams
    ```

1. <span data-ttu-id="ede60-130">Ensuite, fournissez une série de valeurs utilisées dans le fichiermanifest.js **application** :</span><span class="sxs-lookup"><span data-stu-id="ede60-130">Next, provide a series of values that are used in your application's **manifest.json** file:</span></span>

    ![Capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="ede60-132">**Quel est le nom de votre solution ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-132">**What is your solution name?**</span></span>

    <span data-ttu-id="ede60-133">Il s’agit du nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="ede60-133">This is your project name.</span></span> <span data-ttu-id="ede60-134">Vous pouvez accepter le nom suggéré en sélectionnant la **touche** Entrée.</span><span class="sxs-lookup"><span data-stu-id="ede60-134">You can accept the suggested name by selecting the **Enter** key.</span></span>

    <span data-ttu-id="ede60-135">**Où souhaitez-vous placer les fichiers ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-135">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="ede60-136">Vous êtes actuellement dans votre répertoire de projet.</span><span class="sxs-lookup"><span data-stu-id="ede60-136">You are currently in your project directory.</span></span> <span data-ttu-id="ede60-137">Sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="ede60-137">Select **Enter**.</span></span>

    <span data-ttu-id="ede60-138">**Titre de votre Microsoft Teams d’application ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-138">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="ede60-139">Il s’agit du nom de votre package d’application et sera utilisé dans le manifeste et la description de l’application.</span><span class="sxs-lookup"><span data-stu-id="ede60-139">This is your app package name and will be used in the app manifest and description.</span></span> <span data-ttu-id="ede60-140">Entrez un titre ou **sélectionnez Entrée** pour accepter le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="ede60-140">Enter a title or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="ede60-141">**Votre nom (d’entreprise) ? (32 caractères maximum)**</span><span class="sxs-lookup"><span data-stu-id="ede60-141">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="ede60-142">Le nom de votre société sera utilisé dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="ede60-142">Your company name will be used in the app manifest.</span></span> <span data-ttu-id="ede60-143">Entrez un nom de société ou **sélectionnez Entrée** pour accepter le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="ede60-143">Enter a company name or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="ede60-144">**Quelle version de manifeste souhaitez-vous utiliser ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-144">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="ede60-145">Sélectionnez le schéma par défaut.</span><span class="sxs-lookup"><span data-stu-id="ede60-145">Select the default schema.</span></span>

    <span data-ttu-id="ede60-146">**La échafaudage rapide ? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="ede60-146">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="ede60-147">La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ede60-147">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="ede60-148">**Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**</span><span class="sxs-lookup"><span data-stu-id="ede60-148">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="ede60-149">Ce champ n’est pas obligatoire et ne doit être utilisé que si vous faites déjà partie de [Microsoft Partner Network](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ede60-149">This field is not required and should only be used if you are already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="ede60-150">**Que voulez-vous ajouter à votre projet ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-150">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="ede60-151">Sélectionnez **( &ast; ) un onglet**.</span><span class="sxs-lookup"><span data-stu-id="ede60-151">Select **( &ast; ) A Tab**.</span></span>

    <span data-ttu-id="ede60-152">**L’URL où vous allez héberger cette solution ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-152">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="ede60-153">Par défaut, le générateur suggère une URL de sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="ede60-153">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="ede60-154">Vous testez uniquement votre application localement, par conséquent, une URL valide n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ede60-154">You are only testing your app locally, therefore, a valid URL is not necessary.</span></span>

    <span data-ttu-id="ede60-155">**Voulez-vous afficher un indicateur de chargement lors du chargement de votre application/onglet ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-155">**Would you like show a loading indicator when your app/tab loads?**</span></span>

    <span data-ttu-id="ede60-156">Choisissez **de ne** pas inclure d’indicateur de chargement lors du chargement de votre application ou de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-156">Choose **not** to include a loading indicator when your app or tab loads.</span></span> <span data-ttu-id="ede60-157">La valeur par défaut est non, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="ede60-157">The default is no, enter **n**.</span></span>

    <span data-ttu-id="ede60-158">**Voulez-vous que les applications personnelles soient restituées sans barre d’en-tête d’onglet ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-158">**Would you like personal apps to be rendered without a tab header-bar?**</span></span>

    <span data-ttu-id="ede60-159">Choisissez **de** ne pas inclure d’applications personnelles à restituer sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-159">Choose **not** to include personal apps to be rendered without a tab header-bar.</span></span> <span data-ttu-id="ede60-160">La valeur par défaut est non, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="ede60-160">Default is no, enter **n**.</span></span>

    <span data-ttu-id="ede60-161">**Souhaitez-vous inclure l’infrastructure test et les tests initiaux ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="ede60-161">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="ede60-162">Choisissez **de ne** pas inclure d’infrastructure de test pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="ede60-162">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="ede60-163">La valeur par défaut est oui, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="ede60-163">The default is yes, enter **n**.</span></span>

    <span data-ttu-id="ede60-164">**Voulez-vous utiliser Azure Applications Informations pour la télémétrie ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="ede60-164">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="ede60-165">Choisissez **de ne** pas inclure Azure Application [Informations](/azure/azure-monitor/app/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="ede60-165">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="ede60-166">La valeur par défaut est non ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="ede60-166">The default is no; enter **n**.</span></span>

    <span data-ttu-id="ede60-167">**Nom de l’onglet par défaut (16 caractères maximum) ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-167">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="ede60-168">Nommez votre onglet. Ce nom d’onglet est utilisé dans l’ensemble de votre projet en tant que composant de chemin d’accès de fichier ou d’URL.</span><span class="sxs-lookup"><span data-stu-id="ede60-168">Name your tab. This tab name is used throughout your project as a file or URL path component.</span></span>

    <span data-ttu-id="ede60-169">**Quel type d’onglet voulez-vous créer ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-169">**What kind of Tab would you like to create?**</span></span>

    <span data-ttu-id="ede60-170">Utilisez les touches de direction pour sélectionner **Personnel (statique).**</span><span class="sxs-lookup"><span data-stu-id="ede60-170">Use the arrow keys to select **Personal (static)**.</span></span>

    <span data-ttu-id="ede60-171">**Avez-vous besoin d’une prise en charge de l’authentification unique Azure AD pour l’onglet ?**</span><span class="sxs-lookup"><span data-stu-id="ede60-171">**Do you require Azure AD Single-Sign-On support for the tab?**</span></span>

    <span data-ttu-id="ede60-172">Choisissez **de** ne pas inclure la prise en charge de l' sign-on unique Azure AD pour l’onglet. La valeur par défaut est oui, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="ede60-172">Choose **not** to include Azure AD Single-Sign-On support for the tab. The default is yes, enter **n**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ede60-173">The path component **yourDefaultTabNameTab** is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span><span class="sxs-lookup"><span data-stu-id="ede60-173">The path component **yourDefaultTabNameTab** is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
    >
    > <span data-ttu-id="ede60-174">Par exemple : DefaultTabName: **MyTab**  >  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="ede60-174">For example: DefaultTabName: **MyTab** > **/MyTabTab/**</span></span>

### <a name="add-a-personal-tab"></a><span data-ttu-id="ede60-175">Ajouter un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="ede60-175">Add a personal tab</span></span>

<span data-ttu-id="ede60-176">**Pour ajouter un onglet personnel à cette application, créez une page de contenu et mettez à jour les fichiers existants**</span><span class="sxs-lookup"><span data-stu-id="ede60-176">**To add a personal tab to this application, create a content page, and update existing files**</span></span>

1. <span data-ttu-id="ede60-177">Dans votre éditeur de code, créez un fichier HTML, **personal.html** et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-177">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. <span data-ttu-id="ede60-178">Enregistrez **personal.html** dans le dossier **web** de votre application à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-178">Save **personal.html** in your application's **web** folder in the following location:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

1. <span data-ttu-id="ede60-179">Ouvrez **manifest.jsà partir** de l’emplacement suivant dans votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="ede60-179">Open **manifest.json** from the following location in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

1. <span data-ttu-id="ede60-180">Ajoutez ce qui suit au tableau `staticTabs` vide ( ) et `staticTabs":[]` ajoutez l’objet JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-180">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

1. <span data-ttu-id="ede60-181">Mettez à jour le composant de chemin **d’accès contentURL** **yourDefaultTabNameTab** avec votre nom d’onglet réel.</span><span class="sxs-lookup"><span data-stu-id="ede60-181">Update the **contentURL** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

1. <span data-ttu-id="ede60-182">Enregistrez **l'manifest.jsmise à jour dans le** fichier.</span><span class="sxs-lookup"><span data-stu-id="ede60-182">Save the updated **manifest.json** file.</span></span>

1. <span data-ttu-id="ede60-183">Pour fournir votre page de contenu dans un IFrame, ouvrez **Tab.ts** dans votre éditeur de code à partir du chemin d’accès suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-183">To provide your content page in an IFrame, open **Tab.ts** in your code editor from the following path:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. <span data-ttu-id="ede60-184">Ajoutez ce qui suit à la liste descorateurs IFrame :</span><span class="sxs-lookup"><span data-stu-id="ede60-184">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

1. <span data-ttu-id="ede60-185">Enregistrez le fichier **Tab.ts** mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ede60-185">Save the updated **Tab.ts** file.</span></span> <span data-ttu-id="ede60-186">Le code de l’onglet est terminé.</span><span class="sxs-lookup"><span data-stu-id="ede60-186">Your tab code is complete.</span></span>

### <a name="build-and-run-your-application"></a><span data-ttu-id="ede60-187">Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ede60-187">Build and run your application</span></span>

<span data-ttu-id="ede60-188">À l’invite de commandes, ouvrez le répertoire de votre projet pour effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="ede60-188">At a command prompt, open your project directory to complete the next tasks.</span></span>

#### <a name="create-the-app-package"></a><span data-ttu-id="ede60-189">Créer le package d’application</span><span class="sxs-lookup"><span data-stu-id="ede60-189">Create the app package</span></span>

<span data-ttu-id="ede60-190">Vous devez avoir un package d’application pour tester votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-190">You must have an app package to test your tab in Teams.</span></span> <span data-ttu-id="ede60-191">Il s’agit d’un dossier zip qui contient les fichiers obligatoires suivants :</span><span class="sxs-lookup"><span data-stu-id="ede60-191">It is a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="ede60-192">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="ede60-192">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ede60-193">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="ede60-193">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ede60-194">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="ede60-194">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ede60-195">Le package est créé par le biais d’une tâche Gulp qui valide l'manifest.jssur le fichier et génère le dossier zip dans le répertoire **./package.**</span><span class="sxs-lookup"><span data-stu-id="ede60-195">The package is created through a gulp task that validates the manifest.json file and generates the zip folder in the **./package directory**.</span></span> <span data-ttu-id="ede60-196">Dans l’invite de commandes, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-196">In the command prompt, enter the following command:</span></span>

```bash
gulp manifest
```

#### <a name="build-your-application"></a><span data-ttu-id="ede60-197">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="ede60-197">Build your application</span></span>

<span data-ttu-id="ede60-198">La commande de build transpile votre solution dans le **dossier ./dist.**</span><span class="sxs-lookup"><span data-stu-id="ede60-198">The build command transpiles your solution into the **./dist** folder.</span></span> <span data-ttu-id="ede60-199">Entrez la commande suivante dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="ede60-199">Enter the following command in the command prompt:</span></span>

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a><span data-ttu-id="ede60-200">Exécuter votre application dans localhost</span><span class="sxs-lookup"><span data-stu-id="ede60-200">Run your application in localhost</span></span>

1. <span data-ttu-id="ede60-201">Démarrez un serveur web local en entrant ce qui suit dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="ede60-201">Start a local web server by entering the following in the command prompt:</span></span>

    ```bash
    gulp serve
    ```

1. <span data-ttu-id="ede60-202">Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur, remplacez-le par votre nom d’onglet et affichez la page d’accueil de votre application, comme illustré **<yourDefaultAppNameTab>** dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-202">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser, replace **<yourDefaultAppNameTab>** with your tab name, and view your application's home page as shown in the following image:</span></span>

    ![capture d’écran de la page d’accueil](~/assets/images/tab-images/homePage.png)

1. <span data-ttu-id="ede60-204">Pour afficher votre onglet personnel, allez sur `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` .</span><span class="sxs-lookup"><span data-stu-id="ede60-204">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`.</span></span>

    >![Capture d’écran de l’onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

### <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="ede60-206">Établir un tunnel sécurisé vers votre onglet</span><span class="sxs-lookup"><span data-stu-id="ede60-206">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="ede60-207">Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ede60-207">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="ede60-208">Teams n’autorise pas l’hébergement local.</span><span class="sxs-lookup"><span data-stu-id="ede60-208">Teams does not allow local hosting.</span></span> <span data-ttu-id="ede60-209">Vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui expose votre port local à une URL internet.</span><span class="sxs-lookup"><span data-stu-id="ede60-209">You must either publish your tab to a public URL or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="ede60-210">Pour tester votre extension d’onglet, vous pouvez utiliser [ngrok,](https://ngrok.com/docs)qui est intégré à cette application.</span><span class="sxs-lookup"><span data-stu-id="ede60-210">To test your tab extension, you can use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="ede60-211">Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="ede60-211">Ngrok is a reverse proxy software tool that creates a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ede60-212">Les points de terminaison web de votre serveur sont disponibles pendant la session en cours sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ede60-212">Your server's web endpoints are available during the current session on your computer.</span></span> <span data-ttu-id="ede60-213">Lorsque l’ordinateur est arrêté ou en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="ede60-213">When the computer is shut down or goes to sleep, the service is no longer available.</span></span>

<span data-ttu-id="ede60-214">Dans votre invite de commandes, quittez localhost et entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ede60-214">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="ede60-215">Une fois que votre onglet a été téléchargé vers Microsoft Teams via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session tunnel.</span><span class="sxs-lookup"><span data-stu-id="ede60-215">After your tab has been uploaded to Microsoft Teams through **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

### <a name="upload-your-application-to-teams"></a><span data-ttu-id="ede60-216">Télécharger votre application à Teams</span><span class="sxs-lookup"><span data-stu-id="ede60-216">Upload your application to Teams</span></span>

<span data-ttu-id="ede60-217">**Pour télécharger votre application sur Teams**</span><span class="sxs-lookup"><span data-stu-id="ede60-217">**To upload your application to Teams**</span></span>

1. <span data-ttu-id="ede60-218">Go to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-218">Go to Microsoft Teams.</span></span> <span data-ttu-id="ede60-219">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ede60-219">If you use the [web-based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="ede60-220">Dans le coin inférieur gauche, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="ede60-220">From the lower left corner, select **Apps**.</span></span>
1. <span data-ttu-id="ede60-221">Dans le coin inférieur gauche, choisissez **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="ede60-221">From the lower left corner, choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="ede60-222">Accédez au répertoire de votre projet, accédez au dossier **./package,** sélectionnez le dossier zip, puis choisissez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="ede60-222">Go to your project directory, browse to the **./package** folder, select the zip folder, and choose **Open**.</span></span>

    ![Ajout de votre onglet personnel](../../assets/images/tab-images/addingpersonaltab.png)

1. <span data-ttu-id="ede60-224">**Sélectionnez** Ajouter dans la boîte de dialogue de fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="ede60-224">Select **Add** in the pop-up dialog box.</span></span> <span data-ttu-id="ede60-225">Votre onglet est téléchargé vers Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-225">Your tab is uploaded to Teams.</span></span>

    ![Onglet personnel chargé](../../assets/images/tab-images/personaltabuploaded.png)

### <a name="view-your-personal-tab"></a><span data-ttu-id="ede60-227">Afficher votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="ede60-227">View your personal tab</span></span>

<span data-ttu-id="ede60-228">Dans la barre de navigation située à l’extrême gauche de Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF; et choisissez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="ede60-228">In the navigation bar located at the far left in Teams, select the ellipses &#x25CF;&#x25CF;&#x25CF; and choose your app from the list.</span></span>

# <a name="aspnet-core"></a>[<span data-ttu-id="ede60-229">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ede60-229">ASP.NET Core</span></span>](#tab/aspnetcore)

### <a name="create-a-custom-personal-tab-using-aspnet-core"></a><span data-ttu-id="ede60-230">Créer un onglet personnel personnalisé à l’aide ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ede60-230">Create a custom personal tab using ASP.NET Core</span></span>

<span data-ttu-id="ede60-231">Vous pouvez créer un onglet personnel personnalisé à l’aide de C# et ASP.NET Core pages De l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ede60-231">You can create a custom personal tab using C# and ASP.NET Core Razor pages.</span></span> <span data-ttu-id="ede60-232">[App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) est également utilisé pour finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-232">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-personal-tab"></a><span data-ttu-id="ede60-233">Conditions préalables pour l’onglet personnel</span><span class="sxs-lookup"><span data-stu-id="ede60-233">Prerequisites for personal tab</span></span>

<span data-ttu-id="ede60-234">Vous devez connaître les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="ede60-234">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="ede60-235">Vous devez avoir un client Office 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="ede60-235">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="ede60-236">Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="ede60-236">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ede60-237">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="ede60-237">If you do not have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="ede60-238">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="ede60-238">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="ede60-239">Utilisez App Studio pour importer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-239">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="ede60-240">Pour installer App Studio, sélectionnez **Apps** Store App dans le coin inférieur gauche de ![ l’application ](~/assets/images/tab-images/storeApp.png) Teams, puis **recherchez App Studio.**</span><span class="sxs-lookup"><span data-stu-id="ede60-240">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="ede60-241">Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez Ajouter **dans** la boîte de dialogue pop-up pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="ede60-241">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="ede60-242">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="ede60-242">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ede60-243">Version actuelle de l’Visual Studio IDE avec la charge de travail de développement **.NET CORE sur** plusieurs plateformes installée.</span><span class="sxs-lookup"><span data-stu-id="ede60-243">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="ede60-244">Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="ede60-244">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="ede60-245">Outil de proxy inverse [ngrok.](https://ngrok.com)</span><span class="sxs-lookup"><span data-stu-id="ede60-245">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="ede60-246">Utilisez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="ede60-246">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ede60-247">Vous pouvez [télécharger ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="ede60-247">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="ede60-248">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="ede60-248">Get the source code</span></span>

<span data-ttu-id="ede60-249">À l’invite de commandes, créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-249">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="ede60-250">Un projet simple est fourni pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="ede60-250">A simple project is provided to get you started.</span></span> <span data-ttu-id="ede60-251">Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-251">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ede60-252">Vous pouvez également récupérer le code source en téléchargeant le dossier zip et en extrayant les fichiers.</span><span class="sxs-lookup"><span data-stu-id="ede60-252">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="ede60-253">**Pour créer et exécuter le projet d’onglet**</span><span class="sxs-lookup"><span data-stu-id="ede60-253">**To build and run the tab project**</span></span>

1. <span data-ttu-id="ede60-254">Une fois que vous avez obtenir le code source, Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="ede60-254">After you get the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="ede60-255">Go to the tab application directory and open **PersonalTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="ede60-255">Go to the tab application directory and open **PersonalTab.sln**.</span></span>
1. <span data-ttu-id="ede60-256">Pour créer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="ede60-256">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="ede60-257">Dans un navigateur, go to the following URLs to verify the application loaded properly:</span><span class="sxs-lookup"><span data-stu-id="ede60-257">In a browser, go to the following URLs to verify the application loaded properly:</span></span>

    - `http://localhost:44325/`
    - `http://localhost:44325/personal`
    - `http://localhost:44325/privacy`
    - `http://localhost:44325/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="ede60-258">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="ede60-258">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="ede60-259">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ede60-259">Startup.cs</span></span>

<span data-ttu-id="ede60-260">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="ede60-260">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="ede60-261">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="ede60-261">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ede60-262">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire de fichiers statiques est ajouté à la méthode à l’aide du `Configure()` code suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-262">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
  {
      services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a><span data-ttu-id="ede60-263">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="ede60-263">wwwroot folder</span></span>

<span data-ttu-id="ede60-264">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="ede60-264">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="indexcshtml"></a><span data-ttu-id="ede60-265">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="ede60-265">Index.cshtml</span></span>

<span data-ttu-id="ede60-266">ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="ede60-266">ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="ede60-267">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="ede60-267">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="ede60-268">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="ede60-268">AppManifest folder</span></span>

<span data-ttu-id="ede60-269">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="ede60-269">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="ede60-270">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="ede60-270">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ede60-271">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="ede60-271">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ede60-272">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="ede60-272">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ede60-273">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-273">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ede60-274">Microsoft Teams charge le spécifié dans votre manifeste, l’incorpore dans un iframe <et l’restituer `contentUrl` \> dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-274">Microsoft Teams loads the `contentUrl` specified in your manifest, embeds it in an <iframe\>, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="ede60-275">.csproj</span><span class="sxs-lookup"><span data-stu-id="ede60-275">.csproj</span></span>

<span data-ttu-id="ede60-276">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="ede60-276">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ede60-277">À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="ede60-277">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

### <a name="update-your-application-for-teams"></a><span data-ttu-id="ede60-278">Mettre à jour votre application pour Teams</span><span class="sxs-lookup"><span data-stu-id="ede60-278">Update your application for Teams</span></span>

#### <a name="_layoutcshtml"></a><span data-ttu-id="ede60-279">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="ede60-279">_Layout.cshtml</span></span>

<span data-ttu-id="ede60-280">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="ede60-280">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="ede60-281">Voici comment votre onglet et l’application Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="ede60-281">This is how your tab and the Teams app communicate:</span></span>

<span data-ttu-id="ede60-282">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span><span class="sxs-lookup"><span data-stu-id="ede60-282">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

#### <a name="personaltabcshtml"></a><span data-ttu-id="ede60-283">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="ede60-283">PersonalTab.cshtml</span></span>

<span data-ttu-id="ede60-284">Ouvrez **PersonalTab.cshtml** et mettez à jour les `<script>` balises incorporées en appelant `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="ede60-284">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="ede60-285">Veillez à enregistrer votre **PersonalTab.cshtml** mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ede60-285">Ensure you save your updated **PersonalTab.cshtml**.</span></span>

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a><span data-ttu-id="ede60-286">Établir un tunnel sécurisé vers votre onglet pour Teams</span><span class="sxs-lookup"><span data-stu-id="ede60-286">Establish a secure tunnel to your tab for Teams</span></span>

<span data-ttu-id="ede60-287">Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ede60-287">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="ede60-288">Teams n’autorise pas l’hébergement local.</span><span class="sxs-lookup"><span data-stu-id="ede60-288">Teams does not allow local hosting.</span></span> <span data-ttu-id="ede60-289">Vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui expose votre port local à une URL internet.</span><span class="sxs-lookup"><span data-stu-id="ede60-289">You must either publish your tab to a public URL, or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="ede60-290">Pour tester votre onglet, utilisez [ngrok](https://ngrok.com/docs).</span><span class="sxs-lookup"><span data-stu-id="ede60-290">To test your tab, use [ngrok](https://ngrok.com/docs).</span></span> <span data-ttu-id="ede60-291">Les points de terminaison web de votre serveur sont disponibles lorsque ngrok est en cours d’exécution sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ede60-291">Your server's web endpoints are available while ngrok is running on your computer.</span></span> <span data-ttu-id="ede60-292">Dans la version gratuite de ngrok, si vous fermez ngrok, les URL sont différentes lors du prochain démarrage.</span><span class="sxs-lookup"><span data-stu-id="ede60-292">In the free version of ngrok, if you close ngrok, the URLs are different the next time you start it.</span></span>

<span data-ttu-id="ede60-293">**Pour établir un tunnel sécurisé sur votre onglet**</span><span class="sxs-lookup"><span data-stu-id="ede60-293">**To establish a secure tunnel to your tab**</span></span>

1. <span data-ttu-id="ede60-294">À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-294">At a command prompt in the root of your project directory, run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

    <span data-ttu-id="ede60-295">Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application lorsqu’elle est en cours d’exécution sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="ede60-295">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44325.</span></span> <span data-ttu-id="ede60-296">Il ressemble à `https://y8rPrT2b.ngrok.io/` **l’endroit où y8rPrT2b** est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="ede60-296">It resembles `https://y8rPrT2b.ngrok.io/` where **y8rPrT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

    <span data-ttu-id="ede60-297">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.</span><span class="sxs-lookup"><span data-stu-id="ede60-297">Ensure that you keep the command prompt with ngrok running, and make a note of the URL.</span></span>

2. <span data-ttu-id="ede60-298">Vérifiez que **ngrok** s’exécute et fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="ede60-298">Verify that **ngrok** is running and working properly by opening your browser and going to your content page through the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="ede60-299">Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ede60-299">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="ede60-300">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="ede60-300">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ede60-301">Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ede60-301">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ede60-302">Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="ede60-302">If you have to restart the ngrok service, it returns a new URL and you have to update every place that uses that URL.</span></span>

#### <a name="run-your-application"></a><span data-ttu-id="ede60-303">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ede60-303">Run your application</span></span>

<span data-ttu-id="ede60-304">Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage de votre** application.</span><span class="sxs-lookup"><span data-stu-id="ede60-304">In Visual Studio, press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

### <a name="upload-your-tab-with-app-studio-for-teams"></a><span data-ttu-id="ede60-305">Télécharger onglet avec App Studio pour Teams</span><span class="sxs-lookup"><span data-stu-id="ede60-305">Upload your tab with App Studio for Teams</span></span>

> [!NOTE]
> <span data-ttu-id="ede60-306">**App Studio peut** être utilisé pour modifier votre **manifest.jsfichier** et télécharger le package terminé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-306">**App Studio** can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="ede60-307">Vous pouvez également modifier manuellement **manifest.jssur**.</span><span class="sxs-lookup"><span data-stu-id="ede60-307">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="ede60-308">Si vous le faites, veillez à générer à nouveau la solution pour créerTab.zip **fichier** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="ede60-308">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="ede60-309">**Pour télécharger votre onglet avec App Studio**</span><span class="sxs-lookup"><span data-stu-id="ede60-309">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="ede60-310">Go to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-310">Go to Microsoft Teams.</span></span> <span data-ttu-id="ede60-311">Si vous utilisez la [version web,](https://teams.microsoft.com)vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ede60-311">If you use the [web-based version](https://teams.microsoft.com), you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="ede60-312">Go to **App Studio** and select the **Manifest editor** tab.</span><span class="sxs-lookup"><span data-stu-id="ede60-312">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="ede60-313">Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet.  Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="ede60-313">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="ede60-314">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="ede60-314">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="ede60-315">Il est disponible à partir du chemin d’accès suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-315">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="ede60-316">Télécharger **tab.zip** **app Studio.**</span><span class="sxs-lookup"><span data-stu-id="ede60-316">Upload **tab.zip** to **App Studio**.</span></span>

#### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="ede60-317">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="ede60-317">Update your app package with Manifest editor</span></span>

<span data-ttu-id="ede60-318">Après avoir chargé votre package d’application dans App Studio, vous devez le configurer.</span><span class="sxs-lookup"><span data-stu-id="ede60-318">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="ede60-319">Sélectionnez la vignette de votre onglet nouvellement importé dans le volet droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="ede60-319">Select the tile for your newly imported tab in the right pane of the Manifest editor welcome page.</span></span>

<span data-ttu-id="ede60-320">Il existe une liste d’étapes sur le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="ede60-320">There is a list of steps on the left side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="ede60-321">La plupart des informations ont été fournies par votre **manifest.js,** mais vous devez mettre à jour certains champs.</span><span class="sxs-lookup"><span data-stu-id="ede60-321">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

##### <a name="details-app-details"></a><span data-ttu-id="ede60-322">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="ede60-322">Details: App details</span></span>

<span data-ttu-id="ede60-323">Dans la section **Détails de l’application** :</span><span class="sxs-lookup"><span data-stu-id="ede60-323">In the **App details** section:</span></span>

1. <span data-ttu-id="ede60-324">Sous **Identification,** **sélectionnez Générer** pour générer un nouvel ID d’application pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ede60-324">Under **Identification**, select **Generate** to generate a new App ID for your app.</span></span>

1. <span data-ttu-id="ede60-325">Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="ede60-325">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

    ![URL d’application mises à jour](../../assets/images/tab-images/appurls.png)

1. <span data-ttu-id="ede60-327">Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="ede60-327">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

##### <a name="capabilities-tabs"></a><span data-ttu-id="ede60-328">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="ede60-328">Capabilities: Tabs</span></span>

<span data-ttu-id="ede60-329">Dans la section **Onglets** :</span><span class="sxs-lookup"><span data-stu-id="ede60-329">In the **Tabs** section:</span></span>

1. <span data-ttu-id="ede60-330">Sous **Ajouter un onglet personnel,** sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="ede60-330">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="ede60-331">Une boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ede60-331">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="ede60-332">Entrez un nom pour l’onglet personnel dans **Nom**.</span><span class="sxs-lookup"><span data-stu-id="ede60-332">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="ede60-333">Entrez **l’ID d’entité**.</span><span class="sxs-lookup"><span data-stu-id="ede60-333">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="ede60-334">Mettre à **jour l’URL de** contenu avec `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="ede60-334">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="ede60-335">Laissez le **champ URL** du site web vide.</span><span class="sxs-lookup"><span data-stu-id="ede60-335">Leave the **Website URL** field blank.</span></span>

    ![Détails de l’onglet personnel](../../assets/images/tab-images/personaltabdetails.png)

1. <span data-ttu-id="ede60-337">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ede60-337">Select **Save**.</span></span>

##### <a name="finish-domains-and-permissions"></a><span data-ttu-id="ede60-338">Finish: Domains and permissions</span><span class="sxs-lookup"><span data-stu-id="ede60-338">Finish: Domains and permissions</span></span>

<span data-ttu-id="ede60-339">Dans la section **Domaines et autorisations,** les domaines de vos **onglets** doivent contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`</span><span class="sxs-lookup"><span data-stu-id="ede60-339">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

###### <a name="finish-test-and-distribute"></a><span data-ttu-id="ede60-340">Fin : Tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="ede60-340">Finish: Test and distribute</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ede60-341">À droite, dans **Description,** vous voyez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-341">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="ede60-342">&#9888; tableau **« validDomains » ne peut pas contenir de site de tunneling...**</span><span class="sxs-lookup"><span data-stu-id="ede60-342">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
> <span data-ttu-id="ede60-343">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-343">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="ede60-344">Dans la section **Tester et distribuer,** sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="ede60-344">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="ede60-345">Dans la boîte de dialogue qui s’affiche, **sélectionnez** Ajouter et votre onglet s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ede60-345">In the pop-up dialog box, select **Add** and your tab is displayed.</span></span>

    ![Onglet personnel ASPNET chargé](../../assets/images/tab-images/personaltabaspnetuploaded.png)

### <a name="view-your-personal-tab-in-teams"></a><span data-ttu-id="ede60-347">Afficher votre onglet personnel dans Teams</span><span class="sxs-lookup"><span data-stu-id="ede60-347">View your personal tab in Teams</span></span>

1. <span data-ttu-id="ede60-348">Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF;.</span><span class="sxs-lookup"><span data-stu-id="ede60-348">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="ede60-349">Une liste d’applications personnelles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ede60-349">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="ede60-350">Sélectionnez votre onglet dans la liste pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="ede60-350">Select your tab from the list to view it.</span></span>

# <a name="aspnet-core-mvc"></a>[<span data-ttu-id="ede60-351">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="ede60-351">ASP.NET Core MVC</span></span>](#tab/aspnetcoremvc)

### <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="ede60-352">Créer un onglet personnel personnalisé avec ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="ede60-352">Create a custom personal tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="ede60-353">Vous pouvez créer un onglet personnel personnalisé à l’aide C# et ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="ede60-353">You can create a custom personal tab using C# and ASP.NET Core MVC.</span></span> <span data-ttu-id="ede60-354">[App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) est également utilisé pour finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-354">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="ede60-355">Conditions préalables pour l’onglet personnel avec ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="ede60-355">Prerequisites for personal tab with ASP.NET Core MVC</span></span>

- <span data-ttu-id="ede60-356">Vous devez avoir un client Microsoft 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="ede60-356">You must have a Microsoft 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="ede60-357">Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="ede60-357">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ede60-358">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="ede60-358">If you do not have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="ede60-359">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="ede60-359">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="ede60-360">Utilisez App Studio pour importer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-360">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="ede60-361">Pour installer App Studio, sélectionnez **Apps** Store App dans le coin inférieur gauche de ![ l’application ](~/assets/images/tab-images/storeApp.png) Teams, puis **recherchez App Studio.**</span><span class="sxs-lookup"><span data-stu-id="ede60-361">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="ede60-362">Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez Ajouter **dans** la boîte de dialogue pop-up pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="ede60-362">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="ede60-363">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="ede60-363">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ede60-364">Version actuelle de l’Visual Studio IDE avec la charge de travail de développement **.NET CORE sur** plusieurs plateformes installée.</span><span class="sxs-lookup"><span data-stu-id="ede60-364">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="ede60-365">Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="ede60-365">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="ede60-366">Outil de proxy inverse [ngrok.](https://ngrok.com)</span><span class="sxs-lookup"><span data-stu-id="ede60-366">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="ede60-367">Utilisez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="ede60-367">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ede60-368">Vous pouvez [télécharger ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="ede60-368">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="ede60-369">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="ede60-369">Get the source code</span></span>

<span data-ttu-id="ede60-370">À l’invite de commandes, créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-370">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="ede60-371">Un projet simple est fourni pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="ede60-371">A simple project is provided to get you started.</span></span> <span data-ttu-id="ede60-372">Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-372">Clone the sample repository into your new directory using the following command:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ede60-373">Vous pouvez également récupérer le code source en téléchargeant le dossier zip et en extrayant les fichiers.</span><span class="sxs-lookup"><span data-stu-id="ede60-373">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="ede60-374">**Pour créer et exécuter le projet d’onglet**</span><span class="sxs-lookup"><span data-stu-id="ede60-374">**To build and run the tab project**</span></span>

1. <span data-ttu-id="ede60-375">Une fois que vous avez le code source, Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="ede60-375">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="ede60-376">Go to the tab application directory and open **PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="ede60-376">Go to the tab application directory and open **PersonalTabMVC.sln**.</span></span>
1. <span data-ttu-id="ede60-377">Pour créer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="ede60-377">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="ede60-378">Dans un navigateur, go to the following URLs to verify that the application loaded properly:</span><span class="sxs-lookup"><span data-stu-id="ede60-378">In a browser, go to the following URLs to verify that the application loaded properly:</span></span>

    * `http://localhost:44335`
    * `http://localhost:44335/privacy`
    * `http://localhost:44335/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="ede60-379">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="ede60-379">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="ede60-380">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ede60-380">Startup.cs</span></span>

<span data-ttu-id="ede60-381">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="ede60-381">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="ede60-382">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="ede60-382">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ede60-383">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire de fichiers statiques est ajouté à la méthode à l’aide du `Configure()` code suivant :</span><span class="sxs-lookup"><span data-stu-id="ede60-383">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

``` csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a><span data-ttu-id="ede60-384">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="ede60-384">wwwroot folder</span></span>

<span data-ttu-id="ede60-385">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="ede60-385">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="ede60-386">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="ede60-386">AppManifest folder</span></span>

<span data-ttu-id="ede60-387">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="ede60-387">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="ede60-388">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="ede60-388">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="ede60-389">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="ede60-389">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="ede60-390">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="ede60-390">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ede60-391">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="ede60-391">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ede60-392">Microsoft Teams charge le spécifié dans votre manifeste, l’incorpore dans un IFrame et l’restituer `contentUrl` dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ede60-392">Microsoft Teams loads the `contentUrl` specified in your manifest, embeds it in an IFrame, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="ede60-393">.csproj</span><span class="sxs-lookup"><span data-stu-id="ede60-393">.csproj</span></span>

<span data-ttu-id="ede60-394">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="ede60-394">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ede60-395">À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="ede60-395">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

``` xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

#### <a name="models"></a><span data-ttu-id="ede60-396">Modèles</span><span class="sxs-lookup"><span data-stu-id="ede60-396">Models</span></span>

<span data-ttu-id="ede60-397">**PersonalTab.cs** présente un objet Message et des méthodes qui sont appelées à partir de **PersonalTabController** lorsqu’un utilisateur sélectionne un bouton dans **l’affichage PersonalTab.**</span><span class="sxs-lookup"><span data-stu-id="ede60-397">**PersonalTab.cs** presents a Message object and methods that are called from **PersonalTabController** when a user selects a button in the **PersonalTab** View.</span></span>

#### <a name="views"></a><span data-ttu-id="ede60-398">Affichages</span><span class="sxs-lookup"><span data-stu-id="ede60-398">Views</span></span>

<span data-ttu-id="ede60-399">Voici les différentes vues dans ASP.NET Core MVC :</span><span class="sxs-lookup"><span data-stu-id="ede60-399">These are the different views in ASP.NET Core MVC:</span></span>

* <span data-ttu-id="ede60-400">Accueil : ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="ede60-400">Home: ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="ede60-401">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="ede60-401">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

* <span data-ttu-id="ede60-402">Partagé : le contrôle de **_Layout.cshtml contient** la structure de page globale de l’application et les éléments visuels partagés.</span><span class="sxs-lookup"><span data-stu-id="ede60-402">Shared: The partial view markup **_Layout.cshtml** contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="ede60-403">Il fait également référence à la Teams bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="ede60-403">It also references the Teams Library.</span></span>

#### <a name="controllers"></a><span data-ttu-id="ede60-404">Contrôleurs</span><span class="sxs-lookup"><span data-stu-id="ede60-404">Controllers</span></span>

<span data-ttu-id="ede60-405">Les contrôleurs utilisent la propriété pour transférer dynamiquement des `ViewBag` valeurs vers les affichages.</span><span class="sxs-lookup"><span data-stu-id="ede60-405">The controllers use the `ViewBag` property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

<span data-ttu-id="ede60-406">**Pour exécuter ngrok et vérifier la page de contenu**</span><span class="sxs-lookup"><span data-stu-id="ede60-406">**To run ngrok and verify the content page**</span></span>

1. <span data-ttu-id="ede60-407">À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ede60-407">At a command prompt in the root of your project directory, run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

    <span data-ttu-id="ede60-408">Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application lorsqu’elle est en cours d’exécution sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="ede60-408">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44325.</span></span> <span data-ttu-id="ede60-409">Il ressemble à `https://y8rPrT2b.ngrok.io/` **l’endroit où y8rPrT2b** est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="ede60-409">It resembles `https://y8rPrT2b.ngrok.io/` where **y8rPrT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

    <span data-ttu-id="ede60-410">Veillez à ce que l’invite de commandes avec ngrok soit en cours d’exécution et notez l’URL.</span><span class="sxs-lookup"><span data-stu-id="ede60-410">Ensure you keep the command prompt with ngrok running, and make a note of the URL.</span></span>

1. <span data-ttu-id="ede60-411">Vérifiez que **ngrok** s’exécute et fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="ede60-411">Verify that **ngrok** is running and working properly by opening your browser and going to your content page through the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="ede60-412">Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ede60-412">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="ede60-413">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="ede60-413">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ede60-414">Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ede60-414">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ede60-415">Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="ede60-415">If you have to restart the ngrok service it returns a new URL and you have to update every place that uses that URL.</span></span>

#### <a name="run-your-application"></a><span data-ttu-id="ede60-416">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ede60-416">Run your application</span></span>

<span data-ttu-id="ede60-417">Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage de votre** application.</span><span class="sxs-lookup"><span data-stu-id="ede60-417">In Visual Studio, press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

---

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="ede60-418">Réordesser les onglets personnels statiques</span><span class="sxs-lookup"><span data-stu-id="ede60-418">Reorder static personal tabs</span></span>

<span data-ttu-id="ede60-419">À partir de la version de manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle.</span><span class="sxs-lookup"><span data-stu-id="ede60-419">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="ede60-420">En particulier, un développeur peut déplacer l’onglet de conversation du **bot,** qui est toujours en première position par défaut, n’importe où dans l’en-tête de l’onglet de l’application personnelle.</span><span class="sxs-lookup"><span data-stu-id="ede60-420">In particular, a developer can move the **bot chat** tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="ede60-421">Deux mots clés `entityId` d’onglet réservés sont déclarés, **conversations** et **à propos de**.</span><span class="sxs-lookup"><span data-stu-id="ede60-421">Two reserved tab `entityId` keywords are declared, **conversations** and **about**.</span></span>

<span data-ttu-id="ede60-422">Si vous créez un bot avec une **étendue** personnelle, il apparaît par défaut dans le premier onglet d’une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="ede60-422">If you create a bot with a **personal** scope, it appears in the first tab position in a personal app by default.</span></span> <span data-ttu-id="ede60-423">Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, **conversations**.</span><span class="sxs-lookup"><span data-stu-id="ede60-423">If you want to move it to another position, you must add a static tab object to your manifest with the reserved keyword, **conversations**.</span></span> <span data-ttu-id="ede60-424">**L’onglet de conversation** s’affiche sur le web ou le bureau en fonction de l’endroit où vous ajoutez l’onglet de **conversation** dans le `staticTabs` tableau.</span><span class="sxs-lookup"><span data-stu-id="ede60-424">The **conversation** tab appears on web or desktop depending on where you add the **conversation** tab in the `staticTabs` array.</span></span>

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="see-also"></a><span data-ttu-id="ede60-425">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ede60-425">See also</span></span>

* [<span data-ttu-id="ede60-426">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="ede60-426">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="ede60-427">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="ede60-427">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="ede60-428">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="ede60-428">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="ede60-429">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="ede60-429">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)

## <a name="next-step"></a><span data-ttu-id="ede60-430">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="ede60-430">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ede60-431">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="ede60-431">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
