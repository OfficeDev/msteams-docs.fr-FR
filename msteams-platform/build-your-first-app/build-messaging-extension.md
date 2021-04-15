---
title: Get started - Build a messaging extension
author: heath-hamilton
description: Créez rapidement une extension de messagerie Microsoft Teams à l'aide de microsoft Teams Shared Computer Toolkit.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 09e851820314efd3dc114b926a0111603cac18a4
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696877"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="8c14c-103">Créer une extension de messagerie pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8c14c-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="8c14c-104">Il existe deux types *d'extensions de messagerie* Teams : les commandes [de recherche et](../messaging-extensions/how-to/search-commands/define-search-command.md) les commandes [d'action.](../messaging-extensions/how-to/action-commands/define-action-command.md)</span><span class="sxs-lookup"><span data-stu-id="8c14c-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="8c14c-105">Dans cette leçon, vous allez créer une commande de recherche *(également* appelée *extension* de messagerie basée sur la recherche), qui est un raccourci pour rechercher du contenu externe et le partager dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="8c14c-106">Les utilisateurs peuvent accéder aux commandes de recherche à partir de la zone de [composition ou de commande Teams.](../messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="8c14c-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="8c14c-107">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="8c14c-107">Your assignment</span></span>

<span data-ttu-id="8c14c-108">Le service d'aide de votre organisation communique avec les utilisateurs via Teams, mais les tickets résident dans un système distinct.</span><span class="sxs-lookup"><span data-stu-id="8c14c-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="8c14c-109">Cela signifie que le personnel de support technique doit constamment faire des allers-retours entre les applications.</span><span class="sxs-lookup"><span data-stu-id="8c14c-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="8c14c-110">Vous allez étudier comment réduire cette quantité de changement de contexte en créant une simple extension de messagerie basée sur la recherche pour Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8c14c-111">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="8c14c-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="8c14c-112">Créer un projet d'application et un bot d'extension de messagerie à l'aide de la Shared Computer Toolkit Microsoft Teams Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8c14c-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="8c14c-113">Identifier les configurations d'application et une partie de la échafaudage pertinente pour les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="8c14c-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="8c14c-114">Héberger une application localement</span><span class="sxs-lookup"><span data-stu-id="8c14c-114">Host an app locally</span></span>
> * <span data-ttu-id="8c14c-115">Configurer le bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="8c14c-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="8c14c-116">Chargement de version test et test d'une extension de messagerie dans Teams</span><span class="sxs-lookup"><span data-stu-id="8c14c-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8c14c-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8c14c-117">Before you begin</span></span>

<span data-ttu-id="8c14c-118">Si vous ne l'avez pas encore fait, assurez-vous de bien comprendre et [d'installer les conditions préalables de développement teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="8c14c-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="8c14c-119">1. Créer votre projet d'application</span><span class="sxs-lookup"><span data-stu-id="8c14c-119">1. Create your app project</span></span>

<span data-ttu-id="8c14c-120">L'Shared Computer Toolkit Microsoft Teams vous aide à configurer les composants suivants pour votre extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="8c14c-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="8c14c-121">**Configurations d'application et échafaudage pertinents** pour les extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="8c14c-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="8c14c-122">**Bot** pour votre extension de messagerie qui est automatiquement inscrite auprès du service Microsoft Azure Bot</span><span class="sxs-lookup"><span data-stu-id="8c14c-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="8c14c-123">Si vous n'avez pas encore créé de projet d'application Teams, il peut vous être utile de suivre ces [instructions](../build-your-first-app/build-and-run.md) qui expliquent les projets plus en détail.</span><span class="sxs-lookup"><span data-stu-id="8c14c-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="8c14c-125">Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="8c14c-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="8c14c-126">Dans **l'écran Ajouter des fonctionnalités,** **sélectionnez Extension de messagerie,** puis **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8c14c-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="8c14c-127">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="8c14c-128">(Il s'agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d'application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="8c14c-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="8c14c-129">Dans **l'écran Configurer l'extension de** messagerie, faites les choses suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c14c-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="8c14c-130">Choisissez uniquement **l'option de recherche** pour le type d'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8c14c-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="8c14c-131">Sélectionnez **Créer un bot,** puis **Créer l'inscription du bot.**</span><span class="sxs-lookup"><span data-stu-id="8c14c-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="8c14c-132">Si elle réussit, votre nouveau bot aura un **état** inscrit.</span><span class="sxs-lookup"><span data-stu-id="8c14c-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="8c14c-133">Pour l'instant, **sélectionnez Non** pour l'option de déploiement de lien.</span><span class="sxs-lookup"><span data-stu-id="8c14c-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="8c14c-134">Sélectionnez **Terminer** en bas de l'écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="8c14c-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="8c14c-135">2. Identifier les composants de projet d'application pertinents</span><span class="sxs-lookup"><span data-stu-id="8c14c-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="8c14c-136">La plupart des configurations d'application et de la création de la Shared Computer Toolkit sont automatiquement définies lorsque vous créez votre projet.</span><span class="sxs-lookup"><span data-stu-id="8c14c-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="8c14c-137">Configurations d'application</span><span class="sxs-lookup"><span data-stu-id="8c14c-137">App configurations</span></span>

<span data-ttu-id="8c14c-138">Pour afficher ou mettre à jour les configurations de votre extension de messagerie, sélectionnez **App Studio** dans le kit de ressources et allez aux **extensions de messagerie.**</span><span class="sxs-lookup"><span data-stu-id="8c14c-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="8c14c-139">Échafaudage d'application</span><span class="sxs-lookup"><span data-stu-id="8c14c-139">App scaffolding</span></span>

<span data-ttu-id="8c14c-140">La création de la échafaudage de l'application fournit un fichier, situé dans le répertoire racine de votre projet, pour gérer la façon dont votre extension de messagerie (ou techniquement, le bot de l'extension de messagerie) répond aux requêtes de recherche dans `botActivityHandler.js` Teams. [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="8c14c-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="8c14c-141">3. Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="8c14c-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="8c14c-142">À des fins de test, nous allons héberger votre extension de messagerie sur un serveur web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="8c14c-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="8c14c-143">Si ce n'est pas déjà fait, installez [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="8c14c-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="8c14c-144">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="8c14c-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="8c14c-145">Copiez l'URL HTTPS dans la sortie (par exemple), car `https://468b9ab725e9.ngrok.io` Teams requiert des connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8c14c-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="8c14c-146">Avec cette URL, Teams (qui nécessite des connexions HTTPS) pourra tunneler vers l'endroit où vous hébergez votre application ( `localhost` sur le port 3978).</span><span class="sxs-lookup"><span data-stu-id="8c14c-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="8c14c-147">4. Configurer le bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="8c14c-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="8c14c-148">Les extensions de messagerie s'appuient sur des bots pour envoyer et traiter les demandes des utilisateurs de Teams vers votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="8c14c-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="8c14c-149">Le bot doit être inscrit auprès d'Azure Bot Service, ce qui a été fait lorsque vous avez installé votre application à l'aide de la Shared Computer Toolkit Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="8c14c-150">Vous devez toujours spécifier une URL de point de terminaison de bot pour recevoir et traiter les requêtes de recherche dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8c14c-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="8c14c-151">En règle générale, l'URL ressemble `https://HOST_URL/api/messages` à .</span><span class="sxs-lookup"><span data-stu-id="8c14c-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="8c14c-152">Vous pouvez configurer cette configuration rapidement dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="8c14c-152">You can configure this quickly in the toolkit.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Shared Computer Toolkit**.
1. <span data-ttu-id="8c14c-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span><span class="sxs-lookup"><span data-stu-id="8c14c-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="8c14c-155">Dans le **champ d'adresse** du point de terminaison bot, entrez l'URL ngrok (par exemple, ) où vous hébergez le bot et y `https://468b9ab725e9.ngrok.io` `/api/messages` appendez-le.</span><span class="sxs-lookup"><span data-stu-id="8c14c-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="8c14c-156">Votre bot sera en mesure de gérer les requêtes dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8c14c-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="8c14c-157">5. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="8c14c-157">5. Build and run your app</span></span>

<span data-ttu-id="8c14c-158">Vous avez configuré une URL pour héberger votre extension de messagerie et configurée pour gérer les recherches.</span><span class="sxs-lookup"><span data-stu-id="8c14c-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="8c14c-159">Il est temps de rendre votre application opérationnel.</span><span class="sxs-lookup"><span data-stu-id="8c14c-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="8c14c-160">Dans un terminal, allez dans le répertoire racine de votre projet d'application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="8c14c-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="8c14c-161">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="8c14c-161">Run `npm start`.</span></span>

<span data-ttu-id="8c14c-162">Si l'opération réussit, le message suivant indique que votre service d'extension de messagerie est à l'écoute de l'activité sur votre `localhost` :</span><span class="sxs-lookup"><span data-stu-id="8c14c-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="8c14c-163">6. Chargement d'une version de version de votre extension de messagerie dans Teams</span><span class="sxs-lookup"><span data-stu-id="8c14c-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="8c14c-164">Une fois votre extension de messagerie en cours d'exécution, vous pouvez l'installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="8c14c-165">Si vous n'avez pas encore chargé une application Teams et que vous avez des problèmes, suivez ces [instructions.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="8c14c-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="8c14c-166">Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="8c14c-167">Dans la boîte de dialogue d'installation de l'application, **sélectionnez Ajouter pour moi.**</span><span class="sxs-lookup"><span data-stu-id="8c14c-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="8c14c-168">7. Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="8c14c-168">7. Test your messaging extension</span></span>

<span data-ttu-id="8c14c-169">Découvrez comment fonctionnent les extensions de messagerie dans une conversation Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="8c14c-170">Démarrez une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="8c14c-170">Start a new chat.</span></span> Dans la zone de composition, sélectionnez **Plus** et choisissez l'application d'extension de messagerie :::image type="icon" source="../assets/icons/teams-client-more.png"::: que vous avez juste chargé de côté.
1. <span data-ttu-id="8c14c-172">Essayez de rechercher quelque chose (par exemple, **Tickets).**</span><span class="sxs-lookup"><span data-stu-id="8c14c-172">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="8c14c-173">Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pourrez en ajouter d'autres ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="8c14c-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d'écran montrant comment une extension de messagerie basée sur la recherche est utilisée dans la zone de composition Teams.":::

## <a name="well-done"></a><span data-ttu-id="8c14c-175">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="8c14c-175">Well done</span></span>

<span data-ttu-id="8c14c-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="8c14c-176">Congratulations!</span></span> <span data-ttu-id="8c14c-177">Vous avez une extension de messagerie Teams de base qui est définie pour rechercher du contenu externe dans la zone de composition ou de commande.</span><span class="sxs-lookup"><span data-stu-id="8c14c-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c14c-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c14c-178">Next steps</span></span>

<span data-ttu-id="8c14c-179">Consultez les pages suivantes pour continuer et créer une extension de messagerie complète :</span><span class="sxs-lookup"><span data-stu-id="8c14c-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="8c14c-180">[Définissez les commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) qui sont pertinentes pour votre service.</span><span class="sxs-lookup"><span data-stu-id="8c14c-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="8c14c-181">Configurez votre service pour [répondre aux recherches des utilisateurs.](../messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="8c14c-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8c14c-182">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="8c14c-182">Troubleshooting</span></span>

<span data-ttu-id="8c14c-183">Les informations suivantes peuvent vous aider si vous avez des problèmes lors de la réalisation de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8c14c-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="8c14c-184">Le bot n'est pas connecté à Teams</span><span class="sxs-lookup"><span data-stu-id="8c14c-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="8c14c-185">Si vous avez installé votre application, mais qu'elle ne fonctionne pas, assurez-vous que le bot de l'extension de messagerie est connecté au canal [Teams d'Azure Bot Service.](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8c14c-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="8c14c-186">Il est important de comprendre que ce n'est pas le même qu'un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8c14c-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="8c14c-187">Dans ce cas, un canal est la façon dont azure Bot Service connecte votre bot à Teams ou à une autre application de communication microsoft ou [tierce prise en charge.](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8c14c-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="8c14c-188">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="8c14c-188">Learn more</span></span>

* [<span data-ttu-id="8c14c-189">Inclure une fonctionnalité de déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="8c14c-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* <span data-ttu-id="8c14c-190">Suivez nos [instructions de conception](../messaging-extensions/design/messaging-extension-design.md) et créez avec des [modèles d'interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.</span><span class="sxs-lookup"><span data-stu-id="8c14c-190">Follow our [design guidelines](../messaging-extensions/design/messaging-extension-design.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="8c14c-191">Ajouter une authentification</span><span class="sxs-lookup"><span data-stu-id="8c14c-191">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="8c14c-192">Créer une extension de messagerie basée sur une action</span><span class="sxs-lookup"><span data-stu-id="8c14c-192">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="8c14c-193">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8c14c-193">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

