---
title: Applications dans les réunions Teams
author: laujan
description: vue d’ensemble des applications dans les réunions Teams en fonction du rôle du participant et de l’utilisateur
ms.topic: overview
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 63c383f1bc7eaa92e2bd4ff378756064ee85ed70
ms.sourcegitcommit: 92fa912a51f295bb8a2dc1593a46ce103752dcdd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/21/2021
ms.locfileid: "49917596"
---
# <a name="apps-in-teams-meetings"></a>Applications dans les réunions Teams

Les réunions sont essentielles à la productivité dans Teams. Ils permettent la collaboration, le partenariat, la communication informée et les commentaires partagés dans un forum actif et inclusif. En tant que développeur, vous pouvez créer des applications [configurables](../tabs/what-are-tabs.md#how-do-tabs-work) [d’onglet,](../messaging-extensions/what-are-messaging-extensions.md) de [bot](../bots/what-are-bots.md)et d’extension de message pour améliorer et enrichir une expérience de réunion Teams. Les utilisateurs de réunion peuvent accéder aux applications, via la galerie d’onglets, pour activer des scénarios pertinents tels que la préparation d’un tableau kanban, le lancement d’une boîte de dialogue actionnable pendant la réunion ou la création d’un sondage post-réunion. Votre application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion en fonction de l’état des participants.

L’extensibilité de l’application de réunion Teams se concentre sur trois concepts :

✔ vie **de réunion** — avant, pendant et après la période de réunion.  
✔ rôle **de participant :** organisateur de réunion, présentateur ou participant.  
✔ type **d’utilisateur** : utilisateur Teams dans le client, invité, fédéré ou anonyme.

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>Scénarios de cycle de vie de réunion

## <a name="tabs"></a>Onglets

> [!IMPORTANT]
> Comme avec toutes les applications d’onglet, votre application doit suivre le flux d’authentification [sso teams](../tabs/how-to/authentication/auth-aad-sso.md) pour les onglets.

> [!NOTE]
> Les clients mobiles ne supportent les onglets que dans les surfaces de pré et de post-réunion. Les expériences en réunion (boîte de dialogue et panneau en réunion) sur mobile seront bientôt disponibles

### <a name="pre-meeting-app-experience"></a>Expérience d’application avant la réunion

**Expérience préalable à la réunion :**

![expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

**Onglet Avant la réunion :**

![Affichage de l’onglet avant la réunion](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔ utilisateurs autorisés peuvent ajouter des applications à une réunion via la galerie d’onglets de deux manières :

&emsp;&emsp;&#9679; via **l’onglet Détails** du formulaire de planification Teams.

&emsp;&emsp;&#9679; via l’onglet **Conversation** de réunion dans une réunion existante.</br> </br>

✔ applications Onglet sont accessibles dans les pages **Détails** des réunions et **Conversations** à l’aide d’un bouton d’icône plus (➕).|

✔ disposition des onglets doit être organisée s’il y a plus de dix sondages ou enquêtes.

### <a name="in-meeting-app-experience"></a>Expérience d’application en réunion

✔ applications de réunion seront hébergées dans la barre supérieure de la fenêtre de conversation et sous la mesure de l’expérience d’onglet de réunion via l’onglet De réunion. Lorsque les utilisateurs ajoutent un onglet à une  réunion via la galerie d’onglets, les applications qui sont pendant les expériences de réunion sont surface.

✔ utilisateurs autorisés peuvent ajouter des applications pendant la réunion.

✔ lors du chargement dans le contexte d’une réunion, les applications pourront tirer parti du SDK client Teams pour accéder au , et pour restituer correctement `meetingId` `userMri` `frameContext` l’expérience.

✔ l’exportation d’un résultat d’une enquête ou d’un sondage doit avertir les utilisateurs indiquant « résultats téléchargés avec succès ».

✔ pour qu’une application soit visible dans une réunion Teams dans deux domaines :

&emsp;&emsp;&#9679; panneau **latéral**. </br>

> [!NOTE]
> Si le _manifeste de votre_ application spécifie que votre onglet est optimisé pour le panneau latéral, c’est là qu’il sera affiché. [](create-apps-for-teams-meetings.md#during-a-meeting) Il peut également faire partie d’une expérience de partage de bac, sous réserve des instructions de conception spécifiées.

&emsp;&emsp;&#9679; boîte **de dialogue En réunion.** Utilisez la boîte de dialogue de réunion pour présenter du contenu actionnable aux participants à la réunion. *Voir* [Créer des applications pour les réunions Teams.](create-apps-for-teams-meetings.md)

**Expérience en réunion :**

![expérience en réunion](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Affichage de la boîte de dialogue en réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**Boîte de dialogue actionnable en réunion pour les utilisateurs :**

![affichage de boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Expérience d’application post-réunion

**Expérience post-réunion :**

![affichage après la réunion](../assets/images/apps-in-meetings/PostMeeting.png)

✔ le scénario d’application post-réunion est similaire à l’expérience post-réunion actuelle avec l’avantage supplémentaire d’avoir des onglets qui existent dans la surface. 

✔ utilisateurs autorisés peuvent ajouter des applications de la galerie d’onglets à une réunion  via l’onglet **Détails** du formulaire de planification Teams et l’onglet Conversation de réunion dans une réunion existante.

✔ disposition des onglets doit être organisée s’il y a plus de dix sondages ou enquêtes.

### <a name="bots"></a>Bots

Pour l’implémentation du bot, consultez la documentation relative aux [bots dans les réunions Teams.](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings)

### <a name="messaging-extensions"></a>Extensions de messagerie

Pour l’implémentation de l’extension de messagerie, consultez la documentation relative aux [extensions de messagerie dans la](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation des réunions Teams.

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Rôles des participants et types d’utilisateurs dans une réunion

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Rôles des participants

Vous pouvez concevoir votre application avec une autorisation spécifique au participant. Par exemple, seuls un organisateur et/ou un présentateur peuvent créer un sondage dans les réunions. Bien que les paramètres des participants par défaut soient déterminés par l’administrateur informatique d’une organisation, un organisateur de réunion peut vouloir modifier les paramètres d’une réunion spécifique. Les organisateurs peuvent apporter ces modifications sur la page web Des options de réunion.

1. **Organisateur**. L’organisateur prévoit une réunion, définit les options de la réunion, attribue des rôles de réunion et démarre la réunion. Seuls les utilisateurs possédant un compte M365 (possédant une licence Teams) peuvent être organisateurs et contrôler les autorisations des participants.
1. **Présentateur**. Les présentateurs ont presque les mêmes fonctionnalités que l’organisateur . toutefois, un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de réunion pour la session. Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.
1. **Participant**. Un participant est un utilisateur qui a été invité à participer à une réunion, mais qui n’est pas autorisé à agir en tant que présentateur. Les participants peuvent interagir avec d’autres membres de la réunion, mais ne peuvent pas gérer les paramètres de la réunion ou partager du contenu.

_Voir_ [ **rôles dans une réunion Teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

Vous pouvez accéder à la page  **Options de** réunion comme suit :

&#11200; Teams, allez au  ![ logo calendrier, sélectionnez une réunion, puis les ](../assets/images/apps-in-meetings/calendar-logo.png) options de **réunion.**

&#11200; dans une invitation à une réunion, sélectionnez **Les options de réunion.**

&#11200; au cours d’une réunion, sélectionnez **Afficher les participants** et afficher l’icône des participants dans les ![ ](../assets/images/apps-in-meetings/show-participants.png) contrôles de réunion. Ensuite, au-dessus de la liste des participants, choisissez **Gérer les autorisations.**

### <a name="user-types"></a>Types d'utilisateur

> [!NOTE]
> Les types d’utilisateurs peuvent participer à des réunions et supposer l’un des rôles de participant décrits ci-dessus. Le type d’utilisateur n’est pas exposé dans le cadre de **l’API getParticipantRole.**

1. **Dans le client**. Ces utilisateurs appartiennent à l’organisation et ont des informations d’identification dans Azure Active Directory pour le client. Il s’agit généralement d’employés à plein temps, sur site ou distants.
1. **Invité**. Un invité est un participant d’une autre organisation qui a été invité à accéder à Teams ou à d’autres ressources dans le client de votre organisation. Les invités sont ajoutés à Active Directory de votre organisation et peuvent avoir presque toutes les mêmes fonctionnalités Teams qu’un membre natif de l’équipe avec un accès total aux conversations, réunions et fichiers de l’équipe. _Voir_ [l’accès invité dans Microsoft Teams](/microsoftteams/guest-access)
1. **Fédéré/externe**. Un utilisateur fédéré est un utilisateur Teams externe d’une autre organisation qui a été invité à participer à une réunion. Étant donné que ces utilisateurs disposent d’informations d’identification valides avec des partenaires fédérés, ils sont traités comme authentifiés par Teams, mais n’ont pas accès à vos équipes ou à d’autres ressources partagées de votre organisation. Si vous souhaitez que les utilisateurs externes ont accès aux équipes et aux canaux, l’accès invité peut être une meilleure option. _Voir Gérer_ [l’accès externe dans Microsoft Teams](/microsoftteams/manage-external-access)
1. **Anonyme**. Les utilisateurs anonymes n’ont pas d’identité Active Directory et ne sont pas fédérés avec un client. Le participant anonyme est comme un utilisateur externe, mais son identité n’est pas projetée dans la réunion. Les utilisateurs anonymes ne pourront pas accéder aux applications dans une fenêtre de réunion.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Concevoir votre application](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [Créer votre application](create-apps-for-teams-meetings.md)
