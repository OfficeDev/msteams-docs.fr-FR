---
title: Créer un onglet personnel avec ASP.NET Core
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet personnel personnalisé avec ASP.NET Core.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: b279c96f47265fe1928ae90d661e7dc042085b39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674002"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core"></a><span data-ttu-id="8773a-103">Créer un onglet personnel personnalisé avec ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8773a-103">Create a Custom Personal Tab with ASP.NET Core</span></span>

<span data-ttu-id="8773a-104">Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet personnel personnalisé avec C# et ASP.Net pages Razor principales.</span><span class="sxs-lookup"><span data-stu-id="8773a-104">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="8773a-105">Nous allons également utiliser [app Studio pour Microsoft teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser votre manifeste de l’application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="8773a-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="8773a-106">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="8773a-106">Get the source code</span></span>

<span data-ttu-id="8773a-107">Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="8773a-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="8773a-108">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="8773a-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="8773a-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel de l’exemple dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="8773a-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="8773a-110">Une fois que vous avez le code source, ouvrez Visual Studio et sélectionnez **ouvrir un projet ou une solution**.</span><span class="sxs-lookup"><span data-stu-id="8773a-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="8773a-111">Accédez au répertoire de l’application d’onglets et ouvrez **PersonalTab. sln**.</span><span class="sxs-lookup"><span data-stu-id="8773a-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="8773a-112">Pour générer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="8773a-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="8773a-113">Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l’application est chargée correctement :</span><span class="sxs-lookup"><span data-stu-id="8773a-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="8773a-114">Vérifier le code source</span><span class="sxs-lookup"><span data-stu-id="8773a-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="8773a-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="8773a-115">Startup.cs</span></span>

<span data-ttu-id="8773a-116">Ce projet a été créé à partir d’un modèle vide d’application Web ASP.NET Core 2,2 et la case à cocher *Advanced-configure for HTTPS* est activée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="8773a-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="8773a-117">Les services MVC sont enregistrés par la méthode de l’infrastructure `ConfigureServices()` d’injection de dépendance.</span><span class="sxs-lookup"><span data-stu-id="8773a-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="8773a-118">En outre, le modèle vide ne permet pas de traiter le contenu statique par défaut, de sorte que l’intergiciel de fichiers `Configure()` statiques est ajouté à la méthode :</span><span class="sxs-lookup"><span data-stu-id="8773a-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="8773a-119">dossier Wwwroot</span><span class="sxs-lookup"><span data-stu-id="8773a-119">wwwroot folder</span></span>

<span data-ttu-id="8773a-120">Dans ASP.NET Core, le dossier racine Web est l’emplacement où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="8773a-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="8773a-121">Index. cshtml</span><span class="sxs-lookup"><span data-stu-id="8773a-121">Index.cshtml</span></span>

<span data-ttu-id="8773a-122">ASP.NET Core traite les fichiers appelés *index* comme page d’accueil par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="8773a-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="8773a-123">Lorsque l’URL de votre navigateur pointe vers la racine du site, **index. cshtml** s’affichera comme page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="8773a-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="8773a-124">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="8773a-124">AppManifest folder</span></span>

<span data-ttu-id="8773a-125">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="8773a-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="8773a-126">Une **icône de couleur complète** mesurant 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="8773a-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="8773a-127">**Icône de contour transparent** mesurant 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="8773a-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="8773a-128">Un fichier **Manifest. JSON** qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="8773a-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="8773a-129">Ces fichiers doivent être Zippés dans un package d’application pour être utilisés dans le téléchargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="8773a-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="8773a-130">Microsoft teams chargera le `contentUrl` spécifié dans votre manifeste, l’incorporera dans un IFRAME et le restituera sous votre onglet.</span><span class="sxs-lookup"><span data-stu-id="8773a-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="8773a-131">. csproj</span><span class="sxs-lookup"><span data-stu-id="8773a-131">.csproj</span></span>

<span data-ttu-id="8773a-132">Dans la fenêtre de l’Explorateur de solutions Visual Studio, cliquez avec le bouton droit sur le projet et sélectionnez **modifier le fichier de projet**.</span><span class="sxs-lookup"><span data-stu-id="8773a-132">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="8773a-133">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application génère les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8773a-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="8773a-134">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8773a-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- <span data-ttu-id="8773a-135">Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application lorsqu’elle s’exécutera sur le port 44325.</span><span class="sxs-lookup"><span data-stu-id="8773a-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="8773a-136">Il doit ressembler à l' `https://y8rPrT2b.ngrok.io/` emplacement où *y8rPrT2b* est remplacé par votre URL HTTPS alphanumériques ngrok.</span><span class="sxs-lookup"><span data-stu-id="8773a-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="8773a-137">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à prendre note de l’URL, vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="8773a-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL—you'll need it later.</span></span>

- <span data-ttu-id="8773a-138">Vérifiez que *ngrok* est en cours d’exécution et qu’il fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok qui a été fournie dans votre fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="8773a-138">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="8773a-139">Vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="8773a-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="8773a-140">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour qu’elle fonctionne, **maintenez ngrok en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="8773a-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="8773a-141">Il continuera à écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarrera dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8773a-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="8773a-142">Si vous devez redémarrer le service ngrok, il renverra une nouvelle URL et vous devrez mettre à jour chaque emplacement qui utilise cette URL.</span><span class="sxs-lookup"><span data-stu-id="8773a-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="8773a-143">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="8773a-143">Run your application</span></span>

- <span data-ttu-id="8773a-144">Dans Visual Studio, appuyez sur **F5** ou sélectionnez **Démarrer le débogage** dans le menu **débogage** de votre application.</span><span class="sxs-lookup"><span data-stu-id="8773a-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
