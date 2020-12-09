---
title: Conception de votre robot
description: Découvrez comment concevoir un bot de teams et obtenir le kit d’interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605426"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="3cb30-103">Conception de votre robot Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="3cb30-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="3cb30-104">Les robots sont des applications de conversation qui effectuent un ensemble spécifique de tâches.</span><span class="sxs-lookup"><span data-stu-id="3cb30-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="3cb30-105">En fonction de <a href="https://dev.botframework.com/" target="_blank">Microsoft bot Framework</a>, les robots communiquent avec les utilisateurs, répondent à leurs questions et les signalent de manière proactive sur les modifications et les autres événements.</span><span class="sxs-lookup"><span data-stu-id="3cb30-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="3cb30-106">Ils constituent un excellent moyen de communiquer.</span><span class="sxs-lookup"><span data-stu-id="3cb30-106">They're a great way to reach out.</span></span>

<span data-ttu-id="3cb30-107">Pour vous aider à concevoir votre application, les informations suivantes décrivent et illustrent la façon dont les utilisateurs peuvent ajouter, utiliser et gérer les robots dans Teams.</span><span class="sxs-lookup"><span data-stu-id="3cb30-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3cb30-108">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="3cb30-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3cb30-109">Vous trouverez des instructions de conception de robot plus complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3cb30-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cb30-110">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="3cb30-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="3cb30-111">Ajouter un bot</span><span class="sxs-lookup"><span data-stu-id="3cb30-111">Add a bot</span></span>

<span data-ttu-id="3cb30-112">Les robots sont disponibles dans les conversations, les canaux et les applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="3cb30-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="3cb30-113">Vous pouvez ajouter un bot de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="3cb30-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="3cb30-114">À partir du magasin de Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="3cb30-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="3cb30-115">À l’aide du lanceur d’application en sélectionnant l’icône **plus** sur le côté gauche de teams.</span><span class="sxs-lookup"><span data-stu-id="3cb30-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="3cb30-116">Avec une @mention dans la boîte de dialogue nouvelle conversation ou composition (l’exemple suivant montre comment effectuer cette opération dans une conversation de groupe).</span><span class="sxs-lookup"><span data-stu-id="3cb30-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="Exemple montre comment ajouter un bot dans une conversation de groupe à l’aide d’une @mention." border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="3cb30-118">Introduire un robot</span><span class="sxs-lookup"><span data-stu-id="3cb30-118">Introduce a bot</span></span>

<span data-ttu-id="3cb30-119">Il est essentiel que votre bot s’introduit lui-même et décrit ce qu’il peut faire.</span><span class="sxs-lookup"><span data-stu-id="3cb30-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="3cb30-120">Cet échange initial permet aux utilisateurs de comprendre ce qu’ils doivent faire avec le bot, de connaître les limites et, plus important encore, d’interagir avec eux.</span><span class="sxs-lookup"><span data-stu-id="3cb30-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="3cb30-121">Message de bienvenue dans une conversation en un seul</span><span class="sxs-lookup"><span data-stu-id="3cb30-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="3cb30-122">Dans les contextes personnels, les messages d’accueil définissent le ton de votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="3cb30-123">Le message inclut un message d’accueil, ce que le robot peut faire et quelques suggestions concernant la façon d’interagir (par exemple, « essayez de me demander... »).</span><span class="sxs-lookup"><span data-stu-id="3cb30-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="3cb30-124">Dans la mesure du possible, ces suggestions doivent renvoyer des réponses stockées sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="3cb30-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="Exemple de présentation d’un bot dans une application personnelle." border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="3cb30-126">Introductions dans les conversations et les canaux de groupe</span><span class="sxs-lookup"><span data-stu-id="3cb30-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="3cb30-127">L’introduction de votre robot doit être légèrement différente dans les conversations et les canaux de groupe par rapport à un contexte personnel (par exemple, une application personnelle).</span><span class="sxs-lookup"><span data-stu-id="3cb30-127">Your bot's introduction should be slightly little different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="3cb30-128">En réalité, si vous avez entré une salle pleine de personnes ; vous vous présenterez vous-même au lieu de accueillir les personnes qui s’y trouvent déjà.</span><span class="sxs-lookup"><span data-stu-id="3cb30-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="3cb30-129">Conpensez-vous à la conception de votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="Exemple de présentation d’un bot dans un contexte collaboratif." border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="3cb30-131">Authentification de robot avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="3cb30-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="3cb30-132">Lorsqu’une personne message un bot, vous pouvez être amené à utiliser toutes ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3cb30-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="3cb30-133">Vous pouvez simplifier le processus d’authentification à l’aide de l’authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="3cb30-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="3cb30-134">N’oubliez pas : dans le menu de commandes du bot (**que puis-je faire ?**), vous devez également fournir une commande pour vous déconnecter.</span><span class="sxs-lookup"><span data-stu-id="3cb30-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="Exemple montre un bot avec un bouton de connexion." border="false":::

### <a name="tours"></a><span data-ttu-id="3cb30-136">Voyages</span><span class="sxs-lookup"><span data-stu-id="3cb30-136">Tours</span></span>

<span data-ttu-id="3cb30-137">Vous pouvez inclure une visite guidée avec des messages de bienvenue et si le robot répond à une commande semblable à celle d’aide.</span><span class="sxs-lookup"><span data-stu-id="3cb30-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="3cb30-138">Une visite guidée est la manière la plus efficace de décrire ce que votre robot peut faire.</span><span class="sxs-lookup"><span data-stu-id="3cb30-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="3cb30-139">Le cas échéant, elles sont également idéales pour décrire les autres fonctionnalités de votre application (par exemple, inclure des captures d’écran de votre extension de messagerie).</span><span class="sxs-lookup"><span data-stu-id="3cb30-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cb30-140">Les visites guidées doivent être accessibles sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="3cb30-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="3cb30-141">Conversations en un seul</span><span class="sxs-lookup"><span data-stu-id="3cb30-141">One-on-one chats</span></span>

<span data-ttu-id="3cb30-142">Dans une application personnelle, un carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="3cb30-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="3cb30-143">Y compris les boutons les commandes autoriser les utilisateurs à essayer le robot sont encouragées (par exemple, **créer une tâche**).</span><span class="sxs-lookup"><span data-stu-id="3cb30-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="Exemple illustre une visite guidée dans une conversation en un seul." border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="3cb30-145">Canaux et conversations de groupe</span><span class="sxs-lookup"><span data-stu-id="3cb30-145">Channels and group chats</span></span>

<span data-ttu-id="3cb30-146">Dans les canaux et les conversations de groupe, une visite guidée doit s’ouvrir dans un module modal (également appelé « [module de tâche](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) » pour ne pas interrompre les conversations en cours.</span><span class="sxs-lookup"><span data-stu-id="3cb30-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="3cb30-147">Cela vous donne également la possibilité d’implémenter des vues basées sur les rôles pour votre visite guidée.</span><span class="sxs-lookup"><span data-stu-id="3cb30-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="Exemple illustre une visite guidée dans un canal." border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="3cb30-149">Conversation avec un bot</span><span class="sxs-lookup"><span data-stu-id="3cb30-149">Chat with a bot</span></span>

<span data-ttu-id="3cb30-150">Les robots s’intègrent directement à l’infrastructure de messagerie de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="3cb30-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="3cb30-151">Les utilisateurs peuvent discuter avec un bot pour obtenir des réponses à leurs questions ou taper des commandes pour que le robot effectue un ensemble de tâches restreint ou spécifique.</span><span class="sxs-lookup"><span data-stu-id="3cb30-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="3cb30-152">Les robots peuvent avertir de manière proactive les utilisateurs concernant les modifications ou les mises à jour de votre application via une conversation.</span><span class="sxs-lookup"><span data-stu-id="3cb30-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="3cb30-153">Conversation avec un bot dans différents contextes</span><span class="sxs-lookup"><span data-stu-id="3cb30-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="3cb30-154">Vous pouvez utiliser les robots dans les contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="3cb30-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="3cb30-155">**Applications personnelles**: dans une application personnelle, un bot a un onglet de conversation dédié.</span><span class="sxs-lookup"><span data-stu-id="3cb30-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="3cb30-156">**Conversation en un seul**: un utilisateur peut lancer une conversation privée avec un bot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="3cb30-157">Il s’agit de la même expérience que l’utilisation d’un bot dans une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="3cb30-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="3cb30-158">**Group chat**: les personnes peuvent interagir avec un bot dans une conversation de groupe en @mentioning le bot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="3cb30-159">**Canal**: les personnes peuvent interagir avec un bot dans un canal.</span><span class="sxs-lookup"><span data-stu-id="3cb30-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="3cb30-160">en @mentioning le nom du bot dans la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="3cb30-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="3cb30-161">N’oubliez pas que dans ce contexte, le bot est disponible pour l’ensemble de l’équipe, pas seulement pour le canal.</span><span class="sxs-lookup"><span data-stu-id="3cb30-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="3cb30-162">Anatomie</span><span class="sxs-lookup"><span data-stu-id="3cb30-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un bot." border="false":::

|<span data-ttu-id="3cb30-164">Compteur</span><span class="sxs-lookup"><span data-stu-id="3cb30-164">Counter</span></span>|<span data-ttu-id="3cb30-165">Description</span><span class="sxs-lookup"><span data-stu-id="3cb30-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3cb30-166">1</span><span class="sxs-lookup"><span data-stu-id="3cb30-166">1</span></span>|<span data-ttu-id="3cb30-167">**Nom et icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="3cb30-167">**App name and icon**</span></span>|
|<span data-ttu-id="3cb30-168">2 </span><span class="sxs-lookup"><span data-stu-id="3cb30-168">2</span></span>|<span data-ttu-id="3cb30-169">**Onglet conversation**: ouvre l’espace pour parler avec votre bot (applicable uniquement aux applications personnelles).</span><span class="sxs-lookup"><span data-stu-id="3cb30-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="3cb30-170">3 </span><span class="sxs-lookup"><span data-stu-id="3cb30-170">3</span></span>|<span data-ttu-id="3cb30-171">**Onglets personnalisés**: ouvre un autre contenu lié à votre application.</span><span class="sxs-lookup"><span data-stu-id="3cb30-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="3cb30-172">4 </span><span class="sxs-lookup"><span data-stu-id="3cb30-172">4</span></span>|<span data-ttu-id="3cb30-173">**À propos** de l’onglet : affiche des informations de base sur votre application.</span><span class="sxs-lookup"><span data-stu-id="3cb30-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="3cb30-174">5 </span><span class="sxs-lookup"><span data-stu-id="3cb30-174">5</span></span>|<span data-ttu-id="3cb30-175">**Bulle de conversation**: les conversations de robots utilisent l’infrastructure de messagerie Teams.</span><span class="sxs-lookup"><span data-stu-id="3cb30-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="3cb30-176">6 </span><span class="sxs-lookup"><span data-stu-id="3cb30-176">6</span></span>|<span data-ttu-id="3cb30-177">**Carte adaptative**: si les réponses de votre robot incluent des cartes adaptatives, la carte occupe toute la largeur de la bulle de conversation.</span><span class="sxs-lookup"><span data-stu-id="3cb30-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="3cb30-178">7 </span><span class="sxs-lookup"><span data-stu-id="3cb30-178">7</span></span>|<span data-ttu-id="3cb30-179">**Menu de commandes**: affiche les commandes standard de votre robot (que vous avez définie).</span><span class="sxs-lookup"><span data-stu-id="3cb30-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="3cb30-180">Menu de commandes</span><span class="sxs-lookup"><span data-stu-id="3cb30-180">Command menu</span></span>

<span data-ttu-id="3cb30-181">Le menu de commandes fournit une liste de mots ou d’expressions auxquelles votre bot doit toujours répondre.</span><span class="sxs-lookup"><span data-stu-id="3cb30-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="3cb30-182">Le menu de commandes s’affiche au-dessus de la zone de composition lorsqu’une personne est contourne d’un bot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="3cb30-183">Lorsqu’une commande est sélectionnée, elle est insérée dans un message.</span><span class="sxs-lookup"><span data-stu-id="3cb30-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="3cb30-184">La liste des commandes doit être brève.</span><span class="sxs-lookup"><span data-stu-id="3cb30-184">The list of commands should be brief.</span></span> <span data-ttu-id="3cb30-185">Le menu est destiné uniquement à mettre en évidence les principales fonctionnalités de votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="3cb30-186">Conservez les commandes de manière concise.</span><span class="sxs-lookup"><span data-stu-id="3cb30-186">Keep commands concise, too.</span></span> <span data-ttu-id="3cb30-187">Par exemple, créez une commande appelée **aide** au lieu de **pouvez-vous m’aider**?</span><span class="sxs-lookup"><span data-stu-id="3cb30-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="3cb30-188">Le menu de commandes doit toujours être disponible indépendamment de l’état de la conversation.</span><span class="sxs-lookup"><span data-stu-id="3cb30-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="Exemple de menu de commandes d’un bot." border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="3cb30-190">Comprendre ce que les utilisateurs disent</span><span class="sxs-lookup"><span data-stu-id="3cb30-190">Understand what people are saying</span></span>

<span data-ttu-id="3cb30-191">Utilisez un dictionnaire des synonymes et obtenez des personnes d’autres arrière-plans, autant que possible, pour vous aider à générer différentes interprétations des requêtes standard.</span><span class="sxs-lookup"><span data-stu-id="3cb30-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Illustration illustrant la façon dont un bot peut interpréter’Hello'." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Illustration illustrant la façon dont un bot peut interpréter’help'." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Illustration illustrant la façon dont un bot peut interpréter’thanks'." border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="3cb30-195">Extraire les intentions et les données des messages</span><span class="sxs-lookup"><span data-stu-id="3cb30-195">Extract intent and data from messages</span></span>

<span data-ttu-id="3cb30-196">Concevez votre robot pour qu’il reconnaisse l’intention, ce qui capture la réponse d’un bot à un message ou à une requête.</span><span class="sxs-lookup"><span data-stu-id="3cb30-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="3cb30-197">L’intention classe un message ou une requête en tant qu’action unique avec un ou plusieurs objets de données qui sont affectés par l’action.</span><span class="sxs-lookup"><span data-stu-id="3cb30-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="3cb30-198">Les exemples suivants décrivent l’intention de l’utilisateur et les données contenues dans les messages envoyés aux robots.</span><span class="sxs-lookup"><span data-stu-id="3cb30-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="Exemple illustrant dans la phrase « réserver un vol à Seattle », l’intention de l’utilisateur est « réserver un vol » et les données sont « Paris »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="Exemple d’affichage dans la phrase « quand le magasin est ouvert », l’intention de l’utilisateur est « quand » et les données sont « ouvertes »." border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="Exemple illustrant la phrase « planifier une réunion à 13h00 avec Bob en distribution », l’intention de l’utilisateur est « planifier une réunion » et les données « 13h00 » et « Bob en distribution »." border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="3cb30-202">Analyser et améliorer</span><span class="sxs-lookup"><span data-stu-id="3cb30-202">Analyze and improve</span></span>

<span data-ttu-id="3cb30-203">Découvrez ce que les utilisateurs disent lorsque vous discutez avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="3cb30-204">Il s’agit d’un processus continu et itératif à mesure que votre base d’utilisateurs se développe à différents emplacements et développées.</span><span class="sxs-lookup"><span data-stu-id="3cb30-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="3cb30-205">Vous pouvez régler le mappage de reconnaissance et d’intention de langue de votre robot avec Microsoft Language mémorandum (LUIS).</span><span class="sxs-lookup"><span data-stu-id="3cb30-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="3cb30-206">[Comprendre Luis](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Découvrez comment Luis utilise ai pour fournir une compréhension de langage naturel (NLU) à vos données d’application.</span><span class="sxs-lookup"><span data-stu-id="3cb30-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="3cb30-207">[Intégration avec Luis](https://www.luis.ai/): ajoutez des fonctionnalités de langage naturel à votre bot sans le processus complexe de création de modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="3cb30-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="3cb30-208">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3cb30-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="3cb30-209">Requêtes simples</span><span class="sxs-lookup"><span data-stu-id="3cb30-209">Simple queries</span></span>

<span data-ttu-id="3cb30-210">Les robots peuvent fournir une correspondance exacte à une requête ou à un groupe de correspondances associées pour faciliter la désambiguïsation.</span><span class="sxs-lookup"><span data-stu-id="3cb30-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="3cb30-211">Pour les correspondances associées, groupez le contenu à l’aide d’une carte de liste.</span><span class="sxs-lookup"><span data-stu-id="3cb30-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="Exemple illustre une interaction de requête simple avec un bot." border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="3cb30-213">Interactions multi-tournage</span><span class="sxs-lookup"><span data-stu-id="3cb30-213">Multi-turn interactions</span></span>

<span data-ttu-id="3cb30-214">Bien que votre robot puisse prendre en charge des demandes et des questions complètes, il doit également être en mesure de gérer les interactions à tour de rôle.</span><span class="sxs-lookup"><span data-stu-id="3cb30-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="3cb30-215">En anticipant les étapes suivantes possibles, il est plus facile pour les utilisateurs d’effectuer un flux de tâches complet (au lieu de s’attendre à créer une requête complète).</span><span class="sxs-lookup"><span data-stu-id="3cb30-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="3cb30-216">Dans l’exemple suivant, le bot répond à chaque message avec des options pour ce qui peut être le plus utile.</span><span class="sxs-lookup"><span data-stu-id="3cb30-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="Exemple illustre une interaction à tournage multiple avec un bot." border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="3cb30-218">Contacter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3cb30-218">Reach out to users</span></span>

<span data-ttu-id="3cb30-219">Avec la messagerie proactive, votre robot peut agir comme un Digest qui envoie des notifications pertinentes à un individu, une conversation de groupe ou un canal à une fréquence spécifique.</span><span class="sxs-lookup"><span data-stu-id="3cb30-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="3cb30-220">Un bot peut envoyer un message lorsqu’un élément a été modifié dans un document ou qu’un élément de travail est fermé.</span><span class="sxs-lookup"><span data-stu-id="3cb30-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="3cb30-221">Dans l’exemple suivant, un utilisateur obtient une notification de Toast qu’un bot a messageé dans un autre canal.</span><span class="sxs-lookup"><span data-stu-id="3cb30-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="L’exemple montre un toast d’un bot à la messagerie proactive d’un utilisateur à partir d’un autre canal." border="false":::

<span data-ttu-id="3cb30-223">Dans ce canal, l’utilisateur peut lire son message à partir du bot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="Exemple montre comment l’utilisateur examine le message proactif du bot." border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="3cb30-225">Utiliser des onglets avec des robots</span><span class="sxs-lookup"><span data-stu-id="3cb30-225">Use tabs with bots</span></span>

<span data-ttu-id="3cb30-226">Un onglet peut faciliter l’utilisation de votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="3cb30-227">Par exemple, si votre bot peut créer des éléments de travail, il serait intéressant d’afficher tous ces éléments dans un emplacement central à l’intérieur d’un onglet. En savoir plus sur la [conception des onglets](../../tabs/design/tabs.md).</span><span class="sxs-lookup"><span data-stu-id="3cb30-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="Cet exemple montre comment un onglet peut vous aider à organiser le contenu de la robots." border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="3cb30-229">Gérer un bot</span><span class="sxs-lookup"><span data-stu-id="3cb30-229">Manage a bot</span></span>

<span data-ttu-id="3cb30-230">Les utilisateurs doivent être en mesure de modifier les paramètres d’un bot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="3cb30-231">Vous pouvez fournir cette fonctionnalité avec les commandes bot, mais il est généralement plus efficace d’inclure tous les paramètres dans un [module de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (comme illustré dans l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="3cb30-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="Exemple de module de tâche permettant de configurer les paramètres d’un bot." border="false":::

## <a name="best-practices"></a><span data-ttu-id="3cb30-233">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="3cb30-233">Best practices</span></span>

### <a name="content"></a><span data-ttu-id="3cb30-234">Contenu</span><span class="sxs-lookup"><span data-stu-id="3cb30-234">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="3cb30-236">Do : établir un personnage clair</span><span class="sxs-lookup"><span data-stu-id="3cb30-236">Do: Establish a clear persona</span></span>

<span data-ttu-id="3cb30-237">Est-ce que le ton est convivial et clair, « juste les faits » ou Super-excentrique ?</span><span class="sxs-lookup"><span data-stu-id="3cb30-237">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="3cb30-238">Comment doit-il répondre dans différents scénarios ?</span><span class="sxs-lookup"><span data-stu-id="3cb30-238">How should it respond in different scenarios?</span></span> <span data-ttu-id="3cb30-239">La planification et la documentation du personnage de votre robot facilitent l’écriture de réponses apparemment naturelles et cohésives.</span><span class="sxs-lookup"><span data-stu-id="3cb30-239">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="3cb30-240">Pour en savoir plus sur la rédaction de robots, consultez le <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Kit d’interface utilisateur Microsoft Teams (Figma).</a></span><span class="sxs-lookup"><span data-stu-id="3cb30-240">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="3cb30-242">Do : transmettez clairement ce que votre robot peut faire</span><span class="sxs-lookup"><span data-stu-id="3cb30-242">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="3cb30-243">Les messages de bienvenue et les visites aident les utilisateurs à comprendre ce qu’ils peuvent faire avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-243">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="3cb30-245">Ne pas : obscurcir les fonctionnalités de votre robot</span><span class="sxs-lookup"><span data-stu-id="3cb30-245">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="3cb30-246">Premières impressions.</span><span class="sxs-lookup"><span data-stu-id="3cb30-246">First impressions matter.</span></span> <span data-ttu-id="3cb30-247">Il se peut que des personnes soient confondues ou suspectes lors de la présentation d’un message de connexion nondescript.</span><span class="sxs-lookup"><span data-stu-id="3cb30-247">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="3cb30-249">Do : reconnaître les non-questions</span><span class="sxs-lookup"><span data-stu-id="3cb30-249">Do: Recognize non-questions</span></span>

<span data-ttu-id="3cb30-250">Votre robot doit pouvoir répondre aux messages tels que « HI », « aide » et « Merci », tout en tenant compte également des fautes d’orthographe courantes et familières.</span><span class="sxs-lookup"><span data-stu-id="3cb30-250">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="3cb30-252">Ne manquez pas les occasions de vous faire plaisir</span><span class="sxs-lookup"><span data-stu-id="3cb30-252">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="3cb30-253">Certaines personnes attendent que les conversations se déplacent naturellement comme elles le ferait avec une personne réelle.</span><span class="sxs-lookup"><span data-stu-id="3cb30-253">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="3cb30-254">Essayez d’éviter des réponses encombrantes aux messages simples.</span><span class="sxs-lookup"><span data-stu-id="3cb30-254">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="3cb30-255">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="3cb30-255">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="3cb30-257">Do : fournir de l’aide</span><span class="sxs-lookup"><span data-stu-id="3cb30-257">Do: Provide help</span></span>

<span data-ttu-id="3cb30-258">Si votre bot ne peut pas répondre à une demande, demandez à un utilisateur de se former de l’interaction avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="3cb30-258">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="3cb30-260">Ne pas : laisser les utilisateurs bloqués</span><span class="sxs-lookup"><span data-stu-id="3cb30-260">Don't: Leave users stranded</span></span>

<span data-ttu-id="3cb30-261">Les utilisateurs abandonneront rapidement votre robot s’ils ne peuvent pas résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="3cb30-261">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="3cb30-262">Interactions complexes</span><span class="sxs-lookup"><span data-stu-id="3cb30-262">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="3cb30-264">Do : utiliser des onglets ou des modules de tâches</span><span class="sxs-lookup"><span data-stu-id="3cb30-264">Do: Use task modules or tabs</span></span>

<span data-ttu-id="3cb30-265">Si votre bot fournit une réponse qui nécessite quelques étapes supplémentaires, vous pouvez créer un lien vers un onglet ou un module de tâches pour effectuer la tâche ou le flux.</span><span class="sxs-lookup"><span data-stu-id="3cb30-265">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="3cb30-267">N’effectuez pas les interactions fastidieux</span><span class="sxs-lookup"><span data-stu-id="3cb30-267">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="3cb30-268">Une conversation complète pour effectuer une tâche unique est lente et excessivement complexe.</span><span class="sxs-lookup"><span data-stu-id="3cb30-268">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="3cb30-269">Le développeur doit également tenir compte des modifications d’État (par exemple, le délai d’expiration de conversation ou l’envoi d’un message d’annulation).</span><span class="sxs-lookup"><span data-stu-id="3cb30-269">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="3cb30-270">Confidentialité</span><span class="sxs-lookup"><span data-stu-id="3cb30-270">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="3cb30-272">Do : afficher uniquement les informations sensibles dans un contexte personnel</span><span class="sxs-lookup"><span data-stu-id="3cb30-272">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="3cb30-273">Si votre bot se trouve dans un canal ou une conversation de groupe, nous vous recommandons de diriger les utilisateurs vers un emplacement privé (par exemple, un module de tâches, un onglet ou un navigateur) pour afficher les informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="3cb30-273">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="Exemple illustrant une meilleure pratique de robot." border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="3cb30-275">Ne pas : certains contenus ne sont pas destinés à être vus par tout le monde</span><span class="sxs-lookup"><span data-stu-id="3cb30-275">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="3cb30-276">Votre bot ne doit pas révéler d’informations sensibles à un groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="3cb30-276">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a><span data-ttu-id="3cb30-277">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="3cb30-277">Learn more</span></span>

<span data-ttu-id="3cb30-278">Ces autres instructions peuvent vous aider dans votre conception de robot :</span><span class="sxs-lookup"><span data-stu-id="3cb30-278">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="3cb30-279">Conception de votre application personnelle</span><span class="sxs-lookup"><span data-stu-id="3cb30-279">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="3cb30-280">Conception de cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="3cb30-280">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="3cb30-281">Création de modules de tâches</span><span class="sxs-lookup"><span data-stu-id="3cb30-281">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a><span data-ttu-id="3cb30-282">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="3cb30-282">Validate your design</span></span>

<span data-ttu-id="3cb30-283">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="3cb30-283">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cb30-284">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="3cb30-284">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
