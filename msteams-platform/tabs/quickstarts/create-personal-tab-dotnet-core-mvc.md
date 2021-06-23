---
title: Créez un onglet personnel avec ASP. NET Core MVC
author: surbhigupta
description: Guide de démarrage rapide pour créer un onglet personnel personnalisé avec ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: ac01ae64f44ccf3e06476d4412b16ac9a4730f6c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069153"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="35a20-105">Créer un onglet personnel personnalisé avec ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="35a20-105">Create a Custom Personal Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="35a20-106">Dans ce démarrage rapide, nous allons créer un onglet personnel personnalisé avec C# et ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="35a20-106">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="35a20-107">Nous utiliserons également [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour Microsoft Teams finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="35a20-107">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="35a20-108">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="35a20-108">Get the source code</span></span>

<span data-ttu-id="35a20-109">Ouvrez une invite de commandes et créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="35a20-109">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="35a20-110">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="35a20-110">We have provided a simple project to get you started.</span></span> <span data-ttu-id="35a20-111">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l’exemple de référentiel dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="35a20-111">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="35a20-112">Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="35a20-112">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="35a20-113">Accédez au répertoire de l’application onglet et **ouvrez PersonalTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="35a20-113">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="35a20-114">Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="35a20-114">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="35a20-115">Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l’application s’est chargée correctement :</span><span class="sxs-lookup"><span data-stu-id="35a20-115">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="35a20-116">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="35a20-116">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="35a20-117">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="35a20-117">Startup.cs</span></span>

<span data-ttu-id="35a20-118">Ce projet a été créé à partir d’un asp.</span><span class="sxs-lookup"><span data-stu-id="35a20-118">This project was created from an ASP.</span></span> <span data-ttu-id="35a20-119">Modèle vide application web NET Core 2.2 avec la case à cocher Avancé - Configurer *pour HTTPS* sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="35a20-119">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="35a20-120">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="35a20-120">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="35a20-121">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="35a20-121">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="35a20-122">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="35a20-122">wwwroot folder</span></span>

<span data-ttu-id="35a20-123">Dans ASP.</span><span class="sxs-lookup"><span data-stu-id="35a20-123">In ASP.</span></span> <span data-ttu-id="35a20-124">NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="35a20-124">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="35a20-125">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="35a20-125">AppManifest folder</span></span>

<span data-ttu-id="35a20-126">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="35a20-126">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="35a20-127">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="35a20-127">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="35a20-128">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="35a20-128">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="35a20-129">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="35a20-129">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="35a20-130">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="35a20-130">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="35a20-131">Microsoft Teams chargez la spécifiée dans votre manifeste, incorporez-la dans un IFrame et restituerez-la `contentUrl` dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="35a20-131">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="35a20-132">.csproj</span><span class="sxs-lookup"><span data-stu-id="35a20-132">.csproj</span></span>

<span data-ttu-id="35a20-133">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="35a20-133">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="35a20-134">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="35a20-134">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="35a20-135">Modèles</span><span class="sxs-lookup"><span data-stu-id="35a20-135">Models</span></span>

<span data-ttu-id="35a20-136">**PersonalTab.cs** présente un objet Message et des méthodes qui seront appelées à partir de *PersonalTabController* lorsqu’un utilisateur sélectionne un bouton dans **l’affichage PersonalTab.**</span><span class="sxs-lookup"><span data-stu-id="35a20-136">**PersonalTab.cs** presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the **PersonalTab** View.</span></span>

### <a name="views"></a><span data-ttu-id="35a20-137">Affichages</span><span class="sxs-lookup"><span data-stu-id="35a20-137">Views</span></span>

#### <a name="home"></a><span data-ttu-id="35a20-138">Accueil</span><span class="sxs-lookup"><span data-stu-id="35a20-138">Home</span></span>

<span data-ttu-id="35a20-139">ASP.</span><span class="sxs-lookup"><span data-stu-id="35a20-139">ASP.</span></span> <span data-ttu-id="35a20-140">NET Core traite les fichiers appelés **Index** comme la page d’accueil ou par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="35a20-140">NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="35a20-141">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="35a20-141">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="35a20-142">Shared</span><span class="sxs-lookup"><span data-stu-id="35a20-142">Shared</span></span>

<span data-ttu-id="35a20-143">Le markup *d’affichage partiel _Layout.cshtml* contient la structure de page globale de l’application et les éléments visuels partagés.</span><span class="sxs-lookup"><span data-stu-id="35a20-143">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="35a20-144">Il référencera également la bibliothèque Teams bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="35a20-144">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="35a20-145">Contrôleurs</span><span class="sxs-lookup"><span data-stu-id="35a20-145">Controllers</span></span>

<span data-ttu-id="35a20-146">Les contrôleurs utilisent la propriété ViewBag pour transférer dynamiquement des valeurs vers les affichages.</span><span class="sxs-lookup"><span data-stu-id="35a20-146">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="35a20-147">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="35a20-147">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* <span data-ttu-id="35a20-148">Ngrok écoute les demandes provenant d’Internet et les route vers votre application lorsqu’elle est en cours d’exécution sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="35a20-148">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="35a20-149">Il doit ressembler `https://y8rPrT2b.ngrok.io/` à *l’endroit où y8rPrT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="35a20-149">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="35a20-150">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à noter l’URL. Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="35a20-150">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="35a20-151">Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="35a20-151">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="35a20-152">Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="35a20-152">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="35a20-153">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="35a20-153">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="35a20-154">Il continuera à écouter et reprendra le routage de la demande de votre application lors de son redémarrage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35a20-154">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="35a20-155">Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="35a20-155">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="35a20-156">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="35a20-156">Run your application</span></span>

* <span data-ttu-id="35a20-157">Dans Visual Studio **appuyez sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage de votre** application.</span><span class="sxs-lookup"><span data-stu-id="35a20-157">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="35a20-158">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="35a20-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35a20-159">Créer un canal et un onglet de groupe personnalisés à l’aide Node.js et du générateur Yeoman pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="35a20-159">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
