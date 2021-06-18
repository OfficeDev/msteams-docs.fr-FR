---
title: 'Prise en main : créer votre premier bot de conversation'
author: adrianhall
description: Créez un bot de conversation pour Microsoft Teams à l’aide du Kit de ressources Teams.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: e59980e7f33c326c16faefd412f9845e47f234e5
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994258"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="8189b-103">Créer votre premier bot de conversation pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8189b-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="8189b-104">Un bot agit en tant qu’intermédiaire entre un utilisateur Teams et un service web.</span><span class="sxs-lookup"><span data-stu-id="8189b-104">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="8189b-105">Les utilisateurs peuvent converser avec un bot pour obtenir rapidement des informations, initier des flux de travail ou tout autre action que votre service web peut effectuer.</span><span class="sxs-lookup"><span data-stu-id="8189b-105">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span>  <span data-ttu-id="8189b-106">Dans ce didacticiel, vous découvrirez comment créer, exécuter et déployer une application bot Teams.</span><span class="sxs-lookup"><span data-stu-id="8189b-106">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8189b-107">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8189b-107">Before you begin</span></span>

<span data-ttu-id="8189b-108">Vérifiez que votre environnement de développement est configuré en installant les [Conditions préalables](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="8189b-108">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8189b-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8189b-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="8189b-110">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="8189b-110">Create your project</span></span>

<span data-ttu-id="8189b-111">Utilisez le Kit de ressources Teams pou créer votre premier projet :</span><span class="sxs-lookup"><span data-stu-id="8189b-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="8189b-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8189b-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="8189b-113">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8189b-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="8189b-114">Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :</span><span class="sxs-lookup"><span data-stu-id="8189b-114">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. <span data-ttu-id="8189b-116">Sélectionnez **Création d’un projet**.</span><span class="sxs-lookup"><span data-stu-id="8189b-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. <span data-ttu-id="8189b-118">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="8189b-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. <span data-ttu-id="8189b-120">À l’étape **Sélectionner les fonctionnalités**, sélectionnez **Bot**, puis désélectionnez **Onglet**. Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8189b-120">On the **Select capabilities** step, select **Bot** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. <span data-ttu-id="8189b-122">À l’étape **Inscription de bot**, sélectionnez **Créer l’inscription d’un nouveau bot**.</span><span class="sxs-lookup"><span data-stu-id="8189b-122">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Sélectionner l’inscription d’un nouveau bot":::

1. <span data-ttu-id="8189b-124">À l’étape **Langage de programmation**, sélectionnez **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="8189b-124">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. <span data-ttu-id="8189b-126">Sélectionnez un dossier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="8189b-126">Select a workspace folder.</span></span>  <span data-ttu-id="8189b-127">Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.</span><span class="sxs-lookup"><span data-stu-id="8189b-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="8189b-128">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="8189b-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="8189b-129">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="8189b-129">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="8189b-130">Appuyez sur **Entrer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="8189b-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="8189b-131">Votre application Teams est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="8189b-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="8189b-132">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="8189b-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="8189b-133">Utilisez le CLI `teamsfx` pou créer votre premier projet.</span><span class="sxs-lookup"><span data-stu-id="8189b-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="8189b-134">Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="8189b-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="8189b-135">Le CLI parcourt quelques questions pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="8189b-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="8189b-136">Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).</span><span class="sxs-lookup"><span data-stu-id="8189b-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="8189b-137">Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="8189b-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="8189b-138">Sélectionnez **Créer une application Teams**.</span><span class="sxs-lookup"><span data-stu-id="8189b-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="8189b-139">Sélectionnez la fonctionnalité **Bot**, puis désélectionnez la fonctionnalité **Onglet**.</span><span class="sxs-lookup"><span data-stu-id="8189b-139">Select the **Bot** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="8189b-140">Sélectionner **Créer l’inscription d’un nouveau bot**.</span><span class="sxs-lookup"><span data-stu-id="8189b-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="8189b-141">Sélectionnez **JavaScript** comme langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="8189b-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="8189b-142">Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.</span><span class="sxs-lookup"><span data-stu-id="8189b-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="8189b-143">Entrez un nom approprié pour votre application, tel que `helloworld`.</span><span class="sxs-lookup"><span data-stu-id="8189b-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="8189b-144">Le nom de l’application doit contenir des caractères alphanumériques uniquement.</span><span class="sxs-lookup"><span data-stu-id="8189b-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="8189b-145">Une fois toutes les questions répondues, votre projet est créé.</span><span class="sxs-lookup"><span data-stu-id="8189b-145">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="8189b-146">Suivre une visite guidée du code source</span><span class="sxs-lookup"><span data-stu-id="8189b-146">Take a tour of the source code</span></span>

<span data-ttu-id="8189b-147">Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).</span><span class="sxs-lookup"><span data-stu-id="8189b-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="8189b-148">Une extension de messagerie utilise [Bot Framework](https://docs.botframework.com) pour autoriser l’utilisateur à interagir avec votre service via une conversation.</span><span class="sxs-lookup"><span data-stu-id="8189b-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="8189b-149">Après structuration, votre projet ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="8189b-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Disposition de fichier d’un projet bot.":::

<span data-ttu-id="8189b-151">Le code bot est stocké dans le répertoire `bot`.</span><span class="sxs-lookup"><span data-stu-id="8189b-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="8189b-152">Le `bots/teamsBot.js` est le point d’entrée principal pour le bot et les boîtes de dialogue sont stockées dans le répertoire `dialogs`.</span><span class="sxs-lookup"><span data-stu-id="8189b-152">The `bots/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="8189b-153">Familiarisez-vous avec les bots en dehors de Teams avant d’intégrer votre premier bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8189b-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="8189b-154">Vous trouverez d’autres informations sur les bots en examinant les didacticiels [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="8189b-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="8189b-155">Exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="8189b-155">Run your app locally</span></span>

<span data-ttu-id="8189b-156">Le Kit de ressources Teams vous permet d’héberger votre application localement.</span><span class="sxs-lookup"><span data-stu-id="8189b-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="8189b-157">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="8189b-157">To do this:</span></span>

- <span data-ttu-id="8189b-158">Une application Azure Active Directory est inscrite dans le client M365.</span><span class="sxs-lookup"><span data-stu-id="8189b-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="8189b-159">Un manifeste d’application est soumis au Centre des développeurs pour Teams.</span><span class="sxs-lookup"><span data-stu-id="8189b-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="8189b-160">Une API est exécutée à l’aide d’Azure Functions Core Tools pour prendre en charge votre application.</span><span class="sxs-lookup"><span data-stu-id="8189b-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="8189b-161">[ngrok](https://ngrok.io) est installé et utilisé pour fournir un tunnel entre Teams et votre code bot.</span><span class="sxs-lookup"><span data-stu-id="8189b-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="8189b-162">Pour créer et exécuter votre application localement :</span><span class="sxs-lookup"><span data-stu-id="8189b-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="8189b-163">À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.</span><span class="sxs-lookup"><span data-stu-id="8189b-163">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="8189b-164">Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.</span><span class="sxs-lookup"><span data-stu-id="8189b-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="8189b-165">Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="8189b-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="8189b-166">Cette finalisation peut prendre entre 3 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="8189b-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="8189b-167">Votre navigateur web commence à exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="8189b-167">Your web browser starts to run the app.</span></span> <span data-ttu-id="8189b-168">Si vous êtes invité à ouvrir Teams bureau, sélectionnez **Annuler** pour rester dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="8189b-168">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="8189b-169">Vous pouvez également être invité à basculer vers Teams bureau à d’autres moments ; sélectionnez l Teams’application web lorsque cela se produit.</span><span class="sxs-lookup"><span data-stu-id="8189b-169">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. <span data-ttu-id="8189b-171">Vous serez peut-être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="8189b-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="8189b-172">Dans ce cas, connectez-vous à l'aide de votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="8189b-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="8189b-173">Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8189b-173">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="8189b-174">Une fois l’application chargée, vous serez directement dirigé vers une session de conversation avec le bot.</span><span class="sxs-lookup"><span data-stu-id="8189b-174">Once the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="8189b-175">Vous pouvez taper `intro` pour afficher une carte d’introduction et `show` pour présenter vos informations à partir de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="8189b-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="8189b-176">(Ceci nécessite une approbation d’autorisations supplémentaire).</span><span class="sxs-lookup"><span data-stu-id="8189b-176">(This will require an additional permissions approval).</span></span>

<span data-ttu-id="8189b-177">Le débogage fonctionne comme prévu. Essayez vous-même.</span><span class="sxs-lookup"><span data-stu-id="8189b-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="8189b-178">Ouvrez le fichier `bot/dialogs/rootDialog.js`, puis localisez la méthode `triggerCommand(...)`.</span><span class="sxs-lookup"><span data-stu-id="8189b-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="8189b-179">Définissez un point d’arrêt sur le cas par défaut.</span><span class="sxs-lookup"><span data-stu-id="8189b-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="8189b-180">Puis tapez du texte.</span><span class="sxs-lookup"><span data-stu-id="8189b-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="8189b-181">Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</span><span class="sxs-lookup"><span data-stu-id="8189b-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="8189b-182">Lorsque vous appuyez sur F5, le Kit de ressources Teams :</span><span class="sxs-lookup"><span data-stu-id="8189b-182">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="8189b-183">A inscrit votre application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8189b-183">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="8189b-184">A inscrit votre application pour le « chargement latéral » dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8189b-184">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="8189b-185">A démarré votre serveur principal d’application s’exécutant localement en utilisant [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span><span class="sxs-lookup"><span data-stu-id="8189b-185">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="8189b-186">A démarré un tunnel ngrok pour que Teams puis communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="8189b-186">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="8189b-187">A démarré Microsoft Teams avec une commande pour demander à Teams de charger la version test de l’application.</span><span class="sxs-lookup"><span data-stu-id="8189b-187">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="8189b-188">Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="8189b-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="8189b-189">Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement de version test d’une application.</span><span class="sxs-lookup"><span data-stu-id="8189b-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="8189b-190">Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).</span><span class="sxs-lookup"><span data-stu-id="8189b-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="8189b-191">Vérifier l’absence de problèmes avant de charger la version test de votre application en utilisant [l’outil de validation d’application](https://dev.teams.microsoft.com/appvalidation.html) qui est inclus dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="8189b-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="8189b-192">Corrigez les erreurs pour charger correctement la version test de l’application.</span><span class="sxs-lookup"><span data-stu-id="8189b-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="8189b-193">Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</span><span class="sxs-lookup"><span data-stu-id="8189b-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="8189b-194">Avant le déploiement, l’application s’est exécutée localement :</span><span class="sxs-lookup"><span data-stu-id="8189b-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="8189b-195">Le serveur principal s’exécute en utilisant _Azure Functions Core Tools_.</span><span class="sxs-lookup"><span data-stu-id="8189b-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="8189b-196">Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.</span><span class="sxs-lookup"><span data-stu-id="8189b-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="8189b-197">Le déploiement implique la mise en service de ressources sur un abonnement Azure actif et le déploiement (chargement) du code du serveur principal et du serveur frontal pour l’application vers Azure.</span><span class="sxs-lookup"><span data-stu-id="8189b-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="8189b-198">Le serveur principal utilise une variété de services Azure, notamment Azure App Service et Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="8189b-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="8189b-199">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8189b-199">See also</span></span>

- [<span data-ttu-id="8189b-200">Créer une application Teams à l’aide de React</span><span class="sxs-lookup"><span data-stu-id="8189b-200">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="8189b-201">Créer une application Teams à l’aide de Blazor</span><span class="sxs-lookup"><span data-stu-id="8189b-201">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="8189b-202">[Créer une application Teams en tant que composant WebPart SharePoint](first-app-spfx.md) (Azure non requis)</span><span class="sxs-lookup"><span data-stu-id="8189b-202">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>

## <a name="next-step"></a><span data-ttu-id="8189b-203">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="8189b-203">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8189b-204">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="8189b-204">Create a messaging extension</span></span>](first-message-extension.md)
