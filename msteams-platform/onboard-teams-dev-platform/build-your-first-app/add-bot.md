---
title: Créer un robot pour Teams
author: heath-hamilton
description: Découvrez comment créer un bot dans votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964724"
---
# <a name="create-a-bot-for-teams"></a><span data-ttu-id="d2d50-103">Créer un robot pour Teams</span><span class="sxs-lookup"><span data-stu-id="d2d50-103">Create a bot for Teams</span></span>

<span data-ttu-id="d2d50-104">Vous allez créer une application *bot* de base dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d2d50-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="d2d50-105">Un bot agit comme un intermédiaire entre les utilisateurs de teams et votre service Web.</span><span class="sxs-lookup"><span data-stu-id="d2d50-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="d2d50-106">Les utilisateurs peuvent discuter avec un bot pour obtenir rapidement des informations ou initier des flux de travail et des tâches effectuées par votre service.</span><span class="sxs-lookup"><span data-stu-id="d2d50-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="d2d50-107">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="d2d50-107">Your assignment</span></span>

<span data-ttu-id="d2d50-108">Votre espace de travail a utilisé des [onglets](../build-your-first-app/add-personal-tab.md) pour exposer les informations de contact importantes dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-108">Your workplace has been using [tabs](../build-your-first-app/add-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="d2d50-109">Par exemple, les collègues ont un accès rapide au numéro de téléphone du support technique.</span><span class="sxs-lookup"><span data-stu-id="d2d50-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="d2d50-110">Mais au lieu d’appeler, que se passe-t-il si des personnes peuvent contacter le support technique à l’aide d’un chatbot ?</span><span class="sxs-lookup"><span data-stu-id="d2d50-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="d2d50-111">Votre patron vous demande de consulter la rapidité avec laquelle vous pouvez faire fonctionner un robot de conversation de base dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d2d50-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="d2d50-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="d2d50-113">Créer un projet d’application et un bot à l’aide de Microsoft teams Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="d2d50-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="d2d50-114">Identifier les propriétés du manifeste de l’application et une partie de la structure concernant les robots</span><span class="sxs-lookup"><span data-stu-id="d2d50-114">Identify the app manifest properties and some of the scaffolding relevant to bots</span></span>
> * <span data-ttu-id="d2d50-115">Héberger un bot localement</span><span class="sxs-lookup"><span data-stu-id="d2d50-115">Host a bot locally</span></span>
> * <span data-ttu-id="d2d50-116">Configurer un bot pour teams</span><span class="sxs-lookup"><span data-stu-id="d2d50-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="d2d50-117">Chargement et tester un bot dans teams</span><span class="sxs-lookup"><span data-stu-id="d2d50-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d2d50-118">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d2d50-118">Before you begin</span></span>

<span data-ttu-id="d2d50-119">Si vous ne l’avez pas encore fait, configurez votre [compte](building-real-world-app.md#set-up-your-development-account) de développement Microsoft 365 et les outils de l' [application teams](building-real-world-app.md#install-your-development-tools).</span><span class="sxs-lookup"><span data-stu-id="d2d50-119">If you haven't yet, set up your Microsoft 365 development [account](building-real-world-app.md#set-up-your-development-account) and [Teams app tools](building-real-world-app.md#install-your-development-tools).</span></span>

## <a name="create-your-app-project-and-bot"></a><span data-ttu-id="d2d50-120">Création de votre projet d’application et de votre robot</span><span class="sxs-lookup"><span data-stu-id="d2d50-120">Create your app project and bot</span></span>

<span data-ttu-id="d2d50-121">La boîte à outils Microsoft teams vous permet de configurer les composants suivants pour votre application :</span><span class="sxs-lookup"><span data-stu-id="d2d50-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="d2d50-122">**Projet d’application**: inclut le manifeste de l’application et la génération de modèles adaptés aux robots</span><span class="sxs-lookup"><span data-stu-id="d2d50-122">**App project**: Includes the app manifest and scaffolding relevant to bots</span></span>
* <span data-ttu-id="d2d50-123">**Bot**: configure un nouveau Bot et l’enregistre avec le service Microsoft Azure bot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-123">**Bot**: Configures a new bot and registers it with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="d2d50-124">Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.</span><span class="sxs-lookup"><span data-stu-id="d2d50-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="d2d50-126">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="d2d50-127">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="d2d50-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="d2d50-128">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **bot** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d2d50-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="d2d50-129">Sélectionnez **créer un nouveau robot** et **Connectez** -vous pour vous connecter à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="d2d50-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="Illustration illustrant comment, dans la boîte à outils Teams, connectez-vous à votre compte Microsoft 365 pour créer un nouveau Bot.":::
1. <span data-ttu-id="d2d50-131">Module Entrez un nom personnalisé pour votre bot et sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="d2d50-131">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="d2d50-132">(Rappelez-vous qu’il s’agit du nom de votre bot et non du nom de l’application teams que vous avez déjà spécifiée.)</span><span class="sxs-lookup"><span data-stu-id="d2d50-132">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="d2d50-133">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="d2d50-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="d2d50-134">Identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="d2d50-134">Identify relevant app project components</span></span>

<span data-ttu-id="d2d50-135">La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-135">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="d2d50-136">Examinons les principaux composants de la création d’un bot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-136">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="d2d50-137">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="d2d50-137">App manifest</span></span>

<span data-ttu-id="d2d50-138">L’extrait de code suivant du manifeste de l’application ( `manifest.json` fichier dans le répertoire de votre projet `.publish` ) affiche les propriétés et les valeurs par défaut relatives aux robots.</span><span class="sxs-lookup"><span data-stu-id="d2d50-138">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

```JSON
    "bots": [
        {
            "botId": "{botId0}",
            "scopes": [
                "personal",
                "groupchat",
                "team"
            ],
            "supportsFiles": false,
            "isNotificationOnly": false,
            "commandLists": [
                {
                    "scopes": [
                        "personal",
                        "groupchat",
                        "team"
                    ],
                    "commands": [
                        {
                            "title": "Hello",
                            "description": "Sends a hello message and @mention the sender"
                        }
                    ]
                }
            ]
        }
    ],
```

<span data-ttu-id="d2d50-139">Pour le moment, nous allons nous concentrer sur les propriétés requises suivantes.</span><span class="sxs-lookup"><span data-stu-id="d2d50-139">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="d2d50-140">(Consultez la liste complète des propriétés prises en charge [`bots`](../../resources/schema/manifest-schema.md#bots) .)</span><span class="sxs-lookup"><span data-stu-id="d2d50-140">(See the full list of supported [`bots`](../../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="d2d50-141">`botId`: ID du bot que vous avez créé lors de la création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="d2d50-141">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="d2d50-142">(Stocké dans `{botId0}` , vous pouvez trouver l’ID réel dans `Development.env` .)</span><span class="sxs-lookup"><span data-stu-id="d2d50-142">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="d2d50-143">`scopes`: Spécifie si votre bot est disponible dans les `personal` `groupchat` `team` contextes, ou (c’est-à-dire, canal).</span><span class="sxs-lookup"><span data-stu-id="d2d50-143">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="d2d50-144">`commands`: Commandes disponibles que les utilisateurs peuvent envoyer à votre robot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-144">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="d2d50-145">`title`: Nom de la commande de bot que les utilisateurs voient dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-145">`title`: A bot command name users see in the Teams client.</span></span>
* <span data-ttu-id="d2d50-146">`description`: Brève description ou exemple de la syntaxe et des arguments pour aider les utilisateurs à comprendre ce que fait la commande bot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-146">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="d2d50-147">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="d2d50-147">App scaffolding</span></span>

<span data-ttu-id="d2d50-148">La génération de modèles automatique d’application fournit un `botActivityHandler.js` fichier, situé dans le répertoire racine de votre projet, pour la gestion de la manière dont votre bot traite les activités dans Teams (par exemple, la façon dont le bot répond à des messages spécifiques, tels que « Hello »).</span><span class="sxs-lookup"><span data-stu-id="d2d50-148">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="d2d50-149">Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="d2d50-149">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="d2d50-150">À des fins de test, nous allons héberger votre robot sur un serveur Web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="d2d50-150">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="d2d50-151">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="d2d50-151">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="d2d50-152">Copiez l’URL HTTPs dans la sortie, car teams nécessite des connexions HTTPs.</span><span class="sxs-lookup"><span data-stu-id="d2d50-152">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="d2d50-153">Dans votre `.publish` répertoire, ouvrez `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="d2d50-153">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="d2d50-154">Remplacez la `baseUrl0` valeur par l’URL copiée.</span><span class="sxs-lookup"><span data-stu-id="d2d50-154">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="d2d50-155">(Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="d2d50-155">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="d2d50-156">Le manifeste de votre application pointe vers l’emplacement où vous hébergez le robot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-156">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="configuring-your-bot"></a><span data-ttu-id="d2d50-157">Configuration de votre robot</span><span class="sxs-lookup"><span data-stu-id="d2d50-157">Configuring your bot</span></span>

<span data-ttu-id="d2d50-158">Pour utiliser un bot dans Teams, vous devez l’enregistrer auprès du service Microsoft Azure bot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="d2d50-159">Heureusement, cette opération est exécutée automatiquement lorsque vous configurez votre application à l’aide de Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d2d50-159">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="d2d50-160">Ajouter l’adresse du point de terminaison du bot</span><span class="sxs-lookup"><span data-stu-id="d2d50-160">Add the bot endpoint address</span></span>

<span data-ttu-id="d2d50-161">Vous devez spécifier une URL de point de terminaison pour recevoir et traiter les messages utilisateur (par exemple, les demandes) envoyées au bot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-161">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="d2d50-162">En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="d2d50-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="d2d50-163">Vous pouvez configurer cet outil rapidement dans Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d2d50-163">You can configure this quickly in the Teams Toolkit.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. <span data-ttu-id="d2d50-165">Accédez à **gestion des robots > inscriptions des robots existants** et sélectionnez le robot que vous avez créé lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="d2d50-165">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="d2d50-166">Dans le champ **adresse du point de terminaison de robot** , entrez le serveur Web local sur lequel vous hébergez le bot et ajoutez-le `/api/messages` à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="d2d50-166">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot and append `/api/messages` to it.</span></span>

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="Illustration illustrant l’emplacement où vous pouvez configurer l’URL du point de terminaison du bot dans Team Toolkit.":::

<span data-ttu-id="d2d50-168">Votre robot pourra répondre aux messages dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-168">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="d2d50-169">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="d2d50-169">Run your app</span></span>

<span data-ttu-id="d2d50-170">Vous avez configuré une URL pour héberger votre robot et le configurer pour qu’il gère les messages.</span><span class="sxs-lookup"><span data-stu-id="d2d50-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="d2d50-171">Il est temps de faire fonctionner votre robot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-171">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="d2d50-172">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="d2d50-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="d2d50-173">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="d2d50-173">Run `npm start`.</span></span>

<span data-ttu-id="d2d50-174">Si elle réussit, un message semblable à celui-ci s’affiche, indiquant que votre robot est à l’écoute de l’activité `localhost` :</span><span class="sxs-lookup"><span data-stu-id="d2d50-174">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a><span data-ttu-id="d2d50-175">Chargement de votre robot dans teams</span><span class="sxs-lookup"><span data-stu-id="d2d50-175">Sideload your bot in Teams</span></span>

<span data-ttu-id="d2d50-176">Une fois que votre robot est en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="d2d50-177">Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="d2d50-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="d2d50-178">Connectez-vous au client teams avec votre compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="d2d50-178">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="d2d50-179">Sélectionnez **applications**, puis **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="d2d50-179">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="d2d50-180">Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="d2d50-180">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="d2d50-181">Dans la fenêtre installation modale, sélectionnez **Ajouter** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="d2d50-181">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-bot"></a><span data-ttu-id="d2d50-182">Tester votre robot</span><span class="sxs-lookup"><span data-stu-id="d2d50-182">Test your bot</span></span>

<span data-ttu-id="d2d50-183">Maintenant pour la partie amusante : disons « Hello » à votre bot dans une conversation en un seul.</span><span class="sxs-lookup"><span data-stu-id="d2d50-183">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. Dans Teams, sélectionnez **autres** :::image type="icon" source="../doc-links/images/teams-client-more.png"::: sur le côté gauche.
1. <span data-ttu-id="d2d50-185">Recherchez et sélectionnez le robot que vous venez de versions test chargées.</span><span class="sxs-lookup"><span data-stu-id="d2d50-185">Locate and select the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="Illustration illustrant l’emplacement où vous accédez à votre bot dans Teams.":::
1. <span data-ttu-id="d2d50-187">Dans la zone de composition, envoyez un `Hello` message.</span><span class="sxs-lookup"><span data-stu-id="d2d50-187">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="d2d50-188">Votre robot répond avec un message semblable à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="d2d50-188">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="Capture d’écran illustrant un utilisateur dire « Hello » à un bot de teams et obtenant une réponse.":::

> [!NOTE]
> <span data-ttu-id="d2d50-190">Si vous effectuez des modifications de code après avoir testé votre bot (par exemple, vous mettez à jour `botActivityHandler.js` ), vous devez réexécuter votre application pour voir ces modifications reflétées dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-190">If you make code changes after testing your bot—for example, you update `botActivityHandler.js`—you must run your app again to see those changes reflected in Teams.</span></span>

## <a name="well-done"></a><span data-ttu-id="d2d50-191">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="d2d50-191">Well done</span></span>

<span data-ttu-id="d2d50-192">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="d2d50-192">Congratulations!</span></span> <span data-ttu-id="d2d50-193">Vous disposez d’un bot de teams de base qui peut communiquer avec des utilisateurs un-sur-un ou des paramètres de groupe (canaux et conversations).</span><span class="sxs-lookup"><span data-stu-id="d2d50-193">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d2d50-194">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d2d50-194">Troubleshooting</span></span>

<span data-ttu-id="d2d50-195">Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d2d50-195">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="d2d50-196">Échec de l’installation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="d2d50-196">Toolkit setup fails</span></span>

<span data-ttu-id="d2d50-197">Lors de la configuration de votre projet d’application avec Team Toolkit, vous obtenez une erreur après avoir sélectionné l’option **créer un nouveau Bot** et vous être connecté avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="d2d50-197">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="d2d50-198">Il peut s’agir d’un problème d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d2d50-198">This could be an authentication issue.</span></span> <span data-ttu-id="d2d50-199">Procédez comme suit pour terminer la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="d2d50-199">Follow these steps to finish setting up your project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis **déconnectez-vous**.
1. <span data-ttu-id="d2d50-201">Recommencez le processus d’installation en vous connectant avec le même compte et en créant un nouveau Bot.</span><span class="sxs-lookup"><span data-stu-id="d2d50-201">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="d2d50-202">Le bot n’est pas connecté à teams</span><span class="sxs-lookup"><span data-stu-id="d2d50-202">Bot isn't connected to Teams</span></span>

<span data-ttu-id="d2d50-203">Si vous avez installé votre application, mais que le bot ne fonctionne pas, vérifiez que le bot est [connecté au *canal*teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d2d50-203">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="d2d50-204">Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d2d50-204">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="d2d50-205">Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d2d50-205">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="d2d50-206">Si vous souhaitez en savoir plus</span><span class="sxs-lookup"><span data-stu-id="d2d50-206">Learn more</span></span>

* [<span data-ttu-id="d2d50-207">Voir les autres robots que les robots peuvent faire avec l’un de nos exemples (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d2d50-207">See what else Teams bots can do with one of our samples (GitHub)</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="d2d50-208">Concepts de base d’une conversation de bot</span><span class="sxs-lookup"><span data-stu-id="d2d50-208">Bot conversation basics</span></span>](../../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="d2d50-209">Authentification de robot dans teams</span><span class="sxs-lookup"><span data-stu-id="d2d50-209">Bot authentication in Teams</span></span>](../../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="d2d50-210">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="d2d50-210">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
