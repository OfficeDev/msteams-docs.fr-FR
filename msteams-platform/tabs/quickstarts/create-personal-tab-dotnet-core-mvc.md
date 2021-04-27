---
title: Créez un onglet personnel avec ASP. NET Core MVC
author: laujan
description: Guide de démarrage rapide pour créer un onglet personnel personnalisé avec ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3ec6b5c054384653e30e46cbffed4a2af6662c33
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019565"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="50c28-105">Créez un onglet personnel personnalisé avec ASP.</span><span class="sxs-lookup"><span data-stu-id="50c28-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="50c28-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="50c28-106">NET Core MVC</span></span>

<span data-ttu-id="50c28-107">Dans ce démarrage rapide, nous allons créer un onglet personnel personnalisé avec C# et ASP.</span><span class="sxs-lookup"><span data-stu-id="50c28-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="50c28-108">Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="50c28-108">Net Core MVC.</span></span> <span data-ttu-id="50c28-109">Nous utiliserons également [App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser le manifeste de votre application et déployer votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="50c28-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="50c28-110">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="50c28-110">Get the source code</span></span>

<span data-ttu-id="50c28-111">Ouvrez une invite de commandes et créez un répertoire pour votre projet d'onglet.</span><span class="sxs-lookup"><span data-stu-id="50c28-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="50c28-112">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="50c28-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="50c28-113">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l'exemple de référentiel dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="50c28-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="50c28-114">Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="50c28-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="50c28-115">Accédez au répertoire d'application d'onglet et **ouvrez PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="50c28-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="50c28-116">Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="50c28-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="50c28-117">Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l'application s'est chargée correctement :</span><span class="sxs-lookup"><span data-stu-id="50c28-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="50c28-118">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="50c28-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="50c28-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="50c28-119">Startup.cs</span></span>

<span data-ttu-id="50c28-120">Ce projet a été créé à partir d'un asp.</span><span class="sxs-lookup"><span data-stu-id="50c28-120">This project was created from an ASP.</span></span> <span data-ttu-id="50c28-121">Modèle vide application Web NET Core 2.2 avec la case à cocher Avancé - Configurer *pour HTTPS* sélectionnée lors de l'installation.</span><span class="sxs-lookup"><span data-stu-id="50c28-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="50c28-122">Les services MVC sont enregistrés par la méthode de l'infrastructure d'injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="50c28-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="50c28-123">En outre, le modèle vide n'active pas la portion de contenu statique par défaut, de sorte que l'intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="50c28-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="50c28-124">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="50c28-124">wwwroot folder</span></span>

<span data-ttu-id="50c28-125">Dans ASP.</span><span class="sxs-lookup"><span data-stu-id="50c28-125">In ASP.</span></span> <span data-ttu-id="50c28-126">NET Core, le dossier racine web, est l'endroit où l'application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="50c28-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="50c28-127">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="50c28-127">AppManifest folder</span></span>

<span data-ttu-id="50c28-128">Ce dossier contient les fichiers de package d'application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="50c28-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="50c28-129">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="50c28-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="50c28-130">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="50c28-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="50c28-131">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="50c28-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="50c28-132">Ces fichiers doivent être compressés dans un package d'application pour être utilisés lors du chargement de votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="50c28-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="50c28-133">Microsoft Teams charge le manifeste spécifié, l'incorpore dans un IFrame et l'restituer `contentUrl` dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="50c28-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="50c28-134">.csproj</span><span class="sxs-lookup"><span data-stu-id="50c28-134">.csproj</span></span>

<span data-ttu-id="50c28-135">Dans la Visual Studio l'Explorateur de solutions, cliquez avec le bouton droit sur le projet et **sélectionnez Modifier le fichier de projet.**</span><span class="sxs-lookup"><span data-stu-id="50c28-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="50c28-136">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l'application est créée :</span><span class="sxs-lookup"><span data-stu-id="50c28-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="50c28-137">Modèles</span><span class="sxs-lookup"><span data-stu-id="50c28-137">Models</span></span>

<span data-ttu-id="50c28-138">*PersonalTab.cs* présente un objet Message et des méthodes qui seront appelées à partir de *PersonalTabController* lorsqu'un utilisateur sélectionne un bouton dans *l'affichage PersonalTab.*</span><span class="sxs-lookup"><span data-stu-id="50c28-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="50c28-139">Affichages</span><span class="sxs-lookup"><span data-stu-id="50c28-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="50c28-140">Accueil</span><span class="sxs-lookup"><span data-stu-id="50c28-140">Home</span></span>

<span data-ttu-id="50c28-141">ASP.</span><span class="sxs-lookup"><span data-stu-id="50c28-141">ASP.</span></span> <span data-ttu-id="50c28-142">NET Core traite les fichiers appelés *Index* comme la page d'accueil/par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="50c28-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="50c28-143">Lorsque l'URL de votre navigateur pointe vers la racine du site, *Index.cshtml* s'affiche en tant que page d'accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="50c28-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="50c28-144">Shared</span><span class="sxs-lookup"><span data-stu-id="50c28-144">Shared</span></span>

<span data-ttu-id="50c28-145">Le markup *d'affichage partiel _Layout.cshtml* contient la structure de page globale de l'application et les éléments visuels partagés.</span><span class="sxs-lookup"><span data-stu-id="50c28-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="50c28-146">Il référencera également la bibliothèque Teams.</span><span class="sxs-lookup"><span data-stu-id="50c28-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="50c28-147">Contrôleurs</span><span class="sxs-lookup"><span data-stu-id="50c28-147">Controllers</span></span>

<span data-ttu-id="50c28-148">Les contrôleurs utilisent la propriété ViewBag pour transférer dynamiquement des valeurs vers les affichages.</span><span class="sxs-lookup"><span data-stu-id="50c28-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="50c28-149">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="50c28-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="50c28-150">Ngrok écoute les demandes provenant d'Internet et les route vers votre application lorsqu'elle est en cours d'exécution sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="50c28-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="50c28-151">Il doit ressembler `https://y8rPrT2b.ngrok.io/` à *l'endroit où y8rPrT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="50c28-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="50c28-152">Veillez à conserver l'invite de commandes avec ngrok en cours d'exécution et à noter l'URL. Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="50c28-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="50c28-153">Vérifiez que *ngrok* fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l'URL HTTPS ngrok fournie dans la fenêtre d'invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="50c28-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="50c28-154">[!</span><span class="sxs-lookup"><span data-stu-id="50c28-154">[!</span></span> <span data-ttu-id="50c28-155">CONSEIL] Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d'exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="50c28-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="50c28-156">Si vous devez arrêter l'exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d'exécution.**</span><span class="sxs-lookup"><span data-stu-id="50c28-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="50c28-157">Il continuera à écouter et reprendra le routage de la demande de votre application au redémarrage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50c28-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="50c28-158">Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="50c28-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="50c28-159">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="50c28-159">Run your application</span></span>

* <span data-ttu-id="50c28-160">Dans Visual Studio **appuyez sur F5** ou choisissez **Démarrer le débogage** à partir du menu **Débogage de votre** application.</span><span class="sxs-lookup"><span data-stu-id="50c28-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
