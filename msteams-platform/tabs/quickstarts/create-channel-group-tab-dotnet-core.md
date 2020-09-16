---
title: Créer un onglet de canal et de groupe avec ASP.NET Core
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet de canal et de groupe personnalisé avec ASP.NET Core.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 6a21d40d4d474fd587b43760d818082b4ab2502d
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818919"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a><span data-ttu-id="16c3c-103">Créer un onglet de canal et de groupe personnalisé avec ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="16c3c-103">Create a Custom Channel and Group Tab with ASP.NET Core</span></span>

<span data-ttu-id="16c3c-104">Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet de canal/groupe personnalisé avec C# et ASP.Net Core Razor page.</span><span class="sxs-lookup"><span data-stu-id="16c3c-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="16c3c-105">Nous allons également utiliser [app Studio pour Microsoft teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser votre manifeste de l’application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="16c3c-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="16c3c-106">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="16c3c-106">Get the source code</span></span>

<span data-ttu-id="16c3c-107">Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="16c3c-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="16c3c-108">Nous avons fourni un projet simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="16c3c-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="16c3c-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel de l’exemple dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="16c3c-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="16c3c-110">Une fois que vous avez le code source, ouvrez Visual Studio et sélectionnez **ouvrir un projet ou une solution**.</span><span class="sxs-lookup"><span data-stu-id="16c3c-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="16c3c-111">Accédez au répertoire de l’application d’onglets et ouvrez **ChannelGroupTab. sln**.</span><span class="sxs-lookup"><span data-stu-id="16c3c-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="16c3c-112">Pour générer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="16c3c-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="16c3c-113">Dans un navigateur, accédez aux URL ci-dessous et vérifiez que l’application est chargée correctement :</span><span class="sxs-lookup"><span data-stu-id="16c3c-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="16c3c-114">Vérifier le code source</span><span class="sxs-lookup"><span data-stu-id="16c3c-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="16c3c-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="16c3c-115">Startup.cs</span></span>

<span data-ttu-id="16c3c-116">Ce projet a été créé à partir d’un modèle vide d’application Web ASP.NET Core 2,2 et la case à cocher *Advanced-configure for HTTPS* est activée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="16c3c-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="16c3c-117">Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendance `ConfigureServices()` .</span><span class="sxs-lookup"><span data-stu-id="16c3c-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="16c3c-118">En outre, le modèle vide ne permet pas de traiter le contenu statique par défaut, de sorte que l’intergiciel de fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="16c3c-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="16c3c-119">dossier Wwwroot</span><span class="sxs-lookup"><span data-stu-id="16c3c-119">wwwroot folder</span></span>

<span data-ttu-id="16c3c-120">Dans ASP.NET Core, le dossier racine Web est l’emplacement où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="16c3c-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="16c3c-121">Index. cshtml</span><span class="sxs-lookup"><span data-stu-id="16c3c-121">Index.cshtml</span></span>

<span data-ttu-id="16c3c-122">ASP.NET Core traite les fichiers appelés *index* comme page d’accueil par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="16c3c-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="16c3c-123">Lorsque l’URL de votre navigateur pointe vers la racine du site, **index. cshtml** s’affichera comme page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="16c3c-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="16c3c-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="16c3c-124">Tab.cs</span></span>

<span data-ttu-id="16c3c-125">Ce fichier C# contient une méthode qui sera appelée à partir de **Tab. cshtml** lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="16c3c-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="16c3c-126">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="16c3c-126">AppManifest folder</span></span>

<span data-ttu-id="16c3c-127">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="16c3c-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="16c3c-128">Une **icône de couleur complète** mesurant 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="16c3c-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="16c3c-129">**Icône de contour transparent** mesurant 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="16c3c-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="16c3c-130">Un fichier **manifest.js** qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="16c3c-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="16c3c-131">Ces fichiers doivent être Zippés dans un package d’application pour être utilisés dans le téléchargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="16c3c-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="16c3c-132">Lorsqu’un utilisateur choisit d’ajouter ou de mettre à jour votre onglet, Microsoft teams charge le `configurationUrl` spécifié dans votre manifeste, l’incorpore dans un IFRAME et l’affiche dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="16c3c-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="16c3c-133">. csproj</span><span class="sxs-lookup"><span data-stu-id="16c3c-133">.csproj</span></span>

<span data-ttu-id="16c3c-134">Dans la fenêtre de l’Explorateur de solutions Visual Studio, cliquez avec le bouton droit sur le projet et sélectionnez **modifier le fichier de projet**.</span><span class="sxs-lookup"><span data-stu-id="16c3c-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="16c3c-135">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application génère les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="16c3c-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="16c3c-136">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="16c3c-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- <span data-ttu-id="16c3c-137">Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application lorsqu’elle s’exécutera sur le port 44355.</span><span class="sxs-lookup"><span data-stu-id="16c3c-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="16c3c-138">Il doit ressembler `https://y8rCgT2b.ngrok.io/` à l’emplacement où *y8rCgT2b* est remplacé par votre URL HTTPS alphanumériques ngrok.</span><span class="sxs-lookup"><span data-stu-id="16c3c-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="16c3c-139">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à prendre note de l’URL, vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="16c3c-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="16c3c-140">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="16c3c-140">Update your application</span></span>

<span data-ttu-id="16c3c-141">Dans *Tab. cshtml* , l’application présente à l’utilisateur deux boutons d’options permettant d’afficher l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="16c3c-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="16c3c-142">Le choix du bouton **Sélectionner le gris** ou sélectionner le bouton **rouge** déclenche `saveGray()` ou `saveRed()` , respectivement, définit `settings.setValidityState(true)` et active le bouton **Enregistrer** dans la page de configuration.</span><span class="sxs-lookup"><span data-stu-id="16c3c-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="16c3c-143">Ce code permet aux équipes de déterminer que vous êtes satisfait de la configuration requise et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="16c3c-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="16c3c-144">Lors de l’enregistrement, les paramètres de `settings.setSettings` sont définis.</span><span class="sxs-lookup"><span data-stu-id="16c3c-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="16c3c-145">Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue avec succès.</span><span class="sxs-lookup"><span data-stu-id="16c3c-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

