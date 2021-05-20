---
title: Créez un canal personnalisé et un onglet de groupe avec Node.js et le générateur Yeoman pour Microsoft Teams
author: laujan
description: Un guide quickstart pour créer un canal et un onglet de groupe avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566643"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="f61d7-103">Créez un canal personnalisé et un onglet de groupe à l’aide Node.js et du générateur Yeoman pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f61d7-103">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="f61d7-104">Ce quickstart suit les étapes décrites dans [le Wiki Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) trouvé dans le référentiel microsoft OfficeDev GitHub’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f61d7-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="f61d7-105">Dans ce quickstart nous allons walk-through créer un canal personnalisé et onglet de groupe en [utilisant le Teams générateur Yeoman](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="f61d7-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="f61d7-106">**Voulez-vous créer un onglet configurable ou statique ?**</span><span class="sxs-lookup"><span data-stu-id="f61d7-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="f61d7-107">Utilisez les touches fléchées pour sélectionner l’onglet configurable.</span><span class="sxs-lookup"><span data-stu-id="f61d7-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="f61d7-108">**Quelles étendues avez-vous l’intention d’utiliser pour votre onglet ?**</span><span class="sxs-lookup"><span data-stu-id="f61d7-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="f61d7-109">Vous pouvez sélectionner une équipe et/ou un chat de groupe</span><span class="sxs-lookup"><span data-stu-id="f61d7-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="f61d7-110">**Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="f61d7-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="f61d7-111">Sélectionnez **n**.</span><span class="sxs-lookup"><span data-stu-id="f61d7-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f61d7-112">Le composant de **chemin yourDefaultTabNameTab**, référencé dans ce quickstart, est la valeur que vous avez entré dans le générateur pour **nom d’onglet par** défaut plus le mot **Onglet**.</span><span class="sxs-lookup"><span data-stu-id="f61d7-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="f61d7-113">Par exemple: DefaultTabName: **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="f61d7-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="f61d7-114">Dans votre répertoire de projet, accédez aux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f61d7-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="f61d7-115">C’est là que vous trouverez votre logique onglet.</span><span class="sxs-lookup"><span data-stu-id="f61d7-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="f61d7-116">`render()`Localisez la méthode et ajoutez la balise et le contenu suivants en haut du code de `<div>` conteneur `<PanelBody>` :</span><span class="sxs-lookup"><span data-stu-id="f61d7-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="f61d7-117">Assurez-vous d’enregistrer le fichier mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f61d7-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="f61d7-118">Créez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="f61d7-118">Build and Run Your Application</span></span>

<span data-ttu-id="f61d7-119">Ouvrez une invite de commande dans votre répertoire de projet pour accomplir les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="f61d7-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="f61d7-120">Pour afficher votre page de configuration d’onglet, rendez-vous `https://localhost:3007/<yourDefaultAppNameTab>/config.html` sur .</span><span class="sxs-lookup"><span data-stu-id="f61d7-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="f61d7-121">Vous devez voir les éléments ci-après :</span><span class="sxs-lookup"><span data-stu-id="f61d7-121">You should see the following:</span></span>

![capture d’écran de page de configuration](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="f61d7-123">Établissez un tunnel sécurisé à votre onglet</span><span class="sxs-lookup"><span data-stu-id="f61d7-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="f61d7-124">Microsoft Teams est un produit entièrement basé sur le cloud et exige que le contenu de votre onglet soit disponible à partir du cloud à l’aide des paramètres HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f61d7-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="f61d7-125">Teams n’autorise pas l’hébergement local, par conséquent, vous devez soit publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL orientée vers Internet.</span><span class="sxs-lookup"><span data-stu-id="f61d7-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="f61d7-126">Pour tester votre extension d’onglet, vous [utiliserez ngrok](https://ngrok.com/docs), qui est intégré dans cette application.</span><span class="sxs-lookup"><span data-stu-id="f61d7-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="f61d7-127">Ngrok est un outil logiciel proxy inversé qui créera un tunnel vers les points de terminaison HTTPS accessibles au public de votre serveur Web en cours d’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="f61d7-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="f61d7-128">Les paramètres Web de votre serveur seront disponibles pendant la session en cours sur votre machine locale.</span><span class="sxs-lookup"><span data-stu-id="f61d7-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="f61d7-129">Lorsque la machine est arrêtée ou s’enort, le service ne sera plus disponible.</span><span class="sxs-lookup"><span data-stu-id="f61d7-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="f61d7-130">Dans votre invite de commande, sortez localhost et entrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f61d7-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="f61d7-131">Une fois que votre onglet a été téléchargé sur les équipes Microsoft et enregistré avec succès, vous pouvez le voir dans la galerie d’onglets, l’ajouter à la barre d’onglets et interagir avec lui jusqu’à la fin de votre session tunnel ngrok.</span><span class="sxs-lookup"><span data-stu-id="f61d7-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="f61d7-132">Si vous redémarrez votre session ngrok, vous devrez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="f61d7-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="f61d7-133">Télécharger votre demande à Teams</span><span class="sxs-lookup"><span data-stu-id="f61d7-133">Upload your application to Teams</span></span>

- <span data-ttu-id="f61d7-134">Ouvrez le Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="f61d7-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="f61d7-135">Si vous utilisez la [version Web, vous pouvez](https://teams.microsoft.com) inspecter votre code front-end à l’aide des outils de développement de votre [navigateur](~/tabs/how-to/developer-tools.md).</span><span class="sxs-lookup"><span data-stu-id="f61d7-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="f61d7-136">Dans le *panneau YourTeams* à gauche, sélectionnez le `...` menu à côté de l’équipe que vous utilisez pour tester votre onglet et choisir **l’équipe Manage**.</span><span class="sxs-lookup"><span data-stu-id="f61d7-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="f61d7-137">Dans le panneau principal, **sélectionnez Apps** à partir de la barre d’onglet **et choisissez Télécharger une application** personnalisée située dans le coin inférieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="f61d7-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="f61d7-138">Ouvrez votre répertoire de projet, naviguez sur le **dossier ./package,** sélectionnez le dossier zip du paquet d’application et choisissez **Open**.</span><span class="sxs-lookup"><span data-stu-id="f61d7-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="f61d7-139">Votre onglet sera téléchargé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="f61d7-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="f61d7-140">Retournez dans votre équipe, choisissez le canal où vous souhaitez afficher l’onglet, sélectionnez ➕ de la barre d’onglets et choisissez votre onglet dans la galerie.</span><span class="sxs-lookup"><span data-stu-id="f61d7-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="f61d7-141">Suivez les instructions pour ajouter un onglet. Notez qu’il existe un dialogue de configuration personnalisé pour votre onglet canal/groupe.</span><span class="sxs-lookup"><span data-stu-id="f61d7-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="f61d7-142">Sélectionnez **Enregistrer** et votre onglet sera ajouté à la barre d’onglets du canal.</span><span class="sxs-lookup"><span data-stu-id="f61d7-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="next-step"></a><span data-ttu-id="f61d7-143">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="f61d7-143">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f61d7-144">Créez un onglet Canal personnalisé et groupe avec ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="f61d7-144">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)