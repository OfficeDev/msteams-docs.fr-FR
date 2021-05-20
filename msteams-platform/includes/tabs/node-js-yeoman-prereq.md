## <a name="prerequisites"></a><span data-ttu-id="7c4b8-101">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7c4b8-101">Prerequisites</span></span>

- <span data-ttu-id="7c4b8-102">Pour compléter ce démarrage rapide, vous aurez besoin d’un Office 365 locataire et d’une équipe configurée avec *autoriser le téléchargement d’applications personnalisées activées.*</span><span class="sxs-lookup"><span data-stu-id="7c4b8-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="7c4b8-103">Pour en savoir plus, [consultez Préparer votre Office 365 locataire.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="7c4b8-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="7c4b8-104">Si vous n’avez pas actuellement de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme Office 365 développeur.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="7c4b8-105">L’abonnement restera actif tant que vous l’utilisez pour le développement continu.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="7c4b8-106">Voir [Bienvenue dans le programme Office 365 développeur de la ville](/office/developer-program/microsoft-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="7c4b8-106">See [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="7c4b8-107">En outre, ce projet exige que vous avez ce qui suit installé dans votre environnement de développement:</span><span class="sxs-lookup"><span data-stu-id="7c4b8-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="7c4b8-108">Tout éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-108">Any text editor or IDE.</span></span> <span data-ttu-id="7c4b8-109">Vous pouvez installer et [utiliser Visual Studio Code](https://code.visualstudio.com/download) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="7c4b8-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="7c4b8-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="7c4b8-111">Vous devez utiliser la dernière version LTS.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-111">You should use the latest LTS version.</span></span> <span data-ttu-id="7c4b8-112">Le nœud Gestionnaire de package (npm) s’installera dans votre système avec l’installation de Node.js.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="7c4b8-113">Une fois que vous avez installé avec succès Node.js, installez [les paquets Yeoman](https://yeoman.io/) [et gulp-cli](https://www.npmjs.com/package/gulp-cli) en tapant ce qui suit dans votre invite de commande :</span><span class="sxs-lookup"><span data-stu-id="7c4b8-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="7c4b8-114">Installez le Microsoft Teams apps en tapant ce qui suit dans votre invite de commande :</span><span class="sxs-lookup"><span data-stu-id="7c4b8-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a><span data-ttu-id="7c4b8-115">Générer votre projet</span><span class="sxs-lookup"><span data-stu-id="7c4b8-115">Generate your project</span></span>

- <span data-ttu-id="7c4b8-116">Ouvrez une invite de commande et créez un nouvel annuaire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="7c4b8-117">Pour démarrer le générateur, accédez à votre nouvel annuaire et tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c4b8-117">To start the generator, navigate to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

- <span data-ttu-id="7c4b8-118">Ensuite, vous fournirez une série de valeurs qui seront utilisées dans les données de votre application **manifest.jsdans le** fichier :</span><span class="sxs-lookup"><span data-stu-id="7c4b8-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

    ![capture d’écran d’ouverture de générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="7c4b8-120">**Quel est le nom de votre solution ?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-120">**What is your solution name?**</span></span>

    <span data-ttu-id="7c4b8-121">C’est le nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-121">This is your project name.</span></span> <span data-ttu-id="7c4b8-122">Vous pouvez accepter le nom suggéré en appuyant sur entrer.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-122">You can accept the suggested name by pressing enter.</span></span>

    <span data-ttu-id="7c4b8-123">**Où souhaitez-vous placer les fichiers ?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-123">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="7c4b8-124">Vous êtes actuellement dans votre répertoire de projet.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-124">You're currently in your project directory.</span></span> <span data-ttu-id="7c4b8-125">Appuyez sur entrez.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-125">Press enter.</span></span>

    <span data-ttu-id="7c4b8-126">**Titre de votre projet Microsoft Teams apprappe ?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-126">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="7c4b8-127">Il s’agit du nom de votre paquet d’application et sera utilisé dans le manifeste et la description de l’application.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-127">This is your app package name and will be used in the app manifest and description.</span></span>

    <span data-ttu-id="7c4b8-128">**Votre nom (d’entreprise)? (max 32 caractères)**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-128">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="7c4b8-129">Le nom de votre entreprise sera utilisé dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-129">Your company name will be used in the app manifest.</span></span>

    <span data-ttu-id="7c4b8-130">**Quelle version manifeste souhaitez-vous utiliser ?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-130">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="7c4b8-131">Sélectionnez le schéma par défaut.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-131">Select the default schema.</span></span>

    <span data-ttu-id="7c4b8-132">**Un échafaudage rapide ? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-132">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="7c4b8-133">La valeur par défaut est oui; entrez **n** pour entrer votre identifiant de partenaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="7c4b8-134">**Entrez votre identifiant microsoft partner, si vous en avez un ? (Laisser vide pour sauter)**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="7c4b8-135">Ce champ n’est pas nécessaire et ne doit être utilisé que si vous faites déjà partie du [Réseau partenaire Microsoft](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7c4b8-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="7c4b8-136">**Qu’est-ce que vous voulez ajouter à votre projet?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-136">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="7c4b8-137">Sélectionnez ( &ast; ) Un onglet.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-137">Select ( &ast; ) A Tab.</span></span>

    <span data-ttu-id="7c4b8-138">**L’URL où vous hébergez cette solution ?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-138">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="7c4b8-139">Par défaut, le générateur suggère une URL de sites Web Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="7c4b8-140">Vous ne testerez votre application que localement, par conséquent, une URL valide n’est pas nécessaire pour compléter ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

    <span data-ttu-id="7c4b8-141">**Souhaitez-vous inclure le cadre de test et les tests initiaux? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="7c4b8-142">Choisissez **de ne** pas inclure de cadre de test pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="7c4b8-143">La valeur par défaut est oui; entrer **n**.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-143">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="7c4b8-144">**Souhaitez-vous utiliser Azure Applications Insights pour la télémétrie ? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="7c4b8-145">Choisissez **de ne** pas inclure [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c4b8-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="7c4b8-146">La valeur par défaut est non; entrer **n**.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-146">The default is no; enter **n**.</span></span>

    <span data-ttu-id="7c4b8-147">**Nom de l’onglet par défaut (max 16 caractères)?**</span><span class="sxs-lookup"><span data-stu-id="7c4b8-147">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="7c4b8-148">Nommez votre onglet. Ce nom d’onglet sera utilisé tout au long de votre projet comme composant de chemin de fichier/URL.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
