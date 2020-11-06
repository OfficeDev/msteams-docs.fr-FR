---
title: Prise en main-créer une extension de messagerie
author: heath-hamilton
description: Créez rapidement une extension de messagerie Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931749"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="65352-103">Créer une extension de messagerie pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="65352-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="65352-104">Il existe deux types d’extensions de *messagerie* d’application teams : [commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) et [commandes d’action](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="65352-104">There are two types of Teams app *messaging extensions* : [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="65352-105">Dans cette leçon, vous allez créer une *commande de recherche* (également appelée *extension de messagerie basée sur la recherche* ), qui est un raccourci permettant de trouver du contenu externe et de le partager dans Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension* ), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="65352-106">Les utilisateurs peuvent accéder aux commandes de recherche à partir de la [zone de composition ou de commande teams](../messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="65352-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="65352-107">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="65352-107">Your assignment</span></span>

<span data-ttu-id="65352-108">Le service d’assistance de votre organisation communique avec les utilisateurs par le biais de teams, mais les tickets se trouvent dans un système distinct.</span><span class="sxs-lookup"><span data-stu-id="65352-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="65352-109">Cela signifie que le personnel de support technique doit constamment basculer entre les applications.</span><span class="sxs-lookup"><span data-stu-id="65352-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="65352-110">Vous allez examiner la manière dont vous pouvez réduire ce pourcentage de changement de contexte en créant une simple extension de messagerie basée sur la recherche pour Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="65352-111">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="65352-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="65352-112">Créer un projet d’application et un bot d’extension de messagerie à l’aide de Microsoft teams Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="65352-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="65352-113">Identifier les configurations des applications et une partie de la structure relative aux extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="65352-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="65352-114">Héberger une application localement</span><span class="sxs-lookup"><span data-stu-id="65352-114">Host an app locally</span></span>
> * <span data-ttu-id="65352-115">Configurer le bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="65352-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="65352-116">Chargement et test d’une extension de messagerie dans teams</span><span class="sxs-lookup"><span data-stu-id="65352-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="65352-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="65352-117">Before you begin</span></span>

<span data-ttu-id="65352-118">Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="65352-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="65352-119">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="65352-119">1. Create your app project</span></span>

<span data-ttu-id="65352-120">Microsoft teams Toolkit vous permet de configurer les composants suivants pour votre extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="65352-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="65352-121">**Configurations d’application et génération de modèles d’application concernant les** extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="65352-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="65352-122">**Robot** de votre extension de messagerie enregistré automatiquement avec le service Microsoft Azure bot</span><span class="sxs-lookup"><span data-stu-id="65352-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="65352-123">Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.</span><span class="sxs-lookup"><span data-stu-id="65352-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="65352-125">Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="65352-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="65352-126">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez extension de **messagerie** , puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="65352-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="65352-127">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="65352-128">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="65352-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="65352-129">Dans l’écran **configurer l’extension de messagerie** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65352-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="65352-130">Choisissez uniquement l’option **basée sur la recherche** pour le type d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="65352-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="65352-131">Sélectionnez **créer un robot** , puis **inscrire un bot**.</span><span class="sxs-lookup"><span data-stu-id="65352-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="65352-132">Si elle réussit, votre nouveau Bot aura un statut **enregistré** .</span><span class="sxs-lookup"><span data-stu-id="65352-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="65352-133">Pour le moment, sélectionnez **non** pour l’option lien unfurling.</span><span class="sxs-lookup"><span data-stu-id="65352-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="65352-134">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="65352-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="65352-135">2. identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="65352-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="65352-136">La plupart des configurations et des modèles d’application sont configurés automatiquement lorsque vous créez votre projet à l’aide de Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="65352-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="65352-137">Configurations d’application</span><span class="sxs-lookup"><span data-stu-id="65352-137">App configurations</span></span>

<span data-ttu-id="65352-138">Pour afficher ou mettre à jour les configurations de votre extension de messagerie, sélectionnez **app Studio** dans la boîte à outils et accédez à **extensions de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="65352-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="65352-139">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="65352-139">App scaffolding</span></span>

<span data-ttu-id="65352-140">La génération de modèles automatique de l’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la façon dont votre extension de messagerie (ou techniquement, le [bot de l’extension de messagerie](#4-configure-the-bot-for-your-messaging-extension)) répond aux requêtes de recherche dans Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="65352-141">3. configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="65352-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="65352-142">À des fins de test, nous allons héberger votre extension de messagerie sur un serveur Web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="65352-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="65352-143">Si vous ne l’avez pas encore fait, installez [ngrok](https://ngrok.com/download).</span><span class="sxs-lookup"><span data-stu-id="65352-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="65352-144">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="65352-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="65352-145">Copiez l’URL HTTPs dans la sortie (par exemple, `https://468b9ab725e9.ngrok.io` ) puisque teams requiert des connexions HTTPS.</span><span class="sxs-lookup"><span data-stu-id="65352-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="65352-146">Avec cette URL, Teams (qui requiert des connexions HTTPs) peut être utilisé pour effectuer un tunnel vers l’endroit où vous hébergez votre application ( `localhost` sur le port 3978).</span><span class="sxs-lookup"><span data-stu-id="65352-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="65352-147">4. configurer le bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="65352-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="65352-148">Les extensions de messagerie s’appuient sur les robots pour envoyer et traiter les demandes des utilisateurs de teams vers votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="65352-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="65352-149">Le bot doit être enregistré avec le service Azure bot, qui a été créé lors de la configuration de votre application à l’aide du kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="65352-150">Vous devez toujours spécifier une URL de point de terminaison de bot pour recevoir et traiter des requêtes de recherche dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="65352-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="65352-151">En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="65352-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="65352-152">Vous pouvez le configurer rapidement dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="65352-152">You can configure this quickly in the toolkit.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. <span data-ttu-id="65352-154">Accédez à **robots > inscriptions de robots existantes** et sélectionnez le robot que vous avez créé lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="65352-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="65352-155">Dans le champ **adresse du point de terminaison de robot** , entrez l’URL ngrok (par exemple, `https://468b9ab725e9.ngrok.io` ) où vous hébergez le bot et ajoutez `/api/messages` -y.</span><span class="sxs-lookup"><span data-stu-id="65352-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="65352-156">Votre robot pourra gérer les requêtes dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="65352-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="65352-157">5. générez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="65352-157">5. Build and run your app</span></span>

<span data-ttu-id="65352-158">Vous avez configuré une URL pour héberger votre extension de messagerie et la configurer pour qu’elle gère les recherches.</span><span class="sxs-lookup"><span data-stu-id="65352-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="65352-159">Il est temps de faire fonctionner votre application.</span><span class="sxs-lookup"><span data-stu-id="65352-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="65352-160">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="65352-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="65352-161">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="65352-161">Run `npm start`.</span></span>

<span data-ttu-id="65352-162">Si elle réussit, vous voyez le message suivant indiquant que votre service d’extension de messagerie est à l’écoute de l’activité `localhost` :</span><span class="sxs-lookup"><span data-stu-id="65352-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="65352-163">6. chargement votre extension de messagerie dans teams</span><span class="sxs-lookup"><span data-stu-id="65352-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="65352-164">Une fois que votre extension de messagerie est en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="65352-165">Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="65352-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="65352-166">Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="65352-167">Dans la boîte de dialogue d’installation de l’application, sélectionnez **Ajouter pour moi**.</span><span class="sxs-lookup"><span data-stu-id="65352-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="65352-168">7. tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="65352-168">7. Test your messaging extension</span></span>

<span data-ttu-id="65352-169">Découvrez comment fonctionnent les extensions de messagerie dans une conversation Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="65352-170">Démarrez une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="65352-170">Start a new chat.</span></span> Dans la zone de composition, sélectionnez **plus** , :::image type="icon" source="../assets/icons/teams-client-more.png"::: puis choisissez l’application de l’extension de messagerie que vous venez de versions test chargées.
1. <span data-ttu-id="65352-172">Essayez de rechercher un article (par exemple, **tickets** ).</span><span class="sxs-lookup"><span data-stu-id="65352-172">Try searching for something (for example, **Tickets** ).</span></span> <span data-ttu-id="65352-173">Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pouvez ajouter votre propre version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="65352-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d’écran illustrant l’utilisation d’une extension de messagerie basée sur la recherche dans la zone de composition de teams.":::

## <a name="well-done"></a><span data-ttu-id="65352-175">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="65352-175">Well done</span></span>

<span data-ttu-id="65352-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="65352-176">Congratulations!</span></span> <span data-ttu-id="65352-177">Vous disposez d’une extension de messagerie teams de base qui est configurée pour rechercher du contenu externe dans la zone de composition ou de commande.</span><span class="sxs-lookup"><span data-stu-id="65352-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65352-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65352-178">Next steps</span></span>

<span data-ttu-id="65352-179">Consultez les pages suivantes pour continuer et créer une extension de messagerie complète :</span><span class="sxs-lookup"><span data-stu-id="65352-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="65352-180">[Définir des commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) pertinentes pour votre service.</span><span class="sxs-lookup"><span data-stu-id="65352-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="65352-181">Configurez votre service pour [répondre aux recherches des utilisateurs](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="65352-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="65352-182">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="65352-182">Troubleshooting</span></span>

<span data-ttu-id="65352-183">Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="65352-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="65352-184">Le bot n’est pas connecté à teams</span><span class="sxs-lookup"><span data-stu-id="65352-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="65352-185">Si vous avez installé votre application, mais qu’elle ne fonctionne pas, vérifiez que le robot de l’extension de messagerie est [connecté au *canal* teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="65352-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="65352-186">Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="65352-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="65352-187">Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="65352-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="65352-188">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="65352-188">Learn more</span></span>

* [<span data-ttu-id="65352-189">Inclure une fonctionnalité de unfurling de liens</span><span class="sxs-lookup"><span data-stu-id="65352-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="65352-190">Ajouter une authentification</span><span class="sxs-lookup"><span data-stu-id="65352-190">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="65352-191">Créer une extension de messagerie basée sur une action</span><span class="sxs-lookup"><span data-stu-id="65352-191">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="65352-192">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="65352-192">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
