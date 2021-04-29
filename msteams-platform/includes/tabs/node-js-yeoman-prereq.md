## <a name="prerequisites"></a><span data-ttu-id="791c4-101">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="791c4-101">Prerequisites</span></span>

- <span data-ttu-id="791c4-102">Pour effectuer ce démarrage rapide, vous aurez besoin d'un client Office 365 et d'une équipe configurée avec l'application Autoriser le téléchargement *d'applications* personnalisées activée.</span><span class="sxs-lookup"><span data-stu-id="791c4-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="791c4-103">Pour plus d'informations, voir Préparer votre client [Office 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="791c4-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="791c4-104">Si vous n'avez pas encore de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme pour les développeurs Office 365.</span><span class="sxs-lookup"><span data-stu-id="791c4-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="791c4-105">L'abonnement reste actif tant que vous l'utilisez pour le développement en cours.</span><span class="sxs-lookup"><span data-stu-id="791c4-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="791c4-106">Voir Bienvenue dans le programme pour les développeurs [Office 365.](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program)</span><span class="sxs-lookup"><span data-stu-id="791c4-106">See [Welcome to the Office 365 Developer Program](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="791c4-107">En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="791c4-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="791c4-108">N'importe quel éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="791c4-108">Any text editor or IDE.</span></span> <span data-ttu-id="791c4-109">Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuit.</span><span class="sxs-lookup"><span data-stu-id="791c4-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="791c4-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="791c4-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="791c4-111">Vous devez utiliser la dernière version de LTS.</span><span class="sxs-lookup"><span data-stu-id="791c4-111">You should use the latest LTS version.</span></span> <span data-ttu-id="791c4-112">Le nœud Gestionnaire de package (npm) s'installera dans votre système avec l'installation de Node.js.</span><span class="sxs-lookup"><span data-stu-id="791c4-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="791c4-113">Une fois que vous avez installé Node.js, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en tapant ce qui suit dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="791c4-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="791c4-114">Installez le générateur d'applications Microsoft Teams en tapant ce qui suit dans votre invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="791c4-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="791c4-115">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="791c4-115">Generate your project</span></span>

- <span data-ttu-id="791c4-116">Ouvrez une invite de commandes et créez un répertoire pour votre projet d'onglet.</span><span class="sxs-lookup"><span data-stu-id="791c4-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="791c4-117">Pour démarrer le générateur, accédez à votre nouveau répertoire et tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="791c4-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="791c4-118">Ensuite, vous allez fournir une série de valeurs qui seront utilisées dans le fichiermanifest.js **votre** application :</span><span class="sxs-lookup"><span data-stu-id="791c4-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![capture d'écran d'ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="791c4-120">**Quel est le nom de votre solution ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-120">**What is your solution name?**</span></span>

<span data-ttu-id="791c4-121">Il s'agit du nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="791c4-121">This is your project name.</span></span> <span data-ttu-id="791c4-122">Vous pouvez accepter le nom suggéré en appuyant sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="791c4-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="791c4-123">**Où souhaitez-vous placer les fichiers ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="791c4-124">Vous êtes actuellement dans votre répertoire de projet.</span><span class="sxs-lookup"><span data-stu-id="791c4-124">You're currently in your project directory.</span></span> <span data-ttu-id="791c4-125">Appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="791c4-125">Press enter.</span></span>

<span data-ttu-id="791c4-126">**Titre de votre projet d'application Microsoft Teams ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="791c4-127">Il s'agit du nom de votre package d'application et sera utilisé dans le manifeste et la description de l'application.</span><span class="sxs-lookup"><span data-stu-id="791c4-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="791c4-128">**Votre nom (d'entreprise) ? (32 caractères maximum)**</span><span class="sxs-lookup"><span data-stu-id="791c4-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="791c4-129">Le nom de votre société sera utilisé dans le manifeste de l'application.</span><span class="sxs-lookup"><span data-stu-id="791c4-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="791c4-130">**Quelle version de manifeste souhaitez-vous utiliser ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="791c4-131">Sélectionnez le schéma par défaut.</span><span class="sxs-lookup"><span data-stu-id="791c4-131">Select the default schema.</span></span>

<span data-ttu-id="791c4-132">**La échafaudage rapide ? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="791c4-132">**Quick scaffolding? (Y/n)**</span></span>

<span data-ttu-id="791c4-133">La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="791c4-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

<span data-ttu-id="791c4-134">**Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**</span><span class="sxs-lookup"><span data-stu-id="791c4-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="791c4-135">Ce champ n'est pas obligatoire et ne doit être utilisé que si vous faites déjà partie de [Microsoft Partner Network](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="791c4-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="791c4-136">**Que voulez-vous ajouter à votre projet ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-136">**What do you want to add to your project?**</span></span>

<span data-ttu-id="791c4-137">Sélectionnez ( &ast; ) Un onglet.</span><span class="sxs-lookup"><span data-stu-id="791c4-137">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="791c4-138">**L'URL dans laquelle vous hébergez cette solution ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-138">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="791c4-139">Par défaut, le générateur suggère une URL de sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="791c4-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="791c4-140">Vous testerez uniquement votre application localement, par conséquent, une URL valide n'est pas nécessaire pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="791c4-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="791c4-141">**Souhaitez-vous inclure l'infrastructure test et les tests initiaux ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="791c4-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="791c4-142">Choisissez **de ne** pas inclure d'infrastructure de test pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="791c4-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="791c4-143">La valeur par défaut est Oui ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="791c4-143">The default is yes; enter **n**.</span></span>

<span data-ttu-id="791c4-144">**Voulez-vous utiliser Azure Applications Insights pour la télémétrie ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="791c4-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="791c4-145">Choisissez **de ne** pas inclure Azure Application [Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="791c4-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="791c4-146">La valeur par défaut est non ; entrez **n**.</span><span class="sxs-lookup"><span data-stu-id="791c4-146">The default is no; enter **n**.</span></span>

<span data-ttu-id="791c4-147">**Nom de l'onglet par défaut (16 caractères maximum) ?**</span><span class="sxs-lookup"><span data-stu-id="791c4-147">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="791c4-148">Nommez votre onglet. Ce nom d'onglet sera utilisé dans l'ensemble de votre projet en tant que composant de chemin d'accès fichier/URL.</span><span class="sxs-lookup"><span data-stu-id="791c4-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
