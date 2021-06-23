---
title: 'Démarrage rapide : créer un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams'
author: surbhigupta
description: Guide de démarrage rapide sur la création d’un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 220d1018f174fc935a10311723a730ebc74ccc33
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069204"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="db4e6-103">Créer un onglet personnel personnalisé à l'Node.js et le générateur Yeoman pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="db4e6-103">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="db4e6-104">Ce démarrage rapide suit les étapes décrites dans le [Wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) de votre première application Microsoft Teams dans le référentiel d’GitHub Microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="db4e6-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="db4e6-105">Dans ce démarrage rapide, nous allons créer un onglet personnel personnalisé à l’aide Teams [générateur Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="db4e6-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="db4e6-106">Nous allons également télécharger l’application dans Team.</span><span class="sxs-lookup"><span data-stu-id="db4e6-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="db4e6-107">**Créer un onglet configurable ou statique**</span><span class="sxs-lookup"><span data-stu-id="db4e6-107">**Create a configurable or static tab**</span></span>

<span data-ttu-id="db4e6-108">Utilisez les touches de direction pour sélectionner l’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="db4e6-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="db4e6-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span><span class="sxs-lookup"><span data-stu-id="db4e6-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="db4e6-110">Par exemple : DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="db4e6-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="db4e6-111">Créer votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="db4e6-111">Create your personal tab</span></span>

<span data-ttu-id="db4e6-112">Pour ajouter un onglet personnel à cette application, vous allez créer une page de contenu et mettre à jour les fichiers existants :</span><span class="sxs-lookup"><span data-stu-id="db4e6-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="db4e6-113">Dans votre éditeur de code, créez un fichier HTML, **personal.html** et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="db4e6-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="db4e6-114">Enregistrez **personal.html** dans le dossier **web de votre** application :</span><span class="sxs-lookup"><span data-stu-id="db4e6-114">Save **personal.html** in your application's **web** folder:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- <span data-ttu-id="db4e6-115">Ouvrez **manifest.jsdans** votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="db4e6-115">Open **manifest.json** in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

<span data-ttu-id="db4e6-116">Ajoutez ce qui suit au tableau `staticTabs` vide ( ) et `staticTabs":[]` ajoutez l’objet JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="db4e6-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="db4e6-117">N’oubliez pas de mettre à jour le composant de chemin d’accès **« contentURL** **» yourDefaultTabNameTab** avec votre nom d’onglet réel.</span><span class="sxs-lookup"><span data-stu-id="db4e6-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="db4e6-118">Enregistrez lemanifest.js **mis à jour sur**.</span><span class="sxs-lookup"><span data-stu-id="db4e6-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="db4e6-119">Votre page de contenu doit être servie dans un IFrame.</span><span class="sxs-lookup"><span data-stu-id="db4e6-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="db4e6-120">Ouvrez **Tab.ts dans** votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="db4e6-120">Open **Tab.ts** in your code editor:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- <span data-ttu-id="db4e6-121">Ajoutez ce qui suit à la liste descorateurs IFrame :</span><span class="sxs-lookup"><span data-stu-id="db4e6-121">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- <span data-ttu-id="db4e6-122">Veillez à enregistrer le fichier **Tab.ts** mis à jour.</span><span class="sxs-lookup"><span data-stu-id="db4e6-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="db4e6-123">Le code de l’onglet est terminé.</span><span class="sxs-lookup"><span data-stu-id="db4e6-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="db4e6-124">Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="db4e6-124">Build and Run Your Application</span></span>

<span data-ttu-id="db4e6-125">Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="db4e6-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="db4e6-126">Pour afficher votre onglet personnel, consultez la page `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="db4e6-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![capture d’écran de l’onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="db4e6-128">Établir un tunnel sécurisé vers votre onglet</span><span class="sxs-lookup"><span data-stu-id="db4e6-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="db4e6-129">Microsoft Teams est un produit entièrement basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="db4e6-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="db4e6-130">Teams n’autorise pas l’hébergement local, par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL internet.</span><span class="sxs-lookup"><span data-stu-id="db4e6-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="db4e6-131">Pour tester votre extension d’onglet, vous allez utiliser [ngrok,](https://ngrok.com/docs)qui est intégré à cette application.</span><span class="sxs-lookup"><span data-stu-id="db4e6-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="db4e6-132">Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="db4e6-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="db4e6-133">Les points de terminaison web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="db4e6-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="db4e6-134">Lorsque l’ordinateur est arrêté ou mis en veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="db4e6-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="db4e6-135">Dans votre invite de commandes, quittez localhost et entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="db4e6-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="db4e6-136">Une fois que votre onglet a été téléchargé vers Microsoft Teams, via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session tunnel.</span><span class="sxs-lookup"><span data-stu-id="db4e6-136">After your tab has been uploaded to Microsoft teams, via **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="db4e6-137">Télécharger votre application à Teams</span><span class="sxs-lookup"><span data-stu-id="db4e6-137">Upload your application to Teams</span></span>

- <span data-ttu-id="db4e6-138">Ouvrez le client Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="db4e6-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="db4e6-139">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="db4e6-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="db4e6-140">Dans le **panneau YourTeams** sur la gauche, sélectionnez le menu en face de l’équipe que vous utilisez pour tester votre onglet et choisissez `...` Gérer **l’équipe.**</span><span class="sxs-lookup"><span data-stu-id="db4e6-140">In the **YourTeams** panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="db4e6-141">Dans le panneau  principal, sélectionnez Applications dans la barre d’onglets et **choisissez Télécharger** une application personnalisée située dans le coin inférieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="db4e6-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="db4e6-142">Ouvrez le répertoire de votre projet, accédez au dossier **./package,** sélectionnez le dossier zip, cliquez avec le bouton droit, puis choisissez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="db4e6-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="db4e6-143">Votre onglet est chargé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="db4e6-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="db4e6-144">Afficher vos onglets personnels</span><span class="sxs-lookup"><span data-stu-id="db4e6-144">View your personal tabs</span></span>

<span data-ttu-id="db4e6-145">Dans la barre de navigation située à l’extrême gauche du client Teams, sélectionnez le menu et choisissez votre application dans `...` la liste.</span><span class="sxs-lookup"><span data-stu-id="db4e6-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

## <a name="next-step"></a><span data-ttu-id="db4e6-146">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="db4e6-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db4e6-147">Créer un onglet personnel à l’aide d’ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="db4e6-147">Create a personal tab using ASP.NETCore</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
