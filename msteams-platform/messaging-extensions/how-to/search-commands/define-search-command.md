---
title: Définir les commandes de recherche d’extension de messagerie
author: clearab
description: Définir les commandes de recherche d’extension de messagerie pour les applications Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673848"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="9b3a5-103">Définir les commandes de recherche d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9b3a5-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="9b3a5-104">Les commandes de recherche d’extension de messagerie permettent à vos utilisateurs d’effectuer des recherches dans des systèmes externes et d’insérer les résultats de cette recherche dans un message sous la forme d’une carte.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="9b3a5-105">Choisir les emplacements d’appel d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9b3a5-105">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="9b3a5-106">La première chose que vous devez décider est l’emplacement où votre commande de recherche peut être déclenchée (ou plus spécifiquement *appelée*).</span><span class="sxs-lookup"><span data-stu-id="9b3a5-106">The first thing you need to decide is where your search command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="9b3a5-107">Votre commande de recherche peut être appelée à partir de l’un des emplacements suivants (ou les deux) :</span><span class="sxs-lookup"><span data-stu-id="9b3a5-107">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="9b3a5-108">Les boutons situés en bas de la zone de message de composition</span><span class="sxs-lookup"><span data-stu-id="9b3a5-108">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="9b3a5-109">Par @mentioning dans la zone de commande</span><span class="sxs-lookup"><span data-stu-id="9b3a5-109">By @mentioning in the command box</span></span>

<span data-ttu-id="9b3a5-110">Lorsqu’il est appelé à partir de la zone de message de composition, votre utilisateur a la possibilité d’envoyer les résultats à la conversation.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-110">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="9b3a5-111">Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur peut interagir avec la carte résultante ou la copier pour une utilisation ailleurs.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-111">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="9b3a5-112">Ajouter la commande à votre manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="9b3a5-112">Add the command to your app manifest</span></span>

<span data-ttu-id="9b3a5-113">Maintenant que vous avez décidé de la façon dont les utilisateurs vont interagir avec votre commande de recherche, il est temps de l’ajouter à votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-113">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="9b3a5-114">Pour ce faire, vous allez ajouter un `composeExtension` nouvel objet au niveau supérieur de votre fichier JSON de manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-114">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="9b3a5-115">Vous pouvez le faire à l’aide de l’aide d’App Studio ou manuellement.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-115">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="9b3a5-116">Créer une commande à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="9b3a5-116">Create a command using App Studio</span></span>

<span data-ttu-id="9b3a5-117">Les étapes suivantes supposent que vous avez déjà [créé une extension de messagerie](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9b3a5-117">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="9b3a5-118">À partir du client Microsoft Teams, ouvrez l' **application Studio** et sélectionnez l’onglet **éditeur de manifeste** .</span><span class="sxs-lookup"><span data-stu-id="9b3a5-118">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="9b3a5-119">Si vous avez déjà créé votre package d’application dans l’application Studio, sélectionnez-le dans la liste.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-119">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="9b3a5-120">Si ce n’est pas le cas, vous pouvez importer un package d’application existant.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-120">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="9b3a5-121">Cliquez sur le bouton **Ajouter** dans la section commande.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-121">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="9b3a5-122">Choisissez **autoriser les utilisateurs à interroger votre service pour obtenir des informations et les insérer dans un message**.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-122">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
5. <span data-ttu-id="9b3a5-123">Ajoutez un **ID de commande** et un **titre**.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-123">Add a **Command Id** and a **Title**.</span></span>
6. <span data-ttu-id="9b3a5-124">Sélectionnez l’emplacement à partir duquel vous souhaitez déclencher la commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-124">Select where you want your search command to be triggered from.</span></span> <span data-ttu-id="9b3a5-125">La sélection de **message** ne modifie actuellement pas le comportement de votre commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-125">Selecting **message** does not currently alter the behavior of your search command.</span></span>
7. <span data-ttu-id="9b3a5-126">Ajoutez votre paramètre de recherche.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-126">Add your search parameter.</span></span>
8. <span data-ttu-id="9b3a5-127">Cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-127">Click Save.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="9b3a5-128">Créer manuellement une commande</span><span class="sxs-lookup"><span data-stu-id="9b3a5-128">Manually create a command</span></span>

<span data-ttu-id="9b3a5-129">Pour ajouter manuellement votre commande de recherche d’extension de messagerie à votre manifeste d’application, vous devez ajouter les paramètres follow `composeExtension.commands` à votre tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-129">To manually add your messaging extension search command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="9b3a5-130">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="9b3a5-130">Property name</span></span> | <span data-ttu-id="9b3a5-131">Objectif</span><span class="sxs-lookup"><span data-stu-id="9b3a5-131">Purpose</span></span> | <span data-ttu-id="9b3a5-132">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="9b3a5-132">Required?</span></span> | <span data-ttu-id="9b3a5-133">Version de manifeste minimale</span><span class="sxs-lookup"><span data-stu-id="9b3a5-133">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="9b3a5-134">ID unique que vous affectez à cette commande.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-134">Unique ID that you assign to this command.</span></span> <span data-ttu-id="9b3a5-135">La demande de l’utilisateur contiendra cet ID.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-135">The user request will include this ID.</span></span> | <span data-ttu-id="9b3a5-136">Oui</span><span class="sxs-lookup"><span data-stu-id="9b3a5-136">Yes</span></span> | <span data-ttu-id="9b3a5-137">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-137">1.0</span></span> |
| `title` | <span data-ttu-id="9b3a5-138">Nom de la commande.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-138">Command name.</span></span> <span data-ttu-id="9b3a5-139">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-139">This value appears in the UI.</span></span> | <span data-ttu-id="9b3a5-140">Oui</span><span class="sxs-lookup"><span data-stu-id="9b3a5-140">Yes</span></span> | <span data-ttu-id="9b3a5-141">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-141">1.0</span></span> |
| `description` | <span data-ttu-id="9b3a5-142">Texte d’aide indiquant la signification de cette commande.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-142">Help text indicating what this command does.</span></span> <span data-ttu-id="9b3a5-143">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-143">This value appears in the UI.</span></span> | <span data-ttu-id="9b3a5-144">Oui</span><span class="sxs-lookup"><span data-stu-id="9b3a5-144">Yes</span></span> | <span data-ttu-id="9b3a5-145">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-145">1.0</span></span> |
| `type` | <span data-ttu-id="9b3a5-146">Doivent être`query`</span><span class="sxs-lookup"><span data-stu-id="9b3a5-146">Must be `query`</span></span> | <span data-ttu-id="9b3a5-147">Non</span><span class="sxs-lookup"><span data-stu-id="9b3a5-147">No</span></span> | <span data-ttu-id="9b3a5-148">1.4</span><span class="sxs-lookup"><span data-stu-id="9b3a5-148">1.4</span></span> |
|`initialRun` | <span data-ttu-id="9b3a5-149">Si la valeur est définie sur **true**, cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-149">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="9b3a5-150">Non</span><span class="sxs-lookup"><span data-stu-id="9b3a5-150">No</span></span> | <span data-ttu-id="9b3a5-151">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-151">1.0</span></span> |
| `context` | <span data-ttu-id="9b3a5-152">Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-152">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="9b3a5-153">Les valeurs possibles `message`sont `compose`, ou `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-153">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="9b3a5-154">La valeur par défaut est `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-154">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="9b3a5-155">Non</span><span class="sxs-lookup"><span data-stu-id="9b3a5-155">No</span></span> | <span data-ttu-id="9b3a5-156">1,5</span><span class="sxs-lookup"><span data-stu-id="9b3a5-156">1.5</span></span> |

<span data-ttu-id="9b3a5-157">Vous devrez également ajouter les détails du paramètre de recherche, qui définira le texte visible par votre utilisateur dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-157">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="9b3a5-158">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="9b3a5-158">Property name</span></span> | <span data-ttu-id="9b3a5-159">Objectif</span><span class="sxs-lookup"><span data-stu-id="9b3a5-159">Purpose</span></span> | <span data-ttu-id="9b3a5-160">Obligatoire ?</span><span class="sxs-lookup"><span data-stu-id="9b3a5-160">Required?</span></span> | <span data-ttu-id="9b3a5-161">Version de manifeste minimale</span><span class="sxs-lookup"><span data-stu-id="9b3a5-161">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="9b3a5-162">Liste statique des paramètres de la commande.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-162">Static list of parameters for the command.</span></span> | <span data-ttu-id="9b3a5-163">Non</span><span class="sxs-lookup"><span data-stu-id="9b3a5-163">No</span></span> | <span data-ttu-id="9b3a5-164">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-164">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="9b3a5-165">Le nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-165">The name of the parameter.</span></span> <span data-ttu-id="9b3a5-166">Cette adresse est envoyée à votre service dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-166">This is sent to your service in the user request.</span></span> | <span data-ttu-id="9b3a5-167">Oui</span><span class="sxs-lookup"><span data-stu-id="9b3a5-167">Yes</span></span> | <span data-ttu-id="9b3a5-168">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-168">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="9b3a5-169">Décrit ce paramètre ou un exemple de la valeur qui doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-169">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="9b3a5-170">Cette valeur apparaît dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-170">This value appears in the UI.</span></span> | <span data-ttu-id="9b3a5-171">Oui</span><span class="sxs-lookup"><span data-stu-id="9b3a5-171">Yes</span></span> | <span data-ttu-id="9b3a5-172">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-172">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="9b3a5-173">Titre de paramètre court convivial ou étiquette.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-173">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="9b3a5-174">Oui</span><span class="sxs-lookup"><span data-stu-id="9b3a5-174">Yes</span></span> | <span data-ttu-id="9b3a5-175">1.0</span><span class="sxs-lookup"><span data-stu-id="9b3a5-175">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="9b3a5-176">Défini sur le type d’entrée requis.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-176">Set to the type of input required.</span></span> <span data-ttu-id="9b3a5-177">Les valeurs possibles `text`sont `textarea`, `number`, `date`, `time`, `toggle`et.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-177">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="9b3a5-178">La valeur par défaut est définie sur`text`</span><span class="sxs-lookup"><span data-stu-id="9b3a5-178">Default is set to `text`</span></span> | <span data-ttu-id="9b3a5-179">Non</span><span class="sxs-lookup"><span data-stu-id="9b3a5-179">No</span></span> | <span data-ttu-id="9b3a5-180">1.4</span><span class="sxs-lookup"><span data-stu-id="9b3a5-180">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="9b3a5-181">Exemple de manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="9b3a5-181">App manifest example</span></span>

<span data-ttu-id="9b3a5-182">Voici un exemple d’un `composeExtensions` objet qui définit une commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="9b3a5-182">The below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="9b3a5-183">Il ne s’agit pas d’un exemple du manifeste complet, pour le schéma de manifeste d’application complet, voir : [schéma de manifeste d’application](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9b3a5-183">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9b3a5-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b3a5-184">Next steps</span></span>

<span data-ttu-id="9b3a5-185">À présent que vous avez ajouté votre commande de recherche, vous devez [gérer la demande de recherche](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="9b3a5-185">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]