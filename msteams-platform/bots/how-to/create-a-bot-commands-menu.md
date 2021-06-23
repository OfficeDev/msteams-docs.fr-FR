---
title: Créer un menu de commandes pour votre bot
author: surbhigupta
description: Comment créer un menu de commandes pour votre bot Microsoft Teams de commande
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 0b8793666e6478e69698c355fb9209d2ca5f5d1e
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069000"
---
# <a name="bot-command-menus"></a><span data-ttu-id="b0b4e-103">Menus de commande du bot</span><span class="sxs-lookup"><span data-stu-id="b0b4e-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="b0b4e-104">Pour définir un ensemble de commandes principales à qui votre bot peut répondre, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-104">To define a set of core commands that your bot can respond to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="b0b4e-105">La liste des commandes est présentée aux utilisateurs dans la zone composer un message lorsqu’ils sont en conversation avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-105">The list of commands is presented to the users in the compose message area when they are in conversation with your bot.</span></span> <span data-ttu-id="b0b4e-106">Sélectionnez une commande dans la liste pour insérer la chaîne de commande dans la zone composer un message et sélectionnez **Envoyer.**</span><span class="sxs-lookup"><span data-stu-id="b0b4e-106">Select a command from the list to insert the command string into the compose message box and select **Send**.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b0b4e-107">Bureau</span><span class="sxs-lookup"><span data-stu-id="b0b4e-107">Desktop</span></span>](#tab/desktop)

![Menu de commande bot](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[<span data-ttu-id="b0b4e-109">Mobile</span><span class="sxs-lookup"><span data-stu-id="b0b4e-109">Mobile</span></span>](#tab/mobile)

![Menu de commande du bot mobile](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="b0b4e-111">Créer un menu de commandes pour votre bot</span><span class="sxs-lookup"><span data-stu-id="b0b4e-111">Create a command menu for your bot</span></span>

<span data-ttu-id="b0b4e-112">Les menus de commande sont définis dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-112">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="b0b4e-113">Vous pouvez utiliser **App Studio** pour les créer ou les ajouter manuellement dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-113">You can either use **App Studio** to create them or add them manually in the app manifest.</span></span>

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="b0b4e-114">Créer un menu de commandes pour votre bot à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="b0b4e-114">Create a command menu for your bot using App Studio</span></span>

<span data-ttu-id="b0b4e-115">Pour créer un menu de commandes pour votre bot, vous devez modifier un manifeste d’application existant.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-115">A prerequisite to create a command menu for your bot is that you must edit an existing app manifest.</span></span> <span data-ttu-id="b0b4e-116">Les étapes d’ajout d’un menu de commandes sont les mêmes, que vous créez un nouveau manifeste ou que vous en modifiiez un existant.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-116">The steps to add a command menu are the same, whether you create a new manifest or edit an existing one.</span></span>

<span data-ttu-id="b0b4e-117">**Pour créer un menu de commandes pour votre bot à l’aide d’App Studio**</span><span class="sxs-lookup"><span data-stu-id="b0b4e-117">**To create a command menu for your bot using App Studio**</span></span>

1. <span data-ttu-id="b0b4e-118">Ouvrez Teams sélectionnez **Applications** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-118">Open Teams and select **Apps** from the left pane.</span></span> <span data-ttu-id="b0b4e-119">Dans la page **Applications,** recherchez **App Studio,** puis sélectionnez **Ouvrir.**</span><span class="sxs-lookup"><span data-stu-id="b0b4e-119">In the **Apps** page, search for **App Studio**, and select **Open**.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="b0b4e-120">Si vous n’avez **pas App Studio,** vous pouvez le télécharger.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-120">If you do not have **App Studio**, you can download it.</span></span> <span data-ttu-id="b0b4e-121">Pour plus d’informations, [voir l’installation d’App Studio.](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)</span><span class="sxs-lookup"><span data-stu-id="b0b4e-121">For more information, see [installing App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="b0b4e-123">Dans **App Studio,** sélectionnez **l’onglet Éditeur de** manifeste. Si vous n’avez pas de package d’application existant, vous pouvez créer ou importer une application existante.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-123">In **App Studio**, select the **Manifest editor** tab. If you do not have an existing app package, you can create or import an existing app.</span></span> <span data-ttu-id="b0b4e-124">Pour plus d’informations, voir [mettre à jour un package d’application.](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)</span><span class="sxs-lookup"><span data-stu-id="b0b4e-124">For more information, see [update an app package](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span></span>

3. <span data-ttu-id="b0b4e-125">Dans le volet gauche de l’éditeur **de manifeste** et dans la **section** **Fonctionnalités,** sélectionnez Bots .</span><span class="sxs-lookup"><span data-stu-id="b0b4e-125">In the left pane of the **Manifest editor** and in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="b0b4e-126">Dans le volet droit de l’éditeur **de manifeste** et dans la section **Commandes,** sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-126">In the right pane of the **Manifest editor** and in the **Commands** section, select **Add**.</span></span> <span data-ttu-id="b0b4e-127">**L’écran Nouvelle commande** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-127">The **New Command** screen appears.</span></span>

    ![Bouton Ajouter du menu commandes App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="b0b4e-129">Entrez le **texte de commande** qui doit apparaître comme menu de commande pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-129">Enter the **Command text** that must appear as the command menu for your bot.</span></span>

6. <span data-ttu-id="b0b4e-130">Entrez le **texte d’aide** qui doit apparaître sous le texte de commande dans le menu.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-130">Enter the **Help text** that must appear under the command text in the menu.</span></span> <span data-ttu-id="b0b4e-131">**Le texte d’aide** doit être une brève explication de l’objectif de la commande.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-131">**Help text** must be a brief explanation of the purpose of the command.</span></span>

7. <span data-ttu-id="b0b4e-132">Cochez **les cases** d’étendue pour sélectionner l’endroit où ce menu de commande doit apparaître, puis sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="b0b4e-132">Select the **Scope** check boxes to select where this command menu must appear, and select **Save**.</span></span>

    ![Bouton de menu Nouvelles commandes App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="b0b4e-134">Créer un menu de commandes pour votre bot en le Manifest.jssur</span><span class="sxs-lookup"><span data-stu-id="b0b4e-134">Create a command menu for your bot by editing Manifest.json</span></span>

<span data-ttu-id="b0b4e-135">Une autre façon de créer un menu de commandes consiste à le créer directement dans le fichier manifeste lors du développement de votre code source de bot.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-135">Another way to create a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="b0b4e-136">Pour utiliser cette méthode, suivez les points ci-après :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-136">To use this method, follow these points:</span></span>

* <span data-ttu-id="b0b4e-137">Chaque menu prend en charge jusqu’à dix commandes.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-137">Each menu supports up to ten commands.</span></span>
* <span data-ttu-id="b0b4e-138">Créez un menu de commande unique qui fonctionne dans toutes les étendues.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-138">Create a single command menu that works in all scopes.</span></span>
* <span data-ttu-id="b0b4e-139">Créez un menu de commandes différent pour chaque étendue.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-139">Create a different command menu for each scope.</span></span>

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a><span data-ttu-id="b0b4e-140">Exemple de manifeste pour un menu unique pour les deux étendues</span><span class="sxs-lookup"><span data-stu-id="b0b4e-140">Manifest example for single menu for both scopes</span></span>

<span data-ttu-id="b0b4e-141">L’exemple de code de manifeste pour un menu unique pour les deux étendues est le suivant :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-141">The manifest example code for single menu for both scopes is as follows:</span></span>

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a><span data-ttu-id="b0b4e-142">Exemple de manifeste pour le menu pour chaque étendue</span><span class="sxs-lookup"><span data-stu-id="b0b4e-142">Manifest example for the menu for each scope</span></span>

<span data-ttu-id="b0b4e-143">L’exemple de code de manifeste pour le menu pour chaque étendue est le suivant :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-143">The manifest example code for the menu for each scope is as follows:</span></span>

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

<span data-ttu-id="b0b4e-144">Vous devez gérer les commandes de menu dans le code de votre bot lorsque vous traitez les messages des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-144">You must handle menu commands in your bot code as you handle any message from users.</span></span> <span data-ttu-id="b0b4e-145">Vous pouvez gérer les commandes de menu dans le code de votre bot en parant la **\@ partie Mention** du texte du message.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-145">You can handle menu commands in your bot code by parsing out the **\@Mention** portion of the message text.</span></span>

## <a name="handle-menu-commands-in-your-bot-code"></a><span data-ttu-id="b0b4e-146">Gérer les commandes de menu dans le code de votre bot</span><span class="sxs-lookup"><span data-stu-id="b0b4e-146">Handle menu commands in your bot code</span></span>

<span data-ttu-id="b0b4e-147">Les bots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés `@botname` dans un message.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-147">Bots in a group or channel respond only when they are mentioned `@botname` in a message.</span></span> <span data-ttu-id="b0b4e-148">Chaque message reçu par un bot dans une étendue de groupe ou de canal contient son nom dans le texte du message renvoyé.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-148">Every message received by a bot when in a group or channel scope contains its name in the message text returned.</span></span> <span data-ttu-id="b0b4e-149">Avant de gérer la commande renvoyée, l’utilisation de votre message doit gérer le message reçu par un bot avec son nom.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-149">Before handling the command being returned, your message parsing must handle the message received by a bot with its name.</span></span>

> [!NOTE]
> <span data-ttu-id="b0b4e-150">Pour gérer les commandes dans le code, elles sont envoyées à votre bot en tant que message normal.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-150">To handle the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="b0b4e-151">Vous devez les gérer comme vous le feriez pour tout autre message de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-151">You must handle them as you would handle any other message from your users.</span></span> <span data-ttu-id="b0b4e-152">Les commandes du code insèrent du texte pré-configuré dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-152">The commands in code insert pre-configured text into the text box.</span></span> <span data-ttu-id="b0b4e-153">L’utilisateur doit ensuite envoyer ce texte comme il le fait pour tout autre message.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-153">The user must then send that text as they do for any other message.</span></span>

# <a name="c"></a>[<span data-ttu-id="b0b4e-154">C#</span><span class="sxs-lookup"><span data-stu-id="b0b4e-154">C#</span></span>](#tab/dotnet)

<span data-ttu-id="b0b4e-155">Vous pouvez analyser la **\@ partie Mention** du texte du message à l’aide d’une méthode statique fournie avec le Microsoft Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-155">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework.</span></span> <span data-ttu-id="b0b4e-156">Il s’agit d’une méthode de `Activity` la classe nommée `RemoveRecipientMention` .</span><span class="sxs-lookup"><span data-stu-id="b0b4e-156">It is a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

<span data-ttu-id="b0b4e-157">Le C# code pour l’utilisation de la partie **\@ Mention** du texte du message est le suivant :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-157">The C# code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[<span data-ttu-id="b0b4e-158">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0b4e-158">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="b0b4e-159">Vous pouvez analyser la **\@ partie Mention** du texte du message à l’aide d’une méthode statique fournie avec Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-159">You can parse out the **\@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="b0b4e-160">Il s’agit d’une méthode de `TurnContext` la classe nommée `removeMentionText` .</span><span class="sxs-lookup"><span data-stu-id="b0b4e-160">It is a method of the `TurnContext` class named `removeMentionText`.</span></span>

<span data-ttu-id="b0b4e-161">Le code JavaScript pour l’utilisation de la **\@ partie Mention** du texte du message est le suivant :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-161">The JavaScript code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="b0b4e-162">Python</span><span class="sxs-lookup"><span data-stu-id="b0b4e-162">Python</span></span>](#tab/python)

<span data-ttu-id="b0b4e-163">Vous pouvez l'@Mention **partie** du texte du message à l’aide d’une méthode statique fournie avec Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-163">You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="b0b4e-164">Il s’agit d’une méthode de `TurnContext` la classe nommée `remove_recipient_mention` .</span><span class="sxs-lookup"><span data-stu-id="b0b4e-164">It is a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

<span data-ttu-id="b0b4e-165">Le code Python pour l’extrait de la **\@ partie Mention** du texte du message est le suivant :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-165">The Python code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

<span data-ttu-id="b0b4e-166">Pour activer le bon fonctionnement de votre code bot, vous devez suivre quelques meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-166">To enable smooth functioning of your bot code, there are few best practices that you must follow.</span></span>

## <a name="command-menu-best-practices"></a><span data-ttu-id="b0b4e-167">Meilleures pratiques en matière de menu de commandes</span><span class="sxs-lookup"><span data-stu-id="b0b4e-167">Command menu best practices</span></span>

<span data-ttu-id="b0b4e-168">Voici les meilleures pratiques en matière de menu de commandes :</span><span class="sxs-lookup"><span data-stu-id="b0b4e-168">Following are the command menu best practices:</span></span>

* <span data-ttu-id="b0b4e-169">Restez simple : le menu bot est destiné à présenter les fonctionnalités clés de votre bot.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-169">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="b0b4e-170">Restez bref : les options de menu ne doivent pas être longues et ne doivent pas être des instructions de langage naturel complexes.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-170">Keep it short: Menu options must not be long and must not be complex natural language statements.</span></span> <span data-ttu-id="b0b4e-171">Ce doivent être des commandes simples.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-171">They must be simple commands.</span></span>
* <span data-ttu-id="b0b4e-172">Restez invocable : les commandes ou les actions de menu bot doivent toujours être disponibles, quel que soit l’état de la conversation ou la boîte de dialogue dans le bot.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-172">Keep it invokable: Bot menu actions or commands must always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> [!NOTE]
> <span data-ttu-id="b0b4e-173">Si vous supprimez des commandes de votre manifeste, vous devez redéployer votre application pour implémenter les modifications.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-173">If you remove any commands from your manifest, you must redeploy your app to implement the changes.</span></span> <span data-ttu-id="b0b4e-174">En règle générale, les modifications apportées au manifeste vous obligent à redéployer votre application.</span><span class="sxs-lookup"><span data-stu-id="b0b4e-174">In general, any changes to the manifest require you to redeploy your app.</span></span>

## <a name="next-step"></a><span data-ttu-id="b0b4e-175">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b0b4e-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b0b4e-176">Conversations de groupe et de canal</span><span class="sxs-lookup"><span data-stu-id="b0b4e-176">Channel and group conversations</span></span>](~/bots/how-to/conversations/channel-and-group-conversations.md)
