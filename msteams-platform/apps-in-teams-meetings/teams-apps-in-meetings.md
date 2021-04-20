---
title: Applications dans les réunions Teams
author: laujan
description: vue d’ensemble des applications dans les réunions Teams en fonction du rôle du participant et de l’utilisateur
ms.topic: overview
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 201fa58cc375440cf6c495028135e32fd51f740c
ms.sourcegitcommit: ee8c4800da3b3569d80c6f3661a2f20aa1f2c5e2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/19/2021
ms.locfileid: "51885079"
---
# <a name="apps-in-teams-meetings"></a>Applications dans les réunions Teams

Les réunions permettent la collaboration, le partenariat, la communication éclairée et les commentaires partagés dans un forum actif et inclusif. L’application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion, y compris l’expérience de l’application avant, en réunion et après la réunion, en fonction de l’état du participant.

Les utilisateurs finaux teams peuvent accéder aux applications pendant les réunions à l’aide de la galerie d’onglets, par exemple :

* Pré-phase d’un tableau kanban
* Lancer une boîte de dialogue actionnable en réunion
* Créer un sondage après la réunion

L’extensibilité des applications de réunion Teams est basée sur les concepts suivants :

✔ le cycle de vie des réunions possède des étapes telles qu’avant, pendant et après la période de réunion.  
✔ rôles de participant à une réunion, tels que l’organisateur de la réunion, le présentateur ou le participant.  
✔ types d’utilisateurs dans une réunion telle que l’utilisateur teams en client, invité, fédéré ou anonyme.

Cet article traite des informations sur le cycle de vie des réunions et sur la façon d’intégrer des onglets, des bots et des extensions de messagerie dans votre réunion. Il vous permet également d’identifier les rôles des participants et d’utiliser différents types d’utilisateurs pour effectuer des tâches.

> [!NOTE]
> Pour travailler avec les fonctionnalités d’extensibilité de l’application de réunion, vous devez avoir les autorisations appropriées.

### <a name="meeting-lifecycle"></a>Cycle de vie des réunions

Le cycle de vie des réunions consiste en une expérience d’application avant, en réunion et après la réunion. Vous pouvez intégrer des onglets, des bots et des extensions de messagerie à chaque étape du cycle de vie de la réunion.

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Intégrer des onglets dans le cycle de vie de la réunion

Les onglets permettent aux membres de l'équipe d'accéder aux services et au contenu dans un espace spécifique au sein d'un canal ou d'une conversation. Cela permet à l'équipe de travailler directement avec des onglets et d'avoir des conversations sur les outils et les données disponibles dans les onglets. Dans une réunion Teams, les utilisateurs peuvent ajouter un onglet en sélectionnant plus <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>et en choisissant l'application qu'ils souhaitent installer en tant qu'onglet.

> [!IMPORTANT]
> Si vous avez intégré un onglet à votre réunion, votre application doit suivre le flux d'authentification unique [Teams pour](../tabs/how-to/authentication/auth-aad-sso.md) les onglets.

> [!NOTE]
> * Les clients mobiles ne supportent les onglets qu'aux étapes préalables et post-réunion. Les expériences en réunion qui sont des boîtes de dialogue et des panneaux en réunion ne sont actuellement pas disponibles sur les appareils mobiles.
> * Les applications sont uniquement pris en charge dans les réunions privées programmées.

### <a name="pre-meeting-app-experience"></a>Expérience d'application avant la réunion

**Expérience préalable à la réunion :**

![expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

**Onglet Avant la réunion :**

![Affichage de l'onglet avant la réunion](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔ utilisateurs autorisés sont des utilisateurs qui peuvent ajouter des applications à une réunion pendant différentes étapes du cycle de vie de la réunion. Ces utilisateurs peuvent ajouter des applications à une réunion via la galerie d'onglets de deux manières :

   * Utilisation de **l'onglet Détails** du formulaire de planification Teams.

   * Utilisation de l'onglet **Conversation** de réunion dans une réunion existante.

✔'onglets sont accessibles dans les pages **Détails** des réunions et **Conversations** à l'aide d'un bouton ➕ plus.

✔ disposition des onglets doit être organisée s'il y a plus de dix sondages ou enquêtes.

### <a name="in-meeting-app-experience"></a>Expérience d'application en réunion

✔ applications de réunion sont hébergées dans la barre supérieure de la fenêtre de conversation et en tant qu'expérience d'onglet dans la réunion à l'aide de l'onglet en réunion. Lorsque les utilisateurs ajoutent un onglet à une réunion via la galerie d'onglets, les applications qui sont pendant les expériences **de** réunion sont affichées.

✔ utilisateurs autorisés peuvent ajouter des applications pendant la réunion.

✔ lorsqu'elles sont chargées dans le contexte d'une réunion, les applications peuvent tirer parti du SDK client Teams pour accéder au , et pour restituer correctement `meetingId` `userMri` `frameContext` l'expérience.

✔ exporter un résultat d'une enquête ou d'un sondage avertit les utilisateurs que les résultats ont été téléchargés avec succès.

✔ Une application est visible dans une réunion Teams dans le panneau latéral ou dans la boîte de dialogue de la réunion. Utilisez la boîte de dialogue de réunion pour présenter le contenu actionnable aux participants à la réunion. Pour plus d'informations, voir [créer des applications pour les réunions Teams.](create-apps-for-teams-meetings.md)

   > [!NOTE]
   > Le manifeste de votre application spécifie que votre onglet est [optimisé pour](create-apps-for-teams-meetings.md#during-a-meeting)le panneau latéral, c'est-à-dire l'endroit où il est affiché. Il peut également faire partie d'une expérience de partage de bac, sous réserve des instructions de conception spécifiées.

Les images suivantes affichent l'application sous la mesure d'une boîte de dialogue de réunion et d'un panneau latéral distinct :

![Expérience en réunion](../assets/images/apps-in-meetings/in-meeting-experience.png)

![Affichage de la boîte de dialogue en réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a>Boîte de dialogue actionnable en réunion pour les utilisateurs

![Affichage de boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>Expérience d'application post-réunion

![Affichage après la réunion](../assets/images/apps-in-meetings/PostMeeting.png)

✔ le scénario d'application post-réunion est similaire à l'expérience post-réunion actuelle avec l'avantage supplémentaire d'avoir des onglets qui existent dans la surface.

✔ utilisateurs autorisés peuvent ajouter des applications de la galerie d'onglets à une réunion à l'aide de l'onglet **Détails** du formulaire de planification Teams et de l'onglet **Conversation** de réunion dans une réunion existante.

✔ la disposition des onglets doit être organisée lorsqu'il y a plus de dix sondages ou enquêtes.

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Intégrer des bots dans le cycle de vie de la réunion

Pour l'implémentation du bot, commencez [par créer un bot,](../build-your-first-app/build-bot.md) puis continuez à créer [des applications pour les réunions Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>Intégrer des extensions de messagerie dans le cycle de vie de la réunion

Pour l'implémentation de l'extension de messagerie, commencez par créer une [extension](../messaging-extensions/how-to/create-messaging-extension.md) de messagerie, puis continuez avec la création d'applications [pour les réunions Teams.](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)

## <a name="participant-roles-and-user-types-in-a-meeting"></a>Rôles des participants et types d'utilisateurs dans une réunion

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>Rôles des participants

Les paramètres de participant par défaut sont déterminés par l'administrateur informatique d'une organisation. Les rôles des participants à une réunion sont les suivants :

* **Organisateur**: l'organisateur prévoit une réunion, définit les options de la réunion, attribue des rôles de réunion et démarre la réunion. Seuls les utilisateurs ayant un compte M365 avec une licence Teams peuvent être organisateurs et contrôler les autorisations des participants. Un organisateur de réunion peut modifier les paramètres d'une réunion spécifique. Les organisateurs peuvent apporter ces modifications sur la page web **Des options de** réunion.
* **Présentateur**: les présentateurs ont les mêmes fonctionnalités que l'organisateur. Toutefois, un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de réunion pour la session. Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.
* **Participant**: un participant est un utilisateur qui a été invité à participer à une réunion, mais qui n'est pas autorisé à agir en tant que présentateur. Les participants peuvent interagir avec d'autres membres de la réunion, mais ne peuvent pas gérer les paramètres de la réunion ou partager du contenu.

Seul un organisateur ou un présentateur peut ajouter, supprimer ou désinstaller des applications. Seul l'organisateur ou le présentateur peut créer des sondages dans une réunion.

Pour plus d'informations, voir [les rôles dans une réunion Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

Vous pouvez accéder à la page  **Options de** réunion comme suit :

* Dans Teams,  allez au ![ logo ](../assets/images/apps-in-meetings/calendar-logo.png) calendrier, sélectionnez une réunion, puis les **options de réunion.**

* Dans une invitation à une réunion, sélectionnez **Les options de réunion.**

* Au cours d'une réunion, **sélectionnez Afficher les participants** ![ et afficher l'icône des participants ](../assets/images/apps-in-meetings/show-participants.png) dans les contrôles de réunion. Ensuite, au-dessus de la liste des participants, choisissez **Gérer les autorisations.**

### <a name="user-types"></a>Types d'utilisateur

> [!NOTE]
> Les utilisateurs avec des types d'utilisateurs spécifiques qui leur sont affectés peuvent participer à des réunions et assumer l'un des rôles de participant décrits dans [les rôles de participant.](#participant-roles) Le type d'utilisateur n'est pas inclus dans **l'API getParticipantRole.**

Les types d'utilisateurs suivants identifient ce que chaque utilisateur peut faire et ce à quoi il peut accéder :

* **Dans le client :** les utilisateurs dans le client appartiennent à l'organisation et ont des informations d'identification dans Azure Active Directory (AAD) pour le client. Il s'agit généralement d'employés à plein temps, sur site ou distants. Un utilisateur dans le client peut être organisateur, présentateur ou participant.
* **Invité**: un invité est un participant d'une autre organisation invité à accéder à Teams ou à d'autres ressources dans le client de l'organisation. Les invités sont ajoutés au AAD de votre organisation et ont les mêmes fonctionnalités Teams qu'un membre natif de l'équipe ayant accès aux conversations, réunions et fichiers de l'équipe. Un utilisateur invité peut être organisateur, présentateur ou participant. Pour plus d'informations, voir [l'accès invité dans Teams.](/microsoftteams/guest-access)
* **Fédéré ou externe**: un utilisateur fédéré est un utilisateur Teams externe dans une autre organisation qui a été invité à participer à une réunion. Ces utilisateurs ont des informations d'identification valides avec des partenaires fédérés et sont autorisés par Teams. Ils n'ont pas accès à vos équipes ou à d'autres ressources partagées de votre organisation. L'accès invité est une meilleure option pour les utilisateurs externes qui ont accès aux équipes et aux canaux. Pour plus d'informations, voir [gérer l'accès externe dans Teams.](/microsoftteams/manage-external-access)
* **Anonyme**: les utilisateurs anonymes n'ont pas d'identité AAD et ne sont pas fédérés avec un client. Le participant anonyme est comme un utilisateur externe, mais son identité n'est pas projetée dans la réunion. Un utilisateur anonyme ne peut pas être un organisateur, mais peut être présentateur ou participant.

> [!NOTE]
> Les utilisateurs anonymes héritent de la stratégie d'autorisation d'application globale au niveau de l'utilisateur par défaut. Pour plus d'informations, voir [Gérer les applications.](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)

Le tableau suivant fournit les types d'utilisateurs et les fonctionnalités accessibles à chaque utilisateur :

| Type d'utilisateur | Onglets | Bots | Extensions de messagerie | Cartes adaptatives | Modules de tâche | Boîtes de dialogue en réunion |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Utilisateur anonyme | Non disponible | Non disponible | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir d'une carte adaptative sont autorisées. | Non disponible |
| Invité qui fait partie du client AAD | L'interaction est autorisée. La création, la mise à jour et la suppression ne sont pas autorisées. | Non disponible | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir d'une carte adaptative sont autorisées. | Available |
| Fédéré | Non disponible | Non disponible | Non disponible | Non disponible | Non disponible | Non disponible |

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Tab](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [Bot](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [Extension de la messagerie](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [Concevoir votre application](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Créer votre application](create-apps-for-teams-meetings.md)
