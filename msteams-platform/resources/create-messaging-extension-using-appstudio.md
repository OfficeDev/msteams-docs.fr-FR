---
title: Créer une extension de messagerie à l’aide de App Studio
author: clearab
description: Découvrez comment créer une extension Microsoft Teams messagerie à l’aide d’App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 10de4c6f9e7b81e1edc47622cb5c0c814d2eb3a7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019740"
---
# <a name="create-a-messaging-extension-using-app-studio"></a><span data-ttu-id="e13fc-103">Créer une extension de messagerie à l’aide de App Studio</span><span class="sxs-lookup"><span data-stu-id="e13fc-103">Create a messaging extension using App Studio</span></span>

> [!TIP]
> <span data-ttu-id="e13fc-104">Vous recherchez un moyen plus rapide de commencer ?</span><span class="sxs-lookup"><span data-stu-id="e13fc-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="e13fc-105">Créez [une extension de messagerie à l’aide](../build-your-first-app/build-messaging-extension.md) Microsoft Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="e13fc-105">Create a [messaging extension](../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="e13fc-106">À un niveau élevé, vous devez effectuer les étapes suivantes pour créer une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="e13fc-107">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="e13fc-107">Prepare your development environment</span></span>
2. <span data-ttu-id="e13fc-108">Créer et déployer votre service web (lors du développement, utilisez un service de tunneling tel que ngrok pour l’exécuter localement)</span><span class="sxs-lookup"><span data-stu-id="e13fc-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="e13fc-109">Inscrivez votre service web à l’aide de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e13fc-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="e13fc-110">Créer votre package d’application</span><span class="sxs-lookup"><span data-stu-id="e13fc-110">Create your app package</span></span>
5. <span data-ttu-id="e13fc-111">Télécharger votre package dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e13fc-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="e13fc-112">La création de votre service web, la création de votre package d’application et l’inscription de votre service web avec Bot Framework peuvent être réalisées dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="e13fc-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="e13fc-113">Étant donné que ces trois éléments sont si dispersés, quel que soit l’ordre dans lequel vous les faites, vous devrez revenir pour mettre à jour les autres.</span><span class="sxs-lookup"><span data-stu-id="e13fc-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="e13fc-114">Votre inscription nécessite le point de terminaison de messagerie de votre service web déployé, et votre service web a besoin de l’ID et du mot de passe créés à partir de votre inscription.</span><span class="sxs-lookup"><span data-stu-id="e13fc-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="e13fc-115">Votre manifeste d’application a également besoin de cet ID pour se connecter Teams à votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="e13fc-116">Lorsque vous construisez votre extension de messagerie, vous allez régulièrement passer de la modification du manifeste de votre application au déploiement de code dans votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="e13fc-117">Lorsque vous travaillez avec le manifeste de l’application, n’oubliez pas que vous pouvez manipuler manuellement le fichier JSON ou apporter des modifications via App Studio.</span><span class="sxs-lookup"><span data-stu-id="e13fc-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="e13fc-118">Dans les deux cas, vous devez re-déployer (télécharger) votre application dans Teams lorsque vous modifiez le manifeste, mais vous n’avez pas besoin de le faire lorsque vous déployez les modifications apportées à votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="e13fc-119">Créez votre service web</span><span class="sxs-lookup"><span data-stu-id="e13fc-119">Create your web service</span></span>

<span data-ttu-id="e13fc-120">Le cœur de votre extension de messagerie est votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="e13fc-121">Il définit un itinéraire unique, `/api/messages` généralement, pour recevoir toutes les demandes.</span><span class="sxs-lookup"><span data-stu-id="e13fc-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="e13fc-122">Si vous débutez à partir de zéro, vous avez le choix entre plusieurs options.</span><span class="sxs-lookup"><span data-stu-id="e13fc-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="e13fc-123">Utilisez l’un de nos [didacticiels](#learn-more) de démarrage rapide qui vous guidera tout au long de la création de votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="e13fc-124">Choisissez l’un des exemples d’extension de messagerie disponibles dans le référentiel d’exemples [Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) à partir de.</span><span class="sxs-lookup"><span data-stu-id="e13fc-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="e13fc-125">Si vous utilisez JavaScript, utilisez le générateur [Yeoman](https://github.com/OfficeDev/generator-teams) pour Microsoft Teams pour échafauder votre application Teams, y compris votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="e13fc-126">Créez votre service web de toutes pièces.</span><span class="sxs-lookup"><span data-stu-id="e13fc-126">Create your web service from scratch.</span></span> <span data-ttu-id="e13fc-127">Vous pouvez choisir d’ajouter le kit de développement logiciel (SDK) Bot Framework pour votre langue. Vous pouvez également travailler directement avec les charges utiles JSON.</span><span class="sxs-lookup"><span data-stu-id="e13fc-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="e13fc-128">Inscrivez votre service web à l’aide de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="e13fc-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="e13fc-129">Les extensions de messagerie tirez parti du schéma de messagerie et du protocole de communication sécurisé de Bot Framework. Si vous n’en avez pas déjà, vous devrez inscrire votre service web sur Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e13fc-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="e13fc-130">ID de l’application Microsoft (nous l’appellerons ID de bot à partir de l’intérieur de Teams, pour l’identifier à partir d’autres ID d’application que vous pourriez utiliser) et le point de terminaison de messagerie de votre inscription avec Bot Framework sera utilisé dans votre extension de messagerie pour recevoir et répondre aux demandes.</span><span class="sxs-lookup"><span data-stu-id="e13fc-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="e13fc-131">Si vous utilisez une inscription existante, veillez à activer le [canal Microsoft Teams.](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e13fc-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="e13fc-132">Si vous suivez l’un des démarrages rapides ou démarrez à partir de l’un des exemples disponibles, vous serez guidé tout au long de l’inscription de votre service web.</span><span class="sxs-lookup"><span data-stu-id="e13fc-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="e13fc-133">Si vous souhaitez inscrire manuellement votre service, trois options s’offrent à vous.</span><span class="sxs-lookup"><span data-stu-id="e13fc-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="e13fc-134">Si vous choisissez de vous inscrire sans utiliser d’abonnement Azure, vous ne pourrez pas tirer parti du flux d’authentification OAuth simplifié fourni par Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e13fc-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="e13fc-135">Vous pourrez migrer votre inscription vers Azure après sa création.</span><span class="sxs-lookup"><span data-stu-id="e13fc-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="e13fc-136">Si vous avez un abonnement Azure (ou que vous souhaitez en créer un), vous pouvez inscrire votre service web manuellement à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e13fc-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="e13fc-137">Créez une ressource « Inscription des canaux bots ».</span><span class="sxs-lookup"><span data-stu-id="e13fc-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="e13fc-138">Vous pouvez choisir le niveau de tarification gratuit, car les messages provenant de Microsoft Teams ne sont pas comptabilisés dans le nombre total de messages par mois.</span><span class="sxs-lookup"><span data-stu-id="e13fc-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="e13fc-139">Si vous ne souhaitez pas utiliser un abonnement Azure, vous pouvez utiliser le [portail d’inscription hérité.](https://dev.botframework.com/bots/new)</span><span class="sxs-lookup"><span data-stu-id="e13fc-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="e13fc-140">App Studio peut également vous aider à inscrire votre service web (bot).</span><span class="sxs-lookup"><span data-stu-id="e13fc-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="e13fc-141">Les services Web enregistrés via App Studio ne sont pas enregistrés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e13fc-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="e13fc-142">Vous pouvez utiliser le [portail hérité pour](https://dev.botframework.com/bots) afficher, gérer et migrer vos inscriptions.</span><span class="sxs-lookup"><span data-stu-id="e13fc-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="e13fc-143">Créer le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="e13fc-143">Create your app manifest</span></span>

<span data-ttu-id="e13fc-144">Vous pouvez utiliser App Studio pour créer votre manifeste d’application ou le créer manuellement.</span><span class="sxs-lookup"><span data-stu-id="e13fc-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="e13fc-145">Créer le manifeste de votre application à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="e13fc-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="e13fc-146">Vous pouvez utiliser l’application App Studio à partir du client Microsoft Teams pour vous aider à créer votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="e13fc-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="e13fc-147">Dans le client Teams, ouvrez App Studio à partir du menu **...** dépassement sur le rail de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="e13fc-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="e13fc-148">S’il n’est pas déjà installé, vous pouvez le faire en le recherchant.</span><span class="sxs-lookup"><span data-stu-id="e13fc-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="e13fc-149">Sous **l’onglet Éditeur** de manifeste, sélectionnez Créer une application **(ou** si vous ajoutez une extension de messagerie à une application existante, vous pouvez importer votre package d’application)</span><span class="sxs-lookup"><span data-stu-id="e13fc-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="e13fc-150">Ajoutez les détails de votre application (consultez [définition de schéma de manifeste](~/resources/schema/manifest-schema.md) pour obtenir une description complète de chaque champ).</span><span class="sxs-lookup"><span data-stu-id="e13fc-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="e13fc-151">Sous **l’onglet Extensions de messagerie,** cliquez sur le **bouton Installation.**</span><span class="sxs-lookup"><span data-stu-id="e13fc-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="e13fc-152">Vous pouvez créer un nouveau service web (bot) pour votre extension de messagerie à utiliser, ou si vous en avez déjà inscrit un, sélectionnez/ajoutez-le ici.</span><span class="sxs-lookup"><span data-stu-id="e13fc-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="e13fc-153">Si nécessaire, mettez à jour votre adresse de point de terminaison de bot pour qu’elle pointe vers votre bot.</span><span class="sxs-lookup"><span data-stu-id="e13fc-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="e13fc-154">Celle-ci doit avoir la forme `https://someplace.com/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="e13fc-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="e13fc-155">Le **bouton** Ajouter dans la section **Commande** vous guide tout au long de l’ajout de commandes à votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="e13fc-156">Pour plus [d’informations](#learn-more) sur l’ajout de commandes, voir la section En savoir plus.</span><span class="sxs-lookup"><span data-stu-id="e13fc-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="e13fc-157">N’oubliez pas que vous pouvez définir jusqu’à 10 commandes pour votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="e13fc-158">La **section Gérer les messages** vous permet d’ajouter un domaine sur le déclenchement de votre messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="e13fc-159">Pour plus [d’informations, voir](~/messaging-extensions/how-to/link-unfurling.md) déploiement de lien.</span><span class="sxs-lookup"><span data-stu-id="e13fc-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="e13fc-160">À partir de **l’onglet Terminer =** > tester et distribuer, vous pouvez télécharger votre package d’application (qui inclut votre manifeste d’application ainsi que les icônes de votre application) ou installer **le** package.</span><span class="sxs-lookup"><span data-stu-id="e13fc-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="e13fc-161">Créer manuellement le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="e13fc-161">Create your app manifest manually</span></span>

<span data-ttu-id="e13fc-162">Comme avec les bots et [](~/resources/schema/manifest-schema.md#composeextensions) les onglets, vous mettez à jour le manifeste de votre application pour inclure les propriétés d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="e13fc-163">Ces propriétés régissent l’apparition et le comportement de votre extension de messagerie dans le client Microsoft Teams messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="e13fc-164">Les extensions de messagerie sont pris en charge à partir de la v1.0 du manifeste.</span><span class="sxs-lookup"><span data-stu-id="e13fc-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="e13fc-165">Déclarer votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="e13fc-165">Declare your messaging extension</span></span>

<span data-ttu-id="e13fc-166">Pour ajouter une extension de messagerie, incluez une nouvelle structure JSON de niveau supérieur dans le manifeste de votre application avec la `composeExtensions` propriété.</span><span class="sxs-lookup"><span data-stu-id="e13fc-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="e13fc-167">Vous créez une extension de messagerie unique pour votre application, avec jusqu’à 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="e13fc-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="e13fc-168">Le manifeste fait référence aux extensions de messagerie comme `composeExtensions` .</span><span class="sxs-lookup"><span data-stu-id="e13fc-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="e13fc-169">Il s’agit de maintenir la compatibilité ascendante.</span><span class="sxs-lookup"><span data-stu-id="e13fc-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="e13fc-170">La définition d’extension est un objet qui a la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="e13fc-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="e13fc-171">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="e13fc-171">Property name</span></span> | <span data-ttu-id="e13fc-172">Objectif</span><span class="sxs-lookup"><span data-stu-id="e13fc-172">Purpose</span></span> | <span data-ttu-id="e13fc-173">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="e13fc-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="e13fc-174">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e13fc-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="e13fc-175">Il doit généralement être identique à l’ID de votre application Teams globale.</span><span class="sxs-lookup"><span data-stu-id="e13fc-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="e13fc-176">Oui</span><span class="sxs-lookup"><span data-stu-id="e13fc-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="e13fc-177">Active **Paramètres’élément** de menu.</span><span class="sxs-lookup"><span data-stu-id="e13fc-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="e13fc-178">Non</span><span class="sxs-lookup"><span data-stu-id="e13fc-178">No</span></span> |
| `commands` | <span data-ttu-id="e13fc-179">Tableau de commandes pris en charge par cette extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="e13fc-180">Vous êtes limité à 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="e13fc-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="e13fc-181">Oui</span><span class="sxs-lookup"><span data-stu-id="e13fc-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="e13fc-182">Définir vos commandes</span><span class="sxs-lookup"><span data-stu-id="e13fc-182">Define your commands</span></span>

<span data-ttu-id="e13fc-183">Votre extension de messagerie doit déclarer une ou plusieurs commandes, qui définissent l’endroit où vos utilisateurs peuvent déclencher votre extension de messagerie, ainsi que le type d’interaction.</span><span class="sxs-lookup"><span data-stu-id="e13fc-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="e13fc-184">Pour [plus d’informations](#learn-more) sur les commandes d’extension de messagerie, voir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e13fc-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="e13fc-185">Exemple de manifeste simple</span><span class="sxs-lookup"><span data-stu-id="e13fc-185">Simple manifest example</span></span>

<span data-ttu-id="e13fc-186">L’exemple suivant est un objet d’extension de messagerie simple dans le manifeste de l’application avec une commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="e13fc-186">The following example is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="e13fc-187">Il ne s’agit pas de la totalité du fichier manifeste de l’application, uniquement de la partie spécifique aux extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e13fc-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="e13fc-188">Pour obtenir un exemple [complet, voir](~/resources/schema/manifest-schema.md) schéma de manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="e13fc-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="e13fc-189">Exemple de manifeste d’application complet</span><span class="sxs-lookup"><span data-stu-id="e13fc-189">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="e13fc-190">Ajouter vos handlers de messages d’appel</span><span class="sxs-lookup"><span data-stu-id="e13fc-190">Add your invoke message handlers</span></span>

<span data-ttu-id="e13fc-191">Lorsque vos utilisateurs déclenchent votre extension de messagerie, vous devez gérer le message d’appel initial, collecter des informations auprès de l’utilisateur, puis traiter ces informations et répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="e13fc-191">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="e13fc-192">Pour ce faire, vous devez d’abord décider du type de commande que vous souhaitez ajouter à votre extension de messagerie, puis ajouter une [commande d’action](~/messaging-extensions/how-to/action-commands/define-action-command.md) ou ajouter une commande [de recherche.](~/messaging-extensions/how-to/search-commands/define-search-command.md)</span><span class="sxs-lookup"><span data-stu-id="e13fc-192">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="e13fc-193">Extensions de messagerie dans Teams réunions</span><span class="sxs-lookup"><span data-stu-id="e13fc-193">Messaging extensions in Teams meetings</span></span>

> [!NOTE]
> <span data-ttu-id="e13fc-194">Si une réunion ou une conversation de groupe a des utilisateurs fédérés dans la liste, Teams l’accès aux extensions de messagerie pour tous les utilisateurs, y compris l’organisateur.</span><span class="sxs-lookup"><span data-stu-id="e13fc-194">If a meeting or group chat has federated users in the roster, Teams suppresses access to messaging extensions for all users, including the organizer.</span></span>

<span data-ttu-id="e13fc-195">Une fois la réunion commencée, Teams participants peuvent interagir directement avec votre extension de messagerie pendant un appel en direct.</span><span class="sxs-lookup"><span data-stu-id="e13fc-195">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="e13fc-196">Prenons les considérations suivantes lors de la création de votre extension de messagerie en réunion :</span><span class="sxs-lookup"><span data-stu-id="e13fc-196">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="e13fc-197">**Emplacement :**</span><span class="sxs-lookup"><span data-stu-id="e13fc-197">**Location**.</span></span> <span data-ttu-id="e13fc-198">Votre extension de messagerie peut être invoquée à partir de la zone de composition d’un message, de la zone de commande ou @mentioned la conversation de réunion.</span><span class="sxs-lookup"><span data-stu-id="e13fc-198">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="e13fc-199">**Métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="e13fc-199">**Metadata**.</span></span> <span data-ttu-id="e13fc-200">Lorsque votre extension de messagerie est invoquée, elle peut identifier l’utilisateur et le client à partir `userId` de et `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="e13fc-200">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="e13fc-201">`meetingId` fait partie de l’objet `channelData`.</span><span class="sxs-lookup"><span data-stu-id="e13fc-201">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="e13fc-202">Votre application peut utiliser la demande `userId` d’API et pour récupérer les `meetingId` `GetParticipant` rôles d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e13fc-202">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="e13fc-203">**Type de commande**.</span><span class="sxs-lookup"><span data-stu-id="e13fc-203">**Command type**.</span></span> <span data-ttu-id="e13fc-204">Si votre extension de message utilise des commandes basées sur [l’action,](../messaging-extensions/what-are-messaging-extensions.md#action-commands)elle doit suivre l’authentification par [authentification](../tabs/how-to/authentication/auth-aad-sso.md) unique des onglets.</span><span class="sxs-lookup"><span data-stu-id="e13fc-204">If your message extension uses [action-based commands](../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="e13fc-205">**Expérience utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="e13fc-205">**User experience**.</span></span> <span data-ttu-id="e13fc-206">L’extension de messagerie doit se comporter de la même manière qu’en dehors d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="e13fc-206">You messaging extension should look and behave the same as it would outside a meeting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e13fc-207">Prochaines étapes</span><span class="sxs-lookup"><span data-stu-id="e13fc-207">Next steps</span></span>

* [<span data-ttu-id="e13fc-208">Créer des commandes d'action</span><span class="sxs-lookup"><span data-stu-id="e13fc-208">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="e13fc-209">Créer les commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="e13fc-209">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="e13fc-210">Déploiement de lien</span><span class="sxs-lookup"><span data-stu-id="e13fc-210">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="e13fc-211">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="e13fc-211">Learn more</span></span>

<span data-ttu-id="e13fc-212">Essayez-le dans un démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="e13fc-212">Try it out in a quickstart:</span></span>

* <span data-ttu-id="e13fc-213">Démarrages rapides pour C #</span><span class="sxs-lookup"><span data-stu-id="e13fc-213">Quickstarts for C#</span></span>
  * [<span data-ttu-id="e13fc-214">Extension de messagerie avec commandes basées sur l’action</span><span class="sxs-lookup"><span data-stu-id="e13fc-214">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="e13fc-215">Extension de messagerie avec commandes basées sur la recherche</span><span class="sxs-lookup"><span data-stu-id="e13fc-215">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="e13fc-216">Démarrages rapides pour JavaScript</span><span class="sxs-lookup"><span data-stu-id="e13fc-216">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="e13fc-217">Extension de messagerie avec commandes basées sur l’action</span><span class="sxs-lookup"><span data-stu-id="e13fc-217">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="e13fc-218">Extension de messagerie avec commandes basées sur la recherche</span><span class="sxs-lookup"><span data-stu-id="e13fc-218">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="e13fc-219">En savoir plus sur Teams concepts de développement :</span><span class="sxs-lookup"><span data-stu-id="e13fc-219">Learn more about Teams development concepts:</span></span>

* [<span data-ttu-id="e13fc-220">Comprendre Teams fonctionnalités de l’application</span><span class="sxs-lookup"><span data-stu-id="e13fc-220">Understand Teams app capabilities</span></span>](../concepts/capabilities-overview.md)
* [<span data-ttu-id="e13fc-221">Que sont les extensions de messagerie ?</span><span class="sxs-lookup"><span data-stu-id="e13fc-221">What are messaging extensions?</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
