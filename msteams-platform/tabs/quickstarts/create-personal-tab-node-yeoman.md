---
title: 'Quickstart: Créez un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams'
author: laujan
description: Un guide rapide pour créer un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566603"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="1da2e-103">Créez un onglet personnel personnalisé à l’aide Node.js et du générateur Yeoman pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1da2e-103">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="1da2e-104">Ce quickstart suit les étapes décrites dans [le Wiki Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) trouvé dans le référentiel microsoft OfficeDev GitHub’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1da2e-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="1da2e-105">Dans ce quickstart nous allons walk-through créer un onglet personnel personnalisé en utilisant [le Teams générateur Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="1da2e-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="1da2e-106">Nous téléchargerons également l’application sur Team.</span><span class="sxs-lookup"><span data-stu-id="1da2e-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="1da2e-107">**Créer un onglet configurable ou statique**</span><span class="sxs-lookup"><span data-stu-id="1da2e-107">**Create a configurable or static tab**</span></span>

<span data-ttu-id="1da2e-108">Utilisez les touches fléchées pour sélectionner l’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="1da2e-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1da2e-109">Le composant de *chemin yourDefaultTabNameTab*, référencé dans ce quickstart, est la valeur que vous avez entré dans le générateur pour *nom d’onglet par* défaut plus le mot *Onglet*.</span><span class="sxs-lookup"><span data-stu-id="1da2e-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="1da2e-110">Par exemple: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="1da2e-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="1da2e-111">Créez votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="1da2e-111">Create your personal tab</span></span>

<span data-ttu-id="1da2e-112">Pour ajouter un onglet personnel à cette application, vous créerez une page de contenu et mettrez à jour les fichiers existants :</span><span class="sxs-lookup"><span data-stu-id="1da2e-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="1da2e-113">Dans votre éditeur de code, créez un nouveau fichier HTML, **personal.html** et ajoutez la majoration suivante :</span><span class="sxs-lookup"><span data-stu-id="1da2e-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="1da2e-114">Enregistrez **personal.html** dans le dossier Web de **votre** application :</span><span class="sxs-lookup"><span data-stu-id="1da2e-114">Save **personal.html** in your application's **web** folder:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- <span data-ttu-id="1da2e-115">Ouvrez **manifest.jsdans** votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="1da2e-115">Open **manifest.json** in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

<span data-ttu-id="1da2e-116">Ajouter ce qui suit au tableau `staticTabs` vide ( ) et ajouter `staticTabs":[]` l’objet JSON suivant:</span><span class="sxs-lookup"><span data-stu-id="1da2e-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="1da2e-117">N’oubliez pas de mettre à jour le composant de chemin **« contentURL »** **yourDefaultTabNameTab** avec votre nom d’onglet réel.</span><span class="sxs-lookup"><span data-stu-id="1da2e-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="1da2e-118">Enregistrez la mise **à jourmanifest.jssur**.</span><span class="sxs-lookup"><span data-stu-id="1da2e-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="1da2e-119">Votre page de contenu doit être servie dans un IFrame.</span><span class="sxs-lookup"><span data-stu-id="1da2e-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="1da2e-120">Ouvrez **Tab.ts dans** votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="1da2e-120">Open **Tab.ts** in your code editor:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- <span data-ttu-id="1da2e-121">Ajoutez ce qui suit à la liste des décorateurs IFrame :</span><span class="sxs-lookup"><span data-stu-id="1da2e-121">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- <span data-ttu-id="1da2e-122">Assurez-vous d’enregistrer le fichier **Tab.ts mis à** jour.</span><span class="sxs-lookup"><span data-stu-id="1da2e-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="1da2e-123">Votre code d’onglet est complet.</span><span class="sxs-lookup"><span data-stu-id="1da2e-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="1da2e-124">Créez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="1da2e-124">Build and Run Your Application</span></span>

<span data-ttu-id="1da2e-125">Ouvrez une invite de commande dans votre répertoire de projet pour accomplir les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="1da2e-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="1da2e-126">Pour voir votre onglet personnel, rendez-vous sur `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="1da2e-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![capture d’écran onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="1da2e-128">Établissez un tunnel sécurisé à votre onglet</span><span class="sxs-lookup"><span data-stu-id="1da2e-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="1da2e-129">Microsoft Teams est un produit entièrement basé sur le cloud et exige que le contenu de votre onglet soit disponible à partir du cloud à l’aide des paramètres HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1da2e-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="1da2e-130">Teams n’autorise pas l’hébergement local, par conséquent, vous devez soit publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL orientée vers Internet.</span><span class="sxs-lookup"><span data-stu-id="1da2e-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="1da2e-131">Pour tester votre extension d’onglet, vous [utiliserez ngrok](https://ngrok.com/docs), qui est intégré dans cette application.</span><span class="sxs-lookup"><span data-stu-id="1da2e-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="1da2e-132">Ngrok est un outil logiciel proxy inversé qui créera un tunnel vers les points de terminaison HTTPS accessibles au public de votre serveur Web en cours d’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="1da2e-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="1da2e-133">Les paramètres Web de votre serveur seront disponibles pendant la session en cours sur votre machine locale.</span><span class="sxs-lookup"><span data-stu-id="1da2e-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="1da2e-134">Lorsque la machine est arrêtée ou s’enort, le service ne sera plus disponible.</span><span class="sxs-lookup"><span data-stu-id="1da2e-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="1da2e-135">Dans votre invite de commande, sortez localhost et entrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="1da2e-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="1da2e-136">Une fois que votre onglet a été téléchargé sur les équipes Microsoft, via **ngrok**, et enregistré avec succès, vous pouvez le voir en Teams jusqu’à la fin de votre session tunnel.</span><span class="sxs-lookup"><span data-stu-id="1da2e-136">After your tab has been uploaded to Microsoft teams, via **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="1da2e-137">Télécharger votre demande à Teams</span><span class="sxs-lookup"><span data-stu-id="1da2e-137">Upload your application to Teams</span></span>

- <span data-ttu-id="1da2e-138">Ouvrez le Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="1da2e-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="1da2e-139">Si vous utilisez la [version Web, vous pouvez](https://teams.microsoft.com) inspecter votre code front-end à l’aide des outils de développement de votre [navigateur](~/tabs/how-to/developer-tools.md).</span><span class="sxs-lookup"><span data-stu-id="1da2e-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="1da2e-140">Dans le **panneau YourTeams** à gauche, sélectionnez le `...` menu à côté de l’équipe que vous utilisez pour tester votre onglet et choisir **l’équipe Manage**.</span><span class="sxs-lookup"><span data-stu-id="1da2e-140">In the **YourTeams** panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="1da2e-141">Dans le panneau principal, **sélectionnez Apps** à partir de la barre d’onglet **et choisissez Télécharger une application** personnalisée située dans le coin inférieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="1da2e-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="1da2e-142">Ouvrez votre répertoire de projet, parcourez **le dossier ./package,** sélectionnez le dossier zip, cliquez à droite et choisissez **Open**.</span><span class="sxs-lookup"><span data-stu-id="1da2e-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="1da2e-143">Votre onglet sera téléchargé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1da2e-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="1da2e-144">Consultez vos onglets personnels</span><span class="sxs-lookup"><span data-stu-id="1da2e-144">View your personal tabs</span></span>

<span data-ttu-id="1da2e-145">Dans le navbar situé à l’extrême gauche du client Teams, sélectionnez le `...` menu et choisissez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="1da2e-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

## <a name="next-step"></a><span data-ttu-id="1da2e-146">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1da2e-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1da2e-147">Créez un onglet personnel à l’aide d’ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="1da2e-147">Create a personal tab using ASP.NETCore</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
