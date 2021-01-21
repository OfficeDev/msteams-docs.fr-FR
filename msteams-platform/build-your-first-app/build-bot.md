---
title: Get started - Build a bot
author: heath-hamilton
description: Créez rapidement un bot Microsoft Teams à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: fbabd5130f0b7eb648a980f5f143792cc4c17933
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911946"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="9caed-103">Créer un bot pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9caed-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="9caed-104">Vous allez créer une application *de bot* de base dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9caed-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="9caed-105">Un bot fait office d’intermédiaire entre les utilisateurs de Teams et votre service web.</span><span class="sxs-lookup"><span data-stu-id="9caed-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="9caed-106">Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.</span><span class="sxs-lookup"><span data-stu-id="9caed-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="9caed-107">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="9caed-107">Your assignment</span></span>

<span data-ttu-id="9caed-108">Votre espace de travail a créé une application Teams qui utilise [des onglets](../build-your-first-app/build-personal-tab.md) pour mettre en avant des informations de contact importantes.</span><span class="sxs-lookup"><span data-stu-id="9caed-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="9caed-109">Par exemple, les collègues ont un accès rapide au numéro de téléphone du service d’aide.</span><span class="sxs-lookup"><span data-stu-id="9caed-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="9caed-110">Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le service d’aide à l’aide d’un chatbot ?</span><span class="sxs-lookup"><span data-stu-id="9caed-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="9caed-111">Votre responsable vous demande de voir à quelle vitesse vous pouvez obtenir un bot de conversation de base opérationnel dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="9caed-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="9caed-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9caed-113">Créer un projet d’application et un bot à l’aide de microsoft Teams Shared Computer Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="9caed-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="9caed-114">Identifier certaines configurations d’application et la échafaudage pertinentes pour les bots</span><span class="sxs-lookup"><span data-stu-id="9caed-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="9caed-115">Héberger une application localement</span><span class="sxs-lookup"><span data-stu-id="9caed-115">Host an app locally</span></span>
> * <span data-ttu-id="9caed-116">Configurer un bot pour Teams</span><span class="sxs-lookup"><span data-stu-id="9caed-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="9caed-117">Chargement de version test et test d’un bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="9caed-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9caed-118">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9caed-118">Before you begin</span></span>

<span data-ttu-id="9caed-119">Si vous ne l’avez pas encore fait, assurez-vous de bien comprendre et [d’installer les conditions préalables de développement teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="9caed-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="9caed-120">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="9caed-120">1. Create your app project</span></span>

<span data-ttu-id="9caed-121">La Shared Computer Toolkit Microsoft Teams vous aide à configurer les composants suivants pour votre application :</span><span class="sxs-lookup"><span data-stu-id="9caed-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="9caed-122">**Configurations d’application et échafaudage pertinents** pour les bots</span><span class="sxs-lookup"><span data-stu-id="9caed-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="9caed-123">**Bot** inscrit automatiquement auprès du service de bot Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9caed-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="9caed-124">Si vous n’avez pas encore créé de projet d’application Teams, il peut vous être utile de suivre ces [instructions](../build-your-first-app/build-and-run.md) qui expliquent les projets plus en détail.</span><span class="sxs-lookup"><span data-stu-id="9caed-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="9caed-126">Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="9caed-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="9caed-127">Dans **l’écran Ajouter des fonctionnalités,** **sélectionnez Bot,** puis **Suivant.**</span><span class="sxs-lookup"><span data-stu-id="9caed-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="9caed-128">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="9caed-129">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="9caed-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="9caed-130">Go to **Configure bot** and select **Create a new Bot** then Create Bot **Registration**.</span><span class="sxs-lookup"><span data-stu-id="9caed-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="9caed-131">Si elle réussit, votre nouveau bot aura un **état** inscrit.</span><span class="sxs-lookup"><span data-stu-id="9caed-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="9caed-132">Sélectionnez **Terminer** en bas de l’écran et choisissez un emplacement pour créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="9caed-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="9caed-133">2. Identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="9caed-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="9caed-134">La plupart des configurations d’application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet.</span><span class="sxs-lookup"><span data-stu-id="9caed-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="9caed-135">Examinons les principaux composants de la création d’un bot.</span><span class="sxs-lookup"><span data-stu-id="9caed-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="9caed-136">Configurations d’application</span><span class="sxs-lookup"><span data-stu-id="9caed-136">App configurations</span></span>

<span data-ttu-id="9caed-137">Pour afficher ou mettre à jour les configurations de votre bot, sélectionnez **App Studio** dans le kit de ressources et allez à **Bots**.</span><span class="sxs-lookup"><span data-stu-id="9caed-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="9caed-138">Échafaudage d’application</span><span class="sxs-lookup"><span data-stu-id="9caed-138">App scaffolding</span></span>

<span data-ttu-id="9caed-139">La création de modèles d’application fournit un fichier, situé dans le répertoire racine de votre projet, pour gérer la façon dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques tels que « `botActivityHandler.js` Hello »).</span><span class="sxs-lookup"><span data-stu-id="9caed-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="9caed-140">3. Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="9caed-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="9caed-141">À des fins de test, nous allons héberger votre application sur un serveur web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="9caed-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="9caed-142">Si ce n’est pas déjà fait, installez [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="9caed-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="9caed-143">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="9caed-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="9caed-144">Copiez l’URL HTTPS dans la sortie (par exemple), car `https://468b9ab725e9.ngrok.io` Teams requiert des connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9caed-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="9caed-145">Avec cette URL, Teams (qui nécessite des connexions HTTPS) pourra tunneler vers l’endroit où vous hébergez votre application ( `localhost` sur le port 3978).</span><span class="sxs-lookup"><span data-stu-id="9caed-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="9caed-146">4. Configurer votre bot</span><span class="sxs-lookup"><span data-stu-id="9caed-146">4. Configure your bot</span></span>

<span data-ttu-id="9caed-147">Pour utiliser un bot dans Teams, vous devez l’inscrire auprès d’Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="9caed-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="9caed-148">Pour vous, cela s’effectue automatiquement lorsque vous définissez votre application à l’aide du Shared Computer Toolkit Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="9caed-149">Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages utilisateur (c’est-à-dire, les demandes) envoyés au bot.</span><span class="sxs-lookup"><span data-stu-id="9caed-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="9caed-150">En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à .</span><span class="sxs-lookup"><span data-stu-id="9caed-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="9caed-151">Vous pouvez configurer cette configuration rapidement dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="9caed-151">You can configure this quickly in the toolkit.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Shared Computer Toolkit**.
1. <span data-ttu-id="9caed-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span><span class="sxs-lookup"><span data-stu-id="9caed-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="9caed-154">Dans le **champ d’adresse** du point de terminaison bot, entrez l’URL ngrok (par exemple, ) où vous hébergez le bot et y `https://468b9ab725e9.ngrok.io` `/api/messages` appendez-le.</span><span class="sxs-lookup"><span data-stu-id="9caed-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Illustration montrant où vous pouvez configurer l’URL du point de terminaison du bot dans la Shared Computer Toolkit Teams.":::

<span data-ttu-id="9caed-156">Votre bot pourra répondre aux messages dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="9caed-157">5. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="9caed-157">5. Build and run your app</span></span>

<span data-ttu-id="9caed-158">Vous avez configuré une URL pour héberger votre bot et configurée pour gérer les messages.</span><span class="sxs-lookup"><span data-stu-id="9caed-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="9caed-159">Il est temps de rendre votre application opérationnel.</span><span class="sxs-lookup"><span data-stu-id="9caed-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="9caed-160">Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="9caed-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="9caed-161">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="9caed-161">Run `npm start`.</span></span>

<span data-ttu-id="9caed-162">Si l’opération réussit, vous voyez le message suivant indiquant que votre bot est à l’écoute de l’activité au niveau de votre `localhost` :</span><span class="sxs-lookup"><span data-stu-id="9caed-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="9caed-163">6. Chargement d’une version de version de votre bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="9caed-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="9caed-164">Avec votre bot en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="9caed-165">Si vous n’avez pas encore chargé une application Teams et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="9caed-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="9caed-166">Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="9caed-167">Dans la boîte de dialogue d’installation de l’application, **sélectionnez Ajouter pour moi.**</span><span class="sxs-lookup"><span data-stu-id="9caed-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="9caed-168">(Vous pouvez ajouter le bot à un canal ou une conversation, mais il est moins intrusif pour d’autres personnes de tester un bot dans une conversation un-à-un.)</span><span class="sxs-lookup"><span data-stu-id="9caed-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="9caed-169">7. Testez votre bot</span><span class="sxs-lookup"><span data-stu-id="9caed-169">7. Test your bot</span></span>

<span data-ttu-id="9caed-170">Maintenant, nous allons dire « Hello » à votre bot.</span><span class="sxs-lookup"><span data-stu-id="9caed-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="9caed-171">Dans la zone de composition, envoyez un `Hello` message.</span><span class="sxs-lookup"><span data-stu-id="9caed-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="9caed-172">Votre bot répond par le message suivant.</span><span class="sxs-lookup"><span data-stu-id="9caed-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Capture d’écran montrant un utilisateur dire « Hello » à un bot Teams et obtenir une réponse.":::

## <a name="well-done"></a><span data-ttu-id="9caed-174">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="9caed-174">Well done</span></span>

<span data-ttu-id="9caed-175">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9caed-175">Congratulations!</span></span> <span data-ttu-id="9caed-176">Vous avez un bot Teams de base qui peut communiquer avec les utilisateurs un-à-un ou dans les paramètres de groupe (canaux et conversations).</span><span class="sxs-lookup"><span data-stu-id="9caed-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9caed-177">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="9caed-177">Troubleshooting</span></span>

<span data-ttu-id="9caed-178">Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9caed-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="9caed-179">Le bot n’est pas connecté à Teams</span><span class="sxs-lookup"><span data-stu-id="9caed-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="9caed-180">Si vous avez installé votre application, mais que le bot ne fonctionne pas, assurez-vous que le bot est connecté au canal [Teams d’Azure Bot Service.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9caed-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="9caed-181">Il est important de comprendre que ce n’est pas le même qu’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9caed-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="9caed-182">Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication microsoft ou [tierce prise en charge.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9caed-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="9caed-183">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="9caed-183">Learn more</span></span>

* [<span data-ttu-id="9caed-184">Voir les autres choses que les bots Teams peuvent faire avec l’un de nos exemples</span><span class="sxs-lookup"><span data-stu-id="9caed-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="9caed-185">Concepts de base d’une conversation de bot</span><span class="sxs-lookup"><span data-stu-id="9caed-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="9caed-186">Suivez nos [instructions de conception](../bots/design/bots.md) et créez avec des [modèles d’interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.</span><span class="sxs-lookup"><span data-stu-id="9caed-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="9caed-187">Authentification de bot dans Teams</span><span class="sxs-lookup"><span data-stu-id="9caed-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="9caed-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9caed-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="9caed-189">Créer un bot sans le kit de ressources</span><span class="sxs-lookup"><span data-stu-id="9caed-189">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
