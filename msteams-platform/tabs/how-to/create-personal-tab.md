---
title: Créer un onglet personnel
author: laujan
description: Guide de démarrage rapide pour créer un onglet personnel avec yeoman Generator, ASP.NET Core ou ASP.NET Core MVC pour Microsoft Teams à l’aide de Node.js et mettre à jour le manifeste de l’application.
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET magasin d’autorisations de domaine de conversation appmanifest de package MVC
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 6acb5e0adf24dca7538b6ceaca470b9b6c3126f2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111240"
---
# <a name="create-a-personal-tab"></a>Créer un onglet personnel

Les onglets personnels, ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés au volet gauche pour un accès facile. Vous pouvez également [réordonner](#reorder-static-personal-tabs) vos onglets personnels.

Vérifiez que vous disposez de tous les [conditions préalables](~/tabs/how-to/tab-requirements.md) pour créer votre onglet personnel.

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Créer un onglet personnel avec Node.js

1. À l’invite de commandes, installez les packages [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant la commande suivante après l’installation de Node.js :

    ```cmd
    npm install yo gulp-cli --global
    ```

1. À l’invite de commandes, installez le générateur d’applications Microsoft Teams en entrant la commande suivante :

    ```cmd
    npm install generator-teams --global
    ```

Voici les étapes à suivre pour créer un onglet personnel :

1. [Générer votre application avec un onglet personnel](#generate-your-application-with-a-personal-tab)
1. [Ajouter une page de contenu à l’onglet personnel](#add-a-content-page-to-the-personal-tab)
1. [Créer votre package d’application](#create-your-app-package)
1. [Compiler et exécuter votre application](#build-and-run-your-application)
1. [Établir un tunnel sécurisé vers votre onglet personnel](#establish-a-secure-tunnel-to-your-tab)
1. [Charger votre application dans Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. À l’invite de commandes, créez un répertoire pour votre onglet personnel.

1. Entrez la commande suivante dans votre nouveau répertoire pour démarrer le générateur d’application Microsoft Teams :

    ```cmd
    yo teams
    ```

1. Fournissez vos valeurs à une série de questions posées par le générateur d’applications Microsoft Teams pour mettre à jour votre fichier `manifest.json`.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Générateur Teams" border="true":::

    <details>
    <summary><b>Série de questions pour mettre à jour votre fichier manifest.json</b></summary>

    * **Quel est le nom de votre solution ?**

      Le nom de la solution est le nom de votre projet. Vous pouvez accepter le nom suggéré en sélectionnant **Entrée**.

    * **Où souhaitez-vous placer les fichiers ?**

      Vous êtes actuellement dans le répertoire de votre projet. Ensuite, sélectionnez **Entrée**.

    * **Titre de votre projet d’application Microsoft Teams ?**

      Le titre est le nom de votre package d’application et est utilisé dans le manifeste et la description de l’application. Entrez un titre ou sélectionnez **Entrer** pour accepter le nom par défaut.

    * **Votre nom (société) ? (32 caractères maximum)**

      Le nom de votre entreprise sera utilisé dans le manifeste de l’application. Entrez un nom de société ou sélectionnez **Entrer** pour accepter le nom par défaut.

    * **Quelle version du manifeste voulez-vous utiliser ?**

      Sélectionnez le schéma par défaut.

    * **Échafaudage rapide** : Oui

      La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.

    * **Entrez votre ID de partenaire Microsoft, le cas échéant : (laissez vide pour ignorer)**

      Ce champ n’est pas obligatoire et doit être utilisé uniquement si vous faites déjà partie du [Réseau de partenaire Microsoft](https://partner.microsoft.com).

    * **Que voulez-vous ajouter à votre projet ?**

      Sélectionnez **( &ast; ) Onglet**.

    * **URL dans laquelle vous hébergez cette solution ?**

      Par défaut, le générateur suggère une URL de sites web Azure. Vous testez uniquement votre application localement, donc une URL valide n’est pas nécessaire.

    * **Voulez-vous afficher un indicateur de chargement lorsque votre application/onglet se charge ?**

      Choisissez ne **pas** inclure un indicateur de chargement lors du chargement de votre application ou onglet. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous que les applications personnelles soient restituées sans barre d’en-tête d’onglet ?**

      Choisissez ne **pas** inclure les applications personnelles à afficher sans barre d’en-tête d’onglet. Valeur par défaut est non, entrez **n**.

    * **Voulez-vous inclure l’infrastructure de test et les tests initiaux ? (y/N)**

      Choisissez **pas** pour inclure une infrastructure de test pour ce projet. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous inclure la prise en charge d’ESLint ? (y/N)**

      Choisissez de ne pas inclure la prise en charge d’ESLint. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous utiliser Azure Applications Insights pour la télémétrie ? (y/N)**

      Choisissez ne **pas** inclure [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview). La valeur par défaut est Non ; entrez **n**.

    * **Nom de l’onglet par défaut (16 caractères maximum) ?**

      Nommez votre onglet. Ce nom d’onglet est utilisé dans l’ensemble de votre projet en tant que composant de chemin d’URL ou de fichier.

    * **Quel type d’onglet voulez-vous créer ?**

      Utilisez les touches de direction pour sélectionner onglet **Personnel (statique)** .

    * **Avez-vous besoin de la prise en charge de l’authentification unique Microsoft Azure Active Directory (Azure AD) pour l’onglet ?**

      Choisissez ne **pas** inclure la prise en charge de l’authentification unique Azure AD pour l’onglet. La valeur par défaut est Oui, entrez **n**.

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Ajouter une page de contenu à l’onglet personnel

Créez une page de contenu et mettez à jour les fichiers existants de l’application d’onglet personnel :

1. Créez un fichier **personal.html** dans votre Visual Studio Code avec le balisage suivant :

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

1. Enregistrez **personal.html** dans le dossier **public** de votre application à l’emplacement suivant :

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Ouvrez `manifest.json` à partir de l’emplacement suivant dans votre Visual Studio Code :

    ```
     ./src/manifest/manifest.json
    ```

1. Ajoutez ce qui suit au tableau `staticTabs` vide (`staticTabs":[]`) et ajoutez l’objet JSON suivant :

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{PUBLIC_HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{PUBLIC_HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

    > [!IMPORTANT]
    > Le composant de chemin d’accès **yourDefaultTabNameTab** est la valeur que vous avez entrée dans le générateur pour **nom de tabulation par défaut** plus le mot **Tab**.
    >
    > Par exemple : DefaultTabName est **MyTab** then **/MyTabTab/**

1. Mettez à jour le composant de chemin d’accès **contentURL****yourDefaultTabNameTab** avec le nom de votre onglet réel.

1. Enregistrez le fichier `manifest.json` mis à jour.

1. Ouvrez **Tab.ts** dans votre Visual Studio Code à partir du chemin suivant pour fournir votre page de contenu dans un IFrame :

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Ajoutez ce qui suit à la liste des éléments décoratifs IFrame :

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Enregistrez le fichier mis à jour. Votre code d’onglet est terminé.

### <a name="create-your-app-package"></a>Créer votre package d’application

Vous devez disposer d’un package d’application pour générer et exécuter votre application dans Teams. Le package d’application est créé via une tâche gulp qui valide le fichier `manifest.json` et génère le dossier zip dans le répertoire `./package`. À l’invite de commandes, utilisez la commande `gulp manifest`.

### <a name="build-and-run-your-application"></a>Générer et exécuter votre application

#### <a name="build-your-application"></a>Générer votre application

Entrez la commande suivante à l’invite de commandes pour transpiler votre solution dans le dossier **./dist** :

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

1. Parcourez `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` pour afficher votre onglet personnel.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Onglet HTML par défaut" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes, quittez l’hôte local et entrez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois votre onglet chargé dans Microsoft Teams via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session de tunnel.

### <a name="upload-your-application-to-teams"></a>Charger votre application dans Teams

1. Accédez à Microsoft Teams et sélectionnez **Apps**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Sélectionnez **Gérer vos applications** et **Charger une application personnalisée**.
1. Accédez au répertoire de votre projet, accédez au dossier **./package** , sélectionnez le dossier zip, puis choisissez **Ouvrir**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Ajouter votre onglet personnel" border="true":::

1. Sélectionnez **Ajouter** dans la boîte de dialogue. Votre onglet est chargé dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Onglet Personnel chargé" border="true":::

1. Dans le volet gauche de Teams, sélectionnez des points de suspension &#x25CF;&#x25CF;&#x25CF; puis choisissez votre application chargée pour afficher votre onglet personnel.

   Vous avez créé et ajouté votre onglet personnel dans Teams.
  
   Comme vous disposez de votre onglet personnel dans Teams, vous pouvez également [réordonner](#reorder-static-personal-tabs) votre onglet personnel.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>Créer un onglet personnel avec ASP.NET Core

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes à suivre pour créer un onglet personnel :

1. [Générer votre application avec un onglet personnel](#generate-your-application-with-a-personal-tab-1)
1. [Mettre à jour et exécuter votre application](#update-and-run-your-application)
1. [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-1)
1. [Mettre à jour votre package d’application avec le Portail des développeurs](#update-your-app-package-with-developer-portal)
1. [Prévisualiser votre application dans Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. Ouvrez Visual Studio et sélectionnez **Ouvrir un projet ou une solution**.

1. Accédez à **Modèles de Microsoft Teams** > **modèles** > **tab-personal** > **dossier razor-csharp** et ouvrez **PersonalTab.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** de votre application pour vérifier si l’application s’est correctement chargée. Dans un navigateur, accédez aux URL suivantes :

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Examiner le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application web ASP.NET Core 3.1 avec la case à cocher **Avancé – Configurer pour HTTPS** sélectionnée lors de l’installation. Les services MVC sont inscrits par la méthode `ConfigureServices()` de l’infrastructure d’injection de dépendances. En outre, le modèle vide n’active pas le traitement du contenu statique par défaut. Par conséquent, l’intergiciel de fichiers statiques est ajouté à la méthode `Configure()` à l’aide du code suivant :

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

Dans ASP.NET Core, le dossier racine web est l’emplacement où l’application recherche des fichiers statiques.

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core traite les fichiers appelés **Index** comme page d’accueil ou par défaut pour le site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* Icône de couleur mesurant 192 x 192 pixels.
* Icône de contour transparent mesurant 32 x 32 pixels.
* Un fichier `manifest.json` qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet dans Teams. Microsoft Teams charge le `contentUrl` spécifié dans votre manifeste, l’incorpore dans un <iframe\> et le restitue dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier le fichier projet**. À la fin du fichier, vous pouvez voir le code suivant qui crée et met à jour votre dossier zip lors de la génération de l’application :

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

1. Ouvrez Visual Studio Explorateur de solutions et accédez au dossier **Pages** > **Shared**, ouvrez **_Layout.cshtml**, puis ajoutez les éléments suivants à la section des balises `<head>` :

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Dans Visual Studio Explorateur de solutions ouvrir **PersonalTab.cshtml** à partir du dossier **Pages** et ajoutez `microsoftTeams.initialize()` dans les balises `<script>` et enregistrez.

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** de votre application.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine de votre répertoire de projet, exécutez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec Developer Portal

1. Accédez à [**Portail des développeurs**](https://dev.teams.microsoft.com/home).

1. Ouvrez **Applications** et sélectionnez **Importer une application**.

1. Le nom du fichier de package d’application est `tab.zip` et il est disponible dans `/bin/Debug/netcoreapp3.1/tab.zip` chemin d’accès.

1. Sélectionnez `tab.zip` et ouvrez-le dans le Developer Portal.

1. Un **ID d’application** par défaut est créé et rempli dans la section **Informations de base**.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **information du développeur**, ajoutez les détails requis et dans **Le site web (doit être une URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans les **URL d’application**, mettez à jour la Stratégie de confidentialité vers `https://<yourngrokurl>/privacy` et Conditions d’utilisation vers `https://<yourngrokurl>/tou`, puis enregistrez.

1. Dans **Fonctionnalités de l’application**, sélectionnez **Application personnelle** > **Créer votre premier onglet d’application personnelle** et entrez le nom et mettez à jour **L’URL du content** avec `https://<yourngrokurl>/personalTab`. Laissez le champ URL du site web vide et sélectionnez **Context** comme personalTab dans la liste déroulante et **Ajouter**.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. Sélectionnez **Aperçu dans Teams** dans la barre d’outils Portail des développeurs, le Portail des développeurs vous informe que votre application a été chargée correctement. La page **Ajouter** s’affiche pour votre application dans Teams.

1. Sélectionnez **Ajouter** pour charger l’onglet dans Teams. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Onglet par défaut" border="true":::

   Vous avez créé et ajouté votre onglet personnel dans Teams.
  
   Comme vous disposez de votre onglet personnel dans Teams, vous pouvez également [réordonner](#reorder-static-personal-tabs) votre onglet personnel.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>Créer un onglet personnel avec ASP.NET Core MVC

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes à suivre pour créer un onglet personnel :

1. [Générer votre application avec un onglet personnel](#generate-your-application-with-a-personal-tab-2)
1. [Mettre à jour et exécuter l’application](#update-and-run-your-application-1)
1. [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-2)
1. [Mettre à jour votre package d’application avec le Portail des développeurs](#update-your-app-package-with-developer-portal-1)
1. [Prévisualiser votre application dans Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. Ouvrez Visual Studio et sélectionnez **Ouvrir un projet ou une solution**.

1. Accédez à **Modèles de Microsoft Teams** > **modèles** > **tab-personal** > **dossier mvc-csharp** et ouvrez **PersonalTabMVC.sln** dans Visual Studio.

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** de votre application pour vérifier si l’application s’est correctement chargée. Dans un navigateur, accédez aux URL suivantes :

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Examiner le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application web ASP.NET Core 3.1 avec la case à cocher **Avancé – Configurer pour HTTPS** sélectionnée lors de l’installation. Les services MVC sont inscrits par la méthode `ConfigureServices()` de l’infrastructure d’injection de dépendances. En outre, le modèle vide n’active pas le traitement du contenu statique par défaut. Par conséquent, l’intergiciel de fichiers statiques est ajouté à la méthode `Configure()` à l’aide du code suivant :

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

Dans ASP.NET Core, le dossier racine web est l’emplacement où l’application recherche des fichiers statiques.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* **Icône de couleur** mesurant 192 x 192 pixels.
* **Icône de contour transparent** mesurant 32 x 32 pixels.
* Un fichier `manifest.json` qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet dans Teams. Microsoft Teams charge le `contentUrl` spécifié dans votre manifeste, l’incorpore dans un IFrame et le restitue dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans le Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier le fichier projet**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lors de la génération de l’application :

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

**PersonalTab.cs** présente un objet de message et des méthodes appelés à partir de **PersonalTabController** lorsqu’un utilisateur sélectionne un bouton dans l’affichage **PersonalTab**.

#### <a name="views"></a>Affichages

Ces vues sont les différentes vues dans ASP.NET Core MVC :

* Accueil : ASP.NET Core traite les fichiers appelés **Index** comme page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

* Partagé : le balisage de vue partielle **_Layout.cshtml** contient la structure de page globale de l’application et les éléments visuels partagés. Il référence également la bibliothèque Teams.

#### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la propriété `ViewBag` pour transférer dynamiquement des valeurs vers les vues.

</details>

### <a name="update-and-run-your-application"></a>Mettre à jour et exécuter votre application

1. Ouvrez Visual Studio Explorateur de solutions et accédez au dossier **Vues** > **Shared**, ouvrez **_Layout.cshtml**, puis ajoutez les éléments suivants à la section des balises `<head>` :

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Dans Visual Studio Explorateur de solutions ouvrir **PersonalTab.cshtml** à partir du dossier **Vues** > **PersonalTab** et ajoutez `microsoftTeams.initialize()` à l’intérieur des balises `<script>` et enregistrez.

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** de votre application.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine de votre répertoire de projet, exécutez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec Developer Portal

1. Accédez à [**Portail des développeurs**](https://dev.teams.microsoft.com/home).

1. Ouvrez **Applications** et sélectionnez **Importer une application**.

1. Le nom de votre package d’application est **tab.zip**. Il est disponible dans le chemin d’accès suivant :

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Sélectionnez **tab.zip** et ouvrez-le dans le Developer Portal.

1. Un **ID d’application** par défaut est créé et rempli dans la section **Informations de base**.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **information du développeur**, ajoutez les détails requis et dans **Le site web (doit être une URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans les **URL d’application**, mettez à jour la Stratégie de confidentialité vers `https://<yourngrokurl>/privacy` et Conditions d’utilisation vers `https://<yourngrokurl>/tou`, puis enregistrez.

1. Dans **Fonctionnalités de l’application**, sélectionnez **Application personnelle** > **Créer votre premier onglet d’application personnelle** et entrez le nom et mettez à jour **L’URL du content** avec `https://<yourngrokurl>/personalTab`. Laissez le champ URL du site web vide et sélectionnez **Context** comme personalTab dans la liste déroulante et **Ajouter**.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. Sélectionnez **Aperçu dans Teams** dans la barre d’outils Portail des développeurs, le Portail des développeurs vous informe que votre application a été chargée correctement. La page **Ajouter** s’affiche pour votre application dans Teams.

1. Sélectionnez **Ajouter** pour charger l’onglet dans Teams. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Onglet personnel" border="true":::
  
   Vous avez créé et ajouté votre onglet personnel dans Teams.

   Comme vous disposez de votre onglet personnel dans Teams, vous pouvez également [réordonner](#reorder-static-personal-tabs) votre onglet personnel.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Réorganiser les onglets personnels statiques

À compter de la version 1.7 du manifeste, les développeurs peuvent réorganiser tous les onglets de leur application personnelle. En particulier, un développeur peut déplacer l’onglet **bot chat**, qui est toujours défini par défaut sur la première position, n’importe où dans l’en-tête de l’onglet d’application personnelle. Deux mots clés `entityId` sont déclarés, **conversations** et **à propos de**.

Si vous créez un bot avec une étendue **personnel**, il apparaît par défaut à la première position de l’onglet dans une application personnelle. Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, **conversations**. L’onglet **conversation** s’affiche sur le web ou le bureau en fonction de l’emplacement où vous ajoutez l'onglet **conversation** dans le tableau `staticTabs`.

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

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Voir aussi

* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)
* [Partager dans Teams à partir d’une application ou d’un onglet personnel](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
