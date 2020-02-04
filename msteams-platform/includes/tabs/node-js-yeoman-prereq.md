## <a name="prerequisites"></a><span data-ttu-id="32b47-101">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="32b47-101">Prerequisites</span></span>

- <span data-ttu-id="32b47-102">Pour terminer ce démarrage rapide, vous aurez besoin d’un client Office 365 et d’une équipe configurée avec l’option *autoriser le téléchargement d’applications personnalisées* .</span><span class="sxs-lookup"><span data-stu-id="32b47-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="32b47-103">Pour en savoir plus, consultez [la rubrique préparer votre client Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="32b47-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="32b47-104">Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire pour obtenir un abonnement gratuit via le programme de développement Office 365.</span><span class="sxs-lookup"><span data-stu-id="32b47-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="32b47-105">L’abonnement reste actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="32b47-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="32b47-106">Consultez [la page Bienvenue dans le programme pour les développeurs Office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span><span class="sxs-lookup"><span data-stu-id="32b47-106">See [Welcome to the Office 365 Developer Program](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span></span>

<span data-ttu-id="32b47-107">De plus, ce projet requiert que les éléments suivants soient installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="32b47-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="32b47-108">N’importe quel éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="32b47-108">Any text editor or IDE.</span></span> <span data-ttu-id="32b47-109">Vous pouvez installer et utiliser [Visual Studio code](https://code.visualstudio.com/download) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="32b47-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="32b47-110">[Node. js/NPM](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="32b47-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="32b47-111">Vous devez utiliser la dernière version d’LTS.</span><span class="sxs-lookup"><span data-stu-id="32b47-111">You should use the latest LTS version.</span></span> <span data-ttu-id="32b47-112">Le gestionnaire de package de nœuds (NPM) s’installe dans votre système avec l’installation de node. js.</span><span class="sxs-lookup"><span data-stu-id="32b47-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="32b47-113">Une fois que vous avez installé node. js, installez les packages [Yeoman](https://yeoman.io/) et [Gulp-CLI](https://www.npmjs.com/package/gulp-cli) en tapant ce qui suit dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="32b47-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="32b47-114">Installez le générateur d’applications Microsoft teams en tapant ce qui suit dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="32b47-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="32b47-115">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="32b47-115">Generate your project</span></span>

- <span data-ttu-id="32b47-116">Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="32b47-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="32b47-117">Pour démarrer le générateur, accédez à votre nouveau répertoire et tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="32b47-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="32b47-118">Ensuite, vous devez fournir une série de valeurs qui seront utilisées dans le fichier **Manifest. JSON** de votre application :</span><span class="sxs-lookup"><span data-stu-id="32b47-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="32b47-120">**Quel est le nom de votre solution ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-120">**What is your solution name?**</span></span>

<span data-ttu-id="32b47-121">Il s’agit de votre nom de projet.</span><span class="sxs-lookup"><span data-stu-id="32b47-121">This is your project name.</span></span> <span data-ttu-id="32b47-122">Vous pouvez accepter le nom suggéré en appuyant sur entrée.</span><span class="sxs-lookup"><span data-stu-id="32b47-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="32b47-123">**Où souhaitez-vous placer les fichiers ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="32b47-124">Vous êtes actuellement dans le répertoire de votre projet.</span><span class="sxs-lookup"><span data-stu-id="32b47-124">You're currently in your project directory.</span></span> <span data-ttu-id="32b47-125">Appuyez sur entrée.</span><span class="sxs-lookup"><span data-stu-id="32b47-125">Press enter.</span></span>

<span data-ttu-id="32b47-126">**Titre de votre projet d’application Microsoft teams ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="32b47-127">Il s’agit du nom de votre package d’application et sera utilisé dans le manifeste de l’application et sa description.</span><span class="sxs-lookup"><span data-stu-id="32b47-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="32b47-128">**Votre nom (société) ? (32 caractères max.)**</span><span class="sxs-lookup"><span data-stu-id="32b47-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="32b47-129">Le nom de votre société sera utilisé dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="32b47-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="32b47-130">**Quelle version de manifeste souhaitez-vous utiliser ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="32b47-131">Sélectionnez le schéma par défaut.</span><span class="sxs-lookup"><span data-stu-id="32b47-131">Select the default schema.</span></span>

<span data-ttu-id="32b47-132">**Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez le champ vide pour sauter)**</span><span class="sxs-lookup"><span data-stu-id="32b47-132">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="32b47-133">Ce champ n’est pas obligatoire et doit être utilisé uniquement si vous faites déjà partie du [réseau partenaire de Microsoft](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="32b47-133">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="32b47-134">**Que voulez-vous ajouter à votre projet ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-134">**What do you want to add to your project?**</span></span>

<span data-ttu-id="32b47-135">&ast; Sélectionnez un onglet.</span><span class="sxs-lookup"><span data-stu-id="32b47-135">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="32b47-136">**L’URL où vous allez héberger cette solution ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-136">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="32b47-137">Par défaut, le générateur suggère une URL de sites Web Azure.</span><span class="sxs-lookup"><span data-stu-id="32b47-137">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="32b47-138">Vous testez uniquement votre application localement, par conséquent, une URL valide n’est pas nécessaire pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="32b47-138">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="32b47-139">**Voulez-vous inclure l’infrastructure de test et les tests initiaux ? (o/N)**</span><span class="sxs-lookup"><span data-stu-id="32b47-139">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="32b47-140">Choisissez de **ne pas** inclure d’infrastructure de test pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="32b47-140">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="32b47-141">La valeur par défaut est oui ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="32b47-141">The default is yes; enter **n**.</span></span>

<span data-ttu-id="32b47-142">**Voulez-vous utiliser les analyses des applications Azure pour la télémétrie ? (o/N)**</span><span class="sxs-lookup"><span data-stu-id="32b47-142">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="32b47-143">Choisissez de **ne pas** inclure les informations d' [application Azure](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32b47-143">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="32b47-144">La valeur par défaut est non ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="32b47-144">The default is no; enter **n**.</span></span>

<span data-ttu-id="32b47-145">**Nom d’onglet par défaut (16 caractères maximum) ?**</span><span class="sxs-lookup"><span data-stu-id="32b47-145">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="32b47-146">Nommez votre onglet. Ce nom d’onglet sera utilisé dans votre projet en tant que composant de chemin d’accès de fichier/URL.</span><span class="sxs-lookup"><span data-stu-id="32b47-146">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
