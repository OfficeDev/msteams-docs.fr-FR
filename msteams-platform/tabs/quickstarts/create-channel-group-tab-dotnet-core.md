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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a>Créer un onglet de canal et de groupe personnalisé avec ASP.NET Core

Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet de canal/groupe personnalisé avec C# et ASP.Net Core Razor page. Nous allons également utiliser [app Studio pour Microsoft teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser votre manifeste de l’application et déployer votre onglet sur Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtenir le code source

Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet. Nous avons fourni un projet simple pour vous aider à démarrer. Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel de l’exemple dans votre nouveau répertoire :

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Une fois que vous avez le code source, ouvrez Visual Studio et sélectionnez **ouvrir un projet ou une solution**. Accédez au répertoire de l’application d’onglets et ouvrez **ChannelGroupTab. sln**.

Pour générer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** . Dans un navigateur, accédez aux URL ci-dessous et vérifiez que l’application est chargée correctement :

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a>Vérifier le code source

### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application Web ASP.NET Core 2,2 et la case à cocher *Advanced-configure for HTTPS* est activée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendance `ConfigureServices()` . En outre, le modèle vide ne permet pas de traiter le contenu statique par défaut, de sorte que l’intergiciel de fichiers statiques est ajouté à la `Configure()` méthode :

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

### <a name="wwwroot-folder"></a>dossier Wwwroot

Dans ASP.NET Core, le dossier racine Web est l’emplacement où l’application recherche des fichiers statiques.

### <a name="indexcshtml"></a>Index. cshtml

ASP.NET Core traite les fichiers appelés *index* comme page d’accueil par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **index. cshtml** s’affichera comme page d’accueil de votre application.

### <a name="tabcs"></a>Tab.cs

Ce fichier C# contient une méthode qui sera appelée à partir de **Tab. cshtml** lors de la configuration.

### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

- Une **icône de couleur complète** mesurant 192 x 192 pixels.
- **Icône de contour transparent** mesurant 32 x 32 pixels.
- Un fichier **manifest.js** qui spécifie les attributs de votre application.

Ces fichiers doivent être Zippés dans un package d’application pour être utilisés dans le téléchargement de votre onglet vers Teams. Lorsqu’un utilisateur choisit d’ajouter ou de mettre à jour votre onglet, Microsoft teams charge le `configurationUrl` spécifié dans votre manifeste, l’incorpore dans un IFRAME et l’affiche dans votre onglet.

### <a name="csproj"></a>. csproj

Dans la fenêtre de l’Explorateur de solutions Visual Studio, cliquez avec le bouton droit sur le projet et sélectionnez **modifier le fichier de projet**. En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application génère les éléments suivants :

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

- Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application lorsqu’elle s’exécutera sur le port 44355. Il doit ressembler `https://y8rCgT2b.ngrok.io/` à l’emplacement où *y8rCgT2b* est remplacé par votre URL HTTPS alphanumériques ngrok.

- Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à prendre note de l’URL, vous en aurez besoin plus tard.

## <a name="update-your-application"></a>Mettre à jour votre application

Dans *Tab. cshtml* , l’application présente à l’utilisateur deux boutons d’options permettant d’afficher l’onglet avec une icône rouge ou grise. Le choix du bouton **Sélectionner le gris** ou sélectionner le bouton **rouge** déclenche `saveGray()` ou `saveRed()` , respectivement, définit `settings.setValidityState(true)` et active le bouton **Enregistrer** dans la page de configuration. Ce code permet aux équipes de déterminer que vous êtes satisfait de la configuration requise et que l’installation peut se poursuivre. Lors de l’enregistrement, les paramètres de `settings.setSettings` sont définis. Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue avec succès.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

