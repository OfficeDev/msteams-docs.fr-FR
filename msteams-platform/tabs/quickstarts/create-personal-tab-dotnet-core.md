---
title: Créez un onglet personnel avec ASP.NET Core
author: laujan
description: Un guide quickstart pour créer un onglet personnel personnalisé avec ASP.NET Core.
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
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="52737-103">Créez un onglet personnel à l’aide d’ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="52737-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="52737-104">Dans ce quickstart, nous allons walk-through créer un onglet personnel personnalisé avec C # et ASP.Net pages Core Razor.</span><span class="sxs-lookup"><span data-stu-id="52737-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="52737-105">Nous utiliserons également [App Studio pour vous aider Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="52737-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="52737-106">Obtenez le code source</span><span class="sxs-lookup"><span data-stu-id="52737-106">Get the source code</span></span>

<span data-ttu-id="52737-107">Ouvrez une invite de commande et créez un nouvel annuaire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="52737-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="52737-108">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="52737-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="52737-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel d’échantillons dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="52737-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="52737-110">Une fois que vous avez le code source, Visual Studio et **sélectionnez Ouvrir un projet ou une solution**.</span><span class="sxs-lookup"><span data-stu-id="52737-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="52737-111">Accédez à l’annuaire d’application d’onglets **et ouvrez PersonalTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="52737-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="52737-112">Pour créer et exécuter votre application appuyez **sur F5** ou **choisissez Démarrer le débogage** dans le menu **Debug.**</span><span class="sxs-lookup"><span data-stu-id="52737-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="52737-113">Dans un navigateur naviguer vers les URL ci-dessous pour vérifier l’application chargée correctement:</span><span class="sxs-lookup"><span data-stu-id="52737-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="52737-114">Revoir le code source</span><span class="sxs-lookup"><span data-stu-id="52737-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="52737-115">Démarrage.cs</span><span class="sxs-lookup"><span data-stu-id="52737-115">Startup.cs</span></span>

<span data-ttu-id="52737-116">Ce projet a été créé à partir d’ASP.NET Core modèle vide d’application Web 2.2 avec la case à **cochée Advanced - Configure pour HTTPS** sélectionnée lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="52737-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="52737-117">Les services MVC sont enregistrés par la méthode du cadre d’injection de `ConfigureServices()` dépendance.</span><span class="sxs-lookup"><span data-stu-id="52737-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="52737-118">En outre, le modèle vide ne permet pas de servir le contenu statique par défaut, de sorte que le middleware fichiers statiques est ajouté à la `Configure()` méthode:</span><span class="sxs-lookup"><span data-stu-id="52737-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="52737-119">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="52737-119">wwwroot folder</span></span>

<span data-ttu-id="52737-120">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="52737-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="52737-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="52737-121">Index.cshtml</span></span>

<span data-ttu-id="52737-122">ASP.NET Core traite les fichiers appelés *Index comme la* page par défaut/accueil du site.</span><span class="sxs-lookup"><span data-stu-id="52737-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="52737-123">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml sera** affiché comme page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="52737-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="52737-124">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="52737-124">AppManifest folder</span></span>

<span data-ttu-id="52737-125">Ce dossier contient les fichiers de paquet d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="52737-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="52737-126">Une **icône couleur mesurant** 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="52737-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="52737-127">Une **icône transparente de** contour mesurant 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="52737-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="52737-128">Une **manifest.jsdans le** fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="52737-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="52737-129">Ces fichiers doivent être zippés dans un paquet d’applications pour être utilisés dans le téléchargement de votre onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="52737-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="52737-130">Microsoft Teams chargeront le `contentUrl` spécifié dans votre manifeste, l’intégreront dans un iframe <\> et le rendront dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="52737-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="52737-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="52737-131">.csproj</span></span>

<span data-ttu-id="52737-132">Dans la Visual Studio de solution explorer, cliquez à droite sur le projet et sélectionnez **Modifier Project Fichier**.</span><span class="sxs-lookup"><span data-stu-id="52737-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="52737-133">Au bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application se construit :</span><span class="sxs-lookup"><span data-stu-id="52737-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="52737-134">Ouvrez une invite de commande dans la racine de votre répertoire de projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52737-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="52737-135">Ngrok écoutera les demandes d’Internet et les acheminera vers votre application lorsqu’elle sera en cours d’exécution sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="52737-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="52737-136">Il devrait ressembler `https://y8rPrT2b.ngrok.io/` à *l’endroit où y8rPrT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="52737-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="52737-137">Assurez-vous de garder l’invite de commande avec ngrok en cours d’exécution, et de prendre une note de l’URL - vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="52737-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="52737-138">Vérifiez que **ngrok fonctionne** et fonctionne correctement en ouvrant votre navigateur et en allant à votre page de contenu via l’URL HTTPS ngrok qui a été fourni dans votre fenêtre de commande rapide.</span><span class="sxs-lookup"><span data-stu-id="52737-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="52737-139">Vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour compléter ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="52737-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="52737-140">Si vous avez besoin d’arrêter d’exécuter votre application Visual Studio pour y travailler, **gardez ngrok en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="52737-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="52737-141">Il continuera d’écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarre en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52737-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="52737-142">Si vous devez redémarrer le service ngrok, il va renvoyer une nouvelle URL et vous devrez mettre à jour chaque endroit qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="52737-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="52737-143">Exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="52737-143">Run your application</span></span>

- <span data-ttu-id="52737-144">Dans Visual Studio appuyez **sur F5** ou **choisissez Start Debugging** dans le menu **Debug de votre** application.</span><span class="sxs-lookup"><span data-stu-id="52737-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="52737-145">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="52737-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52737-146">Créez un onglet personnel personnalisé avec ASP.NETCore MVC</span><span class="sxs-lookup"><span data-stu-id="52737-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
