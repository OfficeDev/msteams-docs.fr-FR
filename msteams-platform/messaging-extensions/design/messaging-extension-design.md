---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie Teams et obtenir le Kit d'interface utilisateur Microsoft Teams.
keywords: "Recommandations en matière de conception d'équipes : conseils sur les extensions de messagerie"
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: c616d8e3e7c40ae124f96cb80a42873f9aaa7865
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697010"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="ffc9b-104">Conception de votre extension de messagerie Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ffc9b-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="ffc9b-105">Les extensions de messagerie sont des raccourcis pour insérer du contenu d'application ou agir sur un message sans sortir de la conversation.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="ffc9b-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des extensions de messagerie dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ffc9b-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ffc9b-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ffc9b-108">Vous trouverez des instructions complètes sur la conception des extensions de messagerie, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ffc9b-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="ffc9b-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="ffc9b-110">Ajouter une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-110">Add a messaging extension</span></span>

<span data-ttu-id="ffc9b-111">Vous pouvez ajouter une extension de messagerie dans les contextes Teams suivants :</span><span class="sxs-lookup"><span data-stu-id="ffc9b-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="ffc9b-112">À partir de Teams Store (AppSource).</span><span class="sxs-lookup"><span data-stu-id="ffc9b-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="ffc9b-113">Dans un canal, une conversation ou une réunion (avant, pendant et après) près de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="ffc9b-114">Il est intéressant de noter que si vous ajoutez une extension de messagerie à l'un de ces endroits, vous pouvez uniquement l'utiliser dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="ffc9b-115">L'exemple suivant montre comment ajouter une extension de messagerie dans un canal.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="L'exemple montre comment ajouter une extension de messagerie près de la zone de composition dans un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="ffc9b-117">Configurer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-117">Set up a messaging extension</span></span>

<span data-ttu-id="ffc9b-118">L'authentification n'est pas obligatoire, mais si votre application ressemble à un outil de suivi des tickets, vous devrez peut-être que des personnes se connectent pour utiliser l'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="ffc9b-119">Pour des raisons de cohérence entre les applications Teams, vous ne pouvez pas personnaliser l'écran de la signature.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="ffc9b-120">Si vous utilisez l'authentification unique(SSO), les utilisateurs sont automatiquement connectés.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="L'exemple illustre l'écran de configuration de l'extension de messagerie avec un bouton de signature." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="ffc9b-122">Types d'extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-122">Types of messaging extensions</span></span>

<span data-ttu-id="ffc9b-123">Les extensions de messagerie peuvent avoir des commandes de recherche, des commandes d'action ou les deux.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="ffc9b-124">Vos commandes dépendent des fonctionnalités de votre application et de leur ajustement dans les cas d'utilisation de Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="ffc9b-125">Commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="ffc9b-125">Search commands</span></span>

<span data-ttu-id="ffc9b-126">Grâce aux commandes de recherche, les utilisateurs peuvent utiliser votre extension de messagerie pour trouver rapidement du contenu externe et l'insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="ffc9b-127">Les commandes de recherche sont généralement disponibles dans la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="ffc9b-128">Par exemple, vous pouvez commencer ou ajouter une discussion en partageant un élément de contenu, sans quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple d'une extension de messagerie basée sur la recherche lancée à partir de la zone de composition." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="ffc9b-130">Options de disposition de zone de composition</span><span class="sxs-lookup"><span data-stu-id="ffc9b-130">Compose box layout options</span></span>

<span data-ttu-id="ffc9b-131">Certaines options s'offrent à vous pour afficher les résultats de recherche d'extension de messagerie, y compris les affichages liste [et grille.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="ffc9b-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de disposition pour les résultats de recherche d'extension de messagerie." border="false":::

### <a name="action-commands"></a><span data-ttu-id="ffc9b-133">Commandes d’action</span><span class="sxs-lookup"><span data-stu-id="ffc9b-133">Action commands</span></span>

<span data-ttu-id="ffc9b-134">Les commandes d'action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes au sein de Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="ffc9b-135">Par exemple, si votre application suit les commandes, un utilisateur peut créer une commande à l'aide du contenu du message d'un collègue directement dans sa conversation.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="ffc9b-136">Les extensions de messagerie basées sur une action nécessitent fréquemment que les utilisateurs remplissent un formulaire ou tout autre type de configuration dans une configuration modale.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="ffc9b-137">Vous pouvez créer ces expériences avec [des modules de tâche.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="ffc9b-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="ffc9b-138">Ouvrir une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-138">Open a messaging extension</span></span>

<span data-ttu-id="ffc9b-139">La zone de composition et les messages/publications sont les principaux contextes dans lequel les personnes utilisent les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="ffc9b-140">À partir de la zone de composition</span><span class="sxs-lookup"><span data-stu-id="ffc9b-140">From the compose box</span></span>

<span data-ttu-id="ffc9b-141">Une fois ajouté, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l'icône de votre application sous la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="ffc9b-142">Dans cet exemple, l'extension dispose de commandes de recherche et d'action.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="L'exemple montre comment ouvrir une extension de messagerie à partir de la zone de composition." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="ffc9b-144">À partir d'un message de conversation ou d'un billet de canal</span><span class="sxs-lookup"><span data-stu-id="ffc9b-144">From a chat message or channel post</span></span>

Une fois ajoutés, les utilisateurs peuvent sélectionner l'icône **Plus** dans le message de conversation ou le billet de canal pour trouver les commandes :::image type="icon" source="../../assets/icons/teams-client-more.png"::: d'action de votre extension. <span data-ttu-id="ffc9b-146">Votre extension peut être répertoriée sous **Plus d'actions** basées sur l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="ffc9b-147">La prise en charge d'autres actions à partir d'un message de conversation ou d'un billet de canal n'est pas disponible sur la plateforme mobile Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="ffc9b-148">Message de conversation</span><span class="sxs-lookup"><span data-stu-id="ffc9b-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="L'exemple montre comment ouvrir une extension de messagerie à partir d'un message de conversation." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="ffc9b-150">Billet de canal</span><span class="sxs-lookup"><span data-stu-id="ffc9b-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="L'exemple montre comment ouvrir une extension de messagerie à partir d'un billet de canal." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="ffc9b-152">Utiliser une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-152">Use a messaging extension</span></span>

<span data-ttu-id="ffc9b-153">Les scénarios suivants montrent les principales façons dont les personnes utilisent les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="ffc9b-154">Insérer du contenu dans un message</span><span class="sxs-lookup"><span data-stu-id="ffc9b-154">Insert content into a message</span></span>

<span data-ttu-id="ffc9b-155">**1. Sélectionnez une extension de messagerie.**</span><span class="sxs-lookup"><span data-stu-id="ffc9b-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="ffc9b-156">Les utilisateurs peuvent rechercher le contenu qu'ils souhaitent partager à partir de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple : un utilisateur recherche le contenu à insérer à partir de la zone de composition." border="false":::

<span data-ttu-id="ffc9b-158">**2. Insérer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-158">**2. Insert content**.</span></span> <span data-ttu-id="ffc9b-159">Une fois publié, d'autres personnes peuvent répondre ou sélectionner le contenu pour voir plus d'informations dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple : un utilisateur publie du contenu dans une conversation de canal." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="ffc9b-161">Prendre des mesures sur un message</span><span class="sxs-lookup"><span data-stu-id="ffc9b-161">Take action on a message</span></span>

<span data-ttu-id="ffc9b-162">**1. Sélectionnez une extension de messagerie.**</span><span class="sxs-lookup"><span data-stu-id="ffc9b-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="ffc9b-163">Votre application peut inclure une ou plusieurs commandes d'action.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple : un utilisateur sélectionne une commande d'action d'extension de messagerie." border="false":::

<span data-ttu-id="ffc9b-165">**2. Terminez l'action.**</span><span class="sxs-lookup"><span data-stu-id="ffc9b-165">**2. Complete the action**.</span></span> <span data-ttu-id="ffc9b-166">Votre application peut recevoir et traiter tout contenu ou toute donnée envoyé par l'action de message.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="ffc9b-167">Cela permet aux utilisateurs de rester dans leur conversation et, dans l'exemple suivant, de ne pas se soucier d'entrer des informations directement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d'agir sur un message." border="false":::

### <a name="preview-links"></a><span data-ttu-id="ffc9b-169">Liens d'aperçu</span><span class="sxs-lookup"><span data-stu-id="ffc9b-169">Preview links</span></span>

<span data-ttu-id="ffc9b-170">Les extensions de messagerie vous permettent également d'insérer des liens enrichis à partir d'une URL reconnue dans un message (cette fonctionnalité est appelée déploiement de [lien).)](../../messaging-extensions/how-to/link-unfurling.md)</span><span class="sxs-lookup"><span data-stu-id="ffc9b-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="ffc9b-171">**1. Collez un lien reconnu dans** la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="L'exemple montre un utilisateur qui a passé un lien dans le cadre de l'exemple." border="false":::

<span data-ttu-id="ffc9b-173">**2. Insérer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-173">**2. Insert content**.</span></span> <span data-ttu-id="ffc9b-174">Si votre application reconnaît l'URL dans la zone de composition, elle affiche le lien sous la mesure d'une carte qui fournit un aperçu enrichi de contenu du contenu web.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="ffc9b-175">(Pour plus [d'informations, voir](../../task-modules-and-cards/cards/design-effective-cards.md) les recommandations en matière de conception des cartes adaptatives.)</span><span class="sxs-lookup"><span data-stu-id="ffc9b-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="L'exemple montre comment l'URL, car elle est reconnue par votre application, inclut du contenu enrichi dans la zone de composition." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="ffc9b-177">Gérer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-177">Manage a messaging extension</span></span>

<span data-ttu-id="ffc9b-178">En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="ffc9b-179">Anatomie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="ffc9b-180">Extension de messagerie dans la zone de composition</span><span class="sxs-lookup"><span data-stu-id="ffc9b-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="ffc9b-181">L'exemple suivant est une extension de messagerie ouverte à partir de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'une extension de messagerie dans la zone de composition." border="false":::

|<span data-ttu-id="ffc9b-183">Compteur</span><span class="sxs-lookup"><span data-stu-id="ffc9b-183">Counter</span></span>|<span data-ttu-id="ffc9b-184">Description</span><span class="sxs-lookup"><span data-stu-id="ffc9b-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ffc9b-185">1</span><span class="sxs-lookup"><span data-stu-id="ffc9b-185">1</span></span>|<span data-ttu-id="ffc9b-186">**Logo de l'application**: icône couleur du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="ffc9b-187">2</span><span class="sxs-lookup"><span data-stu-id="ffc9b-187">2</span></span>|<span data-ttu-id="ffc9b-188">**Nom de l'application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="ffc9b-189">3</span><span class="sxs-lookup"><span data-stu-id="ffc9b-189">3</span></span>|<span data-ttu-id="ffc9b-190">**Icône de menu Commandes d'action (facultatif)**: ouvre une liste de commandes d'action pour votre extension de messagerie (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="ffc9b-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="ffc9b-191">4 </span><span class="sxs-lookup"><span data-stu-id="ffc9b-191">4</span></span>|<span data-ttu-id="ffc9b-192">**Zone de recherche**: permet aux utilisateurs de trouver le contenu d'application qu'ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="ffc9b-193">5 </span><span class="sxs-lookup"><span data-stu-id="ffc9b-193">5</span></span>|<span data-ttu-id="ffc9b-194">**Menu Onglet (facultatif)**: fournit plusieurs catégories de contenu.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="ffc9b-195">6 </span><span class="sxs-lookup"><span data-stu-id="ffc9b-195">6</span></span>|<span data-ttu-id="ffc9b-196">**Menu commandes d'action (facultatif)**: affiche la liste des commandes d'action (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="ffc9b-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="ffc9b-197">7 </span><span class="sxs-lookup"><span data-stu-id="ffc9b-197">7</span></span>|<span data-ttu-id="ffc9b-198">**Contenu de l'application**: principalement pour afficher les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="ffc9b-199">L'exemple ci-dessous utilise la disposition de liste (la disposition de grille est une autre option).</span><span class="sxs-lookup"><span data-stu-id="ffc9b-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="ffc9b-200">8 </span><span class="sxs-lookup"><span data-stu-id="ffc9b-200">8</span></span>|<span data-ttu-id="ffc9b-201">**Logo de l'application**: icône de plan du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="ffc9b-202">Menu gestion des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un menu de gestion des extensions de messagerie." border="false":::

|<span data-ttu-id="ffc9b-204">Compteur</span><span class="sxs-lookup"><span data-stu-id="ffc9b-204">Counter</span></span>|<span data-ttu-id="ffc9b-205">Description</span><span class="sxs-lookup"><span data-stu-id="ffc9b-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ffc9b-206">1</span><span class="sxs-lookup"><span data-stu-id="ffc9b-206">1</span></span>|<span data-ttu-id="ffc9b-207">**Unpin**: disponible si l'utilisateur a épinglé votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="ffc9b-208">2</span><span class="sxs-lookup"><span data-stu-id="ffc9b-208">2</span></span>|<span data-ttu-id="ffc9b-209">**Supprimer**: supprime l'extension de messagerie du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="ffc9b-210">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="ffc9b-210">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="ffc9b-211">Configuration et utilisation générale</span><span class="sxs-lookup"><span data-stu-id="ffc9b-211">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur l'installation et l'utilisation générale." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="ffc9b-213">À faire : intégrer avec l' sign-on unique</span><span class="sxs-lookup"><span data-stu-id="ffc9b-213">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="ffc9b-214">SSO facilite, accélère et sécurisation le processus de se connecte.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-214">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="ffc9b-215">En outre, si un utilisateur s'est déjà connecté à votre application personnelle, il n'a pas besoin de se connecter à nouveau pour accéder à l'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-215">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple d'intégration à l' sign-on unique." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="ffc9b-217">À ne pas faire : éloignez les utilisateurs de la conversation</span><span class="sxs-lookup"><span data-stu-id="ffc9b-217">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="ffc9b-218">Les extensions de messagerie sont des raccourcis supposés réduire le changement de contexte.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-218">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="ffc9b-219">Votre extension ne doit pas, par exemple, diriger les utilisateurs vers une page web en dehors de Teams.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-219">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="ffc9b-220">À faire : mettre en surbrillez votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-220">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="ffc9b-221">Les extensions de messagerie ne sont pas toujours faciles à trouver.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-221">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="ffc9b-222">Incluez des captures d'écran de son utilisation dans la page de détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-222">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="ffc9b-223">Si votre application inclut également un bot, vous pouvez inclure la documentation d'aide sur l'extension de messagerie dans une visite guidée du bot.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-223">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="ffc9b-224">Templating</span><span class="sxs-lookup"><span data-stu-id="ffc9b-224">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple de modèle." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="ffc9b-226">À faire : laisser Teams gérer une partie du travail de conception si possible</span><span class="sxs-lookup"><span data-stu-id="ffc9b-226">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="ffc9b-227">Si cela est utile pour vos cas d'utilisation, envisagez de créer une extension de messagerie basée sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-227">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="ffc9b-228">Teams restituera ces types d'extensions avec des modèles intégrés et une accessibilité.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-228">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple de gestion du travail de conception." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="ffc9b-230">À ne pas faire : incorporer l'intégralité de votre application dans un module de tâche</span><span class="sxs-lookup"><span data-stu-id="ffc9b-230">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="ffc9b-231">Si votre extension de messagerie nécessite des commandes d'action, maintenez le module de tâche simple et affichez uniquement les composants requis pour effectuer l'action.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-231">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="ffc9b-232">Thèmes</span><span class="sxs-lookup"><span data-stu-id="ffc9b-232">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur les themings." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="ffc9b-234">À faire : tirer parti des jetons de couleur Teams</span><span class="sxs-lookup"><span data-stu-id="ffc9b-234">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="ffc9b-235">Chaque thème Teams possède son propre modèle de couleurs.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-235">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="ffc9b-236">Pour gérer automatiquement les modifications de thème, utilisez des jetons <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de couleur (interface</a> utilisateur Fluent) dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-236">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="ffc9b-238">À ne pas faire : valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="ffc9b-238">Don't: Hard code color values</span></span>

<span data-ttu-id="ffc9b-239">Si vous n'utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prenons plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-239">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="ffc9b-240">Actions</span><span class="sxs-lookup"><span data-stu-id="ffc9b-240">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="ffc9b-242">À faire : inclure des commandes d'action qui ont du sens dans le contexte</span><span class="sxs-lookup"><span data-stu-id="ffc9b-242">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="ffc9b-243">Les actions de message doivent être liées à ce qu'un utilisateur regarde.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-243">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="ffc9b-244">Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou un élément de travail à l'aide du texte dans le billet d'une personne.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-244">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d'action." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="ffc9b-246">À ne pas faire : inclure des commandes d'actions qui ne sont pas contextuelles</span><span class="sxs-lookup"><span data-stu-id="ffc9b-246">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="ffc9b-247">Une action de message pour **afficher votre tableau de** bord semble probablement déconnectée de la plupart des conversations.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-247">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="ffc9b-248">Recherches</span><span class="sxs-lookup"><span data-stu-id="ffc9b-248">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="ffc9b-249">À faire : afficher les résultats de la recherche lors de la saisie</span><span class="sxs-lookup"><span data-stu-id="ffc9b-249">Do: Show search results while typing</span></span>

<span data-ttu-id="ffc9b-250">Fournissez des résultats de recherche suggérés pendant que les utilisateurs tapent.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-250">Provide suggested search results while users type.</span></span> <span data-ttu-id="ffc9b-251">Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un nombre minimal de caractères.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-251">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="ffc9b-252">À ne pas faire : exiger que les utilisateurs soumettent une requête</span><span class="sxs-lookup"><span data-stu-id="ffc9b-252">Don't: Require users to submit a query</span></span>

<span data-ttu-id="ffc9b-253">Vous pouvez faire en sorte que les utilisateurs appuient sur une touche ou sélectionnent un bouton pour envoyer des requêtes à votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-253">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="ffc9b-254">Bien que cela puisse être plus facile sur votre service de services d'application, les personnes peuvent être confondues avec le fait qu'elles ne voient pas les résultats de recherche en temps réel lorsqu'elles tapent.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-254">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="ffc9b-255">À faire : envisagez les requêtes à terme zéro</span><span class="sxs-lookup"><span data-stu-id="ffc9b-255">Do: Consider zero-term queries</span></span>

<span data-ttu-id="ffc9b-256">Par exemple, avant qu'un utilisateur n'écrive quoi que ce soit dans la zone de recherche, affichez ce qu'il a affiché pour la dernière fois sur votre application.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-256">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="ffc9b-257">Il est possible qu'ils souhaitent insérer ce contenu dans leur conversation.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-257">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="ffc9b-258">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="ffc9b-258">Validate your design</span></span>

<span data-ttu-id="ffc9b-259">Si vous envisagez de publier votre application sur AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l'échec des applications lors de l'envoi.</span><span class="sxs-lookup"><span data-stu-id="ffc9b-259">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ffc9b-260">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="ffc9b-260">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
