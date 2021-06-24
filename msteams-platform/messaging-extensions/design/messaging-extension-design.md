---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
keywords: équipes conception lignes directrices référence extension de la messagerie conseils meilleure pratique
author: heath-hamilton
localization_priority: Priority
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: f4d1ba1e6e0b71b37e2b7b2d2a32fb729822ba1c
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037669"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="9535d-104">Conception de votre extension de messagerie Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9535d-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="9535d-105">Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou agir sur un message sans quitter la conversation.</span><span class="sxs-lookup"><span data-stu-id="9535d-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="9535d-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des extensions de messagerie dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="9535d-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9535d-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="9535d-108">Vous trouverez des instructions plus détaillées sur la conception de l’extension de messagerie, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface utilisateur de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9535d-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="9535d-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="9535d-110">Ajouter une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-110">Add a messaging extension</span></span>

<span data-ttu-id="9535d-111">Vous pouvez ajouter une extension de messagerie dans les contextes Teams suivants :</span><span class="sxs-lookup"><span data-stu-id="9535d-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="9535d-112">À partir de Teams Store.</span><span class="sxs-lookup"><span data-stu-id="9535d-112">From the Teams store.</span></span>
* <span data-ttu-id="9535d-113">Dans un canal, une conversation ou une réunion (avant, pendant et après) près de la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="9535d-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="9535d-114">Il est important de noter que si vous ajoutez une extension de messagerie à l’un de ces emplacements, vous seul pouvez l’utiliser dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="9535d-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="9535d-115">L’exemple suivant montre comment ajouter une extension de messagerie dans un canal :</span><span class="sxs-lookup"><span data-stu-id="9535d-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-116">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Exemple montrant comment ajouter une extension de messagerie près de la zone de rédaction dans un canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-118">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="Exemple montrant comment ajouter une extension de messagerie près de la zone de rédaction dans un canal sur un appareil mobile." border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="9535d-120">Configurer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-120">Set up a messaging extension</span></span>

<span data-ttu-id="9535d-121">L'authentification n'est pas obligatoire, mais si votre application est une sorte d'outil de suivi des tickets, il se peut que vous ayez besoin que les utilisateurs se connectent pour utiliser l'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9535d-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="9535d-122">Pour assurer la cohérence entre les applications Teams, vous ne pouvez pas personnaliser l’écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="9535d-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="9535d-123">Si vous utilisez l’authentification unique (SSO), les utilisateurs sont connectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9535d-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-124">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Exemple présentant l'écran de configuration d'une extension de messagerie avec un bouton de connexion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-126">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="Exemple présentant l'écran de configuration d'une extension de messagerie avec un bouton de connexion sur un appareil mobile." border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="9535d-128">Types d’extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-128">Types of messaging extensions</span></span>

<span data-ttu-id="9535d-129">Les extensions de messagerie peuvent avoir des commandes de recherche, des commandes d’action ou les deux.</span><span class="sxs-lookup"><span data-stu-id="9535d-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="9535d-130">Vos commandes dépendent des fonctionnalités de votre application et de la façon dont elles s’intègrent aux cas d'utilisation Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="9535d-131">Commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="9535d-131">Search commands</span></span>

<span data-ttu-id="9535d-132">Avec les commandes de recherche, les utilisateurs peuvent recourir à votre extension de messagerie pour trouver rapidement du contenu externe et les insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="9535d-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="9535d-133">Les commandes de recherche sont généralement disponibles dans la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="9535d-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="9535d-134">Par exemple, vous pouvez démarrer ou ajouter à une discussion en partageant un élément de contenu, sans jamais quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-135">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple d'une extension de messagerie basée sur la recherche et lancée à partir de la zone de rédaction." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-137">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="Exemple d'une extension de messagerie basée sur la recherche et lancée à partir de la zone de rédaction sur un appareil mobile." border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="9535d-139">Options de disposition de la zone de rédaction</span><span class="sxs-lookup"><span data-stu-id="9535d-139">Compose box layout options</span></span>

<span data-ttu-id="9535d-140">Vous disposez de certaines options pour afficher les résultats de recherche de l’extension de messagerie, notamment [liste et les vues de grille](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span><span class="sxs-lookup"><span data-stu-id="9535d-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de disposition pour les résultats de recherche d’extension de messagerie." border="false":::

### <a name="action-commands"></a><span data-ttu-id="9535d-142">Commandes d'action</span><span class="sxs-lookup"><span data-stu-id="9535d-142">Action commands</span></span>

<span data-ttu-id="9535d-143">Les commandes d’action permettent aux utilisateurs de déclencher des actions et de traiter des demandes dans des services externes dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="9535d-144">Par exemple, si votre application assure le suivi des commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d'un collègue, et ce, directement dans sa conversation.</span><span class="sxs-lookup"><span data-stu-id="9535d-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="9535d-145">Les extensions de messagerie basées sur des actions nécessitent souvent que les utilisateurs remplissent un formulaire ou un autre type de configuration au sein d’un modal.</span><span class="sxs-lookup"><span data-stu-id="9535d-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="9535d-146">Vous pouvez créer ces expériences avec [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="9535d-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="9535d-147">Ouvrir une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-147">Open a messaging extension</span></span>

<span data-ttu-id="9535d-148">La zone de rédaction et les messages ou publications sont les principaux contextes dans lesquels les utilisateurs utilisent des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9535d-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="9535d-149">À partir de la zone de rédaction</span><span class="sxs-lookup"><span data-stu-id="9535d-149">From the compose box</span></span>

<span data-ttu-id="9535d-150">Une fois ajoutée, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l'icône de votre application sous la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="9535d-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="9535d-151">Dans ces exemples, l’extension comporte des commandes de recherche et d’action.</span><span class="sxs-lookup"><span data-stu-id="9535d-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-152">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir de la zone de rédaction." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-154">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir de la zone de rédaction sur un appareil mobile." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="9535d-156">À partir d’un message de conversation ou d’un billet de canal</span><span class="sxs-lookup"><span data-stu-id="9535d-156">From a chat message or channel post</span></span>

Une fois ajoutés, les utilisateurs peuvent sélectionner l’icône **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: dans le message de conversation ou le billet de canal pour rechercher les commandes d’action de votre extension. <span data-ttu-id="9535d-158">Votre extension peut être répertoriée sous **Plus d’actions** en fonction de l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="9535d-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="9535d-159">La prise en charge d’autres actions à partir d’un message de conversation ou d’un billet de canal n’est pas disponible sur la plateforme mobile Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="9535d-160">Message de conversation</span><span class="sxs-lookup"><span data-stu-id="9535d-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-161">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir d’un message de conversation." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-163">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="Exemple montrant comment ouvrir une extension de messagerie à partir d’un billet de conversation sur un appareil mobile." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="9535d-165">Utiliser une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-165">Use a messaging extension</span></span>

<span data-ttu-id="9535d-166">Les scénarios suivants montrent les principales façons dont les utilisateurs utilisent les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9535d-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="9535d-167">Insérer du contenu dans un message</span><span class="sxs-lookup"><span data-stu-id="9535d-167">Insert content into a message</span></span>

<span data-ttu-id="9535d-168">**1. Sélectionner une extension de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="9535d-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="9535d-169">Les utilisateurs peuvent rechercher le contenu qu'ils veulent partager à partir de la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="9535d-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-170">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple montrant un utilisateur recherchant du contenu à insérer à partir de la zone de rédaction." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-172">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="Exemple montrant un utilisateur recherchant du contenu à insérer à partir de la zone de rédaction sur un appareil mobile." border="false":::

---

<span data-ttu-id="9535d-174">**2. Insérer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="9535d-174">**2. Insert content**.</span></span> <span data-ttu-id="9535d-175">Une fois publiés, d’autres utilisateurs peuvent répondre ou sélectionner le contenu pour afficher plus d’informations dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-176">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple montrant un utilisateur publiant du contenu dans une conversation de canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-178">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="Exemple montrant un utilisateur publiant du contenu dans une conversation de canal sur un appareil mobile." border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="9535d-180">Effectuez des actions sur un message</span><span class="sxs-lookup"><span data-stu-id="9535d-180">Take action on a message</span></span>

<span data-ttu-id="9535d-181">**1. Sélectionner une extension de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="9535d-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="9535d-182">Votre application peut inclure une ou plusieurs commandes d’action.</span><span class="sxs-lookup"><span data-stu-id="9535d-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-183">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple montrant un utilisateur sélectionnant une commande d’action d’extension de messagerie." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-185">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="Exemple montrant un utilisateur sélectionnant une commande d’action d’extension de messagerie sur un appareil mobile." border="false":::

---

<span data-ttu-id="9535d-187">**2. Terminer l'action**.</span><span class="sxs-lookup"><span data-stu-id="9535d-187">**2. Complete the action**.</span></span> <span data-ttu-id="9535d-188">Votre application peut recevoir et traiter le contenu ou les données envoyés par l’action de message.</span><span class="sxs-lookup"><span data-stu-id="9535d-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="9535d-189">Cela permet aux utilisateurs de rester dans leur conversation et, dans l’exemple suivant, de ne pas se soucier de la saisie d’informations directement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-190">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-192">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message sur un appareil mobile." border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="9535d-194">Liens d’aperçu</span><span class="sxs-lookup"><span data-stu-id="9535d-194">Preview links</span></span>

<span data-ttu-id="9535d-195">Les extensions de messagerie vous permettent également d’insérer des liens enrichis à partir d’une URL reconnue dans un message (cette fonctionnalité est appelée [lien en cours de déploiement](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="9535d-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="9535d-196">**1. Coller un lien reconnu** dans la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="9535d-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-197">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montrant un utilisateur collant un lien dans la zone de rédaction." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-199">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="Exemple montrant un utilisateur collant un lien dans la zone de rédaction sur un appareil mobile." border="false":::

---

<span data-ttu-id="9535d-201">**2. Insérer du contenu**.</span><span class="sxs-lookup"><span data-stu-id="9535d-201">**2. Insert content**.</span></span> <span data-ttu-id="9535d-202">Si votre application reconnaît l’URL dans la zone de rédaction, elle affiche le lien sous la forme d’une carte qui fournit un aperçu riche en contenu du contenu web.</span><span class="sxs-lookup"><span data-stu-id="9535d-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="9535d-203">(Pour plus d’informations, consultez les [Instructions de conception de Cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) .)</span><span class="sxs-lookup"><span data-stu-id="9535d-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-204">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Exemple montrant comment l'URL, étant donné qu'elle est reconnue par votre application, inclut un contenu enrichi dans la zone de rédaction." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="9535d-206">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="Exemple montrant comment l'URL, étant donné qu'elle est reconnue par votre application, inclut un contenu enrichi dans la zone de rédaction sur un appareil mobile." border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="9535d-208">Gérer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-208">Manage a messaging extension</span></span>

<span data-ttu-id="9535d-209">En cliquant avec le bouton droit sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9535d-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="9535d-210">Anatomie</span><span class="sxs-lookup"><span data-stu-id="9535d-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="9535d-211">Extension de messagerie dans la zone de rédaction</span><span class="sxs-lookup"><span data-stu-id="9535d-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="9535d-212">L’exemple suivant est une extension de messagerie ouverte à partir de la zone de rédaction.</span><span class="sxs-lookup"><span data-stu-id="9535d-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9535d-213">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="9535d-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'une extension de messagerie dans la zone de rédaction." border="false":::

|<span data-ttu-id="9535d-215">Compteur</span><span class="sxs-lookup"><span data-stu-id="9535d-215">Counter</span></span>|<span data-ttu-id="9535d-216">Description</span><span class="sxs-lookup"><span data-stu-id="9535d-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9535d-217">1</span><span class="sxs-lookup"><span data-stu-id="9535d-217">1</span></span>|<span data-ttu-id="9535d-218">**Logo de l’application** : icône couleur du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="9535d-219">2.</span><span class="sxs-lookup"><span data-stu-id="9535d-219">2</span></span>|<span data-ttu-id="9535d-220">**Nom de l’application** : nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="9535d-221">3</span><span class="sxs-lookup"><span data-stu-id="9535d-221">3</span></span>|<span data-ttu-id="9535d-222">**Icône de menu Commandes d’action (facultatif)** : ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="9535d-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="9535d-223">4</span><span class="sxs-lookup"><span data-stu-id="9535d-223">4</span></span>|<span data-ttu-id="9535d-224">**Zone de recherche** : permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="9535d-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="9535d-225">5</span><span class="sxs-lookup"><span data-stu-id="9535d-225">5</span></span>|<span data-ttu-id="9535d-226">**Menu onglet (facultatif)** : fournit plusieurs catégories de contenu.</span><span class="sxs-lookup"><span data-stu-id="9535d-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="9535d-227">6</span><span class="sxs-lookup"><span data-stu-id="9535d-227">6</span></span>|<span data-ttu-id="9535d-228">**Menu commandes d’action (facultatif)** : affiche la liste des commandes d’action (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="9535d-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="9535d-229">7</span><span class="sxs-lookup"><span data-stu-id="9535d-229">7</span></span>|<span data-ttu-id="9535d-230">**Contenu de l’application** : principalement pour afficher les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="9535d-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="9535d-231">L’exemple suivant utilise la disposition de liste (la disposition de la grille est une autre option).</span><span class="sxs-lookup"><span data-stu-id="9535d-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="9535d-232">8</span><span class="sxs-lookup"><span data-stu-id="9535d-232">8</span></span>|<span data-ttu-id="9535d-233">**Logo de l’application** : icône contour du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="9535d-234">Mobile</span><span class="sxs-lookup"><span data-stu-id="9535d-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'une extension de messagerie dans la zone de rédaction sur un appareil mobile." border="false":::

|<span data-ttu-id="9535d-236">Compteur</span><span class="sxs-lookup"><span data-stu-id="9535d-236">Counter</span></span>|<span data-ttu-id="9535d-237">Description</span><span class="sxs-lookup"><span data-stu-id="9535d-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9535d-238">1</span><span class="sxs-lookup"><span data-stu-id="9535d-238">1</span></span>|<span data-ttu-id="9535d-239">**Nom de l’application** : nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="9535d-240">2.</span><span class="sxs-lookup"><span data-stu-id="9535d-240">2</span></span>|<span data-ttu-id="9535d-241">**Icône de menu Commandes d’action (facultatif)** : ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="9535d-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="9535d-242">3</span><span class="sxs-lookup"><span data-stu-id="9535d-242">3</span></span>|<span data-ttu-id="9535d-243">**Zone de recherche** : permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="9535d-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="9535d-244">4</span><span class="sxs-lookup"><span data-stu-id="9535d-244">4</span></span>|<span data-ttu-id="9535d-245">**Menu onglet (facultatif)** : fournit plusieurs catégories de contenu.</span><span class="sxs-lookup"><span data-stu-id="9535d-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="9535d-246">5</span><span class="sxs-lookup"><span data-stu-id="9535d-246">5</span></span>|<span data-ttu-id="9535d-247">**Menu commandes d’action (facultatif)** : affiche la liste des commandes d’action (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="9535d-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="9535d-248">6</span><span class="sxs-lookup"><span data-stu-id="9535d-248">6</span></span>|<span data-ttu-id="9535d-249">**Contenu de l’application** : principalement pour afficher les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="9535d-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="9535d-250">Menu de gestion des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un menu de gestion des extensions de messagerie." border="false":::

|<span data-ttu-id="9535d-252">Compteur</span><span class="sxs-lookup"><span data-stu-id="9535d-252">Counter</span></span>|<span data-ttu-id="9535d-253">Description</span><span class="sxs-lookup"><span data-stu-id="9535d-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9535d-254">1</span><span class="sxs-lookup"><span data-stu-id="9535d-254">1</span></span>|<span data-ttu-id="9535d-255">**Désépingler** : disponible si l’utilisateur a épinglé votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="9535d-256">2.</span><span class="sxs-lookup"><span data-stu-id="9535d-256">2</span></span>|<span data-ttu-id="9535d-257">**Supprimer** : supprime l’extension de messagerie du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="9535d-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="9535d-258">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="9535d-258">Best practices</span></span>

<span data-ttu-id="9535d-259">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="9535d-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="9535d-260">Configuration et utilisation générale</span><span class="sxs-lookup"><span data-stu-id="9535d-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur l’installation et l’utilisation générale." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="9535d-262">À faire : intégrer avec l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9535d-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="9535d-263">L’authentification unique facilite, accélère et sécurise le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="9535d-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="9535d-264">En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a pas besoin de se reconnecter pour accéder à l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9535d-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple d’intégration avec l’authentification unique." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="9535d-266">À ne pas faire : retirer les utilisateurs de la conversation</span><span class="sxs-lookup"><span data-stu-id="9535d-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="9535d-267">Les extensions de messagerie sont des raccourcis censés réduire le changement de contexte.</span><span class="sxs-lookup"><span data-stu-id="9535d-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="9535d-268">Par exemple, votre extension ne doit pas diriger les utilisateurs vers une page web en dehors de Teams.</span><span class="sxs-lookup"><span data-stu-id="9535d-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="9535d-269">À faire : mettre en surbrillance votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="9535d-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="9535d-270">Les extensions de messagerie ne sont pas toujours faciles à trouver.</span><span class="sxs-lookup"><span data-stu-id="9535d-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="9535d-271">Incluez des captures d’écran de l’utilisation dans la page de détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="9535d-272">Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide de l’extension de messagerie dans une visite guidée de bienvenue du bot.</span><span class="sxs-lookup"><span data-stu-id="9535d-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="9535d-273">Création de modèles</span><span class="sxs-lookup"><span data-stu-id="9535d-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple sur la création de modèles." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="9535d-275">À faire : permettre à Teams de gérer une partie du travail de conception si possible</span><span class="sxs-lookup"><span data-stu-id="9535d-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="9535d-276">Si cela s'avère utile pour vos cas d'utilisation, envisagez de créer une extension de messagerie basée sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="9535d-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="9535d-277">Teams affiche ces types d’extensions avec un thème et une accessibilité intégrés.</span><span class="sxs-lookup"><span data-stu-id="9535d-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple de gestion du travail de conception." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="9535d-279">À ne pas faire : incorporer l’intégralité de votre application dans un module de tâche</span><span class="sxs-lookup"><span data-stu-id="9535d-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="9535d-280">Si votre extension de messagerie nécessite des commandes d’action, conservez le module de tâche simple et affichez uniquement les composants nécessaires à l’exécution de l’action.</span><span class="sxs-lookup"><span data-stu-id="9535d-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="9535d-281">Thèmes</span><span class="sxs-lookup"><span data-stu-id="9535d-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur les thèmes." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="9535d-283">À faire : tirer parti des jetons de couleur Teams</span><span class="sxs-lookup"><span data-stu-id="9535d-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="9535d-284">Chaque thème Teams a son propre modèle de couleurs.</span><span class="sxs-lookup"><span data-stu-id="9535d-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="9535d-285">Pour gérer automatiquement les modifications de thème, utilisez <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (Fluent UI)</a> dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="9535d-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="9535d-287">À ne pas faire : valeurs de couleur du code dur</span><span class="sxs-lookup"><span data-stu-id="9535d-287">Don't: Hard code color values</span></span>

<span data-ttu-id="9535d-288">Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendront plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="9535d-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="9535d-289">Actions</span><span class="sxs-lookup"><span data-stu-id="9535d-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="9535d-291">À faire : inclure des commandes d’action qui ont du sens dans le contexte</span><span class="sxs-lookup"><span data-stu-id="9535d-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="9535d-292">Les actions de message doivent être liées à ce qu’un utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="9535d-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="9535d-293">Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou une tâche en utilisant le texte d'une publication.</span><span class="sxs-lookup"><span data-stu-id="9535d-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d’action." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="9535d-295">À ne pas faire : inclure des commandes d’actions qui ne sont pas contextuelles</span><span class="sxs-lookup"><span data-stu-id="9535d-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="9535d-296">Une action de message pour **Afficher votre tableau de bord** semble probablement déconnectée de la plupart des conversations.</span><span class="sxs-lookup"><span data-stu-id="9535d-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="9535d-297">Recherches</span><span class="sxs-lookup"><span data-stu-id="9535d-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="9535d-298">À faire : afficher les résultats de la recherche lors de la saisie</span><span class="sxs-lookup"><span data-stu-id="9535d-298">Do: Show search results while typing</span></span>

<span data-ttu-id="9535d-299">Fournissez des résultats de recherche suggérés pendant que les utilisateurs tapent.</span><span class="sxs-lookup"><span data-stu-id="9535d-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="9535d-300">Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un minimum de caractères.</span><span class="sxs-lookup"><span data-stu-id="9535d-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="9535d-301">À ne pas faire : demander aux utilisateurs de soumettre une requête</span><span class="sxs-lookup"><span data-stu-id="9535d-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="9535d-302">Vous pouvez faire en sorte que les utilisateurs appuient sur une touche ou sélectionnent un bouton pour envoyer des requêtes à votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="9535d-303">Bien que cela puisse être plus facile pour votre service de services d'applications, les utilisateurs peuvent être déconcertés par le fait qu'ils ne voient pas les résultats de recherche en temps réel au fur et à mesure qu'ils tapent.</span><span class="sxs-lookup"><span data-stu-id="9535d-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="9535d-304">À faire : prendre en compte les requêtes sans terme</span><span class="sxs-lookup"><span data-stu-id="9535d-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="9535d-305">Par exemple, avant qu’un utilisateur n’écrive quoi que ce soit dans la zone de recherche, affichez ce qu’il a affiché pour la dernière fois sur votre application.</span><span class="sxs-lookup"><span data-stu-id="9535d-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="9535d-306">Il est possible qu'ils veuillent insérer ce contenu dans leur conversation.</span><span class="sxs-lookup"><span data-stu-id="9535d-306">It's possible that they want to insert that content into their conversation.</span></span>
