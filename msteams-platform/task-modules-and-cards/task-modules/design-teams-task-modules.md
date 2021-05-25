---
title: Conception de modules de tâches
author: heath-hamilton
description: Découvrez comment concevoir des modules de tâche pour Teams applications et obtenir le kit Microsoft Teams’interface utilisateur.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 48e47a6c0bde0f0a3fefb8fcbfb362687ce58947
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629906"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="ff0a9-103">Conception de modules de tâche pour votre Microsoft Teams application</span><span class="sxs-lookup"><span data-stu-id="ff0a9-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="ff0a9-104">Vous pouvez créer des expériences popup modales dans votre application Teams avec des modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="ff0a9-105">Utilisez cette fonctionnalité pour afficher des informations et des médias enrichis ou effectuer une tâche complexe.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="L’exemple montre un module de tâche." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ff0a9-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ff0a9-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ff0a9-108">Vous trouverez des instructions de conception de module de tâche plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d’interface Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff0a9-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="ff0a9-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="ff0a9-110">Ouvrir un module de tâche</span><span class="sxs-lookup"><span data-stu-id="ff0a9-110">Open a task module</span></span>

<span data-ttu-id="ff0a9-111">Les modules de tâche peuvent être lancés à partir de pratiquement n’importe où dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="ff0a9-112">**Onglet**: un module de tâche peut être lancé à partir de n’importe quel lien d’un onglet. À utiliser dans les scénarios où vous souhaitez que l’utilisateur se concentre sur une interaction.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="ff0a9-113">**Bot**: un module de tâche peut être lancé à partir d’un lien à l’intérieur d’un message de bot.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="ff0a9-114">**Carte adaptative**: un module de tâche peut être lancé à partir d’une carte adaptative (envoyée avec une extension de messagerie ou par un bot) lorsqu’un utilisateur sélectionne un bouton.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="ff0a9-115">**Extension de messagerie (commandes d’action)**: les extensions de messagerie vous permettent d’agir en particulier sur le contenu des messages.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="ff0a9-116">La sélection d’une action ouvre un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="ff0a9-117">**Extension de messagerie (contexte de la** zone de composition) : dans la zone de composition, vous pouvez concevoir une extension de messagerie pour ouvrir un module de tâche au lieu du volant classique.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="ff0a9-118">Réservez les modules de tâche pour les interactions complexes, telles que la réalisation d’un formulaire.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="ff0a9-119">Anatomie</span><span class="sxs-lookup"><span data-stu-id="ff0a9-119">Anatomy</span></span>

<span data-ttu-id="ff0a9-120">Les modules de tâche offrent une surface flexible pour les expériences d’application hébergées.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-120">Task modules provide a flexible surface for hosted app experiences.</span></span> <span data-ttu-id="ff0a9-121">Ils sont créés à l’aide d’un iframe (bureau) ou d’une vue web (mobile), afin que vous pouvez concevoir des modules de tâche avec nos modèles d’interface utilisateur (recommandés) ou à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-121">They're built using an iframe (desktop) or webview (mobile), so you can design task modules with our UI templates (recommended) or from scratch.</span></span>

<span data-ttu-id="ff0a9-122">Ils peuvent également être [](../../task-modules-and-cards/cards/design-effective-cards.md) créés avec l’infrastructure de cartes adaptatives, qui peut être un moyen plus simple et plus rapide de faciliter les scénarios courants (tels que les formulaires).</span><span class="sxs-lookup"><span data-stu-id="ff0a9-122">They can also be built with the [Adaptive Cards](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to facilitate common scenarios (such as forms).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-123">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-123">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un module de tâche." border="false":::

|<span data-ttu-id="ff0a9-125">Compteur</span><span class="sxs-lookup"><span data-stu-id="ff0a9-125">Counter</span></span>|<span data-ttu-id="ff0a9-126">Description</span><span class="sxs-lookup"><span data-stu-id="ff0a9-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ff0a9-127">1</span><span class="sxs-lookup"><span data-stu-id="ff0a9-127">1</span></span>|<span data-ttu-id="ff0a9-128">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="ff0a9-128">**App icon**</span></span>|
|<span data-ttu-id="ff0a9-129">2</span><span class="sxs-lookup"><span data-stu-id="ff0a9-129">2</span></span>|<span data-ttu-id="ff0a9-130">**Nom de l’application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="ff0a9-131">3</span><span class="sxs-lookup"><span data-stu-id="ff0a9-131">3</span></span>|<span data-ttu-id="ff0a9-132">**En-tête :** rendre les en-têtes clairs et concis.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="ff0a9-133">Décrivez la tâche que vous souhaitez que les utilisateurs terminent.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="ff0a9-134">4 </span><span class="sxs-lookup"><span data-stu-id="ff0a9-134">4</span></span>|<span data-ttu-id="ff0a9-135">**Bouton Fermer :** ferme le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-135">**Close button**: Closes the task module.</span></span> <span data-ttu-id="ff0a9-136">N’applique pas les modifications non notées dans le contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-136">Does not apply unsaved changes in the app content.</span></span>|
|<span data-ttu-id="ff0a9-137">5 </span><span class="sxs-lookup"><span data-stu-id="ff0a9-137">5</span></span>|<span data-ttu-id="ff0a9-138">**iframe**: espace réactif qui héberge le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-138">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="ff0a9-139">6 </span><span class="sxs-lookup"><span data-stu-id="ff0a9-139">6</span></span>|<span data-ttu-id="ff0a9-140">**Actions (facultatives)**: boutons liés au contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-140">**Actions (optional)**: Buttons related to your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-141">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-141">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un module de tâche sur mobile." border="false":::

|<span data-ttu-id="ff0a9-143">Compteur</span><span class="sxs-lookup"><span data-stu-id="ff0a9-143">Counter</span></span>|<span data-ttu-id="ff0a9-144">Description</span><span class="sxs-lookup"><span data-stu-id="ff0a9-144">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ff0a9-145">1</span><span class="sxs-lookup"><span data-stu-id="ff0a9-145">1</span></span>|<span data-ttu-id="ff0a9-146">**En-tête :** rendre les en-têtes clairs et concis.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-146">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="ff0a9-147">Décrivez la tâche que vous souhaitez que les utilisateurs terminent.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-147">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="ff0a9-148">2</span><span class="sxs-lookup"><span data-stu-id="ff0a9-148">2</span></span>|<span data-ttu-id="ff0a9-149">**Nom de l’application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-149">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="ff0a9-150">3</span><span class="sxs-lookup"><span data-stu-id="ff0a9-150">3</span></span>|<span data-ttu-id="ff0a9-151">**Bouton Fermer :** ferme le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-151">**Close button**: Closes the task module.</span></span> <span data-ttu-id="ff0a9-152">N’applique pas les modifications non notées dans le contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-152">Does not apply unsaved changes in the app content.</span></span>|
|<span data-ttu-id="ff0a9-153">4 </span><span class="sxs-lookup"><span data-stu-id="ff0a9-153">4</span></span>|<span data-ttu-id="ff0a9-154">**webview**: espace réactif qui héberge le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-154">**webview**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="ff0a9-155">5 </span><span class="sxs-lookup"><span data-stu-id="ff0a9-155">5</span></span>|<span data-ttu-id="ff0a9-156">**Actions (facultatives)**: boutons liés au contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-156">**Actions (optional)**: Buttons related to your app content.</span></span>|

---

## <a name="designing-with-ui-templates"></a><span data-ttu-id="ff0a9-157">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ff0a9-157">Designing with UI templates</span></span>

<span data-ttu-id="ff0a9-158">Envisagez d’utiliser des modèles pour les dispositions courantes à l’intérieur de vos modules de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-158">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="ff0a9-159">Chacun d’eux est composé de composants plus petits pour créer une conception réactive et eloyable qui peut être utilisée de manière personnalisée ou adaptée à votre scénario ou à votre apparence de marque.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-159">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="ff0a9-160">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-160">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="ff0a9-161">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-161">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="ff0a9-162">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-162">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="ff0a9-163">Exemples</span><span class="sxs-lookup"><span data-stu-id="ff0a9-163">Examples</span></span>

### <a name="list"></a><span data-ttu-id="ff0a9-164">Répertorier</span><span class="sxs-lookup"><span data-stu-id="ff0a9-164">List</span></span>

<span data-ttu-id="ff0a9-165">Les listes fonctionnent parfaitement dans un module de tâche, car elles sont faciles à analyser.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-165">Lists work nicely in a task module because they're easy to scan.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-166">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-166">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Exemple de liste dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-168">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-168">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="Exemple de liste dans un module de tâche sur mobile." border="false":::

---

### <a name="form"></a><span data-ttu-id="ff0a9-170">Formulaire</span><span class="sxs-lookup"><span data-stu-id="ff0a9-170">Form</span></span>

<span data-ttu-id="ff0a9-171">Les modules de tâche sont un excellent endroit pour faire surface à des formulaires avec des entrées utilisateur séquentielles et une validation en ligne.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-171">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="ff0a9-172">Vous pouvez utiliser des cartes adaptatives pour incorporer des éléments de formulaire.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-172">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-173">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-173">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Exemple de formulaire dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-175">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="Exemple de formulaire dans un module de tâche sur mobile." border="false":::

---

### <a name="sign-in"></a><span data-ttu-id="ff0a9-177">Se connecter</span><span class="sxs-lookup"><span data-stu-id="ff0a9-177">Sign in</span></span>

<span data-ttu-id="ff0a9-178">Créez un flux de signature ou d’inscription centré avec une série de modules de tâche, ce qui permet aux utilisateurs de se déplacer facilement à travers les étapes séquentielles.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-178">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-179">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Exemple d’expérience de signature dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-181">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="Exemple d’expérience de la signature dans un module de tâche sur mobile." border="false":::

---

### <a name="media"></a><span data-ttu-id="ff0a9-183">Support</span><span class="sxs-lookup"><span data-stu-id="ff0a9-183">Media</span></span>

<span data-ttu-id="ff0a9-184">Incorporer du contenu multimédia dans un module de tâche pour une expérience d’affichage axée sur l’affichage.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-184">Embed media content in a task module for a focused viewing experience.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-185">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-185">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Exemple de contenu multimédia dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-187">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-187">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="Exemple de contenu multimédia dans un module de tâche sur mobile." border="false":::

---

### <a name="empty-state"></a><span data-ttu-id="ff0a9-189">État vide</span><span class="sxs-lookup"><span data-stu-id="ff0a9-189">Empty state</span></span>

<span data-ttu-id="ff0a9-190">À utiliser pour les messages d’accueil, d’erreur et de réussite.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-190">Use for welcome, error, and success messages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-191">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-191">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Exemple d’état vide dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-193">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-193">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="Exemple d’état vide dans un module de tâche sur mobile." border="false":::

---

### <a name="image-gallery"></a><span data-ttu-id="ff0a9-195">Galerie d’images</span><span class="sxs-lookup"><span data-stu-id="ff0a9-195">Image gallery</span></span>

<span data-ttu-id="ff0a9-196">Incorporer un carrousel de galerie dans un iframe (bureau) ou une vue web (mobile).</span><span class="sxs-lookup"><span data-stu-id="ff0a9-196">Embed a gallery carousel in an iframe (desktop) or webview (mobile).</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-197">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Exemple de galerie d’images dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-199">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="Exemple de galerie d’images dans un module de tâche sur mobile." border="false":::

---

### <a name="poll"></a><span data-ttu-id="ff0a9-201">Sondage</span><span class="sxs-lookup"><span data-stu-id="ff0a9-201">Poll</span></span>

<span data-ttu-id="ff0a9-202">Cet exemple montre les résultats des sondages lancés à partir d’une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-202">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="ff0a9-203">Le sondage peut également être placé à l’intérieur d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-203">The poll can be placed inside a task module, too.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="ff0a9-204">Desktop</span><span class="sxs-lookup"><span data-stu-id="ff0a9-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Exemple d’enquête dans un module de tâche." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="ff0a9-206">Mobile</span><span class="sxs-lookup"><span data-stu-id="ff0a9-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="Exemple d’enquête dans un module de tâche sur mobile." border="false":::

---

## <a name="best-practices"></a><span data-ttu-id="ff0a9-208">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="ff0a9-208">Best practices</span></span>

<span data-ttu-id="ff0a9-209">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-209">Use these recommendations to create a quality app experience.</span></span>

### <a name="usability"></a><span data-ttu-id="ff0a9-210">Utilisation</span><span class="sxs-lookup"><span data-stu-id="ff0a9-210">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (un module de tâche à la fois)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="ff0a9-212">À faire : utiliser un module de tâche à la fois</span><span class="sxs-lookup"><span data-stu-id="ff0a9-212">Do: Use one task module at a time</span></span>

<span data-ttu-id="ff0a9-213">L’objectif est de concentrer l’utilisateur sur l’exécution d’une tâche après tout !</span><span class="sxs-lookup"><span data-stu-id="ff0a9-213">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (afficher une boîte de dialogue au-dessus d’un module de tâche)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="ff0a9-215">À ne pas faire : faire apparaître une boîte de dialogue au-dessus d’un module de tâche</span><span class="sxs-lookup"><span data-stu-id="ff0a9-215">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="ff0a9-216">Cela crée une expérience utilisateur déconcertante et non recentrée.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-216">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="ff0a9-217">Réactive</span><span class="sxs-lookup"><span data-stu-id="ff0a9-217">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Exemple montrant une meilleure pratique de module de tâche (assurez-vous que le contenu est réactif)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="ff0a9-219">À faire : assurez-vous que le contenu est réactif</span><span class="sxs-lookup"><span data-stu-id="ff0a9-219">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="ff0a9-220">Bien que les cartes adaptatives hébergées dans un module de tâche s’restituent bien sur les appareils mobiles, si vous choisissez d’utiliser un iframe pour héberger du contenu d’application, assurez-vous que l’interface utilisateur est réactive et fonctionne bien sur tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-220">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (n’utilisez pas de barres de défilement horizontales)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="ff0a9-222">À ne pas faire : utiliser des barres de défilement horizontales</span><span class="sxs-lookup"><span data-stu-id="ff0a9-222">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="ff0a9-223">Il est préférable de garder le contenu concentré et pas trop long.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-223">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="ff0a9-224">Si un défilement est nécessaire, faites défiler verticalement et non horizontalement.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-224">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="ff0a9-225">Simplicité</span><span class="sxs-lookup"><span data-stu-id="ff0a9-225">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (restez bref)." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="ff0a9-227">Do: Keep it short</span><span class="sxs-lookup"><span data-stu-id="ff0a9-227">Do: Keep it short</span></span>

<span data-ttu-id="ff0a9-228">Vous pouvez facilement créer un Assistant en plusieurs étapes, mais cela ne signifie pas nécessairement que vous le devriez !</span><span class="sxs-lookup"><span data-stu-id="ff0a9-228">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="ff0a9-229">Un module de tâche multi-écran peut être problématique, car les messages entrants sont distrayants et tentant les utilisateurs de quitter.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-229">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="ff0a9-230">Si votre tâche est vraiment impliquée, itéz une page web complète au lieu d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-230">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (n’avez pas d’interactions longues)." border="false":::

#### <a name="dont-have-long-interactions"></a><span data-ttu-id="ff0a9-232">À ne pas faire : avoir de longues interactions</span><span class="sxs-lookup"><span data-stu-id="ff0a9-232">Don't: Have long interactions</span></span>

<span data-ttu-id="ff0a9-233">Essayez de maintenir vos interactions courtes et au point.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-233">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="ff0a9-234">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="ff0a9-234">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (utiliser des messages d’erreur en ligne)." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="ff0a9-236">À faire : utiliser les messages d’erreur inline</span><span class="sxs-lookup"><span data-stu-id="ff0a9-236">Do: Use inline error messages</span></span>

<span data-ttu-id="ff0a9-237">Consultez le modèle d’interface utilisateur de formulaires pour obtenir des instructions sur la gestion des erreurs en ligne.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-237">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Exemple montrant la meilleure pratique d’un module de tâche (placer des messages d’erreur dans des boîtes de dialogue)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="ff0a9-239">À ne pas faire : placer des messages d’erreur dans des boîtes de dialogue</span><span class="sxs-lookup"><span data-stu-id="ff0a9-239">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="ff0a9-240">Ne pas faire apparaître de message d’erreur dans une boîte de dialogue au-dessus d’un module de tâche.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-240">Don't pop an error message in a dialog on top of a task module.</span></span> <span data-ttu-id="ff0a9-241">Cela crée une expérience utilisateur confuse.</span><span class="sxs-lookup"><span data-stu-id="ff0a9-241">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
