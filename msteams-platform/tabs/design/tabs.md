---
title: Conception de votre onglet pour le bureau et le web
description: Découvrez comment concevoir un onglet Teams (bureau et web) et obtenir le Kit d'interface utilisateur Microsoft Teams.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 840cb9f65f867358615ea006594433d8a1099111
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019684"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="72c6e-103">Conception de votre onglet pour le bureau et le web Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="72c6e-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="72c6e-104">Un onglet est un canevas de grande taille pour votre contenu.</span><span class="sxs-lookup"><span data-stu-id="72c6e-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="72c6e-105">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="72c6e-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="72c6e-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="72c6e-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="72c6e-107">Vous trouverez des recommandations complètes en matière de conception d'onglets, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface utilisateur Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="72c6e-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="72c6e-108">Le kit d'interface utilisateur contient également des rubriques essentielles telles que l'accessibilité et le resserrement réactif qui ne sont pas abordés ici.</span><span class="sxs-lookup"><span data-stu-id="72c6e-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72c6e-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="72c6e-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="72c6e-110">Ajouter un onglet</span><span class="sxs-lookup"><span data-stu-id="72c6e-110">Add a tab</span></span>

<span data-ttu-id="72c6e-111">Vous pouvez ajouter un onglet à partir du magasin Teams (AppSource) ou dans l'un des contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="72c6e-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="72c6e-112">Conversation</span><span class="sxs-lookup"><span data-stu-id="72c6e-112">Chat</span></span>
* <span data-ttu-id="72c6e-113">Canal</span><span class="sxs-lookup"><span data-stu-id="72c6e-113">Channel</span></span>
* <span data-ttu-id="72c6e-114">Réunion (avant, pendant ou après la réunion)</span><span class="sxs-lookup"><span data-stu-id="72c6e-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="72c6e-115">L'exemple suivant montre comment un onglet est ajouté dans un canal.</span><span class="sxs-lookup"><span data-stu-id="72c6e-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="L'exemple montre comment ajouter un onglet dans un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="72c6e-117">Configurer un onglet</span><span class="sxs-lookup"><span data-stu-id="72c6e-117">Set up a tab</span></span>

<span data-ttu-id="72c6e-118">Il existe un processus de configuration court pour ajouter une application en tant que canal, conversation ou onglet de réunion. C'est en grande partie à vous de faire l'expérience.</span><span class="sxs-lookup"><span data-stu-id="72c6e-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="72c6e-119">Par exemple, vous pouvez avoir une description de l'utilisation de l'application et certains paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="72c6e-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="72c6e-120">Incluez une étape de connectez-vous ici si vous devez authentifier les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="72c6e-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="72c6e-121">Tab configuration modal</span><span class="sxs-lookup"><span data-stu-id="72c6e-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple de configuration modale d'onglet." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="72c6e-123">Anatomie : modal de configuration de l'onglet</span><span class="sxs-lookup"><span data-stu-id="72c6e-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un modèle de configuration d'onglet." border="false":::

|<span data-ttu-id="72c6e-125">Compteur</span><span class="sxs-lookup"><span data-stu-id="72c6e-125">Counter</span></span>|<span data-ttu-id="72c6e-126">Description</span><span class="sxs-lookup"><span data-stu-id="72c6e-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="72c6e-127">1</span><span class="sxs-lookup"><span data-stu-id="72c6e-127">1</span></span>|<span data-ttu-id="72c6e-128">**Logo de l'application**: logo d'application en couleur complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="72c6e-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="72c6e-129">2</span><span class="sxs-lookup"><span data-stu-id="72c6e-129">2</span></span>|<span data-ttu-id="72c6e-130">**Nom de l'application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="72c6e-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="72c6e-131">3</span><span class="sxs-lookup"><span data-stu-id="72c6e-131">3</span></span>|<span data-ttu-id="72c6e-132">**iframe**: espace réactif pour le contenu de votre application (par exemple, paramètres d'onglet ou authentification).</span><span class="sxs-lookup"><span data-stu-id="72c6e-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="72c6e-133">4 </span><span class="sxs-lookup"><span data-stu-id="72c6e-133">4</span></span>|<span data-ttu-id="72c6e-134">**À** propos du lien : ouvre une boîte de dialogue affichant plus d'informations sur l'application, telles qu'une description complète, les autorisations requises par l'application et des liens vers votre politique de confidentialité et les conditions d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="72c6e-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="72c6e-135">5 </span><span class="sxs-lookup"><span data-stu-id="72c6e-135">5</span></span>|<span data-ttu-id="72c6e-136">**Bouton Fermer**: ferme la modale.</span><span class="sxs-lookup"><span data-stu-id="72c6e-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="72c6e-137">6 </span><span class="sxs-lookup"><span data-stu-id="72c6e-137">6</span></span>|<span data-ttu-id="72c6e-138">**Option Avertir les membres de l'équipe**: la modale vous demande si vous souhaitez créer un billet pour informer d'autres utilisateurs que vous avez ajouté un onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="72c6e-139">7 </span><span class="sxs-lookup"><span data-stu-id="72c6e-139">7</span></span>|<span data-ttu-id="72c6e-140">**Bouton Précédent**: passe à l'étape précédente en fonction de l'endroit où la boîte de dialogue s'est ouverte.</span><span class="sxs-lookup"><span data-stu-id="72c6e-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="72c6e-141">8 </span><span class="sxs-lookup"><span data-stu-id="72c6e-141">8</span></span>|<span data-ttu-id="72c6e-142">**Bouton Enregistrer :** termine la configuration de l'onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="72c6e-143">Authentification par onglet avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="72c6e-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="72c6e-144">Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d'abord se connecter avec leurs informations d'identification Microsoft.</span><span class="sxs-lookup"><span data-stu-id="72c6e-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="72c6e-145">Cette méthode d'authentification est appelée authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="72c6e-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple d'écran d'authentification par onglet." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="72c6e-147">Conception d'une configuration d'onglet avec des modèles d'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="72c6e-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="72c6e-148">Utilisez l'un des modèles d'interface utilisateur Teams suivants pour vous aider à concevoir votre expérience de configuration d'onglet :</span><span class="sxs-lookup"><span data-stu-id="72c6e-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="72c6e-149">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="72c6e-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="72c6e-150">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="72c6e-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="72c6e-151">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="72c6e-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="72c6e-152">Afficher un onglet</span><span class="sxs-lookup"><span data-stu-id="72c6e-152">View a tab</span></span>

<span data-ttu-id="72c6e-153">Les onglets offrent une expérience web en plein écran dans Teams dans laquelle vous pouvez afficher du contenu collaboratif (tableaux de tâches et tableaux de bord, par exemple) et des informations importantes.</span><span class="sxs-lookup"><span data-stu-id="72c6e-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="L'exemple montre un onglet avec un tableau des tâches." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="72c6e-155">Anatomie : tabulation</span><span class="sxs-lookup"><span data-stu-id="72c6e-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un onglet." border="false":::

|<span data-ttu-id="72c6e-157">Compteur</span><span class="sxs-lookup"><span data-stu-id="72c6e-157">Counter</span></span>|<span data-ttu-id="72c6e-158">Description</span><span class="sxs-lookup"><span data-stu-id="72c6e-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="72c6e-159">1</span><span class="sxs-lookup"><span data-stu-id="72c6e-159">1</span></span>|<span data-ttu-id="72c6e-160">**Nom de l'onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="72c6e-161">2</span><span class="sxs-lookup"><span data-stu-id="72c6e-161">2</span></span>|<span data-ttu-id="72c6e-162">**Dépassement de tabulation**: ouvre les actions d'onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="72c6e-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="72c6e-163">3</span><span class="sxs-lookup"><span data-stu-id="72c6e-163">3</span></span>|<span data-ttu-id="72c6e-164">**Conversation par onglet**: ouvre un thread de conversation à droite, ce qui permet aux utilisateurs d'avoir une conversation à côté du contenu.</span><span class="sxs-lookup"><span data-stu-id="72c6e-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="72c6e-165">4 </span><span class="sxs-lookup"><span data-stu-id="72c6e-165">4</span></span>|<span data-ttu-id="72c6e-166">**iframe**: affiche le contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="72c6e-167">Conception d'un onglet avec des modèles d'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="72c6e-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="72c6e-168">Utilisez l'un des modèles d'interface utilisateur Teams suivants pour vous aider à concevoir votre expérience d'onglet :</span><span class="sxs-lookup"><span data-stu-id="72c6e-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="72c6e-169">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d'agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="72c6e-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="72c6e-170">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l'état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="72c6e-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="72c6e-171">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d'ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="72c6e-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="72c6e-172">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="72c6e-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="72c6e-173">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d'état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d'erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="72c6e-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="72c6e-174">[Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="72c6e-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="72c6e-175">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="72c6e-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="72c6e-176">Utiliser un onglet pour collaborer</span><span class="sxs-lookup"><span data-stu-id="72c6e-176">Use a tab to collaborate</span></span>

<span data-ttu-id="72c6e-177">Les onglets facilitent les conversations sur le contenu dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="72c6e-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="72c6e-178">Discussion sur les threads</span><span class="sxs-lookup"><span data-stu-id="72c6e-178">Thread discussion</span></span>

<span data-ttu-id="72c6e-179">Les utilisateurs peuvent publier automatiquement sur un canal ou une conversation une fois qu'ils ont ajouté un nouvel onglet. Non seulement cela informe les membres de l'équipe du nouveau contenu et fournit un lien vers l'onglet, mais permet aux utilisateurs de commencer à parler de l'onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="L'exemple montre un onglet abordé dans un thread de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="72c6e-181">Discussion côte à côte</span><span class="sxs-lookup"><span data-stu-id="72c6e-181">Side-by-side discussion</span></span>

<span data-ttu-id="72c6e-182">Les utilisateurs peuvent ensuite avoir une conversation lors de l'affichage du contenu de l'onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="L'exemple montre un onglet avec une conversation ouverte sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="72c6e-184">Autorisations et affichages basés sur les rôles</span><span class="sxs-lookup"><span data-stu-id="72c6e-184">Permissions and role-based views</span></span>

<span data-ttu-id="72c6e-185">L'expérience d'onglet peut être différente pour les utilisateurs en fonction de leurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="72c6e-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="72c6e-186">Par exemple, un utilisateur peut accéder à l'onglet sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="72c6e-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="72c6e-187">Toutefois, un autre utilisateur doit signer et affiche un contenu légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="72c6e-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="72c6e-188">Gérer un onglet</span><span class="sxs-lookup"><span data-stu-id="72c6e-188">Manage a tab</span></span>

<span data-ttu-id="72c6e-189">Vous pouvez inclure des options pour renommer, supprimer ou modifier un onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="72c6e-190">Anatomie : menu Onglet</span><span class="sxs-lookup"><span data-stu-id="72c6e-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration montrant l'anatomie de l'interface utilisateur d'un menu Onglet." border="false":::

|<span data-ttu-id="72c6e-192">Compteur</span><span class="sxs-lookup"><span data-stu-id="72c6e-192">Counter</span></span>|<span data-ttu-id="72c6e-193">Description</span><span class="sxs-lookup"><span data-stu-id="72c6e-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="72c6e-194">1</span><span class="sxs-lookup"><span data-stu-id="72c6e-194">1</span></span>|<span data-ttu-id="72c6e-195">**Paramètres**: (Facultatif) Permet aux utilisateurs de modifier les paramètres d'un onglet après son ajout.</span><span class="sxs-lookup"><span data-stu-id="72c6e-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="72c6e-196">2</span><span class="sxs-lookup"><span data-stu-id="72c6e-196">2</span></span>|<span data-ttu-id="72c6e-197">**Renommer**: permet aux utilisateurs de donner à l'onglet un nom plus significatif pour l'équipe.</span><span class="sxs-lookup"><span data-stu-id="72c6e-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="72c6e-198">3</span><span class="sxs-lookup"><span data-stu-id="72c6e-198">3</span></span>|<span data-ttu-id="72c6e-199">**Supprimer**: supprime l'onglet du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="72c6e-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="72c6e-200">Notifications d'onglet et liaison approfondie</span><span class="sxs-lookup"><span data-stu-id="72c6e-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="72c6e-201">Vous pouvez envoyer un message avec un lien profond vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu'un utilisateur peut sélectionner pour voir l'intégralité du bogue dans un onglet. L'envoi de messages sur l'activité de l'onglet augmente la sensibilisation sans avertir explicitement tout le monde (c'est-à-dire, activité sans bruit).</span><span class="sxs-lookup"><span data-stu-id="72c6e-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="72c6e-202">Vous pouvez également @mention utilisateurs spécifiques si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="72c6e-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="72c6e-203">Informez les utilisateurs de l'activité de l'onglet de l'une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="72c6e-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="72c6e-204">**Bot**: cette méthode est préférée, en particulier si le thread d'onglet est ciblé.</span><span class="sxs-lookup"><span data-stu-id="72c6e-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="72c6e-205">La conversation threadée de l'onglet est déplacée en tant que conversation récemment active.</span><span class="sxs-lookup"><span data-stu-id="72c6e-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="72c6e-206">Cette méthode permet également une certaine complexité dans la façon dont la notification est envoyée.</span><span class="sxs-lookup"><span data-stu-id="72c6e-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="72c6e-207">**Message**: un message s'affiche dans le flux d'activités de l'utilisateur avec un [lien profond vers l'onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="72c6e-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="72c6e-208">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="72c6e-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="72c6e-209">Collaboration</span><span class="sxs-lookup"><span data-stu-id="72c6e-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Illustration shows what to do with tab navigation design." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="72c6e-211">À faire : faciliter la conversation</span><span class="sxs-lookup"><span data-stu-id="72c6e-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="72c6e-212">Inclure du contenu et des composants dont les utilisateurs peuvent parler.</span><span class="sxs-lookup"><span data-stu-id="72c6e-212">Include content and components people can talk about.</span></span> <span data-ttu-id="72c6e-213">S'il ne s'intègre pas dans le contexte d'une conversation, d'un canal ou d'une réunion, il n'appartient pas à votre onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="L'exemple montre ce qu'il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="72c6e-215">À ne pas faire : traiter votre onglet comme n'importe quelle autre page web</span><span class="sxs-lookup"><span data-stu-id="72c6e-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="72c6e-216">Un onglet n'est pas une page web que quelqu'un peut afficher une seule fois.</span><span class="sxs-lookup"><span data-stu-id="72c6e-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="72c6e-217">Un onglet doit afficher le contenu le plus important et pertinent dont les utilisateurs ont besoin pour accomplir quelque chose ensemble.</span><span class="sxs-lookup"><span data-stu-id="72c6e-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="72c6e-218">Navigation</span><span class="sxs-lookup"><span data-stu-id="72c6e-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Exemple montrant comment faire avec la conception de navigation par onglets." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="72c6e-220">À faire : limiter les tâches et les données</span><span class="sxs-lookup"><span data-stu-id="72c6e-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="72c6e-221">Les onglets fonctionnent mieux lorsqu'ils s'adressent à des besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="72c6e-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="72c6e-222">Inclure un ensemble limité de tâches et de données pertinentes pour l'équipe ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="72c6e-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu'il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="72c6e-224">À ne pas faire : incorporer l'intégralité de votre application</span><span class="sxs-lookup"><span data-stu-id="72c6e-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="72c6e-225">L'utilisation d'un onglet pour afficher l'ensemble d'une application avec une navigation à plusieurs niveaux et des interactions complexes entraîne une surcharge d'informations.</span><span class="sxs-lookup"><span data-stu-id="72c6e-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="72c6e-226">Configuration</span><span class="sxs-lookup"><span data-stu-id="72c6e-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration montrant ce qu'il faut faire avec la conception de la configuration de l'onglet." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="72c6e-228">À faire : restez simple</span><span class="sxs-lookup"><span data-stu-id="72c6e-228">Do: Keep it simple</span></span>

<span data-ttu-id="72c6e-229">Si votre application nécessite une authentification, essayez d'intégrer l'authentification unique (SSO) Microsoft pour une expérience de authentification plus transparente.</span><span class="sxs-lookup"><span data-stu-id="72c6e-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="72c6e-230">En outre, incluez uniquement les informations essentielles et les étapes à suivre pour ajouter l'onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu'il ne faut pas faire avec la conception de la configuration de l'onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="72c6e-232">À ne pas faire : trop d'étapes</span><span class="sxs-lookup"><span data-stu-id="72c6e-232">Don't: Have too many steps</span></span>

<span data-ttu-id="72c6e-233">Supprimez les étapes inutiles pour ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="72c6e-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="72c6e-234">Thèmes</span><span class="sxs-lookup"><span data-stu-id="72c6e-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration montrant ce qu'il faut faire avec les tabulations." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="72c6e-236">À faire : tirer parti des jetons de couleur Teams</span><span class="sxs-lookup"><span data-stu-id="72c6e-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="72c6e-237">Chaque thème Teams possède son propre modèle de couleurs.</span><span class="sxs-lookup"><span data-stu-id="72c6e-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="72c6e-238">Pour gérer automatiquement les modifications de thème, utilisez des jetons <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de couleur (interface</a> utilisateur Fluent) dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="72c6e-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration montrant ce qu'il ne faut pas faire avec les tabulations." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="72c6e-240">À ne pas faire : valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="72c6e-240">Don't: Hard code color values</span></span>

<span data-ttu-id="72c6e-241">Si vous n'utilisez pas de jetons de couleur Teams, vos conceptions seront moins évolutives et prenons plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="72c6e-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="72c6e-242">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="72c6e-242">Validate your design</span></span>

<span data-ttu-id="72c6e-243">Si vous envisagez de publier votre application sur AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l'échec des applications lors de l'envoi.</span><span class="sxs-lookup"><span data-stu-id="72c6e-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72c6e-244">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="72c6e-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
