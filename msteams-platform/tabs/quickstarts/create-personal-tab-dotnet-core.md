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
# <a name="create-a-custom-personal-tab-with-aspnet-core"></a>Créer un onglet personnel personnalisé avec ASP.NET Core

Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet personnel personnalisé avec C# et ASP.Net pages Razor principales. Nous allons également utiliser [app Studio pour Microsoft teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser votre manifeste de l’application et déployer votre onglet sur Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtenir le code source

Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet. Nous avons fourni un projet simple pour vous aider à démarrer. Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel de l’exemple dans votre nouveau répertoire :

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Une fois que vous avez le code source, ouvrez Visual Studio et sélectionnez **ouvrir un projet ou une solution**. Accédez au répertoire de l’application d’onglets et ouvrez **PersonalTab. sln**.

Pour générer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** . Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l’application est chargée correctement :

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a>Vérifier le code source

### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application Web ASP.NET Core 2,2 et la case à cocher *Advanced-configure for HTTPS* est activée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure `ConfigureServices()` d’injection de dépendance. En outre, le modèle vide ne permet pas de traiter le contenu statique par défaut, de sorte que l’intergiciel de fichiers `Configure()` statiques est ajouté à la méthode :

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

### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

- Une **icône de couleur complète** mesurant 192 x 192 pixels.
- **Icône de contour transparent** mesurant 32 x 32 pixels.
- Un fichier **Manifest. JSON** qui spécifie les attributs de votre application.

Ces fichiers doivent être Zippés dans un package d’application pour être utilisés dans le téléchargement de votre onglet vers Teams. Microsoft teams chargera le `contentUrl` spécifié dans votre manifeste, l’incorporera dans un IFRAME et le restituera sous votre onglet.

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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application lorsqu’elle s’exécutera sur le port 44325.  Il doit ressembler à l' `https://y8rPrT2b.ngrok.io/` emplacement où *y8rPrT2b* est remplacé par votre URL HTTPS alphanumériques ngrok.

- Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et à prendre note de l’URL, vous en aurez besoin plus tard.

- Vérifiez que *ngrok* est en cours d’exécution et qu’il fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok qui a été fournie dans votre fenêtre d’invite de commandes.

>[!TIP]
>Vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour qu’elle fonctionne, **maintenez ngrok en cours d’exécution**. Il continuera à écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarrera dans Visual Studio. Si vous devez redémarrer le service ngrok, il renverra une nouvelle URL et vous devrez mettre à jour chaque emplacement qui utilise cette URL.

### <a name="run-your-application"></a>Exécuter votre application

- Dans Visual Studio, appuyez sur **F5** ou sélectionnez **Démarrer le débogage** dans le menu **débogage** de votre application.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
