---
title: Applications dans les réunions Teams
author: laujan
description: vue d’ensemble des applications dans les réunions Teams en fonction du rôle du participant et de l’utilisateur
ms.topic: overview
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 217737cbbf73104d4d78cf817e6df0244229c53c
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797756"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="0eff9-104">Applications dans les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="0eff9-104">Apps in Teams meetings</span></span>

<span data-ttu-id="0eff9-105">Les réunions sont essentielles à la productivité dans Teams.</span><span class="sxs-lookup"><span data-stu-id="0eff9-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="0eff9-106">Ils permettent la collaboration, le partenariat, la communication informée et les commentaires partagés dans un forum actif et inclusif.</span><span class="sxs-lookup"><span data-stu-id="0eff9-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="0eff9-107">En tant que développeur, vous pouvez créer des applications [configurables](../tabs/what-are-tabs.md#how-do-tabs-work) [d’onglet,](../messaging-extensions/what-are-messaging-extensions.md) de [bot](../bots/what-are-bots.md)et d’extension de message pour améliorer et enrichir une expérience de réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="0eff9-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="0eff9-108">Les utilisateurs de réunion peuvent accéder aux applications, via la galerie d’onglets, pour activer des scénarios pertinents tels que la préparation d’un tableau kanban, le lancement d’une boîte de dialogue actionnable pendant la réunion ou la création d’un sondage post-réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="0eff9-109">Votre application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion en fonction de l’état des participants.</span><span class="sxs-lookup"><span data-stu-id="0eff9-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="0eff9-110">L’extensibilité des applications de réunion Teams se concentre sur trois concepts :</span><span class="sxs-lookup"><span data-stu-id="0eff9-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="0eff9-111">✔ cycle **de vie de la** réunion — avant, pendant et après la période de réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="0eff9-112">✔ rôle **de participant :** organisateur de réunion, présentateur ou participant.</span><span class="sxs-lookup"><span data-stu-id="0eff9-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="0eff9-113">✔ type **d’utilisateur** : utilisateur teams in-tenant, invité, fédéré ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="0eff9-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="0eff9-114">Scénarios de cycle de vie de réunion</span><span class="sxs-lookup"><span data-stu-id="0eff9-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="0eff9-115">Onglets</span><span class="sxs-lookup"><span data-stu-id="0eff9-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0eff9-116">Comme avec toutes les applications d’onglet, votre application devra suivre le flux d’authentification [sso teams](../tabs/how-to/authentication/auth-aad-sso.md) pour les onglets.</span><span class="sxs-lookup"><span data-stu-id="0eff9-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="0eff9-117">Les clients mobiles ne supportent les onglets que dans les surfaces de pré et de post-réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-117">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="0eff9-118">Les expériences en réunion (boîte de dialogue et panneau en réunion) sur mobile seront bientôt disponibles</span><span class="sxs-lookup"><span data-stu-id="0eff9-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="0eff9-119">Expérience d’application avant la réunion</span><span class="sxs-lookup"><span data-stu-id="0eff9-119">Pre-meeting app experience</span></span>

<span data-ttu-id="0eff9-120">**Expérience préalable à la réunion :**</span><span class="sxs-lookup"><span data-stu-id="0eff9-120">**Pre-meeting experience:**</span></span>

![expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="0eff9-122">**Onglet Avant la réunion :**</span><span class="sxs-lookup"><span data-stu-id="0eff9-122">**Pre-meeting tab:**</span></span>

![Affichage de l’onglet avant la réunion](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="0eff9-124">✔ utilisateurs autorisés peuvent ajouter des applications à une réunion via la galerie d’onglets de deux manières :</span><span class="sxs-lookup"><span data-stu-id="0eff9-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="0eff9-125">&emsp;&emsp;&#9679; via **l’onglet Détails** du formulaire de planification Teams.</span><span class="sxs-lookup"><span data-stu-id="0eff9-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="0eff9-126">&emsp;&emsp;&#9679; via l’onglet **Conversation** de réunion dans une réunion existante.</span><span class="sxs-lookup"><span data-stu-id="0eff9-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="0eff9-127">✔ onglets sont accessibles dans les **pages** **Détails** des réunions et Conversations à l’aide d’un bouton d’icône plus (➕).</span><span class="sxs-lookup"><span data-stu-id="0eff9-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="0eff9-128">✔ disposition de l’onglet doit être organisée s’il y a plus de dix sondages ou enquêtes.</span><span class="sxs-lookup"><span data-stu-id="0eff9-128">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="0eff9-129">Expérience d’application en réunion</span><span class="sxs-lookup"><span data-stu-id="0eff9-129">In-meeting app experience</span></span>

<span data-ttu-id="0eff9-130">✔ applications de réunion seront hébergées dans la barre supérieure de la fenêtre de conversation et en tant qu’expérience d’onglet dans la réunion via l’onglet en réunion. Lorsque les utilisateurs ajoutent un onglet à une  réunion par le biais de la galerie d’onglets, les applications qui sont pendant les expériences de réunion sont surface.</span><span class="sxs-lookup"><span data-stu-id="0eff9-130">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="0eff9-131">✔ utilisateurs autorisés peuvent ajouter des applications pendant la réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-131">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="0eff9-132">✔ lors du chargement dans le contexte d’une réunion, les applications pourront tirer parti du SDK client Teams pour accéder au , et pour restituer correctement `meetingId` `userMri` `frameContext` l’expérience.</span><span class="sxs-lookup"><span data-stu-id="0eff9-132">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="0eff9-133">✔ l’exportation d’un résultat d’une enquête ou d’un sondage doit avertir les utilisateurs indiquant « résultats téléchargés avec succès ».</span><span class="sxs-lookup"><span data-stu-id="0eff9-133">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="0eff9-134">✔ pour qu’une application soit visible dans une réunion Teams dans deux domaines :</span><span class="sxs-lookup"><span data-stu-id="0eff9-134">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="0eff9-135">&emsp;&emsp;&#9679; panneau **latéral**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-135">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="0eff9-136">Si le _manifeste de votre_ application spécifie que votre onglet est optimisé pour le panneau latéral, c’est là qu’il sera affiché. [](create-apps-for-teams-meetings.md#during-a-meeting)</span><span class="sxs-lookup"><span data-stu-id="0eff9-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="0eff9-137">Il peut également faire partie d’une expérience de partage de bac, sous réserve des instructions de conception spécifiées.</span><span class="sxs-lookup"><span data-stu-id="0eff9-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="0eff9-138">&emsp;&emsp;&#9679; boîte **de dialogue En réunion.**</span><span class="sxs-lookup"><span data-stu-id="0eff9-138">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="0eff9-139">Utilisez la boîte de dialogue de réunion pour présenter du contenu actionnable aux participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="0eff9-140">*Voir* [Créer des applications pour les réunions Teams.](create-apps-for-teams-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="0eff9-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="0eff9-141">**Expérience en réunion :**</span><span class="sxs-lookup"><span data-stu-id="0eff9-141">**In-meeting experience:**</span></span>

![expérience en réunion](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Affichage de la boîte de dialogue en réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="0eff9-144">**Boîte de dialogue actionnable en réunion pour les utilisateurs :**</span><span class="sxs-lookup"><span data-stu-id="0eff9-144">**In-meeting actionable dialog for users:**</span></span>

![affichage de boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="0eff9-146">Expérience d’application post-réunion</span><span class="sxs-lookup"><span data-stu-id="0eff9-146">Post-meeting app experience</span></span>

<span data-ttu-id="0eff9-147">**Expérience post-réunion :**</span><span class="sxs-lookup"><span data-stu-id="0eff9-147">**Post-meeting experience:**</span></span>

![affichage après la réunion](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="0eff9-149">✔ le scénario d’application post-réunion est similaire à l’expérience post-réunion actuelle avec l’avantage supplémentaire d’avoir des onglets qui existent dans la surface.</span><span class="sxs-lookup"><span data-stu-id="0eff9-149">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="0eff9-150">✔ utilisateurs autorisés peuvent ajouter des applications de la galerie d’onglets à une réunion  via l’onglet **Détails** du formulaire de planification Teams et l’onglet Conversation de réunion dans une réunion existante.</span><span class="sxs-lookup"><span data-stu-id="0eff9-150">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="0eff9-151">✔ disposition de l’onglet doit être organisée s’il y a plus de dix sondages ou enquêtes.</span><span class="sxs-lookup"><span data-stu-id="0eff9-151">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="0eff9-152">Bots</span><span class="sxs-lookup"><span data-stu-id="0eff9-152">Bots</span></span>

<span data-ttu-id="0eff9-153">Pour l’implémentation du bot, consultez la documentation relative aux [bots dans les réunions Teams.](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings)</span><span class="sxs-lookup"><span data-stu-id="0eff9-153">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="0eff9-154">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="0eff9-154">Messaging Extensions</span></span>

<span data-ttu-id="0eff9-155">Pour l’implémentation de l’extension de messagerie, consultez la documentation relative aux [extensions de messagerie dans la](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation des réunions Teams.</span><span class="sxs-lookup"><span data-stu-id="0eff9-155">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="0eff9-156">Rôles des participants et types d’utilisateurs dans une réunion</span><span class="sxs-lookup"><span data-stu-id="0eff9-156">Participant roles and user types in a meeting</span></span>

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="0eff9-158">Rôles des participants</span><span class="sxs-lookup"><span data-stu-id="0eff9-158">Participant roles</span></span>

<span data-ttu-id="0eff9-159">Vous pouvez concevoir votre application avec une autorisation spécifique au participant.</span><span class="sxs-lookup"><span data-stu-id="0eff9-159">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="0eff9-160">Par exemple, seuls un organisateur et/ou un présentateur peuvent créer un sondage dans les réunions.</span><span class="sxs-lookup"><span data-stu-id="0eff9-160">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="0eff9-161">Bien que les paramètres des participants par défaut soient déterminés par l’administrateur informatique d’une organisation, un organisateur de réunion peut vouloir modifier les paramètres d’une réunion spécifique.</span><span class="sxs-lookup"><span data-stu-id="0eff9-161">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="0eff9-162">Les organisateurs peuvent apporter ces modifications sur la page web Des options de réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-162">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="0eff9-163">**Organisateur**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-163">**Organizer**.</span></span> <span data-ttu-id="0eff9-164">L’organisateur prévoit une réunion, définit les options de la réunion, attribue des rôles de réunion et démarre la réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-164">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="0eff9-165">Seuls les utilisateurs possédant un compte M365 (possédant une licence Teams) peuvent être organisateurs et contrôler les autorisations des participants.</span><span class="sxs-lookup"><span data-stu-id="0eff9-165">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="0eff9-166">**Présentateur**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-166">**Presenter**.</span></span> <span data-ttu-id="0eff9-167">Les présentateurs ont presque les mêmes fonctionnalités que l’organisateur . toutefois, un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de réunion pour la session.</span><span class="sxs-lookup"><span data-stu-id="0eff9-167">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="0eff9-168">Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.</span><span class="sxs-lookup"><span data-stu-id="0eff9-168">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="0eff9-169">**Participant**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-169">**Attendee**.</span></span> <span data-ttu-id="0eff9-170">Un participant est un utilisateur qui a été invité à participer à une réunion, mais qui n’est pas autorisé à agir en tant que présentateur.</span><span class="sxs-lookup"><span data-stu-id="0eff9-170">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="0eff9-171">Les participants peuvent interagir avec d’autres membres de la réunion, mais ne peuvent pas gérer les paramètres de la réunion ou partager du contenu.</span><span class="sxs-lookup"><span data-stu-id="0eff9-171">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="0eff9-172">_Voir_ [ **rôles dans une réunion Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="0eff9-172">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="0eff9-173">Vous pouvez accéder à la page  **Options de** réunion comme suit :</span><span class="sxs-lookup"><span data-stu-id="0eff9-173">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="0eff9-174">&#11200; Teams, allez au  ![ logo calendrier, sélectionnez une réunion, puis les ](../assets/images/apps-in-meetings/calendar-logo.png) options de **réunion.**</span><span class="sxs-lookup"><span data-stu-id="0eff9-174">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="0eff9-175">&#11200; dans une invitation à une réunion, sélectionnez **Les options de réunion.**</span><span class="sxs-lookup"><span data-stu-id="0eff9-175">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="0eff9-176">&#11200; au cours d’une réunion, sélectionnez **Afficher les participants** et afficher l’icône des participants dans les ![ ](../assets/images/apps-in-meetings/show-participants.png) contrôles de réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-176">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="0eff9-177">Ensuite, au-dessus de la liste des participants, choisissez **Gérer les autorisations.**</span><span class="sxs-lookup"><span data-stu-id="0eff9-177">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="0eff9-178">Types d'utilisateur</span><span class="sxs-lookup"><span data-stu-id="0eff9-178">User types</span></span>

> [!NOTE]
> <span data-ttu-id="0eff9-179">Les types d’utilisateurs peuvent participer à des réunions et supposer l’un des rôles de participant décrits ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0eff9-179">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="0eff9-180">Le type d’utilisateur n’est pas exposé dans le cadre de **l’API getParticipantRole.**</span><span class="sxs-lookup"><span data-stu-id="0eff9-180">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="0eff9-181">**Dans le client**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-181">**In-tenant**.</span></span> <span data-ttu-id="0eff9-182">Ces utilisateurs appartiennent à l’organisation et ont des informations d’identification dans Azure Active Directory pour le client.</span><span class="sxs-lookup"><span data-stu-id="0eff9-182">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="0eff9-183">Il s’agit généralement d’employés à plein temps, sur site ou distants.</span><span class="sxs-lookup"><span data-stu-id="0eff9-183">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="0eff9-184">**Invité**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-184">**Guest**.</span></span> <span data-ttu-id="0eff9-185">Un invité est un participant d’une autre organisation qui a été invité à accéder à Teams ou à d’autres ressources dans le client de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="0eff9-185">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="0eff9-186">Les invités sont ajoutés à Active Directory de votre organisation et peuvent obtenir presque toutes les mêmes fonctionnalités Teams qu’un membre natif de l’équipe avec un accès total aux conversations, réunions et fichiers de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="0eff9-186">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="0eff9-187">_Voir_ [l’accès invité dans Microsoft Teams](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="0eff9-187">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="0eff9-188">**Fédéré/externe**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-188">**Federated/External**.</span></span> <span data-ttu-id="0eff9-189">Un utilisateur fédéré est un utilisateur Teams externe d’une autre organisation qui a été invité à participer à une réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-189">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="0eff9-190">Étant donné que ces utilisateurs disposent d’informations d’identification valides avec des partenaires fédérés, ils sont traités comme authentifiés par Teams, mais n’ont pas accès à vos équipes ou à d’autres ressources partagées de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="0eff9-190">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="0eff9-191">Si vous souhaitez que les utilisateurs externes accèdent aux équipes et aux canaux, l’accès invité peut être une meilleure option.</span><span class="sxs-lookup"><span data-stu-id="0eff9-191">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="0eff9-192">_Voir Gérer_ [l’accès externe dans Microsoft Teams](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="0eff9-192">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="0eff9-193">**Anonyme**.</span><span class="sxs-lookup"><span data-stu-id="0eff9-193">**Anonymous**.</span></span> <span data-ttu-id="0eff9-194">Les utilisateurs anonymes n’ont pas d’identité Active Directory et ne sont pas fédérés avec un client.</span><span class="sxs-lookup"><span data-stu-id="0eff9-194">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="0eff9-195">Le participant anonyme est comme un utilisateur externe, mais son identité n’est pas projetée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-195">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="0eff9-196">Les utilisateurs anonymes ne pourront pas accéder aux applications dans une fenêtre de réunion.</span><span class="sxs-lookup"><span data-stu-id="0eff9-196">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eff9-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0eff9-197">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0eff9-198">Concevoir votre application</span><span class="sxs-lookup"><span data-stu-id="0eff9-198">Design your app</span></span>](create-apps-for-teams-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="0eff9-199">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="0eff9-199">Build your app</span></span>](create-apps-for-teams-meetings.md)
