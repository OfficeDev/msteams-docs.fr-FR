---
title: Applications pour les réunions Teams
author: surbhigupta
description: Dans cet article, découvrez comment fonctionnent les applications dans les réunions Microsoft Teams en fonction du rôle de participant et d’utilisateur et de l’extensibilité des applications.
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: f253a4ca3d09e48f99df36fdcb77bdd740fab5ff
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772271"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Applications pour les réunions et les appels Teams

Les réunions permettent la collaboration, le partenariat, la communication éclairée et le partage de commentaires. L’espace de réunion peut fournir une expérience utilisateur pour chaque étape du cycle de vie de la réunion. L'illustration suivante vous donne une idée des caractéristiques d'extensibilité de l'application de réunion :

:::image type="content" source="../assets/images/apps-in-meetings/meetingappextensibility.png" alt-text="La capture d’écran vous montre comment fonctionne l’extensibilité de l’application de réunion.":::

Vous devez connaître les concepts de produit suivants pour créer des expériences de réunion personnalisées avec des applications dans Microsoft Teams.

## <a name="supported-meeting-types-in-teams"></a>Types de réunion pris en charge dans Teams

Teams prend en charge l’accès aux applications pendant la réunion pour les types de réunion suivants :

* [**Réunions planifiées**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop) : réunions planifiées via le calendrier Teams.
* [**Réunions de canal planifiées**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop) : réunions planifiées via les canaux publics Teams.
* [**Appels en tête-à-tête**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798) : appels lancés dans une conversation en tête-à-tête.
* [**Appels de groupe**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798) : appels lancés dans une conversation de groupe.
* [**Réunions instantanées**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5) : réunions lancées via le bouton **Répondre maintenant** dans le calendrier Teams.
* [**Webinaire**](https://support.microsoft.com/office/get-started-with-teams-webinars-42f3f874-22dc-4289-b53f-bbc1a69013e3) : Webinaire initié via le bouton **Webinaire** sous la liste déroulante **Nouvelle réunion** .

En savoir plus sur [les réunions, l’expiration et les stratégies et réunions Teams](/MicrosoftTeams/meeting-expiration)[, les webinaires et les événements en direct](/microsoftteams/quick-start-meetings-live-events).
> [!NOTE]
>
> * Les applications pour les réunions de canal public planifiées sont actuellement disponibles uniquement en [préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md).
> * Les applications ne sont pas prises en charge dans les éléments suivants :
>   * [Appels Teams RTC (Réseau téléphonique commuté public)](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options)
>   * [Appels Teams chiffrés de bout en bout](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90)
>   * [Réunions de canal instantanées](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)
>   * Réunions dans un [canal partagé](https://support.microsoft.com/office/what-is-a-shared-channel-in-teams-e70a8c22-fee4-4d6e-986f-9e0781d7d11d)

## <a name="meeting-lifecycle"></a>Cycle de vie des réunions

Un cycle de vie de réunion comprend l’expérience d’application avant la réunion, en réunion et après la réunion, en fonction du type d’utilisateur et du rôle de l’utilisateur dans une réunion Teams.

## <a name="user-types-in-teams"></a>Types d’utilisateurs dans Teams

Teams prend en charge les types d’utilisateurs, tels que les utilisateurs in-tenant, invités, fédérés ou externes dans une réunion Teams. Chaque type d’utilisateur peut avoir l’un des [rôles d’utilisateur dans la réunion Teams](#user-roles-in-teams-meeting).

> [!NOTE]
>
> Actuellement, lorsqu’une troisième personne est ajoutée à un appel en face à face, l’appel est élevé en appel de groupe, ce qui signifie qu’une nouvelle session démarre. Les applications ajoutées à l’appel en un ne sont pas disponibles dans l’appel de groupe. Toutefois, ils peuvent être ajoutés à nouveau.

La liste suivante détaille les différents types d’utilisateurs ainsi que leur accessibilité :

* **In-tenant** : les utilisateurs in-tenant appartiennent à l’organisation et ont des informations d’identification dans Azure Active Directory (AAD) pour le locataire. Ce sont des employés à temps plein, sur site ou à distance. Un utilisateur dans le locataire peut être organisateur, présentateur ou participant.
* **Invité** : un invité est un participant d’une autre organisation invité à accéder à Teams ou à d’autres ressources dans le locataire de l’organisation. Les invités sont ajoutés à Azure AD de l’organisation et ont les mêmes fonctionnalités Teams qu’un membre de l’équipe native. Ils ont accès aux conversations d’équipe, aux réunions et aux fichiers. Un invité peut être un organisateur, un présentateur ou un participant. Pour plus d’informations, consultez [Accès invité dans Teams](/microsoftteams/guest-access).
* **Fédéré ou externe** : un utilisateur fédéré ou externe est un utilisateur Teams d’une autre organisation qui a été invité à participer à une réunion. Les utilisateurs fédérés disposent d’informations d’identification valides auprès de partenaires fédérés et sont autorisés par Teams. Ils n’ont pas accès à vos ressources Teams ou à d’autres ressources partagées de votre organisation. L’accès invité est une meilleure option pour les utilisateurs externes d’avoir accès à Teams et aux canaux. Pour plus d’informations, consultez [Gérer l’accès externe dans Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Les utilisateurs de Teams peuvent ajouter des applications lorsqu’ils hébergent des réunions ou des conversations avec d’autres organisations. Lorsqu’un utilisateur externe partage des applications avec la réunion, tous les utilisateurs peuvent accéder à l’application. Les stratégies de données de l’organisation hôte et les pratiques de partage de données des applications tierces partagées par l’organisation de cet utilisateur seront appliquées.

* **Anonyme** : les utilisateurs anonymes n’ont pas d’identité Azure AD et ne sont pas fédérés avec un locataire. Les participants anonymes sont comme des utilisateurs externes, mais leur identité n’est pas affichée dans la réunion. Les utilisateurs anonymes ne peuvent pas accéder aux applications dans une fenêtre de réunion. Un utilisateur anonyme ne peut pas afficher le logo du bot dans la conversation de réunion. Un utilisateur anonyme peut être un présentateur ou un participant, mais pas un organisateur.

    > [!NOTE]
    > Les utilisateurs anonymes héritent de la stratégie d’autorisation d’application globale au niveau de l’utilisateur par défaut. Pour plus d’informations, consultez [Gérer les applications](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

## <a name="user-roles-in-teams-meeting"></a>Rôles d’utilisateur dans une réunion Teams

Voici les rôles d’utilisateur dans une réunion Teams :

* **Organisateur** : l’organisateur planifie une réunion, définit les options de réunion, attribue des rôles de réunion, contrôle les autorisations des participants et démarre la réunion. Seuls les utilisateurs disposant d’un compte Microsoft 365 et d’une licence Teams peuvent être l’organisateur. Un organisateur de réunion peut modifier les paramètres d’une réunion spécifique à partir de la [page **Options de**](https://support.microsoft.com/en-us/office/change-participant-settings-for-a-teams-meeting-53261366-dbd5-45f9-aae9-a70e6354f88e) réunion.

* **Présentateur** : les présentateurs d’une réunion ont des fonctionnalités similaires à celles de l’organisateur, à l’exception de la suppression d’un organisateur de la session et de la modification des options de réunion pour la session.

* **Participant** : un participant est un utilisateur qui est invité à participer à la réunion. Les participants ont des capacités limitées pendant la réunion.

> [!NOTE]
> Seul un organisateur ou un présentateur peut ajouter, supprimer ou désinstaller des applications.

Pour plus d’informations, consultez [Partager du contenu dans une réunion Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

> [!TIP]
>
> * Les [paramètres de participant par défaut](/microsoftteams/meeting-policies-participants-and-guests) sont déterminés par l’administrateur informatique d’une organisation.Conformément aux paramètres par défaut, les participants qui rejoignent une réunion ont le rôle de présentateur.
> * Le rôle de présentateur n’est pas disponible dans les appels en tête-à-tête.
> * Un utilisateur qui démarre l’appel de groupe à partir d’une conversation est considéré comme organisateur.

> [!IMPORTANT]
>
> * Actuellement, les applications tierces sont disponibles dans government Community Cloud (GCC), mais ne sont pas disponibles pour les locataires GCC-High et department of Defense (DOD).
> * Les applications tierces sont désactivées par défaut pour GCC. Pour activer des applications tierces pour GCC, consultez [gérer les stratégies d’autorisation d’application](/microsoftteams/teams-app-permission-policies) et [gérer les applications](/microsoftteams/manage-apps).

## <a name="see-also"></a>Voir aussi

* [Conception de votre extension de réunion Microsoft Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Onglets générer pour la réunion](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Créer des applications pour la phase de réunion Teams](build-apps-for-teams-meeting-stage.md)
* [Créer une conversation extensible pour la conversation de réunion](build-extensible-conversation-for-meeting-chat.md)
* [Créer des applications pour les utilisateurs anonymes](build-apps-for-anonymous-user.md)
* [API des applications de réunion](meeting-apps-apis.md)
* [Collaboration améliorée avec Live Share SDK](teams-live-share-overview.md)
* [Scènes personnalisées du mode ensemble](~/apps-in-teams-meetings/teams-together-mode.md)
