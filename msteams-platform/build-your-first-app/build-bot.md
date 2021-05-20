---
title: Démarrer - Construire un bot
author: girliemac
description: Créez rapidement un bot Microsoft Teams en utilisant le Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565885"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="dc4aa-103">Créez votre premier bot pour Teams</span><span class="sxs-lookup"><span data-stu-id="dc4aa-103">Create your first bot for Teams</span></span>

<span data-ttu-id="dc4aa-104">Ce tutoriel vous apprend à construire une application de bot de base.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="dc4aa-105">Un bot agit comme un intermédiaire entre Teams utilisateurs et votre application web ou service avec une interface conversationnelle.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="dc4aa-106">Les gens peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des workflows et des tâches effectuées par votre service.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dc4aa-107">Ce que vous apprendrez</span><span class="sxs-lookup"><span data-stu-id="dc4aa-107">What you'll learn</span></span>

* <span data-ttu-id="dc4aa-108">Créez un projet d’application et un bot en utilisant Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="dc4aa-109">Comprendre les configurations Teams’applications pertinentes pour les bots.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="dc4aa-110">Hébergez et exécutez une application localement à l’aide d’une solution de tunneling localhost.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="dc4aa-111">Sideload et tester un bot dans Teams.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc4aa-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="dc4aa-112">Prerequisites</span></span>

<span data-ttu-id="dc4aa-113">Assurez-vous de bien comprendre comment configurer et construire une application Teams simple.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="dc4aa-114">Pour plus d’informations, [consultez la première Microsoft Teams application « Hello, World! »](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="dc4aa-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="dc4aa-115">1. Créez votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="dc4aa-115">1. Create your app project</span></span>

<span data-ttu-id="dc4aa-116">Le Microsoft Teams Shared Computer Toolkit vous aide à configurer les composants suivants pour votre application :</span><span class="sxs-lookup"><span data-stu-id="dc4aa-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="dc4aa-117">**Configurations d’applications et échafaudages** pertinents pour les bots.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="dc4aa-118">**Bot** qui est automatiquement enregistré auprès du Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="dc4aa-119">**Pour créer votre projet d’application**</span><span class="sxs-lookup"><span data-stu-id="dc4aa-119">**To create your app project**</span></span>

1. Dans Visual Studio Code, sélectionnez **Microsoft Teams la** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: barre d’activité gauche et **choisissez Créer une nouvelle application Teams.**

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Capture d’écran montrant comment créer une application dans le Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="dc4aa-122">Lorsque cela est demandé, connectez-vous à votre compte Microsoft 365 développement de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="dc4aa-123">Sur l’écran du projet Select, sélectionnez Robots conversation :</span><span class="sxs-lookup"><span data-stu-id="dc4aa-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Capture d’écran montrant comment créer un nouveau bot dans le Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="dc4aa-125">Sur **l’écran du** projet Configure, entrez un nom pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="dc4aa-126">Il s’agit du nom par défaut de votre application et aussi du nom de l’annuaire du projet d’application sur votre machine locale.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="dc4aa-127">Sélectionnez **Créer un nouveau Bot** Créer  >  **l’enregistrement bot** comme indiqué dans l’image suivante:</span><span class="sxs-lookup"><span data-stu-id="dc4aa-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Capture d’écran montrant nommer un nouveau bot dans Teams Shared Computer Toolkit.":::

    <span data-ttu-id="dc4aa-129">En cas de succès, votre nouveau bot aura un **statut** enregistré.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="dc4aa-130">Maintenant, votre bot est automatiquement enregistré auprès du Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Capture d’écran montrant l’enregistrement du nouveau bot dans Teams Shared Computer Toolkit.":::

1. <span data-ttu-id="dc4aa-132">Sélectionnez **Finition** en bas de l’écran et enregistrez votre projet sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="dc4aa-133">2. Comprendre les composants de votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="dc4aa-133">2. Understand your app project components</span></span>

<span data-ttu-id="dc4aa-134">Une grande partie des configurations d’applications et des échafaudages sont mis en place automatiquement lorsque vous créez votre projet avec Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="dc4aa-135">Examinons les principaux composants pour la construction d’un bot:</span><span class="sxs-lookup"><span data-stu-id="dc4aa-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Capture d’écran montrant un échafaudage de projet dans Teams Shared Computer Toolkit.":::

<span data-ttu-id="dc4aa-137">Si vous avez créé un onglet dans un autre tutoriel, l’échafaudage de l’application pour le bot est différent.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="dc4aa-138">Contrairement aux onglets, le développement de bots ne vous oblige pas à construire des composants Web front-end ou à utiliser les Teams client JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="dc4aa-139">Au lieu de cela, [l’échafaudage utilise le Microsoft Bot Framework](https://dev.botframework.com/), qui est un SDK open-source pour la construction intelligente, bots de qualité entreprise qui peuvent travailler sur le web, mobile, et bien sûr Teams!</span><span class="sxs-lookup"><span data-stu-id="dc4aa-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="dc4aa-140">Le `botActivityHandler.js` fichier, situé dans l’annuaire racine de votre projet, est le gestionnaire spécifique à Teams qui gère les activités de bot, telles que la façon dont le bot répond à des messages spécifiques.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="dc4aa-141">L’échafaudage de `botActivityHandler.js` l’application fournit un fichier situé dans l’annuaire racine de votre projet, est le gestionnaire spécifique Teams qui gère les activités bot telles que la façon dont le bot répond à des messages spécifiques.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-141">The app scaffolding provides a `botActivityHandler.js` file located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="dc4aa-142">3. Exposez en toute sécurité votre heure locale à Internet</span><span class="sxs-lookup"><span data-stu-id="dc4aa-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="dc4aa-143">Jetez un oeil au `index.js` fichier, qui crée un serveur HTTP et gère le routage pour écouter les demandes entrantes à votre bot.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="dc4aa-144">`/api/messages`L’URL du point de terminaison de votre application est la réponse aux demandes des clients :</span><span class="sxs-lookup"><span data-stu-id="dc4aa-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="dc4aa-145">Pour transmettre les demandes à la logique de votre bot, vous devez configurer une URL accessible au public, par `https://example.com/api/messages` exemple, au lieu de `https://localhost` .</span><span class="sxs-lookup"><span data-stu-id="dc4aa-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="dc4aa-146">Étant donné que votre application est en cours d’exécution à partir de votre localhost actuellement, vous *devez tunnel* le réseau.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="dc4aa-147">Tunneling est un protocole qui vous permet de transporter des données sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="dc4aa-148">Et le tunnelage local vous donne une connexion entre votre machine locale et une connexion distante.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="dc4aa-149">Pour exposer en toute sécurité votre localhost à l’Internet, nous vous recommandons d’utiliser l’outil tiers appelé, **ngrok**.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="dc4aa-150">Cela vous donnera une URL sécurisée.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="dc4aa-151">Rendez-vous [sur ngrok.com](https://ngrok.com/download) site et suivez les instructions d’installation et de mise en place de ngrok dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="dc4aa-152">Ajoutez le chemin complet au fichier ngrok.exe que vous avez installé à la variable environnement PATH du système.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="dc4aa-153">Les étapes exactes sont spécifiques à la coquille que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="dc4aa-154">Une fois que vous avez terminé sa mise en place, ouvrez un terminal et `ngrok http -host-header=rewrite 3978` exécutez.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="dc4aa-155">Maintenant ngrok vous fournit une URL publique et sécurisée qui est transmise à votre localhost au port 3978, alors copiez l’URL HTTPS, par exemple, comme le montre la `https://287a4f4223bc.ngrok.io` capture d’écran ci-dessous, puisque Teams nécessite des connexions HTTPS :</span><span class="sxs-lookup"><span data-stu-id="dc4aa-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="Capture d’écran montrant tunnelling de localhost avec ngrok.":::

1. <span data-ttu-id="dc4aa-157">Enregistrez l’URL dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="dc4aa-158">4. Enregistrez votre point de terminaison bot</span><span class="sxs-lookup"><span data-stu-id="dc4aa-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="dc4aa-159">Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du Service Bot Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="dc4aa-160">Cela se fait automatiquement lorsque vous configurez votre application à l’aide de la Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="dc4aa-161">Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages utilisateur, ou les demandes envoyées au bot.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-161">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="dc4aa-162">En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à .</span><span class="sxs-lookup"><span data-stu-id="dc4aa-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="dc4aa-163">Vous pouvez configurer cela dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-163">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="dc4aa-164">En Visual Studio Code, ouvrez **Microsoft Teams Shared Computer Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="dc4aa-165">Sélectionnez **bots**  >  **enregistrements bot existants et** sélectionnez le bot que vous avez créé lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="dc4aa-166">Dans le **champ d’adresse bot,** entrez l’URL ngrok, par `https://287a4f4223bc.ngrok.io` exemple, où vous hébergez le bot et `/api/messages` annexez-le :</span><span class="sxs-lookup"><span data-stu-id="dc4aa-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="Capture d’écran montrant comment tunnel localhost avec ngrok.":::

    <span data-ttu-id="dc4aa-168">Votre bot sera en mesure de répondre aux messages dans Teams, après avoir correctement défini le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="dc4aa-169">5. Créez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="dc4aa-169">5. Build and run your app</span></span>

<span data-ttu-id="dc4aa-170">Vous avez configuré une URL pour héberger votre bot et l’avez configurée pour gérer les messages.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="dc4aa-171">Il est temps de mettre votre application en marche.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="dc4aa-172">Dans un terminal, allez à l’annuaire racine de votre projet d’application et `npm install` exécutez.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="dc4aa-173">Exécutez `npm start`.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-173">Run `npm start`.</span></span>

   <span data-ttu-id="dc4aa-174">En cas de succès, vous voyez le message suivant indiquant que votre bot est à l’écoute de l’activité à votre `localhost` :</span><span class="sxs-lookup"><span data-stu-id="dc4aa-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="dc4aa-175">6. Chargez votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="dc4aa-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="dc4aa-176">Avec votre bot en cours d’exécution, vous pouvez l’installer Teams.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="dc4aa-177">Si vous n’avez pas déchargé une application Teams avant et que vous ne vous êtes pas aperçu de problèmes, suivez [ces instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="dc4aa-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="dc4aa-178">Dans Visual Studio Code, sélectionnez **la clé F5** pour lancer un client web Teams et spécial.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="dc4aa-179">Dans le dialogue d’installation de l’application, **sélectionnez Ajouter pour moi**.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="dc4aa-180">Par défaut, l’application est ajoutée à votre message de chat direct 1:1, mais vous pouvez choisir de l’installer à une équipe ou de discuter en cliquant sur la petite flèche **à côté ajouter pour moi**.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="dc4aa-181">Dans ce tutoriel, il suffit de cliquer sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="Capture d’écran montrant tunnelling localhost avec ngrok.":::

## <a name="7-test-your-bot"></a><span data-ttu-id="dc4aa-183">7. Testez votre bot</span><span class="sxs-lookup"><span data-stu-id="dc4aa-183">7. Test your bot</span></span>

<span data-ttu-id="dc4aa-184">Disons « Bonjour » à votre bot.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="dc4aa-185">Dans la boîte de composition, envoyez un `Hello` message.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="dc4aa-186">Votre bot répond par quelque chose comme le message suivant:</span><span class="sxs-lookup"><span data-stu-id="dc4aa-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="Une capture d’écran montrant un utilisateur dire « Bonjour » à un bot Teams et obtenir une réponse.":::

    <span data-ttu-id="dc4aa-188">Vous avez maintenant créé un bot de Teams de base qui peut communiquer avec les utilisateurs en tête-à-tête ou en groupe (canaux et chats) 🎉.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="dc4aa-189">Dépanner votre bot</span><span class="sxs-lookup"><span data-stu-id="dc4aa-189">Troubleshoot your bot</span></span>

<span data-ttu-id="dc4aa-190">Les informations suivantes peuvent vous aider si vous avez eu des problèmes pour terminer ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="dc4aa-191">Bot n’est pas connecté à Teams</span><span class="sxs-lookup"><span data-stu-id="dc4aa-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="dc4aa-192">Si vous avez installé votre application mais que le bot ne fonctionne pas, assurez-vous que le bot [est connecté au canal de Teams Azure Bot Service. ](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="dc4aa-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="dc4aa-193">Il est important de comprendre que ce n’est pas la même chose qu’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="dc4aa-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="dc4aa-194">Dans ce cas, un canal est la façon dont le Service Bot Azure connecte votre bot à Teams ou une autre application de [communication Microsoft ou tierce prise en charge](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="dc4aa-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="dc4aa-195">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dc4aa-195">See also</span></span>

* [<span data-ttu-id="dc4aa-196">Bases bot</span><span class="sxs-lookup"><span data-stu-id="dc4aa-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="dc4aa-197">Créez un onglet personnel pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dc4aa-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="dc4aa-198">Voyez ce que Teams bots peuvent faire avec un de nos échantillons</span><span class="sxs-lookup"><span data-stu-id="dc4aa-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="dc4aa-199">Concepts de base d’une conversation de bot</span><span class="sxs-lookup"><span data-stu-id="dc4aa-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="dc4aa-200">Instructions de conception</span><span class="sxs-lookup"><span data-stu-id="dc4aa-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="dc4aa-201">Modèles d’interface utilisateur prêts à la production</span><span class="sxs-lookup"><span data-stu-id="dc4aa-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="dc4aa-202">Authentification bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="dc4aa-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="dc4aa-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="dc4aa-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="dc4aa-204">Créer un bot sans la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="dc4aa-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="dc4aa-205">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="dc4aa-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc4aa-206">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="dc4aa-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
