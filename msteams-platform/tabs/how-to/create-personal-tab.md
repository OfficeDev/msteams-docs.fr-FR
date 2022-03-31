---
title: Créer un onglet personnel
author: laujan
description: Guide de démarrage rapide pour créer un onglet personnel avec le générateur Yeoman, ASP.NET Core ou ASP.NET Core MVC pour Microsoft Teams à l’aide de Node.js et mettre à jour le manifeste de l’application.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET du magasin d’autorisations de domaine de conversation appmanifest du package MVC
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 43302047a3c5712a17e2bc506eca2eeb350db825
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571363"
---
# <a name="create-a-personal-tab"></a>Créer un onglet personnel

Les onglets personnels, ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés au volet gauche pour faciliter l’accès. Vous pouvez également [réorder et](#reorder-static-personal-tabs) ajouter des [`registerOnFocused` API](#add-registeronfocused-api-for-tabs-or-personal-apps) pour les onglets personnels.

Assurez-vous que vous avez tous les [prérequis pour](~/tabs/how-to/tab-requirements.md) créer votre onglet personnel.

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Créer un onglet personnel avec Node.js

Pour créer un onglet personnel avec Node.js

1. À l’invite de commandes, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant la commande suivante après avoir installé le Node.js :

    ```cmd
    npm install yo gulp-cli --global
    ```

1. À l’invite de commandes, installez Microsoft Teams générateur d’application en entrant la commande suivante :

    ```cmd
    npm install generator-teams --global
    ```

Voici les étapes à suivre pour créer un onglet personnel :

1. [Générer votre application avec un onglet personnel](#generate-your-application-with-a-personal-tab)
1. [Ajouter une page de contenu à l’onglet personnel](#add-a-content-page-to-the-personal-tab)
1. [Créer votre package d’application](#create-your-app-package)
1. [Créer et exécuter votre application](#build-and-run-your-application)
1. [Établir un tunnel sécurisé vers votre onglet personnel](#establish-a-secure-tunnel-to-your-tab)
1. [Télécharger votre application à Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. À l’invite de commandes, créez un répertoire pour votre onglet personnel.

1. Entrez la commande suivante dans votre nouveau répertoire pour démarrer le générateur Microsoft Teams App :

    ```cmd
    yo teams
    ```

1. Fournissez vos valeurs à une série de questions posées par Microsoft Teams générateur d’application pour mettre à jour votre **fichier manifest.json**.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams générateur" border="true":::

    <details>
    <summary><b>Série de questions pour mettre à jour votre fichier manifest.json</b></summary>

    * **Quel est le nom de votre solution ?**

      Le nom de la solution est le nom de votre projet. Vous pouvez accepter le nom suggéré en sélectionnant **Entrée**.

    * **Où souhaitez-vous placer les fichiers ?**

      Vous êtes actuellement dans votre répertoire de projet. **Sélectionnez Entrée**.

    * **Titre de votre Microsoft Teams d’application ?**

      Le titre est le nom de votre package d’application et est utilisé dans le manifeste et la description de l’application. Entrez un titre ou **sélectionnez Entrée** pour accepter le nom par défaut.

    * **Votre nom (d’entreprise) ? (32 caractères maximum)**

      Le nom de votre société sera utilisé dans le manifeste de l’application. Entrez un nom de société ou **sélectionnez Entrée** pour accepter le nom par défaut.

    * **Quelle version de manifeste souhaitez-vous utiliser ?**

      Sélectionnez le schéma par défaut.

    * **La échafaudage rapide ? (Y/n)**

      La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.

    * **Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**

      Ce champ n’est pas obligatoire et ne doit être utilisé que si vous faites déjà partie de [Microsoft Partner Network](https://partner.microsoft.com).

    * **Que voulez-vous ajouter à votre projet ?**

      **Sélectionnez ( &ast; ) Un onglet**.

    * **L’URL dans laquelle vous hébergez cette solution ?**

      Par défaut, le générateur suggère une URL de sites web Azure. Vous testez uniquement votre application localement, de sorte qu’une URL valide n’est pas nécessaire.

    * **Voulez-vous afficher un indicateur de chargement lors du chargement de votre application/onglet ?**

      Choisissez **de ne** pas inclure d’indicateur de chargement lors du chargement de votre application ou de votre onglet. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous que les applications personnelles soient restituées sans barre d’en-tête d’onglet ?**

      Choisissez **de** ne pas inclure d’applications personnelles à restituer sans barre d’en-tête d’onglet. La valeur par défaut est non, entrez **n**.

    * **Souhaitez-vous inclure l’infrastructure test et les tests initiaux ? (y/N)**

      Choisissez **de ne** pas inclure d’infrastructure de test pour ce projet. La valeur par défaut est non, entrez **n**.

    * **Souhaitez-vous inclure la prise en charge esLint ? (y/N)**

      Choisissez de ne pas inclure la prise en charge esLint. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous utiliser Azure Applications Informations pour la télémétrie ? (y/N)**

      Choisissez **de ne** pas inclure [Azure Application Informations](/azure/azure-monitor/app/app-insights-overview). La valeur par défaut est non ; entrez **n**.

    * **Nom de l’onglet par défaut (16 caractères maximum) ?**

      Nommez votre onglet. Ce nom d’onglet est utilisé dans l’ensemble de votre projet en tant que composant de chemin d’URL ou de fichier.

    * **Quel type d’onglet voulez-vous créer ?**

      Utilisez les touches de direction pour sélectionner **Personnel (statique).**

    * **Avez-vous besoin Microsoft Azure Active Directory (Azure AD) prise en charge de l’sign-on unique pour l’onglet ?**

      Choisissez **de** ne pas inclure Azure AD prise en charge de l’sign-on unique pour l’onglet. La valeur par défaut est oui, entrez **n**.

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Ajouter une page de contenu à l’onglet personnel

Créez une page de contenu et mettez à jour les fichiers existants de l’application d’onglet personnel :

1. Créez un **fichierpersonal.html** dans votre Visual Studio Code avec le markup suivant :

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. **Enregistrezpersonal.html** dans le dossier **public de votre** application à l’emplacement suivant :

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. **Ouvrez manifest.json à** partir de l’emplacement suivant dans votre Visual Studio Code :

    ```
     ./src/manifest/manifest.json
    ```

1. Ajoutez ce qui suit au tableau `staticTabs` vide (`staticTabs":[]`) et ajoutez l’objet JSON suivant :

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

    > [!IMPORTANT]
    > Le composant **de chemin d’accès yourDefaultTabNameTab** est la valeur que vous avez entrée dans le générateur pour le nom de l’onglet par **défaut, ainsi** que le mot **Tab**.
    >
    > Par exemple : DefaultTabName est **MyTab** puis **/MyTabTab/**

1. Mettez à **jour le composant de chemin d’accès contentURL** **yourDefaultTabNameTab** avec votre nom d’onglet réel.

1. Enregistrez le fichier **manifest.json mis à** jour.

1. **Ouvrez Tab.ts** dans votre Visual Studio Code à partir du chemin d’accès suivant pour fournir votre page de contenu dans un IFrame :

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Ajoutez ce qui suit à la liste descorateurs IFrame :

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Enregistrez le fichier mis à jour. Le code de l’onglet est terminé.

### <a name="create-your-app-package"></a>Créer votre package d’application

Vous devez avoir un package d’application pour créer et exécuter votre application dans Teams. Le package d’application est créé par le biais d’une tâche Gulp qui valide le **fichier manifest.json** et génère le dossier zip dans le répertoire **./package** . À l'invite de commandes, tapez la commande suivante :

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Créer et exécuter votre application

#### <a name="build-your-application"></a>Créer votre application

Entrez la commande suivante à l’invite de commandes pour transpiler votre solution dans **le dossier ./dist** :

```cmd
gulp build
```

#### <a name="run-your-application"></a>Exécuter votre application

1. À l’invite de commandes, entrez la commande suivante pour démarrer un serveur web local :

    ```cmd
    gulp serve
    ```

1. Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur pour afficher la page d’accueil de votre application.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Onglet par défaut" border="true":::

1. Parcourir `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`, pour afficher votre onglet personnel.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Onglet html par défaut" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes, quittez l’environnement localhost et entrez la commande suivante pour établir un tunnel sécurisé sur votre onglet :

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet est téléchargé vers Microsoft Teams via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session tunnel.

### <a name="upload-your-application-to-teams"></a>Télécharger votre application à Teams

1. Go to Microsoft Teams and select **Store**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. **Sélectionnez Gérer vos applications**
1. **Sélectionnez Publier une application et** **Télécharger une application personnalisée**.

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Télécharger application personnalisée" border="true":::

1. Accédez au répertoire de votre projet, accédez au dossier **./package** , sélectionnez le dossier zip, puis choisissez **Ouvrir**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Ajout de votre onglet personnel" border="true":::

1. **Sélectionnez Ajouter** dans la fenêtre pop-up. Votre onglet est téléchargé vers Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Onglet personnel chargé" border="true":::

1. Dans le volet gauche du Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF; puis choisissez votre application téléchargée pour afficher votre onglet personnel.

   Vous avez créé et ajouté votre onglet personnel dans Teams.
  
   Comme vous avez votre onglet personnel dans Teams, vous pouvez également [réorder](#reorder-static-personal-tabs) [`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps) et ajouter une API pour votre onglet personnel.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Créer un onglet personnel avec ASP.NET Core

Vous pouvez créer un onglet personnel personnalisé à l’aide de C# et ASP.NET Core pages De la page Page. Pour créer un onglet personnel avec ASP.NET Core

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes à suivre pour créer un onglet personnel :

1. [Générer votre application avec un onglet personnel](#generate-your-application-with-a-personal-tab-1)
1. [Mettre à jour et exécuter votre application](#update-and-run-your-application)
1. [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-1)
1. [Mettre à jour votre package d’application avec le Portail du développeur](#update-your-app-package-with-developer-portal)
1. [Afficher un aperçu de votre application dans Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. Ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution**.

1. Go to Microsoft-Teams-Samplessamplestab-personalrazor-csharp  >  >  >  folder and open **PersonalTab.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou démarrez le  débogage à partir du menu **Débogage** de votre application pour vérifier si l’application s’est chargée correctement. Dans un navigateur, allez aux URL suivantes :

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Passer en revue le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir ASP.NET Core modèle vide d’application web 3.1 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendances `ConfigureServices()` . En outre, le modèle vide n’active pas la portion de contenu statique par défaut, `Configure()` de sorte que l’intermédiaire des fichiers statiques est ajouté à la méthode à l’aide du code suivant :

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

#### <a name="wwwroot-folder"></a>dossier wwwroot

Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* Icône **en couleurs complètes** de 192 x 192 pixels.
* Icône **de plan transparente de** 32 x 32 pixels.
* Fichier **manifest.json** qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams. Microsoft Teams charge `contentUrl` le spécifié dans votre manifeste, l’incorpore dans un iframe\> <et l’restituer dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier**. À la fin du fichier, vous pouvez voir le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :

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

</details>

### <a name="update-and-run-your-application"></a>Mettre à jour et exécuter votre application

1. Go to the **PagesShared**  >  folder and open **_Layout.cshtml** and add the following to the `<head>` tags section:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. **Ouvrez PersonalTab.cshtml** à partir du dossier **Pages**, ajoutez `microsoftTeams.initialize()` les balises `<script>` et enregistrez.

1. Dans Visual Studio, sélectionnez **F5** ou démarrez **le débogage** à partir du menu **Débogage de votre** application.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante pour établir un tunnel sécurisé sur votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec le Portail du développeur

1. Go to **Developer portal** in Teams.

1. **Ouvrez applications** et sélectionnez **Importer l’application**.

1. Le nom de votre package d’application **esttab.zip**. Il est disponible dans le chemin d’accès suivant :

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **Sélectionneztab.zip** et ouvrez-le dans le Portail du développeur.

1. Un **ID d’application par défaut** est créé et rempli dans la section **Informations de** base.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **Les informations du** développeur, ajoutez les détails requis et dans le site web (doit être une **URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans **les URL d’application**, mettez à jour la politique de confidentialité `https://<yourngrokurl>/privacy` et les conditions d’utilisation pour `https://<yourngrokurl>/tou` et enregistrer.

1. Dans **les fonctionnalités de** l’application, sélectionnez Application personnelle, entrez le nom et mettez à jour **l’URL de** contenu avec `https://<yourngrokurl>/personalTab`. Laissez le champ URL du site web vide.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. **Sélectionnez Aperçu dans Teams** la barre d’outils du Portail du développeur. Le portail du développeur vous informe que votre application est correctement rechargée.

1. **Sélectionnez Gérer vos applications**. Votre application est répertoriée dans les applications téléchargées de côté.

1. Recherchez votre application à l’aide de la recherche, sélectionnez les trois points dans sa ligne.

1. Sélectionnez **l’option** Afficher. La page **Ajouter** s’affiche pour votre application.

1. **Sélectionnez Ajouter** pour charger l’onglet sur Teams. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Onglet par défaut" border="true":::

   Vous avez créé et ajouté votre onglet personnel dans Teams.
  
   Comme vous avez votre onglet personnel dans Teams, vous pouvez également [réorder](#reorder-static-personal-tabs) [`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps) et ajouter une API pour votre onglet personnel.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Créer un onglet personnel avec ASP.NET Core MVC

Vous pouvez créer un onglet personnel personnalisé à l’aide C# et ASP.NET Core MVC. Pour créer un onglet personnel avec ASP.NET Core MVC

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes à suivre pour créer un onglet personnel :

1. [Générer votre application avec un onglet personnel](#generate-your-application-with-a-personal-tab-2)
1. [Mettre à jour et exécuter l’application](#update-and-run-your-application-1)
1. [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-2)
1. [Mettre à jour votre package d’application avec le Portail du développeur](#update-your-app-package-with-developer-portal-1)
1. [Afficher un aperçu de votre application dans Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. Ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution**.

1. Go to Microsoft-Teams-Samplessamplestab-personalmvc-csharp  >  >  >  folder and open **PersonalTabMVC.sln** in Visual Studio.

1. Dans Visual Studio, sélectionnez **F5** ou démarrez le  débogage à partir du menu **Débogage** de votre application pour vérifier si l’application s’est chargée correctement. Dans un navigateur, allez aux URL suivantes :

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Passer en revue le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir ASP.NET Core modèle vide d’application web 3.1 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendances `ConfigureServices()` . En outre, le modèle vide n’active pas la portion de contenu statique par défaut, `Configure()` de sorte que l’intermédiaire des fichiers statiques est ajouté à la méthode à l’aide du code suivant :

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

#### <a name="wwwroot-folder"></a>dossier wwwroot

Dans ASP.NET Core, le dossier racine web est l’endroit où l’application recherche des fichiers statiques.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* Icône **en couleurs complètes** de 192 x 192 pixels.
* Icône **de plan transparente de** 32 x 32 pixels.
* Fichier **manifest.json** qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams. Microsoft Teams charge le `contentUrl` spécifié dans votre manifeste, l’incorpore dans un IFrame et l’restituer dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans la Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :

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

#### <a name="models"></a>Modèles

**PersonalTab.cs** présente un objet message et les méthodes qui sont appelées à partir de **PersonalTabController** lorsqu’un utilisateur sélectionne un bouton dans **l’affichage PersonalTab** .

#### <a name="views"></a>Affichages

Ces affichages sont les différents dans ASP.NET Core MVC :

* Accueil : ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

* Partagé : le contrôle de **_Layout.cshtml contient** la structure de page globale de l’application et les éléments visuels partagés. Il fait également référence à la Teams bibliothèque.

#### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la propriété `ViewBag` pour transférer dynamiquement des valeurs vers les affichages.

</details>

### <a name="update-and-run-your-application"></a>Mettre à jour et exécuter votre application

1. Go to **ViewsShared**  >  folder and open **_Layout.cshtml**, and add the following to the `<head>` tags section:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. **Ouvrez PersonalTab.cshtml** à partir du **dossier ViewsPersonalTab** `microsoftTeams.initialize()`  > , ajoutez-le à l’intérieur des `<script>` balises et enregistrez- le.

1. Dans Visual Studio, sélectionnez **F5** ou démarrez **le débogage** à partir du menu **Débogage de votre** application.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante pour établir un tunnel sécurisé sur votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec le Portail du développeur

1. Go to **Developer portal** in Teams.

1. **Ouvrez applications** et sélectionnez **Importer l’application**.

1. Le nom de votre package d’application **esttab.zip**. Il est disponible dans le chemin d’accès suivant :

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **Sélectionneztab.zip** et ouvrez-le dans le Portail du développeur.

1. Un **ID d’application par défaut** est créé et rempli dans la section **Informations de** base.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **Les informations du** développeur, ajoutez les détails requis et dans le site web (doit être une **URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans **les URL d’application**, mettez à jour la politique de confidentialité `https://<yourngrokurl>/privacy` et les conditions d’utilisation pour `https://<yourngrokurl>/tou` et enregistrer.

1. Dans **les fonctionnalités de** l’application, sélectionnez Application personnelle, entrez le nom et mettez à jour **l’URL de** contenu avec `https://<yourngrokurl>/personalTab`. Laissez le champ URL du site web vide.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. **Sélectionnez Aperçu dans Teams** la barre d’outils du Portail du développeur. Le portail du développeur vous informe que votre application est correctement rechargée.

1. **Sélectionnez Gérer vos applications**. Votre application est répertoriée dans les applications téléchargées de côté.

1. Recherchez votre application à l’aide de la recherche, sélectionnez les trois points dans sa ligne.

1. **Sélectionnez l’option** Afficher. La page **Ajouter** s’affiche pour votre application.

1. **Sélectionnez Ajouter** pour charger l’onglet sur Teams. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Onglet personnel" border="true":::
  
   Vous avez créé et ajouté votre onglet personnel dans Teams.

   Comme vous avez votre onglet personnel dans Teams, vous pouvez également [réorder](#reorder-static-personal-tabs) [`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps) et ajouter une API pour votre onglet personnel.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Réordesser les onglets personnels statiques

À partir de la version de manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle. En particulier, un développeur peut déplacer l’onglet de **conversation du bot** , qui est toujours en première position par défaut, n’importe où dans l’en-tête de l’onglet de l’application personnelle. Deux mots clés d’onglet `entityId` réservés sont déclarés, **conversations** et **autres.**

Si vous créez un bot avec une **étendue** personnelle, il apparaît par défaut dans le premier onglet d’une application personnelle. Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, **conversations**. **L’onglet conversation** s’affiche sur le web ou sur le bureau en fonction de l’endroit où vous ajoutez **l’onglet de conversation** dans le `staticTabs` tableau.

``` JSON

{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}

```

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>Ajouter une `registerOnFocused` API pour les onglets ou les applications personnelles

L’API `registerOnFocused` du SDK vous permet d’utiliser un clavier sur Teams. Vous pouvez revenir à une application personnelle et maintenir le focus sur un onglet ou une application personnelle à l’aide des touches Ctrl, Shift et F6. Par exemple, vous pouvez vous éloigner de l’application personnelle pour rechercher quelque chose, puis revenir à l’application personnelle ou utiliser Ctrl+F6 pour contourner les endroits requis.

Le code suivant fournit un exemple de définition de handler `registerFocusEnterHandler` sur le SDK lorsque le focus doit être renvoyé à l’onglet ou à l’application personnelle :

``` C#

export function registerFocusEnterHandler(handler: (navigateForward: boolean) => void): 
void {
  HandlersPrivate.focusEnterHandler = handler;
  handler && sendMessageToParent('registerHandler', ['focusEnter']);
}
function handleFocusEnter(navigateForward: boolean): void
 {
  if (HandlersPrivate.focusEnterHandler)
   {
    HandlersPrivate.focusEnterHandler(navigateForward);
  }
}

```

Une fois que le handler `focusEnter`est déclenché avec le mot clé, le handler `registerFocusEnterHandler` `focusEnterHandler` est appelé avec une fonction de rappel qui prend un paramètre appelé `navigateForward`. La valeur de `navigateForward` détermine le type d’événements. Il `focusEnterHandler` est appelé uniquement par Ctrl+F6 et non par la touche de tabulation.
Les clés utiles pour les événements de déplacement Teams sont les suivantes :

* Événement Forward : touches Ctrl+F6
* Événement backward : touches Ctrl+Shift+F6

``` C#

case 'focusEnter':     
this.registerFocusEnterHandler((navigateForward: boolean = true) => {
this.sdkWindowMessageHandler.sendRequestMessage(this.frame, this.constants.SdkMessageTypes.focusEnter, [navigateForward]);
// Set focus on iframe or webview
if (this.frame && this.frame.sourceElem) {
  this.frame.sourceElem.focus();
}
return true;
});
}

// callback function to be passed to the handler
private focusEnterHandler: (navigateForward: boolean) => boolean;

// function that gets invoked after handler is registered.
private registerFocusEnterHandler(focusEnterHandler: (navigateForward: boolean) => boolean): void {
this.focusEnterHandler = focusEnterHandler;
this.layoutService.registerAppFocusEnterCallback(this.focusEnterHandler);
}

```

### <a name="personal-app"></a>Application personnelle

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="Exemple d’options pour l’ajout de l’API registerOnFocussed" border="true":::

#### <a name="personal-app-forward-event"></a>Application personnelle : événement Forward

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="Exemple d’options pour l’ajout d’un déplacement de l’API registerOnFocussed" border="true":::

#### <a name="personal-app-backward-event"></a>Application personnelle : événement backward

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="Exemple d’options pour ajouter un déplacement arrière de l’API registerOnFocussed" border="true":::

### <a name="tab"></a>Onglet

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="Exemple d’options pour l’ajout de l’API registerOnFocussed pour l’onglet" border="true":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)
