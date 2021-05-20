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
# <a name="create-a-personal-tab-using-aspnetcore"></a>Créez un onglet personnel à l’aide d’ASP.NETCore

Dans ce quickstart, nous allons walk-through créer un onglet personnel personnalisé avec C # et ASP.Net pages Core Razor. Nous utiliserons également [App Studio pour vous aider Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) finaliser le manifeste de votre application et déployer votre onglet sur Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtenez le code source

Ouvrez une invite de commande et créez un nouvel annuaire pour votre projet d’onglet. Nous avons fourni un projet simple pour vous aider à démarrer. Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner le référentiel d’échantillons dans votre nouveau répertoire :

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Une fois que vous avez le code source, Visual Studio et **sélectionnez Ouvrir un projet ou une solution**. Accédez à l’annuaire d’application d’onglets **et ouvrez PersonalTab.sln**.

Pour créer et exécuter votre application appuyez **sur F5** ou **choisissez Démarrer le débogage** dans le menu **Debug.** Dans un navigateur naviguer vers les URL ci-dessous pour vérifier l’application chargée correctement:

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a>Revoir le code source

### <a name="startupcs"></a>Démarrage.cs

Ce projet a été créé à partir d’ASP.NET Core modèle vide d’application Web 2.2 avec la case à **cochée Advanced - Configure pour HTTPS** sélectionnée lors de la configuration. Les services MVC sont enregistrés par la méthode du cadre d’injection de `ConfigureServices()` dépendance. En outre, le modèle vide ne permet pas de servir le contenu statique par défaut, de sorte que le middleware fichiers statiques est ajouté à la `Configure()` méthode:

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

### <a name="wwwroot-folder"></a>dossier wwwroot

Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core traite les fichiers appelés *Index comme la* page par défaut/accueil du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml sera** affiché comme page d’accueil de votre application.

### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de paquet d’application requis suivants :

- Une **icône couleur mesurant** 192 x 192 pixels.
- Une **icône transparente de** contour mesurant 32 x 32 pixels.
- Une **manifest.jsdans le** fichier qui spécifie les attributs de votre application.

Ces fichiers doivent être zippés dans un paquet d’applications pour être utilisés dans le téléchargement de votre onglet Teams. Microsoft Teams chargeront le `contentUrl` spécifié dans votre manifeste, l’intégreront dans un iframe <\> et le rendront dans votre onglet.

### <a name="csproj"></a>.csproj

Dans la Visual Studio de solution explorer, cliquez à droite sur le projet et sélectionnez **Modifier Project Fichier**. Au bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l’application se construit :

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

- Ouvrez une invite de commande dans la racine de votre répertoire de projet et exécutez la commande suivante :

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- Ngrok écoutera les demandes d’Internet et les acheminera vers votre application lorsqu’elle sera en cours d’exécution sur le port 44325.  Il devrait ressembler `https://y8rPrT2b.ngrok.io/` à *l’endroit où y8rPrT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.

- Assurez-vous de garder l’invite de commande avec ngrok en cours d’exécution, et de prendre une note de l’URL - vous en aurez besoin plus tard.

- Vérifiez que **ngrok fonctionne** et fonctionne correctement en ouvrant votre navigateur et en allant à votre page de contenu via l’URL HTTPS ngrok qui a été fourni dans votre fenêtre de commande rapide.

>[!TIP]
>Vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour compléter ce démarrage rapide. Si vous avez besoin d’arrêter d’exécuter votre application Visual Studio pour y travailler, **gardez ngrok en cours d’exécution**. Il continuera d’écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarre en Visual Studio. Si vous devez redémarrer le service ngrok, il va renvoyer une nouvelle URL et vous devrez mettre à jour chaque endroit qui utilise cette URL.

### <a name="run-your-application"></a>Exécutez votre application

- Dans Visual Studio appuyez **sur F5** ou **choisissez Start Debugging** dans le menu **Debug de votre** application.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créez un onglet personnel personnalisé avec ASP.NETCore MVC](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
