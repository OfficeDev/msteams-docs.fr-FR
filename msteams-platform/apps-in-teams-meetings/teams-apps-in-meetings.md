---
title: Applications dans les réunions Teams
author: laujan
description: vue d’ensemble des applications dans les réunions Teams en fonction du rôle du participant et de l’utilisateur
ms.topic: overview
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: ac4e270090dd89d370d37de88b8cba552b77a5cb
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382337"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="4ffe7-104">Applications dans les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="4ffe7-104">Apps in Teams meetings</span></span>

<span data-ttu-id="4ffe7-105">Les réunions permettent la collaboration, le partenariat, la communication éclairée et les commentaires partagés dans un forum actif et inclusif.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="4ffe7-106">L’application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion, y compris l’expérience de l’application avant, en réunion et après la réunion, en fonction de l’état du participant.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="4ffe7-107">Les utilisateurs finaux teams peuvent accéder aux applications pendant les réunions à l’aide de la galerie d’onglets, par exemple :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-107">Teams end-users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="4ffe7-108">Pré-phase d’un tableau kanban</span><span class="sxs-lookup"><span data-stu-id="4ffe7-108">Pre-stage a Kanban board</span></span>
* <span data-ttu-id="4ffe7-109">Lancer une boîte de dialogue actionnable en réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-109">Launch an in-meeting actionable dialog</span></span>
* <span data-ttu-id="4ffe7-110">Créer un sondage après la réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-110">Create a post-meeting poll</span></span>

<span data-ttu-id="4ffe7-111">L’extensibilité des applications de réunion Teams est basée sur les concepts suivants :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-111">Teams’ meeting app extensibility is based on the following concepts:</span></span>

<span data-ttu-id="4ffe7-112">✔ le cycle de vie des réunions possède des étapes telles qu’avant, pendant et après la période de réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-112">✔ Meeting lifecycle has stages such as before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="4ffe7-113">✔ rôles de participant à une réunion, tels que l’organisateur de la réunion, le présentateur ou le participant.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-113">✔ Participant roles in a meeting such as meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="4ffe7-114">✔ types d’utilisateurs dans une réunion telle que l’utilisateur teams en client, invité, fédéré ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-114">✔ User types in a meeting such as in-tenant, guest, federated, or anonymous Teams user.</span></span>

<span data-ttu-id="4ffe7-115">Cet article traite des informations sur le cycle de vie des réunions et sur la façon d’intégrer des onglets, des bots et des extensions de messagerie dans votre réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-115">This article covers information about the meeting lifecycle and how to integrate tabs, bots, and messaging extensions in your meeting.</span></span> <span data-ttu-id="4ffe7-116">Il vous permet également d’identifier les rôles des participants et d’utiliser différents types d’utilisateurs pour effectuer des tâches.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-116">It also enables you to identify participant roles and also use different user types to perform tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="4ffe7-117">Pour travailler avec les fonctionnalités d’extensibilité de l’application de réunion, vous devez avoir les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-117">To work with the meeting app extensibility features, you must have the appropriate permissions.</span></span>

### <a name="meeting-lifecycle"></a><span data-ttu-id="4ffe7-118">Cycle de vie des réunions</span><span class="sxs-lookup"><span data-stu-id="4ffe7-118">Meeting lifecycle</span></span>

<span data-ttu-id="4ffe7-119">Le cycle de vie des réunions consiste en une expérience d’application avant, en réunion et après la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-119">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="4ffe7-120">Vous pouvez intégrer des onglets, des bots et des extensions de messagerie à chaque étape du cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-120">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="4ffe7-121">Intégrer des onglets dans le cycle de vie de la réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-121">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="4ffe7-122">Les onglets permettent aux membres de l’équipe d’accéder aux services et au contenu dans un espace spécifique au sein d’un canal ou d’une conversation.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-122">Tabs allow team members to access services and content in a specific space within a channel or chat.</span></span> <span data-ttu-id="4ffe7-123">Cela permet à l’équipe de travailler directement avec des onglets et d’avoir des conversations sur les outils et les données disponibles dans les onglets.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-123">This lets the team work directly with tabs and have conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="4ffe7-124">Dans une réunion Teams, les utilisateurs peuvent ajouter un onglet en sélectionnant plus</span><span class="sxs-lookup"><span data-stu-id="4ffe7-124">In Teams meeting, users can add a tab by selecting plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="4ffe7-125">, et en choisissant l’application qu’ils souhaitent installer en tant qu’onglet.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-125">, and choosing the app that they want to install as a tab.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ffe7-126">Si vous avez intégré un onglet à votre réunion, votre application doit suivre le flux d’authentification unique [Teams pour](../tabs/how-to/authentication/auth-aad-sso.md) les onglets.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-126">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="4ffe7-127">Les clients mobiles ne supportent les onglets qu’aux étapes préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-127">Mobile clients support tabs only in pre and post meeting stages.</span></span> <span data-ttu-id="4ffe7-128">Les expériences en réunion qui sont des boîtes de dialogue et des panneaux en réunion ne sont actuellement pas disponibles sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-128">The in-meeting experiences that is in-meeting dialog and panel are currently not available on mobile.</span></span>
> * <span data-ttu-id="4ffe7-129">Les applications sont uniquement pris en charge dans les réunions privées programmées.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-129">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="4ffe7-130">Expérience d’application avant la réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-130">Pre-meeting app experience</span></span>

<span data-ttu-id="4ffe7-131">**Expérience préalable à la réunion :**</span><span class="sxs-lookup"><span data-stu-id="4ffe7-131">**Pre-meeting experience:**</span></span>

![expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="4ffe7-133">**Onglet Avant la réunion :**</span><span class="sxs-lookup"><span data-stu-id="4ffe7-133">**Pre-meeting tab:**</span></span>

![Affichage de l’onglet avant la réunion](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="4ffe7-135">✔ utilisateurs autorisés sont des utilisateurs qui peuvent ajouter des applications à une réunion pendant différentes étapes du cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-135">✔ Permissioned users are users who can add apps to a meeting during different stages of the meeting lifecycle.</span></span> <span data-ttu-id="4ffe7-136">Ces utilisateurs peuvent ajouter des applications à une réunion via la galerie d’onglets de deux manières :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-136">These users can add apps to a meeting through the tab gallery in two ways:</span></span>

   * <span data-ttu-id="4ffe7-137">Utilisation de **l’onglet Détails** du formulaire de planification Teams.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-137">Using the **Details** tab on the Teams scheduling form.</span></span>

   * <span data-ttu-id="4ffe7-138">Utilisation de l’onglet **Conversation** de réunion dans une réunion existante.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-138">Using the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="4ffe7-139">✔ onglets sont accessibles dans les pages **Détails** des réunions et **Conversations** à l’aide d’un bouton ➕ plus.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-139">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus ➕ button.</span></span>

<span data-ttu-id="4ffe7-140">✔ disposition des onglets doit être organisée s’il y a plus de dix sondages ou enquêtes.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-140">✔ Tab layout must be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="4ffe7-141">Expérience d’application en réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-141">In-meeting app experience</span></span>

<span data-ttu-id="4ffe7-142">✔ applications de réunion sont hébergées dans la barre supérieure de la fenêtre de conversation et en tant qu’expérience d’onglet dans la réunion à l’aide de l’onglet en réunion. Lorsque les utilisateurs ajoutent un onglet à une réunion via la galerie d’onglets, les applications qui sont pendant les expériences **de** réunion sont affichées.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-142">✔ Meeting apps are hosted in the top upper bar of the chat window and as in-meeting tab experience using the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences are shown.</span></span>

<span data-ttu-id="4ffe7-143">✔ utilisateurs autorisés peuvent ajouter des applications pendant la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-143">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="4ffe7-144">✔ lorsqu’elles sont chargées dans le contexte d’une réunion, les applications peuvent tirer parti du SDK client Teams pour accéder au , et pour restituer correctement `meetingId` `userMri` `frameContext` l’expérience.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-144">✔ When loaded in the context of a meeting, apps can leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="4ffe7-145">✔ exporter un résultat d’une enquête ou d’un sondage avertit les utilisateurs que les résultats ont été téléchargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-145">✔ Exporting a result of a survey or poll notifies the users that the results successfully downloaded.</span></span>

<span data-ttu-id="4ffe7-146">✔ Une application est visible dans une réunion Teams dans le panneau latéral ou dans la boîte de dialogue de la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-146">✔ An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span> <span data-ttu-id="4ffe7-147">Utilisez la boîte de dialogue de réunion pour présenter du contenu actionnable aux participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-147">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="4ffe7-148">*Voir* [Créer des applications pour les réunions Teams.](create-apps-for-teams-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-148">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ffe7-149">Le manifeste de votre application spécifie que votre onglet est [optimisé](create-apps-for-teams-meetings.md#during-a-meeting)pour le panneau latéral, c’est-à-dire l’endroit où il est affiché.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-149">Your app manifest specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it is displayed.</span></span> <span data-ttu-id="4ffe7-150">Il peut également faire partie d’une expérience de partage de bacs, sous réserve des instructions de conception spécifiées.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-150">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="4ffe7-151">Les images suivantes affichent l’application sous la mesure d’une boîte de dialogue de réunion et d’un panneau latéral distinct :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-151">The following images display the app as an in-meeting dialog box and as a separate side panel:</span></span>

![Expérience en réunion](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Affichage de la boîte de dialogue en réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a><span data-ttu-id="4ffe7-154">Boîte de dialogue actionnable en réunion pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4ffe7-154">In-meeting actionable dialog for users</span></span>

![Affichage de boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="4ffe7-156">Expérience d’application post-réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-156">Post-meeting app experience</span></span>

![Affichage après la réunion](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="4ffe7-158">✔ le scénario d’application post-réunion est similaire à l’expérience post-réunion actuelle avec l’avantage supplémentaire d’avoir des onglets qui existent dans la surface.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-158">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span>

<span data-ttu-id="4ffe7-159">✔ utilisateurs autorisés peuvent ajouter des applications de la galerie d’onglets à une réunion à l’aide de l’onglet **Détails** du formulaire de planification Teams et de l’onglet **Conversation** de réunion dans une réunion existante.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-159">✔ Permissioned users can add apps from the tab gallery to a meeting using the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="4ffe7-160">✔ la disposition des onglets doit être organisée lorsqu’il y a plus de dix sondages ou enquêtes.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-160">✔  Tab layout must be organized when there are more than ten polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="4ffe7-161">Intégrer des bots dans le cycle de vie de la réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-161">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="4ffe7-162">Pour l’implémentation du bot, commencez [par créer un bot,](../build-your-first-app/build-bot.md) puis continuez à créer [des applications pour les réunions Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-162">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="4ffe7-163">Intégrer des extensions de messagerie dans le cycle de vie de la réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-163">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="4ffe7-164">Pour l’implémentation de l’extension de messagerie, commencez par créer une [extension](../messaging-extensions/how-to/create-messaging-extension.md) de messagerie, puis continuez avec la création d’applications [pour les réunions Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-164">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="4ffe7-165">Rôles des participants et types d’utilisateurs dans une réunion</span><span class="sxs-lookup"><span data-stu-id="4ffe7-165">Participant roles and user types in a meeting</span></span>

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="4ffe7-167">Rôles des participants</span><span class="sxs-lookup"><span data-stu-id="4ffe7-167">Participant roles</span></span>

<span data-ttu-id="4ffe7-168">Les paramètres de participant par défaut sont déterminés par l’administrateur informatique d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-168">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="4ffe7-169">Les rôles des participants à une réunion sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-169">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="4ffe7-170">**Organisateur**: l’organisateur prévoit une réunion, définit les options de la réunion, attribue des rôles de réunion et démarre la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-170">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="4ffe7-171">Seuls les utilisateurs ayant un compte M365 avec une licence Teams peuvent être organisateurs et contrôler les autorisations des participants.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-171">Only users with a M365 account with a Teams license can be organizers and control attendee permissions.</span></span> <span data-ttu-id="4ffe7-172">Un organisateur de réunion peut modifier les paramètres d’une réunion spécifique.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-172">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="4ffe7-173">Les organisateurs peuvent apporter ces modifications sur la page web **Des options de** réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-173">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="4ffe7-174">**Présentateur**: les présentateurs ont les mêmes fonctionnalités que l’organisateur.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-174">**Presenter**: Presenters have the same capabilities as organizer.</span></span> <span data-ttu-id="4ffe7-175">Toutefois, un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de réunion pour la session.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-175">However, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="4ffe7-176">Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-176">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="4ffe7-177">**Participant**: un participant est un utilisateur qui a été invité à participer à une réunion, mais qui n’est pas autorisé à agir en tant que présentateur.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-177">**Attendee**: An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="4ffe7-178">Les participants peuvent interagir avec d’autres membres de la réunion, mais ne peuvent pas gérer les paramètres de la réunion ou partager du contenu.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-178">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="4ffe7-179">Seul un organisateur ou un présentateur peut ajouter, supprimer ou désinstaller des applications.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-179">Only an organizer or presenter can add, remove, or uninstall apps.</span></span> <span data-ttu-id="4ffe7-180">Seul l’organisateur ou le présentateur peut créer des sondages dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-180">Only organizer or presenter can create polls in a meeting.</span></span>

<span data-ttu-id="4ffe7-181">Pour plus d’informations, voir [les rôles dans une réunion Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-181">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="4ffe7-182">Vous pouvez accéder à la page  **Options de** réunion comme suit :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-182">You can access the  **Meeting options** page as follows:</span></span>

* <span data-ttu-id="4ffe7-183">Dans Teams,  allez au ![ logo ](../assets/images/apps-in-meetings/calendar-logo.png) calendrier, sélectionnez une réunion, puis les **options de réunion.**</span><span class="sxs-lookup"><span data-stu-id="4ffe7-183">In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

* <span data-ttu-id="4ffe7-184">Dans une invitation à une réunion, sélectionnez **Les options de réunion.**</span><span class="sxs-lookup"><span data-stu-id="4ffe7-184">In a meeting invitation, select **Meeting options**.</span></span>

* <span data-ttu-id="4ffe7-185">Au cours d’une réunion, **sélectionnez Afficher les participants** ![ et afficher l’icône des participants ](../assets/images/apps-in-meetings/show-participants.png) dans les contrôles de réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-185">During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="4ffe7-186">Ensuite, au-dessus de la liste des participants, choisissez **Gérer les autorisations.**</span><span class="sxs-lookup"><span data-stu-id="4ffe7-186">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="4ffe7-187">Types d'utilisateur</span><span class="sxs-lookup"><span data-stu-id="4ffe7-187">User types</span></span>

> [!NOTE]
> <span data-ttu-id="4ffe7-188">Les utilisateurs avec des types d’utilisateurs spécifiques qui leur sont affectés peuvent participer à des réunions et assumer l’un des rôles de participant décrits dans [les rôles de participant.](#participant-roles)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-188">Users with specific user types assigned to them can join meetings and assume one of the participant roles described in [participant roles](#participant-roles).</span></span> <span data-ttu-id="4ffe7-189">Le type d’utilisateur n’est pas inclus dans **l’API getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="4ffe7-189">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="4ffe7-190">Les types d’utilisateurs suivants identifient ce que chaque utilisateur peut faire et ce à quoi il peut accéder :</span><span class="sxs-lookup"><span data-stu-id="4ffe7-190">The following user types identify what each user can do and what they can access:</span></span>

* <span data-ttu-id="4ffe7-191">**Dans le client :** les utilisateurs dans le client appartiennent à l’organisation et ont des informations d’identification dans Azure Active Directory (AAD) pour le client.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-191">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="4ffe7-192">Il s’agit généralement d’employés à plein temps, sur site ou distants.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-192">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="4ffe7-193">Un utilisateur dans le client peut être organisateur, présentateur ou participant.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-193">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="4ffe7-194">**Invité**: un invité est un participant d’une autre organisation invité à accéder à Teams ou à d’autres ressources dans le client de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-194">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="4ffe7-195">Les invités sont ajoutés au AAD de votre organisation et ont les mêmes fonctionnalités Teams qu’un membre natif de l’équipe ayant accès aux conversations, réunions et fichiers de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-195">Guests are added to your organization’s AAD and have the same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="4ffe7-196">Un utilisateur invité peut être organisateur, présentateur ou participant.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-196">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="4ffe7-197">Pour plus d’informations, voir [l’accès invité dans Teams.](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-197">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="4ffe7-198">**Fédéré ou externe**: un utilisateur fédéré est un utilisateur Teams externe dans une autre organisation qui a été invité à participer à une réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-198">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="4ffe7-199">Ces utilisateurs ont des informations d’identification valides avec des partenaires fédérés et sont autorisés par Teams.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-199">These users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="4ffe7-200">Ils n’ont pas accès à vos équipes ou à d’autres ressources partagées de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-200">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="4ffe7-201">L’accès invité est une meilleure option pour les utilisateurs externes qui ont accès aux équipes et aux canaux.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-201">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="4ffe7-202">Pour plus d’informations, voir [gérer l’accès externe dans Teams.](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="4ffe7-202">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>
* <span data-ttu-id="4ffe7-203">**Anonyme**: les utilisateurs anonymes n’ont pas d’identité AAD et ne sont pas fédérés avec un client.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-203">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="4ffe7-204">Le participant anonyme est comme un utilisateur externe, mais son identité n’est pas projetée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-204">The anonymous participant is like an external user, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="4ffe7-205">Les utilisateurs anonymes ne peuvent pas accéder aux applications dans une fenêtre de réunion.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-205">Anonymous users are not able to access apps in a meeting window.</span></span> <span data-ttu-id="4ffe7-206">Un utilisateur anonyme ne peut pas être un organisateur, mais peut être présentateur ou participant.</span><span class="sxs-lookup"><span data-stu-id="4ffe7-206">An anonymous user cannot be an organizer but can be a presenter or attendee.</span></span>

## <a name="see-also"></a><span data-ttu-id="4ffe7-207">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4ffe7-207">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ffe7-208">Tab</span><span class="sxs-lookup"><span data-stu-id="4ffe7-208">Tab</span></span>](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ffe7-209">Bot</span><span class="sxs-lookup"><span data-stu-id="4ffe7-209">Bot</span></span>](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ffe7-210">Extension de la messagerie</span><span class="sxs-lookup"><span data-stu-id="4ffe7-210">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ffe7-211">Concevoir votre application</span><span class="sxs-lookup"><span data-stu-id="4ffe7-211">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a><span data-ttu-id="4ffe7-212">Prochaines étapes</span><span class="sxs-lookup"><span data-stu-id="4ffe7-212">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ffe7-213">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="4ffe7-213">Build your app</span></span>](create-apps-for-teams-meetings.md)
