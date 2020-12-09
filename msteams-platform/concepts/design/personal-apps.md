---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application personnelle teams et obtenir le kit d’interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604989"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="c0722-103">Conception de votre application personnelle pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="c0722-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="c0722-104">Une application personnelle peut être un bot, un espace de travail privé ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c0722-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="c0722-105">Parfois, il fonctionne comme un emplacement de création ou d’affichage de contenu, d’autres fois qu’il offre à l’utilisateur un aperçu de tous ses éléments lorsque l’application a été configurée sous la forme d’un onglet dans plusieurs canaux.</span><span class="sxs-lookup"><span data-stu-id="c0722-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that’s theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="c0722-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.</span><span class="sxs-lookup"><span data-stu-id="c0722-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c0722-107">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="c0722-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c0722-108">Vous trouverez des instructions de conception d’applications personnelles complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c0722-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="c0722-109">Le kit d’interface utilisateur comporte également des rubriques essentielles, telles que l’accessibilité et le dimensionnement réactif, qui ne sont pas abordées ici.</span><span class="sxs-lookup"><span data-stu-id="c0722-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0722-110">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="c0722-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="c0722-111">Ajouter une application personnelle</span><span class="sxs-lookup"><span data-stu-id="c0722-111">Add a personal app</span></span>

<span data-ttu-id="c0722-112">Vous pouvez ajouter une application personnelle à partir du magasin de Teams (AppSource) ou le menu volant d’application en sélectionnant l’icône **plus** sur le côté gauche de Teams (illustré dans l’exemple ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="c0722-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Exemple montre comment ajouter une application personnelle à partir de la fenêtre mobile d’application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="c0722-114">Utiliser une application personnelle (espace de travail privé)</span><span class="sxs-lookup"><span data-stu-id="c0722-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="c0722-115">Avec un espace de travail privé, vous pouvez afficher le contenu de l’application qui est significatif pour vous dans un emplacement central sans quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="c0722-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="c0722-116">(Mise en œuvre Remarque : l’espace de travail privé est basé sur les fonctionnalités de l' [*onglet personnel*](../../build-your-first-app/build-personal-tab.md) .)</span><span class="sxs-lookup"><span data-stu-id="c0722-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="c0722-117">Anatomie : application personnelle (espace de travail privé)</span><span class="sxs-lookup"><span data-stu-id="c0722-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="Exemple illustre l’anatomie du composant de l’onglet personnel." border="false":::

|<span data-ttu-id="c0722-119">Compteur</span><span class="sxs-lookup"><span data-stu-id="c0722-119">Counter</span></span>|<span data-ttu-id="c0722-120">Description</span><span class="sxs-lookup"><span data-stu-id="c0722-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c0722-121">A</span><span class="sxs-lookup"><span data-stu-id="c0722-121">A</span></span>|<span data-ttu-id="c0722-122">**Attribution d’application**: logo et nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="c0722-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="c0722-123">B</span><span class="sxs-lookup"><span data-stu-id="c0722-123">B</span></span>|<span data-ttu-id="c0722-124">**Onglets**: permet de naviguer dans votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="c0722-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="c0722-125">Par exemple, inclure un onglet **à propos** de ou **d’aide** .</span><span class="sxs-lookup"><span data-stu-id="c0722-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="c0722-126">C</span><span class="sxs-lookup"><span data-stu-id="c0722-126">C</span></span>|<span data-ttu-id="c0722-127">**Vue contextuelle**: envoie le contenu de votre application d’une fenêtre parente à une fenêtre enfant autonome.</span><span class="sxs-lookup"><span data-stu-id="c0722-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="c0722-128">D</span><span class="sxs-lookup"><span data-stu-id="c0722-128">D</span></span>|<span data-ttu-id="c0722-129">**Autres menus**: inclut des informations et des options d’application supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="c0722-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="c0722-130">(Vous pouvez également définir les **paramètres** d’un onglet.)</span><span class="sxs-lookup"><span data-stu-id="c0722-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle de l’onglet personnel." border="false":::

|<span data-ttu-id="c0722-132">Compteur</span><span class="sxs-lookup"><span data-stu-id="c0722-132">Counter</span></span>|<span data-ttu-id="c0722-133">Description</span><span class="sxs-lookup"><span data-stu-id="c0722-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c0722-134">A</span><span class="sxs-lookup"><span data-stu-id="c0722-134">A</span></span>|<span data-ttu-id="c0722-135">**Onglets**: permet de naviguer dans votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="c0722-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="c0722-136">1 </span><span class="sxs-lookup"><span data-stu-id="c0722-136">1</span></span>|<span data-ttu-id="c0722-137">**IFRAME**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="c0722-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="c0722-138">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="c0722-138">Designing with UI templates</span></span>

<span data-ttu-id="c0722-139">Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre onglet personnel :</span><span class="sxs-lookup"><span data-stu-id="c0722-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="c0722-140">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="c0722-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="c0722-141">[Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board): un tableau des tâches, parfois appelé tableau kanban ou couloirs de natation, est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="c0722-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="c0722-142">[Tableau](../../concepts/design/design-teams-app-ui-templates.md#dashboard)de bord : un tableau de bord est une zone de dessin contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="c0722-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="c0722-143">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="c0722-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="c0722-144">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="c0722-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="c0722-145">Navigation de [gauche](../../concepts/design/design-teams-app-ui-templates.md#left-nav): le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="c0722-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="c0722-146">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="c0722-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="c0722-147">Utiliser une application personnelle (bot)</span><span class="sxs-lookup"><span data-stu-id="c0722-147">Use a personal app (bot)</span></span>

<span data-ttu-id="c0722-148">Les applications personnelles peuvent inclure un bot pour les conversations et les notifications privées en un seul (par exemple, lorsqu’un collègue envoie un commentaire sur votre planche graphique).</span><span class="sxs-lookup"><span data-stu-id="c0722-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="c0722-149">Le bot est disponible sous un onglet que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="c0722-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="c0722-150">Anatomie : application personnelle (bot)</span><span class="sxs-lookup"><span data-stu-id="c0722-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Exemple illustre l’anatomie du composant bot personnel." border="false":::

|<span data-ttu-id="c0722-152">Compteur</span><span class="sxs-lookup"><span data-stu-id="c0722-152">Counter</span></span>|<span data-ttu-id="c0722-153">Description</span><span class="sxs-lookup"><span data-stu-id="c0722-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c0722-154">A</span><span class="sxs-lookup"><span data-stu-id="c0722-154">A</span></span>|<span data-ttu-id="c0722-155">**Onglet bot**: par exemple, inclure un onglet de **conversation** pour accéder aux conversations et notifications du robot.</span><span class="sxs-lookup"><span data-stu-id="c0722-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="c0722-156">B</span><span class="sxs-lookup"><span data-stu-id="c0722-156">B</span></span>|<span data-ttu-id="c0722-157">**Message bot**: les robots envoient souvent des messages et des notifications sous la forme d’une carte (telle qu’une carte adaptative).</span><span class="sxs-lookup"><span data-stu-id="c0722-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="c0722-158">C</span><span class="sxs-lookup"><span data-stu-id="c0722-158">C</span></span>|<span data-ttu-id="c0722-159">**Zone de composition**: champ d’entrée pour l’envoi de messages au bot.</span><span class="sxs-lookup"><span data-stu-id="c0722-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="c0722-160">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="c0722-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="c0722-161">Priorité de l’onglet</span><span class="sxs-lookup"><span data-stu-id="c0722-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="c0722-162">Do : afficher le contenu le plus pertinent dans le premier onglet</span><span class="sxs-lookup"><span data-stu-id="c0722-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="c0722-163">Avec un dimensionnement réactif, les onglets à droite peuvent être tronqués ou en dehors de l’affichage.</span><span class="sxs-lookup"><span data-stu-id="c0722-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="c0722-165">Ne pas : utiliser le contenu secondaire ou les métadonnées</span><span class="sxs-lookup"><span data-stu-id="c0722-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="c0722-166">À l’instar d’une application Web standard, la navigation à onglet doit progresser dans un ordre qui permet de mieux appréhender les fonctionnalités principales de votre application.</span><span class="sxs-lookup"><span data-stu-id="c0722-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="c0722-168">Hiérarchie d’onglets</span><span class="sxs-lookup"><span data-stu-id="c0722-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="c0722-169">Do : les onglets doivent être de même hiérarchie et représenter les pages d’application clés</span><span class="sxs-lookup"><span data-stu-id="c0722-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="c0722-170">Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="c0722-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="c0722-171">Avec un dimensionnement réactif, le contenu à droite peut être tronqué ou inactif.</span><span class="sxs-lookup"><span data-stu-id="c0722-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="c0722-173">Ne pas inclure différents niveaux de hiérarchie</span><span class="sxs-lookup"><span data-stu-id="c0722-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="c0722-174">Votre contenu doit progresser dans un ordre logique qui permet aux utilisateurs de le détecter.</span><span class="sxs-lookup"><span data-stu-id="c0722-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="c0722-175">Si vous avez deux onglets étroitement liés, envisagez de les combiner en un seul onglet.</span><span class="sxs-lookup"><span data-stu-id="c0722-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="c0722-177">Première expérience d’utilisation</span><span class="sxs-lookup"><span data-stu-id="c0722-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="c0722-178">Do : inclure une expérience de première exécution</span><span class="sxs-lookup"><span data-stu-id="c0722-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="c0722-179">Il doit y avoir au moins un écran d’accueil la première fois que vous utilisez une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="c0722-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="c0722-180">Pour les robots, décrivez ce que votre robot peut faire et fournissez des actions rapides, telles qu’un bouton de connexion.</span><span class="sxs-lookup"><span data-stu-id="c0722-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="c0722-183">Ne pas : Démarrer avec un écran vide</span><span class="sxs-lookup"><span data-stu-id="c0722-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="c0722-184">Les utilisateurs peuvent être confondus si rien ne s’affiche la première fois qu’ils exécutent votre application.</span><span class="sxs-lookup"><span data-stu-id="c0722-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="c0722-186">Contenu personnalisé</span><span class="sxs-lookup"><span data-stu-id="c0722-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="c0722-187">Do : agréger le contenu d’application pertinent pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="c0722-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="c0722-188">Qu’il s’agisse d’un onglet personnel ou d’un bot, affiche le contenu associé uniquement à l’activité d’un utilisateur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="c0722-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="c0722-191">Ne pas : afficher le contenu non lié ou trop large</span><span class="sxs-lookup"><span data-stu-id="c0722-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="c0722-192">Dans les contextes personnels, n’affichez pas de contenu pour les équipes auxquelles l’utilisateur ne fait pas partie.</span><span class="sxs-lookup"><span data-stu-id="c0722-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="c0722-193">Le contenu de la bot doit se concentrer sur le individu, pas sur un groupe.</span><span class="sxs-lookup"><span data-stu-id="c0722-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="c0722-196">Fonctionnalités d’application complexes</span><span class="sxs-lookup"><span data-stu-id="c0722-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="c0722-197">Do : autoriser les utilisateurs à accéder aux fonctionnalités complexes dans un navigateur</span><span class="sxs-lookup"><span data-stu-id="c0722-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="c0722-198">Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l’application autonome complète dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="c0722-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="c0722-200">Ne pas inclure votre application entière</span><span class="sxs-lookup"><span data-stu-id="c0722-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="c0722-201">Sauf si vous avez créé votre application spécifiquement pour Teams, vous disposez probablement de fonctionnalités qui n’ont pas de sens dans un outil de collaboration.</span><span class="sxs-lookup"><span data-stu-id="c0722-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Exemple illustre une meilleure pratique pour une application personnelle." border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="c0722-203">Gérer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="c0722-203">Manage a personal tab</span></span>

<span data-ttu-id="c0722-204">Sur le côté gauche de teams, les utilisateurs peuvent cliquer avec le bouton droit sur l’application personnelle pour épingler, supprimer et configurer d’autres options d’application.</span><span class="sxs-lookup"><span data-stu-id="c0722-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Exemple affiche des options de gestion d’une application personnelle." border="false":::

## <a name="learn-more"></a><span data-ttu-id="c0722-206">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="c0722-206">Learn more</span></span>

<span data-ttu-id="c0722-207">Ces autres instructions de conception peuvent vous aider en fonction de l’étendue de votre application personnelle :</span><span class="sxs-lookup"><span data-stu-id="c0722-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="c0722-208">Création de votre onglet</span><span class="sxs-lookup"><span data-stu-id="c0722-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="c0722-209">Conception de votre robot</span><span class="sxs-lookup"><span data-stu-id="c0722-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="c0722-210">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="c0722-210">Validate your design</span></span>

<span data-ttu-id="c0722-211">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="c0722-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0722-212">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="c0722-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
