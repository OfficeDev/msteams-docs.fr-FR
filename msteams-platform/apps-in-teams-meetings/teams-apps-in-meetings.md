---
title: Réunions des applications dans teams
author: laujan
description: vue d’ensemble des applications dans les réunions teams en fonction des participants et du rôle d’utilisateur
ms.topic: overview
ms.author: lajanuar
keywords: applications Team Apps Meeting User Role Role API
ms.openlocfilehash: 8a1b5b7d95e91273c794a2aa86a51e0ddeb1c610
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605169"
---
# <a name="apps-in-teams-meetings"></a>Réunions des applications dans teams

Les réunions sont les clés de la productivité dans Teams. Ils permettent la collaboration, le partenariat, la communication informée et le partage de commentaires dans un forum inclusif et actif. En tant que développeur, vous pouvez créer des applications de tabulation, de [robot](../bots/what-are-bots.md)et d' [extension de message](../messaging-extensions/what-are-messaging-extensions.md) [configurables](../tabs/what-are-tabs.md#how-do-tabs-work)pour améliorer et enrichir une expérience de réunion Teams. Les utilisateurs de la réunion peuvent accéder aux applications via la Galerie d’onglets pour activer des scénarios pertinents, tels que la pré-configuration d’un tableau kanban, le lancement d’une boîte de dialogue intégrant une action de réunion ou la création d’un sondage post-réunion. Votre application de réunion peut fournir une expérience utilisateur pour chaque étape du cycle de vie de la réunion en fonction de l’état des participants.

Les centres d’extensibilité des applications de réunion teams sur trois concepts :

✔ **Cycle de vie** de la réunion — avant, pendant et après la période de réunion.  
✔ **Rôle de participant** — organisateur de réunion, présentateur ou participant.  
✔ **Type d’utilisateur** : utilisateur de teams in-client, invité, fédéré ou anonyme.

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>Scénarios de cycle de vie de réunion

## <a name="tabs"></a>Onglets

> [!IMPORTANT]
> Comme avec toutes les applications d’onglet, votre application doit suivre le [flux d’authentification unique](../tabs/how-to/authentication/auth-aad-sso.md) teams pour les onglets.

> [!NOTE]
> Les clients mobiles prennent en charge les onglets uniquement dans les surfaces pre et post Meeting. Les expériences de réunion (boîte de dialogue et volet de réunion) sur mobile seront bientôt disponibles.

### <a name="pre-meeting-app-experience"></a>Expérience des applications préalables à la réunion

**Expérience préalable à la réunion :**

![expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

**Onglet pré-réunion :**

![affichage de l’onglet pre-Meeting](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔ Les utilisateurs autorisés peuvent ajouter des applications à une réunion via la Galerie d’onglets de deux manières :

&emsp;&emsp;&#9679; via l’onglet **Détails** de l’écran planification des équipes.

&emsp;&emsp;&#9679; via l’onglet **conversation** de réunion dans une réunion existante.</br> </br>

✔ Les applications d’onglet sont accessibles dans les pages **Détails** des réunions et **conversations** à l’aide d’une icône plus (➕). |

✔ Disposition des onglets doit être dans un État organisé s’il y a plus de dix sondages ou enquêtes.

### <a name="in-meeting-app-experience"></a>Expérience d’application dans la réunion

Les applications de réunion ✔ seront hébergées dans la barre supérieure supérieure de la fenêtre de conversation et sous la forme d’onglets de réunion via l’onglet dans la réunion. Lorsque les utilisateurs ajoutent un onglet à une réunion par le biais de la Galerie d’onglets, les applications qui se trouvent **pendant les réunions** sont exposées.

✔ Les utilisateurs autorisés peuvent ajouter des applications pendant la réunion.

✔ Lorsqu’elles sont chargées dans le cadre d’une réunion, les applications peuvent tirer parti du kit de développement logiciel (SDK) du client teams pour accéder à `meetingId` , `userMri` et `frameContext` pour restituer l’expérience de manière appropriée.

✔ L’exportation d’un résultat d’une enquête ou des sondages doivent avertir les utilisateurs de l’indication « résultats correctement téléchargés ».

✔ Pour qu’une application soit visible dans une réunion teams dans deux domaines :

&emsp;&emsp;&#9679; **panneau latéral**. </br>

> [!NOTE]
> Si votre _manifeste d’application_ spécifie que votre onglet est [optimisé pour le panneau de configuration](create-apps-for-teams-meetings.md#during-a-meeting), c’est ici qu’il sera affiché. Il peut également faire partie d’une expérience de bac à papier, sous réserve des instructions de conception spécifiées.

&emsp;&emsp;&#9679; **boîte de dialogue de réunion**. Utilisez la boîte de dialogue de réunion pour présenter un contenu actionnable pour les participants à la réunion. *Consultez la rubrique* [créer des applications pour les réunions teams](create-apps-for-teams-meetings.md).

**Expérience de réunion :**

![expérience de réunion](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Affichage de la boîte de dialogue réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**Boîte de dialogue intégrée à la réunion pour les utilisateurs :**

![affichage de la boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Expérience d’application post-réunion

**Expérience post-réunion :**

![affichage de la réunion post](../assets/images/apps-in-meetings/PostMeeting.png)

✔ Le scénario d’application post-réunion est semblable à l’expérience de post-réunion actuelle avec l’avantage supplémentaire d’avoir des onglets qui existent dans la surface. 

✔ Les utilisateurs autorisés peuvent ajouter des applications à une réunion à partir de la Galerie d’onglets à l’aide de l’onglet **Détails** du formulaire planification de teams et de l’onglet **conversation** de réunion dans une réunion existante.

✔ Disposition des onglets doit être dans un État organisé s’il y a plus de dix sondages ou enquêtes.

### <a name="bots"></a>Bots

Pour la mise en œuvre de bot, consultez nos robots dans la documentation des [réunions teams](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) .

### <a name="messaging-extensions"></a>Extensions de messagerie

Pour l’implémentation de l’extension de messagerie, consultez nos [extensions de messagerie dans la documentation des réunions teams](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) .

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Rôles des participants et types d’utilisateur dans une réunion

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Rôles des participants

Vous pouvez concevoir votre application avec l’autorisation spécifique aux participants. Par exemple, seul un organisateur et/ou un présentateur peuvent créer une interrogation dans les réunions. Bien que les paramètres de participant par défaut soient déterminés par l’administrateur informatique d’une organisation, un organisateur de réunion peut souhaiter modifier les paramètres d’une réunion spécifique. Les organisateurs peuvent faire ces modifications dans la page Web options de la réunion.

1. **Organisateur**. L’organisateur planifie une réunion, définit les options de la réunion, affecte des rôles de réunion et démarre la réunion. Seuls les utilisateurs disposant d’un compte M365 (possédant une licence Teams) peuvent être des organisateurs et contrôler les autorisations des participants.
1. **Présentateur**. Les présentateurs ont presque les mêmes fonctionnalités que l’organisateur ; Toutefois, un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de la réunion pour la session. Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.
1. **Participant**. Un participant est un utilisateur qui a été invité à participer à une réunion, mais qui n’est pas autorisé à agir en tant que présentateur. Les participants peuvent interagir avec d’autres membres de la réunion, mais ils ne peuvent pas gérer les paramètres de la réunion ou partager du contenu.

_Voir_ [ **rôles dans une réunion teams**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

Vous pouvez accéder à la page Options de la  **réunion** comme suit :

&#11200; dans Teams, accédez **à calendrier** ![ calendrier ](../assets/images/apps-in-meetings/calendar-logo.png) , sélectionnez une réunion, puis **options** de la réunion.

&#11200; dans une invitation à une réunion, sélectionnez Options de la **réunion**.

&#11200; pendant une réunion, sélectionnez **Afficher** ![ l’icône des participants ](../assets/images/apps-in-meetings/show-participants.png) dans les contrôles de réunion. Ensuite, au-dessus de la liste des participants, sélectionnez **gérer les autorisations**.

### <a name="user-types"></a>Types d'utilisateur

> [!NOTE]
> Les types d’utilisateurs peuvent participer à des réunions et assumer l’un des rôles de participant décrits ci-dessus. Le type d’utilisateur n’est pas exposé dans le cadre de l’API **getParticipantRole** .

1. **Dans le client**. Ces utilisateurs appartiennent à l’organisation et disposent d’informations d’identification dans Azure Active Directory pour le client. Il s’agit généralement d’employés à temps plein, sur site ou à distance.
1. **Invité**. Un invité est un participant d’une autre organisation qui a été invité à accéder aux équipes ou à d’autres ressources dans le client de votre organisation. Les invités sont ajoutés à Active Directory de votre organisation et peuvent être attribués à presque toutes les mêmes fonctionnalités teams qu’un membre d’équipe natif avec un accès total aux conversations, réunions et fichiers d’équipe. _Voir_ [accès invité dans Microsoft teams](/microsoftteams/guest-access)
1. **Fédéré/externe**. Un utilisateur fédéré est un utilisateur de teams externes d’une autre organisation qui a été invité à participer à une réunion. Étant donné que ces utilisateurs ont des informations d’identification valides avec des partenaires fédérés, ils sont traités comme étant authentifiés par Teams, mais n’ont pas accès à vos équipes ou aux autres ressources partagées de votre organisation. Si vous souhaitez que les utilisateurs externes aient accès aux équipes et aux canaux, l’accès invité peut être une meilleure solution. _Voir_ [gérer l’accès externe dans Microsoft teams](/microsoftteams/manage-external-access)
1. **Anonyme**. Les utilisateurs anonymes n’ont pas d’identité Active Directory et ne sont pas fédérés avec un client. Le participant anonyme est comme un utilisateur externe, mais son identité n’est pas projetée dans la réunion. Les utilisateurs anonymes ne pourront pas accéder aux applications dans une fenêtre de réunion.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Créer des applications pour les réunions Teams](create-apps-for-teams-meetings.md)
