---
title: Onglets de conception pour ordinateur de bureau, web et mobile
description: Découvrez comment concevoir un onglet Teams pour ordinateur de bureau, web et mobile, et obtenir le kit Microsoft Teams’interface utilisateur.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f1823a064cd182d0271aa97bef58ec724c7819b3
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721842"
---
# <a name="design-your-tab-for-microsoft-teams"></a><span data-ttu-id="f6882-103">Concevez votre onglet pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f6882-103">Design your tab for Microsoft Teams</span></span>

<span data-ttu-id="f6882-104">Un onglet est un canevas de grande taille pour le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6882-104">A tab is a large canvas for your app content.</span></span> <span data-ttu-id="f6882-105">Pour guider la conception de votre application, les informations suivantes décrivent et illustrent comment les personnes peuvent ajouter, utiliser et gérer des onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="f6882-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="f6882-106">Kit d’interface utilisateur de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f6882-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="f6882-107">Vous trouverez des recommandations complètes en matière de conception d’onglets, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans Microsoft Teams kit d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f6882-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="f6882-108">Le kit d’interface utilisateur contient également des rubriques essentielles telles que l’accessibilité et le resserrement réactif qui ne sont pas abordés ici.</span><span class="sxs-lookup"><span data-stu-id="f6882-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6882-109">Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)</span><span class="sxs-lookup"><span data-stu-id="f6882-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="f6882-110">Ajouter un onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-110">Add a tab</span></span>

<span data-ttu-id="f6882-111">Vous pouvez ajouter un onglet à partir Teams store (AppSource) ou dans l’un des contextes suivants :</span><span class="sxs-lookup"><span data-stu-id="f6882-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="f6882-112">Conversation</span><span class="sxs-lookup"><span data-stu-id="f6882-112">Chat</span></span>
* <span data-ttu-id="f6882-113">Canal</span><span class="sxs-lookup"><span data-stu-id="f6882-113">Channel</span></span>
* <span data-ttu-id="f6882-114">Réunion (avant, pendant ou après la réunion)</span><span class="sxs-lookup"><span data-stu-id="f6882-114">Meeting (before, during, or after the meeting)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f6882-115">Desktop</span><span class="sxs-lookup"><span data-stu-id="f6882-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="f6882-116">L’exemple suivant montre comment les utilisateurs peuvent ajouter un onglet dans un canal.</span><span class="sxs-lookup"><span data-stu-id="f6882-116">The following example shows how users can add a tab in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="L’exemple montre comment ajouter un onglet dans un canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f6882-118">Mobile</span><span class="sxs-lookup"><span data-stu-id="f6882-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="f6882-119">Les utilisateurs peuvent accéder aux onglets en sélectionnant le bouton **Plus** dans le canal (exemple ci-dessous) ou en chat dans lequel ils ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="f6882-119">Users can access tabs by selecting the **More** button in the channel (example below) or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="L’exemple illustre l’ajout d’un onglet mobile dans un canal." border="false":::

---

## <a name="set-up-a-tab"></a><span data-ttu-id="f6882-121">Configurer un onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-121">Set up a tab</span></span>

<span data-ttu-id="f6882-122">Il existe un processus de configuration court pour ajouter une application en tant que canal, conversation ou onglet de réunion. C’est en grande partie à vous de faire l’expérience.</span><span class="sxs-lookup"><span data-stu-id="f6882-122">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="f6882-123">Par exemple, vous pouvez avoir une description de l’utilisation de l’application et certains paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="f6882-123">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="f6882-124">Incluez une étape de connectez-vous ici si vous avez besoin d’authentifier les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f6882-124">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-dialog"></a><span data-ttu-id="f6882-125">Boîte de dialogue de configuration de l’onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-125">Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Exemple de configuration modale d’onglet." border="false":::

### <a name="anatomy-tab-configuration-dialog"></a><span data-ttu-id="f6882-127">Anatomie : boîte de dialogue de configuration de l’onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-127">Anatomy: Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un modèle de configuration d’onglet." border="false":::

|<span data-ttu-id="f6882-129">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6882-129">Counter</span></span>|<span data-ttu-id="f6882-130">Description</span><span class="sxs-lookup"><span data-stu-id="f6882-130">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6882-131">1</span><span class="sxs-lookup"><span data-stu-id="f6882-131">1</span></span>|<span data-ttu-id="f6882-132">**Logo de l’application**: logo d’application en couleur complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6882-132">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="f6882-133">2</span><span class="sxs-lookup"><span data-stu-id="f6882-133">2</span></span>|<span data-ttu-id="f6882-134">**Nom de l’application**: nom complet de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6882-134">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="f6882-135">3</span><span class="sxs-lookup"><span data-stu-id="f6882-135">3</span></span>|<span data-ttu-id="f6882-136">**iframe**: espace réactif pour le contenu de votre application (par exemple, paramètres d’onglet ou authentification).</span><span class="sxs-lookup"><span data-stu-id="f6882-136">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="f6882-137">4 </span><span class="sxs-lookup"><span data-stu-id="f6882-137">4</span></span>|<span data-ttu-id="f6882-138">**À** propos du lien : ouvre une boîte de dialogue affichant plus d’informations sur l’application, telles qu’une description complète, les autorisations requises par l’application et des liens vers votre politique de confidentialité et les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="f6882-138">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>|
|<span data-ttu-id="f6882-139">5 </span><span class="sxs-lookup"><span data-stu-id="f6882-139">5</span></span>|<span data-ttu-id="f6882-140">**Bouton Fermer :** ferme la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f6882-140">**Close button**: Closes the dialog.</span></span>|
|<span data-ttu-id="f6882-141">6 </span><span class="sxs-lookup"><span data-stu-id="f6882-141">6</span></span>|<span data-ttu-id="f6882-142">**Option Avertir les membres de l’équipe**: la boîte de dialogue demande aux utilisateurs s’ils souhaitent créer un billet pour informer d’autres utilisateurs qu’ils ont ajouté un onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-142">**Notify team members option**: The dialog asks users if they want to create a post letting others know they added a tab.</span></span>|
|<span data-ttu-id="f6882-143">7 </span><span class="sxs-lookup"><span data-stu-id="f6882-143">7</span></span>|<span data-ttu-id="f6882-144">**Bouton Précédent**: passe à l’étape précédente en fonction de l’endroit où la boîte de dialogue s’est ouverte.</span><span class="sxs-lookup"><span data-stu-id="f6882-144">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="f6882-145">8 </span><span class="sxs-lookup"><span data-stu-id="f6882-145">8</span></span>|<span data-ttu-id="f6882-146">**Bouton Enregistrer :** termine la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-146">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="f6882-147">Authentification par onglet avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="f6882-147">Tab authentication with single sign-on</span></span>

<span data-ttu-id="f6882-148">Vous pouvez ajouter une étape dans laquelle les utilisateurs doivent d’abord se connecter avec leurs informations d’identification Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f6882-148">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="f6882-149">Cette méthode d’authentification est appelée authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="f6882-149">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Exemple d’écran d’authentification par onglet." border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a><span data-ttu-id="f6882-151">Concevoir une configuration d’onglet avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f6882-151">Design a tab setup with UI templates</span></span>

<span data-ttu-id="f6882-152">Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre expérience de configuration d’onglets :</span><span class="sxs-lookup"><span data-stu-id="f6882-152">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="f6882-153">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="f6882-153">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="f6882-154">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="f6882-154">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="f6882-155">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="f6882-155">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="f6882-156">Afficher un onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-156">View a tab</span></span>

<span data-ttu-id="f6882-157">Les onglets offrent une expérience web en plein écran dans Teams où vous pouvez afficher du contenu collaboratif (tableaux de tâches et tableaux de bord, par exemple) et des informations importantes.</span><span class="sxs-lookup"><span data-stu-id="f6882-157">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f6882-158">Desktop</span><span class="sxs-lookup"><span data-stu-id="f6882-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="L’exemple montre un onglet avec un tableau des tâches." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f6882-160">Mobile</span><span class="sxs-lookup"><span data-stu-id="f6882-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="L’exemple montre un onglet mobile avec un tableau des tâches." border="false":::

---

### <a name="anatomy-tab"></a><span data-ttu-id="f6882-162">Anatomie : tabulation</span><span class="sxs-lookup"><span data-stu-id="f6882-162">Anatomy: Tab</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f6882-163">Desktop</span><span class="sxs-lookup"><span data-stu-id="f6882-163">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|<span data-ttu-id="f6882-165">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6882-165">Counter</span></span>|<span data-ttu-id="f6882-166">Description</span><span class="sxs-lookup"><span data-stu-id="f6882-166">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6882-167">1</span><span class="sxs-lookup"><span data-stu-id="f6882-167">1</span></span>|<span data-ttu-id="f6882-168">**Nom de l’onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-168">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="f6882-169">2</span><span class="sxs-lookup"><span data-stu-id="f6882-169">2</span></span>|<span data-ttu-id="f6882-170">**Dépassement de tabulation**: ouvre les actions d’onglet, telles que renommer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="f6882-170">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="f6882-171">3</span><span class="sxs-lookup"><span data-stu-id="f6882-171">3</span></span>|<span data-ttu-id="f6882-172">**Conversation par onglet**: ouvre une conversation à droite, ce qui permet aux utilisateurs d’avoir une conversation à côté du contenu.</span><span class="sxs-lookup"><span data-stu-id="f6882-172">**Tab chat**: Opens a chat to the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="f6882-173">4 </span><span class="sxs-lookup"><span data-stu-id="f6882-173">4</span></span>|<span data-ttu-id="f6882-174">**iframe**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6882-174">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="f6882-175">Mobile</span><span class="sxs-lookup"><span data-stu-id="f6882-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un onglet." border="false":::

|<span data-ttu-id="f6882-177">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6882-177">Counter</span></span>|<span data-ttu-id="f6882-178">Description</span><span class="sxs-lookup"><span data-stu-id="f6882-178">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6882-179">1</span><span class="sxs-lookup"><span data-stu-id="f6882-179">1</span></span>|<span data-ttu-id="f6882-180">**Nom de l’onglet**: étiquette de navigation pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-180">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="f6882-181">2</span><span class="sxs-lookup"><span data-stu-id="f6882-181">2</span></span>|<span data-ttu-id="f6882-182">**Conversation par onglet**: ouvre une conversation qui permet aux utilisateurs d’avoir une conversation à côté du contenu.</span><span class="sxs-lookup"><span data-stu-id="f6882-182">**Tab chat**: Opens a chat that allows users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="f6882-183">3</span><span class="sxs-lookup"><span data-stu-id="f6882-183">3</span></span>|<span data-ttu-id="f6882-184">**webview**: affiche le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="f6882-184">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a><span data-ttu-id="f6882-185">Conception d’un onglet avec des modèles d’interface utilisateur et des composants avancés</span><span class="sxs-lookup"><span data-stu-id="f6882-185">Designing a tab with UI templates and advanced components</span></span>

<span data-ttu-id="f6882-186">Utilisez l’un des Teams et composants suivants pour vous aider à concevoir votre expérience d’onglet :</span><span class="sxs-lookup"><span data-stu-id="f6882-186">Use one of the following Teams templates and components to help design your tab experience:</span></span>

* <span data-ttu-id="f6882-187">[Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.</span><span class="sxs-lookup"><span data-stu-id="f6882-187">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="f6882-188">[Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.</span><span class="sxs-lookup"><span data-stu-id="f6882-188">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="f6882-189">[Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.</span><span class="sxs-lookup"><span data-stu-id="f6882-189">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="f6882-190">[Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.</span><span class="sxs-lookup"><span data-stu-id="f6882-190">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="f6882-191">[État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.</span><span class="sxs-lookup"><span data-stu-id="f6882-191">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="f6882-192">[Navigation gauche :](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation.</span><span class="sxs-lookup"><span data-stu-id="f6882-192">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="f6882-193">En règle générale, vous devez conserver la navigation par onglets au minimum.</span><span class="sxs-lookup"><span data-stu-id="f6882-193">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="f6882-194">Utiliser un onglet pour collaborer</span><span class="sxs-lookup"><span data-stu-id="f6882-194">Use a tab to collaborate</span></span>

<span data-ttu-id="f6882-195">Les onglets facilitent les conversations sur le contenu dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="f6882-195">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="f6882-196">Discussion sur les threads</span><span class="sxs-lookup"><span data-stu-id="f6882-196">Thread discussion</span></span>

<span data-ttu-id="f6882-197">Les utilisateurs peuvent publier automatiquement sur un canal ou une conversation une fois qu’ils ont ajouté un nouvel onglet. Non seulement cela informe les membres de l’équipe du nouveau contenu et fournit un lien vers l’onglet, mais permet aux utilisateurs de commencer à parler de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-197">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f6882-198">Desktop</span><span class="sxs-lookup"><span data-stu-id="f6882-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="L’exemple montre un onglet abordé dans un thread de canal." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f6882-200">Mobile</span><span class="sxs-lookup"><span data-stu-id="f6882-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="L’exemple montre un onglet mobile abordé dans un thread de canal." border="false":::

---

### <a name="tab-chat"></a><span data-ttu-id="f6882-202">Conversation par onglets</span><span class="sxs-lookup"><span data-stu-id="f6882-202">Tab chat</span></span>

<span data-ttu-id="f6882-203">Les utilisateurs peuvent avoir une conversation en regard du contenu de l’onglet qu’ils visionnagent.</span><span class="sxs-lookup"><span data-stu-id="f6882-203">Users can have a conversation next to the tab content they're viewing.</span></span> <span data-ttu-id="f6882-204">Sur le bureau, la conversation s’ouvre sur le côté du contenu de l’application.</span><span class="sxs-lookup"><span data-stu-id="f6882-204">On desktop, the chat opens to the side of the app content.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f6882-205">Desktop</span><span class="sxs-lookup"><span data-stu-id="f6882-205">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="L’exemple montre un onglet avec une conversation ouverte sur le côté droit." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="f6882-207">Mobile</span><span class="sxs-lookup"><span data-stu-id="f6882-207">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="L’exemple montre un onglet mobile avec une zone de conversation dans le contexte." border="false":::

---

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="f6882-209">Autorisations et affichages basés sur les rôles</span><span class="sxs-lookup"><span data-stu-id="f6882-209">Permissions and role-based views</span></span>

<span data-ttu-id="f6882-210">L’expérience d’onglet peut être différente pour les utilisateurs en fonction de leurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="f6882-210">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="f6882-211">Par exemple, un utilisateur peut accéder à l’onglet sans avoir à se connecter.</span><span class="sxs-lookup"><span data-stu-id="f6882-211">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="f6882-212">Toutefois, un autre utilisateur doit se connecter et voir du contenu légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="f6882-212">Another user, however, must sign in and see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="f6882-213">Gérer un onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-213">Manage a tab</span></span>

<span data-ttu-id="f6882-214">Vous pouvez inclure des options pour renommer, supprimer ou modifier un onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-214">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="f6882-215">Anatomie : menu Onglet</span><span class="sxs-lookup"><span data-stu-id="f6882-215">Anatomy: Tab menu</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f6882-216">Desktop</span><span class="sxs-lookup"><span data-stu-id="f6882-216">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu Onglet." border="false":::

|<span data-ttu-id="f6882-218">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6882-218">Counter</span></span>|<span data-ttu-id="f6882-219">Description</span><span class="sxs-lookup"><span data-stu-id="f6882-219">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6882-220">1</span><span class="sxs-lookup"><span data-stu-id="f6882-220">1</span></span>|<span data-ttu-id="f6882-221">**Paramètres**: (Facultatif) Permet aux utilisateurs de modifier les paramètres d’un onglet après son ajout.</span><span class="sxs-lookup"><span data-stu-id="f6882-221">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="f6882-222">2</span><span class="sxs-lookup"><span data-stu-id="f6882-222">2</span></span>|<span data-ttu-id="f6882-223">**Renommer**: les utilisateurs peuvent donner à l’onglet un nom significatif pour le canal, la conversation ou la réunion.</span><span class="sxs-lookup"><span data-stu-id="f6882-223">**Rename**: Users can give the tab a name that’s meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="f6882-224">3</span><span class="sxs-lookup"><span data-stu-id="f6882-224">3</span></span>|<span data-ttu-id="f6882-225">**Supprimer**: supprime l’onglet du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f6882-225">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="f6882-226">Mobile</span><span class="sxs-lookup"><span data-stu-id="f6882-226">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="Illustration montrant l’anatomie de l’interface utilisateur d’un menu onglet mobile." border="false":::

|<span data-ttu-id="f6882-228">Compteur</span><span class="sxs-lookup"><span data-stu-id="f6882-228">Counter</span></span>|<span data-ttu-id="f6882-229">Description</span><span class="sxs-lookup"><span data-stu-id="f6882-229">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f6882-230">1</span><span class="sxs-lookup"><span data-stu-id="f6882-230">1</span></span>|<span data-ttu-id="f6882-231">**Ouvrir dans le navigateur**: ouvre l’application dans le navigateur par défaut de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="f6882-231">**Open in browser**: Opens the app in the device’s default browser.</span></span>|
|<span data-ttu-id="f6882-232">2</span><span class="sxs-lookup"><span data-stu-id="f6882-232">2</span></span>|<span data-ttu-id="f6882-233">**Lien copier :** les utilisateurs peuvent copier et partager un lien vers l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-233">**Copy link**: Users can copy and share a link to the tab.</span></span>|
|<span data-ttu-id="f6882-234">3</span><span class="sxs-lookup"><span data-stu-id="f6882-234">3</span></span>|<span data-ttu-id="f6882-235">**Paramètres**: (Facultatif) Modifier les paramètres d’un onglet après son ajout.</span><span class="sxs-lookup"><span data-stu-id="f6882-235">**Settings**: (Optional) Modify a tab’s settings after it's been added.</span></span>|
|<span data-ttu-id="f6882-236">4 </span><span class="sxs-lookup"><span data-stu-id="f6882-236">4</span></span>|<span data-ttu-id="f6882-237">**Renommer**: les utilisateurs peuvent donner à l’onglet un nom significatif pour le canal, la conversation ou la réunion.</span><span class="sxs-lookup"><span data-stu-id="f6882-237">**Rename**: Users can give the tab a name that's meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="f6882-238">5 </span><span class="sxs-lookup"><span data-stu-id="f6882-238">5</span></span>|<span data-ttu-id="f6882-239">**Supprimer**: supprime l’onglet du canal, de la conversation ou de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f6882-239">**Delete**: Removes the tab from the channel, chat, or meeting.</span></span>|

---

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="f6882-240">Notifications d’onglet et liaison approfondie</span><span class="sxs-lookup"><span data-stu-id="f6882-240">Tab notifications and deep linking</span></span>

<span data-ttu-id="f6882-241">Vous pouvez envoyer un message avec un lien profond vers votre onglet. Par exemple, une carte affiche un résumé des données de bogue qu’un utilisateur peut sélectionner pour voir l’intégralité du bogue dans un onglet. L’envoi de messages sur l’activité de l’onglet augmente la sensibilisation sans avertir explicitement tout le monde (c’est-à-dire, activité sans bruit).</span><span class="sxs-lookup"><span data-stu-id="f6882-241">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="f6882-242">Vous pouvez également @mention utilisateurs spécifiques si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f6882-242">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="f6882-243">Informez les utilisateurs de l’activité de l’onglet de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="f6882-243">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="f6882-244">**Bot**: cette méthode est préférée, en particulier si le thread d’onglet est ciblé.</span><span class="sxs-lookup"><span data-stu-id="f6882-244">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="f6882-245">La conversation threadée de l’onglet est déplacée dans l’affichage comme étant récemment active.</span><span class="sxs-lookup"><span data-stu-id="f6882-245">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="f6882-246">Cette méthode permet également une certaine complexité dans la façon dont la notification est envoyée.</span><span class="sxs-lookup"><span data-stu-id="f6882-246">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="f6882-247">**Message**: un message s’affiche dans le flux d’activités de l’utilisateur avec un [lien profond vers l’onglet](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f6882-247">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="f6882-248">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="f6882-248">Best practices</span></span>

<span data-ttu-id="f6882-249">Utilisez ces recommandations pour créer une expérience d’application de qualité :</span><span class="sxs-lookup"><span data-stu-id="f6882-249">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="f6882-250">Collaboration</span><span class="sxs-lookup"><span data-stu-id="f6882-250">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Illustration shows what to do with tab navigation design." border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="f6882-252">À faire : faciliter la conversation</span><span class="sxs-lookup"><span data-stu-id="f6882-252">Do: Facilitate conversation</span></span>

<span data-ttu-id="f6882-253">Inclure du contenu et des composants dont les utilisateurs peuvent parler.</span><span class="sxs-lookup"><span data-stu-id="f6882-253">Include content and components people can talk about.</span></span> <span data-ttu-id="f6882-254">S’il ne s’intègre pas dans le contexte d’une conversation, d’un canal ou d’une réunion, il n’appartient pas à votre onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-254">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="L’exemple montre ce qu’il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="f6882-256">À ne pas faire : traiter votre onglet comme n’importe quelle autre page web</span><span class="sxs-lookup"><span data-stu-id="f6882-256">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="f6882-257">Un onglet n’est pas une page web que quelqu’un peut afficher une seule fois.</span><span class="sxs-lookup"><span data-stu-id="f6882-257">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="f6882-258">Un onglet doit afficher le contenu le plus important et pertinent dont les utilisateurs ont besoin pour accomplir quelque chose ensemble.</span><span class="sxs-lookup"><span data-stu-id="f6882-258">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="f6882-259">Navigation</span><span class="sxs-lookup"><span data-stu-id="f6882-259">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Exemple montrant comment faire avec la conception de navigation par onglets." border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="f6882-261">À faire : limiter les tâches et les données</span><span class="sxs-lookup"><span data-stu-id="f6882-261">Do: Limit tasks and data</span></span>

<span data-ttu-id="f6882-262">Les onglets fonctionnent mieux lorsqu’ils s’adressent à des besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f6882-262">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="f6882-263">Inclure un ensemble limité de tâches et de données pertinentes pour l’équipe ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="f6882-263">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de navigation par onglets." border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="f6882-265">À ne pas faire : incorporer l’intégralité de votre application</span><span class="sxs-lookup"><span data-stu-id="f6882-265">Don't: Embed your entire app</span></span>

<span data-ttu-id="f6882-266">L’utilisation d’un onglet pour afficher l’ensemble d’une application avec une navigation à plusieurs niveaux et des interactions complexes entraîne une surcharge d’informations.</span><span class="sxs-lookup"><span data-stu-id="f6882-266">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="f6882-267">Configuration</span><span class="sxs-lookup"><span data-stu-id="f6882-267">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Illustration montrant ce qu’il faut faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="f6882-269">À faire : restez simple</span><span class="sxs-lookup"><span data-stu-id="f6882-269">Do: Keep it simple</span></span>

<span data-ttu-id="f6882-270">Si votre application nécessite une authentification, essayez d’intégrer l’authentification unique (SSO) Microsoft pour une expérience de authentification plus transparente.</span><span class="sxs-lookup"><span data-stu-id="f6882-270">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="f6882-271">En outre, incluez uniquement les informations essentielles et les étapes à suivre pour ajouter l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-271">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec la conception de la configuration de l’onglet." border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="f6882-273">À ne pas faire : trop d’étapes</span><span class="sxs-lookup"><span data-stu-id="f6882-273">Don't: Have too many steps</span></span>

<span data-ttu-id="f6882-274">Supprimez les étapes inutiles pour ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="f6882-274">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="f6882-275">Thèmes</span><span class="sxs-lookup"><span data-stu-id="f6882-275">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Illustration montrant ce qu’il faut faire avec les tabulations." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="f6882-277">À faire : tirer parti des jetons Teams couleur</span><span class="sxs-lookup"><span data-stu-id="f6882-277">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="f6882-278">Chaque Teams thème possède son propre modèle de couleurs.</span><span class="sxs-lookup"><span data-stu-id="f6882-278">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="f6882-279">Pour gérer automatiquement les modifications de thème, utilisez des jetons <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de couleur (interface</a> utilisateur Fluent) dans votre conception.</span><span class="sxs-lookup"><span data-stu-id="f6882-279">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec les tabulations." border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="f6882-281">À ne pas faire : valeurs de couleur de code dur</span><span class="sxs-lookup"><span data-stu-id="f6882-281">Don't: Hard code color values</span></span>

<span data-ttu-id="f6882-282">Si vous n’utilisez pas Teams couleur, vos conceptions seront moins évolutives et prenons plus de temps à gérer.</span><span class="sxs-lookup"><span data-stu-id="f6882-282">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
