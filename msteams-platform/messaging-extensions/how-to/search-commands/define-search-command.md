---
title: Définir les commandes de recherche d’extension de messagerie
author: clearab
description: Définissez les commandes de recherche d’extension de messagerie pour les applications Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449268"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="c14c7-103">Définir les commandes de recherche d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="c14c7-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="c14c7-104">Les commandes de recherche d’extension de messagerie permettent à vos utilisateurs d’effectuer une recherche dans des systèmes externes et d’insérer les résultats de la recherche dans un message sous la forme d’une carte.</span><span class="sxs-lookup"><span data-stu-id="c14c7-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

> [!NOTE]
> <span data-ttu-id="c14c7-105">La limite de taille de carte de résultat est de 28 Ko.</span><span class="sxs-lookup"><span data-stu-id="c14c7-105">The result card size limit is 28 KB.</span></span> <span data-ttu-id="c14c7-106">La carte n’est pas envoyée si sa taille dépasse 28 Ko.</span><span class="sxs-lookup"><span data-stu-id="c14c7-106">The card is not sent if its size exceeds 28 KB.</span></span> 

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="c14c7-107">Choisir les emplacements d’appel d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="c14c7-107">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="c14c7-108">La première chose que vous devez déterminer est l’endroit à partir de lequel votre commande de recherche peut être déclenchée (ou spécifiquement *invoquée).*</span><span class="sxs-lookup"><span data-stu-id="c14c7-108">The first thing you need to decide is where your search command can be triggered (or specifically, *invoked*) from.</span></span> <span data-ttu-id="c14c7-109">Votre commande de recherche peut être invoquée à partir de l’un des emplacements suivants ou des deux :</span><span class="sxs-lookup"><span data-stu-id="c14c7-109">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="c14c7-110">Boutons situés en bas de la zone composer un message</span><span class="sxs-lookup"><span data-stu-id="c14c7-110">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="c14c7-111">En @mentioning dans la zone de commande</span><span class="sxs-lookup"><span data-stu-id="c14c7-111">By @mentioning in the command box</span></span>

<span data-ttu-id="c14c7-112">Lorsqu’il est appelé à partir de la zone de composition du message, votre utilisateur a la possibilité d’envoyer les résultats à la conversation.</span><span class="sxs-lookup"><span data-stu-id="c14c7-112">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="c14c7-113">Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur peut interagir avec la carte résultante ou la copier pour l’utiliser ailleurs.</span><span class="sxs-lookup"><span data-stu-id="c14c7-113">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="c14c7-114">Ajouter la commande au manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="c14c7-114">Add the command to your app manifest</span></span>

<span data-ttu-id="c14c7-115">Maintenant que vous avez décidé de la façon dont les utilisateurs interagira avec votre commande de recherche, il est temps de l’ajouter au manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="c14c7-115">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="c14c7-116">Pour ce faire, vous allez ajouter un nouvel objet au niveau `composeExtension` supérieur du manifeste JSON de votre application.</span><span class="sxs-lookup"><span data-stu-id="c14c7-116">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="c14c7-117">Vous pouvez le faire à l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="c14c7-117">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="c14c7-118">Créer une commande à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="c14c7-118">Create a command using App Studio</span></span>

<span data-ttu-id="c14c7-119">La condition préalable à la création d’une commande de recherche est que vous devez déjà créer une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c14c7-119">The prerequisite to create a search command is that you must already create a messaging extension.</span></span> <span data-ttu-id="c14c7-120">Pour plus d’informations sur la création d’une extension de messagerie, voir [créer une extension de messagerie.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="c14c7-120">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="c14c7-121">**Pour créer une commande de recherche**</span><span class="sxs-lookup"><span data-stu-id="c14c7-121">**To create a search command**</span></span>

1. <span data-ttu-id="c14c7-122">Dans le client Microsoft Teams, ouvrez **App Studio** et sélectionnez l’onglet **Éditeur de** manifeste.</span><span class="sxs-lookup"><span data-stu-id="c14c7-122">From the Microsoft Teams client, open **App Studio**, and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="c14c7-123">Si vous avez déjà créé un package d’application dans **App Studio,** choisissez-le dans la liste.</span><span class="sxs-lookup"><span data-stu-id="c14c7-123">If you already created an app package in the **App Studio**, choose it from the list.</span></span> <span data-ttu-id="c14c7-124">Si vous n’avez pas créé de package d’application, importez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="c14c7-124">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="c14c7-125">Après avoir importé un package d’application, sélectionnez **les extensions de messagerie sous** **Fonctionnalités.**</span><span class="sxs-lookup"><span data-stu-id="c14c7-125">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span>
1. <span data-ttu-id="c14c7-126">Sélectionnez **Ajouter** dans la section **Commande** de la page Extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="c14c7-126">Select **Add** in the **Command** section in the messaging extensions page.</span></span>
1. <span data-ttu-id="c14c7-127">Choisissez **Autoriser les utilisateurs à interroger votre service pour obtenir des informations et à les insérer dans un message.**</span><span class="sxs-lookup"><span data-stu-id="c14c7-127">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
1. <span data-ttu-id="c14c7-128">Ajoutez **un ID de commande** et un **titre.**</span><span class="sxs-lookup"><span data-stu-id="c14c7-128">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="c14c7-129">Sélectionnez l’emplacement à partir de lequel votre commande de recherche doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="c14c7-129">Select the location from where your search command must be triggered.</span></span> <span data-ttu-id="c14c7-130">La sélection **d’un message** ne modifie pas actuellement le comportement de votre commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="c14c7-130">Selecting **message** does not currently alter the behavior of your search command.</span></span>
1. <span data-ttu-id="c14c7-131">Ajoutez votre paramètre de recherche et sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="c14c7-131">Add your search parameter and select **Save**.</span></span>
 
### <a name="manually-create-a-command"></a><span data-ttu-id="c14c7-132">Créer manuellement une commande</span><span class="sxs-lookup"><span data-stu-id="c14c7-132">Manually create a command</span></span>

<span data-ttu-id="c14c7-133">Pour ajouter manuellement votre commande de recherche d’extension de messagerie au manifeste de votre application, vous devez ajouter les paramètres suivants à votre `composeExtension.commands` tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="c14c7-133">To manually add your messaging extension search command to your app manifest, you'll need to add the following parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="c14c7-134">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="c14c7-134">Property name</span></span> | <span data-ttu-id="c14c7-135">Objectif</span><span class="sxs-lookup"><span data-stu-id="c14c7-135">Purpose</span></span> | <span data-ttu-id="c14c7-136">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="c14c7-136">Required?</span></span> | <span data-ttu-id="c14c7-137">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="c14c7-137">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="c14c7-138">ID unique que vous affectez à cette commande.</span><span class="sxs-lookup"><span data-stu-id="c14c7-138">Unique ID that you assign to this command.</span></span> <span data-ttu-id="c14c7-139">La demande de l’utilisateur inclut cet ID.</span><span class="sxs-lookup"><span data-stu-id="c14c7-139">The user request will include this ID.</span></span> | <span data-ttu-id="c14c7-140">Oui</span><span class="sxs-lookup"><span data-stu-id="c14c7-140">Yes</span></span> | <span data-ttu-id="c14c7-141">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-141">1.0</span></span> |
| `title` | <span data-ttu-id="c14c7-142">Nom de la commande.</span><span class="sxs-lookup"><span data-stu-id="c14c7-142">Command name.</span></span> <span data-ttu-id="c14c7-143">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c14c7-143">This value appears in the UI.</span></span> | <span data-ttu-id="c14c7-144">Oui</span><span class="sxs-lookup"><span data-stu-id="c14c7-144">Yes</span></span> | <span data-ttu-id="c14c7-145">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-145">1.0</span></span> |
| `description` | <span data-ttu-id="c14c7-146">Texte d’aide indiquant ce que fait cette commande.</span><span class="sxs-lookup"><span data-stu-id="c14c7-146">Help text indicating what this command does.</span></span> <span data-ttu-id="c14c7-147">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c14c7-147">This value appears in the UI.</span></span> | <span data-ttu-id="c14c7-148">Oui</span><span class="sxs-lookup"><span data-stu-id="c14c7-148">Yes</span></span> | <span data-ttu-id="c14c7-149">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-149">1.0</span></span> |
| `type` | <span data-ttu-id="c14c7-150">Doit être `query`</span><span class="sxs-lookup"><span data-stu-id="c14c7-150">Must be `query`</span></span> | <span data-ttu-id="c14c7-151">Non</span><span class="sxs-lookup"><span data-stu-id="c14c7-151">No</span></span> | <span data-ttu-id="c14c7-152">1.4</span><span class="sxs-lookup"><span data-stu-id="c14c7-152">1.4</span></span> |
|`initialRun` | <span data-ttu-id="c14c7-153">Si la valeur **est true,** indique que cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c14c7-153">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="c14c7-154">Non</span><span class="sxs-lookup"><span data-stu-id="c14c7-154">No</span></span> | <span data-ttu-id="c14c7-155">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-155">1.0</span></span> |
| `context` | <span data-ttu-id="c14c7-156">Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible.</span><span class="sxs-lookup"><span data-stu-id="c14c7-156">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="c14c7-157">Les valeurs possibles `message` sont , `compose` ou `commandBox` .</span><span class="sxs-lookup"><span data-stu-id="c14c7-157">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="c14c7-158">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="c14c7-158">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="c14c7-159">Non</span><span class="sxs-lookup"><span data-stu-id="c14c7-159">No</span></span> | <span data-ttu-id="c14c7-160">1,5</span><span class="sxs-lookup"><span data-stu-id="c14c7-160">1.5</span></span> |

<span data-ttu-id="c14c7-161">Vous devez également ajouter les détails du paramètre de recherche, qui définit le texte visible pour votre utilisateur dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="c14c7-161">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="c14c7-162">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="c14c7-162">Property name</span></span> | <span data-ttu-id="c14c7-163">Objectif</span><span class="sxs-lookup"><span data-stu-id="c14c7-163">Purpose</span></span> | <span data-ttu-id="c14c7-164">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="c14c7-164">Required?</span></span> | <span data-ttu-id="c14c7-165">Version minimale du manifeste</span><span class="sxs-lookup"><span data-stu-id="c14c7-165">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="c14c7-166">Liste statique des paramètres de la commande.</span><span class="sxs-lookup"><span data-stu-id="c14c7-166">Static list of parameters for the command.</span></span> | <span data-ttu-id="c14c7-167">Non</span><span class="sxs-lookup"><span data-stu-id="c14c7-167">No</span></span> | <span data-ttu-id="c14c7-168">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-168">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="c14c7-169">Le nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="c14c7-169">The name of the parameter.</span></span> <span data-ttu-id="c14c7-170">Cette information est envoyée à votre service dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c14c7-170">This is sent to your service in the user request.</span></span> | <span data-ttu-id="c14c7-171">Oui</span><span class="sxs-lookup"><span data-stu-id="c14c7-171">Yes</span></span> | <span data-ttu-id="c14c7-172">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-172">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="c14c7-173">Décrit les objectifs de ce paramètre ou un exemple de la valeur à fournir.</span><span class="sxs-lookup"><span data-stu-id="c14c7-173">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="c14c7-174">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c14c7-174">This value appears in the UI.</span></span> | <span data-ttu-id="c14c7-175">Oui</span><span class="sxs-lookup"><span data-stu-id="c14c7-175">Yes</span></span> | <span data-ttu-id="c14c7-176">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-176">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="c14c7-177">Titre ou étiquette de paramètre convivial court.</span><span class="sxs-lookup"><span data-stu-id="c14c7-177">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="c14c7-178">Oui</span><span class="sxs-lookup"><span data-stu-id="c14c7-178">Yes</span></span> | <span data-ttu-id="c14c7-179">1.0</span><span class="sxs-lookup"><span data-stu-id="c14c7-179">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="c14c7-180">Définir sur le type d’entrée requis.</span><span class="sxs-lookup"><span data-stu-id="c14c7-180">Set to the type of input required.</span></span> <span data-ttu-id="c14c7-181">Les valeurs `text` possibles sont , , , , `textarea` `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="c14c7-181">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="c14c7-182">La valeur par défaut est définie sur `text`</span><span class="sxs-lookup"><span data-stu-id="c14c7-182">Default is set to `text`</span></span> | <span data-ttu-id="c14c7-183">Non</span><span class="sxs-lookup"><span data-stu-id="c14c7-183">No</span></span> | <span data-ttu-id="c14c7-184">1.4</span><span class="sxs-lookup"><span data-stu-id="c14c7-184">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="c14c7-185">Exemple de manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="c14c7-185">App manifest example</span></span>

<span data-ttu-id="c14c7-186">Vous trouverez ci-dessous un exemple `composeExtensions` d’objet définissant une commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="c14c7-186">Below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="c14c7-187">Il ne s’agit pas d’un exemple de manifeste complet, pour le schéma de manifeste d’application complet, voir : [Schéma de manifeste d’application](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c14c7-187">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c14c7-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c14c7-188">Next steps</span></span>

<span data-ttu-id="c14c7-189">Maintenant que vous avez ajouté votre commande de recherche, vous devez gérer [la demande de recherche.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="c14c7-189">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
