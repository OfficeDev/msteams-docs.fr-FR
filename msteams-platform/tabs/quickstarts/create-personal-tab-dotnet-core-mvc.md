---
title: Créez un onglet personnel avec ASP. NET Core MVC
author: laujan
description: Guide de démarrage rapide pour créer un onglet personnel personnalisé avec ASP. NET Core MVC.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3ec6b5c054384653e30e46cbffed4a2af6662c33
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019565"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a>Créez un onglet personnel personnalisé avec ASP. NET Core MVC

Dans ce démarrage rapide, nous allons créer un onglet personnel personnalisé avec C# et ASP. Net Core MVC. Nous utiliserons également [App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) pour finaliser le manifeste de votre application et déployer votre onglet dans Teams.

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>Obtenir le code source

Ouvrez une invite de commandes et créez un répertoire pour votre projet d'onglet. Nous avons fourni un projet simple pour vous aider à démarrer. Pour récupérer le code source, vous pouvez télécharger le dossier zip et extraire les fichiers ou cloner l'exemple de référentiel dans votre nouveau répertoire :

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Une fois que vous avez le code source, ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.** Accédez au répertoire d'application d'onglet et **ouvrez PersonalTabMVC.sln**.

Pour créer et exécuter votre application, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.** Dans un navigateur, accédez aux URL ci-dessous pour vérifier que l'application s'est chargée correctement :

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>Passer en revue le code source

### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d'un asp. Modèle vide application Web NET Core 2.2 avec la case à cocher Avancé - Configurer *pour HTTPS* sélectionnée lors de l'installation. Les services MVC sont enregistrés par la méthode de l'infrastructure d'injection de `ConfigureServices()` dépendances. En outre, le modèle vide n'active pas la portion de contenu statique par défaut, de sorte que l'intermédiaire des fichiers statiques est ajouté à la `Configure()` méthode :

``` csharp
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

Dans ASP. NET Core, le dossier racine web, est l'endroit où l'application recherche des fichiers statiques.

### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d'application requis suivants :

* Icône **en couleurs complètes** de 192 x 192 pixels.
* Icône **de plan transparente de** 32 x 32 pixels.
* Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d'application pour être utilisés lors du chargement de votre onglet dans Teams. Microsoft Teams charge le manifeste spécifié, l'incorpore dans un IFrame et l'restituer `contentUrl` dans votre onglet.

### <a name="csproj"></a>.csproj

Dans la Visual Studio l'Explorateur de solutions, cliquez avec le bouton droit sur le projet et **sélectionnez Modifier le fichier de projet.** En bas du fichier, vous verrez le code qui crée et met à jour votre dossier zip lorsque l'application est créée :

``` xml
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

### <a name="models"></a>Modèles

*PersonalTab.cs* présente un objet Message et des méthodes qui seront appelées à partir de *PersonalTabController* lorsqu'un utilisateur sélectionne un bouton dans *l'affichage PersonalTab.*

### <a name="views"></a>Affichages

#### <a name="home"></a>Accueil

ASP. NET Core traite les fichiers appelés *Index* comme la page d'accueil/par défaut du site. Lorsque l'URL de votre navigateur pointe vers la racine du site, *Index.cshtml* s'affiche en tant que page d'accueil de votre application.

#### <a name="shared"></a>Shared

Le markup *d'affichage partiel _Layout.cshtml* contient la structure de page globale de l'application et les éléments visuels partagés. Il référencera également la bibliothèque Teams.

### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la propriété ViewBag pour transférer dynamiquement des valeurs vers les affichages.

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* Ouvrez une invite de commandes à la racine du répertoire de votre projet et exécutez la commande suivante :

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* Ngrok écoute les demandes provenant d'Internet et les route vers votre application lorsqu'elle est en cours d'exécution sur le port 44325.  Il doit ressembler `https://y8rPrT2b.ngrok.io/` à *l'endroit où y8rPrT2b* est remplacé par votre URL HTTPS alpha-numérique ngrok.

* Veillez à conserver l'invite de commandes avec ngrok en cours d'exécution et à noter l'URL. Vous en aurez besoin ultérieurement.

* Vérifiez que *ngrok* fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l'URL HTTPS ngrok fournie dans la fenêtre d'invite de commandes.

> [! CONSEIL] Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d'exécution pour effectuer ce démarrage rapide. Si vous devez arrêter l'exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d'exécution.** Il continuera à écouter et reprendra le routage de la demande de votre application au redémarrage dans Visual Studio. Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.

### <a name="run-your-application"></a>Exécuter votre application

* Dans Visual Studio **appuyez sur F5** ou choisissez **Démarrer le débogage** à partir du menu **Débogage de votre** application.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
