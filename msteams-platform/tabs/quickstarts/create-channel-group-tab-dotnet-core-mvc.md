---
title: Créer un onglet canal et de groupe avec ASP.NET Core MVC
author: surbhigupta
description: Guide de démarrage rapide pour créer un canal personnalisé et un onglet de groupe avec ASP.NET Core MVC
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: b265e413d1f1d1239eda8285ea7066ad01750bba
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069125"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="02d42-103">Créer un canal et un onglet de groupe personnalisés avec ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="02d42-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="02d42-104">Dans ce démarrage rapide, nous allons créer un onglet canal/groupe personnalisé avec C# et ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="02d42-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="02d42-105">Nous utiliserons également [App Studio](~/concepts/build-and-test/app-studio-overview.md) pour Microsoft Teams finaliser le manifeste de votre application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="02d42-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="02d42-106">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="02d42-106">Get the source code</span></span>

<span data-ttu-id="02d42-107">Ouvrez une invite de commandes et créez un répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="02d42-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="02d42-108">Nous avons fourni un projet d’onglet de [groupe](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) de canaux simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="02d42-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="02d42-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l’exemple de référentiel dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="02d42-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="02d42-110">Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**</span><span class="sxs-lookup"><span data-stu-id="02d42-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="02d42-111">Accédez au répertoire d’application de l’onglet et **ouvrez ChannelGroupTabMVC.sln**.</span><span class="sxs-lookup"><span data-stu-id="02d42-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="02d42-112">Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="02d42-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="02d42-113">Dans un navigateur, accédez aux URL ci-dessous et vérifiez que l’application s’est chargée correctement :</span><span class="sxs-lookup"><span data-stu-id="02d42-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="02d42-114">Passer en revue le code source</span><span class="sxs-lookup"><span data-stu-id="02d42-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="02d42-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="02d42-115">Startup.cs</span></span>

<span data-ttu-id="02d42-116">Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour *HTTPS* sélectionnée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="02d42-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="02d42-117">Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances.</span><span class="sxs-lookup"><span data-stu-id="02d42-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="02d42-118">En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :</span><span class="sxs-lookup"><span data-stu-id="02d42-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="02d42-119">dossier wwwroot</span><span class="sxs-lookup"><span data-stu-id="02d42-119">wwwroot folder</span></span>

<span data-ttu-id="02d42-120">Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="02d42-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="02d42-121">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="02d42-121">AppManifest folder</span></span>

<span data-ttu-id="02d42-122">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="02d42-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="02d42-123">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="02d42-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="02d42-124">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="02d42-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="02d42-125">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="02d42-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="02d42-126">Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="02d42-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="02d42-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="02d42-127">.csproj</span></span>

<span data-ttu-id="02d42-128">Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .**</span><span class="sxs-lookup"><span data-stu-id="02d42-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="02d42-129">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application est créée :</span><span class="sxs-lookup"><span data-stu-id="02d42-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="02d42-130">Modèles</span><span class="sxs-lookup"><span data-stu-id="02d42-130">Models</span></span>

<span data-ttu-id="02d42-131">*ChannelGroup.cs* présente un objet message et des méthodes qui seront appelés à partir des contrôleurs lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="02d42-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="02d42-132">Affichages</span><span class="sxs-lookup"><span data-stu-id="02d42-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="02d42-133">Accueil</span><span class="sxs-lookup"><span data-stu-id="02d42-133">Home</span></span>

<span data-ttu-id="02d42-134">ASP.NET Core fichiers appelés *Index* comme page d’accueil/par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="02d42-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="02d42-135">Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="02d42-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="02d42-136">Shared</span><span class="sxs-lookup"><span data-stu-id="02d42-136">Shared</span></span>

<span data-ttu-id="02d42-137">Le markup *d’affichage partiel _Layout.cshtml* contient la structure de page globale de l’application et les éléments visuels partagés.</span><span class="sxs-lookup"><span data-stu-id="02d42-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="02d42-138">Il référencera également la bibliothèque Teams bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="02d42-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="02d42-139">Contrôleurs</span><span class="sxs-lookup"><span data-stu-id="02d42-139">Controllers</span></span>

<span data-ttu-id="02d42-140">Les contrôleurs utilisent la propriété ViewBag pour transférer dynamiquement des valeurs vers les affichages.</span><span class="sxs-lookup"><span data-stu-id="02d42-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="02d42-141">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02d42-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

- <span data-ttu-id="02d42-142">Ngrok écoute les demandes provenant d’Internet et les route vers votre application lorsqu’elle est en cours d’exécution sur le port 44355.</span><span class="sxs-lookup"><span data-stu-id="02d42-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="02d42-143">Il doit ressembler `https://y8rCgT2b.ngrok.io/` à *l’endroit où y8rCgT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.</span><span class="sxs-lookup"><span data-stu-id="02d42-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="02d42-144">Veillez à maintenir l’invite de commandes avec ngrok en cours d’exécution et à noter l’URL. Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="02d42-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="02d42-145">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="02d42-145">Update your application</span></span>

<span data-ttu-id="02d42-146">Dans **Tab.cshtml,** l’application présente à l’utilisateur deux boutons d’option pour afficher l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="02d42-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="02d42-147">Le choix du  **bouton Sélectionner** gris ou Sélectionner rouge se déclenche `saveGray()` ou, respectivement, définit et active le bouton Enregistrer `saveRed()` sur la page de `settings.setValidityState(true)` configuration. </span><span class="sxs-lookup"><span data-stu-id="02d42-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="02d42-148">Ce code vous permet Teams que vous avez satisfait aux exigences de configuration et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="02d42-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="02d42-149">Lors de l’enregistrer, les paramètres `settings.setSettings` sont définies.</span><span class="sxs-lookup"><span data-stu-id="02d42-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="02d42-150">Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été correctement résolue.</span><span class="sxs-lookup"><span data-stu-id="02d42-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]
