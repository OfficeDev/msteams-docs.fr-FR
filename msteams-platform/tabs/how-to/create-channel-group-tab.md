---
title: Créer un onglet de canal ou de groupe
author: laujan
description: Guide de démarrage rapide sur la création d’un onglet de canal et de groupe avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: fedaf3ec639917110e16c666734fa3eedbcda18e
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179975"
---
# <a name="create-a-channel-or-group-tab"></a><span data-ttu-id="b2e6f-103">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="b2e6f-103">Create a channel or group tab</span></span>

## <a name="create-a-custom-channel-or-group-tab"></a><span data-ttu-id="b2e6f-104">Créer un onglet de canal ou de groupe personnalisé</span><span class="sxs-lookup"><span data-stu-id="b2e6f-104">Create a custom channel or group tab</span></span>

<span data-ttu-id="b2e6f-105">Vous pouvez créer un onglet de canal ou de groupe en utilisant Node.js et le générateur Yeoman, ASP.NETCore ou ASP.NETCore MVC.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-105">You can create a channel or group tab using Node.js and the Yeoman Generator, ASP.NETCore, or ASP.NETCore MVC.</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="b2e6f-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="b2e6f-106">Node.js</span></span>](#tab/nodejs)

### <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator"></a><span data-ttu-id="b2e6f-107">Créer un canal et un onglet de groupe personnalisés à l’aide Node.js et du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="b2e6f-107">Create a custom channel and group tab using Node.js and the Yeoman Generator</span></span>

> [!NOTE]
> <span data-ttu-id="b2e6f-108">Cet article suit les étapes décrites dans la build your [first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-108">This article follows the steps outlined in the [build Your first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="b2e6f-109">Vous pouvez créer un onglet de canal ou de groupe personnalisé à [l’aide Teams générateur Yeoman.](https://github.com/OfficeDev/generator-teams/)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-109">You can create a custom channel or group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

### <a name="prerequisites-for-apps"></a><span data-ttu-id="b2e6f-110">Conditions préalables pour les applications</span><span class="sxs-lookup"><span data-stu-id="b2e6f-110">Prerequisites for apps</span></span>

<span data-ttu-id="b2e6f-111">Vous devez connaître les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-111">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="b2e6f-112">Vous devez avoir un client Office 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-112">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="b2e6f-113">Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-113">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b2e6f-114">Si vous n’avez pas de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme Office 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-114">If you do not currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="b2e6f-115">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-115">The subscription remains active as long as you are using it for ongoing development.</span></span> <span data-ttu-id="b2e6f-116">Bienvenue [dans le programme Office 365 développeur.](/office/developer-program/microsoft-365-developer-program)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-116">See [welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="b2e6f-117">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-117">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="b2e6f-118">N’importe quel éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-118">Any text editor or IDE.</span></span> <span data-ttu-id="b2e6f-119">Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-119">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="b2e6f-120">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-120">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="b2e6f-121">Utilisez la dernière version de LTS.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-121">Use the latest LTS version.</span></span> <span data-ttu-id="b2e6f-122">Le nœud Gestionnaire de package (npm) s’installe dans votre système avec l’installation de Node.js.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-122">The Node Package Manager (npm) installs in your system with the installation of Node.js.</span></span>

- <span data-ttu-id="b2e6f-123">Une fois que vous avez installé Node.js, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant les commandes suivantes dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-123">After you have successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by entering the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="b2e6f-124">Installez le générateur Microsoft Teams Apps en entrant les commandes suivantes dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-124">Install the Microsoft Teams Apps generator by entering the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a><span data-ttu-id="b2e6f-125">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="b2e6f-125">Generate your project</span></span>

<span data-ttu-id="b2e6f-126">**Pour générer votre projet**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-126">**To generate your project**</span></span>

1. <span data-ttu-id="b2e6f-127">À l’invite de commandes, créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-127">At a command prompt, create a new directory for your tab project.</span></span>

1. <span data-ttu-id="b2e6f-128">Pour démarrer le générateur, allez dans votre nouveau répertoire et tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-128">To start the generator, go to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

1. <span data-ttu-id="b2e6f-129">Ensuite, fournissez une série de valeurs utilisées dans le fichiermanifest.js **application** :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-129">Next, provide a series of values that are used in your application's **manifest.json** file:</span></span>

    ![Capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="b2e6f-131">**Quel est le nom de votre solution ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-131">**What is your solution name?**</span></span>

    <span data-ttu-id="b2e6f-132">Il s’agit du nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-132">This is your project name.</span></span> <span data-ttu-id="b2e6f-133">Vous pouvez accepter le nom suggéré en sélectionnant la **touche** Entrée.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-133">You can accept the suggested name by selecting the **Enter** key.</span></span>

    <span data-ttu-id="b2e6f-134">**Où souhaitez-vous placer les fichiers ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-134">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="b2e6f-135">Vous êtes actuellement dans votre répertoire de projet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-135">You are currently in your project directory.</span></span> <span data-ttu-id="b2e6f-136">Sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-136">Select **Enter**.</span></span>

    <span data-ttu-id="b2e6f-137">**Titre de votre Microsoft Teams d’application ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-137">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="b2e6f-138">Il s’agit du nom de votre package d’application et sera utilisé dans le manifeste et la description de l’application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-138">This is your app package name and will be used in the app manifest and description.</span></span> <span data-ttu-id="b2e6f-139">Entrez un titre ou **sélectionnez Entrée** pour accepter le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-139">Enter a title or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="b2e6f-140">**Votre nom (d’entreprise) ? (32 caractères maximum)**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-140">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="b2e6f-141">Le nom de votre société sera utilisé dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-141">Your company name will be used in the app manifest.</span></span> <span data-ttu-id="b2e6f-142">Entrez un nom de société ou **sélectionnez Entrée** pour accepter le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-142">Enter a company name or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="b2e6f-143">**Quelle version de manifeste souhaitez-vous utiliser ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-143">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="b2e6f-144">Sélectionnez le schéma par défaut.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-144">Select the default schema.</span></span>

    <span data-ttu-id="b2e6f-145">**La échafaudage rapide ? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-145">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="b2e6f-146">La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-146">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="b2e6f-147">**Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-147">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="b2e6f-148">Ce champ n’est pas obligatoire et ne doit être utilisé que si vous faites déjà partie de [Microsoft Partner Network](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-148">This field is not required and should only be used if you are already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="b2e6f-149">**Que voulez-vous ajouter à votre projet ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-149">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="b2e6f-150">Sélectionnez **( &ast; ) un onglet**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-150">Select **( &ast; ) A Tab**.</span></span>

    <span data-ttu-id="b2e6f-151">**L’URL où vous allez héberger cette solution ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-151">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="b2e6f-152">Par défaut, le générateur suggère une URL de sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-152">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="b2e6f-153">Vous testez uniquement votre application localement, par conséquent, une URL valide n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-153">You are only testing your app locally, therefore, a valid URL is not necessary.</span></span>

    <span data-ttu-id="b2e6f-154">**Voulez-vous afficher un indicateur de chargement lors du chargement de votre application/onglet ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-154">**Would you like show a loading indicator when your app/tab loads?**</span></span>

    <span data-ttu-id="b2e6f-155">Choisissez **de ne** pas inclure d’indicateur de chargement lors du chargement de votre application ou de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-155">Choose **not** to include a loading indicator when your app or tab loads.</span></span> <span data-ttu-id="b2e6f-156">La valeur par défaut est non, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-156">The default is no, enter **n**.</span></span>

   <span data-ttu-id="b2e6f-157">**Voulez-vous que les applications personnelles soient restituées sans barre d’en-tête d’onglet ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-157">**Would you like personal apps to be rendered without a tab header-bar?**</span></span>

    <span data-ttu-id="b2e6f-158">Choisissez **de** ne pas inclure d’applications personnelles à restituer sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-158">Choose **not** to include personal apps to be rendered without a tab header-bar.</span></span> <span data-ttu-id="b2e6f-159">La valeur par défaut est non, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-159">Default is no, enter **n**.</span></span>

    <span data-ttu-id="b2e6f-160">**Souhaitez-vous inclure l’infrastructure test et les tests initiaux ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-160">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="b2e6f-161">Choisissez **de ne** pas inclure d’infrastructure de test pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-161">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="b2e6f-162">La valeur par défaut est Oui ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-162">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="b2e6f-163">**Voulez-vous utiliser Azure Applications Informations pour la télémétrie ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-163">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="b2e6f-164">Choisissez **de ne** pas inclure Azure Application [Informations](/azure/azure-monitor/app/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-164">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="b2e6f-165">La valeur par défaut est non ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-165">The default is no; enter **n**.</span></span>

    <span data-ttu-id="b2e6f-166">**Nom de l’onglet par défaut (16 caractères maximum) ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-166">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="b2e6f-167">Nommez votre onglet. Ce nom d’onglet sera utilisé dans l’ensemble de votre projet en tant que composant de chemin d’accès de fichier ou d’URL.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-167">Name your tab. This tab name will be used throughout your project as a file or URL path component.</span></span>

    <span data-ttu-id="b2e6f-168">**Quel type d’onglet voulez-vous créer ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-168">**What kind of Tab would you like to create?**</span></span>

    <span data-ttu-id="b2e6f-169">Utilisez les touches de direction pour sélectionner **l’onglet Configurable.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-169">Use the arrow keys to select **Configurable** tab.</span></span>

    <span data-ttu-id="b2e6f-170">**Quelles étendues avez-vous l’intention d’utiliser pour votre onglet ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-170">**What scopes do you intend to use for your Tab?**</span></span>

    <span data-ttu-id="b2e6f-171">Vous pouvez sélectionner une équipe ou une conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-171">You can select a team or a group chat.</span></span>

    <span data-ttu-id="b2e6f-172">**Avez-vous besoin d’une prise en charge de l’authentification unique Azure AD pour l’onglet ?**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-172">**Do you require Azure AD Single-Sign-On support for the tab?**</span></span>

    <span data-ttu-id="b2e6f-173">Choisissez **de** ne pas inclure la prise en charge de l' sign-on unique Azure AD pour l’onglet. La valeur par défaut est oui, entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-173">Choose **not** to include Azure AD Single-Sign-On support for the tab. The default is yes, enter **n**.</span></span>

    <span data-ttu-id="b2e6f-174">**Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-174">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span>

    <span data-ttu-id="b2e6f-175">Entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-175">Enter **n**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b2e6f-176">Le composant de **chemin d’accès yourDefaultTabNameTab**, est la valeur que vous avez entrée dans le générateur pour le nom de l’onglet par défaut **plus** le mot **Tab**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-176">The path component **yourDefaultTabNameTab**, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
    >
    > <span data-ttu-id="b2e6f-177">Par exemple : DefaultTabName: **MyTab**  >  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-177">For example: DefaultTabName: **MyTab** > **/MyTabTab/**</span></span>

1. <span data-ttu-id="b2e6f-178">Dans Visual Studio Code ou n’importe quel éditeur de code, allez dans le répertoire de votre projet et ouvrez le fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-178">In Visual Studio Code or any code editor, go to your project directory and open the following file:</span></span>

    ```bash
    ./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
    ```

1. <span data-ttu-id="b2e6f-179">Recherchez la méthode et ajoutez la balise et le contenu suivants `render()` en haut du code de conteneur `<div>` `<PanelBody>` :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-179">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

    ```html
        <PanelBody>
            <div style={styles.section}>
                Hello World! Yo Teams rocks!
            </div>
        </PanelBody>
    ```

1. <span data-ttu-id="b2e6f-180">Veillez à enregistrer le fichier mis à jour.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-180">Make sure to save the updated file.</span></span>

### <a name="build-and-run-your-application"></a><span data-ttu-id="b2e6f-181">Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="b2e6f-181">Build and run your application</span></span>

<span data-ttu-id="b2e6f-182">À l’invite de commandes, ouvrez le répertoire de votre projet pour effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-182">At a command prompt, open your project directory to complete the next tasks.</span></span>

#### <a name="create-the-app-package"></a><span data-ttu-id="b2e6f-183">Créer le package d’application</span><span class="sxs-lookup"><span data-stu-id="b2e6f-183">Create the app package</span></span>

<span data-ttu-id="b2e6f-184">Vous devez avoir un package d’application pour tester votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-184">You must have an app package to test your tab in Teams.</span></span> <span data-ttu-id="b2e6f-185">Il s’agit d’un dossier zip qui contient les fichiers obligatoires suivants :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-185">It is a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="b2e6f-186">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-186">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="b2e6f-187">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-187">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="b2e6f-188">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-188">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="b2e6f-189">Le package est créé par le biais d’une tâche Gulp qui valide l'manifest.jssur le fichier et génère le dossier zip dans le répertoire **./package.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-189">The package is created through a gulp task that validates the manifest.json file and generates the zip folder in the **./package directory**.</span></span> <span data-ttu-id="b2e6f-190">Dans l’invite de commandes, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-190">In the command prompt, enter the following command:</span></span>

```bash
gulp manifest
```

#### <a name="build-your-application"></a><span data-ttu-id="b2e6f-191">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="b2e6f-191">Build your application</span></span>

<span data-ttu-id="b2e6f-192">La commande de build transpile votre solution dans le **dossier ./dist.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-192">The build command transpiles your solution into the **./dist** folder.</span></span> <span data-ttu-id="b2e6f-193">Entrez la commande suivante dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-193">Enter the following command in the command prompt:</span></span>

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a><span data-ttu-id="b2e6f-194">Exécuter votre application dans localhost</span><span class="sxs-lookup"><span data-stu-id="b2e6f-194">Run your application in localhost</span></span>

1. <span data-ttu-id="b2e6f-195">Démarrez un serveur web local en entrant ce qui suit dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-195">Start a local web server by entering the following in the command prompt:</span></span>

    ```bash
    gulp serve
    ```

1. <span data-ttu-id="b2e6f-196">Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur, remplacez-le par votre nom d’onglet et affichez la page d’accueil de votre application, comme illustré **<yourDefaultAppNameTab>** dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-196">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser, replace **<yourDefaultAppNameTab>** with your tab name, and view your application's home page as shown in the following image:</span></span>

    ![capture d’écran de la page d’accueil](~/assets/images/tab-images/homePage.png)

1. <span data-ttu-id="b2e6f-198">Pour afficher la page de configuration de votre onglet, allez sur `https://localhost:3007/<yourDefaultAppNameTab>/config.html` .</span><span class="sxs-lookup"><span data-stu-id="b2e6f-198">To view your tab configuration page, go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="b2e6f-199">Les exemples suivants sont présentés :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-199">The following is shown:</span></span>

    ![Capture d’écran de la page de configuration](~/assets/images/tab-images/configurationPage.png)

### <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="b2e6f-201">Établir un tunnel sécurisé vers votre onglet</span><span class="sxs-lookup"><span data-stu-id="b2e6f-201">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="b2e6f-202">Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-202">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="b2e6f-203">Teams n’autorise pas l’hébergement local.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-203">Teams does not allow local hosting.</span></span> <span data-ttu-id="b2e6f-204">Vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui expose votre port local à une URL internet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-204">You must either publish your tab to a public URL or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="b2e6f-205">Pour tester votre extension d’onglet, [utilisez ngrok,](https://ngrok.com/docs)qui est intégré à cette application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-205">To test your tab extension, use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="b2e6f-206">Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-206">Ngrok is a reverse proxy software tool that creates a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="b2e6f-207">Les points de terminaison web de votre serveur sont disponibles pendant la session en cours sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-207">Your server's web endpoints are available during the current session on your computer.</span></span> <span data-ttu-id="b2e6f-208">Lorsque l’ordinateur est arrêté ou mis en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-208">When the computer is shut down or goes to sleep the service is no longer available.</span></span>

<span data-ttu-id="b2e6f-209">Dans votre invite de commandes, quittez localhost et entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-209">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="b2e6f-210">Une fois que votre onglet a été téléchargé sur Microsoft Teams et enregistré, vous pouvez l’afficher dans la galerie d’onglets, l’ajouter à la barre d’onglets et interagir avec lui jusqu’à la fin de votre session tunnel ngrok.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-210">After your tab has been uploaded to Microsoft Teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="b2e6f-211">Si vous redémarrez votre session ngrok, vous devez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-211">If you restart your ngrok session, you must update your app with the new URL.</span></span>

### <a name="upload-your-application-to-teams"></a><span data-ttu-id="b2e6f-212">Télécharger votre application à Teams</span><span class="sxs-lookup"><span data-stu-id="b2e6f-212">Upload your application to Teams</span></span>

<span data-ttu-id="b2e6f-213">**Pour télécharger votre application sur Teams**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-213">**To upload your application to Teams**</span></span>

1. <span data-ttu-id="b2e6f-214">Go to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-214">Go to Microsoft Teams.</span></span> <span data-ttu-id="b2e6f-215">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-215">If you use the [web-based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="b2e6f-216">Dans vos équipes dans le volet gauche, sélectionnez les &#x25CF;&#x25CF;&#x25CF; en de côté de l’équipe que vous utilisez pour tester votre onglet et choisissez Gérer **l’équipe.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-216">From your teams on the left pane, select the ellipses &#x25CF;&#x25CF;&#x25CF; next to the team that you are using to test your tab and choose **Manage team**.</span></span>
1. <span data-ttu-id="b2e6f-217">Dans le volet principal, sélectionnez **Applications** dans la barre d’onglets et choisissez **Télécharger une** application personnalisée située dans le coin inférieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-217">In the main pane, select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right corner of the page.</span></span>
1. <span data-ttu-id="b2e6f-218">Accédez au répertoire de votre projet, accédez au dossier **./package,** sélectionnez le dossier zip du package d’application, puis choisissez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-218">Go your project directory, browse to the **./package** folder, select the app package zip folder, and choose **Open**.</span></span>

    ![Onglet Canal ajouté](../../assets/images/tab-images/channeltabadded.png)

1. <span data-ttu-id="b2e6f-220">**Sélectionnez** Ajouter dans la boîte de dialogue de fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-220">Select **Add** in the pop-up dialog box.</span></span> <span data-ttu-id="b2e6f-221">Votre onglet se charge dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-221">Your tab uploads into Teams.</span></span>
1. <span data-ttu-id="b2e6f-222">Revenir à votre équipe, choisissez le canal dans lequel vous souhaitez afficher l’onglet, sélectionnez ➕ dans la barre d’onglets et choisissez votre onglet dans la galerie.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-222">Return to your team, choose the channel where you want to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
1. <span data-ttu-id="b2e6f-223">Suivez les instructions pour ajouter un onglet. Il existe une boîte de dialogue de configuration personnalisée pour votre canal ou onglet de groupe.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-223">Follow the directions for adding a tab. There is a custom configuration dialog box for your channel or group tab.</span></span>
1. <span data-ttu-id="b2e6f-224">Sélectionnez **Enregistrer** et votre onglet est ajouté à la barre d’onglets du canal.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-224">Select **Save** and your tab is added to the channel's tab bar.</span></span>

    ![Onglet Canal chargé](../../assets/images/tab-images/channeltabuploaded.png)

# <a name="aspnet-core"></a>[<span data-ttu-id="b2e6f-226">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b2e6f-226">ASP.NET Core</span></span>](#tab/aspnetcore)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a><span data-ttu-id="b2e6f-227">Créer un onglet de canal ou de groupe personnalisé avec ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b2e6f-227">Create a custom channel or group tab with ASP.NET Core</span></span>

<span data-ttu-id="b2e6f-228">Vous pouvez créer un onglet de canal ou de groupe personnalisé à l’C# et ASP.Net page Principale.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-228">You can create a custom channel or group tab using C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="b2e6f-229">[App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) est également utilisé pour finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-229">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-teams-apps"></a><span data-ttu-id="b2e6f-230">Conditions préalables pour Teams applications</span><span class="sxs-lookup"><span data-stu-id="b2e6f-230">Prerequisites for Teams apps</span></span>

<span data-ttu-id="b2e6f-231">Vous devez connaître les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-231">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="b2e6f-232">Vous devez avoir un client Office 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-232">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="b2e6f-233">Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-233">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b2e6f-234">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-234">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="b2e6f-235">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-235">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="b2e6f-236">Utilisez App Studio pour importer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-236">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="b2e6f-237">Pour installer App Studio, sélectionnez **Apps** Store App dans le coin inférieur gauche de ![ l’application ](~/assets/images/tab-images/storeApp.png) Teams, puis **recherchez App Studio.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-237">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="b2e6f-238">Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez Ajouter **dans** la boîte de dialogue pop-up pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-238">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="b2e6f-239">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-239">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="b2e6f-240">Version actuelle de l’Visual Studio IDE avec la charge de travail de développement **.NET CORE sur** plusieurs plateformes installée.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-240">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="b2e6f-241">Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-241">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="b2e6f-242">Outil de proxy inverse [ngrok.](https://ngrok.com)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-242">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="b2e6f-243">Utilisez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-243">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="b2e6f-244">Vous pouvez [télécharger ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-244">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="b2e6f-245">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="b2e6f-245">Get the source code</span></span>

<span data-ttu-id="b2e6f-246">À l’invite de commandes, créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-246">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="b2e6f-247">Un projet simple est fourni pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-247">A simple project is provided to get you started.</span></span> <span data-ttu-id="b2e6f-248">Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-248">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="b2e6f-249">Vous pouvez également récupérer le code source en téléchargeant le dossier zip et en extrayant les fichiers.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-249">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="b2e6f-250">**Pour créer et exécuter le projet d’onglet**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-250">**To build and run the tab project**</span></span>

1. <span data-ttu-id="b2e6f-251">Une fois que vous avez le code source, Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-251">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="b2e6f-252">Go to the tab application directory and open **ChannelGroupTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-252">Go to the tab application directory and open **ChannelGroupTab.sln**.</span></span>
1. <span data-ttu-id="b2e6f-253">Pour créer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-253">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="b2e6f-254">Dans un navigateur, go to the following URLs and verify the application loaded properly:</span><span class="sxs-lookup"><span data-stu-id="b2e6f-254">In a browser, go to the following URLs and verify the application loaded properly:</span></span>

    - `http://localhost:44355`
    - `http://localhost:44355/privacy`
    - `http://localhost:44355/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="b2e6f-255">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="b2e6f-255">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="b2e6f-256">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="b2e6f-256">Startup.cs</span></span>

<span data-ttu-id="b2e6f-257">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-257">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="b2e6f-258">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-258">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="b2e6f-259">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire de fichiers statiques est ajouté à la méthode à l’aide du `Configure()` code suivant :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-259">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

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

#### <a name="wwwroot-folder"></a><span data-ttu-id="b2e6f-260">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="b2e6f-260">wwwroot folder</span></span>

<span data-ttu-id="b2e6f-261">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-261">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="indexcshtml"></a><span data-ttu-id="b2e6f-262">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="b2e6f-262">Index.cshtml</span></span>

<span data-ttu-id="b2e6f-263">ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-263">ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="b2e6f-264">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-264">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

#### <a name="tabcs"></a><span data-ttu-id="b2e6f-265">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="b2e6f-265">Tab.cs</span></span>

<span data-ttu-id="b2e6f-266">Ce C# contient une méthode qui est appelée à partir de **Tab.cshtml** lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-266">This C# file contains a method that is called from **Tab.cshtml** during configuration.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="b2e6f-267">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="b2e6f-267">AppManifest folder</span></span>

<span data-ttu-id="b2e6f-268">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-268">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="b2e6f-269">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-269">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="b2e6f-270">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-270">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="b2e6f-271">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-271">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="b2e6f-272">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-272">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="b2e6f-273">Lorsqu’un utilisateur choisit d’ajouter ou de mettre à jour votre onglet, Microsoft Teams charge le contenu spécifié dans votre manifeste, l’incorpore dans un IFrame et l’restituer dans `configurationUrl` votre onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-273">When a user chooses to add or update your tab, Microsoft Teams loads the `configurationUrl` specified in your manifest, embeds it in an IFrame, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="b2e6f-274">.csproj</span><span class="sxs-lookup"><span data-stu-id="b2e6f-274">.csproj</span></span>

<span data-ttu-id="b2e6f-275">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-275">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="b2e6f-276">À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-276">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a><span data-ttu-id="b2e6f-277">Établir un tunnel sécurisé vers votre onglet pour Teams</span><span class="sxs-lookup"><span data-stu-id="b2e6f-277">Establish a secure tunnel to your tab for Teams</span></span>

<span data-ttu-id="b2e6f-278">Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-278">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="b2e6f-279">Teams n’autorise pas l’hébergement local.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-279">Teams does not allow local hosting.</span></span> <span data-ttu-id="b2e6f-280">Vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui expose votre port local à une URL internet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-280">You must either publish your tab to a public URL, or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="b2e6f-281">Pour tester votre onglet, utilisez [ngrok](https://ngrok.com/docs).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-281">To test your tab, use [ngrok](https://ngrok.com/docs).</span></span> <span data-ttu-id="b2e6f-282">Les points de terminaison web de votre serveur sont disponibles lorsque ngrok est en cours d’exécution sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-282">Your server's web endpoints are available while ngrok is running on your computer.</span></span> <span data-ttu-id="b2e6f-283">Dans la version gratuite de ngrok, si vous fermez ngrok, les URL sont différentes lors du prochain démarrage.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-283">In the free version of ngrok, if you close ngrok, the URLs are different the next time you start it.</span></span>

- <span data-ttu-id="b2e6f-284">À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-284">At a command prompt in the root of your project directory, run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="b2e6f-285">Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application lorsqu’elle est en cours d’exécution sur le port 44355.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-285">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44355.</span></span> <span data-ttu-id="b2e6f-286">Il doit ressembler `https://y8rCgT2b.ngrok.io/` à **l’endroit où y8rCgT2b** est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-286">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="b2e6f-287">Veillez à maintenir l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-287">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="b2e6f-288">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="b2e6f-288">Update your application</span></span>

<span data-ttu-id="b2e6f-289">Dans **Tab.cshtml,** l’application présente à l’utilisateur deux boutons d’option pour afficher l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-289">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="b2e6f-290">Le choix du  **bouton Sélectionner** gris ou Rouge déclenche `saveGray()` ou, respectivement, définit et active le bouton Enregistrer `saveRed()` sur la page de `settings.setValidityState(true)` configuration. </span><span class="sxs-lookup"><span data-stu-id="b2e6f-290">Choosing the **Select Gray** or **Select Red** button triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="b2e6f-291">Ce code vous permet Teams que vous avez rempli les conditions requises pour la configuration et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-291">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="b2e6f-292">Les paramètres sont `settings.setSettings` définies.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-292">The parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="b2e6f-293">Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été résolue avec succès.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-293">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

#### <a name="_layoutcshtml"></a><span data-ttu-id="b2e6f-294">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="b2e6f-294">_Layout.cshtml</span></span>

<span data-ttu-id="b2e6f-295">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-295">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="b2e6f-296">Voici comment votre onglet et le client Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-296">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="b2e6f-297">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span><span class="sxs-lookup"><span data-stu-id="b2e6f-297">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

> [!IMPORTANT]
> <span data-ttu-id="b2e6f-298">Ne copiez pas et collez les URL de cette page, car elles ne représentent pas `<script src="...">` la dernière version.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-298">Do not copy and paste the `<script src="...">` URLs from this page, as they do not represent the latest version.</span></span> <span data-ttu-id="b2e6f-299">Pour obtenir la dernière version du SDK, toujours Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-299">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

#### <a name="tabcshtml"></a><span data-ttu-id="b2e6f-300">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="b2e6f-300">Tab.cshtml</span></span>

<span data-ttu-id="b2e6f-301">**Pour mettre à jour Tab.cshtml**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-301">**To update Tab.cshtml**</span></span>

1. <span data-ttu-id="b2e6f-302">Ouvrez **Tab.cshtml** dans Visual Studio et mettez à jour l’incorporé `<script>` .</span><span class="sxs-lookup"><span data-stu-id="b2e6f-302">Open **Tab.cshtml** in Visual Studio and update the embedded `<script>`.</span></span>

1. <span data-ttu-id="b2e6f-303">En haut du script, appelez `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="b2e6f-303">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="b2e6f-304">Mettez à `websiteUrl` jour les `contentUrl` valeurs de chaque fonction avec l’URL HTTPS ngrok sur votre onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-304">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="b2e6f-305">Votre code doit maintenant inclure les données suivantes avec **y8rCgT2b** remplacé par votre URL ngrok :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-305">Your code should now include the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. <span data-ttu-id="b2e6f-306">Enregistrez le **tab.cshtml mis à jour.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-306">Save the updated **Tab.cshtml**.</span></span>

### <a name="build-and-run-your-application-for-teams"></a><span data-ttu-id="b2e6f-307">Créer et exécuter votre application pour Teams</span><span class="sxs-lookup"><span data-stu-id="b2e6f-307">Build and run your application for Teams</span></span>

<span data-ttu-id="b2e6f-308">**Pour créer et exécuter votre application**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-308">**To build and run your application**</span></span>

1. <span data-ttu-id="b2e6f-309">Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-309">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="b2e6f-310">Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-310">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="b2e6f-311">Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-311">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="b2e6f-312">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-312">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="b2e6f-313">Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-313">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="b2e6f-314">Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-314">If you have to restart the ngrok service it returns a new URL and you have to update your application with the new URL.</span></span>

### <a name="upload-your-tab-for-teams"></a><span data-ttu-id="b2e6f-315">Télécharger votre onglet pour Teams</span><span class="sxs-lookup"><span data-stu-id="b2e6f-315">Upload your tab for Teams</span></span>

> [!NOTE]
> <span data-ttu-id="b2e6f-316">App Studio peut être utilisé pour modifier votre **manifest.jsfichier** et télécharger le package terminé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-316">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="b2e6f-317">Vous pouvez également modifier manuellement **l'manifest.jssur le** fichier.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-317">You can also manually edit the **manifest.json** file.</span></span> <span data-ttu-id="b2e6f-318">Si vous le faites, veillez à générer à nouveau la solution pour créertab.zip **fichier** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-318">If you do, ensure that you build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="b2e6f-319">**Pour télécharger votre onglet avec App Studio**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-319">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="b2e6f-320">Go to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-320">Go to Microsoft Teams.</span></span> <span data-ttu-id="b2e6f-321">Si vous utilisez la [version web,](https://teams.microsoft.com)vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-321">If you use the [web-based version](https://teams.microsoft.com), you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="b2e6f-322">Go to **App Studio** and select the **Manifest editor** tab.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-322">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="b2e6f-323">Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet.  Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-323">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="b2e6f-324">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-324">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="b2e6f-325">Il est disponible à partir du chemin d’accès suivant :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-325">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="b2e6f-326">Télécharger **tab.zip** app Studio.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-326">Upload **tab.zip** to App Studio.</span></span>

#### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="b2e6f-327">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="b2e6f-327">Update your app package with Manifest editor</span></span>

<span data-ttu-id="b2e6f-328">Après avoir chargé votre package d’application dans App Studio, vous devez le configurer.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-328">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="b2e6f-329">Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-329">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="b2e6f-330">Il existe une liste d’étapes sur le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-330">There is a list of steps on the left side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="b2e6f-331">La plupart des informations ont été fournies par votre **manifest.js,** mais vous devez mettre à jour certains champs.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-331">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

##### <a name="details-app-details"></a><span data-ttu-id="b2e6f-332">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="b2e6f-332">Details: App details</span></span>

<span data-ttu-id="b2e6f-333">Dans la section **Détails de l’application** :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-333">In the **App details** section:</span></span>

1. <span data-ttu-id="b2e6f-334">Sous **Identification,** **sélectionnez Générer** pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-334">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="b2e6f-335">Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-335">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="b2e6f-336">Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-336">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

##### <a name="capabilities-tabs"></a><span data-ttu-id="b2e6f-337">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="b2e6f-337">Capabilities: Tabs</span></span>

<span data-ttu-id="b2e6f-338">Dans la section **Onglets** :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-338">In the **Tabs** section:</span></span>

1. <span data-ttu-id="b2e6f-339">Sous **l’onglet Équipe,** **sélectionnez Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-339">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="b2e6f-340">Dans la fenêtre **pop-up de** l’onglet Équipe, mettez à jour l’URL **de configuration** sur `https://<yourngrokurl>/tab` .</span><span class="sxs-lookup"><span data-stu-id="b2e6f-340">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="b2e6f-341">Assurez-vous **que les case**  à cocher Mettre à jour la configuration ? , **Équipe** et Groupe sont sélectionnées et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-341">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

##### <a name="finish-domains-and-permissions"></a><span data-ttu-id="b2e6f-342">Finish: Domains and permissions</span><span class="sxs-lookup"><span data-stu-id="b2e6f-342">Finish: Domains and permissions</span></span>

<span data-ttu-id="b2e6f-343">Dans la section **Domaines et autorisations,** les domaines de vos **onglets** doivent contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`</span><span class="sxs-lookup"><span data-stu-id="b2e6f-343">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="b2e6f-344">Fin : Tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="b2e6f-344">Finish: Test and distribute</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2e6f-345">À droite, dans **Description,** vous voyez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-345">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="b2e6f-346">&#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »</span><span class="sxs-lookup"><span data-stu-id="b2e6f-346">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="b2e6f-347">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-347">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="b2e6f-348">Dans la section **Tester et distribuer,** sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-348">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="b2e6f-349">Dans la boîte de dialogue  de fenêtre instantanée, sélectionnez Ajouter à une équipe ou, dans la zone de la boîte de dialogue, sélectionnez Ajouter **à une conversation.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-349">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="b2e6f-350">Choisissez l’équipe ou la conversation dans laquelle vous souhaitez afficher l’onglet, puis sélectionnez **Configurer un onglet.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-350">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="b2e6f-351">Dans la boîte de dialogue de fenêtre pop-up suivante, sélectionnez **Gris** ou **Rouge,** puis sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-351">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="b2e6f-352">Pour afficher votre onglet, allez à l’équipe ou à la conversation dans laquelle vous avez installé l’onglet, puis sélectionnez-le dans la barre d’onglets.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-352">To view your tab, go to the team or chat where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="b2e6f-353">La page que vous avez choisie lors de la configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-353">The page that you chose during configuration is displayed.</span></span>

    ![Onglet canal ASPNET chargé](../../assets/images/tab-images/channeltabaspnetuploaded.png)

# <a name="aspnet-core-mvc"></a>[<span data-ttu-id="b2e6f-355">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="b2e6f-355">ASP.NET Core MVC</span></span>](#tab/aspnetcoremvc)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="b2e6f-356">Créer un onglet de canal ou de groupe personnalisé avec ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="b2e6f-356">Create a custom channel or group tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="b2e6f-357">Vous pouvez créer un onglet de canal ou de groupe personnalisé à l’C# et ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-357">You can create a custom channel or group tab using C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="b2e6f-358">[App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) est également utilisé pour finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-358">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-custom-channel-or-group-tab"></a><span data-ttu-id="b2e6f-359">Conditions préalables pour un onglet de groupe ou de canal personnalisé</span><span class="sxs-lookup"><span data-stu-id="b2e6f-359">Prerequisites for custom channel or group tab</span></span>

- <span data-ttu-id="b2e6f-360">Vous devez avoir un client Microsoft 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-360">You must have a Microsoft 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="b2e6f-361">Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-361">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b2e6f-362">Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-362">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="b2e6f-363">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-363">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="b2e6f-364">Utilisez App Studio pour importer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-364">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="b2e6f-365">Pour installer App Studio, sélectionnez **Apps** Store App dans le coin inférieur gauche de ![ l’application ](~/assets/images/tab-images/storeApp.png) Teams, puis **recherchez App Studio.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-365">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="b2e6f-366">Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez Ajouter **dans** la boîte de dialogue pop-up pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-366">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="b2e6f-367">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-367">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="b2e6f-368">Version actuelle de l’Visual Studio IDE avec la charge de travail de développement **.NET CORE sur** plusieurs plateformes installée.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-368">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="b2e6f-369">Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-369">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="b2e6f-370">Outil de proxy inverse [ngrok.](https://ngrok.com)</span><span class="sxs-lookup"><span data-stu-id="b2e6f-370">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="b2e6f-371">Utilisez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-371">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="b2e6f-372">Vous pouvez [télécharger ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="b2e6f-372">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="b2e6f-373">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="b2e6f-373">Get the source code</span></span>

<span data-ttu-id="b2e6f-374">À l’invite de commandes, créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-374">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="b2e6f-375">Un projet [d’onglet de groupe](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) de canaux simple est fourni pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-375">A simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) project is provided to get you started.</span></span> <span data-ttu-id="b2e6f-376">Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-376">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="b2e6f-377">Vous pouvez également récupérer le code source en téléchargeant le dossier zip et en extrayant les fichiers.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-377">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="b2e6f-378">**Pour créer et exécuter le projet d’onglet**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-378">**To build and run the tab project**</span></span>

1. <span data-ttu-id="b2e6f-379">Une fois que vous avez le code source, Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-379">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="b2e6f-380">Go to the tab application directory and open **ChannelGroupTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-380">Go to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>
1. <span data-ttu-id="b2e6f-381">Pour créer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-381">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="b2e6f-382">Dans un navigateur, accédez aux URL suivantes et vérifiez que l’application s’est chargée correctement :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-382">In a browser, navigate to the following URLs and verify that the application loaded properly:</span></span>

    - `http://localhost:44360`
    - `http://localhost:44360/privacy`
    - `http://localhost:44360/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="b2e6f-383">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="b2e6f-383">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="b2e6f-384">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="b2e6f-384">Startup.cs</span></span>

<span data-ttu-id="b2e6f-385">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-385">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="b2e6f-386">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-386">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="b2e6f-387">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire de fichiers statiques est ajouté à la méthode à l’aide du `Configure()` code suivant :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-387">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

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

#### <a name="wwwroot-folder"></a><span data-ttu-id="b2e6f-388">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="b2e6f-388">wwwroot folder</span></span>

<span data-ttu-id="b2e6f-389">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-389">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="b2e6f-390">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="b2e6f-390">AppManifest folder</span></span>

<span data-ttu-id="b2e6f-391">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-391">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="b2e6f-392">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-392">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="b2e6f-393">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-393">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="b2e6f-394">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-394">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="b2e6f-395">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-395">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

#### <a name="csproj"></a><span data-ttu-id="b2e6f-396">.csproj</span><span class="sxs-lookup"><span data-stu-id="b2e6f-396">.csproj</span></span>

<span data-ttu-id="b2e6f-397">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="b2e6f-397">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="b2e6f-398">À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-398">At the end of the file you see the following code that creates and updates your zip folder when the application builds:</span></span>

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

#### <a name="models"></a><span data-ttu-id="b2e6f-399">Modèles</span><span class="sxs-lookup"><span data-stu-id="b2e6f-399">Models</span></span>

<span data-ttu-id="b2e6f-400">**ChannelGroup.cs** présente un objet Message et des méthodes qui seront appelés à partir des contrôleurs lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-400">**ChannelGroup.cs** presents a Message object and methods that will be called from the controllers during configuration.</span></span>

#### <a name="views"></a><span data-ttu-id="b2e6f-401">Affichages</span><span class="sxs-lookup"><span data-stu-id="b2e6f-401">Views</span></span>

<span data-ttu-id="b2e6f-402">Voici les différentes vues dans ASP.NET Core MVC :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-402">These are the different views in ASP.NET Core MVC:</span></span>

* <span data-ttu-id="b2e6f-403">Accueil : ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-403">Home: ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="b2e6f-404">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-404">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

* <span data-ttu-id="b2e6f-405">Partagé : le contrôle de **_Layout.cshtml contient** la structure de page globale de l’application et les éléments visuels partagés.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-405">Shared: The partial view markup **_Layout.cshtml** contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="b2e6f-406">Il référencera également la bibliothèque Teams bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-406">It will also reference the Teams Library.</span></span>

#### <a name="controllers"></a><span data-ttu-id="b2e6f-407">Contrôleurs</span><span class="sxs-lookup"><span data-stu-id="b2e6f-407">Controllers</span></span>

<span data-ttu-id="b2e6f-408">Les contrôleurs utilisent la propriété pour transférer dynamiquement des `ViewBag` valeurs vers les vues.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-408">The controllers use the `ViewBag` property to transfer values dynamically to the views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="b2e6f-409">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2e6f-409">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

* <span data-ttu-id="b2e6f-410">Ngrok écoute les demandes provenant d’Internet et les route vers votre application lorsqu’elle est en cours d’exécution sur le port 44355.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-410">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="b2e6f-411">Il doit ressembler `https://y8rCgT2b.ngrok.io/` à **l’endroit où y8rCgT2b** est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-411">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="b2e6f-412">Veillez à maintenir l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-412">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="b2e6f-413">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="b2e6f-413">Update your application</span></span>

<span data-ttu-id="b2e6f-414">Dans **Tab.cshtml,** l’application présente à l’utilisateur deux boutons d’option pour afficher l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-414">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="b2e6f-415">Le choix du  **bouton Sélectionner** gris ou Rouge, déclenche `saveGray()` ou, respectivement, définit et active le bouton Enregistrer `saveRed()` sur la page de `settings.setValidityState(true)` configuration. </span><span class="sxs-lookup"><span data-stu-id="b2e6f-415">Choosing the **Select Gray** or **Select Red** button, triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="b2e6f-416">Ce code vous permet Teams que vous avez rempli les conditions requises pour la configuration et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-416">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="b2e6f-417">Lors de l’enregistrer, les paramètres `settings.setSettings` sont définies.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-417">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="b2e6f-418">Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été résolue avec succès.</span><span class="sxs-lookup"><span data-stu-id="b2e6f-418">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

---

## <a name="see-also"></a><span data-ttu-id="b2e6f-419">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b2e6f-419">See also</span></span>

* [<span data-ttu-id="b2e6f-420">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="b2e6f-420">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="b2e6f-421">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="b2e6f-421">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="b2e6f-422">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="b2e6f-422">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="b2e6f-423">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="b2e6f-423">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a><span data-ttu-id="b2e6f-424">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b2e6f-424">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2e6f-425">Créer une page de contenu</span><span class="sxs-lookup"><span data-stu-id="b2e6f-425">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
