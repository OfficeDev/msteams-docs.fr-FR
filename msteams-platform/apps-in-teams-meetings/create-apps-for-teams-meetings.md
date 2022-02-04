---
title: Conditions préalables et références d’API pour les applications dans les réunions Teams
author: surbhigupta
description: Identifier les conditions préalables avec les applications pour Teams réunions
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 4c42a66f7891691b8c53d61d1ce637d57048eae8
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2022
ms.locfileid: "62362738"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Conditions préalables et références d’API pour les applications dans les réunions Teams

Les applications pour Teams réunions, vous pouvez développer les fonctionnalités de vos applications tout au long du cycle de vie des réunions. Avant de travailler avec des applications pour Teams réunions, vous devez remplir les conditions préalables suivantes :

* Savoir comment développer des Teams applications. Pour plus d’informations sur le développement d’Teams’application, voir [Teams développement d’applications](../overview.md).

* Mettez à jour Teams manifeste de l’application pour indiquer que l’application est disponible pour les réunions. Pour plus d’informations, voir [le manifeste de l’application](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).

* Utilisez votre application qui prend en charge les onglets configurables dans l’étendue groupchat. Pour plus d’informations, voir [étendue de conversation de groupe](../resources/schema/manifest-schema.md#configurabletabs) et [créer un onglet de groupe](../build-your-first-app/build-channel-tab.md).

* Respectez les recommandations Teams la conception d’onglets pour les scénarios préalables et post-réunion. Pour les expériences pendant les réunions, reportez-vous aux recommandations en matière de conception de l’onglet réunion et de la boîte de dialogue en réunion. Pour plus d’informations, [voir Teams recommandations](../tabs/design/tabs.md) en matière de conception d’onglets[,](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) les recommandations en matière de conception d’onglets en réunion et les instructions de conception de boîte [de dialogue en réunion](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

* Prendre en charge l’étendue `groupchat` pour activer votre application dans les conversations préalables à la réunion et post-réunion. Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer les tâches préalables à la réunion. Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats ou les frais d’enquête.
* Les paramètres d’URL de l’API de réunion doivent `meetingId`avoir , `userId`et `tenantId`. Les paramètres sont disponibles dans le cadre de l’activité Teams Client SDK et bot. En outre, vous pouvez récupérer des informations fiables pour l’ID d’utilisateur et l’ID client à l’aide de l’authentification [sso onglet](../tabs/how-to/authentication/auth-aad-sso.md).

* L’API `GetParticipant` doit avoir un ID et une inscription de bot pour générer des jetons d’th. Pour plus d’informations, voir [l’inscription et l’ID du bot](../build-your-first-app/build-bot.md).

* Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue en réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue de réunion, voir paramètre d’achèvement `bot Id` dans l’API `NotificationSignal` .

* L’API `Meeting Details` doit avoir un enregistrement de bot et un ID de bot. Il nécessite le SDK bot pour obtenir `TurnContext`. Pour utiliser l’API Détails de la réunion, vous devez obtenir différentes autorisations RSC en fonction de l’étendue d’une réunion, telle qu’une réunion privée ou une réunion de canal.

* Pour les événements de réunion en temps réel, vous devez `TurnContext` connaître l’objet disponible via le Bot SDK. L’objet `Activity` dans `TurnContext` contient la charge utile avec l’heure de début et de fin réelle. Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la Teams web. Le bot peut recevoir automatiquement l’événement de début ou de fin de réunion en ajoutant dans `ChannelMeeting.ReadBasic.Group` le manifeste.

* Avoir des paramètres `meetingId`et `userId`dans l’URL `tenantId` de l’API de réunion. Les paramètres sont disponibles dans le cadre de l’activité Teams Client SDK et bot. En outre, vous pouvez récupérer des informations fiables pour l’ID d’utilisateur et l’ID client à l’aide de l’authentification [sso onglet](../tabs/how-to/authentication/auth-aad-sso.md).

* Avoir un ID et une inscription de bot dans l’API `GetParticipant` pour générer des jetons d’th. Pour plus d’informations, voir [l’inscription et l’ID du bot](../build-your-first-app/build-bot.md).

* Maintenez votre application à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue en réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue de réunion, vérifiez le paramètre d’achèvement `bot Id` dans l’API `NotificationSignal` .

* Avoir un enregistrement de bot et un ID de bot dans l’API `MeetingDetails` . Il nécessite le SDK bot pour obtenir `TurnContext`.

* Familiarisez-vous avec `TurnContext` l’objet disponible via le Bot SDK. L’objet `Activity` dans `TurnContext` contient la charge utile avec l’heure de début et de fin réelle. Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la Teams web.

Une fois que vous avez passé en compte les conditions préalables, vous pouvez utiliser les références `GetUserContext``GetParticipant`d’API d’applications de réunion , et `NotificationSignal``Meeting Details` qui vous permettent d’accéder aux informations à l’aide d’attributs et d’afficher le contenu pertinent.

> [!NOTE]
> Teams SDK JavaScript (_version_ 1.10 et ultérieure) pour que l’sso fonctionne dans le panneau latéral de réunion.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Activer et configurer vos applications pour Teams réunions](enable-and-configure-your-app-for-teams-meetings.md)

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour les réunions Teams](teams-apps-in-meetings.md)
* [Teams’API du bot pour récupérer des membres d’équipe ou de conversation](~/resources/team-chat-member-api-changes.md)
