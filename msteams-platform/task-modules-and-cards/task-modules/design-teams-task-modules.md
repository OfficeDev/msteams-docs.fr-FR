---
title: Création de modules de tâches
author: heath-hamilton
description: Découvrez comment concevoir des modules de tâches pour les applications teams et obtenir le kit d’interface utilisateur Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606198"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="e1a3e-103">Conception de modules de tâches pour votre application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="e1a3e-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="e1a3e-104">Vous pouvez créer des expériences de menu contextuel modal dans votre application de teams avec des modules de tâches.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="e1a3e-105">Utilisez cette fonctionnalité pour afficher des informations et des médias enrichis ou effectuer une tâche complexe.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="Exemple de module de tâche." border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="e1a3e-107">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="e1a3e-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="e1a3e-108">Vous trouverez des instructions de conception de module de tâches plus complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1a3e-109">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="e1a3e-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="e1a3e-110">Ouvrir un module de tâches</span><span class="sxs-lookup"><span data-stu-id="e1a3e-110">Open a task module</span></span>

<span data-ttu-id="e1a3e-111">Les modules de tâches peuvent être lancés à partir de quasiment n’importe où dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="e1a3e-112">**Onglet**: un module de tâches peut être lancé à partir de n’importe quel lien dans un onglet ou un IFRAME.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-112">**Tab**: A task module can be launched from any link within a tab or iframe.</span></span> <span data-ttu-id="e1a3e-113">À utiliser dans les scénarios dans lesquels vous souhaitez que l’utilisateur se focalise sur une interaction.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-113">Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="e1a3e-114">**Bot**: un module de tâche peut être lancé à partir d’un lien à l’intérieur d’un message de robot.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-114">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="e1a3e-115">**Carte adaptative**: un module de tâches peut être lancé à partir d’une carte adaptative (envoyée avec une extension de messagerie ou un bot) lorsqu’un utilisateur sélectionne un bouton.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-115">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="e1a3e-116">**Extension de messagerie (commandes action)**: les extensions de messagerie vous permettent d’effectuer une action particulière sur le contenu des messages.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-116">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="e1a3e-117">La sélection d’une action ouvre un module de tâches.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-117">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="e1a3e-118">**Extension de messagerie (contexte de la zone de composition)**: dans la zone de composition, vous pouvez concevoir une extension de messagerie pour ouvrir un module de tâches au lieu du menu volant standard.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-118">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="e1a3e-119">Réservez les modules de tâche pour les interactions complexes, comme la réalisation d’un formulaire.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-119">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="e1a3e-120">Anatomie</span><span class="sxs-lookup"><span data-stu-id="e1a3e-120">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un module de tâches." border="false":::

<span data-ttu-id="e1a3e-122">Les modules de tâches sont des surfaces très flexibles.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-122">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="e1a3e-123">Ils peuvent être créés avec des IFRAMES, en extrayant d’autres modèles de l’interface utilisateur, pour héberger des expériences créées par des partenaires.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-123">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="e1a3e-124">Cette approche est recommandée pour l’expérience la plus soignée.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-124">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="e1a3e-125">Elles peuvent également être créées à l’aide de l’infrastructure de [carte adaptative](../../task-modules-and-cards/cards/design-effective-cards.md) , qui peut être plus simple et plus rapide pour exécuter des scénarios courants (tels que des formulaires).</span><span class="sxs-lookup"><span data-stu-id="e1a3e-125">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="e1a3e-126">Compteur</span><span class="sxs-lookup"><span data-stu-id="e1a3e-126">Counter</span></span>|<span data-ttu-id="e1a3e-127">Description</span><span class="sxs-lookup"><span data-stu-id="e1a3e-127">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e1a3e-128">1</span><span class="sxs-lookup"><span data-stu-id="e1a3e-128">1</span></span>|<span data-ttu-id="e1a3e-129">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="e1a3e-129">**App icon**</span></span>|
|<span data-ttu-id="e1a3e-130">2 </span><span class="sxs-lookup"><span data-stu-id="e1a3e-130">2</span></span>|<span data-ttu-id="e1a3e-131">**Nom** de l’application : nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-131">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="e1a3e-132">3 </span><span class="sxs-lookup"><span data-stu-id="e1a3e-132">3</span></span>|<span data-ttu-id="e1a3e-133">**En-tête**: rendez les en-têtes claires et concise.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-133">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="e1a3e-134">Décrivez la tâche que les utilisateurs doivent effectuer.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-134">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="e1a3e-135">4 </span><span class="sxs-lookup"><span data-stu-id="e1a3e-135">4</span></span>|<span data-ttu-id="e1a3e-136">**Bouton Fermer**: permet aux utilisateurs de rechercher le contenu d’application qu’ils souhaitent insérer.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-136">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="e1a3e-137">5 </span><span class="sxs-lookup"><span data-stu-id="e1a3e-137">5</span></span>|<span data-ttu-id="e1a3e-138">**IFRAME**: espace réactif qui héberge le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-138">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="e1a3e-139">6 </span><span class="sxs-lookup"><span data-stu-id="e1a3e-139">6</span></span>|<span data-ttu-id="e1a3e-140">**Actions (facultatif)**: boutons liés au contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-140">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="e1a3e-141">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="e1a3e-141">Designing with UI templates</span></span>

<span data-ttu-id="e1a3e-142">Envisagez d’utiliser des modèles pour des dispositions courantes à l’intérieur de vos modules de tâches.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-142">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="e1a3e-143">Chacune d’entre elles est composée de plus petits composants pour créer une conception élégante et réactive pouvant être utilisée ou personnalisée pour votre scénario ou avec l’apparence de votre marque.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-143">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="e1a3e-144">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-144">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="e1a3e-145">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-145">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="e1a3e-146">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-146">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="e1a3e-147">Exemples</span><span class="sxs-lookup"><span data-stu-id="e1a3e-147">Examples</span></span>

### <a name="list"></a><span data-ttu-id="e1a3e-148">Répertorier</span><span class="sxs-lookup"><span data-stu-id="e1a3e-148">List</span></span>

<span data-ttu-id="e1a3e-149">Les listes fonctionnent parfaitement dans un module de tâches, car elles sont faciles à analyser.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-149">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Exemple de liste dans un module de tâches." border="false":::

### <a name="form"></a><span data-ttu-id="e1a3e-151">Formulaire</span><span class="sxs-lookup"><span data-stu-id="e1a3e-151">Form</span></span>

<span data-ttu-id="e1a3e-152">Les modules de tâches constituent un excellent point de vue des formulaires avec des entrées utilisateur et une validation en ligne séquentielles.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-152">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="e1a3e-153">Vous pouvez utiliser des cartes adaptatives pour incorporer des éléments de formulaire.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-153">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Exemple de formulaire dans un module de tâches." border="false":::

### <a name="sign-in"></a><span data-ttu-id="e1a3e-155">Se connecter</span><span class="sxs-lookup"><span data-stu-id="e1a3e-155">Sign in</span></span>

<span data-ttu-id="e1a3e-156">Créez une connexion ciblée ou un flux d’inscription avec une série de modules de tâches, ce qui permet aux utilisateurs de se déplacer facilement via des étapes séquentielles.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-156">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Exemple d’expérience de connexion dans un module de tâches." border="false":::

### <a name="media"></a><span data-ttu-id="e1a3e-158">Multimédia</span><span class="sxs-lookup"><span data-stu-id="e1a3e-158">Media</span></span>

<span data-ttu-id="e1a3e-159">Incorporer du contenu multimédia dans un module de tâches pour une expérience de visualisation ciblée.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-159">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Exemple de contenu multimédia dans un module de tâches." border="false":::

### <a name="empty-state"></a><span data-ttu-id="e1a3e-161">État vide</span><span class="sxs-lookup"><span data-stu-id="e1a3e-161">Empty state</span></span>

<span data-ttu-id="e1a3e-162">À utiliser pour les messages d’accueil, d’erreur et de réussite.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-162">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Exemple d’état vide dans un module de tâches." border="false":::

### <a name="image-gallery"></a><span data-ttu-id="e1a3e-164">Galerie d’images</span><span class="sxs-lookup"><span data-stu-id="e1a3e-164">Image gallery</span></span>

<span data-ttu-id="e1a3e-165">Incorporer un carrousel de galerie dans un IFRAME.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-165">Embed a gallery carousel inside an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Exemple de Galerie d’images dans un module de tâches." border="false":::

### <a name="poll"></a><span data-ttu-id="e1a3e-167">Temporisateur</span><span class="sxs-lookup"><span data-stu-id="e1a3e-167">Poll</span></span>

<span data-ttu-id="e1a3e-168">Cet exemple montre les résultats de la requête lancés à partir d’une carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-168">This example shows poll results launched from an Adaptive Card.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Exemple d’interrogation dans un module de tâches." border="false":::

## <a name="best-practices"></a><span data-ttu-id="e1a3e-170">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="e1a3e-170">Best practices</span></span>

### <a name="usability"></a><span data-ttu-id="e1a3e-171">Facilement</span><span class="sxs-lookup"><span data-stu-id="e1a3e-171">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="e1a3e-173">Do : utiliser un module de tâche à la fois</span><span class="sxs-lookup"><span data-stu-id="e1a3e-173">Do: Use one task module at a time</span></span>

<span data-ttu-id="e1a3e-174">L’objectif est de concentrer l’utilisateur sur la réalisation d’une tâche après tout !</span><span class="sxs-lookup"><span data-stu-id="e1a3e-174">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="e1a3e-176">Ne pas : dépiler une boîte de dialogue par-dessus un module de tâches</span><span class="sxs-lookup"><span data-stu-id="e1a3e-176">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="e1a3e-177">Cela crée une expérience utilisateur non ciblée et confuse.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-177">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="e1a3e-178">Réactive</span><span class="sxs-lookup"><span data-stu-id="e1a3e-178">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="e1a3e-180">Do : Assurez-vous que le contenu est réactif</span><span class="sxs-lookup"><span data-stu-id="e1a3e-180">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="e1a3e-181">Alors que les cartes adaptatives hébergées dans un module de tâches s’affichent correctement sur les appareils mobiles, si vous choisissez d’utiliser un IFRAME pour héberger le contenu de l’application, assurez-vous que l’interface utilisateur est réactive et fonctionne bien sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-181">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a><span data-ttu-id="e1a3e-183">Ne pas : utiliser des barres de défilement horizontales</span><span class="sxs-lookup"><span data-stu-id="e1a3e-183">Don't: Use horizontal scrollbars</span></span>

<span data-ttu-id="e1a3e-184">Il est recommandé de conserver le contenu axé sur le contenu et pas trop long.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-184">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="e1a3e-185">Si un défilement est nécessaire, faites défiler verticalement et pas horizontalement.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-185">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="e1a3e-186">Simplification</span><span class="sxs-lookup"><span data-stu-id="e1a3e-186">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="e1a3e-188">Do : conservez-le short</span><span class="sxs-lookup"><span data-stu-id="e1a3e-188">Do: Keep it short</span></span>

<span data-ttu-id="e1a3e-189">Vous pouvez facilement créer un assistant à plusieurs étapes, mais cela ne signifie pas nécessairement que vous devez le faire !</span><span class="sxs-lookup"><span data-stu-id="e1a3e-189">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="e1a3e-190">Un module de tâches à écrans multiples peut être problématique, car les messages entrants sont gênants et les utilisateurs tentant de quitter.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-190">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="e1a3e-191">Si votre tâche est réellement impliquée, affichez-la sur une page Web complète au lieu d’un module de tâches.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-191">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-do-long-interactions"></a><span data-ttu-id="e1a3e-193">Ne pas : effectuer des interactions longues</span><span class="sxs-lookup"><span data-stu-id="e1a3e-193">Don't: Do long interactions</span></span>

<span data-ttu-id="e1a3e-194">Essayez de conserver vos interactions courtes et jusqu’au point.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-194">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="e1a3e-195">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="e1a3e-195">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="e1a3e-197">Do : utiliser des messages d’erreur incorporés</span><span class="sxs-lookup"><span data-stu-id="e1a3e-197">Do: Use inline error messages</span></span>

<span data-ttu-id="e1a3e-198">Consultez le modèle d’interface utilisateur formulaires pour obtenir des instructions sur la gestion des erreurs Inline.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-198">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Exemple illustrant une meilleure pratique pour le module de tâches." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="e1a3e-200">Ne pas : placer les messages d’erreur dans les boîtes de dialogue</span><span class="sxs-lookup"><span data-stu-id="e1a3e-200">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="e1a3e-201">Ne pas afficher un message d’erreur dans une boîte de dialogue en haut d’un module de tâches.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-201">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="e1a3e-202">Il crée une expérience utilisateur confuse.</span><span class="sxs-lookup"><span data-stu-id="e1a3e-202">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
