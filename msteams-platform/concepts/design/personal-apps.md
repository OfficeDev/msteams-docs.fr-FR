---
title: Conception de votre application personnelle
description: Découvrez comment concevoir une application Teams et obtenir le kit Microsoft Teams’interface utilisateur.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 83fad746d71dd196f6efa6526f5c6c28ceac9e20
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644888"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="4f8a9-103">Conception de votre application personnelle pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4f8a9-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="4f8a9-104">Une application personnelle peut être un bot, un espace de travail privé ou les deux.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="4f8a9-105">Parfois, il fonctionne comme un endroit pour créer ou afficher du contenu, d’autres fois il offre à l’utilisateur une vue d’ensemble de tout ce qui lui est propre lorsque l’application a été configurée sous la forme d’un onglet dans plusieurs canaux.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="4f8a9-106">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des applications personnelles dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4f8a9-107">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4f8a9-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4f8a9-108">Vous trouverez des instructions complètes sur la conception d’applications personnelles, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le kit Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="4f8a9-109">Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le resserrement réactif qui ne sont pas abordés ici.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f8a9-110">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="4f8a9-111">Ajouter une application personnelle</span><span class="sxs-lookup"><span data-stu-id="4f8a9-111">Add a personal app</span></span>

<span data-ttu-id="4f8a9-112">Vous pouvez ajouter une application personnelle à partir du Teams store (AppSource)  ou du flyout de l’application en sélectionnant l’icône Plus sur le côté gauche de Teams (illustré dans l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="4f8a9-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="L’exemple montre comment ajouter une application personnelle à partir du flyout de l’application." border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="4f8a9-114">Utiliser une application personnelle (espace de travail privé)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="4f8a9-115">Avec un espace de travail privé, vous pouvez afficher du contenu d’application qui vous semble significatif dans un emplacement central sans quitter Teams.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="4f8a9-116">(Remarque d’implémentation : l’espace de travail privé est basé sur la [*fonctionnalité d’onglet*](../../build-your-first-app/build-personal-tab.md) personnel.)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="4f8a9-117">Anatomie : application personnelle (espace de travail privé)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-117">Anatomy: Personal app (private workspace)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4f8a9-118">Desktop</span><span class="sxs-lookup"><span data-stu-id="4f8a9-118">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="L’exemple montre l’anatomie des composants de l’onglet personnel." border="false":::

|<span data-ttu-id="4f8a9-120">Compteur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-120">Counter</span></span>|<span data-ttu-id="4f8a9-121">Description</span><span class="sxs-lookup"><span data-stu-id="4f8a9-121">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4f8a9-122">A</span><span class="sxs-lookup"><span data-stu-id="4f8a9-122">A</span></span>|<span data-ttu-id="4f8a9-123">**Attribution de l’application**: nom et logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-123">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="4f8a9-124">B</span><span class="sxs-lookup"><span data-stu-id="4f8a9-124">B</span></span>|<span data-ttu-id="4f8a9-125">**Onglets :** fournit la navigation pour votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-125">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="4f8a9-126">C</span><span class="sxs-lookup"><span data-stu-id="4f8a9-126">C</span></span>|<span data-ttu-id="4f8a9-127">**Affichage popout :** pousse le contenu de votre application d’une fenêtre parent vers une fenêtre enfant autonome.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="4f8a9-128">D</span><span class="sxs-lookup"><span data-stu-id="4f8a9-128">D</span></span>|<span data-ttu-id="4f8a9-129">**Menu supplémentaire**: inclut des informations et options d’application supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-129">**More menu**: Includes additional app options and information.</span></span> <span data-ttu-id="4f8a9-130">(Vous pouvez également Paramètres **un** onglet.)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle de l’onglet personnel." border="false":::

|<span data-ttu-id="4f8a9-132">Compteur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-132">Counter</span></span>|<span data-ttu-id="4f8a9-133">Description</span><span class="sxs-lookup"><span data-stu-id="4f8a9-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4f8a9-134">A</span><span class="sxs-lookup"><span data-stu-id="4f8a9-134">A</span></span>|<span data-ttu-id="4f8a9-135">**Onglets :** fournit la navigation pour votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="4f8a9-136">1</span><span class="sxs-lookup"><span data-stu-id="4f8a9-136">1</span></span>|<span data-ttu-id="4f8a9-137">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-137">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="4f8a9-138">Mobile</span><span class="sxs-lookup"><span data-stu-id="4f8a9-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="L’exemple montre l’anatomie des composants de l’onglet personnel." border="false":::

|<span data-ttu-id="4f8a9-140">Compteur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-140">Counter</span></span>|<span data-ttu-id="4f8a9-141">Description</span><span class="sxs-lookup"><span data-stu-id="4f8a9-141">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4f8a9-142">A</span><span class="sxs-lookup"><span data-stu-id="4f8a9-142">A</span></span>|<span data-ttu-id="4f8a9-143">**Attribution de l’application**: nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-143">**App attribution**: Your app name.</span></span>|
|<span data-ttu-id="4f8a9-144">B</span><span class="sxs-lookup"><span data-stu-id="4f8a9-144">B</span></span>|<span data-ttu-id="4f8a9-145">**Onglets :** fournit la navigation pour votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-145">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="4f8a9-146">C</span><span class="sxs-lookup"><span data-stu-id="4f8a9-146">C</span></span>|<span data-ttu-id="4f8a9-147">**Menu supplémentaire**: inclut des informations et options d’application supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-147">**More menu**: Includes additional app options and information.</span></span>|
|<span data-ttu-id="4f8a9-148">D</span><span class="sxs-lookup"><span data-stu-id="4f8a9-148">D</span></span>|<span data-ttu-id="4f8a9-149">**Navigation principale**: fournit la navigation vers les autres fonctionnalités principales Teams votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-149">**Primary navigation**: Provides navigation to your app other main Teams features.</span></span>|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle de l’onglet personnel." border="false":::

|<span data-ttu-id="4f8a9-151">Compteur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-151">Counter</span></span>|<span data-ttu-id="4f8a9-152">Description</span><span class="sxs-lookup"><span data-stu-id="4f8a9-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4f8a9-153">A</span><span class="sxs-lookup"><span data-stu-id="4f8a9-153">A</span></span>|<span data-ttu-id="4f8a9-154">**Onglets :** fournit la navigation pour votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-154">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="4f8a9-155">1</span><span class="sxs-lookup"><span data-stu-id="4f8a9-155">1</span></span>|<span data-ttu-id="4f8a9-156">**webview**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-156">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a><span data-ttu-id="4f8a9-157">Conception avec des modèles d’interface utilisateur et des composants avancés</span><span class="sxs-lookup"><span data-stu-id="4f8a9-157">Designing with UI templates and advanced components</span></span>

<span data-ttu-id="4f8a9-158">Utilisez l’un des Teams et composants suivants pour vous aider à concevoir votre onglet personnel :</span><span class="sxs-lookup"><span data-stu-id="4f8a9-158">Use one of the following Teams templates and components to help design your personal tab:</span></span>

* <span data-ttu-id="4f8a9-159">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-159">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="4f8a9-160">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-160">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="4f8a9-161">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-161">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="4f8a9-162">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-162">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="4f8a9-163">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-163">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="4f8a9-164">[Navigation gauche](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): le composant de navigation gauche peut vous aider si votre application personnelle nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-164">[Left nav](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your personal app requires some navigation.</span></span> <span data-ttu-id="4f8a9-165">En règle générale, vous devez conserver la navigation au minimum.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-165">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="4f8a9-166">Utiliser une application personnelle (bot)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-166">Use a personal app (bot)</span></span>

<span data-ttu-id="4f8a9-167">Les applications personnelles peuvent inclure un bot pour les conversations un-à-un et des notifications privées (par exemple, lorsqu’un collègue publie un commentaire sur votre tableau de bord).</span><span class="sxs-lookup"><span data-stu-id="4f8a9-167">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="4f8a9-168">Le bot est disponible dans un onglet que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-168">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="4f8a9-169">Anatomie : application personnelle (bot)</span><span class="sxs-lookup"><span data-stu-id="4f8a9-169">Anatomy: Personal app (bot)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4f8a9-170">Desktop</span><span class="sxs-lookup"><span data-stu-id="4f8a9-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="L’exemple montre l’anatomie des composants personnels du bot." border="false":::

|<span data-ttu-id="4f8a9-172">Compteur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-172">Counter</span></span>|<span data-ttu-id="4f8a9-173">Description</span><span class="sxs-lookup"><span data-stu-id="4f8a9-173">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4f8a9-174">A</span><span class="sxs-lookup"><span data-stu-id="4f8a9-174">A</span></span>|<span data-ttu-id="4f8a9-175">**Onglet Bot**: par exemple, incluez un onglet **Conversation** pour accéder aux conversations et notifications du bot.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-175">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="4f8a9-176">B</span><span class="sxs-lookup"><span data-stu-id="4f8a9-176">B</span></span>|<span data-ttu-id="4f8a9-177">**Message du bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).</span><span class="sxs-lookup"><span data-stu-id="4f8a9-177">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="4f8a9-178">C</span><span class="sxs-lookup"><span data-stu-id="4f8a9-178">C</span></span>|<span data-ttu-id="4f8a9-179">**Zone de composition**: champ d’entrée pour l’envoi de messages au bot.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-179">**Compose box**: Input field for sending messages to the bot.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="4f8a9-180">Mobile</span><span class="sxs-lookup"><span data-stu-id="4f8a9-180">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="L’exemple montre l’anatomie des composants personnels du bot." border="false":::

|<span data-ttu-id="4f8a9-182">Compteur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-182">Counter</span></span>|<span data-ttu-id="4f8a9-183">Description</span><span class="sxs-lookup"><span data-stu-id="4f8a9-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4f8a9-184">A</span><span class="sxs-lookup"><span data-stu-id="4f8a9-184">A</span></span>|<span data-ttu-id="4f8a9-185">**Point d’entrée du bot**: point d’entrée pour que les utilisateurs accèdent à la fonctionnalité bot dans votre application personnelle.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-185">**Bot entry point**: Entry point for users to access the bot feature in your personal app.</span></span>|
|<span data-ttu-id="4f8a9-186">B</span><span class="sxs-lookup"><span data-stu-id="4f8a9-186">B</span></span>|<span data-ttu-id="4f8a9-187">**Bouton Retour :** permet aux utilisateurs de revenir à l’espace de travail privé.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-187">**Back button**: Takes users back to the private workspace.</span></span>|
|<span data-ttu-id="4f8a9-188">C</span><span class="sxs-lookup"><span data-stu-id="4f8a9-188">C</span></span>|<span data-ttu-id="4f8a9-189">**Message du bot**: les bots envoient souvent des messages et des notifications sous la forme d’une carte (par exemple, une carte adaptative).</span><span class="sxs-lookup"><span data-stu-id="4f8a9-189">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="4f8a9-190">D</span><span class="sxs-lookup"><span data-stu-id="4f8a9-190">D</span></span>|<span data-ttu-id="4f8a9-191">**Zone de composition**: champ d’entrée pour l’envoi de messages au bot.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-191">**Compose box**: Input field for sending messages to the bot.</span></span>|

---

## <a name="manage-a-personal-tab"></a><span data-ttu-id="4f8a9-192">Gérer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="4f8a9-192">Manage a personal tab</span></span>

<span data-ttu-id="4f8a9-193">Sur le côté gauche du Teams, les utilisateurs peuvent cliquer avec le bouton droit sur l’application personnelle pour épingler, supprimer et configurer d’autres options d’application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-193">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="L’exemple montre les options de gestion d’une application personnelle." border="false":::

## <a name="best-practices"></a><span data-ttu-id="4f8a9-195">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="4f8a9-195">Best practices</span></span>

<span data-ttu-id="4f8a9-196">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-196">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="4f8a9-197">Priorité de l’onglet</span><span class="sxs-lookup"><span data-stu-id="4f8a9-197">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="4f8a9-198">À faire : afficher le contenu le plus pertinent dans le premier onglet</span><span class="sxs-lookup"><span data-stu-id="4f8a9-198">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="4f8a9-199">Avec le resserré réactif, les onglets de droite peuvent être tronqués ou en dehors de la vue.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-199">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="L’exemple montre une application personnelle affichant le contenu le plus pertinent dans le premier onglet." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="4f8a9-201">À ne pas faire : diriger avec du contenu ou des métadonnées secondaires</span><span class="sxs-lookup"><span data-stu-id="4f8a9-201">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="4f8a9-202">À l’exemple d’une application web standard, la navigation par onglets doit s’effectuer dans un ordre qui vous aide à prendre en compte les principales fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-202">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="L’exemple montre une application personnelle en tête avec du contenu ou des métadonnées secondaires." border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="4f8a9-204">Hiérarchie d’onglets</span><span class="sxs-lookup"><span data-stu-id="4f8a9-204">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="4f8a9-205">À faire : les onglets doivent être de hiérarchie égale et représenter des pages d’application clés</span><span class="sxs-lookup"><span data-stu-id="4f8a9-205">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="4f8a9-206">Vos onglets doivent catégoriser les principales fonctionnalités et le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-206">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="4f8a9-207">Avec le resserré réactif, le contenu à droite peut être tronqué ou hors de vue.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-207">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="L’exemple montre une application personnelle avec des onglets de hiérarchie égale." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="4f8a9-209">À ne pas faire : inclure différents niveaux de hiérarchie</span><span class="sxs-lookup"><span data-stu-id="4f8a9-209">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="4f8a9-210">Votre contenu doit évoluer dans un ordre logique qui aide les utilisateurs à le comprendre.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-210">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="4f8a9-211">Si vous avez deux onglets qui sont étroitement liés, envisagez de les combiner en un seul onglet.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-211">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="L’exemple montre une application personnelle avec différents niveaux de hiérarchie." border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="4f8a9-213">Première expérience d’utilisation</span><span class="sxs-lookup"><span data-stu-id="4f8a9-213">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="4f8a9-214">À faire : inclure une expérience de première expérience</span><span class="sxs-lookup"><span data-stu-id="4f8a9-214">Do: Include a first-run experience</span></span>

<span data-ttu-id="4f8a9-215">Il doit y avoir au moins un écran d’accueil la première fois que vous utilisez une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-215">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="4f8a9-216">Pour les bots, décrivez ce que votre bot peut faire et fournissez des actions rapides, telles qu’un bouton de sign-in.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-216">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="L’exemple montre comment faire lors de la première expérience de première application personnelle." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Un autre exemple montre comment faire lors de la première expérience de première application personnelle." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="4f8a9-219">À ne pas faire : démarrer avec un écran vide</span><span class="sxs-lookup"><span data-stu-id="4f8a9-219">Don't: Start with a blank screen</span></span>

<span data-ttu-id="4f8a9-220">Les utilisateurs peuvent être confondus si rien ne s’affiche la première fois qu’ils exécutent votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-220">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire lors de la première expérience de première application personnelle." border="false":::

### <a name="personalized-content"></a><span data-ttu-id="4f8a9-222">Contenu personnalisé</span><span class="sxs-lookup"><span data-stu-id="4f8a9-222">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="4f8a9-223">À faire : agréger le contenu d’application pertinent pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-223">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="4f8a9-224">Qu’il s’agit d’un onglet personnel ou d’un bot, affichez le contenu lié uniquement à l’activité d’un utilisateur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-224">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="L’exemple montre comment faire avec une application personnelle et du contenu personnalisé." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Un autre exemple montre comment faire avec une application personnelle et du contenu personnalisé." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="4f8a9-227">À ne pas faire : afficher du contenu non lié ou trop large</span><span class="sxs-lookup"><span data-stu-id="4f8a9-227">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="4f8a9-228">Dans les contextes personnels, n’affichez pas de contenu pour les équipes dont un utilisateur ne fait pas partie.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-228">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="4f8a9-229">Le contenu du bot personnel doit se concentrer sur la personne, et non sur un groupe.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-229">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Un autre exemple montre ce qu’il ne faut pas faire avec une application personnelle et du contenu personnalisé." border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="4f8a9-232">Fonctionnalités d’application complexes</span><span class="sxs-lookup"><span data-stu-id="4f8a9-232">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="4f8a9-233">À faire : autoriser les utilisateurs à accéder à des fonctionnalités complexes dans un navigateur</span><span class="sxs-lookup"><span data-stu-id="4f8a9-233">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="4f8a9-234">Votre application doit se concentrer sur les tâches principales dans Teams, mais vous pouvez toujours afficher l’application autonome complète dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-234">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="L’exemple montre comment gérer des fonctionnalités d’application complexes avec une application personnelle." border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="4f8a9-236">À ne pas faire : inclure l’intégralité de votre application</span><span class="sxs-lookup"><span data-stu-id="4f8a9-236">Don’t: Include your entire app</span></span>

<span data-ttu-id="4f8a9-237">Sauf si vous avez créé votre application spécifiquement Teams, vous disposez probablement de fonctionnalités qui n’ont pas de sens dans un outil de collaboration.</span><span class="sxs-lookup"><span data-stu-id="4f8a9-237">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="L’exemple montre comment ne pas gérer des fonctionnalités d’application complexes avec une application personnelle." border="false":::

## <a name="see-also"></a><span data-ttu-id="4f8a9-239">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4f8a9-239">See also</span></span>

<span data-ttu-id="4f8a9-240">Ces autres recommandations de conception peuvent vous aider en fonction de l’étendue de votre application personnelle :</span><span class="sxs-lookup"><span data-stu-id="4f8a9-240">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="4f8a9-241">Conception de votre onglet</span><span class="sxs-lookup"><span data-stu-id="4f8a9-241">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="4f8a9-242">Conception de votre bot</span><span class="sxs-lookup"><span data-stu-id="4f8a9-242">Designing you bot</span></span>](../../bots/design/bots.md)
