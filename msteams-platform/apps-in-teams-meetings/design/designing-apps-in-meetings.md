---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans Teams réunions et obtenir le kit Microsoft Teams’interface utilisateur.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 33b11a6dfc759fabd54ca2fe2c68978a5d5d1475
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644616"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="a0a42-103">Conception de votre extension Microsoft Teams réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="a0a42-104">Vous pouvez créer des applications pour rendre les réunions plus productives.</span><span class="sxs-lookup"><span data-stu-id="a0a42-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="a0a42-105">Par exemple, demandez aux personnes de répondre à une enquête pendant un appel ou d’envoyer un rappel rapide qui n’interrompt pas le flux de la réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a0a42-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a0a42-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a0a42-107">Vous trouverez des instructions de conception plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le kit Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0a42-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0a42-108">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="a0a42-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="a0a42-109">Ajouter une extension de réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-109">Add a meeting extension</span></span>

<span data-ttu-id="a0a42-110">Les utilisateurs peuvent ajouter une extension de réunion avant et pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="a0a42-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="a0a42-111">Ils peuvent également ajouter une application pour une réunion spécifique directement à partir du Teams store.</span><span class="sxs-lookup"><span data-stu-id="a0a42-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="a0a42-112">Ajouter avant une réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-112">Add before a meeting</span></span>

<span data-ttu-id="a0a42-113">Dans les détails de la réunion, les utilisateurs peuvent sélectionner Ajouter un **onglet +** pour ouvrir le programme volant de l’application et rechercher des applications optimisées pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="a0a42-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="a0a42-115">Ajouter au cours d’une réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="a0a42-116">Desktop</span><span class="sxs-lookup"><span data-stu-id="a0a42-116">Desktop</span></span>](#tab/desktop)

Lors d’une réunion, les utilisateurs peuvent sélectionner **Plus** ajouter :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **une application** et choisir l’application de leur choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion au cours d’une réunion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="a0a42-119">Mobile</span><span class="sxs-lookup"><span data-stu-id="a0a42-119">Mobile</span></span>](#tab/mobile)

Lors d’une réunion, les utilisateurs peuvent sélectionner **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: et choisir l’application de leur choix.

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion lors d’une réunion sur mobile." border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="a0a42-122">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-122">Before a meeting</span></span>

<span data-ttu-id="a0a42-123">Avant une réunion, les utilisateurs peuvent ajouter du contenu dans l’onglet. L’exemple suivant montre un brouillon de question d’enquête à qui les personnes répondront pendant l’appel.</span><span class="sxs-lookup"><span data-stu-id="a0a42-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="L’exemple montre comment apper le contenu des détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="a0a42-125">Anatomie : onglet Réunion (avant et après les réunions)</span><span class="sxs-lookup"><span data-stu-id="a0a42-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|<span data-ttu-id="a0a42-127">Compteur</span><span class="sxs-lookup"><span data-stu-id="a0a42-127">Counter</span></span>|<span data-ttu-id="a0a42-128">Description</span><span class="sxs-lookup"><span data-stu-id="a0a42-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a0a42-129">1</span><span class="sxs-lookup"><span data-stu-id="a0a42-129">1</span></span>|<span data-ttu-id="a0a42-130">**Nom de l’onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="a0a42-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="a0a42-131">2</span><span class="sxs-lookup"><span data-stu-id="a0a42-131">2</span></span>|<span data-ttu-id="a0a42-132">**Dépassement de tabulation**: ouvre les actions d’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="a0a42-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="a0a42-133">3</span><span class="sxs-lookup"><span data-stu-id="a0a42-133">3</span></span>|<span data-ttu-id="a0a42-134">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="a0a42-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="a0a42-135">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="a0a42-135">Designing with UI templates</span></span>

<span data-ttu-id="a0a42-136">Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre onglet de réunion :</span><span class="sxs-lookup"><span data-stu-id="a0a42-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="a0a42-137">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="a0a42-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a0a42-138">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="a0a42-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="a0a42-139">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="a0a42-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="a0a42-140">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="a0a42-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a0a42-141">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="a0a42-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="a0a42-142">[Navigation gauche :](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="a0a42-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="a0a42-143">En règle générale, vous devez conserver la navigation au minimum.</span><span class="sxs-lookup"><span data-stu-id="a0a42-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="a0a42-144">Utiliser un onglet de réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-144">Use an in-meeting tab</span></span>

<span data-ttu-id="a0a42-145">L’onglet de réunion est un canevas qui permet d’accroître la collaboration pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="a0a42-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="a0a42-146">Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion par le biais d’affichages partagés ou basés sur des rôles.</span><span class="sxs-lookup"><span data-stu-id="a0a42-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="a0a42-147">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="a0a42-147">Use cases</span></span>

<span data-ttu-id="a0a42-148">Les personnes peuvent utiliser l’onglet réunion pour :</span><span class="sxs-lookup"><span data-stu-id="a0a42-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="a0a42-149">Fournissez des commentaires détaillés.</span><span class="sxs-lookup"><span data-stu-id="a0a42-149">Provide detailed feedback.</span></span> <span data-ttu-id="a0a42-150">Par exemple, évaluez un candidat au poste.</span><span class="sxs-lookup"><span data-stu-id="a0a42-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="a0a42-151">Créez un sondage, une enquête ou un élément de tâche pour les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="a0a42-152">Afficher les notes pertinentes pour la réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="a0a42-153">Par exemple, des informations sur un responsable commercial.</span><span class="sxs-lookup"><span data-stu-id="a0a42-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="a0a42-154">Desktop</span><span class="sxs-lookup"><span data-stu-id="a0a42-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="a0a42-156">Mobile</span><span class="sxs-lookup"><span data-stu-id="a0a42-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion sur un appareil mobile." border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="a0a42-158">Anatomie : onglet En réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet en réunion." border="false":::

|<span data-ttu-id="a0a42-160">Compteur</span><span class="sxs-lookup"><span data-stu-id="a0a42-160">Counter</span></span>|<span data-ttu-id="a0a42-161">Description</span><span class="sxs-lookup"><span data-stu-id="a0a42-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a0a42-162">1</span><span class="sxs-lookup"><span data-stu-id="a0a42-162">1</span></span>|<span data-ttu-id="a0a42-163">**Icône de l’application (sélectionnée)**: logo d’application transparent de 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="a0a42-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="a0a42-164">2</span><span class="sxs-lookup"><span data-stu-id="a0a42-164">2</span></span>|<span data-ttu-id="a0a42-165">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="a0a42-165">**App name**</span></span>|
|<span data-ttu-id="a0a42-166">3</span><span class="sxs-lookup"><span data-stu-id="a0a42-166">3</span></span>|<span data-ttu-id="a0a42-167">**En-tête**: inclut le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="a0a42-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="a0a42-168">4 </span><span class="sxs-lookup"><span data-stu-id="a0a42-168">4</span></span>|<span data-ttu-id="a0a42-169">**Bouton Fermer :** ferme l’onglet. Utilisez toujours l’icône de fermeture supérieure droite au lieu d’une action dans le pied de plan.</span><span class="sxs-lookup"><span data-stu-id="a0a42-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="a0a42-170">5 </span><span class="sxs-lookup"><span data-stu-id="a0a42-170">5</span></span>|<span data-ttu-id="a0a42-171">**Barre de notification**: les alertes d’erreur s’affichent directement sous l’en-tête et poussent le contenu de l’iFrame vers le bas de 20 pixels.</span><span class="sxs-lookup"><span data-stu-id="a0a42-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="a0a42-172">6 </span><span class="sxs-lookup"><span data-stu-id="a0a42-172">6</span></span>|<span data-ttu-id="a0a42-173">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="a0a42-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="a0a42-174">Espacement</span><span class="sxs-lookup"><span data-stu-id="a0a42-174">Spacing</span></span>

<span data-ttu-id="a0a42-175">Optimisez votre onglet de réunion pour qu’il s’adapte de bord à bord dans la zone iFrame de 280 pixels.</span><span class="sxs-lookup"><span data-stu-id="a0a42-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="a0a42-176">Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’iframe et entre l’en-tête de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="a0a42-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="a0a42-177">L’iframe est pleine page en bas de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="a0a42-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="L’exemple montre les dimensions d’espacement des onglets dans la réunion." border="false":::

### <a name="scrolling"></a><span data-ttu-id="a0a42-179">Défilement</span><span class="sxs-lookup"><span data-stu-id="a0a42-179">Scrolling</span></span>

<span data-ttu-id="a0a42-180">Le contenu de l’Iframe doit défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="a0a42-180">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="a0a42-181">Vous pouvez uniquement voir le contenu vers qui vous avez fait défiler (rien au-dessus ou au-dessous).</span><span class="sxs-lookup"><span data-stu-id="a0a42-181">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="a0a42-182">La barre de défilement fait partie du contenu de l’iframe.</span><span class="sxs-lookup"><span data-stu-id="a0a42-182">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="L’exemple montre comment défile l’onglet dans la réunion." border="false":::

### <a name="navigation"></a><span data-ttu-id="a0a42-184">Navigation</span><span class="sxs-lookup"><span data-stu-id="a0a42-184">Navigation</span></span>

<span data-ttu-id="a0a42-185">Pour les scénarios avec des couches de navigation ou un contenu lourd, nous vous recommandons de permettre aux utilisateurs d’accéder à une couche secondaire.</span><span class="sxs-lookup"><span data-stu-id="a0a42-185">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="a0a42-186">Les utilisateurs doivent pouvoir revenir à la couche précédente.</span><span class="sxs-lookup"><span data-stu-id="a0a42-186">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple de navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="a0a42-188">Utiliser une boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-188">Use an in-meeting dialog</span></span>

<span data-ttu-id="a0a42-189">Les boîtes de dialogue de réunion s’affichent sur la Teams de réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-189">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="a0a42-190">Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont discrets et n’interrompent pas la réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-190">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="a0a42-191">Vous devez les utiliser avec parcimonie et pour les scénarios légers et orientés vers les tâches.</span><span class="sxs-lookup"><span data-stu-id="a0a42-191">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="a0a42-192">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="a0a42-192">Use cases</span></span>

<span data-ttu-id="a0a42-193">Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (tel que l’organisateur de la réunion) qui souhaite peut-être que les participants :</span><span class="sxs-lookup"><span data-stu-id="a0a42-193">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="a0a42-194">Fournir de brefs commentaires</span><span class="sxs-lookup"><span data-stu-id="a0a42-194">Provide brief feedback</span></span>
* <span data-ttu-id="a0a42-195">Prendre une courte enquête ou un sondage</span><span class="sxs-lookup"><span data-stu-id="a0a42-195">Take a short survey or poll</span></span>
* <span data-ttu-id="a0a42-196">Envoyer des approbations</span><span class="sxs-lookup"><span data-stu-id="a0a42-196">Submit approvals</span></span>
* <span data-ttu-id="a0a42-197">Obtenir des rappels</span><span class="sxs-lookup"><span data-stu-id="a0a42-197">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="a0a42-198">Desktop</span><span class="sxs-lookup"><span data-stu-id="a0a42-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="a0a42-200">Mobile</span><span class="sxs-lookup"><span data-stu-id="a0a42-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion sur un appareil mobile." border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="a0a42-202">Anatomie : boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-202">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’une boîte de dialogue en réunion." border="false":::

|<span data-ttu-id="a0a42-204">Compteur</span><span class="sxs-lookup"><span data-stu-id="a0a42-204">Counter</span></span>|<span data-ttu-id="a0a42-205">Description</span><span class="sxs-lookup"><span data-stu-id="a0a42-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a0a42-206">1</span><span class="sxs-lookup"><span data-stu-id="a0a42-206">1</span></span>|<span data-ttu-id="a0a42-207">**En-tête :** inclut l’icône de l’application, le nom, la chaîne d’action et l’icône fermer.</span><span class="sxs-lookup"><span data-stu-id="a0a42-207">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="a0a42-208">2</span><span class="sxs-lookup"><span data-stu-id="a0a42-208">2</span></span>|<span data-ttu-id="a0a42-209">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="a0a42-209">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="a0a42-210">Anatomie : en-tête de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-210">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un en-tête de boîte de dialogue en réunion." border="false":::

<span data-ttu-id="a0a42-212">Il existe deux variantes d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="a0a42-212">There are two header variants.</span></span> <span data-ttu-id="a0a42-213">Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer le fait que la boîte de dialogue vient d’une personne.</span><span class="sxs-lookup"><span data-stu-id="a0a42-213">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="a0a42-214">Compteur</span><span class="sxs-lookup"><span data-stu-id="a0a42-214">Counter</span></span>|<span data-ttu-id="a0a42-215">Description</span><span class="sxs-lookup"><span data-stu-id="a0a42-215">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a0a42-216">1</span><span class="sxs-lookup"><span data-stu-id="a0a42-216">1</span></span>|<span data-ttu-id="a0a42-217">**Avatar**: personne qui lance la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-217">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="a0a42-218">2</span><span class="sxs-lookup"><span data-stu-id="a0a42-218">2</span></span>|<span data-ttu-id="a0a42-219">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="a0a42-219">**App icon**</span></span>|
|<span data-ttu-id="a0a42-220">3</span><span class="sxs-lookup"><span data-stu-id="a0a42-220">3</span></span>|<span data-ttu-id="a0a42-221">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="a0a42-221">**App name**</span></span>|
|<span data-ttu-id="a0a42-222">4 </span><span class="sxs-lookup"><span data-stu-id="a0a42-222">4</span></span>|<span data-ttu-id="a0a42-223">**Bouton Fermer :** ferme la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a0a42-223">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="a0a42-224">5 </span><span class="sxs-lookup"><span data-stu-id="a0a42-224">5</span></span>|<span data-ttu-id="a0a42-225">**Chaîne d’action**: décrit généralement l’auteur de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a0a42-225">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="a0a42-226">Comportement réactif</span><span class="sxs-lookup"><span data-stu-id="a0a42-226">Responsive behavior</span></span>

<span data-ttu-id="a0a42-227">Les boîtes de dialogue de réunion peuvent varier en taille pour tenir compte de différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="a0a42-227">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="a0a42-228">Veillez à maintenir la taille des remplissages et des composants.</span><span class="sxs-lookup"><span data-stu-id="a0a42-228">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="a0a42-229">**Largeur**: vous pouvez spécifier la largeur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.</span><span class="sxs-lookup"><span data-stu-id="a0a42-229">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="a0a42-230">**Hauteur**: vous pouvez spécifier la hauteur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.</span><span class="sxs-lookup"><span data-stu-id="a0a42-230">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="a0a42-231">Vous pouvez également autoriser les utilisateurs à faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.</span><span class="sxs-lookup"><span data-stu-id="a0a42-231">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="a0a42-232">Pour implémenter, spécifiez la largeur et la hauteur à l’aide de la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clé.</span><span class="sxs-lookup"><span data-stu-id="a0a42-232">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple de boîte de dialogue en réunion. Largeur : Min--280 pixels (248 pixels iframe). Max--460 pixels (428 pixels iframe). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="a0a42-234">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-234">After a meeting</span></span>

<span data-ttu-id="a0a42-235">Vous pouvez revenir à une réunion une fois qu’elle s’est terminée et afficher le contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="a0a42-235">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="a0a42-236">Dans cet exemple, l’organisateur de la réunion peut examiner les résultats des sondages dans l’onglet **Contoso.** (Remarque : du point de vue de la conception, il n’y a aucune différence entre l’expérience d’onglet avant et après la réunion.)</span><span class="sxs-lookup"><span data-stu-id="a0a42-236">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="L’exemple d’illustration montre un onglet après la réunion." border="false":::

## <a name="best-practices"></a><span data-ttu-id="a0a42-238">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="a0a42-238">Best practices</span></span>

<span data-ttu-id="a0a42-239">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="a0a42-239">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="a0a42-240">Interactions</span><span class="sxs-lookup"><span data-stu-id="a0a42-240">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d’interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="a0a42-242">À faire : limiter le nombre d’interactions</span><span class="sxs-lookup"><span data-stu-id="a0a42-242">Do: Limit the number of interactions</span></span>

<span data-ttu-id="a0a42-243">Pour les boîtes de dialogue de réunion, supprimez le contenu inutile qui n’aide pas les utilisateurs à accomplir une tâche rapidement.</span><span class="sxs-lookup"><span data-stu-id="a0a42-243">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d’éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="a0a42-245">À ne pas faire : introduire des éléments inutiles</span><span class="sxs-lookup"><span data-stu-id="a0a42-245">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="a0a42-246">Une seule boîte de dialogue de réunion avec plusieurs interactions peut distrayer l’appel.</span><span class="sxs-lookup"><span data-stu-id="a0a42-246">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="a0a42-247">Disposition</span><span class="sxs-lookup"><span data-stu-id="a0a42-247">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment utiliser une mise en page de boîte de dialogue à une seule colonne." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="a0a42-249">À faire : utiliser une disposition de boîte de dialogue à une seule colonne</span><span class="sxs-lookup"><span data-stu-id="a0a42-249">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="a0a42-250">Étant donné que les boîtes de dialogue sont au centre de la phase de réunion, l’achèvement des tâches doit être rapide et simple pour éviter toute frustration de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0a42-250">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="a0a42-252">À ne pas faire : encombrer l’espace</span><span class="sxs-lookup"><span data-stu-id="a0a42-252">Don't: Clutter the space</span></span>

<span data-ttu-id="a0a42-253">Le contenu épais ou trop structuré peut être gênant et gênant, en particulier au cours d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="a0a42-253">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une disposition d’onglet à une seule colonne." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="a0a42-255">À faire : utiliser une disposition d’onglet à une seule colonne</span><span class="sxs-lookup"><span data-stu-id="a0a42-255">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="a0a42-256">Étant donné la nature étroite de l’onglet en réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="a0a42-256">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="a0a42-258">À ne pas faire : utiliser plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="a0a42-258">Don't: Use multiple columns</span></span>

<span data-ttu-id="a0a42-259">En raison de l’espace limité de l’onglet en réunion, les dispositions avec plusieurs colonnes ne sont pas recommandées.</span><span class="sxs-lookup"><span data-stu-id="a0a42-259">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="a0a42-260">Contrôles</span><span class="sxs-lookup"><span data-stu-id="a0a42-260">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple montrant comment aligner à droite les contrôles principaux." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="a0a42-262">À faire : aligner à droite l’action principale</span><span class="sxs-lookup"><span data-stu-id="a0a42-262">Do: Right align the primary action</span></span>

<span data-ttu-id="a0a42-263">Nous vous recommandons de positionner l’action la plus lourde visuellement à l’emplacement le plus à droite.</span><span class="sxs-lookup"><span data-stu-id="a0a42-263">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment ne pas aligner à gauche les contrôles principaux." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="a0a42-265">À ne pas faire : aligner les actions à gauche ou au centre</span><span class="sxs-lookup"><span data-stu-id="a0a42-265">Don't: Left or center align actions</span></span>

<span data-ttu-id="a0a42-266">Cela s’écarte du modèle Teams standard pour l’emplacement des contrôles dans une boîte de dialogue et peut être en conflit avec une boîte de dialogue derrière la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="a0a42-266">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="a0a42-267">Faire défiler</span><span class="sxs-lookup"><span data-stu-id="a0a42-267">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple de défilement vertical dans un onglet de réunion." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="a0a42-269">À faire : faire défiler verticalement</span><span class="sxs-lookup"><span data-stu-id="a0a42-269">Do: Scroll vertically</span></span>

<span data-ttu-id="a0a42-270">Les utilisateurs s’attendent à ce que le défilement vertical Teams (et ailleurs).</span><span class="sxs-lookup"><span data-stu-id="a0a42-270">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple de défilement horizontal dans un onglet de réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="a0a42-272">À ne pas faire : faire défiler horizontalement</span><span class="sxs-lookup"><span data-stu-id="a0a42-272">Don't: Scroll horizontally</span></span>

<span data-ttu-id="a0a42-273">Le défilement horizontal n’est pas un comportement attendu dans Teams.</span><span class="sxs-lookup"><span data-stu-id="a0a42-273">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="a0a42-274">Les autres canevas de l’environnement de réunion défilent verticalement.</span><span class="sxs-lookup"><span data-stu-id="a0a42-274">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="a0a42-275">Flux de travail</span><span class="sxs-lookup"><span data-stu-id="a0a42-275">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet de réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="a0a42-277">À faire : surfacer des scénarios complexes dans l’onglet réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-277">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="a0a42-278">Si votre application comprend plusieurs tâches, nous vous recommandons vivement d’utiliser un onglet de réunion avec une disposition sur une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="a0a42-278">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple de scénarios complexes dans une boîte de dialogue de réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="a0a42-280">À ne pas faire : rendre les boîtes de dialogue de réunion complexes</span><span class="sxs-lookup"><span data-stu-id="a0a42-280">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="a0a42-281">Les boîtes de dialogue en réunion sont conçues pour de brèves interactions.</span><span class="sxs-lookup"><span data-stu-id="a0a42-281">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="a0a42-282">Thèmes</span><span class="sxs-lookup"><span data-stu-id="a0a42-282">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème foncé." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="a0a42-284">À faire : utiliser Teams de couleur</span><span class="sxs-lookup"><span data-stu-id="a0a42-284">Do: Use Teams color tokens</span></span>

<span data-ttu-id="a0a42-285">Teams réunions sont optimisées pour le mode sombre afin de réduire les bruits visuels et cognitifs afin que les utilisateurs se concentrent sur la discussion et le contenu partagé.</span><span class="sxs-lookup"><span data-stu-id="a0a42-285">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="a0a42-286">En savoir plus sur <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">l’utilisation des jetons de couleur (interface utilisateur Fluent).</a></span><span class="sxs-lookup"><span data-stu-id="a0a42-286">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec un thème par défaut (clair)." border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="a0a42-288">À ne pas faire : valeurs hexades de code dur</span><span class="sxs-lookup"><span data-stu-id="a0a42-288">Don't: Hard code hex values</span></span>

<span data-ttu-id="a0a42-289">Si vous n’utilisez pas Teams couleur, vos conceptions seront moins évolutives et prenons plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="a0a42-289">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="a0a42-290">Navigation</span><span class="sxs-lookup"><span data-stu-id="a0a42-290">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton Retour." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="a0a42-292">À faire : avoir un bouton Retour</span><span class="sxs-lookup"><span data-stu-id="a0a42-292">Do: Have a back button</span></span>

<span data-ttu-id="a0a42-293">Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent pouvoir revenir à leurs vues précédentes.</span><span class="sxs-lookup"><span data-stu-id="a0a42-293">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons d’mascmit." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="a0a42-295">À ne pas faire : inclure un autre bouton d’arrêt</span><span class="sxs-lookup"><span data-stu-id="a0a42-295">Don't: Include another dismiss button</span></span>

<span data-ttu-id="a0a42-296">La fourniture d’une option permettant de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car l’en-tête est déjà sur un bouton pour faire disparaître l’onglet de la réunion lui-même.</span><span class="sxs-lookup"><span data-stu-id="a0a42-296">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modales (ou des modules de tâche) dans un onglet de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="a0a42-298">Attention : évitez les modales dans l’onglet de la réunion</span><span class="sxs-lookup"><span data-stu-id="a0a42-298">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="a0a42-299">Les modales (également appelées modules de tâche) dans l’onglet déjà étroit de la réunion peuvent encapsuler et masquer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a0a42-299">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::
