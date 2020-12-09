---
title: Création d’un onglet pour le bureau et le Web
description: Découvrez comment concevoir un onglet Teams (de bureau et Web) et obtenir le kit d’interface utilisateur de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604670"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="0cdcd-103">Conception de votre onglet pour le bureau et le Web Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="0cdcd-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="0cdcd-104">Un onglet est un grand canevas pour le contenu qui facilite la collaboration.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-104">A tab is a large canvas for content that facilitates collaboration.</span></span> <span data-ttu-id="0cdcd-105">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les utilisateurs peuvent ajouter, utiliser et gérer des onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0cdcd-106">Kit d’interface utilisateur Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="0cdcd-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0cdcd-107">Vous trouverez des instructions détaillées sur la conception des onglets, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="0cdcd-108">Le kit d’interface utilisateur comporte également des rubriques essentielles, telles que l’accessibilité et le dimensionnement réactif, qui ne sont pas abordées ici.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cdcd-109">Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="0cdcd-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="0cdcd-110">Ajouter un onglet</span><span class="sxs-lookup"><span data-stu-id="0cdcd-110">Add a tab</span></span>

<span data-ttu-id="0cdcd-111">Vous pouvez ajouter un onglet à partir du magasin Teams (AppSource) ou dans l’un des contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="0cdcd-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="0cdcd-112">Conversation</span><span class="sxs-lookup"><span data-stu-id="0cdcd-112">Chat</span></span>
* <span data-ttu-id="0cdcd-113">Canal</span><span class="sxs-lookup"><span data-stu-id="0cdcd-113">Channel</span></span>
* <span data-ttu-id="0cdcd-114">Réunion (avant, pendant ou après la réunion)</span><span class="sxs-lookup"><span data-stu-id="0cdcd-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="0cdcd-115">L’exemple suivant montre comment un onglet est ajouté dans un canal.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Exemple illustre l’ajout d’un onglet à un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="0cdcd-117">Configurer un onglet</span><span class="sxs-lookup"><span data-stu-id="0cdcd-117">Set up a tab</span></span>

<span data-ttu-id="0cdcd-118">Il existe un petit processus de configuration pour ajouter une application sous la forme d’un onglet canal, conversation ou réunion. L’expérience est largement à votre place.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="0cdcd-119">Par exemple, vous pouvez avoir une description de l’utilisation de l’application et de certains paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="0cdcd-120">Incluez ici une étape de connexion si vous devez authentifier les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="0cdcd-121">Configuration de l’onglet modal</span><span class="sxs-lookup"><span data-stu-id="0cdcd-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple montre une configuration d’onglet modale." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="0cdcd-123">Anatomie : modal de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="0cdcd-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une configuration d’onglet modale." border="false":::

|<span data-ttu-id="0cdcd-125">Compteur</span><span class="sxs-lookup"><span data-stu-id="0cdcd-125">Counter</span></span>|<span data-ttu-id="0cdcd-126">Description</span><span class="sxs-lookup"><span data-stu-id="0cdcd-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0cdcd-127">1</span><span class="sxs-lookup"><span data-stu-id="0cdcd-127">1</span></span>|<span data-ttu-id="0cdcd-128">**Logo** de l’application : logo de l’application couleur complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="0cdcd-129">2 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-129">2</span></span>|<span data-ttu-id="0cdcd-130">**Nom** de l’application : nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="0cdcd-131">3 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-131">3</span></span>|<span data-ttu-id="0cdcd-132">**IFRAME**: espace réactif pour le contenu de votre application (par exemple, paramètres de tabulation ou authentification).</span><span class="sxs-lookup"><span data-stu-id="0cdcd-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="0cdcd-133">4 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-133">4</span></span>|<span data-ttu-id="0cdcd-134">**À propos de Link**: ouvre une boîte de dialogue affichant plus d’informations sur l’application, telle qu’une description complète, les autorisations requises par l’application, ainsi que des liens vers votre politique de confidentialité et les conditions de service.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="0cdcd-135">5 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-135">5</span></span>|<span data-ttu-id="0cdcd-136">**Bouton Fermer**: ferme le modal.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="0cdcd-137">6 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-137">6</span></span>|<span data-ttu-id="0cdcd-138">**Option de notification des membres** de l’équipe : le modal vous demande si vous souhaitez créer un billet indiquant que vous avez ajouté un onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="0cdcd-139">7 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-139">7</span></span>|<span data-ttu-id="0cdcd-140">**Bouton précédent**: passe à l’étape précédente en fonction de l’emplacement de la boîte de dialogue ouverte.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="0cdcd-141">8 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-141">8</span></span>|<span data-ttu-id="0cdcd-142">**Bouton enregistrer**: termine la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="0cdcd-143">Authentification de l’onglet avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="0cdcd-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="0cdcd-144">Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="0cdcd-145">Cette méthode d’authentification est appelée authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="0cdcd-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple affiche un écran d’authentification de tabulation." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="0cdcd-147">Conception d’une configuration d’onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="0cdcd-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="0cdcd-148">Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre configuration d’onglet :</span><span class="sxs-lookup"><span data-stu-id="0cdcd-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="0cdcd-149">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="0cdcd-150">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="0cdcd-151">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="0cdcd-152">Afficher un onglet</span><span class="sxs-lookup"><span data-stu-id="0cdcd-152">View a tab</span></span>

<span data-ttu-id="0cdcd-153">Les onglets fournissent une expérience Web en plein écran dans Teams, qui vous permet d’afficher du contenu collaboratif, ainsi que des tableaux de tâches et des tableaux de bord, ainsi que des informations importantes.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Exemple affiche un onglet avec un tableau des tâches." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="0cdcd-155">Anatomie : Tab</span><span class="sxs-lookup"><span data-stu-id="0cdcd-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|<span data-ttu-id="0cdcd-157">Compteur</span><span class="sxs-lookup"><span data-stu-id="0cdcd-157">Counter</span></span>|<span data-ttu-id="0cdcd-158">Description</span><span class="sxs-lookup"><span data-stu-id="0cdcd-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0cdcd-159">1</span><span class="sxs-lookup"><span data-stu-id="0cdcd-159">1</span></span>|<span data-ttu-id="0cdcd-160">**Nom** de l’onglet : étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="0cdcd-161">2 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-161">2</span></span>|<span data-ttu-id="0cdcd-162">**Débordement d’onglets**: ouvre les actions d’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="0cdcd-163">3 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-163">3</span></span>|<span data-ttu-id="0cdcd-164">**Conversation par onglets**: ouvre un fil de conversation sur la droite, ce qui permet aux utilisateurs de disposer d’une conversation en regard du contenu.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="0cdcd-165">4 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-165">4</span></span>|<span data-ttu-id="0cdcd-166">**IFRAME**: affiche le contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="0cdcd-167">Création d’un onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="0cdcd-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="0cdcd-168">Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre onglet :</span><span class="sxs-lookup"><span data-stu-id="0cdcd-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="0cdcd-169">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="0cdcd-170">[Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board): un tableau des tâches, parfois appelé tableau kanban ou couloirs de natation, est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="0cdcd-171">[Tableau](../../concepts/design/design-teams-app-ui-templates.md#dashboard)de bord : un tableau de bord est une zone de dessin contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="0cdcd-172">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="0cdcd-173">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="0cdcd-174">Navigation de [gauche](../../concepts/design/design-teams-app-ui-templates.md#left-nav): le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="0cdcd-175">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="0cdcd-176">Utiliser un onglet pour collaborer</span><span class="sxs-lookup"><span data-stu-id="0cdcd-176">Use a tab to collaborate</span></span>

<span data-ttu-id="0cdcd-177">Les onglets aident à faciliter les conversations sur le contenu à un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="0cdcd-178">Discussion de thread</span><span class="sxs-lookup"><span data-stu-id="0cdcd-178">Thread discussion</span></span>

<span data-ttu-id="0cdcd-179">Les utilisateurs peuvent automatiquement effectuer des publications sur un canal ou une conversation une fois qu’ils ont ajouté un nouvel onglet. Cette opération indique non seulement les membres de l’équipe du nouveau contenu et fournit un lien vers l’onglet, mais permet aux utilisateurs de commencer à parler de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Exemple montre un onglet discuté dans un thread de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="0cdcd-181">Discussion côte à côte</span><span class="sxs-lookup"><span data-stu-id="0cdcd-181">Side-by-side discussion</span></span>

<span data-ttu-id="0cdcd-182">Les utilisateurs peuvent avoir une conversation lors de l’affichage du contenu de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Exemple affiche un onglet avec une conversation ouverte sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="0cdcd-184">Autorisations et vues basées sur les rôles</span><span class="sxs-lookup"><span data-stu-id="0cdcd-184">Permissions and role-based views</span></span>

<span data-ttu-id="0cdcd-185">L’expérience utilisateur peut être différente pour les utilisateurs en fonction de leurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="0cdcd-186">Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="0cdcd-187">Toutefois, un autre utilisateur doit se connecter et afficher un contenu légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="0cdcd-188">Gérer un onglet</span><span class="sxs-lookup"><span data-stu-id="0cdcd-188">Manage a tab</span></span>

<span data-ttu-id="0cdcd-189">Vous pouvez inclure des options permettant de renommer, de supprimer ou de modifier un onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="0cdcd-190">Anatomie : menu de l’onglet</span><span class="sxs-lookup"><span data-stu-id="0cdcd-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’un menu d’onglets." border="false":::

|<span data-ttu-id="0cdcd-192">Compteur</span><span class="sxs-lookup"><span data-stu-id="0cdcd-192">Counter</span></span>|<span data-ttu-id="0cdcd-193">Description</span><span class="sxs-lookup"><span data-stu-id="0cdcd-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0cdcd-194">1</span><span class="sxs-lookup"><span data-stu-id="0cdcd-194">1</span></span>|<span data-ttu-id="0cdcd-195">**Paramètres**: (facultatif) permet aux utilisateurs de modifier les paramètres d’un onglet après qu’il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="0cdcd-196">2 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-196">2</span></span>|<span data-ttu-id="0cdcd-197">**Rename**: permet aux utilisateurs d’attribuer un nom plus significatif à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="0cdcd-198">3 </span><span class="sxs-lookup"><span data-stu-id="0cdcd-198">3</span></span>|<span data-ttu-id="0cdcd-199">**Supprimer**: supprime l’onglet du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="0cdcd-200">Notifications de tabulation et liens détaillés</span><span class="sxs-lookup"><span data-stu-id="0cdcd-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="0cdcd-201">Vous pouvez envoyer un message avec un lien détaillé vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour afficher l’intégralité du bogue dans un onglet. L’envoi de messages sur l’activité des onglets augmente la sensibilisation sans notification explicite à tous les utilisateurs (c.-à-d., activité sans bruit).</span><span class="sxs-lookup"><span data-stu-id="0cdcd-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="0cdcd-202">Vous pouvez également @mention des utilisateurs spécifiques, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="0cdcd-203">Avertissez les utilisateurs de l’activité des onglets de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="0cdcd-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="0cdcd-204">**Bot**: cette méthode est préférée en particulier si le thread d’onglet est ciblé.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="0cdcd-205">La conversation de thème de l’onglet est déplacée vers le mode récemment actif.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="0cdcd-206">Cette méthode permet également une sophistication du mode d’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="0cdcd-207">**Message**: un message s’affiche dans le flux d’activités de l’utilisateur avec un [lien détaillé vers l’onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0cdcd-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="0cdcd-208">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="0cdcd-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="0cdcd-209">Collaboration</span><span class="sxs-lookup"><span data-stu-id="0cdcd-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Illustration illustrant la marche à suivre pour la conception de la navigation par onglets." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="0cdcd-211">Do : faciliter la conversation</span><span class="sxs-lookup"><span data-stu-id="0cdcd-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="0cdcd-212">Inclure le contenu et les composants que les utilisateurs peuvent parler.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-212">Include content and components people can talk about.</span></span> <span data-ttu-id="0cdcd-213">S’il ne rentre pas dans le contexte d’une conversation, d’un canal ou d’une réunion, il n’appartient pas à votre onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la navigation par onglet." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="0cdcd-215">Ne pas : traiter votre onglet comme n’importe quelle autre page Web</span><span class="sxs-lookup"><span data-stu-id="0cdcd-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="0cdcd-216">Un onglet n’est pas une page Web qui peut s’afficher une seule fois.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="0cdcd-217">Un onglet doit afficher votre contenu le plus important et pertinent dont les utilisateurs ont besoin pour effectuer une tâche conjointe.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="0cdcd-218">Navigation</span><span class="sxs-lookup"><span data-stu-id="0cdcd-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Illustration illustrant la marche à suivre pour la conception de la navigation par onglets." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="0cdcd-220">Do : limiter les tâches et les données</span><span class="sxs-lookup"><span data-stu-id="0cdcd-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="0cdcd-221">Les onglets fonctionnent mieux lorsqu’ils répondent à des besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="0cdcd-222">Incluez un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la navigation par onglet." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="0cdcd-224">Ne pas : incorporer votre application entière</span><span class="sxs-lookup"><span data-stu-id="0cdcd-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="0cdcd-225">L’utilisation d’un onglet pour afficher une application entière avec une navigation à plusieurs niveaux et des interactions complexes entraîne une surcharge d’informations.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="0cdcd-226">Configuration</span><span class="sxs-lookup"><span data-stu-id="0cdcd-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration illustrant les actions à effectuer avec la conception de la configuration de l’onglet." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="0cdcd-228">Do : restez simple</span><span class="sxs-lookup"><span data-stu-id="0cdcd-228">Do: Keep it simple</span></span>

<span data-ttu-id="0cdcd-229">Si votre application requiert une authentification, essayez d’intégrer Microsoft Single Sign-On (SSO) pour une expérience de connexion plus transparente.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="0cdcd-230">En outre, n’incluez que les informations essentielles et les étapes à suivre pour ajouter l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="0cdcd-232">Ne pas faire : trop d’étapes</span><span class="sxs-lookup"><span data-stu-id="0cdcd-232">Don't: Have too many steps</span></span>

<span data-ttu-id="0cdcd-233">Supprimez toutes les étapes inutiles pour l’ajout d’un onglet.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="0cdcd-234">Thèmes</span><span class="sxs-lookup"><span data-stu-id="0cdcd-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration illustrant la procédure d’affichage des onglets." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="0cdcd-236">Do : tirer parti des jetons de couleur teams</span><span class="sxs-lookup"><span data-stu-id="0cdcd-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="0cdcd-237">Chaque thème teams possède son propre jeu de couleurs.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="0cdcd-238">Pour gérer automatiquement les modifications de thème, utilisez des <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">jetons de couleur (IU Fluent)</a> dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration illustrant ce qu’il ne faut pas faire avec des tabulations." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="0cdcd-240">Ne pas : valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="0cdcd-240">Don't: Hard code color values</span></span>

<span data-ttu-id="0cdcd-241">Si vous n’utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prendre plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="0cdcd-242">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="0cdcd-242">Validate your design</span></span>

<span data-ttu-id="0cdcd-243">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="0cdcd-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cdcd-244">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="0cdcd-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
