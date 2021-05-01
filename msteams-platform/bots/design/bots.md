---
title: Conception de votre bot
description: Découvrez comment concevoir un bot Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: d2967abdc6c0055eca8c94ed4e4a7fdf1bdba322
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101694"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="681e7-103">Conception de votre bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="681e7-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="681e7-104">Les bots sont des applications de conversation qui effectuent un ensemble spécifique de tâches.</span><span class="sxs-lookup"><span data-stu-id="681e7-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="681e7-105">Basés sur <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, les bots communiquent avec les utilisateurs, répondent à leurs questions et informent les utilisateurs de façon proactive en cas de modifications et d’autres événements.</span><span class="sxs-lookup"><span data-stu-id="681e7-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="681e7-106">C’est un excellent moyen de les joindre.</span><span class="sxs-lookup"><span data-stu-id="681e7-106">They're a great way to reach out.</span></span>

<span data-ttu-id="681e7-107">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des bots dans Teams.</span><span class="sxs-lookup"><span data-stu-id="681e7-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="681e7-108">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="681e7-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="681e7-109">Vous trouverez des instructions plus détaillées sur la conception du bot, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="681e7-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="681e7-110">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="681e7-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="681e7-111">Ajouter un bot</span><span class="sxs-lookup"><span data-stu-id="681e7-111">Add a bot</span></span>

<span data-ttu-id="681e7-112">Les bots sont disponibles dans les conversations, les canaux et les applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="681e7-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="681e7-113">Pour ajouter un bot, vous pouvez utiliser l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="681e7-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="681e7-114">À partir de Teams Store (AppSource).</span><span class="sxs-lookup"><span data-stu-id="681e7-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="681e7-115">Utilisez le menu volant de l’application en sélectionnant l’icône **Plus** sur le côté gauche de Teams.</span><span class="sxs-lookup"><span data-stu-id="681e7-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="681e7-116">Avec un @mention dans la nouvelle conversation ou zone de rédaction (l’exemple suivant montre comment faire dans une conversation de groupe).</span><span class="sxs-lookup"><span data-stu-id="681e7-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="L’exemple montre comment ajouter un bot dans une conversation de groupe à l’aide de @mention." border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="681e7-118">Présentation d’un bot</span><span class="sxs-lookup"><span data-stu-id="681e7-118">Introduce a bot</span></span>

<span data-ttu-id="681e7-119">Il est essentiel que votre bot se présente et décrive ce qu'il peut faire.</span><span class="sxs-lookup"><span data-stu-id="681e7-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="681e7-120">Cet échange initial permet aux utilisateurs de comprendre ce qu’il faut faire avec le bot, de connaître ses limites et, surtout, de se mettre à l’interaction avec.</span><span class="sxs-lookup"><span data-stu-id="681e7-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="681e7-121">Message de bienvenue dans une conversation à deux</span><span class="sxs-lookup"><span data-stu-id="681e7-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="681e7-122">En contexte personnel, les messages d’accueil définissent le ton de votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="681e7-123">Le message inclut une salutation, ce que le bot peut faire et quelques suggestions sur l’interaction (par exemple, « Essayez de me demander ... »).</span><span class="sxs-lookup"><span data-stu-id="681e7-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="681e7-124">Si possible, ces suggestions doivent renvoyer les réponses stockées sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="681e7-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="L'exemple montre l'introduction d'un bot dans une application personnelle." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="681e7-126">Introductions dans les conversations et canaux de groupe</span><span class="sxs-lookup"><span data-stu-id="681e7-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="681e7-127">L’introduction de votre bot doit être légèrement différente dans les conversations et canaux de groupe par rapport à un contexte personnel (comme une application personnelle).</span><span class="sxs-lookup"><span data-stu-id="681e7-127">Your bot's introduction should be slightly different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="681e7-128">Dans la vie réelle, si vous entrez dans une salle pleine de gens, vous vous présenterez au lieu de souhaiter la bienvenue à tous ceux qui sont déjà là.</span><span class="sxs-lookup"><span data-stu-id="681e7-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="681e7-129">Portez cette réflexion dans votre conception bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="L'exemple montre l'introduction d'un bot dans un contexte de collaboration." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="681e7-131">Authentification bot avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="681e7-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="681e7-132">Lorsqu'une personne envoie un message à un bot, il peut être nécessaire de se connecter pour utiliser toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="681e7-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="681e7-133">Vous pouvez simplifier le processus d'authentification à l'aide de l'authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="681e7-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="681e7-134">N’oubliez pas : dans le menu de commandes du bot (**Que puis-je faire ?**), vous devez également fournir une commande pour vous sortir.</span><span class="sxs-lookup"><span data-stu-id="681e7-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="L'exemple montre un bot avec un bouton de connexion." border="false":::

### <a name="tours"></a><span data-ttu-id="681e7-136">Visites guidées</span><span class="sxs-lookup"><span data-stu-id="681e7-136">Tours</span></span>

<span data-ttu-id="681e7-137">Vous pouvez inclure une visite guidée avec des messages d’accueil et si le bot répond à une commande telle qu’une « aide ».</span><span class="sxs-lookup"><span data-stu-id="681e7-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="681e7-138">Une visite guidée est le moyen le plus efficace de décrire ce que peut faire votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="681e7-139">Le cas échéant, ils sont également utiles pour décrire les autres fonctionnalités de votre application (par exemple, inclure des captures d’écran de votre extension de messagerie).</span><span class="sxs-lookup"><span data-stu-id="681e7-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="681e7-140">Les visites guidées doivent être accessibles sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="681e7-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="681e7-141">Conversations à deux</span><span class="sxs-lookup"><span data-stu-id="681e7-141">One-on-one chats</span></span>

<span data-ttu-id="681e7-142">Dans une application personnelle, un carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="681e7-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="681e7-143">L’inclure dans les boutons permet aux utilisateurs d’essayer les commandes du bot (par exemple, **Créer une tâche**).</span><span class="sxs-lookup"><span data-stu-id="681e7-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="L'exemple montre une visite guidée d'un bot dans une conversation à deux." border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="681e7-145">Canaux et conversations de groupe</span><span class="sxs-lookup"><span data-stu-id="681e7-145">Channels and group chats</span></span>

<span data-ttu-id="681e7-146">Dans les canaux et conversations de groupe, une visite guidée doit s’ouvrir dans un modal (également appelé [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) de sorte qu’elle n’interrompe pas les conversations en cours.</span><span class="sxs-lookup"><span data-stu-id="681e7-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="681e7-147">Cela vous permet également d’implémenter des affichages basés sur les rôles pour votre visite guidée.</span><span class="sxs-lookup"><span data-stu-id="681e7-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="L'exemple montre une visite guidée d'un bot dans un canal." border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="681e7-149">Discuter avec un robot</span><span class="sxs-lookup"><span data-stu-id="681e7-149">Chat with a bot</span></span>

<span data-ttu-id="681e7-150">Les bots s’intègrent directement dans l’infrastructure de messagerie de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="681e7-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="681e7-151">Les utilisateurs peuvent discuter avec un bot pour trouver une réponse à leurs questions ou taper des commandes pour que le bot effectue un ensemble de tâches étroit ou spécifique.</span><span class="sxs-lookup"><span data-stu-id="681e7-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="681e7-152">Les bots peuvent informer les utilisateurs des modifications ou mises à jour apportées à votre application par conversation instantanée.</span><span class="sxs-lookup"><span data-stu-id="681e7-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="681e7-153">Discuter avec un bot dans différents contextes</span><span class="sxs-lookup"><span data-stu-id="681e7-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="681e7-154">Vous pouvez utiliser des bots dans les contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="681e7-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="681e7-155">**Applications personnelles** : dans une application personnelle, un bot possède un onglet de conversation dédié.</span><span class="sxs-lookup"><span data-stu-id="681e7-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="681e7-156">**Conversation à deux** : un utilisateur peut démarrer une conversation privée avec un bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="681e7-157">C’est la même expérience que l’utilisation d’un bot dans une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="681e7-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="681e7-158">**Conversation de groupe** : les utilisateurs peuvent interagir avec un bot dans une conversation de groupe en @mentionnant le bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="681e7-159">**Canal** : les utilisateurs peuvent interagir avec un bot dans un canal.</span><span class="sxs-lookup"><span data-stu-id="681e7-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="681e7-160">en @mentionnant nom du bot dans la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="681e7-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="681e7-161">N’oubliez pas que, dans ce contexte, le bot est disponible pour l’ensemble de l’équipe, pas seulement pour le canal.</span><span class="sxs-lookup"><span data-stu-id="681e7-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="681e7-162">Anatomie</span><span class="sxs-lookup"><span data-stu-id="681e7-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="L’exemple montre la forme structurelle d’un bot." border="false":::

|<span data-ttu-id="681e7-164">Compteur</span><span class="sxs-lookup"><span data-stu-id="681e7-164">Counter</span></span>|<span data-ttu-id="681e7-165">Description</span><span class="sxs-lookup"><span data-stu-id="681e7-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="681e7-166">1</span><span class="sxs-lookup"><span data-stu-id="681e7-166">1</span></span>|<span data-ttu-id="681e7-167">**Nom et icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="681e7-167">**App name and icon**</span></span>|
|<span data-ttu-id="681e7-168">2</span><span class="sxs-lookup"><span data-stu-id="681e7-168">2</span></span>|<span data-ttu-id="681e7-169">**Onglet Conversation** : ouvre l’espace pour discuter avec votre bot (applicable uniquement aux applications personnelles).</span><span class="sxs-lookup"><span data-stu-id="681e7-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="681e7-170">3</span><span class="sxs-lookup"><span data-stu-id="681e7-170">3</span></span>|<span data-ttu-id="681e7-171">**Onglets Personnalisé** : ouvre le contenu lié à votre application.</span><span class="sxs-lookup"><span data-stu-id="681e7-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="681e7-172">4 </span><span class="sxs-lookup"><span data-stu-id="681e7-172">4</span></span>|<span data-ttu-id="681e7-173">**Onglet À propos** : affiche des informations de base sur votre application.</span><span class="sxs-lookup"><span data-stu-id="681e7-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="681e7-174">5 </span><span class="sxs-lookup"><span data-stu-id="681e7-174">5</span></span>|<span data-ttu-id="681e7-175">**Bulle de conversation** : les conversations bot utilisent le cadre de stratégie de messagerie Teams.</span><span class="sxs-lookup"><span data-stu-id="681e7-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="681e7-176">6 </span><span class="sxs-lookup"><span data-stu-id="681e7-176">6</span></span>|<span data-ttu-id="681e7-177">**Carte adaptative** : si les réponses de votre bot incluent des cartes adaptatives, la carte prend toute la largeur de la bulle de conversation.</span><span class="sxs-lookup"><span data-stu-id="681e7-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="681e7-178">7 </span><span class="sxs-lookup"><span data-stu-id="681e7-178">7</span></span>|<span data-ttu-id="681e7-179">**Menu de commandes** : affiche les commandes standard de votre bot (définies par vous).</span><span class="sxs-lookup"><span data-stu-id="681e7-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="681e7-180">Menu de commandes</span><span class="sxs-lookup"><span data-stu-id="681e7-180">Command menu</span></span>

<span data-ttu-id="681e7-181">Le menu de commandes fournit la liste des mots ou phrases à qui votre robot doit toujours répondre.</span><span class="sxs-lookup"><span data-stu-id="681e7-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="681e7-182">Le menu de commande s'affiche au-dessus de la zone de rédaction lorsqu'une personne converse avec un bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="681e7-183">Lorsqu’une commande est sélectionnée, elle est insérée dans un message.</span><span class="sxs-lookup"><span data-stu-id="681e7-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="681e7-184">La liste des commandes doit être brève.</span><span class="sxs-lookup"><span data-stu-id="681e7-184">The list of commands should be brief.</span></span> <span data-ttu-id="681e7-185">Le menu est destiné à mettre en évidence les principales fonctionnalités de votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="681e7-186">Gardez également les commandes concises.</span><span class="sxs-lookup"><span data-stu-id="681e7-186">Keep commands concise, too.</span></span> <span data-ttu-id="681e7-187">Par exemple, vous pouvez créer une commande appelée **Aide** au lieu d’une commande **Pouvez-vous m’aider** ?</span><span class="sxs-lookup"><span data-stu-id="681e7-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="681e7-188">Le menu de commandes doit toujours être disponible quel que soit l’état de la conversation.</span><span class="sxs-lookup"><span data-stu-id="681e7-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="L'exemple montre le menu de commandes d'un bot." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="681e7-190">Comprendre ce que les gens disent</span><span class="sxs-lookup"><span data-stu-id="681e7-190">Understand what people are saying</span></span>

<span data-ttu-id="681e7-191">Utilisez un dictionnaire des synonymes et demandez à des personnes issues d'horizons aussi différents que possible de vous aider à générer différentes interprétations de requêtes standard.</span><span class="sxs-lookup"><span data-stu-id="681e7-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

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

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="681e7-195">Extraire l’intention et les données des messages</span><span class="sxs-lookup"><span data-stu-id="681e7-195">Extract intent and data from messages</span></span>

<span data-ttu-id="681e7-196">Concevez votre bot pour reconnaître l'intention, c'est-à-dire ce que quelqu'un attend d'un bot en réponse à un message ou une requête.</span><span class="sxs-lookup"><span data-stu-id="681e7-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="681e7-197">L'intention classe un message ou une requête comme une action unique avec un ou plusieurs objets de données affectés par l'action.</span><span class="sxs-lookup"><span data-stu-id="681e7-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="681e7-198">Les exemples suivants décrivent l’objectif de l’utilisateur et les données dans les messages envoyés à des bots.</span><span class="sxs-lookup"><span data-stu-id="681e7-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

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

### <a name="analyze-and-improve"></a><span data-ttu-id="681e7-202">Analyser et améliorer</span><span class="sxs-lookup"><span data-stu-id="681e7-202">Analyze and improve</span></span>

<span data-ttu-id="681e7-203">Découvrez les dires des utilisateurs en discutant avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="681e7-204">Il s’agit d’un processus itératif continu à mesure que votre base d’utilisateurs s’agrandit à différents emplacements et organisation.</span><span class="sxs-lookup"><span data-stu-id="681e7-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="681e7-205">Vous pouvez affiner la reconnaissance linguistique et le mappage d’intention de votre bot avec Microsoft Language Understanding (LUIS).</span><span class="sxs-lookup"><span data-stu-id="681e7-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="681e7-206">[Comprendre LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence) : découvrez comment LUIS utilise l’intelligence artificielle pour fournir une compréhension du langage naturel (NLU) aux données de votre application.</span><span class="sxs-lookup"><span data-stu-id="681e7-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="681e7-207">[Intégration à LUIS](https://www.luis.ai/) : ajoutez des fonctionnalités de langage naturel à votre bot sans le processus complexe de création de modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="681e7-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="681e7-208">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="681e7-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="681e7-209">Requêtes simples</span><span class="sxs-lookup"><span data-stu-id="681e7-209">Simple queries</span></span>

<span data-ttu-id="681e7-210">Les bots peuvent fournir une correspondance exacte à une requête ou à un groupe de correspondances associées pour vous aider à mettre fin à l’ambiguïté.</span><span class="sxs-lookup"><span data-stu-id="681e7-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="681e7-211">Pour les correspondances associées, groupez le contenu à l’aide d’une carte de liste.</span><span class="sxs-lookup"><span data-stu-id="681e7-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="L'exemple montre une interaction de requête simple avec un bot." border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="681e7-213">Interactions à plusieurs tour</span><span class="sxs-lookup"><span data-stu-id="681e7-213">Multi-turn interactions</span></span>

<span data-ttu-id="681e7-214">Si votre bot peut prendre en charge les demandes complètes et les questions, il doit également être en mesure de gérer les interactions à plusieurs tour.</span><span class="sxs-lookup"><span data-stu-id="681e7-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="681e7-215">L'anticipation des étapes suivantes possibles permet aux personnes d'effectuer un flux de tâches plus facilement (plutôt que d'attendre d'elles qu'elles rédigent une demande complète).</span><span class="sxs-lookup"><span data-stu-id="681e7-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="681e7-216">Dans l'exemple suivant, le bot répond à chaque message en proposant des options pour la suite.</span><span class="sxs-lookup"><span data-stu-id="681e7-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="L'exemple montre une interaction à plusieurs tours avec un bot." border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="681e7-218">Contacter les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="681e7-218">Reach out to users</span></span>

<span data-ttu-id="681e7-219">Grâce à une messagerie proactive, votre robot peut agir comme un résumé qui envoie des notifications pertinentes à une personne, une conversation de groupe ou un canal à une fréquence spécifique.</span><span class="sxs-lookup"><span data-stu-id="681e7-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="681e7-220">Un bot peut envoyer un message lorsqu’un élément a changé dans un document ou qu’un élément de travail est fermé.</span><span class="sxs-lookup"><span data-stu-id="681e7-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="681e7-221">Dans l’exemple suivant, un utilisateur reçoit une notification toast lui indiquant qu'un bot lui a envoyé un message sur un autre canal.</span><span class="sxs-lookup"><span data-stu-id="681e7-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="L’exemple montre le toast d’un bot qui a envoyer un message de façon proactive à un utilisateur d’un autre canal." border="false":::

<span data-ttu-id="681e7-223">Dans ce canal, l’utilisateur peut lire son message à partir du bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="L'exemple montre l'utilisateur regardant le message proactif du bot." border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="681e7-225">Utiliser des onglets avec des bots</span><span class="sxs-lookup"><span data-stu-id="681e7-225">Use tabs with bots</span></span>

<span data-ttu-id="681e7-226">Un onglet peut faciliter l’utilisation de votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="681e7-227">Par exemple, si votre bot peut créer des éléments de travail, il peut être agréable d’afficher tous ces éléments dans un emplacement central au sein d’un onglet. En savoir plus sur la [création d’onglets](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="681e7-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="L'exemple montre comment un onglet peut aider à organiser le contenu d'un bot." border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="681e7-229">Gérer un bot</span><span class="sxs-lookup"><span data-stu-id="681e7-229">Manage a bot</span></span>

<span data-ttu-id="681e7-230">Les utilisateurs doivent pouvoir modifier les paramètres d’un bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="681e7-231">Vous pouvez fournir cette fonctionnalité avec des commandes bot, mais il est généralement plus efficace d’inclure tous les paramètres dans un [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (comme illustré dans l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="681e7-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="L'exemple montre un module de tâches permettant de configurer les paramètres d'un bot." border="false":::

## <a name="best-practices"></a><span data-ttu-id="681e7-233">Les bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="681e7-233">Best practices</span></span>

<span data-ttu-id="681e7-234">Utilisez ces recommandations pour créer une expérience d'application de qualité.</span><span class="sxs-lookup"><span data-stu-id="681e7-234">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="681e7-235">Contenu</span><span class="sxs-lookup"><span data-stu-id="681e7-235">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Exemple montrant une meilleure pratique de bot pour l'établissement d'un personnage clair." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="681e7-237">À faire : établir un personnage clair</span><span class="sxs-lookup"><span data-stu-id="681e7-237">Do: Establish a clear persona</span></span>

<span data-ttu-id="681e7-238">Le ton de votre bot est-il amical et léger, « juste les faits », ou plus excentrique ?</span><span class="sxs-lookup"><span data-stu-id="681e7-238">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="681e7-239">Comment doit-il répondre dans différents scénarios ?</span><span class="sxs-lookup"><span data-stu-id="681e7-239">How should it respond in different scenarios?</span></span> <span data-ttu-id="681e7-240">La planification et la documentation du personnage de votre bot facilitent l’écriture des réponses qui semblent naturelles et cohérentes.</span><span class="sxs-lookup"><span data-stu-id="681e7-240">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="681e7-241">En savoir plus sur l’écriture pour les bots dans <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">kit d’interface utilisateur de Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="681e7-241">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Exemple montrant comment transmettre clairement ce que votre bot peut faire." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="681e7-243">À faire : communiquer clairement ce que votre bot peut faire</span><span class="sxs-lookup"><span data-stu-id="681e7-243">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="681e7-244">Les messages de bienvenue et les visites guidées aident les personnes à comprendre ce qu’elles peuvent faire avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-244">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Exemple montrant qu'il ne faut pas masquer les fonctionnalités de votre bot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="681e7-246">À ne pas faire : masquer les fonctionnalités de votre bot</span><span class="sxs-lookup"><span data-stu-id="681e7-246">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="681e7-247">Les premières impressions sont importantes.</span><span class="sxs-lookup"><span data-stu-id="681e7-247">First impressions matter.</span></span> <span data-ttu-id="681e7-248">Les personnes seront probablement confuses ou méfiantes lorsqu'elles verront un message de connexion indéfini.</span><span class="sxs-lookup"><span data-stu-id="681e7-248">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="L'exemple montrant votre bot doit reconnaître les questions non posées." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="681e7-250">À faire : reconnaître les questions non posées</span><span class="sxs-lookup"><span data-stu-id="681e7-250">Do: Recognize non-questions</span></span>

<span data-ttu-id="681e7-251">Votre bot doit pouvoir répondre à des messages tels que « Bonjour », « Aide » et « Merci », tout en tenant compte des fautes d'orthographe et des expressions familières courantes.</span><span class="sxs-lookup"><span data-stu-id="681e7-251">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Exemple montrant que vous devez éviter les réponses à des messages de bot simples." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="681e7-253">À ne pas faire : manquer les opportunités de satisfaction</span><span class="sxs-lookup"><span data-stu-id="681e7-253">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="681e7-254">Certaines personnes s'attendent à ce que les conversations se déroulent naturellement, comme avec une personne réelle.</span><span class="sxs-lookup"><span data-stu-id="681e7-254">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="681e7-255">Essayez d'éviter les réponses maladroites à des messages simples.</span><span class="sxs-lookup"><span data-stu-id="681e7-255">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="681e7-256">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="681e7-256">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="L'exemple de bots doit aider les utilisateurs à comprendre comment les utiliser." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="681e7-258">À faire : fournir de l’aide</span><span class="sxs-lookup"><span data-stu-id="681e7-258">Do: Provide help</span></span>

<span data-ttu-id="681e7-259">Si votre bot ne peut pas répondre à une demande, fournissez à l’utilisateur les moyens de s’informer sur l’interaction avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="681e7-259">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Exemple montrant que votre bot ne doit pas être un groupe d'utilisateurs." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="681e7-261">À ne pas faire : laisser les utilisateurs bloqués</span><span class="sxs-lookup"><span data-stu-id="681e7-261">Don't: Leave users stranded</span></span>

<span data-ttu-id="681e7-262">Les personnes vont rapidement abandonner votre robot s’ils ne peuvent pas résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="681e7-262">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="681e7-263">Interactions complexes</span><span class="sxs-lookup"><span data-stu-id="681e7-263">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Exemple montrant que vous pouvez utiliser des modules de tâche ou des onglets avec votre bot pour des interactions complexes." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="681e7-265">A faire : utiliser des modules ou des onglets de tâches</span><span class="sxs-lookup"><span data-stu-id="681e7-265">Do: Use task modules or tabs</span></span>

<span data-ttu-id="681e7-266">Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, vous pouvez lier un module de tâches ou un onglet pour terminer la tâche ou le flux.</span><span class="sxs-lookup"><span data-stu-id="681e7-266">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Exemple montrant comment votre bot doit éviter les interactions à plusieurs tour." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="681e7-268">À ne pas faire : rendre les interactions à plusieurs tour fastidieuses</span><span class="sxs-lookup"><span data-stu-id="681e7-268">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="681e7-269">Une conversation approfondie pour accomplir une seule tâche est lente et trop complexe.</span><span class="sxs-lookup"><span data-stu-id="681e7-269">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="681e7-270">Le développeur doit également prendre en compte les modifications apportées aux états (par exemple, le délai d’annulation de la conversation ou l’envoi d’un message « Annuler »).</span><span class="sxs-lookup"><span data-stu-id="681e7-270">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="681e7-271">Confidentialité</span><span class="sxs-lookup"><span data-stu-id="681e7-271">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Exemple montrant comment les bots doivent uniquement afficher des informations privées dans un contexte personnel." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="681e7-273">À faire : afficher uniquement les informations sensibles dans un contexte personnel</span><span class="sxs-lookup"><span data-stu-id="681e7-273">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="681e7-274">Si votre bot se trouve dans une conversation ou un canal de groupe, nous vous recommandons de diriger les utilisateurs vers un emplacement privé (tel qu’un module de tâches, un onglet ou un navigateur) pour afficher les informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="681e7-274">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Exemple montrant comment les bots ne doivent pas révéler d'informations sensibles à un groupe ou à des personnes." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="681e7-276">À ne pas faire : certains contenus ne sont pas destinés à être vus par tout le monde</span><span class="sxs-lookup"><span data-stu-id="681e7-276">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="681e7-277">Votre bot ne doit pas révéler d’informations sensibles à un groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="681e7-277">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="681e7-278">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="681e7-278">See also</span></span>

<span data-ttu-id="681e7-279">Ces autres instructions peuvent vous aider dans la conception de votre bot :</span><span class="sxs-lookup"><span data-stu-id="681e7-279">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="681e7-280">Conception de votre application personnelle</span><span class="sxs-lookup"><span data-stu-id="681e7-280">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="681e7-281">Conception de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="681e7-281">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="681e7-282">Conception de modules de tâches</span><span class="sxs-lookup"><span data-stu-id="681e7-282">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
