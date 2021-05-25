---
title: Conception de votre bot
description: Découvrez comment concevoir un bot Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98e36bf55e61ef59261959021409d9e60d8542f5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630083"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="fbfd8-103">Conception de votre bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fbfd8-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="fbfd8-104">Les bots sont des applications de conversation qui effectuent un ensemble spécifique de tâches.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="fbfd8-105">Basés sur <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, les bots communiquent avec les utilisateurs, répondent à leurs questions et informent les utilisateurs de façon proactive en cas de modifications et d’autres événements.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="fbfd8-106">C’est un excellent moyen de les joindre.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-106">They're a great way to reach out.</span></span>

<span data-ttu-id="fbfd8-107">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des bots dans Teams.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="fbfd8-108">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fbfd8-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="fbfd8-109">Vous trouverez des instructions plus détaillées sur la conception du bot, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbfd8-110">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="fbfd8-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="fbfd8-111">Ajouter un bot</span><span class="sxs-lookup"><span data-stu-id="fbfd8-111">Add a bot</span></span>

<span data-ttu-id="fbfd8-112">Les bots sont disponibles dans les conversations, les canaux et les applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-112">Bots are available in chats, channels, and personal apps.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-113">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-113">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="fbfd8-114">Les utilisateurs peuvent ajouter un bot de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbfd8-114">Users can add a bot one of the following ways:</span></span>

* <span data-ttu-id="fbfd8-115">À partir du magasin Teams de données.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-115">From the Teams store.</span></span>
* <span data-ttu-id="fbfd8-116">Utilisez le menu volant de l’application en sélectionnant l’icône **Plus** sur le côté gauche de Teams.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-116">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="fbfd8-117">Avec un @mention dans la nouvelle conversation ou zone de rédaction (l’exemple suivant montre comment faire dans une conversation de groupe).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-117">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="L’exemple montre comment ajouter un bot dans une conversation de groupe à l’aide de @mention." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-119">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-119">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="fbfd8-120">Les utilisateurs peuvent accéder aux bots qui ont été ajoutés sur le bureau à l'@mention.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-120">Users can access bots that were added on desktop with an @mention.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="L’exemple montre comment accéder à un bot mobile dans une conversation de groupe à l’aide d’une @mention." border="false":::

---

## <a name="introduce-a-bot"></a><span data-ttu-id="fbfd8-122">Présentation d’un bot</span><span class="sxs-lookup"><span data-stu-id="fbfd8-122">Introduce a bot</span></span>

<span data-ttu-id="fbfd8-123">Il est essentiel que votre bot se présente et décrive ce qu'il peut faire.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-123">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="fbfd8-124">Cet échange initial permet aux utilisateurs de comprendre ce qu’il faut faire avec le bot, de connaître ses limites et, surtout, de se mettre à l’interaction avec.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-124">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="fbfd8-125">Message de bienvenue dans une conversation à deux</span><span class="sxs-lookup"><span data-stu-id="fbfd8-125">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="fbfd8-126">En contexte personnel, les messages d’accueil définissent le ton de votre bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-126">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="fbfd8-127">Le message inclut un message d’accueil, ce que le bot peut faire et quelques suggestions pour l’interaction.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-127">The message includes a greeting, what the bot can do, and some suggestions for how to interact.</span></span> <span data-ttu-id="fbfd8-128">Par exemple, « Essayez de me demander ... ».</span><span class="sxs-lookup"><span data-stu-id="fbfd8-128">For example, “Try asking me about …”.</span></span> <span data-ttu-id="fbfd8-129">Si possible, ces suggestions doivent renvoyer les réponses stockées sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-129">If possible, these suggestions should return stored responses without having to sign in.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-130">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-130">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="L'exemple montre l'introduction d'un bot dans une application personnelle." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-132">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-132">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="Exemple d’introduction d’un bot dans une application personnelle sur un appareil mobile." border="false":::

---

### <a name="welcome-message-in-channels-and-group-chats"></a><span data-ttu-id="fbfd8-134">Message de bienvenue dans les canaux et les conversations de groupe</span><span class="sxs-lookup"><span data-stu-id="fbfd8-134">Welcome message in channels and group chats</span></span>

<span data-ttu-id="fbfd8-135">L’introduction de votre bot doit être légèrement différente dans les canaux et les conversations de groupe par rapport à un espace personnel (comme une application personnelle).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-135">Your bot's introduction should be slightly different in channels and group chats compared to a personal space (like a personal app).</span></span> <span data-ttu-id="fbfd8-136">Dans la vie réelle, si vous entrez dans une salle pleine de gens, vous vous présenterez au lieu de souhaiter la bienvenue à tous ceux qui sont déjà là.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-136">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="fbfd8-137">Portez cette réflexion dans votre conception bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-137">Carry that thinking into your bot design.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-138">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-138">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="L'exemple montre l'introduction d'un bot dans un contexte de collaboration." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-140">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-140">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="Exemple d’introduction d’un bot dans un contexte de collaboration sur mobile." border="false":::

---

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="fbfd8-142">Authentification bot avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="fbfd8-142">Bot authentication with single sign-on</span></span>

<span data-ttu-id="fbfd8-143">Lorsqu'une personne envoie un message à un bot, il peut être nécessaire de se connecter pour utiliser toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-143">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="fbfd8-144">Vous pouvez simplifier le processus d'authentification à l'aide de l'authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-144">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="fbfd8-145">N’oubliez pas : dans le menu de commandes du bot (**Que puis-je faire ?**), vous devez également fournir une commande pour vous sortir.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-145">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-146">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="L'exemple montre un bot avec un bouton de connexion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-148">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="L’exemple montre un bot avec un bouton de sign-in sur mobile." border="false":::

---

### <a name="tours"></a><span data-ttu-id="fbfd8-150">Visites guidées</span><span class="sxs-lookup"><span data-stu-id="fbfd8-150">Tours</span></span>

<span data-ttu-id="fbfd8-151">Vous pouvez inclure une visite guidée avec des messages d’accueil et si le bot répond à une commande telle qu’une « aide ».</span><span class="sxs-lookup"><span data-stu-id="fbfd8-151">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="fbfd8-152">Une visite guidée est le moyen le plus efficace de décrire ce que peut faire votre bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-152">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="fbfd8-153">Le cas échéant, ils sont également parfaits pour décrire les autres fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-153">If applicable, they’re also great for describing your app’s other features.</span></span> <span data-ttu-id="fbfd8-154">Par exemple, incluez des captures d’écran de votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-154">For example, include screenshots of your messaging extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbfd8-155">Les visites guidées doivent être accessibles sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-155">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="fbfd8-156">Conversations à deux</span><span class="sxs-lookup"><span data-stu-id="fbfd8-156">One-on-one chats</span></span>

<span data-ttu-id="fbfd8-157">Dans une application personnelle, un carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-157">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="fbfd8-158">Il est vivement encouragé d’inclure des boutons pour que les utilisateurs essaient les commandes de bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-158">Including buttons the let users try bot commands is encouraged.</span></span> <span data-ttu-id="fbfd8-159">Par exemple, **créez une tâche.**</span><span class="sxs-lookup"><span data-stu-id="fbfd8-159">For example, **Create a task**.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-160">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-160">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="L'exemple montre une visite guidée d'un bot dans une conversation à deux." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-162">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-162">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="Exemple d’une visite guidée de bot dans une conversation un-à-un sur mobile." border="false":::

---

#### <a name="channels-and-group-chats"></a><span data-ttu-id="fbfd8-164">Canaux et conversations de groupe</span><span class="sxs-lookup"><span data-stu-id="fbfd8-164">Channels and group chats</span></span>

<span data-ttu-id="fbfd8-165">Dans les canaux et conversations de groupe, une visite guidée doit s’ouvrir dans un modal (également appelé [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) de sorte qu’elle n’interrompe pas les conversations en cours.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-165">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="fbfd8-166">Cela vous permet également d’implémenter des affichages basés sur les rôles pour votre visite guidée.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-166">This also gives you the option to implement role-based views for your tour.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-167">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-167">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="L'exemple montre une visite guidée d'un bot dans un canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-169">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-169">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="Exemple de visite guidée d’un bot dans un canal mobile." border="false":::

---

## <a name="chat-with-a-bot"></a><span data-ttu-id="fbfd8-171">Discuter avec un robot</span><span class="sxs-lookup"><span data-stu-id="fbfd8-171">Chat with a bot</span></span>

<span data-ttu-id="fbfd8-172">Les bots s’intègrent directement dans l’infrastructure de messagerie de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-172">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="fbfd8-173">Les utilisateurs peuvent discuter avec un bot pour trouver une réponse à leurs questions ou taper des commandes pour que le bot effectue un ensemble de tâches étroit ou spécifique.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-173">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="fbfd8-174">Les bots peuvent informer les utilisateurs des modifications ou mises à jour apportées à votre application par conversation instantanée.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-174">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="fbfd8-175">Discuter avec un bot dans différents contextes</span><span class="sxs-lookup"><span data-stu-id="fbfd8-175">Chat with a bot in different contexts</span></span>

<span data-ttu-id="fbfd8-176">Vous pouvez utiliser des bots dans les contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="fbfd8-176">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="fbfd8-177">**Applications personnelles** : dans une application personnelle, un bot possède un onglet de conversation dédié.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-177">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="fbfd8-178">**Conversation à deux** : un utilisateur peut démarrer une conversation privée avec un bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-178">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="fbfd8-179">C’est la même expérience que l’utilisation d’un bot dans une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-179">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="fbfd8-180">**Conversation de groupe** : les utilisateurs peuvent interagir avec un bot dans une conversation de groupe en @mentionnant le bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-180">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="fbfd8-181">**Canal** : les utilisateurs peuvent interagir avec un bot dans un canal.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-181">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="fbfd8-182">en @mentionnant nom du bot dans la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-182">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="fbfd8-183">N’oubliez pas que, dans ce contexte, le bot est disponible pour l’ensemble de l’équipe, pas seulement pour le canal.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-183">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="fbfd8-184">Anatomie</span><span class="sxs-lookup"><span data-stu-id="fbfd8-184">Anatomy</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-185">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-185">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="L’exemple montre la forme structurelle d’un bot." border="false":::

|<span data-ttu-id="fbfd8-187">Compteur</span><span class="sxs-lookup"><span data-stu-id="fbfd8-187">Counter</span></span>|<span data-ttu-id="fbfd8-188">Description</span><span class="sxs-lookup"><span data-stu-id="fbfd8-188">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fbfd8-189">1</span><span class="sxs-lookup"><span data-stu-id="fbfd8-189">1</span></span>|<span data-ttu-id="fbfd8-190">**Nom et icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="fbfd8-190">**App name and icon**</span></span>|
|<span data-ttu-id="fbfd8-191">2</span><span class="sxs-lookup"><span data-stu-id="fbfd8-191">2</span></span>|<span data-ttu-id="fbfd8-192">**Onglet Conversation** : ouvre l’espace pour discuter avec votre bot (applicable uniquement aux applications personnelles).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-192">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="fbfd8-193">3</span><span class="sxs-lookup"><span data-stu-id="fbfd8-193">3</span></span>|<span data-ttu-id="fbfd8-194">**Onglets Personnalisé** : ouvre le contenu lié à votre application.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-194">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="fbfd8-195">4 </span><span class="sxs-lookup"><span data-stu-id="fbfd8-195">4</span></span>|<span data-ttu-id="fbfd8-196">**Onglet À propos** : affiche des informations de base sur votre application.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-196">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="fbfd8-197">5 </span><span class="sxs-lookup"><span data-stu-id="fbfd8-197">5</span></span>|<span data-ttu-id="fbfd8-198">**Bulle de conversation** : les conversations bot utilisent le cadre de stratégie de messagerie Teams.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-198">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="fbfd8-199">6 </span><span class="sxs-lookup"><span data-stu-id="fbfd8-199">6</span></span>|<span data-ttu-id="fbfd8-200">**Carte adaptative**: si les réponses de votre bot incluent des cartes adaptatives, la carte prend toute la largeur de la bulle de conversation.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-200">**Adaptive Card**: If your bot's responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="fbfd8-201">7 </span><span class="sxs-lookup"><span data-stu-id="fbfd8-201">7</span></span>|<span data-ttu-id="fbfd8-202">**Menu de commandes** : affiche les commandes standard de votre bot (définies par vous).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-202">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-203">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-203">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un bot mobile." border="false":::

|<span data-ttu-id="fbfd8-205">Compteur</span><span class="sxs-lookup"><span data-stu-id="fbfd8-205">Counter</span></span>|<span data-ttu-id="fbfd8-206">Description</span><span class="sxs-lookup"><span data-stu-id="fbfd8-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fbfd8-207">1</span><span class="sxs-lookup"><span data-stu-id="fbfd8-207">1</span></span>|<span data-ttu-id="fbfd8-208">**Nom et icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="fbfd8-208">**App name and icon**</span></span>|
|<span data-ttu-id="fbfd8-209">2</span><span class="sxs-lookup"><span data-stu-id="fbfd8-209">2</span></span>|<span data-ttu-id="fbfd8-210">**Onglet Conversation** : ouvre l’espace pour discuter avec votre bot (applicable uniquement aux applications personnelles).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-210">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="fbfd8-211">3</span><span class="sxs-lookup"><span data-stu-id="fbfd8-211">3</span></span>|<span data-ttu-id="fbfd8-212">**Onglets Personnalisé** : ouvre le contenu lié à votre application.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-212">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="fbfd8-213">4 </span><span class="sxs-lookup"><span data-stu-id="fbfd8-213">4</span></span>|<span data-ttu-id="fbfd8-214">**Bulle de conversation** : les conversations bot utilisent le cadre de stratégie de messagerie Teams.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-214">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="fbfd8-215">5 </span><span class="sxs-lookup"><span data-stu-id="fbfd8-215">5</span></span>|<span data-ttu-id="fbfd8-216">**Carte adaptative**: si les réponses de votre bot incluent des cartes adaptatives, la carte prend toute la largeur de la bulle de conversation.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-216">**Adaptive Card**: If your bot's responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|

---

### <a name="command-menu"></a><span data-ttu-id="fbfd8-217">Menu de commandes</span><span class="sxs-lookup"><span data-stu-id="fbfd8-217">Command menu</span></span>

<span data-ttu-id="fbfd8-218">Le menu de commandes fournit la liste des mots ou phrases à qui votre robot doit toujours répondre.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-218">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="fbfd8-219">Le menu de commande s'affiche au-dessus de la zone de rédaction lorsqu'une personne converse avec un bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-219">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="fbfd8-220">Lorsqu’une commande est sélectionnée, elle est insérée dans un message.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-220">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="fbfd8-221">La liste des commandes doit être brève.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-221">The list of commands should be brief.</span></span> <span data-ttu-id="fbfd8-222">Le menu est destiné à mettre en évidence les principales fonctionnalités de votre bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-222">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="fbfd8-223">Gardez également les commandes concises.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-223">Keep commands concise, too.</span></span> <span data-ttu-id="fbfd8-224">Par exemple, vous pouvez créer une commande appelée **Aide** au lieu d’une commande **Pouvez-vous m’aider** ?</span><span class="sxs-lookup"><span data-stu-id="fbfd8-224">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="fbfd8-225">Le menu de commandes doit toujours être disponible quel que soit l’état de la conversation.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-225">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="L'exemple montre le menu de commandes d'un bot." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="fbfd8-227">Comprendre ce que les gens disent</span><span class="sxs-lookup"><span data-stu-id="fbfd8-227">Understand what people are saying</span></span>

<span data-ttu-id="fbfd8-228">Utilisez un dictionnaire des synonymes et demandez à des personnes issues d'horizons aussi différents que possible de vous aider à générer différentes interprétations de requêtes standard.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-228">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Illustration montrant comment un bot peut interpréter « Bonjour »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Illustration montrant comment un bot peut interpréter « Aide »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Illustration montrant comment un bot peut interpréter « Merci »." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="fbfd8-232">Extraire l’intention et les données des messages</span><span class="sxs-lookup"><span data-stu-id="fbfd8-232">Extract intent and data from messages</span></span>

<span data-ttu-id="fbfd8-233">Concevez votre bot pour reconnaître l'intention, c'est-à-dire ce que quelqu'un attend d'un bot en réponse à un message ou une requête.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-233">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="fbfd8-234">L'intention classe un message ou une requête comme une action unique avec un ou plusieurs objets de données affectés par l'action.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-234">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="fbfd8-235">Les exemples suivants décrivent l’intention et les données de l’utilisateur dans les messages envoyés aux bots :</span><span class="sxs-lookup"><span data-stu-id="fbfd8-235">The following examples outline the user intent and data in messages sent to bots:</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Exemple montrant que dans la phrase « Réserver un vol pour Seattle », l’intention de l’utilisateur est « réserver un vol » et les données sont « Seattle »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Exemple montrant que dans la phrase « Quand le magasin est-il ouvert » l’intention de l’utilisateur est « quand » et les données sont « ouvert »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Exemple montrant que dans la phrase « Planifier une réunion à 13h avec Bob dans Distribution », l’intention de l’utilisateur est « planifier une réunion » et les données sont « 13h » et « Bob dans Distribution »." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="fbfd8-239">Analyser et améliorer</span><span class="sxs-lookup"><span data-stu-id="fbfd8-239">Analyze and improve</span></span>

<span data-ttu-id="fbfd8-240">Découvrez les dires des utilisateurs en discutant avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-240">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="fbfd8-241">Il s’agit d’un processus itératif continu à mesure que votre base d’utilisateurs s’agrandit à différents emplacements et organisation.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-241">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="fbfd8-242">Vous pouvez affiner la reconnaissance linguistique et le mappage d’intention de votre bot avec Microsoft Language Understanding (LUIS).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-242">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="fbfd8-243">[Comprendre LUIS](/azure/cognitive-services/luis/artificial-intelligence) : découvrez comment LUIS utilise l’intelligence artificielle pour fournir une compréhension du langage naturel (NLU) aux données de votre application.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-243">[Understanding LUIS](/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="fbfd8-244">[Intégration à LUIS](https://www.luis.ai/) : ajoutez des fonctionnalités de langage naturel à votre bot sans le processus complexe de création de modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-244">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="fbfd8-245">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="fbfd8-245">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="fbfd8-246">Requêtes simples</span><span class="sxs-lookup"><span data-stu-id="fbfd8-246">Simple queries</span></span>

<span data-ttu-id="fbfd8-247">Les bots peuvent fournir une correspondance exacte à une requête ou à un groupe de correspondances associées pour vous aider à mettre fin à l’ambiguïté.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-247">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="fbfd8-248">Pour les correspondances associées, groupez le contenu à l’aide d’une carte de liste.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-248">For related matches, group the content using a list card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-249">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-249">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="L'exemple montre une interaction de requête simple avec un bot." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-251">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-251">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="L’exemple illustre une interaction de requête simple avec un bot sur un appareil mobile." border="false":::

---

### <a name="multi-turn-interactions"></a><span data-ttu-id="fbfd8-253">Interactions à plusieurs tour</span><span class="sxs-lookup"><span data-stu-id="fbfd8-253">Multi-turn interactions</span></span>

<span data-ttu-id="fbfd8-254">Si votre bot peut prendre en charge les demandes complètes et les questions, il doit également être en mesure de gérer les interactions à plusieurs tour.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-254">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="fbfd8-255">L'anticipation des étapes suivantes possibles permet aux personnes d'effectuer un flux de tâches plus facilement (plutôt que d'attendre d'elles qu'elles rédigent une demande complète).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-255">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="fbfd8-256">Dans les exemples suivants, le bot répond à chaque message avec des options pour ce que vous souhaitez faire ensuite.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-256">In the following examples, the bot responds to each message with options for what might want to do next.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-257">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-257">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="L'exemple montre une interaction à plusieurs tours avec un bot." border="false":::


# <a name="mobile"></a>[<span data-ttu-id="fbfd8-259">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-259">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="L’exemple illustre une interaction à plusieurs tour avec un bot sur mobile." border="false":::


---

### <a name="reach-out-to-users"></a><span data-ttu-id="fbfd8-261">Contacter les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="fbfd8-261">Reach out to users</span></span>

<span data-ttu-id="fbfd8-262">Grâce à une messagerie proactive, votre robot peut agir comme un résumé qui envoie des notifications pertinentes à une personne, une conversation de groupe ou un canal à une fréquence spécifique.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-262">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="fbfd8-263">Un bot peut envoyer un message lorsqu’un élément a changé dans un document ou qu’un élément de travail est fermé.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-263">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-264">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-264">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="fbfd8-265">Dans l’exemple suivant, l’utilisateur reçoit une notification toast qu’un bot les a envoyés dans un autre canal.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-265">In the following example, the user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="L’exemple montre le toast d’un bot qui a envoyer un message de façon proactive à un utilisateur d’un autre canal." border="false":::

<span data-ttu-id="fbfd8-267">Dans ce canal, l’utilisateur peut lire son message à partir du bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-267">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="L'exemple montre l'utilisateur regardant le message proactif du bot." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-269">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-269">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="fbfd8-270">Dans l’exemple suivant, l’utilisateur reçoit une notification qu’un bot les a envoyés dans un autre canal.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-270">In the following example, the user gets a notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="L’exemple montre un toast d’un bot qui messagerie de manière proactive un utilisateur à partir d’un autre canal sur mobile." border="false":::

<span data-ttu-id="fbfd8-272">Dans ce canal, l’utilisateur peut lire son message à partir du bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-272">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="L’exemple montre l’utilisateur regardant le message proactif du bot sur un appareil mobile." border="false":::

---

### <a name="use-tabs-with-bots"></a><span data-ttu-id="fbfd8-274">Utiliser des onglets avec des bots</span><span class="sxs-lookup"><span data-stu-id="fbfd8-274">Use tabs with bots</span></span>

<span data-ttu-id="fbfd8-275">Dans les applications personnelles, un onglet peut compléter ce que votre bot peut faire.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-275">In personal apps, a tab can complement what your bot can do.</span></span> <span data-ttu-id="fbfd8-276">Par exemple, si votre bot peut créer des éléments de travail, il peut être agréable d’afficher tous ces éléments dans un emplacement central au sein d’un onglet. En savoir plus sur la [création d’onglets](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-276">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="fbfd8-277">Desktop</span><span class="sxs-lookup"><span data-stu-id="fbfd8-277">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="L'exemple montre comment un onglet peut aider à organiser le contenu d'un bot." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="fbfd8-279">Mobile</span><span class="sxs-lookup"><span data-stu-id="fbfd8-279">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="Un exemple montre comment un onglet peut aider à organiser le contenu du bot sur mobile." border="false":::

---

## <a name="manage-a-bot"></a><span data-ttu-id="fbfd8-281">Gérer un bot</span><span class="sxs-lookup"><span data-stu-id="fbfd8-281">Manage a bot</span></span>

<span data-ttu-id="fbfd8-282">Les utilisateurs doivent pouvoir modifier les paramètres d’un bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-282">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="fbfd8-283">Vous pouvez fournir cette fonctionnalité avec des commandes bot, mais il est généralement plus efficace d’inclure tous les paramètres dans un [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (comme illustré dans l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-283">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="L'exemple montre un module de tâches permettant de configurer les paramètres d'un bot." border="false":::

## <a name="best-practices"></a><span data-ttu-id="fbfd8-285">Les bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="fbfd8-285">Best practices</span></span>

<span data-ttu-id="fbfd8-286">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-286">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="fbfd8-287">Contenu</span><span class="sxs-lookup"><span data-stu-id="fbfd8-287">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Exemple montrant une meilleure pratique de bot pour établir un personnage clair." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="fbfd8-289">À faire : établir un personnage clair</span><span class="sxs-lookup"><span data-stu-id="fbfd8-289">Do: Establish a clear persona</span></span>

<span data-ttu-id="fbfd8-290">Le ton de votre bot est-il amical et léger, « juste les faits », ou plus excentrique ?</span><span class="sxs-lookup"><span data-stu-id="fbfd8-290">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="fbfd8-291">Comment doit-il répondre dans différents scénarios ?</span><span class="sxs-lookup"><span data-stu-id="fbfd8-291">How should it respond in different scenarios?</span></span> <span data-ttu-id="fbfd8-292">La planification et la documentation du personnage de votre bot facilitent l’écriture des réponses qui semblent naturelles et cohérentes.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-292">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="fbfd8-293">En savoir plus sur l’écriture pour les bots dans <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">kit d’interface utilisateur de Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="fbfd8-293">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Exemple montrant comment transmettre clairement ce que votre bot peut faire." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="fbfd8-295">À faire : communiquer clairement ce que votre bot peut faire</span><span class="sxs-lookup"><span data-stu-id="fbfd8-295">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="fbfd8-296">Les messages de bienvenue et les visites guidées aident les personnes à comprendre ce qu’elles peuvent faire avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-296">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Exemple montrant qu’il ne faut pas masquer les fonctionnalités de votre bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="fbfd8-298">À ne pas faire : masquer les fonctionnalités de votre bot</span><span class="sxs-lookup"><span data-stu-id="fbfd8-298">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="fbfd8-299">Les premières impressions sont importantes.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-299">First impressions matter.</span></span> <span data-ttu-id="fbfd8-300">Les personnes seront probablement confuses ou méfiantes lorsqu'elles verront un message de connexion indéfini.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-300">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="L’exemple montrant votre bot doit reconnaître les questions non posées." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="fbfd8-302">À faire : reconnaître les questions non posées</span><span class="sxs-lookup"><span data-stu-id="fbfd8-302">Do: Recognize non-questions</span></span>

<span data-ttu-id="fbfd8-303">Votre bot doit pouvoir répondre à des messages tels que « Bonjour », « Aide » et « Merci », tout en tenant compte des fautes d'orthographe et des expressions familières courantes.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-303">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Exemple montrant que vous devez éviter les réponses à des messages de bot simples." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="fbfd8-305">À ne pas faire : manquer les opportunités de satisfaction</span><span class="sxs-lookup"><span data-stu-id="fbfd8-305">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="fbfd8-306">Certaines personnes s'attendent à ce que les conversations se déroulent naturellement, comme avec une personne réelle.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-306">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="fbfd8-307">Essayez d'éviter les réponses maladroites à des messages simples.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-307">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="fbfd8-308">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="fbfd8-308">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="L’exemple de bots doit aider les utilisateurs à comprendre comment les utiliser." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="fbfd8-310">À faire : fournir de l’aide</span><span class="sxs-lookup"><span data-stu-id="fbfd8-310">Do: Provide help</span></span>

<span data-ttu-id="fbfd8-311">Si votre bot ne peut pas répondre à une demande, fournissez à l’utilisateur les moyens de s’informer sur l’interaction avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-311">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Exemple montrant que votre bot ne doit pas être un groupe d’utilisateurs." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="fbfd8-313">À ne pas faire : laisser les utilisateurs bloqués</span><span class="sxs-lookup"><span data-stu-id="fbfd8-313">Don't: Leave users stranded</span></span>

<span data-ttu-id="fbfd8-314">Les personnes vont rapidement abandonner votre robot s’ils ne peuvent pas résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-314">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="fbfd8-315">Interactions complexes</span><span class="sxs-lookup"><span data-stu-id="fbfd8-315">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Exemple montrant que vous pouvez utiliser des modules de tâche ou des onglets avec votre bot pour des interactions complexes." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="fbfd8-317">A faire : utiliser des modules ou des onglets de tâches</span><span class="sxs-lookup"><span data-stu-id="fbfd8-317">Do: Use task modules or tabs</span></span>

<span data-ttu-id="fbfd8-318">Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, vous pouvez lier un module de tâches ou un onglet pour terminer la tâche ou le flux.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-318">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Exemple montrant comment votre bot doit éviter les interactions à plusieurs tour." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="fbfd8-320">À ne pas faire : rendre les interactions à plusieurs tour fastidieuses</span><span class="sxs-lookup"><span data-stu-id="fbfd8-320">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="fbfd8-321">Une conversation approfondie pour accomplir une seule tâche est lente et trop complexe.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-321">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="fbfd8-322">Le développeur doit également prendre en compte les modifications apportées aux états (par exemple, le délai d’annulation de la conversation ou l’envoi d’un message « Annuler »).</span><span class="sxs-lookup"><span data-stu-id="fbfd8-322">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="fbfd8-323">Confidentialité</span><span class="sxs-lookup"><span data-stu-id="fbfd8-323">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Exemple montrant comment les bots doivent uniquement afficher des informations privées dans un contexte personnel." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="fbfd8-325">À faire : afficher uniquement les informations sensibles dans un contexte personnel</span><span class="sxs-lookup"><span data-stu-id="fbfd8-325">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="fbfd8-326">Si votre bot se trouve dans une conversation ou un canal de groupe, nous vous recommandons de diriger les utilisateurs vers un emplacement privé (tel qu’un module de tâches, un onglet ou un navigateur) pour afficher les informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-326">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Exemple montrant comment les bots ne doivent pas révéler d’informations sensibles à un groupe ou à des personnes." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="fbfd8-328">À ne pas faire : certains contenus ne sont pas destinés à être vus par tout le monde</span><span class="sxs-lookup"><span data-stu-id="fbfd8-328">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="fbfd8-329">Votre bot ne doit pas révéler d’informations sensibles à un groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="fbfd8-329">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="fbfd8-330">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fbfd8-330">See also</span></span>

<span data-ttu-id="fbfd8-331">Ces autres instructions peuvent vous aider dans la conception de votre bot :</span><span class="sxs-lookup"><span data-stu-id="fbfd8-331">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="fbfd8-332">Conception de votre application personnelle</span><span class="sxs-lookup"><span data-stu-id="fbfd8-332">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="fbfd8-333">Conception de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="fbfd8-333">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="fbfd8-334">Conception de modules de tâches</span><span class="sxs-lookup"><span data-stu-id="fbfd8-334">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
