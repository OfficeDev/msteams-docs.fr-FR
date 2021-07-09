---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans Teams réunions et obtenir le kit Microsoft Teams’interface utilisateur.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a08e5a850a62b0cf73661d00e07e55e46abce32f
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335409"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="8e268-103">Conception de votre extension Microsoft Teams réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="8e268-104">Vous pouvez créer des applications pour rendre les réunions plus productives.</span><span class="sxs-lookup"><span data-stu-id="8e268-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="8e268-105">Par exemple, demandez aux personnes de répondre à une enquête pendant un appel ou d’envoyer un rappel rapide qui n’interrompt pas le flux de la réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="8e268-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8e268-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="8e268-107">Vous trouverez des instructions de conception plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le kit Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8e268-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e268-108">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="8e268-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="8e268-109">Ajouter une extension de réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-109">Add a meeting extension</span></span>

<span data-ttu-id="8e268-110">Les utilisateurs peuvent ajouter une extension de réunion avant et pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="8e268-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="8e268-111">Ils peuvent également ajouter une application pour une réunion spécifique directement à partir du Teams store.</span><span class="sxs-lookup"><span data-stu-id="8e268-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="8e268-112">Ajouter avant une réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-112">Add before a meeting</span></span>

<span data-ttu-id="8e268-113">Dans les détails de la réunion, les utilisateurs peuvent sélectionner Ajouter un **onglet +** pour ouvrir le programme volant de l’application et rechercher des applications optimisées pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="8e268-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="8e268-115">Ajouter au cours d’une réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="8e268-116">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="8e268-116">Desktop</span></span>](#tab/desktop)

Lors d’une réunion, les utilisateurs peuvent sélectionner **Ajouter** une :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **application** et l’application de leur choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion au cours d’une réunion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="8e268-119">Mobile</span><span class="sxs-lookup"><span data-stu-id="8e268-119">Mobile</span></span>](#tab/mobile)

Après avoir ajouté l’application sur le bureau, vous pouvez sélectionner l’application et l’utiliser lors d’une réunion en sélectionnant **Plus.** :::image type="icon" source="../../assets/icons/teams-client-more.png":::

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion lors d’une réunion sur mobile." border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="8e268-122">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-122">Before a meeting</span></span>

<span data-ttu-id="8e268-123">Avant une réunion, les utilisateurs peuvent ajouter du contenu dans l’onglet. L’exemple suivant montre un brouillon de question d’enquête à répondre pendant l’appel.</span><span class="sxs-lookup"><span data-stu-id="8e268-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="L’exemple montre comment apper le contenu des détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="8e268-125">Anatomie : onglet Réunion (avant et après les réunions)</span><span class="sxs-lookup"><span data-stu-id="8e268-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|<span data-ttu-id="8e268-127">Compteur</span><span class="sxs-lookup"><span data-stu-id="8e268-127">Counter</span></span>|<span data-ttu-id="8e268-128">Description</span><span class="sxs-lookup"><span data-stu-id="8e268-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="8e268-129">1</span><span class="sxs-lookup"><span data-stu-id="8e268-129">1</span></span>|<span data-ttu-id="8e268-130">**Nom de l’onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="8e268-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="8e268-131">2</span><span class="sxs-lookup"><span data-stu-id="8e268-131">2</span></span>|<span data-ttu-id="8e268-132">**Dépassement de tabulation**: ouvre les actions d’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="8e268-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="8e268-133">3</span><span class="sxs-lookup"><span data-stu-id="8e268-133">3</span></span>|<span data-ttu-id="8e268-134">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e268-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="8e268-135">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="8e268-135">Designing with UI templates</span></span>

<span data-ttu-id="8e268-136">Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre onglet de réunion :</span><span class="sxs-lookup"><span data-stu-id="8e268-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="8e268-137">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="8e268-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="8e268-138">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="8e268-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="8e268-139">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="8e268-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="8e268-140">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="8e268-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="8e268-141">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="8e268-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="8e268-142">[Navigation gauche](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="8e268-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="8e268-143">En règle générale, vous devez conserver la navigation au minimum.</span><span class="sxs-lookup"><span data-stu-id="8e268-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="8e268-144">Utiliser un onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-144">Use an in-meeting tab</span></span>

<span data-ttu-id="8e268-145">L’onglet de réunion est un canevas qui permet d’accroître la collaboration pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="8e268-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="8e268-146">Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion par le biais d’affichages partagés ou basés sur des rôles.</span><span class="sxs-lookup"><span data-stu-id="8e268-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="8e268-147">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="8e268-147">Use cases</span></span>

<span data-ttu-id="8e268-148">Les personnes peuvent utiliser l’onglet réunion pour :</span><span class="sxs-lookup"><span data-stu-id="8e268-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="8e268-149">Fournissez des commentaires détaillés.</span><span class="sxs-lookup"><span data-stu-id="8e268-149">Provide detailed feedback.</span></span> <span data-ttu-id="8e268-150">Par exemple, évaluez un candidat au poste.</span><span class="sxs-lookup"><span data-stu-id="8e268-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="8e268-151">Créez un sondage, une enquête ou un élément de tâche pour les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="8e268-152">Afficher les notes pertinentes pour la réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="8e268-153">Par exemple, des informations sur un responsable commercial.</span><span class="sxs-lookup"><span data-stu-id="8e268-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="8e268-154">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="8e268-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="8e268-156">Mobile</span><span class="sxs-lookup"><span data-stu-id="8e268-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion sur un appareil mobile." border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="8e268-158">Anatomie : onglet En réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet en réunion." border="false":::

|<span data-ttu-id="8e268-160">Compteur</span><span class="sxs-lookup"><span data-stu-id="8e268-160">Counter</span></span>|<span data-ttu-id="8e268-161">Description</span><span class="sxs-lookup"><span data-stu-id="8e268-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="8e268-162">1</span><span class="sxs-lookup"><span data-stu-id="8e268-162">1</span></span>|<span data-ttu-id="8e268-163">**Icône de l’application (sélectionnée)**: logo d’application transparent de 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="8e268-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="8e268-164">2</span><span class="sxs-lookup"><span data-stu-id="8e268-164">2</span></span>|<span data-ttu-id="8e268-165">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="8e268-165">**App name**</span></span>|
|<span data-ttu-id="8e268-166">3</span><span class="sxs-lookup"><span data-stu-id="8e268-166">3</span></span>|<span data-ttu-id="8e268-167">**En-tête**: inclut le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e268-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="8e268-168">4 </span><span class="sxs-lookup"><span data-stu-id="8e268-168">4</span></span>|<span data-ttu-id="8e268-169">**Bouton Fermer :** ferme l’onglet. Utilisez toujours l’icône de fermeture supérieure droite au lieu d’une action dans le pied de plan.</span><span class="sxs-lookup"><span data-stu-id="8e268-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="8e268-170">5 </span><span class="sxs-lookup"><span data-stu-id="8e268-170">5</span></span>|<span data-ttu-id="8e268-171">**Barre de notification**: les alertes d’erreur s’affichent directement sous l’en-tête et poussent le contenu de l’iFrame vers le bas de 20 pixels.</span><span class="sxs-lookup"><span data-stu-id="8e268-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="8e268-172">6 </span><span class="sxs-lookup"><span data-stu-id="8e268-172">6</span></span>|<span data-ttu-id="8e268-173">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e268-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="8e268-174">Espacement</span><span class="sxs-lookup"><span data-stu-id="8e268-174">Spacing</span></span>

<span data-ttu-id="8e268-175">Optimisez votre onglet de réunion pour qu’il s’adapte de bord à bord dans la zone iFrame de 280 pixels.</span><span class="sxs-lookup"><span data-stu-id="8e268-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="8e268-176">Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’iframe et entre l’en-tête de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="8e268-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="8e268-177">L’iframe est pleine page en bas de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="8e268-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="L’exemple montre les dimensions d’espacement des onglets dans la réunion." border="false":::

### <a name="scrolling"></a><span data-ttu-id="8e268-179">Défilement</span><span class="sxs-lookup"><span data-stu-id="8e268-179">Scrolling</span></span>

<span data-ttu-id="8e268-180">N’oubliez pas les choses suivantes si vous autorisez le défilement :</span><span class="sxs-lookup"><span data-stu-id="8e268-180">Remember the following if you allow scrolling:</span></span>

* <span data-ttu-id="8e268-181">Le contenu du contenu de l’iframe doit uniquement défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="8e268-181">Content in the iframe contents should only scroll vertically.</span></span>
* <span data-ttu-id="8e268-182">Les utilisateurs doivent voir uniquement le contenu vers qui ils ont fait défiler le contenu (rien au-dessus ou au-dessous).</span><span class="sxs-lookup"><span data-stu-id="8e268-182">Users should only see the content they've scrolled to (nothing above or below).</span></span> 
* <span data-ttu-id="8e268-183">La barre de défilement fait partie du contenu de l’iframe.</span><span class="sxs-lookup"><span data-stu-id="8e268-183">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="L’exemple montre comment défile l’onglet dans la réunion." border="false":::

### <a name="navigation"></a><span data-ttu-id="8e268-185">Navigation</span><span class="sxs-lookup"><span data-stu-id="8e268-185">Navigation</span></span>

<span data-ttu-id="8e268-186">Pour les scénarios avec des couches de navigation ou un contenu épais, nous vous recommandons de permettre aux utilisateurs d’accéder à une couche secondaire.</span><span class="sxs-lookup"><span data-stu-id="8e268-186">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="8e268-187">Les utilisateurs doivent pouvoir revenir à la couche précédente.</span><span class="sxs-lookup"><span data-stu-id="8e268-187">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple de navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="8e268-189">Utiliser une boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-189">Use an in-meeting dialog</span></span>

<span data-ttu-id="8e268-190">Les boîtes de dialogue de réunion s’affichent sur la Teams de réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-190">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="8e268-191">Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont discrets et n’interrompent pas la réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-191">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="8e268-192">Vous devez les utiliser avec parcimonie et pour les scénarios légers et orientés vers les tâches.</span><span class="sxs-lookup"><span data-stu-id="8e268-192">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="8e268-193">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="8e268-193">Use cases</span></span>

<span data-ttu-id="8e268-194">Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (tel que l’organisateur de la réunion) qui souhaite peut-être que les participants :</span><span class="sxs-lookup"><span data-stu-id="8e268-194">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="8e268-195">Fournir de brefs commentaires</span><span class="sxs-lookup"><span data-stu-id="8e268-195">Provide brief feedback</span></span>
* <span data-ttu-id="8e268-196">Prendre une courte enquête ou un sondage</span><span class="sxs-lookup"><span data-stu-id="8e268-196">Take a short survey or poll</span></span>
* <span data-ttu-id="8e268-197">Envoyer des approbations</span><span class="sxs-lookup"><span data-stu-id="8e268-197">Submit approvals</span></span>
* <span data-ttu-id="8e268-198">Obtenir des rappels</span><span class="sxs-lookup"><span data-stu-id="8e268-198">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="8e268-199">Imprimante de bureau</span><span class="sxs-lookup"><span data-stu-id="8e268-199">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="8e268-201">Mobile</span><span class="sxs-lookup"><span data-stu-id="8e268-201">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion sur un appareil mobile." border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="8e268-203">Anatomie : boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-203">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’une boîte de dialogue en réunion." border="false":::

|<span data-ttu-id="8e268-205">Compteur</span><span class="sxs-lookup"><span data-stu-id="8e268-205">Counter</span></span>|<span data-ttu-id="8e268-206">Description</span><span class="sxs-lookup"><span data-stu-id="8e268-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="8e268-207">1</span><span class="sxs-lookup"><span data-stu-id="8e268-207">1</span></span>|<span data-ttu-id="8e268-208">**En-tête :** inclut l’icône de l’application, le nom, la chaîne d’action et l’icône fermer.</span><span class="sxs-lookup"><span data-stu-id="8e268-208">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="8e268-209">2</span><span class="sxs-lookup"><span data-stu-id="8e268-209">2</span></span>|<span data-ttu-id="8e268-210">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e268-210">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="8e268-211">Anatomie : en-tête de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-211">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un en-tête de boîte de dialogue en réunion." border="false":::

<span data-ttu-id="8e268-213">Il existe deux variantes d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="8e268-213">There are two header variants.</span></span> <span data-ttu-id="8e268-214">Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer le fait que la boîte de dialogue vient d’une personne.</span><span class="sxs-lookup"><span data-stu-id="8e268-214">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="8e268-215">Compteur</span><span class="sxs-lookup"><span data-stu-id="8e268-215">Counter</span></span>|<span data-ttu-id="8e268-216">Description</span><span class="sxs-lookup"><span data-stu-id="8e268-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="8e268-217">1</span><span class="sxs-lookup"><span data-stu-id="8e268-217">1</span></span>|<span data-ttu-id="8e268-218">**Avatar**: personne qui lance la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-218">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="8e268-219">2</span><span class="sxs-lookup"><span data-stu-id="8e268-219">2</span></span>|<span data-ttu-id="8e268-220">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="8e268-220">**App icon**</span></span>|
|<span data-ttu-id="8e268-221">3</span><span class="sxs-lookup"><span data-stu-id="8e268-221">3</span></span>|<span data-ttu-id="8e268-222">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="8e268-222">**App name**</span></span>|
|<span data-ttu-id="8e268-223">4 </span><span class="sxs-lookup"><span data-stu-id="8e268-223">4</span></span>|<span data-ttu-id="8e268-224">**Bouton Fermer :** ferme la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8e268-224">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="8e268-225">5 </span><span class="sxs-lookup"><span data-stu-id="8e268-225">5</span></span>|<span data-ttu-id="8e268-226">**Chaîne d’action**: décrit généralement qui a initié la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8e268-226">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior-in-meeting-dialogs"></a><span data-ttu-id="8e268-227">Comportement réactif : boîtes de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-227">Responsive behavior: In-meeting dialogs</span></span>

<span data-ttu-id="8e268-228">Les boîtes de dialogue de réunion peuvent varier en taille pour tenir compte de différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="8e268-228">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="8e268-229">Veillez à maintenir la taille des remplissages et des composants.</span><span class="sxs-lookup"><span data-stu-id="8e268-229">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="8e268-230">**Largeur**: vous pouvez spécifier la largeur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.</span><span class="sxs-lookup"><span data-stu-id="8e268-230">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="8e268-231">**Hauteur**: vous pouvez spécifier la hauteur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.</span><span class="sxs-lookup"><span data-stu-id="8e268-231">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="8e268-232">Vous pouvez également autoriser les utilisateurs à faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.</span><span class="sxs-lookup"><span data-stu-id="8e268-232">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="8e268-233">Pour implémenter, spécifiez la largeur et la hauteur à l’aide de la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clé.</span><span class="sxs-lookup"><span data-stu-id="8e268-233">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple de boîte de dialogue de réunion. Largeur : Min--280 pixels (248 pixels iframe). Max--460 pixels (428 pixels iframe). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a><span data-ttu-id="8e268-235">Utiliser l’étape de réunion partagée</span><span class="sxs-lookup"><span data-stu-id="8e268-235">Use the shared meeting stage</span></span>

<span data-ttu-id="8e268-236">La phase de réunion partagée permet aux participants de la réunion d’interagir et de collaborer sur le contenu de l’application en temps réel.</span><span class="sxs-lookup"><span data-stu-id="8e268-236">Shared meeting stage helps meeting participants interact with and collaborate on app content in real-time.</span></span> <span data-ttu-id="8e268-237">Par exemple, les utilisateurs peuvent se concentrer sur la modification d’un document, le brainstorming avec un tableau blanc ou la révision d’un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8e268-237">For example, users can focus their call on editing a document, brainstorming with a whiteboard, or reviewing a dashboard.</span></span>

<span data-ttu-id="8e268-238">Les applications partagées à l’étape de la réunion occupent le même espace qu’un écran partagé.</span><span class="sxs-lookup"><span data-stu-id="8e268-238">Apps shared to the meeting stage occupy the same space as a shared screen.</span></span> <span data-ttu-id="8e268-239">L’étape se réoriente pour tous les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-239">The stage reorients for all meeting participants.</span></span>

### <a name="use-cases"></a><span data-ttu-id="8e268-240">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="8e268-240">Use cases</span></span>

<span data-ttu-id="8e268-241">L’étape de la réunion partagée est une question de collaboration et de participation.</span><span class="sxs-lookup"><span data-stu-id="8e268-241">The shared meeting stage is all about collaboration and participation.</span></span> <span data-ttu-id="8e268-242">Voici quelques exemples de scénarios pour vous aider à commencer.</span><span class="sxs-lookup"><span data-stu-id="8e268-242">Here are some example scenarios to help you get started.</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="8e268-243">**Modifier et réviser :** examinez les tableaux de bord et la planification avec tous les utilisateurs de l’appel.</span><span class="sxs-lookup"><span data-stu-id="8e268-243">**Edit and review**: Dive into dashboards and planning with everyone on the call.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="L’exemple montre un tableau de bord en cours de révision lors de la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="8e268-245">**Tableau blanc :** dessin et idée ensemble sur une zone de dessin partagée.</span><span class="sxs-lookup"><span data-stu-id="8e268-245">**Whiteboard**: Draw and ideate together on a shared canvas.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="L’exemple montre un tableau blanc sur la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="8e268-247">**Questionnaire :** Tester les connaissances et obtenir des informations avec des supports interactifs.</span><span class="sxs-lookup"><span data-stu-id="8e268-247">**Quiz**: Test knowledge and gain insights with interactive materials.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="Un exemple montre un questionnaire sur la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a><span data-ttu-id="8e268-249">Anatomie : étape de réunion partagée</span><span class="sxs-lookup"><span data-stu-id="8e268-249">Anatomy: Shared meeting stage</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="L’image illustre l’anatomie de conception de la phase de réunion partagée." border="false":::

|<span data-ttu-id="8e268-251">Compteur</span><span class="sxs-lookup"><span data-stu-id="8e268-251">Counter</span></span>|<span data-ttu-id="8e268-252">Description</span><span class="sxs-lookup"><span data-stu-id="8e268-252">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="8e268-253">1</span><span class="sxs-lookup"><span data-stu-id="8e268-253">1</span></span>|<span data-ttu-id="8e268-254">**Icône de l’application**: l’icône en surbrillant indique que l’onglet de réunion de l’application est ouvert.</span><span class="sxs-lookup"><span data-stu-id="8e268-254">**App icon**: The highlighted icon indicates the app's in-meeting tab is open.</span></span>|
|<span data-ttu-id="8e268-255">2</span><span class="sxs-lookup"><span data-stu-id="8e268-255">2</span></span>|<span data-ttu-id="8e268-256">**Bouton Partager à l’étape de la réunion**: point d’entrée pour partager l’application à la phase de réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-256">**Share to meeting stage button**: The entry point to share the app to the meeting stage.</span></span> <span data-ttu-id="8e268-257">S’affiche si vous configurez votre application pour utiliser la phase de réunion partagée.</span><span class="sxs-lookup"><span data-stu-id="8e268-257">Displays if you configure your app to use the shared meeting stage.</span></span>|
|<span data-ttu-id="8e268-258">3</span><span class="sxs-lookup"><span data-stu-id="8e268-258">3</span></span>|<span data-ttu-id="8e268-259">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e268-259">**iframe**: Displays your app content.</span></span>|
|<span data-ttu-id="8e268-260">4 </span><span class="sxs-lookup"><span data-stu-id="8e268-260">4</span></span>|<span data-ttu-id="8e268-261">**Bouton Arrêter le partage :** arrête le partage de l’application à la phase de réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-261">**Stop sharing button**: Stops sharing the app to the meeting stage.</span></span> <span data-ttu-id="8e268-262">S’affiche uniquement pour le participant qui a démarré le partage.</span><span class="sxs-lookup"><span data-stu-id="8e268-262">Displays only for the participant who started the share.</span></span>|
|<span data-ttu-id="8e268-263">5 </span><span class="sxs-lookup"><span data-stu-id="8e268-263">5</span></span>|<span data-ttu-id="8e268-264">**Attribution du présentateur**: affiche le nom du participant qui a partagé l’application.</span><span class="sxs-lookup"><span data-stu-id="8e268-264">**Presenter attribution**: Displays the name of the participant who shared the app.</span></span>|

### <a name="responsive-behavior-shared-meeting-stage"></a><span data-ttu-id="8e268-265">Comportement réactif : étape de réunion partagée</span><span class="sxs-lookup"><span data-stu-id="8e268-265">Responsive behavior: Shared meeting stage</span></span>

<span data-ttu-id="8e268-266">Les applications partagées à l’étape de la réunion varient en taille en fonction de l’état de la réunion et de la façon dont l’utilisateur re dimensionne la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8e268-266">Apps shared to the meeting stage vary in size based on the state of the meeting and how the user resizes the window.</span></span> <span data-ttu-id="8e268-267">Maintenez le remplissage et la disposition réactive de la navigation et des contrôles comme vous le feriez dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="8e268-267">Maintain padding and the responsive layout of navigation and controls just as you would in a browser.</span></span>

* <span data-ttu-id="8e268-268">**Panneau latéral**: un utilisateur peut ouvrir le panneau latéral à tout moment au cours d’une réunion pour discuter, afficher la liste de membres ou utiliser une application (c’est-à-dire, l’onglet de la réunion).</span><span class="sxs-lookup"><span data-stu-id="8e268-268">**Side panel**: A user can have the side panel open at any time during a meeting to chat, view the roster, or use an app (i.e., in-meeting tab).</span></span> <span data-ttu-id="8e268-269">L’étape est réorganiser dynamiquement lorsque le panneau est ouvert.</span><span class="sxs-lookup"><span data-stu-id="8e268-269">The stage dynamically rearranges when the panel is open.</span></span>
* <span data-ttu-id="8e268-270">**Grille vidéo et audio :** la grille vidéo et audio est toujours visible pour afficher les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-270">**Video and audio grid**: The video and audio grid is always visible to show meeting participants.</span></span> <span data-ttu-id="8e268-271">Lorsqu’un utilisateur met à la une ou épingle une personne dans la réunion, cela augmente la hauteur ou la largeur de la grille des participants en fonction de l’orientation.</span><span class="sxs-lookup"><span data-stu-id="8e268-271">When a user spotlights or pins someone in the meeting, this increases the height or width of the participant grid depending on the orientation.</span></span>

#### <a name="meeting-stage-without-side-panel"></a><span data-ttu-id="8e268-272">Étape de la réunion (sans panneau latéral)</span><span class="sxs-lookup"><span data-stu-id="8e268-272">Meeting stage (without side panel)</span></span>

<span data-ttu-id="8e268-273">Lorsque le panneau latéral n’est pas ouvert, l’étape de la réunion est de 994 x 678 pixels par défaut et peut être d’au moins 792 x 382 pixels.</span><span class="sxs-lookup"><span data-stu-id="8e268-273">When the side panel isn't open, the meeting stage is 994x678 pixels by default and can be a minimum 792x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Image montrant la réactivité de la phase de réunion partagée avec le panneau latéral fermé." border="false":::

#### <a name="meeting-stage-with-side-panel"></a><span data-ttu-id="8e268-275">Étape de la réunion (avec panneau latéral)</span><span class="sxs-lookup"><span data-stu-id="8e268-275">Meeting stage (with side panel)</span></span>

<span data-ttu-id="8e268-276">Lorsque le panneau latéral est ouvert, l’étape de la réunion est de 918 x 540 pixels par défaut et peut être d’au moins 472 x 382 pixels.</span><span class="sxs-lookup"><span data-stu-id="8e268-276">When the side panel is open, the meeting stage is 918x540 pixels by default and can be a minimum 472x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Image montrant la réactivité de la phase de réunion partagée avec le panneau latéral ouvert." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="8e268-278">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-278">After a meeting</span></span>

<span data-ttu-id="8e268-279">Vous pouvez revenir à une réunion une fois qu’elle s’est terminée et afficher le contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="8e268-279">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="8e268-280">Dans cet exemple, l’organisateur de la réunion peut examiner les résultats des sondages dans l’onglet **Contoso.** (Remarque : du point de vue de la conception, il n’y a aucune différence entre l’expérience d’onglet avant et après la réunion.)</span><span class="sxs-lookup"><span data-stu-id="8e268-280">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="L’exemple d’illustration montre un onglet après la réunion." border="false":::

## <a name="best-practices"></a><span data-ttu-id="8e268-282">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="8e268-282">Best practices</span></span>

<span data-ttu-id="8e268-283">Utilisez ces recommandations pour créer une expérience d’application de qualité.</span><span class="sxs-lookup"><span data-stu-id="8e268-283">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="8e268-284">Interactions</span><span class="sxs-lookup"><span data-stu-id="8e268-284">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d’interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="8e268-286">À faire : limiter le nombre d’interactions</span><span class="sxs-lookup"><span data-stu-id="8e268-286">Do: Limit the number of interactions</span></span>

<span data-ttu-id="8e268-287">Pour les boîtes de dialogue de réunion, supprimez le contenu inutile qui n’aide pas les utilisateurs à accomplir une tâche rapidement.</span><span class="sxs-lookup"><span data-stu-id="8e268-287">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d’éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="8e268-289">À ne pas faire : introduire des éléments inutiles</span><span class="sxs-lookup"><span data-stu-id="8e268-289">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="8e268-290">Une seule boîte de dialogue de réunion avec plusieurs interactions peut distrayer l’appel.</span><span class="sxs-lookup"><span data-stu-id="8e268-290">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Exemple montrant comment créer un environnement centré." border="false":::

#### <a name="do-create-a-focused-environment"></a><span data-ttu-id="8e268-292">À faire : créer un environnement axé sur le travail</span><span class="sxs-lookup"><span data-stu-id="8e268-292">Do: Create a focused environment</span></span>

<span data-ttu-id="8e268-293">Nous vous recommandons de conserver l’étendue de l’expérience de votre application uniquement à la phase de réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-293">We recommend keeping your app’s experience scoped to just the meeting stage.</span></span> <span data-ttu-id="8e268-294">Vous pouvez utiliser un onglet de réunion dans le panneau latéral en tant qu’affichage privé secondaire pour certains scénarios.</span><span class="sxs-lookup"><span data-stu-id="8e268-294">You can use an in-meeting tab in the side panel as a secondary, private view for certain scenarios.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Exemple montrant comment ne pas inclure de surfaces concurrentes pendant les réunions." border="false":::

#### <a name="dont-include-competing-surfaces"></a><span data-ttu-id="8e268-296">À ne pas faire : inclure des surfaces concurrentes</span><span class="sxs-lookup"><span data-stu-id="8e268-296">Don't: Include competing surfaces</span></span>

<span data-ttu-id="8e268-297">Votre application doit uniquement demander aux utilisateurs de se concentrer sur une seule surface à la fois, qu’elle collabore sur la scène ou qu’elle réponde à une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-297">Your app should only ask users to focus on a single surface a time, whether it's collaborating on the stage or responding to an in-meeting dialog.</span></span> <span data-ttu-id="8e268-298">(Remarque : vous ne pouvez pas conserver les boîtes de dialogue déclenchées par d’autres applications pendant que votre application est sur le terrain.)</span><span class="sxs-lookup"><span data-stu-id="8e268-298">(Note: You can’t keep dialogs being triggered by other apps while your app is on the stage.)</span></span> 

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="8e268-299">Disposition</span><span class="sxs-lookup"><span data-stu-id="8e268-299">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment utiliser une mise en page de boîte de dialogue à une seule colonne." border="false":::

#### <a name="do-use-a-one-column-dialog"></a><span data-ttu-id="8e268-301">À faire : utiliser une boîte de dialogue d’une colonne</span><span class="sxs-lookup"><span data-stu-id="8e268-301">Do: Use a one-column dialog</span></span>

<span data-ttu-id="8e268-302">Étant donné que les boîtes de dialogue sont au centre de la phase de réunion, l’achèvement des tâches doit être rapide et simple pour éviter toute frustration de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8e268-302">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="8e268-304">À ne pas faire : encombrer l’espace</span><span class="sxs-lookup"><span data-stu-id="8e268-304">Don't: Clutter the space</span></span>

<span data-ttu-id="8e268-305">Le contenu épais ou trop structuré peut être gênant et gênant, en particulier lors d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="8e268-305">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une disposition d’onglet à une seule colonne." border="false":::

#### <a name="do-use-a-one-column-tab"></a><span data-ttu-id="8e268-307">À faire : utiliser un onglet d’une colonne</span><span class="sxs-lookup"><span data-stu-id="8e268-307">Do: Use a one-column tab</span></span>

<span data-ttu-id="8e268-308">Étant donné la nature étroite de l’onglet en réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="8e268-308">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="8e268-310">À ne pas faire : utiliser plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="8e268-310">Don't: Use multiple columns</span></span>

<span data-ttu-id="8e268-311">En raison de l’espace limité de l’onglet en réunion, les dispositions avec plusieurs colonnes ne sont pas recommandées.</span><span class="sxs-lookup"><span data-stu-id="8e268-311">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="8e268-312">Contrôles</span><span class="sxs-lookup"><span data-stu-id="8e268-312">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple montrant comment aligner à droite les contrôles principaux." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="8e268-314">À faire : aligner à droite l’action principale</span><span class="sxs-lookup"><span data-stu-id="8e268-314">Do: Right align the primary action</span></span>

<span data-ttu-id="8e268-315">Nous vous recommandons de positionner l’action la plus lourde visuellement à l’emplacement le plus à droite.</span><span class="sxs-lookup"><span data-stu-id="8e268-315">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment ne pas aligner à gauche les contrôles principaux." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="8e268-317">À ne pas faire : aligner les actions à gauche ou au centre</span><span class="sxs-lookup"><span data-stu-id="8e268-317">Don't: Left or center align actions</span></span>

<span data-ttu-id="8e268-318">Cela s’écarte du modèle Teams standard pour l’emplacement des contrôles dans une boîte de dialogue et peut être en conflit avec une boîte de dialogue derrière la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="8e268-318">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="8e268-319">Défilement</span><span class="sxs-lookup"><span data-stu-id="8e268-319">Scrolling</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple de défilement vertical dans un onglet de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Exemple de défilement vertical dans l’étape de réunion partagée." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="8e268-322">À faire : faire défiler verticalement</span><span class="sxs-lookup"><span data-stu-id="8e268-322">Do: Scroll vertically</span></span>

<span data-ttu-id="8e268-323">Les utilisateurs s’attendent à ce que le défilement vertical Teams (et ailleurs).</span><span class="sxs-lookup"><span data-stu-id="8e268-323">Users expect vertical scrolling in Teams (and elsewhere).</span></span> <span data-ttu-id="8e268-324">Cela peut ne pas s’appliquer si vous avez un canevas créatif, tel qu’un tableau blanc, que les utilisateurs peuvent faire panoramique sur les axes x et y.</span><span class="sxs-lookup"><span data-stu-id="8e268-324">This may not apply if you have a creative canvas, such as a whiteboard, which users can pan across the x and y axis.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple de défilement horizontal dans un onglet de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Exemple de défilement horizontal dans l’étape de réunion partagée." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="8e268-327">À ne pas faire : faire défiler horizontalement</span><span class="sxs-lookup"><span data-stu-id="8e268-327">Don't: Scroll horizontally</span></span>

<span data-ttu-id="8e268-328">Le défilement horizontal n’est pas un comportement attendu dans Teams (y compris l’environnement de réunion).</span><span class="sxs-lookup"><span data-stu-id="8e268-328">Horizontal scrolling isn’t an expected behavior in Teams (including the meeting environment).</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="8e268-329">Flux de travail</span><span class="sxs-lookup"><span data-stu-id="8e268-329">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet de réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="8e268-331">À faire : surfacer des scénarios complexes dans l’onglet réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-331">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="8e268-332">Si votre application comprend plusieurs tâches, nous vous recommandons vivement d’utiliser un onglet de réunion avec une disposition sur une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="8e268-332">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple de scénarios complexes dans une boîte de dialogue en réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="8e268-334">À ne pas faire : rendre les boîtes de dialogue de réunion complexes</span><span class="sxs-lookup"><span data-stu-id="8e268-334">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="8e268-335">Les boîtes de dialogue en réunion sont conçues pour de brèves interactions.</span><span class="sxs-lookup"><span data-stu-id="8e268-335">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="8e268-336">Thèmes</span><span class="sxs-lookup"><span data-stu-id="8e268-336">Theming</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème foncé." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Autre exemple montrant l’extension de réunion avec le thème foncé." border="false":::

#### <a name="do-focus-on-dark-theme"></a><span data-ttu-id="8e268-339">À faire : concentrez-vous sur le thème foncé</span><span class="sxs-lookup"><span data-stu-id="8e268-339">Do: Focus on dark theme</span></span>

<span data-ttu-id="8e268-340">Teams réunions sont optimisées pour le thème foncé afin de réduire les bruits visuels et cognitifs afin que les utilisateurs peuvent se concentrer sur la discussion et le contenu partagé.</span><span class="sxs-lookup"><span data-stu-id="8e268-340">Teams meetings are optimized for dark theme to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="8e268-341">Gardez à l’esprit que certains types d’applications (par exemple, tableau blanc et modification de documents) n’ont pas besoin d’une zone de dessin sombre.</span><span class="sxs-lookup"><span data-stu-id="8e268-341">Keep in mind certain types of apps (such as whiteboarding and document editing) don't need a dark canvas.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec des couleurs qui ne correspondent pas au thème de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Autre exemple montrant une extension de réunion avec des couleurs qui ne correspondent pas au thème de la réunion." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="8e268-344">À ne pas faire : utiliser des couleurs inconnues</span><span class="sxs-lookup"><span data-stu-id="8e268-344">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="8e268-345">Les couleurs qui entrent en conflit avec l’environnement de réunion peuvent être gênantes et apparaître moins natives Teams.</span><span class="sxs-lookup"><span data-stu-id="8e268-345">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span> <span data-ttu-id="8e268-346">Découvrez la palette de couleurs [Teams,](https://developer.microsoft.com/fluentui#/styles/web/colors/products)y compris les neutres du thème d’appel.</span><span class="sxs-lookup"><span data-stu-id="8e268-346">Learn about the Teams [color ramp](https://developer.microsoft.com/fluentui#/styles/web/colors/products), including call theme neutrals.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="8e268-347">Navigation</span><span class="sxs-lookup"><span data-stu-id="8e268-347">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton Retour." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="8e268-349">À faire : avoir un bouton Retour</span><span class="sxs-lookup"><span data-stu-id="8e268-349">Do: Have a back button</span></span>

<span data-ttu-id="8e268-350">Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent pouvoir revenir à leurs vues précédentes.</span><span class="sxs-lookup"><span data-stu-id="8e268-350">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons d’mascmit." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="8e268-352">À ne pas faire : inclure un autre bouton d’arrêt</span><span class="sxs-lookup"><span data-stu-id="8e268-352">Don't: Include another dismiss button</span></span>

<span data-ttu-id="8e268-353">La fourniture d’une option pour fermer le contenu de l’onglet en réunion peut entraîner des problèmes, car l’en-tête ne doit pas être fermé par un bouton.</span><span class="sxs-lookup"><span data-stu-id="8e268-353">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modales (ou des modules de tâche) dans un onglet de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="8e268-355">Attention : évitez les modales dans l’onglet de la réunion</span><span class="sxs-lookup"><span data-stu-id="8e268-355">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="8e268-356">Les modaux (également appelés modules de tâche) dans l’onglet déjà étroit de la réunion peuvent encapsuler et masquer le contenu.</span><span class="sxs-lookup"><span data-stu-id="8e268-356">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a><span data-ttu-id="8e268-357">Comportement réactif</span><span class="sxs-lookup"><span data-stu-id="8e268-357">Responsive behavior</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Exemple montrant comment re tailler correctement une extension de réunion." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a><span data-ttu-id="8e268-359">À faire : resize and scale your app responsively</span><span class="sxs-lookup"><span data-stu-id="8e268-359">Do: Resize and scale your app responsively</span></span>

<span data-ttu-id="8e268-360">Le contenu de l’application doit être resserre et condensé dynamiquement dans des fenêtres plus petites.</span><span class="sxs-lookup"><span data-stu-id="8e268-360">App content should dynamically resize and condense in smaller windows.</span></span> <span data-ttu-id="8e268-361">Conservez la navigation principale de votre application et tous les contrôles flottants visibles.</span><span class="sxs-lookup"><span data-stu-id="8e268-361">Keep your app’s main navigation and any floating controls visible.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Exemple montrant comment ne pas re tailler correctement une extension de réunion." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a><span data-ttu-id="8e268-363">À ne pas faire : rognez ou clipez les composants principaux de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="8e268-363">Don't: Crop or clip primary UI components</span></span>

<span data-ttu-id="8e268-364">La navigation flottante et les contrôles hors écran et la nécessité d’un défilement à rechercher peuvent prêter à confusion pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8e268-364">Floating navigation and controls off screen and requiring a scroll to find can be confusing for users.</span></span> <span data-ttu-id="8e268-365">Le contenu de votre application ne doit pas défiler horizontalement lorsqu’il ne peut pas tenir dans l’iframe.</span><span class="sxs-lookup"><span data-stu-id="8e268-365">Your app content shouldn’t scroll horizontally when it can't fit in the iframe.</span></span>

   :::column-end:::
:::row-end:::

## <a name="next-step"></a><span data-ttu-id="8e268-366">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="8e268-366">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e268-367">Configurer votre application pour les réunions</span><span class="sxs-lookup"><span data-stu-id="8e268-367">Configure your app for meetings</span></span>](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
