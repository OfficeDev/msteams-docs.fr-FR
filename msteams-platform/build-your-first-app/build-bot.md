---
title: Prise en main-créer un bot
author: heath-hamilton
description: Créez rapidement un robot Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931737"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="c7b47-103">Créer un robot pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="c7b47-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="c7b47-104">Vous allez créer une application *bot* de base dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c7b47-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="c7b47-105">Un bot agit comme un intermédiaire entre les utilisateurs de teams et votre service Web.</span><span class="sxs-lookup"><span data-stu-id="c7b47-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="c7b47-106">Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.</span><span class="sxs-lookup"><span data-stu-id="c7b47-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="c7b47-107">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="c7b47-107">Your assignment</span></span>

<span data-ttu-id="c7b47-108">Votre espace de travail a créé une application teams qui utilise des [onglets](../build-your-first-app/build-personal-tab.md) pour exposer les informations de contact importantes.</span><span class="sxs-lookup"><span data-stu-id="c7b47-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="c7b47-109">Par exemple, les collègues ont un accès rapide au numéro de téléphone du support technique.</span><span class="sxs-lookup"><span data-stu-id="c7b47-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="c7b47-110">Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le support technique à l’aide d’un chatbot ?</span><span class="sxs-lookup"><span data-stu-id="c7b47-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="c7b47-111">Votre patron vous demande de consulter la rapidité avec laquelle vous pouvez faire fonctionner un robot de conversation de base dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7b47-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c7b47-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="c7b47-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="c7b47-113">Créer un projet d’application et un bot à l’aide de Microsoft teams Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="c7b47-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="c7b47-114">Identifier certaines configurations d’application et la génération de modèles automatique propres aux robots</span><span class="sxs-lookup"><span data-stu-id="c7b47-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="c7b47-115">Héberger une application localement</span><span class="sxs-lookup"><span data-stu-id="c7b47-115">Host an app locally</span></span>
> * <span data-ttu-id="c7b47-116">Configurer un bot pour teams</span><span class="sxs-lookup"><span data-stu-id="c7b47-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="c7b47-117">Chargement et tester un bot dans teams</span><span class="sxs-lookup"><span data-stu-id="c7b47-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c7b47-118">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c7b47-118">Before you begin</span></span>

<span data-ttu-id="c7b47-119">Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="c7b47-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="c7b47-120">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="c7b47-120">1. Create your app project</span></span>

<span data-ttu-id="c7b47-121">La boîte à outils Microsoft teams vous permet de configurer les composants suivants pour votre application :</span><span class="sxs-lookup"><span data-stu-id="c7b47-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="c7b47-122">**Configurations d’application et génération** d’une structure adaptée aux robots</span><span class="sxs-lookup"><span data-stu-id="c7b47-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="c7b47-123">**Robot** enregistré automatiquement avec le service Microsoft Azure bot</span><span class="sxs-lookup"><span data-stu-id="c7b47-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="c7b47-124">Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.</span><span class="sxs-lookup"><span data-stu-id="c7b47-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="c7b47-126">Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="c7b47-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="c7b47-127">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **bot** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c7b47-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="c7b47-128">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="c7b47-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="c7b47-129">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="c7b47-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="c7b47-130">Accédez à **configurer bot** et sélectionnez **créer un nouveau robot** , puis **inscrire un bot**.</span><span class="sxs-lookup"><span data-stu-id="c7b47-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="c7b47-131">Si elle réussit, votre nouveau Bot aura un statut **enregistré** .</span><span class="sxs-lookup"><span data-stu-id="c7b47-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="c7b47-132">Sélectionnez **Terminer** en bas de l’écran et choisissez un emplacement pour créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="c7b47-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="c7b47-133">2. identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="c7b47-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="c7b47-134">La plupart des configurations et des modèles d’application sont configurés automatiquement lorsque vous créez votre projet à l’aide de Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="c7b47-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="c7b47-135">Examinons les principaux composants de la création d’un bot.</span><span class="sxs-lookup"><span data-stu-id="c7b47-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="c7b47-136">Configurations d’application</span><span class="sxs-lookup"><span data-stu-id="c7b47-136">App configurations</span></span>

<span data-ttu-id="c7b47-137">Pour afficher ou mettre à jour les configurations de votre bot, sélectionnez **app Studio** dans la boîte à outils et accédez à **robots**.</span><span class="sxs-lookup"><span data-stu-id="c7b47-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="c7b47-138">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="c7b47-138">App scaffolding</span></span>

<span data-ttu-id="c7b47-139">La génération de modèles automatique d’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la manière dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques, tels que « Hello »).</span><span class="sxs-lookup"><span data-stu-id="c7b47-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="c7b47-140">3. configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="c7b47-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="c7b47-141">À des fins de test, nous allons héberger votre application sur un serveur Web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="c7b47-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="c7b47-142">Si vous ne l’avez pas encore fait, installez [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="c7b47-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="c7b47-143">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="c7b47-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="c7b47-144">Copiez l’URL HTTPs dans la sortie (par exemple, `https://468b9ab725e9.ngrok.io` ) puisque teams requiert des connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c7b47-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="c7b47-145">Avec cette URL, Teams (qui requiert des connexions HTTPs) peut être utilisé pour effectuer un tunnel vers l’endroit où vous hébergez votre application ( `localhost` sur le port 3978).</span><span class="sxs-lookup"><span data-stu-id="c7b47-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="c7b47-146">4. configurer votre robot</span><span class="sxs-lookup"><span data-stu-id="c7b47-146">4. Configure your bot</span></span>

<span data-ttu-id="c7b47-147">Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du service Microsoft Azure bot.</span><span class="sxs-lookup"><span data-stu-id="c7b47-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="c7b47-148">Heureusement, cette opération est exécutée automatiquement lorsque vous configurez votre application à l’aide de Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="c7b47-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="c7b47-149">Vous devez toujours spécifier une adresse de point de terminaison pour recevoir et traiter les messages utilisateur (par exemple, les demandes) envoyées au bot.</span><span class="sxs-lookup"><span data-stu-id="c7b47-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="c7b47-150">En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="c7b47-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="c7b47-151">Vous pouvez le configurer rapidement dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="c7b47-151">You can configure this quickly in the toolkit.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. <span data-ttu-id="c7b47-153">Accédez à **robots > inscriptions de robots existantes** et sélectionnez le robot que vous avez créé lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="c7b47-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="c7b47-154">Dans le champ **adresse du point de terminaison de robot** , entrez l’URL ngrok (par exemple, `https://468b9ab725e9.ngrok.io` ) où vous hébergez le bot et ajoutez `/api/messages` -y.</span><span class="sxs-lookup"><span data-stu-id="c7b47-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Illustration illustrant l’emplacement où vous pouvez configurer l’URL du point de terminaison du bot dans Team Toolkit.":::

<span data-ttu-id="c7b47-156">Votre robot pourra répondre aux messages dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7b47-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="c7b47-157">5. générez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="c7b47-157">5. Build and run your app</span></span>

<span data-ttu-id="c7b47-158">Vous avez configuré une URL pour héberger votre robot et le configurer pour qu’il gère les messages.</span><span class="sxs-lookup"><span data-stu-id="c7b47-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="c7b47-159">Il est temps de faire fonctionner votre application.</span><span class="sxs-lookup"><span data-stu-id="c7b47-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="c7b47-160">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="c7b47-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="c7b47-161">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="c7b47-161">Run `npm start`.</span></span>

<span data-ttu-id="c7b47-162">Si elle réussit, vous voyez le message suivant indiquant que votre robot est à l’écoute des activités sur le `localhost` :</span><span class="sxs-lookup"><span data-stu-id="c7b47-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="c7b47-163">6. chargement de votre robot dans teams</span><span class="sxs-lookup"><span data-stu-id="c7b47-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="c7b47-164">Une fois que votre robot est en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7b47-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="c7b47-165">Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="c7b47-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="c7b47-166">Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.</span><span class="sxs-lookup"><span data-stu-id="c7b47-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="c7b47-167">Dans la boîte de dialogue d’installation de l’application, sélectionnez **Ajouter pour moi**.</span><span class="sxs-lookup"><span data-stu-id="c7b47-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="c7b47-168">(Vous pouvez ajouter le bot à un canal ou une conversation, mais il est moins gênant pour les autres personnes de tester un bot dans une conversation en un seul.)</span><span class="sxs-lookup"><span data-stu-id="c7b47-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="c7b47-169">7. tester votre robot</span><span class="sxs-lookup"><span data-stu-id="c7b47-169">7. Test your bot</span></span>

<span data-ttu-id="c7b47-170">Maintenant pour la partie amusante : disons « Hello » à votre bot.</span><span class="sxs-lookup"><span data-stu-id="c7b47-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="c7b47-171">Dans la zone de composition, envoyez un `Hello` message.</span><span class="sxs-lookup"><span data-stu-id="c7b47-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="c7b47-172">Votre robot répond avec un message semblable à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c7b47-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Capture d’écran illustrant un utilisateur dire « Hello » à un bot de teams et obtenant une réponse.":::

## <a name="well-done"></a><span data-ttu-id="c7b47-174">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="c7b47-174">Well done</span></span>

<span data-ttu-id="c7b47-175">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="c7b47-175">Congratulations!</span></span> <span data-ttu-id="c7b47-176">Vous disposez d’un bot de teams de base qui peut communiquer avec des utilisateurs un-sur-un ou des paramètres de groupe (canaux et conversations).</span><span class="sxs-lookup"><span data-stu-id="c7b47-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c7b47-177">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="c7b47-177">Troubleshooting</span></span>

<span data-ttu-id="c7b47-178">Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c7b47-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="c7b47-179">Le bot n’est pas connecté à teams</span><span class="sxs-lookup"><span data-stu-id="c7b47-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="c7b47-180">Si vous avez installé votre application, mais que le bot ne fonctionne pas, vérifiez que le bot est [connecté au *canal* teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c7b47-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="c7b47-181">Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c7b47-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="c7b47-182">Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="c7b47-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c7b47-183">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="c7b47-183">Learn more</span></span>

* [<span data-ttu-id="c7b47-184">Voir les autres robots que les robots peuvent faire avec l’un de nos exemples</span><span class="sxs-lookup"><span data-stu-id="c7b47-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="c7b47-185">Concepts de base d’une conversation de bot</span><span class="sxs-lookup"><span data-stu-id="c7b47-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="c7b47-186">Authentification de robot dans teams</span><span class="sxs-lookup"><span data-stu-id="c7b47-186">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="c7b47-187">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="c7b47-187">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="c7b47-188">Créer un bot sans la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="c7b47-188">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
