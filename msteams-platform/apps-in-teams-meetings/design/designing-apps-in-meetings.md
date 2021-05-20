---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans le Teams et obtenir le kit d’interface Microsoft Teams’interface utilisateur.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566025"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="6133a-103">Concevoir votre extension Microsoft Teams réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="6133a-104">Vous pouvez créer des applications pour rendre les réunions plus productives.</span><span class="sxs-lookup"><span data-stu-id="6133a-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="6133a-105">Par exemple, demandez aux gens de remplir un sondage lors d’un appel ou d’envoyer un rappel rapide qui n’interrompt pas le déroulement de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="6133a-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6133a-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="6133a-107">Vous pouvez trouver des lignes directrices de conception plus complètes, y compris des éléments que vous pouvez saisir et modifier au besoin, dans le kit d Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6133a-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6133a-108">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="6133a-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="6133a-109">Ajouter une extension de réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-109">Add a meeting extension</span></span>

<span data-ttu-id="6133a-110">Vous pouvez ajouter une extension de réunion avant et pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="6133a-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="6133a-111">Vous pouvez également ajouter une application pour une réunion spécifique directement à partir du Teams store (AppSource).</span><span class="sxs-lookup"><span data-stu-id="6133a-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="6133a-112">Ajouter avant une réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-112">Add before a meeting</span></span>

<span data-ttu-id="6133a-113">Dans les détails de la réunion, **sélectionnez Ajouter un onglet +** pour ouvrir le flyout de l’application et trouver des applications optimisées pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="6133a-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="6133a-115">Ajouter lors d’une réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-115">Add during a meeting</span></span>

Lors d’une réunion, **sélectionnez** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Ajouter une application et** choisissez l’application que vous souhaitez.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion lors d’une réunion." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="6133a-118">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-118">Before a meeting</span></span>

<span data-ttu-id="6133a-119">Avant votre réunion, vous pouvez ajouter du contenu dans l’onglet. L’exemple suivant montre un projet de question de sondage à laquelle les gens répondront pendant l’appel.</span><span class="sxs-lookup"><span data-stu-id="6133a-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Exemple montre comment app contenu dans les détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="6133a-121">Anatomie: Onglet Réunion (avant et après les réunions)</span><span class="sxs-lookup"><span data-stu-id="6133a-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Exemple montre l’anatomie structurale d’un onglet de réunion avant et après une réunion." border="false":::

|<span data-ttu-id="6133a-123">Compteur</span><span class="sxs-lookup"><span data-stu-id="6133a-123">Counter</span></span>|<span data-ttu-id="6133a-124">Description</span><span class="sxs-lookup"><span data-stu-id="6133a-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="6133a-125">1</span><span class="sxs-lookup"><span data-stu-id="6133a-125">1</span></span>|<span data-ttu-id="6133a-126">**Nom de l’onglet**: Étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="6133a-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="6133a-127">2</span><span class="sxs-lookup"><span data-stu-id="6133a-127">2</span></span>|<span data-ttu-id="6133a-128">**Débordement d’onglets**: Ouvre les actions de l’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="6133a-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="6133a-129">3</span><span class="sxs-lookup"><span data-stu-id="6133a-129">3</span></span>|<span data-ttu-id="6133a-130">**iframe**: Affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="6133a-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="6133a-131">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="6133a-131">Designing with UI templates</span></span>

<span data-ttu-id="6133a-132">Utilisez l’un des modèles d Teams d’interface utilisateur suivants pour aider à concevoir votre onglet réunion :</span><span class="sxs-lookup"><span data-stu-id="6133a-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="6133a-133">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): Les listes peuvent afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="6133a-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="6133a-134">[Tableau de travail](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tableau de travail, parfois appelé planche kanban ou pistes de natation, est une collection de cartes souvent utilisées pour suivre l’état des articles de travail ou des billets.</span><span class="sxs-lookup"><span data-stu-id="6133a-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="6133a-135">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : Un tableau de bord est une toile contenant plusieurs cartes qui donnent un aperçu des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="6133a-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="6133a-136">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): Les formulaires sont pour la collecte, la validation et la soumission structurée des entrées de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6133a-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="6133a-137">[État vide :](../../concepts/design/design-teams-app-ui-templates.md#empty-state)Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="6133a-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="6133a-138">[Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)Le modèle de navigation gauche peut vous aider si votre onglet nécessite une certaine navigation.</span><span class="sxs-lookup"><span data-stu-id="6133a-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="6133a-139">En général, vous devez garder un œil sur la navigation au minimum.</span><span class="sxs-lookup"><span data-stu-id="6133a-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="6133a-140">Utiliser un onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-140">Use an in-meeting tab</span></span>

<span data-ttu-id="6133a-141">L’onglet en réunion est une toile pour augmenter la collaboration pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="6133a-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="6133a-142">Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de l’étape de la réunion grâce à des vues partagées ou basées sur des rôle.</span><span class="sxs-lookup"><span data-stu-id="6133a-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="6133a-143">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="6133a-143">Use cases</span></span>

<span data-ttu-id="6133a-144">Les gens peuvent utiliser l’onglet en réunion pour :</span><span class="sxs-lookup"><span data-stu-id="6133a-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="6133a-145">Fournir une rétroaction détaillée.</span><span class="sxs-lookup"><span data-stu-id="6133a-145">Provide detailed feedback.</span></span> <span data-ttu-id="6133a-146">Par exemple, évaluez un candidat à un emploi.</span><span class="sxs-lookup"><span data-stu-id="6133a-146">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="6133a-147">Créez un sondage, un sondage ou un élément de tâche pour les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-147">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="6133a-148">Affichez les notes pertinentes à la réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-148">Display notes relevant to the meeting.</span></span> <span data-ttu-id="6133a-149">Par exemple, des informations sur un responsable commercial.</span><span class="sxs-lookup"><span data-stu-id="6133a-149">For example, information about a sales lead.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Exemple montre comment vous pouvez présenter le contenu du sondage dans un onglet en réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="6133a-151">Anatomie: Onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-151">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Exemple montre l’anatomie structurale d’un onglet en réunion." border="false":::

|<span data-ttu-id="6133a-153">Compteur</span><span class="sxs-lookup"><span data-stu-id="6133a-153">Counter</span></span>|<span data-ttu-id="6133a-154">Description</span><span class="sxs-lookup"><span data-stu-id="6133a-154">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="6133a-155">1</span><span class="sxs-lookup"><span data-stu-id="6133a-155">1</span></span>|<span data-ttu-id="6133a-156">**Icône de l’application (sélectionnée)**: logo transparent de l’application de 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="6133a-156">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="6133a-157">2</span><span class="sxs-lookup"><span data-stu-id="6133a-157">2</span></span>|<span data-ttu-id="6133a-158">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="6133a-158">**App name**</span></span>|
|<span data-ttu-id="6133a-159">3</span><span class="sxs-lookup"><span data-stu-id="6133a-159">3</span></span>|<span data-ttu-id="6133a-160">**En-tête**: Inclut le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="6133a-160">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="6133a-161">4 </span><span class="sxs-lookup"><span data-stu-id="6133a-161">4</span></span>|<span data-ttu-id="6133a-162">**Bouton fermer**: Rejette l’onglet. Utilisez toujours l’icône de fermeture supérieure-droite au lieu d’une action dans le pied.</span><span class="sxs-lookup"><span data-stu-id="6133a-162">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="6133a-163">5 </span><span class="sxs-lookup"><span data-stu-id="6133a-163">5</span></span>|<span data-ttu-id="6133a-164">**Barre de notification**: Les alertes d’erreur s’affichent directement sous l’en-tête et font baisser le contenu de l’iframe de 20 pixels.</span><span class="sxs-lookup"><span data-stu-id="6133a-164">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="6133a-165">6 </span><span class="sxs-lookup"><span data-stu-id="6133a-165">6</span></span>|<span data-ttu-id="6133a-166">**iframe**: Affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="6133a-166">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="6133a-167">Espacement</span><span class="sxs-lookup"><span data-stu-id="6133a-167">Spacing</span></span>

<span data-ttu-id="6133a-168">Optimisez votre onglet en réunion pour vous adapter de bord en bord dans la zone iframe de 280 pixels de large.</span><span class="sxs-lookup"><span data-stu-id="6133a-168">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="6133a-169">Il y a 20 pixels de rembourrage sur les côtés gauche et droit de l’iframe et entre l’en-tête de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="6133a-169">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="6133a-170">L’iframe est saigné au fond de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="6133a-170">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Exemple montre les dimensions d’espacement des onglets en réunion." border="false":::

### <a name="scrolling"></a><span data-ttu-id="6133a-172">défilement</span><span class="sxs-lookup"><span data-stu-id="6133a-172">Scrolling</span></span>

<span data-ttu-id="6133a-173">Le contenu iframe doit défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="6133a-173">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="6133a-174">Vous ne pouvez voir que le contenu sur quoi vous avez fait défiler (rien au-dessus ou au-dessous).</span><span class="sxs-lookup"><span data-stu-id="6133a-174">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="6133a-175">La barre de défilement fait partie du contenu iframe.</span><span class="sxs-lookup"><span data-stu-id="6133a-175">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Exemple montre comment l’onglet en réunion défile." border="false":::

### <a name="navigation"></a><span data-ttu-id="6133a-177">Navigation</span><span class="sxs-lookup"><span data-stu-id="6133a-177">Navigation</span></span>

<span data-ttu-id="6133a-178">Pour les scénarios avec des couches de navigation ou un contenu lourd, nous vous recommandons de permettre aux utilisateurs de naviguer vers une couche secondaire.</span><span class="sxs-lookup"><span data-stu-id="6133a-178">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="6133a-179">Les utilisateurs doivent pouvoir revenir à la couche précédente.</span><span class="sxs-lookup"><span data-stu-id="6133a-179">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple montre la navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="6133a-181">Utiliser un dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-181">Use an in-meeting dialog</span></span>

<span data-ttu-id="6133a-182">Les dialogues en réunion s’affichent sur Teams étape de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-182">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="6133a-183">Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont subtils et n’interrompent pas la réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-183">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="6133a-184">Vous devez les utiliser avec parcimonie et pour des scénarios qui sont légers et axés sur les tâches.</span><span class="sxs-lookup"><span data-stu-id="6133a-184">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="6133a-185">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="6133a-185">Use cases</span></span>

<span data-ttu-id="6133a-186">Les dialogues en réunion sont déclenchés par un utilisateur (tel que l’organisateur de la réunion) qui peut vouloir que les participants :</span><span class="sxs-lookup"><span data-stu-id="6133a-186">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="6133a-187">Fournir de brèves commentaires</span><span class="sxs-lookup"><span data-stu-id="6133a-187">Provide brief feedback</span></span>
* <span data-ttu-id="6133a-188">Faites un court sondage ou un sondage</span><span class="sxs-lookup"><span data-stu-id="6133a-188">Take a short survey or poll</span></span>
* <span data-ttu-id="6133a-189">Soumettre les approbations</span><span class="sxs-lookup"><span data-stu-id="6133a-189">Submit approvals</span></span>
* <span data-ttu-id="6133a-190">Obtenez des rappels</span><span class="sxs-lookup"><span data-stu-id="6133a-190">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Exemple montre comment vous pouvez utiliser un dialogue en réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="6133a-192">Anatomie: Dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-192">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Exemple montre l’anatomie structurelle d’un dialogue en réunion." border="false":::

|<span data-ttu-id="6133a-194">Compteur</span><span class="sxs-lookup"><span data-stu-id="6133a-194">Counter</span></span>|<span data-ttu-id="6133a-195">Description</span><span class="sxs-lookup"><span data-stu-id="6133a-195">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="6133a-196">1</span><span class="sxs-lookup"><span data-stu-id="6133a-196">1</span></span>|<span data-ttu-id="6133a-197">**En-tête**: Inclut l’icône d’application, le nom, la chaîne d’action et l’icône proche.</span><span class="sxs-lookup"><span data-stu-id="6133a-197">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="6133a-198">2</span><span class="sxs-lookup"><span data-stu-id="6133a-198">2</span></span>|<span data-ttu-id="6133a-199">**iframe**: Affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="6133a-199">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="6133a-200">Anatomie : En-tête de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-200">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Exemple montre l’anatomie structurale d’un en-tête de dialogue en réunion." border="false":::

<span data-ttu-id="6133a-202">Il existe deux variantes d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="6133a-202">There are two header variants.</span></span> <span data-ttu-id="6133a-203">Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer que le dialogue vient d’une personne.</span><span class="sxs-lookup"><span data-stu-id="6133a-203">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="6133a-204">Compteur</span><span class="sxs-lookup"><span data-stu-id="6133a-204">Counter</span></span>|<span data-ttu-id="6133a-205">Description</span><span class="sxs-lookup"><span data-stu-id="6133a-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="6133a-206">1</span><span class="sxs-lookup"><span data-stu-id="6133a-206">1</span></span>|<span data-ttu-id="6133a-207">**Avatar**: Personne qui initie le dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-207">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="6133a-208">2</span><span class="sxs-lookup"><span data-stu-id="6133a-208">2</span></span>|<span data-ttu-id="6133a-209">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="6133a-209">**App icon**</span></span>|
|<span data-ttu-id="6133a-210">3</span><span class="sxs-lookup"><span data-stu-id="6133a-210">3</span></span>|<span data-ttu-id="6133a-211">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="6133a-211">**App name**</span></span>|
|<span data-ttu-id="6133a-212">4 </span><span class="sxs-lookup"><span data-stu-id="6133a-212">4</span></span>|<span data-ttu-id="6133a-213">**Bouton fermer**: Rejette le dialogue.</span><span class="sxs-lookup"><span data-stu-id="6133a-213">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="6133a-214">5 </span><span class="sxs-lookup"><span data-stu-id="6133a-214">5</span></span>|<span data-ttu-id="6133a-215">**Chaîne d’action**: Décrit généralement qui a initié le dialogue.</span><span class="sxs-lookup"><span data-stu-id="6133a-215">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="6133a-216">Comportement réactif</span><span class="sxs-lookup"><span data-stu-id="6133a-216">Responsive behavior</span></span>

<span data-ttu-id="6133a-217">Les dialogues en réunion peuvent varier en taille pour tenir compte de différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="6133a-217">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="6133a-218">Assurez-vous de maintenir le rembourrage et la taille des composants.</span><span class="sxs-lookup"><span data-stu-id="6133a-218">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="6133a-219">**Largeur**: Vous pouvez spécifier la largeur de l’iframe du dialogue n’importe où dans la plage de taille prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6133a-219">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="6133a-220">**Hauteur**: Vous pouvez spécifier la hauteur de l’iframe du dialogue n’importe où dans la plage de taille prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6133a-220">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="6133a-221">Vous pouvez également permettre aux utilisateurs de faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.</span><span class="sxs-lookup"><span data-stu-id="6133a-221">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="6133a-222">Pour implémenter, spécifiez la largeur et la hauteur à l’aide de [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) la clé.</span><span class="sxs-lookup"><span data-stu-id="6133a-222">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple montre le dialogue en réunion. Largeur: Min--280 pixels (248 pixels iframe). Max---460 pixels (428 pixels iframe). Hauteur: 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="6133a-224">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-224">After a meeting</span></span>

<span data-ttu-id="6133a-225">Vous pouvez revenir à une réunion après sa fin et afficher le contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="6133a-225">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="6133a-226">Dans cet exemple, l’organisateur de la réunion peut examiner les résultats du sondage dans **l’onglet Contoso.** (Note : Du point de vue de la conception, il n’y a pas de différence entre l’expérience de l’onglet avant et après la réunion.)</span><span class="sxs-lookup"><span data-stu-id="6133a-226">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="Exemple d’illustration montre un onglet post-réunion." border="false":::

## <a name="best-practices"></a><span data-ttu-id="6133a-228">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="6133a-228">Best practices</span></span>

<span data-ttu-id="6133a-229">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="6133a-229">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="6133a-230">Interactions</span><span class="sxs-lookup"><span data-stu-id="6133a-230">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d’interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="6133a-232">Faire : Limiter le nombre d’interactions</span><span class="sxs-lookup"><span data-stu-id="6133a-232">Do: Limit the number of interactions</span></span>

<span data-ttu-id="6133a-233">Pour les dialogues en réunion, supprimez le contenu inutile qui n’aide pas les utilisateurs à accomplir quelque chose rapidement.</span><span class="sxs-lookup"><span data-stu-id="6133a-233">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d’éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="6133a-235">Ne pas : Introduire des éléments inutiles</span><span class="sxs-lookup"><span data-stu-id="6133a-235">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="6133a-236">Un seul dialogue en réunion avec plusieurs interactions peut détourner l’attention de l’appel.</span><span class="sxs-lookup"><span data-stu-id="6133a-236">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="6133a-237">Disposition</span><span class="sxs-lookup"><span data-stu-id="6133a-237">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment vous devez utiliser une mise en page de dialogue à colonne unique." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="6133a-239">Faire : Utiliser une mise en page de dialogue à colonne unique</span><span class="sxs-lookup"><span data-stu-id="6133a-239">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="6133a-240">Étant donné que les dialogues sont au centre de l’étape de la réunion, l’achèvement des tâches doit être rapide et simple pour éviter la frustration des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6133a-240">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devriez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="6133a-242">Ne pas : encombrer l’espace</span><span class="sxs-lookup"><span data-stu-id="6133a-242">Don't: Clutter the space</span></span>

<span data-ttu-id="6133a-243">Le contenu dense ou trop structuré peut être distrayant et accablant, surtout lors d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="6133a-243">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une mise en page d’onglet à colonne unique." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="6133a-245">Faire : Utilisez une mise en page d’onglet à colonne unique</span><span class="sxs-lookup"><span data-stu-id="6133a-245">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="6133a-246">Compte tenu de la nature étroite de l’onglet en réunion, nous vous recommandons fortement d’afficher le contenu dans une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="6133a-246">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="6133a-248">Ne pas : Utilisez plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="6133a-248">Don't: Use multiple columns</span></span>

<span data-ttu-id="6133a-249">En raison de l’espace limité de l’onglet en réunion, les dispositions avec plus d’une colonne ne sont pas recommandées.</span><span class="sxs-lookup"><span data-stu-id="6133a-249">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="6133a-250">Contrôles</span><span class="sxs-lookup"><span data-stu-id="6133a-250">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple montrant comment aligner à droite les contrôles primaires." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="6133a-252">Faire: Droit aligner l’action primaire</span><span class="sxs-lookup"><span data-stu-id="6133a-252">Do: Right align the primary action</span></span>

<span data-ttu-id="6133a-253">Nous vous recommandons de positionner l’action la plus lourde visuellement à l’endroit le plus approprié.</span><span class="sxs-lookup"><span data-stu-id="6133a-253">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment vous ne devriez pas laisser aligner les contrôles primaires." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="6133a-255">Ne pas : La gauche ou le centre alignent les actions</span><span class="sxs-lookup"><span data-stu-id="6133a-255">Don't: Left or center align actions</span></span>

<span data-ttu-id="6133a-256">Cela s’écarte de la norme Teams modèle de contrôle dans un dialogue et peut entrer en conflit avec un dialogue derrière le haut.</span><span class="sxs-lookup"><span data-stu-id="6133a-256">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="6133a-257">Faire défiler</span><span class="sxs-lookup"><span data-stu-id="6133a-257">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple montrant le défilement vertical dans un onglet en réunion." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="6133a-259">Faire: Faire défiler verticalement</span><span class="sxs-lookup"><span data-stu-id="6133a-259">Do: Scroll vertically</span></span>

<span data-ttu-id="6133a-260">Les utilisateurs s’attendent à un défilement vertical Teams (et ailleurs).</span><span class="sxs-lookup"><span data-stu-id="6133a-260">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple montrant le défilement horizontal dans un onglet en réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="6133a-262">Ne pas : Faites défiler horizontalement</span><span class="sxs-lookup"><span data-stu-id="6133a-262">Don't: Scroll horizontally</span></span>

<span data-ttu-id="6133a-263">Le défilement horizontal n’est pas un comportement attendu dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6133a-263">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="6133a-264">D’autres toiles de l’environnement de réunion défilent verticalement.</span><span class="sxs-lookup"><span data-stu-id="6133a-264">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="6133a-265">Flux de travail</span><span class="sxs-lookup"><span data-stu-id="6133a-265">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet en réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="6133a-267">Faire : Scénarios complexes de surface dans l’onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-267">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="6133a-268">Si votre application comprend plusieurs tâches, nous vous recommandons fortement d’utiliser un onglet en réunion avec une mise en page à colonne unique.</span><span class="sxs-lookup"><span data-stu-id="6133a-268">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple montrant des scénarios complexes dans un dialogue en réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="6133a-270">Ne pas : Rendre les dialogues en réunion complexes</span><span class="sxs-lookup"><span data-stu-id="6133a-270">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="6133a-271">Les dialogues en réunion sont destinés à de brèves interactions.</span><span class="sxs-lookup"><span data-stu-id="6133a-271">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="6133a-272">Thèmes</span><span class="sxs-lookup"><span data-stu-id="6133a-272">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème sombre." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="6133a-274">Faire: Utilisez Teams de couleur</span><span class="sxs-lookup"><span data-stu-id="6133a-274">Do: Use Teams color tokens</span></span>

<span data-ttu-id="6133a-275">Teams réunions sont optimisées pour le mode sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé.</span><span class="sxs-lookup"><span data-stu-id="6133a-275">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="6133a-276">En savoir plus sur <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">l’utilisation de jetons de couleur (interface utilisateur couramment)</a>.</span><span class="sxs-lookup"><span data-stu-id="6133a-276">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec un thème par défaut (lumière)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="6133a-278">Ne pas: Valeurs hex code dur</span><span class="sxs-lookup"><span data-stu-id="6133a-278">Don't: Hard code hex values</span></span>

<span data-ttu-id="6133a-279">Si vous n’utilisez pas Teams jetons de couleur, vos créations seront moins évolutives et prennent plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="6133a-279">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="6133a-280">Navigation</span><span class="sxs-lookup"><span data-stu-id="6133a-280">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton arrière." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="6133a-282">Faire: Avoir un bouton arrière</span><span class="sxs-lookup"><span data-stu-id="6133a-282">Do: Have a back button</span></span>

<span data-ttu-id="6133a-283">Si vous avez plus d’une couche de navigation dans un onglet en réunion, les utilisateurs doivent être en mesure de revenir à leurs vues précédentes.</span><span class="sxs-lookup"><span data-stu-id="6133a-283">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons de rejet." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="6133a-285">Ne pas: Inclure un autre bouton de rejet</span><span class="sxs-lookup"><span data-stu-id="6133a-285">Don't: Include another dismiss button</span></span>

<span data-ttu-id="6133a-286">Fournir une option pour fermer le contenu de l’onglet en réunion peut causer des problèmes car il ya déjà un bouton dans l’en-tête pour rejeter l’onglet en réunion lui-même.</span><span class="sxs-lookup"><span data-stu-id="6133a-286">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modalités (ou modules de tâches) dans un onglet en réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="6133a-288">Attention : Évitez les modalités dans l’onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="6133a-288">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="6133a-289">Les modules modaux (également connus sous le nom de modules de tâches) dans l’onglet en réunion déjà étroit peuvent envelopper et obscurcir le contenu.</span><span class="sxs-lookup"><span data-stu-id="6133a-289">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::
