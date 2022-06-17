---
title: Modifications de l’API du bot pour les membres de l’équipe et de la conversation
author: ojasvichoudhary
description: Dans ce module, découvrez les modifications à venir et en cours des API bot utilisées pour récupérer les membres des équipes et des conversations
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 5f5bb009abd5a9e0dc8a14d0bea5bdd0f43a71c9
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142324"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Modifications apportées à l’API du bot Teams pour récupérer les membres d’équipe ou de conversation

>[!NOTE]
> Le processus de dépréciation de `TeamsInfo.getMembers` et `TeamsInfo.GetMembersAsync` API a démarré. Initialement, ils sont fortement limités à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe. La liste complète n’est donc pas retournée à mesure que la taille de l’équipe augmente.
> Vous devez effectuer une mise à jour vers la version 4.10 ou ultérieure du SDK Bot Framework et basculer vers les points de terminaison d’API paginés, ou la classe `TeamsInfo.GetMemberAsync`'API mono-utilisateur. Cela s’applique également à votre bot même si vous n’utilisez pas directement ces API, car les SDK plus anciens appellent ces API pendant événements [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#members-added). Pour afficher la liste des modifications à venir, consultez [modifications de l’API](team-chat-member-api-changes.md#api-changes).

Actuellement, si vous souhaitez récupérer des informations pour un ou plusieurs membres d’une conversation ou d’une équipe, vous pouvez utiliser les API de bot [Microsoft Teams](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` pour C# ou `TeamsInfo.getMembers` pour les API TypeScript ou Node.js. Pour plus d’informations, consultez [récupérer la liste ou le profil utilisateur](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).

Ces API présentent les inconvénients suivants :

* Pour les grandes équipes, les performances sont médiocres et les délais d’attente sont plus probables : la taille maximale de l’équipe a considérablement augmenté depuis la publication de Teams début 2017. En tant que `GetMembersAsync` liste de membres entière ou `getMembers` en retourne, l’appel d’API prend beaucoup de temps à revenir pour les grandes équipes, et il est courant que l’appel expire et que vous devez réessayer.
* L’obtention des détails du profil pour un seul utilisateur est difficile : pour obtenir les informations de profil d’un seul utilisateur, vous devez récupérer la liste des membres entière, puis rechercher celle souhaitée. Il existe une fonction d’assistance dans le Kit de développement logiciel (SDK) Bot Framework pour la simplifier, mais elle n’est pas efficace.

Avec l’introduction d’équipes à l’échelle de l’organisation, il est nécessaire de mieux aligner ces API sur Office 365 contrôles de confidentialité. Les bots utilisés dans les grandes équipes peuvent récupérer des informations de profil de base similaires à l’autorisation `User.ReadBasic.All` Microsoft Graph. Les administrateurs clients ont un grand contrôle sur les applications et les bots qui peuvent être utilisés dans leur locataire, mais ces paramètres sont différents de Microsoft Graph.

Le code suivant fournit un exemple de représentation JSON de ce qui est retourné par les API de bot Teams :

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "anonymous"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}]
```

## <a name="api-changes"></a>Modifications de l’API

Voici les modifications à venir de l’API :

* Une nouvelle API est créée [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) pour récupérer les informations de profil des membres d'un chat ou d'une équipe. Cette API est désormais disponible avec le SDK Bot Framework version 4.8 ou ultérieure. Pour le développement dans toutes les autres versions, utilisez la méthode [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true).

    > [!NOTE]
    > Dans v3 ou v4, la meilleure action consiste à effectuer une mise à niveau vers la dernière version de point, 3.30.2 ou 4.8 ou ultérieure, respectivement.

* Une nouvelle API est créée [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) pour récupérer les informations de profil pour un seul utilisateur. Il prend l'ID de l'équipe ou du chat et un [UPN](/windows/win32/ad/naming-properties#userprincipalname) qui est `userPrincipalName`, Microsoft Azure Active Directory (Azure AD) Object ID `objectId`, ou l'ID de l'utilisateur Teams `id` comme paramètres et renvoie les informations de profil pour cet utilisateur.

    > [!NOTE]
    > `objectId` est remplacé par `aadObjectId` pour correspondre à ce qui est appelé dans l’objet `Activity` d’un message Bot Framework. La nouvelle API est disponible avec la version 4.8 ou ultérieure du SDK Bot Framework. Il est également disponible dans l’extension du Kit de développement logiciel (SDK) Teams Bot Framework 3.x. Pendant ce temps, vous pouvez utiliser le point de terminaison [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details).

* `TeamsInfo.GetMembersAsync` en C# et `TeamsInfo.getMembers` dans TypeScript ou Node.js est formellement déconseillé. Une fois la nouvelle API disponible, vous devez mettre à jour vos bots pour l’utiliser. Cela s’applique également à la [API REST sous-jacente que ces API utilisent](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).
* Fin 2022, les bots ne peuvent pas récupérer de manière proactive les propriétés `userPrincipalName` ou `email` pour les membres d’une conversation ou d’une équipe. Les bots doivent utiliser les API Graph pour récupérer les informations requises. La nouvelle api `GetConversationPagedMembers` ne peut pas retourner les propriétés `userPrincipalName` et `email` de fin 2022. Les bots doivent utiliser API Graph avec un jeton d’accès pour récupérer des informations. 
