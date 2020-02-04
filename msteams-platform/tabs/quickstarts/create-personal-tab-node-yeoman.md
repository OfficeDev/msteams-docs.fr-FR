---
title: 'QuickStart : créer un onglet personnel personnalisé avec node. js et le générateur Yeoman pour Microsoft teams'
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673532"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="cb410-103">QuickStart : créer un onglet personnel personnalisé avec node. js et le générateur Yeoman pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="cb410-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="cb410-104">Ce démarrage rapide suit les étapes décrites dans le wiki de [création de votre première application Microsoft teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) dans le référentiel GitHub de Microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="cb410-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="cb410-105">Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet personnel personnalisé à l’aide du [Générateur Yeoman teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="cb410-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="cb410-106">Nous allons également télécharger l’application vers Team.</span><span class="sxs-lookup"><span data-stu-id="cb410-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="cb410-107">**Voulez-vous créer un onglet configurable ou statique ?**</span><span class="sxs-lookup"><span data-stu-id="cb410-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="cb410-108">Utilisez les touches de direction pour sélectionner l’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="cb410-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cb410-109">Le composant de chemin d’accès *yourDefaultTabNameTab*, référencé dans ce démarrage rapide, est la valeur que vous avez entrée dans le générateur pour le nom de l' *onglet par défaut* , ainsi que l' *onglet*mot.</span><span class="sxs-lookup"><span data-stu-id="cb410-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="cb410-110">Par exemple : DefaultTabName : *MyTab* => */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="cb410-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="cb410-111">Créer votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="cb410-111">Create your personal tab</span></span>

<span data-ttu-id="cb410-112">Pour ajouter un onglet personnel à cette application, vous allez créer une page de contenu et mettre à jour les fichiers existants :</span><span class="sxs-lookup"><span data-stu-id="cb410-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="cb410-113">Dans votre éditeur de code, créez un fichier HTML, **Personal. html** et ajoutez le balisage suivant :</span><span class="sxs-lookup"><span data-stu-id="cb410-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="cb410-114">Enregistrez **Personal. html** dans le dossier **Web** de votre application :</span><span class="sxs-lookup"><span data-stu-id="cb410-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="cb410-115">Ouvrez **Manifest. JSON** dans votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="cb410-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="cb410-116">Ajoutez ce qui suit dans le `staticTabs` tableau vide`staticTabs":[]`() et ajoutez l’objet JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="cb410-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="cb410-117">N’oubliez pas de mettre à jour le composant de chemin d’accès **« contentURL »** **yourDefaultTabNameTab** avec votre nom d’onglet réel.</span><span class="sxs-lookup"><span data-stu-id="cb410-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="cb410-118">Enregistrez la mise à jour de **Manifest. JSON**.</span><span class="sxs-lookup"><span data-stu-id="cb410-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="cb410-119">Votre page de contenu doit être fournie dans un IFrame.</span><span class="sxs-lookup"><span data-stu-id="cb410-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="cb410-120">Ouvrez **Tab. TS** dans votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="cb410-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="cb410-121">Ajoutez les éléments suivants à la liste des décorateurs IFrame :</span><span class="sxs-lookup"><span data-stu-id="cb410-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="cb410-122">Veillez à enregistrer le fichier **Tab. TS** mis à jour.</span><span class="sxs-lookup"><span data-stu-id="cb410-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="cb410-123">Votre code d’onglet est complet.</span><span class="sxs-lookup"><span data-stu-id="cb410-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="cb410-124">Création et exécution de votre application</span><span class="sxs-lookup"><span data-stu-id="cb410-124">Build and Run Your Application</span></span>

<span data-ttu-id="cb410-125">Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="cb410-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="cb410-126">Pour afficher votre onglet personnel, accédez à`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="cb410-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![capture d’écran de l’onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="cb410-128">Établir un tunnel sécurisé vers votre onglet</span><span class="sxs-lookup"><span data-stu-id="cb410-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="cb410-129">Microsoft teams est un produit entièrement basé sur le Cloud et nécessite que le contenu de votre onglet soit disponible dans le nuage à l’aide de points de terminaison HTTPs.</span><span class="sxs-lookup"><span data-stu-id="cb410-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="cb410-130">Teams n’autorise pas l’hébergement local ; par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="cb410-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="cb410-131">Pour tester votre extension d’onglet, vous utiliserez [ngrok](https://ngrok.com/docs), qui est intégré à cette application.</span><span class="sxs-lookup"><span data-stu-id="cb410-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="cb410-132">Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers vos points de terminaison HTTPs de serveur Web en cours d’exécution locaux.</span><span class="sxs-lookup"><span data-stu-id="cb410-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="cb410-133">Les points de terminaison Web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="cb410-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="cb410-134">Lorsque l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="cb410-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="cb410-135">À l’invite de commandes, quittez localhost et entrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="cb410-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="cb410-136">Une fois que votre onglet a été téléchargé dans Microsoft Teams, via *ngrok*, et enregistré correctement, vous pouvez l’afficher dans teams jusqu’à ce que la session de tunnel se termine.</span><span class="sxs-lookup"><span data-stu-id="cb410-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="cb410-137">Chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="cb410-137">Upload your application to Teams</span></span>

- <span data-ttu-id="cb410-138">Ouvrez le client Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cb410-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="cb410-139">Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="cb410-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="cb410-140">Dans le volet *YourTeams* à gauche, sélectionnez le `...` menu en regard de l’équipe que vous utilisez pour tester votre onglet, puis sélectionnez **gérer l’équipe**.</span><span class="sxs-lookup"><span data-stu-id="cb410-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="cb410-141">Dans le panneau principal, sélectionnez **applications** dans la barre d’onglets et choisissez **Télécharger une application personnalisée** située dans l’angle inférieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="cb410-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="cb410-142">Ouvrez le répertoire de votre projet, accédez au dossier **./Package** , sélectionnez le dossier zip, cliquez avec le bouton droit, puis choisissez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="cb410-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="cb410-143">Votre onglet est chargé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cb410-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="cb410-144">Afficher vos onglets personnels</span><span class="sxs-lookup"><span data-stu-id="cb410-144">View your personal tabs</span></span>

<span data-ttu-id="cb410-145">Dans la barre de navigation située à l’extrême gauche du client Teams, sélectionnez `...` le menu et choisissez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="cb410-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
