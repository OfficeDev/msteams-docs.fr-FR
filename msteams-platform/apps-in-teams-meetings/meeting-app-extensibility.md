---
title: Applications de réunions unifiées
author: surbhigupta
description: Comprendre les applications de réunions unifiées
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 45633546825a54ed4d2adffbb60f459f26efe1c6
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475621"
---
# <a name="unified-meetings-apps"></a>Applications de réunions unifiées

Teams applications de réunions unifiées sont basées sur les concepts suivants :

* Le cycle de vie des réunions se produit selon différentes étapes : avant la réunion, en réunion et après la réunion.  
* Il existe trois rôles de participant distincts dans une réunion : organisateur, présentateur et participant. Pour plus d’informations, voir [les rôles dans une Teams réunion.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)  
* Il existe différents [types d’utilisateurs](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) dans une réunion : utilisateurs en [client,](/microsoftteams/guest-access)invités, [fédérés](/microsoftteams/manage-external-access)et anonymes.

> [!VIDEO https://www.youtube-nocookie.com/embed/rrNpFJbxqrg]

Cet article traite des informations sur le cycle de vie des réunions et sur la façon d’intégrer des onglets, des bots et des extensions de messagerie. Il identifie différents rôles de participant et types d’utilisateurs.

## <a name="meeting-lifecycle"></a>Cycle de vie des réunions

Un cycle de vie de réunion se compose de l’expérience de l’application avant, en réunion et après la réunion. Vous pouvez intégrer des onglets, des bots et des extensions de messagerie à chaque étape du cycle de vie de la réunion.

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>Intégrer des onglets dans le cycle de vie de la réunion

Les onglets permettent aux membres de l’équipe d’accéder aux services et au contenu dans un espace spécifique au sein d’une réunion. L’équipe travaille directement avec les onglets et a des conversations sur les outils et les données disponibles dans les onglets. Dans Teams réunion, vous pouvez ajouter un onglet en sélectionnant <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>et sélectionnez l’application que vous souhaitez installer.

> [!IMPORTANT]
> Si vous avez intégré un onglet à votre réunion, votre application doit suivre le flux d’authentification unique Teams [(SSO) pour les onglets.](../tabs/how-to/authentication/auth-aad-sso.md)

> [!NOTE]
> * Les réunions privées programmées ne permettent que la prise en charge des applications.
> * L’option Ajouter une application pour Teams’onglet d’extension de réunion n’est pas prise en charge Teams client web.

#### <a name="pre-meeting-app-experience"></a>Expérience d’application avant la réunion

Avec l’expérience d’application préalable à la réunion, vous pouvez trouver et ajouter des applications de réunion. Vous pouvez également effectuer des tâches préalables à la réunion, telles que le développement d’un sondage pour sondé les participants à la réunion.

**Pour ajouter des onglets à une réunion existante**

1. Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.
1. Sélectionnez **l’onglet Détails** et sélectionnez <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. La galerie d’onglets s’affiche.

    <img src="../assets/images/apps-in-meetings/PreMeeting.png" alt="Pre-meeting experience" width="900"/>

1. Dans la galerie d’onglets, sélectionnez l’application à ajouter et suivez les étapes nécessaires. L’application est installée en tant qu’onglet.

   > [!NOTE]
   > * Vous pouvez également ajouter un onglet à une réunion existante à l’aide de l’onglet **Conversation de** réunion.
   > * La disposition des onglets doit être organisée, s’il y a plus de 10 sondages ou enquêtes.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Affichage de l’onglet avant la réunion](../assets/images/apps-in-meetings/PreMeetingTab.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

Après avoir ajouté les onglets à une réunion existante sur mobile, vous pouvez voir les mêmes applications dans l’expérience de pré-réunion sous la section **Plus** des détails de la réunion.

<img src="../assets/images/apps-in-meetings/mobilepremeeting.png" alt="Mobile pre-meeting experience" width="200"/>  

---

#### <a name="in-meeting-app-experience"></a>Expérience d’application en réunion

Grâce à l’expérience d’application en réunion, vous pouvez impliquer des participants pendant la réunion à l’aide d’applications et de la boîte de dialogue de réunion. Les applications de réunion sont hébergées dans la barre d’outils de la fenêtre de réunion en tant qu’onglet de réunion. Utilisez la boîte de dialogue de réunion pour présenter le contenu actionnable aux participants à la réunion. Pour plus d’informations, voir [créer des applications pour Teams réunions.](create-apps-for-teams-meetings.md)

Pour les appareils mobiles, les applications de réunion sont disponibles à partir **>** les &#x25CF;&#x25CF;&#x25CF; de la réunion. Sélectionnez **Applications** pour afficher toutes les applications disponibles dans la réunion.

**Pour utiliser des onglets pendant une réunion**

1. Go to Teams.
1. Dans votre calendrier, sélectionnez une réunion dans laquelle vous souhaitez utiliser un onglet.
1. Après avoir entré la réunion, dans la barre d’outils de la fenêtre de conversation, sélectionnez l’application requise.
    Une application est visible dans une Teams dans le panneau latéral ou dans la boîte de dialogue de la réunion.
1. Dans la boîte de dialogue de réunion, entrez votre réponse en tant que commentaire.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Affichage boîte de dialogue](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

Une fois entrée dans la réunion et ajouté l’application à partir du bureau ou du web, l’application est visible dans la Teams sous la section **Applications.** Sélectionnez **Applications** pour afficher la liste des applications. L’utilisateur peut lancer n’importe quelle application en tant que panneau latéral en réunion de l’application.

La boîte de dialogue de réunion s’affiche et vous permet d’entrer votre réponse en tant que commentaire.

<img src="../assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt="Mobile dialog box view" width="200"/>

> [!NOTE]
> Vous n’avez pas besoin de modifier le manifeste de l’application pour que les applications fonctionnent sur un appareil mobile.

---

> [!NOTE]
> * Les applications peuvent tirer parti Teams SDK client pour accéder au , et pour `meetingId` `userMri` restituer `frameContext` l’expérience de manière appropriée.
> * Si la boîte de dialogue de réunion s’est correctement restituer, elle envoie une notification de téléchargement des résultats.
> * Le manifeste de l’application utilise le champ de contexte et spécifie les endroits où l’utilisateur souhaite que les applications apparaissent. En outre, fait partie d’une expérience de partage de bacs, comme mentionné dans les instructions de conception spécifiées.

L’image suivante illustre le panneau latéral de la réunion :

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Panneau latéral en réunion](../assets/images/apps-in-meetings/in-meeting-dialog.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

<img src="../assets/images/apps-in-meetings/sidepanelmobile.png" alt="In-meeting side panel mobile" width="300"/>

---

Le tableau suivant décrit le comportement de l’application lorsqu’elle est approuvée et non approuvée :

|Fonctionnalité d’application | L’application est approuvée | L’application n’est pas approuvée |
|---|---|---|
| Extensibilité de réunion | L’application s’affiche dans les réunions. | L’application n’apparaîtra pas dans les réunions pour les clients mobiles. |

#### <a name="post-meeting-app-experience"></a>Expérience d’application post-réunion

Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats des sondages ou les commentaires. Sélectionner <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> pour ajouter un onglet, obtenir des notes de réunion et voir les résultats sur lesquels les organisateurs et les participants doivent agir.

L’image suivante affiche l’onglet **Contoso** avec les résultats du sondage et les commentaires reçus des participants à la réunion :

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Affichage après la réunion](../assets/images/apps-in-meetings/PostMeeting.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

<img src="../assets/images/apps-in-meetings/mobilePostMeeting.png" alt="Mobile post meeting view" width="200"/>

---

> [!NOTE]
> La disposition des onglets doit être organisée lorsqu’il y a plus de 10 sondages ou enquêtes.

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>Intégrer des bots dans le cycle de vie de la réunion

Les bots activés dans l’étendue groupchat commencent à fonctionner dans les réunions. Pour implémenter des bots, commencez par [créer un bot,](../build-your-first-app/build-bot.md) puis continuez à créer des [applications pour Teams réunions.](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>Intégrer des extensions de messagerie dans le cycle de vie de la réunion

Pour implémenter l’extension de messagerie, commencez par créer une [extension](../messaging-extensions/how-to/create-messaging-extension.md) de messagerie, puis continuez à créer des applications pour [Teams réunions.](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)

Les Teams réunions unifiées vous permettent de concevoir votre application en fonction des rôles des participants à une réunion.

## <a name="participant-roles-in-a-meeting"></a>Rôles des participants dans une réunion

![Participants à une réunion](../assets/images/apps-in-meetings/participant-roles.png)

Les paramètres de participant par défaut sont déterminés par l’administrateur informatique d’une organisation. Les rôles des participants à une réunion sont les suivants :

* **Organisateur**: l’organisateur prévoit une réunion, définit les options de la réunion, attribue des rôles de réunion et démarre la réunion. Les utilisateurs ayant Microsoft 365 et une licence Teams ne peuvent être que les organisateurs et contrôler les autorisations des participants. Un organisateur de réunion peut modifier les paramètres d’une réunion spécifique. Les organisateurs peuvent apporter ces modifications sur la page web **Des options de** réunion.
* **Présentateur**: les présentateurs ont les mêmes fonctionnalités que les organisateurs avec des exclusions. Un présentateur ne peut pas supprimer un organisateur de la session ou modifier les options de réunion pour la session. Par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.
* **Participant**: un participant est un utilisateur qui a été invité à participer à une réunion. Toutefois, les participants ne sont pas autorisés à agir en tant que présentateur. Les participants peuvent interagir avec d’autres membres de la réunion, mais ne peuvent pas gérer les paramètres de la réunion ni partager le contenu.

> [!NOTE]
> Seul un organisateur ou un présentateur peut ajouter, supprimer ou désinstaller des applications.

Pour plus d’informations, [voir les rôles dans une Teams réunion.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

Après avoir conçu votre application en fonction des rôles des participants à une réunion, vous pouvez identifier chaque type d’utilisateur pour les réunions et sélectionner ce à quoi ils peuvent accéder.

## <a name="user-types-in-a-meeting"></a>Types d’utilisateurs dans une réunion

Les types d’utilisateurs, tels que l’organisateur, le présentateur ou le participant à une réunion, peuvent jouer l’un des rôles [de participant à une réunion.](#participant-roles-in-a-meeting)

> [!NOTE]
> Le type d’utilisateur n’est pas inclus dans **l’API getParticipantRole.**

La liste suivante détaille les différents types d’utilisateurs, ainsi que leur accessibilité et leurs performances :

* **Dans le client :** les utilisateurs dans le client appartiennent à l’organisation et ont des informations d’identification Azure Active Directory (AAD) pour le client. Ce sont des employés à plein temps, sur site ou distants. Un utilisateur dans le client peut être organisateur, présentateur ou participant.
* **Invité**: un invité est un participant d’une autre organisation invité à accéder Teams ou d’autres ressources dans le client de l’organisation. Les invités sont ajoutés au AAD de l’organisation et ont les mêmes fonctionnalités Teams en tant que membre d’équipe natif. Ils ont accès aux conversations d’équipe, aux réunions et aux fichiers. Un invité peut être organisateur, présentateur ou participant. Pour plus d’informations, [voir l’accès](/microsoftteams/guest-access)invité dans Teams .
* **Fédéré ou externe**: un utilisateur fédéré est un utilisateur Teams d’une autre organisation qui a été invité à participer à une réunion. Les utilisateurs fédérés ont des informations d’identification valides avec des partenaires fédérés et sont autorisés par Teams. Ils n’ont pas accès à vos équipes ou à d’autres ressources partagées de votre organisation. L’accès invité est une meilleure option pour les utilisateurs externes qui ont accès aux équipes et aux canaux. Pour plus d’informations, [voir gérer l’accès externe dans Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Vos Teams peuvent ajouter des applications lorsqu’ils hébergent des réunions ou des conversations avec d’autres organisations. Les utilisateurs peuvent utiliser des applications partagées par des utilisateurs externes lorsque vos utilisateurs rejoignent des réunions ou des conversations hébergées par d’autres organisations. Les stratégies de données de l’organisation de l’utilisateur hôte, ainsi que les pratiques de partage de données des applications tierces partagées par l’organisation de cet utilisateur, seront en vigueur.

    > [!IMPORTANT]
    > Actuellement, les applications tierces sont disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais ne sont pas disponibles pour GCC-High et le Département de la Défense (DOD). Les applications tierces sont désactivées par défaut pour les Cloud de la communauté du secteur public. Pour activer les applications tierces pour Cloud de la communauté du secteur public, voir gérer les stratégies [d’autorisation](/microsoftteams/teams-app-permission-policies) d’application et [gérer les applications.](/microsoftteams/manage-apps)

* **Anonyme**: les utilisateurs anonymes n’ont pas d’identité AAD et ne sont pas fédérés avec un client. Les participants anonymes sont comme des utilisateurs externes, mais leur identité n’est pas affichée dans la réunion. Les utilisateurs anonymes ne peuvent pas accéder aux applications dans une fenêtre de réunion. Un utilisateur anonyme ne peut pas être un organisateur, mais peut être présentateur ou participant.

    > [!NOTE]
    > Les utilisateurs anonymes héritent de la stratégie d’autorisation d’application globale au niveau de l’utilisateur par défaut. Pour plus d’informations, voir [gérer les applications.](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)

Un invité ou un utilisateur anonyme ne peut pas ajouter, supprimer ou désinstaller des applications.

Le tableau suivant fournit les types d’utilisateur et répertorie les fonctionnalités accessibles à chaque utilisateur :

| Type d’utilisateur | Onglets | Bots | Extensions de messagerie | Cartes adaptatives | Modules de tâche | Boîtes de dialogue en réunion | Étape de la réunion | 
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Utilisateur anonyme | Non disponible | Non disponible | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir d’une carte adaptative sont autorisées. | Non disponible | Impossible d’afficher, mais peut interagir avec l’application lors de la phase de réunion |
| Invité qui fait partie du client AAD | L’interaction est autorisée. La création, la mise à jour et la suppression ne sont pas autorisées. | Non disponible | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir d’une carte adaptative sont autorisées. | Disponible | Peut afficher et interagir avec l’application sur la phase de réunion |
| Utilisateur fédéré. Pour plus d’informations, voir [utilisateurs non standard.](/microsoftteams/non-standard-users) | L’interaction est autorisée. La création, la mise à jour et la suppression ne sont pas autorisées. | L’interaction est autorisée. L’acquisition, la mise à jour et la suppression ne sont pas autorisées. | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir d’une carte adaptative sont autorisées. | Non disponible | Peut afficher et interagir avec l’application sur la phase de réunion |

## <a name="see-also"></a>Voir aussi

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [Bot](../bots/what-are-bots.md)
* [Extension de la messagerie](../messaging-extensions/what-are-messaging-extensions.md)
* [Concevoir votre application](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conditions préalables et références d’API pour les applications dans les réunions Teams](create-apps-for-teams-meetings.md)
