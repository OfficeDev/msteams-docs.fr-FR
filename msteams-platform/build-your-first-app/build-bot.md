---
title: Get started - Build a bot
author: girliemac
description: Créez rapidement un bot Microsoft Teams à l’aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: d54766d739ceaf585ab4a1e026f4a6e1150e3a2e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630977"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="abe94-103">Créez votre premier bot pour Teams</span><span class="sxs-lookup"><span data-stu-id="abe94-103">Create your first bot for Teams</span></span>

<span data-ttu-id="abe94-104">Ce didacticiel vous apprend à créer une application de bot de base.</span><span class="sxs-lookup"><span data-stu-id="abe94-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="abe94-105">Un bot fait office d’intermédiaire entre Teams utilisateurs et votre application web ou service avec une interface de conversation.</span><span class="sxs-lookup"><span data-stu-id="abe94-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="abe94-106">Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.</span><span class="sxs-lookup"><span data-stu-id="abe94-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="abe94-107">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="abe94-107">What you'll learn</span></span>

* <span data-ttu-id="abe94-108">Créez un projet d’application et un bot à l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="abe94-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="abe94-109">Comprendre les configurations Teams d’application pertinentes pour les bots.</span><span class="sxs-lookup"><span data-stu-id="abe94-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="abe94-110">Hébergez et exécutez une application localement à l’aide d’une solution de tunnel localhost.</span><span class="sxs-lookup"><span data-stu-id="abe94-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="abe94-111">Chargez une version test d’un bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="abe94-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abe94-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="abe94-112">Prerequisites</span></span>

<span data-ttu-id="abe94-113">Assurez-vous que vous comprenez comment configurer et créer une application Teams simple.</span><span class="sxs-lookup"><span data-stu-id="abe94-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="abe94-114">Pour plus d’informations, [voir créer votre première Microsoft Teams application « Hello World!](../build-your-first-app/build-and-run.md)».</span><span class="sxs-lookup"><span data-stu-id="abe94-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="abe94-115">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="abe94-115">1. Create your app project</span></span>

<span data-ttu-id="abe94-116">Le Microsoft Teams Shared Computer Toolkit vous aide à configurer les composants suivants pour votre application :</span><span class="sxs-lookup"><span data-stu-id="abe94-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="abe94-117">**Configurations d’application et échafaudage pertinents** pour les bots.</span><span class="sxs-lookup"><span data-stu-id="abe94-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="abe94-118">**Bot** inscrit automatiquement auprès du service Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="abe94-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="abe94-119">**Pour créer votre projet d’application**</span><span class="sxs-lookup"><span data-stu-id="abe94-119">**To create your app project**</span></span>

1. In Visual Studio Code, select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Capture d’écran montrant comment créer une application dans le Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="abe94-122">Lorsque vous y invitez, connectez-vous avec votre Microsoft 365 de développement.</span><span class="sxs-lookup"><span data-stu-id="abe94-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="abe94-123">Dans l’écran Sélectionner un projet, sélectionnez Bots de conversation :</span><span class="sxs-lookup"><span data-stu-id="abe94-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Capture d’écran montrant comment créer un bot dans le Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="abe94-125">Dans **l’écran Configurer le projet,** entrez un nom pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="abe94-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="abe94-126">Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="abe94-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="abe94-127">Sélectionnez **Créer un bot d’inscription**  >  **de bot,** comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="abe94-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Capture d’écran montrant l’attribution d’un nom à un nouveau bot dans Teams Shared Computer Toolkit.":::

    <span data-ttu-id="abe94-129">Si elle réussit, votre nouveau bot aura **l’état** Inscrit.</span><span class="sxs-lookup"><span data-stu-id="abe94-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="abe94-130">Votre bot est désormais inscrit automatiquement auprès du service Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="abe94-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Capture d’écran montrant l’inscription d’un nouveau bot dans Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="abe94-132">Sélectionnez **Terminer** en bas de l’écran et enregistrez votre projet sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="abe94-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="abe94-133">2. Comprendre les composants de votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="abe94-133">2. Understand your app project components</span></span>

<span data-ttu-id="abe94-134">La plupart des configurations d’application et de la création de la Teams Shared Computer Toolkit sont automatiquement définies.</span><span class="sxs-lookup"><span data-stu-id="abe94-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="abe94-135">Examinons les principaux composants de la création d’un bot :</span><span class="sxs-lookup"><span data-stu-id="abe94-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Capture d’écran montrant la échafaudage d’un projet dans la Teams Shared Computer Toolkit.":::

<span data-ttu-id="abe94-137">Si vous avez créé un onglet dans un autre didacticiel, la création de la modèle d’application pour le bot est différente.</span><span class="sxs-lookup"><span data-stu-id="abe94-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="abe94-138">Contrairement aux onglets, le développement de bots ne nécessite pas la création de composants web frontaux ou l’utilisation Teams SDK client JavaScript.</span><span class="sxs-lookup"><span data-stu-id="abe94-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="abe94-139">Au lieu de cela, la création de la forme utilise la [Microsoft Bot Framework](https://dev.botframework.com/), qui est un SDK open source pour créer des bots intelligents et de niveau entreprise qui peuvent fonctionner sur le web, mobile et bien sûr Teams!</span><span class="sxs-lookup"><span data-stu-id="abe94-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="abe94-140">La création de la échafaudage d’application fournit un fichier, situé dans le répertoire racine de votre projet, qui est le handler spécifique à Teams qui gère les activités du bot, telles que la façon dont le bot répond à des `botActivityHandler.js` messages spécifiques.</span><span class="sxs-lookup"><span data-stu-id="abe94-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities such as, how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="abe94-141">3. Exposer en toute sécurité votre localhost sur Internet</span><span class="sxs-lookup"><span data-stu-id="abe94-141">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="abe94-142">Consultez le fichier, qui crée un serveur HTTP et gère le routage pour écouter les demandes entrantes `index.js` à votre bot.</span><span class="sxs-lookup"><span data-stu-id="abe94-142">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="abe94-143">Url du point de terminaison de votre application `/api/messages` pour répondre aux demandes des clients :</span><span class="sxs-lookup"><span data-stu-id="abe94-143">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="abe94-144">Pour que les demandes soient transmis à la logique de votre bot, vous devez configurer une URL accessible publiquement, par exemple, au `https://example.com/api/messages` lieu de `https://localhost` .</span><span class="sxs-lookup"><span data-stu-id="abe94-144">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="abe94-145">Étant donné que votre application s’exécute à partir de votre localhost actuellement, vous devez *tunneler* le réseau.</span><span class="sxs-lookup"><span data-stu-id="abe94-145">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="abe94-146">Le tunneling est un protocole qui vous permet de transporter des données sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="abe94-146">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="abe94-147">La tunneling localhost vous permet d’établir une connexion entre votre ordinateur local et une connexion distante.</span><span class="sxs-lookup"><span data-stu-id="abe94-147">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="abe94-148">Pour exposer en toute sécurité votre localhost sur Internet, nous vous recommandons d’utiliser l’outil tiers appelé **ngrok**.</span><span class="sxs-lookup"><span data-stu-id="abe94-148">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="abe94-149">Cela vous donne une URL sécurisée.</span><span class="sxs-lookup"><span data-stu-id="abe94-149">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="abe94-150">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span><span class="sxs-lookup"><span data-stu-id="abe94-150">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="abe94-151">Ajoutez le chemin d’accès complet au ngrok.exe que vous avez installé à la variable d’environnement PATH système.</span><span class="sxs-lookup"><span data-stu-id="abe94-151">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="abe94-152">Les étapes exactes sont spécifiques à l’shell que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="abe94-152">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="abe94-153">Une fois la configuration terminée, ouvrez un terminal et `ngrok http -host-header=rewrite 3978` exécutez.</span><span class="sxs-lookup"><span data-stu-id="abe94-153">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="abe94-154">Maintenant que ngrok vous fournit une URL publique et sécurisée qui est transmis à votre localhost au port 3978, copiez l’URL HTTPS, par exemple, comme illustré dans la capture d’écran ci-dessous, dans la mesure où Teams nécessite des `https://287a4f4223bc.ngrok.io` connexions HTTPS :</span><span class="sxs-lookup"><span data-stu-id="abe94-154">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Screenshot showing tunnelling of localhost with ngrok.":::

1. <span data-ttu-id="abe94-156">Inscrivez l’URL dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="abe94-156">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="abe94-157">4. Inscrire le point de terminaison de votre bot</span><span class="sxs-lookup"><span data-stu-id="abe94-157">4. Register your bot endpoint</span></span>

<span data-ttu-id="abe94-158">Pour utiliser un bot dans Teams, vous devez l’inscrire auprès d’Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="abe94-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="abe94-159">Cette mise à jour est effectuée automatiquement lorsque vous définissez votre application à l’aide du Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="abe94-159">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="abe94-160">Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages des utilisateurs, ou les demandes envoyées au bot.</span><span class="sxs-lookup"><span data-stu-id="abe94-160">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="abe94-161">En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à .</span><span class="sxs-lookup"><span data-stu-id="abe94-161">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="abe94-162">Vous pouvez le configurer dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="abe94-162">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="abe94-163">Dans Visual Studio Code, ouvrez **Microsoft Teams Shared Computer Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="abe94-163">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="abe94-164">Sélectionnez **Bots**  >  **Existing bot registrations** and select the bot you created during setup.</span><span class="sxs-lookup"><span data-stu-id="abe94-164">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="abe94-165">Dans le **champ d’adresse** du point de terminaison bot, entrez l’URL ngrok, par exemple, où vous hébergez le bot et y `https://287a4f4223bc.ngrok.io` `/api/messages` appendez :</span><span class="sxs-lookup"><span data-stu-id="abe94-165">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Capture d’écran montrant comment tunneler localhost avec ngrok.":::

    <span data-ttu-id="abe94-167">Votre bot peut répondre aux messages dans Teams, une fois que vous avez correctement installé le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="abe94-167">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="abe94-168">5. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="abe94-168">5. Build and run your app</span></span>

<span data-ttu-id="abe94-169">Vous avez configuré une URL pour héberger votre bot et configurée pour gérer les messages.</span><span class="sxs-lookup"><span data-stu-id="abe94-169">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="abe94-170">Il est temps de rendre votre application opérationnel.</span><span class="sxs-lookup"><span data-stu-id="abe94-170">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="abe94-171">Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="abe94-171">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="abe94-172">Exécutez `npm start`.</span><span class="sxs-lookup"><span data-stu-id="abe94-172">Run `npm start`.</span></span>

   <span data-ttu-id="abe94-173">Si l’opération réussit, vous voyez le message suivant indiquant que votre bot est à l’écoute de l’activité au niveau de votre `localhost` :</span><span class="sxs-lookup"><span data-stu-id="abe94-173">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="abe94-174">6. Chargement d’une version de version de votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="abe94-174">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="abe94-175">Une fois votre bot en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="abe94-175">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="abe94-176">Si vous n’avez pas chargé une version de version Teams’application avant et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="abe94-176">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="abe94-177">Dans Visual Studio Code, sélectionnez la **touche F5** pour lancer un client Teams web.</span><span class="sxs-lookup"><span data-stu-id="abe94-177">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="abe94-178">Dans la boîte de dialogue d’installation de l’application, **sélectionnez Ajouter pour moi.**</span><span class="sxs-lookup"><span data-stu-id="abe94-178">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="abe94-179">Par défaut, l’application est ajoutée à votre message de conversation directe 1:1, mais vous pouvez choisir de l’installer dans une équipe ou une conversation en cliquant sur la petite flèche à côté d’Ajouter pour **moi.**</span><span class="sxs-lookup"><span data-stu-id="abe94-179">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="abe94-180">Dans ce didacticiel, nous allons simplement cliquer sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="abe94-180">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Capture d’écran montrant le tunnelage localhost avec ngrok.":::

## <a name="7-test-your-bot"></a><span data-ttu-id="abe94-182">7. Testez votre bot</span><span class="sxs-lookup"><span data-stu-id="abe94-182">7. Test your bot</span></span>

<span data-ttu-id="abe94-183">Dites « Hello » à votre bot.</span><span class="sxs-lookup"><span data-stu-id="abe94-183">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="abe94-184">Dans la zone de composition, envoyez un `Hello` message.</span><span class="sxs-lookup"><span data-stu-id="abe94-184">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="abe94-185">Votre bot répond par le message suivant :</span><span class="sxs-lookup"><span data-stu-id="abe94-185">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Capture d’écran montrant un utilisateur dire « Hello » à un bot Teams et obtenir une réponse.":::

    <span data-ttu-id="abe94-187">Vous avez maintenant créé un bot Teams de base qui peut communiquer avec les utilisateurs un-à-un ou dans des paramètres de groupe (canaux et conversations) 🎉.</span><span class="sxs-lookup"><span data-stu-id="abe94-187">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="abe94-188">Résoudre les problèmes de votre bot</span><span class="sxs-lookup"><span data-stu-id="abe94-188">Troubleshoot your bot</span></span>

<span data-ttu-id="abe94-189">Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="abe94-189">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="abe94-190">Le bot n’est pas connecté à Teams</span><span class="sxs-lookup"><span data-stu-id="abe94-190">Bot isn't connected to Teams</span></span>


<span data-ttu-id="abe94-191">Si vous avez installé votre application, mais que le bot ne fonctionne pas, assurez-vous que le bot est connecté au canal Teams [ *Azure* Bot Service.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="abe94-191">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="abe94-192">Il est important de comprendre que ce n’est pas le même qu’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="abe94-192">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="abe94-193">Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication Microsoft ou tierce [prise en charge.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="abe94-193">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="abe94-194">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="abe94-194">See also</span></span>

* [<span data-ttu-id="abe94-195">Informations de base sur les bots</span><span class="sxs-lookup"><span data-stu-id="abe94-195">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="abe94-196">Créer un onglet personnel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="abe94-196">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="abe94-197">Découvrez les autres Teams bots peuvent faire avec l’un de nos exemples</span><span class="sxs-lookup"><span data-stu-id="abe94-197">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="abe94-198">Concepts de base d’une conversation de bot</span><span class="sxs-lookup"><span data-stu-id="abe94-198">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="abe94-199">Instructions de conception</span><span class="sxs-lookup"><span data-stu-id="abe94-199">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="abe94-200">Modèles d’interface utilisateur prêts pour la production</span><span class="sxs-lookup"><span data-stu-id="abe94-200">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="abe94-201">Authentification de bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="abe94-201">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="abe94-202">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="abe94-202">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="abe94-203">Créer un bot sans le kit de ressources</span><span class="sxs-lookup"><span data-stu-id="abe94-203">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="abe94-204">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="abe94-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abe94-205">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="abe94-205">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
