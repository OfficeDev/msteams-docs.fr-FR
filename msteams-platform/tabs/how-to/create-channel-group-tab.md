---
title: Créer un onglet de canal
author: laujan
description: Dans ce module, découvrez comment créer un canal et un onglet de groupe avec le générateur Yeoman pour Microsoft Teams, notamment en examinant le code source avec des exemples de code.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: b9696b4e41393595edc6a0bdb5d81a74bdf8c699
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503647"
---
# <a name="create-a-channel-tab"></a>Créer un onglet de canal

Les onglets de canal ou de groupe offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié.

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Créer un canal personnalisé ou un onglet de groupe avec Node.js

1. À l’invite de commandes, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant la commande suivante après avoir installé le **node.js** :

    ```cmd
    npm install yo gulp-cli --global
    ```

2. À l’invite de commandes, installez le générateur d’applications Microsoft Teams en entrant la commande suivante :

    ```cmd
    npm install generator-teams --global
    ```

Voici les étapes de création d’un canal ou d’un onglet de groupe :

* [Générer votre application avec un canal ou un onglet de groupe](#generate-your-application-with-a-channel-or-group-tab)
* [Créer votre package d’application](#create-your-app-package)
* [Créer et exécuter votre application](#build-and-run-your-application)
* [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab)
* [Charger votre application dans Teams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Générer votre application avec un onglet de canal ou de groupe

1. À l’invite de commandes, créez un répertoire pour votre canal ou onglet de groupe.

1. Entrez la commande suivante dans votre nouveau répertoire pour démarrer le générateur d’application Microsoft Teams :

    ```cmd
    yo teams
    ```

1. Fournissez vos valeurs à une série de questions posées par le générateur d’applications Microsoft Teams pour mettre à jour votre fichier `manifest.json` :

    ![capture d’écran de l’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

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

        Utilisez les touches de direction pour sélectionner onglet **Configurable** .

    * **Quelles étendues envisagez-vous d’utiliser pour votre onglet ?**

        Vous pouvez sélectionner une équipe ou une conversation de groupe.

    * **Avez-vous besoin de la prise en charge de l’authentification unique Microsoft Azure Active Directory (Azure AD) pour l’onglet ?**

        Choisissez ne **pas** inclure la prise en charge de l’authentification unique Microsoft Azure Active Directory (Azure AD) pour l’onglet. La valeur par défaut est Oui, entrez **n**.

    * **Voulez-vous que cet onglet soit disponible dans SharePoint Online ?**  : Oui

        Entrez **n**.

    </details>

> [!IMPORTANT]
> Le composant de chemin d’accès **yourDefaultTabNameTab** est la valeur que vous avez entrée dans le générateur pour **nom de tabulation par défaut** plus le mot **Tab**. Par exemple, `DefaultTabName` est **MyTab** puis **/MyTabTab/**.

<!--- TBD: this info seems removed from the main branch.
* A **full color icon** measuring 192 x 192 pixels.
* A **transparent outline icon** measuring 32 x 32 pixels.
* A `manifest.json` file that specifies the attributes of your app.
--->

### <a name="create-your-app-package"></a>Créer votre package d’application

Vous devez disposer d’un package d’application pour générer et exécuter votre application dans Teams. Le package d’application est créé via une tâche gulp qui valide le fichier `manifest.json` et génère le dossier zip dans le répertoire `./package`. À l'invite de commandes, tapez la commande suivante :

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>Générer et exécuter votre application

#### <a name="build-your-application"></a>Générer votre application

Entrez la commande suivante à l’invite de commandes pour transpiler votre solution dans le dossier `./dist` :

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

1. Pour afficher la page de configuration de votre onglet, accédez à `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. Les éléments suivants sont affichés :

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="Page de configuration de l’onglet" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Pour établir un tunnel sécurisé vers votre onglet, quittez l’hôte local et entrez la commande suivante :

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois votre onglet chargé dans Microsoft Teams via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session de tunnel. Si vous redémarrez votre session ngrok, vous devez mettre à jour votre application avec la nouvelle URL.

### <a name="upload-your-application-to-teams"></a>Charger votre application dans Teams

1. Accédez à Teams et sélectionnez **Applications**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teams Store":::.
1. Sélectionnez **Gérer vos applications** et **Charger une application personnalisée**.
1. Accédez au répertoire de votre projet, accédez au dossier **./package** , sélectionnez le dossier zip du package d’application, puis choisissez **Ouvrir**.

    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="Onglet de canal chargé" border="true":::

1. Sélectionnez **Ajouter** dans la boîte de dialogue. Votre onglet est chargé dans Teams.

    > [!NOTE]
    > Si  **Ajouter** ne s’affiche pas dans la boîte de dialogue, supprimez le code suivant du manifeste du dossier zip du package d’application chargé. Compressez à nouveau le dossier et chargez-le dans Teams.
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. Suivez les instructions pour ajouter un onglet. Il existe une boîte de dialogue de configuration personnalisée pour votre canal ou onglet de groupe.
1. Sélectionnez **Enregistrer** et votre onglet est ajouté à la barre d’onglets du canal.

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="Onglet Canal chargé" border="true":::

    Vous avez créé et ajouté votre canal ou onglet de groupe dans Teams.

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>Créer un canal personnalisé ou un onglet de groupe avec ASP.NET Core

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes de création d’un canal ou d’un onglet de groupe :

* [Générer votre application avec un canal ou un onglet de groupe](#generate-your-application-with-a-channel-or-group-tab-1)
* [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-1)
* [Mettre à jour votre application](#update-your-application)
* [Créer et exécuter votre application](#build-and-run-your-application-1)
* [Mettre à jour votre package d’application avec le Portail des développeurs](#update-your-app-package-with-developer-portal)
* [Prévisualiser votre application dans Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Générer votre application avec un onglet de canal ou de groupe

1. Ouvrez Visual Studio et sélectionnez **Ouvrir un projet ou une solution**.

1. Accédez à **Modèles de Microsoft Teams** > **modèles** > **tab-channel-group** > **dossier razor-csharp** et ouvrez **channelGroupTab.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** de votre application pour vérifier si l’application s’est correctement chargée. Dans un navigateur, accédez aux URL suivantes :

    * <https://localhost:3978/>
    * <https://localhost:3978/privacy>
    * <https://localhost:3978/tou>

<details>
<summary><b>Examiner le code source</b></summary>

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir d’un modèle vide d’application web ASP.NET Core 3.1 avec la case à cocher **Avancé * Configurer pour HTTPS** sélectionnée lors de l’installation. Les services MVC sont inscrits par la méthode `ConfigureServices()` de l’infrastructure d’injection de dépendances. En outre, le modèle vide n’active pas le traitement du contenu statique par défaut. Par conséquent, l’intergiciel de fichiers statiques est ajouté à la méthode `Configure()` à l’aide du code suivant :

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

#### <a name="tabcs"></a>Tab.cs

Ce fichier C# contient une méthode appelée à partir de **Tab.cshtml** pendant la configuration.

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* **Icône de couleur** mesurant 192 x 192 pixels.
* **Icône de contour transparent** mesurant 32 x 32 pixels.
* Un fichier `manifest.json` qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet dans Teams. Lorsqu’un utilisateur choisit d’ajouter ou de mettre à jour votre onglet, Teams charge le `configurationUrl` fichier spécifié dans votre manifeste, l’incorpore dans un IFrame et le restitue dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans la fenêtre Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier le fichier projet**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lors de la génération de l’application :

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

À l’invite de commandes à la racine de votre répertoire de projet, exécutez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.

### <a name="update-your-application"></a>Mettre à jour votre application

1. Ouvrez Visual Studio Explorateur de solutions et accédez au dossier **Pages** > **Shared**, ouvrez **_Layout.cshtml**, puis ajoutez les éléments suivants au <head> section des balises :

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

    > [!IMPORTANT]
    > Ne copiez pas et ne collez pas les URL `<script src="...">` de cette page, car elles ne représentent pas la dernière version. Pour obtenir la dernière version du Kit de développement logiciel (SDK), accédez toujours à l['API JavaScript microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).

1. Insérez un appel à `microsoftTeams.initialize();` dans la balise `script`.

1. Dans Visual Studio Explorateur de solutions accédez au dossier **Pages** et ouvrez **ùTab.cshtml**

    Dans **Tab.cshtml** l’application présente à l’utilisateur deux boutons d’option permettant d’afficher l’onglet avec une icône rouge ou grise. Le choix de **Sélectionner un** gris ou **sélectionner des déclencheurs de bouton** rouges `saveGray()` ou `saveRed()`, respectivement, définit `settings.setValidityState(true)`et active le bouton **Enregistrer** sur la page de configuration. Ce code indique à Teams que vous avez rempli les exigences de configuration et que l’installation peut continuer. Les paramètres de `settings.setSettings` sont définis. Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue.

1. Mettez à jour les valeurs `websiteUrl` et `contentUrl` dans chaque fonction avec l’URL ngrok HTTPS sous votre onglet.

    Votre code doit maintenant inclure ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :

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

1. Enregistrez le **Tab.cshtml** mis à jour.

### <a name="build-and-run-your-application"></a>Générer et exécuter votre application

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer**.

1. Vérifiez que **ngrok** s’exécute et fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

    > [!TIP]
    > Votre application doit être en cours d’exécution dans Visual Studio et ngrok pour effectuer les étapes fournies dans cet article. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **conserver ngrok en cours d’exécution**. Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio. Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.

<!--- TBD: This note seems to be removed from main. Commenting it for now.
> [!NOTE]
> App Studio can be used to edit your `manifest.json` file and upload the completed package to Teams. You can also manually edit the `manifest.json` file. If you do, ensure that you build the solution again to create the `tab.zip` file to upload.
--->

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec Developer Portal

1. Accédez à Teams. Si vous utilisez la [version web](https://teams.microsoft.com), vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur](~/tabs/how-to/developer-tools.md).

1. Accédez à [**Portail des développeurs**](https://dev.teams.microsoft.com/home).

1. Ouvrez **Applications** et sélectionnez **Importer une application**.

<!--- TBD: This steps seems to be removed from main now so commenting it for now.

1. Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest. The name of your app package is `tab.zip`. It is available from the following path:
--->

1. Le nom de votre package d’application est `tab.zip`. Il est disponible dans le chemin d’accès suivant :

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Sélectionnez `tab.zip` et ouvrez-le dans le Developer Portal.

1. Un **ID d’application** par défaut est créé et rempli dans la section **Informations de base**.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **information du développeur**, ajoutez les détails requis et dans **Le site web (doit être une URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans les **URL d’application**, mettez à jour la Stratégie de confidentialité vers `https://<yourngrokurl>/privacy` et Conditions d’utilisation vers `https://<yourngrokurl>/tou`, puis enregistrez.

1. Dans **Fonctionnalités de l’application**, sélectionnez Groupe et application de canal. Mettez à jour l’**URL de configuration** avec `https://<yourngrokurl>/tab`, puis sélectionnez l’**Étendue** de votre onglet.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. Sélectionnez **Aperçu dans Teams** dans la barre d’outils Portail des développeurs, le Portail des développeurs vous informe que votre application a été chargée correctement. La page **Ajouter** s’affiche pour votre application dans Teams.

1. Sélectionnez **Ajouter à l’équipe** pour configurer l’onglet dans une équipe. Configurez votre onglet et sélectionnez **Enregistrer**. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="Onglet Canal ASPNET chargé" border="true":::

    Vous avez créé et ajouté votre canal ou onglet de groupe dans Teams.

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>Créer un canal personnalisé ou un onglet de groupe avec ASP.NET Core MVC

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante ou vous pouvez télécharger le [code source](https://github.com/OfficeDev/Microsoft-Teams-Samples) et extraire les fichiers :

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

Voici les étapes de création d’un canal ou d’un onglet de groupe :

* [Générer votre application avec un canal ou un onglet de groupe](#generate-your-application-with-a-channel-or-group-tab-2)
* [Établir un tunnel sécurisé vers votre onglet](#establish-a-secure-tunnel-to-your-tab-2)
* [Mettre à jour votre application](#update-your-application-1)
* [Créer et exécuter votre application](#build-and-run-your-application-2)
* [Mettre à jour votre package d’application avec le Portail des développeurs](#update-your-app-package-with-developer-portal-1)
* [Prévisualiser votre application dans Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>Générer votre application avec un onglet de canal ou de groupe

1. Ouvrez Visual Studio et sélectionnez **Ouvrir un projet ou une solution**.

1. Accédez au dossier **Modèles Microsoft Teams** > **Modèles** > **tab-channel-group** > **mvc-csharp**, puis ouvrez **ChannelGroupTabMVC.sln**.

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer** de votre application pour vérifier si l’application s’est correctement chargée. Dans un navigateur, accédez aux URL suivantes :

    * <https://localhost:3978/>
    * <https://localhost:3978/privacy>
    * <https://localhost:3978/tou>

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

#### <a name="appmanifest-folder"></a>Dossier AppManifest

Ce dossier contient les fichiers de package d’application requis suivants :

* **Icône de couleur** mesurant 192 x 192 pixels.
* **Icône de contour transparent** mesurant 32 x 32 pixels.
* Un fichier `manifest.json` qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet dans Teams.

#### <a name="csproj"></a>.csproj

Dans la fenêtre Visual Studio Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier le fichier projet**. À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lors de la génération de l’application :

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

**ChannelGroup.cs** présente un objet Message et des méthodes qui seront appelés à partir des contrôleurs pendant la configuration.

#### <a name="views"></a>Affichages

Voici les différentes vues dans ASP.NET Core MVC :

* Accueil : ASP.NET Core traite les fichiers appelés **Index** comme page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

* Partagé : le balisage de vue partielle **_Layout.cshtml** contient la structure de page globale de l’application et les éléments visuels partagés. Il référence également la bibliothèque Teams.

#### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la propriété `ViewBag` pour transférer dynamiquement des valeurs vers les vues.

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

À l’invite de commandes à la racine de votre répertoire de projet, exécutez la commande suivante pour établir un tunnel sécurisé vers votre onglet :

```cmd
ngrok http 3978 --host-header=localhost
```

Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.

### <a name="update-your-application"></a>Mettre à jour votre application

1. Ouvrez l’explorateur Visual Studio, puis accédez au dossier **Affichages** > **Partagé**, ouvrez **_Layout.cshtml**, puis ajoutez les éléments suivants à l’applet de commande <head> section des balises :

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

    > [!IMPORTANT]
    > Ne copiez pas et ne collez pas les URL `<script src="...">` de cette page, car elles ne représentent pas la dernière version. Pour obtenir la dernière version du Kit de développement logiciel (SDK), accédez toujours à l['API JavaScript microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).

1. Insérez un appel à `microsoftTeams.initialize();` dans la balise `script`.

1. Dans Visual Studio Explorateur de solutions accédez au dossier **Tab** et ouvrez **Tab.cshtml**

    Dans **Tab.cshtml** l’application présente à l’utilisateur deux boutons d’option permettant d’afficher l’onglet avec une icône rouge ou grise. Le choix de **Sélectionner un** gris ou **sélectionner des déclencheurs de bouton** rouges `saveGray()` ou `saveRed()`, respectivement, définit `settings.setValidityState(true)`et active le bouton **Enregistrer** sur la page de configuration. Ce code indique à Teams que vous avez rempli les exigences de configuration et que l’installation peut continuer. Les paramètres de `settings.setSettings` sont définis. Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue.

1. Mettez à jour les valeurs `websiteUrl` et `contentUrl` dans chaque fonction avec l’URL ngrok HTTPS sous votre onglet.

    Votre code doit maintenant inclure ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :

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

1. Veillez à enregistrer la **Tab.cshtml**.

### <a name="build-and-run-your-application"></a>Générer et exécuter votre application

1. Dans Visual Studio, sélectionnez **F5** ou choisissez **Démarrer le débogage** dans le menu **Déboguer**.

1. Vérifiez que **ngrok** s’exécute et fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

    > [!TIP]
    > Votre application doit être en cours d’exécution dans Visual Studio et ngrok pour effectuer les étapes fournies dans cet article. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **conserver ngrok en cours d’exécution**. Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio. Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.

### <a name="update-your-app-package-with-developer-portal"></a>Mettre à jour votre package d’application avec Developer Portal

1. Accédez à Teams. Si vous utilisez la [version web](https://teams.microsoft.com), vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur](~/tabs/how-to/developer-tools.md).

1. Accédez à [**Portail des développeurs**](https://dev.teams.microsoft.com/home).

1. Ouvrez **Applications** et sélectionnez **Importer une application**.

1. Le nom de votre package d’application est **tab.zip**. Il est disponible dans le chemin d’accès suivant :

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. Sélectionnez **tab.zip** et ouvrez-le dans le Developer Portal.

1. Un **ID d’application** par défaut est créé et rempli dans la section **Informations de base**.

1. Ajoutez la description courte et longue de votre application dans **Descriptions**.

1. Dans **information du développeur**, ajoutez les détails requis et dans **Le site web (doit être une URL HTTPS valide)** donnez votre URL HTTPS ngrok.

1. Dans les **URL d’application**, mettez à jour la Stratégie de confidentialité vers `https://<yourngrokurl>/privacy` et Conditions d’utilisation vers `https://<yourngrokurl>/tou`, puis enregistrez.

1. Dans **Fonctionnalités de l’application**, sélectionnez Groupe et application de canal. Mettez à jour l’**URL de configuration** avec `https://<yourngrokurl>/tab`, puis sélectionnez l’**Étendue** de votre onglet.

1. Sélectionnez **Enregistrer**.

1. Dans la section Domaines, les domaines de vos onglets doivent contenir votre URL ngrok sans le préfixe HTTPS `<yourngrokurl>.ngrok.io`.

### <a name="preview-your-app-in-teams"></a>Afficher un aperçu de votre application dans Teams

1. Sélectionnez **Aperçu dans Teams** dans la barre d’outils Portail des développeurs, le Portail des développeurs vous informe que votre application a été chargée correctement. La page **Ajouter** s’affiche pour votre application dans Teams.

1. Sélectionnez **Ajouter à l’équipe** pour configurer l’onglet dans une équipe. Configurez votre onglet et sélectionnez **Enregistrer**. Votre onglet est désormais disponible dans Teams.

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="ASPNET MVC de l’onglet de canal chargé" border="true":::

    Vous avez créé et ajouté votre canal ou onglet de groupe dans Teams.

::: zone-end

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>Voir aussi

* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Créer une page de suppression](~/tabs/how-to/create-tab-pages/removal-page.md)
