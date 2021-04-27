---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application personnelle Teams et obtenir le Kit d'interface utilisateur Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 8302f3768034014ef5a446effeee0603afe4a5f4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020757"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="f6079-103">Conception de votre application personnelle pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f6079-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="f6079-104">Une application personnelle peut être un bot, un espace de travail privé ou les deux.</span><span class="sxs-lookup"><span data-stu-id="f6079-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="f6079-105">Parfois, il fonctionne comme un endroit pour créer ou afficher du contenu, d'autres fois, il offre à l'utilisateur une vue d'ensemble de tout ce qui lui est propre lorsque l'application a été configurée sous la forme d'un onglet dans plusieurs canaux.</span><span class="sxs-lookup"><span data-stu-id="f6079-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="f6079-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.</span><span class="sxs-lookup"><span data-stu-id="f6079-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="f6079-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f6079-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="f6079-108">Vous trouverez des instructions complètes sur la conception d'applications personnelles, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f6079-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="f6079-109">Le kit d'interface utilisateur contient également des rubriques essentielles telles que l'accessibilité et le resserrement réactif qui ne sont pas abordés ici.</span><span class="sxs-lookup"><span data-stu-id="f6079-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6079-110">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="f6079-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="f6079-111">Ajouter une application personnelle</span><span class="sxs-lookup"><span data-stu-id="f6079-111">Add a personal app</span></span>

<span data-ttu-id="f6079-112">Vous pouvez ajouter une application personnelle à partir du magasin Teams (AppSource) ou du flyout de l'application en sélectionnant l'icône Plus sur le côté gauche de Teams (illustré dans l'exemple suivant). </span><span class="sxs-lookup"><span data-stu-id="f6079-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="L'exemple montre comment ajouter une application personnelle à partir du flyout de l'application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="f6079-114">Utiliser une application personnelle (espace de travail privé)</span><span class="sxs-lookup"><span data-stu-id="f6079-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="f6079-115">Avec un espace de travail privé, vous pouvez afficher le contenu de l'application qui vous semble significatif dans un emplacement central sans quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="f6079-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="f6079-116">(Remarque d'implémentation : l'espace de travail privé est basé sur la [*fonctionnalité d'onglet*](../../build-your-first-app/build-personal-tab.md) personnel.)</span><span class="sxs-lookup"><span data-stu-id="f6079-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="f6079-117">Anatomie : application personnelle (espace de travail privé)</span><span class="sxs-lookup"><span data-stu-id="f6079-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="L'exemple montre l'anatomie des composants de l'onglet personnel." border="false":::

|<span data-ttu-id="f6079-119">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6079-119">Counter</span></span>|<span data-ttu-id="f6079-120">Description</span><span class="sxs-lookup"><span data-stu-id="f6079-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6079-121">A</span><span class="sxs-lookup"><span data-stu-id="f6079-121">A</span></span>|<span data-ttu-id="f6079-122">**Attribution de l'application**: nom et logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6079-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="f6079-123">B</span><span class="sxs-lookup"><span data-stu-id="f6079-123">B</span></span>|<span data-ttu-id="f6079-124">**Onglets :** fournit la navigation pour votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="f6079-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="f6079-125">Par exemple, incluez un **onglet À** propos de ou **Aide.**</span><span class="sxs-lookup"><span data-stu-id="f6079-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="f6079-126">C</span><span class="sxs-lookup"><span data-stu-id="f6079-126">C</span></span>|<span data-ttu-id="f6079-127">**Affichage popout :** pousse le contenu de votre application d'une fenêtre parent vers une fenêtre enfant autonome.</span><span class="sxs-lookup"><span data-stu-id="f6079-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="f6079-128">D</span><span class="sxs-lookup"><span data-stu-id="f6079-128">D</span></span>|<span data-ttu-id="f6079-129">**Menu supplémentaire**: inclut des informations et options supplémentaires sur l'application.</span><span class="sxs-lookup"><span data-stu-id="f6079-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="f6079-130">(Vous pouvez également définir **Paramètres en** onglet.)</span><span class="sxs-lookup"><span data-stu-id="f6079-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="L'exemple montre l'anatomie structurelle de l'onglet personnel." border="false":::

|<span data-ttu-id="f6079-132">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6079-132">Counter</span></span>|<span data-ttu-id="f6079-133">Description</span><span class="sxs-lookup"><span data-stu-id="f6079-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6079-134">A</span><span class="sxs-lookup"><span data-stu-id="f6079-134">A</span></span>|<span data-ttu-id="f6079-135">**Onglets :** fournit la navigation pour votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="f6079-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="f6079-136">1</span><span class="sxs-lookup"><span data-stu-id="f6079-136">1</span></span>|<span data-ttu-id="f6079-137">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6079-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="f6079-138">Conception avec des modèles d'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f6079-138">Designing with UI templates</span></span>

<span data-ttu-id="f6079-139">Utilisez l'un des modèles d'interface utilisateur Teams suivants pour vous aider à concevoir votre onglet personnel :</span><span class="sxs-lookup"><span data-stu-id="f6079-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="f6079-140">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="f6079-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="f6079-141">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l'état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="f6079-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="f6079-142">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d'ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="f6079-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="f6079-143">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="f6079-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="f6079-144">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="f6079-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="f6079-145">[Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="f6079-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="f6079-146">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="f6079-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="f6079-147">Utiliser une application personnelle (bot)</span><span class="sxs-lookup"><span data-stu-id="f6079-147">Use a personal app (bot)</span></span>

<span data-ttu-id="f6079-148">Les applications personnelles peuvent inclure un bot pour les conversations un-à-un et des notifications privées (par exemple, lorsqu'un collègue publie un commentaire sur votre tableau de bord).</span><span class="sxs-lookup"><span data-stu-id="f6079-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="f6079-149">Le bot est disponible dans un onglet que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="f6079-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="f6079-150">Anatomie : application personnelle (bot)</span><span class="sxs-lookup"><span data-stu-id="f6079-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="L'exemple montre l'anatomie des composants personnels du bot." border="false":::

|<span data-ttu-id="f6079-152">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6079-152">Counter</span></span>|<span data-ttu-id="f6079-153">Description</span><span class="sxs-lookup"><span data-stu-id="f6079-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6079-154">A</span><span class="sxs-lookup"><span data-stu-id="f6079-154">A</span></span>|<span data-ttu-id="f6079-155">**Onglet Bot**: par exemple, incluez un onglet **Conversation** pour accéder aux conversations et notifications des bots.</span><span class="sxs-lookup"><span data-stu-id="f6079-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="f6079-156">B</span><span class="sxs-lookup"><span data-stu-id="f6079-156">B</span></span>|<span data-ttu-id="f6079-157">**Message du bot**: les bots envoient souvent des messages et des notifications sous la forme d'une carte (par exemple, une carte adaptative).</span><span class="sxs-lookup"><span data-stu-id="f6079-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="f6079-158">C</span><span class="sxs-lookup"><span data-stu-id="f6079-158">C</span></span>|<span data-ttu-id="f6079-159">**Zone de composition**: champ d'entrée pour l'envoi de messages au bot.</span><span class="sxs-lookup"><span data-stu-id="f6079-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="f6079-160">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="f6079-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="f6079-161">Priorité de l'onglet</span><span class="sxs-lookup"><span data-stu-id="f6079-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="f6079-162">À faire : afficher le contenu le plus pertinent dans le premier onglet</span><span class="sxs-lookup"><span data-stu-id="f6079-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="f6079-163">Avec le resserré réactif, les onglets de droite peuvent être tronqués ou en dehors de la vue.</span><span class="sxs-lookup"><span data-stu-id="f6079-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="L'exemple illustre les meilleures pratiques d'une application personnelle." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="f6079-165">À ne pas faire : diriger avec du contenu ou des métadonnées secondaires</span><span class="sxs-lookup"><span data-stu-id="f6079-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="f6079-166">À l'exemple d'une application web standard, la navigation par onglets doit s'effectuer dans un ordre qui vous aide à prendre en compte les principales fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6079-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Exemple de meilleure pratique pour une application personnelle." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="f6079-168">Hiérarchie d'onglets</span><span class="sxs-lookup"><span data-stu-id="f6079-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="f6079-169">À faire : les onglets doivent être de hiérarchie égale et représenter des pages d'application clés</span><span class="sxs-lookup"><span data-stu-id="f6079-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="f6079-170">Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6079-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="f6079-171">Avec le resserré réactif, le contenu à droite peut être tronqué ou hors de vue.</span><span class="sxs-lookup"><span data-stu-id="f6079-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="L'exemple illustre les meilleures pratiques d'application personnelle." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="f6079-173">À ne pas faire : inclure différents niveaux de hiérarchie</span><span class="sxs-lookup"><span data-stu-id="f6079-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="f6079-174">Votre contenu doit évoluer dans un ordre logique qui aide les utilisateurs à le comprendre.</span><span class="sxs-lookup"><span data-stu-id="f6079-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="f6079-175">Si vous avez deux onglets qui sont étroitement liés, envisagez de les combiner en un seul onglet.</span><span class="sxs-lookup"><span data-stu-id="f6079-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="L'exemple affiche les meilleures pratiques d'une application personnelle." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="f6079-177">Première expérience d’utilisation</span><span class="sxs-lookup"><span data-stu-id="f6079-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="f6079-178">À faire : inclure une expérience de première expérience</span><span class="sxs-lookup"><span data-stu-id="f6079-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="f6079-179">Il doit y avoir au moins un écran d'accueil la première fois que vous utilisez une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="f6079-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="f6079-180">Pour les bots, décrivez ce que votre bot peut faire et fournissez des actions rapides, telles qu'un bouton de sign-in.</span><span class="sxs-lookup"><span data-stu-id="f6079-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="Illustration shows a personal app best practice." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Illustration des meilleures pratiques d'une application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="f6079-183">À ne pas faire : démarrer avec un écran vide</span><span class="sxs-lookup"><span data-stu-id="f6079-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="f6079-184">Les utilisateurs peuvent être confondus si rien ne s'affiche la première fois qu'ils exécutent votre application.</span><span class="sxs-lookup"><span data-stu-id="f6079-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="L'illustration affiche les meilleures pratiques d'une application personnelle." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="f6079-186">Contenu personnalisé</span><span class="sxs-lookup"><span data-stu-id="f6079-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="f6079-187">À faire : agréger le contenu d'application pertinent pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f6079-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="f6079-188">Qu'il s'agit d'un onglet personnel ou d'un bot, affichez le contenu lié uniquement à l'activité d'un utilisateur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="f6079-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Cet exemple fournit une meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="L'exemple illustre les meilleures pratiques d'une application personnelle." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="f6079-191">À ne pas faire : afficher du contenu non lié ou trop large</span><span class="sxs-lookup"><span data-stu-id="f6079-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="f6079-192">Dans les contextes personnels, n'affichez pas de contenu pour les équipes dont un utilisateur ne fait pas partie.</span><span class="sxs-lookup"><span data-stu-id="f6079-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="f6079-193">Le contenu du bot personnel doit se concentrer sur la personne, et non sur un groupe.</span><span class="sxs-lookup"><span data-stu-id="f6079-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="La divulgation est un exemple de meilleure pratique pour une application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="L'exemple montre les meilleures pratiques d'une application personnelle." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="f6079-196">Fonctionnalités d'application complexes</span><span class="sxs-lookup"><span data-stu-id="f6079-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="f6079-197">À faire : autoriser les utilisateurs à accéder à des fonctionnalités complexes dans un navigateur</span><span class="sxs-lookup"><span data-stu-id="f6079-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="f6079-198">Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l'application autonome complète dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="f6079-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="L'exemple montre les meilleures pratiques d'application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="f6079-200">À ne pas faire : inclure l'intégralité de votre application</span><span class="sxs-lookup"><span data-stu-id="f6079-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="f6079-201">Sauf si vous avez créé votre application spécifiquement pour Teams, vous disposez probablement de fonctionnalités qui n'ont pas de sens dans un outil de collaboration.</span><span class="sxs-lookup"><span data-stu-id="f6079-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="L'illustration fournit les meilleures pratiques d'application personnelles." border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="f6079-203">Gérer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="f6079-203">Manage a personal tab</span></span>

<span data-ttu-id="f6079-204">Sur le côté gauche de Teams, les utilisateurs peuvent cliquer avec le bouton droit sur l'application personnelle pour épingler, supprimer et configurer d'autres options d'application.</span><span class="sxs-lookup"><span data-stu-id="f6079-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="L'exemple montre les options de gestion d'une application personnelle." border="false":::

## <a name="learn-more"></a><span data-ttu-id="f6079-206">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="f6079-206">Learn more</span></span>

<span data-ttu-id="f6079-207">Ces autres recommandations de conception peuvent vous aider en fonction de l'étendue de votre application personnelle :</span><span class="sxs-lookup"><span data-stu-id="f6079-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="f6079-208">Conception de votre onglet</span><span class="sxs-lookup"><span data-stu-id="f6079-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="f6079-209">Conception de votre bot</span><span class="sxs-lookup"><span data-stu-id="f6079-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="f6079-210">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="f6079-210">Validate your design</span></span>

<span data-ttu-id="f6079-211">Si vous envisagez de publier votre application sur AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l'échec des applications lors de l'envoi.</span><span class="sxs-lookup"><span data-stu-id="f6079-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6079-212">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="f6079-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
