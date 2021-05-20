---
title: Conception de votre extension de messagerie
description: Découvrez comment concevoir une extension de messagerie Teams et obtenir le kit d’interface Microsoft Teams’interface utilisateur.
keywords: les équipes conçoivent des lignes directrices sur les extensions de messagerie de référence conseils pratiques
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566214"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="728bf-104">Conception de votre extension Microsoft Teams messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="728bf-105">Les extensions de messagerie sont des raccourcis pour insérer du contenu d’application ou agir sur un message sans naviguer loin de la conversation.</span><span class="sxs-lookup"><span data-stu-id="728bf-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="728bf-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les gens peuvent ajouter, utiliser et gérer les extensions de messagerie dans Teams.</span><span class="sxs-lookup"><span data-stu-id="728bf-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="728bf-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="728bf-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="728bf-108">Vous pouvez trouver des lignes directrices complètes de conception d’extension de messagerie, y compris des éléments que vous pouvez saisir et modifier au besoin, dans le kit d Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="728bf-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="728bf-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="728bf-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="728bf-110">Ajouter une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-110">Add a messaging extension</span></span>

<span data-ttu-id="728bf-111">Vous pouvez ajouter une extension de messagerie dans les Teams suivants :</span><span class="sxs-lookup"><span data-stu-id="728bf-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="728bf-112">À partir de Teams Store (AppSource).</span><span class="sxs-lookup"><span data-stu-id="728bf-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="728bf-113">Dans un canal, chat ou réunion (avant, pendant et après) près de la boîte de composition.</span><span class="sxs-lookup"><span data-stu-id="728bf-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="728bf-114">Il est intéressant de noter que si vous ajoutez une extension de messagerie dans l’un de ces endroits, vous seul pouvez l’utiliser dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="728bf-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="728bf-115">L’exemple suivant montre comment vous ajoutez une extension de messagerie dans un canal :</span><span class="sxs-lookup"><span data-stu-id="728bf-115">The following example shows how you add a messaging extension in a channel:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="Exemple montre comment ajouter une extension de messagerie près de la boîte de composition dans un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="728bf-117">Configurer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-117">Set up a messaging extension</span></span>

<span data-ttu-id="728bf-118">L’authentification n’est pas obligatoire, mais si votre application ressemble à un outil de suivi des billets, vous devrez peut-être que les gens se connectent pour utiliser l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="728bf-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="728bf-119">Pour plus de cohérence Teams les applications, vous ne pouvez pas personnaliser l’écran de dédisation.</span><span class="sxs-lookup"><span data-stu-id="728bf-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="728bf-120">Si vous utilisez l’authentification unique de connect-on (SSO), les utilisateurs sont automatiquement connectés.</span><span class="sxs-lookup"><span data-stu-id="728bf-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="Exemple montre l’écran d’installation d’extension de messagerie avec un bouton de dédation." border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="728bf-122">Types d’extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-122">Types of messaging extensions</span></span>

<span data-ttu-id="728bf-123">Les extensions de messagerie peuvent avoir des commandes de recherche, des commandes d’action ou les deux.</span><span class="sxs-lookup"><span data-stu-id="728bf-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="728bf-124">Vos commandes dépendent des fonctionnalités de votre application et de la façon dont celles-ci s’Teams les cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="728bf-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="728bf-125">Commandes de recherche</span><span class="sxs-lookup"><span data-stu-id="728bf-125">Search commands</span></span>

<span data-ttu-id="728bf-126">Avec les commandes de recherche, les gens peuvent utiliser votre extension de messagerie pour trouver rapidement du contenu externe et insérer dans un message.</span><span class="sxs-lookup"><span data-stu-id="728bf-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="728bf-127">Les commandes de recherche sont généralement disponibles dans la boîte de composition.</span><span class="sxs-lookup"><span data-stu-id="728bf-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="728bf-128">Par exemple, vous pouvez démarrer ou ajouter à une discussion en partageant un élément de contenu, sans jamais laisser Teams.</span><span class="sxs-lookup"><span data-stu-id="728bf-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="Exemple montre une extension de messagerie basée sur la recherche lancée à partir de la boîte de composition." border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="728bf-130">Composer des options de mise en page de boîte</span><span class="sxs-lookup"><span data-stu-id="728bf-130">Compose box layout options</span></span>

<span data-ttu-id="728bf-131">Vous avez quelques options pour afficher les résultats de recherche d’extension de messagerie, y compris les vues [de liste et de grille.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)</span><span class="sxs-lookup"><span data-stu-id="728bf-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Illustrations montrant les options de mise en page pour les résultats de recherche d’extension de messagerie." border="false":::

### <a name="action-commands"></a><span data-ttu-id="728bf-133">Commandes d'action</span><span class="sxs-lookup"><span data-stu-id="728bf-133">Action commands</span></span>

<span data-ttu-id="728bf-134">Les commandes d’action permettent aux gens de déclencher des actions et de traiter les demandes dans les services externes Teams.</span><span class="sxs-lookup"><span data-stu-id="728bf-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="728bf-135">Par exemple, si votre application suit les commandes, un utilisateur peut créer une nouvelle commande en utilisant le contenu du message d’un collègue à partir de l’intérieur de son chat.</span><span class="sxs-lookup"><span data-stu-id="728bf-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="728bf-136">Les extensions de messagerie basées sur l’action exigent fréquemment que les utilisateurs remplissent un formulaire ou un autre type de configuration dans un module.</span><span class="sxs-lookup"><span data-stu-id="728bf-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="728bf-137">Vous pouvez créer ces expériences avec des [modules de tâches](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="728bf-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="728bf-138">Ouvrez une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-138">Open a messaging extension</span></span>

<span data-ttu-id="728bf-139">La boîte de composition et les messages ou messages sont les principaux contextes où les gens utilisent des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="728bf-139">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="728bf-140">De la boîte à composer</span><span class="sxs-lookup"><span data-stu-id="728bf-140">From the compose box</span></span>

<span data-ttu-id="728bf-141">Une fois ajouté, les utilisateurs peuvent ouvrir votre extension de messagerie en sélectionnant l’icône de votre application sous la boîte de composition.</span><span class="sxs-lookup"><span data-stu-id="728bf-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="728bf-142">Dans cet exemple, l’extension a des commandes de recherche et d’action :</span><span class="sxs-lookup"><span data-stu-id="728bf-142">In this example, the extension has search and action commands:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir de la boîte de composition." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="728bf-144">À partir d’un message de chat ou d’un message de canal</span><span class="sxs-lookup"><span data-stu-id="728bf-144">From a chat message or channel post</span></span>

Une fois ajouté,  les utilisateurs peuvent sélectionner :::image type="icon" source="../../assets/icons/teams-client-more.png"::: l’icône Plus sur le message de chat ou le message de canal pour trouver les commandes d’action de votre extension. <span data-ttu-id="728bf-146">Votre extension peut être répertoriée sous Plus **d’actions basées** sur l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="728bf-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="728bf-147">La prise en charge d’un plus grand nombre d’actions à partir d’un message de chat ou d’une publication de canal n’est pas disponible Microsoft Teams la plate-forme mobile.</span><span class="sxs-lookup"><span data-stu-id="728bf-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="728bf-148">Message de conversation</span><span class="sxs-lookup"><span data-stu-id="728bf-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un message de chat." border="false":::

#### <a name="channel-post"></a><span data-ttu-id="728bf-150">Poste de canal</span><span class="sxs-lookup"><span data-stu-id="728bf-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Exemple montre comment ouvrir une extension de messagerie à partir d’un poste de canal." border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="728bf-152">Utiliser une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-152">Use a messaging extension</span></span>

<span data-ttu-id="728bf-153">Les scénarios suivants montrent les principales façons dont les gens utilisent les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="728bf-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="728bf-154">Insérer du contenu dans un message</span><span class="sxs-lookup"><span data-stu-id="728bf-154">Insert content into a message</span></span>

<span data-ttu-id="728bf-155">**1. Sélectionnez une extension de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="728bf-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="728bf-156">Les utilisateurs peuvent rechercher le contenu qu’ils souhaitent partager à partir de la boîte de composition.</span><span class="sxs-lookup"><span data-stu-id="728bf-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="Exemple montre un utilisateur à la recherche de contenu à insérer à partir de la boîte de composition." border="false":::

<span data-ttu-id="728bf-158">**2. Insérer le contenu**.</span><span class="sxs-lookup"><span data-stu-id="728bf-158">**2. Insert content**.</span></span> <span data-ttu-id="728bf-159">Une fois affiché, d’autres peuvent répondre ou sélectionner le contenu pour voir plus d’informations dans votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="Exemple montre un utilisateur affichant du contenu dans une conversation de canal." border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="728bf-161">Agir sur un message</span><span class="sxs-lookup"><span data-stu-id="728bf-161">Take action on a message</span></span>

<span data-ttu-id="728bf-162">**1. Sélectionnez une extension de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="728bf-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="728bf-163">Votre application peut inclure une ou plusieurs commandes d’action.</span><span class="sxs-lookup"><span data-stu-id="728bf-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="Exemple montre un utilisateur sélectionnant une commande d’action d’extension de messagerie." border="false":::

<span data-ttu-id="728bf-165">**2. Terminer l’action**.</span><span class="sxs-lookup"><span data-stu-id="728bf-165">**2. Complete the action**.</span></span> <span data-ttu-id="728bf-166">Votre application peut recevoir et traiter tout contenu ou données envoyés par l’action de message.</span><span class="sxs-lookup"><span data-stu-id="728bf-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="728bf-167">Cela permet aux utilisateurs de rester dans leur conversation et, l’exemple suivant, de ne pas s’inquiéter d’entrer des informations directement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Exemple sur la façon d’agir sur un message." border="false":::

### <a name="preview-links"></a><span data-ttu-id="728bf-169">Liens d’aperçu</span><span class="sxs-lookup"><span data-stu-id="728bf-169">Preview links</span></span>

<span data-ttu-id="728bf-170">Les extensions de messagerie vous permettent également d’insérer des liens riches à partir d’une URL reconnue dans un message (cette fonctionnalité [est appelée lien de déploiement](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="728bf-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="728bf-171">**1. Coller un lien reconnu dans** la boîte de composition.</span><span class="sxs-lookup"><span data-stu-id="728bf-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="Exemple montre un utilisateur qui a passé un lien dans la boîte de compost." border="false":::

<span data-ttu-id="728bf-173">**2. Insérer le contenu**.</span><span class="sxs-lookup"><span data-stu-id="728bf-173">**2. Insert content**.</span></span> <span data-ttu-id="728bf-174">Si votre application reconnaît l’URL dans la boîte de composition, elle rend le lien comme une carte qui fournit un aperçu riche en contenu du contenu Web.</span><span class="sxs-lookup"><span data-stu-id="728bf-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="728bf-175">(Voir les lignes [directrices de conception des cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md) pour plus d’informations.)</span><span class="sxs-lookup"><span data-stu-id="728bf-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="Exemple montre comment l’URL, puisqu’elle est reconnue par votre application, inclut un contenu riche dans la boîte de composition." border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="728bf-177">Gérer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-177">Manage a messaging extension</span></span>

<span data-ttu-id="728bf-178">En cliquant à droite sur votre icône, les utilisateurs peuvent épingler, supprimer ou configurer votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="728bf-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="728bf-179">Anatomie</span><span class="sxs-lookup"><span data-stu-id="728bf-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="728bf-180">Extension de messagerie dans la boîte de composition</span><span class="sxs-lookup"><span data-stu-id="728bf-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="728bf-181">L’exemple suivant est une extension de messagerie ouverte à partir de la boîte de composition.</span><span class="sxs-lookup"><span data-stu-id="728bf-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Illustration montrant l’anatomie d’interface utilisateur d’une extension de messagerie dans la boîte de composition." border="false":::

|<span data-ttu-id="728bf-183">Compteur</span><span class="sxs-lookup"><span data-stu-id="728bf-183">Counter</span></span>|<span data-ttu-id="728bf-184">Description</span><span class="sxs-lookup"><span data-stu-id="728bf-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="728bf-185">1</span><span class="sxs-lookup"><span data-stu-id="728bf-185">1</span></span>|<span data-ttu-id="728bf-186">**Logo de l’application**: Icône couleur du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="728bf-187">2</span><span class="sxs-lookup"><span data-stu-id="728bf-187">2</span></span>|<span data-ttu-id="728bf-188">**Nom de l’application**: Nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="728bf-189">3</span><span class="sxs-lookup"><span data-stu-id="728bf-189">3</span></span>|<span data-ttu-id="728bf-190">**Icône de menu commandes d’action (facultatif)**: Ouvre une liste de commandes d’action pour votre extension de messagerie (si vous en spécifiez une).</span><span class="sxs-lookup"><span data-stu-id="728bf-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="728bf-191">4 </span><span class="sxs-lookup"><span data-stu-id="728bf-191">4</span></span>|<span data-ttu-id="728bf-192">**Boîte de recherche**: Permet aux utilisateurs de trouver le contenu de l’application qu’ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="728bf-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="728bf-193">5 </span><span class="sxs-lookup"><span data-stu-id="728bf-193">5</span></span>|<span data-ttu-id="728bf-194">**Menu onglet (facultatif)**: Fournit plusieurs catégories de contenu.</span><span class="sxs-lookup"><span data-stu-id="728bf-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="728bf-195">6 </span><span class="sxs-lookup"><span data-stu-id="728bf-195">6</span></span>|<span data-ttu-id="728bf-196">**Menu commandes d’action (facultatif)**: Affiche la liste des commandes d’action (si vous en spécifiez).</span><span class="sxs-lookup"><span data-stu-id="728bf-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="728bf-197">7 </span><span class="sxs-lookup"><span data-stu-id="728bf-197">7</span></span>|<span data-ttu-id="728bf-198">**Contenu de l’application**: Principalement pour afficher les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="728bf-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="728bf-199">L’exemple ici est l’utilisation de la mise en page de liste (mise en page de grille est une autre option).</span><span class="sxs-lookup"><span data-stu-id="728bf-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="728bf-200">8 </span><span class="sxs-lookup"><span data-stu-id="728bf-200">8</span></span>|<span data-ttu-id="728bf-201">**Logo de l’application**: Icône de contour du logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="728bf-202">Menu de gestion d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un menu de gestion d’extension de messagerie." border="false":::

|<span data-ttu-id="728bf-204">Compteur</span><span class="sxs-lookup"><span data-stu-id="728bf-204">Counter</span></span>|<span data-ttu-id="728bf-205">Description</span><span class="sxs-lookup"><span data-stu-id="728bf-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="728bf-206">1</span><span class="sxs-lookup"><span data-stu-id="728bf-206">1</span></span>|<span data-ttu-id="728bf-207">**Unpin**: Disponible si l’utilisateur a épinglé votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="728bf-208">2</span><span class="sxs-lookup"><span data-stu-id="728bf-208">2</span></span>|<span data-ttu-id="728bf-209">**Supprimer**: Supprime l’extension de messagerie du canal, du chat ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="728bf-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="728bf-210">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="728bf-210">Best practices</span></span>

<span data-ttu-id="728bf-211">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="728bf-211">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="728bf-212">Configuration et utilisation générale</span><span class="sxs-lookup"><span data-stu-id="728bf-212">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Exemple sur la configuration et l’utilisation générale." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="728bf-214">Faire: Intégrer avec un seul signe sur</span><span class="sxs-lookup"><span data-stu-id="728bf-214">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="728bf-215">SSO facilite, accélère et sécurise le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="728bf-215">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="728bf-216">En outre, si un utilisateur s’est déjà connecté à votre application personnelle, il n’a pas à se connecter à nouveau pour accéder à l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="728bf-216">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Exemple sur l’intégration avec un seul signe." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="728bf-218">Ne pas : Éloignez les utilisateurs de la conversation</span><span class="sxs-lookup"><span data-stu-id="728bf-218">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="728bf-219">Les extensions de messagerie sont des raccourcis qui sont censés réduire la commutation de contexte.</span><span class="sxs-lookup"><span data-stu-id="728bf-219">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="728bf-220">Votre extension ne doit pas, par exemple, diriger les utilisateurs vers une page Web en dehors de Teams.</span><span class="sxs-lookup"><span data-stu-id="728bf-220">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="728bf-221">Faire: Mettre en surbrillance votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="728bf-221">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="728bf-222">Les extensions de messagerie ne sont pas toujours faciles à trouver.</span><span class="sxs-lookup"><span data-stu-id="728bf-222">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="728bf-223">Incluez des captures d’écran de la façon de l’utiliser dans votre page de détails d’application.</span><span class="sxs-lookup"><span data-stu-id="728bf-223">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="728bf-224">Si votre application inclut également un bot, vous pouvez inclure la documentation d’aide d’extension de messagerie dans une visite de bienvenue de bot.</span><span class="sxs-lookup"><span data-stu-id="728bf-224">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="728bf-225">Templating (templating)</span><span class="sxs-lookup"><span data-stu-id="728bf-225">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Exemple sur templating." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="728bf-227">Faire: Laissez-Teams gérer une partie du travail de conception si possible</span><span class="sxs-lookup"><span data-stu-id="728bf-227">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="728bf-228">Si cela est logique pour vos cas d’utilisation, envisagez de créer une extension de messagerie basée sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="728bf-228">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="728bf-229">Teams rend ces types d’extensions avec le sur lent et l’accessibilité intégrés.</span><span class="sxs-lookup"><span data-stu-id="728bf-229">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Exemple sur le travail de conception de manipulation." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="728bf-231">Ne pas : Intégrer toute votre application dans un module de tâches</span><span class="sxs-lookup"><span data-stu-id="728bf-231">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="728bf-232">Si votre extension de messagerie nécessite des commandes d’action, gardez le module de tâches simple et affichez uniquement les composants nécessaires pour compléter l’action.</span><span class="sxs-lookup"><span data-stu-id="728bf-232">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="728bf-233">Thèmes</span><span class="sxs-lookup"><span data-stu-id="728bf-233">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Exemple sur le sujet." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="728bf-235">Faire: Profitez de Teams de couleur</span><span class="sxs-lookup"><span data-stu-id="728bf-235">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="728bf-236">Chaque Teams a son propre schéma de couleurs.</span><span class="sxs-lookup"><span data-stu-id="728bf-236">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="728bf-237">Pour gérer automatiquement les modifications de thème, <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">utilisez des jetons de couleur (interface utilisateur fluide)</a> dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="728bf-237">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Exemple sur les jetons de couleur." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="728bf-239">Ne pas : Valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="728bf-239">Don't: Hard code color values</span></span>

<span data-ttu-id="728bf-240">Si vous n’utilisez pas Teams jetons de couleur, vos créations seront moins évolutives et prennent plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="728bf-240">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="728bf-241">Actions</span><span class="sxs-lookup"><span data-stu-id="728bf-241">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Exemple sur les actions." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="728bf-243">Faire : Inclure des commandes d’action qui ont du sens dans leur contexte</span><span class="sxs-lookup"><span data-stu-id="728bf-243">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="728bf-244">Les actions de message doivent se rapporter à ce qu’un utilisateur regarde.</span><span class="sxs-lookup"><span data-stu-id="728bf-244">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="728bf-245">Par exemple, fournissez aux utilisateurs un raccourci pour créer un problème ou un élément de travail en utilisant le texte dans la publication de quelqu’un.</span><span class="sxs-lookup"><span data-stu-id="728bf-245">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Exemple sur les commandes d’action." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="728bf-247">Ne pas : Inclure des commandes d’actions qui ne sont pas contextuelles</span><span class="sxs-lookup"><span data-stu-id="728bf-247">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="728bf-248">Une action de message pour **afficher votre tableau de** bord semble probablement déconnectée de la plupart des conversations.</span><span class="sxs-lookup"><span data-stu-id="728bf-248">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="728bf-249">Recherches</span><span class="sxs-lookup"><span data-stu-id="728bf-249">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="728bf-250">Faire: Afficher les résultats de recherche tout en tapant</span><span class="sxs-lookup"><span data-stu-id="728bf-250">Do: Show search results while typing</span></span>

<span data-ttu-id="728bf-251">Fournissez les résultats de recherche suggérés pendant que les utilisateurs tapent.</span><span class="sxs-lookup"><span data-stu-id="728bf-251">Provide suggested search results while users type.</span></span> <span data-ttu-id="728bf-252">Ils peuvent trouver le contenu dont ils ont besoin plus rapidement avec un minimum de caractères.</span><span class="sxs-lookup"><span data-stu-id="728bf-252">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="728bf-253">Ne pas : Exiger des utilisateurs qu’ils soumettent une requête</span><span class="sxs-lookup"><span data-stu-id="728bf-253">Don't: Require users to submit a query</span></span>

<span data-ttu-id="728bf-254">Vous pouvez faire appuyer sur une clé par les utilisateurs ou sélectionner un bouton pour envoyer des requêtes à votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-254">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="728bf-255">Bien que cela puisse être plus facile sur votre service de services d’application, les gens peuvent être confus qu’ils ne voient pas les résultats de recherche en temps réel comme ils tapent.</span><span class="sxs-lookup"><span data-stu-id="728bf-255">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="728bf-256">Faire : Considérez les requêtes à durée zéro</span><span class="sxs-lookup"><span data-stu-id="728bf-256">Do: Consider zero-term queries</span></span>

<span data-ttu-id="728bf-257">Par exemple, avant qu’un utilisateur n’écrive quoi que ce soit dans la boîte de recherche, affichez ce qu’il a vu pour la dernière fois sur votre application.</span><span class="sxs-lookup"><span data-stu-id="728bf-257">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="728bf-258">Il est possible qu’ils veuillent insérer ce contenu dans leur conversation.</span><span class="sxs-lookup"><span data-stu-id="728bf-258">It's possible that they want to insert that content into their conversation.</span></span>
