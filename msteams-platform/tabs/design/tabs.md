---
title: Conception de votre onglet pour le bureau et le web
description: Découvrez comment concevoir un onglet Teams (bureau et web) et obtenir le kit Microsoft Teams’interface utilisateur.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566879"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="7374b-103">Conception de votre onglet pour Microsoft Teams bureau et web</span><span class="sxs-lookup"><span data-stu-id="7374b-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="7374b-104">Un onglet est un canevas de grande taille pour votre contenu.</span><span class="sxs-lookup"><span data-stu-id="7374b-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="7374b-105">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="7374b-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="7374b-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7374b-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7374b-107">Vous trouverez des recommandations complètes en matière de conception d’onglets, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans Microsoft Teams kit d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7374b-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="7374b-108">Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le resserrement réactif qui ne sont pas abordés ici.</span><span class="sxs-lookup"><span data-stu-id="7374b-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7374b-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="7374b-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="7374b-110">Ajouter un onglet</span><span class="sxs-lookup"><span data-stu-id="7374b-110">Add a tab</span></span>

<span data-ttu-id="7374b-111">Vous pouvez ajouter un onglet à partir Teams store (AppSource) ou dans l’un des contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="7374b-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="7374b-112">Conversation</span><span class="sxs-lookup"><span data-stu-id="7374b-112">Chat</span></span>
* <span data-ttu-id="7374b-113">Canal</span><span class="sxs-lookup"><span data-stu-id="7374b-113">Channel</span></span>
* <span data-ttu-id="7374b-114">Réunion (avant, pendant ou après la réunion)</span><span class="sxs-lookup"><span data-stu-id="7374b-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="7374b-115">L’exemple suivant montre comment un onglet est ajouté dans un canal :</span><span class="sxs-lookup"><span data-stu-id="7374b-115">The following example shows how a tab is added in a channel:</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="L’exemple montre comment ajouter un onglet dans un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="7374b-117">Configurer un onglet</span><span class="sxs-lookup"><span data-stu-id="7374b-117">Set up a tab</span></span>

<span data-ttu-id="7374b-118">Il existe un processus de configuration court pour ajouter une application en tant que canal, conversation ou onglet de réunion. C’est en grande partie à vous de faire l’expérience.</span><span class="sxs-lookup"><span data-stu-id="7374b-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="7374b-119">Par exemple, vous pouvez avoir une description de l’utilisation de l’application et certains paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="7374b-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="7374b-120">Incluez une étape de connectez-vous ici si vous devez authentifier les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7374b-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="7374b-121">Tab configuration modal</span><span class="sxs-lookup"><span data-stu-id="7374b-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple de configuration modale d’onglet." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="7374b-123">Anatomie : modal de configuration de l’onglet</span><span class="sxs-lookup"><span data-stu-id="7374b-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un modèle de configuration d’onglet." border="false":::

|<span data-ttu-id="7374b-125">Compteur</span><span class="sxs-lookup"><span data-stu-id="7374b-125">Counter</span></span>|<span data-ttu-id="7374b-126">Description</span><span class="sxs-lookup"><span data-stu-id="7374b-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7374b-127">1</span><span class="sxs-lookup"><span data-stu-id="7374b-127">1</span></span>|<span data-ttu-id="7374b-128">**Logo de l’application**: logo d’application en couleur complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="7374b-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="7374b-129">2</span><span class="sxs-lookup"><span data-stu-id="7374b-129">2</span></span>|<span data-ttu-id="7374b-130">**Nom de l’application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="7374b-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="7374b-131">3</span><span class="sxs-lookup"><span data-stu-id="7374b-131">3</span></span>|<span data-ttu-id="7374b-132">**iframe**: espace réactif pour le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="7374b-132">**iframe**: Responsive space for your app’s content.</span></span> <span data-ttu-id="7374b-133">Par exemple, les paramètres d’onglet ou l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7374b-133">For example, tab settings or authentication.</span></span>|
|<span data-ttu-id="7374b-134">4 </span><span class="sxs-lookup"><span data-stu-id="7374b-134">4</span></span>|<span data-ttu-id="7374b-135">**À** propos du lien : ouvre une boîte de dialogue affichant plus d’informations sur l’application, telles qu’une description complète, les autorisations requises par l’application et des liens vers votre politique de confidentialité et les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="7374b-135">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="7374b-136">5 </span><span class="sxs-lookup"><span data-stu-id="7374b-136">5</span></span>|<span data-ttu-id="7374b-137">**Bouton Fermer**: ferme la modale.</span><span class="sxs-lookup"><span data-stu-id="7374b-137">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="7374b-138">6 </span><span class="sxs-lookup"><span data-stu-id="7374b-138">6</span></span>|<span data-ttu-id="7374b-139">**Option Avertir les membres de l’équipe**: la modale vous demande si vous souhaitez créer un billet pour informer d’autres utilisateurs que vous avez ajouté un onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-139">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="7374b-140">7 </span><span class="sxs-lookup"><span data-stu-id="7374b-140">7</span></span>|<span data-ttu-id="7374b-141">**Bouton Précédent**: passe à l’étape précédente en fonction de l’endroit où la boîte de dialogue s’est ouverte.</span><span class="sxs-lookup"><span data-stu-id="7374b-141">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="7374b-142">8 </span><span class="sxs-lookup"><span data-stu-id="7374b-142">8</span></span>|<span data-ttu-id="7374b-143">**Bouton Enregistrer :** termine la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-143">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="7374b-144">Authentification par onglet avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="7374b-144">Tab authentication with single sign-on</span></span>

<span data-ttu-id="7374b-145">Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7374b-145">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="7374b-146">Cette méthode d’authentification est appelée authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="7374b-146">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple d’écran d’authentification par onglet." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="7374b-148">Conception d’une configuration d’onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7374b-148">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="7374b-149">Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre expérience de configuration d’onglets :</span><span class="sxs-lookup"><span data-stu-id="7374b-149">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="7374b-150">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="7374b-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="7374b-151">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="7374b-151">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="7374b-152">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="7374b-152">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="7374b-153">Afficher un onglet</span><span class="sxs-lookup"><span data-stu-id="7374b-153">View a tab</span></span>

<span data-ttu-id="7374b-154">Les onglets offrent une expérience web en plein écran dans Teams où vous pouvez afficher du contenu collaboratif (tableaux de tâches et tableaux de bord, par exemple) et des informations importantes.</span><span class="sxs-lookup"><span data-stu-id="7374b-154">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="L’exemple montre un onglet avec un tableau des tâches." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="7374b-156">Anatomie : tabulation</span><span class="sxs-lookup"><span data-stu-id="7374b-156">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|<span data-ttu-id="7374b-158">Compteur</span><span class="sxs-lookup"><span data-stu-id="7374b-158">Counter</span></span>|<span data-ttu-id="7374b-159">Description</span><span class="sxs-lookup"><span data-stu-id="7374b-159">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7374b-160">1</span><span class="sxs-lookup"><span data-stu-id="7374b-160">1</span></span>|<span data-ttu-id="7374b-161">**Nom de l’onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-161">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="7374b-162">2</span><span class="sxs-lookup"><span data-stu-id="7374b-162">2</span></span>|<span data-ttu-id="7374b-163">**Dépassement de tabulation**: ouvre les actions d’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="7374b-163">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="7374b-164">3</span><span class="sxs-lookup"><span data-stu-id="7374b-164">3</span></span>|<span data-ttu-id="7374b-165">**Conversation par onglet**: ouvre un thread de conversation à droite, ce qui permet aux utilisateurs d’avoir une conversation à côté du contenu.</span><span class="sxs-lookup"><span data-stu-id="7374b-165">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="7374b-166">4 </span><span class="sxs-lookup"><span data-stu-id="7374b-166">4</span></span>|<span data-ttu-id="7374b-167">**iframe**: affiche le contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-167">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="7374b-168">Conception d’un onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7374b-168">Designing a tab with UI templates</span></span>

<span data-ttu-id="7374b-169">Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre expérience d’onglet :</span><span class="sxs-lookup"><span data-stu-id="7374b-169">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="7374b-170">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="7374b-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="7374b-171">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="7374b-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="7374b-172">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="7374b-172">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="7374b-173">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="7374b-173">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="7374b-174">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="7374b-174">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="7374b-175">[Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="7374b-175">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="7374b-176">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="7374b-176">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="7374b-177">Utiliser un onglet pour collaborer</span><span class="sxs-lookup"><span data-stu-id="7374b-177">Use a tab to collaborate</span></span>

<span data-ttu-id="7374b-178">Les onglets facilitent les conversations sur le contenu dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="7374b-178">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="7374b-179">Discussion sur les threads</span><span class="sxs-lookup"><span data-stu-id="7374b-179">Thread discussion</span></span>

<span data-ttu-id="7374b-180">Les utilisateurs peuvent publier automatiquement sur un canal ou une conversation une fois qu’ils ont ajouté un nouvel onglet. Non seulement cela informe les membres de l’équipe du nouveau contenu et fournit un lien vers l’onglet, mais permet aux utilisateurs de commencer à parler de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-180">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="L’exemple montre un onglet abordé dans un thread de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="7374b-182">Discussion côte à côte</span><span class="sxs-lookup"><span data-stu-id="7374b-182">Side-by-side discussion</span></span>

<span data-ttu-id="7374b-183">Les utilisateurs peuvent ensuite avoir une conversation lors de l’affichage du contenu de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-183">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="L’exemple montre un onglet avec une conversation ouverte sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="7374b-185">Autorisations et affichages basés sur les rôles</span><span class="sxs-lookup"><span data-stu-id="7374b-185">Permissions and role-based views</span></span>

<span data-ttu-id="7374b-186">L’expérience d’onglet peut être différente pour les utilisateurs en fonction de leurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="7374b-186">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="7374b-187">Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="7374b-187">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="7374b-188">Toutefois, un autre utilisateur doit signer et affiche un contenu légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="7374b-188">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="7374b-189">Gérer un onglet</span><span class="sxs-lookup"><span data-stu-id="7374b-189">Manage a tab</span></span>

<span data-ttu-id="7374b-190">Vous pouvez inclure des options pour renommer, supprimer ou modifier un onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-190">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="7374b-191">Anatomie : menu Onglet</span><span class="sxs-lookup"><span data-stu-id="7374b-191">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu Onglet." border="false":::

|<span data-ttu-id="7374b-193">Compteur</span><span class="sxs-lookup"><span data-stu-id="7374b-193">Counter</span></span>|<span data-ttu-id="7374b-194">Description</span><span class="sxs-lookup"><span data-stu-id="7374b-194">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7374b-195">1</span><span class="sxs-lookup"><span data-stu-id="7374b-195">1</span></span>|<span data-ttu-id="7374b-196">**Paramètres**: (Facultatif) Permet aux utilisateurs de modifier les paramètres d’un onglet après son ajout.</span><span class="sxs-lookup"><span data-stu-id="7374b-196">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="7374b-197">2</span><span class="sxs-lookup"><span data-stu-id="7374b-197">2</span></span>|<span data-ttu-id="7374b-198">**Renommer**: permet aux utilisateurs de donner à l’onglet un nom plus significatif pour l’équipe.</span><span class="sxs-lookup"><span data-stu-id="7374b-198">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="7374b-199">3</span><span class="sxs-lookup"><span data-stu-id="7374b-199">3</span></span>|<span data-ttu-id="7374b-200">**Supprimer**: supprime l’onglet du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="7374b-200">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="7374b-201">Notifications d’onglet et liaison approfondie</span><span class="sxs-lookup"><span data-stu-id="7374b-201">Tab notifications and deep linking</span></span>

<span data-ttu-id="7374b-202">Vous pouvez envoyer un message avec un lien profond vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour voir l’intégralité du bogue dans un onglet. L’envoi de messages sur l’activité de l’onglet augmente la sensibilisation sans avertir explicitement tout le monde (c’est-à-dire, activité sans bruit).</span><span class="sxs-lookup"><span data-stu-id="7374b-202">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="7374b-203">Vous pouvez également @mention utilisateurs spécifiques si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7374b-203">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="7374b-204">Informez les utilisateurs de l’activité de l’onglet de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="7374b-204">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="7374b-205">**Bot**: cette méthode est préférée, en particulier si le thread d’onglet est ciblé.</span><span class="sxs-lookup"><span data-stu-id="7374b-205">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="7374b-206">La conversation threadée de l’onglet est déplacée dans l’affichage comme étant récemment active.</span><span class="sxs-lookup"><span data-stu-id="7374b-206">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="7374b-207">Cette méthode permet également une certaine complexité dans la façon dont la notification est envoyée.</span><span class="sxs-lookup"><span data-stu-id="7374b-207">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="7374b-208">**Message**: un message s’affiche dans le flux d’activités de l’utilisateur avec un [lien profond vers l’onglet.](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7374b-208">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="7374b-209">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="7374b-209">Best practices</span></span>

<span data-ttu-id="7374b-210">Utilisez ces recommandations pour créer une expérience d’application de qualité :</span><span class="sxs-lookup"><span data-stu-id="7374b-210">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="7374b-211">Collaboration</span><span class="sxs-lookup"><span data-stu-id="7374b-211">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Illustration shows what to do with tab navigation design." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="7374b-213">À faire : faciliter la conversation</span><span class="sxs-lookup"><span data-stu-id="7374b-213">Do: Facilitate conversation</span></span>

<span data-ttu-id="7374b-214">Inclure du contenu et des composants dont les utilisateurs peuvent parler.</span><span class="sxs-lookup"><span data-stu-id="7374b-214">Include content and components people can talk about.</span></span> <span data-ttu-id="7374b-215">S’il ne s’intègre pas dans le contexte d’une conversation, d’un canal ou d’une réunion, il n’appartient pas à votre onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-215">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="7374b-217">À ne pas faire : traiter votre onglet comme n’importe quelle autre page web</span><span class="sxs-lookup"><span data-stu-id="7374b-217">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="7374b-218">Un onglet n’est pas une page web que quelqu’un peut afficher une seule fois.</span><span class="sxs-lookup"><span data-stu-id="7374b-218">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="7374b-219">Un onglet doit afficher le contenu le plus important et pertinent dont les utilisateurs ont besoin pour accomplir quelque chose ensemble.</span><span class="sxs-lookup"><span data-stu-id="7374b-219">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="7374b-220">Navigation</span><span class="sxs-lookup"><span data-stu-id="7374b-220">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Exemple montrant comment faire avec la conception de navigation par onglets." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="7374b-222">À faire : limiter les tâches et les données</span><span class="sxs-lookup"><span data-stu-id="7374b-222">Do: Limit tasks and data</span></span>

<span data-ttu-id="7374b-223">Les onglets fonctionnent mieux lorsqu’ils s’adressent à des besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7374b-223">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="7374b-224">Inclure un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="7374b-224">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="7374b-226">À ne pas faire : incorporer l’intégralité de votre application</span><span class="sxs-lookup"><span data-stu-id="7374b-226">Don't: Embed your entire app</span></span>

<span data-ttu-id="7374b-227">L’utilisation d’un onglet pour afficher l’ensemble d’une application avec une navigation à plusieurs niveaux et des interactions complexes entraîne une surcharge d’informations.</span><span class="sxs-lookup"><span data-stu-id="7374b-227">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="7374b-228">Configuration</span><span class="sxs-lookup"><span data-stu-id="7374b-228">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration montrant ce qu’il faut faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="7374b-230">À faire : restez simple</span><span class="sxs-lookup"><span data-stu-id="7374b-230">Do: Keep it simple</span></span>

<span data-ttu-id="7374b-231">Si votre application nécessite une authentification, essayez d’intégrer l’authentification unique (SSO) Microsoft pour une expérience de authentification plus transparente.</span><span class="sxs-lookup"><span data-stu-id="7374b-231">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="7374b-232">En outre, incluez uniquement les informations essentielles et les étapes à suivre pour ajouter l’onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-232">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="7374b-234">À ne pas faire : trop d’étapes</span><span class="sxs-lookup"><span data-stu-id="7374b-234">Don't: Have too many steps</span></span>

<span data-ttu-id="7374b-235">Supprimez les étapes inutiles pour ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="7374b-235">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="7374b-236">Thèmes</span><span class="sxs-lookup"><span data-stu-id="7374b-236">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration montrant ce qu’il faut faire avec les tabulations." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="7374b-238">À faire : tirer parti des jetons Teams couleur</span><span class="sxs-lookup"><span data-stu-id="7374b-238">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="7374b-239">Chaque Teams thème possède son propre modèle de couleurs.</span><span class="sxs-lookup"><span data-stu-id="7374b-239">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="7374b-240">Pour gérer automatiquement les modifications de thème, utilisez des jetons <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de couleur (interface</a> utilisateur Fluent) dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="7374b-240">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec les tabulations." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="7374b-242">À ne pas faire : valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="7374b-242">Don't: Hard code color values</span></span>

<span data-ttu-id="7374b-243">Si vous n’utilisez pas Teams de couleur, vos conceptions seront moins évolutives et prenons plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="7374b-243">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
