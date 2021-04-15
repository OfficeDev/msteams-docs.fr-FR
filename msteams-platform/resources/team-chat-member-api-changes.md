---
title: Modifications de l’API du bot pour les membres de l’équipe et de la conversation
author: ojasvichoudhary
description: Décrit les modifications à venir et en cours apportées aux API bot utilisées pour récupérer les membres des équipes et des conversations
keywords: liste des membres de l'équipe de l'infrastructure de bot
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 38ccdd1d3052e906ceacaa47fa0cd14a1be7a41d
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696519"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Modifications apportées à l'API du bot Teams pour récupérer des membres d'équipe ou de conversation

>[!NOTE]
> Le processus d'annulation et `TeamsInfo.getMembers` les `TeamsInfo.GetMembersAsync` API ont démarré. Initialement, ils sont fortement limitées à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe. Ainsi, la liste complète n'est pas renvoyée à mesure que la taille de l'équipe augmente.
> Vous devez mettre à jour vers la version 4.10 ou une version supérieure du SDK Bot Framework et basculer vers les points de terminaison de l'API paginée ou l'API utilisateur `TeamsInfo.GetMemberAsync` unique. Cela s'applique également à votre bot même si vous n'utilisez pas directement ces API, car les anciens SDK appellent ces API pendant les événements [MembersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Pour afficher la liste des modifications à venir, consultez [les modifications apportées aux API.](team-chat-member-api-changes.md#api-changes) 

Actuellement, les développeurs de bots qui souhaitent récupérer des informations pour un ou plusieurs membres d'une conversation ou d'une équipe utilisent les API de bot Microsoft Teams pour C# ou pour les API TypeScript ou `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` Node.js. Pour plus d'informations, voir [récupérer la liste ou le profil utilisateur.](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile) Ces API ont plusieurs défauts.

Actuellement, si vous souhaitez récupérer des informations pour un ou plusieurs membres d'une conversation ou d'une équipe, vous pouvez utiliser les API de [bot Microsoft Teams](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) pour C# ou pour les API TypeScript ou `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` Node.js. Ces API ont les défauts suivants :

* Pour les grandes équipes, les performances sont médiocres et les délai d'avance sont plus probables : la taille maximale de l'équipe a considérablement augmenté depuis la publication de Teams début 2017. À mesure que vous renvoyez l'intégralité de la liste des membres, le retour de l'appel d'API pour les grandes équipes prend beaucoup de temps, et il est courant pour l'appel d'avoir un délai d'attente et vous devez essayer à `GetMembersAsync` `getMembers` nouveau.
* Il est difficile d'obtenir les détails du profil d'un seul utilisateur : pour obtenir les informations de profil d'un seul utilisateur, vous devez récupérer l'intégralité de la liste des membres, puis rechercher celle que vous souhaitez. Il existe une fonction d'aide dans le SDK Bot Framework pour la simplifier, mais elle n'est pas efficace.

Avec l'introduction des équipes à l'échelle de l'organisation, il est nécessaire de mieux aligner ces API avec les contrôles de confidentialité Office 365. Les bots utilisés dans les grandes équipes peuvent récupérer des informations de profil de base semblables à `User.ReadBasic.All` l'autorisation Microsoft Graph. Les administrateurs client contrôlent de manière très grande les applications et les robots qui peuvent être utilisés dans leur client, mais ces paramètres sont différents de Ceux de Microsoft Graph.

Le code suivant fournit un exemple de représentation JSON de ce qui est renvoyé par les API de bot Teams :

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

## <a name="api-changes"></a>Modifications apportées aux API

Voici les modifications à venir apportées aux API :

* Une nouvelle API est créée pour récupérer les informations de profil pour les [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) membres d'une conversation ou d'une équipe. Cette API est désormais disponible avec le SDK Bot Framework 4.8. Pour le développement dans toutes les autres versions, utilisez la [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) méthode.

    > [!NOTE]
    > Dans la version v3 ou v4, la meilleure action consiste à mettre à niveau vers la dernière version de point 3.30.2 ou 4.8, respectivement.

* Une nouvelle API est créée pour récupérer les informations de [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) profil d'un seul utilisateur. Elle prend l'ID de l'équipe ou de la conversation, ainsi qu'un [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) , l'ID d'objet Azure Active Directory ou l'ID utilisateur Teams comme paramètres et renvoie les informations de profil de cet `userPrincipalName` `objectId` `id` utilisateur.

    > [!NOTE]
    > `objectId` est modifié pour `aadObjectId` correspondre à ce qui est appelé dans `Activity` l'objet d'un message Bot Framework. La nouvelle API est disponible avec la version 4.8 du SDK Bot Framework. Il est également disponible dans l'extension du SDK Teams Bot Framework 3.x. En attendant, vous pouvez utiliser le point de terminaison [REST.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` dans C# et `TeamsInfo.getMembers` dans TypeScript ou Node.js est officiellement supprimé. Une fois la nouvelle API disponible, vous devez mettre à jour vos bots pour l'utiliser. Cela s'applique également à [l'API REST sous-jacente que ces API utilisent.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)
* Fin 2021, les bots ne peuvent pas récupérer de manière proactive les propriétés des membres `userPrincipalName` `email` d'une conversation ou d'une équipe. Les bots doivent utiliser Graph pour les récupérer. Les `userPrincipalName` `email` propriétés et les propriétés ne sont pas renvoyées à partir de la nouvelle `GetConversationPagedMembers` API à partir de la fin 2021. Les bots doivent utiliser Graph avec un jeton d'accès pour récupérer des informations. Il doit être plus facile pour les bots d'obtenir un jeton d'accès et de rationaliser et simplifier le processus de consentement de l'utilisateur final.
