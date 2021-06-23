---
title: Définir les commandes de recherche d’extension de messagerie
author: surbhigupta
description: Définissez les commandes de recherche d’extension de messagerie pour Microsoft Teams applications.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 6333840e6817761911b2b5acd4b53849448b5b68
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068915"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="01e35-103">Définir les commandes de recherche d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="01e35-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="01e35-104">Les commandes de recherche d’extension de messagerie permettent aux utilisateurs de rechercher des systèmes externes et d’insérer les résultats de cette recherche dans un message sous la forme d’une carte.</span><span class="sxs-lookup"><span data-stu-id="01e35-104">Messaging extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card.</span></span> <span data-ttu-id="01e35-105">Ce document vous guide sur la sélection des emplacements d’appel de commande de recherche et ajoute la commande de recherche au manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="01e35-105">This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.</span></span>

> [!NOTE]
> <span data-ttu-id="01e35-106">La limite de taille de carte de résultat est de 28 Ko.</span><span class="sxs-lookup"><span data-stu-id="01e35-106">The result card size limit is 28 KB.</span></span> <span data-ttu-id="01e35-107">La carte n’est pas envoyée si sa taille dépasse 28 Ko.</span><span class="sxs-lookup"><span data-stu-id="01e35-107">The card is not sent if its size exceeds 28 KB.</span></span>

## <a name="select-search-command-invoke-locations"></a><span data-ttu-id="01e35-108">Sélectionner des emplacements d’appel de commande de recherche</span><span class="sxs-lookup"><span data-stu-id="01e35-108">Select search command invoke locations</span></span>

<span data-ttu-id="01e35-109">La commande de recherche est invoquée à partir de l’un des emplacements suivants ou des deux :</span><span class="sxs-lookup"><span data-stu-id="01e35-109">The search command is invoked from any one or both of the following locations:</span></span>

* <span data-ttu-id="01e35-110">Zone de composition de message : boutons situés en bas de la zone composer un message.</span><span class="sxs-lookup"><span data-stu-id="01e35-110">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="01e35-111">Zone de commande : en @mentioning dans la zone de commande.</span><span class="sxs-lookup"><span data-stu-id="01e35-111">Command box: By @mentioning in the command box.</span></span>

<span data-ttu-id="01e35-112">Lorsque la commande de recherche est invoquée à partir de la zone composer un message, l’utilisateur envoie les résultats à la conversation.</span><span class="sxs-lookup"><span data-stu-id="01e35-112">When search command is invoked from the compose message area, the user sends the results to the conversation.</span></span> <span data-ttu-id="01e35-113">Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur interagit avec la carte résultante ou la copie pour l’utiliser ailleurs.</span><span class="sxs-lookup"><span data-stu-id="01e35-113">When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.</span></span>

<span data-ttu-id="01e35-114">L’image suivante affiche les emplacements d’appel de la commande de recherche :</span><span class="sxs-lookup"><span data-stu-id="01e35-114">The following image displays the invoke locations of the search command:</span></span>

![emplacements d’appel de commande de recherche](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a><span data-ttu-id="01e35-116">Ajouter la commande de recherche au manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="01e35-116">Add the search command to your app manifest</span></span>

<span data-ttu-id="01e35-117">Pour ajouter la commande de recherche au manifeste de votre application, vous devez ajouter un nouvel objet au niveau supérieur du manifeste JSON de `composeExtension` votre application.</span><span class="sxs-lookup"><span data-stu-id="01e35-117">To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="01e35-118">Vous pouvez ajouter la commande de recherche à l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="01e35-118">You can add the search command either with the help of App Studio, or manually.</span></span>

### <a name="create-a-search-command-using-app-studio"></a><span data-ttu-id="01e35-119">Créer une commande de recherche à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="01e35-119">Create a search command using App Studio</span></span>

<span data-ttu-id="01e35-120">La condition préalable à la création d’une commande de recherche est que vous devez déjà avoir créé une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="01e35-120">The prerequisite to create a search command is that you must already have created a messaging extension.</span></span> <span data-ttu-id="01e35-121">Pour plus d’informations sur la création d’une extension de messagerie, voir [créer une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="01e35-121">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="01e35-122">**Pour créer une commande de recherche**</span><span class="sxs-lookup"><span data-stu-id="01e35-122">**To create a search command**</span></span>

1. <span data-ttu-id="01e35-123">Ouvrez **App Studio** à partir Microsoft Teams client, puis sélectionnez l’onglet **Éditeur de** manifeste.</span><span class="sxs-lookup"><span data-stu-id="01e35-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1.  <span data-ttu-id="01e35-124">Si vous avez déjà créé votre package d’application dans **App Studio,** sélectionnez-le dans la liste.</span><span class="sxs-lookup"><span data-stu-id="01e35-124">If you already created your app package in **App Studio**, select from the list.</span></span> <span data-ttu-id="01e35-125">Si vous n’avez pas créé de package d’application, importez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="01e35-125">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="01e35-126">Après avoir importé le package d’application, sélectionnez **les extensions de messagerie sous** **Fonctionnalités.**</span><span class="sxs-lookup"><span data-stu-id="01e35-126">After importing app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="01e35-127">Vous obtenez une fenêtre instantanée pour configurer l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="01e35-127">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="01e35-128">Sélectionnez **Configurer dans** la fenêtre pour inclure l’extension de messagerie dans l’expérience de votre application.</span><span class="sxs-lookup"><span data-stu-id="01e35-128">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="01e35-129">L’image suivante affiche la page de mise en place de l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="01e35-129">The following image displays the messaging extension set up page:</span></span> 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. <span data-ttu-id="01e35-130">Pour créer l’extension de messagerie, vous avez besoin d’un bot inscrit par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01e35-130">To create the messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="01e35-131">Vous pouvez utiliser un bot existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="01e35-131">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="01e35-132">Sélectionnez Créer une option **de bot,** donnez un nom au nouveau bot, puis sélectionnez **Créer.**</span><span class="sxs-lookup"><span data-stu-id="01e35-132">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="01e35-133">L’image suivante affiche la création d’un bot pour l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="01e35-133">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="01e35-134">Sélectionnez **Ajouter** dans **la section Commande** de la page Extensions de messagerie pour inclure les commandes qui déterminent le comportement de l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="01e35-134">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="01e35-135">L’image suivante affiche l’ajout de commande pour l’extension de messagerie :</span><span class="sxs-lookup"><span data-stu-id="01e35-135">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. <span data-ttu-id="01e35-136">Sélectionnez **Autoriser les utilisateurs à interroger votre service pour obtenir des informations** et à les insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="01e35-136">Select **Allow users to query your service for information and insert that into a message**.</span></span> <span data-ttu-id="01e35-137">L’image suivante affiche la sélection du paramètre de commande de recherche :</span><span class="sxs-lookup"><span data-stu-id="01e35-137">The following image displays the search command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. <span data-ttu-id="01e35-138">Ajoutez **un ID de commande** et un **titre.**</span><span class="sxs-lookup"><span data-stu-id="01e35-138">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="01e35-139">Sélectionnez l’emplacement à partir de lequel votre commande de recherche doit être invoquée.</span><span class="sxs-lookup"><span data-stu-id="01e35-139">Select the location from where your search command must be invoked.</span></span> <span data-ttu-id="01e35-140">La sélection **d’un message** ne modifie pas actuellement le comportement de votre commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="01e35-140">Selecting **message** does not currently alter the behavior of your search command.</span></span> <span data-ttu-id="01e35-141">L’image suivante affiche l’emplacement d’appel de commande de recherche :</span><span class="sxs-lookup"><span data-stu-id="01e35-141">The following image displays the search command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. <span data-ttu-id="01e35-142">Ajoutez votre paramètre de recherche et sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="01e35-142">Add your search parameter and select **Save**.</span></span>

### <a name="create-a-search-command-manually"></a><span data-ttu-id="01e35-143">Créer une commande de recherche manuellement</span><span class="sxs-lookup"><span data-stu-id="01e35-143">Create a search command manually</span></span> 

<span data-ttu-id="01e35-144">Pour ajouter manuellement votre commande de recherche d’extension de messagerie au manifeste de votre application, vous devez ajouter les paramètres suivants à votre `composeExtension.commands` tableau d’objets :</span><span class="sxs-lookup"><span data-stu-id="01e35-144">To manually add your messaging extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="01e35-145">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="01e35-145">Property name</span></span> | <span data-ttu-id="01e35-146">Objectif</span><span class="sxs-lookup"><span data-stu-id="01e35-146">Purpose</span></span> | <span data-ttu-id="01e35-147">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="01e35-147">Required?</span></span> | <span data-ttu-id="01e35-148">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="01e35-148">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="01e35-149">Cette propriété est un ID unique que vous affectez à la commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="01e35-149">This property is an unique ID that you assign to search command.</span></span> <span data-ttu-id="01e35-150">La demande de l’utilisateur inclut cet ID.</span><span class="sxs-lookup"><span data-stu-id="01e35-150">The user request includes this ID.</span></span> | <span data-ttu-id="01e35-151">Oui</span><span class="sxs-lookup"><span data-stu-id="01e35-151">Yes</span></span> | <span data-ttu-id="01e35-152">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-152">1.0</span></span> |
| `title` | <span data-ttu-id="01e35-153">Cette propriété est un nom de commande.</span><span class="sxs-lookup"><span data-stu-id="01e35-153">This property is a command name.</span></span> <span data-ttu-id="01e35-154">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01e35-154">This value appears in the user interface (UI).</span></span> | <span data-ttu-id="01e35-155">Oui</span><span class="sxs-lookup"><span data-stu-id="01e35-155">Yes</span></span> | <span data-ttu-id="01e35-156">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-156">1.0</span></span> |
| `description` | <span data-ttu-id="01e35-157">Cette propriété est un texte d’aide indiquant ce que fait cette commande.</span><span class="sxs-lookup"><span data-stu-id="01e35-157">This property is a help text indicating what this command does.</span></span> <span data-ttu-id="01e35-158">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01e35-158">This value appears in the UI.</span></span> | <span data-ttu-id="01e35-159">Oui</span><span class="sxs-lookup"><span data-stu-id="01e35-159">Yes</span></span> | <span data-ttu-id="01e35-160">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-160">1.0</span></span> |
| `type` | <span data-ttu-id="01e35-161">Cette propriété doit être une `query` .</span><span class="sxs-lookup"><span data-stu-id="01e35-161">This property must be a `query`.</span></span> | <span data-ttu-id="01e35-162">Non</span><span class="sxs-lookup"><span data-stu-id="01e35-162">No</span></span> | <span data-ttu-id="01e35-163">1.4</span><span class="sxs-lookup"><span data-stu-id="01e35-163">1.4</span></span> |
|`initialRun` | <span data-ttu-id="01e35-164">Si cette propriété est définie sur **true,** elle indique que cette commande doit être exécutée dès que l’utilisateur sélectionne cette commande dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01e35-164">If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI.</span></span> | <span data-ttu-id="01e35-165">Non</span><span class="sxs-lookup"><span data-stu-id="01e35-165">No</span></span> | <span data-ttu-id="01e35-166">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-166">1.0</span></span> |
| `context` | <span data-ttu-id="01e35-167">Cette propriété est un tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible.</span><span class="sxs-lookup"><span data-stu-id="01e35-167">This property is an optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="01e35-168">Les valeurs possibles sont `message`, `compose` ou `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="01e35-168">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="01e35-169">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="01e35-169">The default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="01e35-170">Non</span><span class="sxs-lookup"><span data-stu-id="01e35-170">No</span></span> | <span data-ttu-id="01e35-171">1,5</span><span class="sxs-lookup"><span data-stu-id="01e35-171">1.5</span></span> |

<span data-ttu-id="01e35-172">Vous devez ajouter les détails du paramètre de recherche, qui définit le texte visible pour votre utilisateur dans le client Teams recherche.</span><span class="sxs-lookup"><span data-stu-id="01e35-172">You must add the details of the search parameter, that defines the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="01e35-173">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="01e35-173">Property name</span></span> | <span data-ttu-id="01e35-174">Objectif</span><span class="sxs-lookup"><span data-stu-id="01e35-174">Purpose</span></span> | <span data-ttu-id="01e35-175">Est-ce obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="01e35-175">Is required?</span></span> | <span data-ttu-id="01e35-176">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="01e35-176">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="01e35-177">Cette propriété définit une liste statique de paramètres pour la commande.</span><span class="sxs-lookup"><span data-stu-id="01e35-177">This property defines a static list of parameters for the command.</span></span> | <span data-ttu-id="01e35-178">Non</span><span class="sxs-lookup"><span data-stu-id="01e35-178">No</span></span> | <span data-ttu-id="01e35-179">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-179">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="01e35-180">Cette propriété décrit le nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="01e35-180">This property describes the name of the parameter.</span></span> <span data-ttu-id="01e35-181">Cette information est envoyée à votre service dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01e35-181">This is sent to your service in the user request.</span></span> | <span data-ttu-id="01e35-182">Oui</span><span class="sxs-lookup"><span data-stu-id="01e35-182">Yes</span></span> | <span data-ttu-id="01e35-183">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-183">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="01e35-184">Cette propriété décrit les objectifs du paramètre ou un exemple de la valeur à fournir.</span><span class="sxs-lookup"><span data-stu-id="01e35-184">This property describes the parameter’s purposes or example of the value that must be provided.</span></span> <span data-ttu-id="01e35-185">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01e35-185">This value appears in the UI.</span></span> | <span data-ttu-id="01e35-186">Oui</span><span class="sxs-lookup"><span data-stu-id="01e35-186">Yes</span></span> | <span data-ttu-id="01e35-187">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-187">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="01e35-188">Cette propriété est un titre ou une étiquette de paramètre convivial court.</span><span class="sxs-lookup"><span data-stu-id="01e35-188">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="01e35-189">Oui</span><span class="sxs-lookup"><span data-stu-id="01e35-189">Yes</span></span> | <span data-ttu-id="01e35-190">1.0</span><span class="sxs-lookup"><span data-stu-id="01e35-190">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="01e35-191">Cette propriété est définie sur le type d’entrée requis.</span><span class="sxs-lookup"><span data-stu-id="01e35-191">This property is set to the type of the input required.</span></span> <span data-ttu-id="01e35-192">Les valeurs `text` possibles sont , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="01e35-192">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="01e35-193">La valeur par défaut est définie sur `text` .</span><span class="sxs-lookup"><span data-stu-id="01e35-193">Default is set to `text`.</span></span> | <span data-ttu-id="01e35-194">Non</span><span class="sxs-lookup"><span data-stu-id="01e35-194">No</span></span> | <span data-ttu-id="01e35-195">1.4</span><span class="sxs-lookup"><span data-stu-id="01e35-195">1.4</span></span> |

#### <a name="example"></a><span data-ttu-id="01e35-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="01e35-196">Example</span></span>

<span data-ttu-id="01e35-197">La section suivante est un exemple du manifeste d’application simple de `composeExtensions` l’objet définissant une commande de recherche :</span><span class="sxs-lookup"><span data-stu-id="01e35-197">Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:</span></span> 

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```
<span data-ttu-id="01e35-198">Pour obtenir le manifeste complet de l’application, voir [schéma de manifeste d’application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="01e35-198">For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="01e35-199">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="01e35-199">Code sample</span></span>

| <span data-ttu-id="01e35-200">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="01e35-200">Sample Name</span></span>           | <span data-ttu-id="01e35-201">Description</span><span class="sxs-lookup"><span data-stu-id="01e35-201">Description</span></span> | <span data-ttu-id="01e35-202">.NET</span><span class="sxs-lookup"><span data-stu-id="01e35-202">.NET</span></span>    | <span data-ttu-id="01e35-203">Node.js</span><span class="sxs-lookup"><span data-stu-id="01e35-203">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="01e35-204">Teams d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="01e35-204">Teams messaging extension action</span></span>| <span data-ttu-id="01e35-205">Décrit comment définir des commandes d’action, créer un module de tâche et répondre à l’action d’soumission du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="01e35-205">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="01e35-206">View</span><span class="sxs-lookup"><span data-stu-id="01e35-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="01e35-207">View</span><span class="sxs-lookup"><span data-stu-id="01e35-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="01e35-208">Teams d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="01e35-208">Teams messaging extension search</span></span>   |  <span data-ttu-id="01e35-209">Décrit comment définir des commandes de recherche et répondre aux recherches.</span><span class="sxs-lookup"><span data-stu-id="01e35-209">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="01e35-210">View</span><span class="sxs-lookup"><span data-stu-id="01e35-210">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="01e35-211">View</span><span class="sxs-lookup"><span data-stu-id="01e35-211">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="01e35-212">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="01e35-212">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="01e35-213">[Répondez aux commandes de recherche.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="01e35-213">[Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

