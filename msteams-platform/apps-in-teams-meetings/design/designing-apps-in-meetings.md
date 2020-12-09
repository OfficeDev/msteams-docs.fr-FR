---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans des réunions teams et obtenir le kit d’interface utilisateur Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606133"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="ae160-103">Conception de votre extension de réunion Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="ae160-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="ae160-104">Vous pouvez créer des applications pour améliorer la productivité des réunions.</span><span class="sxs-lookup"><span data-stu-id="ae160-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="ae160-105">Par exemple, demandez aux personnes de finaliser une enquête pendant un appel ou envoyez un rappel rapide qui n’interrompt pas le flux de la réunion.</span><span class="sxs-lookup"><span data-stu-id="ae160-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ae160-106">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="ae160-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ae160-107">Vous trouverez des instructions de conception plus complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ae160-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae160-108">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="ae160-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="ae160-109">Ajouter une extension de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-109">Add a meeting extension</span></span>

<span data-ttu-id="ae160-110">Vous pouvez ajouter une extension de réunion avant et Pendant des réunions.</span><span class="sxs-lookup"><span data-stu-id="ae160-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="ae160-111">Vous pouvez également une application pour une réunion spécifique directement à partir du magasin de Teams (AppSource).</span><span class="sxs-lookup"><span data-stu-id="ae160-111">You also can an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="ae160-112">Ajouter avant une réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-112">Add before a meeting</span></span>

<span data-ttu-id="ae160-113">Avant une réunion, les détails de la réunion sélectionnent **Ajouter un onglet +** pour ouvrir le menu volant d’application et Rechercher des applications optimisées pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="ae160-113">Before a meeting, the meeting details select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="ae160-115">Ajouter pendant une réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-115">Add during a meeting</span></span>

Dans une réunion, sélectionnez **plus** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Ajouter une application** et choisissez l’application de votre choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion pendant une réunion." border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="ae160-118">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-118">Before a meeting</span></span>

<span data-ttu-id="ae160-119">Avant la réunion, vous pouvez ajouter du contenu dans l’onglet. L’exemple suivant montre une question d’enquête préliminaire à laquelle les personnes répondront pendant l’appel.</span><span class="sxs-lookup"><span data-stu-id="ae160-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Exemple montre comment afficher du contenu dans les détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="ae160-121">Anatomie : onglet réunion (avant et après les réunions)</span><span class="sxs-lookup"><span data-stu-id="ae160-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|<span data-ttu-id="ae160-123">Compteur</span><span class="sxs-lookup"><span data-stu-id="ae160-123">Counter</span></span>|<span data-ttu-id="ae160-124">Description</span><span class="sxs-lookup"><span data-stu-id="ae160-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ae160-125">1</span><span class="sxs-lookup"><span data-stu-id="ae160-125">1</span></span>|<span data-ttu-id="ae160-126">**Nom** de l’onglet : étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ae160-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="ae160-127">2 </span><span class="sxs-lookup"><span data-stu-id="ae160-127">2</span></span>|<span data-ttu-id="ae160-128">**Débordement d’onglets**: ouvre les actions d’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="ae160-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="ae160-129">3 </span><span class="sxs-lookup"><span data-stu-id="ae160-129">3</span></span>|<span data-ttu-id="ae160-130">**IFRAME**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ae160-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="ae160-131">Conception avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ae160-131">Designing with UI templates</span></span>

<span data-ttu-id="ae160-132">Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre onglet réunion :</span><span class="sxs-lookup"><span data-stu-id="ae160-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="ae160-133">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="ae160-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="ae160-134">[Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board): un tableau des tâches, parfois appelé tableau kanban ou couloirs de natation, est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="ae160-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="ae160-135">[Tableau](../../concepts/design/design-teams-app-ui-templates.md#dashboard)de bord : un tableau de bord est une zone de dessin contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="ae160-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="ae160-136">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="ae160-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="ae160-137">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="ae160-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="ae160-138">Navigation de [gauche](../../concepts/design/design-teams-app-ui-templates.md#left-nav): le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="ae160-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="ae160-139">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="ae160-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="ae160-140">Utiliser un onglet de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-140">Use an in-meeting tab</span></span>

<span data-ttu-id="ae160-141">L’onglet dans la réunion est un canevas permettant d’augmenter la collaboration pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="ae160-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="ae160-142">Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion via des affichages partagés ou basés sur des rôles.</span><span class="sxs-lookup"><span data-stu-id="ae160-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="ae160-143">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="ae160-143">Use cases</span></span>

<span data-ttu-id="ae160-144">Les utilisateurs peuvent utiliser l’onglet dans la réunion pour :</span><span class="sxs-lookup"><span data-stu-id="ae160-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="ae160-145">Fournir des commentaires détaillés (par exemple, évaluer un candidat de travail)</span><span class="sxs-lookup"><span data-stu-id="ae160-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="ae160-146">Créer rapidement un élément de sondage, d’enquête ou de tâche pour les participants à la réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="ae160-147">Afficher les notes relatives à la réunion (par exemple, informations sur un prospect)</span><span class="sxs-lookup"><span data-stu-id="ae160-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Cet exemple montre comment vous pouvez présenter du contenu de sondage dans un onglet de réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="ae160-149">Anatomie : onglet sous-réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un onglet de réunion." border="false":::

|<span data-ttu-id="ae160-151">Compteur</span><span class="sxs-lookup"><span data-stu-id="ae160-151">Counter</span></span>|<span data-ttu-id="ae160-152">Description</span><span class="sxs-lookup"><span data-stu-id="ae160-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ae160-153">1</span><span class="sxs-lookup"><span data-stu-id="ae160-153">1</span></span>|<span data-ttu-id="ae160-154">**Icône de l’application (sélectionnée)**: logo de l’application transparente 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="ae160-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="ae160-155">2 </span><span class="sxs-lookup"><span data-stu-id="ae160-155">2</span></span>|<span data-ttu-id="ae160-156">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="ae160-156">**App name**</span></span>|
|<span data-ttu-id="ae160-157">3 </span><span class="sxs-lookup"><span data-stu-id="ae160-157">3</span></span>|<span data-ttu-id="ae160-158">**En-tête**: inclut le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="ae160-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="ae160-159">4 </span><span class="sxs-lookup"><span data-stu-id="ae160-159">4</span></span>|<span data-ttu-id="ae160-160">**Bouton Fermer : ferme** l’onglet. Toujours utiliser l’icône fermer en haut à droite au lieu d’une action dans le pied de page.</span><span class="sxs-lookup"><span data-stu-id="ae160-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="ae160-161">5 </span><span class="sxs-lookup"><span data-stu-id="ae160-161">5</span></span>|<span data-ttu-id="ae160-162">**Barre de notification**: les alertes d’erreur s’affichent directement sous l’en-tête et redescendent le contenu iframe de 20 pixels.</span><span class="sxs-lookup"><span data-stu-id="ae160-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="ae160-163">6 </span><span class="sxs-lookup"><span data-stu-id="ae160-163">6</span></span>|<span data-ttu-id="ae160-164">**IFRAME**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ae160-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="ae160-165">Espacement</span><span class="sxs-lookup"><span data-stu-id="ae160-165">Spacing</span></span>

<span data-ttu-id="ae160-166">Optimisez votre onglet de réunion pour qu’il s’ajuste au bord de la zone iframe de 280 pixels.</span><span class="sxs-lookup"><span data-stu-id="ae160-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="ae160-167">Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’IFRAME et entre l’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="ae160-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="ae160-168">L’iframe est un fond perdu en bas de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="ae160-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Exemple affiche les dimensions d’espacement des tabulations dans la réunion." border="false":::

### <a name="scrolling"></a><span data-ttu-id="ae160-170">Défilement</span><span class="sxs-lookup"><span data-stu-id="ae160-170">Scrolling</span></span>

<span data-ttu-id="ae160-171">Le contenu d’un IFRAME doit faire défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="ae160-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="ae160-172">Vous ne pouvez voir que le contenu auquel vous avez fait défiler (rien au-dessus ou en dessous).</span><span class="sxs-lookup"><span data-stu-id="ae160-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="ae160-173">La barre de défilement fait partie du contenu IFRAME.</span><span class="sxs-lookup"><span data-stu-id="ae160-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Cet exemple montre comment faire défiler l’onglet de réunion." border="false":::

### <a name="navigation"></a><span data-ttu-id="ae160-175">Navigation</span><span class="sxs-lookup"><span data-stu-id="ae160-175">Navigation</span></span>

<span data-ttu-id="ae160-176">Pour les scénarios avec des calques de navigation ou du contenu lourd, il est recommandé d’autoriser les utilisateurs à accéder à un calque secondaire.</span><span class="sxs-lookup"><span data-stu-id="ae160-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="ae160-177">Les utilisateurs doivent pouvoir revenir à la couche précédente.</span><span class="sxs-lookup"><span data-stu-id="ae160-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple illustre la navigation dans la réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="ae160-179">Utiliser une boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="ae160-180">Les boîtes de dialogue de réunion sont affichées à l’étape de réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="ae160-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="ae160-181">Elles requièrent l’attention, la confirmation ou l’interaction d’un utilisateur, mais elles sont subtiles et n’interrompent pas la réunion.</span><span class="sxs-lookup"><span data-stu-id="ae160-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="ae160-182">Vous devez les utiliser avec modération et pour les scénarios orientés sur les tâches et la lumière.</span><span class="sxs-lookup"><span data-stu-id="ae160-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="ae160-183">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="ae160-183">Use cases</span></span>

<span data-ttu-id="ae160-184">Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (par exemple, l’organisateur de la réunion) qui peut souhaiter que les participants :</span><span class="sxs-lookup"><span data-stu-id="ae160-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="ae160-185">Fournir des commentaires succincts</span><span class="sxs-lookup"><span data-stu-id="ae160-185">Provide brief feedback</span></span>
* <span data-ttu-id="ae160-186">Suivre une brève enquête ou sondage</span><span class="sxs-lookup"><span data-stu-id="ae160-186">Take a short survey or poll</span></span>
* <span data-ttu-id="ae160-187">Soumettre des approbations</span><span class="sxs-lookup"><span data-stu-id="ae160-187">Submit approvals</span></span>
* <span data-ttu-id="ae160-188">Obtenir les rappels</span><span class="sxs-lookup"><span data-stu-id="ae160-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Exemple vous montre comment utiliser une boîte de dialogue de réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="ae160-190">Anatomie : boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’une boîte de dialogue de réunion." border="false":::

|<span data-ttu-id="ae160-192">Compteur</span><span class="sxs-lookup"><span data-stu-id="ae160-192">Counter</span></span>|<span data-ttu-id="ae160-193">Description</span><span class="sxs-lookup"><span data-stu-id="ae160-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ae160-194">1</span><span class="sxs-lookup"><span data-stu-id="ae160-194">1</span></span>|<span data-ttu-id="ae160-195">**En-tête**: inclut l’icône de l’application, le nom, la chaîne d’action et l’icône fermer.</span><span class="sxs-lookup"><span data-stu-id="ae160-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="ae160-196">2 </span><span class="sxs-lookup"><span data-stu-id="ae160-196">2</span></span>|<span data-ttu-id="ae160-197">**IFRAME**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ae160-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="ae160-198">Anatomie : en-tête de boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un en-tête de boîte de dialogue de réunion." border="false":::

<span data-ttu-id="ae160-200">Il existe deux variantes d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="ae160-200">There are two header variants.</span></span> <span data-ttu-id="ae160-201">Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer le fait que la boîte de dialogue provient d’une personne.</span><span class="sxs-lookup"><span data-stu-id="ae160-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="ae160-202">Compteur</span><span class="sxs-lookup"><span data-stu-id="ae160-202">Counter</span></span>|<span data-ttu-id="ae160-203">Description</span><span class="sxs-lookup"><span data-stu-id="ae160-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="ae160-204">1</span><span class="sxs-lookup"><span data-stu-id="ae160-204">1</span></span>|<span data-ttu-id="ae160-205">**Avatar**: personne qui lance la boîte de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="ae160-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="ae160-206">2 </span><span class="sxs-lookup"><span data-stu-id="ae160-206">2</span></span>|<span data-ttu-id="ae160-207">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="ae160-207">**App icon**</span></span>|
|<span data-ttu-id="ae160-208">3 </span><span class="sxs-lookup"><span data-stu-id="ae160-208">3</span></span>|<span data-ttu-id="ae160-209">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="ae160-209">**App name**</span></span>|
|<span data-ttu-id="ae160-210">4 </span><span class="sxs-lookup"><span data-stu-id="ae160-210">4</span></span>|<span data-ttu-id="ae160-211">**Bouton Fermer : ferme** la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae160-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="ae160-212">5 </span><span class="sxs-lookup"><span data-stu-id="ae160-212">5</span></span>|<span data-ttu-id="ae160-213">**Chaîne d’action**: indique généralement qui a initié la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae160-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="ae160-214">Comportement réactif</span><span class="sxs-lookup"><span data-stu-id="ae160-214">Responsive behavior</span></span>

<span data-ttu-id="ae160-215">Les boîtes de dialogue de réunion peuvent varier en fonction de la taille pour tenir compte de différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="ae160-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="ae160-216">Veillez à maintenir les tailles de remplissage et de composant.</span><span class="sxs-lookup"><span data-stu-id="ae160-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="ae160-217">**Width**: la largeur de l’iframe est une valeur absolue comprise dans la plage que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="ae160-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="ae160-218">**Height**: la hauteur de la boîte de dialogue est déterminée par le contenu de l’IFRAME.</span><span class="sxs-lookup"><span data-stu-id="ae160-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="ae160-219">Le défilement vertical est pris en charge pour le contenu qui dépasse la hauteur maximale.</span><span class="sxs-lookup"><span data-stu-id="ae160-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple affiche la boîte de dialogue de réunion. Width : min--280 pixels (248 pixels IFRAME). Max--460 pixels (428 pixels IFRAME). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="ae160-221">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-221">After a meeting</span></span>

<span data-ttu-id="ae160-222">Vous pouvez revenir à une réunion une fois qu’elle a terminé et affiché le contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="ae160-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="ae160-223">Dans cet exemple, l’organisateur de la réunion peut consulter les résultats de la recherche dans l’onglet **contoso** . (Remarque : du point de vue de la conception, il n’y a pas de différence entre les onglets pré-et post-réunion.)</span><span class="sxs-lookup"><span data-stu-id="ae160-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="Exemple montre un onglet post-réunion." border="false":::

## <a name="best-practices"></a><span data-ttu-id="ae160-225">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="ae160-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="ae160-226">Leurs</span><span class="sxs-lookup"><span data-stu-id="ae160-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="ae160-228">Do : limiter le nombre d’interactions</span><span class="sxs-lookup"><span data-stu-id="ae160-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="ae160-229">Pour les boîtes de dialogue de réunion, supprimez le contenu inutile qui ne permet pas aux utilisateurs d’effectuer une tâche rapidement.</span><span class="sxs-lookup"><span data-stu-id="ae160-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="ae160-231">Ne pas faire : introduire des éléments inutiles</span><span class="sxs-lookup"><span data-stu-id="ae160-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="ae160-232">Une seule boîte de dialogue de réunion avec plusieurs interactions peut gêner l’appel.</span><span class="sxs-lookup"><span data-stu-id="ae160-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="ae160-233">Disposition</span><span class="sxs-lookup"><span data-stu-id="ae160-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="ae160-235">Do : utiliser des mises en page à une seule colonne</span><span class="sxs-lookup"><span data-stu-id="ae160-235">Do: Use single-column layouts</span></span>

<span data-ttu-id="ae160-236">Étant donné que les boîtes de dialogue sont au centre de l’étape de la réunion, l’exécution de la tâche doit être rapide et simple pour éviter toute frustration des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ae160-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="ae160-238">Ne pas : emcombrer l’espace</span><span class="sxs-lookup"><span data-stu-id="ae160-238">Don't: Clutter the space</span></span>

<span data-ttu-id="ae160-239">Le contenu dense ou très structuré peut être gênant et écrasant, en particulier lors d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="ae160-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-use-single-columns"></a><span data-ttu-id="ae160-241">Do : utiliser des colonnes uniques</span><span class="sxs-lookup"><span data-stu-id="ae160-241">Do: Use single columns</span></span>

<span data-ttu-id="ae160-242">Étant donné la nature étroite de l’onglet dans la réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="ae160-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="ae160-244">Ne pas : utiliser plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="ae160-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="ae160-245">En raison de l’espace limité de l’onglet dans la réunion, les mises en page comportant plusieurs colonnes ne sont pas recommandées.</span><span class="sxs-lookup"><span data-stu-id="ae160-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="ae160-246">Contrôles</span><span class="sxs-lookup"><span data-stu-id="ae160-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="ae160-248">Do : aligner à droite l’action principale</span><span class="sxs-lookup"><span data-stu-id="ae160-248">Do: Right align the primary action</span></span>

<span data-ttu-id="ae160-249">Nous vous recommandons de positioining l’action la plus intense à l’emplacement le plus à droite.</span><span class="sxs-lookup"><span data-stu-id="ae160-249">We recommend positioining the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="ae160-251">Ne pas : Left ou Center align actions</span><span class="sxs-lookup"><span data-stu-id="ae160-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="ae160-252">Cela diffère du modèle standard teams pour le positionnement du contrôle dans une boîte de dialogue et peut entrer en conflit avec une boîte de dialogue située en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="ae160-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="ae160-253">Faire défiler</span><span class="sxs-lookup"><span data-stu-id="ae160-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="ae160-255">Do : faites défiler verticalement</span><span class="sxs-lookup"><span data-stu-id="ae160-255">Do: Scroll vertically</span></span>

<span data-ttu-id="ae160-256">Nous vous recommandons de placer l’action la plus intense à l’emplacement le plus à droite.</span><span class="sxs-lookup"><span data-stu-id="ae160-256">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="ae160-258">Ne pas faire défiler horizontalement</span><span class="sxs-lookup"><span data-stu-id="ae160-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="ae160-259">Le défilement horizontal n’est pas un comportement attendu dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ae160-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="ae160-260">Les autres canevas dans l’environnement de réunion sont déroulants verticalement.</span><span class="sxs-lookup"><span data-stu-id="ae160-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="ae160-261">Flux de travail</span><span class="sxs-lookup"><span data-stu-id="ae160-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="ae160-263">Do : scénarios de surface complexe dans l’onglet de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="ae160-264">Si votre application inclut plusieurs tâches, nous vous recommandons vivement d’utiliser une disposition sur une seule colonne dans un onglet de réunion.</span><span class="sxs-lookup"><span data-stu-id="ae160-264">If your app includes multiple tasks, we strongly recommend a single-column layout in an in-meeting tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a><span data-ttu-id="ae160-266">Ne pas : créer un package de scénarios complexes dans la boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-266">Don't: Package complex scenarios in the in-meeting dialog</span></span>

<span data-ttu-id="ae160-267">Les boîtes de dialogue de réunion sont destinées à de brèves interactions.</span><span class="sxs-lookup"><span data-stu-id="ae160-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="ae160-268">Thèmes</span><span class="sxs-lookup"><span data-stu-id="ae160-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="ae160-270">Do : utiliser des jetons de couleur teams</span><span class="sxs-lookup"><span data-stu-id="ae160-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="ae160-271">Les réunions de teams sont optimisées pour le mode sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé.</span><span class="sxs-lookup"><span data-stu-id="ae160-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="ae160-272">En savoir plus sur l’utilisation <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de jetons de couleur (interface utilisateur Fluent)</a>.</span><span class="sxs-lookup"><span data-stu-id="ae160-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="ae160-274">Ne pas inclure un autre bouton ignorer</span><span class="sxs-lookup"><span data-stu-id="ae160-274">Don't: Include another dismiss button</span></span>

<span data-ttu-id="ae160-275">La fourniture d’une option permettant de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car il existe déjà un bouton dans l’en-tête pour faire disparaître l’onglet de réunion lui-même.</span><span class="sxs-lookup"><span data-stu-id="ae160-275">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="ae160-276">Navigation</span><span class="sxs-lookup"><span data-stu-id="ae160-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="ae160-278">Do : avoir un bouton retour</span><span class="sxs-lookup"><span data-stu-id="ae160-278">Do: Have a back button</span></span>

<span data-ttu-id="ae160-279">Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent pouvoir revenir à leurs vues précédentes.</span><span class="sxs-lookup"><span data-stu-id="ae160-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="ae160-281">Ne pas inclure un autre bouton ignorer</span><span class="sxs-lookup"><span data-stu-id="ae160-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="ae160-282">La fourniture d’une option permettant de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car il existe déjà un bouton dans l’en-tête pour faire disparaître l’onglet de réunion lui-même.</span><span class="sxs-lookup"><span data-stu-id="ae160-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="ae160-284">ATTENTION : Évitez les éléments modaux au sein de l’onglet de réunion</span><span class="sxs-lookup"><span data-stu-id="ae160-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="ae160-285">Les modaux (également appelés modules de tâches) dans l’onglet de la réunion déjà étroite peuvent encapsuler et obscurcir le contenu.</span><span class="sxs-lookup"><span data-stu-id="ae160-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="ae160-286">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="ae160-286">Validate your design</span></span>

<span data-ttu-id="ae160-287">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="ae160-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae160-288">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="ae160-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
