---
title: Créer un onglet personnel avec ASP.NET Core
author: laujan
description: Guide de démarrage rapide pour créer un onglet personnel personnalisé avec ASP.NET Core.
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 41aa916f4c69d50e48254d0f4934109429dab83c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566893"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="ceacb-103">Créer un onglet personnel à l’aide d’ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="ceacb-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="ceacb-104">Dans ce démarrage rapide, nous allons créer un onglet personnel personnalisé avec des pages C# et ASP.Net core.</span><span class="sxs-lookup"><span data-stu-id="ceacb-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="ceacb-105">Nous utiliserons également [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour Microsoft Teams finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="ceacb-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="ceacb-106">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="ceacb-106">Get the source code</span></span>

<span data-ttu-id="ceacb-107">Ouvrez une invite de commandes et créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ceacb-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="ceacb-108">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="ceacb-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="ceacb-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l’exemple de référentiel dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="ceacb-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ceacb-110">Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="ceacb-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="ceacb-111">Accédez au répertoire d’application de l’onglet et **ouvrez PersonalTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="ceacb-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="ceacb-112">Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="ceacb-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="ceacb-113">Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l’application a correctement chargé :</span><span class="sxs-lookup"><span data-stu-id="ceacb-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="ceacb-114">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="ceacb-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="ceacb-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ceacb-115">Startup.cs</span></span>

<span data-ttu-id="ceacb-116">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="ceacb-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="ceacb-117">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="ceacb-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ceacb-118">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="ceacb-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="ceacb-119">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="ceacb-119">wwwroot folder</span></span>

<span data-ttu-id="ceacb-120">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="ceacb-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="ceacb-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="ceacb-121">Index.cshtml</span></span>

<span data-ttu-id="ceacb-122">ASP.NET Core fichiers appelés *Index* comme page d’accueil/par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="ceacb-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="ceacb-123">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="ceacb-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="ceacb-124">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="ceacb-124">AppManifest folder</span></span>

<span data-ttu-id="ceacb-125">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="ceacb-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="ceacb-126">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="ceacb-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ceacb-127">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="ceacb-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ceacb-128">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="ceacb-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ceacb-129">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="ceacb-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ceacb-130">Microsoft Teams chargez le spécifié dans votre manifeste, l’incorporez dans un iframe <et restituerez-le `contentUrl` \> dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ceacb-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="ceacb-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="ceacb-131">.csproj</span></span>

<span data-ttu-id="ceacb-132">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="ceacb-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ceacb-133">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="ceacb-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="ceacb-134">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ceacb-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="ceacb-135">Ngrok écoute les demandes provenant d’Internet et les route vers votre application lorsqu’elle est en cours d’exécution sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="ceacb-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="ceacb-136">Il doit ressembler `https://y8rPrT2b.ngrok.io/` à *l’endroit où y8rPrT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="ceacb-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="ceacb-137">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à noter l’URL. Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ceacb-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="ceacb-138">Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="ceacb-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="ceacb-139">Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="ceacb-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="ceacb-140">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="ceacb-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ceacb-141">Il continuera à écouter et reprendra le routage de la demande de votre application lors de son redémarrage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ceacb-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ceacb-142">Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="ceacb-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="ceacb-143">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ceacb-143">Run your application</span></span>

- <span data-ttu-id="ceacb-144">Dans Visual Studio **appuyez sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage de votre** application.</span><span class="sxs-lookup"><span data-stu-id="ceacb-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="ceacb-145">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="ceacb-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ceacb-146">Créer un onglet personnel personnalisé avec ASP.NETCore MVC</span><span class="sxs-lookup"><span data-stu-id="ceacb-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
