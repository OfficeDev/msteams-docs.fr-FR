---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans les réunions Teams et obtenir le Kit d'interface utilisateur Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 022ffdd7341f60a9c6732948a0914383ddb248a8
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018473"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="00ce8-103">Conception de votre extension de réunion Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="00ce8-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="00ce8-104">Vous pouvez créer des applications pour rendre les réunions plus productives.</span><span class="sxs-lookup"><span data-stu-id="00ce8-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="00ce8-105">Par exemple, demandez aux personnes de répondre à une enquête pendant un appel ou d'envoyer un rappel rapide qui n'interrompt pas le flux de la réunion.</span><span class="sxs-lookup"><span data-stu-id="00ce8-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="00ce8-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="00ce8-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="00ce8-107">Vous trouverez des instructions de conception plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="00ce8-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00ce8-108">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="00ce8-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="00ce8-109">Ajouter une extension de réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-109">Add a meeting extension</span></span>

<span data-ttu-id="00ce8-110">Vous pouvez ajouter une extension de réunion avant et pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="00ce8-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="00ce8-111">Vous pouvez également ajouter une application pour une réunion spécifique directement à partir du magasin Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="00ce8-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="00ce8-112">Ajouter avant une réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-112">Add before a meeting</span></span>

<span data-ttu-id="00ce8-113">Dans les détails de la réunion, sélectionnez Ajouter un **onglet +** pour ouvrir le programme volant de l'application et rechercher les applications optimisées pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="00ce8-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="L'exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="00ce8-115">Ajouter au cours d'une réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-115">Add during a meeting</span></span>

Lors d'une réunion, **sélectionnez Ajouter** une :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **application** et choisissez l'application de votre choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="L'exemple montre comment ajouter une extension de réunion au cours d'une réunion." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="00ce8-118">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-118">Before a meeting</span></span>

<span data-ttu-id="00ce8-119">Avant votre réunion, vous pouvez ajouter du contenu dans l'onglet. L'exemple suivant montre un brouillon de question d'enquête à répondre pendant l'appel.</span><span class="sxs-lookup"><span data-stu-id="00ce8-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="L'exemple montre comment apper le contenu des détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="00ce8-121">Anatomie : onglet Réunion (avant et après les réunions)</span><span class="sxs-lookup"><span data-stu-id="00ce8-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="L'exemple illustre l'anatomie structurelle d'un onglet de réunion avant et après une réunion." border="false":::

|<span data-ttu-id="00ce8-123">Compteur</span><span class="sxs-lookup"><span data-stu-id="00ce8-123">Counter</span></span>|<span data-ttu-id="00ce8-124">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="00ce8-125">1</span><span class="sxs-lookup"><span data-stu-id="00ce8-125">1</span></span>|<span data-ttu-id="00ce8-126">**Nom de l'onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="00ce8-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="00ce8-127">2</span><span class="sxs-lookup"><span data-stu-id="00ce8-127">2</span></span>|<span data-ttu-id="00ce8-128">**Dépassement de tabulation**: ouvre les actions d'onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="00ce8-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="00ce8-129">3</span><span class="sxs-lookup"><span data-stu-id="00ce8-129">3</span></span>|<span data-ttu-id="00ce8-130">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="00ce8-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="00ce8-131">Conception avec des modèles d'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="00ce8-131">Designing with UI templates</span></span>

<span data-ttu-id="00ce8-132">Utilisez l'un des modèles d'interface utilisateur Teams suivants pour vous aider à concevoir votre onglet de réunion :</span><span class="sxs-lookup"><span data-stu-id="00ce8-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="00ce8-133">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="00ce8-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="00ce8-134">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l'état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="00ce8-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="00ce8-135">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d'ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="00ce8-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="00ce8-136">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="00ce8-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="00ce8-137">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="00ce8-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="00ce8-138">[Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="00ce8-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="00ce8-139">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="00ce8-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="00ce8-140">Utiliser un onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-140">Use an in-meeting tab</span></span>

<span data-ttu-id="00ce8-141">L'onglet de réunion est un canevas qui permet d'accroître la collaboration pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="00ce8-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="00ce8-142">Les participants peuvent voir et interagir avec le contenu de l'application dans un espace dédié en dehors de la phase de réunion par le biais d'affichages partagés ou basés sur des rôles.</span><span class="sxs-lookup"><span data-stu-id="00ce8-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="00ce8-143">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="00ce8-143">Use cases</span></span>

<span data-ttu-id="00ce8-144">Les personnes peuvent utiliser l'onglet réunion pour :</span><span class="sxs-lookup"><span data-stu-id="00ce8-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="00ce8-145">Fournir des commentaires détaillés (par exemple, évaluer un candidat au poste)</span><span class="sxs-lookup"><span data-stu-id="00ce8-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="00ce8-146">Créer rapidement un sondage, une enquête ou un élément de tâche pour les participants à la réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="00ce8-147">Afficher les notes pertinentes pour la réunion (par exemple, des informations sur un responsable commercial)</span><span class="sxs-lookup"><span data-stu-id="00ce8-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="L'exemple montre comment présenter le contenu d'un sondage dans un onglet de réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="00ce8-149">Anatomie : onglet En réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="L'exemple montre l'anatomie structurelle d'un onglet en réunion." border="false":::

|<span data-ttu-id="00ce8-151">Compteur</span><span class="sxs-lookup"><span data-stu-id="00ce8-151">Counter</span></span>|<span data-ttu-id="00ce8-152">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="00ce8-153">1</span><span class="sxs-lookup"><span data-stu-id="00ce8-153">1</span></span>|<span data-ttu-id="00ce8-154">**Icône de l'application (sélectionnée)**: logo d'application transparent de 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="00ce8-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="00ce8-155">2</span><span class="sxs-lookup"><span data-stu-id="00ce8-155">2</span></span>|<span data-ttu-id="00ce8-156">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="00ce8-156">**App name**</span></span>|
|<span data-ttu-id="00ce8-157">3</span><span class="sxs-lookup"><span data-stu-id="00ce8-157">3</span></span>|<span data-ttu-id="00ce8-158">**En-tête**: inclut le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="00ce8-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="00ce8-159">4 </span><span class="sxs-lookup"><span data-stu-id="00ce8-159">4</span></span>|<span data-ttu-id="00ce8-160">**Bouton Fermer :** ferme l'onglet. Utilisez toujours l'icône de fermeture supérieure droite au lieu d'une action dans le pied de plan.</span><span class="sxs-lookup"><span data-stu-id="00ce8-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="00ce8-161">5 </span><span class="sxs-lookup"><span data-stu-id="00ce8-161">5</span></span>|<span data-ttu-id="00ce8-162">**Barre de notification**: les alertes d'erreur s'affichent directement sous l'en-tête et poussent le contenu de l'iFrame vers le bas de 20 pixels.</span><span class="sxs-lookup"><span data-stu-id="00ce8-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="00ce8-163">6 </span><span class="sxs-lookup"><span data-stu-id="00ce8-163">6</span></span>|<span data-ttu-id="00ce8-164">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="00ce8-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="00ce8-165">Espacement</span><span class="sxs-lookup"><span data-stu-id="00ce8-165">Spacing</span></span>

<span data-ttu-id="00ce8-166">Optimisez votre onglet de réunion pour qu'il s'adapte de bord à bord dans la zone iFrame de 280 pixels.</span><span class="sxs-lookup"><span data-stu-id="00ce8-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="00ce8-167">Il y a 20 pixels de remplissage sur les côtés gauche et droit de l'iframe et entre l'en-tête de l'onglet.</span><span class="sxs-lookup"><span data-stu-id="00ce8-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="00ce8-168">L'iframe est pleine page en bas de l'onglet.</span><span class="sxs-lookup"><span data-stu-id="00ce8-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="L'exemple montre les dimensions d'espacement des onglets dans la réunion." border="false":::

### <a name="scrolling"></a><span data-ttu-id="00ce8-170">Défilement</span><span class="sxs-lookup"><span data-stu-id="00ce8-170">Scrolling</span></span>

<span data-ttu-id="00ce8-171">Le contenu de l'Iframe doit défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="00ce8-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="00ce8-172">Vous pouvez uniquement voir le contenu vers qui vous avez fait défiler (rien au-dessus ou au-dessous).</span><span class="sxs-lookup"><span data-stu-id="00ce8-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="00ce8-173">La barre de défilement fait partie du contenu de l'iframe.</span><span class="sxs-lookup"><span data-stu-id="00ce8-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="L'exemple montre comment défile l'onglet dans la réunion." border="false":::

### <a name="navigation"></a><span data-ttu-id="00ce8-175">Navigation</span><span class="sxs-lookup"><span data-stu-id="00ce8-175">Navigation</span></span>

<span data-ttu-id="00ce8-176">Pour les scénarios avec des couches de navigation ou un contenu lourd, nous vous recommandons de permettre aux utilisateurs d'accéder à une couche secondaire.</span><span class="sxs-lookup"><span data-stu-id="00ce8-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="00ce8-177">Les utilisateurs doivent pouvoir revenir à la couche précédente.</span><span class="sxs-lookup"><span data-stu-id="00ce8-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple de navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="00ce8-179">Utiliser une boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="00ce8-180">Les boîtes de dialogue de réunion s'affichent lors de la phase de réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="00ce8-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="00ce8-181">Ils nécessitent l'attention, la confirmation ou l'interaction d'un utilisateur, mais sont discrets et n'interrompent pas la réunion.</span><span class="sxs-lookup"><span data-stu-id="00ce8-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="00ce8-182">Vous devez les utiliser avec parcimonie et pour les scénarios légers et orientés vers les tâches.</span><span class="sxs-lookup"><span data-stu-id="00ce8-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="00ce8-183">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="00ce8-183">Use cases</span></span>

<span data-ttu-id="00ce8-184">Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (tel que l'organisateur de la réunion) qui souhaite peut-être que les participants :</span><span class="sxs-lookup"><span data-stu-id="00ce8-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="00ce8-185">Fournir de brefs commentaires</span><span class="sxs-lookup"><span data-stu-id="00ce8-185">Provide brief feedback</span></span>
* <span data-ttu-id="00ce8-186">Prendre une courte enquête ou un sondage</span><span class="sxs-lookup"><span data-stu-id="00ce8-186">Take a short survey or poll</span></span>
* <span data-ttu-id="00ce8-187">Envoyer des approbations</span><span class="sxs-lookup"><span data-stu-id="00ce8-187">Submit approvals</span></span>
* <span data-ttu-id="00ce8-188">Obtenir des rappels</span><span class="sxs-lookup"><span data-stu-id="00ce8-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="L'exemple montre comment utiliser une boîte de dialogue en réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="00ce8-190">Anatomie : boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="L'exemple illustre l'anatomie structurelle d'une boîte de dialogue en réunion." border="false":::

|<span data-ttu-id="00ce8-192">Compteur</span><span class="sxs-lookup"><span data-stu-id="00ce8-192">Counter</span></span>|<span data-ttu-id="00ce8-193">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="00ce8-194">1</span><span class="sxs-lookup"><span data-stu-id="00ce8-194">1</span></span>|<span data-ttu-id="00ce8-195">**En-tête :** inclut l'icône de l'application, le nom, la chaîne d'action et l'icône fermer.</span><span class="sxs-lookup"><span data-stu-id="00ce8-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="00ce8-196">2</span><span class="sxs-lookup"><span data-stu-id="00ce8-196">2</span></span>|<span data-ttu-id="00ce8-197">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="00ce8-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="00ce8-198">Anatomie : en-tête de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="L'exemple montre l'anatomie structurelle d'un en-tête de boîte de dialogue en réunion." border="false":::

<span data-ttu-id="00ce8-200">Il existe deux variantes d'en-tête.</span><span class="sxs-lookup"><span data-stu-id="00ce8-200">There are two header variants.</span></span> <span data-ttu-id="00ce8-201">Dans la mesure du possible, utilisez la variante avec l'avatar pour renforcer le fait que la boîte de dialogue vient d'une personne.</span><span class="sxs-lookup"><span data-stu-id="00ce8-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="00ce8-202">Compteur</span><span class="sxs-lookup"><span data-stu-id="00ce8-202">Counter</span></span>|<span data-ttu-id="00ce8-203">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="00ce8-204">1</span><span class="sxs-lookup"><span data-stu-id="00ce8-204">1</span></span>|<span data-ttu-id="00ce8-205">**Avatar**: personne qui initie la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="00ce8-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="00ce8-206">2</span><span class="sxs-lookup"><span data-stu-id="00ce8-206">2</span></span>|<span data-ttu-id="00ce8-207">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="00ce8-207">**App icon**</span></span>|
|<span data-ttu-id="00ce8-208">3</span><span class="sxs-lookup"><span data-stu-id="00ce8-208">3</span></span>|<span data-ttu-id="00ce8-209">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="00ce8-209">**App name**</span></span>|
|<span data-ttu-id="00ce8-210">4 </span><span class="sxs-lookup"><span data-stu-id="00ce8-210">4</span></span>|<span data-ttu-id="00ce8-211">**Bouton Fermer :** ferme la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="00ce8-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="00ce8-212">5 </span><span class="sxs-lookup"><span data-stu-id="00ce8-212">5</span></span>|<span data-ttu-id="00ce8-213">**Chaîne d'action**: décrit généralement l'auteur de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="00ce8-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="00ce8-214">Comportement réactif</span><span class="sxs-lookup"><span data-stu-id="00ce8-214">Responsive behavior</span></span>

<span data-ttu-id="00ce8-215">Les boîtes de dialogue de réunion peuvent varier en taille pour tenir compte de différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="00ce8-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="00ce8-216">Veillez à maintenir la taille des remplissages et des composants.</span><span class="sxs-lookup"><span data-stu-id="00ce8-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="00ce8-217">**Largeur**: vous pouvez spécifier la largeur de l'iframe de la boîte de dialogue n'importe où dans la plage de tailles prise en charge.</span><span class="sxs-lookup"><span data-stu-id="00ce8-217">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="00ce8-218">**Hauteur**: vous pouvez spécifier la hauteur de l'iframe de la boîte de dialogue n'importe où dans la plage de tailles prise en charge.</span><span class="sxs-lookup"><span data-stu-id="00ce8-218">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="00ce8-219">Vous pouvez également autoriser les utilisateurs à faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.</span><span class="sxs-lookup"><span data-stu-id="00ce8-219">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="00ce8-220">Pour implémenter, spécifiez la largeur et la hauteur à l'aide de la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clé.</span><span class="sxs-lookup"><span data-stu-id="00ce8-220">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple de boîte de dialogue de réunion. Largeur : Min--280 pixels (248 pixels iframe). Max--460 pixels (428 pixels iframe). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="00ce8-222">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-222">After a meeting</span></span>

<span data-ttu-id="00ce8-223">Vous pouvez revenir à une réunion une fois qu'elle s'est terminée et afficher le contenu de l'application.</span><span class="sxs-lookup"><span data-stu-id="00ce8-223">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="00ce8-224">Dans cet exemple, l'organisateur de la réunion peut examiner les résultats des sondages dans l'onglet **Contoso.** (Remarque : du point de vue de la conception, il n'y a aucune différence entre l'expérience d'onglet avant et après la réunion.)</span><span class="sxs-lookup"><span data-stu-id="00ce8-224">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="L'exemple d'illustration montre un onglet après la réunion." border="false":::

## <a name="best-practices"></a><span data-ttu-id="00ce8-226">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="00ce8-226">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="00ce8-227">Interactions</span><span class="sxs-lookup"><span data-stu-id="00ce8-227">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d'interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="00ce8-229">À faire : limiter le nombre d'interactions</span><span class="sxs-lookup"><span data-stu-id="00ce8-229">Do: Limit the number of interactions</span></span>

<span data-ttu-id="00ce8-230">Pour les boîtes de dialogue de réunion, supprimez le contenu inutile qui n'aide pas les utilisateurs à accomplir une tâche rapidement.</span><span class="sxs-lookup"><span data-stu-id="00ce8-230">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d'éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="00ce8-232">À ne pas faire : introduire des éléments inutiles</span><span class="sxs-lookup"><span data-stu-id="00ce8-232">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="00ce8-233">Une seule boîte de dialogue de réunion avec plusieurs interactions peut distrayer l'appel.</span><span class="sxs-lookup"><span data-stu-id="00ce8-233">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="00ce8-234">Disposition</span><span class="sxs-lookup"><span data-stu-id="00ce8-234">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment utiliser une mise en page de boîte de dialogue à une seule colonne." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="00ce8-236">À faire : utiliser une disposition de boîte de dialogue à une seule colonne</span><span class="sxs-lookup"><span data-stu-id="00ce8-236">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="00ce8-237">Étant donné que les boîtes de dialogue sont au centre de la phase de réunion, l'achèvement des tâches doit être rapide et simple pour éviter toute frustration de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="00ce8-237">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devez pas encombrer l'espace d'une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="00ce8-239">À ne pas faire : encombrer l'espace</span><span class="sxs-lookup"><span data-stu-id="00ce8-239">Don't: Clutter the space</span></span>

<span data-ttu-id="00ce8-240">Le contenu épais ou trop structuré peut être gênant et gênant, en particulier au cours d'une réunion.</span><span class="sxs-lookup"><span data-stu-id="00ce8-240">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une disposition d'onglet à une seule colonne." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="00ce8-242">À faire : utiliser une disposition d'onglet à une seule colonne</span><span class="sxs-lookup"><span data-stu-id="00ce8-242">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="00ce8-243">Étant donné la nature étroite de l'onglet en réunion, nous vous recommandons vivement d'afficher le contenu dans une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="00ce8-243">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="00ce8-245">À ne pas faire : utiliser plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="00ce8-245">Don't: Use multiple columns</span></span>

<span data-ttu-id="00ce8-246">En raison de l'espace limité de l'onglet en réunion, les dispositions avec plusieurs colonnes ne sont pas recommandées.</span><span class="sxs-lookup"><span data-stu-id="00ce8-246">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="00ce8-247">Contrôles</span><span class="sxs-lookup"><span data-stu-id="00ce8-247">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple montrant comment aligner à droite les contrôles principaux." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="00ce8-249">À faire : aligner à droite l'action principale</span><span class="sxs-lookup"><span data-stu-id="00ce8-249">Do: Right align the primary action</span></span>

<span data-ttu-id="00ce8-250">Nous vous recommandons de positionner l'action la plus lourde visuellement à l'emplacement le plus à droite.</span><span class="sxs-lookup"><span data-stu-id="00ce8-250">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment ne pas aligner à gauche les contrôles principaux." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="00ce8-252">À ne pas faire : aligner les actions à gauche ou au centre</span><span class="sxs-lookup"><span data-stu-id="00ce8-252">Don't: Left or center align actions</span></span>

<span data-ttu-id="00ce8-253">Cela s'écarte du modèle Teams standard pour l'emplacement des contrôles dans une boîte de dialogue et peut être en conflit avec une boîte de dialogue derrière la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="00ce8-253">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="00ce8-254">Faire défiler</span><span class="sxs-lookup"><span data-stu-id="00ce8-254">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple de défilement vertical dans un onglet de réunion." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="00ce8-256">À faire : faire défiler verticalement</span><span class="sxs-lookup"><span data-stu-id="00ce8-256">Do: Scroll vertically</span></span>

<span data-ttu-id="00ce8-257">Les utilisateurs s'attendent à un défilement vertical dans Teams (et ailleurs).</span><span class="sxs-lookup"><span data-stu-id="00ce8-257">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple de défilement horizontal dans un onglet de réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="00ce8-259">À ne pas faire : faire défiler horizontalement</span><span class="sxs-lookup"><span data-stu-id="00ce8-259">Don't: Scroll horizontally</span></span>

<span data-ttu-id="00ce8-260">Le défilement horizontal n'est pas un comportement attendu dans Teams.</span><span class="sxs-lookup"><span data-stu-id="00ce8-260">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="00ce8-261">Les autres canevas de l'environnement de réunion défilent verticalement.</span><span class="sxs-lookup"><span data-stu-id="00ce8-261">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="00ce8-262">Flux de travail</span><span class="sxs-lookup"><span data-stu-id="00ce8-262">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet de réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="00ce8-264">À faire : surfacer des scénarios complexes dans l'onglet réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-264">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="00ce8-265">Si votre application comprend plusieurs tâches, nous vous recommandons vivement d'utiliser un onglet de réunion avec une disposition sur une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="00ce8-265">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple de scénarios complexes dans une boîte de dialogue en réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="00ce8-267">À ne pas faire : rendre les boîtes de dialogue de réunion complexes</span><span class="sxs-lookup"><span data-stu-id="00ce8-267">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="00ce8-268">Les boîtes de dialogue en réunion sont conçues pour de brèves interactions.</span><span class="sxs-lookup"><span data-stu-id="00ce8-268">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="00ce8-269">Thèmes</span><span class="sxs-lookup"><span data-stu-id="00ce8-269">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème foncé." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="00ce8-271">À faire : utiliser des jetons de couleur Teams</span><span class="sxs-lookup"><span data-stu-id="00ce8-271">Do: Use Teams color tokens</span></span>

<span data-ttu-id="00ce8-272">Les réunions Teams sont optimisées pour le mode sombre afin de réduire les bruits visuels et cognitifs afin que les utilisateurs peuvent se concentrer sur la discussion et le contenu partagé.</span><span class="sxs-lookup"><span data-stu-id="00ce8-272">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="00ce8-273">En savoir plus sur <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">l'utilisation des jetons de couleur (interface utilisateur Fluent).</a></span><span class="sxs-lookup"><span data-stu-id="00ce8-273">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec un thème par défaut (clair)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="00ce8-275">À ne pas faire : valeurs hexades de code dur</span><span class="sxs-lookup"><span data-stu-id="00ce8-275">Don't: Hard code hex values</span></span>

<span data-ttu-id="00ce8-276">Si vous n'utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prenons plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="00ce8-276">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="00ce8-277">Navigation</span><span class="sxs-lookup"><span data-stu-id="00ce8-277">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton Retour." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="00ce8-279">À faire : avoir un bouton Retour</span><span class="sxs-lookup"><span data-stu-id="00ce8-279">Do: Have a back button</span></span>

<span data-ttu-id="00ce8-280">Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent pouvoir revenir à leurs vues précédentes.</span><span class="sxs-lookup"><span data-stu-id="00ce8-280">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons d'mascmit." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="00ce8-282">À ne pas faire : inclure un autre bouton d'arrêt</span><span class="sxs-lookup"><span data-stu-id="00ce8-282">Don't: Include another dismiss button</span></span>

<span data-ttu-id="00ce8-283">La fourniture d'une option permettant de fermer le contenu de l'onglet de réunion peut entraîner des problèmes, car l'en-tête est déjà sur un bouton pour faire disparaître l'onglet de la réunion lui-même.</span><span class="sxs-lookup"><span data-stu-id="00ce8-283">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modales (ou des modules de tâche) dans un onglet de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="00ce8-285">Attention : évitez les modales dans l'onglet de la réunion</span><span class="sxs-lookup"><span data-stu-id="00ce8-285">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="00ce8-286">Les modaux (également appelés modules de tâche) dans l'onglet déjà étroit de la réunion peuvent encapsuler et masquer le contenu.</span><span class="sxs-lookup"><span data-stu-id="00ce8-286">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="00ce8-287">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="00ce8-287">Validate your design</span></span>

<span data-ttu-id="00ce8-288">Si vous envisagez de publier votre application sur AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l'échec des applications lors de l'envoi.</span><span class="sxs-lookup"><span data-stu-id="00ce8-288">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00ce8-289">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="00ce8-289">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
