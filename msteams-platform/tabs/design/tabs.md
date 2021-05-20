---
title: Conception de votre onglet pour le bureau et le Web
description: Apprenez à concevoir un onglet Teams (bureau et web) et obtenez le kit d’interface utilisateur Microsoft Teams’interface utilisateur.
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
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="4931f-103">Conception de votre onglet pour Microsoft Teams bureau et web</span><span class="sxs-lookup"><span data-stu-id="4931f-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="4931f-104">Un onglet est une grande toile pour votre contenu.</span><span class="sxs-lookup"><span data-stu-id="4931f-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="4931f-105">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les gens peuvent ajouter, utiliser et gérer les onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4931f-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4931f-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4931f-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4931f-107">Vous pouvez trouver des lignes directrices complètes de conception d’onglets, y compris des éléments que vous pouvez saisir et modifier au besoin, dans le kit d Microsoft Teams’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4931f-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="4931f-108">La trousse d’interface utilisateur a également des sujets essentiels tels que l’accessibilité et le dimensionnement réactif qui ne sont pas couverts ici.</span><span class="sxs-lookup"><span data-stu-id="4931f-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4931f-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="4931f-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="4931f-110">Ajouter un onglet</span><span class="sxs-lookup"><span data-stu-id="4931f-110">Add a tab</span></span>

<span data-ttu-id="4931f-111">Vous pouvez ajouter un onglet du magasin Teams (AppSource) ou dans l’un des contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="4931f-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="4931f-112">Conversation</span><span class="sxs-lookup"><span data-stu-id="4931f-112">Chat</span></span>
* <span data-ttu-id="4931f-113">Canal</span><span class="sxs-lookup"><span data-stu-id="4931f-113">Channel</span></span>
* <span data-ttu-id="4931f-114">Réunion (avant, pendant ou après la réunion)</span><span class="sxs-lookup"><span data-stu-id="4931f-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="4931f-115">L’exemple suivant montre comment un onglet est ajouté dans un canal :</span><span class="sxs-lookup"><span data-stu-id="4931f-115">The following example shows how a tab is added in a channel:</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Exemple montre un onglet ajouté dans un canal." border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="4931f-117">Configurer un onglet</span><span class="sxs-lookup"><span data-stu-id="4931f-117">Set up a tab</span></span>

<span data-ttu-id="4931f-118">Il y a un court processus de configuration pour ajouter une application en tant que canal, chat ou onglet de réunion. L’expérience dépend en grande partie de vous.</span><span class="sxs-lookup"><span data-stu-id="4931f-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="4931f-119">Par exemple, vous pouvez avoir une description de la façon d’utiliser l’application et certains paramètres optionnels.</span><span class="sxs-lookup"><span data-stu-id="4931f-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="4931f-120">Incluez une étape de dédentification ici si vous avez besoin d’authentifier les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4931f-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="4931f-121">Configuration de l’onglet modal</span><span class="sxs-lookup"><span data-stu-id="4931f-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple montre une configuration d’onglet modal." border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="4931f-123">Anatomie: Configuration de l’onglet modal</span><span class="sxs-lookup"><span data-stu-id="4931f-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un modal de configuration d’onglet." border="false":::

|<span data-ttu-id="4931f-125">Compteur</span><span class="sxs-lookup"><span data-stu-id="4931f-125">Counter</span></span>|<span data-ttu-id="4931f-126">Description</span><span class="sxs-lookup"><span data-stu-id="4931f-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4931f-127">1</span><span class="sxs-lookup"><span data-stu-id="4931f-127">1</span></span>|<span data-ttu-id="4931f-128">**Logo de l’application**: Logo de l’application en couleur de votre application.</span><span class="sxs-lookup"><span data-stu-id="4931f-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="4931f-129">2</span><span class="sxs-lookup"><span data-stu-id="4931f-129">2</span></span>|<span data-ttu-id="4931f-130">**Nom de l’application**: Nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="4931f-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="4931f-131">3</span><span class="sxs-lookup"><span data-stu-id="4931f-131">3</span></span>|<span data-ttu-id="4931f-132">**iframe**: Espace réactif pour le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="4931f-132">**iframe**: Responsive space for your app’s content.</span></span> <span data-ttu-id="4931f-133">Par exemple, paramètres d’onglet ou authentification.</span><span class="sxs-lookup"><span data-stu-id="4931f-133">For example, tab settings or authentication.</span></span>|
|<span data-ttu-id="4931f-134">4 </span><span class="sxs-lookup"><span data-stu-id="4931f-134">4</span></span>|<span data-ttu-id="4931f-135">**À propos du** lien : Ouvre un dialogue montrant plus d’informations sur l’application, telles qu’une description complète, les autorisations requises par l’application et les liens vers votre politique de confidentialité et vos conditions de service.</span><span class="sxs-lookup"><span data-stu-id="4931f-135">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="4931f-136">5 </span><span class="sxs-lookup"><span data-stu-id="4931f-136">5</span></span>|<span data-ttu-id="4931f-137">**Bouton fermer**: Ferme le modale.</span><span class="sxs-lookup"><span data-stu-id="4931f-137">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="4931f-138">6 </span><span class="sxs-lookup"><span data-stu-id="4931f-138">6</span></span>|<span data-ttu-id="4931f-139">**Aviser l’option membres** de l’équipe : Le modal vous demande si vous souhaitez créer un message permettant aux autres de savoir que vous avez ajouté un onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-139">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="4931f-140">7 </span><span class="sxs-lookup"><span data-stu-id="4931f-140">7</span></span>|<span data-ttu-id="4931f-141">**Bouton arrière : Passe** à l’étape précédente en fonction de l’endroit où le dialogue s’est ouvert.</span><span class="sxs-lookup"><span data-stu-id="4931f-141">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="4931f-142">8 </span><span class="sxs-lookup"><span data-stu-id="4931f-142">8</span></span>|<span data-ttu-id="4931f-143">**Enregistrer le bouton**: Termine la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-143">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="4931f-144">Authentification de l’onglet avec une seule inscription</span><span class="sxs-lookup"><span data-stu-id="4931f-144">Tab authentication with single sign-on</span></span>

<span data-ttu-id="4931f-145">Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4931f-145">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="4931f-146">Cette méthode d’authentification est appelée simple connectement (SSO).</span><span class="sxs-lookup"><span data-stu-id="4931f-146">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple montre un écran d’authentification d’onglet." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="4931f-148">Conception d’une configuration d’onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="4931f-148">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="4931f-149">Utilisez l’un des modèles d’interface Teams d’interface utilisateur suivants pour aider à concevoir votre expérience de configuration d’onglets :</span><span class="sxs-lookup"><span data-stu-id="4931f-149">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="4931f-150">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): Les listes peuvent afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="4931f-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="4931f-151">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): Les formulaires sont pour la collecte, la validation et la soumission structurée des entrées de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4931f-151">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="4931f-152">[État vide :](../../concepts/design/design-teams-app-ui-templates.md#empty-state)Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="4931f-152">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="4931f-153">Afficher un onglet</span><span class="sxs-lookup"><span data-stu-id="4931f-153">View a tab</span></span>

<span data-ttu-id="4931f-154">Les onglets offrent une expérience Web en plein écran dans les Teams où vous pouvez afficher du contenu collaboratif – tels que des tableaux de bord et des tableaux de bord – et des informations importantes.</span><span class="sxs-lookup"><span data-stu-id="4931f-154">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Exemple montre un onglet avec un tableau de tâches." border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="4931f-156">Anatomie: Onglet</span><span class="sxs-lookup"><span data-stu-id="4931f-156">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un onglet." border="false":::

|<span data-ttu-id="4931f-158">Compteur</span><span class="sxs-lookup"><span data-stu-id="4931f-158">Counter</span></span>|<span data-ttu-id="4931f-159">Description</span><span class="sxs-lookup"><span data-stu-id="4931f-159">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4931f-160">1</span><span class="sxs-lookup"><span data-stu-id="4931f-160">1</span></span>|<span data-ttu-id="4931f-161">**Nom de l’onglet**: Étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-161">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="4931f-162">2</span><span class="sxs-lookup"><span data-stu-id="4931f-162">2</span></span>|<span data-ttu-id="4931f-163">**Débordement d’onglets**: Ouvre les actions de l’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="4931f-163">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="4931f-164">3</span><span class="sxs-lookup"><span data-stu-id="4931f-164">3</span></span>|<span data-ttu-id="4931f-165">**Tab chat**: Ouvre un fil de chat sur la droite, permettant aux utilisateurs d’avoir une conversation à côté du contenu.</span><span class="sxs-lookup"><span data-stu-id="4931f-165">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="4931f-166">4 </span><span class="sxs-lookup"><span data-stu-id="4931f-166">4</span></span>|<span data-ttu-id="4931f-167">**iframe**: Affiche le contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-167">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="4931f-168">Conception d’un onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="4931f-168">Designing a tab with UI templates</span></span>

<span data-ttu-id="4931f-169">Utilisez l’un des modèles d Teams d’interface utilisateur suivants pour aider à concevoir votre expérience d’onglet :</span><span class="sxs-lookup"><span data-stu-id="4931f-169">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="4931f-170">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): Les listes peuvent afficher des éléments connexes dans un format scannable et permettre aux utilisateurs de prendre des mesures sur une liste entière ou des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="4931f-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="4931f-171">[Tableau de travail](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tableau de travail, parfois appelé planche kanban ou pistes de natation, est une collection de cartes souvent utilisées pour suivre l’état des articles de travail ou des billets.</span><span class="sxs-lookup"><span data-stu-id="4931f-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="4931f-172">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : Un tableau de bord est une toile contenant plusieurs cartes qui donnent un aperçu des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="4931f-172">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="4931f-173">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): Les formulaires sont pour la collecte, la validation et la soumission structurée des entrées de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4931f-173">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="4931f-174">[État vide :](../../concepts/design/design-teams-app-ui-templates.md#empty-state)Le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la dé connecte, les expériences de première série, les messages d’erreur, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="4931f-174">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="4931f-175">[Navigation gauche :](../../concepts/design/design-teams-app-ui-templates.md#left-nav)Le modèle de navigation gauche peut vous aider si votre onglet nécessite une certaine navigation.</span><span class="sxs-lookup"><span data-stu-id="4931f-175">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="4931f-176">En général, vous devez garder un œil sur la navigation au minimum.</span><span class="sxs-lookup"><span data-stu-id="4931f-176">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="4931f-177">Utilisez un onglet pour collaborer</span><span class="sxs-lookup"><span data-stu-id="4931f-177">Use a tab to collaborate</span></span>

<span data-ttu-id="4931f-178">Les onglets facilitent les conversations sur le contenu dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="4931f-178">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="4931f-179">Discussion de fil</span><span class="sxs-lookup"><span data-stu-id="4931f-179">Thread discussion</span></span>

<span data-ttu-id="4931f-180">Les utilisateurs peuvent automatiquement publier sur un canal ou discuter une fois qu’ils ont ajouté un nouvel onglet. Cela permet non seulement d’aviser les membres de l’équipe du nouveau contenu et fournit un lien vers l’onglet, il permet aux gens de commencer à parler de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-180">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Exemple montre un onglet en cours de discussion dans un thread de canal." border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="4931f-182">Discussion côte à côte</span><span class="sxs-lookup"><span data-stu-id="4931f-182">Side-by-side discussion</span></span>

<span data-ttu-id="4931f-183">Les utilisateurs peuvent avoir une conversation ensuite tout en visualiser le contenu de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-183">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Exemple montre un onglet avec un chat ouvert sur le côté droit." border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="4931f-185">Autorisations et vues basées sur les rôle</span><span class="sxs-lookup"><span data-stu-id="4931f-185">Permissions and role-based views</span></span>

<span data-ttu-id="4931f-186">L’expérience de l’onglet peut être différente pour les utilisateurs en fonction de leurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="4931f-186">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="4931f-187">Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="4931f-187">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="4931f-188">Un autre utilisateur, cependant, doit signer et verra un contenu légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="4931f-188">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="4931f-189">Gérer un onglet</span><span class="sxs-lookup"><span data-stu-id="4931f-189">Manage a tab</span></span>

<span data-ttu-id="4931f-190">Vous pouvez inclure des options pour renommer, supprimer ou modifier un onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-190">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="4931f-191">Anatomie: Menu onglet</span><span class="sxs-lookup"><span data-stu-id="4931f-191">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration affichant l’anatomie d’interface utilisateur d’un menu d’onglet." border="false":::

|<span data-ttu-id="4931f-193">Compteur</span><span class="sxs-lookup"><span data-stu-id="4931f-193">Counter</span></span>|<span data-ttu-id="4931f-194">Description</span><span class="sxs-lookup"><span data-stu-id="4931f-194">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4931f-195">1</span><span class="sxs-lookup"><span data-stu-id="4931f-195">1</span></span>|<span data-ttu-id="4931f-196">**Paramètres**: (Facultatif) Permet aux utilisateurs de modifier les paramètres d’un onglet après son ajout.</span><span class="sxs-lookup"><span data-stu-id="4931f-196">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="4931f-197">2</span><span class="sxs-lookup"><span data-stu-id="4931f-197">2</span></span>|<span data-ttu-id="4931f-198">**Renommer**: Permet aux utilisateurs de donner à l’onglet un nom plus significatif pour l’équipe.</span><span class="sxs-lookup"><span data-stu-id="4931f-198">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="4931f-199">3</span><span class="sxs-lookup"><span data-stu-id="4931f-199">3</span></span>|<span data-ttu-id="4931f-200">**Supprimer**: Supprime l’onglet du canal, du chat ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="4931f-200">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="4931f-201">Notifications d’onglets et liaison profonde</span><span class="sxs-lookup"><span data-stu-id="4931f-201">Tab notifications and deep linking</span></span>

<span data-ttu-id="4931f-202">Vous pouvez envoyer un message avec un lien profond vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour voir l’ensemble du bogue dans un onglet. L’envoi de messages sur l’activité de l’onglet augmente la sensibilisation sans en informer explicitement tout le monde (c.-à-d. l’activité sans bruit).</span><span class="sxs-lookup"><span data-stu-id="4931f-202">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="4931f-203">Vous pouvez également @mention utilisateurs spécifiques si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4931f-203">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="4931f-204">Informez les utilisateurs de l’activité de l’onglet de l’une des façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="4931f-204">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="4931f-205">**Bot**: Cette méthode est préférée surtout si le thread d’onglet est ciblé.</span><span class="sxs-lookup"><span data-stu-id="4931f-205">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="4931f-206">La conversation filetée de l’onglet est déplacée en vue aussi récemment active.</span><span class="sxs-lookup"><span data-stu-id="4931f-206">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="4931f-207">Cette méthode permet également une certaine sophistication dans la façon dont la notification est envoyée.</span><span class="sxs-lookup"><span data-stu-id="4931f-207">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="4931f-208">**Message**: Un message apparaît dans le flux d’activité de l’utilisateur avec un [lien profond vers l’onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="4931f-208">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="4931f-209">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="4931f-209">Best practices</span></span>

<span data-ttu-id="4931f-210">Utilisez ces recommandations pour créer une expérience d’application de qualité :</span><span class="sxs-lookup"><span data-stu-id="4931f-210">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="4931f-211">Collaboration</span><span class="sxs-lookup"><span data-stu-id="4931f-211">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="L’illustration montre ce qu’il faut faire avec la conception de navigation d’onglet." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="4931f-213">Faire: Faciliter la conversation</span><span class="sxs-lookup"><span data-stu-id="4931f-213">Do: Facilitate conversation</span></span>

<span data-ttu-id="4931f-214">Incluez le contenu et les composants dont les gens peuvent parler.</span><span class="sxs-lookup"><span data-stu-id="4931f-214">Include content and components people can talk about.</span></span> <span data-ttu-id="4931f-215">S’il ne s’inscrit pas dans le contexte d’un chat, d’un canal ou d’une réunion, il n’a pas sa place dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-215">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Exemple montre ce qu’il ne faut pas faire avec la conception de navigation onglet." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="4931f-217">Ne pas : Traitez votre onglet comme n’importe quelle autre page Web</span><span class="sxs-lookup"><span data-stu-id="4931f-217">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="4931f-218">Un onglet n’est pas une page Web que quelqu’un peut afficher une fois.</span><span class="sxs-lookup"><span data-stu-id="4931f-218">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="4931f-219">Un onglet doit afficher votre contenu le plus important et pertinent dont les gens ont besoin pour accomplir quelque chose ensemble.</span><span class="sxs-lookup"><span data-stu-id="4931f-219">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="4931f-220">Navigation</span><span class="sxs-lookup"><span data-stu-id="4931f-220">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Exemple montrant ce qu’il faut faire avec la conception de navigation d’onglet." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="4931f-222">Faire : Limiter les tâches et les données</span><span class="sxs-lookup"><span data-stu-id="4931f-222">Do: Limit tasks and data</span></span>

<span data-ttu-id="4931f-223">Les onglets fonctionnent mieux lorsqu’ils répondent à des besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="4931f-223">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="4931f-224">Inclure un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="4931f-224">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de navigation d’onglet." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="4931f-226">Ne pas : Intégrir toute votre application</span><span class="sxs-lookup"><span data-stu-id="4931f-226">Don't: Embed your entire app</span></span>

<span data-ttu-id="4931f-227">L’utilisation d’un onglet pour afficher une application entière avec navigation à plusieurs niveaux et interactions complexes conduit à une surcharge d’informations.</span><span class="sxs-lookup"><span data-stu-id="4931f-227">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="4931f-228">Configuration</span><span class="sxs-lookup"><span data-stu-id="4931f-228">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration montrant ce qu’il faut faire avec la conception de configuration d’onglet." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="4931f-230">Faire: Garder les choses simples</span><span class="sxs-lookup"><span data-stu-id="4931f-230">Do: Keep it simple</span></span>

<span data-ttu-id="4931f-231">Si votre application nécessite une authentification, essayez d’intégrer microsoft single sign-on (SSO) pour une expérience de connexion plus transparente.</span><span class="sxs-lookup"><span data-stu-id="4931f-231">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="4931f-232">En outre, ne comprennent que des informations essentielles et des étapes pour ajouter l’onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-232">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de configuration d’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="4931f-234">Ne pas: Avoir trop d’étapes</span><span class="sxs-lookup"><span data-stu-id="4931f-234">Don't: Have too many steps</span></span>

<span data-ttu-id="4931f-235">Supprimez toutes les étapes inutiles pour ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="4931f-235">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="4931f-236">Thèmes</span><span class="sxs-lookup"><span data-stu-id="4931f-236">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration affichant ce qu’il faut faire avec le theming d’onglet." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="4931f-238">Faire: Profitez de Teams de couleur</span><span class="sxs-lookup"><span data-stu-id="4931f-238">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="4931f-239">Chaque Teams a son propre schéma de couleurs.</span><span class="sxs-lookup"><span data-stu-id="4931f-239">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="4931f-240">Pour gérer automatiquement les modifications de thème, <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">utilisez des jetons de couleur (interface utilisateur fluide)</a> dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="4931f-240">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec le theming d’onglet." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="4931f-242">Ne pas : Valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="4931f-242">Don't: Hard code color values</span></span>

<span data-ttu-id="4931f-243">Si vous n’utilisez pas Teams jetons de couleur, vos créations seront moins évolutives et prennent plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="4931f-243">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
