---
title: Créer un onglet de canal et de groupe avec ASP.NET Core MVC
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet de canal et de groupe personnalisé avec ASP.NET Core MVC.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 57c22d10414eb8ec93249584219488397f0b6b33
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673754"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="66859-103">Créer un onglet de canal et de groupe personnalisé avec ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="66859-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="66859-104">Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet de canal/groupe personnalisé avec C# et ASP.Net Core MVC.</span><span class="sxs-lookup"><span data-stu-id="66859-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="66859-105">Nous allons également utiliser [app Studio pour Microsoft teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser votre manifeste de l’application et déployer votre onglet sur Teams.</span><span class="sxs-lookup"><span data-stu-id="66859-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="66859-106">Obtenir le code source</span><span class="sxs-lookup"><span data-stu-id="66859-106">Get the source code</span></span>

<span data-ttu-id="66859-107">Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet.</span><span class="sxs-lookup"><span data-stu-id="66859-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="66859-108">Nous avons fourni un projet d' [onglets de groupe de canaux](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) simple pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="66859-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="66859-109">Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel de l’exemple dans votre nouveau répertoire :</span><span class="sxs-lookup"><span data-stu-id="66859-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="66859-110">Une fois que vous avez le code source, ouvrez Visual Studio et sélectionnez **ouvrir un projet ou une solution**.</span><span class="sxs-lookup"><span data-stu-id="66859-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="66859-111">Accédez au répertoire de l’application d’onglets et ouvrez **ChannelGroupTabMVC. sln**.</span><span class="sxs-lookup"><span data-stu-id="66859-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="66859-112">Pour générer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="66859-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="66859-113">Dans un navigateur, accédez aux URL ci-dessous et vérifiez que l’application a été correctement chargée :</span><span class="sxs-lookup"><span data-stu-id="66859-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="66859-114">Vérifier le code source</span><span class="sxs-lookup"><span data-stu-id="66859-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="66859-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="66859-115">Startup.cs</span></span>

<span data-ttu-id="66859-116">Ce projet a été créé à partir d’un modèle vide d’application Web ASP.NET Core 2,2 et la case à cocher *Advanced-configure for HTTPS* est activée lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="66859-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="66859-117">Les services MVC sont enregistrés par la méthode de l’infrastructure `ConfigureServices()` d’injection de dépendance.</span><span class="sxs-lookup"><span data-stu-id="66859-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="66859-118">En outre, le modèle vide ne permet pas de traiter le contenu statique par défaut, de sorte que l’intergiciel de fichiers `Configure()` statiques est ajouté à la méthode :</span><span class="sxs-lookup"><span data-stu-id="66859-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="66859-119">dossier Wwwroot</span><span class="sxs-lookup"><span data-stu-id="66859-119">wwwroot folder</span></span>

<span data-ttu-id="66859-120">Dans ASP.NET Core, le dossier racine Web est l’emplacement où l’application recherche des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="66859-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="66859-121">Dossier AppManifest</span><span class="sxs-lookup"><span data-stu-id="66859-121">AppManifest folder</span></span>

<span data-ttu-id="66859-122">Ce dossier contient les fichiers de package d’application requis suivants :</span><span class="sxs-lookup"><span data-stu-id="66859-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="66859-123">Une **icône de couleur complète** mesurant 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="66859-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="66859-124">**Icône de contour transparent** mesurant 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="66859-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="66859-125">Un fichier **Manifest. JSON** qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="66859-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="66859-126">Ces fichiers doivent être Zippés dans un package d’application pour être utilisés dans le téléchargement de votre onglet vers Teams.</span><span class="sxs-lookup"><span data-stu-id="66859-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="66859-127">. csproj</span><span class="sxs-lookup"><span data-stu-id="66859-127">.csproj</span></span>

<span data-ttu-id="66859-128">Dans la fenêtre de l’Explorateur de solutions Visual Studio, cliquez avec le bouton droit sur le projet et sélectionnez **modifier le fichier de projet**.</span><span class="sxs-lookup"><span data-stu-id="66859-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="66859-129">En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application génère les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="66859-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="66859-130">CONFORMITE</span><span class="sxs-lookup"><span data-stu-id="66859-130">Models</span></span>

<span data-ttu-id="66859-131">*ChannelGroup.cs* présente un objet message et des méthodes qui seront appelées à partir des contrôleurs lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="66859-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="66859-132">Affichages</span><span class="sxs-lookup"><span data-stu-id="66859-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="66859-133">Accueil</span><span class="sxs-lookup"><span data-stu-id="66859-133">Home</span></span>

<span data-ttu-id="66859-134">ASP.NET Core traite les fichiers appelés *index* comme page d’accueil par défaut du site.</span><span class="sxs-lookup"><span data-stu-id="66859-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="66859-135">Lorsque l’URL de votre navigateur pointe vers la racine du site, **index. cshtml** s’affichera comme page d’accueil de votre application.</span><span class="sxs-lookup"><span data-stu-id="66859-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="66859-136">Shared</span><span class="sxs-lookup"><span data-stu-id="66859-136">Shared</span></span>

<span data-ttu-id="66859-137">Le balisage de vue partielle *_Layout. cshtml* contient la structure de page globale et les éléments visuels partagés de l’application.</span><span class="sxs-lookup"><span data-stu-id="66859-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="66859-138">Elle fait également référence à la bibliothèque Teams.</span><span class="sxs-lookup"><span data-stu-id="66859-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="66859-139">Contrã’leurs</span><span class="sxs-lookup"><span data-stu-id="66859-139">Controllers</span></span>

<span data-ttu-id="66859-140">Les contrôleurs utilisent la propriété ViewBag pour transférer dynamiquement les valeurs dans les vues.</span><span class="sxs-lookup"><span data-stu-id="66859-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="66859-141">Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="66859-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="66859-142">Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application lorsqu’elle s’exécutera sur le port 44355.</span><span class="sxs-lookup"><span data-stu-id="66859-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="66859-143">Il doit ressembler à l' `https://y8rCgT2b.ngrok.io/` emplacement où *y8rCgT2b* est remplacé par votre URL HTTPS alphanumériques ngrok.</span><span class="sxs-lookup"><span data-stu-id="66859-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="66859-144">Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à prendre note de l’URL, vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="66859-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="66859-145">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="66859-145">Update your application</span></span>

<span data-ttu-id="66859-146">Dans **Tab. cshtml** , l’application présente à l’utilisateur deux boutons d’options permettant d’afficher l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="66859-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="66859-147">Le choix du bouton **Sélectionner le gris** ou sélectionner `saveGray()` le `saveRed()`bouton **rouge** déclenche ou `settings.setValidityState(true)`, respectivement, définit et active le bouton **Enregistrer** dans la page de configuration.</span><span class="sxs-lookup"><span data-stu-id="66859-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="66859-148">Ce code permet aux équipes de déterminer que vous êtes satisfait de la configuration requise et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="66859-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="66859-149">Lors de l’enregistrement, les `settings.setSettings` paramètres de sont définis.</span><span class="sxs-lookup"><span data-stu-id="66859-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="66859-150">Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue avec succès.</span><span class="sxs-lookup"><span data-stu-id="66859-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
