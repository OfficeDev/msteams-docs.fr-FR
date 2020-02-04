---
title: Créer un menu de commandes pour votre robot
author: clearab
description: Procédure de création d’un menu de commandes pour votre robot Microsoft teams
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: 81efb94fc882aa4653ab162863d5d973aeae87b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673678"
---
# <a name="bot-command-menus"></a><span data-ttu-id="9e2e4-103">Menus de la commande bot</span><span class="sxs-lookup"><span data-stu-id="9e2e4-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="9e2e4-104">Les menus de bot n’apparaissent pas sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-104">Bot menus won't appear on mobile clients.</span></span>

<span data-ttu-id="9e2e4-105">Add Command menu for your bot vous permet de définir un ensemble de commandes clés auxquelles votre bot peut toujours répondre.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-105">Add command menu for your bot allows you to define a set of core commands your bot can always respond to.</span></span> <span data-ttu-id="9e2e4-106">La liste des commandes est présentée à l’utilisateur au-dessus de la zone de message de composition lorsqu’ils contournent votre robot.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-106">The list of commands is presented to the user above the compose message area when they are conversing with your bot.</span></span> <span data-ttu-id="9e2e4-107">La sélection d’une commande dans la liste entraîne l’insertion de la chaîne de commande dans la boîte de message de composition, puis tous les utilisateurs ont besoin de l’option **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-107">Selecting a command from the list will insert the command string into the compose message box, then all users need to do is select **Send**.</span></span>

![Menu de commandes bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="9e2e4-109">Créer un menu de commandes pour votre robot</span><span class="sxs-lookup"><span data-stu-id="9e2e4-109">Create a command menu for your bot</span></span>

<span data-ttu-id="9e2e4-110">Les menus de commandes sont définis dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="9e2e4-111">Vous pouvez utiliser app Studio pour vous aider à les créer ou les ajouter manuellement.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-111">You can either use App Studio to help you create them, or add them manually.</span></span>

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="9e2e4-112">Création d’un menu de commandes pour votre bot à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="9e2e4-112">Creating a command menu for your bot using App Studio</span></span>

<span data-ttu-id="9e2e4-113">Les instructions fournies ici supposent que vous modifiez un manifeste d’application existant.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-113">The instructions here assume that you'll be editing an existing app manifest.</span></span> <span data-ttu-id="9e2e4-114">Les étapes d’ajout d’un menu de commandes sont les mêmes, que vous soyez en train de créer un nouveau manifeste ou d’en modifier un existant.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-114">The steps for adding a command menu are the same, whether you're creating a new manifest or editing an existing one.</span></span>

1. <span data-ttu-id="9e2e4-115">Ouvrez l’application Studio à partir du... menu débordement sur le rail de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-115">Open App Studio from the ... overflow menu on the left navigation rail.</span></span> <span data-ttu-id="9e2e4-116">Si vous n’avez pas disponible App Studio, vous pouvez le télécharger.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-116">If you don't have App Studio available you can download it.</span></span> <span data-ttu-id="9e2e4-117">Pour plus d’informations sur l’utilisation d’App Studio, voir [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) .</span><span class="sxs-lookup"><span data-stu-id="9e2e4-117">See [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) for more information on using App Studio.</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="9e2e4-119">Une fois dans App Studio, sélectionnez l’onglet **éditeur de manifeste** .</span><span class="sxs-lookup"><span data-stu-id="9e2e4-119">Once in App Studio, select the **Manifest editor** tab.</span></span>

3. <span data-ttu-id="9e2e4-120">Dans la colonne de gauche de la vue de l’éditeur de manifeste dans la section **fonctionnalités** , sélectionnez **bots**.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-120">In the left column of the manifest editor view in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="9e2e4-121">Dans la colonne de droite de la vue de l’éditeur de manifeste dans la section **commandes** , cliquez sur le bouton **Ajouter** .</span><span class="sxs-lookup"><span data-stu-id="9e2e4-121">In the right column of the manifest editor view in the **Commands** section, select the **Add** button.</span></span>

    ![Bouton Ajouter du menu de commandes d’App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="9e2e4-123">L’écran **nouvelle commande** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-123">The **New Command** screen appears.</span></span> <span data-ttu-id="9e2e4-124">Entrez le **texte de commande** qui doit apparaître en tant que commande de menu, ainsi que le **texte d’aide** qui doit apparaître directement sous le texte de commande dans le menu.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-124">Enter the **Command text** that you want to have appear as the menu command, and the **Help text** that you want to have appear directly under the command text in the menu.</span></span> <span data-ttu-id="9e2e4-125">Cela doit être une brève explication de l’objectif de la commande.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-125">This should be a brief explanation of the purpose of the command.</span></span>

6. <span data-ttu-id="9e2e4-126">Ensuite, sélectionnez la ou les étendues dans lesquelles vous souhaitez que ce menu de commandes s’affiche, puis cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9e2e4-126">Next, select the scope(s) where you want this command menu to appear, then select the **Save** button.</span></span>

    ![Bouton Ajouter du menu de commandes d’App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="9e2e4-128">Création d’un menu de commandes pour votre bot en modifiant **Manifest. JSON**</span><span class="sxs-lookup"><span data-stu-id="9e2e4-128">Creating a command menu for your bot by editing **Manifest.json**</span></span>

<span data-ttu-id="9e2e4-129">Une autre approche valide pour la création d’un menu de commandes consiste à le créer directement dans le fichier manifeste lors du développement du code source de votre robot.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-129">Another valid approach for creating a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="9e2e4-130">Voici quelques éléments à garder à l’esprit lors de l’utilisation de cette approche :</span><span class="sxs-lookup"><span data-stu-id="9e2e4-130">Here are a few things to keep in mind when using this approach:</span></span>

1. <span data-ttu-id="9e2e4-131">Chaque menu prend en charge jusqu’à 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-131">Each menu supports up to 10 commands.</span></span>

2. <span data-ttu-id="9e2e4-132">Vous pouvez créer un seul menu de commandes qui fonctionne dans toutes les étendues.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-132">You can create a single command menu that will work in all scopes.</span></span>

3. <span data-ttu-id="9e2e4-133">Vous pouvez créer un autre menu de commandes pour chaque étendue</span><span class="sxs-lookup"><span data-stu-id="9e2e4-133">You can create a different command menu for each scope</span></span>

#### <a name="manifest-example---single-menu-for-both-scopes"></a><span data-ttu-id="9e2e4-134">Exemple de manifeste-menu unique pour les deux étendues</span><span class="sxs-lookup"><span data-stu-id="9e2e4-134">Manifest example - single menu for both scopes</span></span>

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

#### <a name="manifest-example---menu-for-each-scope"></a><span data-ttu-id="9e2e4-135">Exemple de manifeste-menu pour chaque étendue</span><span class="sxs-lookup"><span data-stu-id="9e2e4-135">Manifest example - menu for each scope</span></span>

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

## <a name="handling-menu-commands-in-your-bot-code"></a><span data-ttu-id="9e2e4-136">Gestion des commandes de menu dans votre code de robot</span><span class="sxs-lookup"><span data-stu-id="9e2e4-136">Handling menu commands in your bot code</span></span>

<span data-ttu-id="9e2e4-137">Les robots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés (« @botname ») dans un message.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-137">Bots in a group or channel respond only when they are mentioned ("@botname") in a message.</span></span> <span data-ttu-id="9e2e4-138">Par conséquent, chaque message reçu par un bot dans une étendue de groupe ou de canal contiendra son propre nom dans le texte du message renvoyé.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-138">As a result, every message received by a bot when in a group or channel scope will contain its own name in the message text returned.</span></span> <span data-ttu-id="9e2e4-139">Vous devez veiller à ce que les handles d’analyse de messages qui précèdent la commande renvoyée soient pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-139">You need to ensure your message parsing handles that before handling the command being returned.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9e2e4-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9e2e4-140">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="9e2e4-141">Vous pouvez analyser la `Activity` `RemoveRecipientMention` \*\* \@partie mention\*\* du texte du message à l’aide d’une méthode statique fournie avec Microsoft bot Framework, une méthode de la classe nommée.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-141">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="9e2e4-142">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="9e2e4-142">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9e2e4-143">Vous pouvez analyser la `TurnContext` `removeMentionText` \*\* \@partie mention\*\* du texte du message à l’aide d’une méthode statique fournie avec Microsoft bot Framework, une méthode de la classe nommée.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-143">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `removeMentionText`.</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="9e2e4-144">Python</span><span class="sxs-lookup"><span data-stu-id="9e2e4-144">Python</span></span>](#tab/python)


<span data-ttu-id="9e2e4-145">Vous pouvez analyser la partie **@Mention** du texte du message à l’aide d’une méthode statique fournie avec Microsoft bot Framework, une méthode de `TurnContext` la classe `remove_recipient_mention`nommée.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-145">You can parse out the **@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a><span data-ttu-id="9e2e4-146">Meilleures pratiques du menu de commandes</span><span class="sxs-lookup"><span data-stu-id="9e2e4-146">Command menu best practices</span></span>

* <span data-ttu-id="9e2e4-147">**Restez simple**: le menu robot est conçu pour présenter les fonctionnalités clés de votre bot.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-147">**Keep it simple**: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="9e2e4-148">**Maintenez-le court**: les options de menu ne doivent pas être extrêmement longues et les instructions complexes en langage naturel : elles doivent être des commandes simples.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-148">**Keep it short**: Menu options shouldn’t be extremely long and complex natural language statements — they should be simple commands.</span></span>
* <span data-ttu-id="9e2e4-149">**Conservez-le invokable**: les actions/commandes du menu bot doivent toujours être disponibles, quel que soit l’état de la conversation ou la boîte de dialogue dans laquelle se trouve le robot.</span><span class="sxs-lookup"><span data-stu-id="9e2e4-149">**Keep it invokable**: Bot menu actions/commands should always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>
