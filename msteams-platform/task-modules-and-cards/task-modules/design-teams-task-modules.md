---
title: Conception de modules de tâches
author: heath-hamilton
description: Découvrez comment concevoir des modules de tâche pour Teams applications et obtenir Microsoft Teams kit d'interface utilisateur.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101729"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="e4f61-103">Conception de modules de tâche pour votre application Microsoft Teams web</span><span class="sxs-lookup"><span data-stu-id="e4f61-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="e4f61-104">Vous pouvez créer des expériences popup modales dans votre application Teams avec des modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="e4f61-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="e4f61-105">Utilisez cette fonctionnalité pour afficher des informations et des médias enrichis ou effectuer une tâche complexe.</span><span class="sxs-lookup"><span data-stu-id="e4f61-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="L'exemple montre un module de tâche." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="e4f61-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e4f61-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="e4f61-108">Vous trouverez des instructions de conception de module de tâche plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface Microsoft Teams'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e4f61-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4f61-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="e4f61-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="e4f61-110">Ouvrir un module de tâche</span><span class="sxs-lookup"><span data-stu-id="e4f61-110">Open a task module</span></span>

<span data-ttu-id="e4f61-111">Les modules de tâche peuvent être lancés à partir de pratiquement n'importe où dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e4f61-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="e4f61-112">**Onglet**: un module de tâche peut être lancé à partir de n'importe quel lien d'un onglet. À utiliser dans les scénarios où vous souhaitez que l'utilisateur se concentre sur une interaction.</span><span class="sxs-lookup"><span data-stu-id="e4f61-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="e4f61-113">**Bot**: un module de tâche peut être lancé à partir d'un lien à l'intérieur d'un message de bot.</span><span class="sxs-lookup"><span data-stu-id="e4f61-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="e4f61-114">**Carte adaptative**: un module de tâche peut être lancé à partir d'une carte adaptative (envoyée avec une extension de messagerie ou par un bot) lorsqu'un utilisateur sélectionne un bouton.</span><span class="sxs-lookup"><span data-stu-id="e4f61-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="e4f61-115">**Extension de messagerie (commandes d'action)**: les extensions de messagerie vous permettent d'agir en particulier sur le contenu des messages.</span><span class="sxs-lookup"><span data-stu-id="e4f61-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="e4f61-116">La sélection d'une action ouvre un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="e4f61-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="e4f61-117">**Extension de messagerie (contexte de la** zone de composition) : dans la zone de composition, vous pouvez concevoir une extension de messagerie pour ouvrir un module de tâche au lieu du volant classique.</span><span class="sxs-lookup"><span data-stu-id="e4f61-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="e4f61-118">Réservez les modules de tâche pour les interactions complexes, telles que la réalisation d'un formulaire.</span><span class="sxs-lookup"><span data-stu-id="e4f61-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="e4f61-119">Anatomie</span><span class="sxs-lookup"><span data-stu-id="e4f61-119">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un module de tâche." border="false":::

<span data-ttu-id="e4f61-121">Les modules de tâche sont des surfaces très flexibles.</span><span class="sxs-lookup"><span data-stu-id="e4f61-121">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="e4f61-122">Ils peuvent être créés avec des iframes, en tirant dans d'autres modèles d'interface utilisateur, pour héberger des expériences conçues par des partenaires.</span><span class="sxs-lookup"><span data-stu-id="e4f61-122">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="e4f61-123">Il est préférable pour l'expérience la plus agréable.</span><span class="sxs-lookup"><span data-stu-id="e4f61-123">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="e4f61-124">Ils peuvent également être créés avec l'infrastructure [de](../../task-modules-and-cards/cards/design-effective-cards.md) carte adaptative, qui peut être un moyen plus simple et plus rapide d'exécuter des scénarios courants (tels que des formulaires).</span><span class="sxs-lookup"><span data-stu-id="e4f61-124">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="e4f61-125">Compteur</span><span class="sxs-lookup"><span data-stu-id="e4f61-125">Counter</span></span>|<span data-ttu-id="e4f61-126">Description</span><span class="sxs-lookup"><span data-stu-id="e4f61-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e4f61-127">1</span><span class="sxs-lookup"><span data-stu-id="e4f61-127">1</span></span>|<span data-ttu-id="e4f61-128">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="e4f61-128">**App icon**</span></span>|
|<span data-ttu-id="e4f61-129">2</span><span class="sxs-lookup"><span data-stu-id="e4f61-129">2</span></span>|<span data-ttu-id="e4f61-130">**Nom de l'application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="e4f61-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="e4f61-131">3</span><span class="sxs-lookup"><span data-stu-id="e4f61-131">3</span></span>|<span data-ttu-id="e4f61-132">**En-tête :** rendre les en-têtes clairs et concis.</span><span class="sxs-lookup"><span data-stu-id="e4f61-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="e4f61-133">Décrivez la tâche que vous souhaitez que les utilisateurs terminent.</span><span class="sxs-lookup"><span data-stu-id="e4f61-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="e4f61-134">4 </span><span class="sxs-lookup"><span data-stu-id="e4f61-134">4</span></span>|<span data-ttu-id="e4f61-135">**Bouton Fermer :** permet aux utilisateurs de trouver le contenu d'application qu'ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="e4f61-135">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="e4f61-136">5 </span><span class="sxs-lookup"><span data-stu-id="e4f61-136">5</span></span>|<span data-ttu-id="e4f61-137">**iframe**: espace réactif qui héberge le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="e4f61-137">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="e4f61-138">6 </span><span class="sxs-lookup"><span data-stu-id="e4f61-138">6</span></span>|<span data-ttu-id="e4f61-139">**Actions (facultatives)**: boutons liés au contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="e4f61-139">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="e4f61-140">Conception avec des modèles d'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="e4f61-140">Designing with UI templates</span></span>

<span data-ttu-id="e4f61-141">Envisagez d'utiliser des modèles pour les dispositions courantes à l'intérieur de vos modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="e4f61-141">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="e4f61-142">Chacun d'eux est composé de composants plus petits pour créer une conception réactive et élégante qui peut être utilisée de manière personnalisée ou adaptée à votre scénario ou à votre apparence de marque.</span><span class="sxs-lookup"><span data-stu-id="e4f61-142">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="e4f61-143">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="e4f61-143">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="e4f61-144">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="e4f61-144">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="e4f61-145">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="e4f61-145">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="e4f61-146">Exemples</span><span class="sxs-lookup"><span data-stu-id="e4f61-146">Examples</span></span>

### <a name="list"></a><span data-ttu-id="e4f61-147">Répertorier</span><span class="sxs-lookup"><span data-stu-id="e4f61-147">List</span></span>

<span data-ttu-id="e4f61-148">Les listes fonctionnent parfaitement dans un module de tâche, car elles sont faciles à analyser.</span><span class="sxs-lookup"><span data-stu-id="e4f61-148">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Exemple de liste dans un module de tâche." border="false":::

### <a name="form"></a><span data-ttu-id="e4f61-150">Formulaire</span><span class="sxs-lookup"><span data-stu-id="e4f61-150">Form</span></span>

<span data-ttu-id="e4f61-151">Les modules de tâche sont un excellent endroit pour faire surface à des formulaires avec des entrées utilisateur séquentielles et une validation en ligne.</span><span class="sxs-lookup"><span data-stu-id="e4f61-151">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="e4f61-152">Vous pouvez utiliser des cartes adaptatives pour incorporer des éléments de formulaire.</span><span class="sxs-lookup"><span data-stu-id="e4f61-152">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Exemple de formulaire dans un module de tâche." border="false":::

### <a name="sign-in"></a><span data-ttu-id="e4f61-154">Se connecter</span><span class="sxs-lookup"><span data-stu-id="e4f61-154">Sign in</span></span>

<span data-ttu-id="e4f61-155">Créez un flux de signature ou d'inscription centré avec une série de modules de tâche, ce qui permet aux utilisateurs de se déplacer facilement à travers les étapes séquentielles.</span><span class="sxs-lookup"><span data-stu-id="e4f61-155">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Exemple d'expérience de signature dans un module de tâche." border="false":::

### <a name="media"></a><span data-ttu-id="e4f61-157">Support</span><span class="sxs-lookup"><span data-stu-id="e4f61-157">Media</span></span>

<span data-ttu-id="e4f61-158">Incorporer du contenu multimédia dans un module de tâche pour une expérience d'affichage axée sur l'affichage.</span><span class="sxs-lookup"><span data-stu-id="e4f61-158">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Exemple de contenu multimédia dans un module de tâche." border="false":::

### <a name="empty-state"></a><span data-ttu-id="e4f61-160">État vide</span><span class="sxs-lookup"><span data-stu-id="e4f61-160">Empty state</span></span>

<span data-ttu-id="e4f61-161">À utiliser pour les messages d'accueil, d'erreur et de réussite.</span><span class="sxs-lookup"><span data-stu-id="e4f61-161">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Exemple d'état vide dans un module de tâche." border="false":::

### <a name="image-gallery"></a><span data-ttu-id="e4f61-163">Galerie d’images</span><span class="sxs-lookup"><span data-stu-id="e4f61-163">Image gallery</span></span>

<span data-ttu-id="e4f61-164">Incorporer un carrousel de galerie dans un iFrame.</span><span class="sxs-lookup"><span data-stu-id="e4f61-164">Embed a gallery carousel in an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Exemple de galerie d'images dans un module de tâche." border="false":::

### <a name="poll"></a><span data-ttu-id="e4f61-166">Sondage</span><span class="sxs-lookup"><span data-stu-id="e4f61-166">Poll</span></span>

<span data-ttu-id="e4f61-167">Cet exemple montre les résultats des sondages lancés à partir d'une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="e4f61-167">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="e4f61-168">Le sondage peut également être placé à l'intérieur d'un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="e4f61-168">The poll can be placed inside a task module, too.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Exemple d'enquête dans un module de tâche." border="false":::

## <a name="best-practices"></a><span data-ttu-id="e4f61-170">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="e4f61-170">Best practices</span></span>

<span data-ttu-id="e4f61-171">Utilisez ces recommandations pour créer une expérience d'application de qualité.</span><span class="sxs-lookup"><span data-stu-id="e4f61-171">Use these recommendations to create a quality app experience.</span></span>

### <a name="usability"></a><span data-ttu-id="e4f61-172">Convivialité</span><span class="sxs-lookup"><span data-stu-id="e4f61-172">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (un module de tâche à la fois)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="e4f61-174">À faire : utiliser un module de tâche à la fois</span><span class="sxs-lookup"><span data-stu-id="e4f61-174">Do: Use one task module at a time</span></span>

<span data-ttu-id="e4f61-175">L'objectif est de concentrer l'utilisateur sur l'exécution d'une tâche après tout !</span><span class="sxs-lookup"><span data-stu-id="e4f61-175">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (afficher une boîte de dialogue au-dessus d'un module de tâche)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="e4f61-177">À ne pas faire : faire apparaître une boîte de dialogue au-dessus d'un module de tâche</span><span class="sxs-lookup"><span data-stu-id="e4f61-177">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="e4f61-178">Cela crée une expérience utilisateur non recentrée et confuse.</span><span class="sxs-lookup"><span data-stu-id="e4f61-178">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="e4f61-179">Réactive</span><span class="sxs-lookup"><span data-stu-id="e4f61-179">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (assurez-vous que le contenu est réactif)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="e4f61-181">À faire : assurez-vous que le contenu est réactif</span><span class="sxs-lookup"><span data-stu-id="e4f61-181">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="e4f61-182">Bien que les cartes adaptatives hébergées dans un module de tâche s'restituent bien sur les appareils mobiles, si vous choisissez d'utiliser un iframe pour héberger du contenu d'application, assurez-vous que l'interface utilisateur est réactive et fonctionne bien sur tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="e4f61-182">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (n'utilisez pas de barres de défilement horizontales)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="e4f61-184">À ne pas faire : utiliser des barres de défilement horizontales</span><span class="sxs-lookup"><span data-stu-id="e4f61-184">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="e4f61-185">Il est préférable de garder le contenu concentré et pas trop long.</span><span class="sxs-lookup"><span data-stu-id="e4f61-185">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="e4f61-186">Si un défilement est nécessaire, faites défiler verticalement et non horizontalement.</span><span class="sxs-lookup"><span data-stu-id="e4f61-186">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="e4f61-187">Simplicité</span><span class="sxs-lookup"><span data-stu-id="e4f61-187">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (restez bref)." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="e4f61-189">Do: Keep it short</span><span class="sxs-lookup"><span data-stu-id="e4f61-189">Do: Keep it short</span></span>

<span data-ttu-id="e4f61-190">Vous pouvez facilement créer un Assistant en plusieurs étapes, mais cela ne signifie pas nécessairement que vous le devriez !</span><span class="sxs-lookup"><span data-stu-id="e4f61-190">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="e4f61-191">Un module de tâche multi-écran peut être problématique, car les messages entrants sont distrayants et tentant les utilisateurs de quitter.</span><span class="sxs-lookup"><span data-stu-id="e4f61-191">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="e4f61-192">Si votre tâche est vraiment impliquée, pop out vers une page web complète au lieu d'un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="e4f61-192">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (sans interactions longues)." border="false":::

#### <a name="dont-have-long-interactions"></a><span data-ttu-id="e4f61-194">À ne pas faire : avoir de longues interactions</span><span class="sxs-lookup"><span data-stu-id="e4f61-194">Don't: Have long interactions</span></span>

<span data-ttu-id="e4f61-195">Essayez de maintenir vos interactions courtes et au point.</span><span class="sxs-lookup"><span data-stu-id="e4f61-195">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="e4f61-196">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="e4f61-196">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (utiliser des messages d'erreur inline)." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="e4f61-198">À faire : utiliser les messages d'erreur inline</span><span class="sxs-lookup"><span data-stu-id="e4f61-198">Do: Use inline error messages</span></span>

<span data-ttu-id="e4f61-199">Consultez le modèle d'interface utilisateur de formulaires pour obtenir des instructions sur la gestion des erreurs en ligne.</span><span class="sxs-lookup"><span data-stu-id="e4f61-199">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Exemple montrant la meilleure pratique d'un module de tâche (placer des messages d'erreur dans des boîtes de dialogue)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="e4f61-201">À ne pas faire : placer des messages d’erreur dans des boîtes de dialogue</span><span class="sxs-lookup"><span data-stu-id="e4f61-201">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="e4f61-202">Ne pas faire apparaître de message d’erreur dans une boîte de dialogue au-dessus d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="e4f61-202">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="e4f61-203">Cela crée une expérience utilisateur confuse.</span><span class="sxs-lookup"><span data-stu-id="e4f61-203">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
