---
title: Applications pour les réunions Teams
author: surbhigupta
description: Dans cet article, découvrez comment les applications fonctionnent dans les réunions Microsoft Teams en fonction du rôle des participants et des utilisateurs et de l’extensibilité des applications.
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 2e022ab2a39d399395a1aaf43ca6b282d24b81b7
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560532"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Applications pour les réunions et les appels Teams

Les réunions permettent la collaboration, le partenariat, la communication éclairée et le partage de commentaires. L'application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion. Le cycle de vie de la réunion comprend l'expérience de l'application avant, pendant et après la réunion, en fonction du statut du participant.

> [!NOTE]
>
> * Les applications pour les réunions de canal public planifiées sont actuellement disponibles uniquement en [préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md).
>
> * Les applications ne sont pas prises en charge dans le [réseau téléphonique commuté (RTC) public](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options) et les [appels Teams chiffrés de bout en bout](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90).

Teams prend en charge l’accès aux applications pendant la réunion pour les types de réunion suivants :

* [**Réunions planifiées**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop) : réunions planifiées via le calendrier Teams.
* [**Réunions de canal planifiées**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop) : réunions planifiées via des canaux publics Teams.
* [**Appels en tête-à-tête**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798) : appels lancés dans une conversation en tête-à-tête.
* [**Appels de groupe**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798) : appels lancés dans une conversation de groupe.
* [**Réunions instantanées**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5) : réunions initiées via le bouton **Réunion maintenant** dans le calendrier Teams.

Les utilisateurs peuvent ajouter des applications à la réunion à l’aide de l’option **+** à partir de leur fenêtre de réunion Teams.

:::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="Ajouter une application dans une réunion" border="true":::

Visitez le [magasin Teams](https://go.microsoft.com/fwlink/p/?LinkID=2183121) et explorez les applications conçues spécifiquement pour les réunions.

> [!NOTE]
>
> * Actuellement, lorsqu’une troisième personne est ajoutée à un appel un-à-un, l’appel est élevé à un appel de groupe, ce qui signifie qu’une nouvelle session démarre. Les applications ajoutées à l’appel un-à-un ne sont pas disponibles dans l’appel de groupe. Toutefois, ils peuvent être ajoutés à nouveau.
>
> * Actuellement, les expériences d’application ne sont pas prises en charge dans les réunions de canal instantané Teams.

L'illustration suivante vous donne une idée des caractéristiques d'extensibilité de l'application de réunion :

![Extensibilité de l’application de réunion](../assets/images/apps-in-meetings/meetingappextensibility.png)

Cet article fournit une vue d'ensemble de l'extensibilité des applications de réunion, des références API, de l'activation et de la configuration des applications pour les réunions et des scènes personnalisées en mode Ensemble dans Teams.

> [!NOTE]
>
> Les applications de réunion (panneau latéral, phase de réunion) sont prises en charge dans le client de bureau Teams. Là où, comme dans le client web Teams, il est pris en charge uniquement lorsque la préversion du développeur est activée.

* **Étendre l’application de réunion** : améliorez votre expérience de réunion à l’aide de la fonctionnalité d’extensibilité de réunion. Cette fonctionnalité vous permet d'intégrer vos applications dans les réunions. Il comprend également les différentes étapes du cycle de vie d'une réunion, où vous pouvez intégrer des onglets, des bots et des extensions de messages. Vous pouvez identifier divers rôles de participants et types d'utilisateurs, obtenir des événements de réunion et générer des dialogues en réunion.
* **Configurer des applications pour les réunions** : pour personnaliser Teams avec des applications pour les réunions, activez vos applications pour les réunions Teams en mettant à jour le manifeste de l’application et configurez également les applications pour les scénarios de réunion.
* **Personnaliser avec des scènes en mode ensemble** : la nouvelle fonctionnalité personnalisée de scènes en mode Ensemble permet aux utilisateurs de collaborer dans une réunion avec leur équipe au même endroit.
* **Personnaliser l’autorisation d’application dans un canal partagé** : si votre application partage des informations importantes dans un canal partagé, vous pouvez personnaliser l’autorisation d’application pour les membres externes. Les autorisations d’application dans [les canaux partagés](../concepts/build-and-test/Shared-channels.md) suivent la liste des applications de l’équipe hôte et la stratégie d’application du locataire hôte.
* **Récupérer les transcriptions de réunion** : vous pouvez accéder aux transcriptions de réunion et les récupérer dans un scénario de post-réunion. Configurez votre application pour obtenir automatiquement les transcriptions d’une réunion planifiée et utilisez-les pour obtenir des insights, une analyse intelligente, etc.
* **Générer un lien profond pour partager du contenu à mettre en scène dans les réunions** : vous pouvez générer un lien profond pour partager l’application pour effectuer une phase et démarrer ou participer à une réunion.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Applications de réunions unifiées](meeting-app-extensibility.md)

## <a name="see-also"></a>Voir aussi

* [Conception de votre extension de réunion Microsoft Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Références API des applications de réunion – Teams](~/apps-in-teams-meetings/api-references.md)
* [Scènes personnalisées du mode ensemble](~/apps-in-teams-meetings/teams-together-mode.md)
* [Activer et configurer vos applications pour les réunions Teams](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
* [Cycle de vie des réunions](meeting-app-extensibility.md#meeting-lifecycle)
* [Collaboration améliorée avec Live Share SDK](teams-live-share-overview.md)
