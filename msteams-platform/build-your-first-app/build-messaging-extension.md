---
title: Get started - Build a messaging extension
author: girliemac
description: Créez rapidement une extension Microsoft Teams messagerie à l’aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566060"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="6b406-103">Créez votre première extension de messagerie pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6b406-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="6b406-104">Il existe deux types d’extensions Teams *messagerie électronique*: les commandes [de recherche et](../messaging-extensions/how-to/search-commands/define-search-command.md) les commandes [d’action.](../messaging-extensions/how-to/action-commands/define-action-command.md)</span><span class="sxs-lookup"><span data-stu-id="6b406-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="6b406-105">Ce didacticiel vous apprend à créer une commande de recherche *(également* appelée *extension* de messagerie basée sur la recherche), qui est un raccourci pour rechercher du contenu externe et le partager dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6b406-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="6b406-106">Les utilisateurs peuvent accéder aux commandes de recherche à partir Teams la zone de composition ou de commande.</span><span class="sxs-lookup"><span data-stu-id="6b406-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="6b406-107">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="6b406-107">What you'll learn</span></span>

* <span data-ttu-id="6b406-108">Créez un projet d’application et un bot d’extension de messagerie à l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6b406-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="6b406-109">Comprendre les configurations d’application et la échafaudage pertinente pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6b406-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="6b406-110">Hébergez une application localement.</span><span class="sxs-lookup"><span data-stu-id="6b406-110">Host an app locally.</span></span>
* <span data-ttu-id="6b406-111">Configurez le bot pour votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6b406-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="6b406-112">Chargez et testez une extension de messagerie dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6b406-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b406-113">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="6b406-113">Prerequisites</span></span>

<span data-ttu-id="6b406-114">Assurez-vous que vous comprenez comment configurer et créer une application Teams simple.</span><span class="sxs-lookup"><span data-stu-id="6b406-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="6b406-115">Pour plus d’informations, [voir créer votre première Microsoft Teams application « Hello World!](../build-your-first-app/build-and-run.md)».</span><span class="sxs-lookup"><span data-stu-id="6b406-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="6b406-116">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="6b406-116">1. Create your app project</span></span>

<span data-ttu-id="6b406-117">Le Microsoft Teams Shared Computer Toolkit vous permet de configurer les composants suivants pour votre extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="6b406-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="6b406-118">**Configurations d’application et échafaudage pertinents** pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6b406-118">**App configurations and scaffolding** relevant to messaging extensions.</span></span>
* <span data-ttu-id="6b406-119">**Bot** pour votre extension de messagerie qui est automatiquement inscrite auprès du Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="6b406-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="6b406-120">**Pour créer votre projet d’application**</span><span class="sxs-lookup"><span data-stu-id="6b406-120">**To create your app project**</span></span>

1. In Visual Studio Code, select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.
1. <span data-ttu-id="6b406-122">Lorsque vous y invitez, connectez-vous avec votre Microsoft 365 de développement.</span><span class="sxs-lookup"><span data-stu-id="6b406-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="6b406-123">Dans **l’écran Sélectionner un** projet, dans **recherche d’extensions** de  >  messagerie, cliquez **sur JS (JavaScript).**</span><span class="sxs-lookup"><span data-stu-id="6b406-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="6b406-124">Entrez un nom pour votre application Teams de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6b406-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="6b406-125">Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6b406-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="6b406-126">Sélectionnez **Créer un bot,** puis cliquez **sur Créer l’inscription du** bot.</span><span class="sxs-lookup"><span data-stu-id="6b406-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="6b406-127">Si elle réussit, votre nouveau bot aura *l’état* Inscrit.</span><span class="sxs-lookup"><span data-stu-id="6b406-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="6b406-128">Votre bot est désormais inscrit automatiquement auprès du service Microsoft Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="6b406-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="6b406-129">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet et enregistrez-le sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6b406-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="6b406-130">2. Comprendre les composants de votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="6b406-130">2. Understand your app project components</span></span>

<span data-ttu-id="6b406-131">La plupart des configurations d’application et de la création de la Teams Shared Computer Toolkit sont automatiquement définies.</span><span class="sxs-lookup"><span data-stu-id="6b406-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="6b406-132">Configurations d’application : pour afficher ou mettre à jour les configurations de votre extension de messagerie, sélectionnez **App Studio** dans le kit de ressources et allez aux **extensions de messagerie.**</span><span class="sxs-lookup"><span data-stu-id="6b406-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="6b406-133">Création de la forme de l’application : la création de la forme de l’application fournit un fichier, situé dans le répertoire racine de votre projet, pour gérer la façon dont votre extension de messagerie (ou techniquement, le bot de l’extension de messagerie) répond aux requêtes de recherche dans `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="6b406-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="6b406-134">3. Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="6b406-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="6b406-135">À des fins de test, nous allons héberger votre extension de messagerie sur un serveur web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="6b406-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="6b406-136">Vous allez utiliser [ngrok](https://ngrok.com/download) pour configurer un tunnel sécurisé vers localhost.</span><span class="sxs-lookup"><span data-stu-id="6b406-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="6b406-137">Pour [plus d’informations, voir](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) créer Microsoft Teams bot.</span><span class="sxs-lookup"><span data-stu-id="6b406-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="6b406-138">Si ce n’est pas déjà fait, installez [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="6b406-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="6b406-139">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="6b406-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="6b406-140">Copiez l’URL HTTPS dans la sortie (par exemple), car Teams `https://468b9ab725e9.ngrok.io` nécessite des connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6b406-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="6b406-141">Avec cette URL, Teams (qui nécessite des connexions HTTPS) pourra tunneler vers l’endroit où vous hébergez votre application ( sur le `localhost` port 3978).</span><span class="sxs-lookup"><span data-stu-id="6b406-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="6b406-142">4. Configurer le bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="6b406-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="6b406-143">Les extensions de messagerie s’appuient sur des bots pour envoyer et traiter les demandes des utilisateurs Teams à votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="6b406-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="6b406-144">Le bot doit être inscrit auprès d’Azure Bot Service, ce qui a été fait lorsque vous avez installé votre application à l’aide du Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="6b406-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="6b406-145">Vous devez toujours spécifier une URL de point de terminaison de bot pour recevoir et traiter les requêtes de recherche dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6b406-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="6b406-146">En règle générale, l’URL ressemble `https://HOST_URL/api/messages` à .</span><span class="sxs-lookup"><span data-stu-id="6b406-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="6b406-147">Vous pouvez configurer cette configuration rapidement dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="6b406-147">You can configure this quickly in the toolkit.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Open **Microsoft Teams Shared Computer Toolkit**.
1. <span data-ttu-id="6b406-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span><span class="sxs-lookup"><span data-stu-id="6b406-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="6b406-150">Dans le **champ d’adresse** du point de terminaison bot, entrez l’URL ngrok (par exemple, ) où vous hébergez le bot et y `https://468b9ab725e9.ngrok.io` `/api/messages` appendez-le.</span><span class="sxs-lookup"><span data-stu-id="6b406-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="6b406-151">Votre bot sera en mesure de gérer les requêtes dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="6b406-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="6b406-152">5. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="6b406-152">5. Build and run your app</span></span>

<span data-ttu-id="6b406-153">Vous avez configuré une URL pour héberger votre extension de messagerie et configurée pour gérer les recherches.</span><span class="sxs-lookup"><span data-stu-id="6b406-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="6b406-154">Il est temps de rendre votre application opérationnel.</span><span class="sxs-lookup"><span data-stu-id="6b406-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="6b406-155">Ouvrez le terminal et allez dans le répertoire racine de votre projet d’application.</span><span class="sxs-lookup"><span data-stu-id="6b406-155">Open terminal and go to the root directory of your app project.</span></span>
1. <span data-ttu-id="6b406-156">Exécutez `npm install`.</span><span class="sxs-lookup"><span data-stu-id="6b406-156">Run `npm install`.</span></span>
1. <span data-ttu-id="6b406-157">Exécutez `npm start`.</span><span class="sxs-lookup"><span data-stu-id="6b406-157">Run `npm start`.</span></span>

   <span data-ttu-id="6b406-158">Si l’opération réussit, le message suivant indique que votre service d’extension de messagerie est à l’écoute de l’activité sur votre `localhost` :</span><span class="sxs-lookup"><span data-stu-id="6b406-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="6b406-159">6. Chargement d’une version de version de votre extension de messagerie dans Teams</span><span class="sxs-lookup"><span data-stu-id="6b406-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="6b406-160">Une fois votre extension de messagerie en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6b406-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="6b406-161">Si vous n’avez pas chargé une version de version Teams’application avant et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="6b406-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="6b406-162">Dans Visual Studio Code, sélectionnez la **touche F5** pour lancer un client Teams web.</span><span class="sxs-lookup"><span data-stu-id="6b406-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="6b406-163">Dans la boîte de dialogue d’installation de l’application, **sélectionnez Ajouter pour moi.**</span><span class="sxs-lookup"><span data-stu-id="6b406-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="6b406-164">7. Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="6b406-164">7. Test your messaging extension</span></span>

<span data-ttu-id="6b406-165">Découvrez comment fonctionnent les extensions de messagerie dans Teams conversation instantanée.</span><span class="sxs-lookup"><span data-stu-id="6b406-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="6b406-166">Démarrez une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="6b406-166">Start a new chat.</span></span> Dans la zone de composition, sélectionnez **Plus** et sélectionnez l’application d’extension de messagerie :::image type="icon" source="../assets/icons/teams-client-more.png"::: que vous avez chargé de côté.
1. <span data-ttu-id="6b406-168">Essayez de rechercher quelque chose (par exemple, **Tickets).**</span><span class="sxs-lookup"><span data-stu-id="6b406-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="6b406-169">Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pourrez en ajouter d’autres ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="6b406-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d’écran montrant comment une extension de messagerie basée sur la recherche est utilisée dans la Teams de composition.":::

## <a name="troubleshooting"></a><span data-ttu-id="6b406-171">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="6b406-171">Troubleshooting</span></span>

<span data-ttu-id="6b406-172">Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6b406-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="6b406-173">**Le bot n’est pas connecté à Teams**</span><span class="sxs-lookup"><span data-stu-id="6b406-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="6b406-174">Si vous avez installé votre application, mais qu’elle ne fonctionne pas, assurez-vous que le bot de l’extension de messagerie est connecté au canal Teams [ *azure* Bot Service.](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6b406-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="6b406-175">Il est important de comprendre que ce n’est pas le même qu’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6b406-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="6b406-176">Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication microsoft ou [tierce prise en charge.](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6b406-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="6b406-177">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6b406-177">See also</span></span>

* [<span data-ttu-id="6b406-178">Teams de composition ou de commande</span><span class="sxs-lookup"><span data-stu-id="6b406-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="6b406-179">Inclure une fonctionnalité de déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="6b406-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="6b406-180">Instructions de conception</span><span class="sxs-lookup"><span data-stu-id="6b406-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="6b406-181">Modèles d’interface utilisateur prêts pour la production</span><span class="sxs-lookup"><span data-stu-id="6b406-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="6b406-182">Ajouter une authentification</span><span class="sxs-lookup"><span data-stu-id="6b406-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="6b406-183">Créer une extension de messagerie basée sur une action</span><span class="sxs-lookup"><span data-stu-id="6b406-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="6b406-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="6b406-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="6b406-185">Prochaines étapes</span><span class="sxs-lookup"><span data-stu-id="6b406-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b406-186">Définir les commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="6b406-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b406-187">Répondre aux recherches des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6b406-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)
