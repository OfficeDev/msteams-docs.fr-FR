---
title: Créer une extension de messagerie teams
author: heath-hamilton
description: Découvrez comment créer une extension de messagerie pour votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: 0475fcea7d865849fa60c5b3b23788bf90ee5e25
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210130"
---
# <a name="build-a-teams-messaging-extension"></a><span data-ttu-id="4ae77-103">Créer une extension de messagerie teams</span><span class="sxs-lookup"><span data-stu-id="4ae77-103">Build a Teams messaging extension</span></span>

<span data-ttu-id="4ae77-104">Il existe deux types d' *extensions de messagerie*teams : [commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) et commandes d' [action](../messaging-extensions/how-to/action-commands/define-action-command.md).</span><span class="sxs-lookup"><span data-stu-id="4ae77-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="4ae77-105">Dans cette leçon, vous allez créer une *commande de recherche* (également appelée *extension de messagerie basée sur la recherche*), qui est un raccourci permettant de trouver du contenu externe et de le partager dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="4ae77-106">Les utilisateurs peuvent accéder aux commandes de recherche à partir de la [zone de composition ou de commande teams](../messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="4ae77-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="4ae77-107">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="4ae77-107">Your assignment</span></span>

<span data-ttu-id="4ae77-108">Le service d’assistance de votre organisation communique avec les utilisateurs par le biais de teams, mais les tickets se trouvent dans un système distinct.</span><span class="sxs-lookup"><span data-stu-id="4ae77-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="4ae77-109">Cela signifie que le personnel de support technique doit constamment basculer entre les applications.</span><span class="sxs-lookup"><span data-stu-id="4ae77-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="4ae77-110">Vous allez examiner la manière dont vous pouvez réduire ce pourcentage de changement de contexte en créant une simple extension de messagerie basée sur la recherche pour Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="4ae77-111">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="4ae77-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="4ae77-112">Créer un projet d’application et un bot d’extension de messagerie à l’aide de Microsoft teams Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="4ae77-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="4ae77-113">Identifier les propriétés du manifeste de l’application et une partie de la structure relative aux extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4ae77-113">Identify the app manifest properties and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="4ae77-114">Héberger une application localement</span><span class="sxs-lookup"><span data-stu-id="4ae77-114">Host an app locally</span></span>
> * <span data-ttu-id="4ae77-115">Configurer le bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="4ae77-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="4ae77-116">Chargement et test d’une extension de messagerie dans teams</span><span class="sxs-lookup"><span data-stu-id="4ae77-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ae77-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4ae77-117">Before you begin</span></span>

<span data-ttu-id="4ae77-118">Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="4ae77-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="4ae77-119">Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="4ae77-119">Create your app project</span></span>

<span data-ttu-id="4ae77-120">Microsoft teams Toolkit vous permet de configurer les composants suivants pour votre extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="4ae77-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="4ae77-121">**Manifeste de l’application et génération** d’une structure correspondant aux extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="4ae77-121">**App manifest and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="4ae77-122">**Robot** de votre extension de messagerie enregistré automatiquement avec le service Microsoft Azure bot</span><span class="sxs-lookup"><span data-stu-id="4ae77-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="4ae77-123">Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.</span><span class="sxs-lookup"><span data-stu-id="4ae77-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="4ae77-125">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="4ae77-126">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="4ae77-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="4ae77-127">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez extension de **messagerie** , puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="4ae77-127">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="4ae77-128">Dans l’écran **configurer l’extension de messagerie** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4ae77-128">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="4ae77-129">Choisissez uniquement l’option **basée sur la recherche** pour le type d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-129">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="4ae77-130">Sélectionnez **créer un nouveau robot** et **Connectez** -vous pour vous connecter à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="4ae77-130">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span>
    1. <span data-ttu-id="4ae77-131">Stockez votre ID de robot et votre mot de passe (vous en aurez besoin plus tard).</span><span class="sxs-lookup"><span data-stu-id="4ae77-131">Store your bot ID and password (you need this a little later).</span></span>
    1. <span data-ttu-id="4ae77-132">Module Entrez un nom personnalisé pour votre bot et sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="4ae77-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="4ae77-133">(Il ne s’agit pas du nom de l’application teams que vous avez déjà spécifiée.)</span><span class="sxs-lookup"><span data-stu-id="4ae77-133">(This is not the name of the Teams app you already specified.)</span></span>
    1. <span data-ttu-id="4ae77-134">Pour le moment, sélectionnez **non** pour l’option lien unfurling.</span><span class="sxs-lookup"><span data-stu-id="4ae77-134">For now, select **No** for the link unfurling option.</span></span></br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Illustration illustrant comment, dans Team Toolkit, connectez-vous à votre compte Microsoft 365 afin de créer un nouveau bot pour votre extension de messagerie.":::
1. <span data-ttu-id="4ae77-136">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="4ae77-136">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="4ae77-137">Identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="4ae77-137">Identify relevant app project components</span></span>

<span data-ttu-id="4ae77-138">La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-138">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="4ae77-139">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="4ae77-139">App manifest</span></span>

<span data-ttu-id="4ae77-140">L’extrait de code suivant du manifeste de l’application ( `manifest.json` fichier dans le répertoire de votre projet `.publish` ) affiche les propriétés et les valeurs par défaut relatives aux extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-140">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to messaging extensions.</span></span>

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="4ae77-141">Nous allons comprendre quelques-unes des propriétés que le kit de outils a créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="4ae77-141">Let's understand some of the properties the toolkit created for you.</span></span> <span data-ttu-id="4ae77-142">(Consultez la liste complète des propriétés prises en charge [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) .)</span><span class="sxs-lookup"><span data-stu-id="4ae77-142">(See the full list of supported [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) properties.)</span></span>

* <span data-ttu-id="4ae77-143">`botId`: ID du bot que vous avez créé lors de la création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="4ae77-143">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="4ae77-144">(Stocké dans `{botId0}` , vous pouvez trouver l’ID réel dans `Development.env` .)</span><span class="sxs-lookup"><span data-stu-id="4ae77-144">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="4ae77-145">`commands`: Commandes disponibles pour l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-145">`commands`: Available commands for the messaging extension.</span></span> <span data-ttu-id="4ae77-146">Le kit de outils vous a fourni une génération de modèles pour une commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="4ae77-146">The toolkit provided you scaffolding for a search command.</span></span>
* <span data-ttu-id="4ae77-147">`context`: Où les utilisateurs peuvent appeler l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-147">`context`: Where users can invoke the messaging extension.</span></span> <span data-ttu-id="4ae77-148">Dans ce cas, vous pouvez lancer l’extension de messagerie à partir de la zone de commande ou de composition de teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-148">In this case, you can launch the messaging extension from the Teams compose or command box.</span></span>
* <span data-ttu-id="4ae77-149">`description`: Texte d’aide de l’interface utilisateur indiquant ce que fait la commande ou comment l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="4ae77-149">`description`: UI help text indicating what the command does or how to use it.</span></span>
* <span data-ttu-id="4ae77-150">`parameters`: Inclut tous les paramètres acceptés par une commande (vous devez en avoir au moins un et peut avoir jusqu’à cinq).</span><span class="sxs-lookup"><span data-stu-id="4ae77-150">`parameters`: Includes all parameters a command accepts (you must have at least one and can have up to five).</span></span>
* <span data-ttu-id="4ae77-151">`parameters.description`: Texte d’aide de l’interface utilisateur décrivant l’objectif ou l’exemple d’entrée du paramètre.</span><span class="sxs-lookup"><span data-stu-id="4ae77-151">`parameters.description`: UI help text describing the parameter's purpose or example input.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="4ae77-152">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="4ae77-152">App scaffolding</span></span>

<span data-ttu-id="4ae77-153">Le échafaudage de l’application inclut un `.env` fichier, situé dans le répertoire racine de votre projet, qui stocke l’ID et le mot de passe du bot de votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-153">The app scaffolding includes a `.env` file, located in the root directory of your project, which stores the ID and password of your messaging extension's bot.</span></span>

<span data-ttu-id="4ae77-154">Dans le répertoire racine, il existe un `botActivityHandler.js` fichier permettant de gérer la manière dont votre extension de messagerie (ou techniquement, le [bot de l’extension de messagerie](#configuring-the-bot-for-your-messaging-extension)) répond aux requêtes de recherche dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-154">Also in the root directory, there's a `botActivityHandler.js` file for handling how your messaging extension (or technically, the [messaging extension's bot](#configuring-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="4ae77-155">Configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="4ae77-155">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="4ae77-156">À des fins de test, nous allons héberger votre extension de messagerie sur un serveur Web local (port 3978).</span><span class="sxs-lookup"><span data-stu-id="4ae77-156">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="4ae77-157">Dans un terminal, exécutez `ngrok http -host-header=rewrite 3978` .</span><span class="sxs-lookup"><span data-stu-id="4ae77-157">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="4ae77-158">Copiez l’URL HTTPs dans la sortie, car teams nécessite des connexions HTTPs.</span><span class="sxs-lookup"><span data-stu-id="4ae77-158">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="4ae77-159">Dans votre `.publish` répertoire, ouvrez `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="4ae77-159">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="4ae77-160">Remplacez la `baseUrl0` valeur par l’URL copiée.</span><span class="sxs-lookup"><span data-stu-id="4ae77-160">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="4ae77-161">(Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="4ae77-161">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="4ae77-162">Votre manifeste d’application pointe vers l’emplacement où vous hébergez le bot utilisé par l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-162">Your app manifest is pointing to where you're hosting the bot used by the messaging extension.</span></span>

## <a name="configuring-the-bot-for-your-messaging-extension"></a><span data-ttu-id="4ae77-163">Configuration du bot pour votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="4ae77-163">Configuring the bot for your messaging extension</span></span>

<span data-ttu-id="4ae77-164">Les extensions de messagerie s’appuient sur les robots pour envoyer et traiter les demandes des utilisateurs de teams vers votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="4ae77-164">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span>

<span data-ttu-id="4ae77-165">Le bot doit être enregistré avec le service Azure bot, qui a été créé lors de la configuration de votre application à l’aide du kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-165">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="4ae77-166">Spécifier l’ID et le mot de passe de votre robot</span><span class="sxs-lookup"><span data-stu-id="4ae77-166">Specify your bot ID and password</span></span>

<span data-ttu-id="4ae77-167">Lorsque votre bot est enregistré avec le service Azure bot, il reçoit un ID et un mot de passe sur lesquels votre application teams doit être informée.</span><span class="sxs-lookup"><span data-stu-id="4ae77-167">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="4ae77-168">Localisez l’ID et le mot de passe du robot stocké lors de l’installation de la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="4ae77-168">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="4ae77-169">Dans le répertoire racine, ouvrez le `.env` fichier.</span><span class="sxs-lookup"><span data-stu-id="4ae77-169">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="4ae77-170">Définissez l’ID et le mot de passe de votre robot sur les `BotId` `BotPassword` Propriétés et, respectivement.</span><span class="sxs-lookup"><span data-stu-id="4ae77-170">Set your bot ID and password to the `BotId` and `BotPassword` properties, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="4ae77-171">Ajouter l’adresse du point de terminaison du bot</span><span class="sxs-lookup"><span data-stu-id="4ae77-171">Add the bot endpoint address</span></span>

<span data-ttu-id="4ae77-172">Vous devez spécifier une URL de point de terminaison bot pour recevoir et traiter des requêtes de recherche dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-172">You must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="4ae77-173">En règle générale, l’URL se présente comme suit `https://HOST_URL/api/messages` :</span><span class="sxs-lookup"><span data-stu-id="4ae77-173">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="4ae77-174">Vous pouvez configurer cet outil rapidement dans Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="4ae77-174">You can configure this quickly in the Teams Toolkit.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis choisissez **Ouvrir Microsoft teams Toolkit**.
1. <span data-ttu-id="4ae77-176">Accédez à **gestion des robots > inscriptions des robots existants** et sélectionnez le robot que vous avez créé lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="4ae77-176">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="4ae77-177">Dans le champ **adresse du point de terminaison de robot** , entrez le serveur Web local où vous hébergez le bot ( `baseUrl10` valeur) et ajoutez `/api/messages` -y.</span><span class="sxs-lookup"><span data-stu-id="4ae77-177">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

<span data-ttu-id="4ae77-178">Votre robot pourra gérer les requêtes dans votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4ae77-178">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="4ae77-179">Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="4ae77-179">Run your app</span></span>

<span data-ttu-id="4ae77-180">Vous avez configuré une URL pour héberger votre extension de messagerie et la configurer pour qu’elle gère les recherches.</span><span class="sxs-lookup"><span data-stu-id="4ae77-180">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="4ae77-181">Il est temps de faire fonctionner votre application.</span><span class="sxs-lookup"><span data-stu-id="4ae77-181">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="4ae77-182">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="4ae77-182">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="4ae77-183">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="4ae77-183">Run `npm start`.</span></span>

<span data-ttu-id="4ae77-184">Si elle réussit, un message semblable au suivant s’affiche, indiquant que votre service d’extension de messagerie est à l’écoute de l’activité `localhost` :</span><span class="sxs-lookup"><span data-stu-id="4ae77-184">If successful, you see something like the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="4ae77-185">Chargement de votre extension de messagerie dans teams</span><span class="sxs-lookup"><span data-stu-id="4ae77-185">Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="4ae77-186">Une fois que votre extension de messagerie est en cours d’exécution, vous pouvez l’installer dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-186">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="4ae77-187">Si vous n’avez pas versions test chargées une application teams avant et rencontrez des problèmes, suivez ces [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span><span class="sxs-lookup"><span data-stu-id="4ae77-187">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="4ae77-188">Connectez-vous au client teams avec votre compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="4ae77-188">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="4ae77-189">Sélectionnez **applications**, puis **Télécharger une application personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="4ae77-189">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="4ae77-190">Accédez à votre dossier de projet d’application `.publish` et sélectionnez `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="4ae77-190">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="4ae77-191">Dans la fenêtre installation modale, sélectionnez **Ajouter** pour installer votre application.</span><span class="sxs-lookup"><span data-stu-id="4ae77-191">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-messaging-extension"></a><span data-ttu-id="4ae77-192">Tester votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="4ae77-192">Test your messaging extension</span></span>

<span data-ttu-id="4ae77-193">Découvrez comment fonctionnent les extensions de messagerie dans une conversation Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-193">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="4ae77-194">Démarrez une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="4ae77-194">Start a new chat.</span></span> Dans la zone de composition, sélectionnez **plus** , :::image type="icon" source="../assets/icons/teams-client-more.png"::: puis choisissez l’application de l’extension de messagerie que vous venez de versions test chargées.<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Illustration illustrant comment accéder à une extension de messagerie basée sur la recherche dans la zone de composition de teams.":::
1. <span data-ttu-id="4ae77-197">Essayez de rechercher un article (par exemple, « tickets »).</span><span class="sxs-lookup"><span data-stu-id="4ae77-197">Try searching for something (for example, "Tickets").</span></span> <span data-ttu-id="4ae77-198">Si votre application fonctionne, vous verrez des exemples de résultats de recherche (vous pouvez ajouter votre propre version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="4ae77-198">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Capture d’écran illustrant l’utilisation d’une extension de messagerie basée sur la recherche dans la zone de composition de teams.":::

## <a name="well-done"></a><span data-ttu-id="4ae77-200">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="4ae77-200">Well done</span></span>

<span data-ttu-id="4ae77-201">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="4ae77-201">Congratulations!</span></span> <span data-ttu-id="4ae77-202">Vous disposez d’une extension de messagerie teams de base qui est configurée pour rechercher du contenu externe dans la zone de composition ou de commande.</span><span class="sxs-lookup"><span data-stu-id="4ae77-202">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae77-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ae77-203">Next steps</span></span>

<span data-ttu-id="4ae77-204">Consultez les pages suivantes pour continuer et créer une extension de messagerie complète :</span><span class="sxs-lookup"><span data-stu-id="4ae77-204">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="4ae77-205">[Définir des commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) pertinentes pour votre service.</span><span class="sxs-lookup"><span data-stu-id="4ae77-205">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="4ae77-206">Configurez votre service pour [répondre aux recherches des utilisateurs](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="4ae77-206">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4ae77-207">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="4ae77-207">Troubleshooting</span></span>

<span data-ttu-id="4ae77-208">Les informations suivantes peuvent vous être utiles si vous avez rencontré des problèmes lors de l’exécution de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4ae77-208">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="4ae77-209">Échec de l’installation de la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="4ae77-209">Toolkit setup fails</span></span>

<span data-ttu-id="4ae77-210">Lors de la configuration de votre projet d’application avec Team Toolkit, vous obtenez une erreur après avoir sélectionné l’option **créer un nouveau Bot** et vous être connecté avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="4ae77-210">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="4ae77-211">Il peut s’agir d’un problème d’authentification.</span><span class="sxs-lookup"><span data-stu-id="4ae77-211">This could be an authentication issue.</span></span> <span data-ttu-id="4ae77-212">Procédez comme suit pour terminer la configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="4ae77-212">Follow these steps to finish setting up your project.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche, puis **déconnectez-vous**.
1. <span data-ttu-id="4ae77-214">Recommencez le processus d’installation en vous connectant avec le même compte et en créant un nouveau Bot.</span><span class="sxs-lookup"><span data-stu-id="4ae77-214">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="4ae77-215">Le bot n’est pas connecté à teams</span><span class="sxs-lookup"><span data-stu-id="4ae77-215">Bot isn't connected to Teams</span></span>

<span data-ttu-id="4ae77-216">Si vous avez installé votre application, mais qu’elle ne fonctionne pas, vérifiez que le robot de l’extension de messagerie est [connecté au *canal*teams du service Azure bot](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="4ae77-216">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="4ae77-217">Il est important de comprendre qu’il ne s’agit pas d’un canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4ae77-217">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="4ae77-218">Dans ce cas, un canal indique comment le service Azure bot connecte votre robot à teams ou une autre [application de communication Microsoft ou tierce prise en charge](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="4ae77-218">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="4ae77-219">Si vous souhaitez en savoir plus</span><span class="sxs-lookup"><span data-stu-id="4ae77-219">Learn more</span></span>

* [<span data-ttu-id="4ae77-220">Inclure une fonctionnalité de unfurling de liens</span><span class="sxs-lookup"><span data-stu-id="4ae77-220">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="4ae77-221">Ajouter une authentification</span><span class="sxs-lookup"><span data-stu-id="4ae77-221">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="4ae77-222">Créer une extension de messagerie basée sur une action</span><span class="sxs-lookup"><span data-stu-id="4ae77-222">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="4ae77-223">Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="4ae77-223">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
