---
title: Créer un onglet personnel
author: laujan
description: Guide de démarrage rapide pour créer un onglet personnel avec yeoman Generator, ASP.NET Core ou ASP.NET Core MVC pour Microsoft Teams à l’aide de Node.js et mettre à jour le manifeste de l’application.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET magasin d’autorisations de domaine de conversation appmanifest de package MVC
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 40afdd1692b0f5d7c99eaaf228969ba8c95ba20b
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737213"
---
# <a name="create-a-personal-tab"></a>Créer un onglet personnel

Les onglets personnels, ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés au volet gauche pour un accès facile. Vous pouvez également [réorganiser](#reorder-static-personal-tabs) et ajouter [`registerOnFocused` l’API](#add-registeronfocused-api-for-tabs-or-personal-apps) pour les onglets personnels.

Assurez-vous que vous disposez de tous les [prérequis](~/tabs/how-to/tab-requirements.md) pour créer votre onglet personnel.

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Créer un onglet personnel avec Node.js

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
1. [Ajouter une page de contenu à l’onglet Personnel](#add-a-content-page-to-the-personal-tab)
1. [Créer votre package d’application](#create-your-app-package)
1. [Générer et exécuter votre application](#build-and-run-your-application)
1. [Établir un tunnel sécurisé vers votre onglet personnel](#establish-a-secure-tunnel-to-your-tab)
1. [Télécharger votre application à Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. À l’invite de commandes, créez un répertoire pour votre onglet personnel.

1. Entrez la commande suivante dans votre nouveau répertoire pour démarrer le générateur d’application Microsoft Teams :

    ```cmd
    yo teams
    ```

1. Fournissez vos valeurs à une série de questions posées par Microsoft Teams générateur d’applications pour mettre à jour votre `manifest.json` fichier.

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="générateur Teams" border="true":::

    <details>
    <summary><b>Série de questions pour mettre à jour votre fichier manifest.json</b></summary>

    * **Quel est le nom de votre solution ?**

      Le nom de la solution est le nom de votre projet. Vous pouvez accepter le nom suggéré en sélectionnant **Entrée**.

    * **Où souhaitez-vous placer les fichiers ?**

      Vous êtes actuellement dans le répertoire de votre projet. Sélectionnez **Entrée**.

    * **Titre de votre projet d’application Microsoft Teams ?**

      Le titre est le nom de votre package d’application et est utilisé dans le manifeste et la description de l’application. Entrez un titre ou **sélectionnez Entrée** pour accepter le nom par défaut.

    * **Votre nom (entreprise) ? (32 caractères maximum)**

      Le nom de votre entreprise sera utilisé dans le manifeste de l’application. Entrez un nom d’entreprise ou **sélectionnez Entrée** pour accepter le nom par défaut.

    * **Quelle version de manifeste souhaitez-vous utiliser ?**

      Sélectionnez le schéma par défaut.

    * **Un échafaudage rapide ? (Y/n)**

      La valeur par défaut est Oui; entrez **n** pour entrer votre ID de partenaire Microsoft.

    * **Entrez votre ID de partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**

      Ce champ n’est pas obligatoire et doit être utilisé uniquement si vous faites déjà partie du [Microsoft Partner Network](https://partner.microsoft.com).

    * **Que voulez-vous ajouter à votre projet ?**

      Sélectionnez **( &ast; ) Un onglet**.

    * **URL dans laquelle vous hébergerez cette solution ?**

      Par défaut, le générateur suggère une URL de sites web Azure. Vous testez uniquement votre application localement, donc une URL valide n’est pas nécessaire.

    * **Voulez-vous afficher un indicateur de chargement lorsque votre application/onglet se charge ?**

      Choisissez de **ne pas** inclure d’indicateur de chargement lorsque votre application ou onglet se charge. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous que les applications personnelles soient restituées sans barre d’en-tête d’onglet ?**

      Choisissez de **ne pas** inclure d’applications personnelles à afficher sans barre d’en-tête d’onglet. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous inclure l’infrastructure de test et les tests initiaux ? (y/N)**

      Choisissez de **ne pas** inclure de framework de test pour ce projet. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous inclure le support ESLint ? (y/N)**

      Choisissez de ne pas inclure la prise en charge d’ESLint. La valeur par défaut est non, entrez **n**.

    * **Voulez-vous utiliser Azure Applications Informations pour la télémétrie ? (y/N)**

      Choisissez de **ne pas** inclure [Azure Application Informations](/azure/azure-monitor/app/app-insights-overview). La valeur par défaut est non; entrée **n**.

    * **Nom de tabulation par défaut (16 caractères maximum) ?**

      Nommez votre onglet. Ce nom d’onglet est utilisé dans l’ensemble de votre projet en tant que composant de chemin d’URL ou de fichier.

    * **Quel type de tabulation voulez-vous créer ?**

      Utilisez les touches de direction pour sélectionner **Personnel (statique).**

    * **Avez-vous besoin de la prise en charge de l’authentification unique Microsoft Azure Active Directory (Azure AD) pour l’onglet ?**

      Choisissez de **ne pas** inclure Azure AD prise en charge de l’authentification unique pour l’onglet. La valeur par défaut est Oui, entrez **n**.

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>Ajouter une page de contenu à l’onglet Personnel

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

1. Ajoutez ce qui suit au tableau vide `staticTabs` (`staticTabs":[]`) et ajoutez l’objet JSON suivant :

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
    > Le composant de chemin **d’accès yourDefaultTabNameTab** est la valeur que vous avez entrée dans le générateur pour le **nom de tabulation par défaut** , ainsi que le mot **Tab**.
    >
    > Par exemple : DefaultTabName est **MyTab** puis **/MyTabTab/**

1. Mettez à jour le composant de chemin **contentURL** **yourDefaultTabNameTab** avec le nom de votre onglet réel.

1. Enregistrez le fichier mis à jour `manifest.json` .

1. Ouvrez **Tab.ts** dans votre Visual Studio Code à partir du chemin d’accès suivant pour fournir votre page de contenu dans un IFrame :

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Ajoutez ce qui suit à la liste des décorateurs IFrame :

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. Enregistrez le fichier mis à jour. Votre code d’onglet est terminé.

### <a name="create-your-app-package"></a>Créer votre package d’application

Vous devez disposer d’un package d’application pour générer et exécuter votre application dans Teams. Le package d’application est créé via une tâche Gulp qui valide le `manifest.json` fichier et génère le dossier zip dans le `./package` répertoire. À l’invite de commandes, utilisez la commande `gulp manifest`.

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

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Onglet Par défaut" border="true":::

1. Parcourir `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`, pour afficher votre onglet personnel.

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="Onglet html par défaut" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes, quittez le localhost et entrez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été chargé dans Microsoft Teams via **ngrok** et enregistré avec succès, vous pouvez l’afficher dans Teams jusqu’à ce que votre session de tunnel se termine.

### <a name="upload-your-application-to-teams"></a>Télécharger votre application à Teams

1. Accédez à Microsoft Teams et sélectionnez **Applications**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Sélectionnez **Gérer vos applications** et **Télécharger une application personnalisée**.
1. Accédez au répertoire de votre projet, accédez au dossier **./package** , sélectionnez le dossier zip, puis choisissez **Ouvrir**.

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="Ajout de votre onglet personnel" border="true":::

1. Sélectionnez **Ajouter** dans la boîte de dialogue. Votre onglet est chargé dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="Onglet Personnel chargé" border="true":::

1. Dans le volet gauche de Teams, sélectionnez des points de suspension &#x25CF;&#x25CF;&#x25CF; , puis choisissez votre application chargée pour afficher votre onglet personnel.

   Vous avez maintenant créé et ajouté votre onglet personnel dans Teams.
  
   Comme vous disposez de votre onglet personnel dans Teams, vous pouvez également [réorganiser](#reorder-static-personal-tabs) et ajouter [`registerOnFocused` l’API](#add-registeronfocused-api-for-tabs-or-personal-apps) pour votre onglet personnel.

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
1. [Mettre à jour votre package d’application avec le portail des développeurs](#update-your-app-package-with-developer-portal)
1. [Afficher un aperçu de votre application dans Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. Ouvrez Visual Studio et **sélectionnez Ouvrir un projet ou une solution**.

1. Accédez au dossier Microsoft-Teams-Samplessamplestab-personalrazor-csharp  >  >  >  et ouvrez **PersonalTab.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou **choisissez Démarrer le débogage** dans le menu **Débogage** de votre application pour vérifier si l’application s’est correctement chargée. Dans un navigateur, accédez aux URL suivantes :

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Passer en revue le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application web ASP.NET Core 3.1 avec la case à cocher **Avancé - Configurer pour HTTPS** sélectionnée lors de l’installation. Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances. En outre, le modèle vide n’active pas le service de contenu statique par défaut. Par conséquent, l’intergiciel de fichiers statiques est ajouté à la `Configure()` méthode à l’aide du code suivant :

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

ASP.NET Core traite les fichiers appelés **Index** comme la page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* Icône de couleur complète mesurant 192 x 192 pixels.
* Icône de contour transparente mesurant 32 x 32 pixels.
* Fichier `manifest.json` qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet sur Teams. Microsoft Teams charge le `contentUrl` fichier spécifié dans votre manifeste, l’incorpore dans un iframe\> <et le restitue dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et **sélectionnez Modifier Project Fichier**. À la fin du fichier, vous pouvez voir le code suivant qui crée et met à jour votre dossier zip lors de la génération de l’application :

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

1. Ouvrez Visual Studio Explorateur de solutions et accédez au dossier **PagesShared** > , ouvrez **_Layout.cshtml** et ajoutez ce qui suit à la `<head>` section balises :

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Dans Visual Studio Explorateur de solutions ouvrez **PersonalTab.cshtml** à partir du dossier **Pages**, ajoutez `microsoftTeams.initialize()` les `<script>` balises et enregistrez.

1. Dans Visual Studio, sélectionnez **F5** ou **choisissez Démarrer le débogage** dans le menu **Débogage** de votre application.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine de votre répertoire de projet, exécutez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec le portail des développeurs

1. Accédez au [**portail des développeurs**](https://dev.teams.microsoft.com/home).

1. Ouvrez **Applications** et sélectionnez **Importer l’application**.

1. Le nom du fichier de package d’application est `tab.zip` et il est disponible au `/bin/Debug/netcoreapp3.1/tab.zip` chemin d’accès.

1. Sélectionnez et ouvrez-le `tab.zip` dans le portail des développeurs.

1. Un **ID d’application** par défaut est créé et rempli dans la section **Informations de base** .

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **Informations sur le développeur**, ajoutez les détails requis et, dans **Website (doit être une URL HTTPS valide),** donnez votre URL HTTPS ngrok.

1. Dans **les URL d’application**, mettez à jour la stratégie `https://<yourngrokurl>/privacy` de confidentialité et les conditions d’utilisation pour `https://<yourngrokurl>/tou` les enregistrer.

1. Dans **les fonctionnalités de l’application**, sélectionnez **Personal appCreate** >  **your first personal app tab** and enter the Name and update the **Content URL** with `https://<yourngrokurl>/personalTab`. Laissez le champ URL du site web vide, puis sélectionnez **Context** en tant que personalTab dans la liste déroulante et **Ajouter**.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. Sélectionnez **Aperçu dans Teams** à partir de la barre d’outils Du portail des développeurs. Le portail des développeurs vous informe que votre application est chargée de manière indépendante. La page **Ajouter** s’affiche pour votre application dans Teams.

1. Sélectionnez **Ajouter** pour charger l’onglet dans Teams. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="Onglet Par défaut" border="true":::

   Vous avez maintenant créé et ajouté votre onglet personnel dans Teams.
  
   Comme vous disposez de votre onglet personnel dans Teams, vous pouvez également [réorganiser](#reorder-static-personal-tabs) et ajouter [`registerOnFocused` l’API](#add-registeronfocused-api-for-tabs-or-personal-apps) pour votre onglet personnel.

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
1. [Mettre à jour et exécuter une application](#update-and-run-your-application-1)
1. [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-2)
1. [Mettre à jour votre package d’application avec le portail des développeurs](#update-your-app-package-with-developer-portal-1)
1. [Afficher un aperçu de votre application dans Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>Générer votre application avec un onglet personnel

1. Ouvrez Visual Studio et **sélectionnez Ouvrir un projet ou une solution**.

1. Accédez au dossier Microsoft-Teams-Samplessamplestab-personalmvc-csharp  >  >  >  et ouvrez **PersonalTabMVC.sln** dans Visual Studio.

1. Dans Visual Studio, sélectionnez **F5** ou **choisissez Démarrer le débogage** dans le menu **Débogage** de votre application pour vérifier si l’application s’est correctement chargée. Dans un navigateur, accédez aux URL suivantes :

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>Passer en revue le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application web ASP.NET Core 3.1 avec la case à cocher **Avancé - Configurer pour HTTPS** sélectionnée lors de l’installation. Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances. En outre, le modèle vide n’active pas le service de contenu statique par défaut. Par conséquent, l’intergiciel de fichiers statiques est ajouté à la `Configure()` méthode à l’aide du code suivant :

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

* Icône **de couleur complète** mesurant 192 x 192 pixels.
* **Icône de contour transparente** mesurant 32 x 32 pixels.
* Fichier `manifest.json` qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet sur Teams. Microsoft Teams charge le `contentUrl` fichier spécifié dans votre manifeste, l’incorpore dans un IFrame et le restitue dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans le Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis **sélectionnez Modifier Project Fichier**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lors de la génération de l’application :

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

**PersonalTab.cs** présente un objet de message et des méthodes appelés à partir de **PersonalTabController** lorsqu’un utilisateur sélectionne un bouton dans l’affichage **PersonalTab** .

#### <a name="views"></a>Affichages

Ces vues sont les différentes vues dans ASP.NET Core MVC :

* Accueil : ASP.NET Core traite les fichiers appelés **Index** comme la page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

* Partagé : le balisage d’affichage partiel **_Layout.cshtml** contient la structure de page globale de l’application et les éléments visuels partagés. Il fait également référence à la bibliothèque Teams.

#### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la `ViewBag` propriété pour transférer dynamiquement des valeurs vers les vues.

</details>

### <a name="update-and-run-your-application"></a>Mettre à jour et exécuter votre application

1. Ouvrez Visual Studio Explorateur de solutions et accédez au dossier **ViewsShared** > , **ouvrez _Layout.cshtml**, puis ajoutez ce qui suit à la `<head>` section balises :

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Dans Visual Studio Explorateur de solutions ouvrir **PersonalTab.cshtml** à partir du dossier **ViewsPersonalTab**  >  et ajouter `microsoftTeams.initialize()` à l’intérieur des `<script>` balises et enregistrer.

1. Dans Visual Studio, sélectionnez **F5** ou **choisissez Démarrer le débogage** dans le menu **Débogage** de votre application.

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine de votre répertoire de projet, exécutez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec le portail des développeurs

1. Accédez au [**portail des développeurs**](https://dev.teams.microsoft.com/home).

1. Ouvrez **Applications** et sélectionnez **Importer l’application**.

1. Le nom de votre package d’application est **tab.zip**. Elle est disponible dans le chemin d’accès suivant :

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Sélectionnez **tab.zip** et ouvrez-le dans le portail des développeurs.

1. Un **ID d’application** par défaut est créé et rempli dans la section **Informations de base** .

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **Informations sur le développeur**, ajoutez les détails requis et, dans **Website (doit être une URL HTTPS valide),** donnez votre URL HTTPS ngrok.

1. Dans **les URL d’application**, mettez à jour la stratégie `https://<yourngrokurl>/privacy` de confidentialité et les conditions d’utilisation pour `https://<yourngrokurl>/tou` les enregistrer.

1. Dans **les fonctionnalités de l’application**, sélectionnez **Personal appCreate** >  **your first personal app tab** and enter the Name and update the **Content URL** with `https://<yourngrokurl>/personalTab`. Laissez le champ URL du site web vide, puis sélectionnez **Context** en tant que personalTab dans la liste déroulante et **Ajouter**.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. Sélectionnez **Aperçu dans Teams** à partir de la barre d’outils Du portail des développeurs. Le portail des développeurs vous informe que votre application est chargée de manière indépendante. La page **Ajouter** s’affiche pour votre application dans Teams.

1. Sélectionnez **Ajouter** pour charger l’onglet sur Teams. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="Onglet personnel" border="true":::
  
   Vous avez maintenant créé et ajouté votre onglet personnel dans Teams.

   Comme vous disposez de votre onglet personnel dans Teams, vous pouvez également [réorganiser](#reorder-static-personal-tabs) et ajouter [`registerOnFocused` l’API](#add-registeronfocused-api-for-tabs-or-personal-apps) pour votre onglet personnel.

::: zone-end

## <a name="reorder-static-personal-tabs"></a>Réorganiser les onglets personnels statiques

À compter de la version 1.7 du manifeste, les développeurs peuvent réorganiser tous les onglets de leur application personnelle. En particulier, un développeur peut déplacer l’onglet **de conversation du bot** , qui est toujours défini par défaut sur la première position, n’importe où dans l’en-tête de l’onglet d’application personnelle. Deux mots clés d’onglet `entityId` réservé sont déclarés, **les conversations** et **les environs**.

Si vous créez un bot avec une étendue **personnelle** , il apparaît par défaut à la première position de l’onglet dans une application personnelle. Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, **conversations**. **L’onglet conversation** s’affiche sur le web ou le bureau en fonction de l’endroit où vous ajoutez l’onglet **conversation** dans le `staticTabs` tableau.

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

L’API `registerOnFocused` du Kit de développement logiciel (SDK) vous permet d’utiliser un clavier sur Teams. Vous pouvez revenir à une application personnelle et maintenir le focus sur un onglet ou une application personnelle à l’aide des touches Ctrl, Maj et F6. Par exemple, vous pouvez vous éloigner de l’application personnelle pour rechercher quelque chose, puis revenir à l’application personnelle ou utiliser Ctrl+F6 pour parcourir les emplacements requis.

Le code suivant fournit un exemple de définition de gestionnaire sur le `registerFocusEnterHandler` Kit de développement logiciel (SDK) lorsque le focus doit être retourné à l’onglet ou à l’application personnelle :

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

Une fois le gestionnaire déclenché avec le mot clé `focusEnter`, le gestionnaire `registerFocusEnterHandler` est appelé avec une fonction `focusEnterHandler` de rappel qui accepte un paramètre appelé `navigateForward`. La valeur de `navigateForward` détermine le type d’événements. Elle `focusEnterHandler` est appelée uniquement par Ctrl+F6 et non par la touche tabulation.
Les clés utiles pour déplacer des événements dans Teams sont les suivantes :

* Événement de transfert : touches Ctrl+F6
* Événement précédent : touches Ctrl+Maj+F6

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

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="Exemple montrant les options d’ajout de l’API registerOnFocussed" border="true":::

#### <a name="personal-app-forward-event"></a>Application personnelle : transférer l’événement

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="Exemple montrant les options permettant d’ajouter le déplacement vers l’avant de l’API registerOnFocussed" border="true":::

#### <a name="personal-app-backward-event"></a>Application personnelle : événement précédent

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="Exemple montrant les options permettant d’ajouter l’API registerOnFocussed vers l’arrière" border="true":::

### <a name="tab"></a>Onglet

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="Exemple montrant les options d’ajout de l’API registerOnFocussed pour l’onglet" border="true":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un canal ou un onglet de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Voir aussi

* [onglets Teams](~/tabs/what-are-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)
* [Partager dans Teams à partir d’une application ou d’un onglet personnel](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
