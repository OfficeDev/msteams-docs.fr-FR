---
title: Créer un onglet de canal et de groupe personnalisé avec node. js et le générateur Yeoman pour Microsoft teams
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet de canal et de groupe avec le générateur Yeoman pour Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: c5e028dcc117d729f2bf366923d03568b7f557a4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673747"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="8ba05-103">Créer un onglet de canal et de groupe personnalisé avec node. js et le générateur Yeoman pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="8ba05-103">Create a custom channel and group tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="8ba05-104">Ce démarrage rapide suit les étapes décrites dans le wiki de [création de votre première application Microsoft teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) dans le référentiel GitHub de Microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="8ba05-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="8ba05-105">Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet de canal et de groupe personnalisé à l’aide du [Générateur Yeoman teams](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="8ba05-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="8ba05-106">**Voulez-vous créer un onglet configurable ou statique ?**</span><span class="sxs-lookup"><span data-stu-id="8ba05-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="8ba05-107">Utilisez les touches de direction pour sélectionner l’onglet configurable.</span><span class="sxs-lookup"><span data-stu-id="8ba05-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="8ba05-108">**Quelles étendues envisagez-vous d’utiliser pour votre onglet ?**</span><span class="sxs-lookup"><span data-stu-id="8ba05-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="8ba05-109">Vous pouvez sélectionner une équipe et/ou une conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="8ba05-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="8ba05-110">**Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (O/n)**</span><span class="sxs-lookup"><span data-stu-id="8ba05-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="8ba05-111">Sélectionnez **n**.</span><span class="sxs-lookup"><span data-stu-id="8ba05-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8ba05-112">Le composant de chemin d’accès **yourDefaultTabNameTab**, référencé dans ce démarrage rapide, est la valeur que vous avez entrée dans le générateur pour le nom de l' **onglet par défaut** , ainsi que l' **onglet**mot.</span><span class="sxs-lookup"><span data-stu-id="8ba05-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="8ba05-113">Par exemple : DefaultTabName : **MyTab** => **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="8ba05-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="8ba05-114">Dans le répertoire de votre projet, accédez à l’un des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8ba05-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="8ba05-115">C’est ici que vous trouverez votre logique d’onglet.</span><span class="sxs-lookup"><span data-stu-id="8ba05-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="8ba05-116">Recherchez la `render()` méthode et ajoutez la balise et le contenu suivants `<div>` en haut du `<PanelBody>` code de conteneur :</span><span class="sxs-lookup"><span data-stu-id="8ba05-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="8ba05-117">Veillez à enregistrer le fichier mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8ba05-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="8ba05-118">Création et exécution de votre application</span><span class="sxs-lookup"><span data-stu-id="8ba05-118">Build and Run Your Application</span></span>

<span data-ttu-id="8ba05-119">Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="8ba05-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="8ba05-120">Pour afficher la page de configuration de votre `https://localhost:3007/<yourDefaultAppNameTab>/config.html`onglet, accédez à.</span><span class="sxs-lookup"><span data-stu-id="8ba05-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="8ba05-121">Vous devez voir les éléments ci-après :</span><span class="sxs-lookup"><span data-stu-id="8ba05-121">You should see the following:</span></span>

![capture d’écran de la page de configuration](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="8ba05-123">Établir un tunnel sécurisé vers votre onglet</span><span class="sxs-lookup"><span data-stu-id="8ba05-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="8ba05-124">Microsoft teams est un produit entièrement basé sur le Cloud et nécessite que le contenu de votre onglet soit disponible dans le nuage à l’aide de points de terminaison HTTPs.</span><span class="sxs-lookup"><span data-stu-id="8ba05-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="8ba05-125">Teams n’autorise pas l’hébergement local ; par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="8ba05-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="8ba05-126">Pour tester votre extension d’onglet, vous utiliserez [ngrok](https://ngrok.com/docs), qui est intégré à cette application.</span><span class="sxs-lookup"><span data-stu-id="8ba05-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="8ba05-127">Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers vos points de terminaison HTTPs de serveur Web en cours d’exécution locaux.</span><span class="sxs-lookup"><span data-stu-id="8ba05-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="8ba05-128">Les points de terminaison Web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8ba05-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="8ba05-129">Lorsque l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="8ba05-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="8ba05-130">À l’invite de commandes, quittez localhost et entrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8ba05-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="8ba05-131">Une fois que votre onglet a été téléchargé dans Microsoft teams et enregistré correctement, vous pouvez l’afficher dans la Galerie des onglets, l’ajouter à la barre d’onglets et interagir avec lui jusqu’à la fin de votre session de tunnel ngrok.</span><span class="sxs-lookup"><span data-stu-id="8ba05-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="8ba05-132">Si vous redémarrez votre session ngrok, vous devrez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="8ba05-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="8ba05-133">Chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="8ba05-133">Upload your application to Teams</span></span>

- <span data-ttu-id="8ba05-134">Ouvrez le client Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8ba05-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="8ba05-135">Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8ba05-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="8ba05-136">Dans le volet *YourTeams* à gauche, sélectionnez le `...` menu en regard de l’équipe que vous utilisez pour tester votre onglet, puis sélectionnez **gérer l’équipe**.</span><span class="sxs-lookup"><span data-stu-id="8ba05-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="8ba05-137">Dans le panneau principal, sélectionnez **applications** dans la barre d’onglets et choisissez **Télécharger une application personnalisée** située dans l’angle inférieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="8ba05-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="8ba05-138">Ouvrez le répertoire de votre projet, accédez au dossier **./Package** , sélectionnez le dossier zip du package d’application, puis choisissez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="8ba05-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="8ba05-139">Votre onglet est chargé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8ba05-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="8ba05-140">Revenez à votre équipe, choisissez le canal où vous souhaitez afficher l’onglet, sélectionnez ➕ dans la barre d’onglets, puis choisissez votre onglet dans la Galerie.</span><span class="sxs-lookup"><span data-stu-id="8ba05-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="8ba05-141">Suivez les instructions relatives à l’ajout d’un onglet. Notez qu’il existe une boîte de dialogue de configuration personnalisée pour l’onglet canal/groupe.</span><span class="sxs-lookup"><span data-stu-id="8ba05-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="8ba05-142">Sélectionnez **Enregistrer** et votre onglet est ajouté à la barre d’onglets de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="8ba05-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>
