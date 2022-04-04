---
title: Créer un onglet de canal ou de groupe
author: laujan
description: Guide de démarrage rapide sur la création d’un onglet de canal et de groupe avec le générateur Yeoman pour Microsoft Teams, y compris la révision du code source avec des exemples de code.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 31da2a8ee267ef42e6c0abd4e3bd695cf69d2f01
ms.sourcegitcommit: 3d6aa10d2f58a63c6a4281a30e8771469dba0d0b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2022
ms.locfileid: "64636143"
---
# <a name="channel-or-group-tab"></a>Onglet Canal ou groupe

Les onglets de canal ou de groupe offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié.

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Créer un onglet de canal ou de groupe personnalisé avec Node.js

1. À l’invite de commandes, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant la commande suivante après avoir installé le **Node.js**:

    ```cmd
    npm install yo gulp-cli --global
    ```

2. À l’invite de commandes, installez Microsoft Teams générateur d’application en entrant la commande suivante :

    ```cmd
    npm install generator-teams --global
    ```

Voici les étapes à suivre pour créer un onglet de canal ou de groupe :

* [Générer votre application avec un onglet de canal ou de groupe](#generate-your-application-with-a-channel-or-group-tab)
* [Créer votre package d’application](#create-your-app-package)
* [Créer et exécuter votre application](#build-and-run-your-application)
* [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab)
* [Télécharger votre application à Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Générer votre application avec un onglet de canal ou de groupe

1. À l’invite de commandes, créez un répertoire pour votre onglet de canal ou de groupe.

1. Entrez la commande suivante dans votre nouveau répertoire pour démarrer le générateur Microsoft Teams App :

    ```cmd
    yo teams
    ```

1. Fournissez vos valeurs à une série de questions posées par Microsoft Teams générateur d’application pour mettre à jour votre **fichier manifest.json** :

    ![capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

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

        Utilisez les touches de direction pour sélectionner **l’onglet Configurable** .

    * **Quelles étendues avez-vous l’intention d’utiliser pour votre onglet ?**

        Vous pouvez sélectionner une équipe ou une conversation de groupe.

    * **Avez-vous besoin Microsoft Azure Active Directory (Azure AD) prise en charge de l’sign-on unique pour l’onglet ?**

        Choisissez **de** ne pas inclure Microsoft Azure Active Directory (Azure AD) prise en charge de l’sign-on unique pour l’onglet. La valeur par défaut est oui, entrez **n**.

    * **Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (Y/n)**

        Entrez **n**.

    </details>

> [!IMPORTANT]
> Le composant **de chemin d’accès yourDefaultTabNameTab** est la valeur que vous avez entrée dans le générateur pour le nom de l’onglet par **défaut, ainsi** que le mot **Tab**.
>
> Par exemple : DefaultTabName est **MyTab** puis **/MyTabTab/**

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

    ```bash
    gulp serve
    ```

1. Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur pour afficher la page d’accueil de votre application.

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="Onglet par défaut" border="true":::

1. Pour afficher la page de configuration de votre onglet, allez sur `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. Les exemples suivants sont présentés :

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Page de configuration de l’onglet" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Pour établir un tunnel sécurisé sur votre onglet, quittez l’host local et entrez la commande suivante :

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet est téléchargé vers Microsoft Teams via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session tunnel. Si vous redémarrez votre session ngrok, vous devez mettre à jour votre application avec la nouvelle URL.

### <a name="upload-your-application-to-teams"></a>Télécharger votre application à Teams

1. Go to Microsoft Teams and select **Store**&nbsp; :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. **Sélectionnez Gérer vos applications**.
1. **Sélectionnez Publier une application et** **Télécharger une application personnalisée**.

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="Télécharger application personnalisée" border="true":::

1. Accédez au répertoire de votre projet, accédez au dossier **./package** , sélectionnez le dossier zip du package d’application, puis choisissez **Ouvrir**.
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Onglet Canal téléchargé" border="true":::

1. **Sélectionnez Ajouter** dans la boîte de dialogue. Votre onglet est téléchargé vers Teams.
    
    > [!NOTE]
    > Si  **Add** ne s’affiche pas dans la boîte de dialogue, supprimez le code suivant du manifeste du dossier zip du package d’application téléchargé. Une fois encore, compressez le dossier et téléchargez-le sur Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Suivez les instructions pour ajouter un onglet. Il existe une boîte de dialogue de configuration personnalisée pour votre canal ou onglet de groupe.
1. **Sélectionnez Enregistrer** et votre onglet est ajouté à la barre d’onglets du canal.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Onglet canal chargé" border="true":::
    
    Maintenant, vous avez créé et ajouté avec succès votre onglet de canal ou de groupe dans Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Créer un onglet de canal ou de groupe personnalisé avec ASP.NET Core

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes à suivre pour créer un onglet de canal ou de groupe :

* [Générer votre application avec un onglet de canal ou de groupe](#generate-your-application-with-a-channel-or-group-tab-1)
* [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-1)
* [Mettre à jour votre application](#update-your-application)
* [Créer et exécuter votre application](#build-and-run-your-application-1)
* [Mettre à jour votre package d’application avec le Portail du développeur](#update-your-app-package-with-developer-portal)
* [Afficher un aperçu de votre application dans Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Générer votre application avec un onglet de canal ou de groupe

1. Ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution**.

1. Go to Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  folder and open **channelGroupTab.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou démarrez le  débogage à partir du menu **Débogage** de votre application pour vérifier si l’application s’est chargée correctement. Dans un navigateur, allez aux URL suivantes :

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Passer en revue le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir ASP.NET Core modèle vide d’application web 3.1 avec la case à cocher Avancé * Configurer pour **HTTPS** sélectionnée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendances `ConfigureServices()` . En outre, le modèle vide n’active pas le traitement du contenu statique par défaut, `Configure()` de sorte que l’intermédiaire des fichiers statiques est ajouté à la méthode à l’aide du code suivant :

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

#### <a name="tabcs"></a>Tab.cs

Ce C# contient une méthode qui est appelée à partir de **Tab.cshtml** lors de la configuration.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* Icône **en couleurs complètes** de 192 x 192 pixels.
* Icône **de plan transparente de** 32 x 32 pixels.
* Fichier **manifest.json** qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams. Lorsqu’un utilisateur choisit d’ajouter ou de mettre à jour votre onglet, Microsoft Teams `configurationUrl` charge le contenu spécifié dans votre manifeste, l’incorpore dans un IFrame et l’restituer dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans la Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :

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

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante pour établir un tunnel sécurisé sur votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

Veillez à maintenir l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.

### <a name="update-your-application"></a>Mettre à jour votre application

1. Ouvrez Visual Studio Explorateur de solutions et allez dans le dossier **PagesShared**  >  et ouvrez **_Layout.cshtml**, puis ajoutez les données suivantes à la <head> section balises :

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > Ne copiez pas et collez les `<script src="...">` URL de cette page, car elles ne représentent pas la dernière version. Pour obtenir la dernière version du SDK, toujours Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Insérez un appel `microsoftTeams.initialize();` dans la `script` balise.

1. In Visual Studio Explorateur de solutions go to the **Pages** folder and open **Tab.cshtml**

    Dans **Tab.cshtml** , l’application présente à l’utilisateur deux boutons d’option pour afficher l’onglet avec une icône rouge ou grise. Le choix du **bouton Sélectionner**  `saveGray()` `saveRed()`gris ou Rouge déclenche ou, respectivement,  `settings.setValidityState(true)`définit et active le bouton Enregistrer sur la page de configuration. Ce code vous permet Teams que vous avez rempli les conditions requises pour la configuration et que l’installation peut se poursuivre. Les paramètres sont `settings.setSettings` définies. Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été correctement résolue.

1. Mettez à jour `websiteUrl` les valeurs `contentUrl` de chaque fonction avec l’URL HTTPS ngrok dans votre onglet.

    Votre code doit maintenant inclure les données suivantes avec **y8rCgT2b** remplacé par votre URL ngrok :

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. Enregistrez le **tab.cshtml mis à jour**.

### <a name="build-and-run-your-application"></a>Créer et exécuter votre application

1. Dans Visual Studio, sélectionnez **F5** ou démarrez **le débogage** dans le menu **Débogage**.

1. Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

    > [!TIP]
    > Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution**. Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio. Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec le Portail du développeur

1. Go to Microsoft Teams. Si vous utilisez la [version web](https://teams.microsoft.com), vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur](~/tabs/how-to/developer-tools.md).

1. Go to [**Developer portal**](https://dev.teams.microsoft.com/home).

1. **Ouvrez applications** et sélectionnez **Importer l’application**.

1. Le nom de votre package d’application **esttab.zip**. Il est disponible dans le chemin d’accès suivant :

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **Sélectionneztab.zip** et ouvrez-le dans le Portail du développeur.

1. Un **ID d’application par défaut** est créé et rempli dans la section **Informations de** base.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **Les informations du** développeur, ajoutez les détails requis et dans le site web (doit être une **URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans **les URL d’application**, mettez à jour la politique de confidentialité `https://<yourngrokurl>/privacy` et les conditions d’utilisation pour `https://<yourngrokurl>/tou` et enregistrer.

1. Dans **les fonctionnalités de l’application**, sélectionnez Application de groupe et de canal. Mettez à jour **l’URL de configuration** avec `https://<yourngrokurl>/tab` et sélectionnez l’étendue de votre **onglet**.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. **Sélectionnez Aperçu dans Teams** barre d’outils du Portail du développeur, le Portail du développeur vous informe que votre application est correctement rechargée. La page **Ajouter** s’affiche pour votre application dans Teams.

1. **Sélectionnez Ajouter à l’équipe** pour configurer l’onglet dans une équipe. Configurez votre onglet et sélectionnez **Enregistrer**. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Onglet canal ASPNET chargé" border="true":::
    
    Maintenant, vous avez créé et ajouté avec succès votre onglet de canal ou de groupe dans Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Créer un onglet de canal ou de groupe personnalisé avec ASP.NET Core MVC

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes à suivre pour créer un onglet de canal ou de groupe :

* [Générer votre application avec un onglet de canal ou de groupe](#generate-your-application-with-a-channel-or-group-tab-2)
* [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-2)
* [Mettre à jour votre application](#update-your-application-1)
* [Créer et exécuter votre application](#build-and-run-your-application-2)
* [Mettre à jour votre package d’application avec le Portail du développeur](#update-your-app-package-with-developer-portal-1)
* [Afficher un aperçu de votre application dans Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Générer votre application avec un onglet de canal ou de groupe

1. Ouvrez Visual Studio puis **sélectionnez Ouvrir un projet ou une solution**.

1. Go to Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  folder and open **ChannelGroupTabMVC.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou démarrez le  débogage à partir du menu **Débogage** de votre application pour vérifier si l’application s’est chargée correctement. Dans un navigateur, allez aux URL suivantes :

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>Passer en revue le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir ASP.NET Core modèle vide d’application web 3.1 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de dépendances `ConfigureServices()` . En outre, le modèle vide n’active pas le traitement du contenu statique par défaut, `Configure()` de sorte que l’intermédiaire des fichiers statiques est ajouté à la méthode à l’aide du code suivant :

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

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* Icône **en couleurs complètes** de 192 x 192 pixels.
* Icône **de plan transparente de** 32 x 32 pixels.
* Fichier **manifest.json** qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams.

#### <a name="csproj"></a>.csproj

Dans la Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :

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

#### <a name="models"></a>Modèles

**ChannelGroup.cs** présente un objet Message et des méthodes qui seront appelées à partir des contrôleurs lors de la configuration.

#### <a name="views"></a>Affichages

Voici les différentes vues dans ASP.NET Core MVC :

* Accueil : ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

* Partagé : le contrôle de **_Layout.cshtml contient** la structure de page globale de l’application et les éléments visuels partagés. Il référencera également la bibliothèque Teams bibliothèque.

#### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la propriété `ViewBag` pour transférer dynamiquement des valeurs vers les vues.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante pour établir un tunnel sécurisé sur votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

Veillez à maintenir l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.

### <a name="update-your-application"></a>Mettre à jour votre application

1. Ouvrez Visual Studio Explorateur de solutions,puis allez dans le dossier **ViewsShared**  >  et ouvrez **_Layout.cshtml**, puis ajoutez ce qui suit à la <head> section balises :

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > Ne copiez pas et collez les `<script src="...">` URL de cette page, car elles ne représentent pas la dernière version. Pour obtenir la dernière version du SDK, toujours Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).
    
1. Insérez un appel `microsoftTeams.initialize();` dans la `script` balise.

1. In Visual Studio Explorateur de solutions go to the **Tab** folder and open **Tab.cshtml**

    Dans **Tab.cshtml** , l’application présente à l’utilisateur deux boutons d’option pour afficher l’onglet avec une icône rouge ou grise. Le choix du **bouton Sélectionner**  `saveGray()` `saveRed()`gris ou Rouge déclenche ou, respectivement,  `settings.setValidityState(true)`définit et active le bouton Enregistrer sur la page de configuration. Ce code vous permet Teams que vous avez rempli les conditions requises pour la configuration et que l’installation peut se poursuivre. Les paramètres sont `settings.setSettings` définies. Enfin, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été correctement résolue. 

1. Mettez à jour `websiteUrl` les valeurs `contentUrl` de chaque fonction avec l’URL HTTPS ngrok dans votre onglet.

    Votre code doit maintenant inclure les données suivantes avec **y8rCgT2b** remplacé par votre URL ngrok :

    ```javascript

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Veillez à enregistrer le **tab.cshtml mis à jour**.

### <a name="build-and-run-your-application"></a>Créer et exécuter votre application

1. Dans Visual Studio, sélectionnez **F5** ou démarrez **le débogage** dans le menu **Débogage**.

1. Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

    > [!TIP]
    > Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution**. Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio. Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec le Portail du développeur

1. Go to Microsoft Teams. Si vous utilisez la [version web](https://teams.microsoft.com), vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur](~/tabs/how-to/developer-tools.md).

1. Go to [**Developer portal**](https://dev.teams.microsoft.com/home).

1. **Ouvrez applications** et sélectionnez **Importer l’application**.

1. Le nom de votre package d’application **esttab.zip**. Il est disponible dans le chemin d’accès suivant :

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **Sélectionneztab.zip** et ouvrez-le dans le Portail du développeur.

1. Un **ID d’application par défaut** est créé et rempli dans la section **Informations de** base.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **Les informations du** développeur, ajoutez les détails requis et dans le site web (doit être une **URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans **les URL d’application**, mettez à jour la politique de confidentialité `https://<yourngrokurl>/privacy` et les conditions d’utilisation pour `https://<yourngrokurl>/tou` et enregistrer.

1. Dans **les fonctionnalités de l’application**, sélectionnez Application de groupe et de canal. Mettez à jour **l’URL de configuration** avec `https://<yourngrokurl>/tab` et sélectionnez l’étendue de votre **onglet**.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io`HTTPS.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. **Sélectionnez Aperçu dans Teams** barre d’outils du Portail du développeur, le Portail du développeur vous informe que votre application est correctement rechargée. La page **Ajouter** s’affiche pour votre application dans Teams.

1. **Sélectionnez Ajouter à l’équipe** pour configurer l’onglet dans une équipe. Configurez votre onglet et sélectionnez **Enregistrer**. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Onglet canal ASPNET MVC téléchargé" border="true":::
    
    Maintenant, vous avez créé et ajouté avec succès votre onglet de canal ou de groupe dans Teams.

::: zone-end

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Créer une page de suppression](~/tabs/how-to/create-tab-pages/removal-page.md)
