---
title: Conditions préalables pour les applications dans Teams réunions
author: surbhigupta
description: Identifier les conditions préalables avec les applications pour Teams réunions
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: dcfde3136d711d4049060dd59c37e818bdf1a700
ms.sourcegitcommit: 95e0c767ca0f2a51c4a7ca87700ce50b7b154b7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2021
ms.locfileid: "58528781"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Conditions préalables pour les applications dans Teams réunions

Les applications pour Teams réunions, vous pouvez développer les fonctionnalités de vos applications tout au long du cycle de vie des réunions. Avant de travailler avec des applications pour Teams réunions, vous devez remplir les conditions préalables suivantes :

* Savoir comment développer des Teams applications. Pour plus d’informations sur le développement d’Teams’application, voir [Teams développement d’applications.](../overview.md)

* Mettez à jour Teams manifeste de l’application pour indiquer que l’application est disponible pour les réunions. Pour plus d’informations, voir [le manifeste de l’application.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)

* Utilisez votre application qui prend en charge les onglets configurables dans l’étendue groupchat. Pour plus d’informations, voir [l’étendue de conversation de groupe](../resources/schema/manifest-schema.md#configurabletabs) et créer un onglet de [groupe.](../build-your-first-app/build-channel-tab.md)

* Respectez les recommandations Teams la conception d’onglets pour les scénarios préalables et post-réunion. Pour les expériences pendant les réunions, reportez-vous aux instructions de conception de l’onglet réunion et de la boîte de dialogue en réunion. Pour plus d’informations, [voir Teams recommandations](../tabs/design/tabs.md)en matière de conception d’onglets, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)de recommandations en matière de conception d’onglets en réunion et de conception de boîte de dialogue en [réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Prendre en `groupchat` charge l’étendue pour activer votre application dans les conversations préalables à la réunion et post-réunion. Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer les tâches préalables à la réunion. Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats des sondages ou les commentaires.

* Avoir des paramètres `meetingId` `userId` et dans `tenantId` l’URL de l’API de réunion. Les paramètres sont disponibles dans le cadre de l’activité Teams Client SDK et bot. En outre, vous pouvez récupérer des informations fiables pour l’ID d’utilisateur et l’ID de locataire à l’aide de l’authentification [sso tab .](../tabs/how-to/authentication/auth-aad-sso.md)

* Avoir un ID et une inscription de bot dans `GetParticipant` l’API pour générer des jetons d’th. Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)

* Maintenez votre application à jour en fonction des activités d’événements de la réunion. Ces événements peuvent se trouver dans la boîte de dialogue de réunion et dans d’autres étapes du cycle de vie de la réunion. Pour la boîte de dialogue de réunion, vérifiez le paramètre `bot Id` d’achèvement dans `NotificationSignal` l’API.

* Avoir un enregistrement de bot et un ID de bot dans `MeetingDetails` l’API. Il nécessite le SDK bot pour obtenir `TurnContext` .

* Familiarisez-vous `TurnContext` avec l’objet disponible via le Bot SDK. `Activity`L’objet dans contient la charge utile avec `TurnContext` l’heure de début et de fin réelle. Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la Teams web.

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception de boîte de dialogue en réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams d’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour Teams réunions](teams-apps-in-meetings.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Références de l’API des applications de réunion](API-references.md)
