---
title: Créer un onglet personnel
author: laujan
description: Guide de démarrage rapide sur la création d’un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 8048f317fa0e22353d58b6363271b281a6f3849e
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60719931"
---
# <a name="create-a-personal-tab"></a>Créer un onglet personnel

## <a name="create-a-custom-personal-tab"></a>Créer un onglet personnel personnalisé

Vous pouvez créer un onglet personnel à l'Node.js Yeoman Generator, ASP.NET Core ou ASP.NET Core MVC.

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

### <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator"></a>Créer un onglet personnel personnalisé à l’aide Node.js et du générateur Yeoman

> [!NOTE]
> Cet article suit les étapes décrites dans la build de votre premier Wiki [Microsoft Teams’application,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) qui se trouve dans le référentiel GitHub Microsoft OfficeDev.

Vous pouvez créer un onglet personnel personnalisé à [l’aide Teams générateur Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) L’application est également téléchargée vers Teams.

### <a name="prerequisites-for-teams-apps"></a>Conditions préalables pour Teams applications

Vous devez connaître les conditions préalables suivantes :

- Vous devez avoir un client Office 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée. Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

    > [!NOTE]
    > Si vous n’avez pas de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme Office 365 développeur. L’abonnement reste actif tant que vous l’utilisez pour le développement continu. Bienvenue [dans le programme Office 365 développeur.](/office/developer-program/microsoft-365-developer-program)

En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :

- N’importe quel éditeur de texte ou IDE. Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuitement.

- [Node.js/npm](https://nodejs.org/en/). Utilisez la dernière version de LTS. Le nœud Gestionnaire de package (npm) est installé dans votre système avec l’installation de Node.js.

- Une fois que vous avez installé Node.js, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en entrant la commande suivante dans votre invite de commandes :

    ```bash
    npm install yo gulp-cli --global
    ```

- Installez le générateur Microsoft Teams Apps en entrant la commande suivante dans votre invite de commandes :

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a>Générer votre projet

**Pour générer votre projet**

1. À l’invite de commandes, créez un répertoire pour votre projet d’onglet.

1. Pour démarrer le générateur, allez dans votre nouveau répertoire et entrez la commande suivante :

    ```bash
    yo teams
    ```

1. Ensuite, fournissez une série de valeurs utilisées dans le fichier **manifest.json** de votre application :

    ![capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **Quel est le nom de votre solution ?**

    Le nom de la solution est le nom de votre projet. Vous pouvez accepter le nom suggéré en sélectionnant **Entrée.**

    **Où souhaitez-vous placer les fichiers ?**

    Vous êtes actuellement dans votre répertoire de projet. Sélectionnez **Entrée**.

    **Titre de votre Microsoft Teams d’application ?**

    Le titre est le nom de votre package d’application et est utilisé dans le manifeste et la description de l’application. Entrez un titre ou **sélectionnez Entrée** pour accepter le nom par défaut.

    **Votre nom (d’entreprise) ? (32 caractères maximum)**

    Le nom de votre société sera utilisé dans le manifeste de l’application. Entrez un nom de société ou **sélectionnez Entrée** pour accepter le nom par défaut.

    **Quelle version de manifeste souhaitez-vous utiliser ?**

    Sélectionnez le schéma par défaut.

    **La échafaudage rapide ? (Y/n)**

    La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.

    **Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**

    Ce champ n’est pas obligatoire et doit être utilisé uniquement si vous faites déjà partie de [Microsoft Partner Network](https://partner.microsoft.com).

    **Que voulez-vous ajouter à votre projet ?**

    Sélectionnez **( &ast; ) un onglet**.

    **L’URL où vous allez héberger cette solution ?**

    Par défaut, le générateur suggère une URL de sites web Azure. Vous testez uniquement votre application localement, de sorte qu’une URL valide n’est pas nécessaire.

    **Voulez-vous afficher un indicateur de chargement lors du chargement de votre application/onglet ?**

    Choisissez **de ne** pas inclure d’indicateur de chargement lors du chargement de votre application ou de votre onglet. La valeur par défaut est non, entrez **n**.

    **Voulez-vous que les applications personnelles soient restituées sans barre d’en-tête d’onglet ?**

    Choisissez **de** ne pas inclure d’applications personnelles à restituer sans barre d’en-tête d’onglet. La valeur par défaut est non, entrez **n**.

    **Souhaitez-vous inclure l’infrastructure test et les tests initiaux ? (y/N)**

    Choisissez **de ne** pas inclure d’infrastructure de test pour ce projet. La valeur par défaut est non, entrez **n**.

    **Souhaitez-vous inclure la prise en charge esLint ? (y/N)**

    Choisissez de ne pas inclure la prise en charge esLint. La valeur par défaut est non, entrez **n**.

    **Voulez-vous utiliser Azure Applications Informations pour la télémétrie ? (y/N)**

    Choisissez **de ne** pas inclure Azure Application [Informations](/azure/azure-monitor/app/app-insights-overview). La valeur par défaut est non ; entrez **n**.

    **Nom de l’onglet par défaut (16 caractères maximum) ?**

    Nommez votre onglet. Ce nom d’onglet est utilisé dans l’ensemble de votre projet en tant que composant de chemin d’accès de fichier ou d’URL.

    **Quel type d’onglet voulez-vous créer ?**

    Utilisez les touches de direction pour sélectionner **Personnel (statique).**

    **Avez-vous besoin d’une prise en charge de l’authentification unique Azure AD pour l’onglet ?**

    Choisissez **de** ne pas inclure Azure AD prise en charge de l' sign-on unique pour l’onglet. La valeur par défaut est oui, entrez **n**.

    > [!IMPORTANT]
    > The path component **yourDefaultTabNameTab** is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.
    >
    > Par exemple : DefaultTabName: **MyTab**  >  **/MyTabTab/**

### <a name="add-a-personal-tab"></a>Ajouter un onglet personnel

**Pour ajouter un onglet personnel à cette application, créez une page de contenu et mettez à jour les fichiers existants**

1. Dans votre éditeur de code, créez un fichier HTML **personal.html** et ajoutez le code suivant :

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

1. Enregistrez **personal.html** dans le dossier web de **votre** application à l’emplacement suivant :

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

1. Ouvrez **manifest.json à** partir de l’emplacement suivant dans votre éditeur de code :

    ```bash
    ./src/manifest/manifest.json/
    ```

1. Ajoutez ce qui suit au tableau vide ( ) et `staticTabs` `staticTabs":[]` ajoutez l’objet JSON suivant :

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

1. Mettez à jour le composant de chemin **d’accès contentURL** **yourDefaultTabNameTab** avec votre nom d’onglet réel.

1. Enregistrez le fichier **manifest.json** mis à jour.

1. Pour fournir votre page de contenu dans un IFrame, ouvrez **Tab.ts** dans votre éditeur de code à partir du chemin d’accès suivant :

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. Ajoutez ce qui suit à la liste descorateurs IFrame :

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

1. Enregistrez le fichier **Tab.ts** mis à jour. Le code de l’onglet est terminé.

### <a name="build-and-run-your-application"></a>Créer et exécuter votre application

À l’invite de commandes, ouvrez le répertoire de votre projet pour effectuer les tâches suivantes.

#### <a name="create-the-app-package"></a>Créer le package d’application

Vous devez avoir un package d’application pour tester votre onglet dans Teams. Il s’agit d’un dossier zip qui contient les fichiers requis suivants :

- Icône **en couleurs complètes** de 192 x 192 pixels.
- Icône **de plan transparente de** 32 x 32 pixels.
- Fichier **manifest.json** qui spécifie les attributs de votre application.

Le package est créé par le biais d’une tâche Gulp qui valide le fichier manifest.json et génère le dossier zip dans le répertoire **./package.** Dans l’invite de commandes, entrez la commande suivante :

```bash
gulp manifest
```

#### <a name="build-your-application"></a>Créer votre application

La commande de build transpile votre solution dans le **dossier ./dist.** Entrez la commande suivante dans l’invite de commandes :

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a>Exécuter votre application dans localhost

1. Démarrez un serveur web local en entrant la commande suivante dans l’invite de commandes :

    ```bash
    gulp serve
    ```

1. Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur, remplacez-le par votre nom d’onglet et affichez la page d’accueil de votre application, comme illustré `**<yourDefaultAppNameTab>**` dans l’image suivante :

    ![capture d’écran de la page d’accueil](~/assets/images/tab-images/homePage.png)

1. Pour afficher votre onglet personnel, allez sur `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` .

    >![Capture d’écran de l’onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

### <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS. Teams n’autorise pas l’hébergement local. Publiez votre onglet sur une URL publique ou utilisez un proxy qui expose votre port local à une URL internet.

Pour tester votre extension d’onglet, [utilisez ngrok,](https://ngrok.com/docs)qui est intégré à cette application. Ngrok est un outil logiciel de proxy inverse. Ngrok crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Les points de terminaison web de votre serveur sont disponibles pendant la session en cours sur votre ordinateur. Lorsque l’ordinateur est arrêté ou en veille, le service n’est plus disponible.

Dans votre invite de commandes, quittez localhost et entrez la commande suivante :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé vers Microsoft Teams via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session tunnel.

### <a name="upload-your-application-to-teams"></a>Télécharger votre application à Teams

**Pour télécharger votre application sur Teams**

1. Go to Microsoft Teams. Si vous utilisez la [version web,](https://teams.microsoft.com)vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)
1. Dans le coin inférieur gauche, sélectionnez **Applications.**
1. Dans le coin inférieur gauche, choisissez **Télécharger une application personnalisée.**
1. Accédez au répertoire de votre projet, accédez au dossier **./package,** sélectionnez le dossier zip, puis choisissez **Ouvrir**.

    ![Ajout de votre onglet personnel](../../assets/images/tab-images/addingpersonaltab.png)

1. Sélectionnez **Ajouter** dans la boîte de dialogue. Votre onglet est téléchargé vers Teams.

    ![Onglet personnel chargé](../../assets/images/tab-images/personaltabuploaded.png)

### <a name="view-your-personal-tab"></a>Afficher votre onglet personnel

Dans la barre de navigation à l’extrême gauche Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF; et choisissez votre application.

# <a name="aspnet-core"></a>[ASP.NET Core](#tab/aspnetcore)

### <a name="create-a-custom-personal-tab-using-aspnet-core"></a>Créer un onglet personnel personnalisé à l’aide ASP.NET Core

Vous pouvez créer un onglet personnel personnalisé à l’aide C# et ASP.NET Core pages Dente. [App Studio](~/concepts/build-and-test/app-studio-overview.md) est également utilisé pour compléter le manifeste de votre application et déployer votre onglet sur Teams.

### <a name="prerequisites-for-personal-tab"></a>Conditions préalables pour l’onglet personnel

Vous devez connaître les conditions préalables suivantes :

- Vous devez avoir un client Office 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée. Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

    > [!NOTE]
    > Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program) L’abonnement reste actif tant que vous l’utilisez pour le développement continu.

- Utilisez App Studio pour importer votre application dans Teams. Pour installer App Studio, sélectionnez **Apps** Store App dans le coin inférieur gauche de ![ l’application ](~/assets/images/tab-images/storeApp.png) Teams, puis **recherchez App Studio.** Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez Ajouter **dans** la boîte de dialogue pour l’installer.

En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :

- Version actuelle de l’Visual Studio IDE avec la charge de travail de développement **.NET CORE sur** plusieurs plateformes installée. Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.

- Outil de proxy inverse [ngrok.](https://ngrok.com) Utilisez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Vous pouvez [télécharger ngrok](https://ngrok.com/download).

### <a name="get-the-source-code"></a>Obtenir le code source

À l’invite de commandes, créez un répertoire pour votre projet d’onglet. Un projet simple est fourni pour vous aider à démarrer. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante :

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Vous pouvez également récupérer le code source en téléchargeant le dossier zip et en extrayant les fichiers.

**Pour créer et exécuter le projet d’onglet**

1. Une fois que vous avez obtenir le code source, Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**
1. Go to the tab application directory and open **PersonalTab.sln**.
1. Pour créer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage.**
1. Dans un navigateur, go to the following URLs to verify the application loaded properly:

    - `http://localhost:44325/`
    - `http://localhost:44325/personal`
    - `http://localhost:44325/privacy`
    - `http://localhost:44325/tou`

### <a name="review-the-source-code"></a>Passer en revue le code source

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation. Les services MVC sont inscrits par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances. En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire des fichiers statiques est ajouté à la méthode à l’aide du `Configure()` code suivant :

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

- Icône **en couleurs complètes** de 192 x 192 pixels.
- Icône **de plan transparente de** 32 x 32 pixels.
- Fichier **manifest.json** qui spécifie les attributs de votre application.

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams. Microsoft Teams charge le spécifié dans votre manifeste, l’incorpore dans un iframe <et l’restituer `contentUrl` \> dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .** À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :

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

### <a name="update-your-application-for-teams"></a>Mettre à jour votre application pour Teams

#### <a name="_layoutcshtml"></a>_Layout.cshtml

Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page. Votre onglet et l’application Teams communiquent de cette manière :

Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

#### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Ouvrez **PersonalTab.cshtml** et mettez à jour les `<script>` balises incorporées en appelant `microsoftTeams.initialize()` .

Veillez à enregistrer votre **PersonalTab.cshtml** mis à jour.

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a>Établir un tunnel sécurisé vers votre onglet pour Teams

Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS. Teams n’autorise pas l’hébergement local. Publiez votre onglet sur une URL publique ou utilisez un proxy qui expose votre port local à une URL internet.

Pour tester votre onglet, utilisez [ngrok](https://ngrok.com/docs). Les points de terminaison web de votre serveur sont disponibles lorsque ngrok est en cours d’exécution sur votre ordinateur. Dans la version gratuite de ngrok, si vous fermez ngrok, les URL sont différentes lors du prochain démarrage.

**Pour établir un tunnel sécurisé sur votre onglet**

1. À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante :

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

    Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application lorsqu’elle est en cours d’exécution sur le port 44325. Il ressemble à `https://y8rPrT2b.ngrok.io/` **l’endroit où y8rPrT2b** est remplacé par votre URL HTTPS alpha-numérique ngrok.

    Veillez à conserver l’invite de commandes avec ngrok en cours d’exécution et notez l’URL.

2. Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

> [!TIP]
> Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.** Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio. Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.

#### <a name="run-your-application"></a>Exécuter votre application

Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage de votre** application.

### <a name="upload-your-tab-with-app-studio-for-teams"></a>Télécharger onglet avec App Studio pour Teams

> [!NOTE]
> **App Studio** peut être utilisé pour modifier votre **fichier manifest.json** et télécharger le package terminé dans Teams. Vous pouvez également modifier manuellement **manifest.json**. Si vous le faites, veillez à générer à nouveau la solution pour créerTab.zip **fichier** à télécharger.

**Pour télécharger votre onglet avec App Studio**

1. Go to Microsoft Teams. Si vous utilisez la [version web,](https://teams.microsoft.com)vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)

1. Go to **App Studio** and select the **Manifest editor** tab.

1. Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet.  Le code source est livré avec son propre manifeste partiellement complet. Le nom de votre package d’application **esttab.zip**. Il est disponible à partir du chemin d’accès suivant :

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Télécharger **tab.zip** **app Studio.**

#### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez chargé votre package d’application dans App Studio, vous devez le configurer.

Sélectionnez la vignette de l’onglet nouvellement importé de la page d’accueil de l’éditeur de manifeste.

Il existe une liste d’étapes sur le côté gauche de l’éditeur de manifeste. Sur le côté droit de l’éditeur de manifeste figure une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par **votre manifest.json,** mais vous devez mettre à jour certains champs.

##### <a name="details-app-details"></a>Détails : détails de l’application

Dans la section **Détails de l’application** :

1. Sous **Identification,** **sélectionnez Générer** pour générer un nouvel ID d’application pour votre application.

1. Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**

    ![URL d’application mises à jour](../../assets/images/tab-images/appurls.png)

1. Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.

##### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section **Onglets** :

1. Sous **Ajouter un onglet personnel,** sélectionnez **Ajouter.** Une boîte de dialogue s’affiche.

1. Entrez un nom pour l’onglet personnel dans **Nom**.

1. Entrez **l’ID d’entité**.

1. Mettre à **jour l’URL de** contenu avec `https://<yourngrokurl>/personalTab` .

    Laissez le **champ URL** du site web vide.

    ![Détails de l’onglet personnel](../../assets/images/tab-images/personaltabdetails.png)

1. Sélectionnez **Enregistrer**.

##### <a name="finish-domains-and-permissions"></a>Finish: Domains and permissions

Dans la section **Domaines et autorisations,** les domaines de vos **onglets** doivent contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`

###### <a name="finish-test-and-distribute"></a>Fin : Tester et distribuer

> [!IMPORTANT]
> À droite, dans **Description,** vous voyez l’avertissement suivant :
>
> &#9888; tableau **« validDomains » ne peut pas contenir de site de tunneling...**
>
> Cet avertissement peut être ignoré lors du test de votre onglet.

1. Dans la section **Tester et distribuer,** sélectionnez **Installer.**

1. Dans la boîte de dialogue qui s’affiche, **sélectionnez** Ajouter et votre onglet s’affiche.

    ![Onglet personnel ASPNET chargé](../../assets/images/tab-images/personaltabaspnetuploaded.png)

### <a name="view-your-personal-tab-in-teams"></a>Afficher votre onglet personnel dans Teams

1. Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF;. Une liste d’applications personnelles s’affiche.

1. Sélectionnez votre onglet dans la liste pour l’afficher.

# <a name="aspnet-core-mvc"></a>[ASP.NET Core MVC](#tab/aspnetcoremvc)

### <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>Créer un onglet personnel personnalisé avec ASP.NET Core MVC

Vous pouvez créer un onglet personnel personnalisé à l’aide C# et ASP.NET Core MVC. [App Studio pour Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) est également utilisé pour compléter le manifeste de votre application et déployer votre onglet sur Teams.

### <a name="prerequisites-for-personal-tab-with-aspnet-core-mvc"></a>Conditions préalables pour l’onglet personnel avec ASP.NET Core MVC

- Vous devez avoir un client Microsoft 365 et une équipe configurée avec l’application Autoriser le téléchargement **d’applications** personnalisées activée. Pour plus d’informations, [voir préparer votre Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

    > [!NOTE]
    > Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program) L’abonnement reste actif tant que vous l’utilisez pour le développement continu.

- Utilisez App Studio pour importer votre application dans Teams. Pour installer App Studio, sélectionnez **Apps** Store App dans le coin inférieur gauche de ![ l’application ](~/assets/images/tab-images/storeApp.png) Teams, puis **recherchez App Studio.** Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez Ajouter **dans** la boîte de dialogue pop-up pour l’installer.

En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :

- Version actuelle de l’Visual Studio IDE avec la charge de travail de développement **.NET CORE sur** plusieurs plateformes installée. Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.

- Outil de proxy inverse [ngrok.](https://ngrok.com) Utilisez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Vous pouvez [télécharger ngrok](https://ngrok.com/download).

### <a name="get-the-source-code"></a>Obtenir le code source

À l’invite de commandes, créez un répertoire pour votre projet d’onglet. Un projet simple est fourni pour vous aider à démarrer. Clonez l’exemple de référentiel dans votre nouveau répertoire à l’aide de la commande suivante :

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

Vous pouvez également récupérer le code source en téléchargeant le dossier zip et en extrayant les fichiers.

**Pour créer et exécuter le projet d’onglet**

1. Une fois que vous avez le code source, Visual Studio puis **sélectionnez Ouvrir un projet ou une solution.**
1. Go to the tab application directory and open **PersonalTabMVC.sln**.
1. Pour créer et exécuter votre application, appuyez sur **F5** ou choisissez **Démarrer le** débogage dans le menu **Débogage.**
1. Dans un navigateur, go to the following URLs to verify that the application loaded properly:

    * `http://localhost:44335`
    * `http://localhost:44335/privacy`
    * `http://localhost:44335/tou`

### <a name="review-the-source-code"></a>Passer en revue le code source

#### <a name="startupcs"></a>Startup.cs

Ce projet a été créé à partir ASP.NET Core modèle vide application web 2.2 avec la case à cocher Avancé - Configurer pour **HTTPS** sélectionnée lors de l’installation. Les services MVC sont enregistrés par la méthode de l’infrastructure d’injection de `ConfigureServices()` dépendances. En outre, le modèle vide n’active pas la portion de contenu statique par défaut, de sorte que l’intermédiaire de fichiers statiques est ajouté à la méthode à l’aide du `Configure()` code suivant :

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

Ces fichiers doivent être compressés dans un package d’application pour être utilisés lors du chargement de votre onglet vers Teams. Microsoft Teams charge le spécifié dans votre manifeste, l’incorpore dans un IFrame et l’restituer `contentUrl` dans votre onglet.

#### <a name="csproj"></a>.csproj

Dans la Visual Studio’Explorateur de solutions, cliquez avec le bouton droit sur le projet et sélectionnez **Modifier Project fichier .** À la fin du fichier, vous voyez le code suivant qui crée et met à jour votre dossier zip lorsque l’application est créée :

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

**PersonalTab.cs** présente un objet Message et des méthodes qui sont appelées à partir de **PersonalTabController** lorsqu’un utilisateur sélectionne un bouton dans **l’affichage PersonalTab.**

#### <a name="views"></a>Affichages

Ces affichages sont les différents dans ASP.NET Core MVC :

* Accueil : ASP.NET Core fichiers appelés **Index** comme page d’accueil ou par défaut du site. Lorsque l’URL de votre navigateur pointe vers la racine du site, **Index.cshtml** s’affiche en tant que page d’accueil de votre application.

* Partagé : le contrôle de **_Layout.cshtml contient** la structure de page globale de l’application et les éléments visuels partagés. Il fait également référence à la Teams bibliothèque.

#### <a name="controllers"></a>Contrôleurs

Les contrôleurs utilisent la propriété pour transférer dynamiquement des `ViewBag` valeurs vers les affichages.

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

**Pour exécuter ngrok et vérifier la page de contenu**

1. À l’invite de commandes à la racine du répertoire de votre projet, exécutez la commande suivante :

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

    Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application lorsqu’elle est en cours d’exécution sur le port 44325. Il ressemble à `https://y8rPrT2b.ngrok.io/` **l’endroit où y8rPrT2b** est remplacé par votre URL HTTPS alpha-numérique ngrok.

    Veillez à ce que l’invite de commandes avec ngrok soit en cours d’exécution et notez l’URL.

1. Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

> [!TIP]
> Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer les étapes fournies dans cet article. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **maintenez ngrok en cours d’exécution.** Il écoute et reprend le routage de la demande de votre application lorsqu’elle redémarre dans Visual Studio. Si vous devez redémarrer le service ngrok, il renvoie une nouvelle URL et vous devez mettre à jour chaque endroit qui utilise cette URL.

#### <a name="run-your-application"></a>Exécuter votre application

Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage de votre** application.

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

---

## <a name="reorder-static-personal-tabs"></a>Réordesser les onglets personnels statiques

À partir de la version de manifeste 1.7, les développeurs peuvent réorganiser tous les onglets de leur application personnelle. En particulier, un développeur peut déplacer l’onglet de conversation du **bot,** qui est toujours en première position par défaut, n’importe où dans l’en-tête de l’onglet de l’application personnelle. Deux mots clés `entityId` d’onglet réservés sont déclarés, **conversations** et **à propos de**.

Si vous créez un bot avec une **étendue** personnelle, il apparaît par défaut dans le premier onglet d’une application personnelle. Si vous souhaitez le déplacer vers une autre position, vous devez ajouter un objet onglet statique à votre manifeste avec le mot clé réservé, **conversations**. **L’onglet de conversation** s’affiche sur le web ou le bureau en fonction de l’endroit où vous ajoutez l’onglet de **conversation** dans le `staticTabs` tableau.

```json
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

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>Ajouter `registerOnFocused` une API pour les onglets ou les applications personnelles

`registerOnFocused`L’API du SDK vous permet d’utiliser un clavier sur Teams. Vous pouvez revenir à une application personnelle et maintenir le focus sur un onglet ou une application personnelle à l’aide des touches Ctrl, Shift et F6. Par exemple, vous pouvez vous éloigner de l’application personnelle pour rechercher quelque chose, puis revenir à l’application personnelle ou utiliser Ctrl+F6 pour contourner les endroits requis. 

Le code suivant fournit un exemple de définition de handler sur le SDK lorsque le focus doit être renvoyé à `registerFocusEnterHandler` l’onglet ou à l’application personnelle :

```csharp
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

Une fois que le handler est déclenché avec le mot clé, le handler est appelé avec une fonction de rappel qui prend un `focusEnter` `registerFocusEnterHandler` paramètre appelé `focusEnterHandler` `navigateForward` . La valeur de `navigateForward` détermine le type d’événements. Il `focusEnterHandler` est appelé uniquement par Ctrl+F6 et non par la touche de tabulation.   
Les clés utiles pour les événements de déplacement Teams sont les suivantes :    
* Forward event -> Ctrl+F6 keys
* Événement backward - > touches Ctrl+Shift+F6

```csharp
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

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="Exemple d’options pour l’ajout de l’API registerOnFocussed" border="false":::

#### <a name="personal-app---forward-event"></a>Application personnelle - Événement Forward

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="Exemple d’options pour l’ajout d’un déplacement de l’API registerOnFocussed" border="false":::

#### <a name="personal-app---backward-event"></a>Application personnelle - Événement arrière

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="Exemple d’options pour ajouter un déplacement arrière de l’API registerOnFocussed" border="false":::

### <a name="tab"></a>Tab

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="Exemple d’options pour l’ajout de l’API registerOnFocussed pour l’onglet" border="false":::

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
