---
title: Créez un onglet personnel avec ASP. NET Core MVC
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet personnel personnalisé avec ASP. NET Core MVC.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 7fcb0862647dec15bc93eecf9ce637d52892825c
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818912"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="76930-105">Créez un onglet personnel personnalisé avec ASP.</span><span class="sxs-lookup"><span data-stu-id="76930-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="76930-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="76930-106">NET Core MVC</span></span>

<span data-ttu-id="76930-107">Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet personnel personnalisé avec C# et ASP.</span><span class="sxs-lookup"><span data-stu-id="76930-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="76930-108">NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="76930-108">Net Core MVC.</span></span> <span data-ttu-id="76930-109">Nous allons également utiliser [app Studio pour Microsoft teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser votre manifeste de l’application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="76930-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="76930-110">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="76930-110">Get the source code</span></span>

<span data-ttu-id="76930-111">Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="76930-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="76930-112">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="76930-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="76930-113">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel de l’exemple dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="76930-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="76930-114">Une fois que vous avez le code source, ouvrez Visual Studio et sélectionnez **ouvrir un projet ou une solution**.</span><span class="sxs-lookup"><span data-stu-id="76930-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="76930-115">Accédez au répertoire de l’application d’onglets et ouvrez **PersonalTabMVC. sln**.</span><span class="sxs-lookup"><span data-stu-id="76930-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="76930-116">Pour générer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="76930-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="76930-117">Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l’application a été correctement chargée :</span><span class="sxs-lookup"><span data-stu-id="76930-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="76930-118">Vérifier le code source</span><span class="sxs-lookup"><span data-stu-id="76930-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="76930-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="76930-119">Startup.cs</span></span>

<span data-ttu-id="76930-120">Ce projet a été créé à partir d’une page ASP.</span><span class="sxs-lookup"><span data-stu-id="76930-120">This project was created from an ASP.</span></span> <span data-ttu-id="76930-121">NET Core 2,2 modèle vide de l’application Web avec la case à cocher *Advanced-configure for HTTPS* activée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="76930-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="76930-122">Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendance `ConfigureServices()` .</span><span class="sxs-lookup"><span data-stu-id="76930-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="76930-123">En outre, le modèle vide ne permet pas de traiter le contenu statique par défaut, de sorte que l’intergiciel de fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="76930-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="76930-124">dossier Wwwroot</span><span class="sxs-lookup"><span data-stu-id="76930-124">wwwroot folder</span></span>

<span data-ttu-id="76930-125">Dans ASP.</span><span class="sxs-lookup"><span data-stu-id="76930-125">In ASP.</span></span> <span data-ttu-id="76930-126">NET Core, le dossier racine Web est l’emplacement où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="76930-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="76930-127">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="76930-127">AppManifest folder</span></span>

<span data-ttu-id="76930-128">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="76930-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="76930-129">Une **icône de couleur complète** mesurant 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="76930-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="76930-130">**Icône de contour transparent** mesurant 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="76930-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="76930-131">Un fichier **manifest.js** qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="76930-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="76930-132">Ces fichiers doivent être Zippés dans un package d’application pour être utilisés dans le téléchargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="76930-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="76930-133">Microsoft teams chargera le `contentUrl` spécifié dans votre manifeste, l’incorporera dans un IFRAME et le restituera sous votre onglet.</span><span class="sxs-lookup"><span data-stu-id="76930-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="76930-134">. csproj</span><span class="sxs-lookup"><span data-stu-id="76930-134">.csproj</span></span>

<span data-ttu-id="76930-135">Dans la fenêtre de l’Explorateur de solutions Visual Studio, cliquez avec le bouton droit sur le projet et sélectionnez **modifier le fichier de projet**.</span><span class="sxs-lookup"><span data-stu-id="76930-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="76930-136">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application génère les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="76930-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="76930-137">CONFORMITE</span><span class="sxs-lookup"><span data-stu-id="76930-137">Models</span></span>

<span data-ttu-id="76930-138">*PersonalTab.cs* présente un objet message et des méthodes qui seront appelées à partir de *PersonalTabController* lorsqu’un utilisateur sélectionne un bouton dans la vue *PersonalTab* .</span><span class="sxs-lookup"><span data-stu-id="76930-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="76930-139">Affichages</span><span class="sxs-lookup"><span data-stu-id="76930-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="76930-140">Famille</span><span class="sxs-lookup"><span data-stu-id="76930-140">Home</span></span>

<span data-ttu-id="76930-141">Technologie.</span><span class="sxs-lookup"><span data-stu-id="76930-141">ASP.</span></span> <span data-ttu-id="76930-142">NET Core traite les fichiers appelés *index* comme page d’accueil par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="76930-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="76930-143">Lorsque l’URL de votre navigateur pointe vers la racine du site, *index. cshtml* s’affichera comme page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="76930-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="76930-144">Shared</span><span class="sxs-lookup"><span data-stu-id="76930-144">Shared</span></span>

<span data-ttu-id="76930-145">Le balisage de vue partielle *_Layout. cshtml* contient la structure de page globale et les éléments visuels partagés de l’application.</span><span class="sxs-lookup"><span data-stu-id="76930-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="76930-146">Elle fait également référence à la bibliothèque Teams.</span><span class="sxs-lookup"><span data-stu-id="76930-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="76930-147">Contrã’leurs</span><span class="sxs-lookup"><span data-stu-id="76930-147">Controllers</span></span>

<span data-ttu-id="76930-148">Les contrôleurs utilisent la propriété ViewBag pour transférer dynamiquement les valeurs dans les vues.</span><span class="sxs-lookup"><span data-stu-id="76930-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="76930-149">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="76930-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="76930-150">Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application lorsqu’elle s’exécutera sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="76930-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="76930-151">Il doit ressembler `https://y8rPrT2b.ngrok.io/` à l’emplacement où *y8rPrT2b* est remplacé par votre URL HTTPS alphanumériques ngrok.</span><span class="sxs-lookup"><span data-stu-id="76930-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="76930-152">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à prendre note de l’URL, vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="76930-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="76930-153">Vérifiez que *ngrok* est en cours d’exécution et qu’il fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok qui a été fournie dans votre fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="76930-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="76930-154">[!</span><span class="sxs-lookup"><span data-stu-id="76930-154">[!</span></span> <span data-ttu-id="76930-155">Conseil] vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="76930-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="76930-156">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour qu’elle fonctionne, **maintenez ngrok en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="76930-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="76930-157">Il continuera à écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarrera dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="76930-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="76930-158">Si vous devez redémarrer le service ngrok, il renverra une nouvelle URL et vous devrez mettre à jour chaque emplacement qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="76930-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="76930-159">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="76930-159">Run your application</span></span>

* <span data-ttu-id="76930-160">Dans Visual Studio, appuyez sur **F5** ou sélectionnez **Démarrer le débogage** dans le menu **débogage** de votre application.</span><span class="sxs-lookup"><span data-stu-id="76930-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
