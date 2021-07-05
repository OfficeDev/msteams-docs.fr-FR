---
title: 'Prise en main : créer votre première extension de messagerie'
author: adrianhall
description: Créez une extension de messagerie pour Microsoft Teams à l’aide du Kit de ressources Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3566bc55c9995a8407b1344fbdb7d1548e210046
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254287"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="07d47-103">Créez et exécutez votre première extension de messagerie basée sur la recherche dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="07d47-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="07d47-104">Dans ce didacticiel, vous  allez apprendre à créer une commande de recherche pour rechercher des données externes et insérer les résultats dans un message.</span><span class="sxs-lookup"><span data-stu-id="07d47-104">In this tutorial, you will learn how to create a *search command* to search for external data and insert the results into a message.</span></span> 

<span data-ttu-id="07d47-105">Il existe deux types **d’extension de messagerie** Teams :</span><span class="sxs-lookup"><span data-stu-id="07d47-105">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="07d47-106">Les [commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) vous permettent d’effectuer une recherche dans des systèmes externes et d’insérer les résultats de la recherche dans un message sous la forme d’une carte.</span><span class="sxs-lookup"><span data-stu-id="07d47-106">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="07d47-107">Les [commandes d’action](../messaging-extensions/how-to/action-commands/define-action-command.md) vous permettent de présenter vos utilisateurs à l’aide d’un menu contextuel modal pour collecter ou afficher des informations, puis de traiter leur interaction et de renvoyer les informations à Teams.</span><span class="sxs-lookup"><span data-stu-id="07d47-107">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="07d47-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="07d47-108">Before you begin</span></span>

<span data-ttu-id="07d47-109">Assurez-vous que votre environnement de développement est installé en installant les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="07d47-109">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07d47-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="07d47-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="07d47-111">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="07d47-111">Create your project</span></span>

<span data-ttu-id="07d47-112">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="07d47-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="07d47-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="07d47-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="07d47-114">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="07d47-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="07d47-115">Sélectionnez l Teams dans la barre latérale pour ouvrir le Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="07d47-115">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="07d47-117">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="07d47-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="07d47-119">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="07d47-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="07d47-121">Dans la section **Sélectionner des fonctionnalités,** **sélectionnez Extension de message,** **Désélectionner l’onglet** et **sélectionner OK.**</span><span class="sxs-lookup"><span data-stu-id="07d47-121">In the **Select capabilities** section, select **Message Extension**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="07d47-123">Dans la section **Inscription du** bot, **sélectionnez Créer une nouvelle inscription de bot.**</span><span class="sxs-lookup"><span data-stu-id="07d47-123">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Sélectionner l’inscription d’un nouveau bot":::

   > [!NOTE]
   > <span data-ttu-id="07d47-125">Les extensions de messagerie ont recours à des bots pour fournir un dialogue entre l’utilisateur et votre code.</span><span class="sxs-lookup"><span data-stu-id="07d47-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="07d47-126">Dans la section **Langage de** programmation, **sélectionnez JavaScript.**</span><span class="sxs-lookup"><span data-stu-id="07d47-126">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. <span data-ttu-id="07d47-128">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="07d47-128">Select a workspace folder.</span></span>  <span data-ttu-id="07d47-129">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="07d47-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="07d47-130">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="07d47-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="07d47-131">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="07d47-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="07d47-132">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="07d47-132">Press **Enter** to continue.</span></span>

   <span data-ttu-id="07d47-133">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="07d47-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="07d47-134">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="07d47-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="07d47-135">Utilisez le CLI `teamsfx` pou créer votre premier projet.</span><span class="sxs-lookup"><span data-stu-id="07d47-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="07d47-136">Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="07d47-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="07d47-137">Le CLI parcourt quelques questions pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="07d47-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="07d47-138">Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).</span><span class="sxs-lookup"><span data-stu-id="07d47-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="07d47-139">Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="07d47-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="07d47-140">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="07d47-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="07d47-141">Sélectionnez **l’extension de message** et désélectionne **l’onglet**.</span><span class="sxs-lookup"><span data-stu-id="07d47-141">Select the **Message Extension** and deselect **Tab**.</span></span>
1. <span data-ttu-id="07d47-142">Sélectionner **Créer l’inscription d’un nouveau bot**.</span><span class="sxs-lookup"><span data-stu-id="07d47-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="07d47-143">Sélectionnez **JavaScript** comme langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="07d47-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="07d47-144">Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.</span><span class="sxs-lookup"><span data-stu-id="07d47-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="07d47-145">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="07d47-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="07d47-146">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="07d47-146">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="07d47-147">Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.</span><span class="sxs-lookup"><span data-stu-id="07d47-147">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="07d47-148">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="07d47-148">Take a tour of the source code</span></span>

<span data-ttu-id="07d47-149">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="07d47-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="07d47-150">Une extension de messagerie utilise [Bot Framework](https://docs.botframework.com) pour autoriser l’utilisateur à interagir avec votre service via une conversation.</span><span class="sxs-lookup"><span data-stu-id="07d47-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="07d47-151">Après structuration, votre projet ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="07d47-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Disposition de fichier d’un projet bot.":::

<span data-ttu-id="07d47-153">Le code bot est stocké dans le répertoire `bot`.</span><span class="sxs-lookup"><span data-stu-id="07d47-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="07d47-154">Le `bot/messageExtensionBot.js` est le principal point d’entrée pour l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="07d47-154">The `bot/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="07d47-155">Familiarisez-vous avec les bots en dehors de Teams avant d’intégrer votre premier bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="07d47-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="07d47-156">Vous trouverez d’autres informations sur les bots en examinant les didacticiels [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="07d47-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="07d47-157">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="07d47-157">Run your app locally</span></span>

<span data-ttu-id="07d47-158">Le Kit de ressources Teams vous permet d’héberger votre application localement.</span><span class="sxs-lookup"><span data-stu-id="07d47-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="07d47-159">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="07d47-159">To do this:</span></span>

- <span data-ttu-id="07d47-160">Une application Azure Active Directory est inscrite dans le client M365.</span><span class="sxs-lookup"><span data-stu-id="07d47-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="07d47-161">Un manifeste d’application est soumis au Portail des développeurs pour Teams.</span><span class="sxs-lookup"><span data-stu-id="07d47-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="07d47-162">Une API est exécutée à l’aide d’Azure Functions Core Tools pour prendre en charge votre application.</span><span class="sxs-lookup"><span data-stu-id="07d47-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="07d47-163">[ngrok](https://ngrok.io) est installé et utilisé pour fournir un tunnel entre Teams et votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="07d47-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="07d47-164">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="07d47-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="07d47-165">À Visual Studio Code, appuyez sur la **touche F5** pour exécuter votre application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="07d47-165">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="07d47-166">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="07d47-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="07d47-167">Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="07d47-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="07d47-168">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="07d47-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="07d47-169">Teams sera chargée dans un navigateur web et vous serez invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="07d47-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="07d47-170">Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="07d47-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="07d47-171">Connectez-vous à votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="07d47-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="07d47-172">Sélectionnez **Ajouter** pour ajouter l’application à votre compte.</span><span class="sxs-lookup"><span data-stu-id="07d47-172">Select **Add** to add the app to your account.</span></span>

   <span data-ttu-id="07d47-173">Une fois l’application chargée, vous êtes directement placé dans une boîte de dialogue de recherche :</span><span class="sxs-lookup"><span data-stu-id="07d47-173">After the app is loaded, you will be taken directly to a search dialog:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Votre extension de messagerie basée sur la recherche en action":::

   <span data-ttu-id="07d47-175">Tapez un texte dans la zone de recherche, puis sélectionnez l’une des options.</span><span class="sxs-lookup"><span data-stu-id="07d47-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="07d47-176">Une carte adaptative s’ajoute à votre zone d’entrée.</span><span class="sxs-lookup"><span data-stu-id="07d47-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="07d47-177">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="07d47-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="07d47-178">Lorsque vous appuyez sur **la touche F5,** le Teams Shared Computer Toolkit :</span><span class="sxs-lookup"><span data-stu-id="07d47-178">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="07d47-179">Inscrit votre application avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d47-179">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="07d47-180">Inscrit votre application pour le « chargement de version latéral » dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="07d47-180">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="07d47-181">Démarre le système principal de votre application en cours d’exécution localement à [l’aide des outils Azure Function Core](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="07d47-181">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="07d47-182">Démarre un tunnel ngrok pour Teams communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="07d47-182">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="07d47-183">Démarre Microsoft Teams avec une commande pour indiquer Teams charger une version de version de l’application.</span><span class="sxs-lookup"><span data-stu-id="07d47-183">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="07d47-184">Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="07d47-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="07d47-185">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement de version test d’une application.</span><span class="sxs-lookup"><span data-stu-id="07d47-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="07d47-186">Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="07d47-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="07d47-187">Vérifier l’absence de problèmes avant de charger la version test de votre application en utilisant [l’outil de validation d’application](https://dev.teams.microsoft.com/appvalidation.html) qui est inclus dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="07d47-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="07d47-188">Corrigez les erreurs pour charger correctement la version test de l’application.</span><span class="sxs-lookup"><span data-stu-id="07d47-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="07d47-189">Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</span><span class="sxs-lookup"><span data-stu-id="07d47-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="07d47-190">Avant le déploiement, l’application s’est exécutée localement :</span><span class="sxs-lookup"><span data-stu-id="07d47-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="07d47-191">Le serveur principal s’exécute en utilisant _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="07d47-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="07d47-192">Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.</span><span class="sxs-lookup"><span data-stu-id="07d47-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="07d47-193">Le déploiement implique la mise en service de ressources sur un abonnement Azure actif et le déploiement (chargement) du code du serveur principal et du serveur frontal pour l’application vers Azure.</span><span class="sxs-lookup"><span data-stu-id="07d47-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="07d47-194">Le serveur principal utilise une variété de services Azure, notamment Azure App Service et Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="07d47-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="07d47-195">Ajouter une page de configuration à votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="07d47-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="07d47-196">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="07d47-196">Code sample</span></span>

<span data-ttu-id="07d47-197">La Teams d’authentification de recherche pour les exemples de projets sur GitHub, montrent comment créer des extensions de messagerie qui incluent une page de configuration et l’authentification [bot service](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span><span class="sxs-lookup"><span data-stu-id="07d47-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="07d47-198">Les exemples montrent également comment créer des extensions de message qui acceptent les demandes de recherche et retournent les résultats une fois que l’utilisateur s’est inscrit.</span><span class="sxs-lookup"><span data-stu-id="07d47-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="07d47-199">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="07d47-199">**Sample name**</span></span> | <span data-ttu-id="07d47-200">**Description**</span><span class="sxs-lookup"><span data-stu-id="07d47-200">**Description**</span></span> | <span data-ttu-id="07d47-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="07d47-201">**.NET**</span></span> | <span data-ttu-id="07d47-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="07d47-202">**Node.js**</span></span> | <span data-ttu-id="07d47-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="07d47-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="07d47-204">Générateur de bot</span><span class="sxs-lookup"><span data-stu-id="07d47-204">Bot builder</span></span> | <span data-ttu-id="07d47-205">Pour créer des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="07d47-205">To create messaging extensions.</span></span> | [<span data-ttu-id="07d47-206">View</span><span class="sxs-lookup"><span data-stu-id="07d47-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="07d47-207">View</span><span class="sxs-lookup"><span data-stu-id="07d47-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="07d47-208">View</span><span class="sxs-lookup"><span data-stu-id="07d47-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="07d47-209">Exemple de code supplémentaire</span><span class="sxs-lookup"><span data-stu-id="07d47-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07d47-210">Afficher d’autres exemples Bot Framework sur GitHub</span><span class="sxs-lookup"><span data-stu-id="07d47-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a><span data-ttu-id="07d47-211">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="07d47-211">See also</span></span>

* [<span data-ttu-id="07d47-212">Présentation des didacticiels</span><span class="sxs-lookup"><span data-stu-id="07d47-212">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="07d47-213">Créer une application à l’aide React</span><span class="sxs-lookup"><span data-stu-id="07d47-213">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="07d47-214">Créer une application à l’aide de Blazor</span><span class="sxs-lookup"><span data-stu-id="07d47-214">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="07d47-215">Créer une application à l’aide SPFx</span><span class="sxs-lookup"><span data-stu-id="07d47-215">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="07d47-216">Créer une application en utilisant C# ou .NET</span><span class="sxs-lookup"><span data-stu-id="07d47-216">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="07d47-217">Créer une application en utilisant Node.js</span><span class="sxs-lookup"><span data-stu-id="07d47-217">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="07d47-218">Créer une application à l’aide du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="07d47-218">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="07d47-219">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="07d47-219">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="07d47-220">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="07d47-220">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)