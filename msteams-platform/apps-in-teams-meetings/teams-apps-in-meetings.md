---
title: Réunions des applications dans teams
author: laujan
description: vue d’ensemble des applications dans les réunions teams en fonction des participants et du rôle d’utilisateur
ms.topic: overview
ms.author: lajanuar
keywords: applications Team Apps Meeting User Role Role API
ms.openlocfilehash: db14049d3150eaaa9634b4fa535a989528b1c6a2
ms.sourcegitcommit: e70d41ae793a407fdbb71bc79ef7b67b40386c96
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/19/2020
ms.locfileid: "49358020"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="7c75d-104">Réunions des applications dans teams</span><span class="sxs-lookup"><span data-stu-id="7c75d-104">Apps in Teams meetings</span></span>

<span data-ttu-id="7c75d-105">Les réunions sont les clés de la productivité dans Teams.</span><span class="sxs-lookup"><span data-stu-id="7c75d-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="7c75d-106">Ils permettent la collaboration, le partenariat, la communication informée et le partage de commentaires dans un forum inclusif et actif.</span><span class="sxs-lookup"><span data-stu-id="7c75d-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="7c75d-107">En tant que développeur, vous pouvez créer des applications de tabulation, de [robot](../bots/what-are-bots.md)et d' [extension de message](../messaging-extensions/what-are-messaging-extensions.md) [configurables](../tabs/what-are-tabs.md#how-do-tabs-work)pour améliorer et enrichir une expérience de réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="7c75d-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="7c75d-108">Les utilisateurs de la réunion peuvent accéder aux applications via la Galerie d’onglets pour activer des scénarios pertinents, tels que la pré-configuration d’un tableau kanban, le lancement d’une boîte de dialogue intégrant une action de réunion ou la création d’un sondage post-réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="7c75d-109">Votre application de réunion peut fournir une expérience utilisateur pour chaque étape du cycle de vie de la réunion en fonction de l’état des participants.</span><span class="sxs-lookup"><span data-stu-id="7c75d-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="7c75d-110">Les centres d’extensibilité des applications de réunion teams sur trois concepts :</span><span class="sxs-lookup"><span data-stu-id="7c75d-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="7c75d-111">✔ **Cycle de vie** de la réunion — avant, pendant et après la période de réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="7c75d-112">✔ **Rôle de participant** — organisateur de réunion, présentateur ou participant.</span><span class="sxs-lookup"><span data-stu-id="7c75d-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="7c75d-113">✔ **Type d’utilisateur** : utilisateur de teams in-client, invité, fédéré ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="7c75d-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="7c75d-114">Scénarios de cycle de vie de réunion</span><span class="sxs-lookup"><span data-stu-id="7c75d-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="7c75d-115">Onglets</span><span class="sxs-lookup"><span data-stu-id="7c75d-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c75d-116">Comme avec toutes les applications d’onglet, votre application doit suivre le [flux d’authentification unique](../tabs/how-to/authentication/auth-aad-sso.md) teams pour les onglets.</span><span class="sxs-lookup"><span data-stu-id="7c75d-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="7c75d-117">Les clients mobiles prennent en charge les onglets uniquement dans les surfaces pre et post Meeting.</span><span class="sxs-lookup"><span data-stu-id="7c75d-117">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="7c75d-118">Les expériences de réunion (boîte de dialogue et volet de réunion) sur mobile seront bientôt disponibles.</span><span class="sxs-lookup"><span data-stu-id="7c75d-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="7c75d-119">Expérience des applications préalables à la réunion</span><span class="sxs-lookup"><span data-stu-id="7c75d-119">Pre-meeting app experience</span></span>

<span data-ttu-id="7c75d-120">**Expérience préalable à la réunion :**</span><span class="sxs-lookup"><span data-stu-id="7c75d-120">**Pre-meeting experience:**</span></span>

![expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="7c75d-122">**Onglet pré-réunion :**</span><span class="sxs-lookup"><span data-stu-id="7c75d-122">**Pre-meeting tab:**</span></span>

![affichage de l’onglet pre-Meeting](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="7c75d-124">✔ Les utilisateurs autorisés peuvent ajouter des applications à une réunion via la Galerie d’onglets de deux manières :</span><span class="sxs-lookup"><span data-stu-id="7c75d-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="7c75d-125">&emsp;&emsp;&#9679; via l’onglet **Détails** de l’écran planification des équipes.</span><span class="sxs-lookup"><span data-stu-id="7c75d-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="7c75d-126">&emsp;&emsp;&#9679; via l’onglet **conversation** de réunion dans une réunion existante.</span><span class="sxs-lookup"><span data-stu-id="7c75d-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="7c75d-127">✔ Les applications d’onglet sont accessibles dans les pages **Détails** des réunions et **conversations** à l’aide d’une icône plus (➕). |</span><span class="sxs-lookup"><span data-stu-id="7c75d-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="7c75d-128">✔ Disposition des onglets doit être dans un État organisé s’il y a plus de dix sondages ou enquêtes.</span><span class="sxs-lookup"><span data-stu-id="7c75d-128">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="7c75d-129">Expérience d’application dans la réunion</span><span class="sxs-lookup"><span data-stu-id="7c75d-129">In-meeting app experience</span></span>

<span data-ttu-id="7c75d-130">Les applications de réunion ✔ seront hébergées dans la barre supérieure supérieure de la fenêtre de conversation et sous la forme d’onglets de réunion via l’onglet dans la réunion. Lorsque les utilisateurs ajoutent un onglet à une réunion par le biais de la Galerie d’onglets, les applications qui se trouvent **pendant les réunions** sont exposées.</span><span class="sxs-lookup"><span data-stu-id="7c75d-130">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="7c75d-131">✔ Les utilisateurs autorisés peuvent ajouter des applications pendant la réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-131">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="7c75d-132">✔ Lorsqu’elles sont chargées dans le cadre d’une réunion, les applications peuvent tirer parti du kit de développement logiciel (SDK) du client teams pour accéder à `meetingId` , `userMri` et `frameContext` pour restituer l’expérience de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="7c75d-132">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="7c75d-133">✔ L’exportation d’un résultat d’une enquête ou des sondages doivent avertir les utilisateurs de l’indication « résultats correctement téléchargés ».</span><span class="sxs-lookup"><span data-stu-id="7c75d-133">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="7c75d-134">✔ Pour qu’une application soit visible dans une réunion teams dans deux domaines :</span><span class="sxs-lookup"><span data-stu-id="7c75d-134">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="7c75d-135">&emsp;&emsp;&#9679; **panneau latéral**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-135">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="7c75d-136">Si votre _manifeste d’application_ spécifie que votre onglet est [optimisé pour le panneau de configuration](create-apps-for-teams-meetings.md#in-meeting), c’est ici qu’il sera affiché.</span><span class="sxs-lookup"><span data-stu-id="7c75d-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#in-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="7c75d-137">Il peut également faire partie d’une expérience de bac à papier, sous réserve des instructions de conception spécifiées.</span><span class="sxs-lookup"><span data-stu-id="7c75d-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="7c75d-138">&emsp;&emsp;&#9679; **boîte de dialogue de réunion**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-138">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="7c75d-139">Utilisez la boîte de dialogue de réunion pour présenter un contenu actionnable pour les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="7c75d-140">*Consultez la rubrique* [créer des applications pour les réunions teams](create-apps-for-teams-meetings.md).</span><span class="sxs-lookup"><span data-stu-id="7c75d-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="7c75d-141">**Expérience de réunion :**</span><span class="sxs-lookup"><span data-stu-id="7c75d-141">**In-meeting experience:**</span></span>

![expérience de réunion](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Affichage de la boîte de dialogue réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="7c75d-144">**Boîte de dialogue intégrée à la réunion pour les utilisateurs :**</span><span class="sxs-lookup"><span data-stu-id="7c75d-144">**In-meeting actionable dialog for users:**</span></span>

![affichage de la boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="7c75d-146">Expérience d’application post-réunion</span><span class="sxs-lookup"><span data-stu-id="7c75d-146">Post-meeting app experience</span></span>

<span data-ttu-id="7c75d-147">**Expérience post-réunion :**</span><span class="sxs-lookup"><span data-stu-id="7c75d-147">**Post-meeting experience:**</span></span>

![affichage de la réunion post](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="7c75d-149">✔ Le scénario d’application post-réunion est semblable à l’expérience de post-réunion actuelle avec l’avantage supplémentaire d’avoir des onglets qui existent dans la surface.</span><span class="sxs-lookup"><span data-stu-id="7c75d-149">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="7c75d-150">✔ Les utilisateurs autorisés peuvent ajouter des applications à une réunion à partir de la Galerie d’onglets à l’aide de l’onglet **Détails** du formulaire planification de teams et de l’onglet **conversation** de réunion dans une réunion existante.</span><span class="sxs-lookup"><span data-stu-id="7c75d-150">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="7c75d-151">✔ Disposition des onglets doit être dans un État organisé s’il y a plus de dix sondages ou enquêtes.</span><span class="sxs-lookup"><span data-stu-id="7c75d-151">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="7c75d-152">Bots</span><span class="sxs-lookup"><span data-stu-id="7c75d-152">Bots</span></span>

<span data-ttu-id="7c75d-153">Pour la mise en œuvre de bot, consultez nos robots dans la documentation des [réunions teams](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) .</span><span class="sxs-lookup"><span data-stu-id="7c75d-153">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="7c75d-154">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="7c75d-154">Messaging Extensions</span></span>

<span data-ttu-id="7c75d-155">Pour l’implémentation de l’extension de messagerie, consultez nos [extensions de messagerie dans la documentation des réunions teams](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) .</span><span class="sxs-lookup"><span data-stu-id="7c75d-155">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="7c75d-156">Rôles des participants et types d’utilisateur dans une réunion</span><span class="sxs-lookup"><span data-stu-id="7c75d-156">Participant roles and user types in a meeting</span></span>

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="7c75d-158">Rôles des participants</span><span class="sxs-lookup"><span data-stu-id="7c75d-158">Participant roles</span></span>

<span data-ttu-id="7c75d-159">Vous pouvez concevoir votre application avec l’autorisation spécifique aux participants.</span><span class="sxs-lookup"><span data-stu-id="7c75d-159">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="7c75d-160">Par exemple, seul un organisateur et/ou un présentateur peuvent créer une interrogation dans les réunions.</span><span class="sxs-lookup"><span data-stu-id="7c75d-160">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="7c75d-161">Bien que les paramètres de participant par défaut soient déterminés par l’administrateur informatique d’une organisation, un organisateur de réunion peut souhaiter modifier les paramètres d’une réunion spécifique.</span><span class="sxs-lookup"><span data-stu-id="7c75d-161">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="7c75d-162">Les organisateurs peuvent faire ces modifications dans la page Web options de la réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-162">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="7c75d-163">**Organisateur**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-163">**Organizer**.</span></span> <span data-ttu-id="7c75d-164">L’organisateur planifie une réunion, définit les options de la réunion, affecte des rôles de réunion et démarre la réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-164">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="7c75d-165">Seuls les utilisateurs disposant d’un compte M365 (possédant une licence Teams) peuvent être des organisateurs et contrôler les autorisations des participants.</span><span class="sxs-lookup"><span data-stu-id="7c75d-165">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="7c75d-166">**Présentateur**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-166">**Presenter**.</span></span> <span data-ttu-id="7c75d-167">Les présentateurs ont presque les mêmes fonctionnalités que l’organisateur ; Toutefois, un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de la réunion pour la session.</span><span class="sxs-lookup"><span data-stu-id="7c75d-167">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="7c75d-168">Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.</span><span class="sxs-lookup"><span data-stu-id="7c75d-168">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="7c75d-169">**Participant**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-169">**Attendee**.</span></span> <span data-ttu-id="7c75d-170">Un participant est un utilisateur qui a été invité à participer à une réunion, mais qui n’est pas autorisé à agir en tant que présentateur.</span><span class="sxs-lookup"><span data-stu-id="7c75d-170">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="7c75d-171">Les participants peuvent interagir avec d’autres membres de la réunion, mais ils ne peuvent pas gérer les paramètres de la réunion ou partager du contenu.</span><span class="sxs-lookup"><span data-stu-id="7c75d-171">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="7c75d-172">_Voir_ [ **rôles dans une réunion teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="7c75d-172">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="7c75d-173">Vous pouvez accéder à la page Options de la  **réunion** comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c75d-173">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="7c75d-174">&#11200; dans Teams, accédez **à calendrier** ![ calendrier ](../assets/images/apps-in-meetings/calendar-logo.png) , sélectionnez une réunion, puis **options** de la réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-174">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="7c75d-175">&#11200; dans une invitation à une réunion, sélectionnez Options de la **réunion**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-175">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="7c75d-176">&#11200; pendant une réunion, sélectionnez **Afficher** ![ l’icône des participants ](../assets/images/apps-in-meetings/show-participants.png) dans les contrôles de réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-176">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="7c75d-177">Ensuite, au-dessus de la liste des participants, sélectionnez **gérer les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-177">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="7c75d-178">Types d'utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c75d-178">User types</span></span>

> [!NOTE]
> <span data-ttu-id="7c75d-179">Les types d’utilisateurs peuvent participer à des réunions et assumer l’un des rôles de participant décrits ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7c75d-179">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="7c75d-180">Le type d’utilisateur n’est pas exposé dans le cadre de l’API **getParticipantRole** .</span><span class="sxs-lookup"><span data-stu-id="7c75d-180">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="7c75d-181">**Dans le client**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-181">**In-tenant**.</span></span> <span data-ttu-id="7c75d-182">Ces utilisateurs appartiennent à l’organisation et disposent d’informations d’identification dans Azure Active Directory pour le client.</span><span class="sxs-lookup"><span data-stu-id="7c75d-182">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="7c75d-183">Il s’agit généralement d’employés à temps plein, sur site ou à distance.</span><span class="sxs-lookup"><span data-stu-id="7c75d-183">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="7c75d-184">**Invité**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-184">**Guest**.</span></span> <span data-ttu-id="7c75d-185">Un invité est un participant d’une autre organisation qui a été invité à accéder aux équipes ou à d’autres ressources dans le client de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="7c75d-185">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="7c75d-186">Les invités sont ajoutés à Active Directory de votre organisation et peuvent être attribués à presque toutes les mêmes fonctionnalités teams qu’un membre d’équipe natif avec un accès total aux conversations, réunions et fichiers d’équipe.</span><span class="sxs-lookup"><span data-stu-id="7c75d-186">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="7c75d-187">_Voir_ [accès invité dans Microsoft teams](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="7c75d-187">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="7c75d-188">**Fédéré/externe**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-188">**Federated/External**.</span></span> <span data-ttu-id="7c75d-189">Un utilisateur fédéré est un utilisateur de teams externes d’une autre organisation qui a été invité à participer à une réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-189">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="7c75d-190">Étant donné que ces utilisateurs ont des informations d’identification valides avec des partenaires fédérés, ils sont traités comme étant authentifiés par Teams, mais n’ont pas accès à vos équipes ou aux autres ressources partagées de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="7c75d-190">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="7c75d-191">Si vous souhaitez que les utilisateurs externes aient accès aux équipes et aux canaux, l’accès invité peut être une meilleure solution.</span><span class="sxs-lookup"><span data-stu-id="7c75d-191">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="7c75d-192">_Voir_ [gérer l’accès externe dans Microsoft teams](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="7c75d-192">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="7c75d-193">**Anonyme**.</span><span class="sxs-lookup"><span data-stu-id="7c75d-193">**Anonymous**.</span></span> <span data-ttu-id="7c75d-194">Les utilisateurs anonymes n’ont pas d’identité Active Directory et ne sont pas fédérés avec un client.</span><span class="sxs-lookup"><span data-stu-id="7c75d-194">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="7c75d-195">Le participant anonyme est comme un utilisateur externe, mais son identité n’est pas projetée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-195">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="7c75d-196">Les utilisateurs anonymes ne pourront pas accéder aux applications dans une fenêtre de réunion.</span><span class="sxs-lookup"><span data-stu-id="7c75d-196">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c75d-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c75d-197">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c75d-198">Créer des applications pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="7c75d-198">Create apps for Teams meetings</span></span>](create-apps-for-teams-meetings.md)
