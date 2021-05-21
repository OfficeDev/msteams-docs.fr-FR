---
title: Créer un onglet canal et de groupe avec ASP.NET Core
author: laujan
description: Guide de démarrage rapide sur la création d’un canal personnalisé et d’un onglet de groupe avec ASP.NET Core.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: f748335b621e9bc93272aaeb8d7e12ecc3ebbee0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52580449"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnetcore"></a><span data-ttu-id="8d590-103">Créer un onglet canal et de groupe personnalisé avec ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="8d590-103">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>

<span data-ttu-id="8d590-104">Dans ce démarrage rapide, nous allons créer un onglet canal/groupe personnalisé avec C# et ASP.Net page Principale.</span><span class="sxs-lookup"><span data-stu-id="8d590-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="8d590-105">Nous utiliserons également [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour Microsoft Teams finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="8d590-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="8d590-106">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="8d590-106">Get the source code</span></span>

<span data-ttu-id="8d590-107">Ouvrez une invite de commandes et créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="8d590-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="8d590-108">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="8d590-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="8d590-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l’exemple de référentiel dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="8d590-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="8d590-110">Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="8d590-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="8d590-111">Accédez au répertoire d’application de l’onglet et **ouvrez ChannelGroupTab.sln**.</span><span class="sxs-lookup"><span data-stu-id="8d590-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="8d590-112">Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="8d590-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="8d590-113">Dans un navigateur, accédez aux URL ci-dessous et vérifiez que l’application a correctement chargé :</span><span class="sxs-lookup"><span data-stu-id="8d590-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="8d590-114">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="8d590-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="8d590-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="8d590-115">Startup.cs</span></span>

<span data-ttu-id="8d590-116">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour *HTTPS* sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="8d590-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="8d590-117">Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="8d590-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="8d590-118">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="8d590-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="8d590-119">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="8d590-119">wwwroot folder</span></span>

<span data-ttu-id="8d590-120">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="8d590-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="8d590-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="8d590-121">Index.cshtml</span></span>

<span data-ttu-id="8d590-122">ASP.NET Core fichiers appelés *Index* comme page d’accueil/par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="8d590-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="8d590-123">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="8d590-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="8d590-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="8d590-124">Tab.cs</span></span>

<span data-ttu-id="8d590-125">Ce C# contient une méthode qui sera appelée à partir de **Tab.cshtml** lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="8d590-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="8d590-126">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="8d590-126">AppManifest folder</span></span>

<span data-ttu-id="8d590-127">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="8d590-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="8d590-128">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="8d590-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="8d590-129">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="8d590-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="8d590-130">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="8d590-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="8d590-131">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="8d590-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="8d590-132">Lorsqu’un utilisateur choisit d’ajouter ou de mettre à jour votre onglet, Microsoft Teams charge le contenu spécifié dans votre manifeste, l’incorpore dans un IFrame et l’restituer dans `configurationUrl` votre onglet.</span><span class="sxs-lookup"><span data-stu-id="8d590-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="8d590-133">.csproj</span><span class="sxs-lookup"><span data-stu-id="8d590-133">.csproj</span></span>

<span data-ttu-id="8d590-134">Dans la fenêtre Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="8d590-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="8d590-135">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="8d590-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="8d590-136">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d590-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="8d590-137">Ngrok écoute les demandes provenant d’Internet et les route vers votre application lorsqu’elle est en cours d’exécution sur le port 44355.</span><span class="sxs-lookup"><span data-stu-id="8d590-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="8d590-138">Il doit ressembler `https://y8rCgT2b.ngrok.io/` à *l’endroit où y8rCgT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="8d590-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="8d590-139">Veillez à maintenir l’invite de commandes avec ngrok en cours d’exécution et à noter l’URL. Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8d590-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="8d590-140">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="8d590-140">Update your application</span></span>

<span data-ttu-id="8d590-141">Dans *Tab.cshtml,* l’application présente à l’utilisateur deux boutons d’option pour afficher l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="8d590-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="8d590-142">Le choix du  **bouton Sélectionner** gris ou Sélectionner rouge se déclenche `saveGray()` ou, respectivement, définit et active le bouton Enregistrer `saveRed()` sur la page de `settings.setValidityState(true)` configuration. </span><span class="sxs-lookup"><span data-stu-id="8d590-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="8d590-143">Ce code vous permet Teams que vous avez satisfait aux exigences de configuration et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="8d590-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="8d590-144">Lors de l’enregistrer, les paramètres `settings.setSettings` sont définies.</span><span class="sxs-lookup"><span data-stu-id="8d590-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="8d590-145">Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été correctement résolue.</span><span class="sxs-lookup"><span data-stu-id="8d590-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

## <a name="next-step"></a><span data-ttu-id="8d590-146">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="8d590-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d590-147">Créer un onglet de groupe et de canal personnalisé avec ASP.NETCore MVC</span><span class="sxs-lookup"><span data-stu-id="8d590-147">Create a Custom Channel and Group Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core-mvc.md)