---
title: Créer un onglet canal et de groupe avec ASP.NET Core
author: laujan
description: Guide de démarrage rapide pour créer un canal personnalisé et un onglet de groupe avec ASP.NET Core.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 8271e2d225d5ae3f6458b17b9595c4d23c3ca6c9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019572"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a>Créer un canal et un onglet de groupe personnalisés avec ASP.NET Core

Dans ce démarrage rapide, nous allons créer un onglet canal/groupe personnalisé avec C# et ASP.Net page Principale. Nous utiliserons également [App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser le manifeste de votre application et déployer votre onglet dans Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtenir le code source

Ouvrez une invite de commandes et créez un répertoire pour votre projet d'onglet. Nous avons fourni un projet simple pour vous aider à démarrer. Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l'exemple de référentiel dans votre nouveau répertoire :

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.** Accédez au répertoire d'application de l'onglet et **ouvrez ChannelGroupTab.sln**.

Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.** Dans un navigateur, accédez aux URL ci-dessous et vérifiez que l'application a correctement chargé :

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a>Passer en revue le code source

### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d'un modèle ASP.NET d'application Web Core 2.2 vide avec la case à cocher Avancé - Configurer pour *HTTPS* sélectionnée lors de l'installation. Les services MVC sont inscrits par la méthode de l'infrastructure d'injection de `ConfigureServices()` dépendances. En outre, le modèle vide n'active pas la portion de contenu statique par défaut, de sorte que l'intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :

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

Dans ASP.NET Core, le dossier racine web est l'endroit où l'application recherche des fichiers statiques.

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core traite les fichiers appelés *Index* comme la page d'accueil/par défaut du site. Lorsque l'URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s'affiche en tant que page d'accueil de votre application.

### <a name="tabcs"></a>Tab.cs

Ce C# contient une méthode qui sera appelée à partir de **Tab.cshtml** lors de la configuration.

### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d'application requis suivants :

- Icône **en couleurs complètes** de 192 x 192 pixels.
- Icône **de plan transparente de** 32 x 32 pixels.
- Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d'application pour être utilisés lors du téléchargement de votre onglet vers Teams. Lorsqu'un utilisateur choisit d'ajouter ou de mettre à jour votre onglet, Microsoft Teams charge le contenu spécifié dans votre manifeste, l'incorpore dans un IFrame et l'restituer dans `configurationUrl` votre onglet.

### <a name="csproj"></a>.csproj

Dans la Visual Studio'Explorateur de solutions, cliquez avec le bouton droit sur le projet et **sélectionnez Modifier le fichier de projet.** En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l'application est créée :

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

- Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- Ngrok écoute les demandes provenant d'Internet et les route vers votre application lorsqu'elle est en cours d'exécution sur le port 44355. Il doit ressembler `https://y8rCgT2b.ngrok.io/` à *l'endroit où y8rCgT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.

- Veillez à maintenir l'invite de commandes avec ngrok en cours d'exécution et à noter l'URL. Vous en aurez besoin ultérieurement.

## <a name="update-your-application"></a>Mettre à jour votre application

Dans *Tab.cshtml,* l'application présente à l'utilisateur deux boutons d'option pour afficher l'onglet avec une icône rouge ou grise. Le choix du  **bouton Sélectionner** gris ou Sélectionner rouge se déclenche `saveGray()` ou, respectivement, définit et active le bouton Enregistrer `saveRed()` sur la page de `settings.setValidityState(true)` configuration.  Ce code permet à Teams de savoir que vous avez satisfait aux exigences de configuration et que l'installation peut continuer. Lors de l'enregistrer, les paramètres `settings.setSettings` sont définies. Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l'URL de contenu a été correctement résolue.

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

