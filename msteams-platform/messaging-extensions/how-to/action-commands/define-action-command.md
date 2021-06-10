---
title: Définir des commandes d’action d’extension de messagerie
author: clearab
description: Vue d’ensemble des commandes d’action d’extension de messagerie
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f49e821ecb98659b4cfd68f93b37f1a8f611a9fb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020715"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="81503-103">Définir des commandes d’action d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="81503-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="81503-104">Les commandes d’action vous permettent de présenter à vos utilisateurs une fenêtre popup modale appelée module de tâche dans Teams.</span><span class="sxs-lookup"><span data-stu-id="81503-104">Action commands allow you to present your users with a modal popup called a task module in Teams.</span></span> <span data-ttu-id="81503-105">Le module de tâche collecte ou affiche des informations, traite l’interaction et renvoie les informations à Teams.</span><span class="sxs-lookup"><span data-stu-id="81503-105">The task module collects or displays information, processes the interaction and sends the information back to Teams.</span></span> <span data-ttu-id="81503-106">Ce document vous guide sur la sélection d’emplacements d’appel de commande d’action, la création de votre module de tâche, l’envoi d’un message final ou d’une carte, la création d’une commande d’action à l’aide d’app studio ou sa création manuelle.</span><span class="sxs-lookup"><span data-stu-id="81503-106">This document guides you on how to select action command invoke locations, create your task module, send final message, or card, create action command using app studio, or create it manually.</span></span> 

<span data-ttu-id="81503-107">Avant de créer la commande d’action, vous devez déterminer les facteurs suivants :</span><span class="sxs-lookup"><span data-stu-id="81503-107">Before creating the action command you must decide the following factors:</span></span>

1. [<span data-ttu-id="81503-108">À partir d’où la commande d’action peut-elle être déclenchée ?</span><span class="sxs-lookup"><span data-stu-id="81503-108">Where can the action command be triggered from?</span></span>](#select-action-command-invoke-locations)
1. [<span data-ttu-id="81503-109">Comment le module de tâche sera-t-il créé ?</span><span class="sxs-lookup"><span data-stu-id="81503-109">How will the task module be created?</span></span>](#select-how-to-create-your-task-module)
1. [<span data-ttu-id="81503-110">Le message final ou la carte sera-t-il envoyé au canal à partir d’un bot, ou le message ou la carte sera-t-il inséré dans la zone de composition du message à envoyer par l’utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="81503-110">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a><span data-ttu-id="81503-111">Sélectionner des emplacements d’appel de commande d’action</span><span class="sxs-lookup"><span data-stu-id="81503-111">Select action command invoke locations</span></span>

<span data-ttu-id="81503-112">Tout d’abord, vous devez déterminer l’emplacement à partir de lequel votre commande d’action doit être invoquée.</span><span class="sxs-lookup"><span data-stu-id="81503-112">First, you must decide the location from where your action command must be invoked.</span></span> <span data-ttu-id="81503-113">En spécifiant le manifeste de votre application, votre commande peut être invoquée à partir d’un ou plusieurs `context` des emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="81503-113">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="81503-114">Zone de composition de message : boutons situés en bas de la zone composer un message.</span><span class="sxs-lookup"><span data-stu-id="81503-114">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="81503-115">Zone de commande : en @mentioning votre application dans la zone de commande.</span><span class="sxs-lookup"><span data-stu-id="81503-115">Command box: By @mentioning your app in the command box.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="81503-116">Si l’extension de messagerie est invoquée à partir de la zone de commande, vous ne pouvez pas répondre avec un message bot inséré directement dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="81503-116">If messaging extension is invoked from the command box, you cannot respond with a bot message inserted directly into the conversation.</span></span>

* <span data-ttu-id="81503-117">Message : directement à partir d’un message existant via le `...` menu de dépassement d’un message.</span><span class="sxs-lookup"><span data-stu-id="81503-117">Message: Directly from an existing message through the `...` overflow menu on a message.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="81503-118">L’appel initial à votre bot inclut un objet JSON contenant le message à partir duquel il a été appelé.</span><span class="sxs-lookup"><span data-stu-id="81503-118">The initial invoke to your bot includes a JSON object containing the message from which it was invoked.</span></span> <span data-ttu-id="81503-119">Vous pouvez traiter le message avant de le présenter avec un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="81503-119">You can process the message before presenting them with a task module.</span></span>

<span data-ttu-id="81503-120">L’image suivante affiche les emplacements d’où la commande d’action est invoquée :</span><span class="sxs-lookup"><span data-stu-id="81503-120">The following image displays the locations from where action command is invoked:</span></span>

![emplacements d’appel de commande d’action](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a><span data-ttu-id="81503-122">Sélectionnez comment créer votre module de tâche</span><span class="sxs-lookup"><span data-stu-id="81503-122">Select how to create your task module</span></span>

<span data-ttu-id="81503-123">En plus de sélectionner l’endroit à partir de lequel votre commande peut être invoquée, vous devez également sélectionner comment remplir le formulaire dans le module de tâche pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="81503-123">In addition to selecting where your command can be invoked from, you must also select how to populate the form in the task module for your users.</span></span> <span data-ttu-id="81503-124">Vous avez les trois options suivantes pour créer le formulaire qui est rendu à l’intérieur du module de tâche :</span><span class="sxs-lookup"><span data-stu-id="81503-124">You have the following three options for creating the form that is rendered inside the task module:</span></span>   

* <span data-ttu-id="81503-125">**Liste statique de paramètres**: il s’agit de la méthode la plus simple.</span><span class="sxs-lookup"><span data-stu-id="81503-125">**Static list of parameters**: This is the simplest method.</span></span> <span data-ttu-id="81503-126">Vous pouvez définir une liste de paramètres dans le manifeste de votre application que le client Teams rendu, mais ne peut pas contrôler la mise en forme dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="81503-126">You can define a list of parameters in your app manifest the Teams client renders, but cannot control the formatting in this case.</span></span>
* <span data-ttu-id="81503-127">**Carte adaptative**: vous pouvez choisir d’utiliser une carte adaptative, ce qui offre un meilleur contrôle sur l’interface utilisateur, mais vous limite aux contrôles disponibles et aux options de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="81503-127">**Adaptive Card**:  You can select to use an Adaptive Card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="81503-128">**Affichage web incorporé**: vous pouvez choisir d’incorporer un affichage web personnalisé dans le module de tâche pour avoir un contrôle complet sur l’interface utilisateur et les contrôles.</span><span class="sxs-lookup"><span data-stu-id="81503-128">**Embedded web view**: You can select to embed a custom web view in the task module to have a complete control over the UI and controls.</span></span> 

<span data-ttu-id="81503-129">Si vous choisissez de créer le module de tâche avec une liste statique de paramètres et lorsque l’utilisateur soumet le module de tâche, l’extension de messagerie est appelée.</span><span class="sxs-lookup"><span data-stu-id="81503-129">If you select to create the task module with a static list of parameters and when the user submits the task module, the messaging extension is called.</span></span> <span data-ttu-id="81503-130">Lorsque vous utilisez une vue web incorporée ou une carte adaptative, votre extension de messagerie doit gérer un événement d’appel initial de l’utilisateur, créer le module de tâche et le renvoyer au client.</span><span class="sxs-lookup"><span data-stu-id="81503-130">When using an embedded web view or an Adaptive Card, your messaging extension must handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="select-how-the-final-message-is-sent"></a><span data-ttu-id="81503-131">Sélectionner la façon dont le message final est envoyé</span><span class="sxs-lookup"><span data-stu-id="81503-131">Select how the final message is sent</span></span>

<span data-ttu-id="81503-132">Dans la plupart des cas, la commande d’action entraîne l’insertion d’une carte dans la zone de composition du message.</span><span class="sxs-lookup"><span data-stu-id="81503-132">In most cases, the action command results in a card inserted into the compose message box.</span></span> <span data-ttu-id="81503-133">L’utilisateur peut l’envoyer dans le canal ou la conversation.</span><span class="sxs-lookup"><span data-stu-id="81503-133">The user can send it into the channel or chat.</span></span> <span data-ttu-id="81503-134">Dans ce cas, le message provient de l’utilisateur et le bot ne peut ni modifier ni mettre à jour la carte.</span><span class="sxs-lookup"><span data-stu-id="81503-134">In this case, the message comes from the user, and the bot cannot edit or update the card further.</span></span>

<span data-ttu-id="81503-135">Si l’extension de messagerie est invoquée à partir de la zone de composition ou directement à partir d’un message, votre service web peut insérer la réponse finale directement dans le canal ou la conversation.</span><span class="sxs-lookup"><span data-stu-id="81503-135">If the messaging extension is invoked from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="81503-136">Dans ce cas, la carte adaptative provient du bot, le bot la met à jour et répond au thread de conversation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="81503-136">In this case, the Adaptive Card comes from the bot, the bot updates it, and replies to the conversation thread if needed.</span></span> <span data-ttu-id="81503-137">Vous devez ajouter l’objet au manifeste de l’application à l’aide du même ID et définir `bot` les étendues appropriées.</span><span class="sxs-lookup"><span data-stu-id="81503-137">You must add the `bot` object to the app manifest using  the same ID and defining the appropriate scopes.</span></span>

## <a name="add-the-action-command-to-your-app-manifest"></a><span data-ttu-id="81503-138">Ajouter la commande d’action au manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="81503-138">Add the action command to your app manifest</span></span>

<span data-ttu-id="81503-139">Pour ajouter la commande d’action au manifeste de l’application, vous devez ajouter un nouvel objet au niveau supérieur `composeExtension` du manifeste d’application JSON.</span><span class="sxs-lookup"><span data-stu-id="81503-139">To add the action command to the app manifest, you must add a new `composeExtension` object to the top level of the app manifest JSON.</span></span> <span data-ttu-id="81503-140">Pour ce faire, vous pouvez utiliser l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="81503-140">You can use one of the following ways to do so:</span></span>

* [<span data-ttu-id="81503-141">Créer une commande d’action à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="81503-141">Create an action command using App Studio</span></span>](#create-an-action-command-using-app-studio)
* [<span data-ttu-id="81503-142">Créer une commande d’action manuellement</span><span class="sxs-lookup"><span data-stu-id="81503-142">Create an action command manually</span></span>](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a><span data-ttu-id="81503-143">Créer une commande d’action à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="81503-143">Create an action command using App Studio</span></span>

> [!NOTE]
> <span data-ttu-id="81503-144">La condition préalable à la création d’une commande d’action est que vous avez déjà créé une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="81503-144">The prerequisite to create an action command is that you have already created a messaging extension.</span></span> <span data-ttu-id="81503-145">Pour plus d’informations sur la création d’une extension de messagerie, voir [créer une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="81503-145">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="81503-146">**Pour créer une commande d’action**</span><span class="sxs-lookup"><span data-stu-id="81503-146">**To create an action command**</span></span>

1. <span data-ttu-id="81503-147">Ouvrez **App Studio** à partir Microsoft Teams client et sélectionnez **l’onglet Éditeur de** manifeste.</span><span class="sxs-lookup"><span data-stu-id="81503-147">Open **App Studio** from the Microsoft Teams client and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="81503-148">Si vous avez déjà créé votre package d’application dans **App Studio,** sélectionnez-le dans la liste.</span><span class="sxs-lookup"><span data-stu-id="81503-148">If you already created your app package in **App Studio**, select it from the list.</span></span> <span data-ttu-id="81503-149">Si vous n’avez pas créé de package d’application, importez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="81503-149">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="81503-150">Après avoir importé un package d’application, sélectionnez **les extensions de messagerie sous** **Fonctionnalités.**</span><span class="sxs-lookup"><span data-stu-id="81503-150">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="81503-151">Vous obtenez une fenêtre instantanée pour configurer l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="81503-151">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="81503-152">Sélectionnez **Configurer dans** la fenêtre pour inclure l’extension de messagerie dans l’expérience de votre application.</span><span class="sxs-lookup"><span data-stu-id="81503-152">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="81503-153">L’image suivante affiche la fenêtre de mise en place de l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="81503-153">The following image displays the messaging extension set up window:</span></span>

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. <span data-ttu-id="81503-154">Pour créer une extension de messagerie, vous avez besoin d’un bot inscrit par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="81503-154">To create a messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="81503-155">Vous pouvez utiliser un bot existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="81503-155">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="81503-156">Sélectionnez Créer une option **de bot,** donnez un nom au nouveau bot, puis sélectionnez **Créer.**</span><span class="sxs-lookup"><span data-stu-id="81503-156">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="81503-157">L’image suivante affiche la création d’un bot pour l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="81503-157">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="81503-158">Sélectionnez **Ajouter** dans **la section Commande** de la page Extensions de messagerie pour inclure les commandes qui déterminent le comportement de l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="81503-158">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="81503-159">L’image suivante affiche l’ajout de commande pour l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="81503-159">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. <span data-ttu-id="81503-160">Sélectionnez Autoriser les utilisateurs à déclencher des actions dans des services externes **à l’intérieur Teams**.</span><span class="sxs-lookup"><span data-stu-id="81503-160">Select **Allow users to trigger actions in external services while inside of Teams**.</span></span> <span data-ttu-id="81503-161">L’image suivante affiche la sélection de commande d’action :</span><span class="sxs-lookup"><span data-stu-id="81503-161">The following image displays the action command selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. <span data-ttu-id="81503-162">Pour utiliser un ensemble statique de paramètres pour créer votre module de tâche, sélectionnez Définir un ensemble de **paramètres statiques pour la commande.**</span><span class="sxs-lookup"><span data-stu-id="81503-162">To use a static set of parameters to create your task module, select **Define a set of static parameters for the command**.</span></span> 

    <span data-ttu-id="81503-163">L’image suivante affiche la sélection de paramètre statique de commande d’action :</span><span class="sxs-lookup"><span data-stu-id="81503-163">The following image displays the action command static parameter selection:</span></span>

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    <span data-ttu-id="81503-164">L’image suivante affiche un exemple de paramètre statique :</span><span class="sxs-lookup"><span data-stu-id="81503-164">The following image displays an example static parameter set-up:</span></span> 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    <span data-ttu-id="81503-165">L’image suivante affiche un exemple de test de paramètre statique :</span><span class="sxs-lookup"><span data-stu-id="81503-165">The following image displays an example static parameter testing:</span></span>

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. <span data-ttu-id="81503-166">Pour utiliser des paramètres dynamiques, sélectionnez récupérer un ensemble dynamique de **paramètres à partir de votre bot.**</span><span class="sxs-lookup"><span data-stu-id="81503-166">To use dynamic parameters, select to **Fetch a dynamic set of parameters from your bot**.</span></span> <span data-ttu-id="81503-167">L’image suivante affiche la sélection du paramètre de commande d’action :</span><span class="sxs-lookup"><span data-stu-id="81503-167">The following image displays the action command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. <span data-ttu-id="81503-168">Ajoutez **un ID de commande** et un **titre.**</span><span class="sxs-lookup"><span data-stu-id="81503-168">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="81503-169">Sélectionnez l’emplacement à partir de lequel vous souhaitez appeler la commande d’action.</span><span class="sxs-lookup"><span data-stu-id="81503-169">Select the location from where you want to invoke the action command.</span></span> <span data-ttu-id="81503-170">L’image suivante affiche l’emplacement d’appel de commande d’action :</span><span class="sxs-lookup"><span data-stu-id="81503-170">The following image displays the action command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. <span data-ttu-id="81503-171">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="81503-171">Select **Save**.</span></span>
1. <span data-ttu-id="81503-172">Pour ajouter d’autres paramètres, sélectionnez **le bouton** Ajouter dans la section **Paramètres.**</span><span class="sxs-lookup"><span data-stu-id="81503-172">To add more parameters, select the **Add** button in the **Parameters** section.</span></span>

### <a name="create-an-action-command-manually"></a><span data-ttu-id="81503-173">Créer une commande d’action manuellement</span><span class="sxs-lookup"><span data-stu-id="81503-173">Create an action command manually</span></span>

<span data-ttu-id="81503-174">Pour ajouter manuellement votre commande d’extension de messagerie basée sur l’action au manifeste de votre application, vous devez ajouter les paramètres suivants au tableau `composeExtension.commands` d’objets :</span><span class="sxs-lookup"><span data-stu-id="81503-174">To manually add your action-based messaging extension command to your app manifest, you must add the following parameters to the `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="81503-175">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="81503-175">Property name</span></span> | <span data-ttu-id="81503-176">Objectif</span><span class="sxs-lookup"><span data-stu-id="81503-176">Purpose</span></span> | <span data-ttu-id="81503-177">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="81503-177">Required?</span></span> | <span data-ttu-id="81503-178">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="81503-178">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="81503-179">Cette propriété est un ID unique que vous affectez à cette commande.</span><span class="sxs-lookup"><span data-stu-id="81503-179">This property is an unique ID that you assign to this command.</span></span> <span data-ttu-id="81503-180">La demande de l’utilisateur inclut cet ID.</span><span class="sxs-lookup"><span data-stu-id="81503-180">The user request includes this ID.</span></span> | <span data-ttu-id="81503-181">Oui</span><span class="sxs-lookup"><span data-stu-id="81503-181">Yes</span></span> | <span data-ttu-id="81503-182">1.0</span><span class="sxs-lookup"><span data-stu-id="81503-182">1.0</span></span> |
| `title` | <span data-ttu-id="81503-183">Cette propriété est un nom de commande.</span><span class="sxs-lookup"><span data-stu-id="81503-183">This property is a command name.</span></span> <span data-ttu-id="81503-184">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81503-184">This value appears in the UI.</span></span> | <span data-ttu-id="81503-185">Oui</span><span class="sxs-lookup"><span data-stu-id="81503-185">Yes</span></span> | <span data-ttu-id="81503-186">1.0</span><span class="sxs-lookup"><span data-stu-id="81503-186">1.0</span></span> |
| `type` | <span data-ttu-id="81503-187">Cette propriété doit être une `action` .</span><span class="sxs-lookup"><span data-stu-id="81503-187">This property must be an `action`.</span></span> | <span data-ttu-id="81503-188">Non</span><span class="sxs-lookup"><span data-stu-id="81503-188">No</span></span> | <span data-ttu-id="81503-189">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-189">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="81503-190">Cette propriété est définie sur pour une carte adaptative ou un affichage web incorporé pour votre module de tâche, et pour une liste statique de paramètres ou lors du chargement de l’affichage `true` `false` web par un `taskInfo` .</span><span class="sxs-lookup"><span data-stu-id="81503-190">This property is set to `true` for an adaptive card or embedded web view for your task module, and`false` for a static list of parameters or when loading the web view by a `taskInfo`.</span></span> | <span data-ttu-id="81503-191">Non</span><span class="sxs-lookup"><span data-stu-id="81503-191">No</span></span> | <span data-ttu-id="81503-192">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-192">1.4</span></span> |
| `context` | <span data-ttu-id="81503-193">Cette propriété est un tableau facultatif de valeurs qui définit l’endroit d’où l’extension de messagerie est invoquée.</span><span class="sxs-lookup"><span data-stu-id="81503-193">This property is an optional array of values that defines where the messaging extension is invoked from.</span></span> <span data-ttu-id="81503-194">Les valeurs possibles sont `message`, `compose` ou `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="81503-194">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="81503-195">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="81503-195">The default value is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="81503-196">Non</span><span class="sxs-lookup"><span data-stu-id="81503-196">No</span></span> | <span data-ttu-id="81503-197">1,5</span><span class="sxs-lookup"><span data-stu-id="81503-197">1.5</span></span> |

<span data-ttu-id="81503-198">Si vous utilisez une liste statique de paramètres, vous devez également ajouter les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="81503-198">If you are using a static list of parameters, you must also add the following parameters:</span></span>

| <span data-ttu-id="81503-199">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="81503-199">Property name</span></span> | <span data-ttu-id="81503-200">Objectif</span><span class="sxs-lookup"><span data-stu-id="81503-200">Purpose</span></span> | <span data-ttu-id="81503-201">Est-ce obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="81503-201">Is required?</span></span> | <span data-ttu-id="81503-202">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="81503-202">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="81503-203">Cette propriété décrit la liste statique des paramètres de la commande.</span><span class="sxs-lookup"><span data-stu-id="81503-203">This property describes the static list of parameters for the command.</span></span> <span data-ttu-id="81503-204">Utilisez uniquement quand `fetchTask` `false` est .</span><span class="sxs-lookup"><span data-stu-id="81503-204">Only use when `fetchTask` is `false`.</span></span> | <span data-ttu-id="81503-205">Non</span><span class="sxs-lookup"><span data-stu-id="81503-205">No</span></span> | <span data-ttu-id="81503-206">1.0</span><span class="sxs-lookup"><span data-stu-id="81503-206">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="81503-207">Cette propriété décrit le nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="81503-207">This property describes the name of the parameter.</span></span> <span data-ttu-id="81503-208">Cette information est envoyée à votre service dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81503-208">This is sent to your service in the user request.</span></span> | <span data-ttu-id="81503-209">Oui</span><span class="sxs-lookup"><span data-stu-id="81503-209">Yes</span></span> | <span data-ttu-id="81503-210">1.0</span><span class="sxs-lookup"><span data-stu-id="81503-210">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="81503-211">Cette propriété décrit les objectifs du paramètre ou un exemple de la valeur à fournir.</span><span class="sxs-lookup"><span data-stu-id="81503-211">This property describes the parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="81503-212">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81503-212">This value appears in the UI.</span></span> | <span data-ttu-id="81503-213">Oui</span><span class="sxs-lookup"><span data-stu-id="81503-213">Yes</span></span> | <span data-ttu-id="81503-214">1.0</span><span class="sxs-lookup"><span data-stu-id="81503-214">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="81503-215">Cette propriété est un titre ou une étiquette de paramètre convivial court.</span><span class="sxs-lookup"><span data-stu-id="81503-215">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="81503-216">Oui</span><span class="sxs-lookup"><span data-stu-id="81503-216">Yes</span></span> | <span data-ttu-id="81503-217">1.0</span><span class="sxs-lookup"><span data-stu-id="81503-217">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="81503-218">Cette propriété est définie sur le type d’entrée requis.</span><span class="sxs-lookup"><span data-stu-id="81503-218">This property is set to the type of input required.</span></span> <span data-ttu-id="81503-219">Les valeurs possibles `text` sont , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="81503-219">The possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="81503-220">La valeur par défaut est définie sur `text` .</span><span class="sxs-lookup"><span data-stu-id="81503-220">The default value is set to `text`.</span></span> | <span data-ttu-id="81503-221">Non</span><span class="sxs-lookup"><span data-stu-id="81503-221">No</span></span> | <span data-ttu-id="81503-222">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-222">1.4</span></span> |

<span data-ttu-id="81503-223">Si vous utilisez un affichage web incorporé, vous pouvez éventuellement ajouter l’objet pour récupérer votre affichage web sans appeler `taskInfo` directement votre bot.</span><span class="sxs-lookup"><span data-stu-id="81503-223">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="81503-224">Si vous sélectionnez cette option, le comportement est similaire à celui de l’utilisation d’une liste statique de paramètres.</span><span class="sxs-lookup"><span data-stu-id="81503-224">If you select this option, the behavior is similar to that of using a static list of parameters.</span></span> <span data-ttu-id="81503-225">Dans la mesure où la première interaction avec votre bot [répond à l’action d’soumission du module de tâche.](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span><span class="sxs-lookup"><span data-stu-id="81503-225">In that the first interaction with your bot is [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="81503-226">Si vous utilisez un `taskInfo` objet, vous devez définir le `fetchTask` paramètre sur `false` .</span><span class="sxs-lookup"><span data-stu-id="81503-226">If you are using a `taskInfo` object, you must set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="81503-227">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="81503-227">Property name</span></span> | <span data-ttu-id="81503-228">Objectif</span><span class="sxs-lookup"><span data-stu-id="81503-228">Purpose</span></span> | <span data-ttu-id="81503-229">Est-ce obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="81503-229">Is required?</span></span> | <span data-ttu-id="81503-230">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="81503-230">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="81503-231">Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="81503-231">Specify the task module to preload when using a messaging extension command.</span></span> | <span data-ttu-id="81503-232">Non</span><span class="sxs-lookup"><span data-stu-id="81503-232">No</span></span> | <span data-ttu-id="81503-233">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-233">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="81503-234">Titre du module de tâche initial.</span><span class="sxs-lookup"><span data-stu-id="81503-234">Initial task module title.</span></span> |<span data-ttu-id="81503-235">Non</span><span class="sxs-lookup"><span data-stu-id="81503-235">No</span></span> | <span data-ttu-id="81503-236">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-236">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="81503-237">Largeur du module de tâche, soit un nombre en pixels, soit une disposition par défaut telle `large` que `medium` , ou `small` .</span><span class="sxs-lookup"><span data-stu-id="81503-237">Task module width, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span> |<span data-ttu-id="81503-238">Non</span><span class="sxs-lookup"><span data-stu-id="81503-238">No</span></span> | <span data-ttu-id="81503-239">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-239">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="81503-240">Hauteur du module de tâche, soit un nombre en pixels, soit une disposition par défaut telle `large` que `medium` , ou `small` .</span><span class="sxs-lookup"><span data-stu-id="81503-240">Task module height, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span>|<span data-ttu-id="81503-241">Non</span><span class="sxs-lookup"><span data-stu-id="81503-241">No</span></span> | <span data-ttu-id="81503-242">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-242">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="81503-243">URL d’affichage web initiale.</span><span class="sxs-lookup"><span data-stu-id="81503-243">Initial web view URL.</span></span>|<span data-ttu-id="81503-244">Non</span><span class="sxs-lookup"><span data-stu-id="81503-244">No</span></span> | <span data-ttu-id="81503-245">1.4</span><span class="sxs-lookup"><span data-stu-id="81503-245">1.4</span></span> | 

#### <a name="app-manifest-example"></a><span data-ttu-id="81503-246">Exemple de manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="81503-246">App manifest example</span></span>

<span data-ttu-id="81503-247">La section suivante est un exemple `composeExtensions` d’objet définissant deux commandes d’action.</span><span class="sxs-lookup"><span data-stu-id="81503-247">The following section is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="81503-248">Il ne s’agit pas d’un exemple de manifeste complet.</span><span class="sxs-lookup"><span data-stu-id="81503-248">It is not an example of the complete manifest.</span></span> <span data-ttu-id="81503-249">Pour obtenir le schéma de manifeste d’application complet, voir schéma [de manifeste d’application](~/resources/schema/manifest-schema.md):</span><span class="sxs-lookup"><span data-stu-id="81503-249">For the complete app manifest schema, see [app manifest schema](~/resources/schema/manifest-schema.md):</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": true,
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
      }
    ]
  }
]
...
```

## <a name="code-sample"></a><span data-ttu-id="81503-250">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="81503-250">Code sample</span></span>

| <span data-ttu-id="81503-251">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="81503-251">Sample Name</span></span>           | <span data-ttu-id="81503-252">Description</span><span class="sxs-lookup"><span data-stu-id="81503-252">Description</span></span> | <span data-ttu-id="81503-253">.NET</span><span class="sxs-lookup"><span data-stu-id="81503-253">.NET</span></span>    | <span data-ttu-id="81503-254">Node.js</span><span class="sxs-lookup"><span data-stu-id="81503-254">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="81503-255">Teams d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="81503-255">Teams messaging extension action</span></span>| <span data-ttu-id="81503-256">Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’soumission du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="81503-256">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="81503-257">View</span><span class="sxs-lookup"><span data-stu-id="81503-257">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="81503-258">View</span><span class="sxs-lookup"><span data-stu-id="81503-258">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="81503-259">Teams d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="81503-259">Teams messaging extension search</span></span>   |  <span data-ttu-id="81503-260">Décrit comment définir des commandes de recherche et répondre aux recherches.</span><span class="sxs-lookup"><span data-stu-id="81503-260">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="81503-261">View</span><span class="sxs-lookup"><span data-stu-id="81503-261">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="81503-262">View</span><span class="sxs-lookup"><span data-stu-id="81503-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="81503-263">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="81503-263">Next step</span></span>

<span data-ttu-id="81503-264">Si vous utilisez une carte adaptative ou un affichage web incorporé sans `taskInfo` objet, l’étape suivante consiste à :</span><span class="sxs-lookup"><span data-stu-id="81503-264">If you are using either an Adaptive Card or an embedded web view without a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81503-265">Créer et répondre avec un module de tâche</span><span class="sxs-lookup"><span data-stu-id="81503-265">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="81503-266">Si vous utilisez les paramètres ou un affichage web incorporé avec un `taskInfo` objet, l’étape suivante consiste à :</span><span class="sxs-lookup"><span data-stu-id="81503-266">If you are using the parameters or an embedded web view with a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81503-267">Répondre à l’soumission du module de tâche</span><span class="sxs-lookup"><span data-stu-id="81503-267">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

