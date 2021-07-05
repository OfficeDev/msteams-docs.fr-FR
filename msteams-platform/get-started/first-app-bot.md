---
title: 'Prise en main : créer votre premier bot de conversation'
author: adrianhall
description: Créez un bot de conversation pour Microsoft Teams à l’aide du Kit de ressources Teams.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 96bbddd99b6901a4b92e1e2f2dc98482c755dc66
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254250"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="0d189-103">Créer votre premier bot de conversation pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0d189-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="0d189-104">Dans ce didacticiel, vous découvrirez comment créer, exécuter et déployer une application bot Teams.</span><span class="sxs-lookup"><span data-stu-id="0d189-104">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span> <span data-ttu-id="0d189-105">Un bot agit en tant qu’intermédiaire entre un utilisateur Teams et un service web.</span><span class="sxs-lookup"><span data-stu-id="0d189-105">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="0d189-106">Les utilisateurs peuvent converser avec un bot pour obtenir rapidement des informations, initier des flux de travail ou tout autre action que votre service web peut effectuer.</span><span class="sxs-lookup"><span data-stu-id="0d189-106">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="0d189-107">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0d189-107">Before you begin</span></span>

<span data-ttu-id="0d189-108">Assurez-vous que votre environnement de développement est installé en installant les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="0d189-108">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d189-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0d189-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="0d189-110">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="0d189-110">Create your project</span></span>

<span data-ttu-id="0d189-111">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="0d189-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="0d189-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0d189-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="0d189-113">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0d189-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="0d189-114">Sélectionnez l Teams dans la barre latérale pour ouvrir le Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="0d189-114">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="0d189-116">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="0d189-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="0d189-118">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="0d189-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="0d189-120">Dans la section **Sélectionner des fonctionnalités,** **sélectionnez Bot,** désélectionner **l’onglet** et **sélectionner OK.**</span><span class="sxs-lookup"><span data-stu-id="0d189-120">In the **Select capabilities** section, select **Bot**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="0d189-122">Dans la section **Inscription du** bot, **sélectionnez Créer une nouvelle inscription de bot.**</span><span class="sxs-lookup"><span data-stu-id="0d189-122">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Sélectionner l’inscription d’un nouveau bot":::

1. <span data-ttu-id="0d189-124">Dans la section **Langage de** programmation, **sélectionnez JavaScript.**</span><span class="sxs-lookup"><span data-stu-id="0d189-124">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. <span data-ttu-id="0d189-126">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0d189-126">Select a workspace folder.</span></span>  <span data-ttu-id="0d189-127">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="0d189-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="0d189-128">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="0d189-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="0d189-129">Le nom de l’application doit contenir uniquement des caractères alphanumériques.</span><span class="sxs-lookup"><span data-stu-id="0d189-129">The name of the app must contain only alphanumeric characters.</span></span>  <span data-ttu-id="0d189-130">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="0d189-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="0d189-131">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="0d189-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="0d189-132">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="0d189-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="0d189-133">Utilisez le CLI `teamsfx` pou créer votre premier projet.</span><span class="sxs-lookup"><span data-stu-id="0d189-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="0d189-134">Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="0d189-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="0d189-135">Le CLI parcourt quelques questions pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="0d189-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="0d189-136">Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).</span><span class="sxs-lookup"><span data-stu-id="0d189-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="0d189-137">Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="0d189-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="0d189-138">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="0d189-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="0d189-139">Sélectionnez **Bot** et désélection **de l’onglet.**</span><span class="sxs-lookup"><span data-stu-id="0d189-139">Select **Bot** and deselect **Tab**.</span></span>
1. <span data-ttu-id="0d189-140">Sélectionner **Créer l’inscription d’un nouveau bot**.</span><span class="sxs-lookup"><span data-stu-id="0d189-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="0d189-141">Sélectionnez **JavaScript** comme langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="0d189-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="0d189-142">Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.</span><span class="sxs-lookup"><span data-stu-id="0d189-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="0d189-143">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="0d189-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="0d189-144">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="0d189-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="0d189-145">Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.</span><span class="sxs-lookup"><span data-stu-id="0d189-145">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="0d189-146">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="0d189-146">Take a tour of the source code</span></span>

<span data-ttu-id="0d189-147">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="0d189-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="0d189-148">Une extension de messagerie utilise [Bot Framework](https://docs.botframework.com) pour autoriser l’utilisateur à interagir avec votre service via une conversation.</span><span class="sxs-lookup"><span data-stu-id="0d189-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="0d189-149">Après structuration, votre projet ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="0d189-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Disposition de fichier d’un projet bot.":::

<span data-ttu-id="0d189-151">Le code bot est stocké dans le répertoire `bot`.</span><span class="sxs-lookup"><span data-stu-id="0d189-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="0d189-152">Le `bot/teamsBot.js` est le point d’entrée principal pour le bot et les boîtes de dialogue sont stockées dans le répertoire `dialogs`.</span><span class="sxs-lookup"><span data-stu-id="0d189-152">The `bot/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="0d189-153">Familiarisez-vous avec les bots en dehors de Teams avant d’intégrer votre premier bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="0d189-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="0d189-154">Vous trouverez d’autres informations sur les bots en examinant les didacticiels [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0d189-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="0d189-155">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="0d189-155">Run your app locally</span></span>

<span data-ttu-id="0d189-156">Le Kit de ressources Teams vous permet d’héberger votre application localement.</span><span class="sxs-lookup"><span data-stu-id="0d189-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="0d189-157">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="0d189-157">To do this:</span></span>

- <span data-ttu-id="0d189-158">Une application Azure Active Directory est inscrite dans le client M365.</span><span class="sxs-lookup"><span data-stu-id="0d189-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="0d189-159">Un manifeste d’application est soumis au Centre des développeurs pour Teams.</span><span class="sxs-lookup"><span data-stu-id="0d189-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="0d189-160">Une API est exécutée à l’aide d’Azure Functions Core Tools pour prendre en charge votre application.</span><span class="sxs-lookup"><span data-stu-id="0d189-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="0d189-161">[ngrok](https://ngrok.io) est installé et utilisé pour fournir un tunnel entre Teams et votre code bot.</span><span class="sxs-lookup"><span data-stu-id="0d189-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="0d189-162">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="0d189-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="0d189-163">À Visual Studio Code, appuyez sur la **touche F5** pour exécuter votre application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="0d189-163">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="0d189-164">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="0d189-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="0d189-165">Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="0d189-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="0d189-166">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="0d189-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="0d189-167">Votre navigateur web commence à exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="0d189-167">Your web browser starts to run the app.</span></span> <span data-ttu-id="0d189-168">Si vous êtes invité à ouvrir Teams bureau, sélectionnez **Annuler** pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="0d189-168">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="0d189-169">Vous pouvez également être invité à basculer vers Teams bureau à d’autres moments ; sélectionnez l Teams’application web lorsque cela se produit.</span><span class="sxs-lookup"><span data-stu-id="0d189-169">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. <span data-ttu-id="0d189-171">Vous serez peut-être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="0d189-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="0d189-172">Dans ce cas, connectez-vous à l'aide de votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="0d189-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="0d189-173">Lorsque vous y invitez l’application sur Teams, sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="0d189-173">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="0d189-174">Une fois l’application chargée, vous êtes directement conduit à une session de conversation avec le bot.</span><span class="sxs-lookup"><span data-stu-id="0d189-174">After the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="0d189-175">Vous pouvez taper `intro` pour afficher une carte d’introduction et `show` pour présenter vos informations à partir de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="0d189-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="0d189-176">(Ceci nécessite une approbation d’autorisations supplémentaire).</span><span class="sxs-lookup"><span data-stu-id="0d189-176">(This will require an additional permissions approval).</span></span>

   <span data-ttu-id="0d189-177">Le débogage fonctionne comme prévu. Essayez vous-même.</span><span class="sxs-lookup"><span data-stu-id="0d189-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="0d189-178">Ouvrez le fichier `bot/dialogs/rootDialog.js`, puis localisez la méthode `triggerCommand(...)`.</span><span class="sxs-lookup"><span data-stu-id="0d189-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="0d189-179">Définissez un point d’arrêt sur le cas par défaut.</span><span class="sxs-lookup"><span data-stu-id="0d189-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="0d189-180">Puis tapez du texte.</span><span class="sxs-lookup"><span data-stu-id="0d189-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="0d189-181">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="0d189-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="0d189-182">Lorsque vous appuyez sur **la touche F5,** le Teams Shared Computer Toolkit :</span><span class="sxs-lookup"><span data-stu-id="0d189-182">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="0d189-183">Inscrit votre application avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d189-183">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="0d189-184">Inscrit votre application pour le « chargement de version latéral » dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0d189-184">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="0d189-185">Démarre le système principal de votre application en cours d’exécution localement à [l’aide des outils Azure Function Core](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="0d189-185">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="0d189-186">Démarre un tunnel ngrok pour Teams communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="0d189-186">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="0d189-187">Démarre Microsoft Teams avec une commande pour indiquer Teams charger une version de version de l’application.</span><span class="sxs-lookup"><span data-stu-id="0d189-187">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="0d189-188">Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="0d189-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="0d189-189">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement de version test d’une application.</span><span class="sxs-lookup"><span data-stu-id="0d189-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="0d189-190">Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="0d189-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="0d189-191">Vérifier l’absence de problèmes avant de charger la version test de votre application en utilisant [l’outil de validation d’application](https://dev.teams.microsoft.com/appvalidation.html) qui est inclus dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="0d189-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="0d189-192">Corrigez les erreurs pour charger correctement la version test de l’application.</span><span class="sxs-lookup"><span data-stu-id="0d189-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="0d189-193">Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</span><span class="sxs-lookup"><span data-stu-id="0d189-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="0d189-194">Avant le déploiement, l’application s’est exécutée localement :</span><span class="sxs-lookup"><span data-stu-id="0d189-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="0d189-195">Le serveur principal s’exécute en utilisant _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="0d189-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="0d189-196">Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.</span><span class="sxs-lookup"><span data-stu-id="0d189-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

   <span data-ttu-id="0d189-197">Le déploiement implique la mise en service de ressources sur un abonnement Azure actif et le déploiement (chargement) du code du serveur principal et du serveur frontal pour l’application vers Azure.</span><span class="sxs-lookup"><span data-stu-id="0d189-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="0d189-198">Le serveur principal utilise une variété de services Azure, notamment Azure App Service et Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="0d189-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="0d189-199">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0d189-199">See also</span></span>

* [<span data-ttu-id="0d189-200">Présentation des didacticiels</span><span class="sxs-lookup"><span data-stu-id="0d189-200">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="0d189-201">Créer une application à l’aide React</span><span class="sxs-lookup"><span data-stu-id="0d189-201">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="0d189-202">Créer une application à l’aide de Blazor</span><span class="sxs-lookup"><span data-stu-id="0d189-202">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="0d189-203">Créer une application à l’aide SPFx</span><span class="sxs-lookup"><span data-stu-id="0d189-203">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="0d189-204">Créer une application en utilisant C# ou .NET</span><span class="sxs-lookup"><span data-stu-id="0d189-204">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="0d189-205">Créer une application en utilisant Node.js</span><span class="sxs-lookup"><span data-stu-id="0d189-205">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="0d189-206">Créer une application à l’aide du générateur Yeoman</span><span class="sxs-lookup"><span data-stu-id="0d189-206">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="0d189-207">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="0d189-207">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="0d189-208">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="0d189-208">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)