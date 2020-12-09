---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie teams et obtenir le kit d’interface utilisateur Microsoft Teams.
keywords: recommandations pour la conception des équipes de référence des extensions de messagerie conseils
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604821"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="d4205-104">Conception de votre extension de messagerie Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="d4205-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="d4205-105">Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou d’agir sur un message sans quitter la conversation.</span><span class="sxs-lookup"><span data-stu-id="d4205-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>

<span data-ttu-id="d4205-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer les extensions de messagerie dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d4205-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d4205-107">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="d4205-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d4205-108">Vous trouverez des instructions de conception de l’extension de messagerie complète, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d4205-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4205-109">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="d4205-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="d4205-110">Ajouter une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-110">Add a messaging extension</span></span>

<span data-ttu-id="d4205-111">Vous pouvez ajouter une extension de messagerie dans les contextes de teams suivants :</span><span class="sxs-lookup"><span data-stu-id="d4205-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="d4205-112">À partir du magasin de Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="d4205-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="d4205-113">Dans un canal, une conversation ou une réunion (avant, pendant et après) à proximité de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="d4205-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="d4205-114">Il est important de noter si vous ajoutez une extension de messagerie à l’un de ces emplacements, vous seul pouvez l’utiliser dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="d4205-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="d4205-115">L’exemple suivant montre comment ajouter une extension de messagerie dans un canal.</span><span class="sxs-lookup"><span data-stu-id="d4205-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Cet exemple montre comment ajouter une extension de messagerie à proximité de la zone de composition d’un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="d4205-117">Configurer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-117">Set up a messaging extension</span></span>

<span data-ttu-id="d4205-118">L’authentification n’est pas obligatoire, mais si votre application est semblable à un outil de suivi des tickets, vous aurez peut-être besoin que des personnes se connectent pour utiliser l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d4205-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="d4205-119">Pour assurer la cohérence entre les applications Teams, vous ne pouvez pas personnaliser l’écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="d4205-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="d4205-120">Si vous utilisez l’authentification unique (SSO), les utilisateurs se connectent automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d4205-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Exemple affiche l’écran de configuration de l’extension de messagerie avec un bouton de connexion." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="d4205-122">Types d’extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-122">Types of messaging extensions</span></span>

<span data-ttu-id="d4205-123">Les extensions de messagerie peuvent être dotées de commandes de recherche, de commandes d’action ou des deux.</span><span class="sxs-lookup"><span data-stu-id="d4205-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="d4205-124">Vos commandes dépendent des fonctionnalités de votre application et de la façon dont elles rentrent dans les cas d’utilisation de teams.</span><span class="sxs-lookup"><span data-stu-id="d4205-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="d4205-125">Commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="d4205-125">Search commands</span></span>

<span data-ttu-id="d4205-126">Grâce aux commandes de recherche, les utilisateurs peuvent utiliser votre extension de messagerie pour trouver rapidement du contenu externe et l’insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="d4205-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="d4205-127">Les commandes de recherche sont généralement disponibles dans la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="d4205-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="d4205-128">Par exemple, vous pouvez commencer ou ajouter une discussion en partageant une partie de contenu, sans jamais quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="d4205-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple montre une extension de messagerie basée sur la recherche lancée à partir de la zone de composition." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="d4205-130">Options de disposition de la zone de composition</span><span class="sxs-lookup"><span data-stu-id="d4205-130">Compose box layout options</span></span>

<span data-ttu-id="d4205-131">Vous disposez de plusieurs options pour afficher les résultats de recherche d’extension de messagerie, y compris les [affichages de liste et de grille](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span><span class="sxs-lookup"><span data-stu-id="d4205-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations illustrant les options de disposition pour les résultats de recherche de l’extension de messagerie." border="false":::

### <a name="action-commands"></a><span data-ttu-id="d4205-133">Commandes d’action</span><span class="sxs-lookup"><span data-stu-id="d4205-133">Action commands</span></span>

<span data-ttu-id="d4205-134">Les commandes d’action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes au sein de teams.</span><span class="sxs-lookup"><span data-stu-id="d4205-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="d4205-135">Par exemple, si votre application suit les commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d’un collègue de droite à l’intérieur de la conversation.</span><span class="sxs-lookup"><span data-stu-id="d4205-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="d4205-136">Les extensions de messagerie basées sur les actions nécessitent fréquemment que les utilisateurs exécutent un formulaire ou un autre type de configuration dans un modal.</span><span class="sxs-lookup"><span data-stu-id="d4205-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="d4205-137">Vous pouvez créer ces expériences avec des [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="d4205-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="d4205-138">Ouverture d’une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-138">Open a messaging extension</span></span>

<span data-ttu-id="d4205-139">La zone de composition et les messages/publications sont les contextes principaux dans lesquels les utilisateurs utilisent les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d4205-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="d4205-140">De la zone de composition</span><span class="sxs-lookup"><span data-stu-id="d4205-140">From the compose box</span></span>

<span data-ttu-id="d4205-141">Une fois ajoutés, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l’icône de votre application sous la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="d4205-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="d4205-142">Dans cet exemple, l’extension est dotée de commandes de recherche et d’action.</span><span class="sxs-lookup"><span data-stu-id="d4205-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir de la zone de composition." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="d4205-144">À partir d’un message de conversation ou d’un billet de canal</span><span class="sxs-lookup"><span data-stu-id="d4205-144">From a chat message or channel post</span></span>

Une fois ajoutés, les utilisateurs peuvent sélectionner l’icône **plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: sur le message de conversation ou le billet de canal pour trouver les commandes d’action de votre extension. <span data-ttu-id="d4205-146">Votre extension peut être indiquée sous **autres actions** en fonction de l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="d4205-146">Your extension may be listed under **More actions** based on usage.</span></span>

#### <a name="chat-message"></a><span data-ttu-id="d4205-147">Message de conversation</span><span class="sxs-lookup"><span data-stu-id="d4205-147">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un message de conversation." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="d4205-149">Billet de canal</span><span class="sxs-lookup"><span data-stu-id="d4205-149">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un billet de canal." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="d4205-151">Utiliser une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-151">Use a messaging extension</span></span>

<span data-ttu-id="d4205-152">Les scénarios suivants montrent les principales façons dont les utilisateurs utilisent les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d4205-152">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="d4205-153">Insérer du contenu dans un message</span><span class="sxs-lookup"><span data-stu-id="d4205-153">Insert content into a message</span></span>

<span data-ttu-id="d4205-154">**1. Sélectionnez une extension de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="d4205-154">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d4205-155">Les utilisateurs peuvent rechercher le contenu qu’ils souhaitent partager à partir de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="d4205-155">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Cet exemple montre comment afficher un utilisateur qui recherche du contenu à insérer à partir de la zone de composition." border="false":::

<span data-ttu-id="d4205-157">**2. Insérez du contenu**.</span><span class="sxs-lookup"><span data-stu-id="d4205-157">**2. Insert content**.</span></span> <span data-ttu-id="d4205-158">Une fois publiés, les autres utilisateurs peuvent répondre ou sélectionner le contenu pour afficher plus d’informations dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-158">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple affiche un utilisateur publiant du contenu dans une conversation de canal." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="d4205-160">Effectuer une action sur un message</span><span class="sxs-lookup"><span data-stu-id="d4205-160">Take action on a message</span></span>

<span data-ttu-id="d4205-161">**1. Sélectionnez une extension de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="d4205-161">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d4205-162">Votre application peut inclure une ou plusieurs commandes d’action.</span><span class="sxs-lookup"><span data-stu-id="d4205-162">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple montre un utilisateur sélectionnant une commande action d’extension de messagerie." border="false":::

<span data-ttu-id="d4205-164">**2. Terminez l’action**.</span><span class="sxs-lookup"><span data-stu-id="d4205-164">**2. Complete the action**.</span></span> <span data-ttu-id="d4205-165">Votre application peut recevoir et traiter tout contenu ou données envoyé par l’action de message.</span><span class="sxs-lookup"><span data-stu-id="d4205-165">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="d4205-166">Cela permet aux utilisateurs de rester dans leur conversation et, dans l’exemple suivant, de ne pas se soucier de saisir directement des informations dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-166">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Cet exemple montre comment afficher un utilisateur qui recherche du contenu à insérer à partir de la zone de composition." border="false":::

### <a name="preview-links"></a><span data-ttu-id="d4205-168">Aperçu des liens</span><span class="sxs-lookup"><span data-stu-id="d4205-168">Preview links</span></span>

<span data-ttu-id="d4205-169">Les extensions de messagerie vous permettent également d’insérer des liens enrichis à partir d’une URL reconnue dans un message (cette fonctionnalité est appelée [Link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="d4205-169">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="d4205-170">**1. collez un lien reconnu** dans la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="d4205-170">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montre comment un utilisateur colle un lien dans la zone compost." border="false":::

<span data-ttu-id="d4205-172">**2. Insérez du contenu**.</span><span class="sxs-lookup"><span data-stu-id="d4205-172">**2. Insert content**.</span></span> <span data-ttu-id="d4205-173">Si votre application reconnaît l’URL dans la zone de composition, elle affiche le lien sous la forme d’une carte qui fournit un aperçu riche en contenu du contenu Web.</span><span class="sxs-lookup"><span data-stu-id="d4205-173">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="d4205-174">(Pour plus d’informations, consultez la rubrique [instructions de conception des cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) .)</span><span class="sxs-lookup"><span data-stu-id="d4205-174">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Cet exemple montre comment l’URL, telle qu’elle est reconnue par votre application, inclut du contenu enrichi dans la zone de composition." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="d4205-176">Gérer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-176">Manage a messaging extension</span></span>

<span data-ttu-id="d4205-177">En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d4205-177">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d4205-178">Anatomie</span><span class="sxs-lookup"><span data-stu-id="d4205-178">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="d4205-179">Extension de messagerie dans la zone de composition</span><span class="sxs-lookup"><span data-stu-id="d4205-179">Messaging extension in the compose box</span></span>

<span data-ttu-id="d4205-180">L’exemple suivant est une extension de messagerie ouverte à partir de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="d4205-180">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une extension de messagerie dans la zone de composition." border="false":::

|<span data-ttu-id="d4205-182">Compteur</span><span class="sxs-lookup"><span data-stu-id="d4205-182">Counter</span></span>|<span data-ttu-id="d4205-183">Description</span><span class="sxs-lookup"><span data-stu-id="d4205-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d4205-184">1</span><span class="sxs-lookup"><span data-stu-id="d4205-184">1</span></span>|<span data-ttu-id="d4205-185">**Logo** de l’application : icône de couleur du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-185">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="d4205-186">2 </span><span class="sxs-lookup"><span data-stu-id="d4205-186">2</span></span>|<span data-ttu-id="d4205-187">**Nom** de l’application : nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-187">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d4205-188">3 </span><span class="sxs-lookup"><span data-stu-id="d4205-188">3</span></span>|<span data-ttu-id="d4205-189">**Icône de menu commandes d’action (facultatif)**: ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="d4205-189">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d4205-190">4 </span><span class="sxs-lookup"><span data-stu-id="d4205-190">4</span></span>|<span data-ttu-id="d4205-191">**Zone de recherche**: permet aux utilisateurs de trouver le contenu d’application qu’ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="d4205-191">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d4205-192">5 </span><span class="sxs-lookup"><span data-stu-id="d4205-192">5</span></span>|<span data-ttu-id="d4205-193">**Menu de l’onglet (facultatif)**: fournit plusieurs catégories de contenu.</span><span class="sxs-lookup"><span data-stu-id="d4205-193">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d4205-194">6 </span><span class="sxs-lookup"><span data-stu-id="d4205-194">6</span></span>|<span data-ttu-id="d4205-195">**Menu commandes d’action (facultatif)**: affiche la liste des commandes d’action (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="d4205-195">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d4205-196">7 </span><span class="sxs-lookup"><span data-stu-id="d4205-196">7</span></span>|<span data-ttu-id="d4205-197">**Contenu** de l’application : principalement pour afficher les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="d4205-197">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="d4205-198">Cet exemple utilise la mise en forme de liste (la disposition grille est une autre option).</span><span class="sxs-lookup"><span data-stu-id="d4205-198">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="d4205-199">8 </span><span class="sxs-lookup"><span data-stu-id="d4205-199">8</span></span>|<span data-ttu-id="d4205-200">**Logo** de l’application : icône de plan du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-200">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="d4205-201">Menu gestion des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-201">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un menu de gestion des extensions de messagerie." border="false":::

|<span data-ttu-id="d4205-203">Compteur</span><span class="sxs-lookup"><span data-stu-id="d4205-203">Counter</span></span>|<span data-ttu-id="d4205-204">Description</span><span class="sxs-lookup"><span data-stu-id="d4205-204">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d4205-205">1</span><span class="sxs-lookup"><span data-stu-id="d4205-205">1</span></span>|<span data-ttu-id="d4205-206">**Détacher**: disponible si l’utilisateur a épinglé votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-206">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="d4205-207">2 </span><span class="sxs-lookup"><span data-stu-id="d4205-207">2</span></span>|<span data-ttu-id="d4205-208">**Remove**: supprime l’extension de messagerie du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="d4205-208">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d4205-209">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="d4205-209">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="d4205-210">Configuration et utilisation générale</span><span class="sxs-lookup"><span data-stu-id="d4205-210">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="d4205-212">Do : intégration avec l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d4205-212">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="d4205-213">SSO rend le processus de connexion plus facile, plus rapide et plus sécurisé.</span><span class="sxs-lookup"><span data-stu-id="d4205-213">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="d4205-214">En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a pas besoin de se connecter à nouveau pour accéder à l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d4205-214">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="d4205-216">Ne pas : empêcher les utilisateurs de participer à la conversation</span><span class="sxs-lookup"><span data-stu-id="d4205-216">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="d4205-217">Les extensions de messagerie sont des raccourcis qui sont supposés réduire le changement de contexte.</span><span class="sxs-lookup"><span data-stu-id="d4205-217">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="d4205-218">Votre extension ne doit pas, par exemple, diriger les utilisateurs vers une page Web en dehors de teams.</span><span class="sxs-lookup"><span data-stu-id="d4205-218">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="d4205-219">Do : mettez en surbrillance votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="d4205-219">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="d4205-220">Les extensions de messagerie ne sont pas toujours faciles à trouver.</span><span class="sxs-lookup"><span data-stu-id="d4205-220">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="d4205-221">Incluez des captures d’écran expliquant comment l’utiliser dans la page de détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-221">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="d4205-222">Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide sur les extensions de messagerie dans une présentation de robot.</span><span class="sxs-lookup"><span data-stu-id="d4205-222">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="d4205-223">Création</span><span class="sxs-lookup"><span data-stu-id="d4205-223">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="d4205-225">Do : Permettez à teams de gérer une partie du travail de conception si cela est possible</span><span class="sxs-lookup"><span data-stu-id="d4205-225">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="d4205-226">Si cela est utile pour vos cas d’utilisation, envisagez de créer une extension de messagerie basée sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="d4205-226">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="d4205-227">Teams affiche ces types d’extensions avec des thèmes et une accessibilité intégrés.</span><span class="sxs-lookup"><span data-stu-id="d4205-227">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="d4205-229">Ne pas : incorporer l’intégralité de votre application dans un module de tâches</span><span class="sxs-lookup"><span data-stu-id="d4205-229">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="d4205-230">Si votre extension de messagerie nécessite des commandes d’action, conservez le module de tâches simple et Affichez uniquement les composants requis pour effectuer l’action.</span><span class="sxs-lookup"><span data-stu-id="d4205-230">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d4205-231">Thèmes</span><span class="sxs-lookup"><span data-stu-id="d4205-231">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="d4205-233">Do : tirer parti des jetons de couleur teams</span><span class="sxs-lookup"><span data-stu-id="d4205-233">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="d4205-234">Chaque thème teams possède son propre jeu de couleurs.</span><span class="sxs-lookup"><span data-stu-id="d4205-234">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="d4205-235">Pour gérer automatiquement les modifications de thème, utilisez des <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (IU Fluent)</a> dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="d4205-235">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="d4205-237">Ne pas : valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="d4205-237">Don't: Hard code color values</span></span>

<span data-ttu-id="d4205-238">Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendre plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="d4205-238">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="d4205-239">Actions</span><span class="sxs-lookup"><span data-stu-id="d4205-239">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="d4205-241">Do : inclure des commandes d’action qui ont un sens dans le contexte</span><span class="sxs-lookup"><span data-stu-id="d4205-241">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="d4205-242">Les actions de message doivent être liées à ce qu’un utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="d4205-242">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="d4205-243">Par exemple, fournissez aux utilisateurs un raccourci pour la création d’un problème ou d’un élément de travail à l’aide du texte dans la publication d’une personne.</span><span class="sxs-lookup"><span data-stu-id="d4205-243">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple illustrant une meilleure pratique de l’extension de messagerie." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="d4205-245">Ne pas : inclure les commandes d’actions qui ne sont pas contextuelles</span><span class="sxs-lookup"><span data-stu-id="d4205-245">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="d4205-246">Une action de message pour **afficher votre tableau de bord** semblerait probablement déconnectée de la plupart des conversations.</span><span class="sxs-lookup"><span data-stu-id="d4205-246">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="d4205-247">Recherches</span><span class="sxs-lookup"><span data-stu-id="d4205-247">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="d4205-248">Do : afficher les résultats de la recherche lors de la saisie</span><span class="sxs-lookup"><span data-stu-id="d4205-248">Do: Show search results while typing</span></span>

<span data-ttu-id="d4205-249">Fournissez les suggestions de résultats de recherche pendant que les utilisateurs tapent.</span><span class="sxs-lookup"><span data-stu-id="d4205-249">Provide suggested search results while users type.</span></span> <span data-ttu-id="d4205-250">Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un minimum de caractères.</span><span class="sxs-lookup"><span data-stu-id="d4205-250">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="d4205-251">Ne pas : exiger que les utilisateurs envoient une requête</span><span class="sxs-lookup"><span data-stu-id="d4205-251">Don't: Require users to submit a query</span></span>

<span data-ttu-id="d4205-252">Vous pouvez faire en sorte que les utilisateurs appuient sur une touche ou sélectionnent un bouton pour envoyer des requêtes à votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-252">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="d4205-253">Bien que cela puisse être plus facile sur votre service d’application, il se peut que les utilisateurs ne voient pas les résultats de recherche en temps réel lorsqu’ils sont tapés.</span><span class="sxs-lookup"><span data-stu-id="d4205-253">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="d4205-254">Do : prendre en compte les requêtes à zéro terme</span><span class="sxs-lookup"><span data-stu-id="d4205-254">Do: Consider zero-term queries</span></span>

<span data-ttu-id="d4205-255">Par exemple, avant qu’un utilisateur n’écrit quoi que ce soit dans la zone de recherche, affichez ce qu’il a consulté en dernier sur votre application.</span><span class="sxs-lookup"><span data-stu-id="d4205-255">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="d4205-256">Il est possible qu’ils souhaitent insérer ce contenu dans leur conversation.</span><span class="sxs-lookup"><span data-stu-id="d4205-256">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="d4205-257">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="d4205-257">Validate your design</span></span>

<span data-ttu-id="d4205-258">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="d4205-258">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4205-259">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="d4205-259">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
